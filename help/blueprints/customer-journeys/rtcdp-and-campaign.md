---
title: Real-Time CDP com [!DNL Campaign] Padrão de integração v7 e Campaign Standard
description: Mostra como a Adobe Experience Platform e seu Perfil do cliente em tempo real e a ferramenta de segmentação centralizada podem ser utilizados com o Adobe [!DNL Campaign] para fornecer conversas personalizadas.
solution: Real-Time Customer Data Platform, [!DNL Campaign]
exl-id: a15e8304-2763-42fc-9978-11f2482ea8b8
source-git-commit: 258aea64f6ff2f620b1adaa0c9ba4b02b47acce9
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 42%

---

# [!DNL Real-Time Customer Data Platform] com [!DNL Campaign] padrão de integração

Mostra como o Adobe [!DNL Experience Platform] e seu Perfil do cliente em tempo real e a ferramenta de segmentação centralizada podem ser utilizados com o Adobe [!DNL Campaign] para fornecer conversas personalizadas.

## Aplicativos

* Adobe [!DNL Experience Platform Real-Time Customer Data Platform]
* Adobe [!DNL Campaign] v7 ou [!DNL Campaign Standard]

## Arquitetura

<img src="assets/rtcdp-campaign-architecture.svg" alt="Arquitetura de referência para o padrão de integração de mensagens em lote e Adobe Experience Platform" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## Pré-requisitos

* EXPERIENCE PLATFORM e [!DNL Campaign] Recomenda-se que sejam provisionados na mesma Organização IMS e utilizem o Adobe Admin Console para acesso do usuário. Isso também garante que clientes possam utilizar o alternador de soluções a partir da interface do usuário de marketing

## Medidas de proteção

As seções a seguir descrevem as medidas de proteção para essa integração.

### Adobe [!DNL Campaign]

* Suporta apenas Adobe [!DNL Campaign] implantações de unidade organizacional única
* Adobe [!DNL Campaign] é a fonte da verdade para todos os perfis ativos, o que significa que os perfis devem existir no Adobe [!DNL Campaign] e novos perfis não devem ser criados com base em segmentos Experience Platform.
* [!DNL Campaign] exportar workflows para execução no máximo a cada 4 horas
* Esquema XDM e conjuntos de dados para o Adobe [!DNL Campaign] broadLog, trackingLogs e endereços não entregues não estão prontos para uso e devem ser projetados e criados

### Compartilhamento de segmentos do Real-time Customer Data Platform

* Consulte a RTCDP [!DNL Campaign] Conector de destino - [Conexão de Campanha RTCDP](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/adobe-campaign-managed-services.html?lang=pt-BR)

* Consulte [Medidas de proteção padrão para [!DNL Real-Time Customer Profile Data] e segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)

## Etapas de implementação

As seções a seguir descrevem as etapas de implementação para cada aplicativo.

### Adobe Experience Platform

#### Esquema/Conjuntos de dados

1. [Configure perfil individual, evento de experiência e esquemas de várias entidades](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=pt-BR) na Experience Platform com base nos dados fornecidos pelo cliente.
1. Criar Adobe [!DNL Campaign] esquemas para broadLog, trackingLog, endereços não entregues e preferências de perfil (opcional).
1. [Crie conjuntos de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) na Experience Platform para que os dados sejam assimilados.
1. [Adicione rótulos de uso de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=pt-BR) na Experience Platform para o conjunto de dados para governança.
1. [Crie políticas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=pt-BR) que apliquem governança nos destinos.

#### Perfil/identidade

1. [Crie qualquer namespace específico para clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR).
1. [Adicione identidades a esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR).
1. [Habilite os esquemas e conjuntos de dados para o Perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=pt-BR).
1. [Configure políticas de mesclagem](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=pt-BR) para visualizações diferentes do [!UICONTROL Perfil de cliente em tempo real] (opcional).
1. Criar segmentos para o Adobe [!DNL Campaign] uso.

#### Origens/destinos

1. [EXPERIENCE PLATFORM e [!DNL Campaign] Origens e destinos padrão](https://experienceleague.adobe.com/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/aep-sources-destinations/get-started-sources-destinations.html?lang=pt-BR)
1. [EXPERIENCE PLATFORM e [!DNL Campaign] Origens e destinos do v7](https://experienceleague.adobe.com/docs/campaign-classic/using/integrating-with-adobe-experience-cloud/aep-sources-destinations/get-started-sources-destinations.html?lang=pt-BR)
1. [Assimile dados na Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) usando APIs de transmissão e conectores de origem.
1. Configurar [!DNL Azure] destino de armazenamento de blobs para uso com o Adobe [!DNL Campaign].

#### Adobe [!DNL Campaign]

1. Configure esquemas para perfil, dados de pesquisa e dados relevantes de personalização de entrega.

>[!IMPORTANT]
>
>É essencial entender, nesse ponto, qual é o modelo de dados no Experience Platform para os dados de perfil e evento, para que você saiba quais dados serão necessários no Adobe [!DNL Campaign].

#### Importação de fluxos de trabalho

1. Carregar e assimilar dados de perfil simplificados no Adobe [!DNL Campaign] sFTP.
1. Carregar e assimilar dados de orquestração e personalização de mensagens no Adobe [!DNL Campaign] sFTP.
1. Assimile segmentos da Experience Platform do blob do [!DNL Azure] por meio de fluxos de trabalho.

#### Exportação de fluxos de trabalho

1. Enviar Adobe [!DNL Campaign] faz o logon no Experience Platform por meio de workflows a cada quatro horas (broadLog, trackingLog, endereços não entregues).
1. Devolva preferências de perfil à Experience Platform por meio de fluxos de trabalho criados por consultas a cada quatro horas (opcional).

### Configuração de push para publicação de conteúdo para dispositivos móveis

* Duas abordagens compatíveis de integração com dispositivos móveis para notificações por push:
   * SDK móvel da Experience Platform
   * [!DNL Campaign] SDK móvel
* Roteiro do SDK móvel da Experience Platform:
   * Aproveite as Tags do Adobe e o [!DNL Campaign Classic] extensão para configurar sua integração com o SDK móvel do Experience Platform
   * Requer conhecimento prático sobre coleção de dados e tags da Adobe
   * Requer experiência de desenvolvimento móvel com notificações por push no Android e no iOS para implantar o SDK, integrar ao FCM (Android) e ao APNS (iOS) para obter o token por push, configurar o aplicativo para receber notificações por push e manipular interações por push
* [!DNL Campaign] SDK móvel
   * Consulte a [Documentação do SDK do Campaign Classic](https://developer.adobe.com/client-sdks/solution/adobe-campaign-classic/)

>[!IMPORTANT]
>
>Se você implantar o [!DNL Campaign] e estiverem trabalhando com outros aplicativos Experience Cloud, exigirão o uso do SDK móvel do Experience Platform para a coleta de dados. Isso criará chamadas do lado do cliente duplicadas no dispositivo.

## Documentação relacionada

* [Adobe [!DNL Experience Platform] documentação](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [[!DNL Campaign Classic] documentação](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=pt-BR)
* [[!DNL Campaign Standard] documentação](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=pt-BR)
* [[!DNL Experience Platform] Documentação do Launch](https://experienceleague.adobe.com/docs/launch.html?lang=pt-BR)
* [[!DNL Experience Platform] Documentação do SDK móvel](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
