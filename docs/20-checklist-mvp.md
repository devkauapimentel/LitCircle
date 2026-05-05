# Checklist do MVP e regras de qualidade

> Use este documento para validar se o LitCircle está pronto para ser considerado MVP completo. Cada item deve ser verificado antes de declarar v1.0.

---

## Checklist funcional — o sistema faz o que prometeu?

### Autenticação
- [ ] Usuário consegue se cadastrar com nome, e-mail e senha
- [ ] Usuário consegue fazer login e receber um JWT
- [ ] Rotas privadas redirecionam para login sem token
- [ ] Logout limpa o token e redireciona para login
- [ ] Usuário consegue editar nome e foto de perfil

### Biblioteca
- [ ] Usuário consegue adicionar livros com título, autor e páginas
- [ ] Usuário consegue listar seus livros com paginação
- [ ] Busca por título ou autor funciona em tempo real
- [ ] Favoritar e desfavoritar funciona e persiste
- [ ] Filtro de favoritos funciona

### Sessões
- [ ] Usuário consegue criar uma sessão com livro, datas, senha e limite
- [ ] Código de convite único é gerado automaticamente
- [ ] Usuário consegue entrar em sessão pelo código
- [ ] Sessão com senha exige a senha correta para entrar
- [ ] Sessão lotada não aceita novos participantes
- [ ] Sessão encerrada não aceita entradas
- [ ] Host consegue encerrar a sessão
- [ ] Host consegue alterar configurações da sessão
- [ ] Lista de participantes com progresso visível para todos

### Progresso de leitura
- [ ] Usuário consegue atualizar sua página atual
- [ ] Porcentagem é calculada corretamente
- [ ] Progresso persiste após fechar o navegador
- [ ] Progresso dos outros participantes visível em tempo real

### Chat
- [ ] Mensagens enviadas aparecem para todos os participantes em menos de 1 segundo
- [ ] Histórico das últimas 50 mensagens carregado ao entrar
- [ ] Mensagem em branco não é enviada
- [ ] Reconexão automática após queda de internet

### Pomodoro
- [ ] Timer de 25 minutos inicia e faz a contagem regressiva
- [ ] Timer pode ser pausado e retomado
- [ ] Sinal sonoro ao completar
- [ ] Ao completar um Pomodoro, o dia é marcado no calendário de streak

### Streak e calendário
- [ ] Calendário visual mostra dias com atividade
- [ ] Intensidade varia com o número de Pomodoros
- [ ] Streak atual e recorde exibidos corretamente
- [ ] Navegação por mês funciona

### Rodízio
- [ ] Sistema exibe quem escolhe o livro no mês atual
- [ ] Apenas o escolhedor do mês pode alterar o livro da sessão

### Calendário de sessões
- [ ] Sessões ativas aparecem no calendário mensal
- [ ] Clique em evento leva para a sessão

---

## Checklist técnico — o sistema é feito da forma certa?

### Segurança
- [ ] Nenhuma senha em texto puro no banco de dados
- [ ] Nenhum segredo (JWT_SECRET, DATABASE_URL) no repositório
- [ ] JWT validado em todas as rotas privadas (Spring Boot e Node.js)
- [ ] CORS configurado para aceitar apenas o domínio do frontend em produção
- [ ] Rate limiting nas rotas de autenticação
- [ ] Inputs do usuário validados no backend (não apenas no frontend)

### Qualidade de código
- [ ] Nenhum `console.log` de debug no código mergeado
- [ ] Nenhum código comentado desnecessário
- [ ] Nomes de variáveis e funções descritivos
- [ ] Nenhum arquivo com mais de 300 linhas
- [ ] Nenhuma repetição óbvia de código (DRY)

### Testes
- [ ] Testes unitários para `AuthService` (Spring Boot)
- [ ] Testes unitários para `SessionService` (Spring Boot)
- [ ] Testes unitários para `StreakService` (Spring Boot)
- [ ] Testes para middleware JWT (Node.js)
- [ ] Testes para handlers de chat (Node.js)
- [ ] Todos os testes passam no GitHub Actions

### Deploy e infraestrutura
- [ ] Frontend funcionando na Vercel
- [ ] Spring Boot funcionando no Railway
- [ ] Node.js funcionando no Railway
- [ ] PostgreSQL funcionando no Railway
- [ ] Redis funcionando no Railway
- [ ] `GET /health` responde em ambos os backends em produção
- [ ] GitHub Actions roda e passa em todos os PRs
- [ ] Deploy automático funciona após merge na `main`

### Performance
- [ ] Respostas da API em menos de 500ms para operações simples
- [ ] Índices criados nas colunas de busca frequente
- [ ] React Query usado para cache — não faz requisições repetidas desnecessárias

### Usabilidade
- [ ] Todas as ações têm feedback visual (loading, sucesso, erro)
- [ ] Mensagens de erro em português e orientativas
- [ ] Estados vazios com instrução clara
- [ ] Interface funciona em mobile (testado no Chrome DevTools)
- [ ] Interface funciona em Chrome e Firefox

---

## Checklist de colaboração — vocês trabalharam direito?

- [ ] 100% do código passou por Pull Request — nenhum commit direto na `main`
- [ ] 100% dos PRs foram revisados pelo parceiro antes do merge
- [ ] Todas as issues foram resolvidas com critérios de aceite verificados
- [ ] Documentação atualizada ao longo do desenvolvimento
- [ ] Daily check-ins aconteceram com regularidade
- [ ] Retrospectivas registradas

---

## Checklist de aprendizado — vocês de fato aprenderam?

Ao final do projeto, ambos devem conseguir responder:

**Kauã:**
- [ ] Explica como o React renderiza componentes e o que é o Virtual DOM
- [ ] Explica o que é useState, useEffect e quando usar cada um
- [ ] Explica como o React Query gerencia cache e quando revalida dados
- [ ] Explica o que é WebSocket e por que difere do HTTP
- [ ] Explica como o Socket.IO gerencia rooms e emite eventos
- [ ] Explica o que é o event loop do Node.js
- [ ] Explica o que é JWT e como funciona a validação
- [ ] Explica o que é CORS e por que existe

**Rafael:**
- [ ] Explica o que é Injeção de Dependência e como o Spring aplica
- [ ] Explica a diferença entre Controller, Service e Repository
- [ ] Explica como o JPA/Hibernate mapeia Java para SQL
- [ ] Explica o que são transactions e quando usar `@Transactional`
- [ ] Explica como o Spring Security protege rotas
- [ ] Explica o que é bcrypt e por que não salvar senhas em texto
- [ ] Explica o que são migrations do Flyway e por que são imutáveis
- [ ] Explica como JWT é validado sem consultar o banco

**Ambos:**
- [ ] Explicam como os dois backends se comunicam (JWT compartilhado)
- [ ] Explicam o fluxo completo de uma requisição do browser até o banco
- [ ] Explicam o que é REST e o que o torna diferente de outras abordagens
- [ ] Explicam o que é CI/CD e como o GitHub Actions funciona
- [ ] Explicam o que é um container Docker e para que serve
- [ ] Conseguem fazer um code review construtivo do código do parceiro

---

## Como declarar o MVP como concluído

O MVP está concluído quando:

1. Todos os itens do checklist funcional estão marcados
2. Todos os itens do checklist técnico de segurança estão marcados
3. O fluxo completo foi testado manualmente (Issue #45) por ambos
4. O deploy de produção está estável há pelo menos 48 horas
5. A documentação está atualizada

Quando isso acontecer: **parabéns**. Vocês construíram do zero uma aplicação full-stack com dois backends, banco relacional, cache, WebSocket em tempo real, autenticação com JWT, CI/CD e deploy em cloud. Isso é portfólio de nível de mercado.
