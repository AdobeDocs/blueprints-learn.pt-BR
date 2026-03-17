---
title: Offer Decisioning
description: Saiba como usar a lógica de decisão centralizada para selecionar a próxima melhor oferta ou conteúdo para um perfil em vários canais.
solution: Journey Optimizer, Real-Time Customer Data Platform
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '7889'
ht-degree: 2%

---


# Offer Decisioning

Este guia fornece uma referência de implementação abrangente para o Offer Decisioning usando a [!DNL Adobe Journey Optimizer] (AJO) Decisioning e a [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP). Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam implementar uma lógica centralizada de seleção de ofertas que determine a próxima melhor oferta para cada perfil de cliente em todos os canais.

Use este guia para entender o que precisa ser configurado, onde existem opções e quais compensações se aplicam a cada decisão.

O padrão separa a decisão &quot;o que mostrar&quot; da lógica de canal &quot;onde mostrar&quot;, permitindo uma seleção de oferta consistente e otimizada por email, Web, aplicativo móvel e qualquer outro ponto de contato. O AJO Decisioning gerencia todo o ciclo de vida da oferta: criação de ofertas e gerenciamento de catálogos, regras de elegibilidade (quem pode ver cada oferta), estratégias de classificação (como selecionar entre ofertas elegíveis), disposições (onde as ofertas aparecem) e políticas de decisão (que vinculam tudo).

## Visão geral do caso de uso

As empresas geralmente precisam apresentar a oferta, a promoção ou o incentivo mais relevante para cada cliente no momento da interação. Se a interação ocorrer em uma campanha de email, em uma página inicial do site, em um aplicativo móvel ou em um ponto de decisão em uma jornada de várias etapas, o desafio é o mesmo: selecionar a oferta ideal de um catálogo de opções disponíveis com base em quem é o cliente, para o que ele se qualifica e qual oferta tem maior probabilidade de gerar o resultado desejado.

O Offer Decisioning aborda isso centralizando toda a lógica de seleção de ofertas no mecanismo de Gestão de decisões da AJO. Em vez de codificar atribuições de oferta em campanhas ou canais individuais, o mecanismo de decisão avalia os atributos, a associação de público-alvo e os sinais contextuais de cada perfil para determinar a melhor oferta em tempo real. Essa centralização garante que o mesmo cliente receba ofertas consistentes e otimizadas, independentemente do canal pelo qual se envolva.

Esse padrão difere da personalização da Web/aplicativo de visitante conhecido no escopo — o Offer Decisioning é independente de canal e centralizado, enquanto a personalização de visitante conhecido se concentra na personalização de superfície digital. Ela difere da recomendação comportamental na abordagem — o offer decisioning usa regras de elegibilidade explícitas e estratégias de classificação, enquanto a recomendação comportamental enfatiza recomendações comportamentais orientadas por sinais usando estratégias de seleção e modelos de aprendizado de máquina.

## Principais objetivos de negócios

Os seguintes objetivos de negócios são compatíveis com esse padrão de caso de uso.

**[Fornecer experiências personalizadas ao cliente](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**
Personalize conteúdo, ofertas e mensagens para preferências individuais, comportamentos e estágios do ciclo de vida.
**KPIs:** Envolvimento, Taxas de Conversão, Satisfação do Cliente (CSAT)

**[Impulsionar vendas cruzadas e vendas adicionais](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)**
Promova produtos ou serviços complementares e premium para os clientes existentes com base no histórico de comportamento e de compras.
**KPIs:** % de venda adicional/venda cruzada, receita incremental, valor vitalício do cliente

**[Aumente a fidelidade do cliente e o valor vitalício](../../business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)**
Aprofunde as relações com o cliente e maximize o valor a longo prazo por meio de programas de fidelidade, recompensas e envolvimento personalizado.
**KPIs:** Valor vitalício do cliente, Retenção, % de venda adicional/venda cruzada

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

## Padrão do caso de uso

Esta seção descreve a cadeia de funções e a definição de padrão para o Offer Decisioning.

**Offer Decisioning**

Use a lógica de decisão centralizada para selecionar a melhor oferta ou conteúdo para um perfil em todos os canais.

**Cadeia de funções:** Avaliação de público-alvo > Qualificação da oferta > Estratégia de classificação > Execução de decisão > Entrega > Relatórios

Consulte a seção [Opções de implementação](#implementation-options) para saber como cada composição se manifesta.

## Aplicativos

Os seguintes aplicativos da Adobe são usados neste padrão de caso de uso.

- **[!DNL Adobe Journey Optimizer](AJO)** — Mecanismo do Gerenciamento de Decisões para criação de ofertas, regras de qualificação, estratégias de classificação, posicionamentos e políticas de decisão; configuração de canais e criação de mensagens para entrega de ofertas; execução de campanhas e jornadas
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)** — Avaliação de público-alvo para segmentos de qualificação de oferta; dados de perfil e atributos computados usados na qualificação e classificação
- **[!DNL Adobe Experience Platform](AEP)** — Repositório de perfil unificado, resolução de identidade e base de dados com suporte para AJO e RT-CDP

## Funções básicas

Os seguintes recursos básicos devem estar em vigor para esse padrão de caso de uso. Para cada função, o status indica se ele é tipicamente necessário, se presume ser pré-configurado ou se não é aplicável.

| Função de base | Status | O que deve estar em vigor | Referência do Experience League |
| --- | --- | --- | --- |
| Administração e governança | Presumido em vigor | sandbox da AJO com permissões de decisão ativadas. Funções de gerenciamento de ofertas (Gerente de decisão, Aprovador de oferta) atribuídas à equipe de implementação. | [Visão geral das sandboxes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/home), [Visão geral do controle de acesso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Preparação e modelagem de dados | Obrigatório | O esquema de perfil deve incluir atributos usados para regras de qualificação de oferta (por exemplo, nível de fidelidade, histórico de compras, tipo de assinatura). Um esquema de resposta/interação da oferta para rastrear impressões, cliques e conversões da oferta deve estar em vigor. | [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [noções básicas de composição de esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| Fontes de dados e coleção | Presumido em vigor | Os atributos de perfil usados nas regras de elegibilidade devem ser atuais. Para entrega na Web (Opção B), o Web SDK deve ser implementado com o serviço AJO ativado na sequência de dados. Para delivery de email, os atributos do perfil devem ser resolvíveis no momento do envio. | [Visão geral do Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home), [Configurar sequências de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure) |
| Configuração de identidade e perfil | Presumido em vigor | Os perfis devem ser resolvidos em todos os canais onde as ofertas são entregues. Para a consistência da oferta entre canais, a identidade unificada é essencial — o mesmo perfil deve ser reconhecido nos contextos de email, Web e dispositivos móveis. Uma política de mesclagem ativa de borda é necessária para a entrega de aplicativos/Web em tempo real. | [Visão geral do Serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| Definição e segmentação do público-alvo | Obrigatório | Os públicos-alvo usados como critérios de qualificação de oferta devem ser definidos e avaliados (por exemplo, &quot;clientes de alto valor&quot;, &quot;usuários de avaliação&quot;, &quot;nível gold de fidelidade&quot;). O método de avaliação deve corresponder à latência de delivery — avaliação de borda para web/aplicativo em tempo real, batch ou streaming para campanhas de email. | [Visão geral do Serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder) |

## Funções de suporte

Os recursos a seguir aumentam esse padrão de caso de uso, mas não são necessários para a execução principal.

| Função de suporte | Status | Por que é importante | Referência do Experience League |
| --- | --- | --- | --- |
| Criação de atributo calculado/derivado | Recomendado | As pontuações de propensão da IA do cliente, os cálculos do valor vitalício e as métricas de envolvimento melhoram significativamente a eficácia da estratégia de classificação. Atributos calculados, como &quot;dias desde a última compra&quot; ou &quot;total gasto em 90 dias&quot;, permitem regras de elegibilidade mais precisas e classificação baseada em fórmula. | [Visão geral dos atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview), [Visão geral da IA do cliente](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview) |
| Gerenciamento do ciclo de vida dos dados | Recomendado | O histórico de ofertas e os dados de eventos de decisão se acumulam ao longo do tempo. As políticas de retenção (expiração) devem ser configuradas para oferecer conjuntos de dados de eventos de interação para gerenciar o armazenamento e atender aos requisitos de retenção de dados. | [Visão geral do Gerenciamento Avançado do Ciclo de Vida dos Dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [Expirações do conjunto de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration) |
| Rotulagem e aplicação de uso de dados | Recomendado | Os rótulos de governança garantem que as ofertas com critérios de direcionamento sigilosos (por exemplo, status financeiro, condições de integridade) estejam em conformidade com as políticas de uso de dados. Os rótulos em campos usados nas regras de elegibilidade impedem o direcionamento de ofertas não compatíveis. | [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [Visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview) |
| Monitoramento e capacidade de observação | Recomendado | O desempenho do mecanismo de decisão, as taxas de fallback e a integridade da entrega de ofertas devem ser monitorados. Alertas para altas taxas de fallback podem indicar problemas de configuração incorreta da regra de elegibilidade ou de atualização de dados. | [Visão geral dos alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview), [Visão geral dos Insights de observação](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| Relatórios e análise | Incluído | O relatório de desempenho da oferta faz parte da cadeia de funções (Fase 7). A análise da CJA permite a medição da eficácia da oferta em vários canais, a atribuição de impacto na receita e a identificação da oportunidade de otimização. | [visão geral do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [visão geral do Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home) |

## Funções do aplicativo

Este plano exerce as seguintes funções do Catálogo de Funções da Aplicação. As funções são mapeadas para fases de implementação em vez de etapas numeradas.

### [!DNL Journey Optimizer] (AJO)

A tabela a seguir lista as funções do AJO e as fases de implementação nas quais elas são configuradas.

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Decisão. | Fase 3: Configuração da decisão | Criar itens de oferta, definir regras de qualificação, configurar estratégias de classificação, criar ofertas de fallback, definir disposições e criar políticas de decisão |
| Configuração de canais | Fase 4: Configuração de canal e superfície | Configurar superfícies de canal de email, da Web, no aplicativo ou baseadas em código para entrega de ofertas |
| Criação de mensagens | Fase 5: configuração de conteúdo e entrega | Criar modelos de mensagem com zonas de posicionamento de ofertas; configurar experiências baseadas em código para entrega de aplicativos/Web |
| Execução de campanha | Fase 5: configuração de conteúdo e entrega | Executar campanhas programadas ou acionadas por API que chamam políticas de decisão (Opção A) |
| Experimentação de conteúdo | Fase 5: configuração de conteúdo e entrega | Opcionalmente, teste A/B de diferentes estratégias de classificação ou ofereça variantes criativas |
| Relatórios e análise de desempenho | Fase 7: Monitoramento de desempenho e emissão de relatórios | Monitorar a distribuição da seleção de ofertas, as taxas de aceitação, as taxas de fallback e o desempenho em nível de canal |

### [!DNL Real-Time CDP] (RT-CDP)

A tabela a seguir lista as funções da RT-CDP e as fases de implementação nas quais elas são configuradas.

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Avaliação de público | Fase 2: Avaliação de público-alvo | Defina e avalie os públicos-alvo usados para regras de qualificação de oferta; selecione o método de avaliação apropriado (lote, streaming ou borda) |
| Enriquecimento de perfil | Fase 1 (Suporte): Atributos Calculados | Enriqueça os perfis com atributos computados e pontuações de propensão que melhoram a eficácia da estratégia de classificação |

## Pré-requisitos

Conclua os seguintes pré-requisitos antes de iniciar a implementação.

- [ ] sandbox da AJO com recursos de Gestão de decisões habilitados
- [ ] funções de usuário com permissões de Gerenciamento de decisão (criar/editar ofertas, posicionamentos, decisões)
- [ ] O esquema de perfil inclui atributos necessários para a qualificação da oferta (por exemplo, nível de fidelidade, segmento de cliente, nível de assinatura)
- [ ] Os dados do perfil estão atualizados e foram ativamente assimilados para a atualização do atributo de qualificação
- [ ] Para Opção A (Email): Superfície de canal de email configurada com subdomínio verificado e pool de IP aquecido
- [ ] Para Opção B (Web/Aplicativo): Web SDK implementado com o serviço AJO habilitado na sequência de dados; política de mesclagem de borda ativa configurada
- [ ] Para a Opção C (Jornada): Jornada permissões da tela e pelo menos um evento de entrada de jornada ou público configurado
- [ ] Ofereça ativos criativos (imagens, cópia, CTAs) preparados para cada combinação de oferta e posicionamento
- [ ] Conteúdo de oferta de fallback preparado para cada posicionamento
- [ ] públicos-alvo para regras de qualificação de oferta definidas e avaliadas na RT-CDP

## Opções de implementação

Esta seção descreve as opções de implementação disponíveis para o Offer Decisioning. Cada opção fornece um canal de entrega e um contexto de caso de uso diferentes.

### Opção A: decisão de oferta de email

Essa opção é mais adequada para selecionar a melhor oferta a ser incluída em campanhas de email de saída: emails promocionais, personalização de boletins informativos, emails de ciclo de vida com conteúdo dinâmico de ofertas. A decisão é tomada no momento da renderização da mensagem para cada recipient.

#### Como funciona

As políticas de decisão são chamadas durante a renderização da mensagem de email para selecionar a melhor oferta para cada recipient. O modelo de email inclui uma zona de posicionamento de ofertas em que o mecanismo de decisão insere a representação de conteúdo da oferta selecionada (imagem, HTML ou texto). No momento do envio, o mecanismo avalia o perfil de cada recipient em relação às regras de elegibilidade da oferta, aplica a estratégia de classificação e incorpora o conteúdo da oferta vencedora no email.

Essa abordagem funciona com campanhas agendadas (avaliadas no tempo de execução da campanha) e emails incorporados à jornada (avaliadas quando o perfil atinge o nó de ação da mensagem). O conteúdo da oferta — imagem, título, body copy e CTA — é personalizado por recipient com base no resultado da decisão.

#### Principais considerações

- A elegibilidade da oferta é avaliada no momento do envio usando o estado atual do perfil
- A avaliação de público em lote é suficiente, pois as decisões ocorrem durante a renderização da mensagem
- Cada oferta precisa de uma representação de conteúdo de imagem ou HTML para a disposição do email
- A oferta substituta deve ter conteúdo para cada posicionamento de email usado

#### Vantagens

- Caminho de implementação mais simples — usa delivery de email padrão de campanha ou jornada
- Sem requisitos de SDK do lado do cliente
- Funciona com a infraestrutura de email e as superfícies de canal existentes
- Oferece suporte a grandes volumes de público por meio da execução de campanhas em lote

#### Limitação

- A decisão é tomada no momento do envio; não é possível se adaptar ao comportamento pós-envio
- O conteúdo da oferta é estático após o email ser entregue (sem atualizações em tempo real)
- Limitado aos atributos de perfil disponíveis no armazenamento de perfil do hub (não borda)

#### Recursos do Experience League

- [Entregar ofertas em mensagens](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Criar uma campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)

### Opção B: decisão de oferta em tempo real da Web/aplicativo

Essa opção é melhor para a seleção de ofertas em tempo real em páginas da Web ou aplicativos móveis: banners promocionais de página inicial, widgets de oferta do painel de conta, cartões de oferta no aplicativo ou qualquer superfície digital onde a oferta deve ser selecionada no momento em que a página é carregada ou a tela é renderizada.

#### Como funciona

As políticas de decisão são chamadas no carregamento de página ou no renderizador da tela do aplicativo por meio da rede do Edge Decisioning ou de experiências baseadas em código. Quando um visitante carrega uma página, o Web SDK envia uma solicitação à Edge Network, que avalia o perfil de borda do visitante em relação às regras de elegibilidade de oferta e às estratégias de classificação. A oferta selecionada é retornada na resposta e renderizada no posicionamento configurado na superfície digital.

Para experiências baseadas em código, o aplicativo recupera a resposta de decisão e renderiza o conteúdo da oferta usando a lógica de front-end personalizada. Para experiências de canal da Web, o canal da Web do AJO pode inserir o conteúdo da oferta diretamente na página usando criação visual ou baseada em código.

#### Principais considerações

- Exige implementação do Web SDK ou Mobile SDK com o serviço AJO habilitado na sequência de dados
- A política de mesclagem ativa na Edge é necessária para pesquisas de perfil em tempo real
- Os públicos-alvo usados para qualificação devem oferecer suporte à avaliação de borda (verificações de atributos simples e associação de segmento)
- As representações de conteúdo de oferta devem usar formatos JSON ou de URL de imagem para renderização no lado do cliente
- O rastreamento de impressão deve ser implementado para capturar exibições e cliques de oferta

#### Vantagens

- Seleção de oferta em tempo real e na sessão com base no estado atual do perfil do visitante
- Latência de decisão de subsegundos por meio do Edge Network
- As ofertas se adaptam aos dados de perfil mais atuais disponíveis na borda
- Suporta testes A/B de estratégias de oferta por meio de experimentação de conteúdo

#### Limitação

- Exige implementação do SDK no lado do cliente (Web SDK ou Mobile SDK)
- O perfil do Edge tem um subconjunto de atributos completos de perfil de hub — regras complexas de elegibilidade podem não ser avaliadas corretamente
- Os segmentos do Edge têm restrições de complexidade de regra de segmento (sem consultas de série de tempo)
- Requer desenvolvimento de front-end para renderização personalizada em experiências baseadas em código

#### Recursos do Experience League

- [Fornecer ofertas usando a API do Edge Decisioning](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [Canal de experiência baseado em código](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based-experience/get-started-code-based)

### Opção C: Jornada nó de decisão

Essa opção é mais adequada para a seleção de ofertas em uma jornada de várias etapas: selecionar a melhor oferta em um ponto de decisão em uma jornada do cliente e, em seguida, entregá-la por meio do nó de próxima ação. Use isso quando a decisão de oferta fizer parte de um fluxo de orquestração mais amplo com esperas, condições e várias ações de mensagem.

#### Como funciona

As políticas de decisão são chamadas de um nó de decisão em uma tela de jornada do AJO. Quando um perfil atinge o nó de decisão, o mecanismo avalia a qualificação e a classificação da oferta para selecionar a oferta ideal. A oferta selecionada informa a próxima ação de mensagem — qual conteúdo de oferta deve ser incluído, qual canal deve ser usado ou qual ramificação de jornada deve ser usada com base no resultado da oferta.

Essa abordagem permite jornadas adaptáveis em que a decisão de oferta influencia etapas de jornada subsequentes. Por exemplo, uma jornada pode selecionar a melhor oferta, entregá-la por email, aguardar o engajamento e fazer o acompanhamento com uma notificação por push se a oferta não for aberta.

#### Principais considerações

- A jornada deve ser projetada com um nó de decisão seguido por um ou mais nós de ação de mensagem
- A elegibilidade da oferta é avaliada usando o estado do perfil no momento em que o perfil atinge o nó de decisão
- As etapas de espera de jornada entre a decisão e a entrega podem fazer com que o estado do perfil seja alterado
- Pode combinar com a ramificação de jornada para tomar caminhos diferentes com base na oferta selecionada

#### Vantagens

- Integra a seleção de ofertas em fluxos de orquestração de várias etapas
- Habilita jornadas adaptáveis onde a escolha da oferta influencia etapas subsequentes
- Oferece suporte à entrega entre canais na mesma jornada (email, push, SMS)
- Pode combinar com condições de jornada para rastreamento de envolvimento pós-oferta

#### Limitação

- Configuração mais complexa do que a decisão de campanha independente
- Os limites de taxa de transferência de jornada se aplicam (taxa de entrada de 5.000 perfis por segundo)
- A decisão está vinculada ao contexto do jornada — as alterações exigem o controle de versão do jornada
- A jornada deve ser republicada para que as atualizações do catálogo de ofertas ou da política de decisão entrem em vigor

#### Recursos do Experience League

- [Entregar ofertas em mensagens](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Introdução ao jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

### Comparação de opções

A tabela a seguir compara as três opções de implementação entre os principais critérios.

| Critérios | Opção A: decisão por email | Opção B: tempo real da Web/aplicativo | Opção C: Jornada nó de decisão |
| --- | --- | --- | --- |
| Melhor para | Campanhas de email em lote com seleção de oferta por recipient | Banners de oferta em tempo real em superfícies da Web/do aplicativo | Seleção de oferta em jornadas orquestradas em várias etapas |
| Latência de decisão | No momento do envio (segundos por recipient durante a renderização do lote) | Subsegundo (Edge Network) | Na execução do nó de jornada (segundos) |
| Canal | Email | Web, aplicativo móvel, superfícies baseadas em código | Qualquer canal (email, push, SMS) no jornada |
| SDK obrigatório | Não | Sim (Web SDK ou SDK móvel) | Não (para email/push); Sim (se o canal da Web for uma ação de jornada) |
| Avaliação de público | Lote ou transmissão | Edge | Lote, fluxo ou borda (dependendo da entrada da jornada) |
| Escopo de dados do perfil | Perfil de hub completo | Perfil do Edge (subconjunto) | Perfil de hub completo |
| Complexo | Baixa | Medium-Alto | Médio |
| Taxa de transferência | Alto (volumes de campanha em lote) | Alta (escala Edge Network) | Medium (limites de taxa de transferência de jornada aplicáveis) |

### Escolha a opção certa

Use as orientações a seguir para selecionar a melhor opção de implementação para seu caso de uso.

- **Escolha a Opção A** se o caso de uso principal for selecionar a melhor oferta por destinatário em campanhas de email de saída e se não houver SDK do lado do cliente disponível. Esse é o caminho de implementação mais simples e funciona bem para emails promocionais, boletins informativos e campanhas do ciclo de vida.
- **Escolha a Opção B** se as ofertas tiverem de ser selecionadas em tempo real no momento em que um visitante carregar uma página da Web ou abrir um aplicativo móvel. Isso requer o Web SDK ou Mobile SDK e uma política de mesclagem ativa de borda, mas fornece a seleção de oferta mais rápida e contextual.
- **Escolha a Opção C** se a decisão de oferta fizer parte de uma jornada mais ampla do cliente com várias etapas, esperas e ramificação condicional. Essa é a escolha correta quando a oferta selecionada deve influenciar as ações de jornada downstream ou quando o acompanhamento de vários canais com base no envolvimento da oferta é necessário.
- **Combine opções** quando as ofertas tiverem de ser entregues de forma consistente entre canais. Use a mesma política de decisão em todas as três opções para garantir que um cliente veja a mesma oferta no email (Opção A), no site (Opção B) e em um acompanhamento de jornada (Opção C).

## Fases de implementação

As fases a seguir descrevem a sequência completa de implementação do Offer Decisioning.

### Fase 1: Validar pré-requisitos essenciais

**Função do aplicativo:** AEP: Modelagem e preparação de dados, AEP: Configuração de identidade e perfil

Essa fase valida se a camada de dados fundamentais oferece suporte ao Offer Decisioning. Os esquemas de perfil devem incluir os atributos usados nas regras de elegibilidade da oferta e a configuração de identidade deve permitir a resolução de perfis entre canais.

#### Decisão: atributos de perfil para qualificação

Determine quais atributos de perfil serão usados nas regras de qualificação de oferta.

>[!NOTE]
>A escolha de atributos de perfil afeta o design da regra de elegibilidade e a eficácia da estratégia de classificação. Considere os atributos calculados e as pontuações de propensão para melhorar a qualidade da decisão.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Atributos de perfil padrão (nível de fidelidade, histórico de compras) | Os atributos já existem no esquema de perfil | Nenhuma alteração necessária no esquema; verifique a atualização dos dados |
| Atributos computados (valor vitalício, pontuação de engajamento) | A elegibilidade ou classificação depende dos dados comportamentais agregados | Requer configuração S1; adiciona uma dependência na cadência de atualização de atributo computada |
| Pontuações de propensão do Customer AI | A classificação deve aproveitar as previsões baseadas em aprendizado de máquina | Requer dados de treinamento suficientes (mais de 10.000 perfis com evento de direcionamento); tempo de treinamento do modelo |

#### Principais detalhes de configuração

- Verificar se o esquema de perfil inclui campos referenciados nas regras de qualificação (por exemplo, `_tenantId.loyaltyTier`, `_tenantId.subscriptionType`)
- Confirmar se o esquema de rastreamento de interação de oferta existe para eventos de impressão, clique e conversão
- Para Opção B: verifique se a política de mesclagem de borda ativa está configurada e se a sequência de dados do Web SDK tem o serviço AJO habilitado

#### Documentação do Experience League

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Habilitar um esquema para o perfil](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/union-schema)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### Fase 2: configurar a avaliação do público

**Função do aplicativo:** RT-CDP: Avaliação de Público-Alvo

Essa fase define e avalia os públicos-alvo usados como critérios de qualificação de oferta. Esses públicos-alvo determinam quais segmentos de clientes se qualificam para ofertas específicas (por exemplo, &quot;clientes de alto valor&quot; se qualificam para ofertas premium, &quot;usuários de avaliação&quot; se qualificam para ofertas de conversão).

#### Decisão: método de avaliação do público-alvo

Determine com que rapidez a associação de público-alvo deve ser atualizada para que a oferta seja qualificada.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Avaliação em lote | Opção A (campanhas de email) em que a elegibilidade é avaliada no momento do envio | Mais simples; todas as expressões de regra de segmento são compatíveis; atualização diária ou sob demanda |
| Avaliação de transmissão | Opção A ou C quando atualizações de público-alvo em tempo quase real forem necessárias entre lotes | Automático para segmentos elegíveis; suporte limitado a regras de segmento (eventos únicos, comparações de atributos) |
| Avaliação da borda | Opção B (Web/aplicativo em tempo real), em que a elegibilidade deve ser avaliada no carregamento da página | Subsegundo; necessário para ofertas da Web/aplicativos em tempo real; limitado a verificações de atributos simples e associação de segmentos |

**Navegação da interface do usuário:** Cliente > Públicos-alvo > Criar público-alvo > Criar regra

#### Principais detalhes de configuração

- Definir públicos-alvo de direcionamento para a qualificação da oferta (por exemplo, &quot;Nível Ouro de Fidelidade&quot;, &quot;Clientes de Alto Valor&quot;, &quot;Usuários de Avaliação&quot;)
- Defina públicos de supressão se necessário (por exemplo, &quot;Oferta recentemente recebida X&quot;)
- Para a opção B: verifique se os públicos-alvo de qualificação se qualificam para avaliação de borda — evite consultas de série de tempo e agregações complexas em expressões de regra de segmento

#### Onde as opções divergem

**Para A Opção A (Decisão De Email):**
A avaliação em lote ou por transmissão é suficiente. Os públicos são avaliados antes ou durante a execução da campanha. Expressões de regras de segmentos complexos, incluindo condições baseadas em tempo e agregações de eventos, são totalmente compatíveis.

**Para a Opção B (Tempo Real da Web/Aplicativo):**
É necessária a avaliação do Edge. Os públicos-alvo devem usar verificações de atributo simples ou condições de associação de segmento. Teste a elegibilidade da borda verificando se a expressão de regra de segmento se qualifica para segmentação de borda.

**Para Opção C (Nó de Decisão de Jornada):**
Qualquer método de avaliação funciona dependendo dos critérios de entrada da jornada. Se a jornada usar uma entrada baseada no público-alvo, o método de avaliação do público-alvo corresponderá aos requisitos da jornada.

#### Documentação do Experience League

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentação de transmissão](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentação de borda](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### Fase 3: Configurar decisões

**Função do aplicativo:** AJO: decisão

Essa é a fase principal na qual o catálogo de ofertas, as regras de qualificação, as estratégias de classificação e as políticas de decisão são criados. Essa fase cria a configuração do mecanismo de decisão que todas as opções de entrega (A, B, C) compartilham.

#### Decisão: canal de posicionamento e formato do conteúdo

Determine onde as ofertas serão exibidas e em que formato.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Email (HTML) | Opção A — oferecer conteúdo renderizado como HTML no corpo do email | Suporta formatação avançada; deve ser compatível com clientes de email |
| Email (URL da imagem) | Opção A — oferta renderizada como uma imagem hospedada no email | Mais simples; a imagem deve ser hospedada e acessível; sem texto dinâmico |
| Web (HTML) | Opção B — oferta renderizada como HTML em uma página da Web | Controle de layout completo; suporta elementos interativos |
| Web/Mobile (JSON) | Opção B — dados de oferta retornados como JSON para renderização personalizada | Máxima flexibilidade; requer desenvolvimento de front-end para renderização |
| Baseado em código (JSON) | Opção B — oferecer dados para superfícies de experiência baseadas em código | O aplicativo controla a renderização; mais flexível |

#### Decisão: estratégia de classificação

Determine como a melhor oferta deve ser selecionada dentre as ofertas qualificadas.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Baseado em prioridade (manual) | Catálogos de ofertas pequenos; regras comerciais explícitas para a solicitação de ofertas | Mais simples de configurar; atribuir manualmente o valor de prioridade por oferta; determinístico |
| Baseado em fórmula (expressão personalizada) | A classificação deve considerar os atributos do perfil (por exemplo, nível de fidelidade, recenticidade) | Flexível; usa dados de perfil para calcular uma pontuação de classificação; requer design de expressão de regra de segmento |
| Classificado por IA (otimização automática) | Catálogos de ofertas grandes; deseja que o ML otimize a seleção ao longo do tempo | Exige no mínimo 1.000 eventos de conversão para treinamento de modelo; aprende com os dados de desempenho da oferta |

#### Decisão: Limite de oferta

Determine se deve haver limites na quantidade de vezes que uma oferta é exibida.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Limite por perfil | Evite que a mesma oferta seja exibida muitas vezes para um cliente | Evita a fadiga da oferta; retardo do contador de alguns segundos em cenários de alta taxa de transferência |
| Limite global | Limitar o total de impressões para uma oferta em todos os perfis (por exemplo, inventário limitado) | Controla o suprimento da oferta; uma vez atingido o limite, a oferta é excluída das decisões |
| Sem limite | As ofertas têm disponibilidade ilimitada | Mais simples; adequado para promoções sempre ativas |

**Navegação da interface do usuário:** Componentes > Gerenciamento de decisão > Posicionamentos / Regras / Ofertas / Decisões

#### Principais detalhes de configuração

1. **Criar posicionamentos** — Defina onde as ofertas aparecem especificando o tipo de canal e o formato de conteúdo para cada posicionamento.
   - Interface do usuário: Componentes > Gerenciamento de decisão > Posicionamentos
   - Criar uma inserção por combinação de canal/formato (por exemplo, &quot;Banner de exemplo de email - HTML&quot;, &quot;Página inicial da Web - JSON&quot;, &quot;Cartão de aplicativo móvel - JSON&quot;)

2. **Definir regras de qualificação** — Crie regras usando expressões de regra de segmento que façam referência a atributos de perfil ou associação de público-alvo.
   - Interface do usuário: Componentes > Gerenciamento de decisão > Regras
   - As regras podem fazer referência a associação de público-alvo, atributos de perfil (nível de fidelidade, tipo de assinatura), restrições de data ou dados contextuais

3. **Criar ofertas personalizadas** — Crie cada oferta com representações de conteúdo para cada posicionamento, atribua regras de elegibilidade, defina prioridades e configure limites opcionais.
   - Interface do usuário: Componentes > Gerenciamento de decisão > Ofertas > Criar oferta
   - Cada oferta precisa de uma representação de conteúdo por disposição (por exemplo, HTML para email, JSON para Web)
   - Atribuir regras de elegibilidade para controlar quais perfis podem ver cada oferta
   - Definir datas de validade da oferta (início/fim) e limite de frequência opcional
   - Aprove cada oferta para torná-la qualificada para decisão

4. **Criar ofertas substitutas** — Crie uma oferta padrão para cada posicionamento que é exibido quando nenhuma oferta personalizada é qualificada.
   - Interface do usuário: Componentes > Gerenciamento de decisão > Ofertas > Criar oferta substituta
   - O fallback deve ter representações para cada posicionamento usado na decisão

5. **Criar qualificadores e coleções** — Organize ofertas em coleções usando marcas de qualificador.
   - IU: Componentes > Gerenciamento de decisão > Qualificadores de coleção
   - Ofertas relacionadas ao grupo (por exemplo, &quot;Promoções de Verão&quot;, &quot;Recompensas de fidelidade&quot;) para uso em escopos de decisão

6. **Criar políticas de decisão** — Associe posicionamentos, coleções, estratégias de classificação e ofertas de fallback em decisões executáveis.
   - Interface do usuário: Componentes > Gerenciamento de decisão > Decisões > Criar decisão
   - Cada escopo de decisão vincula um posicionamento a uma coleção e especifica o método de classificação

#### Documentação do Experience League

- [Visão geral da Gestão de decisões](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Criar inserções](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Criar regras de decisão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crie ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Criar ofertas substitutas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Criar coleções](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Criar qualificadores de coleção](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [Criar decisões](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estratégias de classificação](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Fase 4: configurar canal e superfície

**Função do aplicativo:** AJO: configuração de canal

Essa fase configura as superfícies de canal por meio das quais as ofertas serão entregues. A configuração depende de quais opções de implementação estão sendo usadas.

#### Decisão: tipo de canal

Determine qual canal de mensagens é necessário para o caso de uso.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Email | Opção A ou Opção C com delivery de email | Requer delegação de subdomínio, pool de IP e configurações do remetente |
| Web | Opção B para entrega em superfície da web | Requer Web SDK e configuração de sequência de dados |
| No aplicativo | Opção B para entrega de aplicativos móveis | Exige o Mobile SDK e credenciais de push |
| Experiência baseada em código | Opção B para superfícies de renderização personalizadas | Mais flexível; o aplicativo lida com a renderização |

#### Onde as opções divergem

**Para A Opção A (Decisão De Email):**
- Interface do usuário: Administração > Canais > Superfícies de canal > Criar superfície (Email)
- Configurar subdomínio, pool de IP, nome/email do remetente, responder para, cancelar inscrição
- Verificar registros SPF, DKIM e DMARC do subdomínio de envio

**Para a Opção B (Tempo Real da Web/Aplicativo):**
- Interface do usuário: Administração > Canais > Superfícies de canal > Criar superfície (na Web ou no aplicativo)
- Para a Web: configurar o padrão de URL da superfície da Web
- Para experiências baseadas em código: defina o URI da superfície para o aplicativo
- Verifique se a sequência de dados tem o serviço AJO habilitado

**Para Opção C (Nó de Decisão de Jornada):**
- Configure as superfícies dos canais para cada canal usado na jornada (email, push, SMS ou Web)
- Cada ação de mensagem de jornada requer uma superfície de canal ativa correspondente

#### Documentação do Experience League

- [Introdução à configuração de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Configurações de superfície de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Delegar subdomínios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Configurar canal de notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Fase 5: configurar o conteúdo e o delivery

**Função de aplicativo:** AJO: Criação de Mensagens, AJO: Execução de Campanha

Essa fase projeta os modelos de mensagem ou as superfícies de experiência que exibem a oferta selecionada e configura o mecanismo de entrega (campanha, jornada ou experiência baseada em código).

#### Decisão: abordagem de conteúdo para renderização de oferta

Determine como o conteúdo da oferta deve ser integrado à mensagem ou experiência.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Componente do Offer Decision no Email Designer | Opção A — incorporar posicionamento de oferta no modelo de email | Arrastar e soltar; o conteúdo da oferta é renderizado automaticamente com base no resultado da decisão |
| Experiência baseada em código com política de decisão | Opção B — o aplicativo recupera e renderiza dados de oferta | Controle máximo da renderização; requer desenvolvimento de front-end |
| Jornada ação de mensagem com decisão incorporada | Opção C — os feeds de nó de decisão oferecem conteúdo à mensagem do jornada | A seleção e a entrega de ofertas são orquestradas no fluxo de jornada |

#### Decisão: tipo de campanha (opção A somente)

Determine se é uma campanha de marketing agendada ou uma campanha acionada por API.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Campanha programada | Envios em lote únicos ou recorrentes para um público-alvo definido | Público avaliado no tempo de execução; defina a data/hora ou a recorrência |
| Campanha acionada por API | Envios orientados por eventos ou acionados pelo sistema para perfis especificados | Perfis especificados na carga do acionador; suporta até 20 destinatários por solicitação |

#### Onde as opções divergem

**Para A Opção A (Decisão De Email):**

1. Crie a mensagem de email usando o Designer de email
   - Interface do usuário: Campanhas > Criar campanha > Selecionar email > Editar conteúdo
   - Insira um componente de decisão de oferta no layout de email para definir a zona de posicionamento
   - Adicionar tokens de personalização para conteúdo no nível do perfil (nome, nível de fidelidade)
   - Configurar linha de assunto e pré-cabeçalho com personalização opcional
2. Criar e configurar a campanha
   - Interface do usuário: Campanhas > Criar campanha > Programado ou acionado por API
   - Vincular o público-alvo e selecionar a superfície de canal
   - Definir o agendamento de execução ou a configuração do acionador de API
   - Revisar e ativar a campanha

**Para a Opção B (Tempo Real da Web/Aplicativo):**

1. Configurar a experiência baseada em código para o canal da Web
   - Interface do usuário: Campanhas > Criar campanha > Experiência baseada em código (ou Web)
   - Vincular a política de decisão à superfície de experiência
   - Definir o formato de renderização (resposta JSON para baseado em código; editor visual para canal da Web)
2. Implementar renderização no lado do cliente
   - Use a resposta `sendEvent` do Web SDK para recuperar a oferta selecionada
   - Renderizar o conteúdo da oferta no posicionamento designado na página
   - Implementar o rastreamento de impressões e cliques

**Para Opção C (Nó de Decisão de Jornada):**

1. Projetar a jornada com um nó de decisão
   - Interface do usuário: Jornada > Criar Jornada > Adicionar nó de decisão
   - Configurar o nó de decisão para chamar a política de decisão da Fase 3
2. Adicionar nós de ação de mensagem após a decisão
   - Configurar ações de email, push ou SMS que façam referência à oferta selecionada
   - Adicionar etapas de espera, condições ou ramificação com base no envolvimento de oferta
3. Publicar a jornada

#### Documentação do Experience League

- [Entregar ofertas em mensagens](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Criar conteúdo de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Criar uma campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Introdução ao jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Visualizar e testar o conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### Fase 6: testar e validar

**Função do aplicativo:** AJO: Decisioning, AJO: Criação de Mensagens

Essa fase valida se o mecanismo de decisão retorna as ofertas corretas para perfis de teste e se o conteúdo da oferta é renderizado corretamente em cada canal de delivery.

#### Testar lógica de decisão

Use perfis de teste com atributos conhecidos para verificar se as ofertas corretas estão selecionadas com base na qualificação e na classificação.

- Criar perfis de teste que correspondam a diferentes critérios de qualificação (por exemplo, nível Gold, nível Silver, usuário de avaliação)
- Verifique se cada perfil de teste recebe a oferta esperada
- Verificar se os perfis que não correspondem a regras de qualificação recebem a oferta substituta

#### Testar renderização de conteúdo

Pré-visualize o conteúdo da oferta em cada canal de delivery.

- Para a Opção A: use a pré-visualização de email com perfis de teste para verificar se o conteúdo da oferta é renderizado corretamente
- Para a Opção B: testar a resposta do Edge Decisioning em um ambiente de preparo
- Para a Opção C: use o modo de teste do jornada para verificar se o nó de decisão seleciona corretamente

#### Validar rastreamento de impressões

Confirme se as impressões, os cliques e as conversões da oferta estão sendo rastreados.

- Verifique se os eventos de interação de oferta aparecem nos conjuntos de dados de rastreamento
- Confirmar atribuição entre impressões de oferta e conversões downstream

#### Documentação do Experience League

- [Visualizar e testar o conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [Enviar provas de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/proofs)

### Fase 7: configurar a emissão de relatórios e o monitoramento de desempenho

**Função do aplicativo:** AJO: Relatórios e análise de desempenho

Essa fase configura relatórios para rastrear a distribuição da seleção de ofertas, as taxas de aceitação, o impacto da conversão e as taxas de fallback. Essa fase abrange os relatórios nativos do AJO e a análise entre canais com base no CJA.

#### Decisão: método de relatório

Determine quais ferramentas de relatório são necessárias para a análise de desempenho da oferta.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Somente relatórios nativos do AJO | Monitoramento operacional de campanhas ou jornadas individuais | Acesso rápido, métricas integradas de entrega e envolvimento, análise limitada entre entidades |
| Análise de espaço de trabalho do CJA | Eficácia da oferta entre canais, atribuição de receita, análise da funnel | Requer conexão e visualização de dados do CJA; recursos analíticos mais profundos |
| AJO e CJA | Cobertura operacional e analítica completa | Recomendado para implementações de produção; AJO para monitoramento em tempo real, CJA para análise estratégica |

#### Principais detalhes de configuração

1. **Relatórios nativos do AJO** — Monitore o desempenho da campanha ou do jornada usando relatórios internos.
   - Interface do usuário: Campanhas > Selecionar campanha > Relatório de todos os tempos (ou Relatório ao vivo)
   - Revisar métricas específicas da oferta: impressões por oferta, taxa de cliques por oferta, taxa de fallback
   - Monitorar funnel de delivery: Direcionado > Enviado > Entregue > Aberturas > Cliques

2. **Análise do CJA (recomendado)** — Crie painéis de desempenho de ofertas entre canais.
   - Configurar uma conexão do CJA, incluindo conjuntos de dados de interação de oferta do AJO
   - Crie uma visualização de dados com dimensões específicas de oferta (nome da oferta, posicionamento, decisão) e métricas (impressões, cliques, conversões)
   - Criar análise de espaço de trabalho para: distribuição de seleção de oferta, taxa de aceitação por segmento, impacto na receita, consistência da oferta entre canais

#### Documentação do Experience League

- [Relatório global da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Jornada relatório global](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabalhar com o Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Visão geral do Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

## Considerações de implantação

Esta seção aborda medidas de proteção, armadilhas comuns, práticas recomendadas e decisões de compensação para implementações do Offer Decisioning.

### Medidas de proteção e limites

Esteja ciente das seguintes medidas de proteção e limites da plataforma ao planejar sua implementação.

- Máximo de 10.000 ofertas personalizadas aprovadas por sandbox — [Medidas de proteção do Gerenciamento de decisão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Máximo de 30 posicionamentos por decisão
- Máximo de 30 escopos de coleção por solicitação de decisão
- Os modelos de classificação de IA exigem um mínimo de 1.000 eventos de conversão para treinamento
- Os contadores de limite de oferta podem ter um atraso de até alguns segundos em cenários de alta taxa de transferência
- As decisões do Edge são limitadas aos atributos de perfil disponíveis na loja de perfis de borda
- Máximo de 4.000 definições de segmento por sandbox — [Medidas de proteção da plataforma](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Somente uma política de mesclagem pode estar ativa no Edge por sandbox
- Máximo de 500 campanhas ativas por sandbox
- Limite da taxa de entrada de jornada: 5.000 perfis por segundo
- Máximo de 10 superfícies de canal por tipo de canal por sandbox

### Armadilhas comuns

Evite esses problemas encontrados com frequência durante a implementação.

- **A Decision sempre retorna oferta substituta:** Isso normalmente significa que as ofertas personalizadas não são aprovadas, estão fora do intervalo de datas de validade ou as regras de qualificação não correspondem aos atributos do perfil de teste. Verifique cada condição: status de aprovação, intervalo de datas e precisão da expressão de regra de segmento. Verifique também se os limites de limite não foram atingidos.
- **Oferta que não aparece na coleção:** verifique se a oferta foi marcada com o qualificador de coleção correto e se o filtro de coleção corresponde. As ofertas devem ser marcadas e aprovadas para serem exibidas em escopos de decisão baseados em coleção.
- **Fórmula de classificação não aplicada:** verifique se a fórmula é sintaticamente válida e faz referência a atributos de perfil acessíveis. Os erros de fórmula retornam silenciosamente à classificação baseada em prioridade sem erros visíveis.
- **A entrega do Edge retorna uma personalização vazia:** Verifique se a sequência de dados está configurada com o serviço [!DNL Adobe Journey Optimizer] habilitado e se o escopo de decisão está formatado corretamente. Verifique se a política de mesclagem de borda ativa existe.
- **Ofertas inconsistentes entre canais:** Se forem usadas políticas de decisão separadas por canal, o mesmo perfil poderá receber ofertas diferentes. Use uma única política de decisão entre canais para manter a consistência ou aceite uma divergência intencional com base em disposições específicas do canal.
- **Conteúdo da oferta não renderizado no email:** Verifique se a oferta tem uma representação de conteúdo que corresponda ao formato de posicionamento do email (HTML ou URL da imagem). Representações ausentes resultam em zonas de posicionamento em branco.

### Práticas recomendadas

Siga estas recomendações para uma implementação bem-sucedida do Offer Decisioning.

- **Comece com um pequeno catálogo de ofertas e repita** — comece com 5-10 ofertas e expanda conforme a estrutura de decisão é validada. Isso simplifica a solução de problemas e garante que as regras de qualificação funcionem corretamente antes do dimensionamento.
- **Usar qualificadores de coleção estrategicamente** — Marque ofertas por categoria (por exemplo, &quot;Aquisição&quot;, &quot;Retenção&quot;, &quot;Venda adicional&quot;) para habilitar escopos de decisão baseados em coleção flexíveis que possam ser reutilizados em campanhas e jornadas.
- **Sempre criar ofertas substitutas significativas** — As ofertas substitutas não são apenas uma rede de segurança; elas são a experiência padrão para perfis que não correspondem a nenhuma regra de qualificação. Invista em conteúdo de fallback que forneça valor mesmo sem personalização.
- **Crie regras de qualificação para serem mutuamente exclusivas, quando possível** — Quando várias ofertas têm qualificação de sobreposição, a estratégia de classificação se torna crítica. Se os requisitos de negócios ditarem uma oferta específica para um segmento específico, torne as regras de elegibilidade mutuamente exclusivas, em vez de depender apenas da classificação.
- **Testar com perfis de representante de borda para a Opção B** — os perfis do Edge contêm um subconjunto de atributos de perfil de hub. Teste com perfis que tenham atributos de borda disponíveis para garantir que a qualificação seja avaliada corretamente na produção.
- **Monitorar taxas de fallback como uma métrica de integridade** — Uma alta taxa de fallback (acima de 20-30%) indica que o catálogo de ofertas não cobre segmentos de clientes suficientes. Expanda o catálogo de ofertas ou amplie as regras de elegibilidade.
- **Políticas de decisão de versão em vez de editar as ativas** — crie uma nova versão de política de decisão em vez de modificar uma ativa. Isso evita a interrupção das campanhas ativas e permite a comparação A/B das estratégias de decisão.

### Decisões de compensação

Considere as seguintes compensações ao tomar decisões de arquitetura e configuração.

#### Precisão de elegibilidade vs. cobertura da oferta

Regras de elegibilidade rígidas garantem que cada oferta atinja apenas os perfis mais relevantes, mas podem resultar em altas taxas de fallback quando os perfis não corresponderem a nenhuma oferta. Regras amplas de elegibilidade maximizam a cobertura da oferta, mas reduzem a precisão da personalização.

- **A qualificação rígida favorece:** taxas de aceitação mais altas, melhor personalização, menor fadiga da oferta
- **A ampla qualificação favorece:** taxas de fallback mais baixas, mais perfis recebem ofertas personalizadas e um gerenciamento de regras mais simples
- **Recomendação:** comece com regras de qualificação mais amplas e aperte-as com base em dados de desempenho. Monitore taxas de fallback e taxas de aceitação para encontrar o saldo correto. Use estratégias de classificação para diferenciar entre ofertas amplamente qualificadas.

#### Classificação com base em prioridade versus classificação por IA

A classificação com base em prioridade oferece à empresa controle total sobre quais ofertas são exibidas, enquanto a classificação com IA otimiza a conversão, mas reduz o controle humano sobre a seleção da oferta.

- **Prioridades baseadas em:** Controle de negócios, previsibilidade, sem necessidade de dados de treinamento, implantação imediata
- **Favoritos classificados por IA:** Otimização de conversão, descoberta de padrões inesperados, adaptação automática para alterar o comportamento do cliente
- **Recomendação:** use classificação baseada em prioridade para inicializações iniciais e ofertas com restrição regulamentar nas quais o controle empresarial é fundamental. Transição para classificados por IA para casos de uso de alto volume e com desempenho otimizado assim que dados de conversão suficientes (mais de 1.000 eventos) estiverem disponíveis.

#### Política de decisão única versus políticas de decisão por canal

Uma única política de decisão garante a consistência da oferta em todos os canais, mas restringe a otimização por canal. As políticas por canal permitem classificação e qualificação específicas por canal, mas arriscam experiências inconsistentes do cliente.

- **Uma única política favorece:** consistência entre canais, gerenciamento mais simples, relatórios unificados
- **As políticas por canal favorecem:** Classificação otimizada por canal, qualificação específica por canal (por exemplo, ofertas somente da Web), iteração independente
- **Recomendação:** comece com uma única política de decisão para consistência entre canais. Crie políticas por canal somente quando as necessidades dos negócios exigirem estratégias de oferta específicas de canal (por exemplo, vendas rápidas exclusivas para a Web).

#### Decisão do hub (opção A/C) vs. decisão da borda (opção B)

A decisão do hub tem acesso ao perfil completo, mas opera no momento do envio. O Edge decisioning opera em tempo real com latência de subsegundos, mas é limitado aos atributos de perfil de borda disponíveis.

- **A decisão do hub favorece:** acesso a dados completos do perfil, regras complexas de qualificação, volumes de campanha em lote
- **A decisão do Edge favorece:** Contexto em tempo real, personalização na sessão, resposta em subsegundos
- **Recomendação:** use a decisão do hub para canais de saída (email, push) em que os dados completos do perfil melhorem a relevância da oferta. Use o Edge Decisioning para canais de entrada (Web, aplicativo) em que a resposta em tempo real é crítica. Garantir regras de qualificação para atributos disponíveis de borda somente para uso de borda.

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
- [Introdução ao jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

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
