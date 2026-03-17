---
title: Catálogo de casos de uso
description: Procure casos de uso do setor por vertical, nível de maturidade ou padrão de implementação para encontrar o ponto de partida correto para sua jornada do Adobe Experience Platform.
doc-type: overview-page
exl-id: 7a3c2f1e-9b4d-4e6a-8f5c-2d1b3a4e7c9f
source-git-commit: 8ad59ff130dae13553f10049eb685cf557a73ead
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 6%

---

# Catálogo de casos de uso

Explore casos de uso do setor para [!DNL Adobe Experience Platform] e aplicativos. Navegue por setor para ver casos de uso por setor, por nível de maturidade para encontrar o ponto de partida correto para sua organização ou por padrão de implementação para entender qual abordagem técnica se adapta às suas necessidades.

Cada caso de uso vincula-se às orientações detalhadas de implementação por meio de um padrão de caso de uso, que descreve a cadeia de funções, os pontos de decisão e as etapas de configuração necessárias para dar vida ao caso de uso.

## Procurar por setor

>[!BEGINTABS]

>[!TAB Varejo]

As organizações de varejo usam o [!DNL Adobe Experience Platform] para unificar os dados de clientes de lojas online, locais físicos e programas de fidelidade em uma única visualização de cada comprador.

| | Caso de uso | Descrição | Maturidade | Padrão |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-product-recommendations.png" alt="Recomendações de produto personalizadas" width="40"> | [Recomendações personalizadas de produtos](retail/retail-overview.md#personalized-product-recommendations) | Mostrar produtos personalizados com base na navegação e no histórico de compras | [!BADGE Emergentes]{type=Informative} | [Recomendação comportamental](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-abandoned-cart.png" alt="Carrinho abandonado" width="40"> | [Recuperação de email de carrinho abandonado](retail/retail-overview.md#abandoned-cart-email-recovery) | Enviar lembretes personalizados para carrinhos de compras abandonados | [!BADGE Básico]{type=Neutral} | [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-inventory-urgency.png" alt="Urgência do inventário" width="40"> | [Campanhas de urgência baseadas em inventário](retail/retail-overview.md#inventory-based-urgency-campaigns) | Acionar alertas em tempo real quando o inventário de produtos estiver baixo | [!BADGE Básico]{type=Neutral} | [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-cross-sell-upsell.png" alt="Venda cruzada venda adicional" width="40"> | [Recomendações de venda cruzada e venda adicional](retail/retail-overview.md#cross-sell-and-upsell-recommendations) | Exibir produtos relevantes de venda cruzada e venda adicional na finalização da compra e por email | [!BADGE Avançado]{type=Caution} | [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) |
| <img src="assets/use-case-icons/icon-welcome-series.png" alt="Série de boas-vindas" width="40"> | [Nova Série de Boas-vindas ao Cliente](retail/retail-overview.md#new-customer-welcome-series) | Automatize uma série de boas-vindas de vários emails com recomendações personalizadas | [!BADGE Emergentes]{type=Informative} | [Jornada Orquestrada Em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-price-drop.png" alt="Queda de preço" width="40"> | [Alertas de Queda de Preço](retail/retail-overview.md#price-drop-alerts) | Notificar os clientes quando a lista de desejos ou os itens visualizados caírem no preço | [!BADGE Básico]{type=Neutral} | [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-replenishment.png" alt="Reposição" width="40"> | [Lembretes de Reposição](retail/retail-overview.md#replenishment-reminders) | Enviar lembretes automatizados para produtos de consumo comprados regularmente | [!BADGE Emergentes]{type=Informative} | [Jornada Orquestrada Em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-category-pages.png" alt="Páginas de categoria" width="40"> | [Páginas de categoria personalizadas](retail/retail-overview.md#personalized-category-pages) | Reordenar dinamicamente páginas de categoria com base nas preferências de cada cliente | [!BADGE Emergentes]{type=Informative} | [Recomendação comportamental](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-post-purchase.png" alt="Pós-compra" width="40"> | [Campanhas de acompanhamento pós-compra](retail/retail-overview.md#post-purchase-follow-up-campaigns) | Enviar dicas de atendimento, solicitações de revisão e sugestões de produtos relacionadas | [!BADGE Emergentes]{type=Informative} | [Jornada Orquestrada Em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| | [Ofertas exclusivas de clientes do VIP](retail/retail-overview.md#vip-customer-exclusive-offers) | Fornecer ofertas exclusivas e acesso antecipado a clientes de alto valor | [!BADGE Avançado]{type=Caution} | [Jornada entre canais com decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) |
| | [Notificações de Falta de Estoque](retail/retail-overview.md#out-of-stock-notifications) | Notificar os clientes quando produtos indisponíveis estiverem disponíveis | [!BADGE Básico]{type=Neutral} | [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| | [Personalization de prova social](retail/retail-overview.md#social-proof-personalization) | Exibir análises e classificações personalizadas com base no perfil do cliente | [!BADGE Emergentes]{type=Informative} | [Personalization de Aplicativo/Web de Visitante Conhecido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) |

>[!TAB Serviços financeiros]

Os casos de uso de serviços financeiros serão divulgados em breve. [Exibir casos de uso de Serviços Financeiros atuais](financial-services/financial-services-overview.md).

>[!TAB Assistência médica]

Os casos de uso da área de saúde serão divulgados em breve. [Exibir casos de uso atuais da área de saúde](healthcare/healthcare-overview.md).

>[!TAB Automotivo]

Os casos de uso de automóveis serão divulgados em breve. [Exibir casos de uso de Automotivo atuais](automotive/automotive-overview.md).

>[!TAB Viagens e hospitalidade]

Casos de uso de viagem e hospitalidade serão divulgados em breve. [Exibir casos de uso atuais de Viagem e Hospitalidade](travel-hospitality/travel-hospitality-overview.md).

>[!TAB Telecomunicações]

Os casos de uso de telecomunicações serão divulgados em breve. [Exibir casos de uso de Telecomunicações atuais](telecommunications/telecommunications-overview.md).

>[!TAB Mídia e entretenimento]

Os casos de uso de Mídia e entretenimento serão divulgados em breve. [Exibir casos de uso de Mídia e Entretenimento atuais](media-entertainment/media-entertainment-overview.md).

>[!TAB Seguros]

Os casos de uso de seguro serão divulgados em breve. [Exibir casos de uso de Seguro atuais](insurance/insurance-overview.md).

>[!TAB B2B]

Casos de uso B2B serão divulgados em breve. [Exibir casos de uso B2B atuais](b2b/b2b-overview.md).

>[!ENDTABS]

## Procurar por nível de maturidade

>[!BEGINTABS]

>[!TAB Básico]

Padrões básicos e comprovados usando entrega de canal único. Pontos de partida ideais para organizações que iniciam a jornada [!DNL Experience Platform].

| | Caso de uso | Setor | Impacto no negócio | Padrão |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-abandoned-cart.png" alt="Carrinho abandonado" width="40"> | [Recuperação de email de carrinho abandonado](retail/retail-overview.md#abandoned-cart-email-recovery) | Varejo | 25 a 35% da taxa de recuperação do carrinho | [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-inventory-urgency.png" alt="Urgência do inventário" width="40"> | [Campanhas de urgência baseadas em inventário](retail/retail-overview.md#inventory-based-urgency-campaigns) | Varejo | Aumento de 30 a 40% na conversão | [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-price-drop.png" alt="Queda de preço" width="40"> | [Alertas de Queda de Preço](retail/retail-overview.md#price-drop-alerts) | Varejo | Taxa de conversão de 20 a 30% | [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| | [Notificações de Falta de Estoque](retail/retail-overview.md#out-of-stock-notifications) | Varejo | Taxa de conversão de 40 a 50% | [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |

>[!TAB Emergentes]

Padrões multicanal e em várias etapas que se baseiam em recursos essenciais com personalização orientada por IA e jornadas orquestradas.

| | Caso de uso | Setor | Impacto no negócio | Padrão |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-product-recommendations.png" alt="Recomendações de produto" width="40"> | [Recomendações personalizadas de produtos](retail/retail-overview.md#personalized-product-recommendations) | Varejo | Aumento de 20 a 30% no CTR, aumento de conversão de 15 a 25% | [Recomendação comportamental](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-category-pages.png" alt="Páginas de categoria" width="40"> | [Páginas de categoria personalizadas](retail/retail-overview.md#personalized-category-pages) | Varejo | Aumento de 25 a 35% no engajamento | [Recomendação comportamental](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-welcome-series.png" alt="Série de boas-vindas" width="40"> | [Nova Série de Boas-vindas ao Cliente](retail/retail-overview.md#new-customer-welcome-series) | Varejo | Taxa de engajamento de 40 a 50% | [Jornada Orquestrada Em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-replenishment.png" alt="Reposição" width="40"> | [Lembretes de Reposição](retail/retail-overview.md#replenishment-reminders) | Varejo | Taxa de repetição de compra de 30 a 40% | [Jornada Orquestrada Em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-post-purchase.png" alt="Pós-compra" width="40"> | [Campanhas de acompanhamento pós-compra](retail/retail-overview.md#post-purchase-follow-up-campaigns) | Varejo | 15 a 20% de taxa de revisão, 10 a 15% de compra repetida | [Jornada Orquestrada Em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| | [Personalization de prova social](retail/retail-overview.md#social-proof-personalization) | Varejo | Aumento de 10 a 15% na taxa de conversão | [Personalization de Aplicativo/Web de Visitante Conhecido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) |

>[!TAB Avançado]

Orquestração entre canais com decisões em tempo real e seleção de ofertas orientada por IA para as experiências do cliente mais sofisticadas.

| | Caso de uso | Setor | Impacto no negócio | Padrão |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-cross-sell-upsell.png" alt="Venda cruzada venda adicional" width="40"> | [Recomendações de venda cruzada e venda adicional](retail/retail-overview.md#cross-sell-and-upsell-recommendations) | Varejo | Aumento de US$ 25 a US$ 75 na AOV, aumento de 10 a 15% na receita | [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) |
| | [Ofertas exclusivas de clientes do VIP](retail/retail-overview.md#vip-customer-exclusive-offers) | Varejo | Taxa de engajamento de 50 a 70% dos VIPs | [Jornada entre canais com decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) |

>[!ENDTABS]

## Procurar por padrão de implementação

>[!BEGINTABS]

>[!TAB Orquestração e gerenciamento de campanhas]

### Mensagens acionadas por evento

Responda a eventos comportamentais em tempo real com mensagens oportunas e de canal único.

| | Caso de uso | Setor | Maturidade | Impacto no negócio |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-abandoned-cart.png" alt="Carrinho abandonado" width="40"> | [Recuperação de email de carrinho abandonado](retail/retail-overview.md#abandoned-cart-email-recovery) | Varejo | [!BADGE Básico]{type=Neutral} | 25 a 35% da taxa de recuperação do carrinho |
| <img src="assets/use-case-icons/icon-inventory-urgency.png" alt="Urgência do inventário" width="40"> | [Campanhas de urgência baseadas em inventário](retail/retail-overview.md#inventory-based-urgency-campaigns) | Varejo | [!BADGE Básico]{type=Neutral} | Aumento de 30 a 40% na conversão |
| <img src="assets/use-case-icons/icon-price-drop.png" alt="Queda de preço" width="40"> | [Alertas de Queda de Preço](retail/retail-overview.md#price-drop-alerts) | Varejo | [!BADGE Básico]{type=Neutral} | Taxa de conversão de 20 a 30% |
| | [Notificações de Falta de Estoque](retail/retail-overview.md#out-of-stock-notifications) | Varejo | [!BADGE Básico]{type=Neutral} | Taxa de conversão de 40 a 50% |

### Jornada orquestrada em várias etapas

Orientar os clientes por meio de sequências multitoque que se adaptam com base no engajamento e no comportamento.

| | Caso de uso | Setor | Maturidade | Impacto no negócio |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-welcome-series.png" alt="Série de boas-vindas" width="40"> | [Nova Série de Boas-vindas ao Cliente](retail/retail-overview.md#new-customer-welcome-series) | Varejo | [!BADGE Emergentes]{type=Informative} | Taxa de engajamento de 40 a 50% |
| <img src="assets/use-case-icons/icon-replenishment.png" alt="Reposição" width="40"> | [Lembretes de Reposição](retail/retail-overview.md#replenishment-reminders) | Varejo | [!BADGE Emergentes]{type=Informative} | Taxa de repetição de compra de 30 a 40% |
| <img src="assets/use-case-icons/icon-post-purchase.png" alt="Pós-compra" width="40"> | [Campanhas de acompanhamento pós-compra](retail/retail-overview.md#post-purchase-follow-up-campaigns) | Varejo | [!BADGE Emergentes]{type=Informative} | 15 a 20% de taxa de revisão, 10 a 15% de compra repetida |

### Jornada entre canais com decisão

Orquestrar experiências entre canais com o Offer Decisioning em tempo real em cada ponto de contato.

| | Caso de uso | Setor | Maturidade | Impacto no negócio |
| --- | --- | --- | --- | --- |
| | [Ofertas exclusivas de clientes do VIP](retail/retail-overview.md#vip-customer-exclusive-offers) | Varejo | [!BADGE Avançado]{type=Caution} | Taxa de engajamento de 50 a 70% dos VIPs |

>[!TAB Personalization]

### Recomendação comportamental

Use modelos orientados por IA para exibir conteúdo e produtos personalizados com base em sinais comportamentais.

| | Caso de uso | Setor | Maturidade | Impacto no negócio |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-product-recommendations.png" alt="Recomendações de produto" width="40"> | [Recomendações personalizadas de produtos](retail/retail-overview.md#personalized-product-recommendations) | Varejo | [!BADGE Emergentes]{type=Informative} | Aumento de 20 a 30% no CTR, aumento de conversão de 15 a 25% |
| <img src="assets/use-case-icons/icon-category-pages.png" alt="Páginas de categoria" width="40"> | [Páginas de categoria personalizadas](retail/retail-overview.md#personalized-category-pages) | Varejo | [!BADGE Emergentes]{type=Informative} | Aumento de 25 a 35% no engajamento |

### Offer Decisioning

Use a lógica de decisão centralizada para avaliar e selecionar a melhor oferta para cada cliente e contexto.

| | Caso de uso | Setor | Maturidade | Impacto no negócio |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-cross-sell-upsell.png" alt="Venda cruzada venda adicional" width="40"> | [Recomendações de venda cruzada e venda adicional](retail/retail-overview.md#cross-sell-and-upsell-recommendations) | Varejo | [!BADGE Avançado]{type=Caution} | Aumento de US$ 25 a US$ 75 na AOV, aumento de 10 a 15% na receita |

### Personalization de aplicativo/Web de visitante conhecido

Personalize o conteúdo da Web e do aplicativo para visitantes identificados com base no perfil, nas preferências e no contexto de navegação.

| | Caso de uso | Setor | Maturidade | Impacto no negócio |
| --- | --- | --- | --- | --- |
| | [Personalization de prova social](retail/retail-overview.md#social-proof-personalization) | Varejo | [!BADGE Emergentes]{type=Informative} | Aumento de 10 a 15% na taxa de conversão |

>[!ENDTABS]
