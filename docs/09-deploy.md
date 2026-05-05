# Deploy — 100% gratuito

Guia completo para colocar o LitCircle em produção sem gastar nada. Plataformas usadas: Vercel (frontend), Railway (backends + banco), GitHub Actions (CI/CD).

---

## Visão geral

```
GitHub (código fonte)
       │
       ├── GitHub Actions (CI/CD)
       │         │
       │    Roda testes
       │         │
       │    ┌────┴────┐
       │    │         │
       ▼    ▼         ▼
    Vercel         Railway
  (Frontend)    (Spring Boot +
                 Node.js +
                 PostgreSQL +
                 Redis)
```

**Custo total:** R$ 0,00

- Vercel: free para projetos pessoais, ilimitado
- Railway: US$ 5/mês de crédito gratuito — suficiente para os 4 serviços com uso leve
- GitHub Actions: 2000 minutos/mês gratuitos para repositórios públicos

---

## Estrutura do repositório

```
litcircle/
├── frontend/           → deploy na Vercel
├── backend-java/       → deploy na Railway
├── backend-node/       → deploy na Railway
├── docker-compose.yml  → apenas para desenvolvimento local
└── .github/
    └── workflows/
        ├── ci-java.yml
        ├── ci-node.yml
        └── ci-frontend.yml
```

---

## Parte 1 — Deploy do Frontend na Vercel

### Passo 1: Criar conta na Vercel

Acesse [vercel.com](https://vercel.com) e entre com sua conta do GitHub. Autorize o acesso ao repositório.

### Passo 2: Importar o projeto

1. Clique em "Add New Project"
2. Selecione o repositório `litcircle`
3. Configure o Root Directory como `frontend`
4. Framework preset: Vite (detectado automaticamente)
5. Build command: `npm run build`
6. Output directory: `dist`

### Passo 3: Configurar variáveis de ambiente na Vercel

No painel do projeto, vá em Settings > Environment Variables:

```
VITE_API_URL=https://litcircle-java.up.railway.app
VITE_REALTIME_URL=https://litcircle-node.up.railway.app
```

Atenção: as URLs do Railway ficam disponíveis após o deploy dos backends.

### Passo 4: Deploy automático

A partir deste ponto, qualquer push para `main` que altere arquivos dentro de `frontend/` dispara um deploy automático na Vercel.

---

## Parte 2 — Deploy dos backends na Railway

### Passo 1: Criar conta na Railway

Acesse [railway.app](https://railway.app) e entre com sua conta do GitHub.

### Passo 2: Criar o projeto

1. Clique em "New Project"
2. Selecione "Empty Project"
3. Nomeie o projeto como `litcircle`

### Passo 3: Adicionar PostgreSQL

1. No projeto, clique em "+ New"
2. Selecione "Database" > "Add PostgreSQL"
3. O Railway cria e configura automaticamente
4. Anote a variável `DATABASE_URL` gerada — será usada pelo Spring Boot

### Passo 4: Adicionar Redis

1. Clique em "+ New"
2. Selecione "Database" > "Add Redis"
3. Anote a variável `REDIS_URL` gerada — será usada pelo Node.js

### Passo 5: Deploy do Spring Boot

1. Clique em "+ New" > "GitHub Repo"
2. Selecione o repositório `litcircle`
3. Em "Root Directory", coloque `backend-java`
4. O Railway detecta o `pom.xml` e usa o buildpack de Java automaticamente

Configure as variáveis de ambiente do serviço:

```
DATABASE_URL=<valor copiado do PostgreSQL acima>
DATABASE_USERNAME=postgres
DATABASE_PASSWORD=<senha gerada pelo Railway>
JWT_SECRET=<gere com: node -e "console.log(require('crypto').randomBytes(64).toString('hex'))">
PORT=8080
SPRING_PROFILES_ACTIVE=prod
```

No arquivo `backend-java/src/main/resources/application-prod.properties`:

```properties
spring.datasource.url=${DATABASE_URL}
spring.datasource.username=${DATABASE_USERNAME}
spring.datasource.password=${DATABASE_PASSWORD}
spring.jpa.hibernate.ddl-auto=validate
spring.flyway.enabled=true
```

### Passo 6: Deploy do Node.js

1. Clique em "+ New" > "GitHub Repo"
2. Selecione o repositório `litcircle`
3. Em "Root Directory", coloque `backend-node`
4. O Railway detecta o `package.json` automaticamente

Configure as variáveis de ambiente:

```
PORT=3001
REDIS_URL=<valor copiado do Redis acima>
JWT_SECRET=<MESMO valor usado no Spring Boot>
SPRING_BOOT_URL=https://litcircle-java.up.railway.app
NODE_ENV=production
```

Certifique-se de que o `package.json` tem o script de start:

```json
{
  "scripts": {
    "start": "node src/index.js",
    "dev": "nodemon src/index.js"
  }
}
```

### Passo 7: Liberar domínios públicos

Para cada serviço no Railway (Java e Node):
1. Vá em Settings > Networking
2. Clique em "Generate Domain"
3. Anote as URLs geradas (ex: `litcircle-java.up.railway.app`)

Volte na Vercel e atualize as variáveis de ambiente com as URLs corretas.

---

## Parte 3 — CI/CD com GitHub Actions

### Workflow do Spring Boot

Arquivo: `.github/workflows/ci-java.yml`

```yaml
name: CI — Spring Boot

on:
  push:
    paths:
      - 'backend-java/**'
  pull_request:
    paths:
      - 'backend-java/**'

jobs:
  test:
    runs-on: ubuntu-latest

    services:
      postgres:
        image: postgres:15
        env:
          POSTGRES_DB: litcircle_test
          POSTGRES_USER: postgres
          POSTGRES_PASSWORD: postgres
        ports:
          - 5432:5432

    steps:
      - uses: actions/checkout@v4

      - name: Set up Java 21
        uses: actions/setup-java@v4
        with:
          java-version: '21'
          distribution: 'temurin'
          cache: maven

      - name: Run tests
        working-directory: backend-java
        run: ./mvnw test
        env:
          DATABASE_URL: jdbc:postgresql://localhost:5432/litcircle_test
          DATABASE_USERNAME: postgres
          DATABASE_PASSWORD: postgres
          JWT_SECRET: test_secret_key_for_ci_only
```

### Workflow do Node.js

Arquivo: `.github/workflows/ci-node.yml`

```yaml
name: CI — Node.js

on:
  push:
    paths:
      - 'backend-node/**'
  pull_request:
    paths:
      - 'backend-node/**'

jobs:
  test:
    runs-on: ubuntu-latest

    services:
      redis:
        image: redis:7
        ports:
          - 6379:6379

    steps:
      - uses: actions/checkout@v4

      - name: Set up Node.js 20
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: npm
          cache-dependency-path: backend-node/package-lock.json

      - name: Install dependencies
        working-directory: backend-node
        run: npm ci

      - name: Run tests
        working-directory: backend-node
        run: npm test
        env:
          REDIS_URL: redis://localhost:6379
          JWT_SECRET: test_secret_key_for_ci_only
          PORT: 3001
```

### Workflow do Frontend

Arquivo: `.github/workflows/ci-frontend.yml`

```yaml
name: CI — Frontend

on:
  push:
    paths:
      - 'frontend/**'
  pull_request:
    paths:
      - 'frontend/**'

jobs:
  test-and-build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Set up Node.js 20
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: npm
          cache-dependency-path: frontend/package-lock.json

      - name: Install dependencies
        working-directory: frontend
        run: npm ci

      - name: Run tests
        working-directory: frontend
        run: npm test

      - name: Build
        working-directory: frontend
        run: npm run build
        env:
          VITE_API_URL: https://placeholder.railway.app
          VITE_REALTIME_URL: https://placeholder.railway.app
```

O deploy na Vercel e no Railway é automático após os testes passarem — as plataformas detectam o push no GitHub e iniciam o deploy por conta própria.

---

## Docker Compose para desenvolvimento local

Arquivo `docker-compose.yml` na raiz do projeto:

```yaml
version: '3.8'

services:
  postgres:
    image: postgres:15
    environment:
      POSTGRES_DB: litcircle
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"

volumes:
  postgres_data:
```

Para subir localmente:

```bash
docker compose up -d
# Banco disponível em localhost:5432
# Redis disponível em localhost:6379
```

---

## Variáveis de ambiente — resumo

### `.env.example` do Spring Boot

```env
DATABASE_URL=jdbc:postgresql://localhost:5432/litcircle
DATABASE_USERNAME=postgres
DATABASE_PASSWORD=postgres
JWT_SECRET=troque_por_chave_aleatoria_de_64_bytes
PORT=8080
SPRING_PROFILES_ACTIVE=dev
```

### `.env.example` do Node.js

```env
PORT=3001
REDIS_URL=redis://localhost:6379
JWT_SECRET=mesma_chave_do_spring_boot
SPRING_BOOT_URL=http://localhost:8080
NODE_ENV=development
```

### `.env.example` do Frontend

```env
VITE_API_URL=http://localhost:8080
VITE_REALTIME_URL=http://localhost:3001
```

---

## Checklist de deploy

Antes de fazer o primeiro deploy em produção, verificar:

- [ ] `JWT_SECRET` é idêntico no Railway para o serviço Java e para o serviço Node
- [ ] `.env` está no `.gitignore` de todos os serviços
- [ ] Nenhum segredo está hardcoded no código
- [ ] `application-prod.properties` usa variáveis de ambiente, não valores diretos
- [ ] Endpoint `GET /health` funciona nos dois backends
- [ ] CORS no Spring Boot está configurado para aceitar apenas o domínio da Vercel em produção
- [ ] Flyway migrations rodam sem erro no PostgreSQL do Railway
- [ ] Testes passam no GitHub Actions antes do merge
