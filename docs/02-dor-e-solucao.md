# Dor, solução e contexto do produto

---

## O problema

Clubes de leitura existem há décadas. Mas as ferramentas que as pessoas usam para organizá-los foram criadas para outros propósitos: grupos de WhatsApp para combinar datas, planilhas para marcar progresso, timers de celular para Pomodoro, e nada conversa com nada. O resultado é fragmentação — você precisa de quatro aplicativos abertos ao mesmo tempo para ter uma sessão de leitura organizada.

Além disso, manter a consistência de leitura é difícil sem feedback visual de progresso. Aplicativos como GitHub resolveram isso para programadores com o streak de contribuições. Leitores não têm o equivalente.

---

## A dor central

> "Eu e meus amigos queremos ler o mesmo livro juntos, acompanhar o progresso de cada um, ter um lugar para discutir enquanto lemos e não perder o ritmo — mas não existe uma ferramenta única que faça tudo isso."

Dores secundárias identificadas:

- Sem histórico visual de consistência (streak), a leitura vira uma obrigação sem recompensa
- Sem sessões com tempo definido (Pomodoro), as pessoas leem sem foco
- Sem chat no contexto do livro, a discussão se perde em grupos de mensagem genéricos
- Sem controle de progresso compartilhado, ninguém sabe onde o outro parou
- Sem um sistema de rodízio, sempre a mesma pessoa escolhe o livro

---

## A solução — LitCircle

Uma plataforma web de clube de leitura que une em um único lugar:

- Sessões de leitura com host, configuração de livro, data de início/fim e senha opcional
- Chat integrado dentro da sessão, contextualizado ao livro
- Pomodoro de leitura com marcação de streak no calendário (visual estilo GitHub)
- Progresso do livro por página ou porcentagem
- Sistema de rodízio mensal de escolha de livro
- Biblioteca pessoal com favoritos e histórico

---

## Personas

### Persona 1 — O leitor consistente

**Nome:** Lucas, 23 anos, estudante  
**Comportamento:** Lê todo dia, mas perde a consistência quando não tem estrutura  
**Dor:** Não tem feedback visual do hábito que está construindo  
**O que precisa:** Streak de leitura, Pomodoro integrado, calendário de sessões

### Persona 2 — O organizador do clube

**Nome:** Mariana, 27 anos, analista  
**Comportamento:** É quem organiza as reuniões do grupo, define o livro, controla o cronograma  
**Dor:** Usa WhatsApp + Google Agenda + planilha + timer separados  
**O que precisa:** Criar sessões, configurar livro e prazo, convidar participantes, definir senha

### Persona 3 — O participante passivo

**Nome:** Pedro, 25 anos, desenvolvedor  
**Comportamento:** Participa quando convidado, mas não lidera  
**Dor:** Não sabe onde a galera parou, perde discussões por não ter contexto  
**O que precisa:** Ver progresso dos participantes, entrar no chat da sessão, ver o calendário

---

## Escopo do MVP

O MVP entrega o ciclo completo de uma sessão de leitura:

1. Usuário se cadastra e faz login
2. Cria ou entra em uma sessão de leitura
3. Configura livro, datas e senha (opcional)
4. Usa Pomodoro para registrar tempo de leitura
5. Atualiza progresso no livro
6. Troca mensagens no chat da sessão
7. Vê o streak no calendário

Funcionalidades fora do MVP (versão futura):

- Notificações push
- App mobile nativo
- Integração com APIs de catálogo de livros (Open Library, Google Books)
- Gamificação avançada (badges, rankings)
- Recomendações de livros por IA

---

## Métricas de sucesso do MVP

| Métrica | Critério mínimo |
|---|---|
| Usuário consegue criar uma sessão | Menos de 3 cliques para configurar e iniciar |
| Chat funciona em tempo real | Mensagem entregue em menos de 500ms |
| Pomodoro registra streak | Streak atualizado no calendário ao fim de cada sessão |
| Progresso salvo | Estado persistido mesmo após fechar o navegador |
| Deploy estável | Uptime de 95%+ no free tier do Railway |
