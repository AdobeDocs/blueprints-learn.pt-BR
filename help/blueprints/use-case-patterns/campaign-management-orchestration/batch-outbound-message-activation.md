---
title: Ativação de mensagem de saída em lote
description: Saiba como avaliar um público-alvo e fornecer uma mensagem de saída agendada em uma única execução em lote.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 192853ce-02ab-46e6-9092-3db5354bc19c
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1701'
ht-degree: 4%

---

# Ativação de mensagem de saída em lote

Este guia descreve o padrão de caso de uso de ativação de mensagem de saída em lote, que usa o [!DNL Adobe Journey Optimizer] (AJO) e o [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP) para entregar mensagens de saída agendadas a segmentos de público-alvo definidos. Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam entender o que esse padrão faz, os objetivos de negócios que ele aceita, os casos de uso táticos que ele permite e os aplicativos Adobe envolvidos.

A ativação de mensagens de saída em lote é o padrão de campanha fundamental para mensagens de saída de um para muitos. Ele abrange todo o ciclo de vida, desde a definição do público-alvo até a entrega de mensagens e a análise de desempenho.

## Padrão do caso de uso

**Ativação de mensagem de saída em lote**

Avalie um público-alvo e entregue uma mensagem de saída agendada (email, SMS, push) para todos os perfis qualificados em uma única execução em lote.

**Plano de execução:** Avaliação de público-alvo > Criação de mensagem > Execução de campanha > Relatórios

## Visão geral do caso de uso

As organizações geralmente precisam enviar uma única mensagem para um segmento de público-alvo conhecido em um momento específico ou em resposta a um evento do sistema. Este padrão atende a esse requisito combinando a avaliação de público em [!DNL RT-CDP] com a criação de mensagens e a execução de campanha em [!DNL Journey Optimizer].

O cenário de negócios é simples: definir quem deve receber a mensagem, criar o conteúdo da mensagem com personalização, vincular o público-alvo e a mensagem a uma campanha ou jornada e executar o envio de acordo com uma programação, por meio da qualificação de público-alvo ou por meio de um acionador do sistema. O resultado é uma mensagem entregue com relatórios completos sobre entrega, envolvimento e métricas de conversão.

Esse padrão se aplica sempre que um objetivo comercial pode ser avançado ao fornecer uma única mensagem a um público-alvo conhecido em uma execução. Ela é diferente das mensagens acionadas por eventos, que respondem a eventos comportamentais em tempo real, e das jornadas orquestradas em várias etapas, que orientam os perfis por vários pontos de contato ao longo do tempo. A ativação em lote é o padrão de campanha mais simples e o ponto de partida mais comum para casos de uso de mensagens de saída.

## Principais objetivos de negócios

Esta seção identifica os principais objetivos de negócios compatíveis com a ativação de mensagens de saída em lote.

### Aumentar o engajamento do email e da campanha

**Descrição:** Melhore as taxas de abertura, as taxas de click-through e a resposta geral da campanha por meio de conteúdo e direcionamento otimizados.

**KPIs:** Taxas de Abertura, Envolvimento, Taxas de Conversão

### Aumentar receita e vendas

**Descrição:** Impulsione o crescimento da receita principal por meio de canais digitais otimizados, campanhas e jornadas do cliente.

**KPIs:** Taxas de Conversão, Receita Incremental, Valor Médio de Pedido

**Objetivo comercial relacionado:** [Aumentar receita e vendas](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)

### Simplificar a execução da campanha

**Descrição:** reduza o tempo de compilação da campanha e simplifique a entrega de campanhas multicanal por meio de modelos, automação e processos padronizados.

**KPIs:** Velocidade de Comercialização, Eficiência, Conclusão no Prazo %

## Exemplo de casos de uso tático

Os cenários a seguir ilustram aplicativos comuns de ativação de mensagens de saída em lote.

- **Anúncio de venda ou explosão de email promocional** — Transmita uma oferta promocional para um segmento de clientes qualificados em uma data agendada
- **Notificação por push de lançamento de produto** — Notifique os clientes interessados sobre uma nova disponibilidade de produto por push
- **Email de resumo ou informativo** — forneça resumos periódicos de conteúdo aos públicos-alvo dos assinantes
- **Convite de registro em eventos** — Convide clientes potenciais qualificados para webinários, conferências ou eventos presenciais
- **Email de lembrete sobre a renovação da assinatura** — Lembrar os clientes que estão se aproximando das datas de renovação de tomar medidas
- **Notificação de marcos do programa de fidelidade** — parabenize os membros que atingem níveis de fidelidade ou limites de ponto
- **Email específico do call-to-action** — oriente uma ação direcionada, como concluir uma compra, atualizar preferências ou registrar-se em um programa
- **Campanha por SMS para promoção rápida ou oferta com limite de tempo** — envie promoções urgentes e com limite de tempo via SMS para públicos-alvo de aceitação

## Indicadores-chave de desempenho

A tabela a seguir define os KPIs usados para medir a eficácia da campanha.

| KPI | Descrição | Abordagem de medição |
| --- | --- | --- |
| Taxa de entrega | Porcentagem de mensagens entregues com êxito aos destinatários | Entregue/Enviado x 100 |
| Taxa de abertura | Porcentagem de mensagens entregues abertas por destinatários | Aberturas/Entregas únicas x 100 |
| Índice de click-through (CTR) | Porcentagem de mensagens entregues em que um link foi clicado | Cliques únicos/Entregue x 100 |
| Índice de clique para abrir (CTOR) | Porcentagem de mensagens abertas em que um link foi clicado | Cliques únicos / Aberturas únicas x 100 |
| Índice de conversão | Porcentagem de destinatários que concluíram a ação desejada | Conversões / Entregues x 100 |
| Taxa de cancelamento de inscrição | Porcentagem de destinatários que cancelaram a inscrição após receber a mensagem | Cancelamentos de assinatura/Enviado x 100 |
| Taxa de rejeição | Porcentagem de mensagens que não puderam ser entregues | Devoluções / Enviado x 100 |
| Receita por email enviado | Receita atribuída à campanha dividida pelas mensagens enviadas | Receita Total / Enviado |

## Aplicativos

Os aplicativos a seguir são usados para implementar esse padrão.

- **[!DNL Adobe Journey Optimizer](AJO)** — Criação de mensagens, configuração de canal, execução de campanha, orquestração de jornadas, experimentação de conteúdo, regras de frequência e relatórios
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)** — Avaliação de público, consentimento e imposição de governança
- **[!DNL Adobe Experience Platform](AEP)** — Armazenamento de perfil, serviço de identidade, esquemas, conjuntos de dados, coleta de dados

## Documentação relacionada

Esta seção fornece links abrangentes para a documentação do [!DNL Experience League], organizados por tópico.

### Campanhas

- [Introdução às campanhas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Criar uma campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Campanhas acionadas por API](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)

### Jornadas

- [Introdução às jornadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Ler jornada de público-alvo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)

### Configuração de canais

- [Introdução à configuração de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegar subdomínios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Criar pools de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [Planos de aquecimento de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Configurações de superfície de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Configurar canal de SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configurar canal de notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [Gerenciar lista de supressão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Criação e personalização de mensagens

- [Criar um email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [Criar conteúdo de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Usar componentes de conteúdo do Email Designer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/content-components)
- [Importar ou codificar conteúdo de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/code-content)
- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxe do Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Funções auxiliares](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)

### Gestão de conteúdo

- [Trabalhar com modelos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabalhar com fragmentos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Visualizar e testar o conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [Enviar provas de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/proofs)
- [Renderização de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/email-rendering)

### Experimentação de conteúdo

- [Introdução ao experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Criar um experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Relatório de experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Cálculos estatísticos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

### Gerenciamento de frequência e conflitos

- [Regras de frequência](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Visão geral das regras de negócios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [Introdução ao gerenciamento de conflitos e prioridades](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Pontuações de prioridade](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Identificar possíveis conflitos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [Limite de jornada e arbitragem](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)

### Públicos-alvo e segmentação

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentação de transmissão](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentação de borda](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Composição de público](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Referência do Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### Relatório

- [Relatório em tempo real da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Relatório global da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Relatório em tempo real da jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Jornada relatório global](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabalhar com o Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Guia de integração do AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

### Governança e consentimento de dados

- [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview)
- [Grupo de campos Consentimento e preferências](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
- [Consentimento no Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### Modelagem de dados e identidade

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Noções básicas de composição de esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### Medidas de proteção

- [Medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Medidas de proteção de assimilação](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)

### Tutoriais e introdução

- [Introdução ao Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/get-started)
- [Criar sua primeira campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Criar a primeira jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
