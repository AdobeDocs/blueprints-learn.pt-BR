---
title: Blueprint de ativação de público-alvo online/offline
description: Ativação de público-alvo online/offline.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
source-git-commit: f527b23587e4ec893532997c3c99270946d7fa31
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 77%

---

# Blueprint de ativação de público-alvo online/offline

Use atributos e eventos offline, como pedidos, transações, dados de CRM ou de fidelização, com comportamentos online para direcionamento e personalização online.

Ative públicos para destinos conhecidos com base no perfil, como provedores de email, redes sociais e destinos de publicidade.

O Blueprint Audience Activation Online/Offline se alinha ao [Audience and Profile Ativation with Experience Cloud Applications Blueprint](platform-and-applications.md). Detalhes adicionais são fornecidos no [Audience and Profile Ativation with Experience Cloud Applications Blueprint](platform-and-applications.md)   específico para integrações entre aplicativos Experience Platform e Experience Cloud.

## Casos de uso

* Direcionamento de públicos para públicos conhecidos em destinos sociais e de publicidade.
* Personalização online com atributos online e offline.
* Ative públicos para canais conhecidos, como email e SMS.

## Aplicativos

* Adobe Experience Platform
* [!UICONTROL Plataforma de dados do cliente em tempo real]

## Arquitetura

### Audience Activation online/offline com destinos

<img src="assets/online_offline_activation.svg" alt="Arquitetura de referência para o blueprint de ativação de público-alvo online/offline" style="border:1px solid #4a4a4a" />
<br>

## Medidas de proteção

[Consulte as grades de proteção conforme descrito na página Visão geral de público-alvo e ativação de perfil .](overview.md)

## Etapas de implementação

1. [Crie esquemas para que os dados sejam assimilados.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html)
1. [Crie conjuntos de dados para que os dados sejam assimilados.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)
1. [Configure as identidades corretas e os namespaces de identidade no esquema para assegurar que os dados assimilados possam aderir a um perfil unificado.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html)
1. [Ative os esquemas e conjuntos de dados para perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Assimile dados na Experience Platform.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion)
1. [Forneça compartilhamento de segmentos da [!UICONTROL Plataforma de dados do cliente em tempo real] entre a Experience Platform e o Audience Manager. Assim, os públicos definidos na Experience Platform podem ser compartilhados com o Audience Manager.](https://www.adobe.com/go/audiences)
1. [Criar ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=pt-BR) segmentos no Experience Platform. O sistema decide automaticamente se o segmento é avaliado em lote ou por streaming.
1. [Configure destinos para compartilhar atributos de perfil e associações de públicos com destinos desejados.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html)

## Considerações de implementação

* Compartilhar dados de perfil com destinos exige a inclusão de valor específico de identidade, usado pelo destino na carga de destino. Qualquer identidade necessária para um destino de público-alvo deve ser assimilada na Platform e configurada como uma identidade para o [!UICONTROL Perfil de cliente em tempo real].

* Para cenários de ativação em que os públicos são compartilhados da Experience Platform para o Audience Manager, todas as identidades incluídas no [!UICONTROL Perfil de cliente em tempo real] são compartilhadas com o Audience Manager. É possível compartilhar os públicos da Experience Platform por meio dos destinos do Audience Manager, quando as identidades de destino necessárias estiverem incluídas no [!UICONTROL Perfil de cliente em tempo real]. Ou também onde as identidades no [!UICONTROL Perfil de cliente em tempo real] possam ser relacionadas às identidades de destino vinculadas ao Audience Manager.

## Documentação relacionada

* Descrição do produto [[!UICONTROL Plataforma de dados do cliente em tempo real]](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform.html)
* [Guias de perfil e segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)
* [Documentação de segmentação](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=pt-BR)
* [Documentação de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=pt-BR)

## Vídeos e tutoriais relacionados

* Visão geral da [[!UICONTROL Plataforma de dados do cliente em tempo real]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=pt-BR)
* [Demonstração da [!UICONTROL Plataforma de dados do cliente em tempo real]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=pt-BR)
* [Criação de segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
