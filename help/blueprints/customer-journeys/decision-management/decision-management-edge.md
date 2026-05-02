---
title: Gestão de decisões no blueprint do Edge
description: Forneça ofertas personalizadas aos consumidores em todos os canais, incluindo em experiências da Web e móveis em tempo real.
solution: Experience Platform, Journey Optimizer
exl-id: 31e5f624-5578-49e1-ab92-5cabd596a632
TQID: https://experienceleague.adobe.com/SwjKOJIL5WidXtVuLCNbBpNz3mhe0EvD93IhMfxI1oY
product_v2: id: cb954087-f4fc-4456-afb9-e939cabcdc79id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914id: d998adac-2f81-400b-a669-d07bb196e4ebid: daec7ead-f475-492a-a3b3-02ae08565d6fid: df64005d-8f9a-422e-ba4d-c6f6dc3454b4id: fe338112-e2ce-4876-8989-fc4d497613f1
subfeature_v2: id: e5ae22e3-a3b0-46ed-804f-9abf1bbe3e74
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: c18d9e03-ac7d-4811-9c92-3e92ddc70adeid: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: 492
ht-degree: 67%

---

# Journey Optimizer - [!DNL Decision Management] no Blueprint do Edge

>[!TIP]
>Este blueprint também está disponível como um [padrão de caso de uso](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) no Personalization.

[!DNL Decision Management] é um serviço fornecido como parte de [!DNL Journey Optimizer]. Esse blueprint descreve os casos de uso e os recursos técnicos do aplicativo e fornece mais detalhes sobre os diferentes componentes da arquitetura e considerações que compõem a gestão de decisões.

>[!MORELIKETHIS]
>
>Para saber mais sobre [!DNL Decision Management], consulte a [visão geral do blueprint](decision-management-overview.md) ou visite a [documentação do produto](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=pt-BR).

[!DNL Decision Management] pode ser implantado de uma das duas formas. O primeiro é por meio do Hub [!DNL Experience Platform], que é uma arquitetura de data center única. Na abordagem de “hub”, as ofertas são executadas, personalizadas e entregues na latência de segundos. Por isso, a arquitetura de hub é mais adequada para uma experiência do cliente que não exige latência de subsegundo. Exemplos incluem definições de ofertas que são fornecidas para quiosques ou experiências assistidas por agentes, como em centrais de atendimento ou em interações pessoais.

A segunda abordagem é por meio da Experience Platform [!DNL Edge Network], que é uma infraestrutura distribuída globalmente e localizada geograficamente para atender às rápidas experiências de subsegundos e milissegundos. A experiência do consumidor final sendo executada pela infraestrutura do Edge mais próxima à localização geográfica dos consumidores para minimizar a latência. O [!DNL Decision Management] no Edge foi projetado para servir experiências do consumidor em tempo real. Isso inclui experiências como solicitações de personalização de entrada da Web ou móvel.

Esse blueprint abordará as especificidades da gestão de decisões na borda.

Para obter mais informações sobre a gestão de decisões no hub, consulte o blueprint [Gestão de decisões no hub](decision-management-hub.md).

## Casos de uso da gestão de decisões na borda

* Casos de uso de transmissão em que a latência de contexto do perfil é estritamente inferior a 15 minutos e a execução da gestão de decisões é por subsegundos.
* Personalização online por meio de experiências de entrada da Web ou móvel.
* Execução de jornada entre canais – consistência de ofertas na Web, dispositivos móveis, email e outros canais de interação por meio do Adobe Journey Optimizer.

## Arquitetura

<img src="images/offers_edge.svg" alt="Arquitetura de referência do blueprint da gestão de decisões na borda" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## Padrões de integração

| Integração | Descrição |
| :-- | :--- |
| [Gestão de decisões com o Adobe Target](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html?lang=pt-BR) | A gestão de decisões pode ser integrado ao Adobe Target, de modo que as ofertas possam ser testadas e entregues como experiências do Target. |

## Medidas de proteção

* Para as medidas de proteção do Journey Optimizer, consulte [Medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/limitations.html?lang=pt-BR).

* Para as medidas de proteção da gestão de decisões, consulte [Descrição do produto gestão de decisões](https://helpx.adobe.com/br/legal/product-descriptions/offer-decisioning-app-service.html).

[Medidas de proteção e orientação de latência completa](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/guardrails.html)

## Documentação relacionada

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=pt-BR)
* [Gestão de decisões do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=pt-BR)
* [Descrição do produto Adobe Journey Optimizer](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html)
* [Descrição do produto Adobe Decision Management](https://helpx.adobe.com/br/legal/product-descriptions/offer-decisioning-app-service.html)
