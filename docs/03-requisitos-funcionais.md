# Requisitos funcionais — MVP v0

> Apenas o essencial para o primeiro release. 7 requisitos, não 20.

---

## RF-001 — Cadastro de usuário

**Responsável:** Rafael (backend) + Kauã (frontend)

O usuário pode criar uma conta com nome, e-mail e senha.

Critérios de aceite:
- [ ] E-mail único — retorna 409 se já cadastrado
- [ ] Senha mínimo 8 caracteres
- [ ] Senha armazenada com hash bcrypt
- [ ] Retorna JWT ao cadastrar com sucesso

---

## RF-002 — Login

**Responsável:** Rafael (backend) + Kauã (frontend)

O usuário pode autenticar-se com e-mail e senha.

Critérios de aceite:
- [ ] Retorna JWT com validade de 7 dias
- [ ] Retorna 401 com mensagem genérica em caso de falha
- [ ] Token armazenado no localStorage

---

## RF-003 — Logout

**Responsável:** Kauã (frontend)

O usuário pode encerrar sua sessão.

Critérios de aceite:
- [ ] Token removido do localStorage
- [ ] Redireciona para login
- [ ] Conexão WebSocket encerrada

---

## RF-004 — Criar sessão de leitura

**Responsável:** Rafael (backend) + Kauã (frontend)

Um host pode criar uma sessão com livro e datas.

Critérios de aceite:
- [ ] Campos: título do livro, autor, total de páginas, data início, data fim
- [ ] Host é automaticamente o primeiro participante
- [ ] Código de convite único gerado (ex: LIT-X7K2)

---

## RF-005 — Entrar em sessão

**Responsável:** Rafael (backend) + Kauã (frontend)

Um usuário pode entrar em uma sessão pelo código de convite.

Critérios de aceite:
- [ ] Campo para informar código
- [ ] Erro se código não existir
- [ ] Erro se sessão encerrada
- [ ] Erro se já é participante

---

## RF-006 — Registrar progresso

**Responsável:** Rafael (backend) + Kauã (frontend)

O usuário atualiza sua página atual no livro da sessão.

Critérios de aceite:
- [ ] Input numérico para página atual
- [ ] Porcentagem calculada automaticamente
- [ ] Progresso visível para todos os participantes

---

## RF-007 — Chat em tempo real

**Responsável:** Kauã (backend Node.js + frontend)

Participantes trocam mensagens em tempo real.

Critérios de aceite:
- [ ] Mensagem entregue em menos de 1 segundo
- [ ] Nome do remetente e timestamp em cada mensagem
- [ ] Enter envia, Shift+Enter quebra linha
- [ ] Máximo 500 caracteres
- [ ] Mensagem em branco não enviada

---

## Funcionalidades fora do MVP v0 (versão futura)

| Funcionalidade | Versão |
|---------------|--------|
| Biblioteca de livros (CRUD) | v0.5 |
| Perfil do usuário + foto | v0.6 |
| Pomodoro e streak | v1.0 |
| Rodízio de escolha | v1.0 |
| Calendário de sessões | v1.0 |
| Notificações push | v2.0 |
| App mobile | v3.0 |
