# LitCircle
> Um sistema de clube de leitura colaborativo construído do zero para consolidar fundamentos de engenharia de software, arquitetura Full-Stack e integração de APIs.

---

## Sobre o projeto

O LitCircle é o resultado prático de uma imersão focada na metodologia *Learning by Doing*. O sistema opera de forma totalmente desacoplada, separando as responsabilidades de interface (Front-end) e servidor (Back-end), simulando a arquitetura e a cultura de uma equipe real de desenvolvimento de software.

O LitCircle resolve um problema real: pessoas que leem juntas não têm uma ferramenta única que una sessões de leitura sincronizadas, rastreamento de progresso, chat em tempo real e construção de hábito com streak. O projeto nasce dessa dor.

---

## Ecossistema de desenvolvimento

### Planejamento e design

- **Excalidraw** — brainstorming, fluxogramas de lógica e desenhos iniciais de arquitetura
- **Figma** — prototipagem de baixa fidelidade para definir a interface antes do código
- **dbdiagram.io** — modelagem visual do banco de dados e seus relacionamentos

### Execução e stack técnica

- **Frontend** — React + Vite + TailwindCSS
- **Backend principal** — Java 21 com Spring Boot 3 (Rafael)
- **Backend auxiliar / real-time** — Node.js + Express + Socket.IO (Kauã)
- **Banco de dados** — PostgreSQL (dados principais) + Redis (cache, sessões, real-time)
- **Testes de integração** — Insomnia ou Postman

### Gestão e organização

- **GitHub Projects** — quadro Kanban com regra WIP = 1, issues ilimitadas, milestones e roadmap
- **GitHub Wiki** — documentação técnica, ADRs e decisões de arquitetura
- **GitHub Actions** — CI/CD automatizado, 100% gratuito

---

## Arquitetura e fluxo de dados

```
[React Frontend]
      │
      ├── HTTP REST ──────► [Spring Boot API]  ──► [PostgreSQL]
      │                           │
      │                    (eventos internos)
      │                           │
      └── WebSocket ─────► [Node.js Service] ──► [Redis]
```

1. **Client-side (Frontend)** — captura as interações do usuário e gerencia o estado da interface
2. **A ponte REST** — dispara requisições HTTP enviando e recebendo dados JSON para o Spring Boot
3. **A ponte WebSocket** — mantém conexão persistente com o Node.js para chat e Pomodoro em tempo real
4. **Server-side Java** — recebe requisições REST, valida regras de negócio, persiste no PostgreSQL
5. **Server-side Node** — gerencia conexões WebSocket, estado de Pomodoro e mensagens de chat via Redis

---

## Como executar localmente

Pré-requisitos: Node.js 20+, Java 21+, Docker

```bash
# 1. Subir banco e Redis local
docker compose up -d

# 2. Backend Java (porta 8080)
cd backend-java
./mvnw spring-boot:run

# 3. Backend Node (porta 3001)
cd backend-node
npm install
npm run dev

# 4. Frontend (porta 5173)
cd frontend
npm install
npm run dev
```

Acesse: `http://localhost:5173`

---

## Documentação completa

| Documento | Conteúdo |
|---|---|
| [docs/01-manifesto.md](docs/01-manifesto.md) | Filosofia, regras, cultura e pacto da equipe |
| [docs/02-dor-e-solucao.md](docs/02-dor-e-solucao.md) | Problema que o software resolve, personas e contexto |
| [docs/03-requisitos-funcionais.md](docs/03-requisitos-funcionais.md) | Todas as funcionalidades detalhadas com critérios de aceite |
| [docs/04-requisitos-nao-funcionais.md](docs/04-requisitos-nao-funcionais.md) | Performance, segurança, escalabilidade, acessibilidade |
| [docs/05-stack-e-decisoes.md](docs/05-stack-e-decisoes.md) | Stack completa, justificativas e decisões de arquitetura (ADRs) |
| [docs/06-integracao-java-node.md](docs/06-integracao-java-node.md) | Como Spring Boot e Node.js se comunicam — guia completo |
| [docs/07-modelo-de-dados.md](docs/07-modelo-de-dados.md) | Entidades, relacionamentos e esquema do banco de dados |
| [docs/08-contrato-de-api.md](docs/08-contrato-de-api.md) | Todas as rotas REST e eventos WebSocket documentados |
| [docs/09-deploy.md](docs/09-deploy.md) | Deploy 100% gratuito: Railway, Vercel, GitHub Actions |
| [docs/10-gestao-de-projeto.md](docs/10-gestao-de-projeto.md) | GitHub Projects, kanban, milestones, fluxo de trabalho |
| [docs/11-guia-de-contribuicao.md](docs/11-guia-de-contribuicao.md) | Branches, commits, PRs, code review e regras de collab |

---

## Equipe

| Pessoa | Domínio principal | Domínio secundário |
|---|---|---|
| **Kauã** | Frontend (React, UI/UX) | Backend Node.js — chat, Pomodoro, real-time |
| **Raphael** | Backend Java (Spring Boot, PostgreSQL) | Revisão de integrações e contratos de API |

---

## Manifesto e cultura de engenharia

Este projeto obedece a um rigoroso código de cultura técnica, focado no autodidatismo, leitura de documentações primárias e esforço intelectual — com restrições estritas ao uso de IA generativa para código e ideação.

Para entender o fluxo Kanban, regras de code review e o modelo de liderança por domínio, leia na íntegra o [Manifesto de Engenharia](docs/01-manifesto.md).
