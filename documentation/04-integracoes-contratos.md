# BaseERP - Integrações e Contratos

## 🎨 Padrões Recomendados

- **📢 Published Language:** Eventos publicados para mudanças de estado que interessam a outros BCs (event-driven)
- **⚡ APIs Síncronas:** Apenas quando necessário (pricing em tempo real, checagem de crédito)
- **🛡️ Anti-Corruption Layer (ACL):** Para integrar com sistemas legados ou 3PL que tenham modelos distintos
- **📋 MDM como Conformist:** MDM dita modelo e publica canonical events; outros BCs mantêm cópias locais (materialized views)

## 📋 Exemplos de Contratos (Integration Events)

```json
CustomerUpdated { customerId, name, addresses[], creditLimit }
ProductMasterChanged { productId, sku, dimensions, uom }
OrderCreated { orderId, customerId, items[], requestedDate }
InventoryAllocated { orderId, allocations[] }
OrderShipped { orderId, shipmentId, tracking }
InvoiceIssued { invoiceId, orderId, amount, taxBreakdown }
PaymentReceived { paymentId, invoiceId, amount }
```

## ⚡ Quando Usar Síncrono vs Assíncrono

### 🔄 Síncrono
- Pricing lookup durante checkout (latência tolerável)
- Checagem crédito para aprovação imediata

### 📡 Assíncrono
- Reservar estoque
- Downstream accounting post-invoice
- Notificações para 3PL

## 🗺️ Context Map (Padrões de Relacionamento)

```
MDM —(Published Language)→ All
├─ MDM publica eventos de mudança de produto/cliente
└─ Todos consomem e materializam

CRM —(Conformist)→ OMS
├─ OMS aceita modelo de CRM para cliente
└─ CRM é dono do modelo comercial

Pricing —(Anti-Corruption)→ OMS
├─ OMS solicita preço final via API
├─ Pricing aplica regras complexas e retorna price DTO
└─ ACL mapeia

OMS —(Published Language)→ WMS, Billing
├─ OMS publica OrderCreated → WMS aloca
├─ Quando alocação confirmada InventoryAllocated volta
└─ OMS aciona Billing quando pedido faturável

WMS —(ACL)→ 3PL/Transportadoras
├─ WMS traduz instruções para EDI/CSV
└─ 3PL é bounded context separado

Billing —(Published Language)→ Accounting
├─ Billing publica InvoiceIssued
└─ Accounting gera lançamentos contábeis

Procurement —(Published Language)→ WMS
└─ Recebimento de PO atualiza WMS inventory
```

## ⚠️ Conflitos Típicos Mapeados

- **🎯 Source of Truth disputado:** Ex., produto — resolvido com MDM dono e cópias sincronizadas
- **👥 Modelo de clientes divergente:** CRM vs Accounting (use canonical projection e reconciliation)
- **📦 Disponibilidade física vs comercial:** WMS é dono do físico; OMS mantém disponibilidade comercial (reservas, buffers)