---
title: Ativação do Adobe Real-Time CDP
description: Referência de arquitetura para ativar públicos-alvo e dados de perfil do Adobe Real-Time CDP para anúncios, redes sociais, armazenamento em nuvem e destinos corporativos.
solution: Real-Time Customer Data Platform, Experience Platform
product_v2:
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
    internal-label: Real-Time Customer Data Platform
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 1d6ba1444c119437eb8a86d5c4a1050d56d16023
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%
---
# Ativação do Adobe Real-Time CDP

Esta arquitetura mostra como o Adobe [!DNL Real-Time Customer Data Platform] ([!DNL Real-Time CDP]) ativa públicos-alvo e dados de perfil para publicidade, redes sociais, armazenamento na nuvem e destinos corporativos por meio de fluxos de dados em lote e em fluxo contínuo.

## Ativação de público-alvo e perfil

A arquitetura ilustra o caminho de ativação compartilhado de [!DNL Real-Time CDP] públicos-alvo e perfis para aplicativos de destino. Ele inclui ativação de destino para plataformas de publicidade e sociais, bem como destinos corporativos usados para armazenamento, análise e fluxos de trabalho de aplicativos downstream.

![Arquitetura de ativação de perfil e público-alvo da Adobe Real-Time CDP](assets/real_time_cdp_activation.png){width="1000" zoomable="yes"}

## Padrões de caso de uso compatíveis

A arquitetura acima aceita os seguintes padrões de caso de uso:

- [Ativação de público-alvo para destinos](/help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md) — Ative públicos-alvo avaliados para anúncios, redes sociais, armazenamento na nuvem, CRM e outros destinos da empresa.
- [Personalização anônima da Web para visitantes](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md) — Ofereça suporte à ativação de públicos-alvo e à personalização baseada em perfil em canais digitais.

## Fluxos de dados primários e pontos de integração

- Assimilar dados do cliente de várias fontes para [!DNL Real-Time CDP].
- Unificar atributos de identidade e perfil em [!DNL Real-Time Customer Profile].
- Avalie os perfis em públicos-alvo para ativação.
- Faça streaming ou lote de alterações de perfil e público-alvo em anúncios, redes sociais, armazenamento em nuvem e destinos corporativos.
- Use os dados de perfil e público ativados nos fluxos de trabalho de marketing, vendas, suporte, análise e personalização de downstream.

## Leitura adicional

- [Destinos do Adobe Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [Ativar públicos para destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Medidas de proteção do Adobe Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/guardrails/overview)
