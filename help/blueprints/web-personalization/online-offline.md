---
title: Personalização da Web/móvel com dados online e offline
description: Sincronize a personalização da Web com emails e outras personalizações de canais conhecidos e anônimos.
landing-page-description: Sincronize a personalização da Web com emails e outras personalizações de canais conhecidos e anônimos.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7194thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: 4d02197b437c167a90cbadf16b0b19fc733a9f65
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 50%

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
<td class="tg-73oq">Avaliação de segmento em tempo real no Edge compartilhado do Real-time Customer Data Platform para o Target</td>
    <td class="tg-0lax">– Avalie os públicos-alvo em tempo real para a mesma ou próxima personalização de página no Edge.<br>- Além disso, quaisquer segmentos avaliados em streaming ou lote também serão projetados para a Rede de borda para serem incluídos na avaliação e personalização do segmento de borda.</td>
    <td class="tg-73oq">- O conjunto de dados deve ser configurado no Experience Edge com a extensão do Target e do Experience Platform ativada, o ID do conjunto de dados será fornecido na configuração de destino do Target.<br>- O destino do Target deve ser configurado em Destinos do Real-time Customer Data Platform.<br>– A integração com o Target requer uma organização IMS igual a da instância da Experience Platform.<br>– O WebSDK deve ser implementado.<br>- A implementação com base em API e SDK móvel não está disponível no momento</td> 
  </tr>
  <tr>
    <td class="tg-0lax">2</td>
    <td class="tg-73oq">Streaming e compartilhamento em lote do público-alvo no Real-time Customer Data Platform para o Target por meio da abordagem do Edge</td>
    <td class="tg-0lax">- Compartilhe públicos-alvo de fluxo e lote do Real-time Customer Data Platform para o Target por meio da Edge Network. Os públicos-alvo avaliados em tempo real exigem o WebSDK e a avaliação de público-alvo em tempo real descrita no padrão de integração 1.<br>- Normalmente, essa integração é aproveitada para compartilhar públicos de streaming e lote usando SDKs tradicionais, em vez de migrar para o Edge Collection e o WebSDK, que alimenta públicos em tempo real, bem como públicos de streaming e lote, conforme descrito no padrão de integração 1.</td>
    <td class="tg-73oq">- O conjunto de dados deve ser configurado no Experience Edge, a ID do conjunto de dados será fornecida na configuração de destino do Target.<br>- O destino do Target deve ser configurado em Destinos do Real-time Customer Data Platform.<br>– A integração com o Target requer uma organização IMS igual a da instância da Experience Platform.<br>- O WebSDK não é necessário para compartilhar públicos de streaming e lote no Target, embora seja necessário para habilitar a avaliação de segmentos de borda em tempo real, conforme descrito no padrão de integração 1. <br>- Se estiver usando a AT.js, somente a integração de perfil com o namespace de identidade da ECID será compatível. <br>- Para pesquisas de namespace de identidade personalizadas no Edge, a implantação do WebSDK é necessária e cada identidade deve ser definida como uma identidade no mapa de identidade.</td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-73oq"><span style="font-weight:400;font-style:normal">Transmissão e compartilhamento em lote do público-alvo do Real-time Customer Data Platform para o Target e Audience Manager por meio da abordagem do serviço de compartilhamento de público-alvo</span></td>
    <td class="tg-0lax"><span style="font-weight:400;font-style:normal">- Compartilhe públicos-alvo de streaming e lote do Real-time Customer Data Platform para o Target e o Audience Manager por meio do serviço de Compartilhamento de público-alvo.<br> -Esse padrão de integração pode ser aproveitado quando o enriquecimento adicional de dados de terceiros e públicos-alvo no Audience Manager é desejado. Caso contrário, são preferidos os padrões de integração 1 e 2. Os públicos-alvo avaliados em tempo real exigem o WebSDK e a avaliação de público-alvo em tempo real descrita no padrão de integração 1.</span></td>
    <td class="tg-73oq">– A projeção de público-alvo por meio do serviço de compartilhamento de público-alvo deve ser provisionada.<br>– A integração com o Target requer uma organização IMS igual a da instância da Experience Platform.<br>– Para que o Target prossiga, a identidade deve ser transferida para a ECID para que possa ser compartilhada com o Edge.<br>- A implantação do WebSDK não é necessária para essa integração.</td>
  </tr>
</tbody>
</table>


## Arquitetura do padrão de integração 1


Arquitetura detalhada do padrão de integração 1

<img src="assets/RTCDP+Target.png" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:80%; border:1px solid #4a4a4a" />

Diagrama de sequência do padrão de integração 1

<img src="assets/RTCDP+Target_flow.png" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:80%; border:1px solid #4a4a4a" />

<br>

<img src="assets/RTCDP+Target_sequence.png" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:80%; border:1px solid #4a4a4a" />

Arquitetura de visão geral para o padrão de integração 1

<img src="assets/personalization_with_apps.png" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:80%; border:1px solid #4a4a4a"/>


## Implementação do padrão de integração 1

Para segmentação em tempo real no Edge [!UICONTROL SDK da Web da plataforma] e [!UICONTROL Rede Edge] devem ser implementadas. [Consulte o blueprint do SDK da Web e móvel da Experience Platform](../data-ingestion/websdk.md)

### Etapas de implementação do Padrão de integração 1

1. [Implemente o Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=pt-BR) para seus aplicativos da Web ou seus aplicativos para dispositivos móveis
1. [Implemente a Experience Platform e o [!UICONTROL Perfil de cliente em tempo real]](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html?lang=pt-BR)
1. Implementar [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR). O SDK da Web do Experience Platform é necessário para a segmentação de Edge em tempo real, mas não é necessário para compartilhar públicos de streaming e lote do Real-time Customer Data Platform com o Target. Observe que o suporte para segmentação em tempo real por meio do SDK móvel e da API não está disponível no momento.
1. [Configure a rede de borda com um armazenamento de dados de borda](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)
1. [Habilitar o Adobe Target como destino no Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=pt-BR)

## Implementação do padrão de integração 2 e 3

Uso de SDKs tradicionais específicos do aplicativo (por exemplo, AT.js e AppMeasurement.js)
<img src="assets/app_sdk_flow.png" alt="Arquitetura de referência para abordagem do SDK específico para aplicativos" style="width:80%; border:1px solid #4a4a4a" />

### Etapas de implementação para o Padrão de integração 2 e 3

1. [Implemente o Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) para seus aplicativos da Web ou seus aplicativos para dispositivos móveis
1. [Implemente o Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=pt-BR) (opcional)
1. [Implemente o Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=pt-BR) (opcional)
1. [Implemente a Experience Platform e o [!UICONTROL Perfil de cliente em tempo real]](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html)
1. Implementar [Serviço de identidade do Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html?lang=pt-BR)
1. [Solicitar provisionamento para o compartilhamento de público-alvo entre o Experience Platform e a Adobe Target (públicos compartilhados)](https://www.adobe.com/go/audiences) para compartilhar públicos do Experience Platform com o Target.
1. (Opcional) [Configure a rede de borda com um armazenamento de dados de borda](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html) (Isso é necessário apenas para o padrão de integração 2, em que os públicos-alvo não precisam ser compartilhados com o Audience Manager ou enriquecidos por Audience Manager audiences ou dados).
1. (Opcional) [Habilitar o Adobe Target como destino no Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en) para compartilhar públicos-alvo de streaming e lote do Real-time Customer Data Platform diretamente no Edge, por meio do serviço de compartilhamento de público-alvo e do Audience Manager.

## Medidas de proteção

[Consulte as medidas de proteção na página de Visão geral dos Blueprints de personalização móvel e da Web.](overview.md)

## Considerações de implementação

Pré-requisitos de identidade

* Qualquer identidade primária pode ser aproveitada ao utilizar o padrão de integração 1 descrito acima com a rede Edge e o WebSDK. A primeira personalização de logon requer que o conjunto de solicitações de personalização corresponda à identidade primária do perfil do Real-time Customer Data Platform. A identificação entre dispositivos anônimos e clientes conhecidos é processada no hub e subsequentemente projetada para a borda. Portanto, se a identidade primária for definida como o identificador do dispositivo, os dados conhecidos do cliente não serão aplicados até as sessões subsequentes, onde os perfis anônimos e conhecidos foram unificados.
* O compartilhamento de públicos do Adobe Experience Platform para a Adobe Target requer o uso da ECID como uma identidade ao usar o serviço de compartilhamento de público, conforme descrito no padrão de integração 3 acima.
* Identidades alternativas também podem ser usadas para compartilhar públicos-alvo da Experience Platform com o Adobe Target por meio do Audience Manager. A Experience Platform ativa públicos-alvo para o Audience Manager por meio dos seguintes namespaces compatíveis: IDFA, GAID, AdCloud, Google, ECID, EMAIL_LC_SHA256. Observe que o Audience Manager e o Target resolvem as associações de público-alvo por meio da identidade da ECID; portanto, a ECID ainda é necessária para o compartilhamento do público-alvo final com o Adobe Target.

## Documentação relacionada

### Documentação

* [Conexão do Adobe Target com a Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en)
* [Compartilhamento de segmentos da Experience Platform com o Audience Manager e outras soluções da Experience Cloud](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=pt-BR)
* [Documentação do SDK da Web da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Documentação do serviço da Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR)
* [Visão geral da Segmentação da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=pt-BR)
* [Segmentação em tempo real](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html)
* [Segmentação de transmissão](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=pt-BR)
* [Visão geral do Construtor de segmentos da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html)
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
