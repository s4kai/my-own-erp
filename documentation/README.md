# BaseERP - Documentação DDD

Documentação completa da arquitetura DDD para o sistema BaseERP da XPTO Empresa S.A.

## 📚 Estrutura da Documentação

### [01 - Cenário Empresarial](01-cenario-empresarial.md)
- Perfil da empresa XPTO S.A.
- Objetivos do ERP
- Pain points atuais
- Stakeholders e KPIs

### [02 - Análise DDD: Domínios](02-analise-ddd-dominios.md)
- Core, Supporting e Generic Domains
- Visão estratégica DDD
- Objetivos de negócio
- Conexão entre domínios

### [03 - Bounded Contexts](03-bounded-contexts.md)
- Decomposição em BCs
- Modelos e responsabilidades
- Order Management como Core Domain

### [04 - Integrações e Contratos](04-integracoes-contratos.md)
- Padrões de integração DDD
- Context Map
- Contratos de eventos
- Síncrono vs Assíncrono

### [05 - Consistência e Orquestração](05-consistencia-orquestracao.md)
- Políticas de consistência
- Saga Pattern
- Estratégias de compensação

### [06 - Implementação Técnica](06-implementacao-tecnica.md)
- Stack tecnológico
- Padrões de código
- Estratégia de dados
- Event-driven architecture
- Segurança e compliance

### [07 - Roadmap e Métricas](07-roadmap-metricas.md)
- Fases de implementação
- KPIs técnicos e de negócio
- Monitoramento
- Conclusões

## 🎯 Visão Geral

Este projeto implementa uma arquitetura **Domain-Driven Design (DDD)** para um ERP empresarial, focando em:

- **Modularidade** através de bounded contexts bem definidos
- **Escalabilidade** com event-driven architecture
- **Manutenibilidade** com separação clara de responsabilidades
- **Compliance** fiscal e auditoria completa

## 🔥 Core Domain

**Order Management (OMS)** foi identificado como o domínio central, responsável por orquestrar todo o processo de fulfillment e expressar as regras de negócio que definem a vantagem competitiva da empresa.

## 🛠️ Tecnologias Principais

- Java 17 + Spring Boot 3.x
- Apache Kafka para eventos
- PostgreSQL + Redis
- Docker + Kubernetes
- Observabilidade completa (Prometheus, Grafana, ELK)

---

**Empresa:** XPTO Empresa S.A.  
**Projeto:** BaseERP com DDD  
**Arquitetura:** Monólito Modular → Microserviços orientados a domínio