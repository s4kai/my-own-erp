# BaseERP - Análise DDD: Domínios

## 🎯 Visão Geral dos Domínios

### 🔥 Core Domain (Núcleo)
- **Order Management (OMS)**
  - Orquestra pedidos, reservas, split
  - Políticas de prioridade e regras de crédito
  - **Diferencial competitivo:** Tratativas comerciais, SLAs e políticas de fulfillment

### 🛠️ Supporting Domains (Apoio)
- **Warehouse & Inventory (WMS)** — Localização física, alocação, picking, lotes/serial, inventário cíclico
- **Pricing & Promotions** — Cálculo de preço (listas, contratos, descontos, promos)
- **Procurement** — Requisições, PO, recebimento, contratos com fornecedores
- **Manufacturing (MES/Production)** — Ordens de produção, roteiros, apontamento, custo
- **Billing & Fiscal (Finance-AR)** — Emissão de notas fiscais eletrônicas, faturamento, contas a receber
- **Payables & Treasury (Finance-AP/Treasury)** — Contas a pagar, conciliação, pagamentos
- **Accounting / Ledger** — Livro razão, lançamentos contábeis, fechamento fiscal
- **CRM / Customer** — Cadastro, contratos comerciais, limites/condições
- **Service / Field Service** — Ordens de serviço, RMA, contratos de manutenção
- **MDM (Master Data Management)** — Produto, cliente, fornecedor (fonte de verdade)
- **Integration / Messaging** — Barramento de eventos, transformação, roteamento
- **Reporting / BI** — Data warehouse, OLAP, KPIs

### ⚙️ Generic Domains
- **Auth/Identity** — Autenticação e autorização
- **Audit** — Auditoria e logs
- **Notifications** — Notificações

> **💡 Observação:** OMS foi escolhido como Core porque expressa regras de negócio que definem a vantagem competitiva (políticas comerciais, roteamento de pedidos, priorização).

## 🎯 DDD Estratégico — Visão e Objetivos

### Visão
Plataforma modular orientada a domínios que:
- Permite evolução independente dos subsistemas críticos (OMS, WMS, Billing)
- Garante consistência de negócio por contratos bem definidos
- Reduz custo de manutenção
- Acelera lançamento de novas regras comerciais

### 📈 Objetivos de Negócio
- 🚀 **Reduzir lead time** de pedidos em 30% (primeiro ano)
- 📊 **Aumentar acurácia** de inventário para ≥99%
- 💰 **Diminuir custo** de manutenção do core em 40% por modularização
- ⚖️ **Garantir conformidade** fiscal com auditabilidade por jurisdição

### 🔗 Como Domínios se Conectam ao Propósito
- **OMS:** Converte oportunidades em receita e coordena WMS e Billing para cumprir promessas
- **WMS:** Habilita a entrega física
- **Billing:** Fecha a conversão em caixa e alimenta Accounting
- **MDM:** Garante integridade dos cadastros usados por todos os domínios