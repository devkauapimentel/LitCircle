# Manifesto LitCircle — Cultura de engenharia

> "A prática vem antes da teoria. A gente constrói para entender o conceito, não o contrário. O produto final é consequência."

---

## I. A filosofia

### Learning by doing

A prática antecede a teoria. O aprendizado real acontece na construção. Nenhum tutorial substitui o erro que você debugou sozinho às 23h. Quando travar, tente. Quando tentar e falhar, documente. Quando documentar e entender, você aprendeu de verdade.

### Autodidatismo — o "se virar"

A habilidade de investigar e caçar a solução importa mais do que saber a resposta de cor. O desconforto faz parte do crescimento. Travar é normal. Ficar horas parado sem buscar ajuda no lugar certo, não é. O músculo de ler documentação, entender stack traces e formular uma hipótese é o que separa um engenheiro de alguém que apenas executa receitas.

### Fundamentos e esforço

Valorizamos o trabalho duro, a resiliência e a compreensão profunda de como a engrenagem funciona por baixo dos panos. Não copie código que você não consegue explicar linha por linha. Se você não sabe o que aquela função faz, você não entendeu — e isso vai virar dívida técnica amanhã.

### Ajuda mútua

Um levanta o outro. A evolução é conjunta. A ajuda vem em forma de direção e facilitação, nunca de resposta pronta. Apontar o caminho é ajudar. Resolver pelo outro é prejudicar. Se o seu parceiro tiver travado, faça perguntas. Não dê a solução.

---

## II. O fluxo de batalha

### Kanban minimalista — WIP = 1

Fluxo contínuo, visual e sem burocracia. É **estritamente proibido** ter mais de uma tarefa na coluna "Fazendo" por pessoa. Começou, termina. Só depois puxa a próxima.

Colunas do board no GitHub Projects:

```
Backlog → A fazer → Fazendo (máx 1 por pessoa) → Em revisão → Concluído
```

A razão é simples: contexto switching é o inimigo do aprendizado profundo. Quando você trabalha em duas coisas ao mesmo tempo, não entende nenhuma das duas direito.

### Mantenha simples — YAGNI

Faça o básico bem feito. Não adicione camadas, abstrações ou bibliotecas a menos que o projeto literalmente implore por elas. Feito é melhor que perfeito. A refatoração vem depois, quando você entende o problema de verdade. A regra de ouro: "você vai precisar disso agora?" Se a resposta for não, não adicione.

### Regra do martelo — liderança por domínio

Para evitar paralisia por análise, cada domínio tem um dono. O dono bate o martelo nas decisões do seu domínio. O parceiro sugere, questiona, mas respeita a decisão final.

| Domínio | Líder (bate o martelo) | Papel do outro |
|---|---|---|
| Frontend — HTML/CSS/JS, UI, UX, telas | **Kauã** | Rafael sugere |
| Backend Java — Spring Boot, PostgreSQL, JPA | **Rafael** | Kauã sugere |
| Backend Node.js — chat, WebSocket, Socket.IO | **Kauã** | Rafael revisa |
| Integrações — rotas, JSON, regras de negócio | **Ambos (50/50)** | Consenso obrigatório |

Na terra comum (integrações), não há dono. Ambos são co-arquitetos. A decisão exige consenso técnico unânime. Se não houver consenso, a discussão vai para um documento de ADR (Architecture Decision Record) e cada um apresenta seus argumentos por escrito antes de decidir.

### Comunicação e revisão

- Trabalho flexível — síncrono ou assíncrono conforme a disponibilidade
- Revisões ocorrem em horários combinados previamente
- **Ninguém envia código direto para a branch `main`**
- Todo trabalho passa por Pull Request com aprovação mútua
- O dono do domínio é o revisor primário do PR que toca no seu território

---

## III. O pacto anti-sabotagem

### Fontes primárias sempre

A primeira linha de defesa ao travar em um problema é:

1. Documentação oficial da tecnologia
2. Livros da área
3. Cursos de referência
4. Stack Overflow (leitura crítica, não cópia cega)
5. Parceiro (após 45 minutos)

### Zero IA para planejamento e criação

É **estritamente proibido** usar IA para:

- Ter ideias ou fazer brainstorming de funcionalidades
- Planejar arquitetura ou modelar o banco de dados
- Criar issues ou escrever histórias de usuário
- Tomar decisões de stack ou tecnologia

O músculo criativo precisa ser treinado. As ideias nascem de vocês. Se você deixar a IA pensar por você, você não aprende nada que importa.

### IA estritamente como tutor

A IA é o "Sênior de bolso" — use apenas para:

- Tirar dúvidas de sintaxe
- Debugar um erro específico com contexto claro
- Entender o que um trecho de código faz linha por linha
- Pedir explicação de um conceito que você não entendeu na documentação

**É terminantemente proibido** pedir para a IA gerar código final para copiar e colar. Você precisa saber explicar cada linha que digita. Se não souber, não coloca.

---

## IV. Protocolo de emergência — anti-trava

### A regra dos 45 minutos

Travou em um erro? Siga este protocolo:

1. Leia o stack trace completo — o erro já está dizendo onde está o problema
2. Busque na documentação oficial por 45 minutos
3. Formule uma hipótese e teste
4. Se após 45 minutos ainda não resolveu: **pare imediatamente**, documente o problema (o que você tentou, qual é o erro exato, qual é o comportamento esperado) e chame o parceiro

Chamar o parceiro antes do tempo não é fraqueza, é desperdício de aprendizado. Chamar depois do tempo não é teimosia, é orgulho que atrasa o projeto.

### Sem achismos — apenas logs

Quando a integração falhar, olham-se os dados. Nunca assuma o que está errado sem evidência.

- O Frontend enviou o JSON no formato correto?
- O Backend respondeu com qual código de status?
- O Redis está armazenando o dado esperado?
- O log do Spring Boot mostra qual exceção?

Os logs guiam a solução. Achismo é ruído.

---

## V. Definição de "pronto"

Uma tarefa só pode ir para a coluna "Concluído" quando:

- [ ] O código funciona conforme o critério de aceite da issue
- [ ] O código passou por revisão do parceiro
- [ ] Nenhum `console.log` de debug foi deixado no código
- [ ] A branch foi mergeada via Pull Request aprovado
- [ ] A documentação foi atualizada se necessário (rotas novas, modelos novos)
