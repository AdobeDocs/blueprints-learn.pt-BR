---
title: Análise do cliente e geração de Insight
description: Saiba como criar espaços de trabalho de análise entre canais, métricas calculadas e painéis para análise de comportamento e desempenho.
solution: Customer Journey Analytics, Experience Platform
exl-id: 235a4eb0-91ae-4030-b90e-7eda08c67ae1
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1717'
ht-degree: 3%

---

# Análise do cliente e geração de insight

Este guia descreve o padrão de caso de uso da geração de insight e análise do cliente, que conecta conjuntos de dados do [!DNL Adobe Experience Platform] ao [!DNL Customer Journey Analytics] para criar visualizações de dados, espaços de trabalho de análise de forma livre, métricas computadas, painéis e scorecards para dispositivos móveis e, opcionalmente, publicar públicos definidos pela CJA de volta no [!DNL Adobe Experience Platform] para ativação.

Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam entender o que esse padrão faz, os objetivos de negócios que ele aceita, os casos de uso táticos que ele permite e os aplicativos Adobe envolvidos.

Diferentemente dos outros padrões na taxonomia que se concentram na ativação e no engajamento (envio de mensagens, personalização de conteúdo, ativação de públicos), esse padrão se concentra na compreensão — análise do comportamento do cliente, medição do desempenho da campanha, identificação de tendências e geração de insights que informam as decisões de estratégia e otimização.

## Padrão do caso de uso

**Análise de clientes e geração de insight**

Crie espaços de trabalho de análise entre canais, métricas calculadas e painéis para entender o comportamento do cliente e o desempenho da campanha.

**Plano de execução:** Conexão de dados > Configuração de visualização de dados > Workspace Analysis > Publicação de painel

## Visão geral do caso de uso

As organizações precisam entender como os clientes se comportam entre canais, como as campanhas se comportam, onde os clientes caem em suas jornadas, qual conteúdo repercute e como diferentes segmentos são retidos ao longo do tempo. A análise do cliente e a geração de insight atendem a essa necessidade conectando os dados avançados entre canais no [!DNL Adobe Experience Platform] ao [!DNL Customer Journey Analytics], em que os analistas podem criar espaços de trabalho de forma livre, criar métricas personalizadas, configurar modelos de atribuição e publicar painéis para o consumo das partes interessadas.

O padrão atende a vários públicos-alvo: analistas de marketing que precisam de análises exploratórias profundas, gerentes de campanha que precisam de painéis de desempenho, gerentes de produtos que precisam de insights de engajamento e retenção e executivos que precisam de scorecards de KPI instantâneos. A abordagem de implementação varia com base no foco analítico principal — medição de desempenho da campanha, análise de jornada entre canais, ativação de público-alvo orientada por análise ou insights de produto guiados.

## Principais objetivos de negócios

Os seguintes objetivos de negócios são compatíveis com esse padrão de caso de uso.

**Melhorar análises e relatórios**

Aprimore os recursos de relatórios para obter insights de marketing mais rápidos e acionáveis por meio de painéis unificados e ferramentas de autoatendimento.

- **KPIs:** eficiência, produtividade

Consulte [Melhorar o Analytics e os relatórios](/help/blueprints/business-objectives/analytics-insights/improve-analytics-reporting.md) para obter mais informações sobre esse objetivo comercial.

**Habilitar tomada de decisão orientada por dados**

Capacite as equipes com análises de autoatendimento, insights do cliente em tempo real e previsões alimentadas por IA para orientar a estratégia.

- **KPIs:** eficiência, produtividade

Consulte [Habilitar a Tomada de Decisão Orientada por Dados](/help/blueprints/business-objectives/analytics-insights/enable-data-driven-decision-making.md) para obter mais informações sobre esse objetivo comercial.

**Melhorar atribuição de marketing**

Meça com precisão o impacto dos pontos de contato de marketing, canais e campanhas nos resultados da conversão e da receita.

- **KPIs:** Eficiência, Receita Incremental

Consulte [Melhorar a atribuição de marketing](/help/blueprints/business-objectives/analytics-insights/improve-marketing-attribution.md) para obter mais informações sobre esse objetivo comercial.

**Otimizar os gastos com marketing e o ROI**

Otimize a alocação de orçamento de marketing entendendo quais canais e campanhas oferecem o maior retorno.

- **KPIs:** Eficiência, Receita Incremental

Consulte [Otimizar gastos com marketing e o ROI](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md) para obter mais informações sobre esse objetivo comercial.

## Exemplo de casos de uso tático

Veja a seguir exemplos de casos de uso táticos que podem ser implementados com esse padrão.

- Painel de desempenho do Campaign — métricas de delivery, taxas de engajamento, conversão e atribuição de receita em campanhas de email, SMS, push e de mídia paga
- Análise de fallout de jornada do cliente — identifique onde os clientes abandonam os funis de compra, registro ou integração
- Análise de retenção de coorte — meça o desempenho das diferentes coortes de aquisição em semanas, meses e trimestres
- Modelagem de atribuição de canais — compare a atribuição de primeiro e último toque, linear e declínio de tempo para entender quais canais geram conversões
- Análise do desempenho do conteúdo — identifique qual conteúdo corresponde mais aos estágios do segmento, canal e ciclo de vida
- Análise de uso e adoção de produtos — controle a adoção de recursos, a frequência de engajamento e as tendências de crescimento dos usuários
- Análise dos estágios do ciclo de vida do cliente — segmentar e analisar clientes por estágio do ciclo de vida (novo, ativo, em risco, descontinuado)
- Painel de otimização de mix de marketing — compare o investimento no canal com a contribuição de receita
- Pontuação e relatórios de engajamento entre canais: crie pontuações de engajamento compostas a partir de interações da Web, do aplicativo, de email e de campanha

## Indicadores-chave de desempenho

Os KPIs a seguir ajudam a medir o sucesso desse padrão de caso de uso.

| KPI | Descrição | Abordagem de medição |
| --- | --- | --- |
| Eficiência | Redução do tempo de implantação do insight e do esforço manual de emissão de relatórios | Rastrear o tempo gasto pelo analista na criação de relatórios antes e depois da implementação do CJA |
| Proprodutividade | Número de análises de autoatendimento criadas por usuários empresariais | Monitorar a criação de projetos do Workspace e o uso do painel |
| Receita incremental | Receita atribuída às decisões de otimização orientadas por insights | Meça o aumento da receita com campanhas otimizadas com base na análise do CJA |
| Taxas de conversão | Taxas de conclusão do funnel nas principais jornadas do cliente | Rastrear as taxas de fallout em cada etapa da jornada usando a visualização de fallout do CJA |
| Engajamento | Profundidade e frequência da interação do cliente entre canais | Criar métricas calculadas para a pontuação de engajamento no CJA |
| Retenção | Taxas de devolução do cliente em períodos definidos | Usar a análise de coorte do CJA para medir curvas de retenção |

## Aplicativos

Os aplicativos a seguir são usados neste padrão de caso de uso.

- **[!DNL Customer Journey Analytics] (CJA)** — Conexões, visualizações de dados, análise de espaço de trabalho, análise guiada, métricas computadas, painéis, publicação de público e análise de conteúdo
- **[!DNL Adobe Experience Platform] (AEP)** — Data lake, conjuntos de dados, esquemas XDM, dados de perfil e evento que alimentam conexões do CJA

## Documentação relacionada

Os recursos a seguir fornecem informações adicionais para esse padrão de caso de uso.

### [!DNL Customer Journey Analytics] — Introdução

- [Visão geral do CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-overview/cja-overview)
- [Medidas de proteção do CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-admin/guardrails)

### Conexões

- [Visão geral das conexões](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-connections/overview)
- [Criar ou editar uma conexão](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-connections/create-connection)
- [Gerenciar conexões](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-connections/manage-connections)

### Visualizações de dados

- [Visão geral das visualizações de dados](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/data-views)
- [Criar ou editar uma visualização de dados](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Visão geral das configurações de componente](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [Configurações de persistência](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [Configurações de atribuição](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [Configurações de formato](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/format)
- [Desduplicação de métrica](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication)
- [Incluir/excluir valores](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/include-exclude-values)
- [Configurações da sessão](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/session-settings)
- [Campos derivados](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/derived-fields)

### Workspace e análise

- [Visão geral do Workspace](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/home)
- [Criar um projeto](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [Tabela de forma livre](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [Visualização de fluxo](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [Visualização Fallout](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [Tabela de coorte](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [Painel de atribuição](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [Detalhamento de dimensões](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)
- [Compartilhar projetos](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [Agendar projetos](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [Visão geral da exportação](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/export/export-cloud)

### Análise guiada

- [Visão geral da análise guiada](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/guided-analysis/overview)
- [Visualização do funnel](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [Exibição de tendências](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/guided-analysis/trends/usage)
- [Exibição da frequência de engajamento](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/guided-analysis/trends/frequency)
- [Exibição de retenção](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/guided-analysis/retention/retention-rates)
- [Visualização de crescimento ativa](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/guided-analysis/user-growth/active)
- [Visualização do impacto da versão](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/guided-analysis/impact/release)
- [Visualização de impacto de primeiro uso](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/guided-analysis/impact/first-use)
- [Exibição da linha do tempo](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/guided-analysis/streams/timeline)

### Componentes

- [Visão geral dos filtros](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [Criar filtros](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [Visão geral das métricas calculadas](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [Criar métricas calculadas](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [Funções de métrica calculada](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-functions)
- [Visão geral de anotações](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/annotations/overview)
- [Intervalos de datas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)
- [Componente de métricas](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/apply-create-metrics)

### Publicação de público

- [Visão geral dos públicos](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [Criar e publicar públicos-alvo](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/audiences/publish)
- [Gerenciar públicos](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/audiences/manage)

### Análise de conteúdo

- [Content Analytics](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/content-analytics/content-analytics)
- [Configuração do Content Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/config/configuration)

### Painéis e cartões de pontuação

- [Criar um cartão de pontuação para dispositivos móveis](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [Configurar e preparar cartões de pontuação](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Painéis do Adobe Analytics — guia executivo](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dashboards/set-up-execs)
- [Visualização do número do resumo](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/visualizations/summary-number-change)

### AEP foundation

- [Visão geral dos conjuntos de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/catalog/datasets/overview)
- [Visão geral do sistema XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/home)
- [Visão geral das origens](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/home)
- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/home)
- [Visão geral do portal de público](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/audience-portal)

### Integração de relatórios do AJO

- [Guia de integração do AJO + CJA](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Relatório de email da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/reporting/campaign-global-report-cja-email)
- [Jornada relatório de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/reporting/journey-global-report-cja-email)

### Tutoriais e guias

- [Noções básicas de composição de esquema](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/schema/composition)
- [Visão geral do Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/web-sdk/home)
- [Configurar sequências de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/datastreams/configure)
