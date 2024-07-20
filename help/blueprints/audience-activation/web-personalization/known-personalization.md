---
title: Visão geral da Web/Personalization móvel - Adobe Target e RTCDP
description: Sincronize a personalização da Web com emails e outras personalizações de canais conhecidos e anônimos.
landing-page-description: Sincronize a personalização da Web com emails e outras personalizações de canais conhecidos e anônimos.
short-description: Sincronize a personalização da Web com emails e outras personalizações de canais conhecidos e anônimos.
solution: Real-Time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection, Experience Platform
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: 845655a275cdb6d4a9cd397ec7c3515cbf02d321
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 79%

---


# Web/Personalization móvel com blueprint de dados de clientes conhecidos

## Casos de uso

* Personalização online com dados de clientes conhecidos
* Aprimoramento da página de aterrissagem
* Personalização com base em visualizações anteriores de produtos/conteúdos, afinidade com produtos/conteúdos, atributos ambientais e dados demográficos, além de dados offline, como transações, insights de fidelização e de CRM e modelos de insights
* Compartilhe e direcione públicos-alvo definidos na Real-time Customer Data Platform em sites e aplicativos móveis usando o Adobe Target.

## Aplicativos

* [!UICONTROL Real-time Customer Data Platform]
* Adobe Target
* Adobe Audience Manager (opcional): adiciona dados de público-alvo de terceiros
* Adobe Analytics ou Customer Journey Analytics (opcional): adiciona a capacidade de criar segmentos com base em dados históricos de clientes e dados comportamentais com segmentação detalhada

### Documentação de referência

* [Conexão do Adobe Target com a Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html)
* [Configuração da sequência de dados de borda](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=pt-BR)
* [Compartilhamento de segmentos da Experience Platform com o Audience Manager e outras soluções da Experience Cloud](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=pt-BR)


## Padrões de integração

| Padrão de integração | Recurso | Pré-requisitos |
|---|---|---|
| Avaliação de segmentos em tempo real na borda compartilhada da Real-time Customer Data Platform com o Target | <ul><li>Avalie públicos em tempo real personalização da mesma página ou próxima página no Edge.</li><li>Além disso, todos os segmentos avaliados em fluxo ou em lote também serão projetados para o [!DNL Edge Network] para serem incluídos na avaliação e personalização do segmento de borda.</li></ul> | <ul><li>O SDK da Web/Mobile deve ser implementado para a API do Servidor [!DNL Edge Network]</li><li>A sequência de dados precisa ser configurada no Experience Edge com a extensão Target e Experience Platform ativada.</li><li>O destino do Target precisa ser configurado nos Destinos da Real-time Customer Data Platform.</li><li>A integração com o Target requer uma organização IMS igual à da instância da Experience Platform.</li></ul> |
| Compartilhamento de públicos-alvo por streaming e em lote da Real-time Customer Data Platform com o Target por meio da abordagem de borda | <ul><li>Compartilhe públicos-alvo em lote e de transmissão do Real-time Customer Data Platform com o Target por meio do [!DNL Edge Network]. Os públicos avaliados em tempo real exigem o SDK da Web e a implementação do [!DNL Edge Network].</li></ul> | <ul><li>A implantação do Target usando o SDK da Web/Móvel ou a API do Edge não é necessária para compartilhar públicos-alvo da RTCDP por streaming e em lote com o Target, embora seja para habilitar a avaliação de segmentos de borda em tempo real.</li><li>Se estiver usando a AT.js, somente a integração de perfil em relação ao namespace de identidade ECID será permitida.</li><li>Para pesquisas de namespace de identidade personalizadas na borda, a implantação de API do SDK da Web/Edge é necessária, e cada identidade precisa ser definida como uma identidade no mapa de identidade.</li><li>O destino do Target precisa ser configurado nos Destinos da Real-time Customer Data Platform, somente a sandbox de produção padrão em RTCDP é compatível.</li><li>A integração com o Target requer uma organização IMS igual à da instância da Experience Platform.</li></ul> |
| Compartilhamento de públicos-alvo por streaming e em lote da Real-time Customer Data Platform com o Target e o Audience Manager por meio da abordagem do serviço de compartilhamento de público-alvo | <ul><li>Esse padrão de integração pode ser utilizado quando o enriquecimento adicional de dados de terceiros e públicos-alvo é desejado no Audience Manager.</li></ul> | <ul><li>O SDK da Web/Mobile não é necessário para compartilhar públicos-alvo por streaming e em lote com o Target, embora seja para habilitar a avaliação de segmentos de borda em tempo real.</li><li>Se estiver usando a AT.js, somente a integração de perfil em relação ao namespace de identidade ECID será permitida.</li><li>Para pesquisas de namespace de identidade personalizadas na borda, a implantação de API do SDK da Web/Edge é necessária, e cada identidade precisa ser definida como uma identidade no mapa de identidade.</li><li>A projeção de público-alvo por meio do serviço de compartilhamento de público-alvo precisa ser provisionada.</li><li>A integração com o Target requer uma organização IMS igual à da instância da Experience Platform.</li><li>Somente os públicos-alvo da sandbox de produção padrão oferecem suporte ao serviço principal de compartilhamento de público.</li></ul> |

## Compartilhamento de público-alvo em tempo real, por streaming e em lote com o Adobe Target

Arquitetura

<img src="assets/RTCDP+Target.svg" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

Detalhes da sequência

<img src="assets/RTCDP+Target_flow.svg" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

Visão geral da arquitetura

<img src="assets/personalization_with_apps.svg" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## Padrões de implantação

A personalização de cliente conhecido é permitida por várias abordagens de implantação.

### Padrão de implementação 1 - [!DNL Edge Network] com SDK da Web/móvel ou API [!DNL Edge Network] (abordagem recomendada)

* Usando o [!DNL Edge Network] com o SDK da Web/Mobile. A segmentação de borda em tempo real exige a abordagem de implantação do SDK da Web/Mobile ou da API de borda.
* [Consulte o Blueprint do SDK da Web e móvel do Experience Platform](../../experience-platform/deployment/websdk.md) para obter a implementação baseada em SDK.
* Para uso no SDK móvel, a [Adobe Journey Optimizer – Extensão de decisão](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer-decisioning) deve ser instalada no SDK móvel.
* [Consulte a [!DNL Edge Network] API do Servidor](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=pt-BR) para obter uma implementação baseada em API do Adobe Target com o Perfil do Edge.

### Padrão de implantação 2 – SDKs específicos ao aplicativo

Usar SDKs tradicionais específicos para aplicativos (por exemplo, AT.js e AppMeasurement.js). A avaliação de segmento de borda em tempo real não é compatível com essa abordagem de implantação. No entanto, o compartilhamento de público-alvo de lote e streaming do hub da Experience Platform são compatíveis com essa abordagem de implantação.

[Consulte a Documentação do Adobe Target Connector](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection)
[Consulte o Blueprint do SDK específico do aplicativo](../../experience-platform/deployment/appsdk.md)

## Considerações de implantação

Pré-requisitos de identidade

* Qualquer identidade primária pode ser utilizada ao utilizar o padrão de implementação 1 descrito acima com o [!DNL Edge Network] e o SDK da Web. A personalização do primeiro logon exige que a identidade principal do conjunto de solicitações de personalização corresponda à identidade principal do perfil no Real-time Customer Data Platform.

## Documentação relacionada

### Documentação do SDK

* [Documentação do SDK da Web da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR)
* [Documentação de tags da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)
* [Documentação do serviço da Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR)

### Documentação de segmentação

* [Visão geral da Segmentação da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=pt-BR)
* [Segmentação em tempo real](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=pt-BR)
* [Segmentação de transmissão](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=pt-BR)
* [Compartilhamento de segmentos do Adobe Analytics por meio do Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=pt-BR)
* [Configuração da política de mesclagem](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=pt-BR#create-a-merge-policy)

### Tutoriais

* [Personalização de próxima ocorrência com Real-Time CDP e Adobe Target](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=pt-BR)

### Publicações do blog relacionadas

* [Adobe anuncia a mesma personalização aprimorada de página com o Adobe Target e a Real-time Customer Data Platform](https://blog.adobe.com/en/publish/2021/10/05/adobe-announces-same-page-enhanced-personalization-with-adobe-target-real-time-customer-data-platform)
* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Adobe Experience Platform's Identity Service — How to Solve the Customer Identity Conundrum]](https://medium.com/adobetech/adobe-experience-platforms-identity-service-how-to-solve-the-customer-identity-conundrum-f95e22d16ea9)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our "Customer Zero" Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
