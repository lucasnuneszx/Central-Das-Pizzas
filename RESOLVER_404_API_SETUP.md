# 🔧 Resolver 404 em /api/setup - Guia de Troubleshooting

## 🚨 Problema

Endpoints `/api/setup/*` retornam 404 mesmo após commits e pushes.

## ✅ Soluções (em ordem de prioridade)

### 1️⃣ Verificar se Outros Endpoints Funcionam

Teste primeiro:
```
https://centraldaspizzas.up.railway.app/api/health
```

**Se funcionar:**
- O problema é específico de `/api/setup`
- Continue com as soluções abaixo

**Se NÃO funcionar:**
- O problema é geral com a API
- Verifique se o Railway está fazendo deploy
- Veja os logs do Railway

---

### 2️⃣ Verificar Deploy no Railway

1. **Railway Dashboard** → Serviço "web"
2. Aba **"Deployments"**
3. Verifique:
   - ✅ Há um deploy recente?
   - ✅ Status é "Deployment successful"?
   - ✅ O commit mais recente está listado?

**Se não há deploy recente:**
- O Railway pode não estar conectado ao GitHub
- Verifique: Settings → Source → GitHub Repository

---

### 3️⃣ Forçar Rebuild Completo

1. **Railway Dashboard** → Serviço "web"
2. Aba **"Settings"**
3. Procure por **"Clear Build Cache"** ou **"Rebuild"**
4. Clique para limpar cache e fazer rebuild

**OU:**

1. Aba **"Deployments"**
2. Clique nos **3 pontos** (⋯) do último deploy
3. Selecione **"Redeploy"**
4. Aguarde 3-5 minutos

---

### 4️⃣ Verificar Logs do Railway

1. **Railway Dashboard** → Serviço "web"
2. Aba **"Logs"**
3. Procure por:
   - ❌ Erros de build
   - ❌ Erros de compilação TypeScript
   - ❌ Erros de Prisma
   - ❌ Erros de Next.js

**Erros comuns:**
- `Module not found` → Arquivo não está no repositório
- `Type error` → Erro de TypeScript
- `Prisma error` → Problema com schema

---

### 5️⃣ Verificar Estrutura de Arquivos

Certifique-se de que os arquivos estão na estrutura correta:

```
app/
  api/
    setup/
      create-tables/
        route.ts  ← Deve existir
      create-users/
        route.ts  ← Deve existir
      test/
        route.ts  ← Deve existir
```

**Verificar localmente:**
```bash
ls -la app/api/setup/
```

---

### 6️⃣ Verificar Next.js Build

O Railway executa `npm run railway:build` que faz:
1. `prisma generate`
2. `next build`

**Verifique se o build está funcionando:**
- Railway → Logs → Procure por "Build successful"

**Se houver erro de build:**
- Corrija o erro primeiro
- Faça commit e push
- Aguarde novo deploy

---

### 7️⃣ Verificar se Arquivos Estão no Git

```bash
git ls-files app/api/setup/
```

**Deve listar:**
- `app/api/setup/create-tables/route.ts`
- `app/api/setup/create-users/route.ts`
- `app/api/setup/test/route.ts`
- etc.

**Se algum arquivo não aparecer:**
```bash
git add app/api/setup/
git commit -m "fix: adiciona arquivos de setup ao git"
git push origin main
```

---

### 8️⃣ Solução Alternativa: Usar Endpoint Existente

Se nada funcionar, você pode usar o endpoint `/api/setup/create-users` que já existia antes:

```
https://centraldaspizzas.up.railway.app/api/setup/create-users
```

Este endpoint já cria usuários e pode funcionar mesmo se outros não funcionarem.

---

### 9️⃣ Último Recurso: Recrear Serviço

Se nada funcionar:

1. **Railway Dashboard** → Seu projeto
2. Delete o serviço "web"
3. Crie um novo serviço
4. Conecte ao mesmo repositório GitHub
5. Configure as variáveis de ambiente novamente
6. Faça deploy

⚠️ **Atenção:** Isso vai recriar tudo do zero.

---

## 🔍 Diagnóstico Rápido

Execute estes testes na ordem:

1. ✅ `/api/health` funciona?
2. ✅ `/api/setup/create-users` funciona? (endpoint antigo)
3. ✅ `/api/setup/test` funciona? (endpoint novo)
4. ✅ Railway mostra deploy recente?
5. ✅ Logs não mostram erros?

---

## 📋 Checklist Final

- [ ] Testei `/api/health`
- [ ] Verifiquei deploy no Railway
- [ ] Limpei cache e fiz rebuild
- [ ] Verifiquei logs do Railway
- [ ] Verifiquei estrutura de arquivos
- [ ] Verifiquei se arquivos estão no git
- [ ] Tentei endpoint alternativo

---

**Se nada funcionar, o problema pode ser:**
- Railway não está conectado ao GitHub
- Build está falhando silenciosamente
- Cache do Next.js está desatualizado
- Problema de permissões no Railway

**Solução:** Entre em contato com suporte do Railway ou recrie o serviço.

