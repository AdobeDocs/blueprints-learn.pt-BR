---
title: Journey Optimizer - Esquema de mensagens de terceiros
description: Demonstra como o Adobe Journey Optimizer pode ser usado com sistemas de mensagens de terceiros para orquestrar e enviar comunicações personalizadas.
solution: Journey Optimizer
exl-id: 3a14fc06-6d9c-4cd8-bc5c-f38e253d53ce
source-git-commit: b18d491fdefc57762932d1570401b5437bf97c76
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 92%

---

# Esquema de mensagens de terceiros

Demonstra como o Adobe Journey Optimizer pode ser usado com sistemas de mensagens de terceiros para orquestrar e enviar comunicações personalizadas.

<br>

## Arquitetura

<img src="assets/3rd-party-messaging-architecture.svg" alt="Blueprint do Journey Optimizer com arquitetura de referência" style="width:100%; border:1px solid #4a4a4a" />

<br>

## Pré-requisitos

Adobe Experience Platform

* Os esquemas e conjuntos de dados devem ser configurados no sistema antes que você possa configurar as fontes de dados do Journey Optimizer
* Para esquemas do Experience Event baseados em classe, adicione o grupo de campos “eventID de orquestração” quando quiser acionar um evento que não seja baseado em regras
* Para esquemas de Perfil individual baseados em classe, adicione o grupo de campos “Detalhes do teste de perfil” para carregar perfis de teste a serem usados com o Journey Optimizer

Aplicativo de mensagens de terceiros

* Deve ser compatível com chamadas de API REST para enviar cargas transacionais

<br>

## Medidas de proteção

[Link do produto medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=pt-BR)

Medidas de proteção adicionais do Journey Optimizer:

* O limite agora está disponível por meio de API para garantir que o sistema de destino não esteja saturado ao ponto de falha. Isso significa que as mensagens que excederem o limite serão completamente removidas sem ser enviadas. A regulagem não é compatível.
   * Conexões máximas – número máximo de conexões http/s com que um destino pode lidar
   * Contagem máxima de chamadas – número máximo de chamadas a serem realizadas no parâmetro periodInMs
   * periodInMs – tempo em milissegundos
* Jornadas iniciadas por associação de segmentos podem operar em dois modos:
   * Segmentos em lote (atualizados a cada 24 horas)
   * Segmentos de transmissão (qualificação de &lt; 5 minutos)
* Segmentos em lote – precisam assegurar que você entenda o volume diário de usuários qualificados e que o sistema de destino possa lidar com a taxa de transferência intermitente por jornada e em todas as jornadas
* Segmentos de transmissão – precisam assegurar que a intermitência inicial de qualificações de perfis possam ser manipuladas com o volume de qualificações de transmissão diárias por jornada e em todas as jornadas
* A gestão de decisões não é compatível
* Integrações de saída para sistemas de terceiros
   * Não há suporte para um único IP estático, pois nossa infraestrutura é multilocatária (é necessário incluir todos os IPs do data center na lista de permissões)
   * Somente os métodos POST e PUT são compatíveis com ações personalizadas
   * Suporte de autenticação: token | senha | OAuth2
* Não é possível empacotar e mover componentes individuais da Adobe Experience Platform ou do Journey Optimizer entre várias sandboxes. Em ambientes novos, deve ser implementado outra vez

<br>

Sistema de mensagens de terceiros

* É necessário entender qual carga o sistema suporta em chamadas de API transacionais
   * Número de chamadas permitidas por segundo
   * Número de conexões
* É preciso entender qual é a autenticação necessária para fazer chamadas de API
   * Tipo de autenticação: token | senha | OAuth2 são compatíveis com o Journey Optimizer
   * Duração do cache de autenticação: o token é válido por quanto tempo? 
* Se a assimilação em lote for apenas compatível e, então, precisar ser transmitida para um mecanismo de armazenamento na nuvem, como o Amazon Kinesis ou o Azure Event Grid 1st
   * Os dados podem ser agrupados em lotes desses mecanismos de armazenamento em nuvem e canalizados para terceiros
   * Qualquer middleware necessário seria da responsabilidade do cliente ou de terceiros fornecer

<br>

## Etapas de implementação

### Adobe Experience Platform

#### Esquema/conjuntos de dados

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

#### Fontes/destinos

1. [Assimile dados na Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) usando APIs de transmissão e conectores de origem.

### Journey Optimizer

1. Configure sua fonte de dados da Experience Platform e determine quais campos que devem ser armazenados em cache como parte dos dados de profileStreaming usados para iniciar uma jornada do cliente têm que ser primeiro configurados no Journey Optimizer para obter uma ID de orquestração. Depois, essa ID de orquestração será fornecida ao desenvolvedor para usá-la na assimilação
1. Configure as origens de dados externos
1. Configure ações personalizadas para aplicativos de terceiros

### Configuração de push móvel (opcional, pois tokens de terceiros podem ser coletados)

1. Implemente o SDK móvel da Experience Platform para coletar tokens de push e informações de logon a serem vinculadas a perfis de clientes conhecidos
1. Aproveite as tags da Adobe e crie uma propriedade de publicação de conteúdo para dispositivos móveis com a seguinte extensão:
   * Adobe Journey Optimizer
   * Rede de borda da Adobe Experience Platform
   * Identidade    para Edge Network
   * Mobile Core
1. Certifique-se de ter um fluxo de dados dedicado para implantações de aplicativos móveis e implantações da Web
1. Para mais informações, siga o [Manual do Adobe Journey Optimizer Mobile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)

<br>

## Documentação relacionada

* [Documentação da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Documentação de tags da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)
* [Documentação do SDK móvel da Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
* [Documentação do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR)
* [Descrição do produto do Journey Optimizer](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html)
