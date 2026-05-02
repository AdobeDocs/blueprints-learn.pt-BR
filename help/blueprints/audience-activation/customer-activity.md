---
title: Acesso ao perfil em tempo real para cenários de suporte e vendas
description: Pesquisas de [!UICONTROL perfis de clientes em tempo real] para fornecer contexto ao suporte e às vendas atendidas por agentes.
solution: Data Collection
kt: 7195
exl-id: 3616cbf1-2e59-4e68-a1ff-1d2e3b344a1c
TQID: https://experienceleague.adobe.com/Ci9pUbGCLQ9uhlQ9l1na7A2NiI9CpCRMLrUSN6lSOnU
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
feature_v2:
  - id: a075b2c1-7748-4328-b7f6-343aa314616a
  - id: b12f6872-9271-4369-85e5-86969a0b99a2
  - id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
  - id: ba929a52-9339-4154-9487-317dc875a3c7
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
  - id: e5ae22e3-a3b0-46ed-804f-9abf1bbe3e74
  - id: ee602049-8a18-43df-9299-a689a025a371
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: 368
ht-degree: 54%

---

# Acesso ao perfil em tempo real para cenários de suporte e vendas

>[!TIP]
>Este blueprint também está disponível como um [padrão de caso de uso](/help/blueprints/use-case-patterns/audience-building-activation/real-time-profile-lookup.md) em Criação e ativação de público-alvo.

O blueprint Real-time Profile Access for Support and Sales Scenarios (Acesso a perfil em tempo real para suporte e cenários de vendas) mostra como os aplicativos externos podem acessar o [!UICONTROL Perfil do cliente em tempo real] da Adobe Experience Platform.

Aplicativos externos podem acessar Perfis de clientes com uma solicitação GET da API. Atributos, eventos, associações de segmentos e funcionalidades orientadas por modelos armazenadas no perfil podem depois ser usados nesses aplicativos externos que não são da Adobe.

Com essa funcionalidade, é possível acessar conteúdo avançado durante chamadas de clientes à central de atendimento. Agentes de suporte teriam visibilidade do valor vitalício do cliente, da propensão à rotatividade ou exposição a campanhas de marketing, por exemplo. Os agentes de vendas também podem se beneficiar de conteúdos extras ou insights sobre os clientes.

>[!NOTE]
>
>A pesquisa de perfil no hub não se destina a casos de uso de alta taxa de transferência e baixa latência, como personalização de entrada da web/dispositivos móveis. A pesquisa de perfil no hub destina-se a cenários de latência mais baixa, como suporte assistido por agente ou interações de vendas. Para cenários de baixa latência e alta taxa de transferência, como personalização da Web/móvel ou o Offer Decisioning em tempo real, o perfil do Edge deve ser aproveitado. O perfil do Edge habilita o acesso em tempo real por meio da [Conexão personalizada do Personalization](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/catalog/personalization/custom-personalization) da Real-time Customer Data Platform.

## Casos de uso

* Forneça contexto aprofundado do consumidor nas interações com agentes, como suporte e experiências de vendas. Ao usar a pesquisa de perfil na Experience Platform, os agentes podem receber mais contexto sobre o consumidor, como compras recentes, interações com campanhas, propensões, associações do público e outros atributos e insights que são armazenados no perfil do cliente em tempo real.

## Arquitetura

<img src="assets/customer_activity_hub.svg" alt="Blueprint de arquitetura de referência para o Hub de atividades do cliente" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />

## Medidas de proteção

* [Medidas de proteção para dados do [!UICONTROL Perfil de cliente em tempo real]](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)

## Documentação relacionada

* [Descrição do produto Adobe Experience Platform Ativation](https://helpx.adobe.com/br/legal/product-descriptions/adobe-experience-platform0.html)
* [Documentação de [!UICONTROL Perfil de cliente em tempo real]](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=pt-BR)
* [Proteções de perfil](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)
* [API de pesquisa de perfil](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
