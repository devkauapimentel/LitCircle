# Issues — Cadastre no GitHub Projects

> Copie cada issue e crie no GitHub. Organize no board Kanban.

---

## Labels para criar no GitHub

| Label | Cor | Uso |
|-------|-----|-----|
| `feature` | Azul | Nova funcionalidade |
| `chore` | Cinza | Setup, config, infra |
| `bug` | Vermelho | Comportamento incorreto |
| `frontend` | Roxo | HTML/CSS/JS |
| `backend-java` | Laranja | Spring Boot |
| `backend-node` | Verde | Node.js |
| `integration` | Rosa | Envolve os dois backends |
| `docs` | Cinza claro | Documentação |

---

## Milestones

| Milestone | Descrição |
|-----------|-----------|
| v0.1 — Esqueleto | Setup, estrutura, health checks |
| v0.2 — Autenticação | Cadastro, login, JWT |
| v0.3 — Sessões | Criar, entrar, participantes, progresso |
| v0.4 — Chat | Mensagens em tempo real |
| v0.5 — Deploy + Polish | Deploy, testes, polish |

---

## MILESTONE v0.1 — Esqueleto

### ISSUE #1 — Setup do repositório e estrutura

**Labels:** `chore`
**Milestone:** v0.1
**Responsável:** Ambos

**Critérios de aceite:**
- [ ] Estrutura de pastas: `frontend/`, `backend-java/`, `backend-node/`
- [ ] `.gitignore` configurado
- [ ] Ambos conseguem clonar e contribuir
- [ ] Branch protection na `main` (exigir PR)

---

### ISSUE #2 — Boilerplate frontend

**Labels:** `chore` `frontend`
**Milestone:** v0.1
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] `frontend/index.html` com página "LitCircle — Em construção"
- [ ] `frontend/style.css` com reset CSS básico e variáveis de cor
- [ ] `frontend/app.js` vazio com comentário de estrutura
- [ ] Funciona abrindo o HTML no navegador

---

### ISSUE #3 — Boilerplate backend Node.js

**Labels:** `chore` `backend-node`
**Milestone:** v0.1
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] `npm init` feito, `package.json` configurado
- [ ] Express + Socket.IO + jsonwebtoken + cors + dotenv instalados
- [ ] `src/index.js` com servidor na porta 3001
- [ ] `GET /health` retorna `{ "status": "ok" }`
- [ ] Socket.IO aceita conexões
- [ ] `.env` com `PORT=3001` e `JWT_SECRET`
- [ ] `npm run dev` funciona com nodemon

---

### ISSUE #4 — Boilerplate backend Java

**Labels:** `chore` `backend-java`
**Milestone:** v0.1
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] Projeto gerado em start.spring.io (Java 21, Spring Boot 3)
- [ ] Dependências: Web, Data JPA, Security, PostgreSQL Driver, Flyway, Validation, Lombok
- [ ] `application.properties` conecta no PostgreSQL local
- [ ] `GET /health` retorna `{ "status": "ok" }`
- [ ] `./mvnw spring-boot:run` sobe na porta 8080

---

### ISSUE #5 — PostgreSQL local configurado

**Labels:** `chore`
**Milestone:** v0.1
**Responsável:** Ambos

**Critérios de aceite:**
- [ ] PostgreSQL instalado nas máquinas dos dois
- [ ] Banco `litcircle` criado
- [ ] Spring Boot conecta sem erro
- [ ] `.env.example` criado em cada serviço

---

## MILESTONE v0.2 — Autenticação

### ISSUE #6 — Migration: tabela users

**Labels:** `feature` `backend-java`
**Milestone:** v0.2
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] `V1__create_users.sql` com schema do doc 07
- [ ] Migration executa sem erro ao subir o Spring Boot
- [ ] Índice e UNIQUE em `email` criados

---

### ISSUE #7 — Endpoint de cadastro

**Labels:** `feature` `backend-java`
**Milestone:** v0.2
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] `POST /api/auth/register` aceita `{ name, email, password }`
- [ ] Valida campos obrigatórios
- [ ] Retorna 409 se e-mail já existe
- [ ] Senha armazenada com bcrypt
- [ ] Retorna 201 com JWT e dados do usuário
- [ ] Testado no Thunder Client

---

### ISSUE #8 — Configurar JWT no Spring Boot

**Labels:** `feature` `backend-java`
**Milestone:** v0.2
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] `JwtService.java` com `generateToken()` e `validateToken()`
- [ ] JWT contém: `sub` (UUID), `name`, `email`, `iat`, `exp`
- [ ] Chave secreta via variável de ambiente `JWT_SECRET`
- [ ] Spring Security valida JWT em rotas privadas
- [ ] Rotas `/api/auth/*` e `/health` são públicas

---

### ISSUE #9 — Endpoint de login

**Labels:** `feature` `backend-java`
**Milestone:** v0.2
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] `POST /api/auth/login` aceita `{ email, password }`
- [ ] Verifica senha com bcrypt
- [ ] Retorna 401 com mensagem genérica em caso de falha
- [ ] Retorna 200 com JWT em caso de sucesso

---

### ISSUE #10 — Tela de login

**Labels:** `feature` `frontend`
**Milestone:** v0.2
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] Formulário com e-mail e senha
- [ ] Validação antes de enviar (campos vazios)
- [ ] `fetch('POST /api/auth/login')` com body JSON
- [ ] Token salvo no `localStorage`
- [ ] Redireciona para dashboard após login
- [ ] Mensagem de erro visível quando login falha
- [ ] Link "Não tem conta? Cadastre-se"

---

### ISSUE #11 — Tela de cadastro

**Labels:** `feature` `frontend`
**Milestone:** v0.2
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] Formulário com nome, e-mail, senha, confirmar senha
- [ ] Validação: campos obrigatórios, senhas iguais, mínimo 8 chars
- [ ] `fetch('POST /api/auth/register')`
- [ ] Token salvo no `localStorage` e redireciona para dashboard
- [ ] Link "Já tem conta? Entrar"

---

### ISSUE #12 — Middleware JWT no Node.js

**Labels:** `feature` `backend-node`
**Milestone:** v0.2
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] `src/middleware/auth.js` valida JWT no handshake do Socket.IO
- [ ] Usa a mesma `JWT_SECRET` do Spring Boot
- [ ] Rejeita conexões sem token ou com token inválido
- [ ] `socket.userId` e `socket.userName` disponíveis após auth

---

## MILESTONE v0.3 — Sessões

### ISSUE #13 — Migrations: sessions e session_members

**Labels:** `feature` `backend-java`
**Milestone:** v0.3
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] `V2__create_sessions.sql` com código único
- [ ] `V3__create_session_members.sql` com UNIQUE(session_id, user_id)
- [ ] Ambas executam sem erro

---

### ISSUE #14 — Criar sessão de leitura

**Labels:** `feature` `backend-java`
**Milestone:** v0.3
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] `POST /api/sessions` cria sessão com código gerado (ex: LIT-X7K2)
- [ ] Campos: bookTitle, bookAuthor, bookPages, startsAt, endsAt
- [ ] Host é automaticamente o primeiro participante
- [ ] Retorna 201 com dados da sessão

---

### ISSUE #15 — Entrar em sessão por código

**Labels:** `feature` `backend-java`
**Milestone:** v0.3
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] `POST /api/sessions/join` aceita `{ code }`
- [ ] Retorna 404 se código não existe
- [ ] Retorna 409 se usuário já é participante
- [ ] Retorna 410 se sessão encerrada
- [ ] Retorna 200 com dados da sessão

---

### ISSUE #16 — Listar sessões e detalhes

**Labels:** `feature` `backend-java`
**Milestone:** v0.3
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] `GET /api/sessions` lista sessões do usuário autenticado
- [ ] `GET /api/sessions/:id` retorna sessão com participantes e progresso
- [ ] Retorna 403 se usuário não é participante

---

### ISSUE #17 — Atualizar progresso de leitura

**Labels:** `feature` `backend-java`
**Milestone:** v0.3
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] `PUT /api/sessions/:id/progress` aceita `{ currentPage }`
- [ ] Valida: página entre 0 e total de páginas
- [ ] Retorna porcentagem calculada
- [ ] Retorna 403 se não é participante

---

### ISSUE #18 — Tela: Dashboard

**Labels:** `feature` `frontend`
**Milestone:** v0.3
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] Verifica se tem token no localStorage — se não, redireciona para login
- [ ] Botão "Criar sessão" e campo "Entrar com código"
- [ ] Lista de sessões ativas do usuário
- [ ] Clique em sessão leva para a tela da sessão

---

### ISSUE #19 — Tela: Criar sessão

**Labels:** `feature` `frontend`
**Milestone:** v0.3
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] Formulário: título do livro, autor, total de páginas, data início, data fim
- [ ] `fetch('POST /api/sessions')`
- [ ] Após criar, exibe o código de convite e redireciona para a sessão

---

### ISSUE #20 — Tela: Sessão de leitura

**Labels:** `feature` `frontend`
**Milestone:** v0.3
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] Exibe: info do livro, lista de participantes com progresso
- [ ] Input de página atual com botão "Salvar progresso"
- [ ] `fetch('PUT /api/sessions/:id/progress')`
- [ ] Espaço reservado para chat (implementado na milestone v0.4)

---

## MILESTONE v0.4 — Chat

### ISSUE #21 — Migration: tabela messages

**Labels:** `feature` `backend-java`
**Milestone:** v0.4
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] `V4__create_messages.sql` com schema do doc 07
- [ ] Índice em `(session_id, sent_at)`

---

### ISSUE #22 — Servidor de chat com Socket.IO

**Labels:** `feature` `backend-node`
**Milestone:** v0.4
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] `join_session` — entra na room
- [ ] `send_message` — valida texto (não vazio, máx 500 chars), emite para todos
- [ ] `new_message` — emitido para todos na room
- [ ] `user_joined` / `user_left` — notifica presença
- [ ] Mensagens mantidas em memória durante a sessão

---

### ISSUE #23 — Chat no frontend

**Labels:** `feature` `frontend`
**Milestone:** v0.4
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] Conexão Socket.IO com JWT no handshake
- [ ] Lista de mensagens com nome e horário
- [ ] Input de mensagem — Enter envia, Shift+Enter quebra linha
- [ ] Scroll automático para mensagem mais recente
- [ ] Reconexão automática se conexão cair

---

## MILESTONE v0.5 — Deploy + Polish

### ISSUE #24 — Deploy no Render.com

**Labels:** `chore`
**Milestone:** v0.5
**Responsável:** Ambos

**Critérios de aceite:**
- [ ] Frontend estático deployado
- [ ] Spring Boot deployado e conectado ao PostgreSQL do Render
- [ ] Node.js deployado
- [ ] JWT_SECRET idêntico nos dois backends
- [ ] Health check responde nos dois backends
- [ ] Deploy automático funciona após push na main

---

### ISSUE #25 — Teste end-to-end

**Labels:** `integration`
**Milestone:** v0.5
**Responsável:** Ambos

**Critérios de aceite:**
- [ ] Fluxo completo testado: cadastro → login → criar sessão → entrar → chat
- [ ] Testado com 2 usuários simultâneos em produção
- [ ] Testado em Chrome e Firefox

---

### ISSUE #26 — Loading states e mensagens de erro

**Labels:** `feature` `frontend`
**Milestone:** v0.5
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] Todas as ações mostram loading durante requisição
- [ ] Erros da API exibidos em português
- [ ] Página 404 básica

---

## Resumo

| Milestone | Issues | Semanas |
|-----------|--------|---------|
| v0.1 — Esqueleto | #1 a #5 | 1 |
| v0.2 — Autenticação | #6 a #12 | 2 |
| v0.3 — Sessões | #13 a #20 | 2 |
| v0.4 — Chat | #21 a #23 | 2 |
| v0.5 — Deploy | #24 a #26 | 1 |
| **Total** | **26 issues** | **~8 semanas** |
