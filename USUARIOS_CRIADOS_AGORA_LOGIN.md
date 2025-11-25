# ✅ Usuários Criados! Agora Corrigir Login

## 🎉 Ótimo! Os Usuários Foram Criados

Você viu:
```json
{
  "created": [
    {"name": "Administrador", "email": "admin@centraldaspizzas.com"},
    {"name": "Gerente", "email": "gerente@centraldaspizzas.com"},
    {"name": "Caixa", "email": "caixa@centraldaspizzas.com"},
    {"name": "Cozinha", "email": "cozinha@centraldaspizzas.com"}
  ]
}
```

✅ **Usuários criados com sucesso!**

---

## ⚠️ Mas o Login Ainda Dá Erro 401

Isso significa que falta configurar as variáveis do NextAuth.

---

## 🔧 CORRIGIR: Adicionar Variáveis Faltantes

### **PASSO 1: Verificar Variáveis no Serviço "web"**

No Railway Dashboard → Serviço "web" → Variables:

#### ✅ Verificar `NEXTAUTH_URL`

**Deve existir e ter o valor:**
```
https://centraldaspizzass.up.railway.app
```

**Se não existir:**
1. Clique em "+ New Variable"
2. **Nome:** `NEXTAUTH_URL`
3. **Valor:** `https://centraldaspizzass.up.railway.app`
4. Clique em "Add"

---

#### ✅ Verificar `NEXTAUTH_SECRET`

**Deve existir e ter um valor gerado**

**Se não existir:**

1. **Gerar o secret:**
   ```bash
   openssl rand -base64 32
   ```
   
   Ou use este gerador online: https://generate-secret.vercel.app/32

2. **Adicionar no Railway:**
   - Clique em "+ New Variable"
   - **Nome:** `NEXTAUTH_SECRET`
   - **Valor:** Cole o valor gerado
   - Clique em "Add"

---

#### ✅ Verificar `DATABASE_URL`

**Deve ser:**
```
postgresql://postgres:XckYAceZBmzqXmJAGDdTSiYevwZkVgTO@trolley.proxy.rlwy.net:54804/railway
```

**NÃO pode ter:** `postgres.railway.internal`

---

### **PASSO 2: Redeploy Obrigatório**

Após adicionar/verificar as variáveis:

1. Vá em **Settings** do serviço "web"
2. Clique em **Redeploy**
3. Aguarde 2-3 minutos até terminar

---

### **PASSO 3: Tentar Login Novamente**

1. Acesse:
   ```
   https://centraldaspizzass.up.railway.app/auth/signin
   ```

2. Use as credenciais:
   - **Email:** `admin@centraldaspizzas.com`
   - **Senha:** `123456`

3. Clique em **"Entrar"**

---

## 📋 Checklist Final

- [x] ✅ Usuários criados (confirmado!)
- [ ] `DATABASE_URL` correto (URL pública)
- [ ] `NEXTAUTH_URL` = `https://centraldaspizzass.up.railway.app`
- [ ] `NEXTAUTH_SECRET` existe e tem valor
- [ ] Redeploy feito após adicionar variáveis
- [ ] Login funcionando

---

## 🔍 Se Ainda Não Funcionar

### Verificar Logs do Railway

1. Vá em **Deployments** → Último deploy → **Logs**
2. Procure por mensagens de autenticação:
   - `✅ Login bem-sucedido: admin@centraldaspizzas.com`
   - `❌ Usuário não encontrado: ...`
   - `❌ Senha inválida para: ...`
   - `❌ Erro na autenticação: ...`

### Verificar se NEXTAUTH_SECRET está correto

O `NEXTAUTH_SECRET` é **obrigatório** para o NextAuth funcionar. Sem ele, sempre dará erro 401.

---

## 🎯 Resumo

1. ✅ **Usuários criados** (já feito!)
2. ⚠️ **Adicionar `NEXTAUTH_URL`** (se não existir)
3. ⚠️ **Adicionar `NEXTAUTH_SECRET`** (se não existir - OBRIGATÓRIO!)
4. ⚠️ **Redeploy** (obrigatório após adicionar variáveis)
5. ✅ **Tentar login**

---

**O problema agora é falta de `NEXTAUTH_SECRET` ou `NEXTAUTH_URL`!** 

Adicione essas variáveis e faça redeploy! 🚀

