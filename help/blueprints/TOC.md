---
user-guide-title: Objetivos de negócios, casos de uso, diagramas de arquitetura e blueprints da orquestração de experiência do cliente
breadcrumb-title: Casos de uso e blueprints
user-guide-description: Explore os principais objetivos de negócios, padrões de casos de uso e casos de uso do setor para Adobe Experience Platform e aplicativos. Os diagramas e blueprints da arquitetura visual fornecem referências técnicas para integração do sistema, fluxos de dados e design da solução, conectando o valor comercial à implementação.
product: adobe experience platform
mini-toc-levels: 3
role: Developer, User
source-git-commit: 63154ca158b773287f0d1a7f88a81ac3181c43a0
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 26%

---


# Blueprints de orquestração de experiência do cliente {#architecture}

+ [Blueprints de orquestração de experiência do cliente](/help/blueprints/overview.md)
+ Principais objetivos de negócios para AEP e aplicativos{#business-objectives}
   + [Visão geral](/help/blueprints/business-objectives/overview.md)
   + Aquisição e crescimento{#acquisition-growth}
      + [Adquirir novos clientes](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)
      + [Aumentar a geração de leads](/help/blueprints/business-objectives/acquisition-growth/increase-lead-generation.md)
      + [Aumentar o engajamento no site](/help/blueprints/business-objectives/acquisition-growth/increase-website-engagement.md)
   + Receita e monetização{#revenue-monetization}
      + [Aumentar as taxas de conversão](/help/blueprints/business-objectives/revenue-monetization/increase-conversion-rates.md)
      + [Aumentar receita e vendas](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)
      + [Impulsionar receitas de venda cruzada e venda adicional](/help/blueprints/business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)
      + [Aumente a fidelidade do cliente e o valor vitalício](/help/blueprints/business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)
   + Custo e eficiência{#cost-efficiency}
      + [Reduza o custo de aquisição do cliente](/help/blueprints/business-objectives/cost-efficiency/reduce-customer-acquisition-cost.md)
      + [Otimizar os gastos com marketing e o ROI](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)
      + [Melhorar a qualidade e a governança dos dados](/help/blueprints/business-objectives/cost-efficiency/improve-data-quality-governance.md)
      + [Consolidar e modernizar a tecnologia de marketing](/help/blueprints/business-objectives/cost-efficiency/consolidate-modernize-marketing-technology.md)
   + Experiência do cliente{#customer-experience-objectives}
      + [Fornecer experiências personalizadas ao cliente](/help/blueprints/business-objectives/customer-experience/deliver-personalized-customer-experiences.md)
      + [Melhorar a retenção do cliente](/help/blueprints/business-objectives/customer-experience/improve-customer-retention.md)
      + [Melhorar a integração do cliente](/help/blueprints/business-objectives/customer-experience/improve-customer-onboarding.md)
      + [Recuperação de carrinhos e Jornadas abandonados](/help/blueprints/business-objectives/customer-experience/recover-abandoned-carts-journeys.md)
   + Analytics &amp; Insights{#analytics-insights}
      + [Melhorar o Analytics e os relatórios](/help/blueprints/business-objectives/analytics-insights/improve-analytics-reporting.md)
      + [Permita a tomada de decisões orientadas por dados](/help/blueprints/business-objectives/analytics-insights/enable-data-driven-decision-making.md)
      + [Melhorar a atribuição de marketing](/help/blueprints/business-objectives/analytics-insights/improve-marketing-attribution.md)
   + Qualificação e vendas (B2B){#qualification-sales-b2b}
      + [Melhorar a qualificação e a conversão de clientes potenciais](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)
      + [Melhorar o engajamento do cliente](/help/blueprints/business-objectives/qualification-sales-b2b/improve-customer-engagement.md)
+ Padrões de caso de uso{#use-case-patterns}
   + [Visão geral](/help/blueprints/use-case-patterns/overview.md)
   + Criação e ativação de público{#audience-building-activation}
      + [Audience Activation para destinos](/help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md)
      + [Audience Collaboration com correspondência de segmentos](/help/blueprints/use-case-patterns/audience-building-activation/audience-collaboration-segment-match.md)
      + [Encaminhamento de eventos](/help/blueprints/use-case-patterns/audience-building-activation/event-forwarding.md)
      + [Audience Activation B2B](/help/blueprints/use-case-patterns/audience-building-activation/b2b-audience-activation.md)
   + Personalização{#personalization-patterns}
      + [Visitante anônimo - Web Personalization](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md)
      + [Personalization de aplicativo/Web de visitante conhecido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md)
      + [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md)
      + [Recomendação comportamental](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md)
   + Orquestração e gerenciamento de campanhas{#campaign-orchestration-patterns}
      + [Ativação de mensagem de saída em lote](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md)
      + [Mensagens acionadas por evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md)
      + [Jornada orquestrada em várias etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md)
      + [Jornada entre canais com decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md)
      + [Compra de marketing baseado em grupo e gerenciamento de Jornadas](/help/blueprints/use-case-patterns/campaign-management-orchestration/buying-group-based-marketing.md)
   + Análise{#analysis-patterns}
      + [Análise do cliente e geração de Insight](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md)
      + [Análise B2B](/help/blueprints/use-case-patterns/analysis/b2b-analytics.md)
   + Experiência de conversa{#conversational-experience-patterns}
      + [Experiência de conversa do Brand Concierge](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md)
+ Exemplos de casos de uso do setor{#industry-use-cases}
   + [Catálogo de casos de uso](/help/blueprints/industry-use-cases/use-case-catalog.md)
   + [Automotivo](/help/blueprints/industry-use-cases/automotive/automotive-overview.md)
   + [B2B](/help/blueprints/industry-use-cases/b2b/b2b-overview.md)
   + [Serviços financeiros](/help/blueprints/industry-use-cases/financial-services/financial-services-overview.md)
   + [Serviços de saúde](/help/blueprints/industry-use-cases/healthcare/healthcare-overview.md)
   + [Seguro](/help/blueprints/industry-use-cases/insurance/insurance-overview.md)
   + [Mídia e entretenimento](/help/blueprints/industry-use-cases/media-entertainment/media-entertainment-overview.md)
   + [Varejo](/help/blueprints/industry-use-cases/retail/retail-overview.md)
   + [Telecomunicações](/help/blueprints/industry-use-cases/telecommunications/telecommunications-overview.md)
   + [Viagens e hospitalidade](/help/blueprints/industry-use-cases/travel-hospitality/travel-hospitality-overview.md)
+ Diagramas e blueprints de arquitetura{#architecture-diagrams}
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
         + [Ciência de dados personalizada para enriquecimento de perfil](/help/blueprints/audience-activation/data-science.md)
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
   + Customer Journey Analytics{#customer-journey-analytics}
      + [Visão geral](/help/blueprints/customer-journey-analytics/overview.md)
      + [Customer Journey Analytics B2B](/help/blueprints/customer-journey-analytics/b2b-cja.md)
      + [Compartilhamento de públicos da CJA com a RTCDP](/help/blueprints/customer-journey-analytics/cja-rtcdp.md)
      + [CJA e Journey Optimizer](/help/blueprints/customer-journey-analytics/cja-ajo.md)
      + [Análise e inteligência de dados](/help/blueprints/customer-journey-analytics/analysis.md)
   + Jornadas do cliente{#customer-journeys}
      + [Visão geral](/help/blueprints/customer-journeys/overview.md)
      + Journey Optimizer{#journey-optimizer}
         + [Journey Optimizer](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-overview.md)
         + [AJO jornada](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-journeys.md)
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
