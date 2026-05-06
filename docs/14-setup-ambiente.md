# Setup do ambiente — sem Docker

---

## O que instalar

| Ferramenta | Por quê |
|-----------|---------|
| Git | Controle de versão |
| Node.js 20 | Backend Node.js e ferramentas |
| Java 21 | Backend Spring Boot |
| PostgreSQL 15 | Banco de dados |
| VSCode | Editor do Kauã |
| IntelliJ IDEA Community | IDE do Rafael |

---

## 1. Git (ambos)

### Linux
```bash
sudo apt update && sudo apt install git -y
```

### Configuração
```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"
git config --global init.defaultBranch main
git config --global pull.rebase true

# Gerar chave SSH
ssh-keygen -t ed25519 -C "seu@email.com"
cat ~/.ssh/id_ed25519.pub
# Copie e cole em: github.com → Settings → SSH and GPG keys → New SSH key

# Testar
ssh -T git@github.com
```

---

## 2. Node.js 20 (Kauã)

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
# Fechar e reabrir terminal
nvm install 20
nvm alias default 20

node --version   # v20.x.x
npm --version    # 10.x.x
```

---

## 3. Java 21 (Rafael)

### Linux/Mac (SDKMAN)
```bash
curl -s "https://get.sdkman.io" | bash
# Fechar e reabrir terminal
sdk install java 21.0.3-tem

java --version    # 21.x
javac --version   # 21.x
```

### Windows
Baixe em adoptium.net/temurin/releases (JDK 21, Windows, x64). Marque "Set JAVA_HOME" na instalação.

---

## 4. PostgreSQL 15 (ambos)

### Linux
```bash
sudo apt install postgresql postgresql-contrib -y
sudo systemctl start postgresql
sudo systemctl enable postgresql

# Criar banco
sudo -u postgres createdb litcircle
sudo -u postgres psql -c "ALTER USER postgres PASSWORD 'postgres';"

# Testar
psql -U postgres -d litcircle -c "SELECT 1;"
```

### Windows
Baixe em postgresql.org/download/windows. Na instalação, defina a senha do user `postgres` como `postgres`. Crie o banco `litcircle` pelo pgAdmin que vem junto.

---

## 5. VSCode + Extensões (Kauã)

Baixe em code.visualstudio.com. Extensões:
```bash
code --install-extension dbaeumer.vscode-eslint
code --install-extension esbenp.prettier-vscode
code --install-extension rangav.vscode-thunder-client
code --install-extension eamodio.gitlens
code --install-extension ritwickdey.LiveServer
```

A extensão **Live Server** permite servir o frontend HTML com hot reload.

---

## 6. IntelliJ IDEA Community (Rafael)

Baixe em jetbrains.com/idea → Community Edition (grátis).
Plugins: Lombok, Rainbow Brackets.

---

## 7. Clonar e estruturar

```bash
git clone git@github.com:devkauapimentel/LitCircle.git
cd LitCircle
```

---

## 8. Verificação final

```bash
git --version       # 2.x+
node --version      # v20.x
java --version      # 21.x
psql --version      # 15+
```

Se tudo funcionou, o ambiente está pronto.
