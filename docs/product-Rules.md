# Manifesto da Biblioteca: Cultura de Engenharia

> "A prática vem antes da teoria. A gente constrói para entender o conceito, não o contrário. O produto final é consequência."

---

## I. A Filosofia
**(O Espírito do Projeto)**

* **Learning by Doing:** A prática antecede a teoria. O aprendizado real acontece na construção.
* **Autodidatismo ("Se Virar"):** A habilidade de investigar e caçar a solução importa mais do que saber a resposta de cor. O desconforto faz parte do crescimento.
* **Fundamentos e Esforço:** Valorizamos o trabalho duro, a resiliência e a compreensão profunda de como a engrenagem funciona por baixo dos panos.
* **Ajuda Mútua:** Um levanta o outro. A evolução é conjunta. A ajuda vem em forma de direção e facilitação, não de resposta pronta.

---

## II. O Fluxo de Batalha
**(Operação e Trabalho em Equipe)**

* **Kanban Minimalista (WIP = 1):** Fluxo contínuo, visual e sem burocracia. É estritamente proibido ter mais de uma tarefa na coluna "Fazendo" por pessoa. *Começou, termina. Só depois puxa a próxima.*
* **Mantenha Simples:** Faça o básico bem feito. Não adicione camadas ou bibliotecas a menos que o projeto literalmente implore por elas. Feito é melhor que perfeito; a refatoração vem depois.
* **Liderança por Domínio e Polivalência:** Aplicamos a "Regra do Martelo" para evitar paralisia por análise:
  * **Front-end:** A liderança visual e arquitetural é do Kauã. O Rafael sugere, mas o Kauã bate o martelo.
  * **Back-end e Infra (Java):** A liderança do servidor e banco de dados é do Rafael. O Kauã sugere, mas o Rafael bate o martelo.
  * **Polivalência (Full-Stack):** O trânsito é livre. O Kauã puxará ativamente tarefas de APIs em Node.js ou ajudará no Back-end geral. Quem puxa a tarefa, coda. O "Dono do Domínio" atua como revisor rigoroso.
  * **A Terra Comum (50/50):** Nas integrações (formato JSON, rotas, regras de negócio), não há dono. Ambos são Co-Arquitetos. A decisão exige consenso técnico unânime.
* **Comunicação e Revisão:** Trabalho flexível (síncrono ou assíncrono). Revisões ocorrem em horários pontuais. *Ninguém envia código direto para a linha principal (`main`).* O trabalho sempre passa por aprovação mútua.

---

## III. O Pacto Anti-Sabotagem
**(Regras de Estudo e IA)**

* **Fontes Primárias Sempre:** A primeira linha de defesa ao travar em um problema é a documentação oficial, livros da área ou cursos.
* **Esforço Criativo (Zero IA para Planejamento):** É estritamente proibido usar IA para ter ideias, *brainstorm*, arquitetura ou planejamento de *issues*. O músculo criativo precisa ser treinado. As ideias nascem de nós mesmos.
* **IA Estritamente como Tutor:** A IA é o nosso "Sênior de bolso" apenas para tirar dúvidas de sintaxe ou debugar. **É terminantemente proibido** pedir para a IA gerar código final para copiar e colar. Você precisa saber explicar cada linha que digita.

---

## IV. Protocolo de Emergência
**(Anti-Trava)**

* **A Regra dos 45 Minutos:** Travou em um erro bizarro? Tente resolver sozinho nas documentações por 45 minutos. Não conseguiu? Pare imediatamente, documente o problema e chame o parceiro.
* **Sem Achismos, Apenas Logs:** Quando a integração falhar, olham-se os dados. O Front enviou o JSON certo? O Back respondeu com qual código de erro? Os *logs* guiam a solução.
