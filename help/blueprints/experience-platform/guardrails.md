---
title: Experience Platform e medidas de proteção de aplicativos
description: As medidas de proteção definem o impacto e as expectativas de desempenho dos componentes e serviços na Adobe Experience Platform e em Aplicativos da Adobe
solution: Experience Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
TQID: https://experienceleague.adobe.com/ZSHbFR3sEy4C-876IU3yN8U5vOUVvDWIP-O3l-wKm78
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
subfeature_v2:
  - id: d1823595-9241-4128-8a33-e4ac3bf08773
  - id: e5ae22e3-a3b0-46ed-804f-9abf1bbe3e74
  - id: ee602049-8a18-43df-9299-a689a025a371
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 4134ba7db88206379e267841a4642c555a7e56d5
workflow-type: tm+mt
source-wordcount: 486
ht-degree: 14%

---

# Medidas de proteção

As medidas de proteção refletem as restrições do sistema, as latências esperadas e as expectativas de desempenho para otimizar a arquitetura do cliente e o desempenho do caso de uso e ajudar a garantir a estabilidade, evitar erros ou resultados inesperados.

## Tipos de medidas de proteção

| Tipo de grade de proteção | Descrição |
|---|---|
| Proteção de desempenho (limite flexível) | As medidas de proteção de desempenho são limites de uso que estão relacionados ao escopo dos seus casos de uso e descrevem o desempenho esperado em condições normais. Quando excedido, pode ocorrer degradação do desempenho e latência. As medidas de proteção de desempenho estão documentadas nos documentos da Experience League, nas seções de proteção de cada solução, conforme descrito abaixo. |
| Limite estático (limite permanente) | São limites impostos pelo sistema que não podem ser excedidos. Normalmente, os limites estáticos são vinculados por contrato e descritos no contrato do cliente e nas [Descrições do produto](https://helpx.adobe.com/legal/product-descriptions.html). |

>[!NOTE]
>
> As grades de proteção não devem ser contratos de nível de serviço, mas orientação para configurações ideais e comportamento esperado do sistema. Quaisquer medidas de proteção que sejam limites de sistema ou contratuais ou Contratos de nível de serviço serão documentadas especificamente nos contratos do cliente e nas descrições do produto. Se você estiver interessado em saber mais sobre limites personalizados, entre em contato com o representante do Atendimento ao cliente.

>[!NOTE]
>
> Para casos de uso com necessidades rígidas de latência ou desempenho, a Adobe sugere discutir os detalhes com sua equipe de conta da Adobe e seu parceiro de implementação. Cada configuração do cliente pode variar entre padrões de assimilação de dados, contagens e riqueza de perfis, regras de segmentos e canais de ativação. Dessa forma, é importante projetar e testar seu caso de uso para otimizar o desempenho e entender totalmente as características de desempenho esperadas.

## Documentação de referência sobre as medidas de proteção da Adobe Experience Platform e dos aplicativos da Adobe

As seguintes páginas fornecem informações sobre medidas de proteção para recursos, serviços e aplicativos do Adobe Experience Platform:

**aplicativos Experience Platform**

* [Visão geral das medidas de proteção do Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/guardrails/overview.html)
* [Medidas de proteção de compartilhamento de público do Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html#latency)
* [Medidas de proteção de assimilação de dados do Customer Journey Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html#what-is-the-expected-latency-for-analytics-data-on-platform%3F)
* [Medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html)

**Serviços da Experience Platform**

* [Medidas de proteção para a assimilação de dados](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html)
* [[!DNL Edge Network] Medidas de proteção de API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* [Proteções de perfil e segmentação do cliente em tempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)
* [Proteções de identidade](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=pt-BR)
* [Proteções do Serviço de consulta](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=pt-BR)
* [Proteções de ativação de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=pt-BR)

## Diagramas de latência de ponta a ponta {#end-to-end-latency}

### Latências principais observadas do Experience Platform Edge Network e do Hub {#edge-hub-latencies}

O diagrama a seguir descreve as latências observadas de borda e hub principais a serem observadas ao projetar o caso de uso no Experience Platform e nos aplicativos.

![Latências observadas no Experience Platform [!DNL Edge Network] e no hub principal.](/help/blueprints/experience-platform/assets/aep_edge_hub_latency_v1.png "Latências observadas do Experience Platform Edge Network e do hub principal"){width="1000" zoomable="yes"}