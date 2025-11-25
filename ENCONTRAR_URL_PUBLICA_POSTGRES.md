# 🔍 Como Encontrar a URL Pública do PostgreSQL no Railway

## ⚠️ Problema
Você tem:
```
postgresql://postgres:XckYAceZBmzqXmJAGDdTSiYevwZkVgTO@postgres.railway.internal:5432/railway
```

Isso **NÃO funciona** porque `postgres.railway.internal` é uma URL interna.

---

## ✅ SOLUÇÃO: Encontrar a URL Pública

### **Método 1: Na Aba "Variables" do PostgreSQL**

1. No Railway Dashboard, clique no serviço **PostgreSQL**
2. Vá na aba **"Variables"**
3. Procure por uma destas variáveis:
   - `POSTGRES_URL` (pode ser pública)
   - `POSTGRES_PUBLIC_URL`
   - `DATABASE_URL` (pode ter versão pública)
   - `POSTGRES_HOST` (host público)

4. Se encontrar uma URL com `containers-us-west-xxx.railway.app` ou similar, **use essa!**

---

### **Método 2: Na Aba "Connect" do PostgreSQL**

1. No serviço PostgreSQL, vá na aba **"Connect"**
2. Procure por:
   - **"Connection String"**
   - **"Postgres Connection URL"**
   - **"Public Network"** ou **"Public URL"**

3. Copie a URL que tenha um host público (não `postgres.railway.internal`)

---

### **Método 3: Construir Manualmente**

Se não encontrar, você pode construir usando as variáveis:

1. No serviço PostgreSQL → **Variables**, anote:
   - `PGHOST` (deve ser algo como `containers-us-west-xxx.railway.app`)
   - `PGPORT` (geralmente `5432`)
   - `PGDATABASE` (geralmente `railway`)
   - `PGUSER` (geralmente `postgres`)
   - `PGPASSWORD` (sua senha: `XckYAceZBmzqXmJAGDdTSiYevwZkVgTO`)

2. Monte a URL:
   ```
   postgresql://PGUSER:PGPASSWORD@PGHOST:PGPORT/PGDATABASE
   ```

   **Exemplo:**
   ```
   postgresql://postgres:XckYAceZBmzqXmJAGDdTSiYevwZkVgTO@containers-us-west-123.railway.app:5432/railway
   ```

---

### **Método 4: Usar Railway CLI**

Se tiver Railway CLI instalado:

```bash
railway variables --service postgres
```

Isso mostra todas as variáveis, incluindo o host público.

---

## 🎯 O Que Você Precisa

A URL deve ter este formato:
```
postgresql://postgres:XckYAceZBmzqXmJAGDdTSiYevwZkVgTO@HOST-PUBLICO:5432/railway
```

Onde `HOST-PUBLICO` é algo como:
- ✅ `containers-us-west-123.railway.app`
- ✅ `monorail.proxy.rlwy.net`
- ✅ Qualquer host que termine em `.railway.app` ou `.rlwy.net`

**NÃO use:**
- ❌ `postgres.railway.internal`
- ❌ `localhost`
- ❌ `127.0.0.1`

---

## 📋 Passos para Corrigir

1. **Encontre a URL pública** usando um dos métodos acima
2. **No serviço "web"** → Variables
3. **Delete** o `DATABASE_URL` atual (se existir)
4. **Adicione novo** `DATABASE_URL` com a URL pública
5. **Redeploy** o serviço "web"

---

## 🔍 Dica: Verificar no Railway

No Railway, quando você cria um PostgreSQL, ele geralmente cria:
- Uma URL **interna** (`postgres.railway.internal`) - só funciona dentro da rede
- Uma URL **pública** (com host `.railway.app` ou `.rlwy.net`) - funciona de qualquer lugar

**Você precisa da URL pública!**

---

**Encontre a URL pública e substitua no serviço "web"!** ✅

