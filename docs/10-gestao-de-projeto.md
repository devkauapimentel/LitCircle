# Gestão de projeto — GitHub Projects

Guia completo de como Kauã e Rafael organizam o trabalho usando exclusivamente ferramentas gratuitas do GitHub.

---

## Por que GitHub Projects

Avaliamos Linear, Notion e GitHub Projects. A decisão foi pelo GitHub Projects pelos seguintes motivos:

- Issues ilimitadas (Linear limita a 250 no free)
- Totalmente integrado ao código — issues referenciam commits e PRs automaticamente
- Kanban, roadmap e milestones sem custo adicional
- Zero curva de aprendizado para quem já usa GitHub
- Documentação técnica fica na GitHub Wiki, junto com o código

---

## Estrutura do board

O board principal fica em `github.com/SEU_USER/litcircle/projects`.

### Colunas do Kanban

| Coluna | Significado |
|---|---|
| **Backlog** | Ideias e funcionalidades futuras ainda não priorizadas |
| **A fazer** | Itens priorizados para a sprint atual, prontos para puxar |
| **Fazendo** | Em desenvolvimento — **máximo 1 por pessoa** (WIP = 1) |
| **Em revisão** | PR aberto, aguardando revisão do parceiro |
| **Concluído** | PR mergeado, critérios de aceite validados |

### Regra WIP = 1

Nunca mova um segundo item para "Fazendo" enquanto o primeiro não estiver em "Em revisão". Se você precisar trocar de contexto por dependência bloqueante, documente o bloqueio na issue com um comentário e avise o parceiro antes de puxar outra tarefa.

---

## Labels (etiquetas)

Use labels para classificar as issues rapidamente:

| Label | Cor | Uso |
|---|---|---|
| `feature` | Azul | Nova funcionalidade |
| `bug` | Vermelho | Comportamento incorreto |
| `refactor` | Amarelo | Melhoria de código sem mudança de comportamento |
| `docs` | Cinza | Documentação |
| `test` | Verde | Testes unitários ou de integração |
| `frontend` | Roxo | Toca apenas o React |
| `backend-java` | Laranja | Toca apenas o Spring Boot |
| `backend-node` | Verde escuro | Toca apenas o Node.js |
| `integration` | Rosa | Envolve os dois backends |
| `blocked` | Preto | Bloqueada por dependência |

---

## Milestones

Milestones representam entregas significativas do projeto:

| Milestone | Descrição |
|---|---|
| **v0.1 — Esqueleto** | Projeto inicializado, CI/CD rodando, deploy básico |
| **v0.2 — Autenticação** | Cadastro, login e JWT funcionando end-to-end |
| **v0.3 — Biblioteca** | CRUD de livros completo |
| **v0.4 — Sessões** | Criar e entrar em sessões, gestão de participantes |
| **v0.5 — Chat** | Chat em tempo real via WebSocket |
| **v0.6 — Pomodoro** | Timer Pomodoro e calendário de streak |
| **v0.7 — Progresso** | Progresso de leitura e rodízio de escolha |
| **v1.0 — MVP** | Todos os requisitos funcionais implementados e testados |

---

## Como escrever uma issue

Toda issue segue este template:

```markdown
## Descrição
O que precisa ser feito e por quê.

## Critérios de aceite
- [ ] Critério 1
- [ ] Critério 2
- [ ] Critério 3

## Contexto técnico (opcional)
Qual rota, qual componente, qual tabela do banco será afetada.

## Referências
Links para documentação relevante, ADRs, wireframes.
```

**Boas práticas ao criar issues:**
- Título no imperativo: "Implementa rota de login", não "Login"
- Uma issue, uma coisa — se a tarefa é grande demais, divida
- Sempre preencha os critérios de aceite — eles definem quando a issue está pronta
- Atribua a issue para si mesmo quando mover para "Fazendo"
- Associe a issue a uma Milestone

---

## Fluxo de trabalho semanal

### Segunda-feira — planejamento (30 min)

1. Revisar o que foi concluído na semana anterior
2. Mover itens do Backlog para "A fazer" conforme prioridade
3. Cada pessoa escolhe o que vai puxar primeiro
4. Alinhar dependências entre as tasks

### Dia a dia

1. Puxar uma issue de "A fazer" para "Fazendo" e se atribuir
2. Criar uma branch com o nome da issue: `feature/rf-015-chat-mensagens`
3. Desenvolver, fazer commits pequenos e frequentes
4. Quando pronto, abrir PR e mover a issue para "Em revisão"
5. Avisar o parceiro para revisar
6. Após aprovação e merge, mover para "Concluído"

### Sexta-feira — revisão (15 min)

1. Garantir que não há nada preso em "Em revisão" há mais de 2 dias
2. Atualizar o status das issues em andamento
3. Resolver qualquer issue marcada como `blocked`

---

## GitHub Wiki — documentação técnica

A GitHub Wiki do repositório é usada para documentação que muda com frequência e não faz sentido versionar via PR:

- Decisões de arquitetura (ADRs) novas
- Erros frequentes e como resolver (bug book)
- Aprendizados de cada sprint
- Guia de ambiente local para novos colaboradores

Para acessar: `github.com/SEU_USER/litcircle/wiki`

---

## Dicas de uso do GitHub Projects

**Criar issue rapidamente:** No board, clique em "+ Add item" na coluna "A fazer" e escreva o título. Depois abra a issue para preencher os detalhes.

**Vincular PR a issue:** No corpo do PR, escreva `Closes #42` para fechar a issue automaticamente quando o PR for mergeado.

**Filtrar por responsável:** No board, use o filtro "Assignee" para ver apenas suas issues.

**Roadmap view:** Além do Kanban, o GitHub Projects tem uma view de roadmap que mostra as milestones em linha do tempo. Útil para ver o progresso geral do projeto.
