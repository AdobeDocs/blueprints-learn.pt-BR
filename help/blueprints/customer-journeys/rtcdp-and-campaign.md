---
title: Padrão de integração do Real-Time CDP com o Adobe Campaign
description: Mostra como a Adobe Experience Platform, seu Perfil do cliente em tempo real e sua ferramenta de segmentação centralizada podem ser usados com o Adobe Campaign para proporcionar conversas personalizadas.
solution: Real-time Customer Data Platform, Campaign
exl-id: a15e8304-2763-42fc-9978-11f2482ea8b8
source-git-commit: 24d5ec498d09f6dac443561bd530d58a33dae7af
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 100%

---

# Padrão de integração do Real-Time CDP com o Adobe Campaign

Mostra como a Adobe Experience Platform, seu Perfil do cliente em tempo real e sua ferramenta de segmentação centralizada podem ser usados com o Adobe Campaign para proporcionar conversas personalizadas.

<br>

## Aplicativos

* Real-Time CDP da Adobe Experience Platform
* Adobe Campaign v7 ou Campaign Standard

<br>

## Arquitetura

<img src="assets/rtcdp-campaign-architecture.svg" alt="Arquitetura de referência para o padrão de integração de mensagens em lote e Adobe Experience Platform" style="width:100%; border:1px solid #4a4a4a" />

<br>

## Pré-requisitos

* Recomenda-se que o Experience Platform e o Campaign sejam provisionados na mesma organização IMS e usem o Adobe Admin Console para o acesso de usuários. Isso também garante que clientes possam utilizar o alternador de soluções a partir da interface do usuário de marketing

<br>

## Medidas de proteção

### Adobe Campaign

* Compatível somente com implantações de uma única entidade organizacional do Adobe Campaign
* O Adobe Campaign é a fonte confiável para todos os perfis ativos. Isso significa que os perfis devem existir no Adobe Campaign e que novos perfis não devem ser criados com base em segmentos da Experience Platform.
* O Campaign exporta fluxos de trabalho para serem executados no máximo a cada 4 horas
* O esquema XDM e os conjuntos de dados para broadLog, trackingLogs e endereços sem entrega do Adobe Campaign não vêm prontos para uso e devem ser projetados e criados

### Compartilhamento de segmento do Experience Platform CDP

* Recomendação de limite de 20 segmentos
* A ativação é limitada a cada 24 horas
* Somente atributos de esquema de união estão disponíveis para ativação (sem suporte para array/mapas/eventos de experiência)
* Recomendação de não ultrapassar 20 atributos por segmento
* Um arquivo por segmento de todos os perfis com associação de segmentos “realizada”. OU, se a associação de segmentos estiver adicionada como um atributo no arquivo, nos perfis “realizada” e “encerrada”
* Exportações incrementais e de segmentos completos são compatíveis
* A criptografia de arquivos não é compatível

<br>

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

1. [Assimile dados na Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) usando APIs de transmissão e conectores de origem.
1. Configure o destino do armazenamento de blobs do [!DNL Azure] para usar com o Adobe Campaign.

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


### Configuração de push para publicação de conteúdo para dispositivos móveis

* Duas abordagens compatíveis de integração com dispositivos móveis para notificações por push:
   * SDK móvel da Experience Platform
   * SDK móvel do Campaign
* Roteiro do SDK móvel da Experience Platform:
   * Aproveite as tags da Adobe e a extensão do Campaign Classic para configurar sua integração ao SDK móvel da Experience Platform
   * Requer conhecimento prático sobre coleção de dados e tags da Adobe
   * Requer experiência de desenvolvimento móvel com notificações por push no Android e no iOS para implantar o SDK, integrar ao FCM (Android) e ao APNS (iOS) para obter o token por push, configurar o aplicativo para receber notificações por push e manipular interações por push
* SDK móvel do Campaign
   * Siga a [Documentação do SDK do Campaign] (para SDK móvel do Campaign, siga a documentação de implantação descrita aqui)

   >[!IMPORTANT]
   >Se você implantar o SDK do Campaign e estiver trabalhando com outros aplicativos da Experience Cloud, eles exigirão o uso do SDK móvel da Experience Platform para a coleção de dados. Isso criará chamadas do lado do cliente duplicadas no dispositivo.

## Documentação relacionada

* [Documentação da Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Documentação do Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=pt-BR)
* [Documentação do Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=pt-BR)
* [Documentação do Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html?lang=pt-BR)
* [Documentação do SDK móvel da Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
