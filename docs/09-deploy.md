# Deploy — 100% gratuito no Render.com

---

## Visão geral

```
GitHub (código)
    │
    ├── push na main
    │
    ├──► Render Static Site ─── Frontend (HTML/CSS/JS)
    ├──► Render Web Service ─── Spring Boot ──► PostgreSQL (Render)
    └──► Render Web Service ─── Node.js
```

**Custo total: R$ 0,00**

---

## Passo 1 — Criar conta no Render

1. Acesse render.com
2. Entre com GitHub
3. Autorize acesso ao repositório LitCircle

---

## Passo 2 — PostgreSQL

1. Dashboard → New → PostgreSQL
2. Name: `litcircle-db`
3. Database: `litcircle`
4. User: `litcircle_user`
5. Region: Oregon (US West)
6. Plan: Free
7. Anote a **Internal Database URL** (usada pelo Spring Boot)

---

## Passo 3 — Backend Java (Spring Boot)

1. New → Web Service → conecta ao repo
2. Name: `litcircle-java`
3. Root Directory: `backend-java`
4. Runtime: Docker (ou Java, se detectar)
5. Build Command: `./mvnw clean install -DskipTests`
6. Start Command: `java -jar target/*.jar`
7. Plan: Free

**Variáveis de ambiente:**
```
DATABASE_URL=<Internal Database URL do passo 2>
JWT_SECRET=<gere com: node -e "console.log(require('crypto').randomBytes(64).toString('hex'))">
PORT=8080
SPRING_PROFILES_ACTIVE=prod
```

---

## Passo 4 — Backend Node.js

1. New → Web Service → conecta ao repo
2. Name: `litcircle-node`
3. Root Directory: `backend-node`
4. Runtime: Node
5. Build Command: `npm install`
6. Start Command: `node src/index.js`
7. Plan: Free

**Variáveis de ambiente:**
```
PORT=3001
JWT_SECRET=<MESMO valor do Spring Boot>
NODE_ENV=production
```

---

## Passo 5 — Frontend

1. New → Static Site → conecta ao repo
2. Name: `litcircle-app`
3. Root Directory: `frontend`
4. Build Command: (vazio)
5. Publish Directory: `.`

Crie `frontend/config.js`:
```javascript
const CONFIG = {
  API_URL: 'https://litcircle-java.onrender.com',
  REALTIME_URL: 'https://litcircle-node.onrender.com'
};
```

---

## Passo 6 — Verificar

- `https://litcircle-java.onrender.com/health` → `{ "status": "ok" }`
- `https://litcircle-node.onrender.com/health` → `{ "status": "ok" }`
- `https://litcircle-app.onrender.com` → página do LitCircle

---

## Limitações do free tier

| Limitação | Impacto |
|-----------|---------|
| Hiberna após 15min sem tráfego | Primeiro acesso demora ~30s |
| PostgreSQL 1GB, expira em 90 dias | Recria grátis, dados perdidos |
| 750h/mês de runtime | Suficiente para 2 serviços |

Para MVP de aprendizado e portfólio, é perfeito.
