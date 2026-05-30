---
title: Análise B2B
description: Saiba como incluir informações a nível de conta B2B na análise de jornada de clientes entre canais.
solution: Customer Journey Analytics, Real-Time Customer Data Platform
exl-id: 9d576e5c-cbd2-4c60-a6b0-88f8b8b963b4
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1811'
ht-degree: 2%

---

# Análise B2B

Este guia descreve o padrão de caso de uso de análise B2B, que usa o B2B edition [!DNL Customer Journey Analytics] ([!DNL CJA]) e o B2B edition [!DNL Real-Time Customer Data Platform] ([!DNL RT-CDP]) para incorporar informações de nível de conta B2B na análise de jornada de clientes entre canais. Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam entender o que esse padrão faz, os objetivos de negócios que ele aceita, os casos de uso táticos que ele permite e os aplicativos Adobe envolvidos.

O B2B Analytics estende os recursos [!DNL CJA] padrão com conexões baseadas em conta, contêineres específicos B2B (Conta, Conta global, Oportunidade, Grupo de compras) e relatórios no nível da conta. Esse recurso permite que as organizações analisem o marketing e o envolvimento de vendas no nível da conta, rastreiem a progressão da oportunidade, avaliem a integridade do grupo de compras e atribuam a receita aos pontos de contato de marketing em ciclos de vendas B2B estendidos.

## Padrão do caso de uso

**Análise B2B**

Inclua informações a nível de conta B2B na análise de jornada de clientes entre canais.

**Plano de execução:** Conexão de Dados B2B > Configuração de Exibição de Dados da Conta > Workspace Analysis > Publicação do Painel

## Visão geral do caso de uso

As organizações B2B enfrentam um desafio fundamental de análise: seus clientes não são pessoas individuais, mas contas compostas por várias partes interessadas, grupos de compra e oportunidades. A análise padrão com base em pessoas não consegue responder perguntas como &quot;Quais contas são mais engajadas?&quot;, &quot;Qual é o nível de conclusão de nossos grupos de compra?&quot; ou &quot;Quais pontos de contato de marketing impulsionam a progressão da oportunidade?&quot;

A análise B2B aborda isso aproveitando o B2B edition [!DNL CJA] para criar exibições analíticas centradas em conta que combinam dados comportamentais no nível da pessoa com dimensões de conta, oportunidade e grupo de compra. [!DNL RT-CDP] O B2B edition fornece a unificação subjacente do perfil da conta e a resolução de identidade B2B que alimenta a camada de análise. Juntas, essas soluções permitem que as organizações criem análises de jornada entre canais no nível da conta, correlacionem o envolvimento de marketing com a progressão do pipeline e forneçam insights acionáveis para as equipes de marketing e de vendas.

O público-alvo inclui equipes de operações de marketing B2B, líderes de geração de demanda, analistas de operações de receita e líderes de vendas que precisam de visibilidade sobre o envolvimento no nível da conta e a integridade do pipeline.

## Principais objetivos de negócios

Os seguintes objetivos de negócios são compatíveis com esse padrão de caso de uso.

### Melhorar a análise e os relatórios

Aprimore os recursos de relatórios para obter insights de marketing mais rápidos e acionáveis por meio de painéis unificados e ferramentas de autoatendimento. A análise B2B permite que as organizações consolidem dados de envolvimento no nível da conta de várias fontes em um único ambiente analítico, fornecendo visibilidade entre canais sobre como os programas de marketing influenciam o pipeline e a receita.

**KPIs:** eficiência, produtividade

[Saiba mais sobre como melhorar o Analytics e os relatórios](/help/blueprints/business-objectives/analytics-insights/improve-analytics-reporting.md)

### Permita a tomada de decisões orientadas por dados

Capacite as equipes com análises de autoatendimento, insights do cliente em tempo real e previsões alimentadas por IA para orientar a estratégia. A análise no nível da conta equipe de marketing e vendas com os dados necessários para priorizar contas, otimizar estratégias de engajamento e alinhar-se às oportunidades de pipeline.

**KPIs:** eficiência, produtividade

[Saiba mais sobre como ativar a tomada de decisões orientadas por dados](/help/blueprints/business-objectives/analytics-insights/enable-data-driven-decision-making.md)

### Melhorar a qualificação e a conversão de clientes potenciais

Aumente a qualidade do lead e acelere a progressão do pipeline por meio de pontuação, estimulação e acompanhamento personalizado. O CJA B2B edition oferece janelas de pesquisa de conta estendidas por 13 meses, especificamente projetadas para ciclos de vendas B2B, permitindo uma atribuição precisa de multitoque em toda a jornada da conta.

**KPIs:** Eficiência, Receita Incremental

[Saiba mais sobre como melhorar a qualificação e a conversão de clientes potenciais](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

## Exemplo de casos de uso tático

Os cenários a seguir ilustram como esse padrão pode ser aplicado na prática.

- **Análise de pontuação de engajamento da conta** — meça e classifique as contas por seu envolvimento agregado na Web, email, eventos e interações de conteúdo para identificar contas de alta intenção para acompanhamento de vendas
- **Rastreamento da integridade do grupo de compras** — Analise a composição do grupo de compras entre contas para identificar lacunas na cobertura de funções e priorizar a aquisição de clientes potenciais para grupos de compras incompletos
- **Correlação do pipeline de oportunidade** — Correlacione os dados de envolvimento de marketing com a progressão do estágio de oportunidade para entender quais campanhas e pontos de contato impulsionam o avanço do pipeline
- **Atribuição B2B multitoque** — aplique modelos de atribuição com janelas de retrospectiva de 13 meses para creditar pontos de contato de marketing em toda a jornada de compra B2B, do primeiro contato ao fechado
- **Mapeamento de jornada de conta** — Visualize a jornada de conta entre canais desde a percepção inicial até a criação e o fechamento da oportunidade, identificando caminhos e pontos de atrito comuns
- **Influência da campanha no pipeline** — meça como campanhas específicas influenciam a criação de pipeline de conta, o avanço da oportunidade e a geração de receita
- **Progressão do engajamento do grupo de compras** — controle como as pontuações do engajamento do grupo de compras evoluem com o tempo e correlacione os limites de engajamento com os resultados da oportunidade
- **Desempenho do conteúdo baseado em conta** — Analise quais ativos e tópicos de conteúdo refletem em segmentos de conta, setores ou funções de grupo de compras específicos
- **Painéis de alinhamento de vendas e marketing** — crie painéis compartilhados que fornecem às equipes de marketing e vendas uma exibição unificada do envolvimento da conta, da integridade do pipeline e da atribuição de receita
- **Segmentação de conta para ativação** — crie segmentos B2B com base em análises no nível da conta (por exemplo, &quot;contas altamente engajadas sem oportunidades abertas&quot;) e publique-as para ativação downstream

## Indicadores-chave de desempenho

Os KPIs a seguir ajudam a medir o sucesso desse padrão de caso de uso.

| KPI | Descrição | Abordagem de medição |
| --- | --- | --- |
| Pontuação de engajamento da conta | Agregar métrica de envolvimento em todos os contatos de uma conta | Métrica calculada que combina visitas da Web, interações por email, participação em eventos e downloads de conteúdo no nível da conta |
| Integridade do Grupo de Compras | Porcentagem de funções necessárias preenchidas em um grupo de compra | Taxa de funções preenchidas para total de funções necessárias por grupo de compra, rastreadas ao longo do tempo |
| Pipeline influenciado pelo marketing | Receita no pipeline que foi afetada por atividades de marketing | Valor de oportunidade em que os contatos de conta associados têm pontos de contato de marketing dentro da janela de atribuição |
| Índice de conversão de conta em oportunidade | Porcentagem de contas envolvidas que geram oportunidades qualificadas | Contas com oportunidades divididas pelo total de contas envolvidas durante um período definido |
| Duração média do ciclo de negociações | Tempo desde o primeiro contato de marketing até as conclusões | Duração média desde o primeiro ponto de contato atribuído até a data de fechamento da oportunidade |
| Receita de atribuição de marketing | Receita atribuída aos pontos de contato de marketing | Receita de oportunidades fechadas com contatos de marketing, distribuída por modelo de atribuição |
| Alcance e penetração da conta | Número de contatos envolvidos por conta de público alvo | Contatos exclusivos com interações de marketing por conta, em comparação ao total de contatos conhecidos |
| Envolvimento de conteúdo por função de compra | Métricas de engajamento segmentadas pela função de grupo de compra | Exibições de página, downloads e tempo gasto detalhados por personalidade/função nos grupos de compra |

## Aplicativos

Os aplicativos a seguir são usados para implementar esse padrão de caso de uso.

- **[!DNL Customer Journey Analytics]B2B edition** — Fornece conexões baseadas em conta, contêineres de visualização de dados específicos B2B, análise de espaço de trabalho em nível de conta, análise de grupo de compras, análise de oportunidade, segmentação B2B e atribuição B2B com janelas de retrospectiva estendidas
- **[!DNL Real-Time CDP]B2B edition** — Fornece a base de dados B2B incluindo unificação de perfil de conta, resolução de identidade B2B, classes de esquema B2B (Conta, Oportunidade, Grupo de Compras) e integração [!DNL Marketo Engage] para assimilação de dados de envolvimento B2B

## Documentação relacionada

Os recursos a seguir fornecem informações adicionais para implementar esse padrão de caso de uso.

**[!DNL CJA]B2B edition**

- [Visão geral do CJA B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)
- [Visão geral do CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-overview/cja-overview)
- [Medidas de proteção do CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-admin/guardrails)

**Conexões**

- [Visão geral das conexões](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-connections/overview)
- [Criar ou editar uma conexão](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-connections/create-connection)
- [Gerenciar conexões](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-connections/manage-connections)

**Visualizações de dados**

- [Visão geral das visualizações de dados](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/data-views)
- [Criar ou editar uma visualização de dados](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Visão geral das configurações de componente](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [Configurações de persistência](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [Configurações de atribuição](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [Configurações de formato](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/format)
- [Campos derivados](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/derived-fields)
- [Configurações da sessão](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/session-settings)

**Workspace e análise**

- [Visão geral do Workspace](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/home)
- [Criar um projeto](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [Tabela de forma livre](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [Visualização de fluxo](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [Visualização Fallout](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [Tabela de coorte](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [Painel de atribuição](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [Compartilhar projetos](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [Agendar projetos](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [Detalhamento de dimensões](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)

**Componentes**

- [Visão geral dos filtros](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [Criar filtros](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [Visão geral das métricas calculadas](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [Criar métricas calculadas](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [Visão geral de anotações](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/annotations/overview)
- [Intervalos de datas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)

**Públicos-alvo**

- [Visão geral dos públicos](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [Criar e publicar públicos-alvo](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/audiences/publish)
- [Gerenciar públicos](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/audiences/manage)

**Painéis e scorecards**

- [Criar um cartão de pontuação para dispositivos móveis](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [Configurar e preparar cartões de pontuação](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Painéis do Adobe Analytics — guia executivo](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dashboards/set-up-execs)

**Análise guiada**

- [Visão geral da análise guiada](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/guided-analysis/overview)
- [Visualização do funnel](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [Exibição de tendências](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/guided-analysis/trends/usage)
- [Exibição de retenção](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/guided-analysis/retention/retention-rates)

**[!DNL RT-CDP]B2B edition**

- [Visão geral da B2B edition da RT-CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#702702)
- [Esquemas do B2B edition](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/schemas/b2b)
- [Visão geral das fontes B2B](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/sources/b2b)

**AEP data foundation**

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/home)
- [Visão geral das origens](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/home)
- [Conector do Marketo Engage](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/home)
- [Visão geral de sandboxes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/home)

**Governança de dados e ciclo de vida**

- [Visão geral da governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/home)
- [Gerenciamento avançado do ciclo de vida dos dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-lifecycle/home)

**Tutoriais e guias**

- [Noções básicas de composição de esquema](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/schema/composition)
- [Visão geral de atributos computados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/computed-attributes/overview)
- [Visão geral dos Insights de observação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/home)
