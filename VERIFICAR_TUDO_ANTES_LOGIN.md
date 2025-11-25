# ✅ Verificar Tudo Antes de Fazer Login

## 🔍 Checklist Completo

### **1️⃣ Verificar se os Usuários Foram Criados**

Acesse no navegador:
```
https://centraldaspizzass.up.railway.app/api/setup/create-users
```

**Você deve ver:**
```json
{
  "success": true,
  "created": [
    {
      "name": "Administrador",
      "email": "admin@centraldaspizzas.com",
      "role": "ADMIN"
    },
    ...
  ],
  "existing": [],
  "errors": []
}
```

**Se aparecer erros ou `created: []`, os usuários NÃO foram criados!**

---

### **2️⃣ Verificar Variáveis de Ambiente no Serviço "web"**

No Railway Dashboard → Serviço "web" → Variables:

#### ✅ `DATABASE_URL`
**Deve ser:**
```
postgresql://postgres:XckYAceZBmzqXmJAGDdTSiYevwZkVgTO@trolley.proxy.rlwy.net:54804/railway
```

**NÃO pode ser:**
- ❌ `postgresql://...@postgres.railway.internal:...`
- ❌ Qualquer URL com `postgres.railway.internal`

#### ✅ `NEXTAUTH_URL`
**Deve ser:**
```
https://centraldaspizzass.up.railway.app
```

#### ✅ `NEXTAUTH_SECRET`
**Deve existir e ter um valor gerado**

**Como gerar (se não tiver):**
```bash
openssl rand -base64 32
```

---

### **3️⃣ Verificar se Fez Redeploy**

Após adicionar/corrigir variáveis:
1. Vá em **Settings** do serviço "web"
2. Clique em **Redeploy**
3. Aguarde 2-3 minutos
4. Verifique se o deploy terminou com sucesso

---

### **4️⃣ Verificar Logs do Railway**

1. Vá em **Deployments** do serviço "web"
2. Clique no último deploy
3. Veja os logs

**Procure por:**
- ✅ `✅ Login bem-sucedido: admin@centraldaspizzas.com`
- ❌ `❌ Usuário não encontrado: ...`
- ❌ `❌ Senha inválida para: ...`
- ❌ `❌ Erro na autenticação: ...`

---

## 🎯 Ordem Correta de Ações

1. **Corrigir `DATABASE_URL`** no serviço "web" (usar URL pública)
2. **Adicionar `NEXTAUTH_URL`** = `https://centraldaspizzass.up.railway.app`
3. **Adicionar `NEXTAUTH_SECRET`** (gerar com openssl)
4. **Fazer Redeploy**
5. **Criar Usuários:** `/api/setup/create-users`
6. **Verificar se usuários foram criados** (deve aparecer em `created`)
7. **Tentar Login**

---

## 🔧 Se Ainda Não Funcionar

### Verificar se o Banco Está Conectado

Acesse:
```
https://centraldaspizzass.up.railway.app/api/health
```

Deve retornar algo como:
```json
{
  "status": "ok",
  "database": "connected"
}
```

Se retornar erro de banco, o `DATABASE_URL` ainda está errado.

---

## 📋 Checklist Final

- [ ] `DATABASE_URL` está correto (URL pública, não interna)
- [ ] `NEXTAUTH_URL` = `https://centraldaspizzass.up.railway.app`
- [ ] `NEXTAUTH_SECRET` existe e tem valor
- [ ] Redeploy foi feito após adicionar variáveis
- [ ] Acessei `/api/setup/create-users` e vi usuários criados
- [ ] Logs do Railway mostram sucesso (não erros)
- [ ] Tentei login e funcionou

---

**Siga essa ordem e verifique cada item!** ✅

