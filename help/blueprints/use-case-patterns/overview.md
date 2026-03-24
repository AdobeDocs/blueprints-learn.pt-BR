---
title: Padrões de caso de uso
description: Saiba mais sobre os padrões de casos de uso para implementar o Adobe Experience Platform e aplicativos para atingir objetivos comerciais importantes.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
doc-type: overview-page
exl-id: 58caa6ad-0d1c-4290-9614-c68c9c9028bb
source-git-commit: 27f7e230982807ec70ca96af7f737944a6588f27
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# Padrões de caso de uso

Os padrões de caso de uso definem abordagens de implementação repetíveis para o Adobe Experience Platform e os aplicativos. Cada padrão descreve um recurso específico, a cadeia de funções que o fornece, os aplicativos envolvidos e os [principais objetivos de negócios](/help/blueprints/business-objectives/overview.md) aos quais ele dá suporte.

Use as tabelas abaixo para encontrar o padrão que corresponda às suas necessidades de implementação e, em seguida, siga o link para a referência de implementação completa, incluindo opções, fases, orientação de decisão e documentação do Experience League.

## Criação e ativação de público

Os padrões a seguir ajudam a criar, avaliar e ativar segmentos de público-alvo em canais e destinos.

| Padrão | Recurso principal | Soluções principais |
| --- | --- | --- |
| [Ativação de público-alvo para destinos](audience-building-activation/audience-activation-to-destinations.md) | Avaliar e publicar segmentos de público-alvo em destinos externos para direcionamento ou supressão | [!DNL Real-Time CDP] |
| [Collaboration de público-alvo](audience-building-activation/audience-collaboration-segment-match.md) | Compartilhar e corresponder segmentos de público-alvo em sandboxes ou organizações usando a Correspondência de segmentos | [!DNL Real-Time CDP], [!DNL Experience Platform] |
| [Encaminhamento de eventos](audience-building-activation/event-forwarding.md) | Encaminhar dados do evento em tempo real coletados pelo Edge Network para destinos que não sejam da Adobe | [!DNL Experience Platform] (Edge Network, encaminhamento de eventos) |
| [Ativação de público B2B](audience-building-activation/b2b-audience-activation.md) | Ativar públicos-alvo B2B baseados em conta nos canais da Web, de email e de publicidade | B2B edition [!DNL Real-Time CDP] |

## Personalização

Os padrões a seguir fornecem experiências personalizadas para visitantes conhecidos e desconhecidos em superfícies da Web e do aplicativo.

| Padrão | Recurso principal | Soluções principais |
| --- | --- | --- |
| [Personalização anônima da Web para visitantes](personalization/anonymous-visitor-web-personalization.md) | Fornecer conteúdo personalizado com base em sinais comportamentais na sessão para visitantes não identificados | [!DNL Journey Optimizer] (canal da Web), [!DNL Real-Time CDP] |
| [Personalização de aplicativo/Web de visitante conhecido](personalization/known-visitor-web-app-personalization.md) | Fornecer conteúdo personalizado, ofertas ou promoções para visitantes identificados com base no perfil em tempo real e na associação do segmento | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Offer Decisioning](personalization/offer-decisioning.md) | Use a lógica de decisão centralizada para selecionar a melhor oferta ou conteúdo para um perfil em todos os canais | [!DNL Journey Optimizer] (Decisionando), [!DNL Real-Time CDP] |
| [Recomendação comportamental](personalization/behavioral-recommendation.md) | Gerar recomendações de item e conteúdo usando estratégias de seleção e modelos de classificação | [!DNL Journey Optimizer] (Decisionando), [!DNL Real-Time CDP] |

## Gestão e orquestração de campanhas

Os padrões a seguir abordam a entrega de mensagens programada, acionada e em várias etapas entre canais.

| Padrão | Recurso principal | Soluções principais |
| --- | --- | --- |
| [Ativação de mensagem de saída em lote](campaign-management-orchestration/batch-outbound-message-activation.md) | Avalie um público-alvo e entregue uma mensagem de saída agendada em uma única execução em lote | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Mensagens acionadas por evento](campaign-management-orchestration/event-triggered-messaging.md) | Analise um evento comportamental ou do sistema em tempo real e entregue uma mensagem contextual ao perfil de acionamento | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [jornada orquestrada em várias etapas](campaign-management-orchestration/multi-step-orchestrated-journey.md) | Orientar um perfil por meio de uma jornada multitoque de ramificação com esperas, condições e várias ações de mensagem | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [jornada entre canais com decisão](campaign-management-orchestration/cross-channel-journey-with-decisioning.md) | Orquestrar uma jornada em várias etapas, incorporando a decisão em tempo real para selecionar o canal, conteúdo ou oferta ideal | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Comprando marketing baseado em grupo e gerenciamento de jornadas](campaign-management-orchestration/buying-group-based-marketing.md) | Desenvolver jornadas a nível de conta que qualifiquem leads em grupos de compras para melhorar a eficácia do marketing B2B | [!DNL Journey Optimizer] B2B edition, [!DNL Real-Time CDP] B2B edition |

## Análise

Os padrões a seguir oferecem suporte à análise comportamental e de desempenho entre canais.

| Padrão | Recurso principal | Soluções principais |
| --- | --- | --- |
| [Análise de clientes e geração de insight](analysis/customer-analytics-insight-generation.md) | Criar espaços de trabalho de análise entre canais, métricas calculadas e painéis para análise de comportamento e desempenho | [!DNL Customer Journey Analytics], [!DNL Experience Platform] |
| [Análise B2B](analysis/b2b-analytics.md) | Incluir informações a nível de conta B2B na análise de jornada de clientes entre canais | [!DNL Customer Journey Analytics] B2B edition, [!DNL Real-Time CDP] B2B edition |

## Experiência de conversa

Os padrões a seguir permitem interações conversacionais seguras para a marca e acionadas por IA em propriedades digitais.

| Padrão | Recurso principal | Soluções principais |
| --- | --- | --- |
| [experiência de conversação do Brand Concierge](conversational-experience/brand-concierge-conversational-experience.md) | Transforme propriedades digitais em experiências conversacionais habilitadas por IA e seguras para a marca que orientam a descoberta do cliente | [!DNL Brand Concierge], [!DNL Experience Platform], [!DNL Real-Time CDP] |

## Seletor de cenários

Use este guia quando um cenário couber em mais de um padrão. Responda às perguntas de ramificação para encontrar o padrão principal e, opcionalmente, estenda com os padrões listados.

### Conquista com a oferta de incentivo

*Um cliente decorrido não efetuou a compra há 90 dias. Você deseja engajá-los novamente com uma oferta direcionada.*

- **A seleção de ofertas é dinâmica (clientes diferentes recebem ofertas diferentes com base na qualificação ou classificação)?**
   - Sim → [Offer Decisioning](personalization/offer-decisioning.md) como a camada de oferta, encapsulada em [jornada orquestrada de várias etapas](campaign-management-orchestration/multi-step-orchestrated-journey.md) para a sequência de reengajamento
   - Não (mesma oferta para todos os clientes qualificados do programa de aprendizado) → [jornada orquestrada em várias etapas](campaign-management-orchestration/multi-step-orchestrated-journey.md) sozinha

### Acompanhamento pós-compra

*Um cliente acabou de concluir uma compra. Você deseja enviar uma confirmação, recomendação de venda cruzada e notificação de recompensa de fidelidade.*

- **A sequência requer ramificação adaptável com base em eventos em tempo real (por exemplo, recompensa reclamada, produto revisado)?**
   - Sim → [jornada orquestrada em várias etapas](campaign-management-orchestration/multi-step-orchestrated-journey.md)
   - Não (sequência fixa, sem ramificação) → [Ativação de mensagem de saída em lote](campaign-management-orchestration/batch-outbound-message-activation.md)
- **Inclui recomendações personalizadas de produtos?**
   - Sim → Estenda com [recomendação comportamental](personalization/behavioral-recommendation.md) na camada de conteúdo

### Personalização de marco de fidelidade

*Um cliente atinge uma nova camada de fidelidade. Você deseja mostrar conteúdo personalizado da Web e enviar uma mensagem de felicitações.*

- **O conteúdo da Web é personalizado (conteúdo diferente por camada ou segmento)?**
   - Sim → [Personalização de aplicativo/Web de visitante conhecido](personalization/known-visitor-web-app-personalization.md) para a superfície da Web
- **A mensagem de saída é um envio único ou uma sequência de criação?**
   - Envio único → [Mensagens acionadas por evento](campaign-management-orchestration/event-triggered-messaging.md)
   - Sequência → [jornada orquestrada em várias etapas](campaign-management-orchestration/multi-step-orchestrated-journey.md)

### Campanha de reengajamento

*Um segmento de usuários inativos precisa de uma sequência de reativação multitoque.*

- **As mensagens individuais precisam selecionar entre várias variantes de ofertas em tempo real?**
   - Sim → [jornada entre canais com decisão](campaign-management-orchestration/cross-channel-journey-with-decisioning.md)
   - Não → [jornada orquestrada em várias etapas](campaign-management-orchestration/multi-step-orchestrated-journey.md)
