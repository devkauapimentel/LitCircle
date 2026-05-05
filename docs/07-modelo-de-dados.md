# Modelo de dados

Esquema completo do PostgreSQL com todas as entidades, relacionamentos e justificativas de design.

---

## Diagrama de entidades (texto)

```
users ──────────────────┬── books (criados por)
  │                     │
  ├── session_members ──┴── sessions ──── session_messages (histórico)
  │       │
  ├── reading_progress (por sessão)
  │
  ├── pomodoro_records
  │
  └── reading_streaks
```

---

## Tabelas

### users

Armazena os dados de cada usuário cadastrado.

```sql
CREATE TABLE users (
  id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name          VARCHAR(100) NOT NULL,
  email         VARCHAR(255) NOT NULL UNIQUE,
  password_hash VARCHAR(255) NOT NULL,
  avatar_url    VARCHAR(500),
  created_at    TIMESTAMP NOT NULL DEFAULT NOW(),
  updated_at    TIMESTAMP NOT NULL DEFAULT NOW()
);

CREATE INDEX idx_users_email ON users(email);
```

| Coluna | Tipo | Descrição |
|---|---|---|
| id | UUID | Chave primária — UUID v4 gerado automaticamente |
| name | VARCHAR(100) | Nome de exibição do usuário |
| email | VARCHAR(255) | E-mail único, usado no login |
| password_hash | VARCHAR(255) | Hash bcrypt da senha — nunca a senha em texto |
| avatar_url | VARCHAR(500) | URL da foto de perfil (opcional) |

---

### books

Biblioteca de livros. Cada livro pertence ao usuário que o cadastrou.

```sql
CREATE TABLE books (
  id           UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id      UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  title        VARCHAR(300) NOT NULL,
  author       VARCHAR(200) NOT NULL,
  total_pages  INTEGER NOT NULL CHECK (total_pages > 0),
  cover_url    VARCHAR(500),
  is_favorite  BOOLEAN NOT NULL DEFAULT FALSE,
  created_at   TIMESTAMP NOT NULL DEFAULT NOW()
);

CREATE INDEX idx_books_user_id ON books(user_id);
```

| Coluna | Tipo | Descrição |
|---|---|---|
| user_id | UUID | FK para users — dono do livro |
| total_pages | INTEGER | Total de páginas — usado para calcular progresso |
| is_favorite | BOOLEAN | Se o usuário favoritou o livro |

---

### sessions

Uma sessão de leitura criada por um host para um grupo ler um livro juntos.

```sql
CREATE TABLE sessions (
  id               UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  code             VARCHAR(10) NOT NULL UNIQUE,
  host_user_id     UUID NOT NULL REFERENCES users(id),
  book_id          UUID NOT NULL REFERENCES books(id),
  password_hash    VARCHAR(255),
  max_participants INTEGER,
  status           VARCHAR(20) NOT NULL DEFAULT 'active'
                   CHECK (status IN ('active', 'ended')),
  starts_at        DATE NOT NULL,
  ends_at          DATE NOT NULL,
  current_chooser_user_id UUID REFERENCES users(id),
  created_at       TIMESTAMP NOT NULL DEFAULT NOW(),
  updated_at       TIMESTAMP NOT NULL DEFAULT NOW()
);

CREATE INDEX idx_sessions_code ON sessions(code);
CREATE INDEX idx_sessions_host ON sessions(host_user_id);
```

| Coluna | Tipo | Descrição |
|---|---|---|
| code | VARCHAR(10) | Código de convite único (ex: LIT-X7K2) |
| host_user_id | UUID | FK para users — quem criou a sessão |
| book_id | UUID | FK para books — livro da sessão |
| password_hash | VARCHAR | Hash da senha de acesso (nullable se sem senha) |
| max_participants | INTEGER | Limite de participantes (nullable = sem limite) |
| status | VARCHAR | Estado da sessão: 'active' ou 'ended' |
| current_chooser_user_id | UUID | Quem está com o direito de escolha no rodízio |

---

### session_members

Tabela de junção entre usuários e sessões. Registra quem está em qual sessão.

```sql
CREATE TABLE session_members (
  id         UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  session_id UUID NOT NULL REFERENCES sessions(id) ON DELETE CASCADE,
  user_id    UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  joined_at  TIMESTAMP NOT NULL DEFAULT NOW(),
  UNIQUE (session_id, user_id)
);

CREATE INDEX idx_session_members_session ON session_members(session_id);
CREATE INDEX idx_session_members_user    ON session_members(user_id);
```

---

### reading_progress

Rastreia o progresso de leitura de cada participante em cada sessão.

```sql
CREATE TABLE reading_progress (
  id           UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  session_id   UUID NOT NULL REFERENCES sessions(id) ON DELETE CASCADE,
  user_id      UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  current_page INTEGER NOT NULL DEFAULT 0,
  updated_at   TIMESTAMP NOT NULL DEFAULT NOW(),
  UNIQUE (session_id, user_id)
);

CREATE INDEX idx_reading_progress_session ON reading_progress(session_id);
```

| Coluna | Tipo | Descrição |
|---|---|---|
| current_page | INTEGER | Página atual do usuário na sessão |
| updated_at | TIMESTAMP | Última vez que o progresso foi atualizado |

A porcentagem é calculada em tempo real: `(current_page / book.total_pages) * 100`

---

### reading_progress_history

Histórico de todas as atualizações de progresso de um usuário.

```sql
CREATE TABLE reading_progress_history (
  id           UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  session_id   UUID NOT NULL REFERENCES sessions(id) ON DELETE CASCADE,
  user_id      UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  page_at_time INTEGER NOT NULL,
  recorded_at  TIMESTAMP NOT NULL DEFAULT NOW()
);

CREATE INDEX idx_progress_history_user_session ON reading_progress_history(user_id, session_id);
```

---

### session_messages

Histórico persistido de mensagens de chat. Populado quando a sessão encerra.

```sql
CREATE TABLE session_messages (
  id         UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  session_id UUID NOT NULL REFERENCES sessions(id) ON DELETE CASCADE,
  user_id    UUID NOT NULL REFERENCES users(id),
  text       VARCHAR(500) NOT NULL,
  sent_at    TIMESTAMP NOT NULL
);

CREATE INDEX idx_session_messages_session ON session_messages(session_id, sent_at);
```

Mensagens ativas ficam no Redis durante a sessão. Quando a sessão encerra, o Node.js persiste tudo nesta tabela via chamada ao Spring Boot.

---

### pomodoro_records

Registra cada Pomodoro completado por cada usuário. Base para o cálculo de streak.

```sql
CREATE TABLE pomodoro_records (
  id           UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id      UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  session_id   UUID REFERENCES sessions(id),
  completed_at TIMESTAMP NOT NULL DEFAULT NOW(),
  duration_seconds INTEGER NOT NULL DEFAULT 1500
);

CREATE INDEX idx_pomodoro_records_user ON pomodoro_records(user_id, completed_at);
```

---

### reading_streaks

Cache agregado de streak por usuário e dia. Atualizado a cada Pomodoro completado.

```sql
CREATE TABLE reading_streaks (
  id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id     UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  streak_date DATE NOT NULL,
  count       INTEGER NOT NULL DEFAULT 1,
  UNIQUE (user_id, streak_date)
);

CREATE INDEX idx_reading_streaks_user_date ON reading_streaks(user_id, streak_date);
```

| Coluna | Tipo | Descrição |
|---|---|---|
| streak_date | DATE | O dia da atividade (sem horário) |
| count | INTEGER | Quantos Pomodoros completados naquele dia |

A intensidade visual no calendário é calculada com base em `count`: 1 = claro, 2-3 = médio, 4+ = escuro.

---

### chooser_history

Histórico do rodízio de escolha de livro.

```sql
CREATE TABLE chooser_history (
  id         UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  session_id UUID NOT NULL REFERENCES sessions(id) ON DELETE CASCADE,
  user_id    UUID NOT NULL REFERENCES users(id),
  month      DATE NOT NULL,
  UNIQUE (session_id, month)
);
```

---

## Dados no Redis

O Redis armazena dados efêmeros que mudam frequentemente. Estrutura de chaves:

| Chave | Tipo | Conteúdo | TTL |
|---|---|---|---|
| `chat:{sessionId}` | List | Últimas 50 mensagens em JSON | Sem TTL (limpo quando sessão encerra) |
| `pomodoro:{userId}:{sessionId}` | Hash | `startedAt`, `duration`, `status`, `remaining` | 2 horas |
| `online:{sessionId}` | Set | UUIDs dos usuários online na sessão | Sem TTL |

Exemplo de estrutura de mensagem no Redis:

```json
{
  "id": "uuid",
  "userId": "uuid-do-usuario",
  "userName": "Kauã",
  "text": "Que capítulo incrível!",
  "timestamp": "2024-01-15T14:32:00Z"
}
```

---

## Script de criação completo

O Flyway gerencia as migrations. Os arquivos ficam em `backend-java/src/main/resources/db/migration/`:

```
V1__create_users.sql
V2__create_books.sql
V3__create_sessions.sql
V4__create_session_members.sql
V5__create_reading_progress.sql
V6__create_session_messages.sql
V7__create_pomodoro_records.sql
V8__create_reading_streaks.sql
V9__create_chooser_history.sql
```

Cada arquivo contém o SQL de uma tabela. O Flyway executa em ordem e nunca roda a mesma migration duas vezes.
