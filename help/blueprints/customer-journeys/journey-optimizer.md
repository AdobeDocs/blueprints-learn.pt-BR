---
title: Journey Optimizer - Mensagens acionadas e Adobe Experience Platform Blueprint
description: Execute mensagens e experiências acionadas usando a Adobe Experience Platform como um hub central para dados de transmissão, perfis de clientes e segmentação.
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: dc13a1fe9a32f70497c5c73485618e6989b7a644
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 49%

---

# Journey Optimizer

O Adobe Journey Optimizer é um sistema criado para as equipes de marketing reagirem em tempo real aos comportamentos dos clientes e atendê-los onde estiverem. Os recursos de gerenciamento de dados foram transferidos para a Adobe Experience Platform, permitindo que as equipes de marketing se concentrem no que fazem de melhor: que está criando jornadas de clientes de classe mundial e conversas personalizadas.  Este blueprint descreve os recursos técnicos do aplicativo e fornece um mergulho profundo nos vários componentes de arquitetura que compõem o Adobe Journey Optimizer.

## Casos de uso

* Mensagens acionadas
* Confirmações de registro
* Carrinho de compras e abandonos de formulários de aplicação
* Mensagens acionadas de localização

## Arquitetura

<img src="assets/journey-optimizer.png" alt="Arquitetura de referência para o blueprint de mensagens acionadas e Adobe Experience Platform" style="border:1px solid #4a4a4a" />

## Padrões de integração

* Adobe Experience Platform -> Journey Optimizer

## Pré-requisitos

1. O cliente deve ser provisionado para o Experience Cloud com uma Organização IMS válida
1. Push móvel

* O cliente deve ter um desenvolvedor móvel disponível para criar o aplicativo
* Adobe Experience Platform Mobile SDK
* Adobe Launch
   * Propriedade móvel
      * Extensões:
         * Extensão do Adobe Journey Optimizer
         * Rede de borda Adobe Experience Platform
         * Identidade
         * Mobile Core
         * Perfil
   * Configurações do aplicativo
   * Datastreams
      * Ativado para Experience Platform
      * Conjunto de dados de eventos - usado para coletar o comportamento móvel geral
      * Conjunto de dados de perfil - Conjunto de dados do perfil de push do AJO (não pode ser diferente)

## Medidas de proteção

* Consulte o link para obter mais detalhes sobre limitações
* Segmentos em lote - precisam garantir que você compreenda o volume diário de usuários qualificados e garanta que o sistema de destino possa lidar com a taxa de transferência de explosão por jornada e em todas as jornadas
* Segmentos de transmissão - é necessário garantir que a explosão inicial das qualificações de perfil possa ser tratada junto com o volume de qualificação de transmissão diária por jornada e em todas as jornadas
* Atividade de atualização de perfil - o Perfil do cliente em tempo real pode ser atualizado nativamente de uma jornada.  Há um atraso de até 1 minuto no processamento da atualização na loja de perfis
* Eventos de negócios - uma jornada baseada em segmento de leitura pode ser acionada para iniciar com base em uma chamada externa para o sistema JO
* Oferece suporte nativo ao Offer Decisioning somente em mensagens. Suporte futuro por ação nativa
* Canais compatíveis:
   * Email
   * Push (FCM/APNS)
   * Rest Endpoints de API
* Processa eventos 5k por segundo com dimensionamento horizontal (a carteira é limitação)
* O teste A/B é feito usando dois deliveries e determinando resultados usando QS ou CJA
* Integração Litmus - deve ter uma conta com o Litmus para aproveitar a integração

## Etapas de implementação

### Adobe Experience Platform

#### Esquemas/Conjuntos de dados

1. [Configure perfil individual, evento de experiência e esquemas de várias entidades](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html?lang=pt-BR) na Experience Platform com base nos dados fornecidos pelo cliente.
1. Crie esquemas do Adobe Campaign para broadLog, trackingLog, endereços sem entrega e preferências de perfil (opcional).
1. [Crie conjuntos de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) na Experience Platform para que os dados sejam assimilados.
1. [Adicione rótulos de uso de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=pt-BR) na Experience Platform para o conjunto de dados para governança.
1. [Crie políticas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=pt-BR) que apliquem governança nos destinos.

#### Perfil/Identidade

1. [Crie qualquer namespace específico para clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR).
1. [Adicione identidades a esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Habilite os esquemas e conjuntos de dados para o Perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=pt-BR).
1. [Configure políticas de mesclagem](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=pt-BR) para visualizações diferentes do [!UICONTROL Perfil de cliente em tempo real] (opcional).
1. Crie segmentos para o uso do Campaign.

#### Origens/Destinos

1. [Assimile dados na Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) usando APIs de streaming e conectores de origem.1. Configure o destino de armazenamento do [!DNL Azure] blob para usar com o Adobe Campaign.

#### Implantação de aplicativo para dispositivos móveis

1. Implemente o SDK do Adobe Campaign para o Adobe Campaign Classic ou o SDK da Experience Platform para o Adobe Campaign Standard. Se o Experience Platform Launch estiver presente, recomenda-se usar a extensão do Adobe Campaign Classic ou o Adobe Campaign Standard com o SDK da Experience Platform.


### Journey Orchestration

1. Os dados de transmissão usados para iniciar uma jornada do cliente devem ser configurados no Journey Optimizer primeiro para obter uma ID de orquestração. Depois, essa ID de orquestração será fornecida ao desenvolvedor para usá-la na assimilação.
1. Configure as origens de dados externos.
1. Configure as ações personalizadas.

## Documentação relacionada

* [Documentação da Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Documentação do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-orchestration.html?lang=pt-BR)
* [Documentação do Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html?lang=pt-BR)
* [Documentação do SDK móvel da Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
