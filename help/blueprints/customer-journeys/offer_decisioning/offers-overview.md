---
title: Visão geral do Offer Decisioning
description: Forneça ofertas personalizadas nas jornadas do cliente.
solution: Experience Platform, Journey Optimizer
exl-id: f6271802-faab-4ffc-92d6-4c4d7d423ed4
source-git-commit: 8842b8637a30151577a93653c16b4d37e2cf7c27
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 2%

---

# Journey Optimizer - Visão geral do Offer Decisioning

Para saber mais sobre o Gerenciamento de decisões, consulte a documentação do produto [AQUI](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)

O Gerenciamento de decisão do Adobe é um serviço fornecido como parte da Adobe Journey Optimizer. Este blueprint descreve os casos de uso e os recursos técnicos do aplicativo e fornece um mergulho profundo nos vários componentes da arquitetura e considerações que compõem o Offer Decisioning.

O Journey Optimizer é usado para oferecer a melhor oferta e experiência aos clientes em todos os pontos de contato na hora certa. O Offer Decisioning facilita a personalização com uma biblioteca central de ofertas de marketing e um mecanismo de decisão que aplica regras e restrições a perfis ricos em tempo real criados pela Adobe Experience Platform para ajudar você a enviar aos clientes a oferta certa na hora certa.

A capacidade de gerenciamento de decisões consiste em dois componentes principais:

* A Biblioteca de ofertas centralizada, que é a interface onde você cria e gerencia os diferentes elementos que compõem suas ofertas, e define suas regras e restrições.
* O mecanismo de decisão da oferta que aproveita os dados do Adobe Experience Platform e os perfis do cliente em tempo real, juntamente com a Biblioteca de ofertas, para selecionar o momento certo, os clientes e canais para os quais as ofertas serão entregues.

<img src="../assets/offers_overview.png" alt="Offer Decisioning" style="width:100%; border:1px solid #4a4a4a" />

O Gerenciamento de decisões pode ser implantado de uma das duas formas, na borda ou por meio do hub. Cada um desses métodos tem um conjunto específico de interfaces e protocolos para operação do serviço, conforme descrito nos respectivos blueprints referenciados abaixo. Podem igualmente ser obtidas informações adicionais na documentação de gestão das decisões [AQUI](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery-api/decisioning-vs-edge-apis.html).

## Gerenciamento de decisões no hub

A primeira é através do hub Adobe Experience Platform, que é uma arquitetura central de data center. Na abordagem &quot;hub&quot;, as ofertas são executadas, personalizadas e entregues em latência de mais de 500 ms. Assim, a arquitetura do hub é mais adequada para experiências do cliente que não exigem latência de sub-segundo, os exemplos incluem decisões de oferta que são fornecidas para quiosques ou experiências assistidas por agentes, como em centrais de atendimento ou em interações pessoais. As ofertas inseridas em emails, mensagens SMS ou notificações por push e outras campanhas de saída também são acionadas pela abordagem de hub. Para saber mais sobre o Gerenciamento de decisões no hub, consulte [Gerenciamento de decisões no hub](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-hub.html?lang=en) blueprint.

### Casos de uso do gerenciamento de decisões no hub

* Ofertas personalizadas em quiosques e em experiências de loja.
* Ofertas personalizadas por meio de experiência assistida por agente, como centrais de atendimento ou interações de vendas.
* Ofertas incluídas em email, SMS ou outras interações de saída.
* Execução de jornada entre canais - consistência de ofertas na Web, dispositivos móveis, email e outros canais de interação por meio do Adobe Journey Optimizer.

## Gerenciamento de decisões na borda

A segunda abordagem é por meio da Experience Edge Network, que é uma infraestrutura distribuída geograficamente globalmente para fornecer experiências rápidas de sub-segundo e milissegundo. A experiência do consumidor final que está sendo executada pela infraestrutura de borda mais próxima da localização geográfica dos consumidores para minimizar a latência. O Gerenciamento de decisões no Edge foi projetado para fornecer experiências do consumidor em tempo real, como solicitações de personalização de entrada da Web ou móvel. Para saber mais sobre o Gerenciamento de decisões no Edge, consulte [Gerenciamento de decisões na borda](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-edge.html?lang=en) blueprint.

### Casos de uso do gerenciamento de decisões na borda

* Personalização online por meio de experiências de entrada da Web ou móvel.
* Execução de jornada entre canais - consistência de ofertas na Web, dispositivos móveis, email e outros canais de interação por meio do Adobe Journey Optimizer.

## Documentação relacionada

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html)
* [Gerenciamento de decisões da Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)
* [Descrição do produto Adobe Journey Optimizer](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html)
* [Descrição do produto Offer decisioning Adobe](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html)
