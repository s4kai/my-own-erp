# BaseERP - Bounded Contexts

> **Decomposição:** Cada BC = serviço/aplicação ou módulo bem isolado

## 👥 Customer/CRM BC
- **Modelos:** Customer, Account, Contact, CreditProfile, Contract
- **Responsabilidades:** Cadastro, relacionamento, limites de crédito, condições contratuais

## 💰 Pricing & Promotions BC
- **Modelos:** PriceList, PriceRule, PromoCampaign, PriceCalculationService
- **Responsabilidades:** Cálculo de preço final para OMS; expõe APIs síncronas e eventos de mudança

## 🎯 Order Management (OMS) BC — **CORE**
- **Modelos:** SalesOrder, SalesOrderLine, Reservation, FulfillmentRequest
- **Responsabilidades:** Lifecycle do pedido, roteamento, policy engine para split, orquestra Sagas para fulfillment

## 📦 Warehouse & Inventory (WMS) BC
- **Modelos:** InventoryItem (by location/lote/serial), Movement, Picking, Putaway
- **Responsabilidades:** Estado físico do estoque, alocação, instruções de picking

## 🛒 Procurement BC
- **Modelos:** PurchaseRequisition, PurchaseOrder, SupplierContract
- **Responsabilidades:** Abastecimento, PO lifecycle, recepção

## 🏭 Production / MES BC
- **Modelos:** ProductionOrder, BOM, Routing, OperationLog
- **Responsabilidades:** Criar/fechar ordens de produção, consumir matérias no WMS

## 🧾 Billing & Fiscal (Finance-AR) BC
- **Modelos:** Invoice, FiscalDocument (NF-e/CTe), PaymentTerm
- **Responsabilidades:** Emitir NF-e, gerar faturas, integração cobrança

## 📊 Accounting / Ledger BC
- **Modelos:** JournalEntry, GLAccount, PeriodClose
- **Responsabilidades:** Lançar eventos contábeis, fechamento

## 💳 Treasury / Payments BC
- **Modelos:** BankAccount, PaymentBatch, Reconciliation
- **Responsabilidades:** Pagamentos, conciliação (CNAB/SEPA)

## 🗂️ MDM BC
- **Modelos:** ProductMaster, SupplierMaster
- **Responsabilidades:** Fonte autorizada; publica alterações para demais BCs

## 🔄 Integration / Event Bus (Infra)
- **Modelos:** IntegrationEvent schemas
- **Responsabilidades:** Transporte, retry, DLQ, transformações ACL

## 📈 Reporting / DW BC
- **Modelos:** Read models, star schemas
- **Responsabilidades:** Consultas analíticas, KPIs