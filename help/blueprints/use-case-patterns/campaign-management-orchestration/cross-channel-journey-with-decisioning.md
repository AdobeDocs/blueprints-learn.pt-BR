---
title: Jornada entre canais com decisão
description: Saiba como orquestrar uma jornada de várias etapas, incorporando a decisão em tempo real para selecionar o canal, conteúdo ou oferta ideal.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: eabdd91f-bb7d-4de3-adb5-5940d3ca4a78
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1983'
ht-degree: 5%

---

# Jornada entre canais com decisão

Este guia descreve a jornada entre canais com o padrão de caso de uso de decisão, que usa o [!DNL Adobe Journey Optimizer] e o [!DNL Adobe Real-Time Customer Data Platform] para orquestrar jornadas multicanais e de várias etapas que incorporam a tomada de decisão em tempo real em um ou mais nós de jornada. Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam entender o que esse padrão faz, os objetivos de negócios que ele aceita, os casos de uso táticos que ele permite e os aplicativos Adobe envolvidos.

A jornada entre canais com decisão é o padrão de orquestração de campanha mais sofisticado no ecossistema [!DNL Adobe Experience Platform]. Ele estende jornadas orquestradas de várias etapas incorporando decisões em tempo real — usando a Decisão [!DNL AJO] para avaliar o contexto atual de um perfil e selecionar dinamicamente o canal, conteúdo ou oferta ideal em um ou mais pontos de decisão na tela de jornada.

## Padrão do caso de uso

**jornada entre canais com decisão**

Orquestrar uma jornada multicanal de várias etapas que incorpora a decisão em tempo real em um ou mais nós para selecionar o canal, o conteúdo ou a oferta ideal.

**Plano de execução:** Avaliação de público-alvo > Execução de Jornada > Nó de decisão > Seleção de canal > Entrega de mensagem > Relatórios

## Visão geral do caso de uso

As organizações precisam cada vez mais fornecer jornadas personalizadas e adaptáveis ao cliente que respondam dinamicamente ao contexto em tempo real de cada indivíduo, em vez de seguirem uma sequência fixa e predeterminada. O canal preferido de um cliente, o histórico de engajamento, o nível de fidelidade, o valor vitalício previsto e os interesses atuais do produto contribuem para qual deve ser a próxima melhor ação em cada ponto de contato.

A jornada entre canais com decisões atende a essa necessidade combinando dois poderosos recursos do [!DNL AJO]: orquestração de jornadas (que gerencia o fluxo de várias etapas, tempo, condições e entrega de canal) e decisão (que avalia regras de elegibilidade, aplica estratégias de classificação e seleciona a oferta ou variante de conteúdo ideal em cada ponto de decisão).

Este padrão é apropriado quando:

- A jornada deve se adaptar dinamicamente ao estado em tempo real de cada perfil, em vez de seguir um canal fixo ou uma sequência de conteúdo
- Várias ofertas, variantes de conteúdo ou canais são candidatos em um ou mais nós de jornada, e a melhor opção deve ser selecionada com base no contexto do perfil
- A classificação assistida por IA ou baseada em fórmula é necessária para otimizar a seleção de ofertas na jornada
- A organização deseja consolidar a lógica de seleção de canais e o gerenciamento de ofertas em uma estrutura de decisão centralizada, em vez de manter uma lógica de ramificação complexa

O público-alvo inclui profissionais de marketing que gerenciam programas de ciclo de vida, jornadas de fidelidade, sequências de retorno e fluxos de integração, em que a personalização em escala requer tomada de decisão automatizada em cada ponto de contato.

>[!NOTE]
>Se sua jornada não exigir uma decisão dinâmica em nós individuais, por exemplo, um programa de integração ou criação de sequência fixa, consulte a [jornada orquestrada em várias etapas](multi-step-orchestrated-journey.md). Esse padrão é mais simples de configurar e não requer o AJO Decisioning.

## Principais objetivos de negócios

Os seguintes objetivos de negócios são compatíveis com esse padrão de caso de uso.

**[Fornecer experiências personalizadas ao cliente](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**
Personalize conteúdo, ofertas e mensagens para preferências individuais, comportamentos e estágios do ciclo de vida.
**KPIs:** Compromisso, Taxas de Conversão, Satisfação do Cliente (CSAT)

**[Aumente a fidelidade do cliente e o valor vitalício](../../business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)**
Aprofunde as relações com o cliente e maximize o valor a longo prazo por meio de programas de fidelidade, recompensas e envolvimento personalizado.
**KPIs:** Valor vitalício, Retenção, Venda adicional/venda cruzada do cliente %

**[Melhore a retenção do cliente](../../business-objectives/customer-experience/improve-customer-retention.md)**
Mantenha os clientes existentes envolvidos e renovando-os por meio de experiências orientadas por valores e estimulação contínua do relacionamento.
**KPIs:** Retenção, Valor vitalício do cliente, Participação

**[Impulsionar vendas cruzadas e vendas adicionais](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)**
Promova produtos ou serviços complementares e premium para os clientes existentes com base no histórico de comportamento e de compras.
**KPIs:** % de venda adicional/venda cruzada, Receita incremental, Valor vitalício do cliente

## Exemplo de casos de uso tático

Os cenários a seguir ilustram como a jornada entre canais com decisão pode ser aplicada na prática.

- **jornada de retorno adaptável** — uma jornada de várias etapas em que a tomada de decisão seleciona o canal (email, push ou SMS) com base no histórico de engajamento de cada perfil e seleciona dinamicamente a melhor oferta de incentivo com base no valor previsto de tempo de vida
- **jornada de ciclo de vida da próxima melhor ação** — a decisão determina o que comunicar em cada estágio do ciclo de vida do cliente, selecionando entre conteúdo de integração, ofertas de venda cruzada, recompensas de fidelidade ou incentivos de retenção
- **Integração personalizada com seleção de conteúdo dinâmico** — Nova jornada de integração de cliente em que cada ponto de contato usa a decisão para selecionar o conteúdo, as dicas ou as ofertas de ativação mais relevantes do treinamento do produto
- **jornada entre canais do programa de fidelidade com recompensas personalizadas** — os membros de fidelidade avançam por uma jornada em que o decisioning seleciona ofertas de recompensa personalizadas com base na camada, no histórico de compras e na afinidade de categorias
- **Reengajamento dinâmico com otimização de canal e incentivo** — Reengajamento inativo do cliente em que o canal de alcance geral e o incentivo são selecionados dinamicamente para maximizar a probabilidade de resposta
- **Proteção do ciclo de vida do cliente com recomendações de conteúdo classificadas por IA** — jornada de proteção contínua em que a decisão classificada por IA seleciona o conteúdo ou as recomendações de produto mais relevantes em cada ponto de contato

## Indicadores-chave de desempenho

Use os KPIs a seguir para medir a eficácia desse padrão de caso de uso.

| KPI | Descrição | Abordagem de medição |
| --- | --- | --- |
| Taxa de conclusão da jornada | Porcentagem de perfis que concluem a jornada completa | Relatório de Jornada: concluído / inserido |
| Taxa de aceitação da oferta | Porcentagem de ofertas selecionadas pela decisão envolvidas com (clicadas, resgatadas) | Relatório de decisão: cliques na oferta / impressões da oferta |
| Taxa de participação do canal | Taxas de abertura e de clique em cada canal usado na jornada | Métricas de entrega por canal no relatório do jornada |
| Índice de conversão | Porcentagem de participantes do jornada que concluíram a ação de conversão de público alvo | Rastreamento de evento de saída do Jornada para análise do CJA funnel |
| Taxa de oferta substituta | Porcentagem de solicitações de decisão que retornam a oferta substituta em vez de uma oferta personalizada | Relatório de decisão: seleções substitutas / total de seleções |
| Impacto no valor vitalício do cliente | Alteração no CLV para participantes da jornada vs. grupo de controle | Análise de coorte do CJA com comparação de controle |
| Receita de venda cruzada/venda adicional | Receita incremental atribuída às ofertas selecionadas pela decisão | Análise de atribuição do CJA em conversões orientadas por oferta |
| Eficácia da classificação de decisão | Diferença de desempenho entre ofertas classificadas por IA e seleção aleatória/baseada em prioridade | Experimento A/B comparando estratégias de classificação |

## Aplicativos

Os aplicativos a seguir são usados para implementar esse padrão de caso de uso.

- **[!DNL Adobe Journey Optimizer]([!DNL AJO])** — orquestração de Jornadas (design de tela de várias etapas, condições de entrada, esperas, condições, critérios de saída), criação de mensagens entre canais, configuração da superfície de canal, gerenciamento de conflitos e prioridades
- **[!DNL Adobe Journey Optimizer]Decisão** — Gerenciamento de oferta e item de conteúdo, regras de elegibilidade, estratégias de classificação (prioridade, fórmula, IA), políticas de decisão, posicionamentos, ofertas de fallback
- **[!DNL Adobe Real-Time Customer Data Platform]([!DNL RT-CDP])** — Avaliação de público para entrada de jornada e segmentos de qualificação de oferta, enriquecimento de perfil com atributos computados e pontuações de propensão, consentimento e imposição de governança
- **[!DNL Adobe Experience Platform]([!DNL AEP])** — armazenamento de Perfil do Cliente em Tempo Real, Serviço de Identidade para resolução entre canais, modelagem de dados e infraestrutura de assimilação

## Documentação relacionada

Os recursos a seguir fornecem detalhes adicionais sobre os recursos usados neste padrão de caso de uso.

### Jornada orquestração

- [Introdução às jornadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Criar uma jornada](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Propriedades da jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Ler atividade de público](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Eventos gerais](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Eventos de qualificação de público-alvo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [Atividade de condição](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Atividade aguardar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Adicionar uma mensagem em uma jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Critérios de saída](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [Gerenciamento de entradas de jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Testar a jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [Publicar a jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

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

### Configuração de canais

- [Introdução à configuração de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegar subdomínios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Criar pools de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [Planos de aquecimento de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Configurações de superfície de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Configurar canal de SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configurar canal de notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Criação e personalização de mensagens

- [Criar um email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [Criar conteúdo de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxe do Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabalhar com modelos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabalhar com fragmentos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Visualizar e testar o conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### Gerenciamento de conflitos, prioridades e frequências

- [Visão geral do gerenciamento de conflitos e prioridades](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Pontuações de prioridade](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Identificar possíveis conflitos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [Limite de jornada e arbitragem](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)
- [Regras de frequência](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)

### Públicos-alvo e segmentação

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentação de transmissão](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentação de borda](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Composição de público](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Referência do Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### Relatórios e análises

- [Relatório em tempo real da jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Jornada relatório global](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabalhar com o Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Guia de integração do AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Visão geral do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Visão geral do Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

### Perfil e identidade

- [Visão geral do Perfil do cliente em tempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [Visão geral de atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Visão geral do Customer AI](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### Governança e consentimento de dados

- [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Consentimento no Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [Gerenciar lista de supressão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Medidas de proteção

- [Medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Medidas de proteção do serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)
