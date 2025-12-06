# 🔧 Solução Alternativa: Setup Manual

## 🚨 Problema

O endpoint `/api/health?action=...` não está funcionando porque o deploy não foi aplicado ainda.

## ✅ Solução: Usar Scripts Diretamente

Como os endpoints não estão funcionando, você pode executar os scripts diretamente no Railway ou usar o Prisma Studio.

### Opção 1: Executar Scripts no Railway (Recomendado)

1. **Railway Dashboard** → Serviço "web"
2. Aba **"Settings"** → **"Shell"** ou **"Terminal"**
3. Execute os comandos abaixo:

#### Criar Tabelas:
```bash
npx prisma db push --accept-data-loss --skip-generate
```

#### Criar Usuários (via script):
```bash
node -e "
const { PrismaClient } = require('@prisma/client');
const bcrypt = require('bcryptjs');
const prisma = new PrismaClient();

(async () => {
  const hashedPassword = await bcrypt.hash('123456', 12);
  const users = [
    { name: 'Administrador', email: 'admin@centraldaspizzas.com', password: hashedPassword, role: 'ADMIN' },
    { name: 'Gerente', email: 'gerente@centraldaspizzas.com', password: hashedPassword, role: 'MANAGER' },
    { name: 'Caixa', email: 'caixa@centraldaspizzas.com', password: hashedPassword, role: 'CASHIER' },
    { name: 'Cozinha', email: 'cozinha@centraldaspizzas.com', password: hashedPassword, role: 'KITCHEN' }
  ];
  
  for (const user of users) {
    try {
      const existing = await prisma.user.findUnique({ where: { email: user.email } });
      if (!existing) {
        await prisma.user.create({ data: user });
        console.log('✅ Criado:', user.email);
      } else {
        console.log('⚠️ Já existe:', user.email);
      }
    } catch (error) {
      console.error('❌ Erro:', user.email, error.message);
    }
  }
  
  await prisma.\$disconnect();
})();
"
```

### Opção 2: Usar Prisma Studio

1. **Railway Dashboard** → Serviço "web"
2. Aba **"Settings"** → **"Shell"** ou **"Terminal"**
3. Execute:
```bash
npx prisma studio
```
4. Isso abrirá uma interface web para gerenciar o banco
5. Você pode criar usuários manualmente pela interface

### Opção 3: Usar SQL Direto

1. **Railway Dashboard** → Serviço **PostgreSQL**
2. Aba **"Data"** ou **"Query"**
3. Execute:

```sql
-- Criar usuários (senha é hash de '123456')
INSERT INTO "User" (id, name, email, password, role, "createdAt", "updatedAt")
VALUES 
  (gen_random_uuid(), 'Administrador', 'admin@centraldaspizzas.com', '$2a$12$LQv3c1yqBWVHxkd0LHAkCOYz6TtxMQJqhN8/LewY5GyY5Y5Y5Y5Y5Y', 'ADMIN', NOW(), NOW()),
  (gen_random_uuid(), 'Gerente', 'gerente@centraldaspizzas.com', '$2a$12$LQv3c1yqBWVHxkd0LHAkCOYz6TtxMQJqhN8/LewY5GyY5Y5Y5Y5Y', 'MANAGER', NOW(), NOW()),
  (gen_random_uuid(), 'Caixa', 'caixa@centraldaspizzas.com', '$2a$12$LQv3c1yqBWVHxkd0LHAkCOYz6TtxMQJqhN8/LewY5GyY5Y5Y5Y5Y', 'CASHIER', NOW(), NOW()),
  (gen_random_uuid(), 'Cozinha', 'cozinha@centraldaspizzas.com', '$2a$12$LQv3c1yqBWVHxkd0LHAkCOYz6TtxMQJqhN8/LewY5GyY5Y5Y5Y5Y', 'KITCHEN', NOW(), NOW())
ON CONFLICT (email) DO NOTHING;
```

**⚠️ Nota:** O hash acima é um exemplo. Você precisa gerar o hash real de '123456' usando bcrypt.

---

## 🎯 Solução Mais Simples: Aguardar Deploy

Se você já executou os comandos no seu dispositivo e funcionou, os dados já estão no banco. Você pode simplesmente:

1. **Aguardar o deploy ser aplicado** (pode levar até 10 minutos)
2. **Fazer login diretamente:**
   - URL: `https://centraldaspizzas.up.railway.app/auth/signin`
   - Email: `admin@centraldaspizzas.com`
   - Senha: `123456`

Os usuários já foram criados quando você testou no seu dispositivo, então o login deve funcionar mesmo que os endpoints não estejam respondendo corretamente em outros dispositivos.

---

## 📋 Checklist

- [ ] Tentei executar scripts no Railway Shell
- [ ] Tentei usar Prisma Studio
- [ ] Tentei fazer login diretamente (usuários já criados)
- [ ] Aguardei 10 minutos para deploy ser aplicado
- [ ] Verifiquei logs do Railway para erros

---

## 🚀 Próximo Passo

**Tente fazer login diretamente** - os usuários já foram criados quando você testou no seu dispositivo, então o sistema deve funcionar mesmo que os endpoints de setup não estejam respondendo em outros dispositivos.

