---
title: Gestão de decisões no blueprint do Hub
description: Forneça ofertas personalizadas aos consumidores em todos os canais, incluindo em quiosques, em experiências assistidas por agentes e em emails e outras apresentações.
solution: Experience Platform, Journey Optimizer
exl-id: 5a386e18-bbac-4216-a35f-0a5016785e4a
source-git-commit: d7901280f1bc23e6d37bcb285f20343c5ed8b46e
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 100%

---

# Gestão de decisões no blueprint do Hub

Para saber mais sobre a gestão de decisões, consulte a documentação do produto [AQUI](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=pt-BR) e a Visão geral da gestão de decisões [AQUI](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-overview.html?lang=pt-BR)

A gestão de decisões da Adobe é um serviço fornecido como parte do Adobe Journey Optimizer. Esse blueprint descreve os casos de uso e os recursos técnicos do aplicativo e fornece mais detalhes sobre os diferentes componentes da arquitetura e considerações que compõem a gestão de decisões.

O Journey Optimizer é usado para fornecer a melhor oferta e experiência aos clientes em todos os pontos de contato no momento certo. A gestão de decisões ajuda você a enviar a oferta certa para o os clientes no momento certo, facilitando a personalização com uma biblioteca central de ofertas de marketing e um mecanismo de decisão que aplica regras e restrições a perfis avançados em tempo real criados pela Adobe Experience Platform.

A gestão de decisões pode ser implantada de duas maneiras. A primeira é por meio do hub da Adobe Experience Platform, que é uma arquitetura de datacenter centralizada. Na abordagem de “hub”, as ofertas são executadas, personalizadas e entregues na latência de >500 milissegundos. Por isso, a arquitetura de hub é mais adequada para experiências do cliente que não exigem latência de subsegundo. Exemplos incluem definições de ofertas que são fornecidas para quiosques ou experiências assistidas por agentes, como em centrais de atendimento ou em interações pessoais. As ofertas inseridas em emails e campanhas de saída também são possibilitadas pela abordagem de hub.

A segunda abordagem é por meio da Experience Edge Network, que é uma infraestrutura distribuída globalmente para fornecer experiências rápidas de subsegundo e milissegundo. A experiência do consumidor final é executada pela infraestrutura de borda mais próxima da localização geográfica do consumidor para minimizar a latência. A gestão de decisões na borda foi projetada para fornecer experiências do consumidor em tempo real, como solicitações de personalização de entrada da Web ou móvel.

Esse blueprint abordará as especificidades da gestão de decisões no hub.

Para obter mais informações sobre a gestão de decisões na borda, consulte o blueprint [Gestão de decisões na borda](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-edge.html?lang=pt-BR).

## Casos de uso da gestão de decisões no hub

* Ofertas personalizadas em quiosques e experiências em loja.
* Ofertas personalizadas por meio de experiências assistidas por agente, como centrais de atendimento ou interações de vendas.
* Ofertas incluídas em emails, mensagens SMS, notificações por push ou outras interações de saída.
* Forneça ofertas a sistemas externos de ESP e de envio de mensagens para delivery.
* Execução de jornada entre canais – consistência de ofertas na Web, dispositivos móveis, email e outros canais de interação por meio do Adobe Journey Optimizer.

<br>

## Arquitetura

<img src="../assets/offers_hub.svg" alt="Arquitetura de referência do blueprint da gestão de decisões na borda" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Pré-requisitos

Adobe Experience Platform

* Os esquemas e conjuntos de dados devem ser configurados no sistema antes que você possa configurar as fontes de dados do Journey Optimizer
* Para esquemas do Experience Event baseados em classe, adicione o grupo de campos “eventID de orquestração” quando quiser acionar um evento que não seja baseado em regras
* Para esquemas de Perfil individual baseados em classe, adicione o grupo de campos “Detalhes do teste de perfil” para carregar perfis de teste a serem usados com o Journey Optimizer

<br>

## Medidas de proteção

* Para as medidas de proteção do Journey Optimizer, consulte [Medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/limitations.html?lang=pt-BR).
* Para as medidas de proteção da gestão de decisões, consulte [Descrição do produto gestão de decisões](https://helpx.adobe.com/br/legal/product-descriptions/offer-decisioning-app-service.html).
* Solicitações por segundo = 2.000.
* Latência de resposta &lt; 500 ms.
* Acesso ao perfil completo do cliente em tempo real, incluindo atributos, eventos de experiência e associações de público.


### Proteção da assimilação de dados

<img src="../../experience-platform/deployment/assets/aep_data_flow_guardrails.svg" alt="Fluxo de dados da Experience Platform" style="border:1px solid #4a4a4a" width="85%" class="modal-image" />

<br>

### Medidas de proteção de ativação

<img src="../../experience-platform/deployment/assets/AJO_guardrails.svg" alt="Blueprint do Journey Optimizer com arquitetura de referência" style="width:85%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Padrões de implementação

* Implementado em emails, mensagens SMS e canais de saída por meio da integração direta com o [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/offers-e2e.html?lang=pt-BR).
* Para a implementação baseada em API de servidor da gestão de decisões, utilize a [API de decisão](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/decisioning-vs-edge-apis.html?lang=pt-BR).
* Para a implementação de decisões baseadas em lote para fornecer ofertas em massa para um aplicativo de entrega de mensagem, utilize a [API de decisão em lote](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/batch-decisioning-api.html?lang=pt-BR).
* Para experiências em tempo real baseadas em borda, use o SDK da Web/móvel ou a API de decisão na borda, conforme descrito no [Blueprint na borda da gestão de decisões](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-edge.html?lang=pt-BR).
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
