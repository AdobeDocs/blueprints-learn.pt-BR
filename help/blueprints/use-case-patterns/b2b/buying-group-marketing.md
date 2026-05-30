---
title: Compra de marketing baseado em grupo e gerenciamento de Jornadas
description: Saiba como desenvolver jornadas a nível de conta que qualifiquem leads em grupos de compra para melhorar a eficácia do marketing B2B.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 2bf57f67-80c8-4368-98d2-05706427772d
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 1%

---

# Compra de marketing baseado em grupo e gerenciamento de jornadas

Este guia descreve o padrão de caso de uso de gerenciamento de jornadas e marketing com base em grupos de compras, que usa o [!DNL Adobe Journey Optimizer B2B Edition] e o [!DNL Real-Time CDP B2B Edition] para implementar a orquestração de jornadas no nível de conta com o gerenciamento de grupos de compras. Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam entender o que esse padrão faz, os objetivos de negócios que ele aceita, os casos de uso táticos que ele permite e os aplicativos Adobe envolvidos.

Diferentemente dos padrões de jornada no nível da pessoa, esse padrão opera no nível da conta, qualificando leads individuais em grupos de compras associados aos interesses da solução, pontuando o engajamento no nível do grupo de compras e orquestrando jornadas de conta em várias etapas que fazem com que as contas avancem pelos estágios do pipeline em direção à preparação das vendas.

## Padrão do caso de uso

**Comprando marketing baseado em grupo e gerenciamento de jornadas**

Desenvolva jornadas a nível de conta que qualifiquem leads em grupos de compra para melhorar a eficácia do marketing B2B.

**Plano de execução:** Identificação da conta > Definição do grupo de compra > Qualificação de cliente potencial > Execução da Jornada da conta > Pontuação de engajamento > Relatórios

## Visão geral do caso de uso

As organizações B2B enfrentam um desafio fundamental: as decisões de compra raramente são tomadas por um único indivíduo. Compras complexas de B2B envolvem várias partes interessadas — tomadores de decisão, influenciadores, campeões, titulares de orçamento e avaliadores técnicos — que formam coletivamente um &quot;grupo de compras&quot;. O marketing tradicional baseado em lead trata cada pessoa de forma independente, sem o sinal crítico de que a combinação certa de funções em uma conta está envolvida e pronta para comprar.

A compra de marketing baseado em grupo e gerenciamento de jornadas resolve isso mudando a unidade de orquestração de leads individuais para contas e grupos de compras. O padrão permite que os profissionais de marketing B2B definam os interesses da solução (os produtos ou serviços que estão sendo vendidos), criem modelos de grupos de compra que especifiquem quais funções são necessárias para uma decisão de compra, qualifiquem leads recebidos em relação a essas funções, marquem o engajamento no nível do grupo de compra e orquestrem jornadas de conta que respondam aos sinais de integridade e prontidão do grupo de compra.

O resultado desejado é melhorar a qualidade e a velocidade do pipeline: o marketing fornece contas para as vendas somente quando as pessoas certas dentro da conta estão envolvidas e o grupo de compras está suficientemente completo, reduzindo o esforço de vendas desperdiçado e acelerando a progressão do negócio.

## Principais objetivos de negócios

Esse padrão de caso de uso oferece suporte aos seguintes objetivos de negócios.

### Melhorar a qualificação e a conversão de clientes potenciais

Aumente a qualidade do lead e acelere a progressão do pipeline por meio de pontuação, estimulação e acompanhamento personalizado.

**KPIs:** Conversão de Cliente Potencial, Conversão de Cliente Potencial/Cliente Potencial, Eficiência

[Saiba mais sobre como melhorar a qualificação e a conversão de clientes potenciais](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

### Aumentar a geração de leads

Gerar clientes potenciais mais qualificados para o pipeline de vendas por meio de formulários, eventos, conteúdo e envolvimento de vários canais.

**KPIs:** Clientes Potenciais, Custo por Cliente Potencial, Conversão de Cliente Potencial

[Saiba mais sobre o aumento da geração de clientes potenciais](/help/blueprints/business-objectives/acquisition-growth/increase-lead-generation.md)

### Aumentar receita e vendas

Impulsionar o crescimento da receita de ponta por meio de canais digitais, campanhas e jornadas otimizadas do cliente.

**KPIs:** Crescimento de receita, velocidade do pipeline, taxa de fechamento de negócios

[Saiba mais sobre aumento de receita e vendas](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)

## Exemplo de casos de uso tático

Veja a seguir cenários específicos em que esse padrão pode ser aplicado.

- **Qualificação de grupo de compras específica da solução** — Defina grupos de compras para cada linha de produtos (por exemplo, &quot;CRM Empresarial&quot;, &quot;Plataforma de Dados&quot;, &quot;Conjunto de Segurança&quot;) com modelos de função especificando os perfis necessários (Comprador Econômico, Avaliador Técnico, Especialista, Usuário Final) e qualificando clientes potenciais do CRM e do sistema de automação de marketing em relação a essas funções.
- **jornada de conta para aceleração de pipeline** — Orquestre uma jornada de conta em várias etapas que envia emails de criação direcionados para funções não envolvidas em um grupo de compras, aciona alertas de vendas quando os limites de envolvimento são atingidos e faz a transição da conta para um estágio pronto para vendas.
- **Campanhas de integridade do grupo de compra** — Identifique contas em que os grupos de compra têm funções ausentes (por exemplo, nenhum Comprador econômico identificado) e inicie campanhas de aquisição direcionadas para envolver as personalidades certas nessas contas.
- **jornadas de conta de venda cruzada** — Depois que um negócio inicial for fechado, crie novos grupos de compras para interesses de soluções complementares e organize jornadas de conta que estimulem o comitê de compras expandido.
- **Reengajamento para negociações paralisadas** — Detecte contas em que as pontuações de engajamento do grupo de compras foram recusadas e acione jornadas de reengajamento com conteúdo novo, alcance executivo ou convites de evento.
- **Alinhamento de vendas e marketing por meio de insights do CRM** — Status do grupo de compras de superfície, dados de compromisso e progresso da jornada de conta diretamente em [!DNL Salesforce] ou [!DNL Dynamics 365] para que os representantes de vendas tenham visibilidade em tempo real das contas qualificadas para marketing.
- **Atualizações de grupos de compras orientadas por eventos** — Atualize automaticamente as pontuações de participação e associação de grupos de compras quando os clientes potenciais participarem de webinários, baixarem whitepapers, visitarem páginas de preços ou solicitarem demonstrações.
- **Coordenação de contas entre várias regiões** — gerencie grupos de compras em contas globais onde diferentes contatos regionais têm diferentes funções, unificando a pontuação de engajamento entre regiões geográficas.

## Indicadores-chave de desempenho

Os KPIs a seguir ajudam a medir a eficácia desse padrão de caso de uso.

| KPI | Descrição | Abordagem de medição |
| --- | --- | --- |
| Taxa de integralidade do grupo de compras | Porcentagem de grupos de compras com todas as funções necessárias preenchidas | [!DNL AJO B2B] Painéis do Analytics: rastrear a cobertura de função por grupo de compra |
| Pontuação de engajamento do grupo de compra | Pontuação de engajamento agregada em todos os membros de um grupo de compras | Pontuação de engajamento de [!DNL AJO B2B]: pontuações em nível de pessoa acumuladas no grupo de compras |
| Taxa de contas qualificadas de marketing (MQA) | Porcentagem de contas que atingem o limite qualificado de marketing | Critérios de saída da jornada de conta: contas em transição para o estágio pronto para vendas |
| Velocidade do pipeline | Tempo médio desde a criação do grupo de compras até a oportunidade qualificada para vendas | Integração do CRM: rastreie as transições de estágio de [!DNL AJO B2B] para o pipeline de CRM |
| Taxa de Qualificações do Grupo de Cliente Potencial para Compra | Porcentagem de clientes potenciais qualificados com êxito em funções de grupo de compra | [!DNL AJO B2B] Gerenciamento do Grupo de Compras: taxa de clientes potenciais qualificados vs. não qualificados |
| Taxa de Resposta de Alerta de Vendas | Porcentagem de alertas de vendas que resultam na atividade de acompanhamento de vendas | Insights de vendas do CRM: rastreie a conversão de alerta em atividade |
| Taxa de conclusão da Jornada na conta | Porcentagem de contas que concluem o caminho de jornada pretendido | [!DNL AJO B2B] Painéis do Analytics: métricas de conclusão da jornada |
| Taxa de engajamento de email (B2B) | Taxas de abertura e click-through para emails de criação B2B | [!DNL AJO B2B] relatórios: métricas de envolvimento e entrega de email |

## Aplicativos

Os seguintes aplicativos da Adobe são usados neste padrão de caso de uso.

- **[!DNL Journey Optimizer B2B Edition] ([!DNL AJO B2B])** — Orquestra jornadas no nível da conta, gerencia grupos de compras com modelos de função e interesses de solução, classifica o envolvimento no nível da pessoa e do grupo de compras, cria conteúdo de email B2B, envia mensagens SMS, configura alertas de vendas e fornece painéis de análise B2B.
- **[!DNL Real-Time CDP B2B Edition] ([!DNL RT-CDP B2B])** — Unifica perfis de conta de dados B2B entre origens, resolve relações de pessoa para conta, avalia públicos em nível de conta, configura destinos específicos B2B ([!DNL Marketo Engage], [!DNL LinkedIn], CRM) e impõe a governança de dados em dados B2B.

## Documentação relacionada

Os recursos a seguir fornecem detalhes adicionais sobre os aplicativos e recursos referenciados neste guia.

### [!DNL AJO B2B Edition]

- [Página inicial da documentação do AJO B2B edition](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/guide-overview)
- [Visão geral dos grupos de compras](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-overview)
- [Interesses da solução](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/buying-groups/solution-interests)
- [Modelos de função](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-role-templates)
- [Criar grupos de compra](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-create)
- [Estágios do grupo de compra](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [Visão geral das jornadas da conta](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/account-journeys/journey-overview)
- [Nós de jornada de conta](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/account-journeys/journey-nodes)
- [Emails de alerta de vendas](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sales-alert-email)
- [Insights de vendas do CRM](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/crm-sales-insights)

### E-mail e conteúdo B2B

- [Criação de email B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/email-authoring)
- [Criação de SMS no AJO B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sms-authoring)
- [Assistente de IA para criação de email](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/ai-assistant-emails)

### Análises e painéis B2B

- [Painel de grupos de compra](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/dashboards/buying-groups-dashboard)
- [Painel de engajamento](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/dashboards/engagement-dashboard)
- [Painel inteligente](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/dashboards/intelligent-dashboard)
- [Visão geral do CJA B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

### [!DNL RT-CDP B2B Edition]

- [Visão geral da B2B edition da RT-CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview)
- [Esquemas B2B no Real-Time CDP](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/schemas/b2b)
- [Públicos da conta](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/types/account-audiences)
- [Conector de origem do Marketo Engage](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)

### Base de dados

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/home)
- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/home)
- [Visão geral das origens](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/home)
- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/home)

### Configuração de canais

- [Introdução à configuração de email](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Configurar canal de SMS](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)

### Governança e privacidade de dados

- [Visão geral da governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/home)
- [Gerenciamento avançado do ciclo de vida dos dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-lifecycle/home)

### Destinos

- [Visão geral dos destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/catalog/overview)
- [Destino de públicos correspondentes do LinkedIn](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/catalog/social/linkedin)

### Medidas de proteção

- [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/guardrails)
- [Proteções de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails)
- [Medidas de proteção de assimilação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/ingestion/guardrails)
- [Medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/get-started/guardrails)

### Tutoriais e introdução

- [Introdução ao AJO B2B edition](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/guide-overview)
- [Tutorial do RT-CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-tutorial)
