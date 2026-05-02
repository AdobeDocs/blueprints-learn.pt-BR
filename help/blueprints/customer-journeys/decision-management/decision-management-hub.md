---
title: Gestão de decisões no blueprint do Hub
description: Forneça ofertas personalizadas aos consumidores em todos os canais, incluindo em quiosques, em experiências assistidas por agentes e em emails e outras apresentações.
solution: Experience Platform, Journey Optimizer
exl-id: 5a386e18-bbac-4216-a35f-0a5016785e4a
TQID: https://experienceleague.adobe.com/5-kMUczdmmV9chsrSkAirbFXCmxMZfWemXDLa0ppd5I
product_v2:
  - id: cb954087-f4fc-4456-afb9-e939cabcdc79
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: d998adac-2f81-400b-a669-d07bb196e4eb
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: df64005d-8f9a-422e-ba4d-c6f6dc3454b4
  - id: fe338112-e2ce-4876-8989-fc4d497613f1
subfeature_v2:
  - id: e5ae22e3-a3b0-46ed-804f-9abf1bbe3e74
  - id: ee602049-8a18-43df-9299-a689a025a371
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: 776
ht-degree: 76%

---

# Gerenciamento de decisão no blueprint do hub

>[!TIP]
>Este blueprint também está disponível como um [padrão de caso de uso](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) no Personalization.

Para saber mais sobre a gestão de decisões, consulte a documentação do produto [AQUI](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=pt-BR) e a Visão geral da gestão de decisões [AQUI](decision-management-overview.md)

A gestão de decisões da Adobe é um serviço fornecido como parte do Adobe Journey Optimizer. Esse blueprint descreve os casos de uso e os recursos técnicos do aplicativo e fornece mais detalhes sobre os diferentes componentes da arquitetura e considerações que compõem a gestão de decisões.

O Journey Optimizer é usado para fornecer a melhor oferta e experiência aos clientes em todos os pontos de contato no momento certo. A gestão de decisões ajuda você a enviar a oferta certa para o os clientes no momento certo, facilitando a personalização com uma biblioteca central de ofertas de marketing e um mecanismo de decisão que aplica regras e restrições a perfis avançados em tempo real criados pela Adobe Experience Platform.

A gestão de decisões pode ser implantada de duas maneiras. A primeira é por meio do hub da Adobe Experience Platform, que é uma arquitetura de datacenter centralizada. Na abordagem de “hub”, as ofertas são executadas, personalizadas e entregues na latência de >500 milissegundos. Por isso, a arquitetura de hub é mais adequada para experiências do cliente que não exigem latência de subsegundo. Exemplos incluem definições de ofertas que são fornecidas para quiosques ou experiências assistidas por agentes, como em centrais de atendimento ou em interações pessoais. As ofertas inseridas em emails e campanhas de saída também são possibilitadas pela abordagem de hub.

A segunda abordagem é por meio da Experiência [!DNL [!DNL Edge Network]], que é uma infraestrutura distribuída globalmente e localizada geograficamente para atender experiências rápidas de subsegundos e milissegundos. A experiência do consumidor final é executada pela infraestrutura de borda mais próxima da localização geográfica do consumidor para minimizar a latência. A gestão de decisões na borda foi projetada para fornecer experiências do consumidor em tempo real, como solicitações de personalização de entrada da Web ou móvel.

Esse blueprint abordará as especificidades da gestão de decisões no hub.

Para obter mais informações sobre a gestão de decisões na borda, consulte o blueprint [Gestão de decisões na borda](decision-management-edge.md).

## Casos de uso da gestão de decisões no hub

* Casos de uso de transmissão em que a latência de contexto do perfil não é estrita: 15 minutos ou mais.
* Ofertas personalizadas em quiosques e experiências em loja.
* Ofertas personalizadas por meio de experiências assistidas por agente, como centrais de atendimento ou interações de vendas.
* Ofertas incluídas em emails, mensagens SMS, notificações por push ou outras interações de saída.
* Forneça ofertas a sistemas externos de ESP e de envio de mensagens para delivery.
* Execução de jornada entre canais – consistência de ofertas na Web, dispositivos móveis, email e outros canais de interação por meio do Adobe Journey Optimizer.

>[!IMPORTANT]
>
>Para casos de uso de oferta e jornada que exigem o acesso ao perfil para obter informações e contexto adicionais. É importante considerar a latência associada da assimilação de dados no perfil no hub para garantir que ele esteja disponível no momento da decisão. Para cenários em que o contexto é de transmissão ou assimilação no perfil e a oferta ou jornada deve ter esse contexto disponível em segundos ou minutos após a decisão de oferta, esses cenários são mais adequados para o Gerenciamento de decisão no Edge.

## Arquitetura

<img src="images/offers_hub.svg" alt="Arquitetura de referência do blueprint da gestão de decisões na borda" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## Medidas de proteção

* Para as medidas de proteção do Journey Optimizer, consulte [Medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/limitations.html?lang=pt-BR).
* Para as medidas de proteção da gestão de decisões, consulte [Descrição do produto gestão de decisões](https://helpx.adobe.com/br/legal/product-descriptions/offer-decisioning-app-service.html).

[Medidas de proteção e orientação de latência completa](/help/blueprints/experience-platform/guardrails.md)

## Padrões de implementação

* Implementado em emails, mensagens SMS e canais de saída por meio da integração direta com o [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/offers-e2e.html?lang=pt-BR).
* Para a implementação baseada em API de servidor da gestão de decisões, utilize a [API de decisão](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/decisioning-vs-edge-apis.html?lang=pt-BR).
* Para a implementação de decisões baseadas em lote para fornecer ofertas em massa para um aplicativo de entrega de mensagem, utilize a [API de decisão em lote](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/batch-decisioning-api.html?lang=pt-BR).
* Para experiências em tempo real baseadas em Edge, use a Web/Mobile SDK ou a API de decisão da Edge, conforme descrito no [Gerenciamento de decisões no blueprint do Edge](decision-management-edge.md)

## Documentação relacionada

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=pt-BR)
* [Gestão de decisões do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=pt-BR)
* [Descrição do produto Adobe Journey Optimizer](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html)
* [Descrição do produto Adobe Decision Management](https://helpx.adobe.com/br/legal/product-descriptions/offer-decisioning-app-service.html)
