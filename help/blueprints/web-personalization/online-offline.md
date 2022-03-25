---
title: Personalização da Web/móvel com dados online e offline
description: Sincronize a personalização da Web com emails e outras personalizações de canais conhecidos e anônimos.
landing-page-description: Sincronize a personalização da Web com emails e outras personalizações de canais conhecidos e anônimos.
solution: Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7194thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: 17faffdd972f2485951ac1e870b578e9b1a011a5
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 100%

---


# Personalização da Web/móvel com dados online e offline

## Casos de uso

* Personalização com dados online e offline e perfis conhecidos
* Aprimoramento da página de aterrissagem
* Personalização com base em visualizações anteriores de produtos/conteúdos, afinidade com produtos/conteúdos, atributos ambientais e dados demográficos, além de dados offline, como transações, insights de fidelização e de CRM e modelos de insights
* Compartilhe e direcione públicos-alvo definidos na Real-time Customer Data Platform em sites e aplicativos móveis usando o Adobe Target.

## Aplicativos

* [!UICONTROL Real-time Customer Data Platform]
* Adobe Target
* Adobe Audience Manager (opcional): adiciona dados do público de terceiros, gráfico de dispositivos com base em co-op, capacidade de apresentar públicos da Real-time Customer Data Platform no Adobe Analytics e de apresentar públicos do Adobe Analytics na Real-time Customer Data Platform
* Adobe Analytics (opcional): adiciona a capacidade de criar segmentos com base em dados comportamentais históricos e criar segmentação detalhada a partir dos dados do Adobe Analytics

## Cenários de casos de uso

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
    <th class="tg-f7v4">Cenários de casos de uso</th>
    <th class="tg-y6fn">Recurso</th>
    <th class="tg-f7v4">Pré-requisitos</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0lax">1</td>
<td class="tg-73oq">Avaliação de segmentos em tempo real na borda compartilhada da Real-time Customer Data Platform com o Target</td>
    <td class="tg-0lax">- Avalie públicos em tempo real para a mesma ou próxima personalização de página no Edge.<br>- Além disso, quaisquer segmentos avaliados por streaming ou em lote também serão projetados para a rede de borda para serem incluídos na avaliação e personalização do segmento de borda.</td>
    <td class="tg-73oq">- Padrão de implementação 1 descrito abaixo.<br>- O SDK da Web/móvel deve ser implementado.<br>- Observe que o SDK móvel e o suporte baseado em API para segmentação em tempo real não estão disponíveis no momento<br>- A sequência de dados deve ser configurada no Experience Edge com a extensão do Target e da Experience Platform ativada; o ID da sequência de dados será fornecido na configuração de destino do Target.<br>- O destino do Target deve ser configurado nos Destinos da Real-time Customer Data Platform.<br>- A integração com o Target requer uma organização IMS igual à da instância da Experience Platform.</td> 
  </tr>
  <tr>
    <td class="tg-0lax">2</td>
    <td class="tg-73oq">Compartilhamento de públicos-alvo por streaming e em lote da Real-time Customer Data Platform com o Target por meio da abordagem de borda</td>
    <td class="tg-0lax">- Compartilhe públicos de transmissão e em lote da Real-time Customer Data Platform com o Target por meio do Edge Network. Os públicos avaliados em tempo real exigem o WebSDK e a avaliação de público em tempo real descrita no padrão de integração 1.<br>- Normalmente, essa integração é utilizada para compartilhar públicos-alvo por streaming e em lote usando SDKs tradicionais, em vez de migrar para o Edge Collection e o WebSDK, que possibilita públicos-alvo em tempo real, bem como públicos por streaming e em lote, conforme descrito no padrão de integração 1.</td>
    <td class="tg-73oq">- Padrão de implementação 1 ou 2 descrito abaixo.<br>- O SDK da Web/móvel não é necessário para compartilhar públicos-alvo por streaming e em lote com o Target, embora seja necessário para habilitar a avaliação de segmentos de borda em tempo real, conforme descrito no padrão de integração 1. <br>- Se estiver usando a AT.js, somente a integração de perfil em relação ao namespace de identidade ECID será suportada. <br>- Para pesquisas de namespace de identidade personalizadas no Edge, a implantação do WebSDK é necessária, e cada identidade deve ser definida como uma identidade no mapa de identidade.<br>- A sequência de dados deve ser configurada no Experience Edge, o ID da sequência de dados será fornecido na configuração de destino do Target.<br>- O destino do Target deve ser configurado nos Destinos da Real-time Customer Data Platform.<br>- A integração com o Target requer uma organização IMS igual à da instância da Experience Platform.</td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-73oq"><span style="font-weight:400;font-style:normal">Compartilhamento de públicos-alvo por streaming e em lote da Real-time Customer Data Platform com o Target e o Audience Manager por meio da abordagem do serviço de compartilhamento de público-alvo</span></td>
    <td class="tg-0lax"><span style="font-weight:400;font-style:normal">- Compartilhe públicos de transmissão e em lote da Real-time Customer Data Platform com o Target e o Audience Manager por meio do serviço de compartilhamento de público.<br>- Esse padrão de integração pode ser utilizado quando o enriquecimento adicional de dados de terceiros e públicos-alvo é desejado no Audience Manager. Caso contrário, são preferidos os padrões de integração 1 e 2. Os públicos avaliados em tempo real exigem o WebSDK e a avaliação de público em tempo real descrita no padrão de integração 1.</span></td>
    <td class="tg-73oq">- Padrão de implementação 1 ou 2 descrito abaixo.<br>- A implantação do SDK da Web/móvel não é necessária para essa integração.<br>- A projeção de público-alvo por meio do serviço de compartilhamento de público-alvo deve ser provisionada.<br>- A integração com o Target requer uma organização IMS igual à da instância da Experience Platform.<br>- Para que o Target prossiga, a identidade deve ser transferida para a ECID para que possa ser compartilhada com o Edge.</td>
  </tr>
</tbody>
</table>

## Cenários 1 e 2 - Compartilhamento de públicos-alvo em tempo real, por streaming e em lote com o Adobe Target

Arquitetura

<img src="assets/RTCDP+Target.png" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:80%; border:1px solid #4a4a4a" />

Detalhes da sequência

<img src="assets/RTCDP+Target_flow.png" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:80%; border:1px solid #4a4a4a" />

Arquitetura de visão geral para os cenários de casos de uso 1 e 2

<img src="assets/personalization_with_apps.png" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:80%; border:1px solid #4a4a4a"/>

### Etapas de implementação para o cenário de caso de uso 1, também compatível com o cenário de caso de uso 2

1. [Implemente o Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=pt-BR) para seus aplicativos da Web ou seus aplicativos para dispositivos móveis
1. [Implemente a Experience Platform e o [!UICONTROL Real-time Customer Profile]](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html?lang=pt-BR); certifique-se de que os públicos-alvo criados sejam ativados na borda, configurando a [política de mesclagem](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=pt-BR#create-a-merge-policy) como ativa na borda.
1. Implemente o [SDK da Web da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR). O SDK da Web da Experience Platform é necessário para a segmentação do Edge em tempo real, mas não é necessário para compartilhar públicos de transmissão e em lote da Real-time Customer Data Platform com o Target. Observe que o suporte para segmentação em tempo real por meio do SDK móvel e da API não está disponível no momento.
1. [Configure a rede de borda com uma sequência de dados de borda](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=pt-BR)
1. [Habilite o Adobe Target como um destino na Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=pt-BR)

<br>

## Cenário 3 - Compartilhamento de públicos-alvo por streaming e em lote por meio do serviço de compartilhamento de público-alvo com o Adobe Target e o Audience Manager

Arquitetura

<img src="assets/audience_share_architecture.png" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:80%; border:1px solid #4a4a4a" />

### Etapas de implementação do cenário 3, também compatível com o cenário 2

1. [Implemente o Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) para seus aplicativos da Web ou seus aplicativos para dispositivos móveis
1. [Implemente o Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=pt-BR) (opcional)
1. [Implemente o Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=pt-BR) (opcional)
1. [Implemente a Experience Platform e o [!UICONTROL Perfil de cliente em tempo real]](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html)
1. Implemente o [Identity Service da Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html?lang=pt-BR)
1. [Solicite o provisionamento do compartilhamento de público-alvo entre a Experience Platform e o Adobe Target (públicos-alvo compartilhados)](https://www.adobe.com/go/audiences) para compartilhar públicos-alvo da Experience Platform com o Target.
1. (Opcional) [Configure a rede de borda com uma sequência de dados de borda](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html) (Isso é necessário apenas para o padrão de integração 2, em que os públicos-alvo não precisam ser compartilhados com o Audience Manager ou enriquecidos com dados ou públicos-alvo do Audience Manager).
1. (Opcional) [Habilite o Adobe Target como um destino na Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en) para compartilhar públicos-alvo por streaming e em lote da Real-time Customer Data Platform diretamente com a borda, ou por meio do serviço de compartilhamento de público-alvo e o Audience Manager.

<br>

## Padrões de implementação

O suporte à personalização online e offline é oferecido por meio de várias abordagens de implementação.

### Padrão de implementação 1 - Oferece suporte aos cenários de casos de uso 1 e 2. Rede de borda com SDK da Web/móvel (Abordagem recomendada)

Usar a rede de borda com o SDK da Web/móvel
<img src="assets/web_sdk_flow.png" alt="Arquitetura de referência para abordagem do SDK específico para aplicativos" style="width:80%; border:1px solid #4a4a4a" />

Diagrama de sequência

<img src="assets/RTCDP+Target_sequence.png" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:80%; border:1px solid #4a4a4a" />

<br>

### Padrão de implementação 2 - Oferece suporte aos cenários de casos de uso 2 e 3. SDKs específicos do aplicativo

Usar SDKs tradicionais específicos para aplicativos (por exemplo, AT.js e AppMeasurement.js)
<img src="assets/app_sdk_flow.png" alt="Arquitetura de referência para abordagem do SDK específico para aplicativos" style="width:80%; border:1px solid #4a4a4a" />

<br>

## Medidas de proteção

[Consulte as medidas de proteção na página de Visão geral dos Blueprints de personalização móvel e da Web.](overview.md)

## Considerações de implementação

Pré-requisitos de identidade

* Qualquer identidade principal pode ser aproveitada quando se utiliza o padrão de implementação 1 descrito acima com a rede de borda e o WebSDK. A primeira personalização de logon requer que a identidade principal do conjunto de solicitações de personalização corresponda à identidade principal do perfil do Real-time Customer Data Platform. A associação de identidades de dispositivos anônimos a clientes conhecidos é processada no hub e, em uma etapa posterior, projetada para a borda.
* O compartilhamento de públicos-alvo da Adobe Experience Platform com o Adobe Target requer o uso da ECID como identidade quando se usa o serviço de compartilhamento de públicos-alvo, conforme descrito no cenário de caso de uso 3 acima.
* Identidades alternativas também podem ser usadas para compartilhar públicos-alvo da Experience Platform com o Adobe Target por meio do Audience Manager. A Experience Platform ativa públicos-alvo para o Audience Manager por meio dos seguintes namespaces compatíveis: IDFA, GAID, AdCloud, Google, ECID, EMAIL_LC_SHA256. Observe que o Audience Manager e o Target resolvem as associações de público-alvo por meio da identidade da ECID; portanto, a ECID ainda é necessária para o compartilhamento do público-alvo final com o Adobe Target.

## Documentação relacionada

### Documentação do SDK

* [Documentação do SDK da Web da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Documentação de tags da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)
* [Documentação do serviço da Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR)

### Documentação de conexão

* [Conexão do Adobe Target com a Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en)
* [Configuração da sequência de dados de borda](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)
* [Compartilhamento de segmentos da Experience Platform com o Audience Manager e outras soluções da Experience Cloud](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=pt-BR)

### Documentação de segmentação

* [Visão geral da Segmentação da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=pt-BR)
* [Segmentação em tempo real](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=pt-BR)
* [Segmentação de transmissão](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=pt-BR)
* [Compartilhamento de segmentos do Adobe Analytics por meio do Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=pt-BR)
* [Configuração da política de mesclagem](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=en#create-a-merge-policy)

### Tutoriais

* [Personalização de próxima ocorrência com Real-Time CDP e Adobe Target](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=pt-BR)

### Publicações do blog relacionadas

* [Adobe anuncia a mesma personalização aprimorada de página com o Adobe Target e a Real-time Customer Data Platform](https://blog.adobe.com/en/publish/2021/10/05/adobe-announces-same-page-enhanced-personalization-with-adobe-target-real-time-customer-data-platform)
* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Adobe Experience Platform’s Identity Service — How to Solve the Customer Identity Conundrum]](https://medium.com/adobetech/adobe-experience-platforms-identity-service-how-to-solve-the-customer-identity-conundrum-f95e22d16ea9)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our “Customer Zero” Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
