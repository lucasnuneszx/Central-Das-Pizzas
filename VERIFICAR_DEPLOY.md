# 🔍 Como Verificar se o Deploy Foi Aplicado

## 1. Verificar Healthcheck

Acesse: `https://centraldaspizzas.up.railway.app/api/health`

**Se o deploy foi aplicado, você verá:**
```json
{
  "status": "ok",
  "version": "4.0-NEW-AUTH-SYSTEM",
  "DEPLOYED": true,
  "newAuthSystem": true,
  "routes": {
    "login": "/api/login",
    "logout": "/api/logout",
    "me": "/api/me",
    "checkUser": "/api/check-user"
  }
}
```

**Se ainda estiver na versão antiga, você verá:**
```json
{
  "status": "ok",
  "timestamp": "2025-11-29T16:44:32.460Z"
}
```

## 2. Testar Rotas de Autenticação

### Teste `/api/login`:
```bash
POST https://centraldaspizzas.up.railway.app/api/login
Content-Type: application/json

{
  "email": "admin@centraldaspizzas.com",
  "password": "123456"
}
```

**Se funcionar:** Retornará `{"success": true, "user": {...}}`
**Se não funcionar:** Retornará `404 Not Found`

### Teste `/api/me`:
```bash
GET https://centraldaspizzas.up.railway.app/api/me
```

**Se funcionar:** Retornará `{"authenticated": false, ...}` ou `{"authenticated": true, "user": {...}}`
**Se não funcionar:** Retornará `404 Not Found`

## 3. Forçar Rebuild no Railway

Se as rotas ainda retornarem 404:

1. **Acesse o painel do Railway**
2. **Vá em Settings → Clear Build Cache**
3. **Clique em "Clear Cache"**
4. **Vá em Deployments**
5. **Clique em "Redeploy"** ou **"Deploy Latest"**

## 4. Verificar Logs do Railway

1. **Acesse o painel do Railway**
2. **Vá em Deployments**
3. **Clique no deployment mais recente**
4. **Verifique os logs de build**

**Procure por:**
- ✅ `Compiled successfully`
- ✅ `Route (app) /api/login`
- ✅ `Route (app) /api/me`
- ✅ `Route (app) /api/logout`

**Se houver erros:**
- ❌ `Module not found`
- ❌ `Type error`
- ❌ `Build failed`

## 5. Verificar Variáveis de Ambiente

No Railway, verifique se estas variáveis estão configuradas:

- `DATABASE_URL` - Deve começar com `postgresql://` ou `postgres://`
- `NEXTAUTH_SECRET` - String aleatória (pode gerar com: `openssl rand -base64 32`)
- `NEXTAUTH_URL` - URL pública do app (ex: `https://centraldaspizzas.up.railway.app`)

## 6. Limpar Cache do Navegador

**Chrome/Edge:**
1. Pressione `Ctrl + Shift + Delete`
2. Selecione "Cache" e "Cookies"
3. Clique em "Limpar dados"

**Ou use modo anônimo:**
- Pressione `Ctrl + Shift + N` (Chrome) ou `Ctrl + Shift + P` (Edge)

## 7. Testar em Modo Anônimo

Abra uma janela anônima e acesse:
- `https://centraldaspizzas.up.railway.app/auth/signin`
- Tente fazer login

## 8. Verificar DATABASE_URL

O erro mostra que o `DATABASE_URL` pode estar mal formatado. Verifique:

**Formato correto:**
```
postgresql://postgres:senha@host:porta/database
```

**No Railway:**
1. Vá em **Variables**
2. Verifique se `DATABASE_URL` começa com `postgresql://`
3. Se não começar, edite e adicione o prefixo correto

## 9. Criar Usuários

Após o deploy funcionar, crie os usuários:

```
GET https://centraldaspizzas.up.railway.app/api/health?action=create-users
```

Ou:

```
GET https://centraldaspizzas.up.railway.app/api/setup/create-users
```

## 10. Diagnóstico Completo

Para ver todas as informações do sistema:

```
GET https://centraldaspizzas.up.railway.app/api/health?action=diagnose
```

---

## ⚠️ Problemas Comuns

### Rotas retornam 404
- **Causa:** Deploy não foi aplicado ou cache do Railway
- **Solução:** Limpar cache e fazer redeploy manual

### Erro de DATABASE_URL
- **Causa:** URL não começa com `postgresql://`
- **Solução:** Editar variável no Railway e adicionar prefixo correto

### Login não funciona
- **Causa:** Usuários não foram criados ou senha incorreta
- **Solução:** Criar usuários via `/api/health?action=create-users`

### Cache do navegador
- **Causa:** Navegador usando versão antiga do JavaScript
- **Solução:** Limpar cache ou usar modo anônimo

