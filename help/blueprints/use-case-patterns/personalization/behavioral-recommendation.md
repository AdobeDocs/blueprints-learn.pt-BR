---
title: Recomendação comportamental
description: Saiba como gerar recomendações de item e conteúdo usando estratégias de seleção e modelos de classificação.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: db16e773-e0da-46c4-9fa5-d16f04feb46b
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '7545'
ht-degree: 2%

---

# Recomendação comportamental

Este guia aborda como implementar recomendações comportamentais de produto e conteúdo usando a Decisão [!DNL Adobe Journey Optimizer] (AJO), [!DNL Real-Time Customer Data Platform] (RT-CDP) e [!DNL Adobe Experience Platform] (AEP). Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam fornecer experiências de recomendação personalizadas em canais da Web, de aplicativos móveis e de email.

Ele apresenta todas as opções de implementação viáveis, considerações de decisão em cada fase e links para a documentação do [!DNL Adobe Experience League]. A Recomendação comportamental gera recomendações no nível do item ou do conteúdo usando sinais comportamentais — exibições do produto, compras, interações de conteúdo, consultas de pesquisa — combinados com estratégias de seleção e modelos de classificação do AJO Decisioning. Ao contrário do Offer Decisioning, que rege um conjunto limitado de ofertas, promoções ou incentivos usando regras de elegibilidade e restrições comerciais, esse padrão opera em catálogos de itens grandes e em constante alteração (produtos, artigos, vídeos), em que a seleção é orientada por sinais de afinidade comportamental em vez de elegibilidade regida.

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

## Padrão do caso de uso

**Recomendação comportamental**

Gerar recomendações no nível do item ou do conteúdo com base em sinais comportamentais, usando estratégias de seleção e modelos de classificação do AJO Decisioning para veicular conteúdo contextual.

**Cadeia de funções:** Assimilação de sinal comportamental > Avaliação de estratégia de decisão > Entrega de recomendação > Relatórios

Consulte a seção Composição do padrão em Considerações sobre implementação para obter orientação sobre a combinação de padrões.

## Aplicativos

Os aplicativos a seguir são usados neste padrão de caso de uso.

- **[!DNL Adobe Journey Optimizer] (AJO) Decisão** — Estratégias de seleção, modelos de classificação, catálogos de itens e políticas de decisão que avaliam sinais comportamentais e retornam os itens mais relevantes para cada visitante
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** — Acúmulo de dados de perfil comportamental, avaliação de público-alvo para escopo de recomendação e atributos computados para pontuação de afinidade comportamental
- **[!DNL Adobe Experience Platform] (AEP)** — Assimilação comportamental de evento via [!DNL Web SDK] e [!DNL Mobile SDK], processamento de [!DNL Edge Network], gerenciamento de esquema XDM para dados de evento e catálogo

## Funções básicas

Os seguintes recursos básicos devem estar em vigor para esse padrão de caso de uso. Para cada função, o status indica se ele é tipicamente necessário, se presume ser pré-configurado ou se não é aplicável.

| Função de base | Status | O que deve estar em vigor | Referência do Experience League |
| --- | --- | --- | --- |
| Administração e governança | Presumido em vigor | sandbox da AJO com permissões de decisão ativadas. As funções de usuário foram provisionadas com acesso ao gerenciamento de catálogo de itens, configuração de estratégia de seleção e administração de superfície de canal. | [Visão geral das sandboxes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/home), [Visão geral do controle de acesso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Preparação e modelagem de dados | Obrigatório | Esquema de evento de experiência que captura sinais comportamentais (exibições de produtos, suplementos ao carrinho, compras, interações de conteúdo) com identificadores de item/produto. Esquema de catálogo de itens (atributos de produto, categorias, imagens, preços) para o conjunto de itens de recomendação. Esquema de perfil com campos de identidade. Todos os esquemas habilitados para [!DNL Real-Time Customer Profile]. | [Visão geral do Sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [Noções básicas sobre a composição de esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition), [Criar um conjunto de dados](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/create) |
| Fontes de dados e coleção | Obrigatório | A transmissão de eventos comportamentais em tempo real via [!DNL Web SDK] ou [!DNL Mobile SDK] é crítica — a qualidade da recomendação depende de novos sinais comportamentais. Os dados do catálogo de itens devem ser assimilados (em lote ou por transmissão). Sequências de dados configuradas com o serviço AJO habilitado para o Edge Decisioning. | [Visão geral do Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home), [Visão geral do Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview), [Configurar sequências de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure) |
| Configuração de identidade e perfil | Obrigatório | Os sinais comportamentais devem ser associados a uma identidade (conhecida ou anônima por meio da ECID) para criar perfis comportamentais. Para recomendações de visitantes conhecidos, a identidade autenticada (ID de CRM, email) deve ser configurada. Política de mesclagem ativa no Edge para entrega de recomendações em tempo real. | [Visão geral do Serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| Definição e segmentação do público-alvo | Recomendado | Os públicos-alvo podem ser usados para definir o escopo das recomendações (por exemplo, recomendar apenas produtos premium para membros premium) ou para filtragem. Não é estritamente necessário se as recomendações forem puramente comportamentais. Obrigatório para recomendações baseadas em email (Opção C) para definir o público-alvo. | [Visão geral do Serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder) |

## Funções de suporte

Os recursos a seguir aumentam esse padrão de caso de uso, mas não são necessários para a execução principal.

| Função de suporte | Status | Por que é importante | Referência do Experience League |
| --- | --- | --- | --- |
| Criação de atributo calculado/derivado | Recomendado | Atributos calculados, como pontuações de afinidade de categoria, frequência de interação de produto, recenticidade de compra e gasto total, melhoram a qualidade da classificação da recomendação. [!DNL Customer AI] as pontuações de propensão podem aumentar ainda mais a relevância ao prever a probabilidade de compra. | [Visão geral dos atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview), [Visão geral da IA do cliente](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview) |
| Gerenciamento do ciclo de vida dos dados | Recomendado | Os dados de eventos comportamentais devem ter políticas de expiração apropriadas — a relevância da recomendação é degradada com dados obsoletos. Definir políticas de expiração do conjunto de dados em conjuntos de dados de eventos comportamentais garante a atualização e gerencia o armazenamento. A aplicação do consentimento garante o uso compatível de dados comportamentais. | [Expirações do conjunto de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration), [Visão geral do Gerenciamento avançado do ciclo de vida dos dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| Rotulagem e aplicação de uso de dados | Recomendado | Os rótulos de governança em dados comportamentais garantem o uso compatível do histórico de interação para recomendações. Particularmente importante quando os dados comportamentais incluem padrões de navegação, histórico de compras ou sinais de interesse de produtos financeiros/de saúde. | [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [Visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview) |
| Monitoramento e capacidade de observação | Recomendado | A latência de entrega de recomendação, as taxas de fallback e a integridade da assimilação do catálogo de itens devem ser monitoradas. Alertas sobre falhas de assimilação de eventos comportamentais e erros de decisão ajudam a manter a qualidade da recomendação. | [Visão geral dos Insights de Observabilidade](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home), [Visão geral dos alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview) |
| Relatórios e análise | Incluído | O relatório de desempenho de recomendação faz parte da Etapa 4 da Cadeia de Funções. [!DNL Customer Journey Analytics] a análise da eficácia da recomendação, do impacto na receita e do desempenho no nível do item em superfícies e segmentos fornece insights de otimização. | [visão geral do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [visão geral do Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home) |

## Funções do aplicativo

Este plano exerce as seguintes funções do Catálogo de Funções da Aplicação. As funções são mapeadas para fases de implementação em vez de etapas numeradas.

### [!DNL Journey Optimizer] (AJO)

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Decisão. | Configuração da Estratégia de Seleção e Catálogo de Itens | Configurar catálogos de itens (itens de decisão), estratégias de seleção com modelos de classificação comportamental, regras de filtragem e recomendações de fallback |
| Configuração de canais | Configuração de canal e superfície | Configurar superfícies de entrega para canais da Web (experiências baseadas em código), no aplicativo, de cartão de conteúdo ou de email, nos quais as recomendações serão renderizadas |
| Criação de mensagens | Configuração de conteúdo e entrega | Criar modelos de renderização de recomendação, layouts de exibição de item e expressões de personalização para itens recomendados |
| Relatórios e análise de desempenho | Relatórios e otimização | Monitore métricas de click-through, conversão e receita de recomendação por meio de relatórios nativos do AJO e integração com o [!DNL Customer Journey Analytics] |

### [!DNL Real-Time CDP] (RT-CDP)

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Avaliação de público | Escopo Do Público-Alvo (Opção C) | Avaliar os segmentos de público-alvo usados para determinar o escopo das recomendações ou definir o público-alvo para campanhas de recomendação por email |
| Enriquecimento de perfil | Enriquecimento de sinal comportamental | Enriqueça os perfis com atributos computados (pontuações de afinidade de categoria, frequência de interação) que melhoram a classificação da recomendação |

## Pré-requisitos

Conclua o seguinte antes de iniciar a implementação:

- [ O AJO Decisioning ] foi provisionado e habilitado na sandbox de destino
- [ ] [!DNL Web SDK] ou [!DNL Mobile SDK] está implantado e está coletando eventos comportamentais com identificadores de produto/conteúdo
- [ ] Os dados do catálogo de produtos ou conteúdo estão disponíveis para assimilação (nome do produto, categoria, preço, URL da imagem, disponibilidade)
- [ ] Esquemas de evento comportamental incluem identificadores de item/produto que se vinculam a itens de catálogo
- [ A sequência de dados ] está configurada com o serviço [!DNL Adobe Journey Optimizer] habilitado (necessário para a tomada de decisão do Edge)
- [ A política de mesclagem ] com `isActiveOnEdge: true` está configurada (necessária para recomendações da Web/aplicativo em tempo real)
- [ ] Para recomendações de email (Opção C): a superfície de canal de email está configurada e validada
- [ ] Para recomendações de email (Opção C): o público-alvo é definido e avaliado

## Opções de implementação

As opções a seguir descrevem diferentes abordagens para a implementação de recomendações comportamentais. Escolha a opção que melhor se adapta aos requisitos de canal e restrições técnicas.

### Opção A: recomendações em tempo real da Web

**Recomendado para:** Recomendações de produto ou conteúdo em páginas da Web — widgets de venda cruzada da página de detalhes do produto, carrosséis de recomendações da página inicial, listagens personalizadas da página de categoria e personalização do resultado da pesquisa.

**Como funciona:**

Os sinais comportamentais são coletados em tempo real via [!DNL Web SDK] enquanto os visitantes navegam pelo site. Cada exibição de página, interação de produto ou consulta de pesquisa é transmitida para a AEP e associada ao perfil do visitante (por meio da ECID para visitantes anônimos ou da identidade autenticada para visitantes conhecidos). Quando uma página contendo uma superfície de recomendação é carregada, o [!DNL Web SDK] solicita uma avaliação de decisão do AJO por meio do [!DNL Edge Network]. O mecanismo de decisão avalia o perfil comportamental do visitante em relação à estratégia de seleção, aplica lógica de classificação, filtra itens inelegíveis (já comprados, indisponíveis) e retorna os itens recomendados.

As recomendações são renderizadas na página por meio de experiências baseadas em código ou superfícies de canal da Web. A renderização pode ser um carrossel, grade, widget de item único ou qualquer layout personalizado definido no modelo de recomendação. Os eventos de impressão e clique são rastreados automaticamente no AEP para relatórios de desempenho.

**Principais considerações:**

- A decisão do Edge exige que a política de mesclagem esteja ativa no Edge
- A latência de recomendação depende do tempo de resposta de [!DNL Edge Network] (SLA abaixo de 500 ms para solicitações de escopo único)
- Os visitantes anônimos recebem recomendações com base no comportamento na sessão; os visitantes conhecidos se beneficiam do histórico comportamental entre sessões
- Visitantes de início frio sem histórico comportamental recebem recomendações de fallback

**Vantagens:**

- Personalização em tempo real com base no comportamento na sessão
- Entrega de recomendação de subsegundos via [!DNL Edge Network]
- Funciona para visitantes anônimos e conhecidos
- Impressão automática e rastreamento de cliques
- Não é necessário recarregar a página para novas recomendações

**Limitações:**

- A loja de perfis do Edge contém um subconjunto de atributos de perfil completos
- Modelos de classificação complexos com muitos atributos de perfil podem exigir avaliação no lado do hub
- Requer a implantação do [!DNL Web SDK] com monitoramento de eventos comportamentais

**Experience League:**

- [Fornecer ofertas usando a API do Edge Decisioning](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [Visão geral do Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)

### Opção B: recomendações para aplicativos móveis

**Recomendado para:** recomendações de produtos no aplicativo, feeds de conteúdo personalizados, recomendações orientadas por notificação e experiências de comércio móvel.

**Como funciona:**

Os sinais comportamentais são coletados por meio do [!DNL Mobile SDK] conforme os usuários interagem com o aplicativo. Exibições de produtos, interações de conteúdo, pesquisas e compras são transmitidas para o AEP. Quando uma tela contendo uma superfície de recomendação é carregada, o [!DNL Mobile SDK] solicita uma avaliação de decisão. As recomendações são entregues por meio de mensagens no aplicativo, cartões de conteúdo ou experiências baseadas em código no aplicativo móvel.

Os cartões de conteúdo são especialmente adequados para casos de uso de recomendação em aplicativos móveis, pois persistem em uma experiência semelhante a um feed que os usuários podem navegar conforme sua conveniência. As mensagens no aplicativo podem ser usadas para recomendações contextuais acionadas por comportamentos específicos (por exemplo, mostrar produtos complementares depois de adicionar um item ao carrinho).

**Principais considerações:**

- [!DNL Mobile SDK] deve ser configurado com o rastreamento de evento comportamental para interações relevantes
- Os cartões de conteúdo fornecem uma superfície de recomendação persistente; as mensagens no aplicativo são efêmeras
- O rastreamento de comportamento offline requer o gerenciamento de fila do SDK para o envio de evento adiado
- Os ciclos de atualização da App Store afetam a rapidez com que as alterações de renderização de recomendação podem ser implantadas

**Vantagens:**

- Experiência móvel nativa com renderização de recomendação simples e integrada ao aplicativo
- Os cartões de conteúdo fornecem um feed de recomendação persistente e navegável
- As mensagens no aplicativo ativam recomendações contextuais acionadas por comportamento
- Aproveita os sinais no nível do dispositivo (localização, padrões de uso do aplicativo) para maior relevância

**Limitações:**

- Requer integração do [!DNL Mobile SDK] e recursos de desenvolvimento de aplicativos
- As alterações de renderização exigem atualizações do aplicativo (a menos que você use experiências baseadas em código com layouts orientados por servidor)
- Períodos offline criam lacunas na coleção de sinal comportamental

**Experience League:**

- [Visão geral do Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Configurar canal de notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Opção C: Recomendações comportamentais de email

**Recomendado para:** recomendações de produto em campanhas de email — emails de navegação abandonados com recomendações de produto visualizadas, emails de venda cruzada pós-compra, resumos periódicos de &quot;escolhas para você&quot; e emails de reengajamento com sugestões personalizadas de produto.

**Como funciona:**

Os dados de perfil comportamental acumulados de sessões anteriores informam a seleção de recomendação no momento do envio do email ou no momento da renderização. Um público-alvo é definido para direcionar os recipients apropriados (por exemplo, visitantes que navegaram, mas não compraram, clientes que fizeram uma compra recente). Uma campanha ou jornada é configurada para enviar um email que inclui disposições de recomendação. No momento do envio, o AJO Decisioning avalia o perfil comportamental de cada recipient em relação à estratégia de seleção e injeta os itens recomendados no conteúdo de email.

Essa opção depende do histórico comportamental acumulado em vez de sinais na sessão. Os atributos computados (pontuações de afinidade de categoria, exibições de produto recentes, frequência de compra) melhoram significativamente a qualidade da recomendação para email, pois transformam o histórico comportamental em sinais no nível do perfil que a estratégia de seleção pode avaliar com eficiência.

**Principais considerações:**

- As recomendações de email são avaliadas no momento do envio, não no momento da abertura — o estado do perfil comportamental no momento do envio determina as recomendações
- Atributos computados são altamente recomendados para melhorar a qualidade da classificação
- Limitações de renderização de email (sem JavaScript, CSS limitado): restringir formatos de exibição de recomendação
- Requer uma superfície de canal de email configurada e validada

**Vantagens:**

- Aproveita o histórico comportamental completo nas sessões para uma personalização mais profunda
- Integra-se aos workflows existentes do jornada e da campanha
- Eficaz para cenários de reengajamento e reconquista em que os pontos de contato da Web/aplicativo não estão disponíveis
- Pode incluir vários posicionamentos de recomendações em um único email

**Limitações:**

- As recomendações são estáticas no momento do envio — elas não são atualizadas quando o email é aberto
- Formatos de exibição de recomendação de limite de restrições de renderização de email
- Requer avaliação de público-alvo e infraestrutura de orquestração de campanha/jornada
- Maior complexidade de implementação devido a dependências adicionais (configuração de canal, definição de público, execução de campanha)

**Experience League:**

- [Criar um email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [Entregar ofertas em mensagens](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### Comparação de opções

A tabela a seguir resume as principais diferenças entre as opções de implementação.

| Critérios | Opção A: Tempo real da Web | Opção B: aplicativo móvel | Opção C: Comportamento do email |
| --- | --- | --- | --- |
| Melhor para | Recomendações da página da Web (PDP, página inicial, categoria) | Recomendações no aplicativo e feeds de conteúdo | Campanhas de email com recomendações de produto |
| Fonte de sinal comportamental | Na sessão + entre sessões ([!DNL Web SDK]) | Interações no aplicativo ([!DNL Mobile SDK]) | Histórico comportamental acumulado (perfil) |
| Latência de recomendação | Subsegundo ([!DNL Edge Network]) | Subsegundo ([!DNL Edge Network]) | No momento do envio (avaliação no lado do hub) |
| Tipo de visitante | Anônimo e conhecido | Conhecido (usuários do aplicativo) | Conhecido (destinatários de email) |
| Complexo | Médio | Medium-Alto | Alta |
| Dependência de canal | [!DNL Web SDK], superfície de experiência baseada em código | [!DNL Mobile SDK], no aplicativo/superfície de cartão de conteúdo | Superfície de canal de email, público-alvo, campanha/jornada |
| Exige | [!DNL Web SDK] implantação, política de mesclagem do Edge | [!DNL Mobile SDK] implantação, política de mesclagem do Edge | Superfície de email, definição de público, configuração da campanha |

### Escolha a opção certa

Use as orientações a seguir para selecionar a melhor opção para sua situação:

- **Comece com a Opção A** se sua meta principal for as recomendações de produto em tempo real em seu site. Esse é o ponto de partida mais comum e fornece valor imediato com a menor complexidade de implementação.
- **Escolha a Opção B** se o seu aplicativo móvel for um canal de envolvimento principal e se as recomendações no aplicativo resultarem em um aumento de conversão significativo. A opção B pode ser executada em paralelo com a opção A usando as mesmas estratégias de seleção e catálogos de itens.
- **Adicione a Opção C** quando quiser estender recomendações comportamentais em campanhas de email. Normalmente, isso é dividido em camadas sobre a Opção A ou B, usando os mesmos catálogos de itens e estratégias de seleção, mas com modelos de renderização específicos por email e direcionamento baseado no público-alvo.
- **Combine as Opções A + C** para obter um padrão comum: recomendações da Web em tempo real para visitantes ativos, além de recomendações de email de navegação ou pós-compra abandonadas para visitantes que saem sem conversão.

## Fases de implementação

As fases a seguir orientam você pela implementação completa de recomendações comportamentais.

### Fase 1: configurar o esquema de evento comportamental e a coleta de dados

**Função do Aplicativo:** AEP: Modelagem e Preparação de Dados (F2), AEP: Fontes de Dados e Coleção (F3)

Essa fase estabelece os esquemas XDM, conjuntos de dados e mecanismos de coleta de dados que capturam sinais comportamentais e dados de catálogo de itens. Essa base de dados é do que toda a lógica de recomendação depende.

#### Decisão: design de esquema de evento comportamental

Quais sinais comportamentais devem orientar as recomendações?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Somente exibições de produto | Recomendações simples de venda cruzada/venda adicional | Menor esforço de implementação; profundidade limitada do sinal |
| Exibições de produto + compras | Recomendações com exclusão de compra e lógica de venda cruzada | Esforço moderado; permite a filtragem &quot;excluir os já adquiridos&quot; |
| Conjunto comportamental completo (exibições, compras, suplemento ao carrinho, pesquisas, interações de conteúdo) | Recomendações sofisticadas com classificação de vários sinais | Maior qualidade de sinal; requer instrumentação [!DNL Web SDK]/[!DNL Mobile SDK] abrangente |

#### Decisão: método de assimilação do catálogo de itens

Como o produto ou catálogo de conteúdo será assimilado na AEP?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Assimilação em lote pelo conector de origem | As atualizações do catálogo são periódicas (diariamente/semanalmente) | Configuração mais simples; as alterações no catálogo não são refletidas em tempo real |
| Assimilação por transmissão | O catálogo requer atualizações quase em tempo real (alterações de preço, disponibilidade) | Mais complexo; garante que as recomendações reflitam o inventário atual |
| Upload manual/API | Pequeno catálogo com alterações pouco frequentes | Configuração mais simples; não dimensionável para catálogos grandes ou dinâmicos |

Navegação da **UI:** Gerenciamento de Dados > Esquemas > Criar esquema; Coleção de Dados > Fluxos de Dados > Nova Sequência de Dados

**Detalhes de configuração da chave:**

- O esquema do Evento de experiência deve incluir identificadores de produto/item (SKU, ID de produto, ID de conteúdo) na carga do evento
- O esquema do catálogo de itens deve incluir atributos usados para filtragem e classificação: categoria, preço, URL da imagem, status de disponibilidade, tags
- A sequência de dados deve ter o serviço [!DNL Adobe Journey Optimizer] habilitado para a tomada de decisão do Edge
- As chamadas de [!DNL Web SDK] `sendEvent` devem incluir dados de interação do produto mapeados para campos de comércio XDM

**Documentação do Experience League:**

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Noções básicas de composição de esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [Visão geral do Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Configurar sequências de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Definir uma relação entre dois esquemas](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/relationship-api)

### Fase 2: configurar identidade e perfil

**Função do Aplicativo:** AEP: Configuração de Identidade e Perfil (F4)

Essa fase configura namespaces de identidade, designações de identidade primárias e políticas de mesclagem que garantem que os sinais comportamentais sejam associados corretamente aos perfis do visitante e disponibilizados para a entrega de recomendações em tempo real.

#### Decisão: política de mesclagem para decisões do Edge

O caso de uso de recomendação requer uma avaliação do Edge em tempo real?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Ativo na política de mesclagem do Edge | Opções A e B (recomendações da Web e em tempo real para dispositivos móveis) | Necessário para entrega de recomendação em subsegundos; somente uma política de mesclagem do Edge por sandbox |
| Política de mesclagem padrão (não no Edge) | Opção C apenas (recomendações de email avaliadas no momento do envio) | Suficiente para avaliação no lado do hub; não consome o slot da política de mesclagem do Edge |

#### Decisão: identidade de visitante anônima vs. conhecida

Como os sinais comportamentais de visitantes anônimos devem ser tratados?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Somente ECID (anônimo) | Recomendações principalmente para visitantes anônimos com base no comportamento na sessão | Configuração mais simples; não há continuidade entre sessões, a menos que o visitante faça a autenticação |
| ECID + identidade autenticada (ID de CRM, email) | Recomendações entre sessões para visitantes conhecidos com compilação de identidade | Perfis comportamentais mais avançados; requer fluxo de autenticação |
| Ambos com vinculação de gráfico de identidade | Jornada completa de anônimo para conhecido com identificação de identidade | Mais abrangente; requer configuração de regras de vinculação de identidade |

**Navegação da interface do usuário:** Identidades > Namespaces de identidade; Perfis > Políticas de mesclagem

**Detalhes de configuração da chave:**

- O namespace da ECID é pré-configurado e usado automaticamente por [!DNL Web SDK] e [!DNL Mobile SDK]
- Os namespaces de identidade personalizados (ID de CRM, ID de fidelidade) devem ser criados para a identidade autenticada
- A identidade principal no esquema de Evento de experiência deve ser ECID para eventos comportamentais da Web/móveis
- A política de mesclagem deve usar o Gráfico de dispositivos privados para a compilação de identidade entre dispositivos

**Documentação do Experience League:**

- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Visão geral dos namespaces de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/namespaces)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [Regras de vinculação do gráfico de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)

### Fase 3: Configurar catálogo de itens e estratégia de seleção

**Função do Aplicativo:** AJO: Decisão

Essa fase configura o catálogo de itens (itens de decisão), as estratégias de seleção que combinam sinais comportamentais com atributos de item para classificação, as regras de filtragem para excluir itens inelegíveis e as recomendações de fallback para perfis de início frio.

#### Decisão: escopo do catálogo de itens

Quais itens estão disponíveis para recomendação?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Catálogo de produtos (comércio eletrônico) | Recomendando produtos físicos ou digitais para compra | Os atributos do item incluem preço, categoria, disponibilidade, imagens |
| Catálogo de conteúdo (mídia/publicação) | Recomendando artigos, vídeos ou conteúdo educacional | Os atributos de item incluem tópico, autor, data de publicação, tipo de conteúdo |
| Catálogo híbrido | Recomendando produtos e conteúdo | Requer esquema de item unificado que acomode ambos os tipos |

#### Decisão: Abordagem de classificação

Como os itens elegíveis devem ser classificados para determinar as melhores recomendações?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Classificação baseada em fórmula | Lógica comercial clara para classificação (por exemplo, classificar por pontuação de afinidade de categoria multiplicada pela popularidade do item) | Classificação transparente e auditável; requer fórmula de classificação definida |
| Classificado por IA (otimização automática) | O aprendizado de máquina deve determinar a classificação ideal com base nos dados de conversão | Requer no mínimo 1.000 eventos de conversão para treinamento de modelos; menos transparente |
| Baseado em prioridade (manual) | Ordem de recomendação simples e com curadoria manual | É mais fácil de configurar; não se adapta ao comportamento individual |

#### Decisão: regras de filtragem

Quais itens devem ser excluídos das recomendações?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Excluir itens já comprados | Recomendações para venda cruzada e detecção | Requer histórico de compras no perfil comportamental |
| Excluir itens esgotados | Comércio eletrônico com inventário dinâmico | Requer atualizações de catálogo em tempo real ou quase em tempo real |
| Excluir itens descartados anteriormente | Recomendações de conteúdo nas quais os usuários podem descartar sugestões | Requer rastreamento de demissão em eventos comportamentais |
| Filtragem com escopo de categoria | Recomendações limitadas a categorias específicas | Usa atributos de item para filtragem |

#### Decisão: estratégia de arranque a frio

O que deve ser mostrado para novos visitantes sem histórico comportamental?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Itens populares (best-sellers globais) | Fallback de uso geral | Simples de manter; não personalizado |
| Itens populares específicos da categoria | O visitante chegou em uma página de categoria | Fallback contextualmente relevante; requer contexto de página |
| Escolhas editoriais com curadoria | Marca quer controle editorial sobre a experiência de partida a frio | Requer preparação e atualizações manuais |
| Itens em tendência (popularidade ponderada por tempo) | Fallback dinâmico que reflete as tendências atuais | Requer computação de sinal de tendência |

**Navegação da interface do usuário:** [!DNL Journey Optimizer] > Componentes > Gerenciamento de decisão > Decisões; [!DNL Journey Optimizer] > Componentes > Gerenciamento de decisão > Ofertas; [!DNL Journey Optimizer] > Componentes > Gerenciamento de decisão > Posicionamentos

**Detalhes de configuração da chave:**

- Crie itens de decisão que representem cada produto ou item de conteúdo no catálogo, com atributos (categoria, preço, URL da imagem, tags)
- Definir estratégias de seleção que combinam a filtragem do catálogo de itens com a lógica de classificação comportamental
- Configurar modelos de classificação — expressões baseadas em fórmulas podem fazer referência a atributos de perfil (por exemplo, pontuações de afinidade de categoria de atributos calculados)
- Criar ofertas/itens de fallback que servem como recomendações padrão para perfis de inicialização imediata
- Organizar itens em coleções usando qualificadores de coleção (tags) para agrupamento lógico
- Configurar regras de filtragem nas estratégias de seleção para aplicar regras de negócios (excluir comprados, somente em estoque)

**Documentação do Experience League:**

- [Visão geral da Gestão de decisões](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Criar inserções](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Criar regras de decisão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crie ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Criar ofertas substitutas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Criar coleções](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Criar decisões](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estratégias de classificação](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Fase 4: configurar canal e superfície

**Função do Aplicativo:** AJO: Configuração de Canal

Essa fase configura as superfícies de entrega onde as recomendações serão renderizadas. A configuração varia significativamente de acordo com a opção de implementação.

#### Decisão: tipo de superfície de entrega

Onde as recomendações serão exibidas?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Experiência baseada em código (Web) | Widget de recomendação em páginas da Web com renderização personalizada | Flexibilidade máxima para renderização; requer desenvolvimento de front-end |
| Superfície de canal da Web | Superfície de personalização da Web padrão | Usa o AJO Web Designer; menos flexível que o baseado em código |
| Mensagem no aplicativo | Recomendações contextuais acionadas pelo comportamento do aplicativo | Efêmero; desaparece após interação ou demissão |
| Cartão de conteúdo (dispositivos móveis) | Feed de recomendação persistente no aplicativo móvel | Persiste até que o usuário aja; experiência de feed navegável |
| Email | Recomendações de produto incorporadas às campanhas de email | Estático no momento do envio; sujeito a restrições de renderização de email |

**Onde as opções divergem:**

**Para a Opção A (Recomendações em Tempo Real da Web):**
Configure uma superfície de experiência baseada em código ou uma superfície de canal da Web. Experiências baseadas em código fornecem mais flexibilidade para a renderização de recomendação personalizada (carrosséis, grades, cartões de item). O URI de superfície identifica onde as recomendações da página são exibidas.

**Para a Opção B (Recomendações para Aplicativos Móveis):**
Configurar superfícies de cartão de conteúdo ou mensagens no aplicativo. Os cartões de conteúdo são recomendados para feeds de recomendação persistentes. As mensagens no aplicativo funcionam bem para recomendações contextuais acionadas por comportamento.

**Para Opção C (Recomendações Comportamentais De Email):**
Configure uma superfície de canal de email com delegação de subdomínio, atribuição de pool de IP e configurações do remetente. Verifique se a superfície está validada para entrega.

**Navegação da interface do usuário:** Administração > Canais > Superfícies de canal > Criar superfície

**Documentação do Experience League:**

- [Configurar superfícies do canal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Introdução à configuração de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Configurar canal de SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configurar canal de notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Fase 5: configurar o conteúdo e o delivery

**Função do Aplicativo:** AJO: Criação de Mensagens

Essa fase define os modelos de renderização de recomendação que controlam como os itens recomendados são exibidos para o visitante. Isso inclui o design do layout do item, expressões de personalização que extraem atributos de item (nome, imagem, preço, link) e o design da experiência de recomendação geral.

#### Decisão: formato de exibição de recomendação

Como os itens recomendados devem ser renderizados?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Carrossel (rolagem horizontal) | Página inicial ou página de categoria com espaço vertical limitado | Padrão de UX familiar; mostra vários itens em espaço compacto |
| Grade (várias linhas) | Seção de recomendação dedicada com amplo espaço | Mostra mais itens de uma só vez; funciona bem para as seções &quot;recomendado para você&quot; |
| Widget de item único | Recomendação contextual em um local de página específico (por exemplo, barra lateral) | Espaço mínimo, posicionamento de alto impacto |
| Bloqueio de email embutido | Recomendações incorporadas ao corpo do email | Sujeito a restrições de HTML/CSS por email; normalmente de 2 a 4 itens |

#### Decisão: Número de recomendações a serem exibidas

Quantos itens a decisão deve retornar por posicionamento?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| 3-4 itens | Widget de recomendação padrão | Equilibra relevância com densidade visual |
| 6-8 itens | Carrossel com rolagem ou layout de grade | Mais opções para o visitante; requer profundidade suficiente do catálogo |
| 1 item | Recomendação contextual de produto único | Impacto de maior relevância; renderização mais simples |
| Mais de 10 itens | Experiência de recomendação no estilo de feed | Casos de uso de grande volume de conteúdo (mídia, publicação) |

**Onde as opções divergem:**

**Para a Opção A (Recomendações em Tempo Real da Web):**
Projete a renderização da recomendação usando modelos de experiência baseados em código. Use HTML/CSS/JavaScript para criar o layout do carrossel, grade ou widget. As expressões Personalization fazem referência aos atributos de resposta de decisão (nome do item, URL da imagem, preço, URL do produto). O rastreamento de impressões e cliques é feito automaticamente pelo [!DNL Web SDK].

**Para a Opção B (Recomendações para Aplicativos Móveis):**
Configure modelos de cartão de conteúdo ou de mensagem no aplicativo com lógica de exibição de item. Use estruturas de conteúdo baseadas em JSON que o aplicativo móvel renderiza nativamente. Inclua deep links para cada item recomendado.

**Para Opção C (Recomendações Comportamentais De Email):**
Crie conteúdo de email usando o Designer de email. Insira disposições de recomendação usando blocos de conteúdo com poder de decisão. Configure expressões de personalização para atributos de item no modelo de email. A personalização da linha de assunto pode fazer referência aos principais itens recomendados.

**Navegação da interface do usuário:** Gerenciamento de conteúdo > Modelos de conteúdo; Campanha/Jornada > Editar conteúdo > Email Designer

**Detalhes de configuração da chave:**

- Cada posicionamento de recomendação deve fazer referência à decisão criada na Fase 3
- As expressões Personalization usam a sintaxe Handlebars para renderizar atributos de item
- Para Web: configure a experiência baseada em código para chamar a decisão e renderizar a resposta
- Para email: incorpore a decisão na ação de email na campanha ou na jornada
- Visualizar recomendações usando perfis de teste com histórico comportamental conhecido

**Documentação do Experience League:**

- [Criar conteúdo de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxe do Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Entregar ofertas em mensagens](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Visualizar e testar o conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [Trabalhar com modelos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)

### Fase 6: configurar o escopo de público-alvo e a campanha/jornada (somente a opção C)

**Função do Aplicativo:** RT-CDP: Avaliação de Público-Alvo, AJO: Execução de Campanha ou Journey Orchestration

Para recomendações baseadas em email (Opção C), essa fase define o público-alvo e configura a campanha ou jornada que entrega o email de recomendação. As opções A e B ignoram essa fase porque as recomendações são entregues em tempo real no carregamento de página/tela.

#### Decisão: método de avaliação do público-alvo

Como o público-alvo dos emails de recomendação deve ser avaliado?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Avaliação em lote | Campanhas de email de recomendação programadas (resumo diário e semanal) | Tempo de envio previsível; público avaliado antes do envio |
| Avaliação de transmissão | Emails de recomendação acionados por evento (navegação abandonada, pós-compra) | Qualificação de público-alvo em tempo quase real; pares com a orquestração de jornadas |

#### Decisão: mecanismo de entrega

O email deve ser entregue por meio de uma campanha ou jornada?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Campanha programada | Explosões de email de recomendação únicas ou recorrentes para um público-alvo definido | Configuração mais simples, avaliação de público em lote e envio |
| Jornada com entrada de público | Emails de recomendação contínuos acionados pela qualificação de público-alvo | Habilita fluxos de várias etapas (por exemplo, email de recomendação seguido de lembrete) |
| Jornada acionada por evento | Email de recomendação acionado por um evento específico (abandono de navegação, compra) | Acionamento em tempo real; exige entrada de jornada baseada em eventos |

**Navegação da interface do usuário:** Cliente > Públicos > Criar público > Criar regra; Campanhas > Criar campanha; Jornadas > Criar jornada

**Detalhes de configuração da chave:**

- Defina o público-alvo usando expressões de regra de segmento que fazem referência ao histórico comportamental (por exemplo, &quot;produtos visualizados nos últimos 7 dias, mas não comprados&quot;)
- Configure a campanha ou jornada com a ação de email que faz referência à superfície de canal na Fase 4
- Incorporar a decisão da Fase 3 ao conteúdo do email
- Definir regras de programação e frequência para evitar mensagens excessivas

**Documentação do Experience League:**

- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentação de transmissão](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Relatório em tempo real da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)

### Fase 7: configurar relatórios e otimização

**Função do Aplicativo:** AJO: Reporting &amp; Performance Analysis, S5: Reporting &amp; Analysis

Essa fase estabelece o monitoramento do desempenho para métricas de click-through, conversão e receita da recomendação. Ele cria a infraestrutura de relatórios para medir a eficácia da recomendação e identificar oportunidades de otimização.

#### Decisão: profundidade dos relatórios

Qual nível de análise de relatórios é necessário?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Somente relatórios nativos do AJO | Monitoramento básico de desempenho de recomendação | Configuração rápida; limitado a métricas rastreadas pela AJO |
| Integração AJO + [!DNL Customer Journey Analytics] | Análise de impacto da recomendação entre canais e atribuição de receita | Requer conexão [!DNL Customer Journey Analytics] e visualização de dados; fornece insights mais profundos |
| Espaço de trabalho [!DNL Customer Journey Analytics] completo com painéis personalizados | Programa de otimização contínuo com análise de nível de item, nível de segmento e nível de superfície | Mais abrangente; requer experiência e configuração do [!DNL Customer Journey Analytics] |

**Navegação da interface do usuário:** Campanhas > Selecionar campanha > Relatório de todos os tempos; Jornadas > Selecionar jornada > Relatório de todos os tempos; [!DNL Customer Journey Analytics] > Projetos > Criar novo projeto

**Detalhes de configuração da chave:**

- Revisar relatórios de campanha e jornada do AJO para métricas de entrega e envolvimento
- Para integração com o [!DNL Customer Journey Analytics], crie uma conexão que inclua conjuntos de dados de evento de experiência do AJO (Feedback de mensagem, Rastreamento de email, Decisão)
- Crie uma visualização de dados do [!DNL Customer Journey Analytics] com dimensões específicas da recomendação (nome do item, categoria do item, superfície de recomendação) e métricas (impressões, cliques, conversões, receita)
- Criar métricas calculadas para a recomendação CTR, taxa de conversão e receita por impressão
- Criar painéis do espaço de trabalho do [!DNL Customer Journey Analytics] comparando o desempenho da recomendação entre superfícies, segmentos e períodos

**Documentação do Experience League:**

- [Relatório global da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Jornada relatório global](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabalhar com o Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Criar ou editar uma conexão](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [Criar ou editar uma visualização de dados](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Visão geral do Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Visão geral das métricas calculadas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)

## Considerações de implantação

Analise as seguintes medidas de proteção, armadilhas, práticas recomendadas e compensações antes e durante a implementação.

### Medidas de proteção e limites

- Máximo de 10.000 ofertas personalizadas aprovadas (itens de decisão) por sandbox — [Medidas de proteção do Gerenciamento de decisão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Máximo de 30 posicionamentos por decisão
- Máximo de 30 escopos de coleção por solicitação de decisão
- Tempo de resposta do Offer Delivery SLA: menos de 500 ms na P95 para solicitações Edge de escopo único
- Os modelos de classificação de IA exigem um mínimo de 1.000 eventos de conversão para treinamento
- Os contadores de limite de oferta podem ter um atraso de até alguns segundos em cenários de alta taxa de transferência
- As decisões do Edge são limitadas aos atributos de perfil disponíveis na loja de perfis de borda
- Somente uma política de mesclagem pode estar ativa no Edge por sandbox — [Medidas de proteção do perfil](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Máximo de 25 atributos computados ativos por sandbox — [Medidas de proteção de atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- Máximo de 4.000 definições de segmento por sandbox — [Medidas de proteção de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Assimilação de transmissão: máximo de 20.000 registros por segundo por conexão HTTP — [Medidas de proteção de assimilação](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)

### Armadilhas comuns

- **A decisão retorna somente itens de fallback:** verifique se os itens de decisão personalizados estão aprovados, dentro de seu intervalo de datas de validade, e se as regras de qualificação correspondem aos atributos de perfil do visitante. Verifique se os limites de limite não foram atingidos.
- A entrega do **Edge retorna uma personalização vazia:** verifique se a sequência de dados está configurada com o serviço [!DNL Adobe Journey Optimizer] habilitado e se o escopo de decisão está formatado corretamente na solicitação [!DNL Web SDK].
- **Fórmula de classificação não aplicada:** verifique se a fórmula é sintaticamente válida e faz referência a atributos de perfil acessíveis. Os erros de fórmula retornam silenciosamente à classificação baseada em prioridade.
- **Recomendações antigas:** se os dados de eventos comportamentais não estiverem fluindo em tempo real, as recomendações serão baseadas em perfis comportamentais desatualizados. Verifique se [!DNL Web SDK] ou [!DNL Mobile SDK] está transmitindo eventos ativamente.
- **A taxa de fallback de inicialização a frio é muito alta:** se uma grande porcentagem de visitantes receber recomendações de fallback, considere enriquecer a estratégia de inicialização a frio com sinais contextuais (categoria de página atual, fonte de referência) em vez de depender exclusivamente do histórico comportamental.
- **Recomendações que não são renderizadas na página:** Verifique se o URI da superfície de experiência baseada em código corresponde ao padrão de URL da página e se [!DNL Web SDK] está solicitando e renderizando corretamente a resposta de decisão.
- **Itens de catálogo ausentes das recomendações:** verifique se todos os itens de catálogo foram assimilados como itens de decisão, marcados com os qualificadores de coleção corretos e incluídos nas coleções apropriadas referenciadas pela estratégia de seleção.

### Práticas recomendadas

- Comece com um modelo de classificação baseado em fórmulas usando atributos computados (afinidade de categoria, recenticidade de interação) antes de investir em modelos classificados por IA. Os modelos baseados em fórmulas são transparentes, auditáveis e fornecem uma linha de base sólida para comparação.
- Implemente o rastreamento de impressões e cliques desde o primeiro dia. Sem dados de interação, os modelos de classificação de IA não podem ser treinados e você não pode medir a eficácia da recomendação.
- Crie estratégias de seleção separadas para diferentes superfícies de recomendação (página inicial, PDP, email) em vez de reutilizar uma única estratégia em todos os lugares. Superfícies diferentes atendem a intenções de usuários diferentes.
- Use atributos computados para converter o histórico comportamental em sinais de classificação. Os dados brutos do evento são muito granulares para uma classificação baseada em fórmulas eficiente; sinais agregados como &quot;pontuação de afinidade de categoria&quot; e &quot;dias desde a última compra&quot; são mais eficazes.
- Teste recomendações de fallback separadamente das recomendações personalizadas. Verifique se os itens de fallback são padrões de alta qualidade e apropriados para a marca, que fornecem uma boa experiência para os novos visitantes.
- Monitore a taxa de fallback de inicialização a frio como uma métrica principal de integridade. Uma taxa de fallback decrescente ao longo do tempo indica uma crescente cobertura comportamental.
- Para recomendações de email, o agendamento envia nos momentos em que o perfil comportamental é mais completo (por exemplo, após as horas de pico de navegação, não durante elas).

### Decisões de compensação

As seguintes compensações devem ser avaliadas com base em seus requisitos específicos.

#### Sinais em tempo real vs. histórico acumulado

Os sinais comportamentais na sessão fornecem relevância imediata, mas profundidade limitada. A história comportamental acumulada fornece profundidade, mas pode ser obsoleta. O equilíbrio entre essas fontes afeta a qualidade da recomendação.

- **A opção A favorece:** sinais em tempo real para relevância imediata, complementados por histórico acumulado para visitantes conhecidos
- **A Opção C favorece:** Histórico acumulado exclusivamente, já que os emails são enviados de forma assíncrona
- **Recomendação:** para Web e dispositivos móveis (Opções A, B), combine sinais na sessão com atributos computados derivados de comportamento histórico. Para email (Opção C), invista muito em atributos computados que resumem o histórico comportamental em sinais de nível de perfil acionáveis.

#### Modelos com base em fórmulas versus modelos classificados por IA

A classificação baseada em fórmula é transparente e imediata. Os modelos classificados por IA se adaptam automaticamente, mas exigem dados de treinamento e oferecem menos visibilidade nas decisões de classificação.

- **Favoritos baseados em fórmula:** Transparência, auditoria, implantação imediata e controle corporativo refinado sobre a lógica de classificação
- **Favoritos classificados por IA:** otimização automatizada, descoberta de padrões não óbvios e esforço de ajuste manual reduzido
- **Recomendação:** comece com uma classificação baseada em fórmula para estabelecer uma linha de base de desempenho e acumular dados de conversão. Faça a transição para modelos classificados por IA depois de ter dados de treinamento suficientes (mais de 1.000 eventos de conversão) e quiser otimizar além do que o ajuste manual de fórmulas pode alcançar.

#### Cobertura da recomendação versus relevância

Ampliar o catálogo de itens e relaxar as regras de filtragem aumenta a porcentagem de solicitações que recebem recomendações personalizadas, mas pode reduzir a relevância por recomendação.

- **A alta cobertura favorece:** Maximizar o número de visitantes que veem recomendações personalizadas; útil quando a meta principal é o engajamento
- **A alta relevância favorece:** Mostrar apenas itens altamente relevantes, mesmo que isso signifique que mais visitantes vejam recomendações de fallback; útil quando a meta principal é a conversão
- **Recomendação:** comece com uma filtragem moderada (excluir itens comprados, itens indisponíveis) e monitore a taxa de fallback e a taxa de conversão. Restrinja as regras de filtragem somente se os dados de conversão permitirem.

#### Profundidade do Personalization versus complexidade de implementação

Sinais comportamentais mais avançados e modelos de classificação mais sofisticados melhoram a qualidade das recomendações, mas aumentam a complexidade da implementação e a carga de manutenção.

- **A implementação mais simples favorece:** tempo de implantação mais rápido, manutenção mais baixa, depuração e iteração mais fáceis
- **A personalização mais profunda favorece:** maior aumento de conversão, melhor experiência para o cliente, diferencial competitivo
- **Recomendação:** Implementar em fases. Comece com sinais de visualização de produto e classificação baseada em fórmula (Fase 1). Adicionar atributos computados para enriquecimento comportamental (Fase 2). Avaliar os modelos classificados por IA quando a fundação estiver madura e os dados de treinamento suficientes estiverem disponíveis (Fase 3).

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

- [Visão geral das fontes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Visão geral das tags](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)
- [Grupo de campos Consentimento e preferências](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
