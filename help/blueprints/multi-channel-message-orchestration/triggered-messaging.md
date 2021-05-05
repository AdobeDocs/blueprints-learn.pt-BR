---
title: Mensagens acionadas e Adobe Experience Platform Blueprint
description: Execute mensagens e experiências acionadas usando a Adobe Experience Platform como um hub central de dados de transmissão, perfis de clientes e segmentação.
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
exl-id: 97831309-f235-4418-bd52-28af815e1878
translation-type: tm+mt
source-git-commit: 01f70fe432d7be38b71889ae19c0d5fe4cf0f78a
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 69%

---

# Mensagens acionadas e Adobe Experience Platform Blueprint

Execute mensagens e experiências acionadas usando a Adobe Experience Platform como um hub central de dados de transmissão, perfis de clientes e segmentação.

## Casos de uso

* Mensagens acionadas
* Confirmações de registro
* Carrinho de compras e abandonos de formulários de aplicação
* Mensagens acionadas de localização

## Arquitetura

<img src="assets/triggered.svg" alt="Arquitetura de referência para o blueprint do Triggered Messaging e do Adobe Experience Platform" style="border:1px solid #4a4a4a" />

## Padrões de integração

* Adobe Experience Platform -> Journey Orchestration

## Pré-requisitos

* Adobe Experience Platform
* Journey Orchestration

## Medidas de proteção

### Journey Orchestration

* Consulte o link para obter [mais detalhes sobre limitações](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=pt-BR#starting-with-journeys)
* O limite está disponível por meio de configuração de API para garantir que o sistema de destino não esteja saturado ao ponto de falha. Significa que as mensagens que excederem o limite serão completamente removidas sem ser enviadas. O Regulador ainda não é compatível.
   * conexões máximas: número máximo de conexões http/s com que um destino pode lidar.
   * contagem máxima de chamadas: número máximo de chamadas a serem realizadas no parâmetro periodInMs
   * periodInMs: tempo em milissegundos
* Jornadas iniciadas por associação de segmentos podem operar em dois modos:
   * segmentos em lote (atualizados a cada 24 horas)
   * segmentos por streaming (qualificação de &lt;5 minutos)
* Segmentos em lote: asseguram que você entenda o volume diário de usuários qualificados e que o sistema de destino possa lidar com a taxa de transferência intermitente por jornada e em todas as jornadas
* Segmentos por streaming: asseguram que a intermitência inicial de qualificações de perfis possam ser manipuladas com o volume de qualificações de streaming diárias por jornada e em todas as jornadas
* O destino final não deve ser compatível com cargas de REST API e JSON
* Atualmente, não é compatível com o Offer Decisioning
* Consulte [medidas de proteção para assimilação de dados e perfis na Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)

### Adobe Campaign Standard

* Compatível somente com 14 tps (50 mil por hora) na taxa de transferência
* Jornadas iniciadas por associação de segmentos não são compatíveis
* Eventos de reação para abertura/cliques de mensagens transacionais são compatíveis no Journey Orchestration.
* Atualmente, os logs de mensagens transacionais não são sincronizados nativamente com a Experience Platform, o que exige configuração manual. Recomenda-se a exportação dos logs no máximo a cada quatro horas.


## Etapas de implementação

### Adobe Experience Platform

#### Esquemas/Conjuntos de dados

1. [Configure perfil individual, evento de experiência e esquemas de várias entidades na Experience Platform com base nos dados fornecidos pelo cliente.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html)
1. Crie esquemas do Adobe Campaign para broadLog, trackingLog, endereços não entregues e preferências de perfil (opcional).
1. [Crie ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) conjuntos de dados no Experience Platform para que os dados sejam assimilados.
1. [Adicione ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html) rótulos de uso de dados no Experience Platform ao conjunto de dados para controle.
1. [Crie políticas que apliquem governança nos destinos.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html)

#### Perfil/Identidade

1. [Crie qualquer namespace específico para clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Adicione identidades a esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Ative os esquemas e conjuntos de dados para Perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Configure ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html) políticas de mesclagem para diferentes visualizações do Perfil do cliente em tempo  [!UICONTROL real]  (opcional).
1. Crie segmentos para uso do Adobe Campaign.

#### Origens/Destinos

1. [Insira dados na Experience ](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) Platform usando APIs de fluxo e conectores de origem.1. Configure o destino de armazenamento de  [!DNL Azure] blob para uso com o Adobe Campaign.

#### Implantação de aplicativo para dispositivos móveis

1. Implemente o SDK do Adobe Campaign para Adobe Campaign Classic ou Experience Platform SDK para Adobe Campaign Standard. Se o Experience Platform Launch estiver presente, a recomendação é usar a extensão Adobe Campaign Classic ou Adobe Campaign Standard com o Experience Platform SDK.


### Journey Orchestration

1. Dados de streaming usados para inicializar uma jornada do cliente devem estar configurados primeiro dentro do Journey Orchestration para obter uma ID de orquestração. Depois, essa ID de orquestração será fornecida ao desenvolvedor para usá-la na assimilação.
1. Configure as origens de dados externos.
1. Configure as ações personalizadas.

### Adobe Campaign Standard

1. Configure os modelos de mensagens com as definições apropriadas de personalização.
1. Configure os fluxos de trabalho de exportação e exporte os logs de mensagens transacionais. A recomendação é executar no máximo a cada quatro horas.


## Documentos relacionados

* [Documentação da Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Documentação do Journey Orchestration](https://experienceleague.adobe.com/docs/journey-orchestration.html?lang=pt-BR)
* [Documentação do Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=pt-BR)
* [Documentação do Adobe Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=pt-BR)
* [Documentação do Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html?lang=pt-BR)
* [Documentação do SDK móvel da Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
