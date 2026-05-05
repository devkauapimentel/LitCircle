# Contrato de API

Documentação de todas as rotas REST (Spring Boot :8080) e eventos WebSocket (Node.js :3001).

**Convenções:**
- Todas as rotas privadas exigem header: `Authorization: Bearer <jwt_token>`
- Todos os bodies são `Content-Type: application/json`
- Timestamps em ISO 8601: `2024-01-15T14:30:00Z`
- IDs são UUIDs v4

---

## Autenticação — Spring Boot

### POST /api/auth/register

Cria uma nova conta.

**Body:**
```json
{
  "name": "Kauã",
  "email": "kaua@email.com",
  "password": "minhasenha123"
}
```

**Resposta 201:**
```json
{
  "token": "eyJhbGciOiJIUzI1NiJ9...",
  "user": {
    "id": "uuid",
    "name": "Kauã",
    "email": "kaua@email.com",
    "avatarUrl": null
  }
}
```

**Erros:**
- `400` — campos obrigatórios ausentes ou senha curta
- `409` — e-mail já cadastrado

---

### POST /api/auth/login

Autentica um usuário existente.

**Body:**
```json
{
  "email": "kaua@email.com",
  "password": "minhasenha123"
}
```

**Resposta 200:**
```json
{
  "token": "eyJhbGciOiJIUzI1NiJ9...",
  "user": {
    "id": "uuid",
    "name": "Kauã",
    "email": "kaua@email.com",
    "avatarUrl": "https://..."
  }
}
```

**Erros:**
- `401` — credenciais inválidas (mensagem genérica, não revela qual campo)

---

## Usuários — Spring Boot

### GET /api/users/me

Retorna o perfil do usuário autenticado.

**Resposta 200:**
```json
{
  "id": "uuid",
  "name": "Kauã",
  "email": "kaua@email.com",
  "avatarUrl": "https://...",
  "createdAt": "2024-01-01T00:00:00Z"
}
```

---

### PUT /api/users/me

Atualiza o perfil do usuário autenticado.

**Body (todos opcionais):**
```json
{
  "name": "Kauã Ferreira",
  "avatarUrl": "https://..."
}
```

**Resposta 200:** mesmo formato do GET /api/users/me

---

### GET /api/users/:id/streak

Retorna os dados de streak de um usuário.

**Resposta 200:**
```json
{
  "currentStreak": 7,
  "longestStreak": 15,
  "totalPomodoros": 142,
  "calendar": [
    { "date": "2024-01-15", "count": 3 },
    { "date": "2024-01-14", "count": 1 },
    { "date": "2024-01-13", "count": 0 }
  ]
}
```

---

## Livros — Spring Boot

### GET /api/books

Lista os livros da biblioteca do usuário autenticado.

**Query params:**
- `search` (opcional) — busca por título ou autor
- `favorites` (opcional, boolean) — filtra apenas favoritos
- `page` (opcional, default 0) — paginação
- `size` (opcional, default 20) — itens por página

**Resposta 200:**
```json
{
  "content": [
    {
      "id": "uuid",
      "title": "O Senhor dos Anéis",
      "author": "J.R.R. Tolkien",
      "totalPages": 1178,
      "coverUrl": "https://...",
      "isFavorite": true,
      "createdAt": "2024-01-01T00:00:00Z"
    }
  ],
  "totalElements": 42,
  "totalPages": 3,
  "currentPage": 0
}
```

---

### POST /api/books

Cadastra um novo livro na biblioteca.

**Body:**
```json
{
  "title": "O Senhor dos Anéis",
  "author": "J.R.R. Tolkien",
  "totalPages": 1178,
  "coverUrl": "https://..."
}
```

**Resposta 201:** objeto do livro criado

**Erros:**
- `400` — campos obrigatórios ausentes ou totalPages <= 0

---

### PATCH /api/books/:id/favorite

Alterna o estado de favorito de um livro.

**Resposta 200:**
```json
{
  "id": "uuid",
  "isFavorite": true
}
```

**Erros:**
- `403` — livro não pertence ao usuário autenticado
- `404` — livro não encontrado

---

### DELETE /api/books/:id

Remove um livro da biblioteca.

**Resposta 204** (sem body)

**Erros:**
- `403` — livro não pertence ao usuário
- `409` — livro está sendo usado em uma sessão ativa

---

## Sessões — Spring Boot

### POST /api/sessions

Cria uma nova sessão de leitura.

**Body:**
```json
{
  "bookId": "uuid-do-livro",
  "startsAt": "2024-02-01",
  "endsAt": "2024-02-28",
  "password": "senha123",
  "maxParticipants": 10
}
```

`password` e `maxParticipants` são opcionais.

**Resposta 201:**
```json
{
  "id": "uuid",
  "code": "LIT-X7K2",
  "book": { "id": "uuid", "title": "...", "author": "...", "totalPages": 300 },
  "host": { "id": "uuid", "name": "Kauã" },
  "hasPassword": true,
  "maxParticipants": 10,
  "participantCount": 1,
  "status": "active",
  "startsAt": "2024-02-01",
  "endsAt": "2024-02-28"
}
```

---

### POST /api/sessions/join

Entra em uma sessão pelo código de convite.

**Body:**
```json
{
  "code": "LIT-X7K2",
  "password": "senha123"
}
```

`password` obrigatório apenas se a sessão tiver senha.

**Resposta 200:** objeto da sessão (mesmo formato do POST /api/sessions)

**Erros:**
- `400` — código não fornecido
- `401` — senha incorreta
- `404` — sessão não encontrada
- `409` — usuário já é participante
- `410` — sessão encerrada
- `422` — sessão lotada

---

### GET /api/sessions/:id

Retorna detalhes de uma sessão.

**Resposta 200:**
```json
{
  "id": "uuid",
  "code": "LIT-X7K2",
  "book": { "id": "uuid", "title": "...", "author": "...", "totalPages": 300, "coverUrl": "..." },
  "host": { "id": "uuid", "name": "Kauã", "avatarUrl": "..." },
  "participants": [
    {
      "userId": "uuid",
      "name": "Kauã",
      "avatarUrl": "...",
      "currentPage": 150,
      "percentage": 50.0,
      "isHost": true
    }
  ],
  "hasPassword": false,
  "maxParticipants": null,
  "participantCount": 3,
  "status": "active",
  "startsAt": "2024-02-01",
  "endsAt": "2024-02-28",
  "currentChooser": { "id": "uuid", "name": "Rafael" }
}
```

**Erros:**
- `403` — usuário não é participante da sessão
- `404` — sessão não encontrada

---

### PATCH /api/sessions/:id

Atualiza configurações da sessão (apenas host).

**Body (todos opcionais):**
```json
{
  "endsAt": "2024-03-15",
  "password": "nova_senha",
  "maxParticipants": 5
}
```

**Resposta 200:** objeto da sessão atualizado

**Erros:**
- `403` — usuário não é o host

---

### POST /api/sessions/:id/end

Encerra a sessão (apenas host).

**Resposta 200:**
```json
{ "status": "ended" }
```

---

### PUT /api/sessions/:id/progress

Atualiza o progresso de leitura do usuário autenticado na sessão.

**Body:**
```json
{
  "currentPage": 150
}
```

**Resposta 200:**
```json
{
  "currentPage": 150,
  "percentage": 50.0,
  "updatedAt": "2024-01-15T14:30:00Z"
}
```

**Erros:**
- `400` — página fora do intervalo válido (0 a totalPages)
- `403` — usuário não é participante da sessão

---

### GET /api/sessions

Lista as sessões do usuário autenticado.

**Query params:**
- `status` (opcional) — `active` ou `ended`

**Resposta 200:**
```json
[
  {
    "id": "uuid",
    "code": "LIT-X7K2",
    "book": { "title": "...", "coverUrl": "..." },
    "status": "active",
    "startsAt": "2024-02-01",
    "endsAt": "2024-02-28",
    "participantCount": 4
  }
]
```

---

### POST /api/streak/record

Registra um Pomodoro concluído. Chamado internamente pelo Node.js.

**Body:**
```json
{
  "userId": "uuid",
  "completedAt": "2024-01-15T14:30:00Z",
  "sessionId": "uuid",
  "durationSeconds": 1500
}
```

**Resposta 201:**
```json
{
  "date": "2024-01-15",
  "totalToday": 3,
  "currentStreak": 7
}
```

---

### GET /health

Health check para monitoramento.

**Resposta 200:**
```json
{ "status": "ok", "timestamp": "2024-01-15T14:30:00Z" }
```

---

## WebSocket — Node.js :3001

### Conexão

```javascript
import { io } from 'socket.io-client';

const socket = io('http://localhost:3001', {
  auth: {
    token: localStorage.getItem('token')
  }
});

socket.on('connect_error', (err) => {
  console.error('Erro de conexão:', err.message);
  // "Token não fornecido" ou "Token inválido"
});
```

---

### Eventos do cliente para o servidor

**join_session**
```javascript
socket.emit('join_session', { sessionId: 'uuid' });
// Resposta automática: evento "chat_history"
```

**leave_session**
```javascript
socket.emit('leave_session', { sessionId: 'uuid' });
```

**send_message**
```javascript
socket.emit('send_message', {
  sessionId: 'uuid',
  text: 'Que capítulo incrível!'
});
```

**start_pomodoro**
```javascript
socket.emit('start_pomodoro', {
  sessionId: 'uuid',
  duration: 1500  // segundos — padrão 25 min
});
```

**pause_pomodoro / resume_pomodoro**
```javascript
socket.emit('pause_pomodoro', { sessionId: 'uuid' });
socket.emit('resume_pomodoro', { sessionId: 'uuid' });
```

**update_progress** *(real-time — notifica os outros em tempo real)*
```javascript
socket.emit('update_progress', {
  sessionId: 'uuid',
  currentPage: 150
});
// O Spring Boot também é chamado via REST para persistir
```

---

### Eventos do servidor para o cliente

**chat_history** *(recebido ao entrar na sessão)*
```javascript
socket.on('chat_history', ({ messages }) => {
  // messages: array das últimas 50 mensagens
  // [{ id, userId, userName, text, timestamp }]
});
```

**new_message**
```javascript
socket.on('new_message', ({ id, userId, userName, text, timestamp }) => {
  // Adicionar mensagem ao chat
});
```

**user_joined / user_left**
```javascript
socket.on('user_joined', ({ userId, userName }) => { /* ... */ });
socket.on('user_left', ({ userId, userName }) => { /* ... */ });
```

**pomodoro_tick**
```javascript
socket.on('pomodoro_tick', ({ remaining }) => {
  // remaining: segundos restantes
  // Atualizar display do timer
});
```

**pomodoro_completed**
```javascript
socket.on('pomodoro_completed', ({ userId }) => {
  if (userId === currentUser.id) {
    // Mostrar parabéns, buscar streak atualizado
  }
});
```

**progress_updated**
```javascript
socket.on('progress_updated', ({ userId, userName, currentPage, percentage }) => {
  // Atualizar progresso do participante na UI
});
```

**session_config_changed**
```javascript
socket.on('session_config_changed', ({ config }) => {
  // config: { endsAt, maxParticipants, currentChooser }
});
```

**session_ended**
```javascript
socket.on('session_ended', () => {
  // Redirecionar para tela de sessões encerradas
});
```
