---
title: Real-time Customer Data Platform e Adobe Target
description: Integre perfis e públicos-alvo da RTCDP com o Adobe Target.
landing-page-description: Integre perfis e públicos-alvo da RTCDP com o Adobe Target.
short-description: Integre perfis e públicos-alvo da RTCDP com o Adobe Target.
solution: Real-Time Customer Data Platform, Target, Experience Platform
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: 32065a63e1febe0fe4fb76185c955cf124b81ca6
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 32%

---


# Integração da Real-time Customer Data Platform com a Adobe Target

## Casos de uso

* Personalização online com dados de clientes conhecidos
* Aprimoramento da página de aterrissagem
* Personalização com base em visualizações anteriores de produtos/conteúdos, afinidade com produtos/conteúdos, atributos ambientais e dados demográficos, além de dados offline, como transações, insights de fidelização e de CRM e modelos de insights
* Compartilhar e direcionar públicos-alvo definidos na Plataforma de dados do cliente em tempo real em sites e aplicativos móveis que usam o Adobe Target

## Aplicativos

* [!UICONTROL Real-time Customer Data Platform]
* Adobe Target

### Documentação de referência

* [Conexão do Adobe Target com a Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html)
* [Configuração da sequência de dados de borda](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=pt-BR)

## Padrões de integração

| Padrão de integração | Recurso | Pré-requisitos |
|--------------------|------------|---------------|
| **Avaliação de segmento em tempo real na Edge compartilhada da Plataforma de dados do cliente em tempo real para o Target** | - Avalie os públicos-alvo em tempo real para a mesma ou a próxima personalização de página na Edge. <br>- Quaisquer segmentos avaliados em fluxo ou em lote também serão projetados na Edge Network para serem incluídos na avaliação e personalização do segmento de borda. | - O Web/Mobile SDK deve ser implementado para a API do Edge Network Server. <br>- A sequência de dados deve ser configurada no Experience Edge com o Target e a extensão do Experience Platform habilitados. <br>- O destino deve ser configurado em Destinos da Real-time Customer Data Platform. <br>- A integração com o Target requer uma organização IMS igual à da instância da Experience Platform. |
| **Compartilhamento de streaming e público em lote da Real-time Customer Data Platform para o Target através da abordagem da Edge** | - Compartilhe públicos de transmissão e em lote da Real-time Customer Data Platform com o Target por meio do Edge Network. <br>- Os públicos avaliados em tempo real requerem a implementação do Web SDK e do Edge Network. | - A implementação da API do Target na Web/Mobile SDK ou Edge não é necessária para compartilhar públicos-alvo de transmissão e RTCDP em lote com o Target, mas é necessária para habilitar a avaliação de segmentos de borda em tempo real. <br>- Se estiver usando a AT.js, somente a integração de perfil em relação ao namespace de identidade ECID será suportada. <br>- Para pesquisas de namespace de identidade personalizada na Edge, a implantação da API Web SDK/Edge é necessária e cada identidade deve ser definida como uma identidade no mapa de identidade. <br>- O destino deve ser configurado em Destinos da Real-time Customer Data Platform, somente a sandbox de produção padrão no RTCDP é compatível. <br>- A integração com o Target requer uma organização IMS igual à da instância da Experience Platform. |
| **Compartilhamento de streaming e público em lote da Real-time Customer Data Platform para o Target e a Audience Manager através da Abordagem do Serviço de Compartilhamento de Público** | - Esse padrão de integração pode ser aproveitado quando o enriquecimento adicional de dados e públicos de terceiros no Audience Manager for desejado. | - O Web/Mobile SDK não é necessário para compartilhar streaming e públicos em lote com o Target, mas é necessário para habilitar a avaliação de segmentos de borda em tempo real. <br>- Se estiver usando a AT.js, somente a integração de perfil em relação ao namespace de identidade ECID será suportada. <br>- Para pesquisas de namespace de identidade personalizada na Edge, a implantação da API Web SDK/Edge é necessária e cada identidade deve ser definida como uma identidade no mapa de identidade. <br>- A projeção de público através do serviço de compartilhamento de público deve ser provisionada. <br>- A integração com o Target requer a mesma Organização IMS que a instância do Experience Platform. <br>- Somente os públicos-alvo da sandbox de produção padrão dão suporte ao serviço principal de compartilhamento de público-alvo. |

## Compartilhamento de público-alvo em tempo real, por streaming e em lote com o Adobe Target

Arquitetura

<img src="assets/RTCDP+Target.svg" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

Detalhes da sequência

<img src="assets/RTCDP+Target_flow.svg" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

Visão geral da arquitetura

<img src="assets/personalization_with_apps.svg" alt="Arquitetura de referência para o Blueprint de personalização online/offline da Web" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## Padrões de implantação

A personalização de cliente conhecido é permitida por várias abordagens de implantação.

### Padrão de implementação 1 - [!DNL Edge Network] com Web/Mobile SDK ou API [!DNL Edge Network] (Abordagem recomendada)

* Usando o [!DNL Edge Network] com a Web/Mobile SDK. A segmentação de borda em tempo real exige a abordagem de implantação do SDK da Web/Mobile ou da API de borda.
* [Consulte o Blueprint da Web e do SDK Móvel da Experience Platform](../experience-platform/deployment/websdk.md) para a implementação baseada no SDK.
* Para uso no Mobile SDK, a [Adobe Journey Optimizer - Extensão de decisão](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/) deve estar instalada.
* [Consulte a [!DNL Edge Network] API do Servidor](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=pt-BR) para obter uma implementação baseada em API do Adobe Target com o Perfil do Edge.

### Padrão de implantação 2 – SDKs específicos ao aplicativo

Usar SDKs tradicionais específicos para aplicativos (por exemplo, AT.js e AppMeasurement.js). A avaliação de segmento de borda em tempo real não é compatível com essa abordagem de implantação. No entanto, o compartilhamento de público-alvo de lote e streaming do hub da Experience Platform são compatíveis com essa abordagem de implantação.

[Consulte a Documentação do Adobe Target Connector](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection)
[Consulte o SDK Blueprint específico do aplicativo](../experience-platform/deployment/appsdk.md)

## Considerações de implantação

* Qualquer identidade primária pode ser utilizada ao utilizar o padrão de implementação 1 descrito acima com o [!DNL Edge Network] e o Web SDK.
* A primeira personalização de logon com dados conhecidos do cliente que foi assimilada anteriormente na RTCDP exige que a solicitação de personalização tenha uma identidade principal que corresponda ao gráfico de identidade conhecida do cliente na Real-time Customer Data Platform. Se a ID primária for definida como ECID ou uma identidade que ainda não foi compilada com o perfil de cliente conhecido, levará vários minutos para que a compilação de identidade seja realizada na borda e para que a personalização da borda inclua dados anteriores do cliente conhecidos assimilados.
* Os perfis do Edge atualmente têm um TTL de 14 dias. Portanto, se um usuário não tiver feito logon ou estado ativo por 14 dias na borda, o perfil na borda pode estar expirado e, portanto, a borda deve buscar o perfil no hub para ter a visualização do perfil histórico para permitir a personalização, que inclui atributos e segmentos de perfil assimilados anteriormente, isso resultará na personalização com a visualização do histórico de perfis que acontecem em visualizações de página subsequentes em vez do primeiro logon.

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
