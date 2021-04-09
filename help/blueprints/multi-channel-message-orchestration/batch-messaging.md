---
title: Mensagens em lote e Adobe Experience Platform Blueprint
description: Execute campanhas de mensagens programadas e em lote usando o Adobe Experience Platform como hub central para perfis e segmentação do cliente.
solution: Experience Platform, Campaign
kt: 7196
exl-id: 4e55218c-c158-4f78-9f0b-c03528d992fa
translation-type: tm+mt
source-git-commit: 37416aafc997838888edec2658d2621d20839f94
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Mensagens em lote e Adobe Experience Platform Blueprint

Execute campanhas de mensagens programadas e em lote usando o Adobe Experience Platform como hub central para perfis e segmentação do cliente.

## Casos de uso

* Campanhas de email programadas
* Campanhas de integração e remarketing

## Aplicativos

* Adobe Experience Platform
* Adobe Campaign Classic ou Standard

## Padrões de integração

* Adobe Experience Platform → Adobe Campaign Classic
* Adobe Experience Platform → Adobe Campaign Standard

## Arquitetura

<img src="assets/aepbatch.svg" alt="Arquitetura de referência para o Blueprint do Adobe Experience Platform e do Batch Messaging" style="border:1px solid #4a4a4a" />

## Medidas de proteção

* Suporta somente implantações de unidade organizacional única do Adobe Campaign
* O Adobe Campaign é a fonte de verdade para todos os perfis ativos, o que significa que eles devem existir no Adobe Campaign e novos perfis não devem ser criados com base em segmentos de Experience Platform.
* A realização de associação de segmento no Experience Platform é latente para lote (1 por dia) e streaming (~5 minutos)

**[!UICONTROL Compartilhamento de segmentos da ] plataforma de dados do cliente em tempo real com a Adobe Campaign:**

* Recomendação de limite de 20 segmentos
* A ativação é limitada a cada 24 horas
* Somente atributos de esquema de união disponíveis para ativação (sem suporte para eventos de matriz/mapas/experiência).
* Recomendação de no máximo 20 atributos por segmento
* Um arquivo por segmento de todos os perfis com associação de segmento &quot;realizada&quot; OU se a associação de segmento for adicionada como um atributo no arquivo tanto os perfis &quot;realizado&quot; quanto os &quot;concluídos&quot;
* Exportações de segmento incrementais ou completas são compatíveis
* Não há suporte para criptografia de arquivo
* Workflows para exportação do Adobe Campaign a serem executados no máximo a cada 4 horas
* Consulte [medidas de proteção de ingestão de perfil e dados para Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)

## Etapas da implementação

### Adobe Experience Platform

#### Esquema / Conjuntos de dados

1. Configure perfis individuais, eventos de experiência e esquemas de várias entidades no Experience Platform, com base nos dados fornecidos pelo cliente.
1. Crie esquemas do Adobe Campaign para broadLog, trackingLog, endereços não entregues e preferências de perfil (opcional).
1. Adicione rótulos de uso de dados ao conjunto de dados para governança.
1. Crie políticas que impõem a governança em destinos.

#### Perfil / identidade

1. Crie quaisquer namespaces específicos do cliente.
1. Adicionar identidades a esquemas.
1. Habilitar esquemas e conjuntos de dados para perfis.
1. Configure regras de mesclagem para diferentes exibições de [!UICONTROL Real-time Customer Profile] (opcional).
1. Crie segmentos para uso do Adobe Campaign.

#### Fontes / Destinos

1. Insira dados no Experience Platform usando APIs de fluxo e conectores de origem.
1. Configure o [!DNL Azure] destino de armazenamento de blobs para uso com o Adobe Campaign.

#### Implantação de aplicativo móvel

1. Implemente o SDK do Adobe Campaign para Adobe Campaign Classic ou Experience Platform SDK para Adobe Campaign Standard. Se o Experience Platform Launch estiver presente, a recomendação é usar a extensão Adobe Campaign Classic ou Adobe Campaign Standard com o Experience Platform SDK.

#### Adobe Campaign

1. Configure schemas para perfis, dados de pesquisa e dados relevantes de personalização do delivery.

>[!IMPORTANT]
>
>É importante entender neste momento qual é o modelo de dados no Experience Platform para dados de perfil e evento, para que você saiba quais dados serão exigidos no Adobe Campaign.

#### Importar workflows

1. Carregar e assimilar dados de perfil simplificados no Adobe Campaign sFTP.
1. Carregue e assimile dados de personalização de orquestração e mensagens no Adobe Campaign sFTP.
1. Assimilar segmentos de Experience Platform do blob [!DNL Azure] por workflows.

#### Exportar workflows

1. Envie logs do Adobe Campaign de volta para o Experience Platform via workflows a cada quatro horas (broadLog, trackingLog, endereços não entregues).
1. Envie as preferências de perfil de volta ao Experience Platform por meio de fluxos de trabalho criados por consultoria a cada quatro horas (opcional).


## Documentação relacionada

* [Documentação do Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Documentação do Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [Documentação do Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [Documentação do Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Documentação do SDK do Experience Platform Mobile](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
