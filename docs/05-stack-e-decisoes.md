# Stack e decisões de arquitetura

---

## Stack completa

### Frontend

| Tecnologia | Papel |
|-----------|-------|
| HTML5 | Estrutura das páginas |
| CSS3 | Estilização (Flexbox, Grid, variáveis CSS) |
| JavaScript ES6+ | Lógica, fetch API, manipulação do DOM |
| Socket.IO Client | WebSocket para chat em tempo real |

**Dono:** Kauã

**Por que não React?** Vocês não sabem React ainda. Aprender React + Spring Boot + Node.js + PostgreSQL + Git ao mesmo tempo é receita para travar. O frontend em HTML/CSS/JS puro funciona perfeitamente para o MVP. React entra no Nível 2 (após o MVP funcionar).

### Backend Java

| Tecnologia | Versão | Papel |
|-----------|--------|-------|
| Java | 21 LTS | Linguagem principal do backend |
| Spring Boot | 3+ | Framework REST, segurança, configuração |
| Spring Security + JWT | — | Autenticação e autorização |
| Spring Data JPA | — | ORM — mapeamento objeto-relacional |
| PostgreSQL | 15+ | Banco de dados relacional |
| Flyway | — | Migrations de banco versionadas |
| Maven | 3+ | Gerenciamento de dependências |

**Dono:** Rafael

### Backend Node.js

| Tecnologia | Versão | Papel |
|-----------|--------|-------|
| Node.js | 20 LTS | Runtime JavaScript no servidor |
| Express | 4+ | Framework HTTP |
| Socket.IO | 4+ | WebSocket para chat e presença |
| jsonwebtoken | 9+ | Validação de JWT (mesmo segredo do Spring Boot) |

**Dono:** Kauã

### Infraestrutura

| Tecnologia | Papel |
|-----------|-------|
| PostgreSQL 15 | Banco principal — instalado direto na máquina (sem Docker) |

### Deploy (100% gratuito)

| Serviço | O que hospeda | Free tier |
|---------|--------------|-----------|
| Render Static Site | Frontend HTML/CSS/JS | Ilimitado |
| Render Web Service | Spring Boot | Hiberna após 15min |
| Render Web Service | Node.js | Hiberna após 15min |
| Render PostgreSQL | Banco de dados | 1GB, recria a cada 90 dias |
| GitHub Actions | CI/CD automático | Ilimitado (repo público) |

### Ferramentas de desenvolvimento

| Ferramenta | Uso |
|-----------|-----|
| VSCode | Editor do Kauã (frontend + Node.js) |
| IntelliJ IDEA Community | IDE do Rafael (Java) |
| GitHub Projects | Kanban, issues, milestones |
| Thunder Client (VSCode) | Testes de API |
| Excalidraw | Diagramas e brainstorming |

---

## Decisões de arquitetura (ADRs)

### ADR-001 — Dois backends separados (Java + Node.js)

**Status:** Aceito

**Contexto:** Rafael quer aprofundar Java/Spring Boot. Kauã quer backend em JavaScript. Chat em tempo real é especialidade do Node.js (event loop não bloqueante).

**Decisão:** Dois servidores separados:
- Spring Boot: regras de negócio, autenticação, CRUD, banco relacional
- Node.js: WebSocket em tempo real, chat, presença

**Consequências positivas:**
- Cada pessoa evolui na sua stack sem depender do outro
- Separação de responsabilidades clara
- Se Rafael sair, Kauã migra as rotas REST pro Node.js

**Consequências negativas:**
- Dois serviços para deployar
- JWT precisa ser validado nos dois com o mesmo segredo

### ADR-002 — Frontend em HTML/CSS/JS puro (sem React)

**Status:** Aceito

**Contexto:** Kauã sabe HTML, CSS e JS básico. Aprender React simultaneamente com backend é over-engineering para o nível atual.

**Decisão:** Frontend em HTML/CSS/JS puro para o MVP v0. React é adicionado no Nível 2 como refatoração gradual.

**Consequências positivas:**
- Zero curva de aprendizado no frontend — foco no backend e integração
- Funciona em qualquer navegador sem build step
- Migração para React é gradual (cada página vira um componente)

### ADR-003 — PostgreSQL sem Docker

**Status:** Aceito

**Contexto:** Docker é uma ferramenta de infraestrutura. O foco agora é programação.

**Decisão:** PostgreSQL instalado direto na máquina de cada desenvolvedor. Docker entra no Nível 3 (após MVP funcionar).

### ADR-004 — Deploy no Render.com

**Status:** Aceito

**Contexto:** Precisa ser 100% gratuito e funcional para usuários reais.

**Decisão:** Render.com com free tier para todos os serviços.

| Critério | Render | Railway | Vercel |
|----------|--------|---------|--------|
| Frontend estático | Sim (ilimitado) | Sim | Sim |
| Backend Java | Sim | Sim | Não |
| Backend Node | Sim | Sim | Sim (serverless) |
| PostgreSQL grátis | Sim (1GB) | Sim ($5 crédito) | Não |
| Hibernação | 15min | 15min | N/A |
| Complexidade | Baixa | Média | Baixa |

### ADR-005 — Sem Redis no MVP

**Status:** Aceito

**Contexto:** Redis é cache e estado efêmero. Para o MVP com poucos usuários, o Node.js pode manter mensagens em memória.

**Decisão:** Mensagens de chat ficam em memória no Node.js durante a sessão. São persistidas no PostgreSQL via Spring Boot quando a sessão encerra. Redis entra no Nível 3.
