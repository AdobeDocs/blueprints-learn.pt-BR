---
title: Setor de varejo – Ativação com aplicativos da Experience Cloud
description: Oferecimento de experiências do cliente em tempo real em canais de mídia digital, email, push e Web.
solution: Real-time Customer Data Platform, Customer Journey Analytics, Journey Orchestration, Campaign, Analytics, Target
kt: 9474
exl-id: a675bc81-e76c-491a-8718-359867d63351
source-git-commit: f03981dd3fe6ed9e60d2e60ca4eb91e129052a73
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 40%

---

# Desafio das empresas do setor de varejo

Essa empresa baseada em experiências integrada buscou personalizar toda a jornada do cliente para aumentar a fidelidade e a venda adicional para clientes existentes e para melhorar os gastos com marketing em suas campanhas. A estratégia para atingir o objetivo é estender a capacidade digital para incluir dados offline de transações e dos clientes para impulsionar o crescimento.

## Abordagem da Adobe

* Gere um perfil de cliente unificado que inclua todos os dados online/offline relevantes que podem ser ativados em tempo real
* Orquestre as interações com o cliente na Web, em mídias e em canais de push para impulsionar o comportamento de compra pela primeira ou segunda vez.

## Valor comercial fornecido

| Metas | Táticas | Valor desbloqueado |
|---|---|---|
| **Orquestrar jornadas do cliente em tempo real **<br></br>** Impulsionar compras repetidas de novos clientes **<br></br>** Melhorar a eficiência do marketing e reduzir os custos de mídia**</ul> | <ul><li>Dados robustos e estratégia de identidade para alimentar um perfil abrangente em tempo real.</li><li>Transmissão de dados transacionais e do cliente em tempo real, incluindo uma carga histórica de 90 dias</li><li>Segmentação de transmissão para redes publicitárias e Adobe Target para potencializar os gastos com mídia e os esforços de personalização.</li><li>Jornadas do cliente em tempo real por meio do Adobe Campaign que incluem uma estratégia para medir o desempenho</li></ul> | <ul><li><strong>Real-time Customer Data Platform:</strong> Oferecimento de experiências do cliente em tempo real em mídias, emails, push e Web</li><li><strong>Fontes de dados:</strong> Dados de transmissão que abrangem as lojas de perfil deste varejista, o sistema de pedidos, o catálogo de produtos e as lojas de varejo.</li><li><strong>Ativação de mídia em tempo real:</strong>Segmentos de transmissão para redes de publicidade para atribuição e supressão de anúncios</li><li><strong>Personalização da Web em tempo real:</strong>Segmentos de transmissão ativados para o Adobe Target para ativar na experiência da Web do varejista.</li><li><strong>Journey Orchestration em escala:</strong>Mensagens acionadas em tempo real enriquecidas com dados disponíveis do cliente e ativadas em tempo real para canais de email e push</li></ul> |


## Usecases

| Categoria | Meta | Caso de uso | Descrição |
|:----|:----|:----|:----|
| Jornadas do cliente | Aquisição | Série de boas-vindas | Dê as boas-vindas a novos assinantes com introdução aos negócios, produtos e serviços |
|  |  | 1º programa de compra |  |
|  | Melhore as vendas | Carrinho/Navegação abandonado | Recuperar possíveis compradores e aumentar as vendas |
|  |  | Revisão do produto/venda cruzada | Venda cruzada de mais itens com Resenhas de produtos. |
|  |  | Promoções do produto |  |
|  |  | Tempo para reordenar | Lembrete recorrente de produtos/serviços cíclicos |
|  | Fidelidade à marca | Retornar | Recuperar clientes que ficaram inativos. |
|  |  | Lembretes de Aniversário | Promova um relacionamento mais pessoal com seus clientes fazendo parte da celebração de aniversário deles! |
| Merchandising | Gerenciar inventário | De volta ao estoque | Melhorar o inventário, mostrando aos clientes que os produtos que eles queriam estão de volta ao estoque |
|  |  | Próxima Melhor Categoria | Identificar as melhores categorias/vendas para usuários |
|  |  | Melhores vendedores |  |
|  |  | Lembretes de queda de preço | Mostrar aos usuários que os itens de que eles gostaram têm um preço reduzido |
|  |  | Produtos similares |  |
| Personalizar | Aumentar conversão | Cupons/Ofertas | Mostrar as melhores ofertas/cupons aos clientes |
|  |  | Pesquisa personalizada de produtos | Melhorar a experiência de pesquisa |
|  |  | Recommendations do produto | Melhorar a experiência de navegação do produto |
|  |  | Experiência Omnicanal | Alcance clientes em todos os canais |
| Medir | Entender as Jornadas do cliente | Campanha entre canais | Medir campanhas entre canais |
|  |  | Desempenho do segmento | Entender o desempenho e a contribuição do segmento |
|  |  | Relatórios de fallout | Visualizar conversões em cada estágio |
|  |  | Análise de coorte | Medir engajamento entre grupos de segmentos |
|  |  | Relatórios de clique para brick | Veja como as conversões de clientes levam à experiência na loja |
|  |  | Atribuição | Visualizar qual ponto de contato/experiência tem a maior influência na conversão de compra |
|  |  | Insights preditivos | Saiba mais sobre as tendências dos clientes |

## Arquitetura

<img src="../vertical-blueprints/assets/retail-architecture.png" alt="Arquitetura de referência de varejo" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />


## Blueprints relacionados


| Caso de uso/integração  | Link |
|:----|:----|
| CJA + AEP | [Visão geral dos blueprints do Customer Journey Analytics](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journey-analytics/overview.html?lang=pt-BR) |
|  | [Customer Journey Analytics - Casos de uso](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/cja-usecases.html?lang=pt-BR) |
| AJO + AEP | [Adobe Journey Optimizer - Casos de uso](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/journey-optimizer.html?lang=en) |
|  | [Gestão de decisões](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-overview.html?lang=pt-BR) |
| RTCDP + AEP | [Ativação de público-alvo online/offline](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=pt-BR) |
|  | [Experience Platform + Ativação de aplicativo](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=pt-BR) |
| MARKETO + AEP | [Ativação e marketing B2B](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/b2b-activation/overview.html?lang=en) |  |
| Target + AEP | [Caso de uso do Adobe Target — Personalização comportamental da Web/móvel](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/web-personalization/behavioral.html?lang=pt-BR) | [Personalização da Web/Mobile com dados de clientes conhecidos](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/web-personalization/known-personalization.html?lang=en) |  |
