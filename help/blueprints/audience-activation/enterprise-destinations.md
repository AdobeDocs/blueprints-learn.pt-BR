---
title: Audience and Profile Ativation to Enterprise Destinations Blueprint
description: Audience and Profile Ativation to Enterprise Destinations
solution: Experience Platform,Real-time Customer Data Platform
kt: 7475
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5,None
translation-type: tm+mt
source-git-commit: 762836aba236ed78f4f396e8521a99c775dd52fc
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 43%

---

# Audience and Profile Ativation to Enterprise Destinations Blueprint

Compartilhe alterações de perfil e público-alvo e eventos em streaming ou lote da [!UICONTROL Plataforma de dados do cliente em tempo real] para armazenamentos e aplicativos de dados corporativos. Esses eventos de perfil e público-alvo podem ser usados para iniciar uma ação de vendas ou suporte ao cliente, como acompanhar um processo de aplicativo abandonado ou registro de webinar ou atualizar aplicativos corporativos com os atributos e informações mais recentes do cliente da [!UICONTROL Plataforma de dados do cliente em tempo real].

## Casos de uso

* Ativação de perfil e público-alvo para destinos de armazenamento em nuvem ou destinos de fluxo para rastreamento, armazenamento, análise e ativação de dados e insights do cliente em empresas.

## Aplicativos

* Adobe Experience Platform Ativation

## Arquitetura

<img src="assets/enterprise_destination_activation.svg" alt="Arquitetura de referência para o cenário de Ativação Empresarial" style="border:1px solid #4a4a4a" />


## Medidas de proteção

Consulte as grades de proteção conforme descrito na página Visão geral de público-alvo e ativação de perfil - [LINK](overview.md)

## Etapas de implementação

1. [Crie ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html) esquemas para os dados que serão assimilados.
1. [Crie ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) conjuntos de dados para que os dados sejam assimilados.
1. [Configure as identidades certas e os namespaces de identidade no esquema para assegurar que os dados assimilados possam aderir a um perfil unificado.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html)
1. [Habilite esquemas e conjuntos de dados para o Perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Assimile os dados na Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion).
1. [Forneça compartilhamento de segmentos da plataforma de dados do cliente em tempo real entre a Experience Platform e o Audience Manager. Assim, os públicos definidos na Experience Platform podem ser compartilhados com o Audience Manager.](https://www.adobe.com/go/audiences)
1. [Crie segmentos no Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=pt-BR), que serão avaliados em lote ou streaming. O sistema decide automaticamente se o segmento é avaliado em lote ou por streaming.
1. [Configure destinos para compartilhar atributos de perfil e associações de públicos com destinos desejados.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html)

## Documentos relacionados

* [Documentação de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=pt-BR)
* [Visão geral dos destinos de armazenamento na nuvem](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=en#catalog)
* [Destino HTTP](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/http-destination.html?lang=en#overview)
* [Descrição do produto Plataforma de dados do cliente em tempo real](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform.html)
* [Diretrizes de perfil e segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)
* [Documentação de segmentação](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=pt-BR)

## Vídeos e tutoriais relacionados

* [Visão geral da Plataforma de dados do cliente em tempo real](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=pt-BR)
* [[!UICONTROL Demonstração da Plataforma de dados do cliente em tempo real]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=pt-BR)
* [Criação de segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
