---
title: Mensagens em lote e Adobe Experience Platform Blueprint
description: Faça campanhas com mensagens em lote e programadas usando a Adobe Experience Platform como hub central para perfis de clientes e segmentação.
solution: Experience Platform, Campaign
kt: 7196
exl-id: 4e55218c-c158-4f78-9f0b-c03528d992fa
translation-type: tm+mt
source-git-commit: 81df87f850b7ac4be9dce7a3b96d39a3a47685c5
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 51%

---

# Mensagens em lote e Adobe Experience Platform Blueprint

Faça campanhas com mensagens em lote e programadas usando a Adobe Experience Platform como hub central para perfis de clientes e segmentação.

## Casos de uso

* Campanhas de email programadas
* Campanhas de integração e de remarketing

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
* A associação de segmentos da Experience Platform é latente tanto para lotes (1 por dia) quanto para streaming (~5 minutos)

**[!UICONTROL Compartilhamento de segmentos da ] plataforma de dados do cliente em tempo real com a Adobe Campaign:**

* Recomendação de limite de 20 segmentos
* A ativação é limitada a cada 24 horas
* Somente atributos de esquema de união estão disponíveis para ativação (sem suporte para array/mapas/eventos de experiência).
* Recomendação de não ultrapassar 20 atributos por segmento
* Um arquivo por segmento de todos os perfis com associação de segmentos “realizada”. OU, se a associação de segmentos estiver adicionada como um atributo no arquivo, nos perfis “realizada” e “encerrada”
* Exportações incrementais ou de segmentos completos são compatíveis
* A criptografia de arquivos não é compatível
* Workflows para exportação do Adobe Campaign a serem executados no máximo a cada 4 horas
* Consulte [medidas de proteção para assimilação de dados e perfis na Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)

## Etapas de implementação

### Adobe Experience Platform

#### Esquema/Conjuntos de dados

1. [Configure perfil individual, evento de experiência e esquemas de várias entidades na Experience Platform com base nos dados fornecidos pelo cliente.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html)
1. Crie esquemas do Adobe Campaign para broadLog, trackingLog, endereços não entregues e preferências de perfil (opcional).
1. [Crie ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) conjuntos de dados no Experience Platform para que os dados sejam assimilados.
1. [Adicione ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html) rótulos de uso de dados no Experience Platform ao conjunto de dados para controle.
1. [Crie políticas que apliquem governança nos destinos.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html)

#### Perfil/Identidade

1. [Crie qualquer namespace específico para clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Adicione identidades a esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Habilite esquemas e conjuntos de dados para o Perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Configure ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html) políticas de mesclagem para diferentes visualizações do Perfil do cliente em tempo  [!UICONTROL real]  (opcional).
1. Crie segmentos para uso do Adobe Campaign.

#### Origens/Destinos

1. [Assimile dados na Experience Platform usando APIs de streaming e conectores de origem.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion)
1. Configure o [!DNL Azure] destino de armazenamento de blobs para uso com o Adobe Campaign.

#### Implantação de aplicativo para dispositivos móveis

1. Implemente o SDK do Adobe Campaign para Adobe Campaign Classic ou Experience Platform SDK para Adobe Campaign Standard. Se o Experience Platform Launch estiver presente, a recomendação é usar a extensão Adobe Campaign Classic ou Adobe Campaign Standard com o Experience Platform SDK.

#### Adobe Campaign

1. Configure esquemas para perfil, dados de pesquisa e dados relevantes de personalização de entrega.

>[!IMPORTANT]
>
>É importante entender neste momento qual é o modelo de dados no Experience Platform para dados de perfil e evento, para que você saiba quais dados serão exigidos no Adobe Campaign.

#### Importação de fluxos de trabalho

1. Carregar e assimilar dados de perfil simplificados no Adobe Campaign sFTP.
1. Carregue e assimile dados de personalização de orquestração e mensagens no Adobe Campaign sFTP.
1. Assimile segmentos da Experience Platform do blob do [!DNL Azure] por meio de fluxos de trabalho.

#### Exportação de fluxos de trabalho

1. Envie logs do Adobe Campaign de volta para o Experience Platform via workflows a cada quatro horas (broadLog, trackingLog, endereços não entregues).
1. Devolva preferências de perfil à Experience Platform por meio de fluxos de trabalho criados por consultas a cada quatro horas (opcional).


## Documentos relacionados

* [Documentação da Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Documentação do Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=pt-BR)
* [Documentação do Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=pt-BR)
* [Documentação do Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html?lang=pt-BR)
* [Documentação do SDK móvel da Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
