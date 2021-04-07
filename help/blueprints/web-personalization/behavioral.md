---
title: Esquema de personalização comportamental da Web
description: Personalize com base no comportamento online e nos dados do público-alvo.
solution: Experience Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7085thumb-web-personalization-scenario1.jpg
exl-id: b9882c2c-cb45-4efa-a85c-8fe48f641a12
translation-type: tm+mt
source-git-commit: 844fff1cefe367575beb5c03aa0f0d026eb9f39b
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# Esquema de personalização comportamental da Web

Personalize com base no comportamento online e nos dados do público-alvo.

## Casos de uso

* Otimização da página de aterrissagem
* Definição de direcionamento comportamental
* Personalização com base em visualizações anteriores de produto/conteúdo, afinidade de produto/conteúdo, atributos ambientais, dados de público-alvo de terceiros e demografia

## Aplicativos

* Adobe Target
* Adobe Analytics (opcional)
* Adobe Audience Manager (opcional)

## Arquitetura

<img src="assets/personalization.svg" alt="Arquitetura de referência para o cenário de Personalização comportamental da Web" style="border:1px solid #4a4a4a" />


## Medidas de proteção

Por padrão, o serviço de compartilhamento de segmentos permite que no máximo 75 públicos-alvo sejam compartilhados para cada conjunto de relatórios do Adobe Analytics. Se o Audience Manager estiver sendo usado para o compartilhamento de público, não há limite para o número de públicos que podem ser compartilhados. 

## Pré-requisitos de implementação

| Aplicativo/Serviço | Biblioteca obrigatória | Notas |
|---|---|---|
| Adobe Target | Plataforma Web SDK*, at.js 0.9.1+ ou mbox.js 61+ | A at.js é preferida, pois a mbox.js não está mais sendo desenvolvida. |
| Adobe Audience Manager (opcional) | Plataforma Web SDK* ou dil.js 5.0+ |  |
| Adobe Analytics (opcional) | Plataforma Web SDK* ou AppMeasurement.js 1.6.4+ |  |
| Serviço de identidade do Experience Cloud | Plataforma Web SDK* ou VisitorAPI.js 2.0+ |  |
| SDK do Experience Platform Mobile (opcional) | 4.11 ou superior para iOS e Android™ |  |
| Experience Platform Web SDK | 1.0, a versão atual do SDK do Experience Platform tem [vários casos de uso ainda não suportados nos aplicativos do Experience Cloud](https://github.com/adobe/alloy/projects/5) |  |

## Etapas da implementação

1. [Implemente o Adobe ](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) Target para seus aplicativos móveis ou da Web.

   Se estiver usando o Audience Manager ou o Analytics:

1. [Implementar o Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html)
1. [Implementar o Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)
1. [Implementar o serviço de identidade do Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html)

   >[!NOTE]
   >
   >Cada aplicativo deve usar a ID do Experience Cloud e fazer parte da mesma Org do Experience Cloud para permitir o compartilhamento de público-alvo entre aplicativos.

1. [Solicitar provisionamento para os serviços de Pessoas e Compartilhamento de público-alvo (públicos compartilhados)](https://www.adobe.com/go/audiences)
1. Construa segmentos em [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-build.html) ou [Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html) e [configure esses públicos para compartilhar com o Experience Cloud](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html) (se estiver usando o Audience Manager ou Adobe Analytics)
1. Quando os públicos-alvo estiverem disponíveis no Adobe Target, eles poderão ser usados para [segmentar experiências com o Adobe Target](https://experienceleague.adobe.com/docs/target/using/audiences/target.html)


## Diagramas de fluxo de dados da implementação

O Web/Mobile Personalization Blueprint pode ser implementado usando o SDK da Web da plataforma ou o SDK móvel e a rede de borda, ou usando SDKs tradicionais específicos do aplicativo (por exemplo, AppMeasurement.js).

### Plataforma Web/Mobile SDK e Abordagem de rede de borda

<img src="assets/websdkflow.svg" alt="Arquitetura de referência para o SDK da Web da plataforma/SDK móvel e abordagem de rede de borda" style="border:1px solid #4a4a4a" />


### Abordagem do SDK específica do aplicativo

<img src="assets/appsdkflow.png" alt="Arquitetura de referência para a abordagem SDK específica do aplicativo" style="border:1px solid #4a4a4a" />


## Documentação relacionada

* [Públicos-alvo do Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html)
* [Integrar o Audience Manager ao Adobe Target](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html)
* [Compartilhamento de segmentos do Adobe Analytics por meio de AAM](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)


## Publicações de blog relacionadas

* [Blueprint para personalização da Web usando o perfil do cliente em tempo real do Adobe Experience Platform](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [Integração do Adobe Experience Platform Decisioning Engine com AEM Sites da Web](https://jaeness.medium.com/integrating-adobe-experience-platform-decisioning-engine-with-aem-websites-9c222acd12e2)
* [Como os públicos-alvo preditivos do Adobe Experience Platform melhoram as experiências personalizadas](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [Adobe Experience Platform Web SDK para Gerenciamento de público-alvo](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [Implementação do perfil do cliente em tempo real da Adobe Experience Platform por meio do nosso programa &quot;zero para clientes&quot;](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [Como a Adobe Experience Platform pode ajudar os clientes a personalizar suas mensagens móveis em tempo real com o Journey Orchestration Service e um fornecedor de mensagens móveis](https://medium.com/adobetech/how-adobe-experience-platform-helped-a-client-personalize-their-mobile-messaging-in-real-time-with-7d634aefa098)
* [Segmentação em segundos: Como a Adobe Experience Platform tornou os perfis de clientes em tempo real uma realidade](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
