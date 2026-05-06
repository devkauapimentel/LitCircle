# 🚦 COMECE AQUI — O Guia Completo

> Tudo que vocês precisam saber antes de escrever a primeira linha de código. Leiam juntos, na ordem, sem pular.

---

## 1. COMO TUDO FUNCIONA (sem Docker)

### "E se não rodar na máquina do Rafael?"

Sem Docker, cada um instala as ferramentas direto na máquina. Funciona? **Sim, funciona perfeitamente para 2 pessoas.** É assim que 99% dos projetos de faculdade e iniciantes funcionam.

**O que garante que funcione em todas as máquinas:**

| Mecanismo | O que faz |
|-----------|-----------|
| **Versões fixas** | Todos usam Node 20, Java 21, PostgreSQL 15. Doc [14-setup-ambiente.md](14-setup-ambiente.md) tem os comandos exatos |
| **`.env.example`** | Arquivo template com as variáveis. Cada um copia e preenche com seus dados locais |
| **`package.json`** e **`pom.xml`** | Travam as versões das dependências. `npm install` instala as mesmas libs em qualquer máquina |
| **Flyway (migrations)** | SQLs versionados que criam o banco igual em qualquer máquina. Rafael roda `V1__create_users.sql` e o banco dele fica idêntico ao seu |
| **README.md** | Tem o passo a passo de setup completo |

**Quando Docker faria falta?**
- Se tivessem 10+ devs com máquinas diferentes → não é o caso
- Se precisassem de Redis, RabbitMQ, etc → não no MVP
- Se quisessem deploy com 1 comando → Render.com resolve isso

**Quando vão adicionar Docker?**
Após o MVP funcionar. Aí criam um `docker-compose.yml` e qualquer pessoa clona e roda com `docker compose up`. Está no [PROJETOS-FUTUROS.md](../PROJETOS-FUTUROS.md) como Nível 3.

---

## 2. COMO APRENDER O QUE NÃO SABEM

### A regra de ouro: aprenda SOB DEMANDA

Não estudem 3 semanas antes de codar. O ciclo é:

```
1. Pega a issue do board
2. Lê 30-60 min da doc oficial da tech que precisa
3. Tenta implementar
4. Travou? → Busca na doc oficial → Tenta de novo
5. 45 min travado → Documenta → Chama o parceiro
6. Funcionou → Commit → PR → Próxima issue
```

### Mapa do que estudar e quando

#### Semana 0 (ANTES DE CODAR — 1 dia, 6h)

**Ambos fazem juntos:**

| O quê | Recurso | Tempo |
|-------|---------|-------|
| Git básico | [learngitbranching.js.org](https://learngitbranching.js.org) — faça TODOS os níveis "Main" | 1h |
| HTTP | [MDN HTTP Overview](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Overview) — GET, POST, PUT, DELETE, status codes | 1h |
| SQL básico | [sqlbolt.com](https://sqlbolt.com) — tutorial interativo completo | 2h |

**Kauã faz sozinho:**

| O quê | Recurso | Tempo |
|-------|---------|-------|
| JS moderno | [javascript.info](https://javascript.info) cap 4-11 — arrow functions, async/await, fetch | 2h |

**Rafael faz sozinho:**

| O quê | Recurso | Tempo |
|-------|---------|-------|
| Java básico | [dev.java/learn](https://dev.java/learn) — classes, objetos, interfaces | 3h |

#### Durante o projeto (QUANDO A ISSUE EXIGIR)

| Quando a issue pedir... | Estude isso... | Recurso | Tempo |
|-------------------------|----------------|---------|-------|
| Servidor HTTP (Node) | Express | [expressjs.com](https://expressjs.com) tutorial "Hello World" | 30min |
| REST API (Java) | Spring Boot | spring.io/guides "Building a REST Service" | 1h |
| Autenticação | JWT + bcrypt | jwt.io/introduction | 30min |
| Chat tempo real | Socket.IO | socket.io/docs/v4 "Get Started" | 1h |
| Banco (Java) | Spring Data JPA | spring.io/guides "Accessing Data with JPA" | 1h |
| CSS responsivo | Flexbox + Grid | css-tricks.com/guides | 30min |
| Migrations | Flyway | flywaydb.org quickstart | 30min |

**O guia completo com mais detalhes está em [12-guia-de-aprendizado.md](12-guia-de-aprendizado.md)**

---

## 3. GIT WORKFLOW — COMO TRABALHAR EM DUPLA

### "Eu não sei Git Workflow"

Tudo bem. O doc [15-git-workflow.md](15-git-workflow.md) explica **do zero** — conceitos, comandos, exemplos, erros comuns e como resolver conflitos. Leiam juntos.

### O resumo do fluxo (leiam o doc completo depois):

```
┌─────────────────────────────────────────────────┐
│  1. Pego issue do board (WIP = 1 por pessoa)    │
│  2. git checkout main && git pull               │
│  3. git checkout -b feature/nome-da-issue       │
│  4. Codar, testar                               │
│  5. git add . && git commit -m "feat: ..."      │
│  6. git push origin feature/nome-da-issue       │
│  7. Abro Pull Request no GitHub                 │
│  8. Parceiro revisa → aprova                    │
│  9. Merge na main → issue concluída             │
│  10. Próxima issue                              │
└─────────────────────────────────────────────────┘
```

### Regras inegociáveis

| Regra | Por quê |
|-------|---------|
| **Nunca commit na main** | Sempre via Pull Request |
| **WIP = 1** | Só 1 issue por pessoa ao mesmo tempo |
| **`.env` nunca vai pro git** | Use `.env.example` como template |
| **45 min travado → chama parceiro** | Não fique 4h no mesmo bug |
| **Todo PR precisa de review** | O outro lê e aprova antes do merge |

---

## 4. AS ISSUES — O QUE FAZER E EM QUAL ORDEM

### Todas as 26 issues já estão no GitHub (abertas)

Organizadas em 5 milestones na ordem certa:

### Frontend: 100% vanilla (HTML + CSS + JS na mão)

Nenhuma biblioteca CSS. Tudo escrito do zero. Isso treina:
- HTML semântico (tags corretas, formulários, acessibilidade)
- CSS avançado (Flexbox, Grid, variáveis, responsivo)
- JavaScript puro (DOM, fetch, eventos, lógica)

Bibliotecas só no **backend Node.js**: Express, Socket.IO, jsonwebtoken, bcrypt.

### Distribuição de trabalho

| Kauã | Rafael |
|------|--------|
| 8 issues frontend + 3 issues Node.js | 11 issues Java backend |
| Frontend = treina HTML/CSS/JS | Backend = treina Java/Spring/SQL |
| Node.js = treina Express/JWT/Socket.IO | Java = treina Spring Boot/JPA |

### Milestone v0.1 — Esqueleto (Semana 1)

| # | Issue | Quem | O que é |
|---|-------|------|---------|
| #4 | Setup do repositório | Ambos | Estrutura de pastas pronta |
| #5 | Boilerplate frontend | Kauã | `index.html` + CSS reset + variáveis de cor |
| #6 | Boilerplate backend Node | Kauã | Express + `GET /health` |
| #7 | Boilerplate backend Java | Rafael | Spring Boot + `GET /health` |
| #8 | PostgreSQL local | Ambos | Banco criado e rodando |

### Milestone v0.2 — Autenticação (Semanas 2-3)

| # | Issue | Quem | O que é |
|---|-------|------|---------|
| #9 | Migration: tabela users | Rafael | SQL que cria a tabela |
| #10 | Endpoint de cadastro | Rafael | `POST /api/auth/register` |
| #11 | Configurar JWT | Rafael | Gerar e validar tokens |
| #12 | Endpoint de login | Rafael | `POST /api/auth/login` |
| #13 | Tela de login | Kauã | HTML + fetch para API |
| #14 | Tela de cadastro | Kauã | HTML + fetch para API |
| #15 | Middleware JWT no Node | Kauã | Validar token no backend Node |

### Milestone v0.3 — Sessões (Semanas 4-5)

| # | Issue | Quem | O que é |
|---|-------|------|---------|
| #16 | Migrations sessions | Rafael | Tabelas sessions + session_members |
| #17 | Criar sessão | Rafael | `POST /api/sessions` |
| #18 | Entrar por código | Rafael | `POST /api/sessions/join` |
| #19 | Listar sessões | Rafael | `GET /api/sessions` |
| #20 | Atualizar progresso | Rafael | `PUT /api/sessions/:id/progress` |
| #21 | Tela Dashboard | Kauã | Lista de sessões do usuário |
| #22 | Tela Criar sessão | Kauã | Formulário |
| #23 | Tela Sessão de leitura | Kauã | Participantes + progresso |

### Milestone v0.4 — Chat (Semanas 6-7)

| # | Issue | Quem | O que é |
|---|-------|------|---------|
| #24 | Migration messages | Rafael | Tabela messages |
| #25 | Socket.IO servidor | Kauã | Chat em tempo real no Node |
| #26 | Chat no frontend | Kauã | Interface de chat com WebSocket |

### Milestone v0.5 — Deploy + Polish (Semana 8)

| # | Issue | Quem | O que é |
|---|-------|------|---------|
| #27 | Deploy Render.com | Ambos | 3 serviços + banco online |
| #28 | Teste end-to-end | Ambos | 2 usuários reais testando |
| #29 | Loading states e erros | Kauã | UX polish |

---

## 5. SESSÕES DE LEITURA — O QUE LER JUNTOS

### Como ler os docs juntos

```
1. Entrem na call do Discord (voz)
2. Cada um abre o doc na SUA tela (não precisa compartilhar tela)
3. Leiam ao mesmo tempo, cada um no seu ritmo
4. Terminou? Espera o outro
5. Discutam: "entendeu tudo?" → dúvidas → próximo doc
6. Links externos (learngitbranching, sqlbolt):
   → NÃO abram agora — são pra Semana 0
   → Só anotem: "tenho que fazer isso depois"
```

### Sessão 1 — Entender o projeto (45 min)

| Ordem | Documento | Tempo | O que vão entender |
|-------|-----------|-------|---------------------|
| 1 | **[README.md](../README.md)** | 10 min | Visão geral, arquitetura, quem faz o quê |
| 2 | **[01-manifesto.md](01-manifesto.md)** | 10 min | Regras da dupla, cultura |
| 3 | **[03-requisitos-funcionais.md](03-requisitos-funcionais.md)** | 5 min | As 7 funcionalidades do MVP |
| 4 | **[12-guia-de-aprendizado.md](12-guia-de-aprendizado.md)** | 15 min | Como ler docs, pesquisar, resolver problemas (**ESSENCIAL**) |
| 5 | **[05-stack-e-decisoes.md](05-stack-e-decisoes.md)** | 5 min | Tecnologias e por quê |

**Resultado:** vocês sabem O QUE vão construir e COM O QUE.

### Sessão 2 — Entender a técnica (30 min)

| Ordem | Documento | Tempo | O que vão entender |
|-------|-----------|-------|---------------------|
| 5 | **[06-integracao-java-node.md](06-integracao-java-node.md)** | 10 min | Como Java e Node conversam |
| 6 | **[07-modelo-de-dados.md](07-modelo-de-dados.md)** | 10 min | As 4 tabelas do banco |
| 7 | **[08-contrato-de-api.md](08-contrato-de-api.md)** | 10 min | Todas as rotas e eventos |

**Resultado:** vocês entendem COMO as peças se encaixam.

### Sessão 3 — Preparar para codar (30 min)

| Ordem | Documento | Tempo | O que vão entender |
|-------|-----------|-------|---------------------|
| 8 | **[14-setup-ambiente.md](14-setup-ambiente.md)** | 10 min | Instalar tudo (façam juntos ao vivo) |
| 9 | **[15-git-workflow.md](15-git-workflow.md)** | 15 min | Branches, PRs, conflitos |
| 10 | **[18-cronograma.md](18-cronograma.md)** | 5 min | O que fazer cada semana |

**Resultado:** vocês sabem O QUE FAZER AMANHÃ.

### Não precisam ler agora (consultam quando precisar)

| Documento | Quando consultar |
|-----------|-----------------|
| [09-deploy.md](09-deploy.md) | Semana 8, quando forem deployar |
| [11-guia-de-contribuicao.md](11-guia-de-contribuicao.md) | Quando fizerem o primeiro PR |
| ~~12-guia-de-aprendizado.md~~ | **Movido pra Sessão 1 — leitura OBRIGATÓRIA** |
| [16-glossario.md](16-glossario.md) | Quando não entenderem um termo |
| [19-wireframes.md](19-wireframes.md) | Quando forem construir as telas |

---

## 6. METODOLOGIA — O DIA A DIA

### Comunicação — Decisão final

**Discord** para o dia a dia. **GitHub** para o que é do código. Ponto.

| Para quê | Onde | Por quê |
|----------|------|---------|
| Standup diário ("fiz X, vou Y") | **Discord** → canal `#standup` | Rápido, 5 min, não precisa ser formal |
| Pergunta rápida ("tá rodando aí?") | **Discord** → canal `#geral` | Resposta instantânea |
| Pair programming / call de voz | **Discord** → canal de voz | Já estão lá |
| Travou em algo técnico | **GitHub Issues** → comentário na issue | Fica documentado e vinculado ao código |
| Decisão de design ("usamos X ou Y?") | **GitHub Discussions** | Ambos argumentam por escrito, decisão fica registrada |
| PR pronto pra review | **GitHub PR** | Parceiro recebe notificação automática |
| Aprendizado / o que descobri | **GitHub Issues** → comentário na issue | Vira documentação viva |

> **Discord ≠ WhatsApp.** Discord tem canais separados, histórico pesquisável, e não mistura vida pessoal. Criem um servidor privado com 3 canais: `#geral`, `#standup`, `#bugs`.

> **WhatsApp: NÃO.** Pode usar pra combinar horário de call, mas discussão técnica NUNCA vai pro WhatsApp. Se mandou um erro no WhatsApp, já começou errado.

### IA — NÃO nas primeiras 4 semanas. Depois, com regras.

**Por que NÃO usar IA agora (semanas 1-4):**

| Motivo | Explicação |
|--------|-----------|
| **O desconforto ensina** | Gastar 30 min lendo docs e finalmente entender = gruda pra sempre. IA explica em 10 seg = esquece em 10 min. |
| **A 42 proíbe na Piscine** | Na Piscine: `man pages`, Google, colegas. Se se acostumar com IA agora, vai travar lá. |
| **Buscar > saber** | Saber navegar docs, ler Stack Overflow em inglês, formular a pergunta certa — esse é o skill que a 42 cobra. IA pula isso. |
| **Falsa confiança** | Você acha que entendeu porque a explicação foi clara. Mas não testou, não errou, não debugou. |

### Semanas 1-4: ZERO IA. Use apenas isso:

| Travou em... | Faça isso | Recurso exato |
|-------------|-----------|---------------|
| Não sei o que é [termo] | Glossário do repo → doc oficial | `16-glossario.md` → MDN / spring.io |
| Não sei a sintaxe | Google: "how to [X] in [linguagem]" | Stack Overflow (leia, não copie) |
| Erro que não entendo | Google o erro EXATO entre aspas | `"Cannot read property of undefined"` |
| Não sei como começar | Leia o ÍNDICE do tutorial oficial | javascript.info índice / dev.java/learn |
| Dúvida de design | Discuta com Rafael | GitHub Discussions |
| 45 min travado | Documenta na issue → chama parceiro | GitHub Issues |

**DICA:** pesquise em **inglês**. Os resultados são 10x melhores. Mesmo que leia devagar no início, é um investimento que vale pra carreira inteira.

### A partir da semana 5: IA com regras estritas

Depois de 4 semanas com docs + Google + parceiro, vocês terão:
- Vocabulário técnico real (sabem NOMEAR o que não sabem)
- Muscle memory de buscar em documentação
- Experiência de debugar lendo erros

**Aí sim**, a IA vira ferramenta útil (não muleta):

| ✅ PODE | ❌ NÃO PODE |
|---------|-------------|
| "O que é middleware?" → conceito | "Faz o endpoint pra mim" → gerar código |
| "O que esse erro significa?" → entender | "Resolve esse erro" → fazer por você |
| "Explica esse trecho linha por linha" | "Cria a tela de dashboard" |
| "Prós e contras de A vs B?" → design | "Qual é melhor?" → decidir por você |

**Se usar IA na semana 5+, use este prompt:**

```
Você é meu colega de estudo, não meu professor. REGRAS:
1. NUNCA me dê código pronto. Explique o conceito e eu implemento.
2. Se eu pedir código, pergunte: "o que você já tentou?"
3. Use analogias simples.
4. Se eu estiver errado, me faça perguntas que me levem a perceber sozinho.
5. Pode mostrar SINTAXE, mas não LÓGICA.
6. Sempre me indique a página EXATA da documentação oficial.
```

**Prompts por situação (semana 5+):**

| Situação | Prompt |
|----------|--------|
| Não entendo conceito | "Explica [X] com analogia. Me indica a doc oficial pra ler." |
| Não sei começar issue | "Quais conceitos preciso? Em que ordem? Me indica onde ler." |
| Erro que não entendo | "O que esse erro diz? NÃO resolva. Me indica onde ler." |
| Código que encontrei | "Explica linha por linha: o que faz e POR QUE." |
| Dúvida de design | "Prós e contras de A vs B. NÃO escolha por mim." |

### Resumo definitivo

```
SEMANAS 1-4:  Docs oficiais + Google + parceiro. ZERO IA.
SEMANA 5+:    IA como colega socrático (conceitos, nunca código).
SEMPRE:       Doc oficial é a fonte primária. IA complementa, não substitui.
```

### Ritual semanal

```
SEGUNDA (15 min): Abrem o board → cada um pega 1 issue
DIÁRIO  (5 min):  Discord #standup: "fiz X, vou fazer Y, travei em Z"
DOMINGO (15 min): Call no Discord: mostra o que fez → planeja próxima semana
```

### GitHub Projects — Board Kanban

```
┌──────────┬──────────┬───────────┬───────────┐
│ Backlog  │ Fazendo  │ Revisão   │ Concluído │
│          │ (máx 1)  │ (PR)      │           │
└──────────┴──────────┴───────────┴───────────┘
```

> **IMPORTANTE:** O board no GitHub Projects precisa ser configurado por vocês. Vá em github.com/devkauapimentel/LitCircle → aba "Projects" → New project → Board → Crie as colunas acima → Adicione as issues.

---

## 7. CHECKLIST ANTES DE CODAR

Depois de ler todos os docs, vocês devem conseguir responder:

- [ ] O que o LitCircle faz?
- [ ] Quais tecnologias usamos e por quê?
- [ ] O que o Spring Boot faz vs o que o Node.js faz?
- [ ] Quantas tabelas tem no banco e quais são?
- [ ] Como os dois backends se comunicam?
- [ ] O que é uma branch, um commit e um PR?
- [ ] Como funciona sem Docker e por que tá tudo bem?
- [ ] Qual é a minha primeira issue?
- [ ] Onde busco ajuda quando travar?

---

## 8. "MAS QUANDO VAMOS CRIAR TUDO DO ZERO?"

### O que aconteceu aqui

Um arquiteto (no caso, a IA) fez o que um **tech lead faz em qualquer empresa**:
- Definiu a stack
- Desenhou a arquitetura
- Modelou o banco
- Criou as issues
- Escreveu a documentação

Vocês são os **desenvolvedores**. Vocês **executam** o plano, aprendem fazendo, e tomam decisões técnicas dentro de cada issue (como implementar, qual algoritmo usar, como organizar o código).

### Isso é trapaça?

**Não.** É exatamente como funciona em 100% das empresas. Ninguém começa um emprego novo e planeja a arquitetura do sistema inteiro. Você recebe issues, entende o sistema lendo a documentação, e executa.

### Quando vocês VÃO planejar do zero?

**No próximo projeto.** Depois de construir o LitCircle, vocês terão experiência real com:
- REST APIs
- Banco de dados
- Autenticação
- WebSocket
- Deploy
- Git workflow
- Trabalho em dupla

Aí no próximo projeto (ver [PROJETOS-FUTUROS.md](../PROJETOS-FUTUROS.md)), **vocês** vão:

```
1. Definir o problema
2. Escolher a stack (com conhecimento real, não chute)
3. Desenhar a arquitetura
4. Modelar o banco
5. Criar as issues
6. Estimar prazos
7. Executar
```

**O LitCircle ensina a CONSTRUIR. O próximo projeto ensina a ARQUITETAR.**

### O que vocês JÁ vão decidir no LitCircle

Dentro de cada issue, vocês tomam dezenas de decisões reais:
- Como organizar os arquivos?
- Qual nome dar pra variável/função?
- Como validar o input do usuário?
- Como tratar erros?
- Qual query SQL usar?
- Como estilizar a tela?
- Como lidar com estados (loading, erro, vazio)?

Isso **é** engenharia de software. Não precisa definir a stack do zero pra estar aprendendo.

---

## 9. COMO APRENDER COISAS NOVAS — O PROTOCOLO

Quando vocês travarem em algo que não sabem (e VAI acontecer, toda issue), sigam este protocolo **nessa ordem**:

### Passo 0: Descubra QUAL TIPO de dúvida você tem

Existem dois tipos de dúvida. O caminho é diferente pra cada uma:

**Tipo A — Conceitual: "O que é X? Por que funciona assim?"**

| Dúvida | Onde está a resposta |
|--------|---------------------|
| "O que é branch, commit, PR?" | [15-git-workflow.md](15-git-workflow.md) — ensina Git do absoluto zero |
| "Por que as pastas são assim?" | [README.md](../README.md) — explica cada pasta e arquivo |
| "Por que dois backends?" | [05-stack-e-decisoes.md](05-stack-e-decisoes.md) + [06-integracao-java-node.md](06-integracao-java-node.md) |
| "O que é REST? JWT? WebSocket?" | [16-glossario.md](16-glossario.md) — dicionário de termos |
| "O que é migration? FK? UUID?" | [07-modelo-de-dados.md](07-modelo-de-dados.md) — banco explicado pra iniciante |
| "Como funciona o deploy?" | [09-deploy.md](09-deploy.md) — passo a passo |
| "Como fazer PR e code review?" | [11-guia-de-contribuicao.md](11-guia-de-contribuicao.md) |
| "O que é MVC? Camadas? DTO?" | [16-glossario.md](16-glossario.md) + estrutura no README |

**A resposta de dúvidas conceituais está DENTRO do repositório.** Leiam os docs antes de buscar fora.

**Tipo B — Técnica: "Como faço X no código?"**

| Dúvida | Onde buscar |
|--------|------------|
| "Como fazer fetch() em JavaScript?" | Doc oficial → javascript.info |
| "Como criar endpoint no Spring Boot?" | Doc oficial → spring.io/guides |
| "Como usar Socket.IO?" | Doc oficial → socket.io/docs |
| "Como escrever SQL?" | Doc oficial → sqlbolt.com |

**A resposta de dúvidas técnicas está na documentação oficial da tecnologia.** Siga os passos abaixo.

**Tipo C — Estrutural: "Eu nem sei O QUE preciso aprender pra resolver isso"**

Esse é o caso mais difícil. Exemplo: a issue pede "validar o email do usuário no cadastro" e você nem sabe que precisa de uma **função**, nem o que é uma função.

**Por isso a Semana 0 existe.** Os recursos de estudo da Semana 0 te dão o **vocabulário mínimo** pra pelo menos NOMEAR o que não sabe:

| Estudo da Semana 0 | O que te dá |
|--------------------|-------------|
| JS (javascript.info cap 4-11) | Sabe o que é: variável, função, array, objeto, loop, if/else, async/await |
| Java (dev.java/learn) | Sabe o que é: classe, método, interface, exceção |
| SQL (sqlbolt.com) | Sabe o que é: tabela, SELECT, INSERT, WHERE, JOIN |
| HTTP (MDN) | Sabe o que é: GET, POST, status code, header, body |
| Git (learngitbranching) | Sabe o que é: commit, branch, merge, push, pull |

Depois da Semana 0, você consegue pelo menos dizer: *"Eu sei que preciso de uma função, mas não sei como escrever."* — e aí cai no **Tipo B** (doc oficial).

**E se MESMO ASSIM não souber?** Use estas ferramentas para DESCOBRIR o que precisa:

### Ferramentas de descoberta (ONDE pesquisar quando nem sabe o que pesquisar)

| Ferramenta | Como usar | Exemplo |
|-----------|-----------|---------|
| **Google** | Pesquise o PROBLEMA, não a solução | "como verificar se email é válido javascript" → descobre que existe regex |
| **MDN Web Docs** | Referência completa de HTML/CSS/JS | Pesquise qualquer coisa web ali: mdn.dev |
| **Stack Overflow** | Perguntas/respostas reais de devs | Pesquise em inglês: "how to [problema] in [linguagem]" |
| **javascript.info** | Tutorial completo de JS com exemplos | Leia o índice — cada capítulo é um conceito |
| **dev.java/learn** | Tutorial completo de Java | Mesmo princípio: leia o índice |
| **Parceiro** | Após 45 min travado, documenta na issue e chama | Discord #bugs + link da issue |

### O método na prática — 3 exemplos REAIS do LitCircle

---

#### Exemplo 1: Dúvida de DESIGN — "Devo copiar HTML ou reutilizar?"

**Situação:** Kauã terminou `login.html` e vai criar `dashboard.html`. Dashboard precisa do mesmo sidebar/menu que a tela de sessão vai ter. Pensa: "copio e colo o sidebar em todo HTML?"

```
1. INCÔMODO: "Se eu copiar, quando mudar o menu vou ter que mudar em 5 arquivos"
   → Seu cérebro diz "isso tá errado" → ESSE É O SINAL de dúvida de design

2. FORMULA: "como reutilizar HTML entre várias páginas sem React"

3. PESQUISA: Google → "how to reuse HTML across pages vanilla javascript"

4. DESCOBRE: 3 resultados aparecem:
   a) copy-paste (ruim — manutenção impossível)
   b) JavaScript que injeta os elementos comuns ← ESSE
   c) Web Components (avançado, pra depois)

5. IMPLEMENTA a opção (b):
```

```javascript
// frontend/js/components.js — roda em TODAS as páginas

function renderSidebar() {
  const sidebar = document.createElement('nav');
  sidebar.className = 'sidebar';
  sidebar.innerHTML = `
    <div class="logo">📚 LitCircle</div>
    <a href="/pages/dashboard.html" class="nav-link">Dashboard</a>
    <a href="/pages/create-session.html" class="nav-link">Criar Sessão</a>
    <button onclick="logout()" class="nav-link">Sair</button>
  `;
  document.body.prepend(sidebar);
}

// Chama quando a página carrega
document.addEventListener('DOMContentLoaded', renderSidebar);
```

```html
<!-- Em TODA página que precisa do sidebar: -->
<script src="/js/components.js"></script>
```

```
6. RESULTADO: sidebar aparece em todas as páginas. Muda em 1 lugar, muda em todas.
7. ANOTA na issue: "Descobri que JS pode injetar HTML. Criei components.js."
```

**O sinal de dúvida de design:** quando algo parece **repetitivo** ou **errado**, você tem um problema de design. Google: "how to [evitar a repetição] in [tecnologia]".

---

#### Exemplo 2: Dúvida TÉCNICA — "Como guardar o token do login?"

**Situação:** Kauã fez a tela de login (Issue #13). O fetch retorna o JWT. Agora precisa "salvar o token" — mas onde? Como? O critério de aceite diz `Token salvo no localStorage`.

```
1. LÊ a issue → critério: "Token salvo no localStorage"
   → A issue DISSE onde guardar (localStorage), mas Kauã não sabe o que é

2. PESQUISA: Google → "o que é localStorage javascript"
   → Descobre: é um armazenamento no navegador que persiste entre páginas

3. DOC OFICIAL: MDN → "Window.localStorage"
   → Aprende: localStorage.setItem('chave', 'valor')
   → Aprende: localStorage.getItem('chave')

4. IMPLEMENTA:
```

```javascript
// Após login com sucesso:
const response = await fetch(`${CONFIG.API_URL}/api/auth/login`, {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ email, password })
});

const data = await response.json();

if (response.ok) {
  localStorage.setItem('token', data.token);     // salva
  localStorage.setItem('userName', data.user.name);
  window.location.href = '/pages/dashboard.html'; // redireciona
} else {
  showError('Email ou senha incorretos');
}

// Em QUALQUER outra página que precisa autenticar:
const token = localStorage.getItem('token');
if (!token) {
  window.location.href = '/pages/login.html'; // não logado → volta pro login
}
```

```
5. RESULTADO: login funciona, token salvo, redirecionamento ok.
6. ANOTA na issue: "localStorage persiste entre páginas. setItem/getItem."
```

---

#### Exemplo 3: Dúvida de INTEGRAÇÃO — "O Spring Boot tá retornando erro de CORS"

**Situação:** Kauã terminou a tela de login e faz `fetch()` pro backend do Rafael. O navegador mostra: `Access to fetch has been blocked by CORS policy`. Nenhum dos dois sabe o que é CORS.

```
1. LÊ O ERRO: "blocked by CORS policy"
   → Não sabe o que é → olha 16-glossario.md → "CORS: mecanismo do navegador
     que bloqueia requests para domínios diferentes"

2. ENTENDE: frontend tá em localhost:5500, Spring Boot em localhost:8080
   → São "domínios diferentes" → navegador bloqueia por segurança

3. PESQUISA: Google → "como resolver CORS spring boot"

4. DESCOBRE: Rafael precisa adicionar uma config no Spring Boot:
```

```java
// backend-java — CorsConfig.java
@Configuration
public class CorsConfig {
    @Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurer() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/api/**")
                    .allowedOrigins("http://localhost:5500")
                    .allowedMethods("GET", "POST", "PUT", "DELETE")
                    .allowedHeaders("*");
            }
        };
    }
}
```

```
5. RESULTADO: frontend e backend se comunicam.
6. ANOTAM na issue: "CORS = navegador bloqueia cross-origin. Config no Spring."
7. LIÇÃO: erros de integração geralmente são de infra (CORS, porta, URL),
   não de lógica. Leiam o ERRO, não adivinhem.
```

---

### Resumo: como descobrir a resposta de QUALQUER dúvida

| Tipo de dúvida | Como identificar | O que fazer |
|----------------|------------------|-------------|
| **Design** — "devo copiar ou reutilizar?" | Algo parece **repetitivo** ou **errado** | Google: "how to avoid [repetição] in [tech]" |
| **Técnica** — "como faço X?" | A issue pede algo que **não sei fazer** | Google: "como [o que a issue pede] em [linguagem]" → doc oficial |
| **Integração** — "por que não funciona junto?" | O **erro** aparece quando duas partes se conectam | **Leia o erro** → Google o erro **exato** → quase sempre é config |
| **Conceito** — "o que é X?" | Aparece um **termo** que não entendo | Glossário (16) → se não tiver, Google: "o que é [termo] programação" |

**A issue te diz O QUE fazer. O Google te diz COMO se chama. A doc oficial te ensina a FAZER.**

---

### Passo 1: Identifique o que não sabe (2 min)

Escreva em uma frase: "Eu não sei como ___"

Exemplos:
- "Eu não sei como fazer um POST com fetch no JavaScript" → **Tipo B** → doc oficial
- "Eu não sei o que é uma migration" → **Tipo A** → doc 07 do repo
- "Eu não sei como validar JWT no Spring Boot" → **Tipo B** → doc oficial
- "Eu não sei por que usamos duas portas" → **Tipo A** → doc 06 do repo

### Passo 2: Busque na fonte certa (30-60 min)

| Tecnologia | Documentação oficial | Onde buscar |
|-----------|---------------------|-------------|
| JavaScript | [javascript.info](https://javascript.info) | Capítulos por tema |
| Node/Express | [expressjs.com](https://expressjs.com) | Guide → seção relevante |
| HTML/CSS | [developer.mozilla.org](https://developer.mozilla.org/pt-BR/) | Pesquise o elemento/propriedade |
| Java | [dev.java/learn](https://dev.java/learn) | Tutorial oficial |
| Spring Boot | [spring.io/guides](https://spring.io/guides) | Guide específico do tema |
| PostgreSQL | [postgresql.org/docs](https://www.postgresql.org/docs/) | Referência SQL |
| Socket.IO | [socket.io/docs](https://socket.io/docs/v4/) | Get Started + guides |
| Git | [git-scm.com/book](https://git-scm.com/book/pt-br/v2) | Pro Git Book (em português!) |
| JWT | [jwt.io/introduction](https://jwt.io/introduction) | Página única |

**REGRA: sempre a doc oficial PRIMEIRO.** Vídeo do YouTube é o ÚLTIMO recurso, não o primeiro.

### Passo 3: Tente implementar (30+ min)

Escreva o código. Vai dar erro. Leia o erro. Tente de novo. Isso É o aprendizado.

### Passo 4: Se travar 45 min → Documente → Chame o parceiro

Escreva **na issue do GitHub** (não no WhatsApp!):
```
TRAVEI em: [descreva o problema]
O QUE TENTEI: [o que já fez]
ERRO: [cola a mensagem de erro]
```

Se for urgente, manda no Discord `#bugs` com link pro comentário da issue.

O parceiro tenta ajudar. Se nenhum dos dois souber, pesquisem JUNTOS na doc oficial.

### Passo 5: Após resolver → Anote o que aprendeu

Faça um comentário na issue do GitHub explicando o que aprendeu. Isso vira documentação viva do projeto e ajuda vocês no futuro.

---

## 10. LISTA COMPLETA DE TUDO QUE EXISTE NO REPOSITÓRIO

### Documentos que DEVEM ser lidos (em ordem)

| # | Documento | O que é | Quando ler |
|---|-----------|---------|------------|
| 0 | **[README.md](../README.md)** | Visão geral do projeto, arquitetura, estrutura | **Agora — Sessão 1** |
| 1 | **[01-manifesto.md](01-manifesto.md)** | Filosofia, regras da dupla, cultura | **Agora — Sessão 1** |
| 2 | **[03-requisitos-funcionais.md](03-requisitos-funcionais.md)** | 7 funcionalidades do MVP | **Agora — Sessão 1** |
| 3 | **[05-stack-e-decisoes.md](05-stack-e-decisoes.md)** | Stack completa + 5 decisões de arquitetura | **Agora — Sessão 1** |
| 4 | **[06-integracao-java-node.md](06-integracao-java-node.md)** | Como Java e Node conversam via JWT | **Agora — Sessão 2** |
| 5 | **[07-modelo-de-dados.md](07-modelo-de-dados.md)** | 4 tabelas do banco com SQL pronto | **Agora — Sessão 2** |
| 6 | **[08-contrato-de-api.md](08-contrato-de-api.md)** | Todas as rotas REST e eventos WebSocket | **Agora — Sessão 2** |
| 7 | **[14-setup-ambiente.md](14-setup-ambiente.md)** | Instalar Git, Node, Java, PostgreSQL | **Agora — Sessão 3** |
| 8 | **[15-git-workflow.md](15-git-workflow.md)** | Git do zero: conceitos, comandos, PRs, conflitos | **Agora — Sessão 3** |
| 9 | **[18-cronograma.md](18-cronograma.md)** | Roadmap de 8 semanas | **Agora — Sessão 3** |

### Documentos de CONSULTA (leiam quando precisarem)

| # | Documento | O que é | Quando consultar |
|---|-----------|---------|-----------------|
| 10 | [09-deploy.md](09-deploy.md) | Deploy 100% grátis no Render.com | Semana 8 |
| 11 | [11-guia-de-contribuicao.md](11-guia-de-contribuicao.md) | Template de PR, code review | Ao fazer o 1º PR |
| 12 | [12-guia-de-aprendizado.md](12-guia-de-aprendizado.md) | Mapa de estudo: o que estudar por fase | Quando travar |
| 13 | [16-glossario.md](16-glossario.md) | Termos técnicos explicados | Quando não entender um termo |
| 14 | [17-issues-github.md](17-issues-github.md) | Todas as 26 issues detalhadas | Referência |
| 15 | [19-wireframes.md](19-wireframes.md) | Desenho das telas em ASCII | Quando for construir as telas |

### Outros arquivos importantes

| Arquivo | O que é |
|---------|---------|
| [PROJETOS-FUTUROS.md](../PROJETOS-FUTUROS.md) | Roadmap de evolução: React, Docker, TypeScript, IoT |
| [.gitignore](../.gitignore) | Arquivos que o Git ignora (node_modules, .env, etc) |
| `frontend/config.js` | URLs dos backends (dev vs produção) |
| `backend-node/.env.example` | Template de variáveis de ambiente do Node |

---

## 11. RESUMO — O CAMINHO COMPLETO

```
FASE 0 — AGORA (1 dia)
├── Leiam os docs juntos (3 sessões de 30 min)
├── Instalem o ambiente (doc 14)
├── Estudem Git (learngitbranching.js.org, 1h)
├── Estudem SQL (sqlbolt.com, 2h)
├── Kauã: JS moderno (javascript.info, 2h)
└── Rafael: Java básico (dev.java/learn, 3h)

FASE 1 — MVP (8 semanas)
├── Semana 1:   Issues #4-#8 (boilerplate + setup)
├── Semana 2-3: Issues #9-#15 (autenticação)
├── Semana 4-5: Issues #16-#23 (sessões)
├── Semana 6-7: Issues #24-#26 (chat)
└── Semana 8:   Issues #27-#29 (deploy + polish)

FASE 2 — EVOLUÇÃO (depois do MVP)
├── React no frontend
├── Docker para empacotamento
├── Testes automatizados
└── Ver PROJETOS-FUTUROS.md

FASE 3 — PRÓXIMO PROJETO (vocês arquitetam do zero)
├── VOCÊS definem o problema
├── VOCÊS escolhem a stack
├── VOCÊS desenham a arquitetura
├── VOCÊS modelam o banco
├── VOCÊS criam as issues
└── Agora sabem o que estão fazendo porque CONSTRUÍRAM antes
```

**Primeiro passo literal: abram `docs/00-comece-aqui.md` juntos e leiam da Sessão 1 até a Sessão 3.**
