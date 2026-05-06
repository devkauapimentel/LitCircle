# Integração Java (Spring Boot) e Node.js

---

## Visão geral

```
┌─────────────────────────────────────────────────┐
│              FRONTEND (HTML/CSS/JS)             │
│                                                 │
│   fetch() REST requests     Socket.IO connection│
│   (com JWT no header)       (com JWT no auth)   │
└──────────┬──────────────────────────┬───────────┘
           │                          │
           ▼                          ▼
┌─────────────────────┐   ┌────────────────────────┐
│  SPRING BOOT :8080  │   │  NODE.JS :3001         │
│                     │   │                        │
│  - Cadastro/login   │   │  - Chat WebSocket      │
│  - Emite JWT        │   │  - Presença (online)   │
│  - CRUD sessões     │   │  - Valida JWT com      │
│  - Progresso        │   │    mesma JWT_SECRET    │
│  - Persistência     │   │                        │
└────────┬────────────┘   └────────────────────────┘
         │
         ▼
┌─────────────────┐
│   POSTGRESQL    │
└─────────────────┘
```

**Os dois backends NÃO se chamam diretamente.** Compartilham apenas a `JWT_SECRET`.

---

## Como a autenticação funciona

1. Usuário faz `POST /api/auth/login` → **Spring Boot**
2. Spring Boot valida credenciais, gera JWT, retorna ao frontend
3. Frontend salva token no `localStorage`
4. Requisições REST: token no header `Authorization: Bearer <token>`
5. Conexões WebSocket: token no handshake do Socket.IO

### Estrutura do JWT

```json
{
  "sub": "uuid-do-usuario",
  "name": "Kauã",
  "email": "kaua@email.com",
  "iat": 1700000000,
  "exp": 1700604800
}
```

### Como o Node.js valida

```javascript
const jwt = require('jsonwebtoken');

function authenticateToken(socket, next) {
  const token = socket.handshake.auth.token;
  if (!token) return next(new Error('Token não fornecido'));

  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    socket.userId = decoded.sub;
    socket.userName = decoded.name;
    next();
  } catch (err) {
    return next(new Error('Token inválido'));
  }
}
```

**Regra crítica:** `JWT_SECRET` deve ser IDÊNTICO nos dois serviços.

---

## Divisão de responsabilidades

### Spring Boot faz:
- `POST /api/auth/register` — cadastro
- `POST /api/auth/login` — login + JWT
- `POST /api/sessions` — criar sessão
- `POST /api/sessions/join` — entrar
- `GET /api/sessions` — listar
- `GET /api/sessions/:id` — detalhes
- `PUT /api/sessions/:id/progress` — progresso

### Node.js faz:
- Gerencia conexões WebSocket
- Autentica via JWT no handshake
- Emite/recebe eventos de chat
- Notifica presença (quem está online)

---

## Frontend decide pra onde vai

```javascript
// config.js
const CONFIG = {
  API_URL: 'http://localhost:8080',      // Spring Boot
  REALTIME_URL: 'http://localhost:3001'   // Node.js
};

// Buscar dados → Spring Boot
fetch(`${CONFIG.API_URL}/api/sessions`, {
  headers: { 'Authorization': `Bearer ${token}` }
});

// Chat → Node.js
const socket = io(CONFIG.REALTIME_URL, {
  auth: { token }
});
```

---

## Variáveis de ambiente

### Spring Boot — `backend-java/.env`
```
DATABASE_URL=jdbc:postgresql://localhost:5432/litcircle
JWT_SECRET=chave_secreta_compartilhada
PORT=8080
```

### Node.js — `backend-node/.env`
```
PORT=3001
JWT_SECRET=chave_secreta_compartilhada
NODE_ENV=development
```

### Frontend — `frontend/config.js`
```javascript
const CONFIG = {
  API_URL: 'http://localhost:8080',
  REALTIME_URL: 'http://localhost:3001'
};
```

---

## Fluxo: usuário entra e manda mensagem

```
1. Frontend: GET /api/sessions/LIT-X7K2 → Spring Boot
2. Frontend: conecta Socket.IO → Node.js (JWT no handshake)
3. Node.js: valida JWT localmente
4. Frontend: emite "join_session" { sessionId }
5. Frontend: emite "send_message" { sessionId, text: "Oi!" }
6. Node.js: emite "new_message" para todos na sala
```
