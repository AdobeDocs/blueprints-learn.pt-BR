---
user-guide-title: Blueprints de experiência digital
breadcrumb-title: Blueprints
user-guide-description: Blueprints de experiência digital são implantações replicáveis para resolver problemas empresariais consagrados e contêm diagramas de arquitetura, considerações técnicas e links para documentações relevantes.
product: adobe experience platform
mini-toc-levels: 3
role: Architect, Developer, User
source-git-commit: 079c2e6deeeea0ede0f71a8bdda7e9b9f4d9084c
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 100%

---


# Blueprints de experiência digital {#architecture}

+ [Visão geral](/help/blueprints/overview.md)
+ Blueprints de indústria vertical{#vertical-blueprints}
   + [Visão geral](/help/blueprints/vertical-blueprints/overview.md)
   + [Vestuário](/help/blueprints/vertical-blueprints/apparel.md)
   + [Varejo](/help/blueprints/vertical-blueprints/retail.md)
   + [Telecomunicações](/help/blueprints/vertical-blueprints/telecommunications.md)
   + [Viagens e hospitalidade](/help/blueprints/vertical-blueprints/travel-hospitality.md)
+ Visões gerais da arquitetura{#architecture-overview}
   + [Experience Cloud](/help/blueprints/experience-platform/experience-cloud.md)
   + [Experience Platform e aplicativos](/help/blueprints/experience-platform/platform-applications.md)
   + [Fluxo de dados da Experience Platform](/help/blueprints/experience-platform/platform-data-flow.md)
   + Implantação{#deployment}
      + [SDK da Web da Experience Platform e Edge Network](/help/blueprints/experience-platform/deployment/websdk.md)
      + [SDKs do aplicativo](/help/blueprints/experience-platform/deployment/appsdk.md)
      + [Medidas de proteção](/help/blueprints/experience-platform/deployment/guardrails.md)
+ Ativação de público-alvo e perfil{#audience-activation}
   + [Visão geral](/help/blueprints/audience-activation/overview.md)
   + [Ativação de público-alvo anônima    (AAM)](/help/blueprints/audience-activation/anonymous.md)
   + Ativação de cliente conhecido (RTCDP) {#known-customer-audience-activation}
      + [Visão geral](/help/blueprints/audience-activation/known.md)
      + [Ativação para canais sociais e publicitários](/help/blueprints/audience-activation/advertising-activation.md)
      + [Ativação para destinos por transmissão de arquivos e empresas](/help/blueprints/audience-activation/enterprise-destinations.md)
      + [Hub de atividades do cliente](/help/blueprints/audience-activation/customer-activity.md)
      + [Correspondência de Segmentos](/help/blueprints/audience-activation/segment-match.md)
   + [Ativação com aplicativos da Experience Cloud](/help/blueprints/audience-activation/platform-and-applications.md)
+ Ativação e marketing B2B{#b2b-activation}
   + [Visão geral](/help/blueprints/b2b/overview.md)
   + [Ativação B2B](/help/blueprints/b2b/b2bactivation.md)
   + Otimizar a cadeia de suprimento da campanha com o Marketo e o Workfront{#optimize-campaign-supply-chain-with-marketo-and-workfront}
      + [Visão geral](/help/blueprints/b2b/campaign-supply-chain/overview.md)
      + [Entrada e criação](/help/blueprints/b2b/campaign-supply-chain/intake-and-create.md)
      + [Histórias de sucesso do cliente](/help/blueprints/b2b/campaign-supply-chain/customer-success-stories.md)
+ Customer Journey Analytics{#customer-journey-analytics}
   + [Visão geral](/help/blueprints/customer-journey-analytics/overview.md)
   + [Compartilhamento de públicos-alvo do CJA em RTCDP](/help/blueprints/customer-journey-analytics/cja-rtcdp.md)
   + [CJA e Journey Optimizer](/help/blueprints/customer-journey-analytics/cja-ajo.md)
+ Jornadas do cliente{#customer-journeys}
   + [Visão geral](/help/blueprints/customer-journeys/overview.md)
   + Journey Optimizer{#journey-optimizer}
      + [Journey Optimizer](/help/blueprints/customer-journeys/journey-optimizer.md)
      + Gestão de decisões{#decision-management}
         + [Visão geral](/help/blueprints/customer-journeys/decision_management/decision-management-overview.md)
         + [Gestão de decisões na borda](/help/blueprints/customer-journeys/decision_management/decision-management-edge.md)
         + [Gestão de decisões no hub](/help/blueprints/customer-journeys/decision_management/decision-management-hub.md)
      + [Journey Optimizer com Adobe Campaign](/help/blueprints/customer-journeys/ajo-and-campaign.md)
      + [Mensagens de terceiros](/help/blueprints/customer-journeys/3rd-party-messaging.md)
   + Campaign Standard{#campaign-standard}
      + [Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=pt-BR){target="_blank"}
      + [Real-Time CDP com Adobe Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/aep-sources-destinations/get-started-sources-destinations.html?lang=pt-BR){target="_blank"}
   + Campaign v8{#campaign-v8}
      + [Campaign v8](/help/blueprints/customer-journeys/campaign-v8.md)
      + [Real-Time CDP com Adobe Campaign v8](/help/blueprints/customer-journeys/rtcdp-and-campaign-v8.md)
      + [Journey Optimizer com Adobe Campaign v8](/help/blueprints/customer-journeys/ajo-and-campaign-v8.md)
   + Campaign v7{#campaign-v7}
      + [Campaign v7](/help/blueprints/customer-journeys/campaign-v7.md)
      + [Real-Time CDP com Adobe Campaign    v7](/help/blueprints/customer-journeys/rtcdp-and-campaign.md)
      + [Journey Optimizer com Adobe Campaign v7](/help/blueprints/customer-journeys/ajo-and-campaign-v7.md)
+ Coleta, acesso e exportação de dados{#data-ingestion}
   + [Visão geral](/help/blueprints/data-ingestion/overview.md)
   + [ de coleção de dados do Encaminhamento de eventos de várias sandboxes](/help/blueprints/data-ingestion/multi-sandbox-event-forwarding.md)
   + [Assimilação e preparação de dados](/help/blueprints/data-ingestion/ingestion.md)
   + [Acesso e exportação de dados](/help/blueprints/data-ingestion/egress.md)
   + [Encaminhamento de eventos](/help/blueprints/data-ingestion/server-side-collection.md)
+ Análise de dados, Inteligência e IA/Aprendizado de máquina{#data-exploration}
   + [Visão geral](/help/blueprints/data-insights/overview.md)
   + [Análise de dados e Inteligência](/help/blueprints/data-insights/analysis.md)
   + [Ciência de dados personalizada para enriquecimento de perfis](/help/blueprints/data-insights/data-science.md)
+ Personalização da Web e móvel{#web-personalization}
   + [Visão geral](/help/blueprints/web-personalization/overview.md)
   + [Personalização com base comportamental    - Target](/help/blueprints/web-personalization/behavioral.md)
   + [Personalização conhecida do cliente – Target e RTCDP](/help/blueprints/web-personalization/known-personalization.md)
   + [Gestão de decisões](/help/blueprints/web-personalization/decision-management-edge.md)