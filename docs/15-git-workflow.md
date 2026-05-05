# Git e GitHub — workflow completo para iniciantes

> Você vai usar Git todos os dias neste projeto. Este documento ensina tudo que precisa saber, do conceito básico ao fluxo real de trabalho em dupla.

---

## Por que Git existe

Imagine escrever código sem Git: você salva `projeto_v1.js`, `projeto_v2.js`, `projeto_final.js`, `projeto_final_de_verdade.js`. Você perde o histórico de mudanças, não consegue trabalhar em paralelo com outra pessoa e não tem como voltar atrás se algo quebrar.

Git resolve tudo isso. Ele:
- Salva o histórico completo de cada mudança com data, autor e descrição
- Permite trabalhar em paralelo (você na sua branch, Rafael na dele) sem conflito
- Permite voltar para qualquer ponto do histórico se algo quebrar
- Facilita a revisão de código antes de integrar ao projeto

---

## Conceitos fundamentais

### Repositório (repo)
A pasta do projeto rastreada pelo Git. Tudo dentro dela tem seu histórico controlado.

### Commit
Uma "foto" do estado do código em um momento. Cada commit tem:
- Um hash único (ex: `a3f9b2c`)
- Uma mensagem descritiva ("Adiciona rota de login")
- O autor
- A data e hora
- As mudanças em relação ao commit anterior

### Branch (ramo)
Uma linha independente de desenvolvimento. A branch principal chama `main`. Quando você começa uma feature, cria uma nova branch — assim suas mudanças não interferem no que está funcionando.

```
main:        A → B → C → D → E
                      ↑
feature:              C → F → G
```

Quando a feature fica pronta, ela é integrada de volta para `main` via Pull Request.

### Remote (remoto)
O repositório que fica no GitHub (servidor). Seu repositório local e o remoto se sincronizam via `push` e `pull`.

### Staging area
Uma área intermediária entre os arquivos modificados e o commit. Você escolhe quais arquivos entram no próximo commit usando `git add`.

---

## Comandos do dia a dia — referência completa

### Configuração inicial (uma vez só)

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"
git config --global init.defaultBranch main
git config --global pull.rebase true
```

### Clonar um repositório

```bash
git clone git@github.com:usuario/litcircle.git
cd litcircle
```

### Ver o estado atual

```bash
git status          # quais arquivos foram modificados
git log             # histórico de commits
git log --oneline   # histórico resumido (uma linha por commit)
git diff            # o que mudou nos arquivos ainda não commitados
git diff --staged   # o que vai no próximo commit
```

### Fluxo básico de trabalho

```bash
# 1. Atualizar a branch main local com o que está no GitHub
git checkout main
git pull origin main

# 2. Criar uma branch para sua tarefa
git checkout -b feature/rf-001-cadastro-usuario

# 3. Trabalhar... editar arquivos...

# 4. Ver o que mudou
git status

# 5. Adicionar arquivos ao staging (escolher o que vai no commit)
git add src/componentes/Cadastro.jsx    # arquivo específico
git add src/                            # pasta inteira
git add .                               # tudo que mudou (use com cuidado)

# 6. Fazer o commit
git commit -m "feat: adiciona formulário de cadastro"

# 7. Publicar a branch no GitHub
git push origin feature/rf-001-cadastro-usuario

# 8. Repetir passos 3-7 quantas vezes precisar
```

### Manter sua branch atualizada com a main

Quando alguém mergeia um PR enquanto você está trabalhando, sua branch fica desatualizada. Atualize antes de abrir o PR:

```bash
git fetch origin
git rebase origin/main

# Se tiver conflitos, o Git vai parar e mostrar os arquivos conflitantes
# Resolva os conflitos (explicado abaixo)
# Depois:
git add arquivo-resolvido.js
git rebase --continue

# Depois do rebase, force push é necessário
git push --force-with-lease origin feature/rf-001-cadastro-usuario
```

### Desfazer coisas

```bash
# Desfazer mudanças em um arquivo (antes do git add)
git checkout -- nome-do-arquivo.js

# Desfazer o git add (tirar do staging)
git reset HEAD nome-do-arquivo.js

# Desfazer o último commit (mantém as mudanças nos arquivos)
git reset --soft HEAD~1

# Desfazer o último commit (apaga as mudanças — CUIDADO)
git reset --hard HEAD~1

# Ver o que tinha em um commit específico
git show a3f9b2c
```

---

## O fluxo completo do projeto — do início ao merge

### Etapa 1: Pegar uma issue

1. Vá no GitHub Projects
2. Encontre a issue que vai trabalhar na coluna "A fazer"
3. Se atribua à issue (Assignees → seu usuário)
4. Mova a issue para a coluna "Fazendo"

### Etapa 2: Criar a branch

```bash
# Sempre a partir da main atualizada
git checkout main
git pull origin main

# Crie a branch com o padrão: tipo/rf-XXX-descricao
git checkout -b feature/rf-001-cadastro-usuario
```

### Etapa 3: Desenvolver com commits pequenos

Não espere terminar tudo para commitar. Commite a cada mudança lógica completa:

```bash
# Após criar o formulário HTML
git add src/pages/Cadastro.jsx
git commit -m "feat: cria estrutura do formulário de cadastro"

# Após adicionar a validação
git add src/pages/Cadastro.jsx
git commit -m "feat: adiciona validação de e-mail e senha no frontend"

# Após conectar com a API
git add src/pages/Cadastro.jsx src/services/auth.js
git commit -m "feat: conecta formulário com endpoint de cadastro da API"
```

### Etapa 4: Publicar e abrir o Pull Request

```bash
# Atualizar com a main antes de abrir PR
git fetch origin
git rebase origin/main

# Publicar
git push origin feature/rf-001-cadastro-usuario
```

No GitHub:
1. Acesse o repositório
2. O GitHub vai sugerir "Compare & pull request" — clique
3. Preencha o título seguindo o padrão: `feat: implementa cadastro de usuário (RF-001)`
4. Preencha o corpo com o template (ver doc 11-guia-de-contribuicao.md)
5. Em "Reviewers", adicione o parceiro
6. Em "Development", vincule a issue: escreva `Closes #1` no corpo do PR
7. Clique em "Create pull request"
8. Mova a issue para "Em revisão" no board

### Etapa 5: Responder ao code review

O parceiro vai comentar no PR. Para cada mudança solicitada:

```bash
# Faça as alterações nos arquivos
# Commite:
git add arquivo-corrigido.js
git commit -m "fix: corrige validação de e-mail conforme revisão"

# Publique:
git push origin feature/rf-001-cadastro-usuario
```

O PR atualiza automaticamente. Responda aos comentários no GitHub explicando o que mudou.

### Etapa 6: Merge

Após aprovação do parceiro:
1. Clique em "Squash and merge" (não "Merge commit" — squash mantém o histórico limpo)
2. Ajuste a mensagem do commit final se necessário
3. Clique em "Confirm squash and merge"
4. Clique em "Delete branch" (botão que aparece após o merge)
5. Mova a issue para "Concluído" no board

### Etapa 7: Limpar localmente

```bash
git checkout main
git pull origin main
git branch -d feature/rf-001-cadastro-usuario
```

---

## Resolvendo conflitos — passo a passo

Conflitos acontecem quando você e o Rafael editam o mesmo trecho de código. O Git não sabe qual versão manter — você precisa decidir.

### Como um conflito aparece

```bash
git rebase origin/main
# CONFLICT (content): Merge conflict in src/services/auth.js
```

Abra o arquivo conflitante. Você vai ver algo assim:

```javascript
function login(email, password) {
<<<<<<< HEAD (sua mudança)
  return axios.post('/api/auth/login', { email, password, rememberMe: true });
=======
  return axios.post('/api/auth/login', { email, password });
>>>>>>> origin/main (mudança que veio da main)
}
```

### Como resolver

1. **Entenda o conflito:** leia as duas versões e decida qual manter (ou combine as duas)
2. **Edite o arquivo:** remova as marcações `<<<<<<<`, `=======`, `>>>>>>>` e deixe o código como deve ficar:

```javascript
function login(email, password, rememberMe = false) {
  return axios.post('/api/auth/login', { email, password, rememberMe });
}
```

3. **Marque como resolvido:**
```bash
git add src/services/auth.js
git rebase --continue
```

4. Se houver outros conflitos, repita o processo para cada arquivo.

**Dica:** Se o conflito for muito complexo e você não souber como resolver, pare e chame o parceiro. Nunca resolva um conflito no chute.

---

## Comandos avançados que você vai precisar

### Ver diferença entre branches

```bash
git diff main..feature/rf-001-cadastro-usuario
```

### Salvar trabalho temporariamente sem commitar (stash)

Útil quando você precisa trocar de branch mas não quer perder mudanças em progresso:

```bash
# Salvar o trabalho atual
git stash

# Trocar de branch, fazer o que precisar...

# Recuperar o trabalho salvo
git stash pop
```

### Ver quem mudou cada linha de um arquivo

```bash
git blame src/services/auth.js
```

### Criar tag para uma versão

```bash
# Quando terminar a milestone v0.2, por exemplo:
git tag v0.2 -m "Autenticação completa"
git push origin v0.2
```

---

## Erros comuns e como resolver

**"Permission denied (publickey)"**
Sua chave SSH não está configurada no GitHub. Reveja a seção de SSH do doc 14-setup-ambiente.md.

**"Your branch is ahead of 'origin/main' by X commits"**
Você tem commits locais que ainda não foram para o GitHub. Faça `git push`.

**"Your branch is behind 'origin/main'"**
A main no GitHub está mais à frente que a sua local. Faça `git pull origin main`.

**"error: failed to push some refs"**
Alguém fez push enquanto você estava trabalhando. Faça `git fetch origin` e depois `git rebase origin/main` antes de tentar o push novamente.

**"detached HEAD state"**
Você foi para um commit específico sem criar uma branch. Crie uma branch para salvar onde está: `git checkout -b minha-branch-de-recuperacao`.

**"fatal: not a git repository"**
Você está na pasta errada. Use `cd litcircle` para entrar na pasta do projeto.

---

## Boas práticas de commit — guia rápido

### O que faz um bom commit

Um bom commit tem uma mensagem que responde: "Se eu aplicar este commit, ele vai **\_\_\_**".

Bom: "Adiciona validação de senha no formulário de cadastro"  
Ruim: "changes", "fix", "wip", "atualiza codigo"

### Commits pequenos vs grandes

Prefira commits pequenos e frequentes. Um commit por mudança lógica. Se você está com medo de commitar porque "não terminou ainda", commite mesmo assim — você está em uma branch, nada vai para `main` sem PR.

### O que nunca commitar

- Arquivos `.env` (contêm senhas e tokens)
- `node_modules/` ou `target/` (dependências geradas)
- Arquivos de IDE (`.idea/`, `.vscode/` — exceto o `settings.json` compartilhado)
- `console.log` de debug
- Código comentado que não serve mais

Se você acidentalmente commitou um `.env`:
```bash
# Remover do histórico e do tracking
git rm --cached .env
git commit -m "chore: remove .env do tracking"
# Trocar IMEDIATAMENTE todos os segredos que estavam no .env
```

---

## GitHub Projects — como usar no dia a dia

### Configurar o board inicial

1. Vá no repositório → aba "Projects" → "New project"
2. Selecione "Board" (kanban)
3. Crie as colunas: Backlog, A fazer, Fazendo, Em revisão, Concluído

### Configurar o template de issues

1. No repositório, vá em `Settings → General → Features → Issues`
2. Clique em "Set up templates"
3. Clique em "Add template: custom"
4. Cole o template de issue que está no doc 13-metodologia.md

### Criar uma issue

1. Aba "Issues" → "New issue"
2. Preencha com o template
3. Adicione labels relevantes
4. Adicione à Milestone correspondente
5. Adicione ao Project (board)

### Vincular PR a issue automaticamente

No corpo do PR, escreva uma dessas frases (o GitHub fecha a issue automaticamente no merge):
```
Closes #42
Fixes #42
Resolves #42
```

### Shortcut: criar issue direto do board

No board do GitHub Projects, clique em "+ Add item" na coluna "A fazer". Assim a issue já nasce dentro da sprint certa.
