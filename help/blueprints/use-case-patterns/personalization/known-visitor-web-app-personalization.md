---
title: Personalization de aplicativo/Web de visitante conhecido
description: Saiba como fornecer conteúdo, ofertas ou promoções personalizadas para visitantes identificados com base no perfil em tempo real e na associação do segmento.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 585adc0e-f528-4a09-b931-ef6b45fa8ec8
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '7968'
ht-degree: 2%

---

# Personalização da Web/aplicativo de visitante conhecido

Este plano de referência fornece um guia completo de implementação para fornecer conteúdo personalizado a visitantes identificados em superfícies digitais usando o [!DNL Adobe Journey Optimizer] (AJO) e o [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP). Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam entender todas as abordagens de implementação viáveis, as decisões que devem ser tomadas em cada fase e a documentação do Experience League que oferece suporte à configuração.

A personalização da Web/aplicativo de visitante conhecido é o principal padrão de personalização para experiências digitais autenticadas. Diferentemente da personalização de visitante anônimo, que depende exclusivamente de sinais comportamentais na sessão, esse padrão aproveita o perfil unificado completo: dados comportamentais históricos, associação de segmento, nível de fidelidade, histórico de compras, estágio de ciclo de vida, atributos computados e pontuações de propensão. Ele oferece suporte à personalização em páginas da Web (por meio do canal da Web AJO), mensagens móveis no aplicativo e cartões de conteúdo.

Este guia apresenta todas as opções de implementação viáveis — com base em segmentos, em decisões e em várias superfícies — com compensações, orientação de decisão e referências à documentação do [!DNL Adobe Experience League].

## Visão geral do caso de uso

Organizações com propriedades digitais autenticadas — sites de comércio eletrônico, portais bancários, serviços de assinatura, programas de fidelidade, aplicativos móveis — precisam fornecer experiências personalizadas que reflitam o relacionamento de cada cliente com a marca. Quando um visitante faz logon ou é reconhecido por meio da resolução de identidade, a plataforma pode acessar seu perfil totalmente unificado e fornecer conteúdo adaptado a seus atributos, comportamentos e preferências específicos.

Esse padrão aborda o cenário em que um visitante identificado chega em uma propriedade da Web ou abre um aplicativo móvel, e o sistema deve determinar o conteúdo, a oferta ou a promoção ideais para exibição com base nos dados do perfil em tempo real e na associação do público-alvo. A decisão de personalização ocorre na borda em milissegundos, permitindo a entrega de conteúdo em subsegundos sem latência perceptível.

O padrão é compatível com a personalização determinística (em que o conteúdo específico mapeia para segmentos específicos de público-alvo) e com a decisão dinâmica (em que o AJO Decisioning avalia as regras de elegibilidade e as estratégias de classificação para selecionar o conteúdo ideal por perfil). Ele abrange várias superfícies digitais — páginas da Web, mensagens móveis no aplicativo e cartões de conteúdo — permitindo uma personalização consistente na jornada digital do cliente.

## Principais objetivos de negócios

Os seguintes objetivos de negócios são compatíveis com esse padrão de caso de uso.

### Fornecer experiências personalizadas ao cliente

Personalize conteúdo, ofertas e mensagens para preferências individuais, comportamentos e estágios do ciclo de vida. Para obter mais informações, consulte [Fornecer experiências personalizadas ao cliente](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md).

**KPIs:** Compromisso, Taxas de Conversão, Satisfação do Cliente (CSAT)

### Aumentar o engajamento do site

Melhore o tempo no site, as páginas por sessão e a interação com o conteúdo da Web por meio de experiências relevantes. Para obter mais informações, consulte [Aumentar o engajamento no site](../../business-objectives/acquisition-growth/increase-website-engagement.md).

**KPIs:** Tempo na Página (Web), Envolvimento, Taxas de Conversão

### Aumentar o engajamento do aplicativo móvel

Impulsione o uso ativo diário, a adoção de recursos e as conversões no aplicativo por meio de experiências personalizadas no aplicativo.

**KPIs:** Envolvimento, Retenção, Taxas de Conversão

## Exemplo de casos de uso tático

A seguir estão implementações táticas comuns desse padrão:

- Personalização principal da página inicial por nível de fidelidade ou estágio do ciclo de vida — exiba banners principais diferentes com base no fato de o cliente ser novo, ativo, em risco ou VIP
- Carrossel de recomendações de produtos com base no histórico de compras — forneça sugestões de produtos relevantes usando dados de compras anteriores e pontuações de afinidade de produtos
- Banner promocional personalizado por segmento do cliente — mostre diferentes promoções para segmentos de alto valor, em risco e novos clientes
- Mensagem no aplicativo para usuários móveis com base na adoção de recursos — orienta os usuários para recursos subutilizados com base em seus padrões de uso
- Cartão de conteúdo com oferta personalizada no painel de contas — ofertas persistentes e rejeitadas personalizadas de acordo com o perfil do cliente
- Exibição personalizada de preços ou descontos com base na camada do cliente — mostrar preços específicos da camada ou descontos exclusivos para membros do programa de fidelidade
- Widget de recomendação de venda cruzada com base em produtos próprios — sugira produtos ou serviços complementares com base no portfólio atual
- Navegação personalizada ou ordenação de conteúdo com base em interesses — reordene módulos de conteúdo ou elementos de navegação com base em preferências demonstradas

## Indicadores-chave de desempenho

Os KPIs a seguir ajudam a medir a eficácia desse padrão de caso de uso.

| KPI | Abordagem de medição | Orientação de referencial |
| --- | --- | --- |
| Taxa de participação da Personalization | Cliques e interações com elementos de conteúdo personalizados divididos por impressões | O conteúdo personalizado deve superar o desempenho padrão em 20% a 50% |
| Aumento do índice de conversão | Taxa de conversão para experiências personalizadas versus experiências de controle/padrão | Meta de aumento de 10 a 30% em relação a experiências não personalizadas |
| Índice de click-through (CTR) | Cliques em CTAs, ofertas e recomendações personalizadas divididos por impressões | Monitor por superfície (Web, no aplicativo, cartão de conteúdo) e por segmento |
| Receita por visita | Receita atribuída a sessões com experiências personalizadas | Comparar coortes de visitantes personalizadas com não personalizadas |
| Taxa de interação do cartão de conteúdo | Cliques e dispensas no cartão de conteúdo relacionados a impressões | Rastrear por tipo de cartão e segmento de público |
| Engajamento na mensagem no aplicativo | Interações de mensagem no aplicativo (cliques no CTA, rejeições) relativas a impressões | Comparar segmentos de público-alvo e tipos de mensagem |
| Tempo na página | Tempo médio gasto em páginas com conteúdo personalizado em relação ao padrão | As páginas personalizadas devem mostrar maior tempo de permanência |
| Taxa de aceitação da oferta | Porcentagem de ofertas selecionadas pela decisão que resultam em um evento de conversão | Rastrear por oferta, por posicionamento e por estratégia de classificação |

## Padrão do caso de uso

Esta seção descreve o padrão principal e sua cadeia de funções.

**Personalização de aplicativo/Web de visitante conhecido**

Forneça conteúdo, ofertas ou promoções personalizadas a um visitante identificado com base em perfil em tempo real e associação de segmento em superfícies da Web, dispositivos móveis no aplicativo e cartões de conteúdo.

**Cadeia de funções:** Avaliação de público-alvo > Personalization Decisioning > Configuração de superfície/canal > Entrega de conteúdo > Rastreamento de impressão > Relatórios

## Aplicativos

Os aplicativos a seguir são usados neste padrão de caso de uso.

- **[!DNL Adobe Journey Optimizer](AJO)** — Configuração de canal da Web, configuração de canal no aplicativo, configuração de canal de cartão de conteúdo, decisão (seleção e classificação de ofertas), criação de mensagens (criação de conteúdo personalizado), execução de campanha, experimentação de conteúdo e relatórios
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)** — Avaliação de público (borda, streaming e lote), pesquisa de perfil em tempo real via Edge Network, enriquecimento de perfil com atributos computados e pontuações de propensão
- **[!DNL Adobe Experience Platform](AEP)** — Armazenamento de perfil, serviço de identidade, SDK da Web, SDK Móvel, configuração de sequência de dados, entrega de rede de borda

## Funções básicas

Os seguintes recursos básicos devem estar em vigor para esse padrão de caso de uso. Para cada função, o status indica se ele é tipicamente necessário, se presume ser pré-configurado ou se não é aplicável.

| Função de base | Status | O que deve estar em vigor | Referência do Experience League |
| --- | --- | --- | --- |
| Administração e governança | Presumido em vigor | sandbox da AJO com canal da Web, canal no aplicativo e permissões de decisão configuradas. Usuários provisionados com funções de profissional de marketing e autor de conteúdo. | [Visão geral das sandboxes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/home), [Visão geral do controle de acesso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Preparação e modelagem de dados | Obrigatório | O esquema de perfil deve incluir atributos usados para personalização e segmentação (por exemplo, nível de fidelidade, histórico de compras, interesses de produtos, estágio do ciclo de vida). Esquema de evento de experiência para rastreamento de interação na Web/aplicativo e eventos de conversão. Conjuntos de dados habilitados para [!DNL Real-Time Customer Profile]. | [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [noções básicas de composição de esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| Fontes de dados e coleção | Obrigatório | Web SDK implementado em propriedades da Web para entrega de experiência e rastreamento de impressão. Mobile SDK implementado em aplicativos móveis para entrega de cartão de conteúdo e no aplicativo. Sequência de dados configurada com o serviço AJO habilitado para personalização de borda. Dados do perfil em tempo real disponíveis na borda para personalização em subsegundos. | [Visão geral do Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home), [Visão geral do Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview), [Configurar sequências de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure) |
| Configuração de identidade e perfil | Obrigatório | Namespaces de identidade conhecidos (ID de CRM, email, ID de usuário autenticada) configurados. Compilação de identidade entre sessões anônimas e autenticadas operacionais para transição contínua de personalização anônima para personalização de visitante conhecido. Política de mesclagem do Edge configurada com `isActiveOnEdge: true` para resolver o perfil autenticado na borda. | [Visão geral do Serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| Definição e segmentação do público-alvo | Obrigatório | Públicos-alvo definidos com atributos de perfil, dados comportamentais e atributos computados. Avaliação do Edge ou streaming habilitada para qualificação de personalização em tempo real. Os públicos usados para personalização baseada em segmento devem se qualificar para avaliação de borda. | [Visão geral do Serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [Segmentação do Edge](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation) |

## Funções de suporte

Os recursos a seguir aumentam esse padrão de caso de uso, mas não são necessários para a execução principal.

| Função de suporte | Status | Por que é importante | Referência do Experience League |
| --- | --- | --- | --- |
| Criação de atributo calculado/derivado | Recomendado | Os atributos computados (por exemplo, [!DNL Customer AI] pontuações de propensão, valor vitalício, pontuação de engajamento, afinidade de produto, dias desde a última compra) melhoram significativamente a qualidade da personalização, fornecendo sinais mais avançados para a definição do público e a seleção de conteúdo. | [Visão geral dos atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview), [Visão geral da IA do cliente](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview) |
| Gerenciamento do ciclo de vida dos dados | Recomendado | As políticas de retenção de dados de perfis e eventos garantem que dados novos e relevantes fortaleçam as decisões de personalização. A aplicação do consentimento garante que a personalização respeite as preferências do usuário. | [Visão geral do Gerenciamento Avançado do Ciclo de Vida dos Dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [Consentimento no Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted) |
| Rotulagem e aplicação de uso de dados | Recomendado | Os rótulos de governança nos atributos de perfil usados para personalização (especialmente atributos adjacentes às PII, como histórico de compras, localização, dados financeiros) garantem a conformidade com as políticas de uso de dados. | [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [Visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview) |
| Monitoramento e capacidade de observação | Recomendado | O monitoramento do desempenho de entrega e personalização do Edge ajuda a detectar problemas de latência, falhas de entrega ou problemas de atualização de dados que prejudicam a experiência personalizada. | [Visão geral dos Insights de Observabilidade](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home), [Visão geral dos alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview) |
| Relatórios e análise | Incluído | O relatório de desempenho do Personalization faz parte da Etapa 6 da Cadeia de Funções. [!DNL Customer Journey Analytics] a análise permite uma investigação profunda do impacto da personalização na conversão, no envolvimento e na receita dos segmentos de visitantes. | [visão geral do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [guia de integração do AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo) |

## Funções do aplicativo

Este plano exerce as seguintes funções do Catálogo de Funções da Aplicação. As funções são mapeadas para fases de implementação em vez de etapas numeradas.

### [!DNL Journey Optimizer] (AJO)

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Configuração de canais | Configuração de superfície e canal | Configurar superfícies de canal da Web, no aplicativo e no cartão de conteúdo para entrega de personalização |
| Criação de mensagens | Criação de conteúdo | Crie variantes de conteúdo personalizadas com conteúdo dinâmico, expressões de personalização e blocos condicionais para cada superfície |
| Execução de campanha | Configuração e ativação do Campaign | Criar e ativar campanhas da Web (programadas ou acionadas por API) que vinculam públicos, superfícies e conteúdo |
| Decisão. | Configuração de decisão (Opção B/C) | Configurar políticas de decisão com regras de qualificação, estratégias de classificação e itens de oferta/conteúdo para personalização dinâmica |
| Experimentação de conteúdo | Otimização (opcional) | Execute testes A/B em variantes de conteúdo personalizadas para otimizar o desempenho |
| Frequência e regras de negócios | Configuração e ativação do Campaign | Imponha limites de frequência de impressão para evitar a fadiga da personalização excessiva |
| Relatórios e análise de desempenho | Relatórios e otimização | Monitorar métricas de entrega, envolvimento e conversão de personalização por superfície e segmento |

### [!DNL Real-Time CDP] (RT-CDP)

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Avaliação de público | Definição e avaliação de público-alvo | Defina e avalie públicos-alvo usando atributos de perfil, dados comportamentais e atributos computados com avaliação de borda ou transmissão |
| Pesquisa de perfil em tempo real | Entrega de conteúdo (tempo de execução) | Acesse atributos de perfil e associações de segmento em tempo real por meio do Edge Network para decisões de personalização em subsegundos |
| Enriquecimento de perfil | Pré-implementação (suporte) | Enriqueça perfis com atributos computados, [!DNL Customer AI] pontuações e sinais comportamentais agregados que melhoram a qualidade da personalização |

## Pré-requisitos

Antes de implementar esse padrão de caso de uso, verifique se o seguinte está em vigor:

- [ O Web SDK ] implementado nas propriedades da Web de destino com `alloy("sendEvent")` configurado para exibições de página e rastreamento de interação
- [ ] Mobile SDK implementado nos aplicativos móveis de destino (se as superfícies no aplicativo ou no cartão de conteúdo forem usadas)
- [ ] Datastream configurado com o serviço [!DNL Adobe Journey Optimizer] habilitado
- [ ] O esquema de perfil inclui atributos usados para personalização (nível de fidelidade, histórico de compras, interesses de produtos, estágio do ciclo de vida)
- [ ] Esquema de evento de experiência configurado para controle de impressão e conversão
- [ ] Namespaces de identidade conhecidos criados e identificação de identidade operacional entre identidades anônimas (ECID) e autenticadas
- [ Política de mesclagem do Edge ] configurada com `isActiveOnEdge: true`
- [ ] Públicos-alvo definidos com avaliação qualificada para borda para personalização em tempo real
- [ ] ativos de conteúdo (imagens, cópia, CTAs) preparados para cada variante de personalização
- [ ] Estratégia do Personalization documentada: quais atributos determinam qual conteúdo, para quais superfícies

## Opções de implementação

Esta seção descreve as abordagens de implementação disponíveis para este padrão de caso de uso.

### Opção A: Personalização da Web baseada em segmentos

**Recomendado para:** personalização determinística onde variantes de conteúdo específicas mapeiam diretamente para segmentos de público-alvo — banners de fidelidade de nível específico herói, mensagens de estágio do ciclo de vida, conteúdo promocional de segmento de cliente. Ideal quando o mapeamento de conteúdo para segmento é bem definido e não requer classificação ou otimização dinâmica.

**Como funciona:**

A personalização baseada em segmentos mapeia variantes de conteúdo diretamente para segmentos de público-alvo. Quando o perfil de um visitante conhecido é avaliado em relação aos públicos qualificados para borda no carregamento da página, o sistema determina a quais segmentos o visitante pertence e exibe a variante de conteúdo correspondente. A seleção é baseada na prioridade de associação do segmento: se um visitante se qualificar para vários segmentos, o conteúdo do segmento de prioridade mais alta será exibido.

Essa abordagem usa campanhas de canal da Web do AJO (ou campanhas no aplicativo/cartão de conteúdo) com regras de conteúdo condicional ou várias configurações de direcionamento de tratamento. Cada segmento de público-alvo está associado a uma experiência de conteúdo específica. Nenhum mecanismo de decisão está envolvido — a lógica de seleção de conteúdo é totalmente orientada por segmentos.

O conteúdo é criado usando a interface de criação de mensagens do AJO com blocos de conteúdo dinâmico que renderizam conteúdo diferente com base na associação de público-alvo ou nos atributos do perfil. O Web SDK ou Mobile SDK oferece a experiência personalizada em tempo real por meio da Edge Network.

**Principais considerações:**

- As variantes de conteúdo devem ser pré-criadas para cada segmento
- As definições de segmento devem ser qualificadas para qualificação em tempo real
- Adicionar novos segmentos ou variantes de conteúdo requer a atualização da configuração da campanha
- A seleção de conteúdo é determinística — o mesmo segmento sempre vê o mesmo conteúdo

**Vantagens:**

- Simples de implementar e manter com mapeamento claro de conteúdo para segmento
- Fácil de entender e explicar a lógica de personalização para as partes interessadas
- Sem sobrecarga de decisão — resolução de conteúdo mais rápida
- Controle completo sobre qual conteúdo cada segmento recebe

**Limitações:**

- Flexibilidade limitada quando o número de segmentos e variantes de conteúdo aumenta
- Não é possível otimizar dinamicamente a seleção de conteúdo com base em sinais de nível de perfil além da associação do segmento
- A adição de novas variantes de conteúdo requer atualizações manuais de campanha
- Não é compatível com os próximos cenários de melhor oferta em que várias ofertas competem pela mesma inserção

**Experience League:**

- [Introdução ao canal da Web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [Criar experiências da Web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)

### Opção B: Personalização baseada em decisão

**Recomendado para:** Personalização dinâmica, onde o conteúdo ou a oferta ideal deve ser selecionado por perfil usando regras de elegibilidade e estratégias de classificação: próxima melhor oferta na página inicial, recomendações personalizadas de produto, seleção de banner promocional dinâmico. Ideal quando várias ofertas ou itens de conteúdo competem pela mesma disposição e o sistema deve escolher a melhor.

**Como funciona:**

A personalização baseada em decisão usa o AJO Decisioning para avaliar o perfil de cada visitante em relação a um catálogo de itens de conteúdo ou ofertas, aplicando regras de elegibilidade para determinar quais itens se qualificam e aplicando uma estratégia de classificação (baseada em prioridade, baseada em fórmula ou classificada por IA) para selecionar o item ideal para cada posicionamento.

A implementação envolve a criação de disposições (onde o conteúdo aparece), a definição de ofertas com regras de elegibilidade e representações de conteúdo, a organização de ofertas em coleções e a criação de políticas de decisão que vinculam disposições a coleções com estratégias de classificação. No tempo de execução, quando um visitante carrega uma página, o Edge Network avalia a política de decisão em relação ao perfil do visitante e retorna o conteúdo da oferta selecionada.

Essa abordagem oferece suporte a cenários de personalização sofisticados, incluindo a próxima melhor oferta, promoções personalizadas com limitação e seleção de conteúdo otimizado por IA. As ofertas podem ter limites de limite global e por perfil, intervalos de datas de validade e critérios de elegibilidade complexos que combinam atributos de perfil e associação de público-alvo.

**Principais considerações:**

- Requer mais configurações iniciais (posicionamentos, ofertas, regras de qualificação, coleções, decisões)
- As estratégias de classificação podem ser baseadas em prioridade (manual), baseadas em fórmula (expressão personalizada) ou classificadas por IA (otimização automática)
- A classificação de IA exige um mínimo de 1.000 eventos de conversão para o treinamento de modelo
- Os contadores de limite de oferta podem ter um pequeno atraso em cenários de alta taxa de transferência
- Uma oferta substituta deve ser configurada para casos em que nenhuma oferta personalizada é qualificada

**Vantagens:**

- Seleção dinâmica de conteúdo por perfil sem mapeamento de segmento para conteúdo codificado
- Compatível com critérios complexos de qualificação e lógica de classificação
- A opção classificada por IA permite a otimização automática sem intervenção manual
- O limite de oferta impede a exposição excessiva de conteúdo específico
- Gerenciamento centralizado de ofertas — as ofertas podem ser reutilizadas em campanhas e canais

**Limitações:**

- Maior complexidade de implementação do que a personalização baseada em segmentos
- A classificação de IA requer volume de evento de conversão suficiente para treinamento
- A avaliação da decisão adiciona latência marginal em comparação à entrega direta de conteúdo com base em segmentos
- A classificação baseada em fórmula requer um design cuidadoso para evitar priorizações não intencionais

**Experience League:**

- [Visão geral da Gestão de decisões](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Crie ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Criar decisões](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estratégias de classificação](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

**Como isso se diferencia da Opção B do Offer Decisioning:**

A infraestrutura é idêntica — ambos usam o AJO Decisioning na borda com o Web SDK e uma política de mesclagem ativa de borda. A diferença é o que está sendo selecionado. Essa opção gerencia itens de conteúdo nos quais o critério de seleção é o ajuste de personalização (associação de segmento, classificação comportamental). [Offer Decisioning](offer-decisioning.md) A opção B gerencia um catálogo de ofertas controlado em que as regras de elegibilidade, os limites de limite e as janelas de validade são requisitos comerciais. Se o conjunto de itens exigir limite de impressão por perfil, restrições de qualificação regulamentar ou gerenciamento do ciclo de vida da oferta, use a Opção B do Offer Decisioning.

### Opção C: Personalização de várias superfícies (Web + no aplicativo + cartão de conteúdo)

**Recomendado para:** Personalização consistente em várias superfícies digitais — fornecendo experiências personalizadas coordenadas em páginas da Web, mensagens móveis no aplicativo e cartões de conteúdo. Ideal quando a organização tem propriedades da Web e de aplicativos móveis e deseja uma lógica de personalização unificada em todos os pontos de contato digitais.

**Como funciona:**

A personalização de várias superfícies estende a Opção A (baseada em segmentos) ou a Opção B (baseada em decisões) para fornecer conteúdo personalizado em vários tipos de superfície do AJO. Cada tipo de superfície — Web, no aplicativo, cartão de conteúdo — pode ter diferentes formatos de conteúdo e mecanismos de entrega, mas a lógica de personalização subjacente (associação de público ou decisão) é compartilhada.

A implementação envolve a configuração de superfícies de canal para cada tipo de superfície, a criação de conteúdo específico de superfície (HTML/CSS da Web para superfícies da Web, mensagens estruturadas para no aplicativo, layouts de cartão para cartões de conteúdo) e a criação de campanhas direcionadas à superfície apropriada. O Web SDK lida com a entrega da superfície da Web, enquanto o Mobile SDK lida com a entrega no aplicativo e de cartão de conteúdo.

Os cartões de conteúdo são especialmente valiosos para mensagens personalizadas persistentes e descartáveis em painéis de conta ou telas iniciais de aplicativos. As mensagens no aplicativo são ideais para comunicações contextuais e específicas da sessão. A personalização da Web lida com banners ilustrados, widgets de recomendação e conteúdo promocional.

**Principais considerações:**

- Cada tipo de superfície requer sua própria configuração de superfície de canal e criação de conteúdo
- O Web SDK e o Mobile SDK devem ser implementados e configurados
- O conteúdo deve ser projetado para cada formato de superfície (diferentes dimensões, layouts, padrões de interação)
- Públicos-alvo compartilhados e lógica de decisão garantem a consistência entre superfícies
- Os ensaios devem abranger todos os tipos de superfícies nos dispositivos

**Vantagens:**

- Experiência de personalização consistente em todos os pontos de contato digitais
- A lógica de decisão e público compartilhado reduz a duplicação
- Os cartões de conteúdo fornecem uma superfície de personalização persistente e não intrusiva
- As mensagens no aplicativo permitem personalização contextual e específica da sessão em dispositivos móveis

**Limitações:**

- A maior complexidade de implementação — requer configuração para cada tipo de superfície
- Requer a implementação do Web SDK e do Mobile SDK
- O conteúdo deve ser projetado e mantido para cada formato de superfície
- O escopo de teste aumenta a cada tipo de superfície adicional

**Experience League:**

- [Visão geral do canal no aplicativo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/get-started-in-app)
- [Canal de cartão de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/get-started-content-card)
- [Introdução ao canal da Web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)

### Comparação de opções

A tabela a seguir compara as três opções de implementação.

| Critérios | Opção A: Com Base Em Segmentos | Opção B: Com Base Em Decisões | Opção C: Várias Superfícies |
| --- | --- | --- | --- |
| Melhor para | Mapeamento conhecido de segmento para conteúdo | Seleção dinâmica de conteúdo por perfil | Personalização consistente na Web + dispositivos móveis |
| Complexo | Baixa | Medium-Alto | Alta (baseia-se em A ou B) |
| Latência | Mais rápido (resolução de segmento direto) | Ligeiramente maior (avaliação da decisão) | Depende da opção subjacente (A ou B) |
| Flexibilidade | Limitado a pares predefinidos de conteúdo de segmentos | Alta — classificação e elegibilidade dinâmicas | Mais alto — várias superfícies com lógica compartilhada |
| Gerenciamento de conteúdo | Mapeamento manual de segmento para conteúdo | Biblioteca de ofertas centralizada com regras de qualificação | Conteúdo por superfície com lógica de personalização compartilhada |
| Otimização | Teste A/B manual | Otimização automática classificada por IA disponível | Otimização por superfície |
| Exige | Públicos-alvo qualificados para a Edge, Web SDK | Posicionamentos, ofertas, regras de qualificação, decisões | Web SDK + SDK móvel, várias configurações de superfície |
| Superfícies suportadas | Web (principal) | Web (principal) | Web + No Aplicativo + Cartão De Conteúdo |

### Escolha a opção certa

Comece com estas perguntas para selecionar a abordagem de implementação correta:

1. **Quantas superfícies?** Se você precisar de personalização na Web e no aplicativo móvel, escolha a Opção C (que se baseia em A ou B para a lógica subjacente). Se for somente para Web, escolha entre A e B.

2. **Qual é o nível de dinamismo de sua seleção de conteúdo?** Se você tiver um mapeamento bem definido de segmentos para variantes de conteúdo (por exemplo, de 3 a 5 níveis de fidelidade, cada um com um banner principal específico), escolha a Opção A. Se precisar selecionar a partir de um catálogo de ofertas com elegibilidade e classificação complexas, escolha a Opção B.

3. **Você precisa de uma seleção otimizada para IA?** Se você quiser que o sistema aprenda e otimize automaticamente qual conteúdo tem melhor desempenho para cada perfil, escolha a Opção B com decisões classificadas por IA.

4. **Quantas variantes de conteúdo?** Se você tiver menos de 10 variantes de conteúdo com mapeamentos de segmentos claros, a Opção A será mais simples. Se você tiver dezenas de ofertas que precisam de filtragem e classificação de qualificação, a Opção B terá melhor dimensionamento.

5. **Você pretende estender para outros canais?** Se sua lógica de decisão acabar oferecendo ofertas por email, Web e outros canais, a Opção B fornece a base de decisão centralizada que o cross-channel offer decisioning estende.

## Fases de implementação

Esta seção aborda detalhadamente cada fase da implementação.

### Fase 1: definir públicos e configurar a avaliação

**Função do aplicativo:** RT-CDP: Avaliação de Público-Alvo

**O que você configurará:** Defina os públicos que impulsionam a seleção de conteúdo de personalização. Esses públicos-alvo representam os segmentos de visitantes que receberão experiências personalizadas — camadas de fidelidade, estágios do ciclo de vida, coortes comportamentais ou grupos de afinidade de produtos.

**Pontos de decisão nesta fase:**

>[!NOTE]
>**Decisão: método de avaliação de público-alvo**
>
>Com que rapidez a associação de público-alvo deve ser resolvida para personalização? Isso afeta diretamente se a personalização pode acontecer no carregamento da página ou se requer um atraso.
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Avaliação da borda | Personalização da Web/aplicativo em tempo real que requer qualificação em subsegundos | Limitado a verificações simples de atributos de perfil e associação de segmento. Sem consultas de série temporal ou agregações complexas. Necessário para personalização de visitante conhecido. |
>| Avaliação de transmissão | Qualificação quase em tempo real quando perfis entram/saem de públicos com base em eventos comportamentais | Suporta queries de janela de evento único e tempo limitado. As alterações no público foram refletidas em minutos. Adequado para superfícies no aplicativo e de cartão de conteúdo em que um pequeno atraso é aceitável. |
>| Avaliação em lote | O público-alvo diário é atualizado para segmentos com base em agregações complexas ou padrões históricos | Suporte completo à função de regra de segmento. Não é adequado para personalização em tempo real, mas pode complementar públicos-alvo de borda com segmentos complexos pré-calculados. |

>[!NOTE]
>**Decisão: atributos do Personalization**
>
>Quais atributos de perfil devem impulsionar a definição do público-alvo e a seleção de conteúdo?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Atributos do perfil (nível de fidelidade, estágio do ciclo de vida) | Personalização determinante com base nas propriedades conhecidas do cliente | Atributos estáveis e bem definidos. Fácil de mapear para variantes de conteúdo. Disponível na borda se o perfil estiver configurado corretamente. |
>| Sinais comportamentais (histórico de compras, padrões de navegação) | Personalization com base em comportamentos e padrões de engajamento recentes | Requer atributos computados ou segmentos de streaming. Mais dinâmico, mas mais complexo de manter. |
>| Pontuações de propensão ([!DNL Customer AI]) | Personalização preditiva com base na probabilidade de conversão, churn ou compra | Requer atributos computados. Permite personalização sofisticada, mas requer dados de treinamento de modelo ML. |
>| Abordagem combinada | A maioria das implementações de produção | Usa atributos de perfil para segmentação primária com sinais comportamentais e pontuações de propensão para refinamento. |

**Navegação da interface do usuário:** Cliente > Públicos-alvo > Criar público-alvo > Criar regra

**Detalhes de configuração da chave:**

- Defina públicos usando o Construtor de segmentos com expressões de regra de segmento que fazem referência a atributos de perfil
- Garantir que as expressões de regra de segmento se qualifiquem para avaliação de borda (verificações de atributo simples, associação de segmento)
- Configurar públicos-alvo qualificados para a borda para casos de uso de personalização em tempo real
- Considere suprimir públicos-alvo para excluir visitantes recentemente convertidos ou recusados

**Documentação do Experience League:**

- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentação de borda](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Segmentação de transmissão](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Referência do Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### Fase 2: configurar a decisão (somente as opções B e C)

**Função do aplicativo:** AJO: decisão

**O que você configurará:** configure a infraestrutura de decisão que seleciona dinamicamente o conteúdo ou a oferta ideal para cada visitante. Isso inclui disposições (onde as ofertas são exibidas), ofertas (qual conteúdo está disponível), regras de elegibilidade (quem se qualifica), estratégias de classificação (como escolher o melhor) e políticas de decisão (como tudo se conecta).

**Pontos de decisão nesta fase:**

>[!NOTE]
>**Decisão: estratégia de classificação**
>
>Como as ofertas elegíveis devem ser classificadas para selecionar a melhor para cada visitante?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Baseado em prioridade (manual) | Casos de uso simples com hierarquia de ofertas clara | Cada oferta tem um valor de prioridade manual. Vitória da oferta elegível de maior prioridade. Fácil de entender e controlar. |
>| Baseado em fórmula (expressão personalizada) | Quando a classificação deve considerar atributos de perfil | As fórmulas de classificação personalizadas fazem referência aos dados do perfil (por exemplo, pontuação por nível de fidelidade + recenticidade). Flexível, mas requer design e teste de fórmulas. |
>| Classificado por IA (otimização automática) | Quando quiser que o sistema otimize automaticamente a seleção de ofertas | O modelo de aprendizado de máquina aprende quais ofertas têm melhor desempenho para quais perfis. Requer no mínimo 1.000 eventos de conversão para treinamento. Melhor para posicionamentos de alto tráfego. |

>[!NOTE]
>**Decisão: Limite de oferta**
>
>Deve haver limites em quantas vezes uma oferta é exibida a um visitante ou entre todos os visitantes?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Limite por perfil | Evitar que a fadiga veja a mesma oferta repetidamente | Limita impressões por visitante durante um período. Garante a variedade na experiência personalizada. |
>| Limite global | Limitar o total de impressões para uma promoção ou oferta de disponibilidade limitada | Limita o total de impressões em todos os visitantes. Útil para promoções de quantidade limitada. |
>| Sem limite | Conteúdo sempre verde ou ofertas sempre relevantes | Sem limites de impressão. Adequado para conteúdo persistente, como banners de nível de fidelidade. |

**Navegação da interface do usuário:** [!DNL Journey Optimizer] > Componentes > Gerenciamento de decisão

**Detalhes de configuração da chave:**

- Crie inserções para cada superfície em que as ofertas serão exibidas (banner da Web, área de mensagem no aplicativo, slot de cartão de conteúdo)
- Defina regras de elegibilidade usando expressões de regra de segmento que fazem referência a atributos de perfil e associação de público-alvo
- Criar ofertas personalizadas com representações de conteúdo para cada posicionamento
- Criar uma oferta substituta que cubra todos os posicionamentos (exibidos quando nenhuma oferta personalizada é qualificada)
- Organize ofertas com qualificadores de coleção (tags) e agrupe em coleções
- Criar posicionamentos de vinculação de política de decisão para coleções com a estratégia de classificação selecionada

**Documentação do Experience League:**

- [Criar inserções](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Criar regras de decisão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crie ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Criar ofertas substitutas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Criar coleções](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Criar decisões](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estratégias de classificação](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Fase 3: Configurar superfícies e canais

**Função do aplicativo:** AJO: configuração de canal

**O que você configurará:** Configure as superfícies de canal que definem onde o conteúdo personalizado será entregue. Cada tipo de superfície (Web, no aplicativo, cartão de conteúdo) requer sua própria configuração especificando o URI da superfície, o formato de conteúdo e os parâmetros de entrega.

**Pontos de decisão nesta fase:**

>[!NOTE]
>**Decisão: superfícies de destino**
>
>Quais superfícies digitais receberão conteúdo personalizado?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Somente canal da Web | Personalization focada em propriedades da Web | Exige o Web SDK. Implementação mais simples. Abrange banners ilustrados, áreas promocionais e widgets de recomendação. |
>| Somente canal no aplicativo | Personalization focada em experiências de aplicativos móveis | Requer o Mobile SDK. Abrange mensagens contextuais e específicas da sessão no aplicativo. |
>| Somente canal de cartão de conteúdo | Mensagens personalizadas persistentes e rejeitadas | Requer SDK móvel ou Web SDK. Os cartões persistem até serem descartados. Ideal para painéis e telas iniciais. |
>| Superfícies múltiplas (opção C) | Personalização consistente na Web e em dispositivos móveis | Requer Web SDK e SDK móvel. Cada superfície precisa de configuração e conteúdo separados. |

>[!NOTE]
>**Decisão: abordagem de configuração da superfície da Web**
>
>Como a superfície da Web deve ser configurada para entrega de conteúdo?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Aplicativo de página única (SPA) | Aplicativos web modernos com roteamento no lado do cliente | Use `renderDecisions: true` em chamadas `sendEvent` do Web SDK. Conteúdo renderizado automaticamente pela SDK. |
>| Aplicativo de várias páginas (MPA) | Páginas da Web renderizadas pelo servidor tradicional | Conteúdo entregue no carregamento da página por meio da resposta do Edge Network. Pode exigir a configuração do URI da superfície no nível da página. |

Navegação da **UI:** [!DNL Journey Optimizer] > Administração > Canais > Superfícies de canal

**Detalhes de configuração da chave:**

- Para superfícies da Web: configurar o URI da superfície da Web correspondente às páginas de destino
- Para superfícies no aplicativo: configure a superfície do aplicativo móvel com a ID do aplicativo e o tipo de superfície
- Para superfícies de cartão de conteúdo: configure a superfície de cartão de conteúdo com a ID do aplicativo ou o contexto da Web
- Verifique se a sequência de dados tem o serviço AJO habilitado para entrega de personalização de borda

**Documentação do Experience League:**

- [Introdução ao canal da Web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [Configuração do canal da Web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/web-configuration)
- [Pré-requisitos do canal no aplicativo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/inapp-configuration)
- [Configuração do cartão de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/content-card-configuration)

### Fase 4: Conteúdo do autor

**Função do aplicativo:** AJO: Criação de Mensagens

**O que você configurará:** Crie as variantes de conteúdo personalizadas para cada superfície, segmento ou oferta. Isso inclui projetar o layout visual, adicionar expressões de personalização que fazem referência a atributos de perfil, configurar blocos de conteúdo condicional e criar fragmentos de conteúdo reutilizáveis.

**Pontos de decisão nesta fase:**

>[!NOTE]
>**Decisão: abordagem de conteúdo**
>
>Como o conteúdo personalizado deve ser estruturado para este caso de uso?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Blocos de conteúdo condicional | Diferentes seções de conteúdo no mesmo layout variam de acordo com o público-alvo | Um único ativo de conteúdo com regras condicionais. Eficiente para pequenas variações (título, texto CTA, troca de imagem). |
>| Variantes de conteúdo separadas por tratamento | Layouts ou designs fundamentalmente diferentes por público-alvo | Vários ativos de conteúdo completos. Mais flexível, mas mais a manter. Obrigatório para experimentação de conteúdo. |
>| Conteúdo orientado por decisão | Conteúdo selecionado dinamicamente de um catálogo de ofertas | As representações de oferta definem o conteúdo. A gestão de conteúdo é centralizada na biblioteca de ofertas. |

>[!NOTE]
>**Decisão: profundidade do Personalization**
>
>Quanto do conteúdo deve ser personalizado?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Personalização no nível da superfície | Somente elementos específicos são personalizados (imagem principal, CTA, banner de oferta) | Menor complexidade. Personalização focada em áreas de alto impacto. Ponto de partida mais comum. |
>| Personalização de página inteira | O layout da página inteira ou a ordenação de conteúdo é personalizada | Maior complexidade. Requer ampla criação de conteúdo. Oferece a experiência mais personalizada. |
>| Personalização no nível do token | Tokens de personalização em linha (nome, camada, saldo de pontos) | Forma mais simples. Insere valores de atributo de perfil no conteúdo estático. |

Navegação da **UI:** [!DNL Journey Optimizer] > Campanhas > Criar campanha > Editar conteúdo

**Onde as opções divergem:**

**Para a Opção A (baseada em segmento):**

- Crie variantes de conteúdo para cada segmento de público usando o designer da Web ou o editor de código
- Usar blocos de conteúdo dinâmico com condições baseadas na associação de público-alvo
- Configurar expressões de personalização que fazem referência a atributos de perfil (por exemplo, `{{profile.person.name.firstName}}`, `{{profile.loyalty.tier}}`)
- Configurar regras condicionais para exibir conteúdo diferente com base na associação do segmento

**Para a Opção B (baseada em decisão):**

- Crie representações de conteúdo de oferta para cada posicionamento definido na Fase 2
- Cada oferta tem uma ou mais representações (HTML, image, JSON) correspondentes a inserções
- Integrar a saída de decisão à página da Web ou ao aplicativo incorporando disposições de decisão
- O conteúdo é selecionado dinamicamente no tempo de execução — a criação se concentra em itens de oferta individuais

**Para a Opção C (várias superfícies):**

- Conteúdo específico da superfície do autor para cada superfície de destino (HTML/CSS da Web, mensagem estruturada no aplicativo, layout do cartão de conteúdo)
- Mantenha uma lógica de personalização consistente nas superfícies ao adaptar-se às restrições de formato de cada superfície
- Testar a renderização do conteúdo em cada tipo de superfície

**Documentação do Experience League:**

- [Criar experiências da Web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxe do Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Funções auxiliares](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Entregar ofertas em mensagens](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Criar mensagens no aplicativo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/create-in-app)
- [Criar cartões de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/create-content-card)

### Fase 5: configurar e ativar campanhas

**Função do aplicativo:** AJO: Execução de Campanha

**O que você configurará:** crie e ative a campanha do AJO que associa o público, a superfície e o conteúdo para entrega. Para personalização na Web, as campanhas normalmente são configuradas para ativação imediata ou contínua em vez de envios programados únicos.

**Pontos de decisão nesta fase:**

>[!NOTE]
>**Decisão: Tipo de campanha**
>
>Como a campanha de personalização deve ser acionada?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Campanha programada (sempre ativa) | Personalização contínua que é executada continuamente para todos os visitantes qualificados | Defina a data de início como imediata e sem data de término. A campanha permanece ativa até ser interrompida manualmente. Mais comum para personalização da Web. |
>| Campanha programada (limite de tempo) | Personalization vinculada a um período de promoção específico | Defina datas de início e término. O Campaign é interrompido automaticamente após a data de término. Adequado para promoções sazonais ou ofertas de tempo limitado. |
>| Campanha acionada por API | Personalization acionado por um evento de aplicativo específico | Acionado programaticamente. Útil quando a personalização só deve aparecer em resposta a eventos específicos do sistema. |

>[!NOTE]
>**Decisão: Limite de frequência**
>
>A frequência de impressão deve ser limitada para essa personalização?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Aplicar regras de frequência | Personalização promocional ou baseada em oferta que pode fatigar os visitantes | Impede que a mesma personalização apareça muitas vezes. Configurado por meio de regras de negócios do AJO. |
>| Sem limite de frequência | Personalização de conteúdo permanente (banner no nível de fidelidade, conteúdo do painel) | Conteúdo sempre relevante que não causa fadiga. Não são necessários limites de impressão. |

**Navegação da interface do usuário:** [!DNL Journey Optimizer] > Campanhas > Criar campanha

**Detalhes de configuração da chave:**

- Selecione o canal da Web, no aplicativo ou do cartão de conteúdo e a superfície configurada na Fase 3
- Vincular o público-alvo definido na Fase 1
- Vincular o conteúdo criado na Fase 4
- Configurar o agendamento da campanha (imediato, intervalo de datas ou acionado por API)
- Revisar e ativar a campanha
- Para experimentação de conteúdo: ative o experimento, defina tratamentos, defina a alocação de tráfego e as métricas de sucesso antes da ativação

**Documentação do Experience League:**

- [Criar uma campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Introdução às campanhas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Regras de frequência](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Introdução ao experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Criar um experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)

### Fase 6: Rastrear impressões e coletar dados

**Função do aplicativo:** AEP: Fontes de dados e coleção

**O que você configurará:** verifique se as impressões, as interações e as conversões de experiências personalizadas são rastreadas de volta para a plataforma para otimização de relatórios, reavaliação de públicos-alvo e decisões.

**Detalhes de configuração da chave:**

- Verificar se o Web SDK está enviando `decisioning.propositionDisplay` eventos quando o conteúdo personalizado é renderizado
- Verificar se o Web SDK está enviando `decisioning.propositionInteract` eventos quando os visitantes interagem com conteúdo personalizado (cliques, rejeições)
- Para o Mobile SDK: verifique se os eventos de interação de mensagem no aplicativo e cartão de conteúdo foram capturados
- Configurar o rastreamento de eventos de conversão para métricas de sucesso downstream (compras, inscrições, adoção de recursos)
- Garantir que os eventos incluam a ID da apresentação para atribuição a decisões de personalização específicas

**Documentação do Experience League:**

- [Visão geral do Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Rastrear eventos com o Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/sendevent/overview)
- [Visão geral do Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)

### Fase 7: relatar e otimizar

**Função do aplicativo:** AJO: Reporting &amp; Performance Analysis, Reporting &amp; Analysis

**O que você configurará:** Configure o monitoramento e a análise de desempenho para medir a eficácia da personalização em superfícies, segmentos e variantes de conteúdo. Use os relatórios nativos do AJO para métricas operacionais e [!DNL Customer Journey Analytics] para análise de impacto nos negócios entre canais.

**Pontos de decisão nesta fase:**

>[!NOTE]
>**Decisão: escopo dos relatórios**
>
>Qual nível de análise é necessário para esse caso de uso de personalização?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Somente relatórios nativos do AJO | Monitoramento operacional das métricas de entrega e envolvimento | Relatórios de campanha integrados com dados de impressão, clique e conversão. Configuração mais rápida. |
>| Análise entre canais do CJA | Análise profunda do impacto da personalização nos resultados de negócios | Exige conexão e visualização de dados do CJA. Permite a análise, as comparações de coorte e a modelagem de atribuição do funnel em todos os canais. |
>| AJO + CJA | Visibilidade operacional e analítica completa | Use o AJO para monitoramento diário e o CJA para análise estratégica. Recomendado para implementações de produção. |

**Navegação da interface do usuário:**

- Relatórios do AJO: Campanhas > Selecionar campanha > Exibir relatório
- CJA: Projetos > Criar novo projeto

**Detalhes de configuração da chave:**

- Acessar relatórios ao vivo da campanha durante a entrega ativa de personalização
- Revisar relatórios históricos de campanhas concluídas ou análises periódicas
- Para o CJA: configure uma conexão que inclua conjuntos de dados de evento da experiência do AJO e crie uma visualização de dados com métricas de personalização
- Crie painéis que controlam a taxa de envolvimento de personalização, o aumento de conversão, a taxa de aceitação da oferta e a receita por visita
- Para personalização baseada em decisão (Opção B): monitore o desempenho da oferta por posicionamento e eficácia da estratégia de classificação

**Documentação do Experience League:**

- [Relatório em tempo real da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Relatório global da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Relatório de experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Visão geral do Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Guia de integração do AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## Considerações de implantação

Esta seção abrange medidas de proteção, armadilhas comuns, práticas recomendadas e decisões de compensação relevantes para esse padrão de caso de uso.

### Medidas de proteção e limites

- As pesquisas na Edge Network têm um SLA de tempo de resposta menor que 200 ms para segmentos avaliados de borda — [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Máximo de 4.000 definições de segmento por sandbox — [Medidas de proteção de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Os segmentos do Edge estão limitados a verificações de atributos simples e consultas de associação de segmento — sem consultas de série temporal — [Segmentação do Edge](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- Somente uma política de mesclagem pode estar ativa no Edge por sandbox — [Políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- Máximo de 10.000 ofertas personalizadas aprovadas por sandbox — [Medidas de proteção do Gerenciamento de decisão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Máximo de 30 disposições por decisão — [medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Os modelos de classificação de IA exigem um mínimo de 1.000 eventos de conversão para treinamento
- O tempo de resposta do Offer Delivery no SLA é inferior a 500 ms na P95 para solicitações de escopo único
- Máximo de 500 campanhas ativas por sandbox — [medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Máximo de 25 atributos computados ativos por sandbox — [Medidas de proteção de atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)

### Armadilhas comuns

- **Política de mesclagem do Edge não configurada:** sem uma política de mesclagem ativa de borda, o Edge Network não pode resolver o perfil autenticado, fazendo com que a personalização falhe ou volte ao comportamento anônimo. Verifique se exatamente uma política de mesclagem tem `isActiveOnEdge: true` na sandbox.
- **Público-alvo não qualificado para borda:** se as expressões de regra de segmento de público-alvo usarem consultas de série temporal, agregações complexas ou `inSegment()` referências a segmentos somente em lote, elas não serão qualificadas para avaliação de borda e não poderão potencializar a personalização em tempo real. Validar a qualificação da borda durante a definição do público-alvo.
- **Lacuna de identificação durante a autenticação:** Quando um visitante faz a transição de anônimo para autenticado, pode haver um breve momento em que o perfil ainda não tenha sido resolvido. Verifique se a compilação de identidade está configurada corretamente e se o Web SDK envia a identidade autenticada via `identityMap` imediatamente após o logon.
- **Oferta substituta ausente na decisão:** Se nenhuma oferta substituta estiver configurada e nenhuma oferta personalizada se qualificar para um visitante, a decisão retornará um conteúdo vazio, criando uma experiência interrompida. Sempre configure uma oferta substituta que cubra todos os posicionamentos.
- **O Web SDK não está enviando eventos de exibição de apresentação:** Se `renderDecisions` estiver definido como `true`, mas eventos de exibição não estiverem sendo enviados, os relatórios não refletirão impressões reais. Verifique o rastreamento de eventos ao inspecionar solicitações de rede nas ferramentas de desenvolvedor do navegador.
- **Cintilação de conteúdo no carregamento da página:** Se o conteúdo personalizado não for pré-ocultado durante a chamada de decisão, os visitantes poderão ver o conteúdo padrão brevemente antes de ser substituído. Use o trecho de pré-ocultação ou a pré-ocultação baseada em CSS para eliminar a cintilação.

### Práticas recomendadas

- Comece com a personalização baseada em segmento (Opção A) para implementação inicial e, em seguida, evolua para baseada em decisão (Opção B) à medida que o catálogo de ofertas cresce e as necessidades de otimização aumentam
- Use públicos avaliados de borda sempre que possível para personalização em tempo real; reserve streaming e públicos em lote para casos de uso complementares
- Implemente a experimentação de conteúdo em experiências personalizadas para validar se a personalização leva a um aumento mensurável em relação ao conteúdo padrão
- Personalização do design com uma estratégia de degradação adequada — se o perfil não puder ser resolvido na borda, exiba um conteúdo padrão bem projetado em vez de uma experiência interrompida
- Use atributos computados para criar sinais de personalização de alto valor, como pontuação de engajamento, afinidade de produto e dias desde a última compra, o que melhora a qualidade da personalização baseada em segmento e decisão
- Mantenha um processo de governança de conteúdo para garantir que o conteúdo personalizado permaneça atualizado, sob marca e em conformidade em todas as superfícies
- Monitore o desempenho da personalização por segmento para identificar quais públicos se beneficiam mais da personalização e onde o aumento é mais forte

### Decisões de compensação

>[!NOTE]
>**Contrapartida: granularidade do Personalization versus complexidade no gerenciamento de conteúdo**
>
>A personalização mais granular (mais segmentos, mais variantes de conteúdo, mais superfícies) fornece experiências cada vez mais personalizadas, mas requer proporcionalmente mais criação de conteúdo, manutenção e esforço de governança.
>
>- **A granularidade mais alta favorece:** melhor experiência do cliente, maior engajamento, aumento de conversão mais forte
>- **A menor granularidade favorece:** implementação mais rápida, menor carga de manutenção de conteúdo, governança mais simples
>- **Recomendação:** comece com 3 a 5 segmentos de alto impacto (por exemplo, camadas de fidelidade ou estágios do ciclo de vida) com diferenciação clara de conteúdo. Expanda a granularidade com base no aumento de desempenho medido. Use a decisão (opção B) para dimensionar a granularidade sem o crescimento proporcional do gerenciamento de conteúdo.

>[!NOTE]
>**Contrapartida: Decisão em tempo real vs. controle de conteúdo determinístico**
>
>A personalização baseada em decisão (Opção B) fornece otimização dinâmica, mas reduz o controle direto sobre qual conteúdo cada visitante vê. A personalização baseada em segmentos (Opção A) fornece controle determinístico total, mas limita a otimização dinâmica.
>
>- **A decisão favorece:** escalabilidade, otimização automática, cenários complexos de qualificação
>- **Vantagens baseadas em segmentos:** Previsibilidade, controle de conformidade, transparência das partes interessadas
>- **Recomendação:** use personalização baseada em segmento para conteúdo sensível à conformidade (mensagens normativas, preços específicos de camada), onde o controle exato é necessário. Use a decisão para conteúdo promocional, ofertas e recomendações em que a otimização dinâmica agrega valor.

>[!NOTE]
>**Contrapartida: disponibilidade de dados do Edge vs. riqueza de personalização**
>
>A personalização avaliada pela Edge é limitada aos atributos disponíveis na loja de perfis de borda. Sinais de personalização mais avançados (histórico comportamental completo, atributos computados complexos) podem exigir pesquisa ou pré-cálculo no lado do servidor.
>
>- **Somente Edge favorece:** Latência de subsegundos, arquitetura mais simples
>- **O enriquecimento pré-calculado favorece:** sinais de personalização mais avançados, definições de público mais sofisticadas
>- **Recomendação:** Use atributos computados para pré-agregar sinais comportamentais avançados em atributos de perfil de borda disponível. Isso fornece a riqueza de dados comportamentais com a velocidade da avaliação de borda.

## Documentação relacionada

Os recursos a seguir fornecem detalhes adicionais sobre as tecnologias e configurações mencionadas neste guia.

### Personalização do canal da Web

- [Introdução ao canal da Web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [Criar experiências da Web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [Configuração do canal da Web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/web-configuration)

### Canais no aplicativo e de cartão de conteúdo

- [Visão geral do canal no aplicativo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/get-started-in-app)
- [Pré-requisitos do canal no aplicativo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/inapp-configuration)
- [Criar mensagens no aplicativo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/create-in-app)
- [Canal de cartão de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/get-started-content-card)
- [Configuração do cartão de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/content-card-configuration)
- [Criar cartões de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/create-content-card)

### Gerenciamento de decisão

- [Visão geral da Gestão de decisões](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Criar inserções](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Criar regras de decisão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crie ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Criar ofertas substitutas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Criar coleções](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Criar decisões](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estratégias de classificação](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [Entregar ofertas em mensagens](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### Personalization e conteúdo

- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxe do Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Funções auxiliares](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabalhar com modelos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabalhar com fragmentos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)

### Públicos-alvo e segmentação

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentação de borda](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Segmentação de transmissão](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Referência do Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### Identidade e perfil

- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Visão geral dos namespaces de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/namespaces)
- [Regras de vinculação do gráfico de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [Visão geral do perfil](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### Coleta de dados e SDK

- [Visão geral do Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Instalar o Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
- [Visão geral do Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Configurar sequências de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Visão geral da API do Edge Network Server](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)

### Campanhas e experimentação

- [Introdução às campanhas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Criar uma campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Introdução ao experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Criar um experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Relatório de experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)

### Atributos computados e enriquecimento

- [Visão geral de atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Guia da interface de atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)
- [Visão geral do Customer AI](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### Relatórios e análises

- [Relatório em tempo real da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Relatório global da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Guia de integração do AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Visão geral do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Visão geral do Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

### Governança e privacidade

- [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Consentimento no Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [Visão geral do gerenciamento avançado do ciclo de vida dos dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)

### Medidas de proteção

- [Medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Medidas de proteção do serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)
