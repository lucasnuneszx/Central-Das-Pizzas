# 🔧 Resolver: Erro de Banco em Outros Dispositivos

## 🚨 Problema

O sistema funciona perfeitamente no seu dispositivo, mas em **celular e outros notebooks** dá erro de banco de dados.

## 🔍 Possíveis Causas

1. **NextAuth não está confiando no host** - causa falha na validação de origem
2. **Cookies não funcionam** em outros dispositivos
3. **Sessão não é criada** corretamente em outros dispositivos
4. **Prisma Client não consegue conectar** devido a problemas de autenticação

## ✅ Solução Aplicada

### 1. Adicionado `trustHost: true`

Isso permite que o NextAuth funcione em qualquer dispositivo/rede, sem validar estritamente o host.

**Arquivos modificados:**
- `lib/auth-config.ts` - Adicionado `trustHost: true`
- `app/api/auth/[...nextauth]/route.ts` - Adicionado `trustHost: true`

### 2. Melhorado tratamento de erros do Prisma

Adicionado `errorFormat: 'minimal'` para melhorar logs de erro.

---

## 📋 O Que Fazer Agora

### 1. Aguardar Deploy (2-3 minutos)

O código foi atualizado e enviado. Aguarde o Railway fazer o deploy.

### 2. Verificar Variáveis de Ambiente

Certifique-se de que estas variáveis estão configuradas no Railway:

1. **Railway Dashboard** → Serviço "web" → **Variables**

2. Verifique:
   - ✅ `NEXTAUTH_URL` = `https://centraldaspizzas.up.railway.app` (URL pública)
   - ✅ `NEXTAUTH_SECRET` existe e tem valor
   - ✅ `DATABASE_URL` está configurada corretamente (URL pública, não interna)

### 3. Limpar Cache nos Outros Dispositivos

**No celular/outro notebook:**

1. Limpe cache do navegador
2. Ou use modo anônimo/privado
3. Tente fazer login novamente

### 4. Verificar Logs do Railway

1. **Railway Dashboard** → Serviço "web" → **Logs**
2. Procure por erros relacionados a:
   - `Can't reach database server`
   - `Authentication failed`
   - `Invalid credentials`

---

## 🧪 Teste Após Deploy

1. **Aguarde 2-3 minutos** após o push
2. **No celular/outro notebook:**
   - Limpe cache do navegador
   - Acesse: `https://centraldaspizzas.up.railway.app/auth/signin`
   - Tente fazer login

3. **Se ainda não funcionar:**
   - Verifique os logs do Railway
   - Verifique se as variáveis de ambiente estão corretas
   - Tente fazer login em modo anônimo/privado

---

## 🔍 Diagnóstico

Se ainda não funcionar, acesse no dispositivo que não funciona:

```
https://centraldaspizzas.up.railway.app/api/health?action=diagnose
```

Isso vai mostrar:
- Se `DATABASE_URL` está configurada
- Se `NEXTAUTH_SECRET` está configurado
- Se `NEXTAUTH_URL` está configurado

---

## 📝 O Que Mudou

**Antes:**
- NextAuth validava estritamente o host
- Podia falhar em diferentes dispositivos/redes

**Depois:**
- `trustHost: true` - NextAuth confia em qualquer host/rede
- Melhor tratamento de erros do Prisma
- Cookies configurados para funcionar em qualquer dispositivo

---

## 🚀 Próximo Passo

**Aguarde 2-3 minutos** para o deploy ser aplicado, depois teste novamente nos outros dispositivos.

Se ainda não funcionar, verifique os logs do Railway para identificar o erro específico.

