---
title: Recomendação comportamental
description: Saiba como gerar recomendações de item e conteúdo usando estratégias de seleção e modelos de classificação.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: db16e773-e0da-46c4-9fa5-d16f04feb46b
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 5%

---

# Recomendação comportamental

Este guia descreve o padrão de caso de uso de recomendação comportamental, que usa a Decisão do [!DNL Adobe Journey Optimizer] (AJO), o [!DNL Real-Time Customer Data Platform] (RT-CDP) e o [!DNL Adobe Experience Platform] (AEP) para fornecer experiências de recomendação personalizadas em canais da Web, de aplicativos móveis e de email. Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam entender o que esse padrão faz, os objetivos de negócios que ele aceita, os casos de uso táticos que ele permite e os aplicativos Adobe envolvidos.

A Recomendação comportamental gera recomendações no nível do item ou do conteúdo usando sinais comportamentais — exibições do produto, compras, interações de conteúdo, consultas de pesquisa — combinados com estratégias de seleção e modelos de classificação do AJO Decisioning. Ao contrário do Offer Decisioning, que rege um conjunto limitado de ofertas, promoções ou incentivos usando regras de elegibilidade e restrições comerciais, esse padrão opera em catálogos de itens grandes e em constante alteração (produtos, artigos, vídeos), em que a seleção é orientada por sinais de afinidade comportamental em vez de elegibilidade regida.

## Padrão do caso de uso

**Recomendação comportamental**

Gerar recomendações no nível do item ou do conteúdo com base em sinais comportamentais, usando estratégias de seleção e modelos de classificação do AJO Decisioning para veicular conteúdo contextual.

**Plano de execução:** Assimilação de sinal comportamental > Avaliação de estratégia de decisão > Entrega de recomendação > Relatórios

## Visão geral do caso de uso

As organizações com catálogos de produtos, bibliotecas de conteúdo ou bibliotecas de mídia precisam exibir os itens mais relevantes para cada visitante com base em seu histórico comportamental e na atividade da sessão. Seja um carrossel &quot;recomendado para você&quot; em uma página inicial, um widget de venda cruzada em uma página de detalhes do produto ou recomendações de produto incorporadas em uma campanha por email, o desafio subjacente é o mesmo: corresponder o perfil comportamental de cada visitante aos itens mais relevantes de um catálogo e, em seguida, fornecer essas recomendações no canal direito no momento certo.

Esse padrão aborda esse desafio ao assimilar sinais comportamentais em tempo real via [!DNL Web SDK] ou [!DNL Mobile SDK], processando-os por meio de estratégias de seleção do AJO Decisioning que combinam atributos de item com contexto comportamental e entregando os itens recomendados por meio de canais da Web, no aplicativo ou de email. Os modelos de classificação podem ser baseados em fórmulas (por exemplo, classificar por pontuação de afinidade de categoria) ou classificados por IA (por exemplo, modelo de recomendação personalizado). O padrão também lida com cenários de início frio para novos visitantes sem histórico comportamental configurando recomendações de fallback.

O público-alvo para esse padrão inclui equipes de merchandising de comércio eletrônico, equipes de personalização de conteúdo e equipes de experiência digital que buscam melhorar o engajamento, a conversão e o valor médio do pedido por meio de recomendações personalizadas orientadas pelo comportamento real do usuário.

## Principais objetivos de negócios

Os seguintes objetivos de negócios são compatíveis com esse padrão de caso de uso.

### [Impulsionar vendas cruzadas e vendas adicionais](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)

Promova produtos ou serviços complementares e premium para os clientes existentes com base no histórico de comportamento e de compras.

**KPIs:** % de venda adicional/venda cruzada, Receita incremental, Valor vitalício do cliente

### [Aumentar taxas de conversão](../../business-objectives/revenue-monetization/increase-conversion-rates.md)

Melhore a porcentagem de visitantes e prospetos que concluem as ações desejadas, como compras, inscrições ou envios de formulários.

**KPIs:** Taxas de Conversão, Conversão de Cliente Potencial, Custo por Cliente Potencial

### [Fornecer experiências personalizadas ao cliente](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)

Personalize conteúdo, ofertas e mensagens para preferências individuais, comportamentos e estágios do ciclo de vida.

**KPIs:** Compromisso, Taxas de Conversão, Satisfação do Cliente (CSAT)

## Exemplo de casos de uso tático

A seguir estão implementações táticas comuns desse padrão:

- Widget de venda cruzada de produto na página de detalhes do produto (&quot;clientes também comprados&quot;)
- Carrossel &quot;Recomendado para você&quot; na página inicial com base no histórico de navegação
- Recomendações de conteúdo no site de mídia com base no comportamento de leitura
- Widget &quot;Visualizados recentemente&quot; combinado com itens semelhantes
- Recomendações de produto complementar pós-compra
- Enviar recomendações de produto por email com base na afinidade comportamental
- Recomendações específicas por categoria com base no comportamento de navegação na sessão
- Reclassificação de resultados de pesquisa com base em sinais comportamentais

## Indicadores-chave de desempenho

Os KPIs a seguir ajudam a medir a eficácia das implementações de recomendações comportamentais.

| KPI | Abordagem de medição |
| --- | --- |
| Índice de click-through (CTR) da recomendação | Cliques em itens recomendados divididos por impressões de recomendação |
| Índice de conversão de recomendação | Compras ou ações desejadas de cliques de recomendação divididas pelo total de cliques de recomendação |
| Receita influenciada pelas recomendações | Receita total de pedidos que incluíram pelo menos um produto orientado por recomendação |
| Aumento do valor médio de pedido (AOV) | Aumento na AOV para sessões que envolveram recomendações em relação a sessões sem |
| Itens por pedido | Número de itens por pedido para sessões engajadas em recomendações |
| Cobertura da recomendação | Porcentagem de exibições de página ou sessões elegíveis que receberam recomendações personalizadas (não substitutas) |
| Taxa de Fallback de Inicialização a Frio | Porcentagem de solicitações de recomendação atendidas pela lógica de fallback devido ao histórico comportamental insuficiente |

## Aplicativos

Os aplicativos a seguir são usados neste padrão de caso de uso.

- **[!DNL Adobe Journey Optimizer](AJO) Decisão** — Estratégias de seleção, modelos de classificação, catálogos de itens e políticas de decisão que avaliam sinais comportamentais e retornam os itens mais relevantes para cada visitante
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)** — Acúmulo de dados de perfil comportamental, avaliação de público-alvo para escopo de recomendação e atributos computados para pontuação de afinidade comportamental
- **[!DNL Adobe Experience Platform](AEP)** — Assimilação comportamental de evento via [!DNL Web SDK] e [!DNL Mobile SDK], processamento de [!DNL Edge Network], gerenciamento de esquema XDM para dados de evento e catálogo

## Documentação relacionada

Os recursos a seguir fornecem detalhes adicionais sobre as tecnologias e capacidades usadas neste padrão.

### Gerenciamento de decisão

- [Visão geral da Gestão de decisões](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Criar inserções](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Criar regras de decisão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crie ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Criar ofertas substitutas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Criar coleções](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Criar qualificadores de coleção](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [Criar decisões](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estratégias de classificação](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [Entregar ofertas em mensagens](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Fornecer ofertas usando a API do Edge Decisioning](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)

### Coleta de dados e SDK da Web/móvel

- [Visão geral do Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Instalar o Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
- [Visão geral do Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Configurar sequências de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Visão geral da API do Edge Network Server](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)

### XDM e modelagem de dados

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Noções básicas de composição de esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [Criar um conjunto de dados](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/create)
- [Definir uma relação entre dois esquemas](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/relationship-api)

### Identidade e perfil

- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Visão geral dos namespaces de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/namespaces)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [Visão geral do Perfil do cliente em tempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

### Públicos-alvo e segmentação

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentação de transmissão](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentação de borda](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### Atributos computados e enriquecimento de perfil

- [Visão geral de atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Guia da interface de atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)
- [Visão geral do Customer AI](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### Configuração de canais

- [Introdução à configuração de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Configurar superfícies do canal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Delegar subdomínios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)

### Criação e personalização de mensagens

- [Criar conteúdo de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxe do Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabalhar com modelos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)

### Relatórios e análises

- [Relatório global da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Jornada relatório global](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabalhar com o Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Visão geral do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Visão geral do Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Visão geral das métricas calculadas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)

### Governança de dados e ciclo de vida

- [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview)
- [Visão geral do gerenciamento avançado do ciclo de vida dos dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)
- [Expirações do conjunto de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration)

### Monitorização e observabilidade

- [Visão geral dos Insights de observação](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)
- [Visão geral de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)

### Medidas de proteção

- [Medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Medidas de proteção de assimilação](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- [Medidas de proteção do serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)

### Tutoriais e guias

- [Visão geral das origens](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Visão geral das tags](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)
- [Grupo de campos Consentimento e preferências](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
