# LitCircle (Sistema de Biblioteca)

> Um sistema de gerenciamento de biblioteca construído do zero para consolidar fundamentos de engenharia de software, arquitetura Full-Stack e integração de APIs.

---

## 💻 Sobre o Projeto

O LitCircle é o resultado prático de uma imersão focada na metodologia *Learning by Doing*. O sistema opera de forma totalmente desacoplada, separando as responsabilidades de interface (Front-end) e servidor (Back-end), simulando a arquitetura e a cultura de uma equipe real de desenvolvimento de software.

---

## 🛠️ Ecossistema de Desenvolvimento

Para manter o foco na execução e no aprendizado real, utilizamos um conjunto enxuto de ferramentas que priorizam a clareza visual e a produtividade.

### Planejamento e Design
* **Excalidraw:** Brainstorming, fluxogramas de lógica e desenhos iniciais de arquitetura.
* **Figma:** Prototipagem de baixa fidelidade para definir a interface antes do código.
* **dbdiagram.io:** Modelagem visual do Banco de Dados e seus relacionamentos.

### Execução e Stack Técnica
* **Front-end:** HTML5, CSS3, JavaScript Vanilla e TailwindCSS.
* **Back-end Base:** Java (Spring Boot).
* **Back-end Auxiliar (Full-Stack):** Node.js para construção de APIs complementares.
* **Testes de Integração:** Insomnia ou Postman (validação de rotas e retornos JSON).

### Gestão e Organização
* **GitHub Projects:** Quadro Kanban minimalista para controle de fluxo (Regra WIP = 1).
* **Notion:** Wiki pessoal para documentar aprendizados de fontes primárias e resoluções de bugs.

---

## ⚙️ Arquitetura e Fluxo de Dados

O projeto utiliza uma arquitetura baseada em serviços RESTful. A comunicação segue um contrato estrito:

1. **Client-side (Front-end):** Captura as interações do usuário e gerencia o estado da interface.
2. **A Ponte:** Dispara requisições HTTP (`fetch`) enviando e recebendo dados exclusivamente no formato `JSON`.
3. **Server-side (Back-end):** O servidor (Java ou Node) recebe a requisição, valida as regras de negócio e interage com o banco de dados.
4. **Resposta:** Retorna o status HTTP adequado (Sucesso, Erro de Cliente, Erro de Servidor) e o pacote de dados para o Front-end renderizar.

---

## 📝 Regras de Negócio Iniciais (MVP)

* [ ] O sistema não deve permitir o cadastro de livros duplicados (validação por ISBN ou combinação de Título e Autor).
* [ ] Todo livro deve ter uma máquina de estados (ex: "Na Fila", "Lendo", "Finalizado", "Abandonado").
* [ ] Avaliações (notas ou resenhas textuais) só podem ser feitas em livros com o status "Finalizado".
* [ ] (Em Breve) Separação de dados por usuário.

---

## 🚀 Como Executar Localmente

*(As instruções de instalação e os comandos de terminal para iniciar os servidores de desenvolvimento serão documentados aqui assim que a infraestrutura inicial for concluída).*

---

## 📜 Manifesto e Cultura de Engenharia

Este projeto obedece a um rigoroso código de cultura técnica, focado no autodidatismo, leitura de documentações primárias e esforço intelectual (com restrições estritas ao uso de IA generativa para código e ideação).

Para entender nosso fluxo Kanban, regras de Code Review e o modelo de Liderança por Domínio da dupla (Kauã & Rafael), leia na íntegra o nosso **[Manifesto de Engenharia](product-Rules.md)**.
