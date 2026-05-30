---
title: Offer Decisioning
description: Saiba como usar a lógica de decisão centralizada para selecionar a próxima melhor oferta ou conteúdo para um perfil em vários canais.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 8fd511b3-0200-41bf-aff1-e3f2a00a578e
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1640'
ht-degree: 5%

---

# Offer Decisioning

Este guia descreve o padrão de caso de uso do Offer Decisioning, que usa a Decisão do [!DNL Adobe Journey Optimizer] (AJO) e o [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP) para implementar uma lógica de seleção de oferta centralizada que determina a próxima melhor oferta para cada perfil de cliente em todos os canais. Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam entender o que esse padrão faz, os objetivos de negócios que ele aceita, os casos de uso táticos que ele permite e os aplicativos Adobe envolvidos.

O padrão separa a decisão &quot;o que mostrar&quot; da lógica de canal &quot;onde mostrar&quot;, permitindo uma seleção de oferta consistente e otimizada por email, Web, aplicativo móvel e qualquer outro ponto de contato. O AJO Decisioning gerencia todo o ciclo de vida da oferta: criação de ofertas e gerenciamento de catálogos, regras de elegibilidade (quem pode ver cada oferta), estratégias de classificação (como selecionar entre ofertas elegíveis), disposições (onde as ofertas aparecem) e políticas de decisão (que vinculam tudo).

## Padrão do caso de uso

Esta seção descreve o plano de execução e a definição de padrão do Offer Decisioning.

**Offer Decisioning**

Use a lógica de decisão centralizada para selecionar a melhor oferta ou conteúdo para um perfil em todos os canais.

**Plano de execução:** Avaliação de público-alvo > Elegibilidade da oferta > Estratégia de classificação > Execução de decisão > Entrega > Relatórios

## Visão geral do caso de uso

As empresas geralmente precisam apresentar a oferta, a promoção ou o incentivo mais relevante para cada cliente no momento da interação. Se a interação ocorrer em uma campanha de email, em uma página inicial do site, em um aplicativo móvel ou em um ponto de decisão em uma jornada de várias etapas, o desafio é o mesmo: selecionar a oferta ideal de um catálogo de opções disponíveis com base em quem é o cliente, para o que ele se qualifica e qual oferta tem maior probabilidade de gerar o resultado desejado.

O Offer Decisioning aborda isso centralizando toda a lógica de seleção de ofertas no mecanismo de Gestão de decisões da AJO. Em vez de codificar atribuições de oferta em campanhas ou canais individuais, o mecanismo de decisão avalia os atributos, a associação de público-alvo e os sinais contextuais de cada perfil para determinar a melhor oferta em tempo real. Essa centralização garante que o mesmo cliente receba ofertas consistentes e otimizadas, independentemente do canal pelo qual se envolva.

Esse padrão difere da personalização da Web/aplicativo de visitante conhecido no escopo — o Offer Decisioning é independente de canal e centralizado, enquanto a personalização de visitante conhecido se concentra na personalização de superfície digital. Ela difere da recomendação comportamental no modelo de catálogo — use o offer decisioning quando o conjunto de itens elegíveis for regido por regras de negócios, restrições de elegibilidade ou requisitos regulatórios (promoções, produtos financeiros, incentivos). Use recomendações comportamentais quando o conjunto de itens for grande, alterado continuamente e a seleção for impulsionada por similaridade comportamental ou sinais de afinidade (catálogos de produtos, bibliotecas de conteúdo).

## Principais objetivos de negócios

Os seguintes objetivos de negócios são compatíveis com esse padrão de caso de uso.

**[Fornecer experiências personalizadas ao cliente](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**
Personalize conteúdo, ofertas e mensagens para preferências individuais, comportamentos e estágios do ciclo de vida.
**KPIs:** Compromisso, Taxas de Conversão, Satisfação do Cliente (CSAT)

**[Impulsionar vendas cruzadas e vendas adicionais](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)**
Promova produtos ou serviços complementares e premium para os clientes existentes com base no histórico de comportamento e de compras.
**KPIs:** % de venda adicional/venda cruzada, Receita incremental, Valor vitalício do cliente

**[Aumente a fidelidade do cliente e o valor vitalício](../../business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)**
Aprofunde as relações com o cliente e maximize o valor a longo prazo por meio de programas de fidelidade, recompensas e envolvimento personalizado.
**KPIs:** Valor vitalício, Retenção, Venda adicional/venda cruzada do cliente %

## Exemplo de casos de uso tático

Os cenários a seguir ilustram como o Offer Decisioning pode ser aplicado na prática.

- Próxima melhor oferta em campanhas de email — selecione a promoção mais relevante por recipient no momento do envio
- Banner promocional em tempo real no site — a decisão seleciona a oferta no carregamento da página com base no perfil do visitante
- Cartão no aplicativo personalizado com o melhor incentivo para o estágio do ciclo de vida do usuário
- Consistência de ofertas entre canais — a mesma lógica de decisão utiliza email, Web e push para que o cliente veja uma experiência de oferta unificada
- Seleção dinâmica de cupom ou desconto com base no nível de valor do cliente (por exemplo, clientes de alto valor recebem uma oferta premium)
- Atualização de produto ou seleção de oferta de venda adicional com base no nível de assinatura atual
- Personalização da oferta de recompensa de fidelidade com base no nível e no histórico de atividades

## Indicadores-chave de desempenho

Os KPIs a seguir ajudam a medir a eficácia de uma implementação do Offer Decisioning.

| KPI | Descrição | Abordagem de medição |
| --- | --- | --- |
| Taxa de aceitação da oferta | Porcentagem de ofertas entregues que resultam em um clique, resgate ou conversão | Cliques ou resgates da oferta / Total de ofertas entregues |
| Distribuição de seleção de oferta | Proporção de cada oferta selecionada em todas as decisões | Contagem por oferta / Total de decisões renderizadas |
| Taxa de fallback | Porcentagem de decisões em que nenhuma oferta personalizada se qualificou e o fallback foi atendido | Impressões substitutas / Total de decisões |
| Índice de conversão | Porcentagem de recipients da oferta que concluíram a ação desejada (compra, inscrição, resgate) | Conversões/impressões da oferta |
| Receita incremental | Receita atribuível às ofertas selecionadas pela decisão em relação a um grupo de controle ou fallback | Receita de ofertas personalizadas - Receita de fallback/controle |
| Pontuação de consistência entre canais | Porcentagem de perfis que recebem a mesma oferta em vários canais em uma janela definida | Ofertas consistentes/Total de impressões multicanais |
| Índice de click-through da oferta | Porcentagem de impressões da oferta que resultam em um clique | Cliques de oferta / Impressões da oferta |

## Aplicativos

Os seguintes aplicativos da Adobe são usados neste padrão de caso de uso.

- **[!DNL Adobe Journey Optimizer] (AJO)** — Mecanismo do Gerenciamento de Decisões para criação de ofertas, regras de qualificação, estratégias de classificação, posicionamentos e políticas de decisão; configuração de canais e criação de mensagens para entrega de ofertas; execução de campanhas e jornadas
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** — Avaliação de público-alvo para segmentos de qualificação de oferta; dados de perfil e atributos computados usados na qualificação e classificação
- **[!DNL Adobe Experience Platform] (AEP)** — Repositório de perfil unificado, resolução de identidade e base de dados com suporte para AJO e RT-CDP

## Documentação relacionada

Os recursos a seguir fornecem detalhes adicionais sobre os componentes usados neste padrão de caso de uso.

### Gestão de decisões

- [Visão geral da Gestão de decisões](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Criar inserções](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Criar regras de decisão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crie ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Criar ofertas substitutas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Criar coleções](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Criar qualificadores de coleção](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [Criar decisões](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estratégias de classificação](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Entrega de oferta

- [Entregar ofertas em mensagens](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Fornecer ofertas usando a API do Edge Decisioning](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [Entregar ofertas usando a API de decisão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/decisioning-api)

### Configuração de canais

- [Introdução à configuração de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Configurações de superfície de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Delegar subdomínios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Configurar canal de notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [Configurar canal de SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)

### Criação e personalização de mensagens

- [Criar conteúdo de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxe do Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabalhar com modelos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Visualizar e testar o conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### Campanhas e jornadas

- [Introdução às campanhas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Criar uma campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Introdução às jornadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

### Experimentação de conteúdo

- [Introdução ao experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Criar um experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)

### Públicos-alvo e segmentação

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentação de transmissão](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentação de borda](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### Perfil e identidade

- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [Visão geral de atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Visão geral do Customer AI](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### Modelagem e coleta de dados

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Visão geral do Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Configurar sequências de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)

### Relatórios e análises

- [Relatório global da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Jornada relatório global](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabalhar com o Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Visão geral do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Visão geral do Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

### Governança de dados e ciclo de vida

- [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview)
- [Visão geral do gerenciamento avançado do ciclo de vida dos dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)
- [Consentimento no Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### Medidas de proteção

- [Medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)

### Tutoriais

- [Introdução à API de gerenciamento de decisão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/getting-started)
