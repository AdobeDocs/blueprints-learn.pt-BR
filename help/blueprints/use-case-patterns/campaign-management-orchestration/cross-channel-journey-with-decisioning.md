---
title: Jornada entre canais com decisão
description: Saiba como orquestrar uma jornada de várias etapas, incorporando a decisão em tempo real para selecionar o canal, conteúdo ou oferta ideal.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: eabdd91f-bb7d-4de3-adb5-5940d3ca4a78
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '9029'
ht-degree: 2%

---

# Jornada entre canais com decisão

Este guia fornece uma referência completa de implementação para jornada entre canais com decisão. Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam orquestrar jornadas de várias etapas e vários canais que incorporam decisões em tempo real em um ou mais nós de jornada.

Use este guia para entender o panorama completo das opções de implementação, avaliar compensações e navegar até a documentação relevante do Experience League para obter instruções detalhadas de configuração.

A jornada entre canais com decisão é o padrão de orquestração de campanha mais sofisticado no ecossistema [!DNL Adobe Experience Platform]. Ele estende jornadas orquestradas de várias etapas incorporando decisões em tempo real — usando a Decisão [!DNL AJO] para avaliar o contexto atual de um perfil e selecionar dinamicamente o canal, conteúdo ou oferta ideal em um ou mais pontos de decisão na tela de jornada.

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
**KPIs:** Envolvimento, Taxas de Conversão, Satisfação do Cliente (CSAT)

**[Aumente a fidelidade do cliente e o valor vitalício](../../business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)**
Aprofunde as relações com o cliente e maximize o valor a longo prazo por meio de programas de fidelidade, recompensas e envolvimento personalizado.
**KPIs:** Valor vitalício do cliente, Retenção, % de venda adicional/venda cruzada

**[Melhore a retenção do cliente](../../business-objectives/customer-experience/improve-customer-retention.md)**
Mantenha os clientes existentes envolvidos e renovando-os por meio de experiências orientadas por valores e estimulação contínua do relacionamento.
**KPIs:** Retenção, Valor vitalício do cliente, Participação

**[Impulsionar vendas cruzadas e vendas adicionais](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)**
Promova produtos ou serviços complementares e premium para os clientes existentes com base no histórico de comportamento e de compras.
**KPIs:** % de venda adicional/venda cruzada, receita incremental, valor vitalício do cliente

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

## Padrão do caso de uso

**jornada entre canais com decisão**

Orquestrar uma jornada multicanal de várias etapas que incorpora a decisão em tempo real em um ou mais nós para selecionar o canal, o conteúdo ou a oferta ideal.

**Cadeia de funções:** Avaliação de público-alvo > Execução de Jornada > Nó de decisão > Seleção de canal > Entrega de mensagem > Relatórios

## Aplicativos

Os aplicativos a seguir são usados para implementar esse padrão de caso de uso.

- **[!DNL Adobe Journey Optimizer] ([!DNL AJO])** — orquestração de Jornadas (design de tela de várias etapas, condições de entrada, esperas, condições, critérios de saída), criação de mensagens entre canais, configuração da superfície de canal, gerenciamento de conflitos e prioridades
- **[!DNL Adobe Journey Optimizer]Decisão** — Gerenciamento de oferta e item de conteúdo, regras de elegibilidade, estratégias de classificação (prioridade, fórmula, IA), políticas de decisão, posicionamentos, ofertas de fallback
- **[!DNL Adobe Real-Time Customer Data Platform] ([!DNL RT-CDP])** — Avaliação de público para entrada de jornada e segmentos de qualificação de oferta, enriquecimento de perfil com atributos computados e pontuações de propensão, consentimento e imposição de governança
- **[!DNL Adobe Experience Platform] ([!DNL AEP])** — armazenamento de Perfil do Cliente em Tempo Real, Serviço de Identidade para resolução entre canais, modelagem de dados e infraestrutura de assimilação

## Funções básicas

Os seguintes recursos básicos devem estar em vigor para esse padrão de caso de uso. Para cada função, o status indica se ele é tipicamente necessário, se presume ser pré-configurado ou se não é aplicável.

| Função de base | Status | O que deve estar em vigor | Referência do Experience League |
| --- | --- | --- | --- |
| Administração e governança | Presumido em vigor | [!DNL AJO] sandbox com permissões de jornada, campanha e decisão configuradas. Superfícies de canal para todos os canais de entrega possíveis. Funções de usuário para designers de jornada, gerentes de decisão e autores de conteúdo. | [Visão geral das sandboxes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/home), [Visão geral do controle de acesso](https://experienceleague.adobe.com/pt-br/docs/experience-platform/access-control/home) |
| Preparação e modelagem de dados | Obrigatório | O esquema de perfil deve incluir atributos usados para a tomada de decisão (por exemplo, nível de fidelidade, histórico de compras, preferências de canal, pontuações de engajamento). Os esquemas de catálogo de oferta e item de decisão devem ser configurados. Os esquemas ExperienceEvent devem capturar sinais comportamentais usados por regras de elegibilidade e fórmulas de classificação. | [Visão geral do sistema XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/home), [noções básicas de composição de esquema](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/schema/composition) |
| Fontes de dados e coleção | Presumido em vigor | Os atributos de perfil e os sinais comportamentais usados pela decisão devem ser atuais. A transmissão de eventos em tempo real é necessária se a jornada usar critérios de entrada ou saída acionados por eventos. O Web SDK, o Mobile SDK ou a coleção do lado do servidor devem estar ativos para canais que alimentam o contexto de decisão. | [Visão geral do Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/web-sdk/home), [Visão geral das fontes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/home) |
| Configuração de identidade e perfil | Obrigatório | A resolução de identidade entre canais é essencial: a jornada deve resolver perfis em e-mail, push, SMS e Web. As políticas de mesclagem devem produzir um perfil unificado para a tomada de decisão. Os namespaces de identidade para todos os identificadores do cliente (CRM ID, email, ECID, telefone) devem ser configurados. | [Visão geral do Serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/home), [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/merge-policies/overview) |
| Definição e segmentação do público-alvo | Obrigatório | Definição de público-alvo de entrada para a jornada. Segmentos adicionais usados para regras de elegibilidade de oferta e ramificação de condição na jornada. O método de avaliação deve corresponder aos requisitos de latência (streaming para entrada em tempo real, lote para agendamento). | [Visão geral do Serviço de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/home), [guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-builder) |

## Funções de suporte

Os recursos a seguir aumentam esse padrão de caso de uso, mas não são necessários para a execução principal.

| Função de suporte | Status | Por que é importante | Referência do Experience League |
| --- | --- | --- | --- |
| Criação de atributo calculado/derivado | Recomendado | Atributos computados, como pontuações de propensão da IA do cliente, pontuações de engajamento, pontuações de preferência de canal e cálculos do valor vitalício, melhoram significativamente a qualidade da decisão. Esses atributos de perfil enriquecidos permitem regras de elegibilidade e fórmulas de classificação mais sofisticadas. | [Visão geral dos atributos computados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/computed-attributes/overview), [Visão geral da IA do cliente](https://experienceleague.adobe.com/pt-br/docs/experience-platform/intelligent-services/customer-ai/overview) |
| Gerenciamento do ciclo de vida dos dados | Recomendado | O histórico de ofertas e os dados de eventos de decisão se acumulam com o tempo e devem ter políticas de retenção. A aplicação de consentimento em vários canais é essencial — perfis sem consentimento válido para um canal devem ser excluídos do caminho de entrega desse canal. | [Visão geral do Gerenciamento Avançado do Ciclo de Vida dos Dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-lifecycle/home), [Consentimento no Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted) |
| Rotulagem e aplicação de uso de dados | Recomendado | A aplicação de governança em vários canais e tipos de oferta é importante quando a decisão pode rotear perfis para diferentes canais com diferentes restrições de uso de dados. Garante a entrega de ofertas em conformidade em todos os canais. | [Visão geral da governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/home), [Imposição de política](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/enforcement/overview) |
| Monitoramento e capacidade de observação | Incluído | O monitoramento de jornada e decisão é essencial para as operações de produção. Alertas de falhas de entrada de jornada, picos de fallback de decisão e erros de delivery permitem a resolução rápida de problemas. | [Visão geral dos alertas](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/alerts/overview), [Visão geral dos Insights de observação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/home) |
| Relatórios e análise | Incluído | Os relatórios de jornada e decisão são abordados na fase de relatório. A análise da eficácia da decisão do CJA, a otimização da combinação de canais, o desempenho da oferta e o ROI da jornada fornecem os insights necessários para refinar as estratégias de classificação e otimizar a jornada ao longo do tempo. | [visão geral do CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-overview/cja-overview), [guia de integração do AJO + CJA](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/reporting/channel-report/cja-ajo) |

## Funções do aplicativo

Este plano utiliza as seguintes funções do catálogo de funções do aplicativo. As funções são mapeadas para fases de implementação em vez de etapas numeradas.

### [!DNL Journey Optimizer] ([!DNL AJO])

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Configuração de canais | Fase 2: configuração de canal | Configurar superfícies dos canais para todos os canais que a decisão pode selecionar ou que a jornada usa (email, SMS, push, no aplicativo) |
| Criação de mensagens | Fase 4: Criação de mensagens | Crie conteúdo de mensagem para cada canal e integre a saída de decisão: disposições de ofertas, blocos de conteúdo dinâmico, tokens de personalização de ofertas selecionadas |
| Decisão. | Fase 3: Configuração da decisão | Configure itens de oferta, regras de qualificação, estratégias de classificação, políticas de decisão e ofertas de fallback para cada ponto de decisão na jornada |
| Journey Orchestration | Fase 5: Design e ativação da Jornada | Projete a tela de jornada de várias etapas com condições de entrada, nós de decisão, roteamento de canal, etapas de espera, ações de mensagem e critérios de saída |
| Gerenciamento de conflitos e prioridades | Fase 5: Design e ativação da Jornada | Configure pontuações de prioridade e detecção de conflitos se várias jornadas puderem direcionar os mesmos perfis simultaneamente |
| Frequência e regras de negócios | Fase 5: Design e ativação da Jornada | Imponha limites de frequência de mensagem entre canais para evitar mensagens excessivas na jornada de vários canais |
| Relatórios e análise de desempenho | Fase 6: Relatórios e monitoramento | Monitorar a jornada e as métricas de entrega por nó, o desempenho da decisão e o engajamento no canal |

### [!DNL Real-Time CDP] ([!DNL RT-CDP])

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Avaliação de público | Fase 1: Avaliação de público-alvo | Defina e avalie o público-alvo de entrada ou o evento de entrada qualificado; crie segmentos de qualificação usados pela decisão |
| Enriquecimento de perfil | Pré-requisito / Suporte | Enriqueça os perfis com atributos computados e pontuações de propensão que melhoram a qualidade da decisão |
| Consentimento e aplicação de governança | Fase 2: configuração de canal | Impor preferências de consentimento em todos os canais; garantir a entrega de ofertas em conformidade |

## Pré-requisitos

Conclua o seguinte antes de iniciar a implementação.

- [ A sandbox ] [!DNL AJO] está provisionada com os recursos de orquestração e decisão de jornada habilitados
- [ ] Todos os canais de destino (email, SMS, push) têm superfícies de canal ativas e verificadas
- [ ] O esquema de perfil inclui atributos necessários para a tomada de decisão (nível de fidelidade, histórico de compras, preferências de canal, pontuações de engajamento)
- [ ] A resolução de identidade entre canais está configurada — os perfis podem ser resolvidos por email, token de push, número de telefone e identificadores da Web
- [ ] O público de entrada é definido e avaliado com uma população diferente de zero
- [ ] O conteúdo do catálogo de ofertas (ativos criativos, cópia, avisos de isenção legal) está aprovado e pronto para configuração
- [ ] Os dados de consentimento estão sendo assimilados e a imposição de consentimento está ativa para todos os canais de destino
- [ ] modelos e fragmentos de conteúdo para cada canal foram criados e aprovados
- [ ] As regras de limite de frequência são definidas e implantadas se a organização tiver políticas de frequência entre campanhas
- [ ] Se estiver usando uma decisão classificada por IA, existem no mínimo 1.000 eventos de conversão para o treinamento de modelo

## Opções de implementação

Analise as opções a seguir e selecione a abordagem que melhor atenda aos seus requisitos.

### Opção A: Jornada com o Offer Decisioning (canal fixo, conteúdo dinâmico)

**Recomendado para:** Jornadas em que a sequência de canal é predeterminada, mas o conteúdo ou a oferta em cada ponto de contato deve ser selecionado dinamicamente: jornadas de fidelidade com recompensas personalizadas, reengajamento com incentivos dinâmicos, criação de ciclo de vida com recomendações de conteúdo classificado por IA.

#### Como funciona

A tela de jornada define a sequência fixa de canais e tempo (por exemplo, Dia 0: Email, Dia 3: Push, Dia 7: SMS). Em cada nó de ação de mensagem, uma política de decisão seleciona a melhor oferta ou conteúdo a ser incluído na mensagem a partir de um catálogo configurado de itens elegíveis. As ofertas são gerenciadas no catálogo de decisão [!DNL AJO] com regras de elegibilidade que filtram quais ofertas um perfil se qualifica e estratégias de classificação que determinam qual oferta elegível é a melhor opção.

Essa abordagem separa o &quot;quando e onde&quot; (orquestração de jornadas) do &quot;o que&quot; (decisão). O designer de jornadas controla o fluxo do canal, enquanto o gerente de decisões controla o catálogo de ofertas, as regras de elegibilidade e a lógica de classificação de maneira independente. Essa separação de interesses torna a implementação mais sustentável e permite que o catálogo de ofertas evolua sem modificar a tela de jornada.

Os posicionamentos de oferta são incorporados diretamente ao conteúdo da mensagem usando o Designer de email ou outros editores de canal. Quando a mensagem é renderizada no momento do delivery, o mecanismo de decisão avalia a qualificação e a classificação do perfil para selecionar a oferta ideal para cada posicionamento na mensagem.

#### Principais considerações

- A sequência de canais é estática — todos os perfis seguem o mesmo caminho de canal, independentemente de suas preferências
- A complexidade da decisão é menor, pois seleciona apenas conteúdo/ofertas, não canais
- O catálogo de ofertas pode ser gerenciado independentemente da jornada
- As ofertas substitutas devem ser configuradas para cada posicionamento para lidar com perfis sem ofertas personalizadas elegíveis

#### Vantagens

- Tela de jornada mais simples — sem lógica de ramificação para seleção de canal
- Separação clara de preocupações entre o design da jornada e o gerenciamento de ofertas
- Mais fácil de testar e validar — cada caminho de canal é determinístico
- Menor complexidade de implementação e tempo de entrada no mercado mais rápido
- As alterações no catálogo de ofertas entram em vigor imediatamente sem modificações na jornada

#### Limitação

- Não é possível adaptar o canal com base no comportamento ou nas preferências do perfil individual
- Os perfis que preferem um canal a outro ainda recebem mensagens nos canais predeterminados
- Não otimiza as taxas de engajamento no nível do canal

#### Referências do Experience League

- [Entregar ofertas em mensagens](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Visão geral da Gestão de decisões](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)

### Opção B: Jornada com seleção de canal dinâmico (conteúdo fixo, canal dinâmico)

**Recomendado para:** Jornadas em que o conteúdo em cada ponto de contato é semelhante, mas o canal deve ser selecionado dinamicamente com base no contexto do perfil — retorno adaptável (email vs. push vs. SMS com base no engajamento), programas de próxima melhor ação em que a otimização do canal é a meta principal.

#### Como funciona

A jornada usa nós de condição informados por atributos de perfil (como pontuações de preferência de canal, canal de último engajamento ou status de consentimento) ou saída de decisão para rotear perfis para diferentes caminhos de canal. Cada caminho fornece conteúdo específico do canal por meio de seu próprio nó de ação de mensagem. A lógica de decisão determina qual canal tem maior probabilidade de obter engajamento com base no histórico comportamental do perfil.

A seleção de canal pode ser implementada usando nós de condição de jornada com avaliações de atributo de perfil (por exemplo, se `channelPreference = "push"` rotear para o caminho de push), ou usando decisões com itens específicos de canal, onde cada &quot;oferta&quot; representa um canal e a estratégia de classificação determina o melhor canal.

Essa abordagem otimiza o canal de entrega, mantendo o conteúdo relativamente consistente entre os canais. Ele requer que o conteúdo da mensagem seja criado para cada canal possível, e as superfícies dos canais devem ser configuradas para todos os canais candidatos.

#### Principais considerações

- Exige variantes de conteúdo de mensagem para cada canal candidato
- As superfícies do canal devem estar ativas para todos os canais possíveis
- A lógica de condição ou a configuração de decisão deve levar em conta o consentimento — perfis sem consentimento por SMS não podem ser roteados para o caminho SMS
- A tela de Jornada é mais complexa com caminhos de ramificação para cada canal

#### Vantagens

- Otimiza a seleção de canais para cada perfil individual
- Aumenta o engajamento geral, atingindo perfis em seu canal preferido
- Respeita o consentimento específico do canal automaticamente por meio do roteamento com reconhecimento de consentimento
- Pode incorporar o histórico de engajamento e as pontuações de preferência de canal nas decisões de roteamento

#### Limitação

- Tela de jornada mais complexa com várias ramificações de canal
- O conteúdo deve ser criado separadamente para cada canal (embora a intenção da mensagem seja a mesma)
- Difícil de testar — deve validar todos os caminhos de canal possíveis
- A personalização de conteúdo em cada canal é estática (sem offer decisioning)

#### Referências do Experience League

- [Atividade de condição](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Criar uma jornada](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)

### Opção C: jornada adaptável completa (canal dinâmico + conteúdo dinâmico)

**Recomendado para:** Personalização máxima — o canal e o conteúdo/oferta são selecionados dinamicamente em cada nó. Adequado para segmentos de clientes de alto valor, sofisticados programas de fidelidade e organizações com práticas de decisão maduras e dados de perfil avançados.

#### Como funciona

Esta opção combina as Opções A e B. A jornada usa a decisão em dois níveis: primeiro, para determinar qual canal usar para cada ponto de contato, e segundo, para determinar qual conteúdo ou oferta fornecer no canal selecionado. Cada ponto de decisão na jornada avalia o contexto atual do perfil para fazer a seleção do canal e do conteúdo.

A implementação exige uma configuração de decisão abrangente com políticas de decisão para seleção de canal e seleção de conteúdo/oferta. A seleção de canal pode usar uma política de decisão em que cada item representa um canal com regras de qualificação baseadas em consentimento e envolvimento, enquanto a seleção de conteúdo usa uma política de decisão separada com itens de oferta classificados por relevância.

Essa é a variante mais complexa e requer a integração mais profunda entre a orquestração e a tomada de decisões do jornada. Ele fornece o mais alto grau de personalização, mas também exige o máximo de configuração, testes e gerenciamento contínuo.

#### Principais considerações

- Requer duas camadas de decisão — seleção de canal e seleção de conteúdo
- A complexidade da tela de jornada é mais alta com ramificação e decisão aninhadas em cada nó
- São necessários testes abrangentes em todas as combinações possíveis de conteúdo de canal
- Exige dados avançados de perfil (histórico de engajamento, preferências de canal, afinidade de produtos, pontuações de propensão) para decisões eficazes
- A decisão classificada por IA se beneficia significativamente dos atributos computados

#### Vantagens

- Personalização máxima — cada ponto de contato é otimizado para canal e conteúdo
- Melhor potencial de envolvimento e conversão para implementações bem configuradas
- Centraliza toda a lógica de personalização na decisão em vez de ramificações de jornada estáticas
- Pode melhorar continuamente por meio do aprendizado do modelo de classificação de IA

#### Limitação

- Maior complexidade de implementação e maior tempo de entrada no mercado
- Requer o catálogo de ofertas e a preparação de conteúdo do canal mais abrangentes
- Solução de problemas mais difícil quando surgem problemas de entrega
- Exige uma infraestrutura de dados madura com atributos de perfil avançados
- A classificação de IA requer volume de evento de conversão suficiente para o treinamento de modelo

#### Referências do Experience League

- [Visão geral da Gestão de decisões](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Estratégias de classificação](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Comparação de opções

Use a tabela a seguir para comparar as três opções de implementação rapidamente.

| Critérios | Opção A: Offer Decisioning | Opção B: Canal dinâmico | Opção C: Adaptável total |
| --- | --- | --- | --- |
| Melhor para | Sequência de canal fixa, conteúdo dinâmico | Otimização de canal, conteúdo consistente | Personalização máxima em ambas as dimensões |
| Complexo | Médio | Medium-Alto | Alta |
| Tela da jornada | Simples (linear com a decisão em nós de ação) | Moderado (ramificação para caminhos de canal) | Complexo (ramificação aninhada com decisão de vários níveis) |
| Escopo da decisão | Somente seleção de conteúdo/oferta | Somente seleção de canal | Seleção de canal e conteúdo |
| Requisitos de conteúdo | Um conjunto de conteúdo por canal (com disposições de oferta) | Conteúdo para cada canal candidato | Conteúdo com disposições de oferta para cada canal candidato |
| Necessidades de dados do perfil | Moderado (atributos de qualificação da oferta) | Moderado (preferência de canal, envolvimento) | Alto (atributos de canal e oferta) |
| Tempo de entrada no mercado | Mais rápido | Moderado | Mais longo |
| Gerenciamento contínuo | Gerenciamento de catálogo de ofertas | Gerenciamento da lógica de roteamento de canal | Catálogo de ofertas e roteamento de canal |
| Profundidade do Personalization | O conteúdo varia, canal fixo | O canal varia, conteúdo semelhante | O canal e o conteúdo variam |

### Escolha a opção certa

Use as orientações a seguir para determinar a melhor opção para sua situação.

- **Comece com a Opção A** se sua estratégia de canal já estiver definida (por exemplo, &quot;sempre enviamos email primeiro, depois push, depois SMS&quot;) e a principal necessidade de personalização é selecionar a oferta ou o conteúdo correto em cada ponto de contato. Esse é o ponto de partida mais comum para organizações novatas na tomada de decisões.

- **Escolha a Opção B** se a otimização de canal for a sua meta principal: você deseja alcançar cada cliente no canal com o qual ele tem maior probabilidade de se envolver, mas o conteúdo da mensagem é relativamente consistente em todos os canais. Isso requer dados de preferência de canal em perfis.

- **Escolha a Opção C** somente quando tiver uma infraestrutura de decisão madura, dados de perfil avançados (incluindo atributos computados e pontuações de propensão), um catálogo de ofertas bem preenchido e a capacidade organizacional para gerenciar a complexidade. Muitas organizações começam com a Opção A ou B e evoluem para a Opção C à medida que sua maturidade de decisão aumenta.

- **Se você não tiver certeza**, comece com a Opção A. Ele fornece personalização significativa com a menor complexidade, e o catálogo de ofertas criado para a Opção A é diretamente reutilizável se você evoluir posteriormente para a Opção C.

## Fases de implementação

As fases a seguir abordam a implementação completa desse padrão de caso de uso.

### Fase 1: Avaliação do público-alvo

**Função do aplicativo:** [!DNL RT-CDP]: Avaliação de público-alvo

Essa fase configura o público-alvo de entrada que determina quais perfis entram na jornada e quaisquer segmentos adicionais usados para regras de elegibilidade de oferta ou ramificação de condição dentro da jornada. A definição do público-alvo é a base de toda a lógica de jornada e decisão downstream.

#### Decisão: Tipo de entrada

Como os perfis devem entrar na jornada por meio de uma leitura de público agendada ou um acionador de evento em tempo real?

>[!NOTE]
>Selecione um tipo de entrada com base nos requisitos de tempo e acionamento da jornada.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Ler público-alvo (entrada em lote) | Programas de ciclo de vida, jornadas de fidelidade, campanhas de reengajamento programadas | Os perfis entram em lotes em horários programados; o público-alvo é avaliado em tempo de leitura; oferece suporte a grandes tamanhos de público-alvo |
| Qualificação de público-alvo (transmissão) | Jornadas acionadas por comportamento em que a entrada ocorre quando um perfil entra ou sai de um segmento | Entrada quase em tempo real; requer definição de segmento elegível para transmissão; ideal para jornadas baseadas em marcos |
| Evento unitário (acionador de evento) | Um evento específico deve acionar a jornada (por exemplo, compra, abandono de carrinho, registro) | Entrada em tempo real no evento; requer configuração do esquema do evento; limitado a 5.000 eventos/segundo |

#### Decisão: método de avaliação do público-alvo

Com que rapidez o público-alvo deve qualificar perfis?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Lote | Atualizações diárias ou periódicas do público são suficientes; jornadas programadas no estilo da campanha | Processa até 24 milhões de perfis por trabalho; com base em agendamento; a maioria das expressões de regra de segmento é compatível |
| Streaming | A associação de público-alvo em tempo real é necessária para a entrada acionada por eventos ou por qualificação | Quase em tempo real; conjunto de funções de regra de segmento limitado; sem agregações baseadas em tempo |
| Edge | Qualificação necessária na mesma sessão | Latência de milissegundos; somente verificações de atributos simples; limitada aos atributos do perfil de borda |

#### Principais detalhes de configuração

**Navegação da interface do usuário:** Cliente > Públicos-alvo > Criar público-alvo > Criar regra

- Defina o público-alvo de entrada usando o Construtor de segmentos com expressões de regra de segmento direcionadas aos atributos de perfil e eventos comportamentais relevantes
- Crie segmentos de elegibilidade adicionais se as regras de elegibilidade da oferta referenciarem a associação ao segmento (por exemplo, &quot;Clientes de alto valor&quot;, &quot;Nível ouro de fidelidade&quot;)
- Verifique se a população do público-alvo é diferente de zero antes de prosseguir para a configuração do jornada
- Selecione a política de mesclagem que produz a exibição de perfil unificada necessária para a tomada de decisão

#### Documentação do Experience League

- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentação de transmissão](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentação de borda](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Referência do Profile Query Language](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/pql/overview)

### Fase 2: configuração de canal

**Função de aplicativo:** [!DNL AJO]: Configuração de canal

Essa fase configura superfícies de canal para cada canal que a jornada pode usar na entrega de mensagens. Todos os canais candidatos devem ter superfícies ativas e verificadas antes que as mensagens possam ser criadas ou que a jornada possa ser publicada. Para esse padrão, você normalmente configurará no mínimo superfícies para email, SMS e push — e possivelmente no aplicativo ou na Web se a decisão puder selecionar esses canais.

#### Decisão: quais canais devem ser configurados

Quais canais são candidatos à jornada — como etapas de jornada fixas (Opções A/B) ou como canais selecionáveis pela decisão (Opções B/C)?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Somente email | Jornada de canal único com Offer Decisioning (opção A, somente email) | Configuração mais simples; requer delegação de subdomínio e aquecimento de IP |
| Email + Push | Jornada de dois canais; comum para jornadas focadas em engajamento | O push requer credenciais APNs/FCM; o aplicativo móvel deve ter o SDK integrado |
| Email + SMS + Push | Jornada completa entre canais; mais comum para as Opções B e C | O SMS requer credenciais de provedor (Sinch, Twilio, Infobip); cada canal precisa de sua própria superfície |
| Email + SMS + Push + No aplicativo | Cobertura máxima dos canais, incluindo superfícies na sessão | O aplicativo exige SDK móvel e configuração de superfície de aplicativo |

#### Decisão: método de delegação de subdomínio (email)

Como o subdomínio de envio deve ser delegado à Adobe?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Delegação completa | A organização deseja que a Adobe gerencie todos os registros DNS para o subdomínio de envio | Configuração mais simples; o Adobe lida com SPF, DKIM, DMARC; menos controle sobre DNS |
| Delegação CNAME | A organização precisa manter o controle dos registros DNS | Configuração mais complexa; o cliente gerencia o DNS; oferece mais flexibilidade |

#### Principais detalhes de configuração

**Navegação da interface do usuário:** Administração > Canais > Superfícies de canal > Criar superfície

- Para email: configurar subdomínio, pool de IP, nome do remetente, endereço de resposta e manipulação de cancelamento de inscrição
- Para SMS: configurar credenciais do provedor de SMS e número do remetente
- Para push: configurar APNs e credenciais FCM para iOS e Android
- Verifique se cada superfície está com o status Ativo antes de continuar
- Confirmar se a ativação de IP foi concluída para IPs de envio de email

#### Documentação do Experience League

- [Introdução à configuração de email](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegar subdomínios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Criar pools de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [Configurar canal de SMS](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configurar canal de notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Fase 3: Configuração da decisão

**Função de aplicativo:** [!DNL AJO]: decisão

Essa fase configura a estrutura de decisão completa, incluindo disposições, regras de elegibilidade, ofertas personalizadas, ofertas substitutas, qualificadores de coleção, coleções, estratégias de classificação e políticas de decisão. Essa fase cria a lógica de decisão que será chamada nos pontos de decisão da jornada.

#### Decisão: Escopo da decisão

O que a decisão deve selecionar — ofertas/conteúdo (opção A), canais (opção B) ou ambos (opção C)?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Somente seleção de oferta/conteúdo | A sequência de canais é fixa; a personalização está no conteúdo | As políticas de decisão visam itens de oferta com representações de conteúdo por posicionamento |
| Somente seleção de canal | O conteúdo é consistente; a otimização está no canal de delivery | Os itens de decisão representam canais; a qualificação inclui verificações de consentimento; a classificação usa dados de envolvimento |
| Canal e conteúdo | Personalização totalmente adaptável em canais e conteúdo | Requer duas camadas de políticas de decisão: a mais complexa, mas a mais alta personalização |

#### Decisão: estratégia de classificação

Como as ofertas elegíveis devem ser classificadas para selecionar a melhor?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Baseado em prioridade (manual) | Classificação simples em que as regras de negócios determinam a importância da oferta | Cada oferta recebe uma pontuação de prioridade; vitórias de prioridade mais alta; determinística e fácil de entender |
| Baseado em fórmula (expressão personalizada) | A classificação deve considerar os atributos do perfil (por exemplo, CLV, nível, pontuação de afinidade) | A fórmula de classificação personalizada avalia o contexto do perfil; mais dinâmico que a prioridade; sem ML necessário |
| Classificado por IA (otimização automática) | A classificação deve ser otimizada automaticamente com base nos dados históricos de conversão | O modelo de IA aprende com eventos de conversão; requer no mínimo 1.000 eventos para treinamento; melhora continuamente |

#### Decisão: Limite de oferta

Deve haver limites para quantas vezes uma oferta é exibida?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Limite por perfil | Impedir que a mesma oferta seja exibida repetidamente no mesmo perfil | Protege contra a fadiga da oferta; contra atraso possível sob alta taxa de transferência |
| Limite global | Limitar o total de impressões em todos os perfis (por exemplo, promoções de estoque limitadas) | Controla a exposição total; útil para ofertas com suprimento limitado |
| Sem limite | Cada impressão elegível deve mostrar a oferta | Simples; apropriado para conteúdo permanente ou ofertas ilimitadas |

#### Principais detalhes de configuração

**Navegação da interface do usuário:** Componentes > Gerenciamento de decisão > Posicionamentos / Ofertas / Decisões

- Crie inserções para cada combinação de canal e tipo de conteúdo (por exemplo, banner de HTML de email, push JSON, texto SMS)
- Defina regras de elegibilidade usando expressões de regra de segmento que referenciam atributos de perfil ou associação de público-alvo
- Crie ofertas personalizadas com representações para cada posicionamento, atribua regras de elegibilidade e defina a prioridade
- Criar uma oferta substituta que abranja todos os posicionamentos; isso é retornado quando nenhuma oferta personalizada é qualificada
- Organizar ofertas em coleções usando qualificadores de coleção (tags)
- Configurar estratégia de classificação — baseada em prioridade, em fórmula ou classificada por IA
- Criar políticas de decisão que vinculam posicionamentos, coleções, estratégia de classificação e oferta substituta
- Aprovar todas as ofertas antes que possam ser selecionadas por decisão

#### Onde as opções divergem

**Para a Opção A (Offer Decisioning):**
Crie inserções e ofertas com foco na personalização de conteúdo em cada canal (por exemplo, oferta de banner principal de email, oferta de rodapé de email, oferta de corpo de notificação por push). As políticas de decisão selecionam o melhor conteúdo para cada posicionamento na mensagem.

**Para a Opção B (Seleção de Canal Dinâmico):**
Crie itens de decisão que representam cada canal. As regras de elegibilidade incluem verificações de consentimento (por exemplo, um perfil deve ter consentimento por SMS para se qualificar para o item de SMS). A classificação usa pontuações de engajamento de canal ou expressões baseadas em fórmula.

**Para a Opção C (Adaptável Completo):**
Configure duas camadas de decisão: um conjunto de políticas de decisão para a seleção de canal e um conjunto separado para a seleção de conteúdo/oferta no canal selecionado. Ambas as camadas exigem disposições, ofertas, regras de elegibilidade e estratégias de classificação.

#### Documentação do Experience League

- [Visão geral da Gestão de decisões](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Criar inserções](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Criar regras de decisão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crie ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Criar ofertas substitutas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Criar coleções](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Criar decisões](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estratégias de classificação](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Fase 4: criação de mensagens

**Função de aplicativo:** [!DNL AJO]: Criação de Mensagem

Essa fase configura o conteúdo da mensagem para cada canal e ponto de contato na jornada, integrando a saída da decisão (conteúdo de oferta selecionado) aos modelos de mensagem. Cada nó de ação de mensagem na jornada exige conteúdo criado com a superfície de canal apropriada, tokens de personalização e integrações de posicionamento de ofertas.

#### Decisão: abordagem de conteúdo

Como o conteúdo da mensagem deve ser criado para cada canal?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Baseado em modelo | A organização estabeleceu modelos de marca; a consistência é importante | Criação mais rápida; garante a consistência da marca; pode limitar a flexibilidade do design |
| Criar do zero | Criativo exclusivo para esta jornada; sem modelos existentes | Controle completo do design; tempo de criação mais longo; use o arrastar e soltar do Email Designer |
| Importar HTML | A equipe da Creative produz o HTML externamente; importe para [!DNL AJO] | Preserva o fluxo de trabalho de design externo; requer compatibilidade do HTML com o Designer de email |

#### Decisão: escopo do Personalization

Que nível de personalização as mensagens devem incluir além do resultado da decisão?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Personalização básica (nome, saudação) | Necessidades de personalização mínimas além da seleção de oferta | Expressões Handlebars simples; baixa complexidade |
| Blocos de conteúdo condicional | Seções de conteúdo diferentes para segmentos ou atributos diferentes | Usa regras de conteúdo dinâmico; o conteúdo varia de acordo com o atributo de perfil ou a associação de segmento |
| Personalização completa com integração de decisão | Posicionamentos de oferta incorporados à mensagem, combinados com personalização baseada em perfil | Combina a saída do Offer Decisioning com tokens de personalização Handlebars; experiência mais avançada |

#### Principais detalhes de configuração

**Navegação da interface do usuário:** Selecione uma ação de campanha ou jornada > Editar conteúdo > Email Designer / Editor de canal

- Crie conteúdo de mensagem para cada canal usado na jornada (email, SMS, push, no aplicativo)
- Incorpore disposições de decisões de oferta no conteúdo da mensagem em que as ofertas selecionadas para decisão devem aparecer
- Adicionar expressões de personalização usando a sintaxe Handlebars para atributos de perfil (por exemplo, `{{profile.person.name.firstName}}`)
- Configurar blocos de conteúdo condicional para mensagens específicas do segmento
- Criar fragmentos de conteúdo reutilizáveis para elementos compartilhados (cabeçalhos, rodapés, avisos de isenção legal)
- Visualize e teste com perfis de amostra para verificar se a personalização é renderizada corretamente
- Enviar mensagens de prova para revisão das partes interessadas

#### Onde as opções divergem

**Para a Opção A (Offer Decisioning):**
Cada mensagem inclui disposições de oferta em que o conteúdo selecionado para decisão é exibido. O layout da mensagem é consistente, mas a área de oferta mostra dinamicamente a melhor oferta para cada perfil.

**Para a Opção B (Seleção de Canal Dinâmico):**
Cada canal tem seu próprio conteúdo de mensagem criado separadamente. O conteúdo é semelhante nos canais, mas adaptado às restrições do canal (HTML por email vs. texto SMS vs. formato de notificação por push).

**Para a Opção C (Adaptável Completo):**
Cada canal tem seu próprio conteúdo de mensagem com disposições de ofertas incorporadas. O canal e o conteúdo da oferta nesse canal são selecionados dinamicamente.

#### Documentação do Experience League

- [Criar conteúdo de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Entregar ofertas em mensagens](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Trabalhar com modelos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabalhar com fragmentos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Criar uma mensagem SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/create-sms)
- [Criar uma notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/design-push)

### Fase 5: Design e ativação da Jornada

**Função do aplicativo:** [!DNL AJO]: Journey Orchestration, [!DNL AJO]: Gerenciamento de Conflitos e Prioridades, [!DNL AJO]: Frequência e Regras de Negócios

Essa fase configura a tela de jornada completa, incluindo configuração de entrada, nós de decisão vinculados às políticas de decisão configuradas, divisões de condição para roteamento de canal (Opções B/C), nós de ação de mensagem para cada caminho de canal, nós de espera entre pontos de contato, critérios de saída, configurações de conflito/prioridade e regras de limite de frequência. Essa fase reúne todos os componentes configurados anteriormente no fluxo de jornada orquestrado e o ativa.

#### Decisão: política de reentrada

Os perfis podem entrar novamente na jornada depois de concluir ou sair?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Permitir reentrada (com lista de opções) | Jornadas recorrentes nas quais os perfis podem se qualificar novamente (por exemplo, renovação trimestral de fidelidade) | Defina um período de controle (mínimo de 5 minutos) para evitar reentrada imediata; o perfil é reiniciado desde o início |
| Sem reentrada | Jornadas únicas em que cada perfil deve atravessar apenas uma vez (por exemplo, integração) | O perfil não pode ser reinserido após a conclusão ou sair; comportamento mais simples |

#### Decisão: critérios de saída

Sob quais condições um perfil deve ser removido da jornada antes da conclusão?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Alteração de associação de público | O perfil deve ser fechado quando eles saírem do público de entrada ou entrarem em um público de supressão | Saída em tempo real na alteração do segmento; útil para saídas &quot;convertidas&quot; ou &quot;recusadas&quot; |
| Ocorrência do evento | Um evento específico (por exemplo, compra, cancelamento de inscrição) deve acionar a saída | Saída em tempo real no evento; exige a configuração do esquema do evento |
| Tempo limite | A duração máxima na jornada expirou | O padrão máximo é 91 dias; impede que os perfis permaneçam indefinidamente |

#### Decisão: tempo limite da Jornada

Qual é a duração máxima que um perfil pode permanecer na jornada?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| 91 dias (máximo) | Jornadas de ciclo de vida de longa duração com sequências de criação estendidas | Duração máxima permitida; os perfis saem após 91 dias, independentemente |
| Duração menor personalizada | Campanhas com limite de tempo ou jornadas sazonais | Definido com base na lógica de negócios do jornada; um tempo limite mais curto reduz perfis obsoletos |

#### Decisão: configurações de conflito e prioridade

Esta jornada deve ter pontuação de prioridade para a resolução de conflitos com outras jornadas/campanhas?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Alta prioridade (70-100) | Jornadas críticas do cliente (retenção, fidelidade) que devem ter precedência | Maior prioridade ganha quando várias comunicações competem; use com moderação |
| Prioridade do Medium (30-69) | Jornadas padrão do ciclo de vida | Prioridade equilibrada; pode ser suprimido por comunicações de prioridade mais alta |
| Prioridade baixa (0-29) | Jornadas complementares ou informativas | Será suprimido ao concorrer com comunicações mais importantes |

#### Principais detalhes de configuração

**Navegação da interface do usuário:** Jornadas > Criar Jornada

- Crie a jornada e configure as propriedades (nome, descrição, fuso horário, tempo limite)
- Configurar entrada: acionador Ler público (para lote) ou evento (para tempo real)
- Adicionar nós de decisão vinculados às políticas de decisão configuradas da Fase 3
- Adicionar divisões de condição para roteamento de canal com base em saída de decisão ou atributos de perfil (Opções B/C)
- Adicionar nós de ação de mensagem para cada caminho de canal, vinculando ao conteúdo criado da Fase 4
- Adicionar nós de espera entre pontos de contato (mínimo de 1 hora para jornadas lidas pelo público-alvo)
- Definir critérios de saída (alteração de público-alvo, evento, tempo limite)
- Atribuir pontuação de prioridade para resolução de conflitos
- Configurar limite de frequência se os limites de frequência de jornada cruzada forem aplicáveis
- Teste a jornada no modo de teste com perfis de teste antes de publicar
- Publicar a jornada para ativá-la

#### Onde as opções divergem

**Para a Opção A (Offer Decisioning):**
A tela de jornada é linear com as políticas de decisão incorporadas em cada nó de ação de mensagem. Nenhuma ramificação para seleção de canal. A decisão de oferta é tomada no momento da renderização da mensagem no nó de ação.

**Para a Opção B (Seleção de Canal Dinâmico):**
Após cada etapa de espera, adicione um nó de condição que avalia os critérios de seleção de canal (atributos de perfil, saída de decisão ou status de consentimento). Cada ramificação de condição leva a um nó de ação de mensagem específica do canal. Inclua um caminho padrão/else para perfis que não correspondem a nenhuma condição.

**Para a Opção C (Adaptável Completo):**
Combine nós de condição de seleção de canal com nós de ação de mensagem incorporada à política de decisão. Em cada ponto de contato: primeiro, uma condição ou decisão determina o canal; em seguida, na ação de mensagem do canal selecionado, uma política de decisão seleciona a oferta/conteúdo ideal.

#### Documentação do Experience League

- [Criar uma jornada](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Propriedades da jornada](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Ler atividade de público](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Atividade de condição](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Atividade aguardar](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Adicionar uma mensagem em uma jornada](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Critérios de saída](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [Gerenciamento de entradas de jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Testar a jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [Publicar a jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)
- [Pontuações de prioridade](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Visão geral do gerenciamento de conflitos e prioridades](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Regras de frequência](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)

### Fase 6: Relatórios e monitoramento

**Função de aplicativo:** [!DNL AJO]: Análise de Relatórios e Desempenho

Essa fase configura o monitoramento do desempenho do jornada e da decisão por meio de relatórios dinâmicos (durante a execução) e relatórios históricos (após a conclusão). Métricas específicas de decisão, incluindo distribuição de seleção de oferta, taxas de fallback e eficácia da classificação. Opcionalmente, análise de espaço de trabalho do CJA para jornada profunda entre canais e análise de ROI de decisão.

#### Decisão: profundidade dos relatórios

Qual nível de análise de relatórios é necessário?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| [!DNL AJO] somente relatórios nativos | Monitoramento operacional das métricas de entrega e envolvimento | Relatórios dinâmicos e históricos predefinidos; sem configuração adicional; limitado a [!DNL AJO] métricas |
| [!DNL AJO] + análise do CJA | Análise profunda entre canais, eficácia da decisão, ROI da jornada, análise de coorte | Requer conexão com o CJA e visualização de dados; fornece recursos de análise de atribuição, funnel e coorte |

#### Principais detalhes de configuração

**Navegação da interface do usuário:** Jornadas > Selecionar jornada > Relatório ao vivo/Relatório de todos os tempos

- Monitorar o relatório de jornada ao vivo durante a execução inicial para métricas de entrada, saída e por nó
- Revisar o desempenho da decisão: distribuição da seleção de oferta, taxa de oferta de fallback, eficácia da classificação
- Após a conclusão da jornada, revise os relatórios históricos para uma análise completa do funnel
- Para análise da CJA: verifique se a conexão CJA inclui [!DNL AJO] conjuntos de dados (Evento de Feedback de Mensagem, Evento de Rastreamento de Email)
- Crie o espaço de trabalho do CJA com painéis para análise de combinação de canais, ofereça comparação de desempenho e funis de conversão do jornada
- Criar anotações para as datas de inicialização do jornada e alterações significativas na configuração

#### Documentação do Experience League

- [Relatório em tempo real da jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Jornada relatório global](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabalhar com o Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Visão geral do Analysis Workspace](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/home)
- [Guia de integração do AJO + CJA](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## Considerações de implantação

Analise as seguintes medidas de proteção, armadilhas comuns, práticas recomendadas e decisões de compensação antes e durante a implementação.

### Medidas de proteção e limites

- Máximo de 500 jornadas ativas por sandbox — [medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/get-started/guardrails)
- A duração máxima da jornada é de 91 dias (tempo limite global)
- Máximo de 50 atividades por tela de jornada
- As jornadas de leitura de público podem processar até 20.000 perfis por segundo
- As jornadas de eventos unitários aceitam até 5.000 eventos por segundo por sandbox
- Máximo de 10.000 ofertas personalizadas aprovadas por sandbox
- Máximo de 30 posicionamentos por decisão
- Tempo de resposta do Offer Delivery SLA: menos de 500 ms na P95 para solicitações de escopo único
- Os modelos de classificação de IA exigem um mínimo de 1.000 eventos de conversão para treinamento
- Máximo de 10 superfícies de canal por tipo de canal por sandbox
- As etapas de espera têm uma duração mínima de 1 hora para jornadas lidas por público-alvo
- O cooldown mínimo de reentrada da jornada é de 5 minutos
- Máximo de 4.000 definições de segmento por sandbox — [Medidas de proteção da plataforma](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/guardrails)

### Armadilhas comuns

**A Decisão sempre retorna uma oferta substituta:** Verifique se as ofertas personalizadas estão aprovadas (não em estado de rascunho), dentro de seu intervalo de datas de validade, e se as regras de qualificação correspondem aos atributos dos perfis de destino. Verifique se os limites de limite de oferta não foram atingidos. Teste com um perfil que deve se qualificar claramente para uma oferta personalizada.

**As publicações do Jornada, mas os perfis não estão entrando:** Para jornadas lidas por público, confirme se o público tem uma população avaliada maior que zero. Para jornadas acionadas por eventos, verifique o esquema do evento, as condições de acionamento e se os eventos estão sendo enviados. Verifique se a política de mesclagem de público-alvo de entrada corresponde à política de mesclagem esperada da jornada.

**Fórmula de classificação não aplicada corretamente:** verifique se a sintaxe da fórmula é válida e faz referência a atributos de perfil acessíveis. Os erros de fórmula retornam silenciosamente à classificação baseada em prioridade sem aviso. Teste a classificação com perfis que têm valores de atributo diferentes para confirmar se a fórmula produz a ordem esperada.

**O roteamento de canal ignora o consentimento:** Os nós de condição para seleção de canal devem incluir verificações de consentimento. Um perfil sem consentimento por SMS não deve ser roteado para o caminho SMS. Incorpore o consentimento nas regras de qualificação ao usar a decisão para a seleção de canal (opção B/C).

**Os contadores de limite de oferta ficam atrasados sob alta taxa de transferência:** Os contadores de limite de oferta podem ter um atraso de alguns segundos em cenários de alta taxa de transferência. Se o limite exato for crítico, use limites globais com um buffer ou combine com regras de frequência.

**A tela de Jornada excede o limite de 50 atividades:** jornadas de Opção C complexas com muitas ramificações de canal e nós de decisão podem se aproximar do limite de 50 atividades. Simplifique consolidando a lógica de condição, reduzindo o número de pontos de contato ou dividindo em várias jornadas sequenciais.

**As decisões do Edge retornam uma personalização vazia:** Se estiver usando a decisão de borda para decisões em tempo real, verifique se a sequência de dados tem o serviço [!DNL Adobe Journey Optimizer] habilitado e se o escopo da decisão está formatado corretamente. As decisões do Edge são limitadas aos atributos de perfil disponíveis na loja de perfis de borda.

### Práticas recomendadas

**Comece simples e evolua:** comece com a Opção A (canal fixo, ofertas dinâmicas) para validar a estrutura de decisão e, em seguida, evolua para as Opções B ou C à medida que a maturidade dos dados e a capacidade organizacional aumentam.

**Invista no enriquecimento do perfil:** atributos computados, como pontuações de engajamento, índices de preferência de canal e pontuações de propensão da IA do cliente, melhoram drasticamente a qualidade das decisões. Crie esses atributos de enriquecimento antes de configurar estratégias complexas de classificação.

**Sempre configurar ofertas substitutas:** todas as políticas de decisão devem ter uma oferta substituta. Crie ofertas substitutas como conteúdo genuinamente valioso (não espaços reservados vazios), pois elas atendem perfis que não se qualificam para nenhuma oferta personalizada.

**Testar com perfis diversos:** Use o modo de teste com perfis que representem caminhos de qualificação, preferências de canal e combinações de atributos diferentes. Verifique se cada caminho de jornada e resultado de decisão possíveis funciona corretamente antes de publicar.

**Monitorar taxas de fallback como uma métrica de integridade:** Uma alta taxa de oferta de fallback indica que as regras de qualificação são muito restritivas ou o catálogo de ofertas não abrange segmentos de perfil suficientes. Direcione uma taxa de fallback abaixo de 20% para decisões bem configuradas.

**Use fragmentos de conteúdo para consistência entre canais:** crie fragmentos de conteúdo compartilhados (cabeçalhos, rodapés, avisos legais de isenção de responsabilidade, blocos de cancelamento de inscrição) para manter a consistência da marca em emails, SMS e mensagens por push na jornada.

**Configure os critérios de saída de forma proativa:** defina critérios de saída para eventos de conversão (por exemplo, compra, registro) para que os perfis que concluírem a ação desejada sejam removidos da jornada imediatamente em vez de continuarem a receber mensagens.

**Atribuir pontuações de prioridade significativas:** ao executar várias jornadas e campanhas, atribua pontuações de prioridade com base no impacto nos negócios. As jornadas de retenção de alto valor devem ter prioridade mais alta do que as comunicações informativas.

### Decisões de compensação

Analise as seguintes compensações para informar suas opções de implementação.

#### Complexidade de decisão versus tempo de entrada no mercado

A decisão mais sofisticada (opção C com classificação de IA) oferece personalização mais alta, mas requer significativamente mais configuração, preparação de dados e tempo de teste.

- **A opção A/B favorece:** implantação mais rápida, testes mais simples, menor sobrecarga de gerenciamento contínuo
- **A opção C favorece:** personalização máxima, otimização contínua orientada por IA, maior potencial de engajamento
- **Recomendação:** Comece com a Opção A ou B para a primeira inicialização. Colete dados de desempenho e crie atributos de enriquecimento de perfil em paralelo. Evolua para a Opção C quando tiver pelo menos 1.000 eventos de conversão para treinamento de classificação de IA e um catálogo de ofertas bem preenchido.

#### Ramificação estática versus decisão para seleção de canal

A seleção de canais pode ser implementada por meio de nós de condição de jornada simples (avaliando diretamente os atributos do perfil) ou pela estrutura de decisão (em que os canais são modelados como itens de decisão com qualificação e classificação).

- **Os nós de condição estáticos favorecem:** Simplicidade, transparência, fácil solução de problemas. Melhor quando a lógica de seleção de canal é simples (por exemplo, &quot;se o token de push existir e o último push estiver aberto em 30 dias, use push; caso contrário, email&quot;).
- **A seleção de canal baseada em decisão favorece:** gerenciamento centralizado, potencial de otimização de IA, capacidade de evoluir a lógica de classificação sem modificar a tela de jornada. Melhor quando a seleção de canal é complexa e deve melhorar com o tempo.
- **Recomendação:** Use nós de condição estática para a Opção B quando os critérios de seleção de canal forem simples e bem definidos. Use a seleção de canal baseada em decisões quando quiser que a IA otimize a seleção de canais ao longo do tempo ou quando a lógica de seleção de canais for complexa o suficiente para se beneficiar da qualificação centralizada e do gerenciamento de classificação.

#### Granularidade da oferta versus capacidade de gerenciamento de catálogos

Um catálogo de ofertas grande e granular com muitas ofertas direcionadas produz personalização mais precisa, mas requer mais esforço de gerenciamento. Um catálogo menor com qualificação mais ampla é mais fácil de gerenciar, mas menos personalizado.

- **Um catálogo grande (muitas ofertas específicas) favorece:** maior precisão de personalização, seleções mais relevantes para públicos diversos, taxas de fallback mais baixas
- **O catálogo pequeno (menos ofertas amplas) favorece:** Gerenciamento mais fácil, configuração mais rápida, testes mais simples, menor risco de ofertas órfãs
- **Recomendação:** comece com 5 a 15 ofertas personalizadas além de um fallback por decisão. Adicione mais ofertas conforme você observa quais segmentos recebem ofertas substitutas com mais frequência. Use qualificadores de coleta para organizar ofertas por categoria, camada ou linha de produtos para crescimento gerenciável.

#### Decisão com base em prioridades versus AI

A classificação baseada em prioridades é determinística e transparente. A decisão classificada por IA otimiza automaticamente, mas requer dados de treinamento e é menos transparente.

- **A classificação baseada em prioridades favorece:** Previsibilidade, transparência, implantação imediata, nenhum requisito de dados de treinamento
- **A decisão classificada com IA favorece:** otimização contínua, seleção orientada por dados, capacidade de descobrir afinidades não óbvias entre perfis de ofertas
- **Recomendação:** Use classificação baseada em prioridade ou em fórmula para a implantação inicial. Faça a transição para a decisão classificada em IA depois de acumular pelo menos 1.000 eventos de conversão e quiser mudar da otimização baseada em regras para a baseada em modelo.

## Documentação relacionada

Os recursos a seguir fornecem detalhes adicionais sobre os recursos usados neste padrão de caso de uso.

### Jornada orquestração

- [Introdução ao jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Criar uma jornada](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Propriedades da jornada](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Ler atividade de público](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Eventos gerais](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Eventos de qualificação de público-alvo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [Atividade de condição](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Atividade aguardar](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Adicionar uma mensagem em uma jornada](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Critérios de saída](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [Gerenciamento de entradas de jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Testar a jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [Publicar a jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

### Gerenciamento de decisão

- [Visão geral da Gestão de decisões](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Criar inserções](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Criar regras de decisão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crie ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Criar ofertas substitutas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Criar coleções](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Criar qualificadores de coleção](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [Criar decisões](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estratégias de classificação](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [Entregar ofertas em mensagens](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### Configuração de canais

- [Introdução à configuração de email](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegar subdomínios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Criar pools de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [Planos de aquecimento de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Configurações de superfície de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Configurar canal de SMS](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configurar canal de notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Criação e personalização de mensagens

- [Criar um email](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/email/create-email)
- [Criar conteúdo de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxe do Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabalhar com modelos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabalhar com fragmentos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Visualizar e testar o conteúdo](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### Gerenciamento de conflitos, prioridades e frequências

- [Visão geral do gerenciamento de conflitos e prioridades](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Pontuações de prioridade](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Identificar possíveis conflitos](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [Limite de jornada e arbitragem](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/conflict-prioritization/journey-capping)
- [Regras de frequência](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)

### Públicos-alvo e segmentação

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentação de transmissão](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentação de borda](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Composição de público](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Referência do Profile Query Language](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/pql/overview)

### Relatórios e análises

- [Relatório em tempo real da jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Jornada relatório global](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabalhar com o Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Guia de integração do AJO + CJA](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Visão geral do CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-overview/cja-overview)
- [Visão geral do Analysis Workspace](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/home)

### Perfil e identidade

- [Visão geral do Perfil do cliente em tempo real](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/home)
- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/home)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/merge-policies/overview)
- [Visão geral de atributos computados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/computed-attributes/overview)
- [Visão geral do Customer AI](https://experienceleague.adobe.com/pt-br/docs/experience-platform/intelligent-services/customer-ai/overview)

### Governança e consentimento de dados

- [Visão geral da governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/home)
- [Consentimento no Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [Gerenciar lista de supressão](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Medidas de proteção

- [Medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/get-started/guardrails)
- [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/guardrails)
- [Medidas de proteção do serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/guardrails)
