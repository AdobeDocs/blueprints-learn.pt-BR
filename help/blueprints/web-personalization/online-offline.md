---
title: Blueprint de personalização online/offline da Web
description: Sincronize a personalização da Web com emails e outras personalizações de canais conhecidos e anônimos.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7194thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
translation-type: tm+mt
source-git-commit: 9a52c5f9513e39b31956aaa0f30cad1426b63a95
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Blueprint de personalização online/offline Web/móvel

Sincronize a personalização da Web com emails e outras personalizações de canais conhecidos e anônimos.

## Casos de uso

* Aprimoramento da página de aterrissagem
* Direcionamento de perfis comportamentais e offline
* Personalização com base em visualizações anteriores de produtos/conteúdos, afinidade com produtos/conteúdos, características ambientais, dados de público-alvo de terceiros e dados demográficos, além de insights offline, como transações, dados de fidelização e de CRM e modelos de insights

## Aplicativos

* [!UICONTROL Plataforma de dados do cliente em tempo real]
* Adobe Target
* Adobe Audience Manager (opcional): adiciona dados do público-alvo de terceiros, gráfico de dispositivos com base em co-op, capacidade de apresentar segmentos da Platform no Adobe Analytics e de apresentar segmentos do Adobe Analytics na Platform
* Adobe Analytics (opcional): adiciona a capacidade de criar segmentos com base em dados comportamentais históricos e criar segmentação detalhada a partir dos dados do Adobe Analytics

## Arquitetura

<img src="assets/onoff.svg" alt="Arquitetura de referência para o Blueprint de personalização online/offline na Web" style="border:1px solid #4a4a4a" />

## Medidas de proteção

### Grades de proteção para avaliação e ativação de segmentos

| Tipo de segmentação | Frequência | Taxa de transferência | Latência (Avaliação de segmento) | Latência (Ativação de segmento) |
|---|---|---|---|---|
| Segmentação de borda | A segmentação de borda está atualmente em beta e permite que a segmentação válida em tempo real seja avaliada na rede de borda do Experience Platform para obter decisões de página em tempo real e em tempo real, por meio do Adobe Target e do Adobe Journey Optimizer. |  | ~100 ms | Disponível imediatamente para personalização no Adobe Target, para pesquisas de perfil no Perfil do Edge e para ativação via destinos baseados em cookies. |
| Segmentação por streaming | Toda vez que um novo evento ou registro de transmissão é assimilado no perfil do cliente em tempo real e a definição do segmento é um segmento de transmissão válido. <br>Consulte a  [documentação ](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=pt-BR) de segmentação para obter orientação sobre os critérios de segmento de streaming | Até 1500 eventos por segundo. | ~ p95 &lt;5 min | Depois que essas realizações de segmento ocorrem, elas são compartilhadas com o Audience Manager e o serviço de compartilhamento de público-alvo em minutos e disponibilizadas para a mesma/próxima personalização de página no Adobe Target. |
| Segmentação incremental | Uma vez por hora para novos dados que foram assimilados no perfil do cliente em tempo real desde a última avaliação de segmento incremental ou em lote. |  |  | Depois que essas associações de segmento forem realizadas, elas serão compartilhadas com o Audience Manager e o serviço de compartilhamento de público-alvo em minutos e estarão disponíveis para a mesma/próxima personalização de página no Adobe Target. |
| Segmentação em lote | Uma vez por dia, com base em um agendamento predeterminado do conjunto de sistemas ou no início manual da ad hoc por meio da API. |  | Aproximadamente uma hora por trabalho para até 10 TB de tamanho de armazenamento de perfil, 2 horas por trabalho para 10 TB a 100 TB de tamanho de armazenamento de perfil. O desempenho do trabalho do segmento em lote depende do número de perfis, do tamanho dos perfis e do número de segmentos que estão sendo avaliados. | Depois que essas associações de segmento forem realizadas, elas serão compartilhadas com o Audience Manager e o serviço de compartilhamento de público-alvo em minutos e estarão disponíveis para a mesma/próxima personalização de página no Adobe Target. |

### Grades de proteção para compartilhamento de público em aplicativos cruzados


| Padrão de integração de compartilhamento de público-alvo | Detalhe | Frequência | Taxa de transferência | Latência (Avaliação de segmento) | Latência (Ativação de segmento) |
|---|---|---|---|---|---|
| Plataforma de dados do cliente em tempo real para o Audience Manager |  | Dependendo do tipo de segmentação - consulte a tabela de medidas de proteção de segmentação acima. | Dependendo do tipo de segmentação - consulte a tabela de medidas de proteção de segmentação acima. | Dependendo do tipo de segmentação - consulte a tabela de medidas de proteção de segmentação acima. | Em minutos da conclusão da avaliação do segmento.<br>A sincronização da configuração inicial do público-alvo entre a Plataforma de dados do cliente em tempo real e o Audience Manager demora aproximadamente 4 horas.<br>Todas as associações de público-alvo realizadas durante o período de 4 horas serão gravadas no Audience Manager no trabalho subsequente de segmentação em lote como associações de público-alvo &quot;existentes&quot;. |
| Adobe Analytics para Audience Manager | Por padrão, um máximo de 75 públicos-alvo pode ser compartilhado para cada conjunto de relatórios do Adobe Analytics. Se uma licença do Audience Manager for usada, não há limite para o número de públicos-alvo que podem ser compartilhados entre o Adobe Analytics e o Adobe Target ou Adobe Audience Manager e Adobe Target. |  |  |  |  |
| Adobe Analytics para a plataforma de dados do cliente em tempo real | Não disponível no momento. |  |  |  |  |

## Padrões de implementação

O blueprint de personalização Web/Mobile pode ser implementado por meio das seguintes abordagens, conforme descrito abaixo.

1. Usando o [!UICONTROL SDK da Web da plataforma] ou [!UICONTROL SDK móvel da plataforma] e [!UICONTROL Rede de borda].
1. Uso de SDKs tradicionais específicos do aplicativo (por exemplo, AppMeasurement.js)

### 1. Plataforma Web/Mobile SDK e Abordagem de borda

<img src="assets/websdkflow.svg" alt="Arquitetura de referência para o [!UICONTROL Platform Web SDK] ou [!UICONTROL Platform Mobile SDK] e a abordagem [!UICONTROL Edge Network]" style="border:1px solid #4a4a4a" />

### 2. Abordagem do SDK específica do aplicativo

<img src="assets/appsdkflow.png" alt="Arquitetura de referência para abordagem do SDK específico para aplicativos" style="border:1px solid #4a4a4a" />

## Pré-requisitos de implementação

| Aplicativo/Serviço | Biblioteca necessária | Observações |
|---|---|---|
| Adobe Target | [!UICONTROL Plataforma Web SDK]*, at.js 0.9.1+ ou mbox.js 61+ | Preferência pela at.js, uma vez que a mbox.js não está mais sendo desenvolvida. |
| Adobe Audience Manager (opcional) | [!UICONTROL Plataforma Web SDK]* ou dil.js 5.0+ |  |
| Adobe Analytics (opcional) | [!UICONTROL Plataforma Web SDK]* ou AppMeasurement.js 1.6.4+ | O rastreamento do Adobe Analytics deve usar a Coleção de Dados Regionais (RDC). |
| Serviço da Experience Cloud ID | [!UICONTROL Plataforma Web SDK]* ou VisitorAPI.js 2.0+ | (Recomendado) Use o Experience Platform Launch para implantar o ID Service e assim garantir que a ID esteja configurada antes de qualquer chamada de aplicativo |
| SDK Móvel da Experience Platform (opcional) | Versão 4.11 ou posterior para iOS e Android™ |  |
| SDK da Web da Experience Platform | Versão 1.0. A versão atual do SDK da Experience Platform tem [vários casos de uso ainda não compatíveis com os aplicativos da Experience Cloud](https://github.com/adobe/alloy/projects/5) |  |


## Etapas de implementação

1. [Implemente o Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=pt-BR) para seus aplicativos da Web ou seus aplicativos para dispositivos móveis
1. [Implemente o Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=pt-BR) (opcional)
1. [Implemente o Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=pt-BR)  (opcional)
1. [[!UICONTROL Implemente a Experience Platform e o Perfil de cliente em tempo real]](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html?lang=pt-BR)
1. Implemente o [Identity Service da Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html?lang=pt-BR) ou o [SDK da Web da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR)
   >[!NOTE]
   >
   >Cada aplicativo deve usar a Experience Cloud ID e fazer parte da mesma organização da Experience Cloud, permitindo assim o compartilhamento de públicos entre os aplicativos.
1. [Solicite provisionamento para Compartilhamento de públicos-alvos entre a Experience Platform e o Adobe Target (Públicos compartilhados)](https://www.adobe.com/go/audiences)

## Documentos relacionados

* [Compartilhamento de segmentos da Experience Platform com o Audience Manager e outras soluções da Experience Cloud](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=pt-BR)
* [Visão geral da Segmentação da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=pt-BR)
* [Segmentação por streaming](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Visão geral do Construtor de segmentos da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=pt-BR)
* [Conector de origem do Audience Manager](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=pt-BR)
* [Compartilhamento de segmentos do Adobe Analytics por meio da Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=pt-BR)
* [Documentação do SDK da Web da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Documentação do serviço da Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR)
* [Documentação do Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/home.html?lang=pt-BR)

## Publicações do blog relacionadas

* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Build an Optimal Online Experience: Enrich Unified Profile with Query Service]](https://medium.com/adobetech/build-an-optimal-online-experience-enrich-unified-profile-with-query-service-8027c196ab33)
* [[!DNL Integrating Adobe Experience Platform Decisioning Engine with AEM Websites]](https://jaeness.medium.com/integrating-adobe-experience-platform-decisioning-engine-with-aem-websites-9c222acd12e2)
* [[!DNL Adobe Experience Platform’s Identity Service — How to Solve the Customer Identity Conundrum]](https://medium.com/adobetech/adobe-experience-platforms-identity-service-how-to-solve-the-customer-identity-conundrum-f95e22d16ea9)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our “Customer Zero” Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL How Adobe Experience Platform Can Help Customers Personalize Their Mobile Messaging in Real-Time with Journey Orchestration Service and a Mobile Messaging Vendor]](https://medium.com/adobetech/how-adobe-experience-platform-helped-a-client-personalize-their-mobile-messaging-in-real-time-with-7d634aefa098)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
* [[!DNL Build an Optimal Online Experience: Enrich Unified Profile with Query Service]](https://medium.com/adobetech/build-an-optimal-online-experience-enrich-unified-profile-with-query-service-8027c196ab33)
