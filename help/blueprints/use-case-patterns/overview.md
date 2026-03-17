---
title: Padrões de caso de uso
description: Saiba mais sobre os padrões de casos de uso para implementar o Adobe Experience Platform e aplicativos para atingir objetivos comerciais importantes.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
doc-type: overview-page
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Padrões de caso de uso

Os padrões de caso de uso definem abordagens de implementação repetíveis para o Adobe Experience Platform e os aplicativos. Cada padrão descreve um recurso específico, a cadeia de funções que o fornece, os aplicativos envolvidos e os [principais objetivos de negócios](/help/blueprints/business-objectives/overview.md) aos quais ele dá suporte.

Use as tabelas abaixo para encontrar o padrão que corresponda às suas necessidades de implementação e, em seguida, siga o link para a referência de implementação completa, incluindo opções, fases, orientação de decisão e documentação do Experience League.

## Criação e ativação de público

Os padrões a seguir ajudam a criar, avaliar e ativar segmentos de público-alvo em canais e destinos.

| Padrão | Recurso principal | Soluções principais |
| --- | --- | --- |
| [Audience Activation para Destinos](audience-building-activation/audience-activation-to-destinations.md) | Avaliar e publicar segmentos de público-alvo em destinos externos para direcionamento ou supressão | [!DNL Real-Time CDP] |
| [Audience Collaboration com correspondência de segmentos](audience-building-activation/audience-collaboration-segment-match.md) | Compartilhar e corresponder segmentos de público-alvo em sandboxes ou organizações usando a Correspondência de segmentos | [!DNL Real-Time CDP], [!DNL Experience Platform] |
| [Encaminhamento de eventos](audience-building-activation/event-forwarding.md) | Encaminhar dados do evento em tempo real coletados pelo Edge Network para destinos que não sejam da Adobe | [!DNL Experience Platform] (Edge Network, encaminhamento de eventos) |
| [Ativação de público-alvo B2B](audience-building-activation/b2b-audience-activation.md) | Ativar públicos-alvo B2B baseados em conta nos canais da Web, de email e de publicidade | B2B edition [!DNL Real-Time CDP] |

## Personalização

Os padrões a seguir fornecem experiências personalizadas para visitantes conhecidos e desconhecidos em superfícies da Web e do aplicativo.

| Padrão | Recurso principal | Soluções principais |
| --- | --- | --- |
| [Web Personalization de Visitante Anônimo](personalization/anonymous-visitor-web-personalization.md) | Fornecer conteúdo personalizado com base em sinais comportamentais na sessão para visitantes não identificados | [!DNL Journey Optimizer] (canal da Web), [!DNL Real-Time CDP] |
| [Personalization de Aplicativo/Web de Visitante Conhecido](personalization/known-visitor-web-app-personalization.md) | Fornecer conteúdo personalizado, ofertas ou promoções para visitantes identificados com base no perfil em tempo real e na associação do segmento | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Offer Decisioning](personalization/offer-decisioning.md) | Use a lógica de decisão centralizada para selecionar a melhor oferta ou conteúdo para um perfil em todos os canais | [!DNL Journey Optimizer] (Decisionando), [!DNL Real-Time CDP] |
| [Recomendação comportamental](personalization/behavioral-recommendation.md) | Gerar recomendações de item e conteúdo usando estratégias de seleção e modelos de classificação | [!DNL Journey Optimizer] (Decisionando), [!DNL Real-Time CDP] |

## Gestão e orquestração de campanhas

Os padrões a seguir abordam a entrega de mensagens programada, acionada e em várias etapas entre canais.

| Padrão | Recurso principal | Soluções principais |
| --- | --- | --- |
| [Ativação de mensagem de saída em lote](campaign-management-orchestration/batch-outbound-message-activation.md) | Avalie um público-alvo e entregue uma mensagem de saída agendada em uma única execução em lote | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Mensagens acionadas por Evento](campaign-management-orchestration/event-triggered-messaging.md) | Analise um evento comportamental ou do sistema em tempo real e entregue uma mensagem contextual ao perfil de acionamento | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Jornada Orquestrada Em Várias Etapas](campaign-management-orchestration/multi-step-orchestrated-journey.md) | Orientar um perfil por meio de uma jornada multitoque de ramificação com esperas, condições e várias ações de mensagem | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Jornada entre canais com decisão](campaign-management-orchestration/cross-channel-journey-with-decisioning.md) | Orquestrar uma jornada em várias etapas, incorporando a decisão em tempo real para selecionar o canal, conteúdo ou oferta ideal | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Comprando o Gerenciamento de Jornada e Marketing Baseado em Grupo](campaign-management-orchestration/buying-group-based-marketing.md) | Desenvolver jornadas a nível de conta que qualifiquem leads em grupos de compras para melhorar a eficácia do marketing B2B | [!DNL Journey Optimizer] B2B edition, [!DNL Real-Time CDP] B2B edition |

## Análise

Os padrões a seguir oferecem suporte à análise comportamental e de desempenho entre canais.

| Padrão | Recurso principal | Soluções principais |
| --- | --- | --- |
| [Análise de clientes e geração de Insight](analysis/customer-analytics-insight-generation.md) | Criar espaços de trabalho de análise entre canais, métricas calculadas e painéis para análise de comportamento e desempenho | [!DNL Customer Journey Analytics], [!DNL Experience Platform] |
| [Análises B2B](analysis/b2b-analytics.md) | Incluir informações a nível de conta B2B na análise de jornada de clientes entre canais | [!DNL Customer Journey Analytics] B2B edition, [!DNL Real-Time CDP] B2B edition |

## Experiência de conversa

Os padrões a seguir permitem interações conversacionais seguras para a marca e acionadas por IA em propriedades digitais.

| Padrão | Recurso principal | Soluções principais |
| --- | --- | --- |
| [Experiência de conversa do Brand Concierge](conversational-experience/brand-concierge-conversational-experience.md) | Transforme propriedades digitais em experiências conversacionais habilitadas por IA e seguras para a marca que orientam a descoberta do cliente | [!DNL Brand Concierge], [!DNL Experience Platform], [!DNL Real-Time CDP] |
