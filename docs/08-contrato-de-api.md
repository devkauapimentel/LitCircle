# Contrato de API — MVP v0

**Convenções:**
- Rotas privadas exigem: `Authorization: Bearer <jwt_token>`
- Bodies em `Content-Type: application/json`
- Timestamps em ISO 8601
- IDs são UUIDs v4

---

## Rotas públicas

### POST /api/auth/register

**Body:**
```json
{ "name": "Kauã", "email": "kaua@email.com", "password": "minhasenha123" }
```

**201:** `{ "token": "jwt...", "user": { "id", "name", "email" } }`
**400:** campos ausentes ou senha < 8 chars
**409:** e-mail já cadastrado

### POST /api/auth/login

**Body:**
```json
{ "email": "kaua@email.com", "password": "minhasenha123" }
```

**200:** `{ "token": "jwt...", "user": { "id", "name", "email" } }`
**401:** credenciais inválidas (mensagem genérica)

### GET /health

**200:** `{ "status": "ok" }`

---

## Rotas privadas (exigem JWT)

### POST /api/sessions

Cria sessão de leitura.

**Body:**
```json
{
  "bookTitle": "O Senhor dos Anéis",
  "bookAuthor": "J.R.R. Tolkien",
  "bookPages": 1178,
  "startsAt": "2026-06-01",
  "endsAt": "2026-06-30"
}
```

**201:**
```json
{
  "id": "uuid",
  "code": "LIT-X7K2",
  "bookTitle": "O Senhor dos Anéis",
  "bookAuthor": "J.R.R. Tolkien",
  "bookPages": 1178,
  "host": { "id": "uuid", "name": "Kauã" },
  "participantCount": 1,
  "status": "active",
  "startsAt": "2026-06-01",
  "endsAt": "2026-06-30"
}
```

### POST /api/sessions/join

**Body:**
```json
{ "code": "LIT-X7K2" }
```

**200:** objeto da sessão
**404:** sessão não encontrada
**409:** já é participante
**410:** sessão encerrada

### GET /api/sessions

Lista sessões do usuário autenticado.

**200:**
```json
[
  {
    "id": "uuid",
    "code": "LIT-X7K2",
    "bookTitle": "O Senhor dos Anéis",
    "status": "active",
    "participantCount": 4
  }
]
```

### GET /api/sessions/:id

Detalhes de uma sessão com participantes.

**200:**
```json
{
  "id": "uuid",
  "code": "LIT-X7K2",
  "bookTitle": "O Senhor dos Anéis",
  "bookAuthor": "Tolkien",
  "bookPages": 1178,
  "host": { "id": "uuid", "name": "Kauã" },
  "participants": [
    { "userId": "uuid", "name": "Kauã", "currentPage": 918, "percentage": 77.9, "isHost": true },
    { "userId": "uuid", "name": "Rafael", "currentPage": 613, "percentage": 52.0, "isHost": false }
  ],
  "status": "active",
  "startsAt": "2026-06-01",
  "endsAt": "2026-06-30"
}
```

**403:** não é participante | **404:** não encontrada

### PUT /api/sessions/:id/progress

**Body:**
```json
{ "currentPage": 150 }
```

**200:** `{ "currentPage": 150, "percentage": 12.7 }`
**400:** página fora do intervalo | **403:** não é participante

---

## WebSocket — Node.js :3001

### Conexão

```javascript
const socket = io('http://localhost:3001', {
  auth: { token: localStorage.getItem('token') }
});
```

### Eventos: cliente → servidor

| Evento | Payload | Descrição |
|--------|---------|-----------|
| `join_session` | `{ sessionId }` | Entra na sala |
| `leave_session` | `{ sessionId }` | Sai da sala |
| `send_message` | `{ sessionId, text }` | Envia mensagem |

### Eventos: servidor → cliente

| Evento | Payload | Descrição |
|--------|---------|-----------|
| `new_message` | `{ userId, userName, text, timestamp }` | Nova mensagem |
| `user_joined` | `{ userId, userName }` | Alguém entrou |
| `user_left` | `{ userId, userName }` | Alguém saiu |
