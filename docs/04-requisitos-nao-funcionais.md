# Requisitos não funcionais

Os requisitos não funcionais definem como o sistema se comporta — não o que ele faz, mas com qual qualidade faz. Para um projeto de aprendizado em free tier, o foco é no que é viável e realista.

---

## RNF-001 — Performance

**Prioridade:** Alta

- Tempo de resposta das rotas REST deve ser menor que 500ms para 90% das requisições em condições normais
- Mensagens de chat devem ser entregues em menos de 500ms
- O frontend deve carregar (First Contentful Paint) em menos de 3 segundos em conexão 4G
- Queries ao banco de dados devem usar índices nas colunas de busca frequente (e-mail, session_code, user_id)

Limitações do free tier que afetam performance:

- Railway free tier hiberna containers após 15 minutos de inatividade — o primeiro request após hibernação pode levar até 30 segundos (cold start). Isso é aceitável para MVP.
- Redis no free tier tem memória limitada — dados de Pomodoro e chat são efêmeros por design.

---

## RNF-002 — Segurança

**Prioridade:** Alta

- Todas as rotas privadas exigem JWT válido no header `Authorization: Bearer <token>`
- Senhas armazenadas com bcrypt (salt rounds: 12)
- Tokens JWT com expiração de 7 dias, assinados com chave secreta em variável de ambiente
- CORS configurado para aceitar apenas a origem do frontend em produção
- Dados sensíveis (JWT_SECRET, DATABASE_URL, REDIS_URL) nunca vão para o repositório — apenas em variáveis de ambiente
- Arquivo `.env` no `.gitignore` desde o primeiro commit
- Rate limiting básico nas rotas de login e cadastro (máx 10 tentativas por minuto por IP) — usando Spring Boot `@RateLimiter` ou middleware no Express

---

## RNF-003 — Disponibilidade

**Prioridade:** Média

- Objetivo de uptime: 95% (equivalente a ~36 horas de downtime por mês)
- Deploy na Railway com restart automático em caso de crash
- Health check endpoint em ambos os backends: `GET /health` retorna `{ "status": "ok" }`
- GitHub Actions notifica via commit status se o deploy falhar

---

## RNF-004 — Escalabilidade

**Prioridade:** Baixa (MVP)

- O sistema foi projetado para suportar até 50 usuários simultâneos no free tier
- Escalabilidade horizontal não é requisito do MVP — arquitetura desacoplada já facilita escalar cada serviço independentemente no futuro
- Redis como camada de cache e estado já prepara a arquitetura para crescimento

---

## RNF-005 — Manutenibilidade

**Prioridade:** Alta (projeto de aprendizado)

- Código comentado em português quando a lógica não for óbvia
- Nenhum arquivo deve ter mais de 300 linhas — se ultrapassar, refatorar
- Nomes de variáveis, funções e classes em inglês (padrão de mercado)
- Commits em português no imperativo ("Adiciona rota de login", "Corrige validação de e-mail")
- Nenhum `console.log` de debug no código mergeado para `main`
- Cada PR deve ter no máximo 400 linhas de alteração — PRs maiores são divididos

---

## RNF-006 — Usabilidade

**Prioridade:** Média

- Interface responsiva — funciona em desktop e mobile
- Feedback visual para todas as ações do usuário (loading states, mensagens de erro, confirmações)
- Mensagens de erro em português e orientativas ("E-mail já cadastrado. Tente fazer login.")
- Estados vazios com instrução clara ("Você ainda não tem livros. Adicione o primeiro!")
- O Pomodoro e o chat devem funcionar mesmo com conexão instável — reconexão automática via Socket.IO

---

## RNF-007 — Testabilidade

**Prioridade:** Média

- Backend Java: testes unitários com JUnit 5 para as regras de negócio críticas (cálculo de progresso, validação de sessão)
- Backend Node: testes básicos com Jest para os handlers de WebSocket
- Frontend: testes de componentes críticos com Vitest + React Testing Library
- Todos os testes rodam no GitHub Actions a cada push

---

## RNF-008 — Portabilidade e ambiente

**Prioridade:** Alta

- O projeto deve rodar localmente com um único comando: `docker compose up`
- `docker-compose.yml` na raiz sobe PostgreSQL e Redis para desenvolvimento local
- Variáveis de ambiente documentadas em `.env.example` na raiz de cada serviço
- Node.js versão mínima: 20 LTS
- Java versão mínima: 21 LTS
