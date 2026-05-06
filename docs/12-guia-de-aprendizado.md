# Guia de aprendizado — do zero ao LitCircle

> O que precisam aprender, em qual ordem e como aprender de verdade.

---

## Princípio fundamental

**Não aprenda uma tecnologia antes de precisar dela.**

1. Leia a documentação oficial por 30-60 minutos
2. Tente implementar a funcionalidade da issue atual
3. Trave em algo específico
4. Busque na documentação ou com o parceiro
5. Implemente
6. Reflita

---

## Mapa do Kauã — Frontend + Node.js

### Fase 1 — Antes de codar (Semana 0)

**Git (1h):**
- [learngitbranching.js.org](https://learngitbranching.js.org) — faça todos os níveis "Main"

**JavaScript moderno (3h):**
- [javascript.info](https://javascript.info) — capítulos 4 a 11
- Foco em: arrow functions, async/await, destructuring, fetch API, array methods (map, filter)

**HTTP (1h):**
- [MDN HTTP Overview](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Overview)
- Entenda: GET, POST, PUT, DELETE, status codes (200, 201, 400, 401, 404)

**SQL (2h):**
- [sqlbolt.com](https://sqlbolt.com) — tutorial interativo completo

### Fase 2 — Durante o MVP (sob demanda)

| Quando precisar de... | Estude... | Recurso |
|----------------------|-----------|---------|
| Servidor HTTP | Node.js + Express | expressjs.com tutorial |
| Chat em tempo real | Socket.IO | socket.io/docs/v4 "Get Started" |
| Autenticação | JWT | jwt.io/introduction |
| CSS responsivo | Flexbox + Grid | css-tricks.com/guides |
| Formulários | HTML forms + fetch | MDN Forms Guide |

### Fase 3 — Após MVP (evolução)

- [ ] React: [react.dev](https://react.dev) "Learn React"
- [ ] TypeScript: typescriptlang.org handbook
- [ ] Docker: docs.docker.com/get-started (Parts 1-2)
- [ ] Testes: Jest docs

---

## Mapa do Rafael — Backend Java

### Fase 1 — Antes de codar (Semana 0)

**Git (1h):**
- [learngitbranching.js.org](https://learngitbranching.js.org)

**Java básico (5h ao longo da semana):**
- [dev.java/learn](https://dev.java/learn) — tutorial oficial
- Foco em: classes, objetos, herança, interfaces, Collections (List, Map), exceções
- [exercism.org](https://exercism.org) trilha Java — faça 15 exercícios

**HTTP (1h):**
- Mesmos recursos do Kauã

**SQL (2h):**
- [sqlbolt.com](https://sqlbolt.com)

### Fase 2 — Durante o MVP (sob demanda)

| Quando precisar de... | Estude... | Recurso |
|----------------------|-----------|---------|
| REST API | Spring Boot | spring.io/guides "Building a REST Service" |
| Banco de dados | Spring Data JPA | spring.io/guides "Accessing Data with JPA" |
| Autenticação | Spring Security + JWT | Giuliana Bezerra (YouTube) |
| Validação | Bean Validation | docs Spring |
| Migrations | Flyway | flywaydb.org quickstart |

### Fase 3 — Após MVP

- [ ] Testes: JUnit 5 + Mockito
- [ ] Docker: empacotando Spring Boot
- [ ] Microserviços: Spring Cloud (projetos futuros)

---

## Recursos compartilhados (ambos precisam)

| Tema | Recurso |
|------|---------|
| HTTP e REST | MDN HTTP docs |
| JWT | jwt.io/introduction |
| JSON | javascript.info cap. sobre JSON |
| Git | Pro Git Book cap. 1-3 (git-scm.com/book) |
| SQL | sqlbolt.com + pgexercises.com |
| Segurança web | OWASP Top 10 (os 5 primeiros) |

---

## IDEs e extensões

### Kauã — VSCode
- ESLint, Prettier, Thunder Client, GitLens, Live Server

### Rafael — IntelliJ IDEA Community
- Lombok, Rainbow Brackets

---

## Anti-padrões: o que NÃO fazer

1. **Tutorial hell:** para cada 1h de vídeo, 2h de código
2. **Paralisia:** não espere "saber o suficiente" — comece
3. **Copiar sem entender:** se não sabe explicar, não aprendeu
