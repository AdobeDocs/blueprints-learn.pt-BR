---
title: Blueprint de mensagens acionadas e Adobe Experience Platform
description: Execute mensagens e experiências acionadas usando a Adobe Experience Platform como um hub central para dados de transmissão, perfis de clientes e segmentação.
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
exl-id: 97831309-f235-4418-bd52-28af815e1878
translation-type: ht
source-git-commit: 01f70fe432d7be38b71889ae19c0d5fe4cf0f78a
workflow-type: ht
source-wordcount: '694'
ht-degree: 100%

---

# Blueprint de mensagens acionadas e Adobe Experience Platform

Execute mensagens e experiências acionadas usando a Adobe Experience Platform como um hub central para dados de transmissão, perfis de clientes e segmentação.

## Casos de uso

* Mensagens acionadas
* Confirmações de registro
* Carrinho de compras e abandonos de formulários de aplicação
* Mensagens acionadas de localização

## Arquitetura

<img src="assets/triggered.svg" alt="Arquitetura de referência para o blueprint de mensagens acionadas e Adobe Experience Platform" style="border:1px solid #4a4a4a" />

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

1. [Configure perfil individual, evento de experiência e esquemas de várias entidades](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html?lang=pt-BR) na Experience Platform com base nos dados fornecidos pelo cliente.
1. Crie esquemas do Adobe Campaign para broadLog, trackingLog, endereços sem entrega e preferências de perfil (opcional).
1. [Crie conjuntos de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) na Experience Platform para que os dados sejam assimilados.
1. [Adicione rótulos de uso de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=pt-BR) na Experience Platform para o conjunto de dados para governança.
1. [Crie políticas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=pt-BR) que apliquem governança nos destinos.

#### Perfil/Identidade

1. [Crie qualquer namespace específico para clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR).
1. [Adicione identidades a esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR).
1. [Habilite os esquemas e conjuntos de dados para o Perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=pt-BR).
1. [Configure políticas de mesclagem](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=pt-BR) para visualizações diferentes do [!UICONTROL Perfil de cliente em tempo real] (opcional).
1. Crie segmentos para o uso do Adobe Campaign.

#### Origens/Destinos

1. [Assimile dados na Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) usando APIs de streaming e conectores de origem.1. Configure o destino de armazenamento do [!DNL Azure] blob para usar com o Adobe Campaign.

#### Implantação de aplicativo para dispositivos móveis

1. Implemente o SDK do Adobe Campaign para o Adobe Campaign Classic ou o SDK da Experience Platform para o Adobe Campaign Standard. Se o Experience Platform Launch estiver presente, recomenda-se usar a extensão do Adobe Campaign Classic ou o Adobe Campaign Standard com o SDK da Experience Platform.


### Journey Orchestration

1. Dados de streaming usados para inicializar uma jornada do cliente devem estar configurados primeiro dentro do Journey Orchestration para obter uma ID de orquestração. Depois, essa ID de orquestração será fornecida ao desenvolvedor para usá-la na assimilação.
1. Configure as origens de dados externos.
1. Configure as ações personalizadas.

### Adobe Campaign Standard

1. Configure os modelos de mensagens com as definições apropriadas de personalização.
1. Configure os fluxos de trabalho de exportação e exporte os logs de mensagens transacionais. A recomendação é executar no máximo a cada quatro horas.


## Documentação relacionada

* [Documentação da Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Documentação do Journey Orchestration](https://experienceleague.adobe.com/docs/journey-orchestration.html?lang=pt-BR)
* [Documentação do Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=pt-BR)
* [Documentação do Adobe Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=pt-BR)
* [Documentação do Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html?lang=pt-BR)
* [Documentação do SDK móvel da Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
