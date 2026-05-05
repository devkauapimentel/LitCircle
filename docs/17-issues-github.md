# Issues completas — cadastre no GitHub Projects

> Copie cada issue abaixo e crie no GitHub. O formato é: **Título**, **Labels**, **Milestone**, **Descrição completa**.

---

## Como cadastrar uma issue no GitHub

1. Vá no repositório → aba "Issues" → "New issue"
2. Copie o título e a descrição abaixo
3. Adicione as labels listadas
4. Vincule à milestone correspondente
5. Adicione ao Project (board)
6. Deixe em "Backlog" até chegar a sprint da milestone

---

## MILESTONE v0.1 — Esqueleto

---

### ISSUE #1 — Setup do repositório e estrutura de pastas

**Labels:** `chore` `infra`  
**Milestone:** v0.1 — Esqueleto  
**Responsável:** Kauã e Rafael (fazem juntos)

**Descrição:**
Criar a estrutura inicial do repositório seguindo a arquitetura definida na documentação.

**Critérios de aceite:**
- [ ] Repositório `litcircle` criado no GitHub com visibilidade pública
- [ ] Estrutura de pastas criada: `/frontend`, `/backend-java`, `/backend-node`, `/.github/workflows`
- [ ] `.gitignore` configurado na raiz (ver doc 14-setup-ambiente.md)
- [ ] `docker-compose.yml` criado com PostgreSQL 15 e Redis 7
- [ ] `README.md` atualizado com a documentação do projeto
- [ ] Branch protection configurada na `main` (exigir PR + 1 aprovação)
- [ ] Os dois colaboradores conseguem clonar e rodar `docker compose up -d` sem erro

**Contexto técnico:**
Ver `14-setup-ambiente.md` para o conteúdo de cada arquivo.

---

### ISSUE #2 — Boilerplate do frontend React

**Labels:** `chore` `frontend`  
**Milestone:** v0.1 — Esqueleto  
**Responsável:** Kauã

**Descrição:**
Inicializar o projeto React com Vite, TailwindCSS e as dependências do projeto.

**Critérios de aceite:**
- [ ] Projeto criado com `npm create vite@latest . -- --template react`
- [ ] TailwindCSS configurado e funcionando
- [ ] Dependências instaladas: axios, react-router-dom, @tanstack/react-query, socket.io-client
- [ ] Arquivo `frontend/.env` criado com as variáveis de ambiente (ver doc 14)
- [ ] `npm run dev` sobe a aplicação em `localhost:5173` sem erros
- [ ] `npm run build` gera o build de produção sem erros
- [ ] `.vscode/settings.json` com Prettier e ESLint configurados

---

### ISSUE #3 — Boilerplate do backend Node.js

**Labels:** `chore` `backend-node`  
**Milestone:** v0.1 — Esqueleto  
**Responsável:** Kauã

**Descrição:**
Inicializar o projeto Node.js com Express e Socket.IO.

**Critérios de aceite:**
- [ ] `npm init` executado e `package.json` configurado
- [ ] Dependências instaladas: express, socket.io, ioredis, jsonwebtoken, dotenv, cors
- [ ] `backend-node/.env` criado com as variáveis (ver doc 14)
- [ ] `src/index.js` com servidor Express básico na porta 3001
- [ ] `GET /health` retorna `{ "status": "ok" }`
- [ ] `npm run dev` sobe o servidor sem erros
- [ ] Socket.IO configurado e aceitando conexões

---

### ISSUE #4 — Boilerplate do backend Java Spring Boot

**Labels:** `chore` `backend-java`  
**Milestone:** v0.1 — Esqueleto  
**Responsável:** Rafael

**Descrição:**
Inicializar o projeto Spring Boot com as dependências corretas via Spring Initializr.

**Critérios de aceite:**
- [ ] Projeto gerado em start.spring.io com Java 21 e Spring Boot 3.2+
- [ ] Dependências: Web, Data JPA, Security, PostgreSQL Driver, Flyway, Validation, Lombok
- [ ] `application.properties` configurado para conectar no PostgreSQL local
- [ ] Primeira migration Flyway criada: `V1__init.sql` (arquivo vazio por enquanto)
- [ ] `GET /health` retorna `{ "status": "ok" }` com status 200
- [ ] `./mvnw spring-boot:run` sobe na porta 8080 sem erros
- [ ] Conecta no PostgreSQL do Docker sem erro

---

### ISSUE #5 — Configurar GitHub Actions (CI)

**Labels:** `chore` `infra`  
**Milestone:** v0.1 — Esqueleto  
**Responsável:** Kauã e Rafael

**Descrição:**
Criar os workflows de CI para rodar testes automaticamente em cada PR.

**Critérios de aceite:**
- [ ] Workflow `ci-java.yml` criado — roda `./mvnw test` em PRs que tocam `backend-java/`
- [ ] Workflow `ci-node.yml` criado — roda `npm test` em PRs que tocam `backend-node/`
- [ ] Workflow `ci-frontend.yml` criado — roda `npm test` e `npm run build` em PRs que tocam `frontend/`
- [ ] Todos os três workflows passam no GitHub Actions com o código boilerplate
- [ ] Branch protection na `main` exige que os checks do GitHub Actions passem antes do merge

**Contexto técnico:**
Conteúdo dos workflows está no doc `09-deploy.md`.

---

### ISSUE #6 — Configurar deploy no Railway e Vercel

**Labels:** `chore` `infra` `deploy`  
**Milestone:** v0.1 — Esqueleto  
**Responsável:** Kauã e Rafael (fazem juntos)

**Descrição:**
Configurar os deploys automáticos de todos os serviços.

**Critérios de aceite:**
- [ ] Conta criada no Railway com os quatro serviços: Spring Boot, Node.js, PostgreSQL, Redis
- [ ] `JWT_SECRET` idêntico nos serviços Java e Node no Railway
- [ ] Conta criada na Vercel com o frontend deployado
- [ ] `VITE_API_URL` e `VITE_REALTIME_URL` configurados na Vercel com as URLs do Railway
- [ ] Todos os quatro serviços sobem sem erro após o deploy
- [ ] `GET /health` responde nos dois backends em produção
- [ ] Deploy automático funciona: push na `main` → Railway e Vercel atualizam automaticamente

**Contexto técnico:**
Ver `09-deploy.md` para o guia passo a passo completo.

---

## MILESTONE v0.2 — Autenticação

---

### ISSUE #7 — Migration: tabela users

**Labels:** `feature` `backend-java`  
**Milestone:** v0.2 — Autenticação  
**Responsável:** Rafael

**Descrição:**
Criar a migration Flyway para a tabela de usuários.

**Critérios de aceite:**
- [ ] Arquivo `V1__create_users.sql` criado com o schema correto (ver doc `07-modelo-de-dados.md`)
- [ ] Migration executa sem erro ao subir o Spring Boot
- [ ] Índice em `email` criado
- [ ] Constraint UNIQUE em `email` criada

---

### ISSUE #8 — Entidade e repository de usuário (Spring Boot)

**Labels:** `feature` `backend-java`  
**Milestone:** v0.2 — Autenticação  
**Responsável:** Rafael

**Descrição:**
Criar a entidade JPA `User` e o `UserRepository` com Spring Data.

**Critérios de aceite:**
- [ ] Classe `User.java` com `@Entity` mapeando todos os campos da tabela
- [ ] `UserRepository.java` extends `JpaRepository<User, UUID>`
- [ ] Método `findByEmail(String email)` no repository
- [ ] Lombok configurado (`@Data`, `@Builder`, `@NoArgsConstructor`, `@AllArgsConstructor`)
- [ ] Testes unitários básicos para o repository funcionam

---

### ISSUE #9 — Endpoint de cadastro (Spring Boot)

**Labels:** `feature` `backend-java`  
**Milestone:** v0.2 — Autenticação  
**Responsável:** Rafael

**Descrição:**
Implementar `POST /api/auth/register` conforme o contrato de API.

**Critérios de aceite:**
- [ ] Endpoint aceita `{ name, email, password }`
- [ ] Valida campos obrigatórios com Bean Validation
- [ ] Retorna 409 se e-mail já cadastrado
- [ ] Senha armazenada com bcrypt (salt rounds 12)
- [ ] Retorna 201 com token JWT e dados do usuário
- [ ] Testado no Insomnia/Postman
- [ ] Testes unitários no `AuthServiceTest.java`

**Contexto técnico:**
Ver `08-contrato-de-api.md` para o contrato exato da rota.

---

### ISSUE #10 — Configurar JWT (Spring Boot)

**Labels:** `feature` `backend-java`  
**Milestone:** v0.2 — Autenticação  
**Responsável:** Rafael

**Descrição:**
Implementar a geração e validação de JWT no Spring Boot.

**Critérios de aceite:**
- [ ] Dependência `jjwt` adicionada ao `pom.xml`
- [ ] `JwtService.java` com métodos `generateToken(User user)` e `validateToken(String token)`
- [ ] JWT contém: `sub` (UUID do usuário), `name`, `email`, `iat`, `exp`
- [ ] Expiração configurada via `app.jwt.expiration-days` no `application.properties`
- [ ] Chave secreta lida de variável de ambiente `JWT_SECRET`
- [ ] Spring Security configurado para validar JWT em todas as rotas privadas
- [ ] Testes unitários para geração e validação de token

**Contexto técnico:**
Ver `06-integracao-java-node.md` — o payload do JWT precisa ser idêntico ao que o Node.js vai validar.

---

### ISSUE #11 — Endpoint de login (Spring Boot)

**Labels:** `feature` `backend-java`  
**Milestone:** v0.2 — Autenticação  
**Responsável:** Rafael

**Descrição:**
Implementar `POST /api/auth/login`.

**Critérios de aceite:**
- [ ] Endpoint aceita `{ email, password }`
- [ ] Verifica e-mail e senha com bcrypt
- [ ] Retorna 401 com mensagem genérica em caso de falha
- [ ] Retorna 200 com token JWT e dados do usuário em caso de sucesso
- [ ] Testado no Insomnia

---

### ISSUE #12 — Endpoint de perfil (Spring Boot)

**Labels:** `feature` `backend-java`  
**Milestone:** v0.2 — Autenticação  
**Responsável:** Rafael

**Descrição:**
Implementar `GET /api/users/me` e `PUT /api/users/me`.

**Critérios de aceite:**
- [ ] `GET /api/users/me` retorna os dados do usuário autenticado
- [ ] `PUT /api/users/me` atualiza nome e avatarUrl
- [ ] Ambas as rotas exigem JWT válido
- [ ] Retorna 401 se token ausente ou inválido

---

### ISSUE #13 — Tela de cadastro (React)

**Labels:** `feature` `frontend`  
**Milestone:** v0.2 — Autenticação  
**Responsável:** Kauã

**Descrição:**
Criar a tela de cadastro com formulário e integração com a API.

**Critérios de aceite:**
- [ ] Campos: nome, e-mail, senha, confirmar senha
- [ ] Validação no frontend antes de enviar (campos obrigatórios, e-mails válidos, senhas iguais, mínimo 8 chars)
- [ ] Integração com `POST /api/auth/register`
- [ ] Loading state durante a requisição
- [ ] Mensagem de erro vinda da API exibida para o usuário
- [ ] Ao cadastrar com sucesso, token salvo no localStorage e redirecionamento para o dashboard
- [ ] Design responsivo com TailwindCSS

---

### ISSUE #14 — Tela de login (React)

**Labels:** `feature` `frontend`  
**Milestone:** v0.2 — Autenticação  
**Responsável:** Kauã

**Descrição:**
Criar a tela de login com formulário e integração com a API.

**Critérios de aceite:**
- [ ] Campos: e-mail e senha
- [ ] Integração com `POST /api/auth/login`
- [ ] Loading state durante a requisição
- [ ] Mensagem de erro genérica em caso de falha
- [ ] Ao logar com sucesso, token salvo no localStorage e redirecionamento para o dashboard
- [ ] Link "Não tem conta? Cadastre-se" para a tela de cadastro
- [ ] Design responsivo

---

### ISSUE #15 — Contexto de autenticação e rotas protegidas (React)

**Labels:** `feature` `frontend`  
**Milestone:** v0.2 — Autenticação  
**Responsável:** Kauã

**Descrição:**
Implementar o contexto de autenticação e proteger rotas privadas no React.

**Critérios de aceite:**
- [ ] `AuthContext` criado com `user`, `token`, `login()`, `logout()`
- [ ] Token lido do localStorage ao iniciar a aplicação
- [ ] Componente `PrivateRoute` que redireciona para `/login` se não autenticado
- [ ] Axios configurado com interceptor para enviar o token em todas as requisições
- [ ] Logout remove token do localStorage e redireciona para login
- [ ] Botão de logout acessível no menu

---

### ISSUE #16 — Validar JWT no Node.js

**Labels:** `feature` `backend-node`  
**Milestone:** v0.2 — Autenticação  
**Responsável:** Kauã

**Descrição:**
Configurar o middleware de autenticação JWT no servidor Node.js para que o chat só funcione para usuários autenticados.

**Critérios de aceite:**
- [ ] Middleware `authenticateToken` criado em `src/middleware/auth.js`
- [ ] Valida o token do handshake do Socket.IO usando a mesma `JWT_SECRET` do Spring Boot
- [ ] Rejeita conexões sem token ou com token inválido com mensagem de erro
- [ ] `socket.userId` e `socket.userName` disponíveis após autenticação
- [ ] Testes unitários para o middleware

**Contexto técnico:**
Ver `06-integracao-java-node.md` — seção "Como o Node.js valida o JWT".

---

## MILESTONE v0.3 — Biblioteca

---

### ISSUE #17 — Migration: tabela books

**Labels:** `feature` `backend-java`  
**Milestone:** v0.3 — Biblioteca  
**Responsável:** Rafael

**Descrição:**
Criar a migration para a tabela de livros.

**Critérios de aceite:**
- [ ] `V2__create_books.sql` criado com o schema correto
- [ ] Foreign key para `users` com `ON DELETE CASCADE`
- [ ] Índice em `user_id`
- [ ] Migration executa sem erro

---

### ISSUE #18 — CRUD de livros (Spring Boot)

**Labels:** `feature` `backend-java`  
**Milestone:** v0.3 — Biblioteca  
**Responsável:** Rafael

**Descrição:**
Implementar as rotas de gerenciamento da biblioteca pessoal.

**Critérios de aceite:**
- [ ] `GET /api/books` lista livros do usuário autenticado com paginação
- [ ] `GET /api/books` suporta query params `search`, `favorites`, `page`, `size`
- [ ] `POST /api/books` cria novo livro (campos obrigatórios validados)
- [ ] `PATCH /api/books/:id/favorite` alterna estado de favorito
- [ ] `DELETE /api/books/:id` deleta livro (apenas se pertencer ao usuário)
- [ ] Retorna 403 se usuário tentar manipular livro de outro usuário
- [ ] Testes unitários para `BookService`

---

### ISSUE #19 — Tela de biblioteca (React)

**Labels:** `feature` `frontend`  
**Milestone:** v0.3 — Biblioteca  
**Responsável:** Kauã

**Descrição:**
Criar a tela de biblioteca pessoal com listagem e busca de livros.

**Critérios de aceite:**
- [ ] Grid de cards com capa, título, autor e porcentagem de progresso
- [ ] Busca em tempo real por título ou autor (debounce 300ms)
- [ ] Botão de favorito em cada card com feedback visual
- [ ] Filtro para exibir apenas favoritos
- [ ] Paginação (carregar mais ou paginação numérica)
- [ ] Estado vazio com CTA para adicionar o primeiro livro
- [ ] Loading skeleton durante carregamento

---

### ISSUE #20 — Modal de adicionar livro (React)

**Labels:** `feature` `frontend`  
**Milestone:** v0.3 — Biblioteca  
**Responsável:** Kauã

**Descrição:**
Criar o modal/formulário para cadastrar um novo livro.

**Critérios de aceite:**
- [ ] Campos: título, autor, total de páginas, URL da capa (opcional)
- [ ] Validação antes de enviar
- [ ] Preview da capa se URL for fornecida
- [ ] Integração com `POST /api/books`
- [ ] Livro aparece na listagem imediatamente após criar (React Query invalidation)
- [ ] Feedback de sucesso e fechamento automático do modal

---

## MILESTONE v0.4 — Sessões

---

### ISSUE #21 — Migrations: tabelas sessions, session_members, reading_progress

**Labels:** `feature` `backend-java`  
**Milestone:** v0.4 — Sessões  
**Responsável:** Rafael

**Descrição:**
Criar as migrations para o módulo de sessões.

**Critérios de aceite:**
- [ ] `V3__create_sessions.sql` com código único gerado (ex: LIT-XXXX)
- [ ] `V4__create_session_members.sql` com constraint UNIQUE (session_id, user_id)
- [ ] `V5__create_reading_progress.sql` com constraint UNIQUE (session_id, user_id)
- [ ] Todas executam sem erro

---

### ISSUE #22 — Criar e entrar em sessão (Spring Boot)

**Labels:** `feature` `backend-java` `integration`  
**Milestone:** v0.4 — Sessões  
**Responsável:** Rafael

**Descrição:**
Implementar as rotas de criação e entrada em sessões.

**Critérios de aceite:**
- [ ] `POST /api/sessions` cria sessão com código único gerado automaticamente
- [ ] `POST /api/sessions/join` valida código, senha (se houver) e limite
- [ ] Retorna todos os erros corretos (401 senha errada, 404 não existe, 410 encerrada, 422 lotada)
- [ ] Host é automaticamente adicionado como participante ao criar
- [ ] `GET /api/sessions` lista sessões do usuário com status
- [ ] `GET /api/sessions/:id` retorna sessão com participantes e progresso
- [ ] Testes unitários para os casos de erro de `SessionService`

---

### ISSUE #23 — Encerrar sessão e gestão de participantes (Spring Boot)

**Labels:** `feature` `backend-java`  
**Milestone:** v0.4 — Sessões  
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] `PATCH /api/sessions/:id` permite host atualizar configurações
- [ ] `POST /api/sessions/:id/end` encerra a sessão (apenas host)
- [ ] `PUT /api/sessions/:id/progress` atualiza progresso do usuário
- [ ] Todas as rotas protegidas com JWT

---

### ISSUE #24 — Tela de criar sessão (React)

**Labels:** `feature` `frontend`  
**Milestone:** v0.4 — Sessões  
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] Formulário: selecionar livro da biblioteca, data início, data fim, senha opcional, limite opcional
- [ ] Seleção de livro com busca inline
- [ ] Integração com `POST /api/sessions`
- [ ] Após criar, redireciona para a sessão criada
- [ ] Exibe o código de convite gerado em destaque

---

### ISSUE #25 — Tela de entrar em sessão (React)

**Labels:** `feature` `frontend`  
**Milestone:** v0.4 — Sessões  
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] Campo para inserir o código de convite
- [ ] Se sessão tiver senha, campo de senha aparece
- [ ] Mensagens de erro específicas para cada caso (sessão não encontrada, lotada, encerrada)
- [ ] Integração com `POST /api/sessions/join`

---

### ISSUE #26 — Tela principal da sessão (React)

**Labels:** `feature` `frontend`  
**Milestone:** v0.4 — Sessões  
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] Exibe: capa e info do livro, lista de participantes com progresso, área do chat, timer Pomodoro
- [ ] Lista de participantes atualiza em tempo real (via WebSocket)
- [ ] Host vê botões de configuração e encerramento
- [ ] Input de progresso (página atual) com feedback visual ao salvar
- [ ] Layout responsivo para desktop e mobile

---

## MILESTONE v0.5 — Chat

---

### ISSUE #27 — Servidor de chat com Socket.IO (Node.js)

**Labels:** `feature` `backend-node`  
**Milestone:** v0.5 — Chat  
**Responsável:** Kauã

**Descrição:**
Implementar o servidor de chat em tempo real.

**Critérios de aceite:**
- [ ] Evento `join_session` — entra na room da sessão e recebe histórico
- [ ] Evento `leave_session` — sai da room
- [ ] Evento `send_message` — salva no Redis e emite para todos na room
- [ ] Redis armazena as últimas 50 mensagens por sessão (LPUSH + LTRIM)
- [ ] Evento `chat_history` emitido ao entrar com as 50 mensagens
- [ ] Evento `new_message` emitido para todos na room ao receber mensagem
- [ ] Mensagem em branco ou > 500 chars rejeitada
- [ ] Testes unitários para os handlers

**Contexto técnico:**
Ver `06-integracao-java-node.md` — seção de eventos WebSocket.

---

### ISSUE #28 — Componente de chat (React)

**Labels:** `feature` `frontend`  
**Milestone:** v0.5 — Chat  
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] Conexão Socket.IO com autenticação JWT no handshake
- [ ] Emite `join_session` ao entrar na tela de sessão
- [ ] Recebe `chat_history` e exibe as mensagens anteriores
- [ ] Recebe `new_message` e adiciona ao final do chat
- [ ] Input para digitar mensagem — Enter envia, Shift+Enter quebra linha
- [ ] Scroll automático para mensagem mais recente
- [ ] Exibe nome e timestamp de cada mensagem
- [ ] Reconexão automática se a conexão cair

---

### ISSUE #29 — Notificações de presença (Node.js + React)

**Labels:** `feature` `backend-node` `frontend`  
**Milestone:** v0.5 — Chat  
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] Node.js emite `user_joined` quando alguém entra na sessão
- [ ] Node.js emite `user_left` quando alguém desconecta
- [ ] Frontend exibe notificação discreta no chat ("Kauã entrou na sessão")
- [ ] Lista de participantes atualiza em tempo real

---

## MILESTONE v0.6 — Pomodoro e Streak

---

### ISSUE #30 — Migrations: pomodoro_records e reading_streaks

**Labels:** `feature` `backend-java`  
**Milestone:** v0.6 — Pomodoro  
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] `V6__create_pomodoro_records.sql` criado
- [ ] `V7__create_reading_streaks.sql` com constraint UNIQUE (user_id, streak_date)
- [ ] Ambas executam sem erro

---

### ISSUE #31 — Timer Pomodoro (Node.js)

**Labels:** `feature` `backend-node`  
**Milestone:** v0.6 — Pomodoro  
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] Evento `start_pomodoro` — inicia timer e armazena estado no Redis
- [ ] Emite `pomodoro_tick` a cada segundo com tempo restante
- [ ] Evento `pause_pomodoro` — pausa o timer
- [ ] Evento `resume_pomodoro` — retoma o timer
- [ ] Ao completar: emite `pomodoro_completed` e chama `POST /api/streak/record` no Spring Boot
- [ ] Estado do timer sincronizado entre abas do mesmo usuário
- [ ] Testes unitários

---

### ISSUE #32 — Endpoint de registro de streak (Spring Boot)

**Labels:** `feature` `backend-java`  
**Milestone:** v0.6 — Pomodoro  
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] `POST /api/streak/record` recebe `{ userId, completedAt, sessionId, durationSeconds }`
- [ ] Cria ou incrementa registro em `reading_streaks` para a data do dia
- [ ] Cria registro em `pomodoro_records`
- [ ] `GET /api/users/:id/streak` retorna streak atual, recorde e array de calendário
- [ ] Testes unitários para o cálculo de streak

---

### ISSUE #33 — Componente de timer Pomodoro (React)

**Labels:** `feature` `frontend`  
**Milestone:** v0.6 — Pomodoro  
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] Display do timer em destaque (MM:SS)
- [ ] Botões: Iniciar, Pausar, Retomar
- [ ] Progresso circular ou barra de progresso
- [ ] Sinal sonoro ao completar (configurável para silenciar)
- [ ] Animação de celebração ao completar um Pomodoro
- [ ] Integração com os eventos do Socket.IO

---

### ISSUE #34 — Calendário de streak (React)

**Labels:** `feature` `frontend`  
**Milestone:** v0.6 — Pomodoro  
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] Grid visual de semanas (inspirado no contribution graph do GitHub)
- [ ] Dias coloridos conforme intensidade (1 Pomodoro = claro, 4+ = escuro)
- [ ] Exibe streak atual e recorde
- [ ] Navegação por mês
- [ ] Tooltip ao passar o mouse mostrando data e número de Pomodoros
- [ ] Integração com `GET /api/users/:id/streak`

---

## MILESTONE v0.7 — Progresso e Rodízio

---

### ISSUE #35 — Migrations: progress_history e chooser_history

**Labels:** `feature` `backend-java`  
**Milestone:** v0.7 — Progresso  
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] `V8__create_reading_progress_history.sql` criado
- [ ] `V9__create_chooser_history.sql` com constraint UNIQUE (session_id, month)
- [ ] Ambas executam sem erro

---

### ISSUE #36 — Histórico de progresso (Spring Boot)

**Labels:** `feature` `backend-java`  
**Milestone:** v0.7 — Progresso  
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] `PUT /api/sessions/:id/progress` também cria registro em `reading_progress_history`
- [ ] `GET /api/sessions/:id/progress/history` retorna histórico do usuário autenticado
- [ ] Testes unitários

---

### ISSUE #37 — Sistema de rodízio mensal (Spring Boot + React)

**Labels:** `feature` `backend-java` `frontend` `integration`  
**Milestone:** v0.7 — Progresso  
**Responsável:** Rafael (back) + Kauã (front)

**Critérios de aceite:**
- [ ] Ordem de rodízio definida por ordem de entrada na sessão
- [ ] `current_chooser_user_id` atualizado automaticamente no início de cada mês
- [ ] `GET /api/sessions/:id` retorna quem é o escolhedor atual
- [ ] Histórico em `chooser_history`
- [ ] Frontend exibe claramente quem escolhe o livro este mês
- [ ] Apenas o escolhedor atual pode alterar o livro da sessão

---

### ISSUE #38 — Calendário de sessões (React)

**Labels:** `feature` `frontend`  
**Milestone:** v0.7 — Progresso  
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] Visualização mensal de todas as sessões ativas do usuário
- [ ] Eventos coloridos por status (ativa, futura, encerrada)
- [ ] Clique em evento leva para a sessão
- [ ] Navegação por mês
- [ ] Integração com `GET /api/sessions`

---

## MILESTONE v1.0 — Polimento e MVP

---

### ISSUE #39 — Testes unitários Backend Java (cobertura mínima)

**Labels:** `test` `backend-java`  
**Milestone:** v1.0 — MVP  
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] Cobertura de testes em `AuthService`, `SessionService`, `StreakService` acima de 80%
- [ ] Todos os testes passam no GitHub Actions
- [ ] Cenários de erro cobertos (404, 401, 403, 409)

---

### ISSUE #40 — Testes unitários Backend Node.js

**Labels:** `test` `backend-node`  
**Milestone:** v1.0 — MVP  
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] Testes para middleware de autenticação JWT
- [ ] Testes para handlers de chat (mensagem vazia, mensagem muito longa)
- [ ] Testes para lógica do Pomodoro
- [ ] Todos passam no GitHub Actions

---

### ISSUE #41 — Tratamento global de erros (Spring Boot)

**Labels:** `feature` `backend-java`  
**Milestone:** v1.0 — MVP  
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] `@ControllerAdvice` global trata exceções e retorna JSON padronizado
- [ ] Formato: `{ "error": "CODIGO_ERRO", "message": "Descrição legível", "timestamp": "..." }`
- [ ] Nunca retorna stack trace em produção
- [ ] 404, 401, 403, 409, 422 todos com respostas padronizadas

---

### ISSUE #42 — Rate limiting nas rotas de auth (Spring Boot)

**Labels:** `feature` `backend-java` `segurança`  
**Milestone:** v1.0 — MVP  
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] Máximo 10 tentativas de login por minuto por IP
- [ ] Máximo 5 cadastros por minuto por IP
- [ ] Retorna 429 Too Many Requests ao exceder

---

### ISSUE #43 — Configurar CORS em produção (Spring Boot)

**Labels:** `feature` `backend-java` `infra`  
**Milestone:** v1.0 — MVP  
**Responsável:** Rafael

**Critérios de aceite:**
- [ ] CORS configurado para aceitar apenas o domínio da Vercel em produção
- [ ] Em desenvolvimento, aceita `localhost:5173`
- [ ] Configuração via variável de ambiente `CORS_ALLOWED_ORIGINS`

---

### ISSUE #44 — Página de erro 404 e loading states (React)

**Labels:** `feature` `frontend`  
**Milestone:** v1.0 — MVP  
**Responsável:** Kauã

**Critérios de aceite:**
- [ ] Página 404 com botão para voltar ao início
- [ ] Todos os estados de loading têm skeleton ou spinner
- [ ] Todos os estados de erro têm mensagem legível e ação de retry
- [ ] Estado vazio tratado em todas as listas

---

### ISSUE #45 — Testes end-to-end do fluxo principal

**Labels:** `test` `integration`  
**Milestone:** v1.0 — MVP  
**Responsável:** Kauã e Rafael

**Critérios de aceite:**
- [ ] Fluxo completo testado manualmente: cadastro → login → criar sessão → entrar → chat → Pomodoro → streak
- [ ] Todos os critérios de aceite das issues de RF-001 a RF-020 verificados
- [ ] Testado em Chrome e Firefox
- [ ] Testado em mobile (responsive)
- [ ] Deploy de produção testado com os dois usuários simultaneamente

---

### ISSUE #46 — Documentação final e README

**Labels:** `docs`  
**Milestone:** v1.0 — MVP  
**Responsável:** Kauã e Rafael

**Critérios de aceite:**
- [ ] README.md atualizado com instruções de setup funcionando
- [ ] Todos os documentos da pasta `/docs` revisados e atualizados
- [ ] Seção "Como usar" no README com screenshots
- [ ] `.env.example` atualizado em todos os serviços

---

## Resumo — total de issues por milestone

| Milestone | Issues | Estimativa |
|---|---|---|
| v0.1 — Esqueleto | #1 a #6 | 1 sprint |
| v0.2 — Autenticação | #7 a #16 | 2 sprints |
| v0.3 — Biblioteca | #17 a #20 | 2 sprints |
| v0.4 — Sessões | #21 a #26 | 3 sprints |
| v0.5 — Chat | #27 a #29 | 2 sprints |
| v0.6 — Pomodoro | #30 a #34 | 3 sprints |
| v0.7 — Progresso | #35 a #38 | 2 sprints |
| v1.0 — MVP | #39 a #46 | 2 sprints |
| **Total** | **46 issues** | **~17 sprints** |
