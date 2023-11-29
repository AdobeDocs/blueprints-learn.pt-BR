---
title: Experience Platform e medidas de proteção de aplicativos
description: As medidas de proteção definem o impacto e as expectativas de desempenho dos componentes e serviços na Adobe Experience Platform e em Aplicativos da Adobe
solution: Customer Journey Analytics, Journey Orchestration, Real-Time Customer Data Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
source-git-commit: 76ad3dceda37c5f991a43df5828a926f6dfc42a5
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 41%

---

# Medidas de proteção

As medidas de proteção são limites recomendados que fornecem orientação para o uso de dados e do sistema no Adobe Experience Platform e em aplicativos. As medidas de proteção refletem as restrições do sistema e as expectativas de desempenho para otimizar a arquitetura do cliente e o desempenho do caso de uso, além de ajudar a evitar erros ou resultados inesperados. As medidas de proteção não se destinam a ser contratos de nível de serviço.

Para obter informações sobre contratos de nível de serviço específicos para aplicativos e recursos, consulte [Descrições de aplicativos e recursos](#application-feature-descriptions) na parte inferior desta página.


## Documentação de referência sobre as medidas de proteção da Adobe Experience Platform e dos aplicativos da Adobe

As seguintes páginas fornecem informações sobre medidas de proteção para recursos, serviços e aplicativos do Adobe Experience Platform:

**aplicativos Experience Platform**

* [Visão geral das medidas de proteção do Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/guardrails/overview.html)
* [medidas de proteção de compartilhamento de público-alvo do Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=pt-BR#latency)
* [Medidas de proteção de assimilação de dados do Customer Journey Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=pt-BR#what-is-the-expected-latency-for-analytics-data-on-platform%3F)
* [Medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=pt-BR)

**serviços Experience Platform**

* [Proteção da assimilação de dados](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html?lang=pt-BR)
* [Proteção à API de rede de borda](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html?lang=pt-BR)
* [Medidas de proteção do perfil do cliente em tempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)
* [Medidas de proteção de identidade](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=pt-BR)
* [Medidas de proteção do serviço de Query](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=pt-BR)
* [Medidas de proteção de ativação de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=pt-BR)

## Diagramas de latência de ponta a ponta {#end-to-end-latency}

### Assimilação de dados {#data-ingestion}

O diagrama abaixo exibe os valores esperados de latência de assimilação de dados por meio do [assimilação por transmissão](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html) e [assimilação em lote](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/getting-started.html?lang=pt-BR) ao trazer dados para o Real-Time CDP. Clique na imagem para ver uma versão de alta resolução.

![Visão geral visual de alto nível da assimilação de dados.](/help/blueprints/experience-platform/deployment/assets/aep_data_flow_guardrails.svg "Visão geral visual de alto nível da assimilação de dados e valores de latência"){width="1000" zoomable="yes"}

### Segmentação {#segmentation}

O diagrama abaixo exibe os valores de latência esperados ao trabalhar com os públicos-alvo na [Serviço de segmentação do Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=pt-BR). Clique na imagem para ver uma versão de alta resolução.

![Visão geral visual de alto nível da segmentação.](/help/blueprints/experience-platform/deployment/assets/segmentation_guardrails.svg "Visão geral visual de alto nível da segmentação e valores de latência"){width="1000" zoomable="yes"}

### Real-time Customer Data Platform e Adobe Target {#adobe-target-latency}

O diagrama abaixo exibe os valores de latência esperados ao exportar os públicos do Real-Time CDP para o [Adobe Target](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=pt-BR). Clique na imagem para ver uma versão de alta resolução.

![Exportar para visão geral visual de alto nível do Adobe Target.](/help/blueprints/experience-platform/deployment/assets/RTCDP_Target_guardrails.svg "Exportação de públicos-alvo para valores de latência e visão geral visual de alto nível do Adobe Target"){width="1000" zoomable="yes"}

### Customer Journey Analytics    {#customer-journey-analytics}

O diagrama abaixo exibe os valores de latência esperados ao trabalhar com o [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=en). Clique na imagem para ver uma versão de alta resolução.

![Trabalhar com a visão geral de alto nível do Customer Journey Analytics.](/help/blueprints/experience-platform/deployment/assets/CJA_guardrails.svg "Trabalhar com valores de latência e visão geral visual de alto nível do Customer Journey Analytics"){width="1000" zoomable="yes"}

### Journey Optimizer   {#journey-optimizer}

O diagrama abaixo exibe os valores de latência esperados ao trabalhar com o [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en). Clique na imagem para ver uma versão de alta resolução.

![Trabalhar com uma visão geral visual de alto nível do Adobe Journey Optimizer.](/help/blueprints/experience-platform/deployment/assets/AJO_guardrails.svg "Trabalhar com valores de latência e visão geral visual de alto nível do Adobe Journey Optimizer"){width="1000" zoomable="yes"}

## Descrições de aplicativos e recursos {#application-feature-descriptions}

Para obter informações sobre contratos de nível de serviço específicos de recursos, consulte as descrições de produto abaixo:

* [Experience Platform Collection Enterprise](https://helpx.adobe.com/br/legal/product-descriptions/adobe-experience-platform-collection-enterprise.html)
* [Real-time Customer Data Platform](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform.html)
* [B2B Customer Data Platform](https://helpx.adobe.com/br/legal/product-descriptions/adobe-experience-platform-b2b.html)
* [Experience Platform Activation](https://helpx.adobe.com/br/legal/product-descriptions/adobe-experience-platform0.html)
* [Experience Platform Intelligence](https://helpx.adobe.com/br/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Serviços inteligentes](https://helpx.adobe.com/br/legal/product-descriptions/intelligent-services.html)
* [Data Distiller](https://helpx.adobe.com/br/legal/product-descriptions/data-distiller.html)
* [Customer Journey Analytics](https://helpx.adobe.com/br/legal/product-descriptions/customer-journey-analytics.html)
* [Journey Optimizer](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html)
* [Journey Orchestration](https://helpx.adobe.com/br/legal/product-descriptions/journey-orchestration.html)
* [Offer Decisioning](https://helpx.adobe.com/br/legal/product-descriptions/offer-decisioning-app-service.html)
