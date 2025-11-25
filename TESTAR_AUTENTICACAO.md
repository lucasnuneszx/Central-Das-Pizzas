# 🔍 Testar Autenticação - Diagnóstico Completo

## ⚠️ Problema: Login ainda não funciona

Mesmo após criar usuários, o login ainda dá erro 401.

---

## ✅ SOLUÇÃO: Testar Tudo

### **PASSO 1: Testar Autenticação**

Acesse no navegador (POST request) ou use curl:

```bash
curl -X POST https://centraldaspizzass.up.railway.app/api/test-auth \
  -H "Content-Type: application/json" \
  -d '{"email":"admin@centraldaspizzas.com","password":"123456"}'
```

**OU use um cliente REST como Postman ou Insomnia:**

- **URL:** `https://centraldaspizzass.up.railway.app/api/test-auth`
- **Method:** `POST`
- **Body (JSON):**
  ```json
  {
    "email": "admin@centraldaspizzas.com",
    "password": "123456"
  }
  ```

Isso vai mostrar **exatamente** o que está errado!

---

### **PASSO 2: Verificar Resultado do Teste**

O teste vai mostrar:

- ✅ `NEXTAUTH_SECRET configurado` - Deve estar OK
- ✅ `NEXTAUTH_URL configurado` - Deve estar OK
- ✅ `DATABASE_URL configurado` - Deve estar OK
- ✅ `Conexão com banco` - Deve estar OK
- ✅ `Usuário encontrado` - Deve estar OK
- ✅ `Senha válida` - Deve estar OK

**Se algum estiver ❌, esse é o problema!**

---

### **PASSO 3: Corrigir o Problema Encontrado**

#### Se `NEXTAUTH_SECRET` estiver faltando:

1. Gere o secret:
   ```bash
   openssl rand -base64 32
   ```
2. Adicione no Railway → Serviço "web" → Variables
3. Nome: `NEXTAUTH_SECRET`
4. Valor: Cole o valor gerado
5. Redeploy

#### Se `NEXTAUTH_URL` estiver faltando:

1. Railway → Serviço "web" → Variables
2. Adicione: `NEXTAUTH_URL` = `https://centraldaspizzass.up.railway.app`
3. Redeploy

#### Se `DATABASE_URL` estiver errado:

1. Railway → Serviço PostgreSQL → Variables
2. Copie `DATABASE_PUBLIC_URL`
3. Railway → Serviço "web" → Variables
4. Adicione/Atualize `DATABASE_URL` com a URL pública
5. Redeploy

#### Se `Senha válida` estiver ❌:

Os usuários podem ter sido criados com senha errada. Recrie:

1. Acesse: `https://centraldaspizzass.up.railway.app/api/setup/create-users`
2. Isso vai recriar os usuários com senha correta

---

### **PASSO 4: Verificar Logs do Railway**

1. Railway Dashboard → Serviço "web"
2. Vá em **Deployments** → Último deploy → **Logs**
3. Procure por:
   - `✅ Login bem-sucedido: admin@centraldaspizzas.com`
   - `❌ Usuário não encontrado: ...`
   - `❌ Senha inválida para: ...`
   - `❌ Erro na autenticação: ...`

---

## 📋 Checklist Completo

- [ ] Executei `/api/test-auth` e vi os resultados
- [ ] Todos os checks estão ✅
- [ ] Se algum check está ❌, corrigi o problema
- [ ] Fiz redeploy após corrigir
- [ ] Verifiquei os logs do Railway
- [ ] Tentei login novamente

---

## 🎯 Resumo

1. **Teste:** `/api/test-auth` para ver o que está errado
2. **Corrija:** O problema encontrado no teste
3. **Redeploy:** Após corrigir
4. **Teste Login:** Novamente

---

**Execute o teste primeiro para ver exatamente o que está errado!** 🔍

