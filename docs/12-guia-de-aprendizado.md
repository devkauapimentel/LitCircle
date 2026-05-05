# Guia de aprendizado — do zero ao LitCircle

> Este documento responde a pergunta mais importante antes de escrever qualquer linha de código: **o que precisamos aprender, em qual ordem e como aprender de verdade?**

Vocês são dois iniciantes em learning-by-doing. Isso não é fraqueza — é a forma mais eficiente de aprender engenharia. Mas precisa de estrutura. Este guia define o mapa de aprendizado completo para o Kauã e para o Rafael, separados por domínio.

---

## Princípio fundamental de aprendizado deste projeto

**Não aprenda uma tecnologia antes de precisar dela.**

Não assista 40 horas de curso de React antes de escrever um componente. Não leia o livro inteiro de Spring Boot antes de criar uma rota. O caminho é:

1. Leia a documentação oficial da tecnologia por 30–60 minutos para entender o conceito geral
2. Tente implementar a funcionalidade da sua issue atual
3. Trave em algo específico
4. Busque a resposta na documentação, em livros ou com o parceiro
5. Implemente
6. Reflita sobre o que aprendeu

Esse ciclo, repetido 200 vezes ao longo do projeto, vale mais que qualquer bootcamp.

---

## Mapa de aprendizado do Kauã

Kauã trabalha em: **Frontend (React) + Backend Node.js (WebSocket, Pomodoro, chat)**

### Fase 1 — Fundamentos obrigatórios (antes de qualquer milestone)

**JavaScript moderno (ES6+)**

Você precisa dominar isso antes de tudo. Sem isso, React e Node.js vão ser sofrimento puro.

Conceitos obrigatórios:
- Arrow functions, destructuring, spread/rest
- Promises, async/await
- Array methods: map, filter, reduce, find, some
- Módulos: import/export
- Classes (para entender o que o React faz por baixo)

Recursos (nesta ordem):
1. [javascript.info](https://javascript.info) — melhor material gratuito de JS moderno, leia do capítulo 4 ao 11
2. Livro: **"You Don't Know JS"** (série gratuita no GitHub: github.com/getify/You-Dont-Know-JS) — leia "Get Started" e "Scope & Closures"
3. Pratique: faça todos os exercícios do site [exercism.org](https://exercism.org) na trilha de JavaScript (pelo menos 20 exercícios)

**Git e GitHub (fundamental para trabalhar em dupla)**

Conceitos obrigatórios:
- Branches, merge, rebase
- Como resolver conflitos
- Pull Requests e code review
- .gitignore

Recursos:
1. [git-scm.com/book](https://git-scm.com/book) — Pro Git Book, gratuito, leia os capítulos 1, 2 e 3
2. [learngitbranching.js.org](https://learngitbranching.js.org) — prática visual e interativa, faça todos os níveis do "Main"

---

### Fase 2 — Frontend com React (Milestone v0.2 em diante)

**HTML e CSS (se ainda não domina)**

Recursos:
1. [developer.mozilla.org/pt-BR/docs/Web/HTML](https://developer.mozilla.org/pt-BR/docs/Web/HTML) — MDN Web Docs, leia os guias de HTML e CSS
2. Pratique: construa 3 páginas estáticas (landing page, formulário de login, lista de itens) antes de tocar em React

**React**

Conceitos obrigatórios, nesta ordem:
1. O que é um componente e JSX
2. Props e State (useState)
3. useEffect — como funciona o ciclo de vida
4. Renderização condicional e listas
5. Formulários controlados
6. React Router (navegação entre páginas)
7. Context API (estado global simples)
8. React Query (cache de dados do servidor)

Recursos:
1. [react.dev](https://react.dev) — **documentação oficial**, tem tutoriais interativos. Comece pelo "Learn React" no menu. É o melhor recurso existente.
2. [vitejs.dev](https://vitejs.dev) — documentação do Vite, leia o "Getting Started"
3. Livro: **"Road to React"** de Robin Wieruch — gratuito em [roadtoreact.com](https://roadtoreact.com), é o melhor livro prático de React para iniciantes

Método de estudo para React:
- Não assista vídeo antes de ler a documentação
- Para cada conceito, leia, feche a documentação e tente usar sem olhar
- Se travar por mais de 20 minutos, releia a documentação

**TailwindCSS**

Recursos:
1. [tailwindcss.com/docs](https://tailwindcss.com/docs) — documentação oficial tem playground interativo
2. Extensão VSCode: "Tailwind CSS IntelliSense" — instale antes de começar

---

### Fase 3 — Backend Node.js (Milestone v0.5 em diante)

**Node.js e Express**

Conceitos obrigatórios:
1. Como o Node.js funciona (event loop, non-blocking I/O) — entender isso explica POR QUÊ Node é bom para WebSocket
2. HTTP: o que são métodos, status codes, headers, body
3. Express: rotas, middlewares, tratamento de erros
4. Variáveis de ambiente com dotenv
5. Estrutura de um projeto Node.js

Recursos:
1. [nodejs.org/en/docs](https://nodejs.org/en/docs) — documentação oficial, leia "Introduction to Node.js"
2. [expressjs.com/pt-br](https://expressjs.com/pt-br) — documentação oficial do Express, faça o tutorial "Hello World" e leia sobre Routing e Middleware
3. Livro: **"Node.js Design Patterns"** de Mario Casciaro — não precisa ler tudo agora, use como referência

**WebSocket e Socket.IO**

Conceitos obrigatórios:
1. O que é WebSocket e como difere de HTTP
2. Eventos no Socket.IO (emit, on, rooms)
3. Como gerenciar múltiplos clientes

Recursos:
1. [socket.io/docs/v4](https://socket.io/docs/v4) — documentação oficial, leia "Get started" e "Rooms"
2. Assista: o vídeo oficial de introdução do Socket.IO no YouTube é excelente (15 minutos)

**Redis**

Conceitos obrigatórios:
1. O que é um banco chave-valor e quando usar
2. Strings, Lists, Sets, Hashes no Redis
3. TTL (expiração de chaves)

Recursos:
1. [redis.io/docs](https://redis.io/docs) — documentação oficial, leia "Introduction" e "Data types"
2. [try.redis.io](https://try.redis.io) — terminal interativo no browser, pratique os comandos básicos

---

### Fase 4 — Ferramentas de desenvolvimento

**Docker (para rodar banco local)**

Kauã não precisa dominar Docker profundamente — apenas o suficiente para usar o `docker-compose.yml` que está no projeto.

Conceitos mínimos necessários:
- O que é um container e por que usar
- `docker compose up` e `docker compose down`
- O que é uma imagem vs container

Recursos:
1. [docs.docker.com/get-started](https://docs.docker.com/get-started) — tutorial oficial, faça apenas "Part 1: Getting started" e "Part 2: Containerize an application"
2. Para o dia a dia, o arquivo `docker-compose.yml` já está pronto no projeto — você só precisa rodar `docker compose up -d`

**Insomnia/Postman (para testar APIs)**

Recursos:
1. [insomnia.rest/download](https://insomnia.rest/download) — baixe e instale
2. A documentação de uso básico está em 5 minutos no próprio site
3. Use o `08-contrato-de-api.md` deste projeto para criar as requisições de teste

---

## Mapa de aprendizado do Rafael

Rafael trabalha em: **Backend Java com Spring Boot + PostgreSQL**

### Fase 1 — Fundamentos de Java (antes de Spring Boot)

**Java — fundamentos obrigatórios**

Rafael não sabe Java do zero — aqui está o caminho correto:

Conceitos obrigatórios, nesta ordem:
1. Sintaxe básica: variáveis, tipos, operadores, condicionais, loops
2. Orientação a objetos: classes, objetos, herança, interfaces, polimorfismo
3. Collections: List, Map, Set
4. Exceções: try/catch, throws, hierarquia
5. Generics
6. Streams e Lambdas (Java 8+) — muito usados no Spring Boot
7. Optional — evita NullPointerException

Recursos (nesta ordem):
1. Livro: **"Use a Cabeça! Java"** — o melhor livro para iniciantes em Java. Leia os capítulos 1 a 10 antes de tocar no Spring Boot.
2. [dev.java/learn](https://dev.java/learn) — tutorial oficial da Oracle, gratuito
3. [exercism.org](https://exercism.org) — trilha de Java, faça pelo menos 25 exercícios. É a melhor forma de praticar a sintaxe.
4. Livro (referência): **"Java: Como Programar"** de Deitel — não leia do começo, use como dicionário quando travar em algum conceito

**Git e GitHub** — mesmos recursos do Kauã, acima.

---

### Fase 2 — Spring Boot (Milestone v0.2 em diante)

Conceitos obrigatórios, nesta ordem:
1. O que é um framework e o que o Spring resolve
2. Injeção de dependência e IoC (Inversion of Control) — o coração do Spring
3. Spring MVC: controllers, request mapping, response body
4. Spring Data JPA: repositories, entidades, relacionamentos
5. Spring Security + JWT: autenticação e autorização
6. Validação com Bean Validation (@NotBlank, @Email, etc.)
7. Tratamento global de erros (@ControllerAdvice)
8. Profiles (dev/prod) e variáveis de ambiente

Recursos (nesta ordem):
1. [spring.io/guides](https://spring.io/guides) — guias oficiais do Spring. Faça nesta ordem:
   - "Building a RESTful Web Service"
   - "Accessing Data with JPA"
   - "Securing a Web Application"
2. [spring.io/projects/spring-boot](https://spring.io/projects/spring-boot) — documentação de referência. Use como consulta, não leia linearmente.
3. Livro: **"Spring Boot in Action"** de Craig Walls — leia os capítulos 1, 2 e 3 antes de começar a milestone v0.2
4. YouTube: canal **"Giuliana Bezerra"** — melhor conteúdo em português sobre Spring Boot, assistir antes de cada milestone nova funcionalidade

**PostgreSQL e SQL**

Conceitos obrigatórios:
1. SELECT, INSERT, UPDATE, DELETE
2. JOINs (INNER, LEFT)
3. Índices — o que são e quando usar
4. Transações
5. Como o JPA mapeia Java para SQL (você escreve Java, o Hibernate gera SQL)

Recursos:
1. [postgresql.org/docs/current/tutorial.html](https://www.postgresql.org/docs/current/tutorial.html) — tutorial oficial
2. [pgexercises.com](https://pgexercises.com) — exercícios práticos de SQL no browser, faça todos da seção "Basic" e "Joins"
3. DBeaver (ferramenta gratuita para visualizar o banco): [dbeaver.io](https://dbeaver.io)

**Flyway (migrations de banco)**

Recursos:
1. [flywaydb.org/documentation/getstarted](https://flywaydb.org/documentation/getstarted) — documentação oficial, leia o "Quick Start"
2. Conceito chave: cada migration é um arquivo SQL numerado que nunca é alterado após rodar

---

### Fase 3 — Ferramentas de desenvolvimento

**Docker** — mesmos recursos do Kauã, acima.

**Maven**

Conceitos mínimos:
- O que é o `pom.xml`
- Como adicionar uma dependência
- Comandos: `./mvnw test`, `./mvnw spring-boot:run`

Recursos:
1. [maven.apache.org/guides/getting-started](https://maven.apache.org/guides/getting-started) — leia apenas o "Maven in 5 Minutes"

---

## Recursos compartilhados — ambos precisam

### HTTP e APIs REST

Este é o conhecimento mais importante para o projeto. Ambos precisam dominar.

Conceitos obrigatórios:
1. O que é HTTP: request, response, headers, body
2. Métodos: GET, POST, PUT, PATCH, DELETE — qual usar em cada situação
3. Status codes: 200, 201, 204, 400, 401, 403, 404, 409, 500
4. O que é REST e o que o torna "RESTful"
5. JSON: sintaxe, tipos, como serializar/deserializar
6. Autenticação: o que é JWT, como funciona (header.payload.signature)
7. CORS: o que é e por que existe

Recursos:
1. [developer.mozilla.org/pt-BR/docs/Web/HTTP](https://developer.mozilla.org/pt-BR/docs/Web/HTTP) — MDN, leia "HTTP overview", "HTTP Methods" e "HTTP response status codes"
2. Livro: **"RESTful Web APIs"** de Leonard Richardson — leia os capítulos 1 a 4
3. [jwt.io/introduction](https://jwt.io/introduction) — explica JWT com exemplos interativos

### Segurança básica de aplicações web

Recursos:
1. [owasp.org/www-project-top-ten](https://owasp.org/www-project-top-ten) — leia pelo menos os 5 primeiros itens do OWASP Top 10. São as vulnerabilidades mais comuns que vocês precisam evitar.

### Banco de dados — conceitos gerais

Recursos:
1. Livro: **"Sistemas de Banco de Dados"** de Navathe — não leia tudo, use os capítulos 1, 2 (modelo relacional) e 14 (transações) como referência

---

## Ordem de estudo recomendada por milestone

| Milestone | Kauã estuda antes | Rafael estuda antes |
|---|---|---|
| v0.1 — Esqueleto | Git, JS moderno básico, como funciona HTTP | Git, Java básico (cap. 1-5 do Use a Cabeça), HTTP |
| v0.2 — Autenticação | React básico (componentes, state), React Router | Spring Boot básico (guia REST + JPA), Spring Security, JWT |
| v0.3 — Biblioteca | React Query, formulários em React | Spring Data JPA (relacionamentos), validações |
| v0.4 — Sessões | Context API ou Zustand | Transações no banco, lógica de negócio complexa |
| v0.5 — Chat | Socket.IO client, como funciona WebSocket | Apenas revisão — domínio do Kauã |
| v0.6 — Pomodoro | Node.js + Express básico, Redis client | Apenas revisão — domínio do Kauã |
| v0.7 — Progresso | React avançado (otimizações) | Queries complexas, Flyway migrations |
| v1.0 — MVP | Testes com Vitest | Testes com JUnit 5 |

---

## IDEs e ferramentas de desenvolvimento

### Kauã (Frontend + Node.js)

- **VSCode** — [code.visualstudio.com](https://code.visualstudio.com)

Extensões obrigatórias:
  - ESLint
  - Prettier
  - Tailwind CSS IntelliSense
  - ES7+ React/Redux/React-Native snippets
  - GitLens
  - Thunder Client (teste de API direto no VSCode)

### Rafael (Java + Spring Boot)

- **IntelliJ IDEA Community Edition** — gratuito, melhor IDE para Java [jetbrains.com/idea/download](https://www.jetbrains.com/idea/download)

Plugins obrigatórios:
  - Spring Boot (já incluso na versão Community com plugin)
  - Lombok

Alternativa gratuita: VSCode com extensão "Extension Pack for Java" da Microsoft — funciona, mas IntelliJ é superior para Java.

---

## Como não cair na armadilha do tutorial infinito

Os dois maiores inimigos do learning-by-doing são:

**1. Tutorial hell** — assistir vídeo atrás de vídeo sem construir nada. A sensação de progresso é falsa. Regra: para cada 1 hora de tutorial, 2 horas de prática.

**2. Paralisia por perfeição** — não começar porque "ainda não sabe o suficiente". A solução é simples: pegue a primeira issue da milestone v0.1 e comece. Você vai aprender o que precisa pelo caminho.

O sinal de que você aprendeu algo de verdade é conseguir explicar para o parceiro sem consultar nada. Se não consegue explicar, não aprendeu — aprendeu apenas a copiar.
