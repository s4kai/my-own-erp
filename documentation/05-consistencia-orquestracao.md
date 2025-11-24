# BaseERP - Consistência e Orquestração

## 🎯 Princípio

Evitar transações distribuídas; usar **eventual consistency** com compensação quando necessário.

## 📋 Estratégias por Cenário

### 🔄 Saga Pattern para Order Fulfillment

```
OMS → Reserve Inventory (WMS) → Allocate → Ship → Invoice (Billing)
├─ Falha na reserva: cancela pedido
├─ Falha no shipping: libera reserva
└─ Falha no faturamento: reversa shipment
```

### ⚡ Consistência Imediata (Síncrona)
- Pricing durante checkout
- Credit check para aprovação
- Inventory availability check

### 🌊 Consistência Eventual (Assíncrona)
- Atualização de saldos contábeis
- Sincronização de master data
- Notificações para clientes

### 🛡️ Compensação
- Timeout em reservas de estoque (auto-release)
- Reversal de alocações em caso de cancelamento
- Estorno contábil para devoluções