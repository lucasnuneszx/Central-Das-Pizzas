# 🔄 Como Forçar Rebuild Completo no Railway

## ⚠️ PROBLEMA RESOLVIDO

O código foi atualizado para forçar rebuild completo e limpar cache automaticamente.

## 📋 Passos Manuais no Railway (SE AINDA NÃO FUNCIONAR)

### 1. Limpar Cache de Build
1. Acesse: https://railway.app
2. Selecione seu projeto
3. Vá em **Settings** → **Build**
4. Clique em **Clear Build Cache**
5. Confirme a ação

### 2. Forçar Redeploy
1. Vá em **Deployments**
2. Clique nos **3 pontos** (⋯) no deployment mais recente
3. Selecione **Redeploy**
4. Ou clique em **Deploy Latest** na barra superior

### 3. Verificar Variáveis de Ambiente
Certifique-se de que estas variáveis estão configuradas:
- `DATABASE_URL` - URL do PostgreSQL
- `JWT_SECRET` - Chave secreta para JWT
- `NODE_ENV=production`

### 4. Verificar Logs
1. Vá em **Deployments**
2. Clique no deployment mais recente
3. Verifique os logs de build
4. Procure por: `✅ Compiled successfully`

## 🔧 O que foi feito no código:

1. ✅ Script de build atualizado para limpar `.next` e `node_modules/.cache`
2. ✅ `nixpacks.toml` criado para forçar rebuild sem cache
3. ✅ `generateBuildId` dinâmico no `next.config.js`
4. ✅ Versão atualizada para `5.3.0`
5. ✅ `.railway-version` atualizado para forçar rebuild

## 🚀 Após o Deploy

Acesse: `https://centraldaspizzas.up.railway.app/auth/signin`

Você deve ver:
- `v5.3 - JWT Auth System - NO CACHE`
- `Build: v5.3-[timestamp]-[random]`
- `Time: [timestamp completo]`

Se ainda aparecer versão antiga, o problema é cache do Railway que precisa ser limpo manualmente.

