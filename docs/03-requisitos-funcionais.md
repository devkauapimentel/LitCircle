# Requisitos funcionais

Cada requisito tem um identificador único (RF-XXX), uma descrição, o responsável pelo desenvolvimento e os critérios de aceite que definem quando a funcionalidade está pronta.

---

## Módulo 1 — Autenticação e usuário

### RF-001 — Cadastro de usuário

**Responsável:** Rafael (backend) + Kauã (frontend)  
**Descrição:** O usuário pode criar uma conta informando nome, e-mail e senha.

Critérios de aceite:
- [ ] E-mail deve ser único no sistema — retorna erro 409 se já cadastrado
- [ ] Senha deve ter no mínimo 8 caracteres
- [ ] Senha é armazenada com hash bcrypt, nunca em texto plano
- [ ] Ao cadastrar com sucesso, o usuário recebe um token JWT e é redirecionado para o dashboard
- [ ] Campos obrigatórios validados no frontend antes de enviar a requisição

### RF-002 — Login

**Responsável:** Rafael (backend) + Kauã (frontend)  
**Descrição:** O usuário pode autenticar-se com e-mail e senha.

Critérios de aceite:
- [ ] Retorna token JWT com validade de 7 dias em caso de sucesso
- [ ] Retorna erro 401 com mensagem genérica ("credenciais inválidas") em caso de falha — nunca indica qual campo está errado
- [ ] Token é armazenado no localStorage do navegador
- [ ] Rotas privadas redirecionam para login se não houver token válido

### RF-003 — Logout

**Responsável:** Kauã (frontend)  
**Descrição:** O usuário pode encerrar sua sessão.

Critérios de aceite:
- [ ] Token é removido do localStorage
- [ ] Usuário é redirecionado para a tela de login
- [ ] Conexão WebSocket é encerrada

### RF-004 — Perfil do usuário

**Responsável:** Rafael (backend) + Kauã (frontend)  
**Descrição:** O usuário pode visualizar e editar seu nome e foto de perfil.

Critérios de aceite:
- [ ] Pode alterar nome de exibição
- [ ] Pode fazer upload de foto de perfil (formato JPG/PNG, máx 2MB)
- [ ] Não pode alterar e-mail após cadastro (MVP)
- [ ] Alterações salvas com sucesso mostram feedback visual

---

## Módulo 2 — Biblioteca pessoal

### RF-005 — Cadastrar livro

**Responsável:** Rafael (backend) + Kauã (frontend)  
**Descrição:** O usuário pode adicionar livros à sua biblioteca informando título, autor, número de páginas e capa (opcional).

Critérios de aceite:
- [ ] Campos obrigatórios: título, autor, total de páginas
- [ ] Campo opcional: URL da capa
- [ ] Livro aparece na biblioteca do usuário após cadastro
- [ ] Mesmo livro pode ser cadastrado por múltiplos usuários sem conflito

### RF-006 — Favoritar livro

**Responsável:** Rafael (backend) + Kauã (frontend)  
**Descrição:** O usuário pode marcar e desmarcar livros como favoritos.

Critérios de aceite:
- [ ] Livros favoritados aparecem destacados na biblioteca
- [ ] Botão de favorito alterna entre ativo e inativo com feedback visual
- [ ] Estado de favorito é persistido no banco de dados

### RF-007 — Listar e buscar livros

**Responsável:** Rafael (backend) + Kauã (frontend)  
**Descrição:** O usuário pode visualizar todos os livros da sua biblioteca e buscar por título ou autor.

Critérios de aceite:
- [ ] Listagem paginada (20 livros por página)
- [ ] Busca por título ou autor em tempo real (debounce de 300ms)
- [ ] Filtro para exibir apenas favoritos
- [ ] Estado vazio com mensagem orientativa quando não há livros

---

## Módulo 3 — Sessões de leitura

### RF-008 — Criar sessão de leitura

**Responsável:** Rafael (backend) + Kauã (frontend)  
**Descrição:** Um usuário (host) pode criar uma sessão de leitura configurando livro, datas e opções.

Critérios de aceite:
- [ ] Campos obrigatórios: livro (selecionado da biblioteca), data de início, data de fim
- [ ] Campo opcional: senha de acesso (se preenchida, apenas quem tiver a senha pode entrar)
- [ ] Campo opcional: limite de participantes (padrão: sem limite)
- [ ] Ao criar, o host é automaticamente o primeiro participante
- [ ] A sessão recebe um código único de convite (ex: `LIT-X7K2`)

### RF-009 — Entrar em uma sessão

**Responsável:** Rafael (backend) + Kauã (frontend)  
**Descrição:** Um usuário pode entrar em uma sessão existente pelo código de convite.

Critérios de aceite:
- [ ] Campo para informar o código de convite na tela inicial
- [ ] Se a sessão tiver senha, solicita a senha antes de confirmar entrada
- [ ] Retorna erro se o código não existir
- [ ] Retorna erro se a sessão estiver lotada (quando houver limite)
- [ ] Retorna erro se a sessão já tiver encerrado

### RF-010 — Configurar sessão (host)

**Responsável:** Rafael (backend) + Kauã (frontend)  
**Descrição:** O host pode editar as configurações de uma sessão ativa.

Critérios de aceite:
- [ ] Pode alterar data de fim, senha e limite de participantes
- [ ] Não pode alterar o livro após a sessão ter pelo menos 2 participantes
- [ ] Apenas o host vê o botão de configuração
- [ ] Mudanças são refletidas imediatamente para todos os participantes via WebSocket

### RF-011 — Listar participantes da sessão

**Responsável:** Rafael (backend) + Kauã (frontend)  
**Descrição:** Todos os participantes podem ver quem está na sessão e o progresso de cada um.

Critérios de aceite:
- [ ] Lista exibe nome, foto e progresso de leitura de cada participante
- [ ] Host é indicado com um ícone diferenciado
- [ ] Lista atualiza em tempo real quando alguém entra ou sai

### RF-012 — Encerrar sessão (host)

**Responsável:** Rafael (backend) + Kauã (frontend)  
**Descrição:** O host pode encerrar uma sessão manualmente.

Critérios de aceite:
- [ ] Confirmação obrigatória antes de encerrar
- [ ] Ao encerrar, todos os participantes são notificados via WebSocket
- [ ] Sessão encerrada fica no histórico mas não aceita novas interações

---

## Módulo 4 — Progresso de leitura

### RF-013 — Registrar progresso

**Responsável:** Rafael (backend) + Kauã (frontend)  
**Descrição:** O usuário pode atualizar sua página atual no livro da sessão.

Critérios de aceite:
- [ ] Input numérico para página atual (entre 1 e total de páginas)
- [ ] Porcentagem calculada automaticamente e exibida
- [ ] Progresso salvo ao confirmar — não salva automaticamente ao digitar
- [ ] Progresso visível para todos os participantes da sessão

### RF-014 — Histórico de progresso

**Responsável:** Rafael (backend) + Kauã (frontend)  
**Descrição:** O usuário pode ver o histórico das suas atualizações de progresso.

Critérios de aceite:
- [ ] Lista cronológica das atualizações com data e página
- [ ] Visível apenas para o próprio usuário

---

## Módulo 5 — Chat da sessão

### RF-015 — Enviar mensagem no chat

**Responsável:** Kauã (backend Node.js + frontend)  
**Descrição:** Participantes de uma sessão podem trocar mensagens em tempo real.

Critérios de aceite:
- [ ] Mensagem entregue para todos os participantes em menos de 500ms
- [ ] Mensagens têm nome do remetente, texto e timestamp
- [ ] Enter envia a mensagem, Shift+Enter quebra linha
- [ ] Máximo de 500 caracteres por mensagem
- [ ] Mensagem em branco não é enviada

### RF-016 — Histórico do chat

**Responsável:** Kauã (backend Node.js) + Rafael (persistência)  
**Descrição:** Ao entrar na sessão, o usuário vê as últimas 50 mensagens do chat.

Critérios de aceite:
- [ ] Carrega as 50 mensagens mais recentes ao conectar
- [ ] Scroll automático para a mensagem mais recente ao abrir
- [ ] Mensagens antigas podem ser carregadas via "carregar mais"

---

## Módulo 6 — Pomodoro e streak

### RF-017 — Timer Pomodoro

**Responsável:** Kauã (backend Node.js + frontend)  
**Descrição:** O usuário pode iniciar um ciclo Pomodoro de leitura dentro de uma sessão.

Critérios de aceite:
- [ ] Ciclo padrão: 25 minutos de foco + 5 minutos de pausa
- [ ] Timer exibido em destaque durante a sessão
- [ ] Ao concluir um Pomodoro completo, o dia é marcado no calendário de streak
- [ ] Timer pode ser pausado e retomado
- [ ] Ao finalizar, toca um sinal sonoro (configurável para silenciar)
- [ ] Estado do timer sincronizado entre abas do mesmo usuário via Redis

### RF-018 — Calendário de streak

**Responsável:** Rafael (backend) + Kauã (frontend)  
**Descrição:** O usuário tem um calendário visual que marca os dias em que completou pelo menos um Pomodoro.

Critérios de aceite:
- [ ] Visual inspirado no contribution graph do GitHub (grid de semanas)
- [ ] Dias com Pomodoro completo ficam coloridos
- [ ] Intensidade da cor varia com o número de Pomodoros no dia (1, 2-3, 4+)
- [ ] Exibe o streak atual (dias consecutivos) e o recorde
- [ ] Navegação por mês

---

## Módulo 7 — Rodízio de escolha

### RF-019 — Sistema de rodízio mensal

**Responsável:** Rafael (backend) + Kauã (frontend)  
**Descrição:** A cada mês, um participante diferente da sessão tem o direito de escolher o livro.

Critérios de aceite:
- [ ] Ordem de rodízio definida automaticamente na criação da sessão (por ordem de entrada)
- [ ] Exibe claramente quem é o "escolhedor do mês"
- [ ] O escolhedor pode definir ou alterar o livro da sessão atual
- [ ] Histórico de quem escolheu em cada mês

---

## Módulo 8 — Calendário e agenda

### RF-020 — Calendário de sessões

**Responsável:** Rafael (backend) + Kauã (frontend)  
**Descrição:** O usuário tem um calendário que exibe todas as suas sessões ativas com datas de início e fim.

Critérios de aceite:
- [ ] Visualização mensal com eventos por dia
- [ ] Clique em um evento leva para a sessão correspondente
- [ ] Eventos coloridos por status (ativa, futura, encerrada)
- [ ] Calendário navegável por mês

---

## Resumo de módulos e responsabilidades

| Módulo | RF | Dono do domínio |
|---|---|---|
| Autenticação | RF-001 a RF-004 | Rafael (back) + Kauã (front) |
| Biblioteca | RF-005 a RF-007 | Rafael (back) + Kauã (front) |
| Sessões | RF-008 a RF-012 | 50/50 co-arquitetos |
| Progresso | RF-013 a RF-014 | Rafael (back) + Kauã (front) |
| Chat | RF-015 a RF-016 | **Kauã** (Node.js WebSocket) |
| Pomodoro e streak | RF-017 a RF-018 | **Kauã** (Node.js) |
| Rodízio | RF-019 | Rafael (back) + Kauã (front) |
| Calendário | RF-020 | Rafael (back) + Kauã (front) |
