---
user-guide-title: Blueprints do Customer Experience Orchestration
breadcrumb-title: blueprints
user-guide-description: Blueprints de experiência digital são implantações replicáveis para resolver problemas empresariais consagrados e contêm diagramas de arquitetura, considerações técnicas e links para documentações relevantes.
product: adobe experience platform
mini-toc-levels: 3
role: Developer, User
source-git-commit: fb814fe6f5e4e774a96cbe75fea2499d849716b4
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 30%

---


# Blueprints de orquestração de experiência do cliente {#architecture}

+ [Blueprints de orquestrações de experiência do cliente](/help/blueprints/overview.md)
+ Visão geral da arquitetura{#architecture-overview}
   + [Experience Cloud](/help/blueprints/experience-platform/experience-cloud.md)
   + [Experience Platform e aplicativos](/help/blueprints/experience-platform/platform-applications.md)
   + [Fluxo de dados do Experience Platform](/help/blueprints/experience-platform/platform-data-flow.md)
   + [Medidas de proteção do Experience Platform](/help/blueprints/experience-platform/guardrails.md)
   + Implantação{#deployment}
      + [Experience Platform Web SDK &amp; [!DNL Edge Network]](/help/blueprints/experience-platform/deployment/websdk.md)
      + [SDKs do aplicativo](/help/blueprints/experience-platform/deployment/appsdk.md)
+ Ativação de público-alvo e perfil{#audience-activation}
   + [Baseado em dispositivo - Direcionamento anônimo de público-alvo com o Audience Manager](/help/blueprints/audience-activation/audience-manager.md)
   + Real-Time Customer Data Platform (RTCDP) {#known-customer-audience-activation}
      + [Ativação de público-alvo para destinos sociais e de publicidade](/help/blueprints/audience-activation/advertising-activation.md)
      + [Público-alvo e ativação de perfil para blueprint de destinos corporativos](/help/blueprints/audience-activation/enterprise-destinations.md)
      + [Acesso ao perfil em tempo real para cenários de suporte e vendas](/help/blueprints/audience-activation/customer-activity.md)
      + [Acesso ao perfil de borda em tempo real para personalização da Web e móvel](/help/blueprints/audience-activation/real-time-lookup.md)
      + [Colaboração de público com correspondência de segmentos](/help/blueprints/audience-activation/segment-match.md)
      + [Personalização de cliente conhecida com o Target](/help/blueprints/audience-activation/rtcdp-target.md)
+ Ativação e marketing B2B{#b2b-activation}
   + [Visão geral](/help/blueprints/b2b/overview.md)
   + [Ativação B2B](/help/blueprints/b2b/b2bactivation.md)
   + [Ativação da conta B2B](/help/blueprints/b2b/b2b-account-activation.md)
   + [Compra de marketing com base em grupo e gerenciamento de jornadas](/help/blueprints/b2b/b2b-buying-group-journeys.md)
   + [Jornadas B2B usando dados do Marketo](/help/blueprints/b2b/b2b-journeys-with-marketo.md)
   + [Controlador de mídia paga B2B](/help/blueprints/b2b/ajo-b2b-paid-media-controller.md)
   + Blueprint de integração do Marketo Engage e do Workfront{#marketo-engage-and-workfront-integration-blueprint}
      + [Visão geral](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/overview.md)
      + [Entrada e criação](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md)
      + [Revisar e aprovar](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md)
      + [Histórias de sucesso do cliente](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md)
+ Conteúdo e comércio{#content-commerce}
   + [ADOBE COMMERCE e REAL-TIME CDP](/help/blueprints/content-commerce/commerce/commerce-rtcdp.md)
+ Customer Journey Analytics   {#customer-journey-analytics}
   + [Visão geral](/help/blueprints/customer-journey-analytics/overview.md)
   + [Compartilhamento de públicos da CJA com a RTCDP](/help/blueprints/customer-journey-analytics/cja-rtcdp.md)
   + [CJA e Journey Optimizer](/help/blueprints/customer-journey-analytics/cja-ajo.md)
+ Jornadas do cliente{#customer-journeys}
   + [Visão geral](/help/blueprints/customer-journeys/overview.md)
   + Journey Optimizer  {#journey-optimizer}
      + [Journey Optimizer  &#x200B;](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-overview.md)
      + [Jornadas do AJO](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-journeys.md)
      + [Campanhas do AJO](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-campaigns.md)
      + [Mensagens de terceiros](/help/blueprints/customer-journeys/journey-optimizer/3rd-party-messaging.md)
   + Gestão de decisões{#decision-management}
      + [Visão geral](/help/blueprints/customer-journeys/decision-management/decision-management-overview.md)
      + [Gerenciamento de decisão no Edge](/help/blueprints/customer-journeys/decision-management/decision-management-edge.md)
      + [Gerenciamento de decisão no hub](/help/blueprints/customer-journeys/decision-management/decision-management-hub.md)
   + Campaign v8{#campaign-v8}
      + [Campaign v8](/help/blueprints/customer-journeys/campaign-v8/campaign-v8-overview.md)
      + [Real-Time CDP com Adobe [!DNL Campaign] v8](/help/blueprints/customer-journeys/campaign-v8/rtcdp-and-campaign-v8.md)
      + [Journey Optimizer com Adobe Campaign v8](/help/blueprints/customer-journeys/campaign-v8/ajo-and-campaign-v8.md)
   + Blueprints obsoletos{#deprecated-blueprints}
      + Campaign Standard{#campaign-standard}
         + [[!DNL Campaign Standard]](https://experienceleague.adobe.com/pt-br/docs/campaign-standard){target="_blank"}
         + [Real-Time CDP com Adobe [!DNL Campaign Standard]](https://experienceleague.adobe.com/pt-br/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/get-started-sources-destinations)
      + Campaign v7{#campaign-v7}
         + [Campaign v7](/help/blueprints/customer-journeys/campaign-v7/campaign-v7-overview.md)
+ Análise de dados, Inteligência e IA/Aprendizado de máquina {#data-exploration}
   + [Análise e inteligência de dados](/help/blueprints/data-insights/analysis.md)
   + [Ciência de dados personalizada para enriquecimento de perfil](/help/blueprints/data-insights/data-science.md)
