# 🍷 DouroVinhos Mobile Sales (Offline-First)

![DouroVinhos Cover](./assets/project-cover.png)

---

<div align="center">

![Status](https://img.shields.io/badge/Status-Project%20Ready%20for%20Dev-success?style=for-the-badge)
![Role](https://img.shields.io/badge/Role-Lead%20Functional%20Analyst-blue?style=for-the-badge)
![Domain](https://img.shields.io/badge/Domain-Distribution%20%7C%20HORECA-orange?style=for-the-badge)

</div>

> **Projeto de Análise Funcional, Arquitetura de Solução e Prova de Conceito (MVP)** para digitalização de força de vendas em ambientes de baixa conectividade.

---

## 🚀 O Desafio de Negócio
A **DouroVinhos**, líder na distribuição de vinhos no Norte de Portugal, operava com um processo manual que resultava em:
* **Rutura de Stock:** Vendas de produtos esgotados devido ao *delay* na sincronização.
* **Risco Financeiro:** Vendedores incapazes de validar dívidas de clientes em tempo real.
* **Ineficiência:** 2 horas diárias perdidas em burocracia de papel.

**O Requisito Crítico:** A App tinha de garantir vendas em **Caves de Vinho (Offline)**, mas respeitar as regras de negócio complexas (ex: Tabela Mínima, Bonificações) exigidas pelo ERP Legado (PHC).

---

## 💡 A Solução Arquitetada (Híbrida)
Para equilibrar a **Velocidade de Venda** (Negócio) com a **Segurança** (TI), desenhei uma arquitetura **Offline-First com Edge Validation**.

### 1. O Fluxo de Solução (BPMN)
![Fluxo BPMN](./03-architecture/BPMN_Fluxo_Vendas_Integracao_v1.jpg)
*(Clique na imagem para ampliar)*

### 2. Decisões Técnicas Chave
| Desafio | Solução Arquitetada | Porquê? |
| :--- | :--- | :--- |
| **Vender na Cave (Offline)** | **Local SQLite Cache** | A App baixa dados mestres via Wi-Fi pela manhã. O vendedor trabalha autonomamente o dia todo. |
| **Evitar Calotes (Risco)** | **Edge Validation** | A validação de Crédito e Preço Mínimo ocorre **no dispositivo** antes do envio, bloqueando a venda na origem. |
| **Proteger o ERP Antigo** | **Async Batch Processing** | O ERP não é exposto à internet. A App escreve numa **Tabela Intermédia** e um Job processa a cada 10 min. |

---

## 📂 Estrutura do Projeto (Artefactos)

A documentação segue o ciclo de vida completo de Engenharia de Software (SDLC):

### 🔹 [Fase 1: Planeamento & Intake](./01-planning/)
* **Project Charter (One-Pager):** Definição de escopo, restrições e análise inicial de riscos.

### 🔹 [Fase 2: Discovery & AS-IS](./02-discovery/)
* **Relatório de Discovery:** Levantamento de requisitos com Stakeholders.
* **Glossário de Negócio:** Definição de termos críticos (Ex: "Bonificação 12+1", "Stamp PHC").

### 🔹 [Fase 3: Arquitetura Técnica (TO-BE)](./03-architecture/)
* **Especificação de Processo:** Documento da lógica de sincronização.
* **Diagrama BPMN 2.0:** Fluxo técnico de tratamento de erros, *polling* e gestão de estados.

### 🔹 [Fase 4: Especificação Funcional (SRS)](./04-requirements/)
* **[SRS Completo (Software Requirements Specification)](./04-requirements/01_Especificacao_Funcional_SRS_Completa.pdf):** Documento mestre com todas as User Stories (Gherkin), regras de negócio (ex: Tabela Mínima, Recolhas) e Requisitos Não-Funcionais (RNF).

### 🌟 [BÓNUS: MVP & Prova de Conceito](./05-mvp-demo/)
* **Manual Técnico do MVP:** Documentação da stack (React Native) e arquitetura do protótipo.
* **Evidências Visuais:** Prints e vídeo do sistema funcional a aplicar as regras de negócio (Bloqueio de Crédito e Ofertas).

---

## 🛠️ Tech Stack & Ferramentas
* **Análise:** BPMN 2.0 (Camunda), User Stories (Gherkin), SRS (Standard).
* **Arquitetura:** Offline-First, SQL Server Integration, REST concepts.
* **MVP (PoC):** React Native, Expo, Zustand (State Management).

---
*Autor: Jaqueline Daniel | Portfolio de Análise Funcional Sénior*