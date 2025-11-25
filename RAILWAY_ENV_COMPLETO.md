# 🔧 Variáveis de Ambiente Completas para Railway

## 📋 Lista Completa - Copie e Cole

---

## ✅ OBRIGATÓRIAS (Sem essas, o sistema não funciona)

### 1. DATABASE_URL
```
DATABASE_URL=postgresql://postgres:senha@host:port/database?sslmode=require
```
**Como obter:**
- Crie banco PostgreSQL no Railway
- Vá em Variables do banco
- Copie o valor de `DATABASE_URL`

### 2. NEXTAUTH_URL
```
NEXTAUTH_URL=https://www.centraldaspizzas.com
```
**Ou temporariamente:**
```
NEXTAUTH_URL=https://seu-projeto.up.railway.app
```

### 3. NEXTAUTH_SECRET
```
NEXTAUTH_SECRET=gerar-com-openssl-rand-base64-32
```
**Como gerar:**
```bash
openssl rand -base64 32
```

---

## 🤖 OBRIGATÓRIAS para Mila (IA WhatsApp)

### 4. OPENAI_API_KEY
```
OPENAI_API_KEY=sk-proj-your-openai-api-key-here
```

### 5. EVOLUTION_API_URL
```
EVOLUTION_API_URL=https://api.evolution-api.com
```

### 6. EVOLUTION_API_KEY
```
EVOLUTION_API_KEY=sua-evolution-api-key-aqui
```

### 7. EVOLUTION_INSTANCE_NAME
```
EVOLUTION_INSTANCE_NAME=central-das-pizzas
```

### 8. WHATSAPP_WEBHOOK_TOKEN
```
WHATSAPP_WEBHOOK_TOKEN=gerar-token-secreto-aleatorio
```
**Como gerar:**
```bash
openssl rand -hex 32
```

---

## ⚙️ OPCIONAIS (Mas recomendadas)

### iFood API
```
IFOOD_API_URL=https://api.ifood.com.br
IFOOD_API_KEY=sua-ifood-api-key
IFOOD_MERCHANT_ID=seu-merchant-id
```

### Cloudinary (Upload de Imagens)
```
CLOUDINARY_CLOUD_NAME=seu-cloud-name
CLOUDINARY_API_KEY=sua-api-key
CLOUDINARY_API_SECRET=seu-api-secret
```

### Impressora
```
PRINTER_IP=192.168.1.100
PRINTER_PORT=9100
```

### Configurações da Loja
```
RESTAURANT_NAME=Central das Pizzas Av Sul
RESTAURANT_ADDRESS=Av. Sul, 104 - Verdes Horizontes, Camaçari - BA, 42810-021
RESTAURANT_PHONE=(71) 99156-5893
RESTAURANT_EMAIL=contato@centraldaspizzas.com
DELIVERY_ESTIMATE=35 - 70min
OPENING_HOURS=Seg-Dom: 18h-23h
DELIVERY_FEE=5.00
MIN_ORDER_VALUE=25.00
```

---

## 📝 Como Adicionar no Railway

### Método 1: Via Dashboard

1. Acesse: https://railway.app/dashboard
2. Selecione seu projeto
3. Clique no serviço **"web"**
4. Vá na aba **"Variables"**
5. Para cada variável:
   - Clique em **"New Variable"** ou **"+"**
   - **Name:** Nome da variável
   - **Value:** Valor da variável
   - Clique em **"Add"**

### Método 2: Via Railway CLI

```bash
# Instalar Railway CLI
npm i -g @railway/cli

# Login
railway login

# Adicionar variáveis
railway variables set DATABASE_URL="postgresql://..."
railway variables set NEXTAUTH_URL="https://www.centraldaspizzas.com"
railway variables set NEXTAUTH_SECRET="seu-secret"
# ... repita para todas
```

---

## 🎯 Lista Mínima para Funcionar

Se quiser apenas fazer funcionar (sem WhatsApp/IA):

```
DATABASE_URL=[do banco PostgreSQL do Railway]
NEXTAUTH_URL=https://www.centraldaspizzas.com
NEXTAUTH_SECRET=[gerar com openssl rand -base64 32]
```

---

## 🎯 Lista Completa com Mila

Para ter tudo funcionando (incluindo WhatsApp/IA):

```
DATABASE_URL=[do banco PostgreSQL do Railway]
NEXTAUTH_URL=https://www.centraldaspizzas.com
NEXTAUTH_SECRET=[gerar com openssl rand -base64 32]
OPENAI_API_KEY=sk-proj-your-openai-api-key-here
EVOLUTION_API_URL=https://api.evolution-api.com
EVOLUTION_API_KEY=[sua-evolution-api-key]
EVOLUTION_INSTANCE_NAME=central-das-pizzas
WHATSAPP_WEBHOOK_TOKEN=[gerar com openssl rand -hex 32]
```

---

## ✅ Checklist

- [ ] `DATABASE_URL` (do banco PostgreSQL)
- [ ] `NEXTAUTH_URL` (URL do seu domínio)
- [ ] `NEXTAUTH_SECRET` (gerado)
- [ ] `OPENAI_API_KEY` (se usar Mila)
- [ ] `EVOLUTION_API_KEY` (se usar WhatsApp)
- [ ] `EVOLUTION_INSTANCE_NAME` (se usar WhatsApp)
- [ ] `WHATSAPP_WEBHOOK_TOKEN` (se usar WhatsApp)

---

**Adicione todas as obrigatórias e faça redeploy!** 🚀

