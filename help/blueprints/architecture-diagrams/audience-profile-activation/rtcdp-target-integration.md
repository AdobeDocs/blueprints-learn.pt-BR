---
title: Integração do Adobe Real-Time CDP e do Adobe Target
description: Entenda como os públicos-alvo da Real-Time Customer Data Platform e o contexto de perfil se integram ao Adobe Target por meio da Edge Network.
landing-page-description: Entenda como os públicos-alvo da Real-Time Customer Data Platform e o contexto de perfil se integram ao Adobe Target por meio da Edge Network.
short-description: Entenda como os públicos-alvo da Real-Time Customer Data Platform e o contexto de perfil se integram ao Adobe Target por meio da Edge Network.
solution: Real-Time Customer Data Platform, Target, Experience Platform
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
TQID: https://experienceleague.adobe.com/1ti2SqfAFOgnKbaJ70xwGI-xHDE1WXJ7-oTStcJJy1E
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
    internal-label: Real-Time Customer Data Platform
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
    internal-label: Segmentation
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
    internal-label: Audiences
  - id: ba929a52-9339-4154-9487-317dc875a3c7
    internal-label: Use cases
  - id: c132d929-fa62-4271-803e-b823be07b914
    internal-label: Profile
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
    internal-label: Implementation
subfeature_v2:
  - id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342
    internal-label: Segments
  - id: cdd3e38b-fec2-4f39-8b10-83ddaab1ac16
    internal-label: B2B
  - id: d1823595-9241-4128-8a33-e4ac3bf08773
    internal-label: Audiences
  - id: ee602049-8a18-43df-9299-a689a025a371
    internal-label: Use cases
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
    internal-label: at.js
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
    internal-label: Measurement
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
source-git-commit: ce7331f279a6e59db95ca3b763148440598cde84
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 17%
---
# Integração do Adobe Real-Time CDP e do Adobe Target

Esta arquitetura mostra como o [!DNL Real-Time Customer Data Platform] e o [!DNL Adobe Target] se integram por meio da Edge Network. Ele ajuda a selecionar entre a avaliação de público-alvo em tempo real na borda e o compartilhamento de streaming ou públicos em lote com o Target.

## Aplicativos

* [!DNL Real-Time Customer Data Platform]
* [!DNL Adobe Target]
* Edge Network [!DNL Experience Platform]
* API do Experience Platform Web SDK ou do Edge Network Server

## Escolha uma abordagem de integração

### Avaliação de público-alvo em tempo real na borda

Use esta abordagem quando [!DNL Adobe Target] precisar de públicos avaliados de borda e atributos de perfil para personalização de mesma página ou próxima página. Implemente o Web SDK ou a API do Edge Network Server e configure uma sequência de dados com os serviços [!DNL Adobe Target] e [!DNL Experience Platform] habilitados.

### Compartilhamento de público em lote e streaming no Target

Use esta abordagem quando os públicos avaliados em [!DNL Real-Time Customer Data Platform] precisarem estar disponíveis em [!DNL Adobe Target] sem a avaliação de borda em tempo real. Configure o destino [!DNL Adobe Target] na sandbox de produção padrão. A implementação da API do Web SDK ou do Edge Network Server é necessária somente para pesquisas de avaliação de borda em tempo real ou de namespace de identidade personalizado.

## Diagrama de arquitetura

Este diagrama mostra os principais pontos de integração entre a coleta de dados, o Edge Network, [!DNL Real-Time Customer Data Platform] e [!DNL Adobe Target].

![Arquitetura para integração do Real-Time Customer Data Platform e do Adobe Target](assets/real_time_cdp_target.png){zoomable="yes"}

## Diagrama de fluxo de dados

Esta sequência mostra como uma solicitação de cliente chega à Edge Network, avalia públicos-alvo e contexto de perfil, envia uma solicitação de personalização para [!DNL Adobe Target] e retorna a experiência resultante para o cliente.

![Fluxo de dados para integração do Real-Time Customer Data Platform e do Adobe Target](assets/real_time_cdp_target_data_flow_detail.png){zoomable="yes"}

## Considerações de implantação

* [!DNL Adobe Target] e [!DNL Real-Time Customer Data Platform] devem usar a mesma organização IMS.
* O destino [!DNL Adobe Target] dá suporte à sandbox de produção padrão em [!DNL Real-Time Customer Data Platform].
* Para pesquisas de namespace de identidade personalizada na borda, use o Web SDK ou a API do Edge Network Server e inclua cada identidade no mapa de identidade.
* Se estiver usando at.js, a integração de perfil oferecerá suporte somente ao namespace de identidade da ECID.

## Documentação relacionada

### Configurar a integração

* [Conexão Adobe Target para a Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=pt-BR)
* [Configuração da sequência de dados do Edge](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=pt-BR)

### Implementar na borda

* [Documentação do Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR)
* [Documentação de tags do Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)
* [Documentação do Experience Cloud ID Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR)

### Avaliar públicos-alvo

* [Visão geral da segmentação do Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=pt-BR)
* [Segmentação em tempo real](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=pt-BR)
* [Segmentação de transmissão](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=pt-BR)
* [Configuração da política de mesclagem](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=pt-BR#create-a-merge-policy)
