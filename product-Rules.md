The project culture and rules completely
1. O Propósito (Norte)

    Prática Acima da Teoria: O objetivo número um é o aprendizado prático ("Learning by Doing"). O produto final é consequência.

    Sob Demanda: Ferramentas novas (seja no front ou no back) só serão adicionadas quando o projeto literalmente pedir por elas. Sem otimização ou complexidade prematura.

    Feito é Melhor que Perfeito: O código inicial pode (e vai) ser feio. O foco é fazer funcionar. A refatoração (limpeza) acontece depois que a funcionalidade roda na tela.

2. Regras de Batalha (Operação)

    Limite de Foco (WIP = 1): Extremamente proibido ter mais de uma tarefa na coluna "Fazendo" por pessoa. Começou, termina. Só depois puxa a próxima.

    Ponte Front/Back: O contrato entre as partes é o JSON. A responsabilidade de quem faz o Front é garantir que o dado saia no formato certo; a responsabilidade do Back é garantir que a porta (API) esteja aberta para receber.

    Revisão Cruzada: Ninguém envia código direto para a linha principal (main). Um sempre revisa e aprova o código do outro antes de juntar as partes.

3. Lei de Uso da IA (Nosso Mentor)

    Tutor, não Gerador: A IA é usada como um Desenvolvedor Sênior para tirar dúvidas ("Por que essa div não centraliza?", "O que significa este erro no console?").

    Proibição do Ctrl+C / Ctrl+V Cego: É expressamente proibido colar um bloco de código no projeto sem saber explicar linha por linha o que ele faz.

4. Protocolo de Emergência (Anti-Trava)

    A Regra dos 45 Minutos: Travou em um erro bizarro? Tente resolver sozinho pesquisando nas documentações primárias por 45 minutos. Não conseguiu? Pare imediatamente, coloque no Kanban e chame o parceiro para olharem juntos.

    Sem Culpa, Apenas Logs: Quando a integração falhar, não há "achismos". Olha-se o console da rede: o Front enviou o pedido? O Back respondeu com qual código de erro? Os dados guiam a solução.
