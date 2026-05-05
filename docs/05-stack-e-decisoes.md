# Stack e decisões de arquitetura

---

## Stack completa

### Frontend

| Tecnologia | Versão | Papel |
|---|---|---|
| React | 18+ | Framework de UI — componentes, estado, roteamento |
| Vite | 5+ | Build tool — dev server rápido, bundle otimizado |
| TailwindCSS | 3+ | Estilização utilitária — sem CSS files separados |
| React Router | 6+ | Roteamento client-side (SPA) |
| Axios | 1+ | HTTP client para chamadas REST ao Spring Boot |
| Socket.IO Client | 4+ | WebSocket para chat e Pomodoro em tempo real |
| React Query | 5+ | Cache de dados do servidor, estados de loading/error |

**Dono:** Kauã

### Backend Java

| Tecnologia | Versão | Papel |
|---|---|---|
| Java | 21 LTS | Linguagem principal do backend |
| Spring Boot | 3+ | Framework — REST, segurança, DI, configuração |
| Spring Security + JWT | — | Autenticação e autorização |
| Spring Data JPA | — | ORM — mapeamento objeto-relacional |
| Hibernate | 6+ | Implementação do JPA |
| PostgreSQL | 15+ | Banco de dados relacional principal |
| Flyway | — | Migrations de banco de dados versionadas |
| Maven | 3+ | Gerenciamento de dependências e build |
| JUnit 5 | — | Testes unitários |

**Dono:** Rafael

### Backend Node.js

| Tecnologia | Versão | Papel |
|---|---|---|
| Node.js | 20 LTS | Runtime JavaScript no servidor |
| Express | 4+ | Framework HTTP — rotas e middlewares |
| Socket.IO | 4+ | WebSocket para chat e Pomodoro |
| ioredis | 5+ | Cliente Redis — estado de Pomodoro e mensagens |
| jsonwebtoken | 9+ | Validação de JWT (mesmo segredo do Spring Boot) |
| Jest | 29+ | Testes unitários e de integração |

**Dono:** Kauã

### Infraestrutura e dados

| Tecnologia | Papel |
|---|---|
| PostgreSQL 15 | Banco principal — usuários, livros, sessões, progresso, streaks |
| Redis 7 | Cache e estado real-time — mensagens de chat, estado do Pomodoro, sessões ativas |
| Docker + Docker Compose | Ambiente local padronizado para ambos os bancos |

### Deploy (100% gratuito)

| Serviço | O que hospeda | Free tier |
|---|---|---|
| Vercel | Frontend React | Ilimitado para projetos pessoais |
| Railway | Spring Boot + Node.js + PostgreSQL + Redis | US$ 5/mês de crédito gratuito mensal |
| GitHub Actions | CI/CD — testes e deploy automático | 2000 minutos/mês gratuitos |

### Ferramentas de desenvolvimento

| Ferramenta | Uso |
|---|---|
| GitHub Projects | Kanban, issues, milestones, roadmap |
| GitHub Wiki | Documentação técnica e ADRs |
| Excalidraw | Diagramas de arquitetura e brainstorming |
| Figma | Protótipos de interface |
| dbdiagram.io | Modelagem visual do banco de dados |
| Insomnia / Postman | Testes manuais de API |

---

## Decisões de arquitetura (ADRs)

Um ADR (Architecture Decision Record) documenta uma decisão técnica importante: o contexto, as opções consideradas, a decisão tomada e as consequências. É a memória técnica do projeto.

---

### ADR-001 — Dois backends separados (Java + Node.js)

**Data:** início do projeto  
**Status:** Aceito

**Contexto:** Rafael domina Java e quer aprofundar Spring Boot. Kauã quer aprender backend sem precisar aprender Java do zero — e Node.js é natural para quem vem de JavaScript. Além disso, o chat em tempo real com WebSocket é uma especialidade do Node.js (event loop não bloqueante).

**Decisão:** Manter dois servidores backend separados, cada um especializado:
- Spring Boot: regras de negócio, autenticação, CRUD principal, banco relacional
- Node.js: WebSocket em tempo real, Pomodoro, chat, Redis

**Consequências positivas:**
- Cada pessoa evolui na sua stack sem depender do outro para subir o ambiente
- Node.js é mais adequado para WebSocket do que Spring WebFlux (curva de aprendizado menor para quem vem de JS)
- Separação de responsabilidades clara

**Consequências negativas:**
- Dois serviços para deployar e manter
- Precisa de um mecanismo de comunicação entre os dois quando necessário (ver ADR-002)
- JWT precisa ser validado nos dois serviços com o mesmo segredo

---

### ADR-002 — Comunicação entre Java e Node via JWT compartilhado

**Data:** início do projeto  
**Status:** Aceito

**Contexto:** O Node.js precisa saber quem é o usuário que enviou uma mensagem de chat ou iniciou um Pomodoro. Mas o cadastro e login são feitos no Spring Boot.

**Decisão:** Usar JWT com segredo compartilhado. O Spring Boot emite o token no login. O Node.js valida o mesmo token usando a mesma chave secreta (variável de ambiente `JWT_SECRET` igual nos dois serviços). Nenhuma chamada entre os dois backends é necessária para autenticação.

**Alternativas consideradas:**
- Chamada HTTP do Node para o Spring Boot validar o token — descartada por criar acoplamento e latência
- Banco de sessões compartilhado no Redis — descartada por complexidade desnecessária no MVP

**Consequências:** A `JWT_SECRET` precisa ser idêntica nos dois serviços em produção. Documentada como variável de ambiente obrigatória.

---

### ADR-003 — Redis para estado real-time, PostgreSQL para persistência

**Data:** início do projeto  
**Status:** Aceito

**Contexto:** Mensagens de chat, estado do Pomodoro e lista de usuários ativos em uma sessão mudam constantemente. Salvar cada mudança no PostgreSQL causaria sobrecarga desnecessária.

**Decisão:**
- Redis armazena estado efêmero: mensagens recentes de chat (últimas 50 por sessão com TTL), estado do timer Pomodoro, usuários online
- PostgreSQL armazena dados permanentes: histórico de mensagens (após sessão encerrada), streaks, progresso de leitura, usuários, livros

**Consequências:** Mensagens de chat são perdidas se o Redis reiniciar antes de serem persistidas. Para o MVP, isso é aceitável. Em versão futura, implementar persistência assíncrona de mensagens no PostgreSQL via job no Node.js.

---

### ADR-004 — GitHub Projects como única ferramenta de gestão

**Data:** início do projeto  
**Status:** Aceito

**Contexto:** Avaliamos Linear, Notion e GitHub Projects. Restrição absoluta: 100% gratuito, sem limite de issues.

**Decisão:** GitHub Projects + Issues.

**Comparativo:**

| Critério | GitHub Projects | Linear | Notion |
|---|---|---|---|
| Issues | Ilimitadas | 250 no free | N/A |
| Kanban | Sim | Sim | Sim (manual) |
| Milestones | Sim | Sim | Manual |
| Integração com código | Nativa | Via integração | Não |
| Gratuito para sempre | Sim | Sim (com limite) | Sim (com limite) |
| Curva de aprendizado | Baixa | Baixa | Média |

**Consequências:** A documentação técnica fica na GitHub Wiki, não em ferramenta separada. Issues referenciam PRs e commits diretamente.

---

### ADR-005 — Deploy na Railway (não Render ou Heroku)

**Data:** início do projeto  
**Status:** Aceito

**Contexto:** Precisamos hospedar dois backends, um banco PostgreSQL e um Redis de forma gratuita.

**Decisão:** Railway com US$ 5/mês de crédito gratuito. É suficiente para os quatro serviços com uso moderado.

**Comparativo:**

| Serviço | PostgreSQL | Redis | Backend | Crédito gratuito |
|---|---|---|---|---|
| Railway | Sim | Sim | Sim | US$ 5/mês |
| Render | Sim | Sim | Sim | Instâncias hibernam, banco expira em 90 dias no free |
| Fly.io | Sim | Não nativo | Sim | Crédito mensal, mais complexo de configurar |
| Heroku | Sim (pago) | Pago | Sim | Sem free tier real desde 2022 |

**Consequências:** Se o projeto crescer e ultrapassar US$ 5/mês de uso, será necessário um plano pago. Para MVP com poucos usuários, o crédito é suficiente.
