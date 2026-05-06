# Modelo de dados — MVP v0

> 4 tabelas. É isso. Biblioteca, streak, Pomodoro e rodízio vêm em versões futuras.

---

## Diagrama de entidades

```
┌──────────────┐       ┌──────────────────┐
│    users     │       │     sessions     │
├──────────────┤       ├──────────────────┤
│ id (UUID) PK │──┐    │ id (UUID) PK     │
│ name         │  │    │ code (LIT-XXXX)  │
│ email (UQ)   │  │    │ book_title       │
│ password_hash│  ├───►│ host_user_id FK  │
│ created_at   │  │    │ book_author      │
└──────────────┘  │    │ book_pages       │
                  │    │ status           │
                  │    │ starts_at        │
                  │    │ ends_at          │
                  │    │ created_at       │
                  │    └──────────────────┘
                  │
                  │    ┌──────────────────┐
                  │    │ session_members  │
                  │    ├──────────────────┤
                  ├───►│ user_id FK       │
                  │    │ session_id FK    │
                  │    │ current_page     │
                  │    │ joined_at        │
                  │    └──────────────────┘
                  │
                  │    ┌──────────────────┐
                  │    │    messages      │
                  │    ├──────────────────┤
                  └───►│ user_id FK       │
                       │ session_id FK    │
                       │ text             │
                       │ sent_at          │
                       └──────────────────┘
```

**Legenda:** PK = chave primária, FK = chave estrangeira, UQ = único

---

## Tabelas — SQL completo

### users

```sql
CREATE TABLE users (
  id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name          VARCHAR(100) NOT NULL,
  email         VARCHAR(255) NOT NULL UNIQUE,
  password_hash VARCHAR(255) NOT NULL,
  created_at    TIMESTAMP NOT NULL DEFAULT NOW()
);

CREATE INDEX idx_users_email ON users(email);
```

| Coluna | Tipo | Descrição |
|--------|------|-----------|
| id | UUID | Identificador único gerado automaticamente |
| name | VARCHAR(100) | Nome de exibição |
| email | VARCHAR(255) | E-mail único, usado no login |
| password_hash | VARCHAR(255) | Hash bcrypt da senha — nunca a senha real |

### sessions

```sql
CREATE TABLE sessions (
  id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  code          VARCHAR(10) NOT NULL UNIQUE,
  host_user_id  UUID NOT NULL REFERENCES users(id),
  book_title    VARCHAR(300) NOT NULL,
  book_author   VARCHAR(200),
  book_pages    INTEGER NOT NULL DEFAULT 0,
  status        VARCHAR(20) NOT NULL DEFAULT 'active'
                CHECK (status IN ('active', 'ended')),
  starts_at     DATE NOT NULL,
  ends_at       DATE NOT NULL,
  created_at    TIMESTAMP NOT NULL DEFAULT NOW()
);

CREATE INDEX idx_sessions_code ON sessions(code);
```

| Coluna | Tipo | Descrição |
|--------|------|-----------|
| code | VARCHAR(10) | Código de convite único (ex: LIT-X7K2) |
| host_user_id | UUID | Quem criou a sessão |
| book_title | VARCHAR(300) | Título do livro (digitado pelo host) |
| status | VARCHAR(20) | 'active' ou 'ended' |

### session_members

```sql
CREATE TABLE session_members (
  id           UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  session_id   UUID NOT NULL REFERENCES sessions(id) ON DELETE CASCADE,
  user_id      UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  current_page INTEGER NOT NULL DEFAULT 0,
  joined_at    TIMESTAMP NOT NULL DEFAULT NOW(),
  UNIQUE (session_id, user_id)
);

CREATE INDEX idx_session_members_session ON session_members(session_id);
```

### messages

```sql
CREATE TABLE messages (
  id         UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  session_id UUID NOT NULL REFERENCES sessions(id) ON DELETE CASCADE,
  user_id    UUID NOT NULL REFERENCES users(id),
  text       VARCHAR(500) NOT NULL,
  sent_at    TIMESTAMP NOT NULL DEFAULT NOW()
);

CREATE INDEX idx_messages_session ON messages(session_id, sent_at);
```

---

## Migrations com Flyway

Os arquivos ficam em `backend-java/src/main/resources/db/migration/`:

```
V1__create_users.sql
V2__create_sessions.sql
V3__create_session_members.sql
V4__create_messages.sql
```

Cada arquivo contém o SQL de uma tabela. O Flyway executa em ordem e nunca roda a mesma migration duas vezes.

---

## Como aprender banco de dados

1. **Agora (2h):** [sqlbolt.com](https://sqlbolt.com) — tutorial interativo de SQL
2. **Semana 2:** [pgexercises.com](https://pgexercises.com) — exercícios práticos
3. **Referência:** postgresql.org/docs/current/tutorial.html
