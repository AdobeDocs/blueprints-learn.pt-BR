---
title: offer decisioning no hub
description: Forneça ofertas personalizadas aos consumidores em todos os canais, incluindo quiosques, experiências assistidas por agentes e em emails e outros deliveries de saída.
solution: Experience Platform, Journey Optimizer
exl-id: 5a386e18-bbac-4216-a35f-0a5016785e4a
source-git-commit: 494d70fca12a42befb7b726562d98cec17a21d22
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 32%

---

# Journey Optimizer - Offer decisioning no hub

O Gerenciamento de decisão do Adobe é um serviço fornecido como parte da Adobe Journey Optimizer. Este blueprint descreve os casos de uso e os recursos técnicos do aplicativo e fornece um mergulho profundo nos vários componentes da arquitetura e considerações que compõem o Offer Decisioning.

O Gerenciamento de decisões pode ser implantado de uma das duas maneiras. A primeira é através do hub Adobe Experience Platform, que é uma arquitetura central de data center. Na abordagem &quot;hub&quot;, as ofertas são executadas, personalizadas e entregues em latência de mais de 500 ms. Assim, a arquitetura do hub é mais adequada para experiências do cliente que não exigem latência de sub-segundo, os exemplos incluem decisões de oferta que são fornecidas para quiosques ou experiências assistidas por agentes, como em centrais de atendimento ou em interações pessoais. As ofertas inseridas em emails e campanhas de saída também são acionadas pela abordagem de hub.

A segunda abordagem é por meio da Experience Edge Network, que é uma infraestrutura distribuída geograficamente globalmente para fornecer experiências rápidas de sub-segundo e milissegundo. A experiência do consumidor final que está sendo executada pela infraestrutura de borda mais próxima da localização geográfica dos consumidores para minimizar a latência. O Gerenciamento de decisões no Edge foi projetado para fornecer experiências do consumidor em tempo real, como solicitações de personalização de entrada da Web ou móvel.

Esse blueprint abordará as especificidades do Gerenciamento de decisões no hub.

Para saber mais sobre o Gerenciamento de decisões no Edge, consulte [Gerenciamento de decisões na borda](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-edge.html?lang=en) blueprint.

Para saber mais sobre o Gerenciamento de decisões, consulte a documentação do produto [AQUI](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)

## Casos de uso

* Ofertas personalizadas em quiosques e em experiências de loja.
* Ofertas personalizadas por meio de experiência assistida por agente, como centrais de atendimento ou interações de vendas.
* Ofertas incluídas em email, SMS ou outras interações de saída.
* Execução de jornada entre canais - consistência de ofertas na Web, dispositivos móveis, email e outros canais de interação por meio do Adobe Journey Optimizer.

<br>

## Arquitetura

<img src="../assets/offers_hub.svg" alt="Offer decisioning de arquitetura de referência no blueprint da borda" style="width:100%; border:1px solid #4a4a4a" />

<br>

## Padrões de integração

| Integração | Descrição |
| :-- | :--- |
| [Offer Decisioning com Adobe Target](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html) | O Offer Decisioning pode ser integrado ao Adobe Target, de modo que as ofertas possam ser testadas e entregues como experiências do Target. |

## Pré-requisitos

Adobe Experience Platform

* Os esquemas e conjuntos de dados devem ser configurados no sistema antes que você possa configurar as fontes de dados do Journey Optimizer
* Para esquemas do Experience Event baseados em classe, adicione o grupo de campos “eventID de orquestração” quando quiser acionar um evento que não seja baseado em regras
* Para esquemas de Perfil individual baseados em classe, adicione o grupo de campos “Detalhes do teste de perfil” para carregar perfis de teste a serem usados com o Journey Optimizer

<br>

## Medidas de proteção

* Para as medidas de proteção da Journey Optimizer, consulte o seguinte [Journey Optimizer Guardrails](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/limitations.html).
* Para as medidas de proteção de Offer decisioning, consulte [Descrição do produto Offer Decisioning](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html).


### Medidas de proteção da assimilação de dados

<img src="../assets/aep-data-ingestion-details-latency.svg" alt="Blueprint do Journey Optimizer com arquitetura de referência" style="width:80%; border:1px solid #4a4a4a" />

<br>

### Medidas de Proteção de ativação

<img src="../assets/ajo-activation-details-latency.svg" alt="Blueprint do Journey Optimizer com arquitetura de referência" style="width:80%; border:1px solid #4a4a4a" />

<br>

## Padrões de implementação

* Implementado em email, SMS e canais de saída por meio da integração direta com o [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/offers-e2e.html).
* Para a implementação baseada em API do servidor do Offer Decisioning, aproveite o [API de decisão](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/decisioning-vs-edge-apis.html).
* Para a implementação de decisões baseadas em lote para entregar ofertas em massa para um aplicativo de delivery de mensagem, use a [API de decisão em lote](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/batch-decisioning-api.html).
* Para experiências em tempo real baseadas no Edge, use o SDK da Web/Mobile ou a API do Edge Decisioning, conforme descrito na seção [offer decisioning no blueprint do Edge](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-edge.html).
<br>

## Etapas de implementação

### Adobe Experience Platform

#### Esquemas/Conjuntos de dados

1. [Configure perfil individual, evento de experiência e esquemas de várias entidades](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) na Experience Platform com base nos dados fornecidos pelo cliente.
1. [Crie conjuntos de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) na Experience Platform para que os dados sejam assimilados.
1. [Adicione rótulos de uso de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=pt-BR) na Experience Platform para o conjunto de dados para governança.
1. [Crie políticas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=pt-BR) que apliquem governança nos destinos.

#### Perfil/Identidade

1. [Crie qualquer namespace específico para clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR).
1. [Adicione identidades a esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Habilite os esquemas e conjuntos de dados para o Perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=pt-BR).
1. [Configure políticas de mesclagem](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=pt-BR) para visualizações diferentes do [!UICONTROL Perfil de cliente em tempo real] (opcional).
1. Crie segmentos para o uso do Journey.

#### Origens/Destinos

1. [Assimile dados na Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) usando APIs de transmissão e conectores de origem.

## Documentação relacionada

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html)
* [Gerenciamento de decisões da Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)
* [Descrição do produto Adobe Journey Optimizer](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
* [Descrição do produto Offer decisioning Adobe](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html)
