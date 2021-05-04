---
title: Audience Activation Blueprint online/offline
description: Audience Activation online/offline.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
translation-type: tm+mt
source-git-commit: 61cb72965cd528cf264231058b1010829a87df9e
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 74%

---

# Audience Activation Blueprint online/offline

Use atributos e eventos offline, como pedidos, transações, dados de CRM ou de fidelização, com comportamentos online para direcionamento e personalização online.

Ative públicos para destinos conhecidos com base no perfil, como provedores de email, redes sociais e destinos de publicidade.

## Casos de uso

* Direcionamento de públicos para públicos conhecidos em destinos sociais e de publicidade.
* Personalização online com atributos online e offline.
* Ative públicos para canais conhecidos, como email e SMS.

## Aplicativos

* Adobe Experience Platform
* [!UICONTROL Plataforma de dados do cliente em tempo real]

## Arquitetura

### Audience Activation online/offline com destinos

<img src="assets/online_offline_activation.svg" alt="Arquitetura de referência para o Blueprint de Audience Activation online/offline" style="border:1px solid #4a4a4a" />

### Audience Activation on-line/off-line com aplicativos Experience Cloud

<img src="assets/activation+apps.svg" alt="Arquitetura de referência para o Blueprint Audience Activation online/offline com aplicativos Experience Cloud" style="border:1px solid #4a4a4a" />

## Medidas de proteção

Consulte as grades de proteção conforme descrito na página Visão geral de público-alvo e ativação de perfil - [LINK](overview.md)

## Etapas de implementação

1. Configure esquemas e conjuntos de dados na Experience Platform.
1. Configure as identidades certas e os namespaces de identidade no esquema para assegurar que os dados assimilados possam aderir a um perfil unificado.
1. Habilite esquemas e conjuntos de dados para o Perfil.
1. Assimile os dados na Platform.
1. Provisione [!UICONTROL Plataforma de dados do cliente em tempo real] o compartilhamento de segmentos entre o Experience Platform e o Audience Manager para que os públicos-alvo definidos no Experience Platform sejam compartilhados com o Audience Manager.
1. Crie Segmentos na Experience Platform para serem avaliados em lote ou por streaming. O sistema decide automaticamente se o segmento é avaliado em lote ou por streaming.
1. Configure destinos para compartilhar atributos de perfil e associações de públicos com destinos desejados.

## Considerações de implementação

* Compartilhar dados de perfil com destinos exige a inclusão de valor específico de identidade, usado pelo destino na carga de destino. Qualquer identidade necessária para um destino deve ser assimilada na Platform e configurada como uma identidade para o [!UICONTROL Perfil do cliente em tempo real].

* Para cenários de ativação em que os públicos são compartilhados da Experience Platform para o Audience Manager, todas as identidades incluídas no [!UICONTROL Perfil de cliente em tempo real] são compartilhadas com o Audience Manager. É possível compartilhar os públicos da Experience Platform por meio dos destinos do Audience Manager, quando as identidades de destino necessárias estiverem incluídas no [!UICONTROL Perfil de cliente em tempo real]. Ou também onde as identidades no [!UICONTROL Perfil de cliente em tempo real] possam ser relacionadas às identidades de destino vinculadas ao Audience Manager.

## Documentos relacionados

* [Descrição do produto Plataforma de dados do cliente em tempo real](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform.html)
* [Diretrizes de perfil e segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)
* [Documentação de segmentação](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=pt-BR)
* [Documentação de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=pt-BR)

## Vídeos e tutoriais relacionados

* [Visão geral da Plataforma de dados do cliente em tempo real](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=pt-BR)
* [[!UICONTROL Demonstração da Plataforma de dados do cliente em tempo real]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=pt-BR)
* [Criação de segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=pt-BR)
