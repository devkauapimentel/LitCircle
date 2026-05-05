# Cronograma e roadmap — LitCircle

> Planejamento realista considerando que são dois iniciantes dedicando 8–10 horas por semana cada. Ajuste conforme seu ritmo real.

---

## Premissas do planejamento

- **Ritmo:** 8–10 horas por semana por pessoa
- **Sprint:** 1 semana (segunda a domingo)
- **Velocidade inicial:** baixa (sprints 1–3) por conta do setup e aprendizado das ferramentas
- **Velocidade de cruzeiro:** alcançada a partir da sprint 4

Se o ritmo for menor (4–5h/semana), multiplique o tempo estimado por 1,5x.

---

## Roadmap por milestone

```
MÊS 1
─────────────────────────────────────────────────────────────
Sprint 1  │ v0.1 — Esqueleto
          │ Setup do repo, boilerplate dos 3 serviços, CI/CD,
          │ docker-compose, deploy básico no Railway/Vercel

Sprint 2  │ v0.2 — Autenticação (parte 1)
          │ Migration users, entidade JPA, endpoint de cadastro,
          │ configuração JWT no Spring Boot

Sprint 3  │ v0.2 — Autenticação (parte 2)
          │ Endpoint de login, tela de cadastro e login no React,
          │ contexto de autenticação, JWT no Node.js

MÊS 2
─────────────────────────────────────────────────────────────
Sprint 4  │ v0.3 — Biblioteca (parte 1)
          │ Migration books, CRUD de livros no Spring Boot

Sprint 5  │ v0.3 — Biblioteca (parte 2)
          │ Tela de biblioteca, modal de adicionar livro, favoritos

Sprint 6  │ v0.4 — Sessões (parte 1)
          │ Migrations de sessões, criar/entrar em sessão (backend)

Sprint 7  │ v0.4 — Sessões (parte 2)
          │ Encerrar sessão, gestão de participantes (backend)
          │ Tela de criar e entrar em sessão (frontend)

MÊS 3
─────────────────────────────────────────────────────────────
Sprint 8  │ v0.4 — Sessões (parte 3)
          │ Tela principal da sessão, lista de participantes,
          │ atualização de progresso

Sprint 9  │ v0.5 — Chat (parte 1)
          │ Servidor Socket.IO, eventos de chat, Redis

Sprint 10 │ v0.5 — Chat (parte 2)
          │ Componente de chat no React, notificações de presença

Sprint 11 │ v0.6 — Pomodoro (parte 1)
          │ Migrations streak, endpoint de registro, timer no Node.js

MÊS 4
─────────────────────────────────────────────────────────────
Sprint 12 │ v0.6 — Pomodoro (parte 2)
          │ Componente de timer no React, integração WebSocket

Sprint 13 │ v0.6 — Pomodoro (parte 3)
          │ Calendário de streak no React

Sprint 14 │ v0.7 — Progresso e rodízio (parte 1)
          │ Migrations, histórico de progresso, sistema de rodízio

Sprint 15 │ v0.7 — Progresso e rodízio (parte 2)
          │ Calendário de sessões no React

MÊS 5
─────────────────────────────────────────────────────────────
Sprint 16 │ v1.0 — Polimento (parte 1)
          │ Testes, tratamento de erros, rate limiting, CORS prod

Sprint 17 │ v1.0 — Polimento (parte 2)
          │ Testes e2e, 404, loading states, documentação final

🎉 MVP ENTREGUE
```

---

## Detalhamento por sprint

### Sprint 1 — v0.1 Esqueleto
**Meta:** "O ambiente está configurado, os três serviços sobem localmente e em produção"

| Issue | Responsável | Estimativa |
|---|---|---|
| #1 Setup do repositório | Ambos | 2h |
| #2 Boilerplate frontend | Kauã | 3h |
| #3 Boilerplate Node.js | Kauã | 2h |
| #4 Boilerplate Spring Boot | Rafael | 3h |
| #5 GitHub Actions CI | Ambos | 2h |
| #6 Deploy Railway + Vercel | Ambos | 3h |

---

### Sprint 2 — v0.2 Autenticação parte 1
**Meta:** "O cadastro de usuário funciona no backend com JWT"

| Issue | Responsável | Estimativa |
|---|---|---|
| #7 Migration users | Rafael | 1h |
| #8 Entidade e repository User | Rafael | 2h |
| #9 Endpoint de cadastro | Rafael | 3h |
| #10 Configurar JWT | Rafael | 4h |

---

### Sprint 3 — v0.2 Autenticação parte 2
**Meta:** "O usuário consegue se cadastrar, fazer login e acessar o dashboard"

| Issue | Responsável | Estimativa |
|---|---|---|
| #11 Endpoint de login | Rafael | 2h |
| #12 Endpoint de perfil | Rafael | 2h |
| #13 Tela de cadastro | Kauã | 4h |
| #14 Tela de login | Kauã | 3h |
| #15 Contexto de auth + rotas protegidas | Kauã | 4h |
| #16 JWT no Node.js | Kauã | 2h |

---

### Sprint 4 — v0.3 Biblioteca parte 1
**Meta:** "O backend de livros está completo com CRUD e testes"

| Issue | Responsável | Estimativa |
|---|---|---|
| #17 Migration books | Rafael | 1h |
| #18 CRUD de livros Spring Boot | Rafael | 6h |

---

### Sprint 5 — v0.3 Biblioteca parte 2
**Meta:** "O usuário consegue ver, buscar, adicionar e favoritar livros"

| Issue | Responsável | Estimativa |
|---|---|---|
| #19 Tela de biblioteca | Kauã | 5h |
| #20 Modal de adicionar livro | Kauã | 3h |

---

### Sprint 6 — v0.4 Sessões parte 1
**Meta:** "O backend de sessões funciona: criar, entrar, sair"

| Issue | Responsável | Estimativa |
|---|---|---|
| #21 Migrations sessões | Rafael | 1h |
| #22 Criar e entrar em sessão | Rafael | 6h |

---

### Sprint 7 — v0.4 Sessões parte 2
**Meta:** "Sessões completas no backend + primeiras telas no frontend"

| Issue | Responsável | Estimativa |
|---|---|---|
| #23 Encerrar sessão + participantes | Rafael | 4h |
| #24 Tela de criar sessão | Kauã | 4h |
| #25 Tela de entrar em sessão | Kauã | 2h |

---

### Sprint 8 — v0.4 Sessões parte 3
**Meta:** "O usuário vê a tela da sessão com participantes e progresso"

| Issue | Responsável | Estimativa |
|---|---|---|
| #26 Tela principal da sessão | Kauã | 6h |

---

### Sprint 9 — v0.5 Chat parte 1
**Meta:** "O servidor de chat em tempo real está funcionando"

| Issue | Responsável | Estimativa |
|---|---|---|
| #27 Servidor de chat Socket.IO | Kauã | 6h |

---

### Sprint 10 — v0.5 Chat parte 2
**Meta:** "O chat em tempo real funciona no frontend"

| Issue | Responsável | Estimativa |
|---|---|---|
| #28 Componente de chat | Kauã | 5h |
| #29 Notificações de presença | Kauã | 2h |

---

### Sprint 11 — v0.6 Pomodoro parte 1
**Meta:** "O backend de streak está pronto e o timer Pomodoro funciona no Node.js"

| Issue | Responsável | Estimativa |
|---|---|---|
| #30 Migrations Pomodoro/streak | Rafael | 1h |
| #31 Timer Pomodoro Node.js | Kauã | 5h |
| #32 Endpoint streak Spring Boot | Rafael | 4h |

---

### Sprint 12 — v0.6 Pomodoro parte 2
**Meta:** "O timer Pomodoro funciona no frontend"

| Issue | Responsável | Estimativa |
|---|---|---|
| #33 Componente timer React | Kauã | 5h |

---

### Sprint 13 — v0.6 Pomodoro parte 3
**Meta:** "O calendário de streak está completo"

| Issue | Responsável | Estimativa |
|---|---|---|
| #34 Calendário de streak | Kauã | 6h |

---

### Sprint 14 — v0.7 Progresso parte 1
**Meta:** "Histórico de progresso e rodízio funcionam no backend"

| Issue | Responsável | Estimativa |
|---|---|---|
| #35 Migrations progresso/rodízio | Rafael | 1h |
| #36 Histórico de progresso | Rafael | 3h |
| #37 Sistema de rodízio (back) | Rafael | 3h |
| #37 Sistema de rodízio (front) | Kauã | 2h |

---

### Sprint 15 — v0.7 Progresso parte 2
**Meta:** "O calendário de sessões está funcionando"

| Issue | Responsável | Estimativa |
|---|---|---|
| #38 Calendário de sessões | Kauã | 5h |

---

### Sprint 16 — v1.0 Polimento parte 1
**Meta:** "O projeto tem testes, tratamento de erros e está seguro"

| Issue | Responsável | Estimativa |
|---|---|---|
| #39 Testes Java | Rafael | 5h |
| #40 Testes Node.js | Kauã | 3h |
| #41 Tratamento global de erros | Rafael | 2h |
| #42 Rate limiting | Rafael | 2h |
| #43 CORS produção | Rafael | 1h |

---

### Sprint 17 — v1.0 Polimento parte 2
**Meta:** "MVP completo, documentado e testado end-to-end"

| Issue | Responsável | Estimativa |
|---|---|---|
| #44 Página 404 + loading states | Kauã | 3h |
| #45 Testes e2e manuais | Ambos | 3h |
| #46 Documentação final | Ambos | 2h |

---

## Marcos de aprendizado por mês

### Mês 1 — "Aprendo o básico"
- Kauã domina: Git, JS moderno, React básico, Vite, TailwindCSS, HTTP e JWT
- Rafael domina: Git, Java básico, Spring Boot inicial, JPA, bcrypt

### Mês 2 — "Construo funcionalidades reais"
- Kauã domina: React Query, formulários, Context API, integração com API
- Rafael domina: Spring Data, validações, segurança com Spring Security

### Mês 3 — "Enfrento complexidade"
- Kauã domina: WebSocket com Socket.IO, Node.js, Redis, real-time
- Rafael domina: lógica de negócio complexa, transações, queries avançadas

### Mês 4 — "Consolido e integro"
- Ambos dominam: integração entre sistemas, debugging de sistemas distribuídos

### Mês 5 — "Entrego com qualidade"
- Ambos dominam: testes, CI/CD, deploy, monitoramento básico

---

## Como lidar com desvios do cronograma

Se uma sprint atrasar:

1. **Não tente recuperar na próxima sprint** — acelerar causa bugs e aprendizado superficial
2. Mova as issues não concluídas para o Backlog com contexto ("pausada por X")
3. Na planning da próxima sprint, recalcule o cronograma a partir do ponto atual
4. O projeto não tem prazo externo — é aprendizado

Se uma sprint for muito rápida:
1. Puxe issues do início da próxima milestone
2. Use o tempo extra para aprofundar testes ou refatorar código existente
3. Nunca avance para funcionalidades futuras sem concluir a milestone atual
