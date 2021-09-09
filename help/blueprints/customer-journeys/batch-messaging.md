---
title: Blueprint de mensagens em lote e Adobe Experience Platform
description: Crie campanhas com mensagens em lote e programadas usando a Adobe Experience Platform como hub central para perfis de clientes e segmentação.
solution: Experience Platform, Campaign
kt: 7196
exl-id: 4e55218c-c158-4f78-9f0b-c03528d992fa
source-git-commit: 3c950cebaa25901ae50433775c510ed834d8bcd5
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 99%

---

# Blueprint de mensagens em lote e Adobe Experience Platform

Crie campanhas com mensagens em lote e programadas usando a Adobe Experience Platform como hub central para perfis de clientes e segmentação.

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

<img src="assets/aepbatch.svg" alt="Arquitetura de referência para o Blueprint de mensagens em lote e Adobe Experience Platform" style="border:1px solid #4a4a4a" />

## Medidas de proteção

* Compatível somente com implantações de uma única unidade organizacional do Adobe Campaign
* O Adobe Campaign é a fonte confiável para todos os perfis ativos. Isso significa que os perfis devem existir no Adobe Campaign e que novos perfis não devem ser criados com base em segmentos da Experience Platform.
* A associação de segmentos da Experience Platform é latente tanto para lotes (um por dia) quanto para streaming (cerca de 5 minutos)

Compartilhamento de segmentos da **[!UICONTROL Plataforma de dados do cliente em tempo real] com o Adobe Campaign:**

* Recomendação de limite de 20 segmentos
* A ativação é limitada a cada 24 horas
* Somente atributos de esquema de união estão disponíveis para ativação (sem suporte para array/mapas/eventos de experiência).
* Recomendação de não ultrapassar 20 atributos por segmento
* Um arquivo por segmento de todos os perfis com associação de segmentos “realizada”. OU, se a associação de segmentos estiver adicionada como um atributo no arquivo, nos perfis “realizada” e “encerrada”
* Exportações incrementais ou de segmentos completos são compatíveis
* A criptografia de arquivos não é compatível
* Fluxos de trabalho de exportação do Adobe Campaign para serem executados no máximo a cada 4 horas
* Consulte [medidas de proteção para assimilação de dados e perfis na Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)

## Etapas de implementação

### Adobe Experience Platform

#### Esquema/Conjuntos de dados

1. [Configure perfil individual, evento de experiência e esquemas de várias entidades](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) na Experience Platform com base nos dados fornecidos pelo cliente.
1. Crie esquemas do Adobe Campaign para broadLog, trackingLog, endereços sem entrega e preferências de perfil (opcional).
1. [Crie conjuntos de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) na Experience Platform para que os dados sejam assimilados.
1. [Adicione rótulos de uso de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=pt-BR) na Experience Platform para o conjunto de dados para governança.
1. [Crie políticas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=pt-BR) que apliquem governança nos destinos.

#### Perfil/Identidade

1. [Crie qualquer namespace específico para clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR).
1. [Adicione identidades a esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Habilite os esquemas e conjuntos de dados para o Perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=pt-BR).
1. [Configure políticas de mesclagem](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=pt-BR) para visualizações diferentes do [!UICONTROL Perfil de cliente em tempo real] (opcional).
1. Crie segmentos para o uso do Adobe Campaign.

#### Origens/Destinos

1. [Assimile dados na Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) usando APIs de streaming e conectores de origem.
1. Configure o destino do armazenamento de blobs do [!DNL Azure] para usar com o Adobe Campaign.

#### Implantação de aplicativo para dispositivos móveis

1. Implemente o SDK do Adobe Campaign para o Adobe Campaign Classic ou o SDK da Experience Platform para o Adobe Campaign Standard. Se o Experience Platform Launch estiver presente, recomenda-se usar a extensão do Adobe Campaign Classic ou o Adobe Campaign Standard com o SDK da Experience Platform.

#### Adobe Campaign

1. Configure esquemas para perfil, dados de pesquisa e dados relevantes de personalização de entrega.

>[!IMPORTANT]
>
>À esta altura, é fundamental entender que modelo de dados está contido na Experience Platform para dados de perfil e de eventos. Assim é possível saber quais dados serão necessários no Adobe Campaign.

#### Importação de fluxos de trabalho

1. Carregue e assimile dados de perfil simplificados no sFTP do Adobe Campaign.
1. Carregue e assimile dados de personalização de mensagens e orquestrações no sFTP do Adobe Campaign.
1. Assimile segmentos da Experience Platform do blob do [!DNL Azure] por meio de fluxos de trabalho.

#### Exportação de fluxos de trabalho

1. Devolva logs do Adobe Campaign à Experience Platform por meio de fluxos de trabalho a cada quatro horas (broadLog, trackingLog, endereços sem entrega).
1. Devolva preferências de perfil à Experience Platform por meio de fluxos de trabalho criados por consultas a cada quatro horas (opcional).


## Documentação relacionada

* [Documentação da Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Documentação do Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=pt-BR)
* [Documentação do Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=pt-BR)
* [Documentação do Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html?lang=pt-BR)
* [Documentação do SDK móvel da Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
