---
title: Personalization do cliente conhecido com Target
description: Integre perfis e públicos-alvo da RTCDP com o Adobe Target.
landing-page-description: Integre perfis e públicos-alvo da RTCDP com o Adobe Target.
short-description: Integre perfis e públicos-alvo da RTCDP com o Adobe Target.
solution: Real-Time Customer Data Platform, Target, Experience Platform
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
TQID: https://experienceleague.adobe.com/1ti2SqfAFOgnKbaJ70xwGI-xHDE1WXJ7-oTStcJJy1E
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: ba929a52-9339-4154-9487-317dc875a3c7
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
subfeature_v2:
  - id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342
  - id: cdd3e38b-fec2-4f39-8b10-83ddaab1ac16
  - id: d1823595-9241-4128-8a33-e4ac3bf08773
  - id: ee602049-8a18-43df-9299-a689a025a371
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 045fac8362795eefcac0ef5202fe7a90cb6875da
workflow-type: tm+mt
source-wordcount: 735
ht-degree: 37%

---

# Personalization do cliente conhecido com Target

>[!TIP]
>Este blueprint também está disponível como um [padrão de caso de uso](/help/blueprints/use-case-patterns/personalization/audience-sharing-with-target.md) no Personalization.

## Casos de uso

* Personalização online com dados de clientes conhecidos
* Aprimoramento da página de aterrissagem
* Personalização com base em visualizações anteriores de produtos/conteúdos, afinidade com produtos/conteúdos, atributos ambientais e dados demográficos, além de dados offline, como transações, insights de fidelização e de CRM e modelos de insights
* Compartilhar e direcionar públicos-alvo definidos na Plataforma de dados do cliente em tempo real em sites e aplicativos móveis que usam o Adobe Target

## Aplicativos

* [!UICONTROL Real-time Customer Data Platform]
* Adobe Target

### Documentação de referência

* [Conexão Adobe Target para a Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html)
* [Configuração da sequência de dados do Edge](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=pt-BR)

## Padrões de integração

| Padrão de integração | Recurso | Pré-requisitos |
|--------------------|------------|---------------|
| **Avaliação de segmento em tempo real na Edge compartilhada da Plataforma de dados do cliente em tempo real para o Target** | - Avalie os públicos-alvo em tempo real para a mesma ou a próxima personalização de página na Edge. <br>- Quaisquer segmentos avaliados em fluxo ou em lote também serão projetados na Edge Network para serem incluídos na avaliação e personalização do segmento de borda. | - O Web/Mobile SDK deve ser implementado para a API do Edge Network Server. <br>- A sequência de dados deve ser configurada no Experience Edge com o Target e a extensão do Experience Platform habilitados. <br>- O destino deve ser configurado em Destinos da Real-time Customer Data Platform. <br>- A integração com o Target requer uma organização IMS igual à da instância da Experience Platform. |
| **Compartilhamento de streaming e público em lote da Real-time Customer Data Platform para o Target através da abordagem da Edge** | - Compartilhe públicos de transmissão e em lote da Real-time Customer Data Platform com o Target por meio do Edge Network. <br>- Os públicos avaliados em tempo real requerem a implementação do Web SDK e do Edge Network. | - A implementação da API do Target na Web/Mobile SDK ou Edge não é necessária para compartilhar públicos-alvo de transmissão e RTCDP em lote com o Target, mas é necessária para habilitar a avaliação de segmentos de borda em tempo real. <br>- Se estiver usando a AT.js, somente a integração de perfil em relação ao namespace de identidade ECID será suportada. <br>- Para pesquisas de namespace de identidade personalizada na Edge, a implantação da API Web SDK/Edge é necessária e cada identidade deve ser definida como uma identidade no mapa de identidade. <br>- O destino deve ser configurado em Destinos da Real-time Customer Data Platform, somente a sandbox de produção padrão no RTCDP é compatível. <br>- A integração com o Target requer uma organização IMS igual à da instância da Experience Platform. |
| **Compartilhamento de streaming e público em lote da Real-time Customer Data Platform para o Target e a Audience Manager através da Abordagem do Serviço de Compartilhamento de Público** | - Esse padrão de integração pode ser aproveitado quando o enriquecimento adicional de dados e públicos de terceiros no Audience Manager for desejado. | - O Web/Mobile SDK não é necessário para compartilhar streaming e públicos em lote com o Target, mas é necessário para habilitar a avaliação de segmentos de borda em tempo real. <br>- Se estiver usando a AT.js, somente a integração de perfil em relação ao namespace de identidade ECID será suportada. <br>- Para pesquisas de namespace de identidade personalizada na Edge, a implantação da API Web SDK/Edge é necessária e cada identidade deve ser definida como uma identidade no mapa de identidade. <br>- A projeção de público através do serviço de compartilhamento de público deve ser provisionada. <br>- A integração com o Target requer uma organização IMS igual à da instância da Experience Platform. <br>- Somente os públicos-alvo da sandbox de produção padrão dão suporte ao serviço principal de compartilhamento de público-alvo. |

## Compartilhamento de público-alvo em tempo real, por streaming e em lote com o Adobe Target

Arquitetura

![Arquitetura de referência para o Blueprint Online/Offline do Web Personalization](assets/RTCDP-Target.png)

Detalhes da sequência

![Arquitetura de referência para o Blueprint Online/Offline do Web Personalization](assets/RTCDP-Target_flow.png)

Visão geral da arquitetura

![Arquitetura de referência para o Blueprint Online/Offline do Web Personalization](assets/personalization_with_apps.png)

## Documentação relacionada

### Documentação do SDK

* [Documentação do Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR)
* [Documentação de tags do Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)
* [Documentação do Experience Cloud ID Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR)

### Documentação de segmentação

* [Visão geral da segmentação do Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=pt-BR)
* [Segmentação em tempo real](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=pt-BR)
* [Segmentação de transmissão](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=pt-BR)
* [Compartilhamento de segmentos do Adobe Analytics por meio do Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=pt-BR)
* [Configuração da política de mesclagem](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=pt-BR#create-a-merge-policy)

### Tutoriais

* [Personalização de próxima ocorrência com Real-Time CDP e Adobe Target](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=pt-BR)
