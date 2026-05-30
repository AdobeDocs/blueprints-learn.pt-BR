---
title: Mensagens acionadas por evento
description: Saiba como fornecer mensagens contextuais em tempo real em resposta a eventos comportamentais ou do sistema.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 75137990-9848-40c0-abf3-adbd21d2de52
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1955'
ht-degree: 5%

---

# Mensagens acionadas por evento

Este guia descreve o padrão de caso de uso de mensagem acionada por evento, que usa [!DNL Adobe Journey Optimizer] (AJO), [!DNL Real-Time Customer Data Platform] (RT-CDP) e [!DNL Adobe Experience Platform] (AEP) para entregar mensagens contextuais em tempo real em resposta a eventos comportamentais ou do sistema. Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam entender o que esse padrão faz, os objetivos de negócios que ele aceita, os casos de uso táticos que ele permite e os aplicativos Adobe envolvidos.

Esse padrão abrange o ciclo de vida completo, desde a assimilação de eventos e a criação de jornadas até a entrega de mensagens e a geração de relatórios de desempenho.

## Padrão do caso de uso

Esta seção descreve o padrão principal e o plano de execução que direciona as mensagens acionadas por eventos.

**Mensagens acionadas por Evento**

Analise um evento comportamental ou de sistema em tempo real e entregue uma mensagem contextual ao perfil de acionamento.

**Plano de execução:** Assimilação de evento > Entrada de Jornada > Avaliação de condição > Entrega de mensagem > Relatórios

## Visão geral do caso de uso

As mensagens acionadas por eventos fornecem uma mensagem contextual em resposta a um evento comportamental ou do sistema em tempo real. Diferentemente da ativação de mensagem de saída em lote, que envia para um público-alvo pré-avaliado em uma programação, esse padrão escuta um evento qualificado — como um abandono de carrinho, uma sessão de navegação, um envio de formulário ou uma alteração de status do sistema — e insere imediatamente o perfil de acionamento em uma jornada que avalia as condições e entrega uma mensagem.

O padrão depende da transmissão de eventos em tempo real para o AEP (via Web SDK, Mobile SDK ou API do lado do servidor), de uma jornada com uma entrada de evento unitária no AJO e de uma lógica de avaliação de condição que determina se e o que enviar. Normalmente, a mensagem é enviada em minutos após o evento de acionamento, tornando esse padrão ideal para comunicações sensíveis ao tempo e contextualmente relevantes.

As organizações usam esse padrão para responder às ações do cliente em tempo real, aumentando a relevância e gerando taxas de participação e conversão mais altas em comparação às comunicações programadas em lote. Cenários comuns incluem recuperação de carrinho abandonado, acompanhamento pós-compra, mensagens de boas-vindas após o registro e notificações sensíveis ao tempo, como falhas de pagamento ou alertas de queda de preço.

## Principais objetivos de negócios

Os seguintes objetivos de negócios são compatíveis com esse padrão de caso de uso.

**[Recuperar carrinhos abandonados e jornadas](../../business-objectives/customer-experience/recover-abandoned-carts-journeys.md)**

Reenvolva os usuários que abandonaram o durante os fluxos de compra, aplicativo ou inscrição com acompanhamentos oportunos e personalizados.

| KPIs |
| --- |
| Taxas de conversão, receita incremental, envolvimento |

**[Aumentar taxas de conversão](../../business-objectives/revenue-monetization/increase-conversion-rates.md)**

Melhore a porcentagem de visitantes e prospetos que concluem as ações desejadas, como compras, inscrições ou envios de formulários.

| KPIs |
| --- |
| Taxas De Conversão, Conversão De Clientes Potenciais, Custo Por Cliente Potencial |

**[Fornecer experiências personalizadas ao cliente](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**

Personalize conteúdo, ofertas e mensagens para preferências individuais, comportamentos e estágios do ciclo de vida.

| KPIs |
| --- |
| Envolvimento, taxas de conversão, satisfação do cliente (CSAT) |

**[Melhore a integração do cliente](../../business-objectives/customer-experience/improve-customer-onboarding.md)**

Acelere o tempo de implantação para novos clientes com experiências de boas-vindas e jornadas de ativação simplificadas e personalizadas.

| KPIs |
| --- |
| Taxas de engajamento, retenção e conversão |

## Exemplo de casos de uso tático

Os cenários a seguir ilustram como as mensagens acionadas por eventos podem ser aplicadas em diferentes contextos de negócios.

- **Email de abandono de carrinho ou SMS** — Envie uma mensagem de lembrete quando um cliente adicionar itens ao carrinho, mas não concluir a compra em uma janela de tempo definida
- **Acompanhamento de abandono de navegação** — Reenvolva os visitantes que visualizaram produtos ou conteúdo, mas não realizaram uma ação de conversão
- **Venda cruzada ou agradecimento pós-compra** — forneça uma confirmação e uma recomendação de venda cruzada imediatamente após um evento de compra
- **Lembrete de expiração de avaliação** — Notifique os usuários que estão se aproximando do fim de uma avaliação gratuita com mensagens de renovação ou conversão
- **Mensagem de boas-vindas após o registro** — Enviar uma mensagem de integração imediata quando um novo usuário se registrar ou criar uma conta
- **Confirmação de envio de formulário** — Confirmar envios de formulário (solicitações de contato, inscrições, inscrições) com uma confirmação contextual
- **Notificação de falha de pagamento** — Alertar os clientes quando um pagamento recorrente falhar, solicitando que eles atualizem as informações de pagamento
- **Notificação por push de reversão de desinstalação de aplicativo** — Acionar uma mensagem de reversão quando um usuário desinstalar um aplicativo móvel
- **Confirmação de reserva ou compromisso** — Enviar confirmação imediata depois que uma reserva, reserva ou compromisso for agendado
- **Alerta de queda de preço para itens da lista de desejos** — Notifique os clientes quando um produto na lista de desejos cair no preço

## Indicadores-chave de desempenho

Os KPIs a seguir ajudam a medir a eficácia das implementações de mensagens acionadas por eventos.

| KPI | Descrição | Abordagem de medição |
| --- | --- | --- |
| Índice de conversão | Porcentagem de destinatários de mensagens acionadas que concluíram a ação desejada (compra, inscrição, renovação) | Conversões/Mensagens Entregues * 100 |
| Receita incremental | Receita adicional atribuível a mensagens acionadas por eventos em comparação a grupos de controle sem envio | Receita de envios acionados - Linha de base do grupo de controle |
| Taxa de abertura | Porcentagem de mensagens entregues abertas por destinatários | Aberturas/Entregues * 100 |
| Índice de click-through (CTR) | Porcentagem de mensagens entregues que geram pelo menos um clique | Cliques/Entregues * 100 |
| Tempo para conversão | Tempo médio decorrido entre a entrega de mensagens e o evento de conversão | Avg(carimbo de data e hora de conversão - carimbo de data e hora de entrega) |
| Taxa de conclusão da jornada | Porcentagem de perfis que entram na jornada e atingem a etapa de entrega de mensagens (não descartados por condições ou saídas) | Perfis que atingem o delivery/Perfis que entram no jornada * 100 |
| Taxa de supressão de mensagens | Porcentagem de perfis qualificados suprimidos devido a limites de frequência, consentimento ou avaliação de condição | Perfis suprimidos/Total de perfis qualificados * 100 |
| Taxa de rejeição | Porcentagem de mensagens que não puderam ser entregues devido a devoluções permanentes ou temporárias | Devoluções / Enviado * 100 |

## Aplicativos

Os seguintes aplicativos da Adobe são usados neste padrão de caso de uso.

- **[!DNL Adobe Journey Optimizer] (AJO)** — Orquestração de Jornadas com entrada de evento unitária, avaliação de condição, etapas de espera, criação de mensagens, configuração de canal, governança de frequência e relatórios de entrega
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** — Avaliação de público-alvo para filtragem baseada em condição em jornadas, imposição de consentimento e governança, enriquecimento de perfil
- **[!DNL Adobe Experience Platform] (AEP)** — Assimilação de eventos em tempo real via Web SDK, Mobile SDK ou API do lado do servidor; modelagem de dados; resolução de identidade; Edge Network

## Documentação relacionada

Os recursos a seguir fornecem detalhes adicionais sobre os recursos usados nesta implementação.

### Jornada orquestração

- [Introdução às jornadas](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Criar uma jornada](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Propriedades da jornada](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Eventos gerais](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Eventos de qualificação de público-alvo](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [Atividade de condição](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Atividade aguardar](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Adicionar uma mensagem em uma jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Critérios de saída](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [Gerenciamento de entradas de jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Testar a jornada](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [Publicar a jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

### Configuração de canais

- [Introdução à configuração de email](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegar subdomínios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Criar pools de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [Planos de aquecimento de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Configurações de superfície de email](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Configurar canal de SMS](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configurar canal de notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [Gerenciar lista de supressão](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Criação e personalização de mensagens

- [Criar um email](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/email/create-email)
- [Criar conteúdo de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxe do Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Funções auxiliares](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabalhar com modelos de conteúdo](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabalhar com fragmentos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Visualizar e testar o conteúdo](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [Criar uma mensagem SMS](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/sms/create-sms)
- [Criar uma notificação por push](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/push/design-push)

### Frequência e regras de negócio

- [Regras de frequência](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Visão geral das regras de negócios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [API de limite](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/channel-surfaces/capping)

### Gerenciamento de conflitos e prioridades

- [Introdução ao gerenciamento de conflitos e prioridades](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Identificar possíveis conflitos](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [Pontuações de prioridade](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Limite de jornada e arbitragem](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/conflict-prioritization/journey-capping)

### Relatórios e desempenho

- [Relatório em tempo real da jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Jornada relatório global](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Guia de integração do AJO + CJA](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

### Coleta e assimilação de dados

- [Visão geral do Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/web-sdk/home)
- [Visão geral do Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Visão geral da API do Edge Network Server](https://experienceleague.adobe.com/pt-br/docs/experience-platform/edge-network-server-api/overview)
- [Configurar sequências de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/datastreams/configure)
- [Visão geral da assimilação de streaming](https://experienceleague.adobe.com/pt-br/docs/experience-platform/ingestion/streaming/overview)

### Modelagem de dados e esquemas

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/home)
- [Noções básicas de composição de esquema](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/schema/composition)

### Identidade e perfil

- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/home)
- [Visão geral dos namespaces de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/namespaces)
- [Regras de vinculação do gráfico de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/identity-linking-logic)
- [Visão geral do perfil](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/home)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/merge-policies/overview)

### Segmentação e públicos

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentação de transmissão](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/methods/streaming-segmentation)

### Governança e consentimento de dados

- [Visão geral da governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/home)
- [Visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview)
- [Grupo de campos Consentimento e preferências](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/field-groups/profile/consents)
- [Consentimento no Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### Atributos computados

- [Visão geral de atributos computados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/computed-attributes/overview)
- [Guia da interface de atributos computados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/computed-attributes/ui)

### Monitorização e observabilidade

- [Visão geral de alertas](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/alerts/overview)
- [Visão geral dos Insights de observação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/home)

### Medidas de proteção

- [Medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/get-started/guardrails)
- [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/guardrails)
- [Medidas de proteção de assimilação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/ingestion/guardrails)

### Tutoriais e guias

- [Criar um tutorial do jornada](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Instalar o Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/web-sdk/install/overview)
