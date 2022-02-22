---
title: Personalização da Web/móvel com dados online e offline
description: Sincronize a personalização da Web com emails e outras personalizações de canais conhecidos e anônimos.
landing-page-description: Sincronize a personalização da Web com emails e outras personalizações de canais conhecidos e anônimos.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7194thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: 91db73c9fb14d461ee62444199c3d053bd094639
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 70%

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
* Adobe Audience Manager (opcional): Adiciona dados de público-alvo de terceiros, gráfico de dispositivos baseado em cooperação, a capacidade de exibir públicos-alvo da Real-time Customer Data Platform no Adobe Analytics e a capacidade de exibir públicos-alvo da Adobe Analytics no Real-time Customer Data Platform
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
<td class="tg-73oq">Avaliação de segmento em tempo real do Real-time Customer Data Platform no Edge compartilhada com o Target</td>
    <td class="tg-0lax">– Avalie os públicos-alvo em tempo real para a mesma ou próxima personalização de página no Edge.</td>
    <td class="tg-73oq">- O destino do Target deve ser configurado em Destinos do Real-time Customer Data Platform.<br>– A integração com o Target requer uma organização IMS igual a da instância da Experience Platform.<br>– O WebSDK deve ser implementado.<br>- A implementação com base em API e SDK móvel não está disponível no momento</td> 
  </tr>
  <tr>
    <td class="tg-0lax">2</td>
    <td class="tg-73oq">Transmissão em lote e compartilhamento de público-alvo do Real-time Customer Data Platform para o Target por meio da abordagem do Edge</td>
    <td class="tg-0lax">- Compartilhe públicos-alvo de fluxo e lote do Real-time Customer Data Platform para o Target por meio da Edge Network. Os públicos-alvo avaliados em tempo real exigem o WebSDK e a avaliação de público-alvo em tempo real descrita no padrão de integração 1.</td>
    <td class="tg-73oq">- O destino do Target deve ser configurado em Destinos do Real-time Customer Data Platform.<br>– A integração com o Target requer uma organização IMS igual a da instância da Experience Platform.<br>WebSDK não é necessário. <br>– Se estiver usando a AT.js, somente a pesquisa de perfil em relação à ECID será suportada. <br>- Para pesquisas de namespace de identidade personalizadas no Edge, a implantação do WebSDK é necessária e cada identidade deve ser definida como uma identidade no mapa de identidade.</td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-73oq"><span style="font-weight:400;font-style:normal">Streaming do Real-time Customer Data Platform e compartilhamento em lote de público-alvo para o Target e o Audience Manager por meio da abordagem do serviço de compartilhamento de público-alvo</span></td>
    <td class="tg-0lax"><span style="font-weight:400;font-style:normal">- Compartilhe públicos-alvo de streaming e lote do Real-time Customer Data Platform para o Target e o Audience Manager por meio do serviço de Compartilhamento de público-alvo. Os públicos-alvo avaliados em tempo real exigem o WebSDK e a avaliação de público-alvo em tempo real descrita no padrão de integração 1.</span></td>
    <td class="tg-73oq">– A projeção de público-alvo por meio do serviço de compartilhamento de público-alvo deve ser provisionada.<br>– A integração com o Target requer uma organização IMS igual a da instância da Experience Platform.<br>– Para que o Target prossiga, a identidade deve ser transferida para a ECID para que possa ser compartilhada com o Edge.<br>- A implantação do WebSDK não é necessária para essa integração.</td>
  </tr>
</tbody>
</table>


## Arquitetura

Arquitetura detalhada

<img src="assets/RTCDP+Target.png" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:80%; border:1px solid #4a4a4a" />

Diagrama de sequência

<img src="assets/RTCDP+Target_flow.png" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:80%; border:1px solid #4a4a4a" />

<br>

<img src="assets/RTCDP+Target_sequence.png" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:80%; border:1px solid #4a4a4a" />


Visão geral da arquitetura

<img src="assets/personalization_with_apps.png" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:80%; border:1px solid #4a4a4a"/>

## Medidas de proteção

[Consulte as medidas de proteção na página de Visão geral dos Blueprints de personalização móvel e da Web.](overview.md)

## Padrões de implementação

O blueprint de personalização da Web/móvel pode ser implementado por meio das seguintes abordagens, conforme descrito abaixo.

1. Usando o [!UICONTROL SDK da Web da Platform] ou o [!UICONTROL SDK móvel da Platform] e o [!UICONTROL Edge Network]. [Consulte o blueprint do SDK da Web e móvel da Experience Platform](../data-ingestion/websdk.md)
1. Usando SDKs tradicionais específicos para aplicativos (por exemplo, AppMeasurement.js)
<img src="assets/app_sdk_flow.png" alt="Arquitetura de referência para abordagem do SDK específico para aplicativos" style="width:80%; border:1px solid #4a4a4a" />

## Considerações de implementação

Pré-requisitos de identidade

* Qualquer identidade primária pode ser aproveitada ao utilizar o padrão de integração 1 descrito acima com a rede Edge e o WebSDK. A primeira personalização de logon requer que o conjunto de solicitações de personalização corresponda à identidade primária do perfil do Real-time Customer Data Platform. A identificação entre dispositivos anônimos e clientes conhecidos é processada no hub e subsequentemente projetada para a borda. Portanto, se a identidade primária for definida como o identificador do dispositivo, os dados conhecidos do cliente não serão aplicados até as sessões subsequentes, onde os perfis anônimos e conhecidos foram unificados.
* O compartilhamento de públicos do Adobe Experience Platform para a Adobe Target requer o uso da ECID como uma identidade ao usar o serviço de compartilhamento de público, conforme descrito no padrão de integração 3 acima.
* Identidades alternativas também podem ser usadas para compartilhar públicos-alvo da Experience Platform com o Adobe Target por meio do Audience Manager. A Experience Platform ativa públicos-alvo para o Audience Manager por meio dos seguintes namespaces compatíveis: IDFA, GAID, AdCloud, Google, ECID, EMAIL_LC_SHA256. Observe que o Audience Manager e o Target resolvem as associações de público-alvo por meio da identidade da ECID; portanto, a ECID ainda é necessária para o compartilhamento do público-alvo final com o Adobe Target.

## Etapas de implementação

1. [Implemente o Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=pt-BR) para seus aplicativos da Web ou seus aplicativos para dispositivos móveis
1. [Implemente o Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=pt-BR) (opcional)
1. [Implemente o Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=pt-BR) (opcional)
1. [Implemente a Experience Platform e o [!UICONTROL Perfil de cliente em tempo real]](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html?lang=pt-BR)
1. Implemente o [Identity Service da Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html?lang=pt-BR) ou o [SDK da Web da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR) . O SDK da Web do Experience Platform é necessário para a segmentação de Edge em tempo real, mas não é necessário para compartilhar públicos de streaming e lote do Real-time Customer Data Platform com o Target. Observe que o suporte para segmentação em tempo real por meio do SDK móvel e da API não está disponível no momento.
1. [Habilitar o Adobe Target como destino na Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=pt-BR) ou, para a abordagem de compartilhamento de público-alvo, [Solicitar provisionamento para o compartilhamento de público-alvo entre a Experience Platform e o Adobe Target (públicos-alvo compartilhados)](https://www.adobe.com/go/audiences) para compartilhar públicos-alvo da Experience Platform com o Target.

## Documentação relacionada

### Documentação

* [Conexão do Adobe Target com a Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en)
* [Compartilhamento de segmentos da Experience Platform com o Audience Manager e outras soluções da Experience Cloud](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=pt-BR)
* [Documentação do SDK da Web da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Documentação do serviço da Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR)
* [Visão geral da Segmentação da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=pt-BR)
* [Segmentação de transmissão](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=pt-BR)
* [Visão geral do Construtor de segmentos da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=pt-BR)
* [Conector de origem do Audience Manager](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=pt-BR)
* [Compartilhamento de segmentos do Adobe Analytics por meio do Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=pt-BR)
* [Documentação de tags da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)

### Tutoriais

* [Personalização de próxima ocorrência com Real-Time CDP e Adobe Target](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=pt-BR)

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
