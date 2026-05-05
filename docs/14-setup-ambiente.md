# Setup do ambiente de desenvolvimento — passo a passo completo

> Este documento assume que você nunca configurou um ambiente de desenvolvimento antes. Siga cada passo na ordem. Não pule etapas.

---

## O que vamos instalar e por quê

| Ferramenta | Por quê precisamos |
|---|---|
| Git | Controle de versão — salva o histórico do código e permite colaborar |
| Node.js 20 | Roda o backend Node.js e as ferramentas de frontend (npm, Vite) |
| Java 21 | Roda o backend Spring Boot |
| Docker Desktop | Roda PostgreSQL e Redis localmente sem instalar na máquina |
| VSCode | Editor de código para Kauã (frontend + Node.js) |
| IntelliJ IDEA | IDE para Rafael (Java + Spring Boot) |

---

## Parte 1 — Git

### Windows

1. Acesse [git-scm.com/download/win](https://git-scm.com/download/win)
2. Baixe o instalador (64-bit)
3. Execute o instalador — nas opções, mantenha tudo padrão **exceto**:
   - "Choosing the default editor": selecione **VSCode** se já instalou, ou **Nano** se não sabe qual escolher
   - "Adjusting the name of the initial branch": selecione **"Override the default branch name"** e escreva `main`
   - "Configuring the line ending conversions": selecione **"Checkout as-is, commit Unix-style line endings"**

### macOS

```bash
# Instala o Homebrew primeiro (gerenciador de pacotes do macOS)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Instala o Git
brew install git
```

### Linux (Ubuntu/Debian)

```bash
sudo apt update
sudo apt install git -y
```

### Configuração inicial do Git (obrigatório em todos os sistemas)

Abra o terminal (Git Bash no Windows) e execute:

```bash
git config --global user.name "Seu Nome Aqui"
git config --global user.email "seu@email.com"
git config --global init.defaultBranch main
git config --global core.autocrlf input
git config --global pull.rebase true

# Verificar se funcionou
git config --list
```

### Conectar o Git ao GitHub via SSH

```bash
# Gerar chave SSH
ssh-keygen -t ed25519 -C "seu@email.com"
# Pressione Enter para aceitar o caminho padrão
# Pode deixar a senha em branco (pressione Enter duas vezes)

# Copiar a chave pública
# No macOS:
cat ~/.ssh/id_ed25519.pub | pbcopy
# No Windows (Git Bash):
cat ~/.ssh/id_ed25519.pub | clip
# No Linux:
cat ~/.ssh/id_ed25519.pub
# (selecione e copie manualmente)

# Agora vá em github.com → Settings → SSH and GPG keys → New SSH key
# Cole a chave copiada, dê um nome (ex: "meu notebook") e salve

# Testar a conexão
ssh -T git@github.com
# Deve aparecer: "Hi seunome! You've successfully authenticated..."
```

---

## Parte 2 — Node.js 20

### Por que Node.js 20 e não a versão mais nova?

Node.js 20 é LTS (Long Term Support) — versão com suporte garantido por anos. Versões sem LTS recebem menos suporte e podem ter bugs. Para projetos de aprendizado, sempre use LTS.

### Windows e macOS — usando nvm (recomendado)

O `nvm` (Node Version Manager) permite ter múltiplas versões do Node.js e trocar entre elas. É a forma profissional de instalar Node.

**macOS/Linux:**
```bash
# Instalar nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# Fechar e reabrir o terminal, depois:
nvm install 20
nvm use 20
nvm alias default 20

# Verificar
node --version   # deve mostrar v20.x.x
npm --version    # deve mostrar 10.x.x
```

**Windows:**
1. Acesse [github.com/coreybutler/nvm-windows/releases](https://github.com/coreybutler/nvm-windows/releases)
2. Baixe e instale `nvm-setup.exe`
3. Abra o PowerShell como administrador:

```powershell
nvm install 20
nvm use 20

# Verificar
node --version
npm --version
```

### Configurar npm para não precisar de sudo (Linux/macOS)

```bash
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

---

## Parte 3 — Java 21

### Por que Java 21?

Java 21 é a versão LTS mais recente. Spring Boot 3 exige Java 17 no mínimo, mas 21 é o recomendado.

### Usando SDKMAN (macOS/Linux) — recomendado

O SDKMAN gerencia versões de Java da mesma forma que o nvm gerencia Node.js.

```bash
# Instalar SDKMAN
curl -s "https://get.sdkman.io" | bash

# Fechar e reabrir o terminal, depois:
sdk install java 21.0.3-tem

# Verificar
java --version    # deve mostrar openjdk 21.x.x
javac --version   # deve mostrar javac 21.x.x
```

### Windows

1. Acesse [adoptium.net/temurin/releases](https://adoptium.net/temurin/releases)
2. Selecione: Version 21, OS Windows, Architecture x64, Package JDK
3. Baixe e execute o instalador `.msi`
4. **Importante:** marque a opção "Set JAVA_HOME variable" durante a instalação

```powershell
# Verificar no PowerShell
java --version
javac --version
```

---

## Parte 4 — Docker Desktop

O Docker vai rodar PostgreSQL e Redis localmente sem você precisar instalar esses programas diretamente na máquina. Isso evita conflitos de configuração e garante que o ambiente de todos seja idêntico.

### Windows

1. Certifique-se de que o WSL2 está habilitado:
```powershell
# Execute como administrador
wsl --install
# Reinicie o computador se solicitado
```

2. Acesse [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
3. Baixe e instale o Docker Desktop para Windows
4. Durante a instalação, selecione "Use WSL 2 instead of Hyper-V"
5. Reinicie o computador

### macOS

```bash
brew install --cask docker
# Depois abra o Docker Desktop pelo Launchpad
```

### Linux (Ubuntu)

```bash
# Instalar Docker Engine
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# Adicionar seu usuário ao grupo docker (para rodar sem sudo)
sudo usermod -aG docker $USER
newgrp docker

# Instalar Docker Compose
sudo apt install docker-compose-plugin -y

# Verificar
docker --version
docker compose version
```

### Verificar se o Docker funciona

```bash
docker run hello-world
# Deve aparecer "Hello from Docker!"
```

---

## Parte 5 — VSCode (Kauã)

### Instalação

1. Acesse [code.visualstudio.com](https://code.visualstudio.com)
2. Baixe a versão para seu sistema operacional
3. Instale normalmente

### Extensões obrigatórias

Abra o VSCode e pressione `Ctrl+P` (ou `Cmd+P` no Mac). Para cada extensão abaixo, cole o comando e pressione Enter:

```
ext install dbaeumer.vscode-eslint
ext install esbenp.prettier-vscode
ext install bradlc.vscode-tailwindcss
ext install dsznajder.es7-react-js-snippets
ext install eamodio.gitlens
ext install rangav.vscode-thunder-client
ext install pkief.material-icon-theme
ext install christian-kohler.path-intellisense
```

### Configuração do VSCode

Crie o arquivo `.vscode/settings.json` na raiz do projeto com este conteúdo:

```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.tabSize": 2,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  },
  "files.eol": "\n",
  "files.trimTrailingWhitespace": true,
  "[java]": {
    "editor.defaultFormatter": null
  }
}
```

---

## Parte 6 — IntelliJ IDEA Community Edition (Rafael)

### Instalação

1. Acesse [jetbrains.com/idea/download](https://www.jetbrains.com/idea/download)
2. Selecione **Community Edition** (gratuita)
3. Baixe e instale

### Plugins obrigatórios

Após instalar, abra o IntelliJ e vá em `File → Settings → Plugins → Marketplace`:

- Busque e instale: **Lombok**
- Busque e instale: **Spring Boot Assistant** (se não estiver incluso)
- Busque e instale: **Rainbow Brackets**

### Configurar o Java 21 no IntelliJ

1. `File → Project Structure → Project`
2. Em "SDK", clique em "Edit" e adicione o caminho do Java 21 instalado
3. Em "Language level", selecione "21"

---

## Parte 7 — Clonar o repositório e rodar o projeto

### Criar o repositório no GitHub

1. Acesse github.com e faça login
2. Clique em "New repository"
3. Nome: `litcircle`
4. Descrição: "Clube de leitura colaborativo — learning by doing"
5. Visibilidade: Public (para usar GitHub Actions gratuito sem limite)
6. Marque: "Add a README file"
7. Clique em "Create repository"

### Adicionar o segundo colaborador

1. Vá em `Settings → Collaborators → Add people`
2. Adicione o e-mail ou username do parceiro

### Clonar localmente

```bash
# Clone o repositório (substitua com o seu username)
git clone git@github.com:SEU_USERNAME/litcircle.git
cd litcircle
```

### Criar a estrutura de pastas do projeto

```bash
mkdir frontend backend-java backend-node .github
mkdir .github/workflows
touch docker-compose.yml
touch .gitignore
```

### Conteúdo do `.gitignore` raiz

```gitignore
# Node.js
node_modules/
npm-debug.log*
.npm

# Java / Maven
target/
*.class
*.jar
*.war

# IDEs
.idea/
*.iml
.vscode/
!.vscode/settings.json
!.vscode/extensions.json

# Ambiente
.env
.env.local
.env.*.local

# Build
dist/
build/

# Sistema operacional
.DS_Store
Thumbs.db
```

### docker-compose.yml para desenvolvimento local

Crie o arquivo `docker-compose.yml` na raiz:

```yaml
version: '3.8'

services:
  postgres:
    image: postgres:15-alpine
    container_name: litcircle-postgres
    environment:
      POSTGRES_DB: litcircle
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres"]
      interval: 10s
      timeout: 5s
      retries: 5

  redis:
    image: redis:7-alpine
    container_name: litcircle-redis
    ports:
      - "6379:6379"
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 10s
      timeout: 5s
      retries: 5

volumes:
  postgres_data:
```

### Subir o banco local

```bash
# Na raiz do projeto
docker compose up -d

# Verificar se está rodando
docker compose ps
# Deve mostrar litcircle-postgres e litcircle-redis como "healthy"

# Ver logs se algo der errado
docker compose logs postgres
docker compose logs redis

# Parar os serviços
docker compose down

# Parar e apagar os dados (cuidado!)
docker compose down -v
```

---

## Parte 8 — Inicializar o frontend (Kauã)

```bash
cd frontend

# Criar projeto React com Vite
npm create vite@latest . -- --template react

# Instalar dependências
npm install

# Instalar TailwindCSS
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p

# Instalar bibliotecas do projeto
npm install axios
npm install react-router-dom
npm install @tanstack/react-query
npm install socket.io-client

# Testar
npm run dev
# Acesse http://localhost:5173
```

Configure o `tailwind.config.js`:

```javascript
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

Adicione ao `src/index.css`:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Crie `frontend/.env`:

```env
VITE_API_URL=http://localhost:8080
VITE_REALTIME_URL=http://localhost:3001
```

---

## Parte 9 — Inicializar o backend Node.js (Kauã)

```bash
cd backend-node

npm init -y

# Instalar dependências
npm install express
npm install socket.io
npm install ioredis
npm install jsonwebtoken
npm install dotenv
npm install cors

# Instalar dependências de desenvolvimento
npm install -D nodemon
npm install -D jest

# Atualizar package.json com os scripts
```

`package.json`:

```json
{
  "name": "litcircle-backend-node",
  "version": "1.0.0",
  "scripts": {
    "start": "node src/index.js",
    "dev": "nodemon src/index.js",
    "test": "jest"
  },
  "dependencies": {
    "cors": "^2.8.5",
    "dotenv": "^16.3.1",
    "express": "^4.18.2",
    "ioredis": "^5.3.2",
    "jsonwebtoken": "^9.0.2",
    "socket.io": "^4.7.2"
  },
  "devDependencies": {
    "jest": "^29.7.0",
    "nodemon": "^3.0.2"
  }
}
```

Crie `backend-node/.env`:

```env
PORT=3001
REDIS_URL=redis://localhost:6379
JWT_SECRET=troque_por_uma_chave_aleatoria_longa
SPRING_BOOT_URL=http://localhost:8080
NODE_ENV=development
```

---

## Parte 10 — Inicializar o backend Java (Rafael)

1. Acesse [start.spring.io](https://start.spring.io)
2. Configure:
   - Project: **Maven**
   - Language: **Java**
   - Spring Boot: **3.2.x** (versão estável mais recente)
   - Group: `com.litcircle`
   - Artifact: `api`
   - Java: **21**
3. Adicione as dependências clicando em "+ ADD DEPENDENCIES":
   - Spring Web
   - Spring Data JPA
   - Spring Security
   - PostgreSQL Driver
   - Flyway Migration
   - Validation
   - Lombok
4. Clique em "GENERATE"
5. Extraia o `.zip` dentro da pasta `backend-java/`

Crie `backend-java/src/main/resources/application.properties`:

```properties
# Banco de dados
spring.datasource.url=jdbc:postgresql://localhost:5432/litcircle
spring.datasource.username=postgres
spring.datasource.password=postgres
spring.datasource.driver-class-name=org.postgresql.Driver

# JPA
spring.jpa.hibernate.ddl-auto=validate
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true

# Flyway
spring.flyway.enabled=true
spring.flyway.locations=classpath:db/migration

# Servidor
server.port=8080

# JWT (sobrescrever com variável de ambiente em produção)
app.jwt.secret=${JWT_SECRET:chave_padrao_desenvolvimento_troque_em_producao}
app.jwt.expiration-days=7
```

Teste o startup:

```bash
cd backend-java
./mvnw spring-boot:run
# Deve iniciar na porta 8080 sem erros
```

---

## Verificação final do ambiente

Execute este checklist depois de configurar tudo:

```bash
# Verificar versões
git --version          # deve ser 2.40+
node --version         # deve ser v20.x.x
npm --version          # deve ser 10.x.x
java --version         # deve ser 21.x.x
docker --version       # deve ser 24+
docker compose version # deve ser 2.x.x

# Verificar banco local rodando
docker compose up -d
docker compose ps      # ambos os serviços como "healthy"

# Verificar frontend
cd frontend && npm run dev
# Deve abrir em http://localhost:5173

# Verificar backend Node
cd backend-node && npm run dev
# Deve mostrar: "Servidor rodando na porta 3001"

# Verificar backend Java
cd backend-java && ./mvnw spring-boot:run
# Deve mostrar: "Started ApiApplication in X.XXX seconds"
```

Se tudo funcionou, o ambiente está pronto. Pode abrir a primeira issue.
