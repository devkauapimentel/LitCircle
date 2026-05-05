# Wireframes das telas — LitCircle

> Descrição visual de todas as telas do sistema. Use como referência para o Figma ou diretamente no desenvolvimento. Layouts em ASCII para comunicação rápida entre a dupla.

---

## Tela 1 — Login

```
┌─────────────────────────────────────────────┐
│                                             │
│              📚 LitCircle                   │
│                                             │
│  ┌─────────────────────────────────────┐   │
│  │  E-mail                             │   │
│  │  [___________________________________]  │
│  │                                     │   │
│  │  Senha                              │   │
│  │  [___________________________________]  │
│  │                                     │   │
│  │  [     Entrar →                    ]   │
│  │                                     │   │
│  │  Não tem conta? Cadastre-se         │   │
│  └─────────────────────────────────────┘   │
│                                             │
└─────────────────────────────────────────────┘
```

**Comportamentos:**
- Botão "Entrar" fica desabilitado durante a requisição (loading spinner)
- Erro exibido em vermelho abaixo do formulário
- Enter no campo senha submete o formulário

---

## Tela 2 — Cadastro

```
┌─────────────────────────────────────────────┐
│              📚 LitCircle                   │
│                                             │
│  ┌─────────────────────────────────────┐   │
│  │  Nome                               │   │
│  │  [___________________________________]  │
│  │                                     │   │
│  │  E-mail                             │   │
│  │  [___________________________________]  │
│  │                                     │   │
│  │  Senha (mín. 8 caracteres)          │   │
│  │  [___________________________________]  │
│  │                                     │   │
│  │  Confirmar senha                    │   │
│  │  [___________________________________]  │
│  │                                     │   │
│  │  [    Criar conta →               ]   │
│  │                                     │   │
│  │  Já tem conta? Entrar               │   │
│  └─────────────────────────────────────┘   │
└─────────────────────────────────────────────┘
```

---

## Tela 3 — Dashboard (página inicial após login)

```
┌──────────────────────────────────────────────────────────┐
│  📚 LitCircle          [🔔]  [Kauã ▼]                   │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  Bom dia, Kauã! 🌅                                       │
│  Você está numa sequência de 7 dias 🔥                   │
│                                                          │
│  ┌──────────────────┐  ┌──────────────────┐            │
│  │  Minhas sessões  │  │  + Nova sessão   │            │
│  │  ativas: 2       │  │  ou entrar com   │            │
│  │                  │  │  código          │            │
│  │  [Ver todas →]   │  │  [LIT-____]      │            │
│  └──────────────────┘  └──────────────────┘            │
│                                                          │
│  Sessões ativas                                          │
│  ┌───────────────────────────────────────────────────┐  │
│  │  📖 O Senhor dos Anéis                            │  │
│  │  4 participantes · Termina em 12 dias             │  │
│  │  Seu progresso: ████████░░ 78%    [Entrar →]     │  │
│  └───────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────┐  │
│  │  📖 O Hobbit                                      │  │
│  │  2 participantes · Termina em 5 dias              │  │
│  │  Seu progresso: ████░░░░░░ 42%    [Entrar →]     │  │
│  └───────────────────────────────────────────────────┘  │
│                                                          │
│  Streak de leitura                                       │
│  [mini calendário — últimas 4 semanas]                  │
│                                                          │
└──────────────────────────────────────────────────────────┘
```

**Navegação lateral (mobile: bottom nav):**
- Home (dashboard)
- Biblioteca
- Calendário
- Perfil

---

## Tela 4 — Biblioteca

```
┌──────────────────────────────────────────────────────────┐
│  ← Biblioteca                     [+ Adicionar livro]   │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  [🔍 Buscar por título ou autor...      ]               │
│  [Todos ▼]  [★ Favoritos]                              │
│                                                          │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐             │
│  │  [CAPA]  │  │  [CAPA]  │  │  [CAPA]  │             │
│  │          │  │          │  │          │             │
│  │ O Senhor │  │ O Hobbit │  │  Duna    │             │
│  │ dos Anéis│  │          │  │          │             │
│  │ Tolkien  │  │ Tolkien  │  │  Herbert │             │
│  │ ████ 78% │  │ ██░░ 42% │  │ ░░░░  0% │             │
│  │ [♡→★]   │  │ [★]      │  │ [♡]      │             │
│  └──────────┘  └──────────┘  └──────────┘             │
│                                                          │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐             │
│  │  [CAPA]  │  │  [CAPA]  │  │  +       │             │
│  │          │  │          │  │  Adicionar│             │
│  │ ...      │  │ ...      │  │  livro   │             │
│  └──────────┘  └──────────┘  └──────────┘             │
│                                                          │
└──────────────────────────────────────────────────────────┘
```

---

## Tela 5 — Modal: Adicionar livro

```
┌─────────────────────────────────────────────┐
│  Adicionar livro                        [✕] │
├─────────────────────────────────────────────┤
│                                             │
│  Título *                                   │
│  [___________________________________]      │
│                                             │
│  Autor *                                    │
│  [___________________________________]      │
│                                             │
│  Total de páginas *                         │
│  [_______]                                  │
│                                             │
│  URL da capa (opcional)                     │
│  [___________________________________]      │
│  [  preview da capa se URL válida  ]        │
│                                             │
│              [Cancelar]  [Adicionar →]      │
└─────────────────────────────────────────────┘
```

---

## Tela 6 — Criar sessão

```
┌──────────────────────────────────────────────────────────┐
│  ← Criar sessão de leitura                               │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  Livro *                                                 │
│  [🔍 Buscar na sua biblioteca...        ]               │
│  ┌─────────────────────────────────────────────────┐   │
│  │  📖 O Senhor dos Anéis - Tolkien          [✓]   │   │
│  │  📖 O Hobbit - Tolkien                          │   │
│  └─────────────────────────────────────────────────┘   │
│                                                          │
│  Data de início *        Data de fim *                   │
│  [01/02/2024]            [28/02/2024]                   │
│                                                          │
│  Senha de acesso (opcional)                              │
│  [_______________]  ← deixe vazio para sessão aberta    │
│                                                          │
│  Limite de participantes (opcional)                      │
│  [___]  ← deixe vazio para sem limite                   │
│                                                          │
│                      [Cancelar]  [Criar sessão →]       │
└──────────────────────────────────────────────────────────┘
```

---

## Tela 7 — Entrar em sessão

```
┌─────────────────────────────────────────────┐
│  ← Entrar em sessão                         │
├─────────────────────────────────────────────┤
│                                             │
│  Código de convite                          │
│  [LIT-____]                                 │
│                                             │
│  (campo de senha aparece se sessão          │
│   tiver senha configurada)                  │
│  Senha                                      │
│  [_______________]                          │
│                                             │
│              [Cancelar]  [Entrar →]         │
└─────────────────────────────────────────────┘
```

---

## Tela 8 — Sessão de leitura (tela principal)

```
┌──────────────────────────────────────────────────────────┐
│  📖 O Senhor dos Anéis          [⚙] [Compartilhar]      │
│  Encerra em 12 dias · Código: LIT-X7K2                   │
├───────────────────────────┬──────────────────────────────┤
│                           │                              │
│  PARTICIPANTES (4)        │  CHAT                        │
│  ─────────────────────    │  ─────────────────────────   │
│  👤 Kauã (você) HOST      │  [Kauã] Capítulo incrível!  │
│  ████████░░ 78% · p.918   │  12:30                       │
│                           │                              │
│  👤 Rafael                │  [Rafael] A batalha do       │
│  █████░░░░░ 52% · p.613   │  Helm's Deep foi épica      │
│                           │  12:31                       │
│  👤 Ana                   │                              │
│  ███░░░░░░░ 31% · p.365   │  [Ana] Concordo! 🔥          │
│                           │  12:32                       │
│  👤 Pedro                 │                              │
│  █░░░░░░░░░ 12% · p.141   │  ─────────────────────────   │
│                           │  [Digite uma mensagem...   ] │
│  ─────────────────────    │  [                    Enviar]│
│  Meu progresso            │                              │
│  Página atual: [___]      │                              │
│  de 1178 páginas          │                              │
│  [Salvar progresso]       │                              │
│                           │                              │
├───────────────────────────┴──────────────────────────────┤
│  POMODORO                                                │
│  ┌────────────────────────────────────────────────┐     │
│  │   ⏱  23:47          [▶ Iniciar]               │     │
│  │   ████████████████████░░░░░░  79% concluído   │     │
│  └────────────────────────────────────────────────┘     │
└──────────────────────────────────────────────────────────┘
```

**Comportamentos:**
- Em mobile: chat e participantes ficam em abas separadas
- Timer Pomodoro sempre visível (fixo na parte inferior)
- Host vê botão ⚙ para configurações e opção de encerrar sessão
- Progresso dos outros participantes atualiza em tempo real

---

## Tela 9 — Streak e calendário

```
┌──────────────────────────────────────────────────────────┐
│  ← Meu progresso                                         │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  Sequência atual: 🔥 7 dias                              │
│  Recorde: 🏆 15 dias    Total de Pomodoros: 142          │
│                                                          │
│  ─────────────────────────────────────────────────────  │
│  Calendário de leitura — Janeiro 2024                    │
│  [◄]                                              [►]   │
│                                                          │
│  Dom  Seg  Ter  Qua  Qui  Sex  Sáb                      │
│                  ░    ░    ░    ░    ░                   │
│   ░    █    █    █    ██   ██   ░                        │
│   ░    ██   ░    ██   ██   █    ░                        │
│   ░    ░    ██   ███  ░    █    ████                     │
│   ░    ░    ░    ░    ░    ░    ░                        │
│                                                          │
│  ░ = nenhum  ▓ = 1  █ = 2-3  ██ = 4+                   │
│                                                          │
│  ─────────────────────────────────────────────────────  │
│  Histórico de sessões                                    │
│  ┌─────────────────────────────────────────────────┐   │
│  │  📖 O Senhor dos Anéis · Ativa                  │   │
│  │  01/02/2024 – 28/02/2024 · 78% concluído        │   │
│  └─────────────────────────────────────────────────┘   │
└──────────────────────────────────────────────────────────┘
```

---

## Tela 10 — Calendário de sessões

```
┌──────────────────────────────────────────────────────────┐
│  Calendário                                              │
├──────────────────────────────────────────────────────────┤
│  [◄ Janeiro 2024                                    ►]  │
│                                                          │
│  Dom  Seg  Ter  Qua  Qui  Sex  Sáb                      │
│                 [1]  [2]  [3]  [4]  [5]                 │
│  [6]  [7]  [8]  [9] [10] [11] [12]                      │
│ [13] [14] [15] [16] [17] [18] [19]                      │
│ [20] [21] [22] [23] [24] [25] [26]                      │
│ [27] [28] [29] [30] [31]                                │
│                                                          │
│  Dias com eventos aparecem destacados em verde (ativa)  │
│  Azul = futura  Cinza = encerrada                        │
│                                                          │
│  Ao clicar num dia com sessão:                           │
│  ┌────────────────────────────┐                         │
│  │ 📖 O Senhor dos Anéis     │                         │
│  │ Termina em 5 dias          │                         │
│  │ [Ir para sessão →]         │                         │
│  └────────────────────────────┘                         │
└──────────────────────────────────────────────────────────┘
```

---

## Tela 11 — Perfil

```
┌──────────────────────────────────────────────────────────┐
│  ← Perfil                                                │
├──────────────────────────────────────────────────────────┤
│                                                          │
│              [  FOTO  ]                                  │
│            [Alterar foto]                               │
│                                                          │
│  Nome                                                    │
│  [Kauã_________________________________]                 │
│                                                          │
│  E-mail (não editável)                                   │
│  kaua@email.com                                          │
│                                                          │
│                          [Salvar alterações]             │
│                                                          │
│  ─────────────────────────────────────────              │
│  Estatísticas                                            │
│  Pomodoros totais: 142                                   │
│  Sessões participadas: 8                                 │
│  Livros lidos: 3                                         │
│                                                          │
│  ─────────────────────────────────────────              │
│                   [Sair da conta]                       │
└──────────────────────────────────────────────────────────┘
```

---

## Componentes reutilizáveis identificados

Para Kauã implementar como componentes React separados:

| Componente | Usado em |
|---|---|
| `Button` | Todas as telas |
| `Input` | Formulários |
| `Card` | Biblioteca, dashboard |
| `Modal` | Adicionar livro, confirmações |
| `ProgressBar` | Sessão, biblioteca |
| `Avatar` | Participantes, perfil, chat |
| `BookCover` | Biblioteca, sessão, dashboard |
| `PomodoroTimer` | Sessão |
| `StreakCalendar` | Streak, dashboard |
| `ChatMessage` | Chat da sessão |
| `LoadingSkeleton` | Qualquer lista |
| `EmptyState` | Listas vazias |
| `ErrorMessage` | Formulários |
| `PrivateRoute` | Roteamento |

---

## Paleta de cores sugerida

```
Principal (verde leitura):  #2D6A4F  (botões primários, streak ativo)
Secundário:                 #52B788  (hover states, destaques)
Fundo:                      #F8F9FA  (página)
Fundo card:                 #FFFFFF  (cards)
Texto primário:             #1A1A2E  (títulos)
Texto secundário:           #6B7280  (subtítulos, timestamps)
Erro:                       #DC2626  (mensagens de erro)
Sucesso:                    #16A34A  (feedback positivo)
Streak 1 Pomodoro:          #D1FAE5
Streak 2-3 Pomodoros:       #6EE7B7
Streak 4+ Pomodoros:        #059669
```

---

## Layout responsivo

**Desktop (>= 1024px):**
- Sessão de leitura: layout de duas colunas (participantes + chat)
- Biblioteca: grid de 3–4 colunas

**Tablet (768px – 1023px):**
- Sessão de leitura: layout de duas colunas compacto
- Biblioteca: grid de 2–3 colunas

**Mobile (< 768px):**
- Sessão de leitura: abas (Participantes | Chat) + Pomodoro fixo na base
- Biblioteca: grid de 2 colunas
- Navegação: bottom navigation bar com 4 ícones
