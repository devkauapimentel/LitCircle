# Guia de aprendizado — A Metodologia Autodidata Completa

> Como aprender fazendo, errar certo, e nunca ficar preso.

---

## A verdade sobre aprender programação

**Você VAI errar.** Vai criar 3 HTMLs copiando menu antes de perceber que devia reutilizar. Vai fazer fetch sem tratar erro. Vai commitar na main sem querer. Isso é normal.

O que separa quem aprende rápido de quem fica preso:

```
DEV QUE FICA PRESO:      Issue → codar direto → erro → frustração → desiste
DEV QUE APRENDE RÁPIDO:  Issue → pesquisa 15 min → codar → erro → refatora → aprende
```

A diferença é **um passo de 15 minutos antes de codar**: a pesquisa rápida.

---

## O PROTOCOLO COMPLETO: como executar cada issue

### Passo 1 — LER a issue (5 min)

Leia a issue inteira. Leia os **critérios de aceite** um por um. Sublinhe mentalmente o que não sabe.

Exemplo — Issue #13 "Tela de login":
```
Critérios de aceite:
- [ ] Formulário com e-mail e senha             ← sei fazer
- [ ] Validação antes de enviar (campos vazios)  ← sei fazer
- [ ] fetch('POST /api/auth/login')              ← já fiz? não → pesquisar
- [ ] Token salvo no localStorage                ← o que é localStorage? → pesquisar
- [ ] Redireciona para dashboard após login      ← window.location? → verificar
- [ ] Mensagem de erro visível quando login falha ← sei fazer
- [ ] Link "Não tem conta? Cadastre-se"          ← sei fazer
```

**Resultado:** você sabe que precisa pesquisar 2 coisas antes de codar: `fetch POST` e `localStorage`.

---

### Passo 2 — PESQUISAR antes de codar (15-30 min)

Para cada coisa que não sabe, faça uma pesquisa RÁPIDA. Não faça um curso. Leia 1 artigo ou 1 seção da doc oficial.

```
O QUE NÃO SEI         O QUE PESQUISO                       ONDE
─────────────────────  ────────────────────────────────────  ──────────────
fetch POST             "javascript fetch post example"       javascript.info
localStorage           "localStorage javascript MDN"         developer.mozilla.org
```

**Leia por 10-15 minutos.** Não precisa entender 100%. Precisa entender o suficiente pra tentar.

**DICA:** pesquise em inglês. Os resultados são 10x melhores.

---

### Passo 3 — OLHAR como outros fizeram (10 min)

**Esse é o passo que evita erros bobos.** Antes de codar, veja 1-2 exemplos de como outros devs fizeram a mesma coisa.

```
O QUE VOU FAZER            O QUE PESQUISO
───────────────────────    ─────────────────────────────────────────
Criar tela de login        "vanilla javascript login page example github"
Criar servidor Express     "express.js starter template"
Reutilizar HTML entre      "vanilla js shared components across pages"
  várias páginas
Fazer fetch com JWT        "javascript fetch with authorization header"
```

**POR QUE ISSO FUNCIONA:**

- Você vê padrões que devs experientes usam
- Descobre soluções que nem sabia que existiam (como `components.js`)
- Evita reinventar a roda
- Aprende vocabulário técnico real

**ONDE OLHAR:**

| Recurso | Para quê |
|---------|----------|
| **GitHub** → pesquise "[tecnologia] example" | Ver código real de projetos |
| **MDN Web Docs** | Referência completa de HTML/CSS/JS |
| **javascript.info** | Tutoriais com exemplos executáveis |
| **spring.io/guides** | Guias oficiais do Spring Boot |
| **Dev.to / Medium** | Artigos "How I built X" |

**REGRA:** olhe o código, entenda a estrutura, mas **escreva o seu do zero**. Não copie.

---

### Passo 4 — CODAR (a maior parte do tempo)

Agora sim, code. Vai dar erro. Vai quebrar. **Isso é o aprendizado.**

```
CICLO NORMAL:
  Escrever código → rodar → erro → ler o erro → pesquisar → corrigir → rodar → funciona

CICLO REAL (mais honesto):
  Escrever → erro → frustração → ler erro de novo com calma → ah! era isso → corrigir → FUNCIONA → euforia
```

**Dicas durante o código:**

1. **Teste a cada mudança pequena.** Não escreva 50 linhas e depois teste. Escreva 5, teste, funciona, próximas 5.
2. **Leia o erro.** O erro te diz o que está errado e em qual linha. 90% da solução está na mensagem de erro.
3. **console.log é seu melhor amigo.** Não sabe o valor de uma variável? `console.log(variavel)`.

---

### Passo 5 — REFATORAR quando perceber o erro (a hora mais valiosa)

**Aqui é onde a mágica acontece.** Depois que funciona, olhe pro código e pergunte:

```
"Tem algo REPETIDO?"       → extrair pra uma função ou componente
"Tem algo CONFUSO?"        → renomear variáveis, adicionar comentários
"Funciona mas é FEIO?"     → ok por agora, anota pra melhorar depois
"Fiz do jeito ERRADO?"     → ÓTIMO — refatorar é aprender 2x
```

**Exemplo real: o momento do "components.js"**

```
COMO ACONTECE NA PRÁTICA:

Issue #5:  Criar login.html    → cria o HTML com sidebar
Issue #13: Criar dashboard.html → copia sidebar do login... funciona
Issue #22: Criar sessão.html   → copia sidebar de novo... "peraí..."

SEU CÉREBRO: "Tô copiando esse sidebar pela 3ª vez.
              Se eu mudar, tenho que mudar em 3 arquivos.
              Isso tá errado."

AÇÃO:
1. Google: "how to share HTML between pages vanilla js"
2. Descobre: JavaScript pode injetar HTML
3. Cria components.js → move sidebar pra lá
4. Remove sidebar duplicado dos 3 HTMLs
5. Agora muda em 1 lugar, muda em todos

ISSO É REFATORAÇÃO. Você não errou — você APRENDEU.
O erro é o professor. A refatoração é a prova de que aprendeu.
```

**A regra:** não tem problema fazer errado na primeira vez. Tem problema fazer errado na **quinta** vez e não perceber.

---

### Passo 6 — ANOTAR o que aprendeu (2 min)

Faça um comentário na issue do GitHub:

```markdown
## O que aprendi nessa issue

- `localStorage.setItem/getItem` persiste dados entre páginas
- `fetch()` com POST precisa de `Content-Type: application/json`
- Criei `components.js` pra reutilizar sidebar entre páginas
- Erro de CORS: resolvido com config no Spring Boot
```

**POR QUE:** daqui 2 meses, quando for fazer algo parecido, você pesquisa nas suas próprias issues e encontra a solução que JÁ descobriu.

---

## Quando NÃO é autodidata — quando buscar ajuda

| Situação | O que fazer |
|----------|-------------|
| 45 min travado no mesmo erro | Documenta na issue → chama parceiro |
| Não entende um CONCEITO | Docs do repo → glossário → doc oficial |
| Não entende NADA da issue | Precisa de mais estudo na Semana 0 (volte ao básico) |
| Decisão de DESIGN (2 opções válidas) | GitHub Discussions → discutem juntos |

**Autodidata NÃO significa sozinho.** Significa que você **tenta primeiro, pesquisa primeiro, pensa primeiro** — e só depois pede ajuda com contexto claro.

---

## A Semana 0 — Base mínima antes de codar

Não é um curso. São exercícios práticos curtos que dão **vocabulário mínimo**.

### Kauã — Frontend + Node.js

| O quê | Recurso | Tempo | O que ganha |
|-------|---------|-------|-------------|
| Git | [learngitbranching.js.org](https://learngitbranching.js.org) — níveis "Main" | 1h | Sabe: commit, branch, merge, push |
| JS moderno | [javascript.info](https://javascript.info) cap 4-11 | 3h | Sabe: função, array, async/await, fetch |
| HTTP | [MDN HTTP Overview](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Overview) | 1h | Sabe: GET, POST, status codes |
| SQL | [sqlbolt.com](https://sqlbolt.com) | 2h | Sabe: SELECT, INSERT, WHERE, JOIN |

### Rafael — Backend Java

| O quê | Recurso | Tempo | O que ganha |
|-------|---------|-------|-------------|
| Git | [learngitbranching.js.org](https://learngitbranching.js.org) | 1h | Mesmo do Kauã |
| Java | [dev.java/learn](https://dev.java/learn) + [exercism.org](https://exercism.org) Java (15 exercícios) | 5h | Sabe: classe, método, interface, Collections |
| HTTP | MDN HTTP Overview | 1h | Mesmo do Kauã |
| SQL | [sqlbolt.com](https://sqlbolt.com) | 2h | Mesmo do Kauã |

### O que a Semana 0 NÃO ensina (e tá tudo bem)

- Como fazer REST API → aprende na Issue #10 (quando precisar)
- Como usar Socket.IO → aprende na Issue #25 (quando precisar)
- Como fazer migrations → aprende na Issue #9 (quando precisar)
- Como reutilizar HTML → aprende quando perceber a repetição

**A Semana 0 dá vocabulário. As issues dão experiência.**

---

## Sob demanda — O que estudar quando a issue exigir

| Issue exige... | Estude isso (30-60 min) | Recurso |
|----------------|------------------------|---------|
| Servidor HTTP (Node) | Express básico | [expressjs.com](https://expressjs.com) tutorial |
| REST API (Java) | Spring Boot REST | spring.io/guides "Building a REST Service" |
| Autenticação | JWT + bcrypt | jwt.io/introduction |
| Chat tempo real | Socket.IO | socket.io/docs/v4 "Get Started" |
| Banco (Java) | Spring Data JPA | spring.io/guides "Accessing Data with JPA" |
| CSS responsivo | Flexbox + Grid | css-tricks.com/guides |
| Migrations | Flyway | flywaydb.org quickstart |

---

## Anti-padrões: o que NÃO fazer

| Anti-padrão | Por que é ruim | O que fazer em vez disso |
|-------------|---------------|------------------------|
| **Tutorial hell** — assistir 20h de vídeo antes de codar | Você acha que sabe, mas não sabe fazer | Para cada 1h de estudo, 2h de código |
| **Paralisia** — "ainda não sei o suficiente" | Você nunca vai saber "o suficiente" antes de tentar | Comece. Erre. Corrija. Aprenda. |
| **Copiar sem entender** — cola código do Stack Overflow | Funciona agora, quebra depois, e você não sabe por quê | Leia o código, entenda, depois escreva o seu |
| **Curso como muleta** — "vou fazer um curso de React antes" | React não é do MVP. Você tá procrastinando. | Só estude o que a ISSUE ATUAL pede |
| **Perfeccionismo** — "precisa ficar perfeito" | O primeiro código NUNCA é perfeito. Refatora depois. | Faça funcionar → faça bonito → faça rápido |

---

## Recursos por tecnologia

### Kauã

| Tecnologia | Doc oficial | Quando estudar |
|-----------|-------------|---------------|
| JavaScript | [javascript.info](https://javascript.info) | Semana 0 + sob demanda |
| HTML/CSS | [developer.mozilla.org](https://developer.mozilla.org/pt-BR/) | Sob demanda |
| Node/Express | [expressjs.com](https://expressjs.com) | Issue #6 |
| Socket.IO | [socket.io/docs](https://socket.io/docs/v4/) | Issue #25 |
| JWT (validação) | [jwt.io](https://jwt.io/introduction) | Issue #15 |

### Rafael

| Tecnologia | Doc oficial | Quando estudar |
|-----------|-------------|---------------|
| Java | [dev.java/learn](https://dev.java/learn) | Semana 0 |
| Spring Boot | [spring.io/guides](https://spring.io/guides) | Issue #7 |
| Spring Data JPA | spring.io/guides "Accessing Data with JPA" | Issue #9 |
| Spring Security + JWT | spring.io/guides | Issue #11 |
| Flyway | [flywaydb.org](https://flywaydb.org) quickstart | Issue #9 |

### Ambos

| Tecnologia | Doc oficial | Quando estudar |
|-----------|-------------|---------------|
| Git | [git-scm.com/book](https://git-scm.com/book/pt-br/v2) (Pro Git Book, em PT) | Semana 0 |
| SQL | [sqlbolt.com](https://sqlbolt.com) + [pgexercises.com](https://pgexercises.com) | Semana 0 + sob demanda |
| HTTP/REST | MDN HTTP docs | Semana 0 |

---

## Resumo visual — O ciclo completo de uma issue

```
┌─────────────────────────────────────────────────────────────┐
│                     PEGAR ISSUE DO BOARD                    │
└─────────────────────────┬───────────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  1. LER a issue (5 min)                                     │
│     → Critérios de aceite → marcar o que NÃO sei            │
└─────────────────────────┬───────────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  2. PESQUISAR o que não sei (15 min)                        │
│     → Google → doc oficial → ler 1 artigo/tutorial          │
└─────────────────────────┬───────────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  3. OLHAR como outros fizeram (10 min)                      │
│     → GitHub examples → ver padrões → NÃO copiar            │
└─────────────────────────┬───────────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  4. CODAR (tempo que precisar)                              │
│     → Testar a cada 5 linhas → ler erros → console.log     │
│     → Travou 45 min? → documenta → chama parceiro           │
└─────────────────────────┬───────────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  5. REFATORAR (15 min)                                      │
│     → "Tem algo repetido?" → extrair                        │
│     → "Tem algo confuso?" → renomear                        │
│     → "Fiz errado?" → ÓTIMO → refatorar = aprender 2x      │
└─────────────────────────┬───────────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  6. ANOTAR na issue (2 min)                                 │
│     → "O que aprendi:" → lista de conceitos novos           │
└─────────────────────────┬───────────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  7. PR → Review → Merge → PRÓXIMA ISSUE                    │
└─────────────────────────────────────────────────────────────┘
```
