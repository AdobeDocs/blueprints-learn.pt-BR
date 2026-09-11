---
user-guide-title: Objetivos de negócios, casos de uso, diagramas de arquitetura e blueprints da orquestração de experiência do cliente
breadcrumb-title: Casos de uso e blueprints
user-guide-description: Explore os principais objetivos de negócios, padrões de casos de uso e casos de uso do setor para Adobe Experience Platform e aplicativos. Os diagramas e blueprints da arquitetura visual fornecem referências técnicas para integração do sistema, fluxos de dados e design da solução, conectando o valor comercial à implementação.
product: adobe experience platform
mini-toc-levels: 3
role: Developer, User
nudge: orange
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 15%

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
    + [Pesquisa de perfil em tempo real para suporte e vendas](/help/blueprints/use-case-patterns/audience-building-activation/real-time-profile-lookup.md)
    + [Ciência de dados personalizados para enriquecimento de perfil](/help/blueprints/use-case-patterns/audience-building-activation/data-science-profile-enrichment.md)
  + Personalização{#personalization-patterns}
    + [Visitante anônimo - Web Personalization](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md)
    + [Personalization de aplicativo/Web de visitante conhecido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md)
    + [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md)
    + [Recomendação comportamental](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md)
    + [Acesso ao perfil do Edge para Personalization da Web/móvel](/help/blueprints/use-case-patterns/personalization/edge-profile-access.md)
    + [Compartilhamento de público com a Adobe Target](/help/blueprints/use-case-patterns/personalization/audience-sharing-with-target.md)
  + Orquestração e gerenciamento de campanhas{#campaign-orchestration-patterns}
    + [Ativação de mensagem de saída em lote](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md)
    + [Mensagens acionadas por evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md)
    + [Jornada orquestrada em várias etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md)
    + [Jornada entre canais com decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md)
    + [Orquestração em lote e mensagens transacionais do Campaign v8](/help/blueprints/use-case-patterns/campaign-management-orchestration/campaign-v8-orchestration.md)
    + [Integração de mensagens de terceiros com o Journey Optimizer](/help/blueprints/use-case-patterns/campaign-management-orchestration/third-party-messaging.md)
  + Análise{#analysis-patterns}
    + [Análise do cliente e geração de Insight](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md)
  + Ativação e marketing B2B{#b2b-patterns}
    + [Audience Activation B2B](/help/blueprints/use-case-patterns/b2b/account-audience-activation.md)
    + [Compra de marketing baseado em grupo e gerenciamento de Jornadas](/help/blueprints/use-case-patterns/b2b/buying-group-marketing.md)
    + [Análise B2B](/help/blueprints/use-case-patterns/b2b/account-analytics.md)
    + [Jornadas B2B usando dados do Marketo](/help/blueprints/use-case-patterns/b2b/marketo-data-journeys.md)
    + [Controlador de mídia paga B2B do AJO](/help/blueprints/use-case-patterns/b2b/paid-media-orchestration.md)
    + [Entrada e criação de Marketo e Workfront](/help/blueprints/use-case-patterns/b2b/campaign-intake-and-creation.md)
    + [Revisão e aprovação da Marketo e Workfront](/help/blueprints/use-case-patterns/b2b/campaign-review-and-approval.md)
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
  + [Tecnologia](/help/blueprints/industry-use-cases/technology/technology-overview.md)
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

+ {hide-from-toc}Labs práticos{#labs}
  + [Visão geral dos laboratórios práticos](/help/blueprints/labs/overview.md)
  + Workshops práticos{#workshops}
    + AEP Foundations{#aep-foundations}
      + [Visão geral](/help/blueprints/labs/aep-foundations/overview.md)
      + [Configuração](/help/blueprints/labs/aep-foundations/setup.md)
      + Configuração de sandbox{#aep-sandbox}
        + [Configuração do Developer Console](/help/blueprints/labs/aep-foundations/sandbox-setup/developer-console-setup.md)
        + [Instruções de implantação](/help/blueprints/labs/aep-foundations/sandbox-setup/deployment-instructions.md)
      + Configuração do Postman{#aep-postman}
        + [Instalação do Postman](/help/blueprints/labs/aep-foundations/postman-setup/postman-installation.md)
        + [Arquivo de ambiente](/help/blueprints/labs/aep-foundations/postman-setup/environment-file.md)
        + [Coleção de API](/help/blueprints/labs/aep-foundations/postman-setup/api-collection.md)
        + [Acesso à sandbox](/help/blueprints/labs/aep-foundations/postman-setup/sandbox-access.md)
        + [Token de acesso](/help/blueprints/labs/aep-foundations/postman-setup/access-token.md)
      + Perfil do cliente em tempo real{#aep-rtcp}
        + [Palestras](/help/blueprints/labs/aep-foundations/real-time-customer-profile/lectures.md)
        + Inspeção do perfil{#aep-rtcp-inspect}
          + [Visão geral](/help/blueprints/labs/aep-foundations/real-time-customer-profile/inspecting-the-profile/overview.md)
          + [Noções básicas de perfil](/help/blueprints/labs/aep-foundations/real-time-customer-profile/inspecting-the-profile/profile-basics.md)
          + [Fundir políticas](/help/blueprints/labs/aep-foundations/real-time-customer-profile/inspecting-the-profile/merge-policies.md)
          + [APIs de perfil e identidade](/help/blueprints/labs/aep-foundations/real-time-customer-profile/inspecting-the-profile/profile-and-identity-apis.md)
      + Metodologia da LID{#aep-lid}
        + [Pré-requisitos](/help/blueprints/labs/aep-foundations/lid-methodology/prerequisites.md)
        + [Rótulo](/help/blueprints/labs/aep-foundations/lid-methodology/label.md)
        + Identificar{#aep-lid-identify}
          + [Visão geral](/help/blueprints/labs/aep-foundations/lid-methodology/identify/overview.md)
          + [Parte 1 - Tipos de tabela restantes](/help/blueprints/labs/aep-foundations/lid-methodology/identify/part-1-remaining-table-types.md)
          + [Parte 2 - Campos principais](/help/blueprints/labs/aep-foundations/lid-methodology/identify/part-2-key-fields.md)
        + [Desnormalizar](/help/blueprints/labs/aep-foundations/lid-methodology/denormalize.md)
      + Modelagem XDM{#aep-xdm}
        + [Palestras](/help/blueprints/labs/aep-foundations/xdm-modeling/lectures.md)
        + Modelagem da interface{#aep-xdm-ui}
          + [Visão geral](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/overview.md)
          + [Logon e navegação](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/login-and-browse.md)
          + [Objetos-Padrão de Modelo](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/model-standard-objects.md)
          + [Objetos personalizados do modelo](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/model-custom-objects.md)
          + [Configurar para perfil](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/configure-for-profile.md)
        + Modelagem de API{#aep-xdm-api}
          + [Visão geral](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/overview.md)
          + Criar esquema{#aep-xdm-api-build}
            + [Visão geral](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/overview.md)
            + [Obter grupos de campos padrão](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/get-standard-field-groups.md)
            + [Criar grupos de campos personalizados](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/create-custom-field-groups.md)
            + [Obter Classe de Perfil](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/get-profile-class.md)
            + [Criar esquema](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/create-schema.md)
            + [Exibir esquema](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/view-schema.md)
            + [Modificar esquema - Patch JSON](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/modify-schema-json-patch.md)
          + Marcar campos de identidade{#aep-xdm-api-identity}
            + [Visão geral](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/mark-identity-fields/overview.md)
            + [Criar identidade principal](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/mark-identity-fields/create-primary-identity.md)
            + [Criar outras identidades](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/mark-identity-fields/create-other-identities.md)
            + [Exibir esquema](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/mark-identity-fields/view-schema.md)
          + Definir Relações{#aep-xdm-api-relationships}
            + [Visão geral](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/overview.md)
            + [Obter ID do Esquema do Plano](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/get-plan-schema-id.md)
            + [Criar relação do esquema](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/create-schema-relationship.md)
            + [Criar Identidade de Referência do Plano](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/create-plan-reference-identity.md)
            + [Exibir esquema](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/view-schema.md)
          + [Recapitulação](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/recap.md)
        + Laboratórios Bônus{#aep-xdm-bonus}
          + [Visão geral](/help/blueprints/labs/aep-foundations/xdm-modeling/bonus-labs/overview.md)
          + [Automatizar com APIs](/help/blueprints/labs/aep-foundations/xdm-modeling/bonus-labs/automate-with-apis.md)
      + Ingestão de dados{#aep-ingestion}
        + [Palestras](/help/blueprints/labs/aep-foundations/data-ingestion/lectures.md)
        + [Visão geral do laboratório](/help/blueprints/labs/aep-foundations/data-ingestion/lab-overview.md)
        + [Arquivos de exemplo](/help/blueprints/labs/aep-foundations/data-ingestion/sample-files.md)
        + Assimilação em lote{#aep-ingestion-batch}
          + [Visão geral](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/overview.md)
          + [Criar fluxo de dados](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/create-dataflow.md)
          + Mapeamento de dados{#aep-ingestion-batch-mapping}
            + [Visão geral](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/mapping-data/overview.md)
            + [Corrigir Mapeamentos de Passagem](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/mapping-data/fix-passthrough-mappings.md)
            + [Campos Calculados](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/mapping-data/calculated-fields.md)
            + [Verificar conjunto de mapeamento final](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/mapping-data/check-final-mapping-set.md)
          + [Executar fluxo de dados](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/run-dataflow.md)
          + [Erros de depuração](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/debugging-errors.md)
          + [Criar um novo fluxo de dados](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/create-a-new-dataflow.md)
          + [Correção de erros](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/fixing-errors.md)
          + [Verificação e validação](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/verification-and-validation.md)
        + Assimilação de fluxo{#aep-ingestion-stream}
          + [Visão geral](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/overview.md)
          + [Configurar Source](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/setup-source.md)
          + [Configurar mapeamento](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/configure-mapping.md)
          + [Verificar conjunto de mapeamento final](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/check-final-mapping-set.md)
          + [Transmitir um perfil](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/stream-a-profile.md)
          + [Verificar perfil assimilado](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/verify-ingested-profile.md)
          + [Erros de Monitoramento e Depuração](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/monitoring-and-debugging-errors.md)
          + [Verificação e validação](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/verification-and-validation.md)
        + Laboratórios Bônus{#aep-ingestion-bonus}
          + [Visão geral](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/overview.md)
          + [Corrigir Erros do MAPPER para CreateDate](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/fix-mapper-errors-for-createdate.md)
          + [Transmitir um evento de pedido](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/stream-an-order-event.md)
          + Uso da Landing Zone{#aep-ingestion-dlz}
            + [Visão geral](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/overview.md)
            + [Configurar Source](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/setup-source.md)
            + [Criar Mapeamentos](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/create-mappings.md)
            + [Agendar fluxo de dados](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/schedule-dataflow.md)
            + [Tentar novamente um fluxo de dados com falha](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/retry-a-failed-dataflow.md)
            + Carregar Pedidos{#aep-ingestion-dlz-orders}
              + [Visão geral](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/overview.md)
              + [Configurar Source](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/setup-source.md)
              + [Mapeamentos iniciais](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/initial-mappings.md)
              + [Mapeamentos de Cópia de Objeto](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/object-copy-mappings.md)
              + [Verificar e agendar fluxo de dados](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/verify-and-schedule-dataflow.md)
      + Segmentação e ativação{#aep-segmentation}
        + [Palestra](/help/blueprints/labs/aep-foundations/segmentation-and-activation/lecture.md)
        + Ativação do Edge{#aep-segmentation-edge}
          + [Visão geral](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/overview.md)
          + [Criar público-alvo do Edge](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/create-edge-audience.md)
          + [Enviar um evento do Edge](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/send-an-edge-event.md)
          + Configurar o encaminhamento de eventos{#aep-segmentation-edge-ef}
            + [Visão geral](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/setup-event-forwarding/overview.md)
            + [Criar propriedade](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/setup-event-forwarding/create-property.md)
            + [Criar sequência de dados](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/setup-event-forwarding/create-datastream.md)
      + Criação de público{#aep-audiences}
        + Caso de uso 1 - Aquisição{#aep-uc1}
          + [Visão geral](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/overview.md)
          + Configurar destinos{#aep-uc1-destinations}
            + [Configurar destino Personalization personalizado](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/configure-destinations/setup-custom-personalization-destination.md)
            + [Configurar destino de transmissão](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/configure-destinations/setup-streaming-destination.md)
          + [Criar público-alvo 1](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/build-audience-1.md)
          + [Criar público-alvo 2](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/build-audience-2.md)
          + [Criar público-alvo 3](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/build-audience-3.md)
          + [Enviar um evento do Edge](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/send-an-edge-event.md)
          + [Análise de pensamento crítico](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/critical-thinking-review.md)
        + Caso de uso 2 — venda adicional{#aep-uc2}
          + [Visão geral](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/overview.md)
          + [Trabalho prévio](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/pre-work.md)
          + [Opção 1 - Usar públicos-alvo para agregar](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/option-1-using-audiences-to-aggregate.md)
          + [Opção 2 - Usar pré-agregados](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/option-2-use-pre-aggregates.md)
          + [Análise de pensamento crítico](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/critical-thinking-review.md)
        + Caso de uso 3 — Alcance{#aep-uc3}
          + [Visão geral](/help/blueprints/labs/aep-foundations/audience-building/use-case-3-outreach/overview.md)
          + [Caso de uso de build 3](/help/blueprints/labs/aep-foundations/audience-building/use-case-3-outreach/build-use-case-3.md)
          + [Análise de pensamento crítico](/help/blueprints/labs/aep-foundations/audience-building/use-case-3-outreach/critical-thinking-review.md)
        + Laboratórios Bônus{#aep-audiences-bonus}
          + [Visão geral](/help/blueprints/labs/aep-foundations/audience-building/bonus-labs/overview.md)
          + [Enviar evento de pedido para hub](/help/blueprints/labs/aep-foundations/audience-building/bonus-labs/send-order-event-to-hub.md)
          + [Enviar Evento da Web para Hub](/help/blueprints/labs/aep-foundations/audience-building/bonus-labs/send-web-event-to-hub.md)
          + [Monitorar o evento](/help/blueprints/labs/aep-foundations/audience-building/bonus-labs/monitor-your-event.md)
    + AJO Foundations{#ajo-foundations}
      + [Visão geral](/help/blueprints/labs/ajo-foundations/overview.md)
      + [Configuração](/help/blueprints/labs/ajo-foundations/setup.md)
      + Configuração de sandbox{#ajo-sandbox}
        + [Configuração do Developer Console](/help/blueprints/labs/ajo-foundations/sandbox-setup/developer-console-setup.md)
        + [Instruções de implantação](/help/blueprints/labs/ajo-foundations/sandbox-setup/deployment-instructions.md)
      + Configuração do Postman{#ajo-postman}
        + [Instalação do Postman](/help/blueprints/labs/ajo-foundations/postman-setup/postman-installation.md)
        + [Importar arquivo de ambiente](/help/blueprints/labs/ajo-foundations/postman-setup/import-environment-file.md)
        + [Importar coleção de API](/help/blueprints/labs/ajo-foundations/postman-setup/import-api-collection.md)
      + Blocos de construção de arquitetura{#ajo-architecture}
        + [Palestra](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/lecture.md)
        + Mapeamento de casos de uso para arquitetura{#ajo-architecture-mapping}
          + [Visão geral](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/mapping-use-cases-to-architecture/overview.md)
          + [Introdução ao laboratório](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/mapping-use-cases-to-architecture/lab-introduction.md)
          + [Exercício de laboratório](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/mapping-use-cases-to-architecture/lab-exercise.md)
          + [Revisão do laboratório](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/mapping-use-cases-to-architecture/lab-review.md)
      + Armazenamentos de dados{#ajo-data-stores}
        + [Aula de perfil do cliente em tempo real](/help/blueprints/labs/ajo-foundations/data-stores/real-time-customer-profile-lecture.md)
        + Perfil em ação{#ajo-profile}
          + [Visão geral](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/overview.md)
          + [Logon e navegação](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/login-and-browse.md)
          + [Criar sequência de dados](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/create-datastream.md)
          + [Enviar um evento da Web do Edge](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/send-an-edge-web-event.md)
          + [Validar perfil no hub](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/validate-profile-on-hub.md)
          + [Validar perfil no Edge](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/validate-profile-on-edge.md)
          + [Validar evento no Data Lake](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/validate-event-on-data-lake.md)
          + [Validar instantâneo do perfil](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/validate-profile-snapshot.md)
          + [Resumo](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/summary.md)
        + [Palestra de loja relacional](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-lecture.md)
        + Armazenamento Relacional em Ação{#ajo-relational}
          + [Visão geral](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/overview.md)
          + [Procurar Esquemas](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/browse-schemas.md)
          + [Dimension de destino do perfil](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/profile-target-dimension.md)
          + [Ler um público](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/read-an-audience.md)
          + [Resumo](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/summary.md)
        + Configurar canais de email{#ajo-email}
          + [Visão geral](/help/blueprints/labs/ajo-foundations/data-stores/configure-email-channels/overview.md)
          + [Configurar para perfil](/help/blueprints/labs/ajo-foundations/data-stores/configure-email-channels/configure-for-profile.md)
          + [Configurar para relacional](/help/blueprints/labs/ajo-foundations/data-stores/configure-email-channels/configure-for-relational.md)
          + [Aguardando o status ativo](/help/blueprints/labs/ajo-foundations/data-stores/configure-email-channels/waiting-for-active-status.md)
      + Campanhas orquestradas{#ajo-campaigns}
        + [Lição sobre entrega de mensagens](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-lecture.md)
        + Entrega de mensagem em ação{#ajo-campaigns-delivery}
          + [Visão geral](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/overview.md)
          + [Criar uma campanha](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/create-a-campaign.md)
          + [Criar um público-alvo](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/build-an-audience.md)
          + [Adicionar atividade de bifurcação](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/add-fork-activity.md)
          + [Adicionar atividades de email](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/add-email-activities.md)
          + [Testar a campanha](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/test-the-campaign.md)
          + [Resumo](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/summary.md)
        + [Palestra de Blocos de Construção de Fluxo de Trabalho](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/workflow-building-blocks-lecture.md)
        + Lançamento de telefone emblemático{#ajo-campaigns-flagship}
          + [Visão geral](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/overview.md)
          + [Configurar canal de SMS](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/configure-sms-channel.md)
          + [Criar uma campanha orquestrada](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/create-an-orchestrated-campaign.md)
          + [Criar um público-alvo](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/build-an-audience.md)
          + [Bifurque o resultado](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/fork-the-result.md)
          + [Salvar o público-alvo](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/save-the-audience.md)
          + [Filtrar as linhas](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/filter-the-lines.md)
          + [Compor o SMS](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/compose-the-sms.md)
          + [Executar o fluxo de trabalho](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/run-the-workflow.md)
          + [Resumo](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/summary.md)
      + Jornadas{#ajo-journeys}
        + [Palestra](/help/blueprints/labs/ajo-foundations/journeys/lecture.md)
        + Excitação pós-compra{#ajo-journeys-post-purchase}
          + [Visão geral](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/overview.md)
          + [Configurar evento](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/configure-event.md)
          + [Configurar ação personalizada](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/configure-custom-action.md)
          + [Criar Jornada](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/build-journey.md)
          + [Testar Jornada](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/test-journey.md)
          + [Enviar um evento](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/send-an-event.md)
          + [Validar evento assimilado](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/validate-event-ingested.md)
          + [Validar Jornada](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/validate-journey.md)
          + [Resumo](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/summary.md)
      + Decisão.{#ajo-decisioning}
        + [Experience Edge](/help/blueprints/labs/ajo-foundations/decisioning/experience-edge.md)
        + Explicação da decisão{#ajo-decisioning-explained}
          + [Visão geral](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/overview.md)
          + [Introdução](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/introduction.md)
          + [XDM do item de decisão](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/decision-item-xdm.md)
          + [Criação do item de decisão](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/decision-item-creation.md)
          + [Coleções](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/collections.md)
          + [Fórmulas de Classificação](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/ranking-formulas.md)
          + [Estratégias de seleção](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/selection-strategies.md)
          + [Políticas de decisão](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/decision-policies.md)
          + [Medidas de proteção, Modelos de IA Decisionam o futuro](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/guardrails-ai-models-decisioning-future.md)
        + Navegação abandonada{#ajo-decisioning-abandoned}
          + [Visão geral](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/overview.md)
          + [Criar regra de decisão](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-decision-rule.md)
          + [Criar atributos da oferta](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-offer-attributes.md)
          + [Criar itens de oferta](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-offer-items.md)
          + [Criar coleção de ofertas](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-offer-collection.md)
          + [Criar Fórmula de Classificação](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-ranking-formula.md)
          + [Criar estratégia de seleção](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-selection-strategy.md)
          + [Criar canal de experiência baseado em código](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-code-based-experience-channel.md)
          + [Criar a Jornada](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-the-journey.md)
          + [Decisão e CBEs em ação](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/decisioning-and-cbes-in-action.md)
          + [Resumo](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/summary.md)
      + Criação de conteúdo com IA{#ajo-content-ai}
        + [Palestra](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/lecture.md)
        + [Visão geral](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/overview.md)
        + [Gerenciamento da marca](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/brand-management.md)
        + [Criação de fragmentos de conteúdo](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/building-content-fragments.md)
        + [Criar modelo de conteúdo](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/building-content-template.md)
        + [Criação do email](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/creating-the-email.md)
        + [Assistente de IA e Personalization de conteúdo](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/ai-assistant-and-content-personalization.md)
        + [Personalization e experimentação de conteúdo](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/personalization-and-content-experimentation.md)
        + [Simulação de conteúdo](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/content-simulation.md)
        + [Alinhamento da marca](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/brand-alignment.md)
        + [Testar o email](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/test-the-email.md)
        + [Resumo](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/summary.md)
