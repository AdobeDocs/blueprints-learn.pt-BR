---
title: Mensagens acionadas e Adobe Experience Platform Blueprint
description: Execute mensagens e experiências acionadas usando o Adobe Experience Platform como um hub central de dados de transmissão, perfis de clientes e segmentação.
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
exl-id: 97831309-f235-4418-bd52-28af815e1878
translation-type: tm+mt
source-git-commit: 009a55715b832c3167e9a3413ccf89e0493227df
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 1%

---

# Mensagens acionadas e Adobe Experience Platform Blueprint

Execute mensagens e experiências acionadas usando o Adobe Experience Platform como um hub central de dados de transmissão, perfis de clientes e segmentação.

## Casos de uso

* Mensagens acionadas
* Confirmações de registro
* abandonos de carrinho de compras e formulário de aplicativo
* Mensagens acionadas pelo local

## Arquitetura

<img src="assets/triggered.svg" alt="Arquitetura de referência para o blueprint do Triggered Messaging e do Adobe Experience Platform" style="border:1px solid #4a4a4a" />

## Padrões de integração

* Adobe Experience Platform -> Journey Orchestration

## Pré-requisitos

* Adobe Experience Platform
* Journey Orchestration

## Medidas de proteção

### Journey Orchestration

* Consulte o link para [mais detalhes sobre limitações](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=en#starting-with-journeys)
* O limite está disponível por meio da configuração da API para garantir que o sistema de destino não esteja saturado até o ponto de falha. Limpar significa que as mensagens que excedem a tampa são descartadas completamente e nunca são enviadas. A limitação ainda não é suportada.
   * conexões máximas: Número máximo de conexões http/s que um destino pode manipular
   * contagem máxima de chamadas: Número máximo de chamadas a serem feitas no parâmetro periodInMs
   * periodInMs: Tempo em milissegundos
* As jornadas iniciadas de associação de segmento podem operar em dois modos:
   * segmentos em lote (atualizados a cada 24 horas)
   * Segmentos de transmissão (qualificação de menos de 5 minutos)
* Segmentos em lote: Certifique-se de entender o volume diário de usuários qualificados e garantir que o sistema de destino possa lidar com a taxa de transferência de explosão por jornada e em todas as jornadas
* Segmentos de transmissão: Certifique-se de que a explosão inicial das qualificações de perfil possa ser tratada junto com o volume de qualificação de streaming diário por jornada e em todas as jornadas
* O destino final deve suportar REST API e carga JSON
* Não suporta o Offer Decisioning atualmente
* Consulte [medidas de proteção de ingestão de perfil e dados para Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)

### Campaign Standard

* Só é compatível com 14 tps (50k por hora) na taxa de transferência
* Jornadas iniciadas por associação de segmentos não são suportadas
* Os eventos de reação a aberturas/cliques de mensagem transacional são suportados no Journey Orchestration.
* Os logs de mensagens transacionais não são sincronizados nativamente com o Experience Platform no momento, exigindo uma configuração manual. É recomendável exportar logs no máximo a cada quatro horas.


## Etapas da implementação

### Adobe Experience Platform

#### Esquema/Conjuntos de dados

1. Configure perfis individuais, eventos de experiência e esquemas de várias entidades no Experience Platform com base nos dados fornecidos pelo cliente.
1. Criar esquemas do Campaign para o seguinte: broadLog, trackingLog, endereços não entregues e preferências de perfil (opcional).
1. Adicione rótulos de uso de dados ao conjunto de dados para governança.
1. Crie políticas para impor a governança em destinos.

#### Perfil/identidade

1. Crie quaisquer namespaces específicos do cliente.
1. Adicionar identidades a esquemas.
1. Habilitar esquemas e conjuntos de dados para perfis.
1. Configure regras de mesclagem para diferentes exibições de [!UICONTROL Real-time Customer Profile] (opcional).
1. Crie segmentos para uso da campanha.

#### Fontes/Destinos

1. Insira dados no Experience Platform usando APIs de fluxo e conectores de origem.
1. Configure o [!DNL Azure] destino de armazenamento de blobs para uso com o Campaign.

#### Implantação de aplicativo móvel

1. Implemente o SDK do Campaign para Campaign Classic ou Experience Platform SDK para Campaign Standard. Se o Experience Platform Launch estiver presente, a recomendação é usar a extensão Campaign Classic/Standard com o SDK do Experience Platform.


### Journey Orchestration

1. Os dados de transmissão usados para iniciar uma jornada do cliente devem ser configurados no Journey Orchestration primeiro para obter uma ID de orquestração. Essa ID de orquestração é fornecida ao desenvolvedor para uso com a assimilação.
1. Configure fontes de dados externas.
1. Configure as ações personalizadas.

### Campaign Standard

1. Configure os templates de mensagens com as configurações de personalização apropriadas.
1. Configurar workflows de exportação exportar logs de mensagens transacionais. A recomendação é ser executada no máximo a cada quatro horas.


## Documentação relacionada

* [Documentação do Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Documentação do Journey Orchestration](https://experienceleague.adobe.com/docs/journey-orchestration.html?lang=en)
* [Documentação do Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [Documentação do Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [Documentação do Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Documentação do SDK do Experience Platform Mobile](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
