# 🚨 Forçar Deploy no Railway

## Problema

O código foi atualizado, mas o Railway ainda está servindo a versão antiga.

## ✅ Soluções

### 1️⃣ **Verificar Status do Deploy**

1. **Railway Dashboard** → Serviço "web"
2. Aba **"Deployments"**
3. Verifique:
   - ✅ Há um deploy recente? (últimos 5 minutos)
   - ✅ Status é "Deployment successful"?
   - ✅ O commit mais recente está listado?

**Se não há deploy recente:**
- O Railway pode não ter detectado o push
- Continue com as soluções abaixo

### 2️⃣ **Forçar Redeploy Manual**

1. **Railway Dashboard** → Serviço "web"
2. Aba **"Deployments"**
3. Clique nos **3 pontos** (⋯) do último deploy
4. Selecione **"Redeploy"**
5. Aguarde **3-5 minutos**

### 3️⃣ **Limpar Cache e Rebuild**

1. **Railway Dashboard** → Serviço "web"
2. Aba **"Settings"**
3. Procure por **"Clear Build Cache"** ou **"Rebuild"**
4. Clique para limpar cache
5. Aguarde **5-10 minutos** (pode demorar mais)

### 4️⃣ **Verificar Logs do Build**

1. **Railway Dashboard** → Serviço "web"
2. Aba **"Deployments"** → Clique no último deploy
3. Veja os logs do **Build**
4. Procure por:
   - ✅ `Build successful`
   - ❌ `Build failed`
   - ❌ `Error: ...`

**Se houver erro de build:**
- Corrija o erro primeiro
- Faça commit e push novamente

### 5️⃣ **Verificar Conexão GitHub → Railway**

1. **Railway Dashboard** → Serviço "web"
2. Aba **"Settings"** → **"Source"**
3. Verifique:
   - ✅ Repositório: `lucasnuneszx/Central-Das-Pizzas`
   - ✅ Branch: `main`
   - ✅ Auto-deploy está habilitado?

**Se não estiver conectado:**
- Reconecte o repositório
- Ou faça deploy manual

### 6️⃣ **Fazer Commit Vazio para Forçar Deploy**

Execute localmente:
```bash
git commit --allow-empty -m "trigger: forçar deploy no Railway"
git push origin main
```

Isso força o Railway a detectar uma mudança e fazer deploy.

---

## 🔍 Como Saber se Funcionou

Após aguardar 3-5 minutos, teste:

```
https://centraldaspizzas.up.railway.app/api/health?action=diagnose
```

**Versão ANTIGA (ainda não deployado):**
```json
{"status":"ok","timestamp":"2025-11-29T16:44:32.460Z"}
```

**Versão NOVA (deploy aplicado):**
```json
{
  "success": true,
  "environment": {
    "hasDatabaseUrl": true,
    "hasNextAuthSecret": true,
    ...
  }
}
```

---

## 📋 Checklist

- [ ] Verifiquei status do deploy no Railway
- [ ] Fiz redeploy manual
- [ ] Limpei cache do build
- [ ] Verifiquei logs do build
- [ ] Verifiquei conexão GitHub → Railway
- [ ] Fiz commit vazio para forçar deploy
- [ ] Aguardei 3-5 minutos
- [ ] Testei novamente com `?action=diagnose`

---

## ⏱️ Tempo Esperado

- **Deploy automático:** 2-3 minutos após push
- **Redeploy manual:** 3-5 minutos
- **Rebuild completo:** 5-10 minutos

Se após 10 minutos ainda não funcionar, há um problema mais grave que precisa ser investigado.

