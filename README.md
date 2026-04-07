# 📚 Biblioteca LitCircle 0.0.1

Este projeto é uma aplicação Full-Stack desenvolvida para consolidar conhecimentos práticos de Front-end, Back-end e integração via APIs REST.

## 🛠️ Tecnologias Utilizadas (A Stack)

**Front-end:**
* HTML5 & JavaScript Vanilla
* TailwindCSS (Estilização)
* *React (A ser introduzido sob demanda para componentização futura)*

**Back-end & Infraestrutura:**
* Java (Spring Boot)
* Banco de Dados: [Definir qual usar, ex: PostgreSQL]

## ⚙️ Como Funciona a Arquitetura

O sistema opera de forma desacoplada. O Front-end é responsável apenas pela interface e experiência do usuário, comunicando-se com o Back-end exclusivamente através de requisições HTTP (arquivos JSON).

**Fluxo Básico de Dados:**
1. O usuário interage com a interface (Front-end).
2. O Front-end dispara uma requisição `fetch` contendo um JSON para os *Endpoints* da API.
3. O Back-end (Java) recebe, processa as Regras de Negócio e salva/consulta no Banco de Dados.
4. O Back-end devolve a resposta (Sucesso ou Erro) para o Front-end renderizar na tela.

## 🚀 Como Rodar o Projeto na Sua Máquina

*(Adicionaremos os comandos aqui assim que o código base for criado. Ex: como iniciar o servidor local de Front e Back).*

## 📝 Regras de Negócio Principais (WIP)

* [ ] Um livro não pode ser cadastrado em duplicidade.
* [ ] (Adicionar novas regras aqui conforme o projeto crescer)

---
*Para entender nossas regras de trabalho em equipe, limites de tarefas e uso de IA, leia nosso [Manifesto de Cultura](link-para-o-contributing).*
