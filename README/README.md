# 🍷 DouroVinhos Mobile Sales (Offline-First)

![Status](https://img.shields.io/badge/Status-Architecture%20Approved-success)
![Role](https://img.shields.io/badge/Role-Lead%20Functional%20Analyst-blue)
![Domain](https://img.shields.io/badge/Domain-Distribution%20%7C%20HORECA-orange)

> **Projeto de Análise Funcional e Arquitetura de Solução** para digitalização de força de vendas em ambientes de baixa conectividade.

---

## 🚀 O Desafio de Negócio
A **DouroVinhos**, líder na distribuição de vinhos no Norte de Portugal, operava com um processo manual (Papel/WhatsApp) que resultava em:
* **Rutura de Stock:** Vendas de produtos esgotados devido ao *delay* na inserção de pedidos.
* **Perda de Receita:** Vendedores incapazes de validar crédito em tempo real.
* **Ineficiência:** 2 horas diárias perdidas em burocracia.

**O Requisito Crítico:** A App precisava de funcionar em **Caves de Vinho (Sem Internet/Offline)**, mas garantir a validação financeira exigida pelo ERP Legado (PHC).

---

## 💡 A Solução Arquitetada (Híbrida)
Para equilibrar a **Velocidade de Venda** (Negócio) com a **Segurança do ERP** (TI), desenhei uma arquitetura **Offline-First com Edge Validation**.

### 1. O Fluxo de Solução (BPMN)
![Fluxo BPMN](./03-architecture/BPMN_Fluxo_Vendas_Integracao_v1.jpg)
*(Clique na imagem para ampliar)*

### 2. Decisões Técnicas Chave
| Desafio | Solução Arquitetada | Porquê? |
| :--- | :--- | :--- |
| **Vender na Cave (Offline)** | **Local SQLite Cache** | A App baixa dados críticos (Stock/Saldos) via Wi-Fi pela manhã. O vendedor trabalha autonomamente o dia todo. |
| **Evitar Calotes (Risco)** | **Edge Validation** | A validação de Crédito ocorre **no dispositivo** antes do envio, baseada no cache local. Bloqueia a venda na origem. |
| **Proteger o ERP Antigo** | **Async Batch Processing** | O ERP não é exposto à internet. A App escreve numa **Tabela Intermédia** e um Job processa a cada 10 min. |

---

## 📂 Estrutura do Projeto (Artefactos)

A documentação segue o ciclo de vida completo de Engenharia de Requisitos:

### 🔹 [Fase 1: Planeamento & Intake](./01-planning/)
* **Project Charter (One-Pager):** Definição de escopo, restrições (3 Meses) e análise inicial de riscos (Offline vs ERP).

### 🔹 [Fase 2: Discovery & AS-IS](./02-discovery/)
* **Relatório de Discovery:** Entrevistas com Stakeholders (Vendas e TI).
* **Glossário de Negócio:** Definição de termos críticos (Ex: "Bonificação 12+1", "Stamp PHC") para evitar erros de desenvolvimento.

### 🔹 [Fase 3: Arquitetura Técnica (TO-BE)](./03-architecture/)
* **Especificação de Processo:** Documento detalhado da lógica de sincronização.
* **Diagrama BPMN 2.0:** Fluxo técnico de tratamento de erros, *polling* e gestão de estados (Pendente/Sucesso/Erro).

---

## 🛠️ Tech Stack & Ferramentas
* **Modelagem:** BPMN 2.0 (Camunda Modeler)
* **Documentação:** Especificação Técnica Funcional
* **Metodologia:** Agile / Hybrid
* **Integração:** SQL Server Views, REST concepts, Batch Processing

---

## 🏆 Resultado Projetado (KPIs)
A arquitetura aprovada permite:
1.  **Zero Bloqueios:** O vendedor nunca para de vender, tenha internet ou não.
2.  **Proteção do Legado:** O ERP PHC mantém a performance sem sofrer requisições diretas.
3.  **Feedback Transparente:** O vendedor sabe exatamente o estado da encomenda (Ícones de Estado).

---
*Autor: Jaqueline Daniel*
*Portfolio de Análise Funcional Sénior*