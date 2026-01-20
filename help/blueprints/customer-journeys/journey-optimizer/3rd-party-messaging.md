---
title: Journey Optimizer - Blueprint de mensagens de terceiros
description: Demonstra como o Adobe Journey Optimizer pode ser usado com sistemas de mensagens de terceiros para enviar comunicações personalizadas.
solution: Journey Optimizer
exl-id: 3a14fc06-6d9c-4cd8-bc5c-f38e253d53ce
source-git-commit: 8fcc71abcc29f5dc7d2e2b3a5afcc60d9e844fcc
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 62%

---

# Blueprint de mensagens de terceiros

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

[Link do produto de medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=pt-BR)

[Medidas de Proteção e Orientação de Latência de Ponta a Ponta](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/guardrails.html?lang=pt-BR)

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

* [Documentação da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Documentação de tags da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)
* [Documentação do SDK móvel da Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
* [Documentação do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR)
* [Descrição do produto do Journey Optimizer](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html)
