---
title: Integração do Adobe Customer Journey Analytics e do Adobe Journey Optimizer
description: Arquitetura para analisar insights de campanha e jornadas do Adobe Journey Optimizer no Adobe Customer Journey Analytics e publicar públicos-alvo para execução de jornadas.
solution: Customer Journey Analytics, Journey Optimizer, Experience Platform
product_v2:
  - id: e98b7246-966c-4318-9e95-cad2f7a17dc7
    internal-label: Customer Journey Analytics
  - id: cb954087-f4fc-4456-afb9-e939cabcdc79
    internal-label: Journey Optimizer
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 1d6ba1444c119437eb8a86d5c4a1050d56d16023
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%
---
# Integração do Adobe Customer Journey Analytics e do Adobe Journey Optimizer

Essa arquitetura mostra como os dados de entrega e interação do Adobe Journey Optimizer fluem pelo Adobe Experience Platform para o Customer Journey Analytics para insights de campanha e jornada. Os públicos-alvo criados no Customer Journey Analytics podem ser publicados por meio do Real-Time CDP para uso na execução do Journey Optimizer.

## Arquitetura de insights do Campaign e do jornada

A arquitetura conecta a entrega do Journey Optimizer e os dados de interação com o Experience Platform e o Customer Journey Analytics para gerar relatórios, analisar e criar públicos-alvo.

![Arquitetura de integração do Adobe Customer Journey Analytics e do Adobe Journey Optimizer](assets/cja_ajo_integration.png){width="1000" zoomable="yes"}

## Fluxos de dados primários e pontos de integração

- Os dados de entrega, interação e eficácia do Journey Optimizer são compartilhados com os serviços de dados da Experience Platform.
- Os dados do Experience Platform são assimilados na Customer Journey Analytics por meio de uma conexão CJA.
- As visualizações de dados e análises do Customer Journey Analytics fornecem campanha e jornada insight.
- Os públicos-alvo criados no Customer Journey Analytics são publicados no Real-Time CDP.
- Os públicos-alvo da Real-Time CDP estão disponíveis para execução e personalização do Journey Optimizer jornada.

## Padrões de caso de uso compatíveis

- [Análise de clientes e geração de insight](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md) — Analise o comportamento da campanha e da jornada entre canais.
- [Mensagens acionadas por evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) — Use sinais de jornada e de cliente para oferecer suporte a mensagens orquestradas.

## Leitura adicional

- [Relatórios do Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/reporting/reports/sharing-overview)
- [Visão geral do Customer Journey Analytics](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-overview/cja-overview)
- [Publicar públicos da Customer Journey Analytics](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/audiences/publish)
