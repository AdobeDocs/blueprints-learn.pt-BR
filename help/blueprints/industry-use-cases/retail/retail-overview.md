---
title: Casos de uso de varejo
description: Descubra como as organizações de varejo usam o Adobe Experience Platform para personalizar experiências de compra, recuperar carrinhos abandonados e impulsionar a fidelidade do cliente.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '2590'
ht-degree: 0%

---


# Casos de uso de varejo

As organizações de varejo usam o Adobe Experience Platform para unificar os dados de clientes de lojas online, locais físicos e programas de fidelidade em uma única visualização de cada comprador. Essa base permite experiências de compra personalizadas, alcance imediato que recupera receita perdida e estratégias de fidelidade que mantêm os clientes voltando.

## Recomendações de produto personalizadas

Mostre recomendações de produto personalizadas na página inicial, páginas de categoria e páginas de detalhes do produto com base no histórico de navegação, histórico de compras e comportamento de cliente semelhante. Quando os compradores veem produtos adaptados aos seus interesses, eles gastam mais tempo explorando e têm muito mais probabilidade de comprar.

### Impacto no negócio

Os varejistas normalmente observam um aumento de 20 a 30% nas taxas de click-through e uma melhoria de 15 a 25% nas taxas de conversão ao veicular recomendações personalizadas em vez de listas de produtos estáticas.

### Como implementar o

Use o padrão [Recomendação Comportamental](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Essa abordagem usa modelos de recomendação orientados por IA que aprendem continuamente com as interações do cliente para destacar os produtos mais relevantes para cada indivíduo.

### Considerações técnicas

- Os dados do catálogo de produtos devem ser assimilados e mantidos atualizados, incluindo atributos, imagens, preços e disponibilidade do produto, para garantir que as recomendações reflitam o que os clientes podem realmente comprar.
- Sinais comportamentais, como exibições de produtos, eventos de adição ao carrinho e compras precisam fluir em tempo quase real para manter as recomendações atualizadas em uma única sessão de navegação.
- Os modelos de recomendação exigem uma estratégia de partida a frio para novos visitantes sem histórico de navegação, normalmente recorrendo aos produtos em tendência ou mais vendidos.
- O desempenho do carregamento da página deve ser monitorado com cuidado, pois as chamadas de personalização não devem adicionar latência visível à experiência de compra.


## Recuperação de e-mail de carrinho abandonado

Envie lembretes de email personalizados automaticamente para os clientes que abandonaram o carrinho de compras, incluindo os itens exatos deixados para trás e ofertas relevantes para incentivar a conclusão. O abandono do carrinho é uma das maiores fontes de perda de receita no varejo, e o acompanhamento em tempo hábil pode recuperar uma parte significativa dessas vendas.

### Impacto no negócio

Os programas eficazes de recuperação do carrinho oferecem uma taxa de recuperação de 25 a 35% do carrinho e podem gerar uma receita adicional de US$ 100.000 a US$ 500.000 mensais, dependendo do volume de armazenamento.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Essa abordagem responde a um evento de abandono de carrinho em tempo real, enviando um lembrete em tempo hábil enquanto a intenção de compra ainda é alta.

### Considerações técnicas

- A detecção de abandono do carrinho exige a definição de um limite de inatividade (geralmente de 30 a 60 minutos) antes de acionar o primeiro lembrete, evitando mensagens para clientes que ainda fazem compras ativamente.
- O conteúdo do email deve extrair dinamicamente as imagens, os preços e a disponibilidade atuais do produto do catálogo no momento do envio, já que os itens podem esgotar ou alterar o preço entre o abandono e o delivery.
- As regras de limite de frequência devem impedir que os clientes recebam vários emails de carrinho de abandono em um curto período, especialmente se abandonarem carrinhos com frequência.
- As listas de consentimento e supressão devem ser verificadas antes do envio, e os clientes que concluíram sua compra por meio de outro canal devem ser excluídos em tempo real.


## Campanhas de urgência baseadas em inventário

Acione alertas e campanhas em tempo real quando o inventário de produtos estiver baixo, criando urgência e incentivando a compra imediata. Os compradores que veem que apenas alguns itens permanecem são motivados a agir rapidamente, em vez de atrasar sua decisão.

### Impacto no negócio

As campanhas urgentes de baixo inventário geralmente geram um aumento de 30 a 40% na conversão para produtos em destaque, além de ajudar a reduzir o excesso de estoque acelerando a venda de itens de movimentação lenta.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Essa abordagem responde aos eventos de limite do inventário, ativando automaticamente as mensagens de urgência quando os níveis de estoque caem abaixo dos limites definidos.

### Considerações técnicas

- Os feeds de inventário devem se integrar à plataforma de dados do cliente em tempo quase real, para que as mensagens de urgência reflitam os níveis de estoque reais, em vez dos dados obsoletos.
- Os níveis de limite devem ser configurados por categoria de produto, já que um limite de &quot;estoque baixo&quot; para uma mercadoria de alto volume difere significativamente de um para um item de luxo.
- As mensagens devem ser verdadeiras e cumprir as regras de proteção do consumidor; a exibição de uma falsa escassez pode prejudicar a confiança da marca e violar os padrões de publicidade em certos mercados.
- Os canais de mensagens no local e de email devem ser coordenados para que um cliente que já tenha comprado não continue recebendo notificações de urgência para o mesmo produto.


## Recomendações de venda cruzada e venda adicional

Exiba produtos relevantes de venda cruzada e venda adicional na finalização da compra, por email e em páginas de produtos com base em padrões de compra e relacionamentos de produtos. Sugerir alternativas complementares ou premium no momento certo aumenta o tamanho da cesta sem exigir que os clientes pesquisem por itens relacionados.

### Impacto no negócio

Estratégias bem executadas de venda cruzada e venda adicional aumentam o valor médio de pedido em US$ 25 a US$ 75 e aumentam a receita por transação em 10 a 15%.

### Como implementar o

Use o padrão [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). Essa abordagem usa uma lógica de decisão centralizada para avaliar todas as ofertas disponíveis e selecionar a melhor opção de venda cruzada ou venda adicional para cada cliente e contexto.

### Considerações técnicas

- Os dados de relacionamento do produto, incluindo associações &quot;compradas com frequência&quot; e caminhos de atualização, devem ser mantidos e atualizados regularmente para refletir os padrões de compra atuais.
- A lógica de classificação da oferta deve levar em conta os níveis de margem, relevância e inventário para que as opções mais lucrativas e disponíveis apareçam primeiro.
- As recomendações de venda cruzada na finalização da compra devem ser carregadas rapidamente e não devem interromper o fluxo de compra. Sugestões lentas ou intrusivas podem realmente reduzir a conversão.
- As regras de decisão do [!DNL Journey Optimizer] devem incluir ofertas substitutas para que todos os clientes qualificados recebam uma recomendação, mesmo quando a opção mais bem classificada estiver indisponível.


## Nova série de boas-vindas ao cliente

Automatize uma série de boas-vindas com vários emails para novos clientes com recomendações de produto personalizadas, narrativa de marca e ofertas especiais. As primeiras interações após a adesão de um cliente moldam seu relacionamento de longo prazo com a marca, tornando essa série um dos programas de maior impacto que uma retailer pode executar.

### Impacto no negócio

Uma série de boas-vindas bem projetada gera uma taxa de envolvimento de 40 a 50% entre novos clientes e melhora significativamente o valor vitalício ao criar a afinidade da marca antecipadamente.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Essa jornada de nutrição multitoque orienta novos clientes por meio de uma sequência de apresentação da marca, descoberta de produtos e mensagens de incentivo, adaptando-se com base em seu envolvimento.

### Considerações técnicas

- O acionador de entrada de jornada deve capturar com confiança novos eventos de criação de clientes de todas as fontes de registro, incluindo Web, aplicativo móvel, ponto de venda na loja e mercados de terceiros.
- As etapas de espera entre os emails devem ser configuradas com base nos dados de engajamento; os clientes que abrem e clicam podem receber a próxima mensagem antes, enquanto clientes menos engajados se beneficiam de mais espaçamento.
- As recomendações de produto nos emails de boas-vindas devem refletir o que o cliente navegou ou comprou durante sua primeira visita, não os best-sellers genéricos.
- Os clientes que fazem uma compra durante a série de boas-vindas devem se ramificar em um fluxo pós-compra em vez de continuar a receber mensagens focadas em aquisição.


## Alertas de queda de preço

Notifique os clientes por email ou notificação por push quando os produtos em sua lista de desejos ou itens visualizados anteriormente tiverem um preço baixo. Os compradores que demonstraram interesse, mas não compraram, são altamente responsivos às reduções de preços, tornando esta uma das maneiras mais eficientes de converter a consideração em vendas.

### Impacto no negócio

Os alertas de queda de preço geram uma taxa de conversão de 20 a 30% entre os recipients e aumentam mensuravelmente a satisfação do cliente, ajudando os compradores a sentirem que estão obtendo o melhor valor.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Essa abordagem responde aos eventos de alteração de preço do produto, comparando-os com os sinais de interesse do cliente para fornecer notificações oportunas.

### Considerações técnicas

- A detecção de alteração de preço exige a comparação dos preços atuais com os valores anteriores no feed do catálogo de produtos e o acionamento dos alertas somente para reduções significativas, em vez de flutuações menores.
- Os sinais de interesse do cliente (adições à lista de desejos, visualizações de página de produtos, tempo gasto nas páginas de produtos) devem ser armazenados e correspondidos com eficiência em relação a milhares de alterações diárias de preço, possivelmente.
- As notificações devem incluir o preço original, o novo preço e o valor da economia para comunicar claramente o valor; mensagens vagas de &quot;preço reduzido&quot; têm baixo desempenho em chamadas de economia específicas.
- [!DNL Real-Time Customer Data Platform] segmentos para compradores sensíveis ao preço podem ser usados para priorizar a entrega de alertas e ajustar o tom de mensagem.


## Lembretes de Reposição

Envie lembretes automatizados aos clientes sobre produtos que eles compram regularmente, como itens de assinatura e consumíveis, para incentivar compras repetidas antes que elas acabem. Os lembretes proativos reduzem a chance de os clientes alternarem para um concorrente simplesmente porque esqueceram de fazer o novo pedido.

### Impacto no negócio

Os programas de lembrete de reposição oferecem uma taxa de repetição de compra de 30 a 40% e melhoram significativamente a retenção do cliente, tornando fácil para os compradores reabastecer os produtos dos quais dependem.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Essa jornada recorrente agendada usa previsões de frequência de compra para enviar lembretes no momento ideal antes que um cliente provavelmente precise de um reabastecimento.

### Considerações técnicas

- O cálculo da frequência de compra deve levar em conta as taxas de consumo variáveis entre as categorias de produtos; um lembrete para o café deve chegar em uma cadência diferente de um para os suprimentos de limpeza.
- A jornada deve ajustar dinamicamente seu tempo quando um cliente fizer um novo pedido antes ou depois do previsto, recalibrando o próximo lembrete com base nos dados de compra atualizados.
- Os lembretes devem incluir um link de reordenação direta ou uma opção de recompra com um clique para minimizar o atrito e maximizar a conversão da notificação.
- Os clientes que já reordenaram por meio de outro canal (na loja, serviço de assinatura) devem ser suprimidos para evitar o envio de lembretes irrelevantes.


## Páginas de categoria personalizadas

Personalize dinamicamente as páginas de categoria para mostrar os produtos mais relevantes primeiro com base nas preferências, compras anteriores e comportamento de navegação de cada cliente. Quando os compradores veem produtos alinhados a seus gostos no topo da página, eles descobrem o que desejam mais rápido e fazem conversões a taxas mais altas.

### Impacto no negócio

As páginas de categoria personalizadas geram um aumento de 25 a 35% no engajamento da página de categoria e melhoram significativamente a descoberta de produtos, especialmente para varejistas com catálogos grandes.

### Como implementar o

Use o padrão [Recomendação Comportamental](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Essa abordagem usa estratégias de seleção e modelos de classificação para reordenar produtos nas páginas de categoria com base no perfil e no comportamento em tempo real de cada visitante.

### Considerações técnicas

- A classificação do produto deve ser executada com rapidez suficiente para evitar atrasos percebidos no carregamento da página. Geralmente, a personalização no lado do servidor ou a decisão baseada em borda são necessárias para páginas de categoria com centenas de produtos.
- A lógica de personalização deve combinar preferências individuais com regras de merchandising, garantindo que os produtos promovidos, os recém-chegados e os itens sazonais ainda recebam visibilidade adequada.
- A infraestrutura de teste A/B deve estar em vigor para medir o impacto na receita da classificação personalizada em relação às regras de merchandising padrão de forma contínua.
- A implementação do Web SDK [!DNL Experience Platform] deve capturar as interações de página da categoria (profundidade de rolagem, cliques no produto, uso do filtro) para refinar continuamente os modelos de classificação.


## Campanhas de acompanhamento pós-compra

Envie emails de pós-compra com dicas de atendimento ao produto, sugestões de produto relacionadas, solicitações de revisão e informações do programa de fidelidade. O período imediatamente após uma compra é quando os clientes estão mais envolvidos com a marca, tornando-a uma janela ideal para aprofundar o relacionamento e incentivar atividades futuras.

### Impacto no negócio

Campanhas pós-compra eficazes aumentam as taxas de envio de análise em 15-20% e geram uma taxa de compra repetida de 10-15%, transformando compradores únicos em clientes fiéis.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Esse fluxo pós-compra de várias etapas usa lógica de ramificação para personalizar as mensagens de acompanhamento com base no tipo de produto, no segmento do cliente e no envolvimento com emails anteriores na série.

### Considerações técnicas

- A jornada deve levar em conta o status de atendimento do pedido; dicas de atendimento e solicitações de revisão só devem ser enviadas após a entrega do produto e não imediatamente após a compra.
- O conteúdo específico do produto (instruções de cuidados, guias de uso, sugestões de acessórios) requer um sistema de mapeamento de conteúdo que associe cada categoria de produto ao material de acompanhamento relevante.
- O tempo de solicitação de revisão deve ser otimizado com base na categoria do produto; o equipamento eletrônico pode precisar de um período de uso mais longo antes de uma revisão significativa, enquanto o vestuário pode ser revisado logo após a entrega.
- Os clientes que iniciam um retorno ou troca devem ser automaticamente removidos do fluxo padrão pós-compra e redirecionados para um caminho de recuperação de serviço.


## Ofertas exclusivas de clientes do VIP

Identifique clientes de alto valor e forneça ofertas exclusivas, acesso antecipado a vendas e experiências de compras personalizadas que recompensem sua fidelidade. Manter clientes de alto nível é muito mais econômico do que adquirir novos, e o tratamento exclusivo fortalece a conexão emocional que os mantém gastando.

### Impacto no negócio

Os programas da VIP normalmente geram uma taxa de envolvimento de 50 a 70% de clientes de nível superior e melhoram mensuravelmente o valor vitalício do cliente, reduzindo o abandono entre os segmentos mais lucrativos.

### Como implementar o

Use a [Jornada entre canais com o padrão de decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). Essa abordagem combina a orquestração de jornadas com a decisão em tempo real para a seleção de ofertas, garantindo que cada cliente do VIP receba a oferta exclusiva mais relevante em todos os canais.

### Considerações técnicas

- Os critérios de segmentação do VIP devem ser claramente definidos usando métricas de recenticidade, frequência e valor monetário, e os segmentos devem ser atualizados com frequência suficiente para capturar clientes que se qualificaram ou desqualificaram recentemente.
- As ofertas exclusivas devem ser aplicadas no ponto de resgate (Web, aplicativo, loja) para impedir que clientes não-VIP as acessem, o que requer integração com sistemas de promoção e preços.
- As preferências de canal variam significativamente entre clientes de alto valor; alguns preferem email, outros respondem a notificações do aplicativo ou correspondência direta, portanto, a jornada deve adaptar os canais de entrega com base no engajamento anterior.
- A decisão do [!DNL Journey Optimizer] deve coordenar entre canais para impedir que um cliente da VIP receba a mesma oferta por email, push e SMS simultaneamente.


## Notificações de Falta de Estoque

Permitir que os clientes se inscrevam para receber notificações quando produtos indisponíveis estiverem disponíveis, em seguida, notificá-los automaticamente por email ou mensagem de texto. A captura da demanda por produtos indisponíveis evita a perda de vendas e fornece aos clientes um motivo para retornar à loja em vez de comprar de um concorrente.

### Impacto no negócio

As notificações de retorno ao estoque atingem uma taxa de conversão de 40 a 50% entre os assinantes e reduzem significativamente as vendas perdidas para produtos de alta demanda que passam por estoques temporários.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Essa abordagem aciona notificações sobre eventos de retorno ao estoque, comparando atualizações de inventário com inscrições em notificações de clientes para fornecer alertas oportunos.

### Considerações técnicas

- O monitoramento de inventário deve detectar eventos de reabastecimento rapidamente; atrasos de algumas horas podem resultar na venda do produto novamente, antes que os clientes notificados tenham a chance de comprá-lo.
- Quando um produto popular é reabastecido em quantidade limitada, as notificações devem ser escalonadas ou priorizadas por data de inscrição para evitar o envio de alertas a mais clientes do que o estoque disponível pode atender.
- O mecanismo de inscrição para notificação deve capturar a preferência de canal (email ou mensagem de texto) e atender aos requisitos de aceitação para cada canal, especialmente para SMS.
- Os atributos de perfil do [!DNL Real-Time Customer Data Platform] devem rastrear quais produtos cada cliente está assistindo para evitar notificações duplicadas se o mesmo produto for reabastecido várias vezes.


## Personalization de prova social

Exiba uma prova social personalizada, incluindo revisões, classificações e sugestões de &quot;clientes que compraram isso também compraram&quot;, com base no perfil e nas preferências de cada cliente. Personalizar a prova social para refletir as experiências de clientes semelhantes cria confiança de maneira mais eficaz do que as classificações genéricas sozinhas.

### Impacto no negócio

A prova social personalizada aumenta as taxas de conversão em 10-15% e melhora a confiança do comprador, especialmente para compradores pela primeira vez e produtos com preços mais altos, onde a hesitação de compra é maior.

### Como implementar o

Use o padrão [Personalization de Aplicativo/Web de Visitante Conhecido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md). Essa abordagem personaliza o conteúdo da Web para visitantes identificados, selecionando as revisões mais relevantes e os elementos de prova social com base no perfil do cliente, nas preferências e no contexto de navegação.

### Considerações técnicas

- Os dados de análise e classificação devem ser estruturados e marcados por atributos do cliente (como contexto de compra, segmento do cliente e caso de uso do produto) para permitir filtragem e personalização significativas.
- Os elementos de prova social devem ser carregados de forma assíncrona para evitar o bloqueio da renderização da página principal do produto, já que os dados de revisão podem vir de uma plataforma de revisão de terceiros com tempos de resposta variáveis.
- As regulamentações de privacidade exigem que todos os dados do cliente usados para corresponder revisões aos visitantes sejam tratados de acordo com as preferências de consentimento; exibir o conteúdo de &quot;clientes como você&quot; implica em definição de perfil que pode exigir divulgação.
- A associação de público-alvo [!DNL Experience Platform] pode ser usada para selecionar quais análises destacar, mostrando análises de entusiastas de ambientes externos de outros compradores em vez de análises genéricas mais bem avaliadas.
