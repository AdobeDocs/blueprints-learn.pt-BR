---
title: Experience Platform e medidas de proteção de aplicativos
description: As medidas de proteção definem o impacto e as expectativas de desempenho dos componentes e serviços na Adobe Experience Platform e em Aplicativos da Adobe
solution: Experience Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
source-git-commit: a5d127c2a9e18ebbf25012475b9f474c07575362
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 10%

---


# Medidas de proteção

As medidas de proteção refletem as restrições do sistema, as latências esperadas e as expectativas de desempenho para otimizar a arquitetura do cliente e o desempenho do caso de uso e ajudar a garantir a estabilidade, evitar erros ou resultados inesperados.

## Tipos de medidas de proteção

| Tipo de grade de proteção | Descrição |
|---|---|
| Proteção de desempenho (limite flexível) | As medidas de proteção de desempenho são limites de uso que estão relacionados ao escopo dos seus casos de uso e descrevem o desempenho esperado em condições normais. Quando excedido, pode ocorrer degradação do desempenho e latência. As medidas de proteção de desempenho estão documentadas nos documentos de Experience League, nas seções de medidas de proteção para cada Solução, conforme descrito abaixo. |
| Limite estático (limite permanente) | São limites impostos pelo sistema que não podem ser excedidos. Normalmente, os limites estáticos são vinculados por contrato e descritos no contrato do cliente e nas [Descrições do produto](https://helpx.adobe.com/legal/product-descriptions.html). |

>[!NOTE]
>
> As grades de proteção não devem ser contratos de nível de serviço, mas orientação para configurações ideais e comportamento esperado do sistema. Quaisquer medidas de proteção que sejam limites de sistema ou contratuais ou Contratos de nível de serviço serão documentadas especificamente nos contratos do cliente e nas descrições do produto. Se você estiver interessado em saber mais sobre limites personalizados, entre em contato com o representante do Atendimento ao cliente.

>[!NOTE]
>
> Para casos de uso com necessidades rígidas de latência ou desempenho, a Adobe sugere discutir os detalhes com a Equipe de conta da Adobe e o Parceiro de implementação. Cada configuração do cliente pode variar entre padrões de assimilação de dados, contagens e riqueza de perfis, regras de segmentos e canais de ativação. Dessa forma, é importante projetar e testar seu caso de uso para otimizar o desempenho e entender totalmente as características de desempenho esperadas.

## Documentação de referência sobre as medidas de proteção da Adobe Experience Platform e dos aplicativos da Adobe

As seguintes páginas fornecem informações sobre medidas de proteção para recursos, serviços e aplicativos do Adobe Experience Platform:

**aplicativos de Experience Platform**

* [visão geral das medidas de proteção do Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/guardrails/overview.html)
* [medidas de proteção de compartilhamento de público-alvo de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html#latency)
* [medidas de proteção de assimilação de dados de Customer Journey Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html#what-is-the-expected-latency-for-analytics-data-on-platform%3F)
* [medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html)

**serviços de Experience Platform**

* [Proteção da assimilação de dados](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html)
* [[!DNL Edge Network] Medidas de proteção de API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* [Perfil do cliente em tempo real e Medidas de proteção de segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)
* [Medidas de proteção de identidade](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=pt-BR)
* [Medidas de proteção do serviço de Query](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=pt-BR)
* [Medidas de proteção de ativação de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=pt-BR)

## Diagramas de latência de ponta a ponta {#end-to-end-latency}

### Latências observadas primárias do Edge Network de Experience Platform e do hub {#edge-hub-latencies}

O diagrama a seguir descreve as latências observadas na borda e no hub principais que devem ser observadas ao projetar o caso de uso no Experience Platform e nos aplicativos.

![Experience Platform [!DNL Edge Network] e latências observadas primárias do hub.](/help/blueprints/experience-platform/deployment/assets/aep_edge_hub_latency_v1.svg "Edge Network de Experience Platform e latências observadas primárias de hub"){width="1000" zoomable="yes"}

### Assimilação de dados {#data-ingestion}

O diagrama abaixo exibe os valores esperados da latência de assimilação de dados por meio da [assimilação de streaming](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html) e da [assimilação em lote](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/getting-started.html?lang=pt-BR) ao trazer dados para a Real-Time CDP. Clique na imagem para ver uma versão de alta resolução.

![Visão geral visual de alto nível da assimilação de dados.](/help/blueprints/experience-platform/deployment/assets/aep_data_flow_guardrails.svg "Visão geral visual de alto nível da assimilação de dados e valores de latência"){width="1000" zoomable="yes"}

### Segmentação {#segmentation}

O diagrama abaixo exibe os valores de latência esperados ao trabalhar com públicos no [serviço de segmentação do Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=pt-BR). Clique na imagem para ver uma versão de alta resolução.

![Visão geral visual de alto nível da segmentação.](/help/blueprints/experience-platform/deployment/assets/segmentation_guardrails.svg "Visão geral visual de alto nível da segmentação e valores de latência"){width="1000" zoomable="yes"}

### Real-time Customer Data Platform e [!DNL Edge Network] {#adobe-edge-latency}

O diagrama abaixo exibe os valores de latência esperados ao aproveitar o [!DNL Edge Network] - por exemplo, para aproveitar os públicos da RTCDP no [Adobe Target](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=pt-BR). Clique na imagem para ver uma versão de alta resolução.

![Visão geral visual de alto nível do Adobe Edge Network and Experience Platform.](/help/blueprints/experience-platform/deployment/assets/RTCDP_Edge_guardrails.svg "Exportar audiências para visão geral visual de alto nível e latência do Adobe Target"){width="1000" zoomable="yes"}

### Customer Journey Analytics    {#customer-journey-analytics}

O diagrama abaixo exibe os valores de latência esperados ao trabalhar com [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=en). Clique na imagem para ver uma versão de alta resolução.

![Trabalhando com a visão geral visual de alto nível do Customer Journey Analytics.](/help/blueprints/experience-platform/deployment/assets/CJA_guardrails.svg "Trabalhando com valores de latência e visão geral visual de alto nível do Customer Journey Analytics"){width="1000" zoomable="yes"}

### Journey Optimizer   {#journey-optimizer}

O diagrama abaixo exibe os valores de latência esperados ao trabalhar com o [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en). Clique na imagem para ver uma versão de alta resolução.

![Trabalhando com a visão geral visual de alto nível do Adobe Journey Optimizer.](/help/blueprints/experience-platform/deployment/assets/AJO_guardrails.svg "Trabalhando com valores de latência e visão geral visual de alto nível do Adobe Journey Optimizer"){width="1000" zoomable="yes"}