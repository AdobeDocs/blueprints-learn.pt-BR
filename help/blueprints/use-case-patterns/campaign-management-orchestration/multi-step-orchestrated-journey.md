---
title: Jornada orquestrada em várias etapas
description: Saiba como guiar um perfil por meio de uma jornada multitoque com esperas, condições e várias ações de mensagem ao longo do tempo.
solution: Journey Optimizer, Real-Time Customer Data Platform
source-git-commit: b2e496eb521fc3dd3290fccdd9a8203384934b88
workflow-type: tm+mt
source-wordcount: '8173'
ht-degree: 1%

---


# Jornada orquestrada em várias etapas

Este guia fornece um blueprint de implementação abrangente para a criação de jornadas orquestradas em várias etapas usando o [!DNL Adobe Journey Optimizer] (AJO) e o [!DNL Real-Time Customer Data Platform] (RT-CDP). Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam orquestrar jornadas de clientes multitoque com ramificação que entregam várias mensagens ao longo do tempo.

Ele apresenta todas as opções de implementação viáveis, considerações de decisão em cada ponto de configuração e links para a documentação do [!DNL Adobe Experience League]. Use este guia para planejar, configurar e validar a implementação do jornada em várias etapas.

## Visão geral do caso de uso

As jornadas orquestradas em várias etapas abordam cenários de negócios em que uma única mensagem é insuficiente para alcançar o resultado desejado pelo cliente. Em vez de um envio único, a jornada orienta cada perfil por uma sequência de pontos de contato — emails, mensagens SMS, notificações por push ou mensagens no aplicativo — espaçados por dias ou semanas, com uma lógica de ramificação que adapta o caminho com base em atributos de perfil, sinais comportamentais ou dados de evento.

Essas jornadas são o padrão de campanha mais complexo no AJO. Eles combinam entrada baseada em público ou evento com uma tela de nós de ação (mensagens), nós de condição (lógica de ramificação), nós de espera (atrasos de tempo) e critérios de saída (eventos de conversão ou tempos limite). Cada perfil avança pela jornada independentemente, em seu próprio ritmo, recebendo conteúdo contextualmente relevante em cada etapa.

Esse padrão inclui os padrões mais simples — ativação de mensagens de saída em lote para campanhas de envio único e mensagens acionadas por evento para respostas de evento único. Use esse padrão quando o caso de uso exigir a criação de um perfil por meio de várias interações ao longo do tempo.

## Principais objetivos de negócios

Os seguintes objetivos de negócios são compatíveis com esse padrão de caso de uso.

### Melhorar a retenção do cliente

Mantenha os clientes existentes envolvidos e renovando-os por meio de experiências orientadas por valores e estimulação contínua do relacionamento.

**KPIs:** Retenção, Valor vitalício do cliente, Participação

[Saiba mais sobre como melhorar a retenção do cliente](/help/blueprints/business-objectives/customer-experience/improve-customer-retention.md)

### Melhorar a integração do cliente

Acelere o tempo de implantação para novos clientes com experiências de boas-vindas e jornadas de ativação simplificadas e personalizadas.

**KPIs:** Envolvimento, Retenção, Taxas de Conversão

[Saiba mais sobre como melhorar a integração do cliente](/help/blueprints/business-objectives/customer-experience/improve-customer-onboarding.md)

### Reengajamento de clientes inativos

Conquiste clientes inativos ou antigos com campanhas de reativação direcionadas com base em sinais comportamentais.

**KPIs:** Envolvimento, Retenção, Taxas de Conversão

### Recuperar carrinhos e jornadas abandonados

Reenvolva os usuários que abandonaram o durante os fluxos de compra, aplicativo ou inscrição com acompanhamentos oportunos e personalizados.

**KPIs:** Taxas de Conversão, Receita Incremental, Participação

[Saiba mais sobre como recuperar carrinhos e jornadas abandonados](/help/blueprints/business-objectives/customer-experience/recover-abandoned-carts-journeys.md)

## Exemplo de casos de uso tático

Os cenários a seguir ilustram aplicativos comuns do padrão de jornada orquestrada de várias etapas.

- **Série de integração de clientes** — email de boas-vindas, seguido de treinamento de recursos e prompt de ativação nos primeiros 14 dias após o registro
- **Campanha de reengajamento por gotejamento** — um email de lembrete, depois uma oferta de incentivo e, em seguida, um aviso final para clientes que passaram mais de 3 semanas
- **jornada de marco de fidelidade** — Notificação de atualização de nível, seguida de uma oferta exclusiva e um lembrete de renovação à medida que a data de aniversário da associação se aproxima
- **Sequência de retornos** — email &quot;sentimos sua falta&quot;, depois uma oferta de desconto por email e, em seguida, um lembrete de SMS final para compradores com lapso
- **jornada de adoção de produtos** — Boas-vindas da avaliação, dicas de uso e um prompt de atualização à medida que o período de avaliação avança
- **Sequência de renovação da assinatura** — aviso de 30 dias, lembrete de 7 dias e mensagem de dia de expiração para futuras renovações de assinatura
- **Proteção pós-compra** — email de agradecimento, guia prático, recomendação de venda cruzada e solicitação de revisão mais de 30 dias após a compra

## Indicadores-chave de desempenho

Use os KPIs a seguir para medir a eficácia da implementação da jornada orquestrada em várias etapas.

| KPI | Descrição | Abordagem de medição |
| --- | --- | --- |
| Taxa de conclusão da jornada | Porcentagem de perfis que concluem a jornada completa sem saída antecipada | Relatório de Jornada: Encerrado (concluído) / Informado |
| Índice de conversão de etapa | Porcentagem de perfis que avançam de uma etapa para a próxima | Métricas por nó no relatório de jornada |
| Taxa de participação do canal | Taxas de abertura, taxas de click-through e taxas de resposta em cada ponto de contato | Métricas de entrega e envolvimento por mensagem |
| Taxa de conversão dos critérios de saída | Porcentagem de perfis que acionam o evento de saída (por exemplo, compra, inscrição) antes do tempo limite da jornada | Contagem de ocorrências dos critérios de saída / Total inserido |
| Tempo para conversão | Duração média do evento de entrada de jornada para critérios de saída | Análise de Jornada: carimbo de data e hora de entrada para carimbo de data e hora de evento de conversão |
| Taxa de devolução da Jornada | Porcentagem de perfis que param de se envolver em cada etapa (análise de fallout) | Visualização de fallout do CJA nas etapas do jornada |
| Taxa de retenção/reengajamento | Porcentagem de perfis direcionados que retornam ao status ativo | Análise comportamental pós-jornada no CJA |

## Padrão do caso de uso

**Jornada Orquestrada Em Várias Etapas**

Guie um perfil por meio de uma jornada multitoque com esperas, condições e várias ações de mensagem ao longo do tempo.

**Cadeia de funções:** Avaliação de público-alvo > Execução de Jornada (vários nós) > Ramificação de condição > Entrega de mensagem (xN) > Critérios de saída > Relatórios

## Aplicativos

Os aplicativos a seguir são usados para implementar esse padrão de caso de uso.

- **[!DNL Adobe Journey Optimizer](AJO)** — mecanismo de orquestração de Jornadas, criação de mensagens, configuração de canais, experimentação de conteúdo, gerenciamento de frequência e conflitos e relatórios
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)** — Avaliação e definição de público-alvo para públicos-alvo de entrada de jornada, dados de perfil para personalização e ramificação de condição
- **[!DNL Adobe Experience Platform](AEP)** — Armazenamento de perfil, serviço de identidade, assimilação de dados de evento e infraestrutura de dados de base

## Funções básicas

Os seguintes recursos básicos devem estar em vigor para esse padrão de caso de uso. Para cada função, o status indica se ele é tipicamente necessário, se presume ser pré-configurado ou se não é aplicável.

| Função de base | Status | O que deve estar em vigor | Referência do Experience League |
| --- | --- | --- | --- |
| Administração e governança | Presumido em vigor | sandbox da AJO com permissões de criação e publicação de jornadas. As superfícies de canal de todos os canais usados na jornada devem ser configuradas. Os usuários devem ter as funções apropriadas (profissional de marketing, gerente de Jornadas) com permissões de jornada e campanha. | [Visão geral das sandboxes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/home), [Visão geral do controle de acesso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Preparação e modelagem de dados | Obrigatório | Esquema de perfil XDM com atributos usados para ramificação de condição e personalização em várias mensagens (por exemplo, nível de fidelidade, interesse do produto, pontuação de envolvimento). Esquemas de evento de experiência para eventos de conversão que determinam os critérios de saída e a avaliação da condição (por exemplo, eventos de compra, envios de formulário). | [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [noções básicas de composição de esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| Fontes de dados e coleção | Presumido em vigor | A transmissão do evento deve estar ativa se os critérios ou condições de saída dependerem de eventos em tempo real (por exemplo, comprar evento para sair da jornada). Assimilação em lote para atributos de perfil usados na ramificação. Web SDK ou API do lado do servidor para coleção de eventos comportamentais. | [Visão geral da assimilação de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/streaming/overview), [Visão geral das fontes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home) |
| Configuração de identidade e perfil | Presumido em vigor | Os perfis devem ser resolvidos em todos os canais usados na jornada (email, SMS, push). A identidade entre dispositivos deve ser configurada se a jornada abranger os pontos de contato da Web e móveis. A política de mesclagem deve ser configurada para a sandbox. | [Visão geral do Serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| Definição e segmentação do público-alvo | Obrigatório | O público-alvo de entrada deve ser definido para jornadas lidas por público-alvo. Os segmentos também podem ser usados em nós de condição para ramificação. O método de avaliação (lote ou streaming) deve corresponder aos requisitos de entrada de jornada. | [Visão geral do Serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder) |

## Funções de suporte

Os recursos a seguir aumentam esse padrão de caso de uso, mas não são necessários para a execução principal.

| Função de suporte | Status | Por que é importante | Referência do Experience League |
| --- | --- | --- | --- |
| Criação de atributo calculado/derivado | Recomendado | Atributos computados, como pontuações de engajamento, dias desde a última atividade ou valor de compra vitalício, melhoram a lógica de ramificação de condição, permitindo decisões mais inteligentes de caminho de jornada. | [Visão geral dos atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Gerenciamento do ciclo de vida dos dados | Recomendado | A retenção de dados do evento de jornada deve ser configurada com políticas de expiração do conjunto de dados para gerenciar o armazenamento e estar em conformidade com as normas de retenção de dados. A aplicação do consentimento garante que somente perfis de Opt-in recebam mensagens em cada ponto de contato do canal. | [Visão geral do Gerenciamento Avançado do Ciclo de Vida dos Dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [Expirações do conjunto de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration) |
| Rotulagem e aplicação de uso de dados | Recomendado | Os rótulos de governança garantem a personalização em conformidade em vários pontos de contato de mensagem, especialmente importante quando as jornadas usam PII ou dados confidenciais para personalização em vários canais. | [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [Visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview) |
| Monitoramento e capacidade de observação | Incluído | O monitoramento da execução de jornadas monitora alertas sobre falhas de processamento, gargalos na entrada de perfis e problemas de entrega. Essencial para jornadas de produção em que atrasos ou falhas afetam a experiência do cliente. | [Visão geral dos alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview), [Visão geral dos Insights de observação](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| Relatórios e análise | Incluído | O CJA funnel e a análise de fallout na jornada completa fornecem insight mais profundo do que apenas os relatórios nativos do AJO. Permite a análise de conversão passo a passo, a comparação de coorte e a otimização de jornadas. | [visão geral do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [visão geral do Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home) |

## Funções do aplicativo

Este plano exerce as seguintes funções do Catálogo de Funções da Aplicação. As funções são mapeadas para fases de implementação em vez de etapas numeradas.

### [!DNL Journey Optimizer] (AJO)

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Configuração de canais | Fase 1: Configuração de canal | Configurar superfícies dos canais (email, SMS, push) para cada ponto de contato de mensagem na jornada |
| Criação de mensagens | Fase 2: Criação do conteúdo da mensagem | Crie conteúdo de mensagem com personalização, conteúdo dinâmico e modelos para cada nó de ação de jornada |
| Journey Orchestration | Fase 3: Design e ativação da Jornada | Projete a tela de jornada de várias etapas com nós de entrada, ação, condição, espera e saída; teste e publique |
| Frequência e regras de negócios | Fase 4: governança e otimização | Configure limites de frequência para evitar mensagens excessivas em pontos de contato do jornada e outras campanhas simultâneas |
| Gerenciamento de conflitos e prioridades | Fase 4: governança e otimização | Atribuir pontuações de prioridade e configurar a detecção de conflitos para jornadas que concorrem com outras comunicações ativas |
| Experimentação de conteúdo | Fase 4: governança e otimização | Execute testes A/B no conteúdo da mensagem nos nós de ação do jornada para otimizar o desempenho |
| Relatórios e análise de desempenho | Fase 5: Relatórios e monitoramento | Monitorar a execução da jornada, as métricas de entrega por etapa e o desempenho do envolvimento |

### [!DNL Real-Time CDP] (RT-CDP)

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Avaliação de público | Fase 1: Configuração do canal (pré-requisito) | Defina e avalie o público-alvo de entrada para jornadas lidas por público-alvo; defina públicos-alvo de condição para ramificação |
| Consentimento e aplicação de governança | Fase 4: governança e otimização | Aplicar preferências de consentimento e políticas de uso de dados nas ações de mensagem do jornada |

## Pré-requisitos

Conclua os seguintes pré-requisitos antes de iniciar a implementação.

- [ A sandbox do AJO ] foi provisionada com permissões de criação e publicação de jornadas
- [ ] Pelo menos uma superfície de canal (email, SMS ou push) está configurada e ativa
- [ ] O esquema de perfil inclui atributos necessários para a ramificação e personalização da condição
- [ O esquema do Evento de experiência ] está configurado para eventos de conversão usados nos critérios de saída
- [ ] A transmissão de eventos está ativa para eventos em tempo real usados nos critérios de saída ou na entrada acionada pelo evento
- [ ] namespaces de identidade e políticas de mesclagem estão configurados para resolução de perfis entre canais
- [ ] ativos de conteúdo (imagens, cópia, CTAs) são preparados para cada ponto de contato de mensagem
- [ ] O público de entrada é definido e avaliado (para jornadas lidas por público)
- [ ] O esquema de evento de acionamento está configurado (para jornadas acionadas por eventos)
- [ ] perfis de teste estão disponíveis para validação do modo de teste de jornada
- [ A lista de supressão ] foi revisada e atualizada para todos os canais usados

## Opções de implementação

Revise as opções a seguir para determinar a melhor abordagem para sua jornada orquestrada de várias etapas.

### Opção A: jornada orquestrada de leitura de público

**Recomendado para:** sequências de criação com base no tempo em que um público-alvo conhecido entra na jornada e avança pelos pontos de contato agendados: séries de integração, sequências de renovação, interrupções de reengajamento, jornadas de marcos de fidelidade.

**Como funciona:**

Um público-alvo é lido na entrada da jornada, como uma leitura única ou em um agendamento recorrente. Todos os perfis qualificados entram na jornada simultaneamente e avançam pela tela em seu próprio ritmo, regido pelas durações de espera e avaliações de condição. O caminho de cada perfil pela jornada é independente — alguns podem pegar a ramificação &quot;engajada&quot;, enquanto outros pegam a ramificação &quot;não engajada&quot; com base em seu comportamento ou atributos.

O público é avaliado no momento em que a atividade Ler público é executada. Para jornadas recorrentes, o público-alvo é reavaliado em cada recorrência e novos perfis qualificados entram na jornada, enquanto os perfis que já estão na jornada continuam no caminho. Essa abordagem fornece tempo de entrada previsível e é adequada para programas de ciclo de vida programados.

**Principais considerações:**

- O público deve ser definido e avaliado antes da ativação da jornada
- A leitura recorrente permite que novos qualificadores sejam inseridos em cada ciclo
- Os perfis na jornada não são lidos novamente; somente os novos qualificadores são inseridos nas leituras subsequentes
- As etapas de espera têm uma duração mínima de 1 hora para jornadas lidas por público-alvo

**Vantagens:**

- Tempo de entrada previsível alinhado com as programações de negócios
- Suporta grandes volumes de público (até 20.000 perfis por segundo com aceleração padrão)
- Simples de testar e monitorar com populações conhecidas de públicos-alvo
- Pode ser programado para entrada recorrente (diariamente, semanalmente, mensalmente)

**Limitações:**

- A entrada é baseada em lote, não em tempo real — os perfis são inseridos no tempo de leitura programado, não quando são qualificados
- Não é adequado para sequências iniciadas por comportamento que exigem resposta imediata
- As alterações de público entre leituras não são refletidas para perfis que já estão na jornada

**Experience League:**

- [Ler atividade de público](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Criar uma jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)

### Opção B: jornada orquestrada acionada por eventos

**Recomendado para:** sequências iniciadas por comportamento em que um evento em tempo real inicia a jornada — escalonamento de abandono de carrinho, promoção pós-compra, jornada de fidelidade acionada por marco, sequências de ativação de avaliação.

**Como funciona:**

Um evento unitário (por exemplo, uma compra, abandono de carrinho, envio de formulário ou instalação de aplicativo) aciona a entrada de jornada para perfis individuais em tempo real. Quando o evento é recebido, o perfil entra na jornada e avança pela sequência de pontos de contato com condições, esperas e ramificações. Essa abordagem combina a urgência de mensagens acionadas por eventos com a orquestração de várias etapas de uma jornada completa.

O evento de acionamento deve ser configurado como um evento de jornada com seu schema e condições definidas. A jornada escuta o evento continuamente e insere perfis, um de cada vez, à medida que os eventos chegam. Os nós de jornada subsequentes podem avaliar a resposta do perfil para determinar qual ramificação seguir.

**Principais considerações:**

- Requer que a transmissão de eventos em tempo real esteja ativa
- O esquema e as condições do evento devem ser configurados com precisão para evitar acionadores falsos
- As regras de reentrada são críticas — determine se um perfil pode ser reinserido se o evento for acionado novamente
- Suporta até 5.000 eventos por segundo por sandbox

**Vantagens:**

- Entrada em tempo real com base no comportamento do cliente — altamente contextual
- Cada perfil é inserido independentemente quando o evento ocorre, não de acordo com um agendamento
- Adequação natural para sequências de resposta comportamental (abandono do carrinho, pós-compra)
- Pode combinar com dados de perfil para ramificação personalizada após a entrada

**Limitações:**

- Requer que a infraestrutura de transmissão de eventos esteja em vigor
- Maior complexidade na configuração e no teste do esquema do evento
- Cada evento insere um perfil — inadequado para ativação de público-alvo em massa
- A depuração requer o rastreamento de jornadas de perfis individuais

**Experience League:**

- [Eventos gerais](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Eventos de qualificação de público-alvo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)

### Opção C: jornada orquestrada de vários canais

**Melhor para:** sequências entre canais que usam canais diferentes em cada ponto de contato — email, SMS e escalonamento por push ou email mais mensagens complementares no aplicativo. Pode usar entrada de leitura de público ou acionada por evento.

**Como funciona:**

Essa opção estende a Opção A ou a Opção B ao incorporar vários canais de mensagens na mesma jornada. Cada nó de ação na jornada pode direcionar um canal diferente (email, SMS, push, no aplicativo ou Web), exigindo uma superfície de canal separada para cada um. O designer da jornada seleciona o canal apropriado em cada etapa, permitindo padrões de escalonamento (por exemplo, email primeiro e SMS se não houver engajamento) ou padrões complementares (por exemplo, email com reforço no aplicativo).

As jornadas entre canais exigem superfícies de canal para cada canal usado e devem levar em conta a personalização específica do canal, limites de caracteres e requisitos de aceitação. Os nós de condição podem verificar o engajamento com mensagens anteriores (por exemplo, &quot;email aberto?&quot; como uma condição de ramificação) para determinar o próximo canal.

**Principais considerações:**

- Requer superfícies de canal ativas para cada canal usado na jornada
- Cada canal tem diferentes recursos de personalização e restrições de conteúdo
- O consentimento deve ser verificado por canal — um perfil pode ser aceito para email, mas não para SMS
- Limites de frequência específicos do canal devem ser configurados para evitar mensagens excessivas entre canais

**Vantagens:**

- Maximiza o alcance ao envolver perfis em seus canais preferidos
- Permite estratégias de escalonamento para perfis não responsivos
- Oferece suporte a mensagens complementares entre canais para reforço
- A experiência do cliente mais sofisticada possível

**Limitações:**

- A mais alta complexidade de implementação — requer configuração para cada canal
- O conteúdo deve ser criado para cada canal em cada ponto de contato
- O gerenciamento de consentimento e frequência se torna mais complexo entre canais
- O teste requer validação em todas as superfícies de canal

**Experience League:**

- [Configurar canal de SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configurar canal de notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Comparação de opções

A tabela a seguir compara as três opções de implementação entre os principais critérios.

| Critérios | Opção A: Audience-read | Opção B: acionado por evento | Opção C: Vários canais |
| --- | --- | --- | --- |
| Melhor para | Programas de ciclo de vida programados, séries de nutrição | Sequências de resposta comportamental, abandono de carrinho | Escalonamento entre canais, mensagens complementares |
| Tempo de entrada | Agendado (lote) | Tempo real (orientado por eventos) | Programado ou em tempo real |
| Complexo | Médio | Medium-Alto | Alta |
| Volume de entrada | Até 20.000 perfis/s | Até 5.000 eventos/s | Mesmo que o método de entrada subjacente |
| Escopo do canal | Um ou vários canais | Um ou vários canais | Vários canais necessários |
| Exige | Público definido, programação de avaliação | Infraestrutura de eventos de transmissão | Superfícies de canal para cada canal |
| Resposta em tempo real | Não — entrada de lote | Sim — imediato após o evento | Depende do método de entrada |

### Escolha a opção certa

Use o seguinte fluxo de decisão para selecionar a abordagem de implementação correta:

1. **A jornada é iniciada por um comportamento ou evento do cliente?** Em caso afirmativo, escolha **Opção B** (Acionado por Evento). Se a jornada for iniciada por uma leitura agendada de público, escolha **Opção A** (Audience-Read).

2. **A jornada usa vários canais de mensagens (por exemplo, email E SMS)?** Em caso afirmativo, aplique a **Opção C** (Multicanal) sobre sua opção de método de entrada (A ou B). Se a jornada usar um único canal em todo o, a Opção A ou B sozinha será suficiente.

3. **Você precisa escalar para um canal diferente com base no envolvimento?** Em caso afirmativo, escolha a **Opção C** com nós de condição que verificam o engajamento com mensagens anteriores e ramifique para canais alternativos.

4. **O público-alvo é conhecido antecipadamente e processado de acordo com um cronograma?** Em caso afirmativo, escolha **Opção A**. Se os perfis precisarem entrar na jornada no momento em que executarem uma ação, escolha **Opção B**.

## Fases de implementação

As fases a seguir abordam a implementação completa de uma jornada orquestrada em várias etapas.

### Fase 1: configurar canais e preparar públicos

**Funções do aplicativo:** AJO: configuração de canal, RT-CDP: avaliação de público-alvo

Antes de projetar a jornada, todas as superfícies de canal devem estar ativas e o público-alvo de entrada (para a Opção A) deve ser definido e avaliado. Essa fase garante que a infraestrutura esteja pronta para a entrega de mensagens.

#### Decidir sobre o tipo de canal para cada ponto de contato

Quais canais de mensagens a jornada usará em cada ponto de contato?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Somente email | O Jornada se comunica exclusivamente por email (integração, criação) | Configuração mais simples; requer subdomínio de email e pool de IP; sujeito à inserção da caixa de entrada |
| Somente SMS | Alertas sensíveis ao tempo, lembretes de compromissos | Exige credenciais do provedor de SMS (Sinch, Twilio, Infobip); custo mais alto por mensagem; regras de recusa mais rigorosas |
| Somente push | Sequências de engajamento no aplicativo para usuários móveis | Requer credenciais APNs/FCM; os usuários devem ter o aplicativo instalado |
| Multicanal | Escalonamento ou mensagens complementares entre canais | Requer superfície de canal por canal; mais complexo, mas de maior alcance |

#### Decisão sobre o método de avaliação de público-alvo (Opção A)

Com que rapidez os perfis devem se qualificar para o público-alvo de entrada?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Avaliação em lote | O público é lido de acordo com uma programação (diariamente, semanalmente); nenhuma entrada em tempo real é necessária | Configuração simples; público avaliado antes da leitura da jornada; compatível com regras de segmentos complexas |
| Avaliação de transmissão | Os perfis devem ser qualificados em tempo quase real, à medida que os atributos forem alterados | A expressão da regra de segmento deve ser qualificada para streaming; qualificação quase em tempo real |

#### Decidir sobre o método de delegação de subdomínio (canal de email)

Como o subdomínio de envio de email deve ser delegado à Adobe?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Delegação completa | O Adobe gerencia registros DNS; configuração mais simples | A configuração é mais rápida; o Adobe lida com SPF, DKIM, DMARC |
| Delegação CNAME | A organização retém o controle de DNS | Requer o envolvimento do administrador de DNS; os registros CNAME devem ser configurados |

#### Navegação na interface

- Superfícies de canal: Administração > Canais > Superfícies de canal > Criar superfície
- Subdomínios: Administração > Canais > Subdomínios
- Configuração de SMS: Administração > Canais > Configuração de SMS
- Configuração de push: Administração > Canais > Configurações de notificação por push
- Públicos: Cliente > Públicos > Criar público > Criar regra de criação

#### Principais detalhes de configuração

- Verificar o status de aquecimento do pool de IP para email — novos pools de IP exigem um plano de aquecimento gradual durante 2 a 4 semanas
- Para SMS, configure as credenciais do provedor e verifique o registro do número do remetente
- Para push, carregue certificados APNs e chaves do servidor FCM
- Defina o público-alvo de entrada usando o Construtor de segmentos com regras de segmento que cubram a população do público-alvo
- Incluir regras de supressão na definição de público-alvo (excluir recentemente convertidos, inscrição cancelada globalmente)

#### Onde as opções divergem

**Para Opção A (Leitura De Público-Alvo):**
Defina e avalie o público-alvo de entrada. Confirme se o público-alvo tem uma população diferente de zero. Determine se a jornada usará uma leitura única de público-alvo ou um agendamento de leitura recorrente.

**Para Opção B (Acionado Por Evento):**
Verifique se o esquema de evento de acionamento está configurado e se os eventos estão sendo transmitidos para a plataforma. Nenhum público-alvo predefinido é necessário — os perfis são inseridos individualmente no recebimento do evento.

**Para Opção C (Multicanal):**
Configure as superfícies dos canais para CADA canal usado na jornada (email, SMS, push, no aplicativo). Verificar o status de consentimento por canal para a população do público-alvo.

#### Documentação do Experience League

- [Configurar superfícies do canal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Introdução à configuração de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Configurar canal de SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configurar canal de notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [Planos de aquecimento de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)


### Fase 2: Criar conteúdo da mensagem

**Função do aplicativo:** AJO: Criação de Mensagens

Crie o conteúdo da mensagem para cada ponto de contato na jornada. Cada mensagem pode ter conteúdo, profundidade de personalização e canal diferentes. Essa fase cria todo o conteúdo do material de entrega que os nós de ação de jornada referenciarão.

#### Decidir sobre a abordagem de conteúdo

Cada mensagem deve começar com um modelo, ser projetada do zero ou importar o HTML?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Modelo de conteúdo existente | Mensagens consistentes com a marca e layouts estabelecidos | Mais rápido; garante a conformidade da marca; o modelo deve existir e corresponder ao tipo de canal |
| Criar do zero | Layouts exclusivos e personalizados para cada ponto de contato | Mais flexível; tempo de criação mais longo; use o modo de arrastar e soltar do Email Designer |
| Importar HTML | HTML pré-construído a partir de ferramentas de design externas | Requer HTML limpo; pode precisar de ajuste para a capacidade de resposta |

#### Decidir sobre a profundidade da personalização

Quantas personalizações cada mensagem deve incluir?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Inserção básica de token | Nome, cidade, atributos simples de perfil | Baixa complexidade; usa a sintaxe Handlebars com caminhos XDM |
| Blocos de conteúdo condicional | Conteúdo diferente mostrado com base no segmento ou atributo | Complexidade do Medium; requer regras de conteúdo dinâmico |
| Personalização contextual de Jornada | O conteúdo varia com base no caminho da jornada e nas interações anteriores | Maior complexidade; aproveita as variáveis de contexto do jornada e os dados do evento |

#### Decidir sobre a estratégia de fragmentos

Os blocos de conteúdo compartilhado (cabeçalhos, rodapés, texto legal) devem ser criados como fragmentos reutilizáveis?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Fragmentos reutilizáveis | Várias mensagens compartilham elementos comuns; é necessária a consistência da marca | As alterações se propagam para todas as mensagens usando o fragmento; máximo de 30 fragmentos por mensagem |
| Conteúdo integrado | Mensagens únicas com layouts únicos | Mais rápido para conteúdo de uso único; sem benefício de consistência entre mensagens |

#### Navegação na interface

- Gerenciamento de conteúdo > Modelos de conteúdo > Procurar
- Designer de email (dentro da campanha ou ação de jornada)
- Gerenciamento de conteúdo > Fragmentos > Criar fragmento

#### Principais detalhes de configuração

- Conteúdo de autor para CADA ação de mensagem na jornada — uma jornada de quatro etapas pode exigir quatro designs de mensagem separados
- Usar expressões de personalização que fazem referência a caminhos de perfil XDM (por exemplo, `{{profile.person.name.firstName}}`)
- Configurar blocos de conteúdo dinâmico para variações específicas de segmentos
- Visualizar cada mensagem com perfis de teste para verificar a renderização da personalização
- Enviar provas aos participantes internos para revisão de conteúdo
- Para SMS, respeitar limites de caracteres (160 caracteres para codificação GSM padrão)
- Para push, configure título, corpo, imagem e ação de deep link/URL

#### Documentação do Experience League

- [Criar conteúdo de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Criar um email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxe do Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabalhar com modelos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabalhar com fragmentos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Criar uma mensagem SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/create-sms)
- [Criar uma notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/design-push)
- [Visualizar e testar o conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)


### Fase 3: Projetar e ativar a jornada

**Função do aplicativo:** AJO: Journey Orchestration

Projete a tela de jornada de várias etapas, incluindo o nó de entrada, os nós de ação (mensagens), os nós de condição (ramificação), os nós de espera (atrasos de tempo) e os critérios de saída. Em seguida, teste com perfis de teste e publique.

#### Decidir tipo de entrada

Como os perfis devem entrar na jornada?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Ler público-alvo | Sequências de criação programadas; público-alvo conhecido processado em lote | Público avaliado no tempo de leitura; suporta leituras únicas ou recorrentes; até 20.000 perfis/s |
| Evento unitário | Acionadores comportamentais em tempo real (compra, abandono de carrinho) | Entrada em tempo real; requer transmissão de eventos; até 5.000 eventos/s |
| Qualificação do público-alvo | Entrada quando um perfil entra ou sai de um público-alvo em tempo quase real | Avaliação de transmissão; acionado pela alteração de associação de segmento |
| Evento comercial | O evento em toda a organização aciona a jornada para um público-alvo | Útil para lançamentos de produtos, eventos meteorológicos, alertas de sistema |

#### Decidir sobre a política de reentrada

Um perfil pode entrar novamente na jornada após concluir ou sair?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Permitir reentrada (com lista de opções) | Os perfis podem precisar repetir a jornada (compras recorrentes, reengajamento sazonal) | Redução mínima de 5 minutos; evita entradas duplicadas na janela de retificação |
| Sem reentrada | Jornadas únicas (integração, evento único de ciclo de vida) | O perfil conclui ou sai da jornada e não pode entrar novamente |

#### Decidir sobre as durações de espera entre pontos de contato

Por quanto tempo a jornada deve esperar entre cada mensagem?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Duração fixa (por exemplo, 3 dias) | Ritmo consistente independentemente do comportamento do perfil | Simples; tempo previsível; mínimo de 1 hora para jornadas lidas pelo público-alvo |
| Data/hora específica | A mensagem deve chegar em um horário preciso (por exemplo, data de renovação) | Usa o atributo de perfil ou a expressão para determinar a data/hora exata |
| Expressão personalizada | Espera dinâmica com base nos dados do perfil ou no contexto de jornada | Mais flexível; requer criação de expressão |

#### Decidir sobre as condições de ramificação

Quais condições determinam o caminho que um perfil toma?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Verificação de atributo de perfil | Ramificação baseada no nível de fidelidade, no interesse do produto e na geografia | Usa os dados do perfil disponíveis no momento da avaliação |
| Verificação de associação de segmento | Ramificação baseada no fato de o perfil pertencer a um público específico | Requer que o público-alvo seja definido e avaliado |
| Verificação de dados do evento | Ramificação baseada em se o perfil executou uma ação (email aberto, link clicado) | Avalia os dados do evento com escopo de jornada; útil para ramificação baseada em envolvimento |
| Divisão de porcentagem | Distribuir perfis aleatoriamente entre caminhos (para testes A/B ou implantações controladas) | Não usa dados de perfil; alocação puramente aleatória |

#### Decidir sobre os critérios de saída

Que evento ou condição faz com que um perfil saia da jornada antecipadamente?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Evento de conversão | O perfil conclui a ação desejada (compra, inscrição, envio de formulário) | Requer transmissão contínua de eventos; critérios de saída mais comuns |
| Saída da associação de público | O perfil deixa o público-alvo de entrada ou ingressa em um público-alvo de exclusão | É avaliado em tempo quase real para públicos de transmissão |
| Tempo limite | Duração máxima da jornada atingida (até 91 dias) | Rede de segurança padrão; configurável nas propriedades do jornada |
| Nenhum critério de saída | O perfil conclui todo o caminho de jornada naturalmente | Mais simples; todos os perfis percorrem a jornada completa, a menos que sejam removidos manualmente |

#### Decidir sobre o tempo limite da jornada

Qual é a duração máxima que um perfil pode permanecer na jornada?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| 91 dias (máximo) | Jornadas de longa duração (renovação trimestral, integração estendida) | Máximo permitido; os perfis que ainda estão na jornada no tempo limite são encerrados automaticamente |
| Duração menor personalizada | A Jornada deve ser concluída em uma janela definida (7 dias, 14 dias, 30 dias) | Definido com base no ciclo de vida natural do caso de uso |

#### Navegação na interface

- Criar jornada: Jornadas > Criar Jornada
- Propriedades da Jornada: tela de Jornada > painel Propriedades
- Nó de entrada: tela de Jornada > Arrastar &quot;Ler público-alvo&quot; ou atividade de evento
- Nós de ação: tela de Jornada > Ação Arrastar canal (email, SMS, push)
- Nós de condição: tela de Jornada > atividade Arrastar &quot;Condição&quot;
- Nós de espera: Jornada tela > Arrastar atividade &quot;Wait&quot;
- Critérios de saída: Jornada propriedades > Critérios de saída > Configurar
- Modo de teste: Tela de Jornada > Alternância do modo de teste
- Publicar: tela de Jornada > Publicar

#### Principais detalhes de configuração

- Nomeie a jornada com uma convenção clara e descritiva (por exemplo, &quot;Onboarding_Series_Email_v1&quot;)
- Definir o fuso horário da jornada para processamento consistente da etapa de espera
- Configure cada nó de ação com a superfície de canal apropriada e vincule ao conteúdo de mensagem criado
- Toda ramificação deve terminar com uma atividade Fim
- Configurar regras de reentrada apropriadas ao caso de uso
- Use o modo de teste com perfis de teste para simular o caminho de jornada completo antes de publicar
- Verifique se os perfis de teste percorrem os caminhos esperados e recebem as mensagens corretas

#### Onde as opções divergem

**Para Opção A (Leitura De Público-Alvo):**

- Arraste a atividade &quot;Read Audience&quot; como o nó de entrada
- Selecione o público-alvo definido na Fase 1
- Opcionalmente, configurar uma programação de leitura recorrente (diariamente, semanalmente)
- Configure o acelerador da taxa de leitura se a carga downstream do sistema for um problema

**Para Opção B (Acionado Por Evento):**

- Arraste o evento de acionamento como o nó de entrada
- Configurar o esquema de evento e as condições de entrada
- Defina as regras de reentrada com cuidado para evitar entradas duplicadas de eventos repetidos

**Para Opção C (Multicanal):**

- Use o método de entrada da Opção A ou B
- Em cada nó de ação, selecione a superfície de canal apropriada para esse ponto de contato
- Adicione nós de condição entre canais para verificar o engajamento (por exemplo, &quot;O perfil abriu o email?&quot;) e rotear para canais alternativos

#### Documentação do Experience League

- [Criar uma jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Propriedades da jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Ler atividade de público](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Eventos gerais](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Eventos de qualificação de público-alvo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [Adicionar uma mensagem em uma jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Atividade de condição](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Atividade aguardar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Critérios de saída](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [Atividade de término](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/end-activity)
- [Gerenciamento de entradas de jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Testar a jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [Publicar a jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)


### Fase 4: configurar o controle e a otimização

**Funções do aplicativo:** AJO: Frequency &amp; Business Rules, AJO: Gerenciamento de Conflitos e Prioridades, AJO: Experimentação de Conteúdo, RT-CDP: Consentimento e Imposição de Governança

Aplique limites de frequência para evitar o excesso de mensagens, atribua pontuações de prioridade para a resolução de conflitos com outras comunicações ativas, configure opcionalmente testes A/B nas mensagens do jornada e verifique a imposição de consentimento.

#### Decidir sobre a configuração de limite de frequência

As mensagens de jornada devem respeitar limites de frequência globais?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Aplicar regras de frequência | A jornada opera com outras campanhas e jornadas; os perfis não devem receber mensagens excessivas | As mensagens podem ser suprimidas se o perfil já tiver atingido o limite de outras comunicações |
| Isento de limite | As mensagens de jornada são críticas e sempre devem ser entregues (transacional, regulamentar) | Use com moderação; pode contribuir para a fadiga da mensagem se for usada em excesso |

#### Decidir atribuição de pontuação de prioridade

Como essa jornada deve ser classificada em relação a outras campanhas e jornadas ativas?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Alta prioridade (70-100) | As mensagens de jornada são comunicações críticas do ciclo de vida (integração, renovação) | Maior prioridade ganha quando surgem conflitos com outras comunicações |
| Prioridade do Medium (30-69) | As mensagens de jornada são importantes, mas não urgentes (educação, educação) | Pode ser suprimido por comunicações de prioridade mais alta |
| Prioridade baixa (0-29) | As mensagens de Jornada são complementares ou promocionais | Será suprimido ao concorrer com mensagens de prioridade mais alta |

#### Decidir sobre a experimentação de conteúdo

Alguma mensagem de jornada deve incluir um teste A/B ou multivariado?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Sim — teste A/B | Otimizar linhas de assunto, CTAs ou layouts de conteúdo em um ponto de contato específico | Requer volume suficiente por variante para significância estatística; 2 a 10 tratamentos suportados |
| Sem experimentação | O conteúdo é finalizado ou o volume é muito baixo para testes significativos | Configuração mais simples; não é necessário rastreamento de variantes |

#### Navegação na interface

- Regras de frequência: Administração > Regras de negócio > Criar regra
- Pontuações de prioridade: Jornada propriedades > Pontuação de prioridade
- Detecção de conflitos: Administração > Regras de negócios > Conflito e Prioridade
- Experimento de conteúdo: Jornada tela > Selecionar ação de mensagem > Alternar experimento de conteúdo
- Políticas de consentimento: Privacidade > Políticas > Políticas de consentimento

#### Principais detalhes de configuração

- Definir limites de frequência específicos do canal (por exemplo, máximo de 3 emails/semana, máximo de 1 SMS/dia, máximo de 2 push/dia)
- Atribua uma pontuação de prioridade à jornada (0-100) que reflete sua importância para os negócios em relação a outras comunicações ativas
- Revise o painel de detecção de conflitos para identificar campanhas ou jornadas sobrepostas
- Se estiver executando um experimento de conteúdo, defina variantes de tratamento, defina a alocação de tráfego, escolha a métrica de sucesso (aberturas, cliques ou conversões) e defina o limite de confiança (normalmente 95%)
- Verifique se a imposição de consentimento está ativa para cada canal usado na jornada

#### Documentação do Experience League

- [Regras de frequência](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Visão geral das regras de negócios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [Pontuações de prioridade](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Identificar possíveis conflitos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [Limite de jornada e arbitragem](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)
- [Introdução ao experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Criar um experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Consentimento no Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)


### Fase 5: configurar relatórios e monitoramento

**Funções do aplicativo:** AJO: Relatórios e análise de desempenho, monitoramento e observação, Relatórios e análise

Monitore a execução da jornada durante e após a ativação, revise as métricas de entrega e envolvimento por etapa, configure alertas para falhas de processamento de jornada e, opcionalmente, crie a análise de espaço de trabalho do CJA para visualização detalhada de funnel e fallout.

#### Decidir sobre o método de relatório

Quais ferramentas de relatório são necessárias para essa jornada?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Somente relatórios nativos do AJO | O monitoramento básico da entrega e do envolvimento é suficiente | Relatório ao vivo (durante a execução) e Relatório de tempo todo (pós-execução); atualiza a cada 60 segundos para ficar ativo |
| Análise do AJO + CJA | É necessária uma análise profunda do funnel, taxas de conversão de etapa, visualização de fallout ou comparação entre jornadas | Requer conexão com o CJA e visualização de dados vinculadas aos conjuntos de dados do AJO; mais abrangente |
| Somente CJA | A organização usa o CJA como a plataforma de análise principal | Requer configuração do CJA; os relatórios nativos do AJO ainda estão disponíveis como backup |

#### Decidir sobre a configuração de alertas

Quais falhas de jornada devem acionar alertas?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Jornada alertas de processamento | Sempre recomendado para jornadas de produção | Alertas sobre falhas de entrada de perfil, erros de nó de ação e interrupções de jornada |
| Alertas de falha de entrega | Essencial para jornadas com comunicações de alto valor | Alertas sobre taxas de rejeição que excedem os limites, falhas de delivery |

#### Navegação na interface

- Jornada relatório ao vivo: Jornadas > Selecionar jornada > Relatório ao vivo
- Jornada relatório a todo momento: Jornadas > Selecionar jornada > Relatório a todo momento
- Alertas: Alertas > Regras de alerta > Assinar
- Espaço de trabalho do CJA: Projetos > Criar novo projeto

#### Principais detalhes de configuração

- Acesse o relatório em tempo real durante a execução do jornada para monitorar entradas de perfil, saídas e métricas de entrega por etapa em tempo real
- Após a conclusão da jornada (ou após o acúmulo de dados suficientes), revise o Relatório de todos os tempos para obter uma análise abrangente
- Configurar alertas da plataforma para falhas de processamento e problemas de entrega do jornada
- Para análise do CJA, verifique se a conexão do CJA inclui conjuntos de dados de eventos de experiência do AJO (Feedback de mensagem, Rastreamento de email, Eventos de etapa de Jornada)
- Criar uma CJA Workspace com:
   - Visualização do funnel mostrando as contagens de perfil em cada etapa da jornada
   - Visualização de fallout para identificar pontos de devolução
   - Cálculos da taxa de conversão da etapa
   - Análise do tempo para conversão
   - Detalhamento de engajamento no nível do canal (para jornadas multicanal)

#### Documentação do Experience League

- [Relatório em tempo real da jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Jornada relatório global](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabalhar com o Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Visão geral de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Visão geral do Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Guia de integração do AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## Considerações de implantação

Revise as seguintes medidas de proteção, armadilhas, práticas recomendadas e compensações antes e durante a implementação.

### Medidas de proteção e limites

- Máximo de **500 jornadas ativas** por sandbox — [medidas de proteção da Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- A duração máxima de **jornada é de 91 dias** (tempo limite global) — os perfis que ainda estão na jornada no tempo limite são encerrados automaticamente
- Máximo de **50 atividades** por tela de jornada
- Ler jornadas do Audience processa até **20.000 perfis por segundo** (limite padrão)
- As jornadas de eventos unitários suportam até **5.000 eventos por segundo** por sandbox
- As etapas de espera têm uma **duração mínima de 1 hora** para jornadas lidas por público
- Jornada **o mínimo de restrição de reentrada é de 5 minutos**
- Máximo de **10 superfícies de canal por tipo de canal** por sandbox
- Tamanho máximo de email de **100 KB** recomendado para entrega ideal
- Máximo de **30 fragmentos de conteúdo** por mensagem
- Máximo de **10 tratamentos de experimento de conteúdo** (variantes) por experimento
- Máximo de **10 configurações de limite** por sandbox
- Máximo de **4.000 definições de segmento** por sandbox

### Armadilhas comuns

- **Publicação sem teste:** sempre use o modo de teste com perfis de teste para validar o caminho de jornada completo antes de publicar. Verifique se os perfis percorrem as ramificações esperadas, se as etapas de espera avançam corretamente e se as mensagens são renderizadas corretamente.
- **Atividades de fim ausentes em ramificações:** Cada ramificação de jornada deve terminar com uma atividade End. A jornada não será publicada se qualquer ramificação for deixada sem um nó de encerramento.
- **Condições de entrada muito amplas:** Uma condição de evento ou público-alvo de entrada definido de forma livre pode inundar a jornada com perfis não intencionais. Refinar critérios de entrada com verificações de atributo e regras de supressão específicas.
- **Ignorando regras de reentrada:** Para jornadas acionadas por eventos, os perfis podem acionar o evento de acionamento várias vezes. Sem a configuração de reentrada adequada (negar a reentrada ou o período de controle), os perfis podem se acumular na jornada, causando mensagens duplicadas.
- **Confusão de fuso horário da etapa de espera:** as durações de espera são processadas em UTC. Defina o fuso horário da jornada explicitamente nas propriedades da jornada para garantir que as etapas de espera avancem no horário local esperado.
- **Editar uma jornada em tempo real:** Não é possível editar jornadas em tempo real diretamente. Para fazer alterações, duplique a jornada, modifique a cópia, interrompa o original e publique a nova versão. Planeje o controle de versão do jornada antes de entrar em funcionamento.
- **Nenhum critério de saída definido:** sem critérios de saída, os perfis que convertem o mid-jornada continuarão recebendo mensagens subsequentes — possivelmente irrelevantes ou contraditórias. Sempre configure critérios de saída para eventos de conversão.
- **Desalinhamento de consentimento do canal:** É possível aceitar um perfil para email, mas não para SMS. As jornadas multicanal devem respeitar o consentimento por canal. Verifique se os campos de consentimento estão preenchidos e se são aplicados em cada superfície de canal.

### Práticas recomendadas

- **Comece simples, iterar:** Comece com uma jornada linear de 2 a 3 etapas antes de adicionar ramificações complexas. Valide o funcionamento do fluxo principal antes de dispor em camadas em condições e canais.
- **Usar convenções de nomenclatura descritiva:** Nomeie claramente os nós de jornada, as condições e as etapas de espera (por exemplo, &quot;Wait_3_Days_After_Welcome&quot; em vez de &quot;Wait 1&quot;). Isso facilita muito a depuração do modo de teste e a interpretação de relatórios.
- **Configure os critérios de saída antecipadamente:** Defina o evento de conversão como um critério de saída antes de criar os caminhos de jornada. Isso garante que os perfis que convertem sejam removidos da jornada, independentemente da etapa em que estão.
- **Defina durações de espera significativas:** Baseie as durações de espera nos dados de comportamento do cliente — tempo entre as interações típicas, janelas de resposta esperadas e cadência apropriada ao canal (por exemplo, 2 a 3 dias entre emails, 1 semana entre SMS).
- **Usar nós de condição para verificar o envolvimento:** Após uma ação de mensagem, adicione uma condição para verificar se o perfil está envolvido (aberto, clicado). Direcione perfis envolvidos para um caminho e perfis não envolvidos para um caminho de escalonamento ou canal alternativo.
- **Aproveite os atributos computados para ramificação:** Use atributos computados, como pontuações de engajamento, frequência de compra ou dias desde a última atividade, para tomar decisões de ramificação orientadas por dados em vez de arbitrárias.
- **Monitorar e otimizar interativamente:** Revise os relatórios do jornada semanalmente durante a execução inicial. Identifique pontos de devolução, ajuste as durações de espera, refine as condições e otimize o conteúdo da mensagem com base nos dados de desempenho por etapa.
- **Versão das jornadas:** Ao fazer alterações, duplique a jornada para criar uma nova versão. Mantenha um log de alterações de versão para rastreamento de auditoria e otimização.

### Decisões de compensação

As seguintes compensações devem ser avaliadas no contexto de suas necessidades específicas de negócios.

#### Entrada de leitura de público vs. entrada acionada por evento

A entrada lida pelo público-alvo fornece processamento previsível e baseado em lote, que é mais fácil de gerenciar e testar. A entrada acionada por eventos fornece capacidade de resposta em tempo real, mais relevante contextualmente, mas requer infraestrutura de transmissão e gerenciamento de reentrada mais cuidadoso.

- **O Audience-Read favorece:** previsibilidade, processamento em grandes volumes, programas de ciclo de vida agendados, testes mais simples
- **Favoritos acionados por evento:** relevância em tempo real, contexto comportamental, ritmo de perfil individual, resposta imediata às ações do cliente
- **Recomendação:** use público-alvo lido para programas de ciclo de vida planejado (integração, renovação) em que o tempo é orientado para os negócios. Use acionado por eventos para sequências de resposta comportamental (abandono do carrinho, pós-compra) em que o tempo é orientado pelo cliente.

#### Jornada de canal único vs. de vários canais

As jornadas de canal único são mais simples de implementar, testar e gerenciar. As jornadas multicanal fornecem recursos mais amplos de alcance e escalonamento, mas aumentam a complexidade na criação de conteúdo, no gerenciamento de consentimento e na governança de frequência.

- **Um único canal favorece:** Implementação mais rápida, gerenciamento de consentimento mais simples, menor esforço de produção de conteúdo, depuração mais fácil
- **Vários canais favorecem:** maior potencial de engajamento, escalonamento de canais para perfis não responsivos, experiência do cliente mais abrangente
- **Recomendação:** comece com uma jornada de canal único e valide o fluxo e o impacto nos negócios antes de expandir para vários canais. Adicione canais de forma incremental, onde os dados de engajamento mostram que o canal principal não está atingindo o público-alvo de maneira eficaz.

#### Complexidade de jornadas versus capacidade de gerenciamento

Uma jornada altamente ramificada com muitas condições e caminhos pode resolver mais cenários, mas se torna mais difícil de testar, depurar e otimizar. Uma jornada mais simples com menos ramificações é mais fácil de gerenciar, mas pode fornecer uma experiência menos personalizada.

- **Favoritos de jornadas complexas:** Personalização granular, caminhos específicos de segmento, cobertura abrangente de cenário
- **As jornadas mais simples favorecem:** implantação mais rápida, testes mais fáceis, relatórios mais claros, menor carga de manutenção
- **Recomendação:** Limite as jornadas a 3 a 5 ramificações principais e 15 a 25 atividades. Se a lógica exigir mais complexidade, considere dividir em várias jornadas com coordenação entre jornadas em vez de uma única jornada monolítica.

#### Rigidez do limite de frequência vs. conclusão da jornada

Limites de frequência estritos protegem contra mensagens excessivas, mas podem suprimir mensagens de jornada, fazendo com que os perfis pulem etapas e reduzindo as taxas de conclusão de jornada. Limites tolerantes garantem a entrega das mensagens de jornada, mas arriscam a fadiga do canal.

- **Limites rígidos favorecidos:** proteção da experiência do cliente, taxas reduzidas de cancelamento de inscrição, confiança na marca
- **Limites tolerantes favorecem:** taxas de conclusão de Jornada, entrega completa de sequência de mensagens, eficácia do programa de marketing
- **Recomendação:** atribua pontuações de prioridade mais altas às mensagens de jornada críticas (integração, renovação) para que tenham prioridade sobre as campanhas promocionais quando os limites forem atingidos. Reserve &quot;isento de limitação&quot; somente para comunicações realmente essenciais.

## Documentação relacionada

Os recursos a seguir fornecem detalhes adicionais sobre os recursos usados nesta implementação.

### Jornadas

- [Introdução ao jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Criar uma jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Propriedades da jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Publicar a jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)
- [Testar a jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)

### Jornada atividades

- [Ler atividade de público](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Eventos gerais](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Eventos de qualificação de público-alvo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [Atividade de condição](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Atividade aguardar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Adicionar uma mensagem em uma jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Atividade de término](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/end-activity)
- [Configurar uma ação personalizada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions)

### Gerenciamento de entrada e saída

- [Gerenciamento de entradas de jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Critérios de saída](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)

### Configuração de canais

- [Introdução à configuração de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Configurar superfícies do canal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Delegar subdomínios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Criar pools de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [Planos de aquecimento de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Configurar canal de SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configurar canal de notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Criação e personalização de mensagens

- [Criar um email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [Criar conteúdo de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Usar componentes de conteúdo do Email Designer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/content-components)
- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxe do Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Funções auxiliares](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabalhar com modelos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabalhar com fragmentos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Visualizar e testar o conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### Experimentação de conteúdo

- [Introdução ao experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Criar um experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Relatório de experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Cálculos estatísticos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

### Frequência, conflito e prioridade

- [Regras de frequência](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Visão geral das regras de negócios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [Introdução ao gerenciamento de conflitos e prioridades](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Pontuações de prioridade](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Limite de jornada e arbitragem](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)
- [Identificar possíveis conflitos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)

### Públicos-alvo e segmentação

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Referência do Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)
- [Segmentação de transmissão](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/api/streaming-segmentation)
- [Segmentação de borda](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/api/edge-segmentation)

### Relatórios e análises

- [Relatório em tempo real da jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Jornada relatório global](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabalhar com o Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Guia de integração do AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Visão geral do Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Visão geral do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)

### Consentimento e governança

- [Consentimento no Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Gerenciar lista de supressão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Base de dados

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Visão geral do perfil](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [Visão geral de atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
