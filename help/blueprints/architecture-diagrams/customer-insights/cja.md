---
title: Customer Journey Analytics com a Plataforma de dados do cliente em tempo real
description: Unifique e analise dados e comportamentos do cliente em toda a jornada dele no Customer Journey Analytics e publique o público-alvo do CJA para o RTCDP
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 9e1ba723-63f2-4622-ba67-f2a315c3ba0c
TQID: https://experienceleague.adobe.com/gbNXsco0cQIcn5O83ofB-rb0PF65v7kaTZ7mTngqHks
product_v2:
  - id: e98b7246-966c-4318-9e95-cad2f7a17dc7
    internal-label: Customer Journey Analytics
feature_v2:
  - id: ce577701-5b9e-4fe4-8fa3-4eedea976da4
    internal-label: Components
source-git-commit: ce7331f279a6e59db95ca3b763148440598cde84
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 8%
---

# Adobe Customer Journey Analytics

A Adobe Customer Journey Analytics unifica os dados de interação do cliente da Adobe Experience Platform e de outras fontes em um serviço de análise baseado em jornada. Essa arquitetura fornece a referência principal para análise entre canais, derivações de CJA B2B e publicação de públicos-alvo da CJA na Real-Time CDP.

## Arquitetura do Customer Journey Analytics

Este diagrama mostra o fluxo principal dos dados de interação do cliente no Customer Journey Analytics para conexões, visualizações de dados, análise e criação de público-alvo.

![Arquitetura principal do Adobe Customer Journey Analytics](assets/cja.png){width="1000" zoomable="yes"}

## Derivações de arquitetura

- O B2B Customer Journey Analytics estende a arquitetura principal com dimensões de conta, oportunidade, grupo de compra e pessoa para análise baseada em conta.
- O compartilhamento de público do CJA publica públicos-alvo criados do Customer Journey Analytics para o Real-Time CDP para ativação e execução de jornada downstream.

## Fluxos de dados primários e pontos de integração

- Os dados de interação do cliente são coletados da Web, dispositivos móveis, comércio, CRM e outras fontes na Adobe Experience Platform.
- Os conjuntos de dados do Experience Platform são selecionados em uma conexão do Customer Journey Analytics.
- As visualizações de dados expõem métricas, dimensões e campos calculados para a análise entre canais.
- Os públicos-alvo da Customer Journey Analytics podem ser publicados no Real-Time CDP para ativação.
- Os insights do Customer Journey Analytics podem ser usados com o Journey Optimizer por meio da arquitetura de integração dedicada.

## Padrões de caso de uso compatíveis

- [Análise B2B](/help/blueprints/use-case-patterns/b2b/account-analytics.md) — Analise jornadas de nível de conta, oportunidade e pessoa com dimensões B2B.
- [Análise de clientes e geração de insight](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md) — Analise o comportamento entre canais e gere insights de jornada.

## Leitura adicional

- [Visão geral do Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Conexões do Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [Publicar públicos da Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/publish)
