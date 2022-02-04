---
title: Journey Optimizer - Blueprint de mensagens de terceiros
description: Demonstra como o Adobe Journey Optimizer pode ser usado com sistemas de mensagens de terceiros para orquestrar e enviar comunicações personalizadas.
solution: Experience Platform, Journey Optimizer
hidefromtoc: true
exl-id: 57e4d90a-61c9-444d-9bc5-40c7e58b4d21
source-git-commit: 13f750c0ff820ab01ed4fc615aba864bc2dc7b75
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 35%

---

# Mensagens de terceiros

Demonstra como o Adobe Journey Optimizer pode ser usado com sistemas de mensagens de terceiros para orquestrar e enviar comunicações personalizadas.

<br>

## Arquitetura

<img src="assets/3rd-party-messaging-architecture.svg" alt="Arquitetura de referência Journey Optimizer blueprint" style="width:100%; border:1px solid #4a4a4a" />

<br>

## Pré-requisitos

Adobe Experience Platform

* Os esquemas e conjuntos de dados devem ser configurados no sistema antes que você possa configurar as fontes de dados do Journey Optimizer
* Para esquemas baseados em classe do Experience Event, adicione o grupo de campos &#39;Orchestration eventID quando quiser que um evento seja acionado e não seja um evento baseado em regras
* Para esquemas baseados em classe de Perfil individual, adicione o grupo de campos &quot;Detalhes do teste de perfil&quot; para carregar perfis de teste para uso com o Journey Optimizer

Aplicativo de mensagens de terceiros

* Deve ser compatível com chamadas REST API para enviar cargas transacionais

<br>

## Medidas de proteção

[Link de produto do Journey Optimizer Guardrails](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=pt-BR)

Medidas de proteção adicionais do Journey Optimizer:

* O limite está disponível por meio da API hoje, para garantir que o sistema de destino não esteja saturado até o ponto de falha. Isso significa que as mensagens que excedem a tampa serão descartadas completamente e nunca serão enviadas. Não há suporte para limitação.
   * Conexões máximas - número máximo de conexões http/s que um destino pode lidar
   * Contagem máxima de chamadas - número máximo de chamadas a serem feitas no parâmetro periodInMs
   * periodInMs - tempo em milissegundos
* Jornadas iniciadas por associação de segmentos podem operar em dois modos:
   * Segmentos em lote (atualizados a cada 24 horas)
   * Segmentos de transmissão (qualificação de &lt;5mins)
* Segmentos em lote – precisam assegurar que você entenda o volume diário de usuários qualificados e que o sistema de destino possa lidar com a taxa de transferência intermitente por jornada e em todas as jornadas
* Segmentos por streaming – precisam assegurar que a intermitência inicial de qualificações de perfis possam ser manipuladas com o volume de qualificações de streaming diárias por jornada e em todas as jornadas
* offer decisioning sem suporte
* Integrações de saída para sistemas de terceiros
   * Não há suporte para um único IPs estáticos, pois nossa infraestrutura é de vários locatários (é necessário lista de permissões todos os IPs do data center)
   * Somente os métodos POST e PUT são compatíveis com ações personalizadas
   * Suporte de autenticação: token | senha | OAuth2
* Não é possível empacotar e mover componentes individuais do Adobe Experience Platform ou Journey Optimizer entre várias sandboxes. Deve reimplementar em novos ambientes

<br>

Sistema de mensagens de terceiros

* Precisa entender qual carga o sistema suporta para chamadas de API transacionais
   * Número de chamadas permitidas por segundo
   * Número de conexões
* Precisa entender qual autenticação é necessária para fazer chamadas de API
   * Tipo de autenticação:  token | senha | OAuth2 são compatíveis com Journey Optimizer
   * Duração do cache de autenticação:  por quanto tempo o token é válido? 
* Se a assimilação em lote for compatível somente, será necessário ser transmitida para um mecanismo de armazenamento em nuvem como o Amazon Kinesis ou o Azure Event Grid 1º
   * Os dados podem ser agrupados em lotes desses mecanismos de armazenamento em nuvem e canalizados para terceiros
   * Qualquer middleware necessário seria da responsabilidade do cliente ou de terceiros fornecer

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
1. Crie segmentos para uso da Jornada.

#### Origens/Destinos

1. [Assimile dados na Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) usando APIs de streaming e conectores de origem.

### Journey Optimizer

1. Configure sua fonte de dados do Experience Platform e determine quais campos devem ser armazenados em cache como parte dos dados profileStreaming usados para iniciar uma jornada do cliente devem ser configurados no Journey Optimizer primeiro para obter uma ID de orquestração. Depois, essa ID de orquestração será fornecida ao desenvolvedor para usá-la na assimilação
1. Configure as origens de dados externos
1. Configurar ações personalizadas para aplicativos de terceiros

### Configuração de push móvel (opcional, já que terceiros podem coletar tokens)

1. Implemente o SDK do Experience Platform Mobile para coletar tokens de push e informações de logon para se vincular a perfis de clientes conhecidos
1. Aproveite as Tags do Adobe e crie uma propriedade móvel com a seguinte extensão:
   * Adobe Journey Optimizer
   * Rede de borda da Adobe Experience Platform
   * Identidade para rede Edge
   * Mobile Core
1. Certifique-se de ter um conjunto de dados dedicado para implantações de aplicativos móveis e implantações da Web
1. Para obter mais informações, siga as [Guia do Adobe Journey Optimizer Mobile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)

<br>

## Documentação relacionada

* [Documentação do Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Documentação de tags da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en)
* [Documentação do SDK móvel da Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
* [Documentação do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR)
* [Descrição do produto Journey Optimizer](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
