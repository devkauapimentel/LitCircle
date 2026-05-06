# Cronograma — 8 semanas até MVP v0

---

## Premissas

- **Ritmo:** 8–10 horas por semana por pessoa
- **Sprint:** 1 semana (segunda a domingo)
- Se o ritmo for menor (4-5h/semana), multiplique por 1.5x

---

## Roadmap

```
SEMANA 1  │ v0.1 — Esqueleto
          │ Setup, estrutura, boilerplate, health checks, PostgreSQL
          │ Issues #4 a #8

SEMANA 2  │ v0.2 — Autenticação (parte 1)
          │ Migration users, endpoints register/login, JWT
          │ Issues #9 a #12

SEMANA 3  │ v0.2 — Autenticação (parte 2)
          │ Telas login/cadastro, middleware JWT no Node.js
          │ Issues #13 a #15

SEMANA 4  │ v0.3 — Sessões (parte 1)
          │ Migrations, criar/entrar sessão (backend)
          │ Issues #16 a #18

SEMANA 5  │ v0.3 — Sessões (parte 2)
          │ Listar sessões, progresso, telas frontend
          │ Issues #19 a #23

SEMANA 6  │ v0.4 — Chat (parte 1)
          │ Migration messages, servidor Socket.IO
          │ Issues #24 a #25

SEMANA 7  │ v0.4 — Chat (parte 2)
          │ Chat no frontend, presença
          │ Issue #26

SEMANA 8  │ v0.5 — Deploy + Polish
          │ Deploy Render, teste e2e, loading states
          │ Issues #27 a #29

🎉 MVP v0 ENTREGUE
```

---

## O que cada um faz por semana

| Semana | Kauã | Rafael |
|--------|------|--------|
| 1 | Boilerplate frontend + Node.js | Boilerplate Spring Boot + PostgreSQL |
| 2 | Estudar fetch API + HTTP | Migrations + endpoints auth + JWT |
| 3 | Telas login/cadastro + JWT Node | Endpoint login + perfil |
| 4 | Estudar WebSocket básico | Migrations + CRUD sessões |
| 5 | Telas dashboard + sessão + progresso | Listar sessões + progresso |
| 6 | Servidor Socket.IO chat | Migration messages |
| 7 | Chat no frontend | Revisão + testes manuais |
| 8 | Deploy + polish | Deploy + testes e2e |

---

## Após o MVP v0

| Versão | O que adiciona | Quando |
|--------|---------------|--------|
| v0.5 | Biblioteca de livros (CRUD) | Mês 3 |
| v0.6 | Perfil do usuário + foto | Mês 3 |
| v1.0 | Pomodoro + Streak + Calendário | Mês 4-5 |
| v2.0 | React no frontend + TailwindCSS | Mês 5-6 |
| v3.0 | Docker + Redis + CI/CD completo | Mês 6-7 |
