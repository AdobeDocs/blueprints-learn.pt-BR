---
title: Personalização da Web/móvel com dados online e offline
description: Sincronize a personalização da Web com emails e outras personalizações de canais conhecidos e anônimos.
landing-page-description: Sincronize a personalização da Web com emails e outras personalizações de canais conhecidos e anônimos.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7194thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: 0746a479d4e651244995a8c355ed4c58b968f0c1
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 93%

---

# Personalização da Web/móvel com dados online e offline

Sincronize a personalização da Web com emails e outras personalizações de canais conhecidos e anônimos.

## Casos de uso

* Aprimoramento da página de aterrissagem
* Direcionamento de perfis comportamentais e offline
* Personalização com base em visualizações anteriores de produtos/conteúdos, afinidade com produtos/conteúdos, características ambientais, dados de público-alvo de terceiros e dados demográficos, além de insights offline, como transações, dados de fidelização e de CRM e modelos de insights
* Compartilhe e direcione públicos-alvo definidos na Real-time Customer Data Platform em sites e aplicativos móveis usando o Adobe Target.

## Aplicativos

* [!UICONTROL Real-time Customer Data Platform]
* Adobe Target
* Adobe Audience Manager (opcional): adiciona dados do público-alvo de terceiros, gráfico de dispositivos com base em co-op, capacidade de apresentar segmentos da Platform no Adobe Analytics e de apresentar segmentos do Adobe Analytics na Platform
* Adobe Analytics (opcional): adiciona a capacidade de criar segmentos com base em dados comportamentais históricos e criar segmentação detalhada a partir dos dados do Adobe Analytics

## Padrões de integração

<table class="tg" style="undefined;table-layout: fixed; width: 790px">
<colgroup>
<col style="width: 20px">
<col style="width: 276px">
<col style="width: 229px">
<col style="width: 265px">
</colgroup>
<thead>
  <tr>
    <th class="tg-y6fn">Nº</th>
    <th class="tg-f7v4">Padrão de integração</th>
    <th class="tg-y6fn">Recurso</th>
    <th class="tg-f7v4">Pré-requisitos</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0lax">1</td>
    <td class="tg-73oq"><span style="font-weight:400;font-style:normal">Compartilhamento de públicos-alvo de transmissão e em lote da RTCDP para o Target e o Audience Manager por meio da abordagem de serviço de compartilhamento de público-alvo</span></td>
    <td class="tg-0lax"><span style="font-weight:400;font-style:normal">– Compartilhe públicos-alvo de transmissão e em lote da RTCDP para o Target e o Audience Manager por meio do serviço de compartilhamento de público-alvo. Os públicos-alvo avaliados em tempo real exigem o WebSDK e a avaliação de público-alvo em tempo real descrita no padrão de integração 3.</span></td>
    <td class="tg-73oq">– A projeção de público-alvo por meio do serviço de compartilhamento de público-alvo deve ser provisionada.<br>– A integração com o Target requer uma organização IMS igual a da instância da Experience Platform.<br>– Para que o Target prossiga, a identidade deve ser transferida para a ECID para que possa ser compartilhada com o Edge. AAM tem uma lista separada de identidades aprovadas para correspondência<br>– A implantação do WebSDK não é necessária para essa integração.</td>
  </tr>
  <tr>
    <td class="tg-0lax">2</td>
    <td class="tg-73oq">Compartilhamento de públicos-alvo de transmissão e em lote da RTCDP para o Target por meio da abordagem do Edge</td>
    <td class="tg-0lax">– Compartilhe públicos-alvo de fluxo e em lote da RTCDP no Target por meio do Edge Network. Os públicos-alvo avaliados em tempo real exigem o WebSDK e a avaliação de público-alvo em tempo real descrita no padrão de integração 3.</td>
    <td class="tg-73oq"><span style="text-decoration:none">– Atualmente em versão beta</span><br>– O destino do Target deve ser configurado em Destinos da RTCDP.<br>– A integração com o Target requer uma organização IMS igual a da instância da Experience Platform.<br>WebSDK não é necessário. WebSDk e AT.js são compatíveis. <br>– Se estiver usando a AT.js, somente a pesquisa de perfil em relação à ECID será suportada. <br>– Para pesquisas de namespace de ID personalizadas no Edge, a implantação do WebSDK é necessária, e cada identidade deve ser definida como uma identidade no mapa de identidade.</td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-73oq">Avaliação de segmento em tempo real da RTCDP no Edge compartilhado com o Target por meio do Edge Network usando o WebSDK.</td>
    <td class="tg-0lax">– Avalie os públicos-alvo em tempo real para a mesma ou próxima personalização de página no Edge.</td>
    <td class="tg-73oq"><span style="text-decoration:none">– Atualmente em versão beta</span><br>– O destino do Target deve ser configurado em Destinos da RTCDP.<br>– A integração com o Target requer uma organização IMS igual a da instância da Experience Platform.<br>– O WebSDK deve ser implementado.<br>– Também compatível por meio da API.</td>
  </tr>
</tbody>
</table>


## Arquitetura

Arquitetura da visão geral

<img src="assets/RTCDP+Target.png" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:80%; border:1px solid #4a4a4a" />

Arquitetura do Fluxo de Processos

<img src="assets/RTCDP+Target_flow.png" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:80%; border:1px solid #4a4a4a" />

Arquitetura detalhada

<img src="assets/personalization_with_apps.png" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:80%; border:1px solid #4a4a4a"/>

## Medidas de proteção

[Consulte as medidas de proteção na página de Visão geral dos Blueprints de personalização móvel e da Web.](overview.md)

## Padrões de implementação

O blueprint de personalização da Web/móvel pode ser implementado por meio das seguintes abordagens, conforme descrito abaixo.

1. Usando o [!UICONTROL SDK da Web da Platform] ou o [!UICONTROL SDK móvel da Platform] e o [!UICONTROL Edge Network].
1. Usando SDKs tradicionais específicos para aplicativos (por exemplo, AppMeasurement.js)

### 1. Abordagem do Edge e do SDK da Web/Móvel da Platform

[Consulte o blueprint do SDK da Web e móvel da Experience Platform](../data-ingestion/websdk.md)

### 2. Abordagem do SDK específico para aplicativos

<img src="assets/app_sdk_flow.png" alt="Arquitetura de referência para abordagem do SDK específico para aplicativos" style="width:80%; border:1px solid #4a4a4a" />

## Pré-requisitos de implementação

Pré-requisitos de identidade

* O compartilhamento de públicos-alvo da Adobe Experience Platform para o Adobe Target requer o uso da ECID como identidade.
* Identidades alternativas também podem ser usadas para compartilhar públicos-alvo da Experience Platform com o Adobe Target por meio do Audience Manager. A Experience Platform ativa públicos-alvo para o Audience Manager por meio dos seguintes namespaces compatíveis: IDFA, GAID, AdCloud, Google, ECID, EMAIL_LC_SHA256. Observe que o Audience Manager e o Target resolvem as associações de público-alvo por meio da identidade da ECID; portanto, a ECID ainda é necessária para o compartilhamento do público-alvo final com o Adobe Target.

| Aplicativo/Serviço | Biblioteca necessária | Observações |
|---|---|---|
| Adobe Target | [!UICONTROL SDK da Web da Platform]*, at.js 0.9.1+ ou mbox.js 61+ | Preferência pela at.js, uma vez que a mbox.js não está mais sendo desenvolvida. |
| Adobe Audience Manager (opcional) | [!UICONTROL SDK da Web da Platform]* ou dil.js 5.0+ |  |
| Adobe Analytics (opcional) | [!UICONTROL SDK da Web da Platform]* ou AppMeasurement.js 1.6.4+ | O rastreamento do Adobe Analytics deve usar a Coleção de Dados Regionais (RDC). |
| Serviço da Experience Cloud ID | [!UICONTROL SDK da Web da Platform]* ou VisitorAPI.js 2.0+ | (Recomendado) Use o Experience Platform Launch para implantar o ID Service e assim garantir que a ID esteja configurada antes de qualquer chamada de aplicativo |
| SDK Móvel da Experience Platform (opcional) | Versão 4.11 ou posterior para iOS e Android™ |  |
| SDK da Web da Experience Platform | Versão 1.0. A versão atual do SDK da Experience Platform tem [vários casos de uso ainda não compatíveis com os aplicativos da Experience Cloud](https://github.com/adobe/alloy/projects/5) |  |




## Etapas de implementação


1. [Implemente o Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=pt-BR) para seus aplicativos da Web ou seus aplicativos para dispositivos móveis
1. [Implemente o Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=pt-BR) (opcional)
1. [Implemente o Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=pt-BR) (opcional)
1. [Implemente a Experience Platform e o [!UICONTROL Perfil de cliente em tempo real]](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html?lang=pt-BR)
1. Implemente o [Identity Service da Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html?lang=pt-BR) ou o [SDK da Web da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR)
1. [Habilitar o Adobe Target como destino no Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en) ou para a abordagem de compartilhamento de público [Solicitar provisionamento para o compartilhamento de público-alvo entre o Experience Platform e a Adobe Target (públicos compartilhados)](https://www.adobe.com/go/audiences) para compartilhar públicos do Experience Platform com o Target.
   >[!NOTE]
   >
   >Ao usar o serviço de Compartilhamento de público-alvo entre a RTCDP e o Adobe Target, os públicos-alvo deverão ser compartilhados usando a Experience Cloud ID e fazer parte da mesma organização da Experience Cloud. O suporte para identidades diferentes da ECID requer o uso do WebSDK e do Experience Edge Network.


## Documentação relacionada

* [Compartilhamento de segmentos da Experience Platform com o Audience Manager e outras soluções da Experience Cloud](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=pt-BR)
* [Visão geral da Segmentação da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=pt-BR)
* [Segmentação de transmissão](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=pt-BR)
* [Conexão Adobe Target para Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en)
* [Visão geral do Construtor de segmentos da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=pt-BR)
* [Conector de origem do Audience Manager](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=pt-BR)
* [Compartilhamento de segmentos do Adobe Analytics por meio do Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=pt-BR)
* [Documentação do SDK da Web da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Documentação do serviço da Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR)
* [Documentação de tags da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)

## Publicações do blog relacionadas

* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Build an Optimal Online Experience: Enrich Unified Profile with Query Service]](https://medium.com/adobetech/build-an-optimal-online-experience-enrich-unified-profile-with-query-service-8027c196ab33)
* [[!DNL Integrating Adobe Experience Platform Decisioning Engine with AEM Websites]](https://jaeness.medium.com/integrating-adobe-experience-platform-decisioning-engine-with-aem-websites-9c222acd12e2)
* [[!DNL Adobe Experience Platform’s Identity Service — How to Solve the Customer Identity Conundrum]](https://medium.com/adobetech/adobe-experience-platforms-identity-service-how-to-solve-the-customer-identity-conundrum-f95e22d16ea9)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our “Customer Zero” Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL How Adobe Experience Platform Can Help Customers Personalize Their Mobile Messaging in Real-Time with Journey Orchestration Service and a Mobile Messaging Vendor]](https://medium.com/adobetech/how-adobe-experience-platform-helped-a-client-personalize-their-mobile-messaging-in-real-time-with-7d634aefa098)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
* [[!DNL Build an Optimal Online Experience: Enrich Unified Profile with Query Service]](https://medium.com/adobetech/build-an-optimal-online-experience-enrich-unified-profile-with-query-service-8027c196ab33)
