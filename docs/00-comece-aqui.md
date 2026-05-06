# 🚦 COMECE AQUI — O Guia Completo

> Tudo que vocês precisam saber antes de escrever a primeira linha de código. Leiam juntos, na ordem, sem pular.

---

## 1. COMO TUDO FUNCIONA (sem Docker)

### "E se não rodar na máquina do Rafael?"

Sem Docker, cada um instala as ferramentas direto na máquina. Funciona? **Sim, funciona perfeitamente para 2 pessoas.** É assim que 99% dos projetos de faculdade e iniciantes funcionam.

**O que garante que funcione em todas as máquinas:**

| Mecanismo | O que faz |
|-----------|-----------|
| **Versões fixas** | Todos usam Node 20, Java 21, PostgreSQL 15. Doc [14-setup-ambiente.md](14-setup-ambiente.md) tem os comandos exatos |
| **`.env.example`** | Arquivo template com as variáveis. Cada um copia e preenche com seus dados locais |
| **`package.json`** e **`pom.xml`** | Travam as versões das dependências. `npm install` instala as mesmas libs em qualquer máquina |
| **Flyway (migrations)** | SQLs versionados que criam o banco igual em qualquer máquina. Rafael roda `V1__create_users.sql` e o banco dele fica idêntico ao seu |
| **README.md** | Tem o passo a passo de setup completo |

**Quando Docker faria falta?**
- Se tivessem 10+ devs com máquinas diferentes → não é o caso
- Se precisassem de Redis, RabbitMQ, etc → não no MVP
- Se quisessem deploy com 1 comando → Render.com resolve isso

**Quando vão adicionar Docker?**
Após o MVP funcionar. Aí criam um `docker-compose.yml` e qualquer pessoa clona e roda com `docker compose up`. Está no [PROJETOS-FUTUROS.md](../PROJETOS-FUTUROS.md) como Nível 3.

---

## 2. COMO APRENDER O QUE NÃO SABEM

### A regra de ouro: aprenda SOB DEMANDA

Não estudem 3 semanas antes de codar. O ciclo é:

```
1. Pega a issue do board
2. Lê 30-60 min da doc oficial da tech que precisa
3. Tenta implementar
4. Travou? → Busca na doc oficial → Tenta de novo
5. 45 min travado → Documenta → Chama o parceiro
6. Funcionou → Commit → PR → Próxima issue
```

### Mapa do que estudar e quando

#### Semana 0 (ANTES DE CODAR — 1 dia, 6h)

**Ambos fazem juntos:**

| O quê | Recurso | Tempo |
|-------|---------|-------|
| Git básico | [learngitbranching.js.org](https://learngitbranching.js.org) — faça TODOS os níveis "Main" | 1h |
| HTTP | [MDN HTTP Overview](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Overview) — GET, POST, PUT, DELETE, status codes | 1h |
| SQL básico | [sqlbolt.com](https://sqlbolt.com) — tutorial interativo completo | 2h |

**Kauã faz sozinho:**

| O quê | Recurso | Tempo |
|-------|---------|-------|
| JS moderno | [javascript.info](https://javascript.info) cap 4-11 — arrow functions, async/await, fetch | 2h |

**Rafael faz sozinho:**

| O quê | Recurso | Tempo |
|-------|---------|-------|
| Java básico | [dev.java/learn](https://dev.java/learn) — classes, objetos, interfaces | 3h |

#### Durante o projeto (QUANDO A ISSUE EXIGIR)

| Quando a issue pedir... | Estude isso... | Recurso | Tempo |
|-------------------------|----------------|---------|-------|
| Servidor HTTP (Node) | Express | [expressjs.com](https://expressjs.com) tutorial "Hello World" | 30min |
| REST API (Java) | Spring Boot | spring.io/guides "Building a REST Service" | 1h |
| Autenticação | JWT + bcrypt | jwt.io/introduction | 30min |
| Chat tempo real | Socket.IO | socket.io/docs/v4 "Get Started" | 1h |
| Banco (Java) | Spring Data JPA | spring.io/guides "Accessing Data with JPA" | 1h |
| CSS responsivo | Flexbox + Grid | css-tricks.com/guides | 30min |
| Migrations | Flyway | flywaydb.org quickstart | 30min |

**O guia completo com mais detalhes está em [12-guia-de-aprendizado.md](12-guia-de-aprendizado.md)**

---

## 3. GIT WORKFLOW — COMO TRABALHAR EM DUPLA

### "Eu não sei Git Workflow"

Tudo bem. O doc [15-git-workflow.md](15-git-workflow.md) explica **do zero** — conceitos, comandos, exemplos, erros comuns e como resolver conflitos. Leiam juntos.

### O resumo do fluxo (leiam o doc completo depois):

```
┌─────────────────────────────────────────────────┐
│  1. Pego issue do board (WIP = 1 por pessoa)    │
│  2. git checkout main && git pull               │
│  3. git checkout -b feature/nome-da-issue       │
│  4. Codar, testar                               │
│  5. git add . && git commit -m "feat: ..."      │
│  6. git push origin feature/nome-da-issue       │
│  7. Abro Pull Request no GitHub                 │
│  8. Parceiro revisa → aprova                    │
│  9. Merge na main → issue concluída             │
│  10. Próxima issue                              │
└─────────────────────────────────────────────────┘
```

### Regras inegociáveis

| Regra | Por quê |
|-------|---------|
| **Nunca commit na main** | Sempre via Pull Request |
| **WIP = 1** | Só 1 issue por pessoa ao mesmo tempo |
| **`.env` nunca vai pro git** | Use `.env.example` como template |
| **45 min travado → chama parceiro** | Não fique 4h no mesmo bug |
| **Todo PR precisa de review** | O outro lê e aprova antes do merge |

---

## 4. AS ISSUES — O QUE FAZER E EM QUAL ORDEM

### Todas as 26 issues já estão no GitHub (abertas)

Organizadas em 5 milestones na ordem certa:

### Milestone v0.1 — Esqueleto (Semana 1)

| # | Issue | Quem | O que é |
|---|-------|------|---------|
| #4 | Setup do repositório | Ambos | Estrutura de pastas pronta |
| #5 | Boilerplate frontend | Kauã | `index.html` com "Em construção" |
| #6 | Boilerplate backend Node | Kauã | Express + `GET /health` |
| #7 | Boilerplate backend Java | Rafael | Spring Boot + `GET /health` |
| #8 | PostgreSQL local | Ambos | Banco criado e rodando |

### Milestone v0.2 — Autenticação (Semanas 2-3)

| # | Issue | Quem | O que é |
|---|-------|------|---------|
| #9 | Migration: tabela users | Rafael | SQL que cria a tabela |
| #10 | Endpoint de cadastro | Rafael | `POST /api/auth/register` |
| #11 | Configurar JWT | Rafael | Gerar e validar tokens |
| #12 | Endpoint de login | Rafael | `POST /api/auth/login` |
| #13 | Tela de login | Kauã | HTML + fetch para API |
| #14 | Tela de cadastro | Kauã | HTML + fetch para API |
| #15 | Middleware JWT no Node | Kauã | Validar token no backend Node |

### Milestone v0.3 — Sessões (Semanas 4-5)

| # | Issue | Quem | O que é |
|---|-------|------|---------|
| #16 | Migrations sessions | Rafael | Tabelas sessions + session_members |
| #17 | Criar sessão | Rafael | `POST /api/sessions` |
| #18 | Entrar por código | Rafael | `POST /api/sessions/join` |
| #19 | Listar sessões | Rafael | `GET /api/sessions` |
| #20 | Atualizar progresso | Rafael | `PUT /api/sessions/:id/progress` |
| #21 | Tela Dashboard | Kauã | Lista de sessões do usuário |
| #22 | Tela Criar sessão | Kauã | Formulário |
| #23 | Tela Sessão de leitura | Kauã | Participantes + progresso |

### Milestone v0.4 — Chat (Semanas 6-7)

| # | Issue | Quem | O que é |
|---|-------|------|---------|
| #24 | Migration messages | Rafael | Tabela messages |
| #25 | Socket.IO servidor | Kauã | Chat em tempo real no Node |
| #26 | Chat no frontend | Kauã | Interface de chat com WebSocket |

### Milestone v0.5 — Deploy + Polish (Semana 8)

| # | Issue | Quem | O que é |
|---|-------|------|---------|
| #27 | Deploy Render.com | Ambos | 3 serviços + banco online |
| #28 | Teste end-to-end | Ambos | 2 usuários reais testando |
| #29 | Loading states e erros | Kauã | UX polish |

---

## 5. SESSÕES DE LEITURA — O QUE LER JUNTOS

### Sessão 1 — Entender o projeto (30 min)

| Ordem | Documento | Tempo | O que vão entender |
|-------|-----------|-------|---------------------|
| 1 | **[README.md](../README.md)** | 10 min | Visão geral, arquitetura, quem faz o quê |
| 2 | **[01-manifesto.md](01-manifesto.md)** | 10 min | Regras da dupla, cultura |
| 3 | **[03-requisitos-funcionais.md](03-requisitos-funcionais.md)** | 5 min | As 7 funcionalidades do MVP |
| 4 | **[05-stack-e-decisoes.md](05-stack-e-decisoes.md)** | 5 min | Tecnologias e por quê |

**Resultado:** vocês sabem O QUE vão construir e COM O QUE.

### Sessão 2 — Entender a técnica (30 min)

| Ordem | Documento | Tempo | O que vão entender |
|-------|-----------|-------|---------------------|
| 5 | **[06-integracao-java-node.md](06-integracao-java-node.md)** | 10 min | Como Java e Node conversam |
| 6 | **[07-modelo-de-dados.md](07-modelo-de-dados.md)** | 10 min | As 4 tabelas do banco |
| 7 | **[08-contrato-de-api.md](08-contrato-de-api.md)** | 10 min | Todas as rotas e eventos |

**Resultado:** vocês entendem COMO as peças se encaixam.

### Sessão 3 — Preparar para codar (30 min)

| Ordem | Documento | Tempo | O que vão entender |
|-------|-----------|-------|---------------------|
| 8 | **[14-setup-ambiente.md](14-setup-ambiente.md)** | 10 min | Instalar tudo (façam juntos ao vivo) |
| 9 | **[15-git-workflow.md](15-git-workflow.md)** | 15 min | Branches, PRs, conflitos |
| 10 | **[18-cronograma.md](18-cronograma.md)** | 5 min | O que fazer cada semana |

**Resultado:** vocês sabem O QUE FAZER AMANHÃ.

### Não precisam ler agora (consultam quando precisar)

| Documento | Quando consultar |
|-----------|-----------------|
| [09-deploy.md](09-deploy.md) | Semana 8, quando forem deployar |
| [11-guia-de-contribuicao.md](11-guia-de-contribuicao.md) | Quando fizerem o primeiro PR |
| [12-guia-de-aprendizado.md](12-guia-de-aprendizado.md) | Quando travarem em algo técnico |
| [16-glossario.md](16-glossario.md) | Quando não entenderem um termo |
| [19-wireframes.md](19-wireframes.md) | Quando forem construir as telas |

---

## 6. METODOLOGIA — O DIA A DIA

```
SEGUNDA (15 min): Cada um pega 1 issue do board
DIÁRIO  (5 min):  WhatsApp: "fiz X, vou fazer Y, travei em Z"
DOMINGO (15 min): Mostra o que fez → planeja próxima semana
```

### GitHub Projects — Board Kanban

```
┌──────────┬──────────┬───────────┬───────────┐
│ Backlog  │ Fazendo  │ Revisão   │ Concluído │
│          │ (máx 1)  │ (PR)      │           │
└──────────┴──────────┴───────────┴───────────┘
```

> **IMPORTANTE:** O board no GitHub Projects precisa ser configurado por vocês. Vá em github.com/devkauapimentel/LitCircle → aba "Projects" → New project → Board → Crie as colunas acima → Adicione as issues.

---

## 7. CHECKLIST ANTES DE CODAR

Depois de ler todos os docs, vocês devem conseguir responder:

- [ ] O que o LitCircle faz?
- [ ] Quais tecnologias usamos e por quê?
- [ ] O que o Spring Boot faz vs o que o Node.js faz?
- [ ] Quantas tabelas tem no banco e quais são?
- [ ] Como os dois backends se comunicam?
- [ ] O que é uma branch, um commit e um PR?
- [ ] Como funciona sem Docker e por que tá tudo bem?
- [ ] Qual é a minha primeira issue?
- [ ] Onde busco ajuda quando travar?

---

## 8. RESUMO — O CAMINHO COMPLETO

```
FASE 0 — AGORA (1 dia)
├── Leiam os docs juntos (3 sessões de 30 min)
├── Instalem o ambiente (doc 14)
├── Estudem Git (learngitbranching.js.org, 1h)
├── Estudem SQL (sqlbolt.com, 2h)
├── Kauã: JS moderno (javascript.info, 2h)
└── Rafael: Java básico (dev.java/learn, 3h)

FASE 1 — MVP (8 semanas)
├── Semana 1:  Issues #4-#8 (boilerplate)
├── Semana 2-3: Issues #9-#15 (autenticação)
├── Semana 4-5: Issues #16-#23 (sessões)
├── Semana 6-7: Issues #24-#26 (chat)
└── Semana 8:  Issues #27-#29 (deploy)

FASE 2 — EVOLUÇÃO (depois do MVP)
├── React no frontend
├── Docker para empacotamento
├── Testes automatizados
└── Ver PROJETOS-FUTUROS.md
```

**Primeiro passo literal: abram um terminal e façam o setup do doc [14-setup-ambiente.md](14-setup-ambiente.md).**
