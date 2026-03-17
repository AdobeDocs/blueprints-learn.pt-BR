---
title: Análise do cliente e geração de Insight
description: Saiba como criar espaços de trabalho de análise entre canais, métricas calculadas e painéis para análise de comportamento e desempenho.
solution: Customer Journey Analytics, Experience Platform
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '8947'
ht-degree: 1%

---


# Análise do cliente e geração de insight

Este guia fornece uma referência completa de implementação para análise de clientes e geração de insight. Ele aborda como conectar conjuntos de dados do [!DNL Adobe Experience Platform] ao [!DNL Customer Journey Analytics], configurar visualizações de dados, criar espaços de trabalho de análise de forma livre, criar métricas computadas, publicar painéis e cartões de pontuação móveis e, opcionalmente, publicar públicos definidos pela CJA de volta no [!DNL Adobe Experience Platform] para ativação.

Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam compreender todos os caminhos de implementação viáveis, as compensações entre eles e as decisões de configuração necessárias em cada fase.

Diferentemente dos outros padrões na taxonomia que se concentram na ativação e no engajamento (envio de mensagens, personalização de conteúdo, ativação de públicos), esse padrão se concentra na compreensão — análise do comportamento do cliente, medição do desempenho da campanha, identificação de tendências e geração de insights que informam as decisões de estratégia e otimização. É o padrão e os pares mais compostos com quase todos os padrões de ativação ou personalização.

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

## Padrão do caso de uso

**Análise de clientes e geração de insight**

Crie espaços de trabalho de análise entre canais, métricas calculadas e painéis para entender o comportamento do cliente e o desempenho da campanha.

**Cadeia de funções:** Conexão de Dados > Configuração de Visualização de Dados > Análise do Workspace > Criação de Métricas Computadas > Publicação de Painel

Consulte a seção [Opções de implementação](#implementation-options) para obter orientação sobre composição.

## Aplicativos

Os aplicativos a seguir são usados neste padrão de caso de uso.

- **[!DNL Customer Journey Analytics] (CJA)** — Conexões, visualizações de dados, análise de espaço de trabalho, análise guiada, métricas computadas, painéis, publicação de público e análise de conteúdo
- **[!DNL Adobe Experience Platform] (AEP)** — Data lake, conjuntos de dados, esquemas XDM, dados de perfil e evento que alimentam conexões do CJA

## Funções básicas

Os seguintes recursos básicos devem estar em vigor para esse padrão de caso de uso. Para cada função, o status indica se ele é tipicamente necessário, se presume ser pré-configurado ou se não é aplicável.

| Função de base | Status | O que deve estar em vigor | Referência do Experience League |
| --- | --- | --- | --- |
| Administração e governança | Presumido em vigor | Perfil de produto do CJA provisionado com criação de espaço de trabalho e permissões de acesso de visualização de dados. Conjuntos de dados do AEP acessíveis à conexão do CJA. Usuários atribuídos às funções apropriadas do CJA. | [Visão geral do controle de acesso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Preparação e modelagem de dados | Obrigatório | Os esquemas XDM e conjuntos de dados que serão conectados à CJA devem existir no AEP. O design do esquema afeta diretamente quais dimensões e métricas estão disponíveis nas visualizações de dados do CJA. Esquemas de evento precisam de campos de carimbo de data e hora; esquemas de pesquisa precisam de campos-chave. | [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home) |
| Fontes de dados e coleção | Obrigatório | Os dados devem estar fluindo para conjuntos de dados do AEP — eventos da Web por meio da Web SDK, eventos de aplicativo por meio do Mobile SDK, eventos de campanha do AJO e dados de CRM por meio de conectores de origem. A riqueza da análise depende da amplitude dos dados coletados. | [Visão geral das fontes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home) |
| Configuração de identidade e perfil | Obrigatório | A configuração da ID de pessoa na conexão do CJA determina como os eventos são compilados nos conjuntos de dados. A compilação de identidade entre dispositivos no AEP melhora a capacidade da CJA de criar jornadas completas para o cliente. O namespace de identidade deve ser configurado para o campo ID de pessoa. | [Visão geral do Serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home) |
| Definição e segmentação do público-alvo | Não se aplica | O CJA cria seus próprios filtros e públicos-alvo no contexto da análise. Os públicos-alvo da RT-CDP não são um pré-requisito, embora o CJA possa publicá-los de volta no AEP por meio da publicação de públicos-alvo (opção C). | [Visão geral do Serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home) |

## Funções de suporte

Os recursos a seguir aumentam esse padrão de caso de uso, mas não são necessários para a execução principal.

| Função de suporte | Status | Por que é importante | Referência do Experience League |
| --- | --- | --- | --- |
| Criação de atributo calculado/derivado | Recomendado | Os atributos calculados do AEP podem enriquecer os conjuntos de dados conectados ao CJA, fornecendo dimensões e métricas adicionais para análise (por exemplo, contagem de compras vitalícias, dias desde a última atividade). Essas agregações no nível do perfil ficam disponíveis como dimensões nas visualizações de dados do CJA. | [Visão geral dos atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Gerenciamento do ciclo de vida dos dados | Recomendado | As políticas de retenção de conjuntos de dados afetam quais dados históricos estão disponíveis no CJA. Normalmente, a retenção longa é desejada para que o Analytics permita comparações ano a ano e análises de tendências de longo prazo. Configure os TTLs do conjunto de dados para garantir uma profundidade histórica adequada. | [Visão geral do Gerenciamento Avançado do Ciclo de Vida dos Dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| Rotulagem e aplicação de uso de dados | Recomendado | Os rótulos de governança em campos confidenciais podem restringir o que aparece nas visualizações de dados do CJA. Se as PII ou os dados confidenciais forem incluídos na conexão do CJA, os rótulos de governança de dados garantirão o acesso compatível e evitarão a exposição não autorizada nos painéis compartilhados. | [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| Monitoramento e capacidade de observação | Recomendado | A integridade da conexão do CJA e a atualização de dados devem ser monitoradas. Configure alertas para falhas de fluxo de dados de origem e problemas de assimilação para garantir que a alimentação de dados do CJA seja confiável e atualizada. | [Visão geral dos Insights de Capacidade de Observação](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| Relatórios e análise | Incluído | Essa é a implementação do relatórios e da análise. Quando um plano de referência para outro padrão incluir S5, use este plano de geração de análise do cliente e insight para a implementação de análise. | [visão geral do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## Funções do aplicativo

Este plano utiliza as seguintes funções do catálogo de funções do aplicativo. As funções são mapeadas para fases de implementação em vez de etapas numeradas.

### [!DNL Customer Journey Analytics] (CJA)

A tabela a seguir lista as funções de aplicativo do CJA usadas nesse padrão.

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Conexão de dados | Fase 1: Conexão de dados | Vincule conjuntos de dados do AEP a uma conexão do CJA para análise entre canais, configuração de tipos de conjunto de dados e ID de pessoa para compilação entre conjuntos de dados |
| Configuração da visualização de dados | Fase 2: Configuração da visualização de dados | Definir dimensões, métricas, modelos de atribuição, configurações de persistência, parâmetros de sessão e campos derivados que moldam a perspectiva analítica |
| Análise do Workspace | Fase 3: Análise e criação de métricas | Crie projetos de análise de forma livre com tabelas, visualizações, filtros, anotações e detalhamentos de dimensão (Opções A, B, C) |
| Análise guiada | Fase 3: Análise e criação de métricas | Use fluxos de trabalho estruturados e guiados para análise de funnel, tendências, retenção, crescimento de usuários e frequência de engajamento (opção D) |
| Criação de métricas calculadas | Fase 3: Análise e criação de métricas | Defina métricas calculadas usando fórmulas, filtros e funções para KPIs reutilizáveis como taxa de conversão, pontuação de engajamento e receita por visita |
| Publicação de painel e scorecard | Fase 4: Publicação do painel | Crie e compartilhe painéis interativos e scorecards para dispositivos móveis para relatórios das partes interessadas |
| Publicação de público alvo | Fase 5: Publicação de público-alvo (somente opção C) | Publicar públicos-alvo definidos pela CJA de volta no Perfil do cliente em tempo real da AEP para ativação downstream |
| Content Analytics | Fase 3: Análise e criação de métricas | Analise tendências de desempenho do conteúdo, anomalias e fadiga em propriedades digitais (quando a análise de conteúdo é o foco) |

### [!DNL Adobe Experience Platform] (AEP)

A tabela a seguir lista as funções de aplicativo do AEP usadas nesse padrão.

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Data Lake e conjuntos de dados | Pré-requisito (F2, F3) | Forneça o evento de origem, o perfil e os conjuntos de dados de pesquisa que alimentam a conexão do CJA |
| Serviço de identidade | Pré-requisito (F4) | Fornecer configuração de namespace de identidade para compilação de ID de pessoa em conjuntos de dados na conexão do CJA |

## Pré-requisitos

Os seguintes pré-requisitos devem ser atendidos antes de implementar esse padrão de caso de uso.

- O direito ao produto CJA é provisionado para a organização
- Os perfis de produto do CJA são configurados com acesso de usuário apropriado (criação de espaço de trabalho, acesso à visualização de dados)
- A sandbox da AEP contém os conjuntos de dados de destino com fluxo de dados (eventos da Web, eventos de aplicativo, dados de campanha, registros de CRM)
- Os esquemas XDM são definidos para todos os conjuntos de dados de origem com grupos de campos apropriados
- O campo ID de pessoa é identificado e está consistentemente disponível em todos os conjuntos de dados que serão conectados
- Os namespaces de identidade são configurados no AEP para a ID de pessoa usada na compilação de conexão do CJA
- Os requisitos das partes interessadas estão documentados: quais KPIs, quais públicos-alvo consumirão painéis e qual nível de detalhes
- Para cartões de pontuação móveis: as partes interessadas têm o aplicativo móvel de [!DNL Adobe Analytics] painéis instalado
- Para opção C (Publicação de público-alvo): o Perfil do cliente em tempo real do AEP está ativado na sandbox de destino
- Para a Opção D (Análise guiada): o SKU do CJA inclui recursos de análise guiada

## Opções de implementação

Esta seção descreve as opções de implementação disponíveis para este padrão de caso de uso.

### Opção A: análise de desempenho da campanha

**Melhor para:** Medir e otimizar a eficácia da campanha e da jornada — painéis de campanha de email, análise do jornada funnel, comparação de desempenho do canal e relatórios de ROI de marketing.

**Como funciona:**

Essa opção conecta conjuntos de dados do AJO campaign e do jornada ao CJA, configura visualizações de dados com métricas de entrega e envolvimento (envios, entregas, aberturas, cliques, devoluções, cancelamentos de assinatura), cria painéis de desempenho da campanha e publica cartões de pontuação para as partes interessadas de marketing. O foco é entender como as campanhas de marketing se comportam entre canais e ao longo do tempo.

A visualização de dados é configurada com dimensões específicas da campanha (nome da campanha, nome da jornada, tipo de canal, variante de mensagem) e métricas de entrega. As métricas calculadas são criadas para medidas derivadas, como taxa de abertura, taxa de cliques, taxa de conversão e receita por mensagem. Os painéis apresentam esses KPIs com períodos de comparação para análise de tendência.

**Principais considerações:**

- Exige conjuntos de dados de eventos de jornada e campanha do AJO na AEP
- Os modelos de atribuição devem se alinhar à filosofia de medição de campanha da organização
- Considere incluir relatórios nativos do AJO (para métricas de entrega operacional) e CJA (para impacto nos negócios entre canais)

**Vantagens:**

- Criado especificamente para medição e otimização de campanha
- Permite a comparação entre campanhas e a análise da combinação de canais
- As métricas computadas fornecem definições de KPI padronizadas em todas as campanhas
- Os cartões de pontuação móveis oferecem desempenho instantâneo aos líderes de marketing

**Limitações:**

- Limitado aos dados de campanha e jornada; não fornece o contexto completo de jornada do cliente
- Não inclui definição de caminho de jornada, fallout ou análise de coorte
- A atribuição tem como escopo os pontos de contato da campanha em vez da jornada completa do cliente

**Experience League:**

- [Guia de integração do AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Visão geral do Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

### Opção B: análise de jornada do cliente

**Recomendado para:** Noções básicas sobre jornadas de clientes entre canais — análise de fallout, análise de caminho, retenção de coorte, modelagem de atribuição e análise de estágio de ciclo de vida entre pontos de contato da Web, do aplicativo, do email, do CRM e offline.

**Como funciona:**

Essa opção conecta vários conjuntos de dados do AEP (eventos da Web, eventos de aplicativo, dados de CRM, interações de campanha, registros transacionais) para criar uma visualização unificada entre canais da jornada do cliente. A visualização de dados é configurada com dimensões e métricas que abrangem todos os canais. As visualizações de fluxo, fallout, coorte e atribuição do CJA são usadas para analisar como os clientes se movem pelas jornadas, onde são soltos, como os diferentes segmentos retêm e quais canais merecem crédito por conversões.

Essa é a opção analítica mais abrangente, fornecendo um insight profundo na experiência completa do cliente. Também é a mais complexa de implementar, exigindo uma configuração cuidadosa da ID de pessoa para a compilação entre conjuntos de dados e um design de visualização de dados elaborado para expor as dimensões e métricas certas.

**Principais considerações:**

- Exige uma ID de pessoa consistente em todos os conjuntos de dados conectados para uma análise precisa entre canais
- O design do esquema no AEP afeta diretamente a qualidade e a profundidade da análise do CJA
- Mais conjuntos de dados na conexão significam análises mais avançadas, mas tempos de preenchimento retroativo mais longos
- A modelagem de atribuição requer definições claras de evento de conversão

**Vantagens:**

- Visibilidade completa da jornada de clientes entre canais
- Conjunto completo de visualizações do CJA: tabelas de fluxo, fallout, coorte, atribuição e forma livre
- Permite a descoberta de insights que são invisíveis nos relatórios de canal único
- Oferece suporte a perguntas analíticas complexas sobre o comportamento e o ciclo de vida do cliente

**Limitações:**

- Maior complexidade de implementação devido a conexões de vários conjuntos de dados e compilação entre canais
- Requer mais planejamento antecipado para configuração de visualização de dados e campos derivados
- O preenchimento retroativo para conexões grandes de vários conjuntos de dados pode levar dias
- A qualidade da análise depende da integridade e da consistência dos dados subjacentes

**Experience League:**

- [Visão geral das conexões](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [Visualização de fluxo](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [Visualização Fallout](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [Tabela de coorte](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [Painel de atribuição](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/attribution)

### Opção C: Analytics com publicação de público-alvo

**Recomendado para:** Ativação orientada por análise — descubra segmentos interessantes por meio da análise do CJA e publique-os de volta no AEP para ativação por meio de destinos RT-CDP, campanhas do AJO ou jornadas do AJO.

**Como funciona:**

Essa opção estende a Opção A ou a Opção B com a publicação de público-alvo do CJA. Os analistas criam segmentos no CJA usando dados comportamentais entre canais e o poder analítico total dos filtros do CJA e, em seguida, publicam esses públicos no Perfil do cliente em tempo real da AEP para ativação downstream. Isso elimina a lacuna entre o insight e a ação — os segmentos descobertos durante a análise exploratória se tornam públicos acionáveis sem exigir recriação manual no Construtor de segmentos do AEP.

Os públicos publicados aparecem no AEP Audience Portal com a origem &quot;CJA&quot; e podem ser ativados para qualquer destino da RT-CDP, usados como destinos de campanha no AJO ou usados como condições de entrada de jornada.

**Principais considerações:**

- Exige que o Perfil de cliente em tempo real do AEP esteja ativado na sandbox de destino
- A conexão do CJA deve ter uma ID de pessoa válida que resolva para um namespace de identidade do AEP
- Os públicos publicados são contados para o direito de público-alvo da AEP da organização
- A cadência de atualização deve ser configurada com base nos requisitos de ativação (uma vez, a cada 4 horas, diariamente, semanalmente)

**Vantagens:**

- Fecha o loop entre análise e ativação
- Permite a detecção de segmentos de alto valor usando dados comportamentais entre canais da CJA
- Os públicos definidos no CJA podem aproveitar dimensões e filtros não disponíveis no Construtor de segmentos do AEP
- Suporta refinamento iterativo de critérios de público com base em insights analíticos

**Limitações:**

- No máximo 75 públicos-alvo publicados por cliente da CJA
- A avaliação inicial do público pode levar até 24 horas para conjuntos de dados grandes
- Públicos publicados pela CJA não podem ser editados no AEP — as alterações devem ser feitas no CJA
- Requer configuração de perfil e namespace de identidade adicional além da análise básica

**Experience League:**

- [Visão geral dos públicos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [Criar e publicar públicos-alvo](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/publish)

### Opção D: análise guiada para equipes de produtos

**Recomendado para:** insights de experiência de produtos — adoção de recursos, tendências de engajamento do usuário, análise de retenção, conversão do funnel e análise de impacto de lançamento usando fluxos de trabalho de análise guiada da CJA sem exigir uma configuração complexa de projeto do Workspace de forma livre.

**Como funciona:**

Essa opção usa a Análise guiada do CJA para geração de insight estruturada e modelada. A análise guiada fornece tipos de análise pré-criados — funnel, tendências, retenção, crescimento de usuários, frequência de engajamento, impacto das versões, primeiro uso e linha do tempo — que orientam os analistas por um fluxo de trabalho estruturado para responder perguntas específicas sobre produtos e experiências. É ideal para gerentes e analistas de produtos que precisam de insights rápidos e focados sem criar projetos de forma livre do zero.

A implementação conecta conjuntos de dados do AEP ao CJA, configura uma visualização de dados com dimensões e métricas no nível do evento e usa fluxos de trabalho de análise guiada para gerar insights. Os resultados podem ser salvos como painéis nos projetos do Workspace para personalização adicional.

**Principais considerações:**

- A análise guiada exige os direitos do produto CJA, que incluem recursos de análise guiada
- Mais adequado para análise de produto e experiência do que para medição de desempenho de campanha
- Fornece fluxos de trabalho estruturados que são mais acessíveis a usuários não analistas
- Pode ser combinado com a análise de forma livre do Workspace para uma exploração mais profunda

**Vantagens:**

- Menor barreira à entrada — fluxos de trabalho estruturados orientam os usuários pela análise
- Desenvolvido especificamente para perguntas sobre a experiência do produto (funnel, retenção, crescimento, impacto)
- Tempo de implantação do insight mais rápido para perguntas analíticas comuns
- As análises salvas podem ser incorporadas aos projetos Workspace junto com a análise de forma livre

**Limitações:**

- Menos flexível que a análise de forma livre do Workspace
- Limitado aos tipos de análise pré-criados (funnel, tendências, retenção, crescimento, frequência, impacto, linha do tempo)
- As comparações de segmentos suportam até 3 segmentos simultaneamente
- A análise do funnel suporta no máximo 15 etapas

**Experience League:**

- [Visão geral da análise guiada](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/overview)
- [Visualização do funnel](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [Exibição de retenção](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/retention/retention-rates)

### Comparação de opções

A tabela a seguir compara as opções de implementação disponíveis.

| Critérios | Opção A: desempenho da campanha | Opção B: jornada do cliente | Opção C: Analytics + ativação | Opção D: análise guiada |
| --- | --- | --- | --- | --- |
| Melhor para | Medição e otimização de campanha | Noções básicas sobre a jornada entre canais | Ativação de público orientada pela insight | Insights de experiência do produto |
| Complexo | Low-Medium | Alta | Alta | Baixa |
| Conjuntos de dados necessários | Eventos de campanha/jornada do AJO | Vários conjuntos de dados entre canais | O mesmo que A ou B, além da identidade do perfil | Conjuntos de dados de evento com interações de produto |
| Visualizações principais | Tabelas de forma livre, números de resumo, linhas de tendência | Fluxo, fallout, coorte, atribuição | O mesmo que A ou B, além da publicação do público-alvo | Funnel, tendências, retenção, crescimento |
| Recurso de ativação | Não (somente relatórios) | Não (somente relatórios) | Sim (publica públicos no AEP) | Não (somente relatórios) |
| Público-alvo obrigatório | Analistas de marketing, gerentes de campanha | Analistas de dados, arquitetos do jornada | Analistas + equipes de ativação | Gerentes de produtos, analistas de crescimento |
| Funções do CJA usadas | Conexão, Visualização de dados, Workspace, Métricas calculadas, Painel | Conexão, Visualização de dados, Workspace, Métricas calculadas, Painel | O mesmo que A ou B, além de Publicação de público-alvo | Conexão, Visualização de dados, Análise guiada, Painel |
| Tempo até a primeira insight | Dias | Semanas | Semanas | Horas-Dias |

### Escolha a opção certa

Use as orientações a seguir para selecionar a opção de implementação que melhor atenda às suas necessidades.

- **Se sua meta principal for medir a eficácia da campanha** e você tiver dados de campanha do AJO fluindo para o AEP, comece com a **Opção A**. Ele oferece um tempo de implantação mais rápido para os relatórios de desempenho de marketing.

- **Se você precisar entender a jornada completa do cliente** na Web, no aplicativo, no email e nos pontos de contato offline, e tiver vários conjuntos de dados com uma ID de pessoa consistente, escolha **Opção B**. Ele fornece os recursos analíticos mais profundos, mas requer mais investimento inicial na configuração da visualização de dados.

- **Se você deseja agir com base em insights** publicando segmentos descobertos pela CJA de volta no AEP para ativação no RT-CDP ou no AJO, escolha **Opção C**. Isso estende a Opção A ou B com a publicação de público-alvo e requer a configuração do Perfil do cliente em tempo real do AEP.

- **Se sua equipe precisar de insights de produto rápidos e estruturados** sem a complexidade dos projetos de forma livre da Workspace e se a sua SKU do CJA incluir análise guiada, escolha a **Opção D**. É o caminho mais rápido para responder a perguntas específicas sobre experiência de produtos.

- **Muitas organizações implementam várias opções**: Opção A para painéis de campanha da equipe de marketing, Opção B para a análise entre canais da equipe de análise e Opção D para insights de autoatendimento da equipe de produtos. Essas opções compartilham a mesma conexão CJA e infraestrutura de visualização de dados.

## Fases de implementação

Esta seção detalha as fases de implementação passo a passo para esse padrão de caso de uso.

### Fase 1: Conexão de dados

**Função de aplicativo:** CJA: conexão de dados

Essa fase configura uma conexão do CJA que vincula um ou mais conjuntos de dados do AEP à CJA para análise. A conexão define quais conjuntos de dados fluem para o CJA, como os eventos são compilados entre conjuntos de dados por meio da ID de pessoa e como os dados históricos e de transmissão são assimilados. Esse é o link fundamental entre o data lake da AEP e o CJA.

#### Pontos de decisão

As decisões a seguir devem ser tomadas durante essa fase.

>[!NOTE]
>**Decisão: seleção de sandbox do AEP**
>
>Qual sandbox da AEP contém os conjuntos de dados de origem?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Sandbox de produção | Dados dinâmicos do cliente para relatórios de produção | Use para painéis de produção e relatórios das partes interessadas |
>| Sandbox de desenvolvimento | Teste e iteração antes da implantação de produção | Use para configuração e validação iniciais antes de promover para produção |

>[!NOTE]
>**Decisão: seleção de conjunto de dados e designação de tipo**
>
>Quais conjuntos de dados do AEP devem ser incluídos na conexão e qual tipo deve ser atribuído a cada um?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Conjuntos de dados de evento | Dados comportamentais com carimbo de data e hora (interações da Web, eventos de aplicativo, interações de campanha, transações) | Requer um campo de carimbo de data e hora; é o núcleo da maioria das análises |
>| Pesquisar conjuntos de dados | Dados de referência de valores-chave (catálogo de produtos, metadados de campanha, locais de armazenamento) | Associado aos dados do evento por meio de uma chave compartilhada; somente o estado mais recente é usado |
>| Conjuntos de dados do perfil | Atributos de nível de pessoa (nível de fidelidade, valor vitalício, atributos de CRM) | Fornecer enriquecimento no nível da pessoa; somente o estado mais recente é usado |

>[!NOTE]
>**Decisão: configuração de ID de pessoa**
>
>Qual campo serve como a ID de pessoa para a compilação entre conjuntos de dados?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| ID do CRM | A organização tem um identificador de CRM consistente entre canais | Fornece a compilação entre canais mais precisa para clientes conhecidos |
>| ECID (Experience Cloud ID) | Analisar principalmente o comportamento anônimo da Web/do aplicativo | Com escopo de dispositivo; não compila entre dispositivos sem resolução de identidade |
>| Email (com hash) | O email é o identificador comum entre conjuntos de dados | Funciona bem quando o email é capturado consistentemente nos pontos de contato |
>| Namespace personalizado | A organização usa um identificador proprietário | Deve corresponder a um namespace de identidade da AEP para publicação de público-alvo (Opção C) |

>[!NOTE]
>**Decisão: intervalo de preenchimento retroativo**
>
>Quantos dados históricos devem ser importados para a conexão?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Todos os dados existentes | Profundidade histórica máxima necessária para comparações ano a ano e tendências de longo prazo | O preenchimento retroativo de grandes conjuntos de dados (bilhões de registros) pode levar dias para ser concluído |
>| Intervalo de datas personalizado | Somente o histórico recente é relevante ou a otimização do armazenamento é uma preocupação | Limita a profundidade histórica disponível para análise |
>| Sem preenchimento retroativo | Somente uma análise prospetiva é necessária | Configuração de conexão mais rápida; nenhum dado histórico disponível até que novos dados fluam no |

>[!NOTE]
>**Decisão: habilitação de streaming**
>
>Os novos dados devem fluir para o CJA em tempo quase real?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Ativar transmissão | São necessários relatórios quase em tempo real (dados disponíveis em aproximadamente 90 minutos após a assimilação do AEP) | Mais comum para conexões de produção; permite a análise oportuna |
>| Somente lote | A atualização periódica é suficiente e o streaming não é necessário | Configuração mais simples; dados disponíveis após o processamento em lote |

#### Configurar conexão de dados

**Navegação da interface do usuário:** CJA > Conexões > Criar nova conexão

Principais detalhes de configuração:

- O nome e a descrição da conexão devem seguir as convenções de nomenclatura organizacionais
- O número médio de eventos diários é usado para o planejamento de capacidade do CJA
- Todos os conjuntos de dados em uma única conexão devem vir da mesma sandbox da AEP
- Os campos ID de pessoa devem ser consistentes em todos os conjuntos de dados para uma compilação precisa entre conjuntos de dados
- Verifique se o campo ID de pessoa existe e está preenchido em cada conjunto de dados antes de adicioná-lo à conexão

**Documentação do Experience League:**

- [Visão geral das conexões](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [Criar ou editar uma conexão](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [Gerenciar conexões](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/manage-connections)
- [Medidas de proteção do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-admin/guardrails)

### Fase 2: configuração da visualização de dados

**Função de aplicativo:** CJA: configuração de visualização de dados

Essa fase configura uma visualização de dados que define como os dados da conexão aparecem na análise. A visualização de dados determina quais campos de esquema são expostos como dimensões e métricas, como os valores são atribuídos e persistentes, como as sessões são definidas e quais campos derivados transformam dados brutos em componentes prontos para análise. Várias visualizações de dados podem ser criadas a partir de uma única conexão para diferentes perspectivas analíticas.

#### Pontos de decisão

As decisões a seguir devem ser tomadas durante essa fase.

>[!NOTE]
>**Decisão: nomeação de contêiner**
>
>Qual terminologia os contêineres devem usar para corresponder ao domínio de negócios?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Padrão (Pessoa / Sessão / Evento) | A terminologia padrão do Analytics é entendida pela equipe | Funciona com a maioria das implementações |
>| Nomes personalizados (por exemplo, Comprador/Visita/Interação) | A terminologia específica para o domínio de negócios melhora a adoção de usuários | Ajuda as partes interessadas não técnicas a entender o escopo da análise |
>| Nomes B2B (por exemplo, Conta / Envolvimento / Ponto de contato) | Análise B2B, onde a análise no nível da conta é o foco | Alinha o escopo do contêiner aos conceitos de negócios B2B |

>[!NOTE]
>**Decisão: tempo limite da sessão**
>
>Por quanto tempo de inatividade define um limite de sessão?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| 30 minutos (padrão) | Definição de sessão padrão do Web Analytics | Padrão do setor; alinha-se à maioria dos benchmarks de análise |
>| 15 minutos | Conteúdo em formato curto ou sites transacionais nos quais os usuários concluem tarefas rapidamente | Cria mais sessões; pode capturar melhor intenções distintas do usuário |
>| 60 minutos ou mais | Conteúdo de forma longa, interações complexas B2B ou jornadas com muita pesquisa | Menos sessões; captura pesquisas estendidas como sessões únicas |
>| Personalizar com novos eventos de sessão | Determinados eventos (por exemplo, inicialização de aplicativos, click-through de campanha) sempre devem iniciar uma nova sessão | Fornece limites de sessão orientados por lógica de negócios |

>[!NOTE]
>**Decisão: padrões do modelo de atribuição**
>
>Qual modelo de atribuição padrão deve ser aplicado às métricas de conversão?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Último contato (padrão) | O crédito deve ir para o ponto de contato mais recente antes da conversão | Simples e intuitivo; pode desvalorizar os canais de percepção |
>| Primeiro contato | Compreender quais canais impulsionam a percepção e a aquisição iniciais | Útil para análise de aquisição; ignora pontos de contato de nutrição |
>| Linear | Todos os pontos de contato devem compartilhar o mesmo crédito | Distribuição justa; pode diluir o impacto dos principais pontos de contato |
>| Decaimento de tempo | Os pontos de contato recentes devem receber mais crédito do que os distantes | Recenticidade de saldos com contribuição histórica |
>| Em forma de U | O primeiro e o último ponto de contato merecem mais crédito | Bom para entender os canais de aquisição e fechamento |
>| Algorítmico | Atribuição orientada por dados usando modelos de IA da CJA | Mais preciso, mas requer volume de dados de conversão suficiente |

>[!NOTE]
>**Decisão: lógica de campo derivada**
>
>São necessárias regras de negócios personalizadas para transformar dados brutos em dimensões prontas para análise?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Classificação de canal de marketing (Ocorrência Quando) | Os códigos de rastreamento brutos precisam ser classificados em grupos de canais | Caso de uso de campo derivado mais comum; crítico para análise de canal |
>| Segmentação de valores | Os valores contínuos precisam ser agrupados em intervalos (por exemplo, níveis de valor de pedido) | Simplifica a análise de métricas contínuas |
>| Mesclagem de campos | Vários campos de origem devem ser combinados em uma única dimensão | Útil quando o mesmo conceito existe em diferentes caminhos de esquema entre conjuntos de dados |
>| Extração baseada em regex | Os valores estruturados precisam ser analisados (por exemplo, extração do tipo de campanha do código de campanha) | Poderoso, mas requer design de padrão de regex cuidadoso |

#### Configurar visualização de dados

**Navegação da interface do usuário:** CJA > Visualizações de dados > Criar nova visualização de dados

Principais detalhes de configuração:

- Selecione a conexão principal criada na Fase 1
- Configurar fuso horário e tipo de calendário para corresponder aos requisitos de relatórios
- Mapear campos de esquema XDM para dimensões com configurações de persistência (alocação e expiração) apropriadas
- Mapear campos de esquema XDM para métricas com formato (decimal, número inteiro, moeda, porcentagem, hora) e configurações de atribuição
- Configurar regras de inclusão/exclusão em dimensões para filtrar valores irrelevantes
- Ativar a desduplicação de métrica onde necessário para evitar a dupla contagem
- Criar campos derivados para classificação de canal de marketing, segmentação de valor ou mesclagem de campos
- Máximo de 5.000 dimensões e 5.000 métricas por visualização de dados
- Máximo de 100 campos derivados por visualização de dados

#### Onde as opções divergem

**Para a Opção A (Análise de desempenho de campanha):**

Mapear dimensões específicas da campanha: nome da campanha, nome da jornada, tipo de canal, variante de mensagem, linha de assunto. Mapear métricas de entrega: envios, entregas, aberturas, cliques, devoluções, cancelamentos de assinatura. Configure a atribuição em métricas de conversão com base na filosofia de medição da campanha.

**Para a Opção B (Análise de jornada do cliente):**

Mapear dimensões entre canais: nome da página, tela do aplicativo, canal, campanha, produto, tipo de conteúdo. Mapeie as métricas de envolvimento e conversão em todos os canais. Configurar vários modelos de atribuição para análise de comparação. Crie campos derivados para classificação de canal e identificação de estágio de jornada.

**Para a Opção D (Análise Guiada):**

Mapeie dimensões e métricas de nível de evento relevantes para a análise de experiência do produto: nome do recurso, ação do usuário, tipo de envolvimento. Concentre-se em eventos que definem etapas do funnel, critérios de retenção e sinais de crescimento.

**Documentação do Experience League:**

- [Visão geral das visualizações de dados](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)
- [Criar ou editar uma visualização de dados](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Visão geral das configurações de componente](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [Configurações de persistência](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [Configurações de atribuição](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [Configurações de formato](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/format)
- [Desduplicação de métrica](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication)
- [Incluir/excluir valores](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/include-exclude-values)
- [Configurações da sessão](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/session-settings)
- [Campos derivados](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/derived-fields)

### Fase 3: Análise e criação de métricas

**Função do aplicativo:** CJA: Workspace Analysis, CJA: Análise Guiada, CJA: Criação de Métrica Computada

Essa fase cria os espaços de trabalho de análise (projetos de forma livre ou análise guiada), métricas computadas para KPIs derivados, filtros para análise segmentada e anotações para eventos principais. É aqui que o valor analítico é realizado — a criação de tabelas, visualizações e métricas que respondam a perguntas comerciais.

#### Pontos de decisão

As decisões a seguir devem ser tomadas durante essa fase.

>[!NOTE]
>**Decisão: abordagem de análise**
>
>Essa análise deve usar projetos Workspace de forma livre ou fluxos de trabalho de análise guiada?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Workspace de forma livre (Opções A, B, C) | Análise exploratória profunda, layouts personalizados, detalhamentos complexos e visualizações avançadas | Flexibilidade máxima; exige habilidade de analista; oferece suporte a todos os tipos de visualização |
>| Análise Guiada (Opção D) | Insights estruturados do produto, respostas rápidas a perguntas específicas, menos usuários técnicos | Tempo de insight mais rápido; limitado aos tipos de análise pré-criados; economiza no Workspace para maior personalização |
>| Ambos | A organização precisa de análises profundas e insights estruturados rápidos | Usar análise guiada para perguntas comuns; Workspace para exploração profunda |

>[!NOTE]
>**Decisão: tipos de visualização**
>
>Quais visualizações melhor comunicam os insights para este caso de uso?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Tabela de forma livre | Exploração detalhada de dados com detalhamentos de dimensão | Base da maioria das análises; suporta até dez níveis de detalhamento |
>| Visualização de fluxo | Noções básicas sobre o comportamento da definição de caminho (fluxo de página, transições de canal) | Excelente para descoberta de caminho de jornada; pode ser complexo com alta cardinalidade |
>| Visualização Fallout | Medir a conversão por meio de uma sequência definida de pontos de contato | Melhor para a análise da funnel; mostra claramente a queda em cada etapa |
>| Tabela de coorte | Análise de retenção ao longo do tempo por coorte de aquisição | Mostra como os diferentes grupos são mantidos; crítico para a análise do ciclo de vida |
>| Painel de atribuição | Comparação de modelos de atribuição para métricas de conversão | Comparação de modelo lado a lado; requer definição clara do evento de conversão |
>| Número do resumo / alteração | Exibição do KPI executivo com comparação período a período | Exibição de métrica simples e rápida; ideal para cabeçalhos de painéis de controle |

>[!NOTE]
>**Decisão: fórmulas de métrica computada**
>
>Quais KPIs de negócios exigem métricas calculadas além das métricas de visualização de dados base?
>
>| Padrão de métrica | Exemplo de fórmula | Quando usar |
>| --- | --- | --- |
>| Taxa / Taxa | Pedidos/visitas | Taxa de conversão, taxa de cliques, taxa de rejeição |
>| Métrica filtrada | Receita (em que canal = &quot;email&quot;) | Medidas específicas por canal ou por segmento |
>| Média por item | Receita / Pedidos | Valor médio de pedido, receita por visita |
>| Fórmula composta | (Receita - Custo) / Receita | Percentual de margem, cálculos de ROI |
>| Pontuação de engajamento | Soma ponderada de interações | Pontuação de engajamento composto em canais |

#### Configurar análise e métricas

**Navegação da interface do usuário:**

- Workspace: CJA > Workspace > Projetos > Criar projeto > Projeto em branco
- Análise guiada: CJA > Início > Análise guiada (ou Workspace > Criar > Análise guiada)
- Métricas calculadas: CJA > Componentes > Métricas calculadas > Criar
- Filtros: CJA > Componentes > Filtros > Criar filtro

Principais detalhes de configuração:

- Selecione a visualização de dados criada na Fase 2 como a visualização de dados do projeto
- Definir intervalos de datas e períodos de comparação apropriados para a análise
- Criar tabelas de forma livre arrastando dimensões para linhas e métricas para colunas
- Adicione detalhamentos de dimensão para explorar dados em níveis mais profundos (por exemplo, canal por campanha, página por produto)
- Criar filtros reutilizáveis (segmentos) para análise específica do público-alvo (escopo de nível de pessoa, nível de sessão ou nível de evento)
- Adicione anotações para marcar os principais eventos de negócios (lançamentos de produtos, campanhas, incidentes)
- Definir o formato de métrica calculada (decimal, porcentagem, moeda, tempo) e a polaridade (para cima é bom/para cima é ruim)
- Compartilhar projetos do espaço de trabalho com usuários do CJA em permissões de exibição ou edição

#### Onde as opções divergem

**Para a Opção A (Análise de desempenho de campanha):**

Crie tabelas de forma livre com dimensões de campanha detalhadas por métricas de entrega e envolvimento. Crie métricas calculadas para taxa de abertura, taxa de cliques, taxa de conversão, receita por mensagem e ROI da campanha. Adicione visualizações de tendências para rastrear o desempenho da campanha ao longo do tempo. Comparar variantes de campanha com a comparação de segmentos.

**Para a Opção B (Análise de jornada do cliente):**

Crie visualizações de fallout para identificar os pontos de devolução da jornada. Crie visualizações de fluxo para descobrir padrões de navegação em canais. Crie tabelas de coorte para medir a retenção por coorte de aquisição. Configure o painel de atribuição para comparar modelos de atribuição para métricas de conversão. Crie métricas calculadas para a taxa de conclusão da jornada, a pontuação de engajamento entre canais e a conversão de estágios do ciclo de vida.

**Para a Opção C (Analytics com publicação de público-alvo):**

Crie os espaços de trabalho de análise da Opção A ou B e identifique segmentos de alto valor ou com baixo desempenho durante a análise. Crie filtros do CJA que capturam esses segmentos para publicação na Fase 5.

**Para a Opção D (Análise Guiada):**

Selecione o tipo de análise guiada apropriado com base na pergunta comercial. Configure eventos importantes, intervalos de datas, métodos de contagem e comparações de segmentos. Salve análises concluídas como painéis em projetos do Workspace para personalização adicional.

**Documentação do Experience League:**

- [Visão geral do Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Criar um projeto](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [Tabela de forma livre](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [Visualização de fluxo](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [Visualização Fallout](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [Tabela de coorte](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [Painel de atribuição](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [Detalhamento de dimensões](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)
- [Visão geral dos filtros](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [Criar filtros](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [Visão geral de anotações](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/annotations/overview)
- [Visão geral das métricas calculadas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [Criar métricas calculadas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [Funções de métrica calculada](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-functions)
- [Visão geral da análise guiada](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/overview)
- [Visualização do funnel](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [Exibição de tendências](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/trends/usage)
- [Exibição de retenção](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/retention/retention-rates)
- [Visualização de crescimento ativa](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/user-growth/active)
- [Exibição da frequência de engajamento](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/trends/frequency)
- [Visualização do impacto da versão](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/impact/release)
- [Content Analytics](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/content-analytics/content-analytics)

### Fase 4: publicação do painel

**Função do aplicativo:** CJA: publicação de painel e scorecard

Essa fase cria painéis interativos (projetos do Workspace) e scorecards para dispositivos móveis que fornecem visibilidade de KPI às partes interessadas. Os painéis fornecem visibilidade executiva e operacional por meio de números de resumo, linhas de tendência, detalhamentos e anotações. Os cartões de pontuação móveis fornecem dados de desempenho instantâneos por meio do aplicativo móvel de painéis do [!DNL Adobe Analytics].

#### Pontos de decisão

As decisões a seguir devem ser tomadas durante essa fase.

>[!NOTE]
>**Decisão: Tipo de painel**
>
>Isso é um painel de Workspace de desktop, um cartão de pontuação móvel ou ambos?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Projeto do Workspace (desktop) | Painéis interativos detalhados para analistas e profissionais de marketing | Recursos de visualização completa; suporte a painéis, tabelas e layouts complexos |
>| Cartão de pontuação para dispositivo móvel | KPIs instantâneos para executivos e partes interessadas em dispositivos móveis | Limitado a 16 blocos; números de resumo com gráficos de tendência; requer aplicativo móvel |
>| Ambos | A organização precisa de análise detalhada e relatórios móveis de nível executivo | Artefatos separados, mas que podem compartilhar a mesma visualização de dados e métricas calculadas |

>[!NOTE]
>**Decisão: modelo de compartilhamento**
>
>Quem deve receber o painel e como?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Compartilhar com usuários específicos | Público-alvo limitado com necessidades de acesso específicas | O controle mais granular; requer gerenciamento de usuários individuais |
>| Compartilhar com grupo de perfis de produtos | Acesso em nível de equipe alinhado às funções organizacionais | Eficiente para distribuição em toda a equipe; gerenciado por meio de perfis de produtos da CJA |
>| Agendar entrega de email | Relatórios de PDF/CSV recorrentes para participantes que não fazem logon no CJA | Entrega automatizada; a frequência máxima é por hora; formatos PDF e CSV |

>[!NOTE]
>**Decisão: visibilidade da anotação**
>
>Os principais eventos devem ser anotados nas linhas de tendência do painel?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Sim — criar anotações | As principais campanhas, lançamentos de produtos, incidentes no site ou eventos sazonais podem explicar as tendências dos dados | As anotações são exibidas como marcadores em gráficos de linha e tendências de scorecard; fornecem contexto para picos ou declínios de dados |
>| Não | O público-alvo do painel está familiarizado com o contexto comercial e as anotações podem gerar desordem | Apresentação visual mais simples |

#### Configurar painéis

**Navegação da interface do usuário:**

- Painéis do Workspace: CJA > Workspace > Criar projeto
- Cartões de pontuação para dispositivos móveis: CJA > Projetos > Criar > Cartão de pontuação para dispositivos móveis
- Compartilhamento: CJA > Workspace > Compartilhar > Compartilhar com usuários do Workspace
- Entrega agendada: CJA > Workspace > Compartilhar > Agendar projeto

Principais detalhes de configuração:

- Para cartões de pontuação móveis, crie blocos que exibam uma única métrica com um número de resumo e uma tendência de minigráfico
- Configurar intervalos de datas padrão e períodos de comparação (por exemplo, últimos 30 dias em relação ao período anterior ou mês por mês)
- Adicionar filtros de escopo de público-alvo que os executivos podem alternar em cartões de pontuação móveis
- Configurar a entrega agendada de emails para relatórios recorrentes de PDF ou CSV
- Máximo de 16 blocos por cartão de pontuação móvel; máximo de 15 painéis por projeto do Workspace
- As anotações são limitadas a 100 por visualização de dados

**Documentação do Experience League:**

- [Criar um cartão de pontuação para dispositivos móveis](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [Configurar e preparar cartões de pontuação](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Painéis do Adobe Analytics — guia executivo](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/set-up-execs)
- [Compartilhar projetos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [Agendar projetos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [Visualização do número do resumo](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/summary-number-change)
- [Intervalos de datas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)

### Fase 5: Publicação de público-alvo (somente opção C)

**Função do aplicativo:** CJA: Publicação de público-alvo

Essa fase configura a publicação de público do CJA para enviar segmentos detectados na análise de volta para o Perfil do cliente em tempo real da AEP, para ativação downstream em destinos da RT-CDP, campanhas do AJO ou jornadas do AJO.

#### Pontos de decisão

As decisões a seguir devem ser tomadas durante essa fase.

>[!NOTE]
>**Decisão: Atualizar cadência**
>
>Com que frequência a associação de público-alvo deve ser atualizada?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Uma vez (instantâneo) | Público-alvo específico de campanha que não precisa de atualização contínua | Sem processamento em andamento; deve republicar para obter atualizações |
>| A cada 4 horas | Requisitos de ativação quase em tempo real | Maior custo de processamento; melhor para públicos sensíveis ao tempo |
>| Diariamente | Cadência de ativação de marketing padrão | Atualização e custo equilibrados; escolha mais comum |
>| Semanalmente | Públicos-alvo estáveis e que mudam lentamente | Processamento mínimo; adequado para segmentos de longo prazo |

>[!NOTE]
>**Decisão: namespace de identidade**
>
>Qual namespace de identidade a CJA deve usar para a resolução de membros do público-alvo?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| ID do CRM | Identificador de cliente principal da organização | Melhor precisão para correspondência de cliente conhecido |
>| ECID | Principalmente públicos-alvo baseados na Web/aplicativo | Com escopo de dispositivo; pode não ser resolvido para todos os registros de perfil |
>| Email (com hash) | O email é o identificador comum para ativação | Deve corresponder ao namespace usado na configuração de identidade do AEP |
>| Namespace personalizado | Identificador proprietário usado na organização | Deve ser configurado no Serviço de identidade da AEP |

#### Configurar publicação de público

**Navegação da interface do usuário:** CJA > Componentes > Públicos > Publicar público

Principais detalhes de configuração:

- Defina os critérios de público-alvo usando os filtros do CJA (escopo de pessoa, sessão ou container de evento)
- Selecione a visualização de dados e o filtro para publicar
- Configurar o namespace de identidade para a resolução de perfil do AEP
- Definir a cadência de atualização com base nas necessidades de ativação
- Monitorar o status de publicação na lista de Públicos-alvo da CJA (Componentes > Públicos-alvo > coluna Status)
- Verifique se o público-alvo aparece no AEP Audience Portal (Públicos-alvo > Procurar > Filtrar por origem &quot;CJA&quot;)
- Máximo de 75 públicos-alvo publicados por cliente da CJA (em todas as sandboxes)
- A avaliação inicial do público pode levar até 24 horas para conjuntos de dados grandes

**Documentação do Experience League:**

- [Visão geral dos públicos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [Criar e publicar públicos-alvo](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/publish)
- [Gerenciar públicos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/manage)
- [Visão geral do portal de público](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-portal)

## Considerações de implantação

Esta seção aborda medidas de proteção, armadilhas comuns, práticas recomendadas e decisões de compensação para esse padrão de caso de uso.

### Medidas de proteção e limites

As medidas de proteção e os limites a seguir se aplicam a esta implementação.

- **Limites de conexão:** o número máximo de conexões por organização é limitado pelo direito de SKU do CJA. Uma única conexão pode incluir conjuntos de dados de apenas uma sandbox da AEP. — [medidas de proteção do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-admin/guardrails)
- **Limites de exibição de dados:** Máximo de 5.000 dimensões e 5.000 métricas por exibição de dados. Máximo de 100 campos derivados por visualização de dados com até 5 níveis de funções aninhadas.
- **Limites do Workspace:** Máximo de 40 painéis por projeto. As tabelas de forma livre aceitam até 10 detalhamentos de dimensão. Máximo de 50.000 linhas por solicitação de relatório.
- **Limites do scorecard:** Máximo de 16 blocos por scorecard móvel.
- **Latência de transmissão:** Os dados de transmissão normalmente estão disponíveis no CJA dentro de 90 minutos após a assimilação do AEP.
- **Limites de publicação de público-alvo:** Máximo de 75 públicos-alvo publicados por cliente do CJA. A cadência mínima de atualização é a cada 4 horas.
- **Limites de análise guiada:** a análise do Funnel dá suporte a no máximo 15 etapas. As comparações de segmentos suportam até 3 segmentos simultaneamente.

### Armadilhas comuns

Esteja ciente dos seguintes problemas comuns ao implementar este padrão.

- **Incompatibilidade de ID de pessoa em conjuntos de dados:** todos os conjuntos de dados em uma conexão devem usar um campo de ID de pessoa consistente para análise entre conjuntos de dados. IDs de pessoa incompatíveis resultam em visualizações fragmentadas do cliente, onde a mesma pessoa aparece como várias pessoas. Verifique a consistência da ID de pessoa antes de criar a conexão.

- **Preenchimento retroativo demorando inesperadamente:** Conjuntos de dados grandes com bilhões de registros podem levar dias para serem preenchidos retroativamente. Planeje isso durante os cronogramas de implementação e inicie o preenchimento retroativo antecipadamente. Monitore o progresso na visualização de detalhes da conexão.

- **Exibição de dados que mostra &quot;Não especificado&quot; para a maioria dos valores de dimensão:** O campo de esquema mapeado pode ser populado de forma esparsa nos dados de origem. Verifique a qualidade dos dados no conjunto de dados de origem antes de assumir um erro de configuração. Considere usar um campo derivado para tratar valores nulos.

- **As contagens de sessões parecem incorretas:** as configurações de tempo limite de sessão afetam drasticamente as métricas de escopo de sessão. Um tempo limite muito curto cria mais sessões; um tempo limite muito longo cria menos. Os eventos de início de nova sessão também podem fragmentar sessões inesperadamente. Revisar e testar as configurações de sessão em relação aos padrões conhecidos de comportamento do usuário.

- **O modelo de atribuição não se aplica conforme esperado:** os modelos de atribuição se aplicam somente a métricas, não a dimensões. Verifique se a janela de lookback está definida adequadamente para o ciclo de negócios. As janelas de retrospectiva curtas podem perder pontos de contato iniciais do funnel.

- **Métricas calculadas que retornam zeros ou valores inesperados:** verifique se as métricas base referenciadas na fórmula têm dados na exibição de dados de destino para o intervalo de datas selecionado. Verifique a divisão por zero nas métricas de proporção. Recupere a definição da métrica e verifique a estrutura da fórmula.

- **Falha na publicação de público-alvo (Opção C):** A conexão do CJA deve ter uma ID de pessoa válida que resolva para um namespace de identidade do AEP. Verifique a configuração do namespace de identidade e se o Perfil do cliente em tempo real da AEP está ativado na sandbox de destino.

### Práticas recomendadas

Siga estas práticas recomendadas para uma implementação bem-sucedida.

- **Comece com uma única conexão abrangente:** Crie uma conexão que inclua todos os conjuntos de dados relevantes e, em seguida, crie várias visualizações de dados para diferentes perspectivas analíticas. Isso evita a proliferação de conexões e simplifica o gerenciamento.

- **Usar campos derivados para classificação de canal de marketing:** Em vez de depender de códigos de rastreamento brutos, crie campos derivados com lógica Case When para classificar o tráfego em canais de marketing. Isso garante relatórios de canal consistentes em todas as análises.

- **Criar um dicionário de métrica:** documentar todas as métricas computadas com suas fórmulas, uso pretendido e intervalos de valores esperados. Compartilhe este dicionário com a equipe de análise para garantir o uso consistente de métricas em todos os projetos.

- **Crie visualizações de dados para seu público-alvo:** Crie visualizações de dados separadas para diferentes grupos de partes interessadas: uma visualização de dados de marketing com dimensões e métricas focadas em campanha e uma visualização de dados do produto com dimensões de recurso e envolvimento. Isso simplifica as listas de componentes para cada grupo de usuários.

- **Anote tudo:** crie anotações para lançamentos de campanha, alterações no site, incidentes técnicos, sazonalidade e qualquer evento que possa explicar tendências de dados. As anotações fornecem contexto crítico ao revisar painéis meses depois.

- **Testar métricas computadas em relação a cálculos manuais:** Antes de confiar em uma métrica computada para painéis, execute um relatório lado a lado com a métrica computada e seus componentes básicos. Verifique se os valores calculados correspondem a um cálculo manual.

- **Usar filtros estrategicamente:** Crie filtros reutilizáveis para padrões de segmentação comuns (novos vs. recorrentes, móveis vs. desktop, por região geográfica). Aplique-os como filtros no nível do painel, em vez de incorporá-los em cada tabela de forma livre.

- **Monitorar a integridade da conexão regularmente:** Verifique a exibição de detalhes da conexão quanto a registros ignorados, lotes com falha e atrasos de transmissão. Problemas de qualidade de dados no nível da conexão afetam todas as análises de downstream.

### Decisões de compensação

Considere as seguintes compensações ao planejar sua implementação.

>[!NOTE]
>**Contrapartida: profundidade da análise vs. tempo de insight**
>
>A opção B (Análise de jornada do cliente) fornece os insights mais profundos entre canais, mas requer um investimento inicial significativo na configuração de conexão, no design da visualização de dados e na criação de campos derivados. A opção D (análise guiada) oferece tempo de insight mais rápido com fluxos de trabalho estruturados, mas oferece menos flexibilidade analítica.
>
>- **A Opção B favorece:** compreensão abrangente, análise de vários canais complexa, modelagem de atribuição, desenvolvimento de KPI personalizado
>- **A opção D favorece:** velocidade, acessibilidade para usuários não analistas, perguntas estruturadas sobre a experiência do produto
>- **Recomendação:** comece com a Opção D para obter insights imediatos do produto ao criar a infraestrutura da Opção B em paralelo. Muitas organizações executam ambas simultaneamente para equipes diferentes.

>[!NOTE]
>**Contrapartida: integridade do preenchimento retroativo vs. preparação da conexão**
>
>A importação de todos os dados históricos fornece profundidade analítica máxima para comparações ano a ano e análises de tendências de longo prazo, mas o preenchimento retroativo para conjuntos de dados grandes pode levar dias. Limitar o preenchimento retroativo a um período recente prepara a conexão mais rapidamente, mas limita a análise histórica.
>
>- **Todos os dados favorecem:** Análise de tendências de longo prazo, comparações ano a ano, análise de coorte com histórico estendido
>- **O preenchimento retroativo limitado favorece:** Disponibilidade de conexão mais rápida, tempo mais rápido para o primeiro painel, otimização de armazenamento
>- **Recomendação:** Preencha retroativamente todos os dados para conexões de produção que oferecem suporte à análise estratégica. Use preenchimento retroativo limitado para conexões de desenvolvimento e implementações de prova de conceito.

>[!NOTE]
>**Contrapartida: uma única visualização de dados abrangente vs. várias visualizações de dados focalizadas**
>
>Uma única visualização de dados com todas as dimensões e métricas fornece um espaço de trabalho analítico unificado, mas pode sobrecarregar os usuários com listas de componentes. Várias visualizações de dados focadas (uma por equipe ou caso de uso) simplificam a experiência do componente, mas exigem a manutenção de várias configurações.
>
>- **A visualização de dados única favorece:** Análise unificada, detalhamentos entre domínios, gerenciamento mais simples
>- **Várias exibições de dados favorecem:** Listas de componentes mais limpas, terminologia específica da equipe, diferentes definições de sessão por caso de uso
>- **Recomendação:** comece com uma exibição de dados principal e, em seguida, crie exibições de dados focadas adicionais se a complexidade da lista de componentes se tornar uma barreira para adoção. Todas as visualizações de dados podem fazer referência à mesma conexão.

>[!NOTE]
>**Contrapartida: streaming em tempo real vs. assimilação somente em lote**
>
>A ativação da transmissão na conexão do CJA fornece dados quase em tempo real (cerca de 90 minutos após a assimilação do AEP), mas processa mais dados continuamente. A assimilação somente em lote processa dados periodicamente e pode causar atrasos.
>
>- **Favorecimentos da transmissão:** Relatórios oportunos, monitoramento de campanhas ativas, painéis em tempo quase real
>- **Somente em lote favorece:** configuração mais simples, janelas de processamento previsíveis, suficientes para relatórios semanais ou mensais
>- **Recomendação:** Habilite a transmissão para conexões de produção. O custo de processamento incremental é mínimo em comparação ao valor dos dados oportunos para o monitoramento ativo da campanha e painéis operacionais.

## Documentação relacionada

Os recursos a seguir fornecem informações adicionais para esse padrão de caso de uso.

### [!DNL Customer Journey Analytics] — Introdução

- [Visão geral do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Medidas de proteção do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-admin/guardrails)

### Conexões

- [Visão geral das conexões](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [Criar ou editar uma conexão](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [Gerenciar conexões](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/manage-connections)

### Visualizações de dados

- [Visão geral das visualizações de dados](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)
- [Criar ou editar uma visualização de dados](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Visão geral das configurações de componente](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [Configurações de persistência](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [Configurações de atribuição](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [Configurações de formato](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/format)
- [Desduplicação de métrica](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication)
- [Incluir/excluir valores](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/include-exclude-values)
- [Configurações da sessão](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/session-settings)
- [Campos derivados](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/derived-fields)

### Workspace e análise

- [Visão geral do Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Criar um projeto](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [Tabela de forma livre](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [Visualização de fluxo](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [Visualização Fallout](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [Tabela de coorte](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [Painel de atribuição](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [Detalhamento de dimensões](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)
- [Compartilhar projetos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [Agendar projetos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [Visão geral da exportação](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/export/export-cloud)

### Análise guiada

- [Visão geral da análise guiada](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/overview)
- [Visualização do funnel](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [Exibição de tendências](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/trends/usage)
- [Exibição da frequência de engajamento](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/trends/frequency)
- [Exibição de retenção](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/retention/retention-rates)
- [Visualização de crescimento ativa](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/user-growth/active)
- [Visualização do impacto da versão](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/impact/release)
- [Visualização de impacto de primeiro uso](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/impact/first-use)
- [Exibição da linha do tempo](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/streams/timeline)

### Componentes

- [Visão geral dos filtros](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [Criar filtros](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [Visão geral das métricas calculadas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [Criar métricas calculadas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [Funções de métrica calculada](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-functions)
- [Visão geral de anotações](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/annotations/overview)
- [Intervalos de datas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)
- [Componente de métricas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/apply-create-metrics)

### Publicação de público

- [Visão geral dos públicos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [Criar e publicar públicos-alvo](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/publish)
- [Gerenciar públicos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/manage)

### Análise de conteúdo

- [Content Analytics](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/content-analytics/content-analytics)
- [Configuração do Content Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/config/configuration)

### Painéis e cartões de pontuação

- [Criar um cartão de pontuação para dispositivos móveis](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [Configurar e preparar cartões de pontuação](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Painéis do Adobe Analytics — guia executivo](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/set-up-execs)
- [Visualização do número do resumo](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/summary-number-change)

### AEP foundation

- [Visão geral dos conjuntos de dados](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/overview)
- [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Visão geral das fontes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Visão geral do portal de público](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-portal)

### Integração de relatórios do AJO

- [Guia de integração do AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Relatório de email da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/reporting/campaign-global-report-cja-email)
- [Jornada relatório de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/reporting/journey-global-report-cja-email)

### Tutoriais e guias

- [Noções básicas de composição de esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [Visão geral do Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Configurar sequências de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
