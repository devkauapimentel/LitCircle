# Guia de contribuição

Regras de como Kauã e Rafael colaboram no código: nomenclatura de branches, padrão de commits, processo de Pull Request e code review.

---

## Regra fundamental

**Ninguém faz push direto para `main`.** Todo código passa por uma branch, um Pull Request e aprovação do parceiro. Sem exceção, nem para "uma correção pequena".

---

## Branches

### Nomenclatura

```
tipo/rf-XXX-descricao-curta
```

Tipos:
- `feature` — nova funcionalidade
- `fix` — correção de bug
- `refactor` — refatoração sem mudança de comportamento
- `docs` — apenas documentação
- `test` — apenas testes
- `chore` — configuração, CI, dependências

Exemplos:

```bash
feature/rf-001-cadastro-usuario
feature/rf-015-chat-websocket
fix/rf-008-sessao-senha-incorreta
refactor/progress-service-extrair-metodo
docs/atualiza-contrato-api
chore/configura-github-actions
```

### Fluxo de branches

```
main
 └── feature/rf-001-cadastro-usuario
      │
      ├── commits de desenvolvimento
      │
      └── Pull Request → revisão → merge em main
```

Nunca crie branches a partir de outras branches de feature. Sempre a partir de `main`.

### Comandos básicos

```bash
# Criar branch a partir da main atualizada
git checkout main
git pull origin main
git checkout -b feature/rf-001-cadastro-usuario

# Publicar a branch no GitHub
git push -u origin feature/rf-001-cadastro-usuario

# Manter a branch atualizada com a main durante o desenvolvimento
git fetch origin
git rebase origin/main
```

---

## Padrão de commits

### Formato

```
tipo: descrição curta no imperativo

Corpo opcional com mais detalhes (quando necessário).

Referências: closes #42, refs #38
```

**A descrição curta:**
- Em português
- No imperativo: "Adiciona", não "Adicionado" ou "Adicionando"
- Sem ponto final
- Máximo 72 caracteres

**Tipos de commit:**
- `feat` — nova funcionalidade
- `fix` — correção de bug
- `refactor` — refatoração
- `test` — adicionar ou corrigir testes
- `docs` — documentação
- `chore` — configuração, ferramentas, dependências
- `style` — formatação, sem mudança de lógica

### Exemplos de bons commits

```
feat: adiciona endpoint POST /api/auth/login

fix: corrige validação de e-mail duplicado no cadastro

refactor: extrai lógica de cálculo de progresso para ProgressService

test: adiciona testes unitários para SessionService

docs: atualiza contrato de API com rota de streak

chore: adiciona workflow de CI para o backend Java

feat: implementa timer Pomodoro com Socket.IO

fix: corrige reconexão automática do WebSocket após timeout
```

### Exemplos de commits ruins (evitar)

```
Update                          ← sem contexto
fix bug                         ← qual bug?
wip                             ← não commitar work in progress
Adicionei o login               ← não é imperativo
feat: Added login endpoint      ← não está em português
```

### Tamanho dos commits

Commits pequenos e frequentes. Um commit deve representar uma mudança lógica coesa — não uma tarde inteira de trabalho. Se você está com medo de commitar porque "ainda não está pronto", commite em uma branch e rebase depois.

---

## Pull Requests

### Quando abrir um PR

Abra o PR quando a funcionalidade estiver completa segundo os critérios de aceite da issue. Não abra PR de work-in-progress — use `[WIP]` no título apenas se precisar de feedback antecipado em algo específico.

### Título do PR

Mesmo padrão dos commits:

```
feat: implementa chat em tempo real com Socket.IO (RF-015)
fix: corrige erro 403 ao entrar em sessão sem senha (RF-009)
```

### Template do corpo do PR

```markdown
## O que este PR faz

Descreva em 2-3 frases o que foi implementado ou corrigido.

## Issue relacionada

Closes #15

## Tipo de mudança

- [ ] Nova funcionalidade
- [ ] Correção de bug
- [ ] Refatoração
- [ ] Documentação

## Como testar

1. Passo 1
2. Passo 2
3. Resultado esperado

## Checklist

- [ ] Código funciona conforme os critérios de aceite da issue
- [ ] Testes escritos para a funcionalidade
- [ ] Sem `console.log` de debug no código
- [ ] Documentação atualizada se necessário (rotas novas, modelos novos)
- [ ] Self-review feito — li o meu próprio diff antes de abrir o PR
```

### Tamanho máximo de PR

Máximo 400 linhas alteradas por PR. Se for maior, divida em PRs menores. PRs grandes são difíceis de revisar e aumentam o risco de conflitos.

---

## Code review

### Quem revisa o quê

| Mudança | Revisor primário |
|---|---|
| Frontend (React, CSS) | **Kauã** |
| Backend Java (Spring Boot, PostgreSQL) | **Rafael** |
| Backend Node.js (WebSocket, Redis) | **Kauã** |
| Integração (JSON, rotas, regras de negócio) | **Ambos** |
| Documentação | Qualquer um |

O autor do PR não pode aprovar o próprio PR.

### O que o revisor verifica

**Corretude:**
- O código faz o que a issue pede?
- Os critérios de aceite foram atendidos?
- Tem algum caso extremo não tratado?

**Qualidade:**
- O código é fácil de entender?
- Os nomes fazem sentido?
- Tem repetição desnecessária?
- Tem `console.log` de debug esquecido?

**Segurança:**
- Algum segredo hardcoded?
- Inputs do usuário estão sendo validados?
- Rotas privadas estão protegidas com JWT?

**Padrões do projeto:**
- Nomenclatura de branch e commits seguem o padrão?
- O PR tem a issue referenciada?

### Como deixar um comentário de review

**Aprovação com sugestão:**
```
LGTM! Só uma sugestão: o nome `data` na linha 42 poderia ser
mais descritivo — algo como `sessionData` ou `sessionPayload`
deixaria mais claro o que está armazenado ali.
```

**Mudança obrigatória:**
```
BLOQUEADOR: essa rota está aceitando qualquer usuário autenticado,
mas deveria validar se o usuário é participante da sessão antes
de retornar os dados. Isso é uma falha de autorização.
```

**Pergunta:**
```
Por que você optou por armazenar isso no Redis em vez de calcular
na hora? Curiosidade genuína — querendo entender o raciocínio.
```

### SLA de revisão

- PR pequeno (até 100 linhas): revisar em até 24 horas
- PR médio (100-400 linhas): revisar em até 48 horas
- Se não conseguir revisar no prazo, avise o parceiro para não ficar esperando

### Merge

Após aprovação, o **autor do PR** faz o merge — não o revisor. Use "Squash and merge" para manter o histórico do `main` limpo.

Após o merge:
1. Delete a branch remota (GitHub tem um botão para isso)
2. Mova a issue para "Concluído" no board
3. Delete a branch local: `git branch -d feature/rf-001-cadastro-usuario`

---

## Resolução de conflitos

Se a sua branch tiver conflito com a `main`:

```bash
# Atualizar main local
git checkout main
git pull origin main

# Voltar para sua branch e fazer rebase
git checkout feature/sua-branch
git rebase origin/main

# Resolver conflitos nos arquivos marcados
# Após resolver cada arquivo:
git add arquivo-com-conflito.js
git rebase --continue

# Forçar push da branch após rebase
git push --force-with-lease origin feature/sua-branch
```

Nunca use `git merge main` na sua branch de feature — use sempre `rebase` para manter o histórico linear.

---

## Regras de ouro

1. Nunca force push em `main`
2. Nunca commite segredos ou `.env` no repositório
3. Nunca aprove seu próprio PR
4. Nunca mergee sem os testes do GitHub Actions passando
5. Sempre delete a branch após o merge
6. Sempre referencie a issue no PR (`Closes #XX`)
