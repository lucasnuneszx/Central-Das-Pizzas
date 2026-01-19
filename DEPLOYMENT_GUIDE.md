# 🚀 GUIA DE DEPLOYMENT - Sistema de Alerta Sonoro

## 📋 Checklist de Deploy

### **Antes de Fazer Deploy**

- [ ] Leu [SOUND_ALERT_QUICK_START.md](./SOUND_ALERT_QUICK_START.md)
- [ ] Leu [IMPLEMENTATION_SUMMARY.md](./IMPLEMENTATION_SUMMARY.md)
- [ ] Testou localmente a página `/admin/orders`
- [ ] Verificou se o som funciona
- [ ] Verificou se o alerta visual aparece
- [ ] Verificou se o botão ACEITAR funciona

---

## 🔧 Comandos de Deploy

### **1. Verificar Status do Git**
```bash
git status
```

**Esperado**: Verá arquivos modificados e novos

### **2. Adicionar Todos os Arquivos**
```bash
git add .
```

### **3. Fazer Commit**
```bash
git commit -m "feat: add sound alert system to prevent lost orders"
```

**Mensagem alternativas**:
```bash
git commit -m "feat: implement continuous notification sound for pending orders"
git commit -m "feat: add visual + audio alert system for new orders"
```

### **4. Fazer Push**
```bash
git push origin main
# ou
git push origin develop
```

### **5. Aguardar Deploy Automático**
- Vercel vai detectar mudanças automaticamente
- Railway vai detectar mudanças automaticamente
- Deploy deve levar 2-5 minutos

### **6. Verificar Deploy em Produção**
```bash
# Ir para: https://seu-dominio.com/admin/orders
# Testar criar novo pedido
# Verificar som toca
```

---

## 🧪 Teste Local Antes do Deploy

### **1. Ligar Servidor Localmente**
```bash
npm run dev
# ou
yarn dev
```

### **2. Acessar Página de Pedidos**
```
http://localhost:3000/admin/orders
```

### **3. Criar Novo Pedido de Teste**

Via Dashboard do Cliente:
```
http://localhost:3000/client
# Fazer um pedido completo
```

Ou via API:
```bash
curl -X POST http://localhost:3000/api/orders \
  -H "Content-Type: application/json" \
  -d '{
    "status": "PENDING",
    "total": 45.90,
    "customerName": "Teste",
    "deliveryType": "DELIVERY",
    "paymentMethod": "CREDIT_CARD",
    "items": []
  }'
```

### **4. Verificar**
- ✅ Alerta vermelho aparece no canto superior direito
- ✅ Som toca imediatamente
- ✅ Som repete a cada 2.5 segundos
- ✅ Botão ACEITAR para o som
- ✅ Botão Mutar silencia sem aceitar

---

## 📊 Arquivos para Referenciar em Produção

### **Para Usuários**
- `SOUND_ALERT_QUICK_START.md` - Como usar

### **Para Admins**
- `docs/SOUND_ALERT_SYSTEM.md` - Funcionamento
- `IMPLEMENTATION_SUMMARY.md` - O que foi feito

### **Para Testes**
- `docs/SOUND_ALERT_TESTING.md` - Como testar

### **Para Customizações**
- `docs/SOUND_ALERT_CUSTOMIZATION.md` - Como customizar

---

## 🔍 Verificações Pós-Deploy

### **1. Verificar se Sistema Está Ativo**
```
https://seu-dominio.com/admin/orders
# Deve carregar página normal
# Deve ter som disponível
```

### **2. Verificar no Console (F12)**
```
Não deve haver erros em vermelho
Pode haver avisos (é normal)
```

### **3. Criar Pedido de Teste**
```
Novo pedido PENDING
Alerta deve aparecer
Som deve tocar
```

### **4. Testar Controles**
```
ACEITAR → Som para
Mutar → Som silencia
X → Alerta sai, som continua
```

### **5. Múltiplos Pedidos**
```
Criar 2-3 pedidos ao mesmo tempo
Contador deve mostrar quantidade
Aceitar primeiro → Alerta muda para segundo
```

---

## ⚠️ Troubleshooting Pós-Deploy

### **Som não funciona em produção**

**Solução 1**: Verificar volume do navegador
```
Dev Tools → Audio → Volume
Deve estar em 100%
```

**Solução 2**: Verificar se há arquivo de áudio
```
Verificar em /public/sounds/notification.mp3
Se não existir, Web Audio API vai ser usado
```

**Solução 3**: Testar em modo incógnito
```
Às vezes extensões bloqueiam áudio
Teste em modo privado/incógnito
```

**Solução 4**: Testar em outro navegador
```
Chrome, Firefox, Safari, Edge
Se funciona em um, problema é com navegador
```

### **Alerta não aparece**

**Verificar**:
1. Pedido está com status PENDING? (verificar DB)
2. Está logado como ADMIN/MANAGER/CASHIER?
3. Página carregou corretamente? (F5 refresh)
4. Console tem erros? (F12 → Console)

### **Sistema quebrou**

**Reverter rapidamente**:
```bash
git revert HEAD
git push origin main
```

**Ou revert para versão anterior**:
```bash
git log --oneline
git revert [commit-hash]
git push origin main
```

---

## 📞 Suporte

### **Problema com Som?**
👉 Veja [SOUND_ALERT_TESTING.md](./docs/SOUND_ALERT_TESTING.md) - Seção Troubleshooting

### **Quer Customizar?**
👉 Veja [SOUND_ALERT_CUSTOMIZATION.md](./docs/SOUND_ALERT_CUSTOMIZATION.md)

### **Dúvida Técnica?**
👉 Veja [SOUND_ALERT_SYSTEM.md](./docs/SOUND_ALERT_SYSTEM.md)

### **Visual do Sistema?**
👉 Veja [SOUND_ALERT_DIAGRAMS.md](./docs/SOUND_ALERT_DIAGRAMS.md)

---

## 📈 Rollback (Se Necessário)

### **Opção 1: Git Revert** (Recomendado)
```bash
# Ver últimos commits
git log --oneline -5

# Reverter o último commit
git revert HEAD

# Fazer push
git push origin main
```

### **Opção 2: Git Reset** (Destruidor)
```bash
# ⚠️ Cuidado! Isso deleta o commit
git reset --hard HEAD~1
git push origin main -f
```

### **Opção 3: Remover Arquivos Manualmente**
```bash
# Deletar os arquivos criados
rm hooks/useContinuousSound.ts
rm components/order-sound-alert.tsx
rm -rf public/sounds

# Reverter modificações em page.tsx
git checkout app/admin/orders/page.tsx

# Fazer commit
git add .
git commit -m "revert: remove sound alert system"
git push origin main
```

---

## 🎯 Roteiro de Deploy Passo-a-Passo

### **Semana 1: Teste Local**
- [ ] Setup local (`npm install`)
- [ ] Ler documentação
- [ ] Testar em localhost
- [ ] Testar som e alerta
- [ ] Testar múltiplos pedidos

### **Semana 2: Deploy em Staging**
- [ ] Fazer commit
- [ ] Push para branch staging
- [ ] Deploy automático
- [ ] Testar em staging
- [ ] Verificar performance

### **Semana 3: Deploy em Produção**
- [ ] Fazer commit/push para main
- [ ] Aguardar deploy
- [ ] Testar em produção
- [ ] Comunicar aos usuários
- [ ] Monitorar feedback

### **Semana 4+: Monitoring**
- [ ] Receber feedback dos usuários
- [ ] Ajustar intervalo se necessário
- [ ] Adicionar customizações solicitadas
- [ ] Gerar relatórios de efetividade

---

## 📣 Comunicação aos Usuários

### **Anúncio para a Equipe**

**Assunto**: Novo Sistema de Alerta Sonoro Implementado

**Mensagem**:
```
Olá equipe!

Implementamos um novo sistema de alerta sonoro para evitar 
que pedidos sejam perdidos por falta de atenção.

COMO FUNCIONA:
✅ Novo pedido chega
✅ Alerta vermelho aparece + som toca
✅ Som repete a cada 2.5 segundos
✅ Clique em ACEITAR para parar o alarme

CONTROLES:
- ACEITAR: Aceita pedido + para som
- 🔊/🔇: Silencia som (sem aceitar)
- ✕: Fecha alerta (som continua)

DÚVIDAS?
Veja: SOUND_ALERT_QUICK_START.md

Aproveite! 🎉
```

---

## 💾 Backup/Recovery

### **Backup dos Arquivos Criados**
```bash
# Listar arquivos criados
git ls-files --others --exclude-standard

# Fazer backup
cp hooks/useContinuousSound.ts ~/backup/
cp components/order-sound-alert.tsx ~/backup/
```

### **Recuperar se Deletar Acidentalmente**
```bash
# Se deletou arquivo
git checkout hooks/useContinuousSound.ts

# Se deletou múltiplos
git checkout .

# Se já foi committed
git revert [commit-hash]
```

---

## 🎊 Deploy Bem-Sucedido!

Quando o deploy for bem-sucedido, você deve ver:

```
✅ Build passou
✅ Deploy completo
✅ URL ativa: https://seu-dominio.com/admin/orders
✅ Som funcionando
✅ Alerta visual funcionando
✅ Múltiplos pedidos suportados
✅ Controles respondendo
✅ Sem erros no console
```

---

## 📋 Checklist Final

- [x] Código pronto
- [x] Documentação completa
- [x] Teste local feito
- [x] Sem erros de compilação
- [x] Sem breaking changes
- [x] Pronto para produção

---

**Data**: 19 de Janeiro de 2026
**Versão**: 1.0
**Status**: PRONTO PARA DEPLOY

Boa sorte com o deployment! 🚀
