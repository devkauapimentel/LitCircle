# Metodologia de trabalho — como vamos operar

> Este documento define como Kauã e Rafael trabalham juntos do início ao fim do projeto. Leia antes de criar a primeira issue.

---

## A metodologia escolhida: Scrumban

Para dois iniciantes, Scrum puro (com sprints de 2 semanas, planning poker, retrospectiva formal) é burocracia demais. Kanban puro não tem cadência nem metas claras. A solução é **Scrumban**: o melhor dos dois mundos.

**Do Scrum pegamos:**
- Sprints com duração fixa (1 semana)
- Meta de sprint clara
- Retrospectiva rápida ao final de cada sprint

**Do Kanban pegamos:**
- Board visual com colunas
- WIP = 1 por pessoa (nunca mais de uma tarefa em "Fazendo")
- Fluxo contínuo dentro da sprint

---

## A sprint

### Duração
1 semana. Começa na segunda-feira, termina no domingo.

### Por que 1 semana e não 2?
Vocês são iniciantes. Duas semanas sem feedback é tempo demais para perceber que estão no caminho errado. Sprints de 1 semana forçam revisão frequente e corrigem o curso mais rápido.

### Meta da sprint
Toda sprint tem uma meta única e clara: uma frase que descreve o que será entregue. Exemplos:

- "O usuário consegue se cadastrar, fazer login e ver a tela inicial"
- "O usuário consegue criar uma sessão de leitura e convidar participantes"
- "O chat em tempo real funciona dentro de uma sessão"

A meta não é uma lista de tarefas. É um resultado. As tarefas existem para atingir a meta.

---

## As cerimônias

### 1. Planning — segunda-feira (30–45 minutos)

**Quando:** início de cada sprint  
**Participantes:** Kauã e Rafael  
**Formato:** pode ser síncrona (call) ou assíncrona (comentários no GitHub)

O que acontece:
1. Revisar o que foi concluído na sprint anterior (5 min)
2. Definir a meta da nova sprint (10 min)
3. Selecionar as issues do Backlog que vão para a sprint (10 min)
4. Quebrar as issues grandes em tarefas menores se necessário (10 min)
5. Cada um escolhe sua primeira tarefa e move para "A fazer" (5 min)

**Regra:** Nunca coloque mais issues na sprint do que vocês consigam fazer com conforto. É melhor terminar cedo e puxar mais do que não terminar e acumular dívida.

### 2. Daily check-in — todos os dias (10 minutos)

**Quando:** diariamente, no horário que funcionar para os dois  
**Formato:** assíncrono no GitHub ou em um canal de mensagem

Cada pessoa responde 3 perguntas:
1. O que eu fiz desde o último check-in?
2. O que vou fazer hoje?
3. Tem algum bloqueio?

Não precisa ser uma call. Um comentário rápido numa issue ou mensagem já resolve. O objetivo é visibilidade — ninguém trabalha no escuro.

### 3. Review — domingo (20 minutos)

**Quando:** fim de cada sprint  
**Participantes:** Kauã e Rafael  
**Formato:** síncrono (call ou presencial)

O que acontece:
1. Demonstração do que foi construído na sprint (10 min)
2. Verificar se a meta da sprint foi atingida (5 min)
3. Mover issues não concluídas de volta para o Backlog com contexto (5 min)

**Regra:** Só conta como "pronto" o que está mergeado em `main` e funcionando. Work-in-progress não conta.

### 4. Retrospectiva — domingo, logo após a review (15 minutos)

**Quando:** fim de cada sprint, depois da review  
**Formato:** pode ser assíncrono (cada um escreve antes da call)

Cada pessoa responde:
1. O que funcionou bem essa sprint que devemos repetir?
2. O que foi difícil ou atrasou o trabalho?
3. O que vamos tentar diferente na próxima sprint?

Registrar o resultado da retrospectiva como um comentário na issue da sprint ou na GitHub Wiki.

---

## O board do GitHub Projects

### Colunas

```
┌──────────┬──────────┬─────────────┬──────────────┬───────────┐
│ Backlog  │ A fazer  │   Fazendo   │ Em revisão   │ Concluído │
│          │ (sprint) │  (WIP = 1)  │   (PR aberto)│           │
└──────────┴──────────┴─────────────┴──────────────┴───────────┘
```

| Coluna | O que fica aqui |
|---|---|
| **Backlog** | Tudo que existe mas ainda não foi priorizado para uma sprint. Issues futuras, ideias, bugs descobertos. |
| **A fazer** | Issues selecionadas para a sprint atual. Prontas para serem puxadas. |
| **Fazendo** | Em desenvolvimento ativo. **Máximo 1 por pessoa.** Se você já tem algo aqui, não puxe mais nada. |
| **Em revisão** | PR aberto aguardando code review do parceiro. |
| **Concluído** | PR mergeado, critério de aceite validado. |

### Regra WIP = 1 — por que é tão importante

Contexto switching é o maior inimigo do aprendizado profundo. Quando você trabalha em duas coisas ao mesmo tempo como iniciante, você não termina nenhuma com entendimento real. A regra força você a resolver um problema completamente antes de ir para o próximo.

Se você travar em algo por mais de 45 minutos:
1. Documente o bloqueio na issue com um comentário
2. Aplique a Regra dos 45 Minutos do Manifesto
3. Se necessário, mova a issue para "Bloqueado" (label `blocked`) e chame o parceiro
4. Só então pegue outra tarefa — e documente que fez isso

---

## Planejamento das milestones

O projeto está dividido em 8 milestones. Cada milestone representa uma entrega funcionando de ponta a ponta.

### Estimativa de tempo por milestone

| Milestone | Conteúdo | Sprints estimadas | Prioridade |
|---|---|---|---|
| v0.1 — Esqueleto | Setup, CI/CD, deploy, boilerplate | 1 sprint | Crítica |
| v0.2 — Autenticação | Cadastro, login, JWT | 2 sprints | Crítica |
| v0.3 — Biblioteca | CRUD de livros, favoritos | 2 sprints | Alta |
| v0.4 — Sessões | Criar sessão, entrar, participantes | 3 sprints | Alta |
| v0.5 — Chat | WebSocket, mensagens em tempo real | 2 sprints | Alta |
| v0.6 — Pomodoro | Timer, streak, calendário | 3 sprints | Média |
| v0.7 — Progresso e rodízio | Progresso, calendário de sessões | 2 sprints | Média |
| v1.0 — Polimento MVP | Testes, bugs, deploy estável | 2 sprints | Alta |

**Total estimado: 17 sprints = ~4 meses** com dedicação de 8–10 horas por semana cada.

Se o ritmo for menor (4–5h/semana), planejar para 6–8 meses.

### Velocidade de sprint

Nas primeiras 3 sprints (v0.1 e início do v0.2), a velocidade vai ser baixa porque vocês ainda estão aprendendo as ferramentas. Isso é normal. Não se frustrem. A velocidade aumenta a partir da sprint 4.

---

## Como criar e gerenciar issues

### Quando criar uma issue

- Para toda funcionalidade nova (mesmo pequena)
- Para todo bug descoberto
- Para toda decisão técnica importante (aberta como discussão)
- Para todo item de documentação que precisa ser atualizado

**Nunca trabalhe em algo sem uma issue correspondente.** Se você está codando e não tem uma issue, crie uma antes de continuar.

### Tamanho ideal de uma issue

Uma issue deve ser completável em **1 a 3 dias de trabalho**. Se for maior, quebre em sub-issues.

Exemplos de issues bem dimensionadas:
- "Implementa endpoint POST /api/auth/register no Spring Boot"
- "Cria componente de formulário de cadastro no React"
- "Configura Socket.IO no servidor Node.js"

Exemplos de issues grandes demais (quebre em partes):
- "Implementa autenticação completa" — isso são 5 issues
- "Faz o chat" — isso são 4 issues

### Template de issue (configure no GitHub)

```markdown
## Descrição
O que precisa ser feito e por quê.

## Critérios de aceite
- [ ] Critério 1
- [ ] Critério 2
- [ ] Critério 3

## Contexto técnico
Qual rota REST, componente, tabela ou evento WebSocket está envolvido.
Referências para documentos relevantes do projeto (ex: ver doc 08-contrato-de-api.md).

## Definição de pronto
- [ ] Código funciona conforme os critérios de aceite
- [ ] Testes escritos
- [ ] Sem console.log de debug
- [ ] PR aprovado e mergeado
- [ ] Documentação atualizada se necessário
```

---

## Fluxo completo de uma tarefa — do backlog ao merge

```
1. PLANNING
   Issue está no Backlog
   ↓
   Durante a planning, issue é movida para "A fazer"

2. INÍCIO DO TRABALHO
   Você pega a issue: se atribui e move para "Fazendo"
   ↓
   Cria branch: git checkout -b feature/rf-001-cadastro-usuario

3. DESENVOLVIMENTO
   Commits pequenos e frequentes
   ↓
   Aplica Regra dos 45 min se travar
   ↓
   Daily check-in: reporta progresso

4. FINALIZAÇÃO
   Código pronto, critérios de aceite atendidos
   ↓
   Abre Pull Request com template preenchido
   ↓
   Move issue para "Em revisão"
   ↓
   Avisa o parceiro para revisar

5. CODE REVIEW
   Parceiro revisa dentro de 24–48h
   ↓
   Comentários → autor corrige → parceiro aprova

6. MERGE
   Autor faz merge (squash and merge)
   ↓
   Issue movida para "Concluído"
   ↓
   Branch deletada
```

---

## Regras de convivência técnica

**Sobre decisões técnicas:**
- Decisões no próprio domínio: o dono do domínio decide sozinho
- Decisões de integração: ambos decidem juntos — se não houver consenso em 30 minutos de discussão, abram uma issue de discussão e durmam com o problema antes de decidir

**Sobre bloqueios:**
- Travou por 45 min? Pare, documente, chame o parceiro
- Parceiro não está disponível? Continue explorando, mas documente tudo para quando ele voltar
- Bloqueio crítico que para o projeto? Sinalizar com label `blocked` e discutir na próxima daily

**Sobre qualidade:**
- Nada vai para `main` com os testes quebrando
- Nada vai para `main` com `console.log` de debug
- Nada vai para `main` sem code review
- Feito e funcionando sempre ganha de perfeito e incompleto

**Sobre ritmo:**
- Comunique antes se não vai conseguir trabalhar naquela semana
- Sprint não entregue não é fracasso — é sinal para ajustar o planejamento
- O projeto não tem prazo externo — o ritmo é de aprendizado, não de entrega

---

## Métricas de saúde do projeto

Verifiquem quinzenalmente:

| Métrica | Sinal de saúde | Sinal de alerta |
|---|---|---|
| Issues concluídas por sprint | Consistente ou crescendo | Caindo por 2+ sprints |
| Tempo de code review | Menos de 48h | Mais de 72h regularmente |
| Issues bloqueadas | 0 | 2+ simultaneamente |
| PRs sem review | 0 | Qualquer PR com mais de 3 dias sem revisão |
| Bugs em `main` | 0 | Qualquer bug que quebra funcionalidade existente |
