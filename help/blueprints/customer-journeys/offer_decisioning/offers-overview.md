---
title: Visão geral do Offer Decisioning
description: Forneça ofertas personalizadas nas jornadas do cliente.
solution: Experience Platform, Journey Optimizer
exl-id: f6271802-faab-4ffc-92d6-4c4d7d423ed4
source-git-commit: 7dcbf86b362350312a86445bbe7a020f5ccd1752
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 48%

---

# Journey Optimizer - Visão geral do Offer Decisioning

Para saber mais sobre gestão de decisões, consulte a documentação do produto [AQUI](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=pt-BR).

A gestão de decisões da Adobe é um serviço fornecido como parte do Adobe Journey Optimizer. Esse blueprint descreve os casos de uso e os recursos técnicos do aplicativo e fornece mais detalhes sobre os diferentes componentes da arquitetura e considerações que compõem o Offer Decisioning.

O Journey Optimizer é usado para oferecer a melhor oferta e experiência aos clientes em todos os pontos de contato na hora certa. O Offer Decisioning facilita a personalização com uma biblioteca central de ofertas de marketing e um mecanismo de decisão que aplica regras e restrições a perfis ricos em tempo real criados pela Adobe Experience Platform para ajudar você a enviar aos clientes a oferta certa na hora certa.

A capacidade de gerenciamento de decisões consiste em dois componentes principais:

* A Biblioteca de ofertas centralizada, que é a interface onde você cria e gerencia os diferentes elementos que compõem suas ofertas, e define suas regras e restrições.
* O mecanismo de decisão da oferta que aproveita os dados do Adobe Experience Platform e os perfis do cliente em tempo real, juntamente com a Biblioteca de ofertas, para selecionar o momento certo, os clientes e canais para os quais as ofertas serão entregues.

<img src="../assets/offers_overview.png" alt="Offer Decisioning" style="width:100%; border:1px solid #4a4a4a" />

O Gerenciamento de decisões pode ser implantado de uma das duas formas, na borda ou por meio do hub. Cada um desses métodos tem um conjunto específico de interfaces e protocolos para operação do serviço, conforme descrito nos respectivos blueprints referenciados abaixo. Podem igualmente ser obtidas informações adicionais na documentação de gestão das decisões [AQUI](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery-api/decisioning-vs-edge-apis.html).

## Gerenciamento de decisões no hub

A primeira é por meio do hub da Adobe Experience Platform, que é uma arquitetura de datacenter centralizada. Na abordagem de “hub”, as ofertas são executadas, personalizadas e entregues na latência de >500 milissegundos. Por isso, a arquitetura de hub é mais adequada para experiências do cliente que não exigem latência de subsegundo. Exemplos incluem definições de ofertas que são fornecidas para quiosques ou experiências assistidas por agentes, como em centrais de atendimento ou em interações pessoais. As ofertas inseridas em emails, mensagens SMS ou notificações por push e outras campanhas de saída também são acionadas pela abordagem de hub. Para obter mais informações sobre a gestão de decisões no hub, consulte o blueprint [Gestão de decisões no hub](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-hub.html?lang=pt-BR).

* A qualificação de oferta pode operar em relação ao perfil completo do cliente em tempo real, incluindo todos os atributos e eventos de experiência

### Casos de uso do gerenciamento de decisões no hub

* Ofertas personalizadas em quiosques e experiências em loja.
* Ofertas personalizadas por meio de experiências assistidas por agente, como centrais de atendimento ou interações de vendas.
* Ofertas incluídas em emails, mensagens SMS ou outras interações de saída.
* Execução de jornada entre canais - consistência de ofertas na Web, dispositivos móveis, email e outros canais de interação por meio do Adobe Journey Optimizer.

### Gerenciamento de decisões sobre considerações técnicas do hub

* Solicitações por segundo = 2000.
* Latência da resposta &lt; 500 ms.
* Acesso ao perfil completo do cliente em tempo real, incluindo associações de público-alvo, atributos e eventos de experiência.

## Gerenciamento de decisões na borda

A segunda abordagem é por meio da Experience Edge Network, que é uma infraestrutura distribuída globalmente para fornecer experiências rápidas de subsegundo e milissegundo. A experiência do consumidor final é executada pela infraestrutura de borda mais próxima da localização geográfica do consumidor para minimizar a latência. A gestão de decisões na borda foi projetada para fornecer experiências do consumidor em tempo real, como solicitações de personalização de entrada da Web ou móvel. Para obter mais informações sobre a gestão de decisões na borda, consulte o blueprint [Gestão de decisões na borda](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-edge.html?lang=pt-BR).

### Casos de uso do gerenciamento de decisões na borda

* Personalização online por meio de experiências de entrada da Web ou móvel.
* Execução de jornada entre canais - consistência de ofertas na Web, dispositivos móveis, email e outros canais de interação por meio do Adobe Journey Optimizer.

### Gerenciamento de decisões sobre considerações técnicas de borda

* Solicitações por segundo = 5000.
* Latência da resposta &lt; 250 ms.
* Acesso ao perfil Edge em tempo real. Somente públicos-alvo projetados de borda e atributos de perfil estarão disponíveis no perfil.
* Se a personalização for necessária nas experiências de primeira vez, o hub será ideal, pois o perfil completo está disponível. O perfil de borda deve sincronizar a partir do hub pela primeira vez na experiência de borda. Portanto, a primeira experiência da borda não incluirá dados de perfil previamente carregados no hub.

## Documentação relacionada

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=pt-BR)
* [Gestão de decisões do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)
* [Descrição do produto Adobe Journey Optimizer](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html)
* [Descrição do produto Adobe Offer Decisioning](https://helpx.adobe.com/br/legal/product-descriptions/offer-decisioning-app-service.html)
