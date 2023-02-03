---
title: Blueprint de ativação de público-alvo anônima
description: Saiba como segmentar públicos-alvos na Web e em todos os canais de anúncios com base em dados comportamentais e anônimos de clientes. Essa funcionalidade possibilita experiências do cliente consistentes e personalizadas em tempo real em todos os dispositivos.
landing-page-description: Saiba como segmentar públicos-alvos na Web e em todos os canais de anúncios com base em dados comportamentais e anônimos de clientes.
solution: Audience Manager
kt: 7211
thumbnail: null
exl-id: f17599f1-2e75-4cbe-841a-9fd1dae71ada
source-git-commit: 8355a36a235d847a6faf2398f3fadbed28ccac37
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 68%

---

# Blueprint de ativação de público-alvo anônima

A ativação de público-alvo anônimo é a capacidade de direcionar e personalizar públicos-alvo em canais da Web, mobile e de publicidade com base em dados comportamentais e de dispositivos anônimos.

## Casos de uso

* Execute o direcionamento e a personalização de público-alvo digital anônimo no site, no aplicativo móvel ou nos canais de publicidade compatíveis.
* Otimize a landing page e as experiências antes da autenticação com base em características conhecidas do dispositivo e do comportamento.
* Aproveite a rede de dados de terceiros do Audience Manager para melhorar e expandir seus públicos-alvo para direcionamento.


## Aplicativos

* Audience Manager
* Real-time Customer Data Platform

O Audience Manager e o Real-time Customer Data Platform podem ser aproveitados para alimentar o Audience Activation anônimo para destinos no site e de anúncios. Observe que o Real-time Customer Data Platform suporta apenas um subconjunto de destinos de publicidade com identificadores de dispositivo anônimos, como catalogado na variável [documentação de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/overview.html?lang=pt-BR).

O Microsoft Bing, Google DV360 e TradeDesk são os principais destinos de publicidade da Real-time Customer Data Platform com suporte para definição de metas anônima com base em dispositivos. Além disso, a Real-time Customer Data Platform oferece suporte a vários destinos conhecidos baseados no cliente, como catalogados na [documentação de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/overview.html?lang=pt-BR) e conforme descrito no [Blueprint de Ativação do Cliente Conhecido](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=pt-BR).

## Arquitetura

<img src="assets/anonymous_activation.svg" alt="Arquitetura de referência para o blueprint de ativação de público-alvo anônima" style="width:90%; border:1px solid #4a4a4a" />

<br>

## Etapas para a implementação do Audience Manager

* Para obter detalhes sobre a implementação do Audience Manager, consulte a seguinte [documentação](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=pt-BR).

## Etapas de implementação do Real-time Customer Data Platform

* Para obter as etapas de implementação do Real-time Customer Data Platform, consulte o seguinte [documentação](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=pt-BR).

## Documentação relacionada

* [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager.html?lang=pt-BR)
* [[!UICONTROL Públicos] da Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html?lang=pt-BR)
* [Integração do Audience Manager com o Target](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html?lang=pt-BR)
* [Compartilhamento de segmentos do Adobe Analytics por meio do Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=pt-BR)
* [Blueprint de ativação de cliente conhecido](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=pt-BR).
* [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=pt-BR)
