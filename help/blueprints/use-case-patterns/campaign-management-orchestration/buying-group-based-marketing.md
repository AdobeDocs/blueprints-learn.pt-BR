---
title: Compra de marketing baseado em grupo e gerenciamento de Jornadas
description: Saiba como desenvolver jornadas a nível de conta que qualifiquem leads em grupos de compra para melhorar a eficácia do marketing B2B.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 2bf57f67-80c8-4368-98d2-05706427772d
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '7932'
ht-degree: 0%

---

# Compra de marketing baseado em grupo e gerenciamento de jornadas

Este guia fornece uma referência de implementação abrangente para gerenciamento de marketing e jornadas com base em grupos de compras. Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam implementar a orquestração de jornadas no nível da conta com o gerenciamento de grupos de compras usando o [!DNL Adobe Journey Optimizer B2B Edition] e o [!DNL Real-Time CDP B2B Edition].

Use este documento para entender o que configurar, onde existem opções de implementação e quais trade-offs impulsionam cada decisão.

Diferentemente dos padrões de jornada no nível da pessoa, esse padrão opera no nível da conta, qualificando leads individuais em grupos de compras associados aos interesses da solução, pontuando o engajamento no nível do grupo de compras e orquestrando jornadas de conta em várias etapas que fazem com que as contas avancem pelos estágios do pipeline em direção à preparação das vendas.

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

## Padrão do caso de uso

**Comprando marketing baseado em grupo e gerenciamento de jornadas**

Desenvolva jornadas a nível de conta que qualifiquem leads em grupos de compra para melhorar a eficácia do marketing B2B.

**Cadeia de funções:** Identificação de Conta > Definição de Grupo de Compras > Qualificação de Cliente Potencial > Execução de Jornada de Conta > Pontuação de Compromisso > Relatórios

## Aplicativos

Os seguintes aplicativos da Adobe são usados neste padrão de caso de uso.

- **[!DNL Journey Optimizer B2B Edition]([!DNL AJO B2B])** — Orquestra jornadas no nível da conta, gerencia grupos de compras com modelos de função e interesses de solução, classifica o envolvimento no nível da pessoa e do grupo de compras, cria conteúdo de email B2B, envia mensagens SMS, configura alertas de vendas e fornece painéis de análise B2B.
- **[!DNL Real-Time CDP B2B Edition]([!DNL RT-CDP B2B])** — Unifica perfis de conta de dados B2B entre origens, resolve relações de pessoa para conta, avalia públicos em nível de conta, configura destinos específicos B2B ([!DNL Marketo Engage], [!DNL LinkedIn], CRM) e impõe a governança de dados em dados B2B.

## Funções básicas

Os seguintes recursos básicos devem estar em vigor para esse padrão de caso de uso. Para cada função, o status indica se ele é tipicamente necessário, se presume ser pré-configurado ou se não é aplicável.

| Função de base | Status | O que deve estar em vigor | Referência do Experience League |
| --- | --- | --- | --- |
| Administração e governança | Obrigatório | Sandbox provisionada com [!DNL AJO B2B Edition] e [!DNL RT-CDP B2B Edition] direitos habilitados. Funções configuradas para profissionais de marketing B2B, operações de vendas e administradores com permissões apropriadas para gerenciamento de grupos de compras, jornadas de conta e configurações de integração de CRM. | [Visão geral das sandboxes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/home), [Visão geral do controle de acesso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Preparação e modelagem de dados | Obrigatório | Esquemas XDM B2B configurados usando classes específicas B2B: conta de negócios XDM, oportunidade de negócios XDM, pessoa de negócios XDM (lead/contato), campanha de negócios XDM e lista de marketing de negócios XDM. Os grupos de campos para atributos de conta, atributos de pessoa e dados de atividade/envolvimento devem estar em vigor. Conjuntos de dados criados e habilitados para perfil para cada esquema. | [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [classes de esquema B2B](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| Fontes de dados e coleção | Obrigatório | Pipelines de assimilação de dados B2B estabelecidos, normalmente por meio do conector de origem [!DNL Marketo Engage] ou dos conectores de origem de CRM [!DNL Salesforce]/[!DNL Dynamics]. Dados de conta, pessoa, oportunidade, campanha e membro da campanha devem fluir para os conjuntos de dados da AEP. Os dados de engajamento comportamental (visitas da Web, interações por email, downloads de conteúdo) também devem ser assimilados para pontuação de engajamento. | [Visão geral das fontes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home), [Conector do Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) |
| Configuração de identidade e perfil | Obrigatório | Resolução de identidade B2B configurada para resolver relacionamentos entre pessoas e contas. Os namespaces de identidade para identificadores B2B ([!DNL Marketo] ID de Pessoa, [!DNL Salesforce] ID de Cliente Potencial/Contato, ID de Conta) devem existir. Políticas de mesclagem configuradas para unificação de perfil B2B. Os perfis de conta devem ser unificados a partir dos dados entre fontes. | [Visão geral do Serviço de Identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [Resolução de Identidade B2B](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview) |
| Definição e segmentação do público-alvo | Obrigatório | Definições de público-alvo no nível da conta criadas usando atributos de conta, atributos de pessoa e dados de atividade. Os públicos-alvo da conta identificam quais contas entram nas jornadas do grupo de compra. Normalmente, a avaliação em lote é suficiente para jornadas de conta B2B, embora a avaliação por transmissão possa ser usada para acionadores de qualificação de conta em tempo real. | [Visão geral do Serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [Públicos-alvo da conta](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences) |

## Funções de suporte

Os recursos a seguir aumentam esse padrão de caso de uso, mas não são necessários para a execução principal.

| Função de suporte | Status | Por que é importante | Referência do Experience League |
| --- | --- | --- | --- |
| Criação de atributo calculado/derivado | Recomendado | Os atributos computados podem agregar eventos de engajamento no nível da pessoa (aberturas de email, downloads de conteúdo, participação em webinários) em métricas de engajamento no nível da conta que alimentam a pontuação do grupo de compra e a lógica de qualificação da conta. | [Visão geral dos atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Gerenciamento do ciclo de vida dos dados | Recomendado | O gerenciamento de consentimento é essencial para comunicações por email e SMS B2B. As políticas de expiração do conjunto de dados ajudam a gerenciar o ciclo de vida dos dados de envolvimento temporário e garantem a conformidade com os requisitos de retenção de dados. | [Gerenciamento Avançado do Ciclo de Vida dos Dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| Rotulagem e aplicação de uso de dados | Recomendado | Os dados B2B geralmente contêm informações confidenciais da empresa e dados pessoais de contatos comerciais. As políticas de governança de dados garantem o uso compatível dos dados B2B entre destinos, especialmente ao ativar plataformas de publicidade ou sistemas de terceiros. | [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| Monitoramento e capacidade de observação | Recomendado | O monitoramento garante que os pipelines de dados B2B (sincronizações de CRM/[!DNL Marketo]) estejam íntegros, que os perfis de conta estejam sendo atualizados e que as execuções de jornada de conta prossigam sem falhas. Alertas sobre falhas no fluxo de dados de origem são essenciais para manter a moeda dos dados. | [Visão geral dos Insights de Capacidade de Observação](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| Relatórios e análise | Incluído | Os painéis de análise B2B no [!DNL AJO B2B Edition] fornecem envolvimento de grupo de compra, desempenho de jornada de conta e métricas de pipeline. [!DNL CJA B2B Edition] estende a análise com análise de espaço de trabalho no nível da conta, análise de grupo de compra e correlação de oportunidades. | [visão geral do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## Funções do aplicativo

Este plano utiliza as seguintes funções do catálogo de funções do aplicativo. As funções são mapeadas para fases de implementação em vez de etapas numeradas.

### [!DNL Journey Optimizer B2B Edition] ([!DNL AJO B2B])

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Configuração de interesse da solução | Fase 1: Interesse na solução e configuração do grupo de compra | Definir os interesses da solução que mapeiam produtos ou serviços aos critérios de qualificação do grupo de compras |
| Gerenciamento de Grupo de Compras | Fase 1: Interesse na solução e configuração do grupo de compra | Criar e gerenciar grupos de compras com modelos de função, mapeamento de persona e definições de interesse de solução |
| Journey Orchestration da conta | Fase 3: Design e execução da Jornada de conta | Projete e gerencie jornadas de conta em várias etapas com condições, ações e ramificação baseada em envolvimento |
| Pontuação de engajamento | Fase 2: Pontuação de qualificação e engajamento do lead | Pontuação do engajamento em nível de pessoa nos grupos de compra para medir a integridade e a prontidão dos grupos de compra |
| Qualificação da conta | Fase 2: Pontuação de qualificação e engajamento do lead | Use agentes de qualificação de conta alimentados por IA para avaliar a disponibilidade da conta e a qualidade do pipeline |
| Criação de email B2B | Fase 3: Design e execução da Jornada de conta | Crie conteúdo de email B2B com modelos, fragmentos visuais, temas de marca e geração de conteúdo assistido por IA |
| Gerenciamento de canal de SMS | Fase 3: Design e execução da Jornada de conta | Configurar e gerenciar comunicações SMS em jornadas de conta B2B |
| Configuração de alerta de vendas | Fase 4: alinhamento de vendas e integração de CRM | Configurar emails de alerta de vendas para notificar as equipes de vendas sobre marcos de engajamento na conta e sinais de compra |
| Insights de vendas do CRM | Fase 4: alinhamento de vendas e integração de CRM | Forneça visibilidade no CRM ([!DNL Salesforce], [!DNL Dynamics]) para o status do grupo de compras, dados de participação e progresso da jornada da conta |
| Painéis do Analytics B2B | Fase 5: Relatórios e otimização | Monitore o desempenho da jornada de conta, o envolvimento do grupo de compra e as métricas de pipeline por meio de painéis inteligentes e de engajamento |

### [!DNL Real-Time CDP B2B Edition] ([!DNL RT-CDP B2B])

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Unificação de perfil da conta | Fase 0: Fundação de dados B2B | Consolidar dados B2B entre origens em perfis de conta unificados usando classes de esquema B2B XDM especializadas e grupos de campo |
| Resolução de identidade B2B | Fase 0: Fundação de dados B2B | Resolver relacionamentos pessoa-para-conta usando identificadores principais, suportando hierarquias de conta de vários níveis e mapeamentos pessoa-para-conta muitos |
| Avaliação de público-alvo da conta | Fase 0: Fundação de dados B2B | Avaliar a associação de segmento em nível de conta combinando atributos de conta, atributos de pessoa e dados de atividade |
| Configuração de destino da conta | Fase 4: alinhamento de vendas e integração de CRM | Configurar conexões para destinos específicos B2B ([!DNL Marketo Engage], [!DNL LinkedIn], sistemas CRM) com mapeamento de campo no nível da conta |
| Audience Activation da conta | Fase 4: alinhamento de vendas e integração de CRM | Publicar públicos-alvo baseados em conta nos destinos para direcionamento e supressão baseados em conta |
| Integração do [!DNL Marketo Engage] | Fase 0: Fundação de dados B2B | Assimilar e ativar dados bidirecionalmente com [!DNL Marketo Engage] usando conectores de origem e destino B2B nativos |
| Governança de dados B2B | Fase 0: Fundação de dados B2B | Aplicar políticas e consentimento de uso de dados nos processos de centralização e ativação de dados da conta B2B |

## Pré-requisitos

Conclua o seguinte antes de iniciar a implementação.

- [ ] [!DNL AJO B2B Edition] licença provisionada e habilitada na sandbox de destino
- [ ] [!DNL RT-CDP B2B Edition] licença provisionada e habilitada na sandbox de destino
- [ ] sistema do CRM ([!DNL Salesforce] ou [!DNL Microsoft Dynamics 365]) acessível com credenciais de API apropriadas para sincronização de dados bidirecional
- [ ] [!DNL Marketo Engage] instância conectada (se estiver usando [!DNL Marketo] como plataforma de automação de marketing) com o conector de origem configurado
- [ ] esquemas XDM B2B implantados: classes de Membro de Conta, Pessoa, Oportunidade, Campanha e Campanha com grupos de campos obrigatórios
- [ ] Dados de conta e de pessoa assimilados na AEP com relacionamentos de pessoa para conta resolvidos
- [ ] Canal de email configurado: subdomínio delegado, pool de IP aquecido e superfície de canal criada para envio de email B2B
- [ Provedor de SMS ] configurado (se o canal SMS for usado nas jornadas da conta): credenciais [!DNL Sinch], [!DNL Twilio] ou [!DNL Infobip] provisionadas
- [ ] Equipe de vendas integrada ao componente do CRM Sales Insights ([!DNL Salesforce] pacote do AppExchange ou [!DNL Dynamics] solução instalada)
- [ ] ativos de conteúdo preparados: modelos de email B2B, temas de marca e fragmentos visuais para emails de alertas de promoção e vendas
- [ ] Taxonomia de interesse da solução definida: lista de produtos/serviços que terão grupos de compras associados
- [ ] Modelos de função do grupo de compras criados: personas e funções necessárias para cada interesse de solução (por exemplo, Comprador econômico, Avaliador técnico, Especialista)

## Opções de implementação

Esta seção descreve as abordagens de implementação disponíveis, cada uma adaptada às diferentes necessidades organizacionais e níveis de maturidade.

### Opção A: interesse em solução única com jornada de conta linear

**Recomendado para:** Organizações novatas no gerenciamento de grupos de compras que desejam começar com uma única oferta de linha de produtos ou solução, validar a abordagem e iterar antes de dimensionar para vários interesses de solução.

**Como funciona:**

Essa abordagem foca em um único interesse de solução (um produto ou serviço) com um modelo de grupo de compra. Uma jornada de conta linear foi projetada com estágios sequenciais: identificação de conta, formação de grupo de compra, envolvimento de criação, limite de pontuação de engajamento e entrega de vendas. A jornada segue um caminho simples sem ramificações complexas ou trilhas paralelas.

Os clientes potenciais são qualificados em funções de grupo de compra conforme são assimilados do CRM ou do [!DNL Marketo Engage]. A jornada de conta envia emails de criação para funções pouco engajadas, monitora pontuações de engajamento e aciona um alerta de vendas quando o grupo de compras atinge um limite definido de integridade e engajamento. Essa abordagem fornece uma prova de conceito clara e mensurável antes de introduzir a complexidade.

**Principais considerações:**

- Mais simples de implementar e validar, tornando-o adequado para uma primeira implantação
- Limitado a um movimento de compra de produto/serviço por vez
- A estrutura de jornada linear pode não acomodar ciclos de compra complexos de vários estágios

**Vantagens:**

- Retorno do valor mais rápido com o mínimo de complexidade de configuração
- Métricas de sucesso claras associadas a um único interesse de solução
- Mais fácil de explicar e ganhar adesão organizacional
- Relatório simples e medição de KPI

**Limitações:**

- Não aborda cenários de venda cruzada ou de vários produtos
- Contas interessadas em várias soluções exigem jornadas separadas e descoordenadas
- Pode não aproveitar totalmente os recursos de gerenciamento de grupos de compra

**Experience League:**

- [Visão geral do AJO B2B edition](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)
- [Criar grupos de compra](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-overview)

### Opção B: vários interesses de solução com jornadas de conta de ramificação

**Recomendado para:** Organizações com várias linhas de produtos ou ofertas de serviço que precisam gerenciar grupos de compras distintos por interesse de solução, com jornadas de conta que se ramificam com base em quais interesses de solução estão ativos e em quanto tempo cada grupo de compras está no processo de qualificação.

**Como funciona:**

Vários interesses de solução são definidos, cada um com seu próprio modelo de função de grupo de compras. Uma jornada de conta começa com a identificação da conta e avalia quais interesses de solução se aplicam a cada conta com base em sinais comportamentais, dados firmográficos ou intenção explícita. As ramificações de jornadas para tratar de cada interesse ativo da solução, executando acompanhamentos de desenvolvimento paralelos para diferentes grupos de compras na mesma conta.

A pontuação de engajamento opera independentemente por grupo de compra, permitindo que um grupo de compra alcance a preparação para vendas enquanto outro ainda está sendo desenvolvido. Os alertas de vendas são configurados de acordo com os interesses da solução, portanto, a equipe de vendas ou o especialista apropriado é notificado quando um grupo de compras específico é qualificado. Os insights do CRM trazem todos os grupos de compras ativos para uma conta, dando às vendas uma visão holística.

**Principais considerações:**

- Requer taxonomia de interesse de solução bem definida e modelos de grupo de compras distintos
- A complexidade da jornada aumenta a cada interesse adicional na solução
- A coordenação entre grupos de compra (por exemplo, contatos compartilhados que desempenham funções em vários grupos de compra) deve ser planejada

**Vantagens:**

- Oferece suporte a vendas cruzadas e estratégias de contas de vários produtos
- A pontuação independente por grupo de compra oferece visibilidade granular do pipeline
- As equipes de vendas recebem alertas direcionados por interesse na solução
- Maximiza os recursos de gerenciamento de grupos de compra do [!DNL AJO B2B Edition]

**Limitações:**

- Maior complexidade de implementação e maior tempo de implantação
- São necessários mais ativos de conteúdo (controles de email separados por interesse da solução)
- Os relatórios são mais complexos com vários grupos de compra por conta
- Risco de excesso de contatos de mensagens que estão em vários grupos de compras (requer gerenciamento de frequência)

**Experience League:**

- [Interesses da solução](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/solution-interests)
- [Jornadas da conta](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-overview)

### Opção C: qualificação de conta assistida por IA com progressão automatizada da jornada

**Recomendado para:** organizações B2B maduras com dados históricos significativos que desejam utilizar agentes de qualificação de conta alimentados por IA para automatizar a avaliação de prontidão da conta, reduzir o esforço de qualificação manual e ajustar dinamicamente os caminhos de jornada com base nas pontuações de prontidão geradas por IA.

**Como funciona:**

Essa abordagem se baseia na base de vários interesses de soluções da Opção B, mas adiciona a qualificação de conta alimentada por IA para automatizar a transição entre os estágios de jornada. Em vez de depender exclusivamente de limites de pontuação de engajamento baseados em regras, o agente de qualificação de IA avalia a disponibilidade da conta usando um conjunto mais amplo de sinais — integridade do grupo de compra, velocidade de engajamento, ajuste firmográfico, padrões de conversão históricos e dados de intenção.

As jornadas de conta usam o resultado das qualificações de IA para determinar as próximas etapas: as contas com pontuação alta na prontidão são rapidamente rastreadas para alertas de vendas, as contas no nível intermediário recebem nutrição intensificada e as contas de baixa prontidão são colocadas em rastreamentos de percepção de longo prazo. O agente de IA é continuamente reavaliado à medida que novos dados de envolvimento chegam, permitindo a progressão dinâmica da jornada sem intervenção manual.

**Principais considerações:**

- Requer dados históricos suficientes para treinar modelos de qualificação eficazes
- Os resultados da IA devem ser validados em relação aos resultados reais do pipeline antes da implantação completa
- Combina bem com [!DNL CJA B2B Edition] para analisar a precisão da qualificação e a correlação de pipeline

**Vantagens:**

- Reduz o esforço manual de qualificação e elimina transferências arbitrárias baseadas em limites
- Adapta-se dinamicamente às alterações no comportamento da conta e nos padrões de engajamento
- Maior qualidade de pipeline ao incorporar vários sinais além das pontuações de engajamento simples
- A reavaliação contínua impede que as contas fiquem presas em estágios de jornada incorretos

**Limitações:**

- Requer dados de conversão históricos para treinamento significativo em IA
- As decisões de qualificação de &quot;caixa preta&quot; podem ser mais difíceis para as equipes de vendas entenderem e confiarem inicialmente
- Solução de problemas mais complexa quando as contas são qualificadas inesperadamente ou não são qualificadas
- Depende da qualidade e integridade dos dados em todos os sinais de entrada

**Experience League:**

- [Qualificação da conta](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [Assistente de IA no AJO B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)

### Comparação de opções

| Critérios | Opção A: interesse em uma única solução | Opção B: vários interesses da solução | Opção C: qualificação assistida por IA |
| --- | --- | --- | --- |
| Melhor para | Primeira implantação, única linha de produtos | Organizações de vários produtos | Organizações maduras com dados históricos |
| Complexo | Baixa | Medium-Alto | Alta |
| Tempo de implantação | 2 a 4 semanas | 4 a 8 semanas | 6 a 12 semanas |
| Interesses da solução | 1 | Múltiplo | Múltiplo |
| Estrutura de jornada | Linear | Ramificação, trilhas paralelas | Progressão dinâmica orientada por IA |
| Abordagem de pontuação | Limites baseados em regras | Baseado em regras por grupo de compras | Qualificação + regras alimentadas por IA |
| Requisitos de conteúdo | Mínimo (uma via de alimentação) | Alto (por interesse da solução) | Seleção de conteúdo alto + dinâmico |
| Alinhamento de vendas | Fluxo de trabalho de alerta único | Alertas com interesse por solução | Alertas classificados por IA e priorizados |
| Exige | Base de dados B2B básica | Taxonomia de solução bem definida | Dados de conversão históricos + taxonomia |

### Escolha a opção certa

Comece com estas perguntas para determinar a melhor abordagem de implementação:

1. **Quantos produtos ou serviços distintos têm comitês de compras independentes?** Se a resposta for um (ou se a organização quiser provar o conceito primeiro), comece com a Opção A. Se for múltiplo, vá para a pergunta 2.

2. **Há dados históricos suficientes sobre negócios ganhos/perdas, composição de comitês de compras e padrões de envolvimento?** Em caso afirmativo, e se a organização quiser minimizar a qualificação manual, a opção C oferece a abordagem mais automatizada. Caso contrário, a opção B oferece suporte a interesses de várias soluções com pontuação baseada em regras.

3. **Qual é a capacidade de gerenciamento de alterações da organização?** As opções B e C exigem mais alinhamento organizacional (produção de conteúdo, capacitação de vendas, coordenação multifuncional). Se a capacidade for limitada, comece com a Opção A e expanda.

Um caminho de progressão comum é: comece com a opção A para provar o conceito com um interesse de solução, expanda para a opção B adicionando interesses de solução à medida que a confiança cresce, em seguida, crie uma camada na qualificação de IA da opção C, uma vez que dados históricos suficientes estejam disponíveis para treinar os modelos de maneira eficaz.

## Fases de implementação

As fases a seguir descrevem o processo de implementação passo a passo desse padrão de caso de uso.

### Fase 0: base de dados B2B

**Funções do aplicativo:** [!DNL RT-CDP B2B]: Unificação de Perfil de Conta, Resolução de Identidade B2B, Integração de [!DNL Marketo Engage], Governança de Dados B2B, Avaliação de Público-Alvo de Conta

Esta fase estabelece a infraestrutura de dados B2B em [!DNL RT-CDP B2B Edition]. Você unificará os dados da conta do CRM, a automação de marketing e outras fontes em um único perfil de conta, resolverá os relacionamentos entre pessoas e contas, configurará a governança de dados B2B e criará públicos-alvo no nível da conta que serão alimentados pelo gerenciamento de grupos de compra do [!DNL AJO B2B Edition].

#### Decisão: estratégia da fonte de dados B2B

Quais sistemas funcionam como as principais fontes de dados de conta, pessoa e envolvimento?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| [!DNL Marketo Engage] como fonte primária | [!DNL Marketo] é a plataforma de automação de marketing da organização com um histórico de engajamento avançado | O conector bidirecional nativo simplifica a configuração; os dados de envolvimento fluem automaticamente; as relações entre pessoa e conta herdadas de [!DNL Marketo] |
| CRM ([!DNL Salesforce]/[!DNL Dynamics]) como origem primária | O CRM é o sistema de registro de contas e contatos; [!DNL Marketo] não é usado | Requer configuração do conector de origem do CRM; os dados do compromisso podem precisar de fontes complementares; relacionamentos de pessoa para conta de associações de conta-contato do CRM |
| Híbrido: CRM para contas + [!DNL Marketo] para envolvimento | O CRM possui dados mestres de conta/contato enquanto [!DNL Marketo] captura o envolvimento comportamental | Padrão mais comum para organizações que usam ambos; requer uma resolução de identidade cuidadosa para vincular [!DNL Marketo] pessoas aos contatos do CRM |

#### Decisão: estratégia de público-alvo da conta

Como os públicos-alvo da conta devem ser definidos para a entrada de jornada?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Públicos-alvo de contas firmadas | Contas de destino com base no setor, tamanho da empresa, nível de receita ou região | Bom para listas de metas ABM; não requer dados de engajamento; pode ser amplo |
| Públicos-alvo de conta baseados em participação | Contas do Target nas quais as pessoas mostraram sinais de intenção comportamental | Requer fluxo de dados de envolvimento; direcionamento mais preciso; pode perder contas com interesse latente |
| Firmográfico combinado + engajamento | Contas do Target que correspondem ao perfil ideal do cliente E mostram engajamento | Mais preciso; requer ambos os tipos de dados; recomendado para geração de pipeline qualificado |

Navegação da **IU:** Plataforma > Fontes > Catálogo > Selecionar origem ([!DNL Marketo Engage], [!DNL Salesforce], etc.) > Configurar fluxo de dados

**Detalhes de configuração da chave:**

- Configurar esquemas XDM B2B para cada entidade B2B (Conta, Pessoa, Oportunidade, Campanha, Membro da campanha) com grupos de campos obrigatórios
- Configure conectores de origem para CRM e/ou [!DNL Marketo Engage] com agendamento apropriado (normalmente intervalos de 1 a 4 horas para dados B2B)
- Configurar namespaces de identidade para identificadores B2B ([!DNL Marketo] ID de Pessoa, ID de Cliente Potencial da SFDC, ID de Contato da SFDC, ID de Conta)
- Ativar a resolução de identidade B2B para vincular pessoas a contas
- Criar públicos-alvo no nível da conta usando o recurso Públicos-alvo da Conta em [!DNL RT-CDP]

**Documentação do Experience League:**

- [Visão geral da B2B edition da RT-CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview)
- [Esquemas B2B no Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Conector de origem do Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Públicos da conta](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences)
- [Resolução de identidade B2B](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview)

### Fase 1: Interesse na solução e configuração do grupo de compras

**Funções do aplicativo:** [!DNL AJO B2B]: Configuração de Interesse da Solução, Gerenciamento do Grupo de Compras

Essa fase define os interesses da solução (produtos/serviços) e os modelos do grupo de compra que formam a base do modelo de gerenciamento do grupo de compra. Você criará interesses de solução, definirá modelos de função com requisitos de persona e configurará como os clientes potenciais são qualificados para funções de grupos de compra.

#### Decisão: granularidade de interesse da solução

Em que nível os interesses da solução devem ser definidos?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Interesses da solução em nível de produto | Cada produto distinto tem seu próprio grupo de compras | Mais granular; permite modelos de grupos de compra específicos do produto; pode resultar em muitos grupos de compra por conta |
| Interesses no nível da categoria de solução | Agrupar produtos relacionados em categorias de solução (por exemplo, &quot;Marketing Cloud&quot; em vez de produtos individuais) | Gerenciamento mais simples; menos grupos de compra; funções podem ser mais genéricas; recomendado para implantações iniciais |
| Interesses no nível de caso de uso | Definir interesses em torno dos resultados de negócios em vez de produtos (por exemplo, &quot;Transformação digital&quot;) | Alinha-se à venda consultiva; as funções de grupo de compra podem abranger vários produtos; é mais difícil mapear para os estágios do pipeline de CRM |

#### Decisão: design do modelo de função do grupo de compra

Como as funções devem ser definidas em cada grupo de compra?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Modelo de função padrão | Usar um conjunto comum de funções em todos os interesses da solução (por exemplo, Comprador econômico, Avaliador técnico, Especialista, Usuário final) | Pontuação e qualificação consistentes; mais fácil de gerenciar; pode não capturar funções específicas da solução |
| Modelos de função específicos da solução | Definir funções exclusivas por interesse de solução com base no comitê de compra real desse produto | Qualificações mais precisas; exige maior conhecimento de cada processo de compra; maior manutenção |
| Modelos de função hierárquicos | Defina as funções necessárias (obrigatórias para qualificação) e as funções opcionais (aprimoram a integridade, mas não são obrigatórias) | Equilibra precisão com flexibilidade; impede que critérios de qualificação excessivamente rigorosos bloqueiem o pipeline |

**Navegação da interface do usuário:** [!DNL AJO B2B Edition] > Grupos de Compra > Interesses de Solução > Criar Interesse de Solução

**Navegação da interface do usuário:** [!DNL AJO B2B Edition] > Comprando Grupos > Modelos de Função > Criar Modelo de Função

**Detalhes de configuração da chave:**

- Definir o interesse de cada solução com um nome, uma descrição e o resultado de negócios abordado
- Crie modelos de função especificando os perfis necessários para cada grupo de compras (por exemplo, &quot;Tomador de decisão&quot;, &quot;Influenciador&quot;, &quot;Profissional&quot;, &quot;Patrocinador executivo&quot;)
- Configurar critérios de qualificação de lead para função: como o sistema determina para qual persona um lead é mapeado (com base no título do cargo, departamento, antiguidade ou atributos personalizados)
- Definir limites de integridade: define qual porcentagem de funções deve ser preenchida para que um grupo de compras seja considerado &quot;completo&quot;
- Vincular interesses da solução a públicos-alvo da conta ou atributos da conta que indicam interesse potencial

**Onde as opções divergem:**

**Para A Opção A (Interesse Único Na Solução):**
Crie um interesse de solução e um modelo de função. Concentre-se em um movimento de compra claro e bem compreendido para o produto ou serviço principal da organização.

**Para A Opção B (Vários Interesses Da Solução):**
Criar vários interesses de solução, cada um com seu próprio modelo de função. Mapeie cada interesse de solução para o produto/tipo de oportunidade de CRM apropriado para rastreamento de pipeline downstream.

**Para a Opção C (Qualificação Assistida por IA):**
Configure os interesses da solução e os modelos de função como na Opção B, mas configure também o agente de qualificação de IA com dados históricos sobre composições de grupos de compras bem-sucedidas e resultados de negócios para treinar o modelo de qualificação.

**Documentação do Experience League:**

- [Visão geral dos grupos de compras](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-overview)
- [Interesses da solução](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/solution-interests)
- [Modelos de função](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-role-templates)
- [Criar grupos de compra](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-create)

### Fase 2: qualificação principal e pontuação de engajamento

**Funções do aplicativo:** [!DNL AJO B2B]: Pontuação de Compromisso, Qualificação de Conta

Essa fase configura o modelo de pontuação de engajamento que mede o engajamento no nível da pessoa nos grupos de compra e o acumula nas pontuações de preparação no nível do grupo de compra e da conta. Você configurará regras de pontuação, definirá limites de engajamento para qualificação e, opcionalmente, ativará a qualificação da conta baseada em IA.

#### Decisão: modelo de pontuação de engajamento

Como o engajamento deve ser pontuado no nível da pessoa e do grupo de compras?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Pontuação baseada em atividade | Atribuir valores de ponto a ações específicas (email aberto = 5 pontos, download de conteúdo = 15 pontos, solicitação de demonstração = 50 pontos) | Transparente e fácil de ajustar; requer manutenção contínua à medida que o conteúdo e os canais mudam; mais familiar para [!DNL Marketo] usuários |
| Pontuação ponderada por recenticidade | Ponderar atividades recentes mais altas do que as mais antigas (modelo de pontuação em decomposição) | Reflete melhor a intenção atual; impede que pontuações altas obsoletas aumentem a qualificação; configuração mais complexa |
| Pontuação baseada em IA | Use o agente de qualificação de IA do [!DNL AJO B2B] para gerar pontuações de preparação com base no reconhecimento de padrão | Mais sofisticado; adapta-se automaticamente; requer dados históricos; pode ser opaco inicialmente para as equipes de vendas |

#### Decisão: abordagem do limite de qualificação

Quando um grupo de compras deve ser considerado pronto para entrega de vendas?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Somente limite de pontuação | O grupo de compras é qualificado quando a pontuação de envolvimento agregado excede um valor definido | Simples de implementar; o limite de pontuação pode precisar de ajuste ao longo do tempo; não considera a composição da função |
| Integridade + limite de pontuação | O grupo de compras é qualificado quando a cobertura de função mínima E o limite de pontuação são atingidos | Qualificação mais robusta; impede a transferência de grupos de compra com pontuações altas, mas sem funções principais |
| Disponibilidade determinada por IA | O agente de qualificação de IA determina a prontidão usando vários sinais além da pontuação e da integridade | Mais sofisticado; conta com velocidade de compra, sinais competitivos e padrões históricos; somente a opção C |

Navegação da **UI:** [!DNL AJO B2B Edition] > Grupos de Compras > Pontuação de Envolvimento > Configurar Regras de Pontuação

**Detalhes de configuração da chave:**

- Definir regras de pontuação de engajamento: atribuir valores de ponto a eventos comportamentais (aberturas de email, cliques, visitas a páginas da Web, downloads de conteúdo, envios de formulários, participação em webinários, solicitações de demonstração)
- Configurar declínio de pontuação ou ponderação de recenticidade se estiver usando a pontuação sensível ao tempo
- Definir agregação de pontuação no nível do grupo de compras: como as pontuações de pessoas se combinam em uma pontuação de grupo de compras (soma, média ponderada ou limite mínimo por função)
- Definir limites de qualificação: os níveis de pontuação e integridade que acionam a transição para o próximo estágio de compra
- Configurar o agente de qualificação de IA (Opção C): treinar com dados históricos do negócio, definir os sinais que o agente deve considerar e definir limites de confiança

**Documentação do Experience League:**

- [Pontuação de engajamento](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [Estágios do grupo de compra](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [Qualificação da conta](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)

### Fase 3: Design e execução da jornada de conta

**Funções do aplicativo:** [!DNL AJO B2B]: Journey Orchestration de Conta, Criação de Email B2B, Gerenciamento de Canal de SMS

Essa fase projeta e implanta a jornada de conta que orquestra o engajamento com os membros do grupo de compra. Você criará jornadas de conta com condições de entrada, nós de ação (email, SMS), ramificações de condição (com base no estágio de grupo de compras, pontuação de engajamento, cobertura de função), etapas de espera e critérios de saída.

#### Decisão: acionador de entrada de Jornada

Que evento ou condição faz com que uma conta entre na jornada?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Qualificação de público da conta | Entrada de conta ao ingressar em um público-alvo de conta de destino | Orientado a lote; adequado para entrada baseada em lista ABM; o público-alvo deve ser predefinido |
| Evento de criação do grupo de compras | A conta entra quando um grupo de compras é criado pela primeira vez para a conta | Orientado a eventos; acionado pela qualificação de clientes potenciais em uma função de grupo de compra; mais tempo real |
| Alteração de atributo de conta | Entradas de conta quando um atributo específico é alterado (por exemplo, pontuação de intenção, nível de conta) | Requer que o atributo de acionamento seja atualizado em tempo real ou quase em tempo real |

#### Decisão: combinação de canais para criação B2B

Quais canais a jornada de conta deve usar para envolver membros do grupo de compras?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Somente email | A maioria das interações B2B ocorre por email; não existe uma infraestrutura de aceitação de SMS | Configuração mais simples; padrão B2B mais comum; pode perder contatos móveis |
| Email + SMS | A organização tem aceitação de SMS de contatos comerciais; notificações de alta urgência garantidas | SMS eficaz para alertas sensíveis ao tempo (lembretes de eventos, confirmações de reuniões); exige a configuração do provedor de SMS |
| Email + SMS + Alertas de vendas | Espectro completo: criação de marketing por email/SMS mais notificações da equipe de vendas | Mais abrangente; exige a adoção do fluxo de trabalho de alerta pela equipe de vendas; coordena os pontos de contato de marketing e vendas |

#### Decisão: estratégia de ramificação do Jornada

Como a ramificação de jornada deve se basear no status da conta e do grupo de compras?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Ramificação baseada em estágio | Ramificação baseada no estágio de grupo de compra (por exemplo, Percepção, Consideração, Decisão) | Alinha-se aos estágios tradicionais do funnel; conteúdo mapeado para estágios; caminho de progressão claro |
| Ramificação baseada em função | Filial para enviar conteúdo diferente a diferentes funções de grupo de compras (conteúdo técnico para avaliadores, conteúdo de ROI para compradores econômicos) | Mais personalizado; requer ativos de conteúdo específicos à função; maior esforço de produção de conteúdo |
| Ramificação baseada em participação | Ramificação baseada nos limites de pontuação de engajamento (baixo engajamento = reengajamento, alto = aceleração) | Dinâmico e responsivo; adapta-se ao comportamento real; pode criar árvores de ramificação complexas |

**Navegação da interface do usuário:** [!DNL AJO B2B Edition] > Jornadas da conta > Criar Jornada

**Detalhes de configuração da chave:**

- Criar a tela de jornada da conta com a condição de entrada selecionada
- Adicionar nós de jornada de conta: ações de email, ações de SMS, etapas de espera, divisões de condição e ramificação de caminho
- Crie conteúdo de email B2B usando o Designer de email B2B com temas de marca, fragmentos visuais e geração de conteúdo assistido por IA
- Configure tokens de personalização que fazem referência a atributos de conta, atributos de pessoa e dados de grupo de compras
- Definir durações de espera entre pontos de contato (as jornadas B2B normalmente usam esperas mais longas: 3 a 7 dias entre emails)
- Definir critérios de saída: condições sob as quais as contas deixam a jornada (o grupo de compras atinge o limite de qualificação, a oportunidade criada no CRM, a conta recusa)
- Configurar ações de SMS se estiver usando um canal SMS (requer a configuração do provedor SMS e a aceitação de contato)
- Testar a jornada com contas de teste antes de publicar

**Onde as opções divergem:**

**Para A Opção A (Interesse Único Na Solução):**
Projetar uma jornada linear com estágios sequenciais. A entrada é baseada em um único público-alvo de conta ou evento de criação de grupo de compra. Uma trilha de criação de email com urgência e profundidade crescentes de conteúdo.

**Para A Opção B (Vários Interesses Da Solução):**
Criar uma jornada com ramificações paralelas por interesse de solução. Use nós de condição para rotear contas para o rastreamento de criação apropriado com base nos grupos de compra existentes. Cada ramificação tem seu próprio conteúdo e limites de pontuação.

**Para a Opção C (Qualificação Assistida por IA):**
Crie uma jornada em que os nós de condição avaliem a pontuação de qualificação de IA em vez de (ou além de) limites baseados em regras. Inclua a seleção de caminho dinâmico na qual a IA determina se uma conta deve ser acelerada, mantida ou não.

**Documentação do Experience League:**

- [Visão geral das jornadas da conta](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-overview)
- [Nós de jornada de conta](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-nodes)
- [Criação de email B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/email-authoring)
- [Canal SMS no AJO B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sms-authoring)
- [Assistente de IA para criação de email](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/ai-assistant-emails)

### Fase 4: Alinhamento de vendas e integração de CRM

**Funções do aplicativo:** [!DNL AJO B2B]: Configuração de Alerta de Vendas, Insights de Vendas do CRM; [!DNL RT-CDP B2B]: Configuração de Destino de Conta, Conta Audience Activation

Essa fase estabelece a ponte entre marketing e vendas, configurando emails de alerta de vendas, implantando os Insights de Vendas do CRM para visibilidade no CRM e, opcionalmente, ativando públicos-alvo de conta para destinos B2B ([!DNL LinkedIn], [!DNL Marketo], sistemas CRM).

#### Decisão: estratégia de acionador de alerta de vendas

Quando as vendas devem ser notificadas sobre o status do grupo de compras de uma conta?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Alertas baseados em marcos | Notificar vendas quando o grupo de compras atingir etapas específicas (qualificado, concluído, alto envolvimento) | Notificações claras e discretas; evita a fadiga do alerta; pode perder tendências de engajamento gradual |
| Alertas baseados em limite | Notificar vendas quando a pontuação do compromisso ultrapassar um limite definido | Monitoramento contínuo; pode acionar vários alertas, já que as pontuações flutuam perto do limite |
| Alertas de transição de preparo | Notificar vendas ao comprar transições de grupo para um novo estágio (por exemplo, da consideração para a decisão) | Alinha-se aos estágios do pipeline; sinal mais claro para ação de vendas; requer definições de estágio bem definidas |

#### Decisão: profundidade da integração do CRM

Até que ponto os dados do grupo de compras devem ser exibidos no CRM?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Somente alertas de vendas (nenhum componente no CRM) | A organização não usa [!DNL Salesforce] ou [!DNL Dynamics], ou a integração com o CRM não é viável | Menor esforço de integração; as vendas recebem notificações por email, mas não têm painel de CRM; visibilidade limitada |
| Painel de insights de vendas do CRM | A organização usa [!DNL Salesforce] ou [!DNL Dynamics] e deseja que o status do grupo de compras fique visível no CRM | Requer a instalação do pacote CRM Sales Insights; fornece inteligência avançada em nível de conta; recomendado para a maioria das implementações |
| Sincronização de CRM bidirecional completa | A compra de estágios de grupo e pontuações retornam aos objetos do CRM, influenciando o fluxo de trabalho e os relatórios do CRM | Maior complexidade de integração; permite a geração de relatórios de pipeline nativo de CRM; requer configuração personalizada de CRM |

Navegação da **UI:** [!DNL AJO B2B Edition] > Administração > Configuração de Alerta de Vendas

**Navegação da interface do usuário:** [!DNL AJO B2B Edition] > Administração > CRM Sales Insights > Configurar

**Detalhes de configuração da chave:**

- Configurar modelos de email de alerta de vendas: incluir status do grupo de compras, perfis de engajamento, pontuação do engajamento e próximas ações recomendadas
- Definir regras de roteamento de alertas: quais representantes de vendas ou equipes receberão alertas com base na propriedade da conta, no território ou nos interesses da solução
- Instalar e configurar o CRM Sales Insights para [!DNL Salesforce] ou [!DNL Dynamics 365]
- Mapear dados do grupo de compra para objetos de CRM para que as vendas possam exibir a composição do grupo de compra, o envolvimento e o progresso da jornada no fluxo de trabalho do CRM
- Opcionalmente, configure conexões de destino de conta para ativar públicos-alvo de conta para [!DNL LinkedIn] (para publicidade ABM), [!DNL Marketo Engage] (para acompanhamento de nível de lead) ou outros destinos B2B

**Documentação do Experience League:**

- [Emails de alerta de vendas](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sales-alert-email)
- [Insights de vendas do CRM](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/crm-sales-insights)
- [Visão geral dos destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [Destino de públicos correspondentes do LinkedIn](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)

### Fase 5: Relatórios e otimização

**Funções de aplicativo:** [!DNL AJO B2B]: painéis B2B do Analytics

Essa fase estabelece a estrutura de relatórios e análises para medir o desempenho do grupo de compras, a eficácia da jornada da conta e o impacto do pipeline. [!DNL AJO B2B Edition] O fornece painéis de análise incorporados; o [!DNL CJA B2B Edition] (se licenciado) estende a análise com insights mais profundos em nível de conta entre canais.

#### Decisão: abordagem de relatórios

Quais ferramentas de análise devem ser configuradas para o monitoramento contínuo do desempenho?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Somente painéis de [!DNL AJO B2B] | Os painéis internos de [!DNL AJO B2B Edition] são suficientes para comprar métricas de grupo e jornada | A configuração é mais rápida; abrange métricas B2B principais; recurso limitado de análise personalizada |
| [!DNL AJO B2B] painéis + [!DNL CJA B2B Edition] | A organização precisa de análises mais detalhadas entre canais, análises de grupos de compras, correlação de oportunidades e atribuição personalizada | Requer [!DNL CJA B2B Edition] licença; mais abrangente; suporta análise de forma livre em nível de conta |
| [!DNL AJO B2B] painéis + relatórios do CRM | A organização prefere centralizar os relatórios de pipeline no CRM ao lado das métricas do grupo de compra | Exige desenvolvimento de painel de CRM; combina métricas de marketing e vendas em um local; limitado aos recursos de relatório de CRM |

**Navegação da interface do usuário:** [!DNL AJO B2B Edition] > Painéis > Visão geral do engajamento / Painel inteligente

**Detalhes de configuração da chave:**

- Acesse o Painel de Envolvimentos do [!DNL AJO B2B] para monitorar as pontuações de engajamento do grupo de compras, as taxas de conclusão e a distribuição de estágios
- Acesse o Painel inteligente para obter insights orientados por IA sobre a disponibilidade da conta e a qualidade do pipeline
- Se estiver usando [!DNL CJA B2B Edition]: configure uma conexão do CJA baseada em conta, incluindo [!DNL AJO B2B] conjuntos de dados, configure uma visualização de dados B2B com contêineres Grupo de compras e Conta e compile a análise do espaço de trabalho para progressão do grupo de compras, correlação de oportunidades e atribuição
- Definir a cadência de relatórios: revisões semanais de desempenho do grupo de compras, análise mensal do impacto do pipeline, otimização trimestral do programa
- Crie anotações para eventos significativos (lançamentos de campanha, atualizações de conteúdo, alterações no modelo de pontuação) para correlacionar com tendências de desempenho

**Documentação do Experience League:**

- [Painéis de análise B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/buying-groups-dashboard)
- [Painel de engajamento](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/engagement-dashboard)
- [Painel inteligente](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/intelligent-dashboard)
- [Visão geral do CJA B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

## Considerações de implantação

As seções a seguir abordam medidas de proteção, armadilhas comuns, práticas recomendadas e decisões de compensação que devem ser consideradas durante a implementação.

### Medidas de proteção e limites

- Limites de jornada de conta do [!DNL AJO B2B Edition], incluindo máximo de jornadas simultâneas e máximo de contas por jornada. Siga as [!DNL AJO B2B Edition] medidas de proteção do produto — [Medidas de proteção B2B do AJO](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)
- O [!DNL RT-CDP B2B Edition] dá suporte a até 50 classes de esquema B2B e segue as medidas de proteção de perfil e segmentação padrão — [Medidas de proteção de perfil do cliente em tempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- A avaliação do público-alvo da conta opera em agendamentos em lote; as atualizações do público-alvo da conta em tempo real não são suportadas para todos os tipos de segmentos — [Medidas de proteção de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails)
- A assimilação do conector de origem B2B tem intervalos mínimos de agendamento (normalmente 15 minutos para [!DNL Marketo], variando para fontes CRM) — [Medidas de proteção de assimilação](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- As superfícies dos canais de email são limitadas a 10 por tipo de canal por sandbox — [medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)

### Armadilhas comuns

- **Definir muitas funções por grupo de compras:** Especificar funções em excesso (por exemplo, exigindo de 8 a 10 personalidades distintas) torna praticamente impossível para grupos de compras atingir limites de integridade. Comece com 3 a 5 funções essenciais e expanda à medida que o modelo amadurece.
- **Definindo limites de pontuação de engajamento muito altos ou muito baixos:** Se os limites forem muito altos, nenhum grupo de compra será qualificado, deixando o pipeline sem efeito. Se forem muito baixas, as contas não qualificadas inundam as vendas. Comece com a análise de dados históricos (se disponível) e repita com base no feedback de vendas.
- **Ignorando a qualidade da resolução de pessoa para conta:** se as pessoas não estiverem corretamente vinculadas às contas, os grupos de compra terão membros ausentes mesmo quando as pessoas certas estiverem envolvidas. Invista na qualidade da resolução de identidade antes de iniciar jornadas de grupos de compra.
- **Contatos de mensagens em excesso em vários grupos de compra:** Um único contato pode ter funções em vários grupos de compra (por exemplo, um CTO que é um Avaliador Técnico para compras de CRM e da Plataforma de Dados). Sem o gerenciamento de frequência, essa pessoa recebe emails de cada jornada ativa. Implemente regras de frequência entre jornadas.
- **Ignorando a habilitação de vendas:** as equipes de vendas devem entender como interpretar os dados do grupo de compras, as pontuações de engajamento e os alertas de vendas. Sem treinamento e adoção, a entrega de marketing para vendas falha, independentemente da qualidade dos dados.
- **Tratando jornadas de conta como jornadas de pessoa:** As jornadas de conta operam no nível de conta, enviando emails para pessoas nos grupos de compra da conta. O design da jornada deve considerar que várias pessoas recebem mensagens por execução de nó de conta, o que é fundamentalmente diferente das jornadas no nível de pessoa [!DNL AJO].

### Práticas recomendadas

- **Comece com um interesse de solução e expanda** — prove que o modelo funciona para um movimento de compra antes de dimensionar para vários interesses de solução. Isso permite que a equipe refine os modelos de função, os modelos de pontuação e o conteúdo antes de adicionar complexidade.
- **Alinhar funções de grupo de compras com o processo de vendas do CRM** — Mapeie as funções de grupo de compras para as personalidades que a equipe de vendas já reconhece. Usar o mesmo idioma (Comprador econômico, Especialista etc.) então a transferência é intuitiva.
- **Implemente um loop de comentários com vendas** — Colete regularmente comentários de vendas sobre a qualidade das contas qualificadas para marketing. Use este feedback para ajustar os limites de pontuação do engajamento e os critérios de qualificação da função.
- **Crie conteúdo para funções, não apenas estágios** — diferentes funções de grupos de compras precisam de conteúdo diferente: os executivos querem ROI e impacto estratégico, os avaliadores técnicos querem detalhes de arquitetura e integração, os usuários finais querem demonstrações fáceis de usar. Mapeie ativos de conteúdo para funções, visando uma criação mais eficaz.
- **Configure os Insights de Vendas do CRM com antecedência** — Não espere até que a jornada completa esteja ativa para implantar a visibilidade do CRM. As equipes de vendas precisam ver os dados do grupo de compras se formando antecipadamente para fornecer feedback sobre a precisão da função e o direcionamento da conta.
- **Usar etapas de espera estrategicamente** — Os ciclos de compra B2B são longos. As etapas de espera da jornada da conta devem refletir essa realidade (intervalos de 5 a 14 dias entre toques) em vez da urgência do estilo do consumidor (1 a 3 dias).
- **Monitorar a velocidade de engajamento, não apenas a pontuação de engajamento** — Um grupo de compras que vai da pontuação 20 para 80 em duas semanas indica uma intenção mais forte do que uma que chega a 80 em seis meses. Configure a pontuação e a qualificação para levar em conta a velocidade.

### Decisões de compensação

As seguintes compensações devem ser avaliadas com base nas necessidades específicas da sua organização.

#### Integridade do grupo de compra vs. volume de pipeline

Exigir que todas as funções sejam preenchidas antes de qualificar um grupo de compras maximiza a qualidade do pipeline, mas pode limitar seriamente o volume de contas qualificadas, especialmente para novos produtos ou mercados onde o banco de dados da organização tem cobertura limitada.

- **O limite de integridade mais alto favorece:** qualidade do pipeline; as vendas recebem grupos de compras totalmente formados; taxas de ganho mais altas por conta
- **O limite de integridade mais baixo favorece:** Volume de pipeline; mais contas atingem as vendas; cobertura mais ampla; volume mais alto, mas qualidade potencialmente mais baixa
- **Recomendação:** comece com um limite moderado (60-70% de cobertura de função) e ajuste com base nos dados da taxa de ganho real. Para mercados estabelecidos com boa cobertura de dados, aumente para mais de 80%. Para novos mercados, aceite inicialmente de 50 a 60% e use campanhas de integridade do grupo de compra para preencher lacunas.

#### Granularidade de pontuação versus simplicidade operacional

Modelos de pontuação altamente granulares (com dezenas de tipos de atividades, ponderação de recenticidade e pontuação específica por função) fornecem sinais de qualificação mais precisos, mas são mais difíceis de manter, explicar e solucionar problemas.

- **A maior granularidade favorece:** Precisão da qualificação; diferenciação diferenciada entre contas; melhor alinhamento com processos de compra complexos
- **A menor granularidade favorece:** simplicidade operacional; mais fácil de manter e explicar para as vendas; implementação mais rápida; menos casos de borda
- **Recomendação:** comece com um modelo de pontuação simples (10 a 15 tipos de atividade, valores de ponto uniformes) e adicione complexidade apenas onde o modelo simples não consegue diferenciar a qualidade da conta. Documente o modelo de pontuação completamente para alinhamento de vendas.

#### Jornada única versus várias jornadas especializadas

Uma jornada de conta única e abrangente que lida com todos os estágios e interesses de solução em uma tela fornece controle unificado, mas pode se tornar difícil de controlar. Várias jornadas especializadas (uma por estágio ou interesse de solução) são mais simples individualmente, mas mais difíceis de coordenar.

- **Uma única jornada favorece:** exibição holística; mais fácil de garantir tempo e mensagens consistentes; mais simples de monitorar; um local para toda a lógica
- **Várias jornadas favorecem:** Modularidade; mais fácil de atualizar um estágio sem afetar os outros; equipes diferentes podem ter jornadas diferentes; design de tela mais limpo
- **Recomendação:** para a Opção A, uma única jornada é apropriada. Para as Opções B e C, use uma jornada de &quot;orquestração&quot; principal que encaminha as contas para sub-jornadas especializadas por interesse da solução ou estágio de compra.

## Documentação relacionada

Os recursos a seguir fornecem detalhes adicionais sobre os aplicativos e recursos referenciados neste guia.

### [!DNL AJO B2B Edition]

- [Página inicial da documentação do AJO B2B edition](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)
- [Visão geral dos grupos de compras](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-overview)
- [Interesses da solução](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/solution-interests)
- [Modelos de função](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-role-templates)
- [Criar grupos de compra](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-create)
- [Estágios do grupo de compra](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [Visão geral das jornadas da conta](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-overview)
- [Nós de jornada de conta](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-nodes)
- [Emails de alerta de vendas](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sales-alert-email)
- [Insights de vendas do CRM](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/crm-sales-insights)

### E-mail e conteúdo B2B

- [Criação de email B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/email-authoring)
- [Criação de SMS no AJO B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sms-authoring)
- [Assistente de IA para criação de email](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/ai-assistant-emails)

### Análises e painéis B2B

- [Painel de grupos de compra](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/buying-groups-dashboard)
- [Painel de engajamento](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/engagement-dashboard)
- [Painel inteligente](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/intelligent-dashboard)
- [Visão geral do CJA B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

### [!DNL RT-CDP B2B Edition]

- [Visão geral da B2B edition da RT-CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview)
- [Esquemas B2B no Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Públicos da conta](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences)
- [Conector de origem do Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)

### Base de dados

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Visão geral das fontes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)

### Configuração de canais

- [Introdução à configuração de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Configurar canal de SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)

### Governança e privacidade de dados

- [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Gerenciamento avançado do ciclo de vida dos dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)

### Destinos

- [Visão geral dos destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [Destino de públicos correspondentes do LinkedIn](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)

### Medidas de proteção

- [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Proteções de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails)
- [Medidas de proteção de assimilação](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- [Medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)

### Tutoriais e introdução

- [Introdução ao AJO B2B edition](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)
- [Tutorial do RT-CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-tutorial)
