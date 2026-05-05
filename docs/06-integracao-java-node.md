# Integração Java (Spring Boot) e Node.js

Este documento explica exatamente como os dois backends se comunicam, compartilham autenticação e dividem responsabilidades. Leia isso antes de desenvolver qualquer funcionalidade que envolva os dois serviços.

---

## Visão geral da arquitetura

```
┌─────────────────────────────────────────────────────────┐
│                     FRONTEND (React)                      │
│                                                           │
│   HTTP REST requests          WebSocket connection        │
│   (com JWT no header)         (com JWT no handshake)      │
└──────────────┬───────────────────────────┬───────────────┘
               │                           │
               ▼                           ▼
┌──────────────────────┐       ┌──────────────────────────┐
│  SPRING BOOT :8080   │       │    NODE.JS :3001          │
│                      │       │                           │
│  - Autenticação      │       │  - Chat WebSocket         │
│  - CRUD de usuários  │       │  - Timer Pomodoro         │
│  - CRUD de livros    │       │  - Usuários online        │
│  - Sessões           │       │  - Eventos real-time      │
│  - Progresso         │       │                           │
│  - Streak            │       │  Valida JWT com o         │
│  - Emite JWT         │       │  mesmo JWT_SECRET         │
└──────────┬───────────┘       └──────────────┬────────────┘
           │                                  │
           ▼                                  ▼
┌──────────────────┐                ┌──────────────────────┐
│   POSTGRESQL     │                │        REDIS          │
│                  │                │                       │
│  Dados           │                │  Estado efêmero       │
│  permanentes     │                │  - Mensagens recentes │
│                  │                │  - Timer Pomodoro     │
│                  │                │  - Usuários online    │
└──────────────────┘                └──────────────────────┘
```

Os dois backends **não se chamam diretamente**. Eles compartilham apenas um segredo (JWT_SECRET) e, indiretamente, o Redis para dados que ambos precisam eventualmente acessar.

---

## Como a autenticação é compartilhada

### O fluxo completo de login

1. O usuário faz `POST /api/auth/login` para o **Spring Boot**
2. O Spring Boot valida as credenciais, gera um JWT e retorna ao frontend
3. O frontend armazena o token no `localStorage`
4. Nas próximas requisições REST, o frontend envia o token no header: `Authorization: Bearer <token>`
5. Nas conexões WebSocket, o frontend passa o token no handshake do Socket.IO

### Estrutura do JWT

O Spring Boot emite tokens com este payload:

```json
{
  "sub": "uuid-do-usuario",
  "name": "Kauã",
  "email": "kaua@email.com",
  "iat": 1700000000,
  "exp": 1700604800
}
```

### Como o Node.js valida o JWT

O Node.js **não chama o Spring Boot** para validar o token. Ele usa a mesma `JWT_SECRET` para verificar a assinatura localmente:

```javascript
// backend-node/src/middleware/auth.js
const jwt = require('jsonwebtoken');

function authenticateToken(socket, next) {
  const token = socket.handshake.auth.token;

  if (!token) {
    return next(new Error('Token não fornecido'));
  }

  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    socket.userId = decoded.sub;
    socket.userName = decoded.name;
    next();
  } catch (err) {
    return next(new Error('Token inválido'));
  }
}

module.exports = { authenticateToken };
```

**Regra crítica:** A variável de ambiente `JWT_SECRET` deve ser **exatamente igual** nos dois serviços. Se forem diferentes, o Node.js vai rejeitar todos os tokens emitidos pelo Spring Boot.

### Configuração da JWT_SECRET

No Railway, configure a mesma variável nos dois serviços:

```
JWT_SECRET=sua_chave_secreta_muito_longa_e_aleatoria_aqui
```

Para gerar uma chave segura localmente:

```bash
node -e "console.log(require('crypto').randomBytes(64).toString('hex'))"
```

---

## Divisão de responsabilidades detalhada

### O que o Spring Boot faz

- `POST /api/auth/register` — cadastro de usuário
- `POST /api/auth/login` — login, emissão de JWT
- `GET/POST/PUT/DELETE /api/users` — CRUD de perfil
- `GET/POST/PUT/DELETE /api/books` — CRUD da biblioteca pessoal
- `GET/POST/PUT/DELETE /api/sessions` — CRUD de sessões
- `POST /api/sessions/:id/join` — entrar em sessão
- `PUT /api/sessions/:id/progress` — atualizar progresso de leitura
- `GET /api/users/:id/streak` — buscar dados de streak e calendário
- `POST /api/streak/record` — registrar um Pomodoro concluído no banco

O Spring Boot é a fonte de verdade para **todos os dados permanentes**.

### O que o Node.js faz

- Gerencia conexões WebSocket com Socket.IO
- Autentica conexões via JWT no handshake
- Armazena mensagens recentes no Redis (últimas 50 por sessão)
- Entrega histórico de mensagens ao conectar
- Gerencia estado do timer Pomodoro no Redis
- Sincroniza Pomodoro entre abas do mesmo usuário
- Emite evento para o frontend quando Pomodoro é concluído
- Notifica participantes de uma sessão sobre mudanças (novo participante, mudança de progresso)

Quando um Pomodoro é concluído, o Node.js **chama o Spring Boot** para registrar o streak:

```javascript
// backend-node/src/services/pomodoro.js
const axios = require('axios');

async function recordPomodoroCompletion(userId, authToken) {
  try {
    await axios.post(
      `${process.env.SPRING_BOOT_URL}/api/streak/record`,
      { userId, completedAt: new Date().toISOString() },
      { headers: { Authorization: `Bearer ${authToken}` } }
    );
  } catch (error) {
    // Log do erro mas não quebra o fluxo do usuário
    console.error('Falha ao registrar streak:', error.message);
  }
}
```

Esta é a **única** chamada direta entre os dois backends no MVP.

---

## Eventos WebSocket — contrato de comunicação

O frontend conecta ao Node.js via Socket.IO. Estes são todos os eventos:

### Eventos emitidos pelo frontend (cliente → servidor)

| Evento | Payload | Descrição |
|---|---|---|
| `join_session` | `{ sessionId: string }` | Entra na sala da sessão |
| `leave_session` | `{ sessionId: string }` | Sai da sala |
| `send_message` | `{ sessionId: string, text: string }` | Envia mensagem no chat |
| `start_pomodoro` | `{ sessionId: string, duration: number }` | Inicia timer (duração em segundos) |
| `pause_pomodoro` | `{ sessionId: string }` | Pausa o timer |
| `resume_pomodoro` | `{ sessionId: string }` | Retoma o timer |
| `update_progress` | `{ sessionId: string, currentPage: number }` | Atualiza progresso (via WebSocket para todos verem em tempo real) |

### Eventos emitidos pelo servidor (servidor → cliente)

| Evento | Payload | Descrição |
|---|---|---|
| `chat_history` | `{ messages: Message[] }` | Histórico das últimas 50 mensagens (ao entrar) |
| `new_message` | `{ id, userId, userName, text, timestamp }` | Nova mensagem de outro participante |
| `user_joined` | `{ userId, userName }` | Participante entrou na sessão |
| `user_left` | `{ userId, userName }` | Participante saiu da sessão |
| `pomodoro_tick` | `{ remaining: number }` | Tick a cada segundo com tempo restante |
| `pomodoro_completed` | `{ userId }` | Pomodoro concluído — frontend mostra parabéns |
| `progress_updated` | `{ userId, userName, currentPage, percentage }` | Progresso de outro participante atualizado |
| `session_config_changed` | `{ config }` | Host alterou configurações da sessão |
| `session_ended` | `{}` | Host encerrou a sessão |

---

## Como o frontend decide qual backend chamar

Regra simples: **REST vai para o Spring Boot, WebSocket vai para o Node.js.**

```javascript
// frontend/src/config/api.js

export const SPRING_BOOT_URL = import.meta.env.VITE_API_URL;      // http://localhost:8080
export const NODE_URL = import.meta.env.VITE_REALTIME_URL;         // http://localhost:3001

// Exemplo de uso
// Buscar sessão: axios.get(`${SPRING_BOOT_URL}/api/sessions/${id}`)
// Chat: socket.emit('send_message', { sessionId, text })
```

---

## Variáveis de ambiente necessárias

### Spring Boot — `backend-java/.env` (não commitar)

```env
DATABASE_URL=jdbc:postgresql://localhost:5432/litcircle
DATABASE_USERNAME=postgres
DATABASE_PASSWORD=postgres
JWT_SECRET=mesma_chave_secreta_do_node
JWT_EXPIRATION_DAYS=7
```

### Node.js — `backend-node/.env` (não commitar)

```env
PORT=3001
REDIS_URL=redis://localhost:6379
JWT_SECRET=mesma_chave_secreta_do_java
SPRING_BOOT_URL=http://localhost:8080
```

### Frontend — `frontend/.env` (pode commitar, sem segredos)

```env
VITE_API_URL=http://localhost:8080
VITE_REALTIME_URL=http://localhost:3001
```

---

## Fluxos de exemplo end-to-end

### Fluxo: usuário entra em uma sessão e manda uma mensagem

```
1. Frontend: GET /api/sessions/LIT-X7K2  →  Spring Boot
   Resposta: dados da sessão (livro, participantes, datas)

2. Frontend: conecta ao Socket.IO  →  Node.js
   Handshake: { auth: { token: "jwt_aqui" } }
   
3. Node.js: valida JWT localmente com JWT_SECRET
   
4. Frontend: emite "join_session" { sessionId: "uuid-da-sessao" }
   
5. Node.js: busca últimas 50 mensagens no Redis
   Emite "chat_history" com as mensagens

6. Frontend: emite "send_message" { sessionId, text: "Oi!" }
   
7. Node.js: salva mensagem no Redis
   Emite "new_message" para todos na sala
   
8. Todos os outros participantes conectados recebem "new_message"
```

### Fluxo: usuário completa um Pomodoro e streak é registrado

```
1. Frontend: emite "start_pomodoro" { sessionId, duration: 1500 }

2. Node.js: armazena estado no Redis: { userId, startedAt, duration }
   Começa a emitir "pomodoro_tick" a cada segundo

3. Após 1500 segundos (25 min):
   Node.js emite "pomodoro_completed" para o usuário
   
4. Node.js: chama POST /api/streak/record no Spring Boot
   Body: { userId, completedAt: "2024-01-15T14:30:00Z" }
   Header: Authorization: Bearer <token_do_usuario>
   
5. Spring Boot: registra o evento de streak no PostgreSQL
   Retorna 201 Created
   
6. Frontend: ao receber "pomodoro_completed", busca streak atualizado
   GET /api/users/:id/streak  →  Spring Boot
   Atualiza o calendário na UI
```
