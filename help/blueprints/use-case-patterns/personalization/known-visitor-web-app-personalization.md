---
title: Personalization de aplicativo/Web de visitante conhecido
description: Saiba como fornecer conteúdo, ofertas ou promoções personalizadas para visitantes identificados com base no perfil em tempo real e na associação do segmento.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 585adc0e-f528-4a09-b931-ef6b45fa8ec8
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1819'
ht-degree: 4%

---

# Personalização da Web/aplicativo de visitante conhecido

Este guia descreve o padrão de caso de uso de personalização de aplicativo/Web de visitante conhecido, que usa o [!DNL Adobe Journey Optimizer] (AJO) e o [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP) para fornecer conteúdo personalizado a visitantes identificados em superfícies digitais. Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam entender o que esse padrão faz, os objetivos de negócios que ele aceita, os casos de uso táticos que ele permite e os aplicativos Adobe envolvidos.

A personalização da Web/aplicativo de visitante conhecido é o principal padrão de personalização para experiências digitais autenticadas. Diferentemente da personalização de visitante anônimo, que depende exclusivamente de sinais comportamentais na sessão, esse padrão aproveita o perfil unificado completo: dados comportamentais históricos, associação de segmento, nível de fidelidade, histórico de compras, estágio de ciclo de vida, atributos computados e pontuações de propensão. Ele oferece suporte à personalização em páginas da Web (por meio do canal da Web AJO), mensagens móveis no aplicativo e cartões de conteúdo.

## Padrão do caso de uso

Esta seção descreve o padrão principal e seu plano de execução.

**Personalização de aplicativo/Web de visitante conhecido**

Forneça conteúdo, ofertas ou promoções personalizadas a um visitante identificado com base em perfil em tempo real e associação de segmento em superfícies da Web, dispositivos móveis no aplicativo e cartões de conteúdo.

**Plano de execução:** Avaliação de público-alvo > Personalization Decisioning > Configuração de superfície/canal > Entrega de conteúdo > Rastreamento de impressão > Relatórios

## Visão geral do caso de uso

Organizações com propriedades digitais autenticadas — sites de comércio eletrônico, portais bancários, serviços de assinatura, programas de fidelidade, aplicativos móveis — precisam fornecer experiências personalizadas que reflitam o relacionamento de cada cliente com a marca. Quando um visitante faz logon ou é reconhecido por meio da resolução de identidade, a plataforma pode acessar seu perfil totalmente unificado e fornecer conteúdo adaptado a seus atributos, comportamentos e preferências específicos.

Esse padrão aborda o cenário em que um visitante identificado chega em uma propriedade da Web ou abre um aplicativo móvel, e o sistema deve determinar o conteúdo, a oferta ou a promoção ideais para exibição com base nos dados do perfil em tempo real e na associação do público-alvo. A decisão de personalização ocorre na borda em milissegundos, permitindo a entrega de conteúdo em subsegundos sem latência perceptível.

O padrão é compatível com a personalização determinística (em que o conteúdo específico mapeia para segmentos específicos de público-alvo) e com a decisão dinâmica (em que o AJO Decisioning avalia as regras de elegibilidade e as estratégias de classificação para selecionar o conteúdo ideal por perfil). Ele abrange várias superfícies digitais — páginas da Web, mensagens móveis no aplicativo e cartões de conteúdo — permitindo uma personalização consistente na jornada digital do cliente.

## Principais objetivos de negócios

Os seguintes objetivos de negócios são compatíveis com esse padrão de caso de uso.

### Fornecer experiências personalizadas ao cliente

Personalize conteúdo, ofertas e mensagens para preferências individuais, comportamentos e estágios do ciclo de vida. Para obter mais informações, consulte [Fornecer experiências personalizadas ao cliente](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md).

**KPIs:** Compromisso, Taxas de Conversão, Satisfação do Cliente (CSAT)

### Aumentar o engajamento do site

Melhore o tempo no site, as páginas por sessão e a interação com o conteúdo da Web por meio de experiências relevantes. Para obter mais informações, consulte [Aumentar o engajamento no site](../../business-objectives/acquisition-growth/increase-website-engagement.md).

**KPIs:** Tempo na Página (Web), Envolvimento, Taxas de Conversão

### Aumentar o engajamento do aplicativo móvel

Impulsione o uso ativo diário, a adoção de recursos e as conversões no aplicativo por meio de experiências personalizadas no aplicativo.

**KPIs:** Envolvimento, Retenção, Taxas de Conversão

## Exemplo de casos de uso tático

A seguir estão implementações táticas comuns desse padrão:

- Personalização principal da página inicial por nível de fidelidade ou estágio do ciclo de vida — exiba banners principais diferentes com base no fato de o cliente ser novo, ativo, em risco ou VIP
- Carrossel de recomendações de produtos com base no histórico de compras — forneça sugestões de produtos relevantes usando dados de compras anteriores e pontuações de afinidade de produtos
- Banner promocional personalizado por segmento do cliente — mostre diferentes promoções para segmentos de alto valor, em risco e novos clientes
- Mensagem no aplicativo para usuários móveis com base na adoção de recursos — orienta os usuários para recursos subutilizados com base em seus padrões de uso
- Cartão de conteúdo com oferta personalizada no painel de contas — ofertas persistentes e rejeitadas personalizadas de acordo com o perfil do cliente
- Exibição personalizada de preços ou descontos com base na camada do cliente — mostrar preços específicos da camada ou descontos exclusivos para membros do programa de fidelidade
- Widget de recomendação de venda cruzada com base em produtos próprios — sugira produtos ou serviços complementares com base no portfólio atual
- Navegação personalizada ou ordenação de conteúdo com base em interesses — reordene módulos de conteúdo ou elementos de navegação com base em preferências demonstradas

## Indicadores-chave de desempenho

Os KPIs a seguir ajudam a medir a eficácia desse padrão de caso de uso.

| KPI | Abordagem de medição | Orientação de referencial |
| --- | --- | --- |
| Taxa de participação da Personalization | Cliques e interações com elementos de conteúdo personalizados divididos por impressões | O conteúdo personalizado deve superar o desempenho padrão em 20% a 50% |
| Aumento do índice de conversão | Taxa de conversão para experiências personalizadas versus experiências de controle/padrão | Meta de aumento de 10 a 30% em relação a experiências não personalizadas |
| Índice de click-through (CTR) | Cliques em CTAs, ofertas e recomendações personalizadas divididos por impressões | Monitor por superfície (Web, no aplicativo, cartão de conteúdo) e por segmento |
| Receita por visita | Receita atribuída a sessões com experiências personalizadas | Comparar coortes de visitantes personalizadas com não personalizadas |
| Taxa de interação do cartão de conteúdo | Cliques e dispensas no cartão de conteúdo relacionados a impressões | Rastrear por tipo de cartão e segmento de público |
| Engajamento na mensagem no aplicativo | Interações de mensagem no aplicativo (cliques no CTA, rejeições) relativas a impressões | Comparar segmentos de público-alvo e tipos de mensagem |
| Tempo na página | Tempo médio gasto em páginas com conteúdo personalizado em relação ao padrão | As páginas personalizadas devem mostrar maior tempo de permanência |
| Taxa de aceitação da oferta | Porcentagem de ofertas selecionadas pela decisão que resultam em um evento de conversão | Rastrear por oferta, por posicionamento e por estratégia de classificação |

## Aplicativos

Os aplicativos a seguir são usados neste padrão de caso de uso.

- **[!DNL Adobe Journey Optimizer] (AJO)** — Configuração de canal da Web, configuração de canal no aplicativo, configuração de canal de cartão de conteúdo, decisão (seleção e classificação de ofertas), criação de mensagens (criação de conteúdo personalizado), execução de campanha, experimentação de conteúdo e relatórios
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** — Avaliação de público (borda, streaming e lote), pesquisa de perfil em tempo real via Edge Network, enriquecimento de perfil com atributos computados e pontuações de propensão
- **[!DNL Adobe Experience Platform] (AEP)** — Armazenamento de perfil, serviço de identidade, SDK da Web, SDK Móvel, configuração de sequência de dados, entrega de rede de borda

## Documentação relacionada

Os recursos a seguir fornecem detalhes adicionais sobre as tecnologias e configurações mencionadas neste guia.

### Personalização do canal da Web

- [Introdução ao canal da Web](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/web/get-started-web)
- [Criar experiências da Web](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/web/create-web)
- [Configuração do canal da Web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/web-configuration)

### Canais no aplicativo e de cartão de conteúdo

- [Visão geral do canal no aplicativo](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/in-app/get-started-in-app)
- [Pré-requisitos do canal no aplicativo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/inapp-configuration)
- [Criar mensagens no aplicativo](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/in-app/create-in-app)
- [Canal de cartão de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/get-started-content-card)
- [Configuração do cartão de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/content-card-configuration)
- [Criar cartões de conteúdo](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/content-card/create-content-card)

### Gerenciamento de decisão

- [Visão geral da Gestão de decisões](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Criar inserções](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Criar regras de decisão](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crie ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Criar ofertas substitutas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Criar coleções](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Criar decisões](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estratégias de classificação](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [Entregar ofertas em mensagens](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### Personalization e conteúdo

- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxe do Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Funções auxiliares](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabalhar com modelos de conteúdo](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabalhar com fragmentos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)

### Públicos-alvo e segmentação

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentação de borda](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Segmentação de transmissão](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Referência do Profile Query Language](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/pql/overview)

### Identidade e perfil

- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/home)
- [Visão geral dos namespaces de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/namespaces)
- [Regras de vinculação do gráfico de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/identity-linking-logic)
- [Visão geral do perfil](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/home)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/merge-policies/overview)

### Coleta de dados e SDK

- [Visão geral do Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/web-sdk/home)
- [Instalar o Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/web-sdk/install/overview)
- [Visão geral do Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Configurar sequências de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/datastreams/configure)
- [Visão geral da API do Edge Network Server](https://experienceleague.adobe.com/pt-br/docs/experience-platform/edge-network-server-api/overview)

### Campanhas e experimentação

- [Introdução às campanhas](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Criar uma campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Introdução ao experimento de conteúdo](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Criar um experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Relatório de experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)

### Atributos computados e enriquecimento

- [Visão geral de atributos computados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/computed-attributes/overview)
- [Guia da interface de atributos computados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/computed-attributes/ui)
- [Visão geral do Customer AI](https://experienceleague.adobe.com/pt-br/docs/experience-platform/intelligent-services/customer-ai/overview)

### Relatórios e análises

- [Relatório em tempo real da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Relatório global da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Guia de integração do AJO + CJA](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Visão geral do CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-overview/cja-overview)
- [Visão geral do Analysis Workspace](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/home)

### Governança e privacidade

- [Visão geral da governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/home)
- [Consentimento no Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [Visão geral do gerenciamento avançado do ciclo de vida dos dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-lifecycle/home)

### Medidas de proteção

- [Medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/get-started/guardrails)
- [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/guardrails)
- [Medidas de proteção do serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/guardrails)
