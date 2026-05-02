---
title: Journey Optimizer - Blueprint de mensagens de terceiros
description: Demonstra como o Adobe Journey Optimizer pode ser usado com sistemas de mensagens de terceiros para enviar comunicações personalizadas.
solution: Journey Optimizer
exl-id: 3a14fc06-6d9c-4cd8-bc5c-f38e253d53ce
TQID: https://experienceleague.adobe.com/dlCwgPnHuoU0IGois2Yy3e9wPELIQsLkStzTBVl5M1M
product_v2:
  - id: cb954087-f4fc-4456-afb9-e939cabcdc79
feature_v2:
  - id: a653cc2e-bc85-4353-a306-399e5b247978
  - id: d556b755-390a-43f0-be32-a08cf6236126
  - id: d998adac-2f81-400b-a669-d07bb196e4eb
subfeature_v2:
  - id: af7571a6-3ddb-4c1c-abdf-4d4dde592140
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: 577
ht-degree: 61%

---

# Blueprint de mensagens de terceiros

>[!TIP]
>Este blueprint também está disponível como um [padrão de caso de uso](/help/blueprints/use-case-patterns/campaign-management-orchestration/third-party-messaging.md) em Gerenciamento e orquestração de campanhas.

Demonstra como o Adobe Journey Optimizer pode ser usado com sistemas de mensagens de terceiros para enviar comunicações personalizadas.

<br>

## Arquitetura

<img src="images/3rd-party-messaging-architecture.svg" alt="Blueprint do Journey Optimizer com arquitetura de referência" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Pré-requisitos

**Adobe Experience Platform**

* Os esquemas e conjuntos de dados devem ser configurados no sistema antes que você possa configurar as fontes de dados do Journey Optimizer
* Para esquemas baseados em classe de Evento de experiência, adicione o grupo de campos &quot;Orchestration eventID&quot; quando quiser que um evento que não seja baseado em regras seja acionado
* Para esquemas baseados em classe de Perfil individual, adicione o grupo de campos &quot;Detalhes do teste de perfil&quot; para poder carregar perfis de teste para uso com o Journey Optimizer

**Aplicativo de Mensagens de Terceiros**

* Deve ser compatível com chamadas de API REST para enviar cargas transacionais

<br>

## Medidas de proteção

[Link do produto Journey Optimizer Guardrails](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html)

[Medidas de proteção e orientação de latência completa](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/guardrails.html)

<br>

## Etapas de implementação

### Adobe Experience Platform

#### Esquema/Conjuntos de dados

1. [Configurar esquemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&lang=pt-BR) no Experience Platform, com base nos dados fornecidos pelo cliente.
1. [Crie conjuntos de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) na Experience Platform para que os dados sejam assimilados.
1. [Adicione rótulos de uso de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=pt-BR) na Experience Platform para o conjunto de dados para governança.
1. [Crie políticas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=pt-BR) que apliquem governança nos destinos.

#### Perfil/identidade

1. [Crie qualquer namespace específico para clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR).
1. [Adicione identidades a esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR).
1. [Habilite os esquemas e conjuntos de dados para o Perfil](https://experienceleague.adobe.com/pt-br/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile).
1. [Configure políticas de mesclagem](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=pt-BR) para visualizações diferentes do [!UICONTROL Perfil de cliente em tempo real] (opcional).
1. Crie segmentos para o uso do Journey.

#### Origens/destinos

1. [Assimile dados na Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&lang=pt-BR) usando APIs de transmissão e conectores de origem.

### Journey Optimizer

1. Configure sua fonte de dados do Experience Platform e determine quais campos devem ser armazenados em cache como parte da jornada
1. Os dados de transmissão, usados para iniciar uma jornada do cliente, devem ser configurados primeiro para obter uma ID de orquestração. Essa ID de orquestração é então fornecida ao desenvolvedor para uso durante a assimilação
1. Configure as origens de dados externos
1. Configure ações personalizadas para aplicativos de terceiros

### Configuração de push para publicação de conteúdo para dispositivos móveis (opcional, já que terceiros podem coletar tokens)

1. Implemente o SDK móvel da Experience Platform para coletar tokens de push e informações de logon a serem vinculadas a perfis de clientes conhecidos
1. Aproveite as tags da Adobe e crie uma propriedade de publicação de conteúdo para dispositivos móveis com a seguinte extensão:
   * Adobe Journey Optimizer
   * Rede de borda da Adobe Experience Platform
   * Identidade para [!DNL Edge Network]
   * Mobile Core
1. Certifique-se de ter um fluxo de dados dedicado para implantações de aplicativos móveis e implantações da Web
1. Para mais informações, siga o [Manual do Adobe Journey Optimizer Mobile](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer/)

<br>

## Documentação relacionada

* [Documentação do Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Documentação de tags do Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)
* [Documentação do Experience Platform Mobile SDK](https://experienceleague.adobe.com/docs/mobile.html)
* [Documentação do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html)
* [Descrição do produto Journey Optimizer](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html)
