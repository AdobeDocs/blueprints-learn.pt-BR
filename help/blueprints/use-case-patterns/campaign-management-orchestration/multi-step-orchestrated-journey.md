---
title: Jornada orquestrada em várias etapas
description: Saiba como guiar um perfil por meio de uma jornada multitoque com esperas, condições e várias ações de mensagem ao longo do tempo.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 5667b188-1b20-4a85-aebb-74efd5f771a1
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1798'
ht-degree: 5%

---

# Jornada orquestrada em várias etapas

Este guia descreve o padrão de caso de uso de jornada orquestrada em várias etapas, que usa o [!DNL Adobe Journey Optimizer] (AJO) e o [!DNL Real-Time Customer Data Platform] (RT-CDP) para orquestrar jornadas de clientes multitoque de ramificação que entregam várias mensagens ao longo do tempo. Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam entender o que esse padrão faz, os objetivos de negócios que ele aceita, os casos de uso táticos que ele permite e os aplicativos Adobe envolvidos.

## Padrão do caso de uso

**Jornada Orquestrada Em Várias Etapas**

Guie um perfil por meio de uma jornada multitoque com esperas, condições e várias ações de mensagem ao longo do tempo.

**Plano de execução:** Avaliação de público-alvo > Execução de Jornada (vários nós) > Ramificação de condição > Entrega de mensagem (xN) > Critérios de saída > Relatórios

## Visão geral do caso de uso

As jornadas orquestradas em várias etapas abordam cenários de negócios em que uma única mensagem é insuficiente para alcançar o resultado desejado pelo cliente. Em vez de um envio único, a jornada orienta cada perfil por uma sequência de pontos de contato — emails, mensagens SMS, notificações por push ou mensagens no aplicativo — espaçados por dias ou semanas, com uma lógica de ramificação que adapta o caminho com base em atributos de perfil, sinais comportamentais ou dados de evento.

Essas jornadas são o padrão de campanha mais complexo no AJO. Eles combinam entrada baseada em público ou evento com uma tela de nós de ação (mensagens), nós de condição (lógica de ramificação), nós de espera (atrasos de tempo) e critérios de saída (eventos de conversão ou tempos limite). Cada perfil avança pela jornada independentemente, em seu próprio ritmo, recebendo conteúdo contextualmente relevante em cada etapa.

Esse padrão inclui os padrões mais simples — ativação de mensagens de saída em lote para campanhas de envio único e mensagens acionadas por evento para respostas de evento único. Use esse padrão quando o caso de uso exigir a criação de um perfil por meio de várias interações ao longo do tempo.

>[!NOTE]
>Se sua jornada exigir seleção dinâmica da oferta, conteúdo ou canal ideal em pontos de decisão individuais, consulte [jornada entre canais com decisão](cross-channel-journey-with-decisioning.md). Esse padrão amplia esse com a integração do AJO Decisioning.

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

[Saiba mais sobre como melhorar a retenção do cliente](/help/blueprints/business-objectives/customer-experience/improve-customer-retention.md)

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

## Aplicativos

Os aplicativos a seguir são usados para implementar esse padrão de caso de uso.

- **[!DNL Adobe Journey Optimizer] (AJO)** — mecanismo de orquestração de Jornadas, criação de mensagens, configuração de canais, experimentação de conteúdo, gerenciamento de frequência e conflitos e relatórios
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** — Avaliação e definição de público-alvo para públicos-alvo de entrada de jornada, dados de perfil para personalização e ramificação de condição
- **[!DNL Adobe Experience Platform] (AEP)** — Armazenamento de perfil, serviço de identidade, assimilação de dados de evento e infraestrutura de dados de base

## Documentação relacionada

Os recursos a seguir fornecem detalhes adicionais sobre os recursos usados nesta implementação.

### Jornadas

- [Introdução às jornadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Criar uma jornada](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
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
