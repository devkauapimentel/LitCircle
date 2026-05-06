# Metodologia de Aprendizado — Estilo 42

> Como aprender programação do zero, dominar web dev, e usar a Rocketseat do jeito certo.

---

## A filosofia da 42 (adaptada pro LitCircle)

Na 42 não existe professor, não existe aula, não existe curso linear. Existe:

```
1. Um PROJETO com especificação clara (= as issues do LitCircle)
2. DOCUMENTAÇÃO oficial das tecnologias (= man pages, MDN, spring.io)
3. Seus COLEGAS (= Rafael, Stack Overflow)
4. SEU CÉREBRO (= a peça mais importante)
```

### A regra de ouro da 42:

**Você NÃO estuda pra depois fazer. Você FAZ e estuda o que precisa no caminho.**

```
ERRADO (escola tradicional):
  Assistir 40h de curso → tentar fazer projeto → travar → voltar pro curso

CERTO (42):
  Ler a issue → "o que preciso saber?" → estudar SÓ isso (30 min) → fazer → errar → corrigir → aprendeu
```

---

## Como usar a Rocketseat (sem cair em tutorial hell)

Você tem o curso fullstack da Rocketseat. **NÃO assista ele linearmente.** Use como dicionário:

### A forma ERRADA de usar a Rocketseat

```
❌ Semana 1: assiste módulo 1 (HTML)
❌ Semana 2: assiste módulo 2 (CSS)
❌ Semana 3: assiste módulo 3 (JS)
❌ Semana 4: assiste módulo 4 (Node)
❌ Semana 5: "agora vou começar o projeto"
❌ Semana 5: trava porque não lembra nada

Resultado: 4 semanas de vídeo, 0 linhas de código, frustração.
```

### A forma CERTA de usar a Rocketseat

```
✅ Pega Issue #5 (Boilerplate frontend)
✅ Lê os critérios: "index.html com reset CSS e variáveis de cor"
✅ Não sabe CSS variables → Rocketseat: assiste SÓ a aula de CSS variables (15 min)
✅ Implementa no projeto
✅ Funciona → próximo critério
✅ Não sabe Flexbox → Rocketseat: assiste SÓ Flexbox (20 min)
✅ Implementa → funciona → issue concluída

Resultado: 35 min de vídeo + 2h de código real + issue entregue + aprendeu 2 conceitos.
```

### Mapa: qual módulo da Rocketseat consultar por issue

| Issue | O que precisa | Onde na Rocketseat | Alternativa gratuita |
|-------|--------------|-------------------|---------------------|
| #5 Boilerplate frontend | HTML + CSS | Módulo HTML/CSS | MDN: HTML basics + CSS first steps |
| #13 Tela de login | HTML forms + CSS | Módulo Formulários | MDN: Your first form |
| #14 Tela de cadastro | Mesma coisa | Mesmo módulo | Mesma alternativa |
| #6 Boilerplate Node | Node + Express | Módulo Node.js | expressjs.com/starter |
| #13/#14 fetch API | JavaScript async | Módulo JS assíncrono | javascript.info cap 11 |
| #21-#23 Telas | DOM manipulation | Módulo JS no browser | javascript.info cap 13-14 |
| #25 Socket.IO | WebSocket | Módulo real-time (se tiver) | socket.io/get-started |
| #15 JWT no Node | Autenticação | Módulo Auth | jwt.io/introduction |

**Regra:** assista no MÁXIMO 30 minutos por sessão. Depois para e implementa. Se precisar de mais, volta e assiste mais 15 min. **Nunca mais de 1h de vídeo seguida.**

---

## Como aprender cada tecnologia — O mapa completo

### HTML — A estrutura

**O que é:** esqueleto da página. Tags que definem o que cada coisa é (título, parágrafo, botão, formulário).

**Como aprender (3h total, não linear):**

```
AGORA (1h):
├── MDN: "Getting started with HTML" → leia, faça os exemplos
├── Foque em: <div>, <h1>-<h6>, <p>, <a>, <button>, <form>, <input>, <label>
└── Resultado: sabe criar qualquer formulário básico

SOB DEMANDA (quando a issue pedir):
├── <table> → quando fizer lista de participantes
├── <select>, <textarea> → quando fizer formulário de criar sessão
└── Semântica (<header>, <main>, <nav>) → quando refatorar
```

**Recurso primário:** [MDN HTML](https://developer.mozilla.org/pt-BR/docs/Learn/HTML)  
**Rocketseat:** Módulo HTML (consultar, não assistir tudo)

**Exercício 42:** abra o VSCode, crie `teste.html`, e construa um formulário de login com email + senha + botão. Sem CSS. Só HTML. Se funciona no navegador, você sabe HTML suficiente pra começar.

---

### CSS — A aparência

**O que é:** regras visuais. Cor, tamanho, posição, espaçamento.

**Como aprender (4h total, não linear):**

```
AGORA (1.5h):
├── MDN: "CSS first steps" → leia até "How CSS works"
├── Foque em: seletores (classe, id), box model, display, color, font
├── CSS Variables: "--primary: #7c3aed;" → usa em tudo
└── Resultado: sabe estilizar qualquer elemento

SEMANA 2 (1h, quando fizer telas):
├── Flexbox: css-tricks.com/snippets/css/a-guide-to-flexbox
├── É isso. Flexbox resolve 90% dos layouts.
└── Resultado: sabe alinhar qualquer coisa

SOB DEMANDA:
├── Grid → quando fizer layout de dashboard
├── Media queries → quando fizer responsivo
├── Transições → quando fizer animações suaves
```

**Recurso primário:** [MDN CSS](https://developer.mozilla.org/pt-BR/docs/Learn/CSS) + [CSS Tricks Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)  
**Rocketseat:** Módulo CSS (consultar Flexbox e Grid)

**Exercício 42:** pegue o formulário HTML que criou e estilize com a paleta do LitCircle (navy #0f172a, purple #7c3aed, amber #f59e0b). Se parece com o wireframe do login, você sabe CSS suficiente.

---

### JavaScript — A lógica

**O que é:** faz a página fazer coisas. Clicou no botão → acontece algo. Dados vêm do servidor → aparecem na tela.

**Como aprender (6h total, não linear):**

```
SEMANA 0 (3h — OBRIGATÓRIO antes de codar):
├── javascript.info cap 2: "JavaScript Fundamentals"
│   → variáveis (let, const), tipos, if/else, loops
├── javascript.info cap 5: "Data types" (só strings e arrays)
│   → .map(), .filter(), .forEach(), template literals
├── javascript.info cap 4.1-4.4: "Objects"
│   → criar objeto, acessar propriedades
└── Resultado: sabe ler e escrever JS básico

SEMANA 1-2 (sob demanda, quando issues pedirem):
├── javascript.info cap 11: "Promises, async/await"
│   → precisa pra fetch() — Issue #13
├── MDN: "Fetch API" → fazer requisições HTTP
│   → precisa pra todas as telas
├── javascript.info cap 13: "Document" (DOM)
│   → querySelector, createElement, addEventListener
│   → precisa pra manipular a página
└── Resultado: sabe fazer fetch, manipular DOM, tratar erros

SOB DEMANDA:
├── localStorage → Issue #13 (login)
├── Socket.IO client → Issue #26 (chat)
├── Módulos (import/export) → quando organizar código
```

**Recurso primário:** [javascript.info](https://javascript.info)  
**Rocketseat:** Módulo JavaScript (consultar async/await e DOM)

**Exercício 42:** abra o console do navegador (F12 → Console). Crie um array de nomes, filtre os que têm mais de 5 letras, e mostre no console. Se funcionou, você sabe JS suficiente pra começar.

```javascript
// Tenta fazer isso SEM olhar a resposta:
const nomes = ["Kauã", "Rafael", "Ana", "Beatriz", "Jo"];
// Filtre os nomes com mais de 3 letras
// Mostre cada um no console com template literal: "Nome: Kauã"
```

---

### Node.js + Express — O servidor

**O que é:** JavaScript rodando fora do navegador, no servidor. Express é um framework que facilita criar rotas HTTP.

**Como aprender (2h, sob demanda — Issue #6):**

```
QUANDO CHEGAR NA ISSUE #6:
├── expressjs.com: "Hello World" (15 min)
│   → cria servidor, define rota GET /health
├── expressjs.com: "Basic routing" (15 min)
│   → GET, POST, rotas com parâmetros
├── Rocketseat: Módulo Node.js — só a parte de Express
└── Resultado: servidor rodando com GET /health

SOB DEMANDA:
├── Middleware → Issue #15 (JWT validation)
├── Socket.IO → Issue #25 (chat)
├── CORS → quando frontend não conectar
```

**Recurso primário:** [expressjs.com](https://expressjs.com)  
**Exercício 42:** crie um `index.js` que responde `{ "status": "ok" }` em `GET /health`. Se `curl localhost:3001/health` retorna o JSON, você sabe Express suficiente.

---

### SQL + PostgreSQL — O banco

**O que é:** linguagem pra criar tabelas, inserir dados, e buscar dados.

**Como aprender (3h total):**

```
SEMANA 0 (2h — OBRIGATÓRIO):
├── sqlbolt.com: todas as lições (é interativo, divertido)
│   → SELECT, WHERE, INSERT, UPDATE, DELETE, JOIN
└── Resultado: sabe ler e escrever SQL básico

SOB DEMANDA:
├── pgexercises.com → exercícios mais avançados
├── CREATE TABLE → quando ver o doc 07-modelo-de-dados.md
├── Indexes → quando entender performance
```

**Recurso primário:** [sqlbolt.com](https://sqlbolt.com) → [pgexercises.com](https://pgexercises.com)

**Exercício 42:** abra o terminal do PostgreSQL (`psql litcircle`), crie uma tabela `teste` com `id` e `nome`, insira 3 registros, e selecione os que têm nome começando com "K". Se funcionou, você sabe SQL suficiente.

---

### Git — O controle de versão

**Como aprender (1h — OBRIGATÓRIO):**

```
SEMANA 0 (1h):
├── learngitbranching.js.org: todos os níveis "Main" + "Remote"
│   → é um jogo, aprende fazendo
├── Leia: 15-git-workflow.md do repo
└── Resultado: sabe commit, branch, merge, push, pull, rebase
```

**Recurso primário:** [learngitbranching.js.org](https://learngitbranching.js.org) + [Pro Git Book](https://git-scm.com/book/pt-br/v2)

---

## O Protocolo Completo — Como executar cada issue

```
┌─────────────────────────────────────────────────────────────┐
│  0. PEGAR a issue do board                                  │
└─────────────────────────┬───────────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  1. LER a issue (5 min)                                     │
│     → Critérios de aceite → marcar o que NÃO sei            │
└─────────────────────────┬───────────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  2. ESTUDAR só o que não sei (15-30 min)                    │
│     → Doc oficial OU Rocketseat (SÓ o trecho relevante)     │
│     → Máximo 30 min de leitura/vídeo antes de codar         │
└─────────────────────────┬───────────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  3. OLHAR como outros fizeram (10 min)                      │
│     → GitHub: "[tecnologia] example"                        │
│     → Ver a ESTRUTURA, não copiar código                    │
└─────────────────────────┬───────────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  4. CODAR (maior parte do tempo)                            │
│     → Testar a cada 5 linhas                                │
│     → Ler erros com calma                                   │
│     → console.log é seu melhor amigo                        │
│     → Travou 45 min? → documenta na issue → chama parceiro  │
└─────────────────────────┬───────────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  5. REFATORAR (15 min)                                      │
│     → "Tem algo repetido?" → extrair pra função/componente  │
│     → "Tem algo confuso?" → renomear                        │
│     → Fez errado? ÓTIMO → refatorar = aprender 2x           │
└─────────────────────────┬───────────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  6. ANOTAR na issue o que aprendeu (2 min)                  │
│     → "O que aprendi:" → lista de conceitos novos           │
│     → Vira documentação viva do projeto                     │
└─────────────────────────┬───────────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  7. PR → Review → Merge → PRÓXIMA ISSUE                    │
└─────────────────────────────────────────────────────────────┘
```

---

## Exercícios 42 — Validação de conhecimento

Antes de começar cada milestone, faça estes exercícios pra validar que sabe o mínimo:

### Antes da Milestone v0.1 (Esqueleto)

| # | Exercício | Validação |
|---|-----------|-----------|
| 1 | Crie um `index.html` com formulário de login (email + senha + botão) | Abre no navegador e mostra o formulário |
| 2 | Estilize com CSS: fundo navy, botão purple, input com borda | Parece profissional |
| 3 | No console (F12), crie um array e use `.filter()` | Retorna os itens filtrados |
| 4 | Faça `git init`, commit, crie branch, volte pra main | `git log` mostra o commit |
| 5 | No psql: `CREATE TABLE`, `INSERT`, `SELECT` | Retorna os dados |

### Antes da Milestone v0.2 (Auth)

| # | Exercício | Validação |
|---|-----------|-----------|
| 1 | Faça `fetch('https://jsonplaceholder.typicode.com/posts')` e mostre no console | Array de posts aparece |
| 2 | Faça um `POST` com `fetch()` enviando JSON | Resposta 201 no console |
| 3 | Use `localStorage.setItem()` e `getItem()` | Valor persiste entre refreshes |
| 4 | Crie um servidor Express com `GET /health` | `curl localhost:3001/health` retorna JSON |

### Antes da Milestone v0.3 (Sessões)

| # | Exercício | Validação |
|---|-----------|-----------|
| 1 | Crie uma página que faz GET e mostra dados numa lista HTML | Lista aparece com dados reais |
| 2 | Crie um formulário que faz POST e mostra resposta | Dados enviados e resposta exibida |
| 3 | Use `document.createElement()` pra adicionar itens dinamicamente | Itens aparecem sem recarregar |

---

## Cronograma de estudo

```
SEMANA 0 (antes de codar — 1 dia, ~7h):
├── Git: learngitbranching.js.org (1h)
├── SQL: sqlbolt.com completo (2h)
├── HTTP: MDN HTTP Overview (1h)
├── JS: javascript.info cap 2, 4, 5 (3h)
├── Exercícios 42 da Milestone v0.1
└── NÃO assista curso nenhum linearmente

SEMANAS 1-2 (Milestone v0.1 + v0.2):
├── Estudo: SÓ o que a issue atual pede
├── Rocketseat: consulta pontual (máx 30 min por sessão)
├── Doc oficial: primeira fonte pra tudo
└── Exercícios 42 da Milestone v0.2 (antes de começar)

SEMANAS 3-5 (Milestone v0.3):
├── Mesmo padrão: issue → estudar → fazer → anotar
├── Mais DOM manipulation (javascript.info cap 13-14)
└── Exercícios 42 da Milestone v0.3

SEMANAS 6-8 (Milestone v0.4 + v0.5):
├── Socket.IO (sob demanda)
├── Deploy (doc 09-deploy.md quando chegar lá)
└── A essa altura vocês já sabem buscar sozinhos
```

---

## Anti-padrões: o que NÃO fazer

| Anti-padrão | Por que é ruim | O que fazer |
|-------------|---------------|-------------|
| Assistir a Rocketseat inteira antes de codar | Tutorial hell — acha que sabe mas não sabe fazer | Consulte SÓ o que a issue pede (máx 30 min) |
| Estudar React "porque vai precisar depois" | Não vai precisar agora. Vai confundir. | Só estude o que a issue ATUAL exige |
| Ler a doc inteira de Express | Over-engineering — 90% você não vai usar no MVP | Leia o "Getting Started" e pare |
| Ficar no console sem fazer projeto | Exercícios soltos não constroem skill real | O projeto É o exercício |
| Copiar código do Stack Overflow | Funciona mas não ensina | Leia a resposta, entenda, escreva o seu |
| Assistir vídeo no 2x sem pausar | Ilusão de produtividade | Pause, implemente, depois continue |

---

## Recursos definitivos por tecnologia

| Tecnologia | Recurso PRIMÁRIO (gratuito) | Rocketseat (complementar) |
|-----------|---------------------------|--------------------------|
| HTML | [MDN Learn HTML](https://developer.mozilla.org/pt-BR/docs/Learn/HTML) | Módulo HTML |
| CSS | [MDN Learn CSS](https://developer.mozilla.org/pt-BR/docs/Learn/CSS) + [Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) | Módulo CSS |
| JavaScript | [javascript.info](https://javascript.info) | Módulo JS |
| Node/Express | [expressjs.com](https://expressjs.com) | Módulo Node |
| Socket.IO | [socket.io/docs](https://socket.io/docs/v4/) | Módulo real-time |
| SQL | [sqlbolt.com](https://sqlbolt.com) | — |
| Git | [learngitbranching.js.org](https://learngitbranching.js.org) | — |
| HTTP | [MDN HTTP](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Overview) | — |

**Prioridade:** Doc oficial → Rocketseat (trecho específico) → Google → Stack Overflow

---

## O resumo de tudo em 1 diagrama

```
                    ┌──────────────────────┐
                    │  PEGA A ISSUE        │
                    └──────────┬───────────┘
                               ▼
                    ┌──────────────────────┐
                    │  O QUE NÃO SEI?      │
                    └──────────┬───────────┘
                               ▼
              ┌────────────────┼────────────────┐
              ▼                ▼                ▼
     ┌──────────────┐ ┌──────────────┐ ┌──────────────┐
     │  Não sei o   │ │  Não sei a   │ │  Não sei     │
     │  CONCEITO    │ │  SINTAXE     │ │  o DESIGN    │
     │              │ │              │ │              │
     │  Glossário   │ │  Doc oficial │ │  Google:     │
     │  do repo     │ │  MDN/spring  │ │  "how to..." │
     │  → MDN       │ │  Rocketseat  │ │  GitHub      │
     │              │ │  (trecho)    │ │  examples    │
     └──────┬───────┘ └──────┬───────┘ └──────┬───────┘
            └────────────────┼────────────────┘
                             ▼
                    ┌──────────────────────┐
                    │  IMPLEMENTA          │
                    │  (testa a cada 5     │
                    │   linhas)            │
                    └──────────┬───────────┘
                               ▼
                    ┌──────────────────────┐
                    │  FUNCIONOU?          │
                    └──────┬───────┬───────┘
                      SIM  ▼       ▼  NÃO
                ┌───────────┐ ┌──────────────┐
                │ REFATORA  │ │ LÊ O ERRO    │
                │ ANOTA     │ │ GOOGLE ERRO  │
                │ PR        │ │ 45 MIN?      │
                │ PRÓXIMA   │ │ → PARCEIRO   │
                └───────────┘ └──────────────┘
```
