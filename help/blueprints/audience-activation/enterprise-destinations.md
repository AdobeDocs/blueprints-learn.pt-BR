---
title: Ativação de público-alvo e perfil para o blueprint de destinos por streaming de arquivos e empresas
description: Ativação de público-alvo e perfil para destinos corporativos
solution: Real-Time Customer Data Platform
kt: 7475
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5
source-git-commit: 8355a36a235d847a6faf2398f3fadbed28ccac37
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 73%

---

# Ativação de público-alvo e perfil para o blueprint de destinos por streaming de arquivos e empresas

Compartilhe alterações de perfil e público-alvo e eventos em streaming ou lote de [!UICONTROL Real-time Customer Data Platform] para armazenamentos e aplicativos de dados corporativos. Esses eventos de perfil e público-alvo podem ser usados para iniciar uma ação de vendas ou suporte ao cliente, como acompanhar um processo de aplicativo abandonado ou registro de webinar ou atualizar aplicativos corporativos com os atributos e informações mais recentes do cliente [!UICONTROL Real-time Customer Data Platform].

## Casos de uso

* Ativação de perfil e público-alvo para destinos de armazenamento na nuvem ou destinos de streaming para empresas que fazem rastreamento, armazenamento, análise e ativação de dados e insights do cliente.

## Aplicativos

* Adobe Experience Platform    Activation

## Arquitetura

<img src="assets/enterprise_destination_activation.svg" alt="Arquitetura de referência para cenários de ativação empresarial" style="width:90%; border:1px solid #4a4a4a" />


## Medidas de proteção

[Consulte as medidas de proteção descritas na página de Visão geral de ativação de público e perfil.](overview.md)

## Etapas de implementação

1. [Crie esquemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=pt-BR) para que os dados sejam assimilados.
1. [Crie conjuntos de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) para que os dados sejam assimilados.
1. [Configure as identidades corretas e os namespaces de identidade](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR) no esquema para assegurar que os dados assimilados possam aderir a um perfil unificado.
1. [Habilite os esquemas e conjuntos de dados para o perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=pt-BR).
1. [Assimile dados](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) na Experience Platform.
1. [Provisionamento [!UICONTROL Real-time Customer Data Platform] compartilhamento de segmentos](https://www.adobe.com/go/audiences) entre o Experience Platform e o Audience Manager para os públicos-alvo definidos no Experience Platform a serem compartilhados com o Audience Manager.
1. [Crie segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=pt-BR) na Experience Platform. O sistema decide automaticamente se o segmento é avaliado em lote ou por transmissão.
1. [Configure destinos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html?lang=pt-BR) para compartilhar atributos de perfil e associações de públicos com destinos desejados.

## Documentação relacionada

* [Documentação de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=pt-BR)
* [Visão geral dos destinos de armazenamento na nuvem](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=pt-BR#catalog)
* [Destino HTTP](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/http-destination.html?lang=pt-BR#overview)
* [[!UICONTROL Real-time Customer Data Platform] Descrição do produto](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform.html)
* [Guias de perfil e segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)
* [Documentação de segmentação](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=pt-BR)

## Vídeos e tutoriais relacionados

* [[!UICONTROL Real-time Customer Data Platform] visão geral](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=pt-BR)
* [Demonstração do [!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=pt-BR)
* [Criação de segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=pt-BR)
