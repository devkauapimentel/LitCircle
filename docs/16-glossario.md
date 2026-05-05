# Glossário técnico — LitCircle

> Definições diretas dos termos técnicos que aparecem na documentação do projeto. Consulte este arquivo sempre que encontrar um termo desconhecido.

---

## A

**API (Application Programming Interface)**
Um contrato que define como dois sistemas se comunicam. No LitCircle, o frontend "conversa" com o backend Spring Boot através de uma API REST. É como um cardápio de restaurante: define o que você pode pedir e o que vai receber.

**Async/Await**
Sintaxe do JavaScript para lidar com operações que levam tempo (como buscar dados de uma API) sem travar o programa. `async` marca uma função como assíncrona. `await` pausa a execução até a operação terminar.

**Autenticação**
Processo de verificar *quem* é o usuário ("você é quem diz ser?"). No LitCircle, feita com e-mail + senha que gera um JWT.

**Autorização**
Processo de verificar *o que* o usuário pode fazer ("você tem permissão para isso?"). Ex: apenas o host pode encerrar a sessão.

---

## B

**Backend**
A parte do sistema que roda no servidor — invisível para o usuário final. Processa a lógica de negócio, acessa o banco de dados e retorna dados para o frontend. No LitCircle temos dois: Spring Boot (Java) e Node.js.

**bcrypt**
Algoritmo de hash para senhas. Ele transforma "minha_senha123" em algo como `$2b$12$...` de forma irreversível. O banco nunca armazena senhas em texto puro.

**Body (corpo da requisição)**
Os dados enviados junto com uma requisição HTTP, geralmente em formato JSON. Ex: `{ "email": "user@email.com", "password": "senha123" }`.

**Branch**
Uma linha independente de desenvolvimento no Git. Você cria uma branch para trabalhar em uma feature sem afetar o código principal (`main`).

**Build**
Processo de transformar código-fonte em arquivos prontos para produção. No React, o `npm run build` gera arquivos HTML/CSS/JS otimizados.

---

## C

**Cache**
Armazenamento temporário de dados para acesso rápido. O Redis é o cache do LitCircle — armazena mensagens de chat e estado do Pomodoro em memória (muito mais rápido que o banco em disco).

**CI/CD (Continuous Integration / Continuous Deployment)**
CI: processo automático que roda testes a cada push. CD: processo automático que faz deploy após os testes passarem. No LitCircle, o GitHub Actions cuida de ambos.

**Cliente (Client)**
Quem faz requisições. No contexto web, o navegador é o cliente. O React roda no navegador (lado do cliente).

**CORS (Cross-Origin Resource Sharing)**
Mecanismo de segurança do navegador que bloqueia requisições para domínios diferentes do atual. O backend Spring Boot precisa ser configurado para aceitar requisições do domínio do frontend.

**Commit**
Um "salvo" no Git com mensagem descritiva. Registra as mudanças feitas no código.

**Container (Docker)**
Um ambiente isolado e padronizado que roda uma aplicação com todas as suas dependências. O Docker roda PostgreSQL e Redis em containers localmente.

**Controller (Spring Boot)**
Classe Java que recebe requisições HTTP, chama os serviços necessários e retorna a resposta. É a camada de entrada do backend Java.

**CRUD**
Create, Read, Update, Delete — as quatro operações básicas de dados. Equivalente a POST, GET, PUT/PATCH, DELETE em REST.

---

## D

**Debounce**
Técnica que atrasa a execução de uma função até que o usuário pare de digitar por X milissegundos. Usado na busca de livros para não disparar uma requisição a cada tecla pressionada.

**Dependency Injection (DI)**
Padrão de design onde os objetos recebem suas dependências prontas em vez de criá-las. O Spring Boot gerencia DI automaticamente com `@Autowired` e `@Component`.

**Deploy**
Publicar a aplicação em um servidor para que fique acessível na internet. No LitCircle: frontend vai para Vercel, backends vão para Railway.

**Docker Compose**
Ferramenta para definir e rodar múltiplos containers com um único arquivo (`docker-compose.yml`). Usada para subir PostgreSQL e Redis localmente.

---

## E

**Endpoint**
Uma URL específica de uma API que responde a um tipo de requisição. Ex: `POST /api/auth/login` é um endpoint.

**Entity (JPA)**
Classe Java anotada com `@Entity` que representa uma tabela do banco de dados. Cada instância da classe é uma linha da tabela.

**ESLint**
Ferramenta que analisa código JavaScript/TypeScript e aponta problemas de estilo e possíveis bugs sem precisar executar o código.

**Event Loop**
Mecanismo do Node.js que permite processar múltiplas operações simultâneas em uma única thread. É o motivo pelo qual Node.js é eficiente para WebSocket.

---

## F

**Flyway**
Ferramenta que gerencia as alterações no esquema do banco de dados através de arquivos SQL numerados (migrations). Garante que todos tenham o mesmo banco.

**Frontend**
A parte do sistema que roda no navegador — o que o usuário vê e interage. No LitCircle, construído com React.

**Free Tier**
Plano gratuito de um serviço de cloud. Railway e Vercel têm free tiers que são suficientes para o MVP do LitCircle.

---

## G

**Git**
Sistema de controle de versão. Rastreia todas as mudanças no código ao longo do tempo.

**GitHub**
Plataforma online que hospeda repositórios Git e adiciona features de colaboração (Pull Requests, Issues, Projects).

**GitHub Actions**
Sistema de CI/CD integrado ao GitHub. Roda workflows (scripts) automaticamente em resposta a eventos (push, PR, etc.).

**GitHub Projects**
Ferramenta de gestão de projetos integrada ao GitHub. Funciona como um kanban board com issues ilimitadas no plano gratuito.

---

## H

**Hash**
Resultado de uma função que transforma dados de qualquer tamanho em uma string de tamanho fixo. Irreversível — você não consegue recuperar o dado original a partir do hash. Usado para armazenar senhas com segurança.

**Header (cabeçalho HTTP)**
Metadados que acompanham uma requisição ou resposta HTTP. O token JWT é enviado no header `Authorization: Bearer <token>`.

**Hibernate**
Implementação do JPA que faz o mapeamento entre objetos Java e tabelas do banco de dados. O Spring Boot usa Hibernate por padrão.

**HTTP (HyperText Transfer Protocol)**
Protocolo de comunicação da web. Define como cliente e servidor trocam mensagens. Toda requisição a uma API REST usa HTTP.

---

## I

**Imagem (Docker)**
Um "molde" para criar containers. A imagem `postgres:15` define como criar um container com PostgreSQL 15.

**Index (banco de dados)**
Estrutura de dados que acelera consultas em colunas específicas. Sem índice, o banco percorre todas as linhas para encontrar o dado (lento). Com índice, vai direto (rápido).

**IoC (Inversion of Control)**
Princípio de design onde o framework controla o fluxo da aplicação em vez do código. O Spring Boot aplica IoC extensivamente.

---

## J

**JPA (Java Persistence API)**
Especificação Java para mapeamento objeto-relacional. Define como objetos Java se relacionam com tabelas de banco de dados.

**JSON (JavaScript Object Notation)**
Formato de texto para trocar dados. Leve, legível por humanos e fácil de processar. O LitCircle usa JSON em todas as comunicações entre frontend e backends.

```json
{
  "nome": "Kauã",
  "email": "kaua@email.com",
  "favoritos": ["livro1", "livro2"]
}
```

**JWT (JSON Web Token)**
Token compacto e seguro para autenticação. Composto por três partes separadas por ponto: `header.payload.signature`. O backend emite um JWT no login, e o cliente o envia em cada requisição para provar sua identidade.

---

## K

**Kanban**
Metodologia de gestão de trabalho visual com colunas que representam o estado das tarefas (A fazer → Fazendo → Concluído). O projeto usa Kanban com regra WIP = 1.

---

## L

**Latência**
Tempo entre enviar uma requisição e receber a resposta. Medida em milissegundos (ms). O objetivo do chat é latência < 500ms.

**LTS (Long Term Support)**
Versão de software com suporte e correções de segurança garantidos por vários anos. Node.js 20 LTS e Java 21 LTS são as versões usadas no projeto.

---

## M

**Main (branch)**
A branch principal e estável do repositório. Só recebe código aprovado via Pull Request. Nunca commite diretamente na `main`.

**Maven**
Ferramenta de build e gerenciamento de dependências para projetos Java. O `pom.xml` lista as bibliotecas do projeto.

**Middleware**
Função que fica entre a requisição e o handler final no Express. Usado para autenticação (verificar JWT), logging, CORS, etc.

**Migration (Flyway)**
Arquivo SQL versionado que representa uma alteração no esquema do banco. Ex: `V1__create_users.sql`. Nunca é alterado após executado.

**Milestone**
Marco do projeto que representa uma entrega funcional. Ex: "v0.2 — Autenticação" significa que o cadastro e login funcionam completamente.

**MVP (Minimum Viable Product)**
Versão mínima do produto que entrega valor ao usuário. O MVP do LitCircle inclui autenticação, biblioteca, sessões, chat e Pomodoro — sem recursos avançados como gamificação ou app mobile.

---

## N

**Node.js**
Runtime JavaScript no servidor. Permite rodar JavaScript fora do navegador. Usado no LitCircle para o backend de chat e Pomodoro em tempo real.

**npm (Node Package Manager)**
Gerenciador de pacotes do Node.js. `npm install` baixa dependências, `npm run dev` roda scripts.

---

## O

**ORM (Object-Relational Mapping)**
Técnica que converte dados entre tabelas do banco (relacional) e objetos da linguagem de programação. O Hibernate é o ORM do projeto.

---

## P

**Payload (JWT)**
A parte do token JWT que contém os dados do usuário (id, nome, e-mail, data de expiração). Não é criptografado — qualquer um pode ler. Mas não pode ser falsificado sem a chave secreta.

**PostgreSQL**
Banco de dados relacional open-source usado para armazenar os dados permanentes do LitCircle (usuários, livros, sessões, progresso).

**Prettier**
Formatador de código automático. Garante que o código tenha sempre o mesmo estilo (indentação, aspas, vírgulas) sem precisar pensar nisso.

**Pull Request (PR)**
Solicitação para integrar uma branch ao `main`. Permite revisão do código pelo parceiro antes do merge.

---

## R

**Railway**
Plataforma de cloud com free tier. Usada para hospedar Spring Boot, Node.js, PostgreSQL e Redis em produção.

**React**
Biblioteca JavaScript para construir interfaces de usuário com componentes reutilizáveis.

**React Query (TanStack Query)**
Biblioteca para gerenciar dados do servidor no React. Cuida de cache, loading states, revalidação e sincronização automática.

**Redis**
Banco de dados em memória ultra-rápido, usado para dados temporários: mensagens de chat, estado do Pomodoro, sessões ativas.

**Repository (Spring Data)**
Interface Java que o Spring implementa automaticamente para fazer operações no banco (findAll, findById, save, delete). Elimina o código repetitivo de SQL.

**REST (Representational State Transfer)**
Estilo arquitetural para APIs. Define convenções: recursos são substantivos nas URLs, verbos HTTP indicam a ação, respostas são em JSON.

**Rebase**
Operação do Git que reaplica seus commits sobre a versão mais recente de outra branch. Mantém o histórico linear. Preferível a `merge` para atualizar branches de feature.

---

## S

**Service (Spring Boot)**
Classe Java com a lógica de negócio. Chamada pelo Controller, chama o Repository. Ex: `SessionService.java` contém a lógica de entrar em uma sessão.

**Socket.IO**
Biblioteca para WebSocket com reconexão automática, rooms e eventos. Usada no backend Node.js e frontend React para o chat e Pomodoro em tempo real.

**Spring Boot**
Framework Java que simplifica a criação de aplicações web. Cuida de configuração, injeção de dependência, mapeamento de rotas e muito mais.

**Sprint**
Período fixo de desenvolvimento (1 semana no LitCircle) com uma meta clara. Ao fim de cada sprint, algo funcional é entregue.

**Squash and Merge**
Forma de merge que compacta todos os commits de uma branch em um único commit na `main`. Mantém o histórico limpo.

**Status Code HTTP**
Número que indica o resultado de uma requisição. Os principais:
- `200 OK` — sucesso com dados
- `201 Created` — criado com sucesso
- `204 No Content` — sucesso sem dados
- `400 Bad Request` — erro do cliente (dados inválidos)
- `401 Unauthorized` — não autenticado
- `403 Forbidden` — autenticado mas sem permissão
- `404 Not Found` — recurso não encontrado
- `409 Conflict` — conflito (ex: e-mail já existe)
- `500 Internal Server Error` — erro do servidor

**Streak**
Sequência de dias consecutivos com atividade. O LitCircle mostra um calendário visual de streaks de leitura, inspirado no contribution graph do GitHub.

---

## T

**TailwindCSS**
Framework CSS utilitário. Em vez de escrever classes CSS personalizadas, você compõe estilos com classes predefinidas diretamente no HTML/JSX.

**Token**
String única que representa a autenticação de um usuário. O JWT é o token de autenticação do LitCircle.

**TTL (Time to Live)**
Tempo de vida de um dado no cache. Após o TTL, o dado é automaticamente deletado pelo Redis.

---

## U

**UUID (Universally Unique Identifier)**
Identificador único gerado aleatoriamente, formato: `550e8400-e29b-41d4-a716-446655440000`. Usado como chave primária nas tabelas para evitar IDs sequenciais previsíveis.

---

## V

**Variável de ambiente**
Configuração externa ao código armazenada no sistema operacional ou em um arquivo `.env`. Usada para segredos (senhas, chaves de API) e configurações que mudam entre ambientes (dev/prod).

**Vercel**
Plataforma de hosting para frontends estáticos e aplicações React. Free tier generoso para projetos pessoais. Integrada ao GitHub para deploy automático.

**Vite**
Ferramenta de build moderna para frontend. Oferece um servidor de desenvolvimento extremamente rápido com hot reload instantâneo.

---

## W

**WebSocket**
Protocolo de comunicação bidirecional e persistente entre cliente e servidor. Diferente do HTTP (que é requisição-resposta), o WebSocket mantém a conexão aberta — perfeito para chat em tempo real.

**WIP (Work in Progress)**
Trabalho em andamento. A regra WIP = 1 significa que cada pessoa só pode ter uma tarefa em desenvolvimento ao mesmo tempo.

---

## X

**XSS (Cross-Site Scripting)**
Vulnerabilidade onde código malicioso é injetado numa página web. O React protege automaticamente contra XSS ao escapar variáveis no JSX. Não use `dangerouslySetInnerHTML`.

---

## Z

**ZIP**
Formato de arquivo compactado. A documentação completa do LitCircle está disponível como `litcircle-docs.zip` para importar direto no repositório.
