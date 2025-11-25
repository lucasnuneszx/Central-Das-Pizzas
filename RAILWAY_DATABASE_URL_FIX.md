# 🔧 Configurar DATABASE_URL no Railway

## 📋 URL que você tem

```
postgresql://postgres:XckYAceZBmzqXmJAGDdTSiYevwZkVgTO@postgres.railway.internal:5432/railway
```

## ⚠️ Importante

Essa URL usa `postgres.railway.internal`, que é uma URL **interna** do Railway.

### Para o serviço web, você tem 2 opções:

#### Opção 1: Usar URL Pública (Recomendado)

No Railway, o banco geralmente expõe uma URL pública também. Para encontrar:

1. No banco Postgres, vá em **"Variables"**
2. Procure por `DATABASE_URL` ou `PGHOST`
3. Pode haver uma URL com domínio público (não `.internal`)

#### Opção 2: Railway Compartilha Automaticamente

Se os serviços estão no mesmo projeto, o Railway pode compartilhar variáveis automaticamente. Verifique:

1. No serviço **"web"**, vá em **"Variables"**
2. Veja se `DATABASE_URL` já aparece automaticamente
3. Se não aparecer, adicione manualmente

## ✅ Como Adicionar no Serviço Web

### Se a URL interna funcionar:

1. No serviço **"web"**, vá em **"Variables"**
2. Clique em **"New Variable"**
3. Preencha:
   - **Name:** `DATABASE_URL`
   - **Value:** `postgresql://postgres:XckYAceZBmzqXmJAGDdTSiYevwZkVgTO@postgres.railway.internal:5432/railway`
4. Clique em **"Add"**

### Se precisar da URL pública:

1. No banco Postgres, vá em **"Variables"**
2. Procure por uma URL que **NÃO** tenha `.internal`
3. Ou vá em **"Settings"** → **"Networking"** para ver a URL pública

## 🔍 Verificar URL Pública

No banco Postgres:
1. Aba **"Settings"**
2. Procure por **"Public Networking"** ou **"Connection"**
3. Deve mostrar uma URL pública

Ou na aba **"Variables"**, pode haver:
- `DATABASE_URL` (interna)
- `PUBLIC_DATABASE_URL` (pública)
- `PGHOST` (host público)

## 🚀 Após Adicionar

1. Faça **Redeploy** do serviço web
2. O deploy deve funcionar agora!

---

**Adicione a DATABASE_URL no serviço web e faça redeploy!** ✅
