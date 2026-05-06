# Metodologia de Aprendizado — Versão Final

> Duas trilhas paralelas. Uma não bloqueia a outra. Ponto.

---

## REGRAS DO PROJETO (inegociáveis)

### Ferramentas PERMITIDAS — lista fechada

| Ferramenta | Para quê | Link |
|-----------|----------|------|
| **Google** | Pesquisar problemas e erros | google.com (pesquise em inglês) |
| **MDN Web Docs** | Referência HTML/CSS/JS | developer.mozilla.org |
| **javascript.info** | Tutorial JavaScript completo | javascript.info |
| **expressjs.com** | Docs do Express | expressjs.com |
| **socket.io/docs** | Docs do Socket.IO | socket.io/docs/v4 |
| **spring.io/guides** | Guias do Spring Boot | spring.io/guides |
| **dev.java/learn** | Tutorial Java | dev.java/learn |
| **sqlbolt.com** | Aprender SQL | sqlbolt.com |
| **pgexercises.com** | Exercícios SQL | pgexercises.com |
| **Stack Overflow** | Perguntas de outros devs | stackoverflow.com (ler, não copiar) |
| **GitHub** (código de outros) | Ver como outros resolveram | github.com (ver estrutura, não copiar) |
| **learngitbranching.js.org** | Aprender Git | learngitbranching.js.org |
| **git-scm.com/book** | Pro Git Book (em PT) | git-scm.com/book/pt-br |
| **jwt.io** | Entender JWT | jwt.io/introduction |
| **css-tricks.com** | Guias de Flexbox/Grid | css-tricks.com |
| **Docs do repo** | Glossário, arquitetura, API | pasta `docs/` |
| **`man` / `--help`** | Comandos do terminal | terminal |
| **Console do navegador (F12)** | Debug, testar JS | navegador |
| **Rafael** (parceiro) | Após 45 min travado | Discord / GitHub Issues |

### Ferramentas PROIBIDAS (semanas 1-4)

| Ferramenta | Por quê |
|-----------|---------|
| **ChatGPT / Gemini / qualquer IA** | Cria dependência. Na 42 Piscine não tem. |
| **GitHub Copilot** | Autocomplete = você não pensou no código. |
| **Vídeo do YouTube como primeira opção** | Leia a doc ANTES. Vídeo é ÚLTIMO recurso. |
| **Copiar código do Stack Overflow** | Ler e entender = OK. Ctrl+C Ctrl+V = proibido. |
| **Pedir pra alguém fazer por você** | Nem parceiro, nem IA, nem amigo. |
| **Curso linear durante horário do projeto** | Rocketseat é trilha separada, horário separado. |

### Semana 5+: IA liberada com restrições

Após 4 semanas sem IA, pode usar COM estas regras:
- Só pra conceitos ("o que é X?"), nunca pra código
- Sempre peça que indique a doc oficial
- Se a IA deu a resposta e você não consegue refazer sozinho → não aprendeu

---

### Como pesquisar — O método exato

**Passo 1: Formule em inglês**

| Português | Inglês (use este) |
|-----------|-------------------|
| "como fazer formulário HTML" | `"html form tutorial"` |
| "como mandar dados pro servidor" | `"javascript fetch post example"` |
| "erro ao conectar no banco" | `"postgresql connection refused spring boot"` |
| "como reutilizar HTML" | `"vanilla javascript reusable components"` |

**Passo 2: Escolha a fonte certa**

```
PRIMEIRO resultado do Google que seja:
  1. MDN (developer.mozilla.org)     → MELHOR pra HTML/CSS/JS
  2. Stack Overflow (stackoverflow)  → MELHOR pra erros específicos
  3. Doc oficial da tecnologia       → MELHOR pra frameworks
  4. javascript.info                 → MELHOR pra JS detalhado
  5. Dev.to / Medium                 → OK pra tutoriais
  6. YouTube                         → ÚLTIMO RECURSO
```

**Passo 3: Leia, não assista**

Ler é mais rápido, mais preciso, e treina o skill de ler documentação técnica em inglês — que é o que a 42 exige.

Se REALMENTE não entendeu lendo → aí sim assista um vídeo CURTO (< 15 min) sobre o conceito específico.

**Passo 4: Para erros, Google o erro EXATO**

```
ERRADO: "erro javascript fetch"
CERTO:  "TypeError: Cannot read property 'json' of undefined"

ERRADO: "spring boot não conecta banco"  
CERTO:  "org.postgresql.util.PSQLException: Connection refused"
```

Copie a mensagem de erro EXATA entre aspas. O Google encontra quem já teve o mesmo erro.

---

### Quando NÃO sabe nem o que pesquisar

| Situação | Faça isso |
|----------|-----------|
| Não sei o termo técnico | Leia `docs/16-glossario.md` — tem todos os termos do projeto |
| Não sei o que a issue quer | Releia os critérios de aceite, palavra por palavra |
| Entendi a issue mas não sei por onde começar | Leia o ÍNDICE do tutorial da tecnologia (javascript.info, expressjs.com) |
| Li o índice e não achei | Google: "how to [o que a issue pede] in [linguagem]" |
| Google não ajudou | Stack Overflow: pesquise em inglês com tags `[javascript]` `[express]` |
| Nada funcionou (45 min) | Documenta na issue do GitHub → chama o Rafael |

## Suas 2 trilhas de estudo

```
TRILHA A — ROCKETSEAT (a faculdade)
├── Linear, no seu ritmo
├── Assistir, fazer exercícios, seguir o currículo
├── Horário fixo separado do projeto
└── Objetivo: base teórica ampla

TRILHA B — LITCIRCLE (o projeto 42)
├── Learning by doing, issue por issue
├── Não assiste nada antes — lê docs, pesquisa, faz
├── Horário fixo separado da Rocketseat
└── Objetivo: skill real aplicado
```

### Como se relacionam

| Situação | O que acontece |
|----------|---------------|
| Rocketseat ensinou fetch() antes da Issue #13 | Ótimo, você já sabe. Implementa mais rápido. |
| Issue #6 pede Express mas Rocketseat não cobriu | Tudo bem. Lê expressjs.com (30 min) e faz. |
| Rocketseat ensinou React | Ignora pro LitCircle. O MVP é HTML/CSS/JS. |
| Conceito aparece nas duas trilhas | Perfeito. Aprendeu 2x de formas diferentes = dominou. |

### A regra de ouro

**Uma trilha NUNCA bloqueia a outra.**

- Não espere a Rocketseat cobrir Express pra fazer a Issue #6.
- Não pare a Rocketseat porque o LitCircle tá puxado.
- São independentes. Se uma acelera a outra, é bônus — não dependência.

---

## TRILHA B — A metodologia 42 pro LitCircle

### Ferramentas permitidas (semanas 1-4)

| ✅ PODE | ❌ NÃO PODE |
|---------|-------------|
| Documentação oficial (MDN, spring.io, expressjs.com) | IA (ChatGPT, Copilot, etc.) |
| Google (pesquise o PROBLEMA em inglês) | Pedir código pra alguém |
| Stack Overflow (leia e entenda, não copie) | Copiar código sem entender cada linha |
| Glossário do repo (`16-glossario.md`) | Assistir vídeo antes de tentar |
| Parceiro (Rafael, após 45 min travado) | Ficar mais de 45 min sem pedir ajuda |
| javascript.info, sqlbolt.com, learngitbranching | Tutorial do YouTube como primeira opção |

### Como executar cada issue (o protocolo)

```
1. LER a issue (5 min)
   └── Critérios de aceite → marcar o que NÃO sei

2. PESQUISAR o que não sei (15-30 min)
   └── Doc oficial da tecnologia → ler 1 página relevante

3. OLHAR como outros fizeram (10 min)
   └── GitHub: "[tecnologia] example" → ver estrutura, NÃO copiar

4. CODAR (maior parte do tempo)
   └── Testar a cada 5 linhas → ler erros → console.log

5. REFATORAR (15 min)
   └── "Repeti algo?" → extrair │ "Confuso?" → renomear

6. ANOTAR na issue (2 min)
   └── Comentar no GitHub: "O que aprendi nessa issue"

7. PR → Review → Merge → Próxima
```

### O que te PROVA que aprendeu (avaliação 42)

Na 42, depois de terminar um projeto, outro aluno te avalia. Ele aponta pra qualquer linha do seu código e pergunta: **"o que isso faz e por que tá aí?"**

Faça isso com você mesmo. Depois de cada issue:

```
TESTE: feche o editor. Abra um arquivo novo.
Tente reescrever a parte principal do que fez SEM olhar.

Se conseguiu → dominou.
Se não conseguiu → volte e releia o que fez até entender cada linha.
```

Exemplos por issue:

| Issue | Teste 42 (faça SEM olhar seu código) |
|-------|--------------------------------------|
| #5 Boilerplate frontend | Crie um HTML com CSS variables e reset do zero |
| #6 Boilerplate Node | Crie um servidor Express com GET /health do zero |
| #13 Tela de login | Faça um formulário que faz fetch POST e trata erro |
| #15 JWT no Node | Escreva um middleware que valida JWT do zero |
| #25 Socket.IO | Crie um chat simples com Socket.IO do zero |

**Se consegue refazer do zero, você DOMINOU. Se só funciona porque copiou, você não aprendeu.**

---

## Como aprender cada tecnologia (pela trilha B)

A trilha B não tem "módulos". Você aprende sob demanda. Mas cada tecnologia tem um recurso primário e um exercício de validação.

### HTML

| O que aprender | Quando | Recurso | Tempo |
|---------------|--------|---------|-------|
| Tags básicas (div, h1, p, a, form, input, button) | Semana 0 | [MDN Learn HTML](https://developer.mozilla.org/pt-BR/docs/Learn/HTML) | 1h |
| Formulários completos | Issue #13/#14 | MDN: "Your first form" | 30 min |
| Semântica (header, main, nav) | Refatoração | MDN: "HTML elements reference" | Sob demanda |

**Exercício 42:** crie um formulário de login (email + senha + botão + link "cadastre-se") num HTML em branco. Sem olhar nada. Se funciona no navegador, você sabe HTML.

### CSS

| O que aprender | Quando | Recurso | Tempo |
|---------------|--------|---------|-------|
| Seletores, cores, fontes, box model | Semana 0 | [MDN Learn CSS](https://developer.mozilla.org/pt-BR/docs/Learn/CSS) | 1.5h |
| CSS Variables | Issue #5 | MDN: "Using CSS custom properties" | 15 min |
| Flexbox | Issue #13 (layout) | [Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) | 30 min |
| Grid | Issue #21 (dashboard) | [Grid Guide](https://css-tricks.com/snippets/css/complete-guide-grid/) | 30 min |

**Exercício 42:** estilize o formulário de login com a paleta do LitCircle (navy, purple, amber). Centralize na tela com Flexbox. Sem olhar nada. Se parece profissional, você sabe CSS.

### JavaScript

| O que aprender | Quando | Recurso | Tempo |
|---------------|--------|---------|-------|
| Variáveis, tipos, if/else, loops | Semana 0 | [javascript.info](https://javascript.info) cap 2 | 1h |
| Objetos e arrays | Semana 0 | javascript.info cap 4-5 | 1h |
| Funções, arrow functions | Semana 0 | javascript.info cap 6 | 30 min |
| DOM (querySelector, createElement, events) | Issue #5/#13 | javascript.info cap 13-14 | 1h |
| async/await, fetch | Issue #13 | javascript.info cap 11 + MDN Fetch | 1h |
| localStorage | Issue #13 | MDN: "Window.localStorage" | 15 min |
| Módulos (import/export) | Quando organizar código | javascript.info cap 13 "Modules" | 30 min |

**Exercício 42:** no console do navegador (F12), crie um array de 5 objetos `{nome, idade}`, filtre os maiores de 18, e mostre os nomes com `.map()`. Sem olhar nada.

### Node.js + Express

| O que aprender | Quando | Recurso | Tempo |
|---------------|--------|---------|-------|
| Servidor básico + rotas | Issue #6 | [expressjs.com](https://expressjs.com) "Hello World" + "Routing" | 1h |
| Middleware | Issue #15 | expressjs.com "Writing middleware" | 30 min |
| Socket.IO | Issue #25 | [socket.io/get-started](https://socket.io/get-started/chat) | 1h |

**Exercício 42:** crie um servidor Express do zero que responde JSON em 3 rotas diferentes. Sem olhar código anterior.

### SQL

| O que aprender | Quando | Recurso | Tempo |
|---------------|--------|---------|-------|
| SELECT, INSERT, UPDATE, DELETE, WHERE | Semana 0 | [sqlbolt.com](https://sqlbolt.com) | 2h |
| JOIN | Quando entender relações | sqlbolt.com lições 6-7 | 30 min |
| CREATE TABLE, constraints | Issue #8 | Doc 07-modelo-de-dados.md | 30 min |

**Exercício 42:** no psql, crie 2 tabelas relacionadas, insira dados, e faça um JOIN. Sem olhar nada.

### Git

| O que aprender | Quando | Recurso | Tempo |
|---------------|--------|---------|-------|
| commit, branch, merge, push, pull | Semana 0 | [learngitbranching.js.org](https://learngitbranching.js.org) | 1h |
| Rebase, conflitos | Quando acontecer | Doc 15-git-workflow.md | Sob demanda |

**Exercício 42:** crie um repo, faça 3 commits na main, crie uma branch, faça 2 commits lá, volte pra main, faça merge. Sem olhar nada.

---

## Cronograma das duas trilhas

```
HORÁRIO DO DIA (exemplo):

Manhã:    Rocketseat (trilha A) — 1-2h no ritmo do curso
Tarde:    LitCircle (trilha B) — 2-3h nas issues
Noite:    Livre / revisão / Rocketseat extra

OU (se pouco tempo):

Seg/Qua/Sex:  Rocketseat
Ter/Qui/Sab:  LitCircle
Dom:          Call com Rafael + revisão semanal
```

**O importante:** horários FIXOS pra cada trilha. Não misture. Quando é hora de Rocketseat, é Rocketseat. Quando é hora de LitCircle, é LitCircle.

---

## O resumo absoluto final

```
TRILHA A (Rocketseat):
  └── Linear, como faculdade. Segue o currículo. Horário fixo.

TRILHA B (LitCircle — estilo 42):
  ├── Semana 0: base mínima (JS, SQL, Git, HTTP) — 7h
  ├── Semanas 1-4: issues com docs + Google. ZERO IA.
  ├── Semana 5+: IA como colega socrático (se quiser).
  ├── Cada issue: ler → pesquisar → olhar exemplos → codar → refatorar → anotar
  ├── Depois de cada issue: teste 42 (refaz do zero sem olhar)
  └── Ferramentas: docs oficiais, Google em inglês, Stack Overflow, parceiro

AS DUAS NÃO SE BLOQUEIAM. NUNCA.
```
