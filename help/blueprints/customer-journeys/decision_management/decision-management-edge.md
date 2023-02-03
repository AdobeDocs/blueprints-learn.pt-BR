---
title: Gestão de decisões no blueprint do Edge
description: Forneça ofertas personalizadas aos consumidores em todos os canais, incluindo em experiências da Web e móveis em tempo real.
solution: Experience Platform, Journey Optimizer
exl-id: 31e5f624-5578-49e1-ab92-5cabd596a632
source-git-commit: b18d491fdefc57762932d1570401b5437bf97c76
workflow-type: ht
source-wordcount: '856'
ht-degree: 100%

---

# Journey Optimizer – Blueprint da gestão de decisões no Edge

Para saber mais sobre a gestão de decisões, consulte a documentação do produto [AQUI](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=pt-BR) e a Visão geral da gestão de decisões [AQUI](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-overview.html?lang=pt-BR)

A gestão de decisões da Adobe é um serviço fornecido como parte do Adobe Journey Optimizer. Esse blueprint descreve os casos de uso e os recursos técnicos do aplicativo e fornece mais detalhes sobre os diferentes componentes da arquitetura e considerações que compõem a gestão de decisões.

A gestão de decisões pode ser implantada de duas maneiras. A primeira é por meio do hub da Adobe Experience Platform, que é uma arquitetura de datacenter única. Na abordagem de “hub”, as ofertas são executadas, personalizadas e entregues na latência de segundos. Por isso, a arquitetura de hub é mais adequada para uma experiência do cliente que não exige latência de subsegundo. Exemplos incluem definições de ofertas que são fornecidas para quiosques ou experiências assistidas por agentes, como em centrais de atendimento ou em interações pessoais.

A segunda abordagem é por meio da Experience Edge Network, que é uma infraestrutura distribuída globalmente para fornecer experiências rápidas de subsegundo e milissegundo. A experiência do consumidor final é executada pela infraestrutura de borda mais próxima da localização geográfica do consumidor para minimizar a latência. A gestão de decisões na borda foi projetada para fornecer experiências do consumidor em tempo real. Isso inclui experiências como solicitações de personalização de entrada da Web ou móvel.

Esse blueprint abordará as especificidades da gestão de decisões na borda.

Para obter mais informações sobre a gestão de decisões no hub, consulte o blueprint [Gestão de decisões no hub](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-hub.html?lang=pt-BR).

## Casos de uso da gestão de decisões na borda

* Personalização online por meio de experiências de entrada da Web ou móvel.
* Execução de jornada entre canais – consistência de ofertas na Web, dispositivos móveis, email e outros canais de interação por meio do Adobe Journey Optimizer.

<br>

## Arquitetura

<img src="../assets/offers_edge.svg" alt="Arquitetura de referência do blueprint da gestão de decisões na borda" style="width:100%; border:1px solid #4a4a4a" />

<br>

## Padrões de integração

| Integração | Descrição |
| :-- | :--- |
| [Gestão de decisões com o Adobe Target](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html?lang=pt-BR) | A gestão de decisões pode ser integrado ao Adobe Target, de modo que as ofertas possam ser testadas e entregues como experiências do Target. |

## Pré-requisitos

Adobe Experience Platform

* Os esquemas e conjuntos de dados devem ser configurados no sistema antes que você possa configurar as fontes de dados do Journey Optimizer
* Para esquemas do Experience Event baseados em classe, adicione o grupo de campos “eventID de orquestração” quando quiser acionar um evento que não seja baseado em regras
* Para esquemas de Perfil individual baseados em classe, adicione o grupo de campos “Detalhes do teste de perfil” para carregar perfis de teste a serem usados com o Journey Optimizer

<br>

## Medidas de proteção

* Para as medidas de proteção do Journey Optimizer, consulte [Medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/limitations.html?lang=pt-BR).
* Para as medidas de proteção da gestão de decisões, consulte [Descrição do produto gestão de decisões](https://helpx.adobe.com/br/legal/product-descriptions/offer-decisioning-app-service.html).
* Solicitações por segundo = 5.000.
* Latência de resposta &lt; 250 ms.
* Acesso ao perfil de borda em tempo real. Somente atributos de perfil e públicos projetados na borda ficam disponíveis no perfil.
* Caso haja necessidade de personalização nas primeiras experiências, o hub é ideal, pois o perfil completo fica disponível. O perfil de borda deve ser sincronizado a partir do hub para a primeira experiência de borda. Portanto, a primeira experiência da borda não inclui dados de perfil cujo upload tenha sido feito anteriormente no hub.

### Proteção da assimilação de dados

<img src="../../experience-platform/assets/aep_data_flow_guardrails.svg" alt="Fluxo de dados da Experience Platform" style="border:1px solid #4a4a4a" width="85%" />

<br>

### Medidas de proteção de ativação

<img src="../../experience-platform/assets/AJO_guardrails.svg" alt="Blueprint do Journey Optimizer com arquitetura de referência" style="width:85%; border:1px solid #4a4a4a" />

<br>

## Padrões de implementação

* Use o SDK da Web ou móvel para implantação em sites e aplicativos para dispositivos móveis, de modo a implementar a gestão de decisões onde o SDK foi implantado.
   * [Blueprint do SDK da Web/móvel](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/websdk.html?lang=pt-BR)
   * [SDK da Web](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/offer-decisioning/offer-decisioning-overview.html?lang=pt-BR)
   * [MobileSDK](https://aep-sdks.gitbook.io/docs/)

Ou

* Para uma implementação baseada em servidor de API, use a API do serviço Edge Network para implementar a gestão de decisões diretamente de um servidor para outro.
   * [API de servidor da Edge Network](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/deliver-offers.html?lang=pt-BR)

<br>

## Etapas de implementação

### Adobe Experience Platform

#### Esquema/Conjuntos de dados

1. [Configure perfil individual, evento de experiência e esquemas de várias entidades](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=pt-BR) na Experience Platform com base nos dados fornecidos pelo cliente.
1. [Crie conjuntos de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) na Experience Platform para que os dados sejam assimilados.
1. [Adicione rótulos de uso de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=pt-BR) na Experience Platform para o conjunto de dados para governança.
1. [Crie políticas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=pt-BR) que apliquem governança nos destinos.

#### Perfil/identidade

1. [Crie qualquer namespace específico para clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR).
1. [Adicione identidades a esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR).
1. [Habilite os esquemas e conjuntos de dados para o Perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=pt-BR).
1. [Configure políticas de mesclagem](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=pt-BR) para visualizações diferentes do [!UICONTROL Perfil de cliente em tempo real] (opcional).
1. Crie segmentos para o uso do Journey.

#### Origens/destinos

1. [Assimile dados na Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) usando APIs de transmissão e conectores de origem.

## Documentação relacionada

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=pt-BR)
* [Gestão de decisões do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=pt-BR)
* [Descrição do produto Adobe Journey Optimizer](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html)
* [Descrição do produto gestão de decisões da Adobe](https://helpx.adobe.com/br/legal/product-descriptions/offer-decisioning-app-service.html)
