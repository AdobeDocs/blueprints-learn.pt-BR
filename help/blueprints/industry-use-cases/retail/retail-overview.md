---
title: Casos de uso de varejo
description: Descubra como as organizações de varejo usam o Adobe Experience Platform para personalizar experiências de compra, recuperar carrinhos abandonados e impulsionar a fidelidade do cliente.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: 89a5b6b5-bb71-4154-bb3b-f6dbbbef13eb
source-git-commit: 3542d76106fada9019b70a8cc9fd4c74872d4995
workflow-type: tm+mt
source-wordcount: '7216'
ht-degree: 0%

---

# Casos de uso de varejo

As organizações de varejo usam o Adobe Experience Platform para unificar os dados de clientes de lojas online, locais físicos e programas de fidelidade em uma única visualização de cada comprador. Essa base permite experiências de compra personalizadas, alcance imediato que recupera receita perdida e estratégias de fidelidade que mantêm os clientes voltando.

## Recomendações de produto personalizadas

Mostre recomendações de produto personalizadas na página inicial, páginas de categoria e páginas de detalhes do produto com base no histórico de navegação, histórico de compras e comportamento de cliente semelhante. Quando os compradores veem produtos adaptados aos seus interesses, eles gastam mais tempo explorando e têm muito mais probabilidade de comprar.

### Impacto no negócio

Os varejistas observam melhores taxas de click-through e taxas de conversão ao veicular recomendações personalizadas em vez de listas de produtos estáticas.

### Como implementar o

Use o padrão [Recomendação Comportamental](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Essa abordagem usa modelos de recomendação orientados por IA que aprendem continuamente com as interações do cliente para destacar os produtos mais relevantes para cada indivíduo. Esse é o padrão correto quando o conjunto de itens é grande e muda continuamente, e a seleção é orientada por afinidade comportamental, em vez de um conjunto limitado de ofertas regido por regras de elegibilidade.

### Considerações técnicas

- Os dados do catálogo de produtos devem ser assimilados e mantidos atualizados, incluindo atributos, imagens, preços e disponibilidade do produto, para garantir que as recomendações reflitam o que os clientes podem realmente comprar.
- Sinais comportamentais, como exibições de produtos, eventos de adição ao carrinho e compras precisam fluir em tempo quase real para manter as recomendações atualizadas em uma única sessão de navegação.
- Os modelos de recomendação exigem uma estratégia de partida a frio para novos visitantes sem histórico de navegação, normalmente recorrendo aos produtos em tendência ou mais vendidos.
- O desempenho do carregamento da página deve ser monitorado com cuidado, pois as chamadas de personalização não devem adicionar latência visível à experiência de compra.


## Recuperação de e-mail de carrinho abandonado

Envie lembretes de email personalizados automaticamente para os clientes que abandonaram o carrinho de compras, incluindo os itens exatos deixados para trás e ofertas relevantes para incentivar a conclusão. O abandono do carrinho é uma das maiores fontes de perda de receita no varejo, e o acompanhamento em tempo hábil pode recuperar uma parte significativa dessas vendas.

### Impacto no negócio

Os programas eficazes de recuperação do carrinho melhoram as taxas de recuperação do carrinho e podem gerar receita incremental significativa, dependendo do volume de armazenamento.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Essa abordagem responde a um evento de abandono de carrinho em tempo real, enviando um lembrete em tempo hábil enquanto a intenção de compra ainda é alta. Esse é o padrão correto quando uma ação distinta do cliente é o acionador e a resposta necessária é uma mensagem única que diferencia tempo, em vez de uma sequência de várias etapas ou seleção de oferta dinâmica.

### Considerações técnicas

- A detecção de abandono do carrinho exige a definição de um limite de inatividade (geralmente de 30 a 60 minutos) antes de acionar o primeiro lembrete, evitando mensagens para clientes que ainda fazem compras ativamente.
- O conteúdo do email deve extrair dinamicamente as imagens, os preços e a disponibilidade atuais do produto do catálogo no momento do envio, já que os itens podem esgotar ou alterar o preço entre o abandono e o delivery.
- As regras de limite de frequência devem impedir que os clientes recebam vários emails de carrinho de abandono em um curto período, especialmente se abandonarem carrinhos com frequência.
- As listas de consentimento e supressão devem ser verificadas antes do envio, e os clientes que concluíram sua compra por meio de outro canal devem ser excluídos em tempo real.


## Campanhas de urgência baseadas em inventário

Acione alertas e campanhas em tempo real quando o inventário de produtos estiver baixo, criando urgência e incentivando a compra imediata. Os compradores que veem que apenas alguns itens permanecem são motivados a agir rapidamente, em vez de atrasar sua decisão.

### Impacto no negócio

Campanhas urgentes de baixo inventário geram conversões aprimoradas para produtos em destaque, além de ajudar a reduzir o excesso de estoque acelerando a venda de itens de movimentação lenta.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Essa abordagem responde aos eventos de limite do inventário, ativando automaticamente as mensagens de urgência quando os níveis de estoque caem abaixo dos limites definidos. Esse é o padrão correto quando o acionador é um evento do sistema e não um comportamento do cliente, e a comunicação necessária é imediata e reativa, em vez de uma sequência de criação contínua.

### Considerações técnicas

- Os feeds de inventário devem se integrar à plataforma de dados do cliente em tempo quase real, para que as mensagens de urgência reflitam os níveis de estoque reais, em vez dos dados obsoletos.
- Os níveis de limite devem ser configurados por categoria de produto, já que um limite de &quot;estoque baixo&quot; para uma mercadoria de alto volume difere significativamente de um para um item de luxo.
- As mensagens devem ser verdadeiras e cumprir as regras de proteção do consumidor; a exibição de uma falsa escassez pode prejudicar a confiança da marca e violar os padrões de publicidade em certos mercados.
- Os canais de mensagens no local e de email devem ser coordenados para que um cliente que já tenha comprado não continue recebendo notificações de urgência para o mesmo produto.


## Recomendações de venda cruzada e venda adicional

Exiba produtos relevantes de venda cruzada e venda adicional na finalização da compra, por email e em páginas de produtos com base em padrões de compra e relacionamentos de produtos. Sugerir alternativas complementares ou premium no momento certo aumenta o tamanho da cesta sem exigir que os clientes pesquisem por itens relacionados.

### Impacto no negócio

Estratégias bem executadas de venda cruzada e venda adicional aumentam o valor médio de pedido e elevam a receita por transação, contribuindo para uma economia mais forte na cesta geral.

### Como implementar o

Use o padrão [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). Essa abordagem usa uma lógica de decisão centralizada para avaliar todas as ofertas disponíveis e selecionar a melhor opção de venda cruzada ou venda adicional para cada cliente e contexto. Esse é o padrão correto quando a seleção da oferta deve levar em conta as regras de margem, disponibilidade de estoque e relacionamento do produto — restrições de negócios que exigem lógica de decisão controlada em vez de classificação de afinidade comportamental sozinha.

### Considerações técnicas

- Os dados de relacionamento do produto, incluindo associações &quot;compradas com frequência&quot; e caminhos de atualização, devem ser mantidos e atualizados regularmente para refletir os padrões de compra atuais.
- A lógica de classificação da oferta deve levar em conta os níveis de margem, relevância e inventário para que as opções mais lucrativas e disponíveis apareçam primeiro.
- As recomendações de venda cruzada na finalização da compra devem ser carregadas rapidamente e não devem interromper o fluxo de compra. Sugestões lentas ou intrusivas podem realmente reduzir a conversão.
- As regras de decisão do [!DNL Journey Optimizer] devem incluir ofertas substitutas para que todos os clientes qualificados recebam uma recomendação, mesmo quando a opção mais bem classificada estiver indisponível.


## Nova série de boas-vindas ao cliente

Automatize uma série de boas-vindas com vários emails para novos clientes com recomendações de produto personalizadas, narrativa de marca e ofertas especiais. As primeiras interações após a adesão de um cliente moldam seu relacionamento de longo prazo com a marca, tornando essa série um dos programas de maior impacto que uma retailer pode executar.

### Impacto no negócio

Uma série de boas-vindas bem projetada impulsiona um forte engajamento entre novos clientes e melhora significativamente o valor vitalício ao criar a afinidade da marca desde o início.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Essa jornada de nutrição multitoque orienta novos clientes por meio de uma sequência de apresentação da marca, descoberta de produtos e mensagens de incentivo, adaptando-se com base em seu envolvimento. Esse é o padrão correto quando o caso de uso requer um fluxo sequenciado de várias mensagens ao longo de dias com ramificação condicional baseada em eventos de engajamento — uma única mensagem acionada não pode acomodar a lógica de dependência entre as etapas.

### Considerações técnicas

- O acionador de entrada de jornada deve capturar com confiança novos eventos de criação de clientes de todas as fontes de registro, incluindo Web, aplicativo móvel, ponto de venda na loja e mercados de terceiros.
- As etapas de espera entre os emails devem ser configuradas com base nos dados de engajamento; os clientes que abrem e clicam podem receber a próxima mensagem antes, enquanto clientes menos engajados se beneficiam de mais espaçamento.
- As recomendações de produto nos emails de boas-vindas devem refletir o que o cliente navegou ou comprou durante sua primeira visita, não os best-sellers genéricos.
- Os clientes que fazem uma compra durante a série de boas-vindas devem se ramificar em um fluxo pós-compra em vez de continuar a receber mensagens focadas em aquisição.


## Alertas de queda de preço

Notifique os clientes por email ou notificação por push quando os produtos em sua lista de desejos ou itens visualizados anteriormente tiverem um preço baixo. Os compradores que demonstraram interesse, mas não compraram, são altamente responsivos às reduções de preços, tornando esta uma das maneiras mais eficientes de converter a consideração em vendas.

### Impacto no negócio

Os alertas de queda de preço geram melhores taxas de conversão entre os recipients e aumentam mensuravelmente a satisfação do cliente, ajudando os compradores a sentirem que estão obtendo o melhor valor.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Essa abordagem responde aos eventos de alteração de preço do produto, comparando-os com os sinais de interesse do cliente para fornecer notificações oportunas. Esse é o padrão correto quando o acionador é um evento do sistema de catálogo e a janela de entrega é sensível ao tempo — uma jornada sustentada seria muito lenta e nenhum acompanhamento de várias etapas seria necessário além da notificação inicial.

### Considerações técnicas

- A detecção de alteração de preço exige a comparação dos preços atuais com os valores anteriores no feed do catálogo de produtos e o acionamento dos alertas somente para reduções significativas, em vez de flutuações menores.
- Os sinais de interesse do cliente (adições à lista de desejos, visualizações de página de produtos, tempo gasto nas páginas de produtos) devem ser armazenados e correspondidos com eficiência em relação a milhares de alterações diárias de preço, possivelmente.
- As notificações devem incluir o preço original, o novo preço e o valor da economia para comunicar claramente o valor; mensagens vagas de &quot;preço reduzido&quot; têm baixo desempenho em chamadas de economia específicas.
- [!DNL Real-Time Customer Data Platform] segmentos para compradores sensíveis ao preço podem ser usados para priorizar a entrega de alertas e ajustar o tom de mensagem.


## Lembretes de Reposição

Envie lembretes automatizados aos clientes sobre produtos que eles compram regularmente, como itens de assinatura e consumíveis, para incentivar compras repetidas antes que elas acabem. Os lembretes proativos reduzem a chance de os clientes alternarem para um concorrente simplesmente porque esqueceram de fazer o novo pedido.

### Impacto no negócio

Programas de lembrete de reposição impulsionam taxas de compra repetidas melhoradas e melhoram a retenção do cliente, tornando fácil para os compradores reabastecer os produtos de que dependem.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Essa jornada recorrente agendada usa previsões de frequência de compra para enviar lembretes no momento ideal antes que um cliente provavelmente precise de um reabastecimento. Esse é o padrão correto quando não há evento de acionamento discreto e o tempo deve ser calculado a partir de modelos de frequência de compra que recalibram dinamicamente — as mensagens acionadas por eventos não podem lidar com agendamento preditivo ou ajustes de tempo quando os clientes fazem novos pedidos com antecedência ou atraso.

### Considerações técnicas

- O cálculo da frequência de compra deve levar em conta as taxas de consumo variáveis entre as categorias de produtos; um lembrete para o café deve chegar em uma cadência diferente de um para os suprimentos de limpeza.
- A jornada deve ajustar dinamicamente seu tempo quando um cliente fizer um novo pedido antes ou depois do previsto, recalibrando o próximo lembrete com base nos dados de compra atualizados.
- Os lembretes devem incluir um link de reordenação direta ou uma opção de recompra com um clique para minimizar o atrito e maximizar a conversão da notificação.
- Os clientes que já reordenaram por meio de outro canal (na loja, serviço de assinatura) devem ser suprimidos para evitar o envio de lembretes irrelevantes.


## Páginas de categoria personalizadas

Personalize dinamicamente as páginas de categoria para mostrar os produtos mais relevantes primeiro com base nas preferências, compras anteriores e comportamento de navegação de cada cliente. Quando os compradores veem produtos alinhados a seus gostos no topo da página, eles descobrem o que desejam mais rápido e fazem conversões a taxas mais altas.

### Impacto no negócio

Páginas de categoria personalizadas impulsionam o envolvimento aprimorado da página de categoria e melhoram significativamente a descoberta de produtos, especialmente para varejistas com catálogos grandes.

### Como implementar o

Use o padrão [Recomendação Comportamental](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Essa abordagem usa estratégias de seleção e modelos de classificação para reordenar produtos nas páginas de categoria com base no perfil e no comportamento em tempo real de cada visitante. Esse é o padrão correto quando a tarefa está classificando um conjunto de produtos grande e aberto usando sinais de afinidade comportamental. O Offer Decisioning não é apropriado aqui porque não há regras de qualificação ou restrições de negócios que limitam quais produtos aparecem.

### Considerações técnicas

- A classificação do produto deve ser executada com rapidez suficiente para evitar atrasos percebidos no carregamento da página. Geralmente, a personalização no lado do servidor ou a decisão baseada em borda são necessárias para páginas de categoria com centenas de produtos.
- A lógica de personalização deve combinar preferências individuais com regras de merchandising, garantindo que os produtos promovidos, os recém-chegados e os itens sazonais ainda recebam visibilidade adequada.
- A infraestrutura de teste A/B deve estar em vigor para medir o impacto na receita da classificação personalizada em relação às regras de merchandising padrão de forma contínua.
- A implementação do Web SDK [!DNL Experience Platform] deve capturar as interações de página da categoria (profundidade de rolagem, cliques no produto, uso do filtro) para refinar continuamente os modelos de classificação.


## Campanhas de acompanhamento pós-compra

Envie emails de pós-compra com dicas de atendimento ao produto, sugestões de produto relacionadas, solicitações de revisão e informações do programa de fidelidade. O período imediatamente após uma compra é quando os clientes estão mais envolvidos com a marca, tornando-a uma janela ideal para aprofundar o relacionamento e incentivar atividades futuras.

### Impacto no negócio

Campanhas pós-compra eficazes aumentam as taxas de envio de análise e geram taxas de compra repetidas melhores, transformando compradores únicos em clientes fiéis.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Esse fluxo pós-compra de várias etapas usa lógica de ramificação para personalizar as mensagens de acompanhamento com base no tipo de produto, no segmento do cliente e no envolvimento com emails anteriores na série. Esse é o padrão correto, pois o acompanhamento abrange vários dias, depende de eventos de status de atendimento e ramificações com base na categoria do produto e eventos de retorno. Uma única mensagem acionada não pode suportar a lógica condicional necessária na linha do tempo completa pós-compra.

### Considerações técnicas

- A jornada deve levar em conta o status de atendimento do pedido; dicas de atendimento e solicitações de revisão só devem ser enviadas após a entrega do produto e não imediatamente após a compra.
- O conteúdo específico do produto (instruções de cuidados, guias de uso, sugestões de acessórios) requer um sistema de mapeamento de conteúdo que associe cada categoria de produto ao material de acompanhamento relevante.
- O tempo de solicitação de revisão deve ser otimizado com base na categoria do produto; o equipamento eletrônico pode precisar de um período de uso mais longo antes de uma revisão significativa, enquanto o vestuário pode ser revisado logo após a entrega.
- Os clientes que iniciam um retorno ou troca devem ser automaticamente removidos do fluxo padrão pós-compra e redirecionados para um caminho de recuperação de serviço.


## Ofertas exclusivas de clientes do VIP

Identifique clientes de alto valor e forneça ofertas exclusivas, acesso antecipado a vendas e experiências de compras personalizadas que recompensem sua fidelidade. Manter clientes de alto nível é muito mais econômico do que adquirir novos, e o tratamento exclusivo fortalece a conexão emocional que os mantém gastando.

### Impacto no negócio

Os programas da VIP geram um forte engajamento dos clientes de nível superior e melhoram mensuravelmente o valor vitalício do cliente, reduzindo o abandono entre os segmentos mais lucrativos.

### Como implementar o

Use a [Jornada entre canais com o padrão de decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). Essa abordagem combina a orquestração de jornadas com a decisão em tempo real para a seleção de ofertas, garantindo que cada cliente do VIP receba a oferta exclusiva mais relevante em todos os canais. Esse é o padrão correto quando a jornada deve coordenar a entrega entre canais para evitar ofertas duplicadas e quando a seleção de ofertas requer regras de elegibilidade e restrições de negócios — a orquestração de várias etapas sozinha não fornece a camada de decisão em tempo real necessária para controlar qual oferta exclusiva cada VIP recebe.

### Considerações técnicas

- Os critérios de segmentação do VIP devem ser claramente definidos usando métricas de recenticidade, frequência e valor monetário, e os segmentos devem ser atualizados com frequência suficiente para capturar clientes que se qualificaram ou desqualificaram recentemente.
- As ofertas exclusivas devem ser aplicadas no ponto de resgate (Web, aplicativo, loja) para impedir que clientes não-VIP as acessem, o que requer integração com sistemas de promoção e preços.
- As preferências de canal variam significativamente entre clientes de alto valor; alguns preferem email, outros respondem a notificações do aplicativo ou correspondência direta, portanto, a jornada deve adaptar os canais de entrega com base no engajamento anterior.
- A decisão do [!DNL Journey Optimizer] deve coordenar entre canais para impedir que um cliente da VIP receba a mesma oferta por email, push e SMS simultaneamente.


## Notificações de Falta de Estoque

Permitir que os clientes se inscrevam para receber notificações quando produtos indisponíveis estiverem disponíveis, em seguida, notificá-los automaticamente por email ou mensagem de texto. A captura da demanda por produtos indisponíveis evita a perda de vendas e fornece aos clientes um motivo para retornar à loja em vez de comprar de um concorrente.

### Impacto no negócio

As notificações de retorno ao estoque atingem altas taxas de conversão entre os assinantes e reduzem significativamente as vendas perdidas para produtos de alta demanda que passam por estoques temporários.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Essa abordagem aciona notificações sobre eventos de retorno ao estoque, comparando atualizações de inventário com inscrições em notificações de clientes para fornecer alertas oportunos. Esse é o padrão correto, pois o acionador é um evento discreto do sistema de inventário, a entrega é crítica em termos de tempo (o inventário pode ser vendido novamente rapidamente) e a comunicação é uma única notificação, em vez de uma jornada contínua.

### Considerações técnicas

- O monitoramento de inventário deve detectar eventos de reabastecimento rapidamente; atrasos de algumas horas podem resultar na venda do produto novamente, antes que os clientes notificados tenham a chance de comprá-lo.
- Quando um produto popular é reabastecido em quantidade limitada, as notificações devem ser escalonadas ou priorizadas por data de inscrição para evitar o envio de alertas a mais clientes do que o estoque disponível pode atender.
- O mecanismo de inscrição para notificação deve capturar a preferência de canal (email ou mensagem de texto) e atender aos requisitos de aceitação para cada canal, especialmente para SMS.
- Os atributos de perfil do [!DNL Real-Time Customer Data Platform] devem rastrear quais produtos cada cliente está assistindo para evitar notificações duplicadas se o mesmo produto for reabastecido várias vezes.


## Personalization de prova social

Exiba uma prova social personalizada, incluindo revisões, classificações e sugestões de &quot;clientes que compraram isso também compraram&quot;, com base no perfil e nas preferências de cada cliente. Personalizar a prova social para refletir as experiências de clientes semelhantes cria confiança de maneira mais eficaz do que as classificações genéricas sozinhas.

### Impacto no negócio

Prova social personalizada aumenta as taxas de conversão e melhora a confiança do comprador, especialmente para compradores de primeira viagem e produtos com preços mais altos, onde a hesitação de compra é maior.

### Como implementar o

Use o padrão [Personalization de Aplicativo/Web de Visitante Conhecido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md). Essa abordagem personaliza o conteúdo da Web para visitantes identificados, selecionando as revisões mais relevantes e os elementos de prova social com base no perfil do cliente, nas preferências e no contexto de navegação. Esse é o padrão correto quando a personalização é orientada por atributos de perfil e associação de segmento, em vez de um modelo de afinidade comportamental. A recomendação comportamental não é apropriada aqui, pois a seleção de prova social depende de quem é o cliente, não de quais itens ele navegou.

### Considerações técnicas

- Os dados de análise e classificação devem ser estruturados e marcados por atributos do cliente (como contexto de compra, segmento do cliente e caso de uso do produto) para permitir filtragem e personalização significativas.
- Os elementos de prova social devem ser carregados de forma assíncrona para evitar o bloqueio da renderização da página principal do produto, já que os dados de revisão podem vir de uma plataforma de revisão de terceiros com tempos de resposta variáveis.
- As regulamentações de privacidade exigem que todos os dados do cliente usados para corresponder revisões aos visitantes sejam tratados de acordo com as preferências de consentimento; exibir o conteúdo de &quot;clientes como você&quot; implica em definição de perfil que pode exigir divulgação.
- A associação de público-alvo [!DNL Experience Platform] pode ser usada para selecionar quais análises destacar, mostrando análises de entusiastas de ambientes externos de outros compradores em vez de análises genéricas mais bem avaliadas.


## Consultor de produto de IA

Os varejistas online carregam milhares de SKUs em hierarquias de categorias complexas, dificultando aos compradores encontrar o produto certo sem navegação estendida ou pesquisas abandonadas. Um consultor de produtos alimentado por IA envolve os compradores em um diálogo natural de várias voltas — fazendo perguntas de qualificação sobre necessidades, preferências e orçamento — e, em seguida, restringe o sortimento a um conjunto preparado de recomendações personalizadas. A experiência reflete a orientação que um associado experiente na loja forneceria, fornecida em escala digital.

### Impacto no negócio

Os varejistas que implantam a detecção conversacional guiada observam taxas de conversão e valor médio de pedido melhores em comparação à navegação sem assistência, além de reduzir o retorno dos produtos por meio de decisões de compra mais bem informadas.

### Como implementar o

Use o padrão [Brand Concierge Conversational Experience](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md). Essa abordagem implanta a Product Advisor Agent em relação a um catálogo de produtos estruturado, usando os dados de perfil do cliente em tempo real e da AEP Agent Orchestrator para gerar recomendações de produtos personalizadas e seguras para a marca por meio de um diálogo natural. Esse é o padrão correto quando a meta é uma descoberta interativa conversacional em várias ocasiões, orientada por necessidades declaradas pelo cliente — distinta das mensagens acionadas por eventos, que são unidirecionais e reativas a uma ação específica, e das experiências personalizadas na Web, que exibem recomendações passivamente em vez de envolver os clientes em conversas. Ela requer a configuração do AEP Agent Orchestrator e do controle de marca.

### Considerações técnicas

- O catálogo de produtos deve ser estruturado com dados de atributos avançados — incluindo tamanho, material, compatibilidade, disponibilidade e preços — porque a Product Advisor Agent fundamenta recomendações no conteúdo do catálogo e não pode aconselhar de forma confiável sobre produtos com atributos incompletos.
- A pesquisa de perfil do cliente em tempo real via RT-CDP deve ser configurada com ativação de borda para que o histórico de compras, o comportamento de navegação e os dados da camada de fidelidade fiquem acessíveis durante a conversa em tempo real, sem latência que interrompa a experiência.
- As medidas de proteção do controle de marca devem ser definidas para especificar como o agente lida com itens indisponíveis, comparações de produtos competitivos, solicitações de preços promocionais e tópicos proibidos, garantindo que cada resposta esteja alinhada aos padrões de marca do varejo.
- Eventos de conversa — incluindo sinais de intenção, interações de produtos e aceitação de recomendações — devem ser capturados como XDM ExperienceEvents e transmitidos de volta para o AEP, enriquecendo os perfis do cliente com dados de afinidade de produtos que melhoram a personalização futura em todos os canais.


## Análise de atribuição entre canais

Meça como cada ponto de contato de marketing — pesquisa paga, email, promoções sociais e na loja — contribui para conversões de compras online e offline. Os varejistas que dependem da atribuição de último contato sistematicamente subvalorizam os canais de funnel superiores e tomam decisões de alocação de orçamento com base em uma imagem incompleta do caminho de compra.

### Impacto no negócio

As equipes de marketing de varejo que mudam da atribuição de último contato para multitoque obtêm uma visão mais clara de quais canais impulsionam a intenção de compra, resultando em decisões de orçamento mais bem informadas e melhor retorno sobre os gastos com marketing.

### Como implementar o

Use o padrão [Customer Analytics &amp; Insight Generation](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md). Essa abordagem conecta dados de eventos online e offline — cliques na Web, contratos de email, transações de fidelidade e registros de ponto de venda — ao Customer Journey Analytics, onde os modelos de atribuição podem ser configurados e comparados em todo o caminho de compra. Este é o padrão correto quando a meta é a medição e a geração de insight em uma jornada complexa de vários canais — em vez de ativar públicos ou acionar mensagens — e quando a análise requer o Customer Journey Analytics em vez de uma ferramenta de CDP ou de orquestração de campanhas.

### Considerações técnicas

- Os dados de transações de ponto de venda e comércio eletrônico devem compartilhar um identificador de cliente consistente para que as conversões online e na loja possam ser agrupadas em uma única visualização entre canais no CJA.
- Vários modelos de atribuição — primeiro toque, último toque, linear e declínio de tempo — devem ser configurados na visualização de dados do CJA para que os analistas possam compará-los lado a lado sem reconstruir a análise.
- Os dados de impressão de mídia paga e de cliques de plataformas de anúncios externas devem ser assimilados por meio de conectores de origem ou uploads em lote para incluir canais pagos no caminho de atribuição ao lado de canais próprios.
- As janelas de conversão e os períodos de pesquisa de crédito precisam ser definidos por tipo de canal, já que a janela de atribuição relevante para um clique de pesquisa paga é significativamente diferente de uma campanha de email sazonal.

## Segmentação e ativação de público para mídia paga

Crie segmentos de público-alvo de alto valor a partir de perfis unificados do cliente e ative-os em destinos de mídia paga, como Google Ads, Meta e The Trade Desk para campanhas de aquisição e redirecionamento. A unificação de dados comportamentais, transacionais e de fidelidade permite um direcionamento mais preciso, que reduz o desperdício de anúncios e melhora o retorno do investimento da campanha.

### Impacto no negócio

Os varejistas que ativam públicos originais de alta qualidade observam taxas de correspondência aprimoradas em plataformas de mídia paga, custo por aquisição reduzido e retorno mais forte sobre o gasto com anúncios em comparação a depender de segmentos de terceiros.

### Como implementar o

Use o padrão [Audience Activation para Destinos](/help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md) para avaliar a associação de público-alvo em relação a perfis unificados e publicar segmentos em destinos de mídia paga conectados, de forma programada ou por transmissão. Esse é o padrão correto quando o requisito principal é a publicação de segmentos em sistemas externos, em vez de mensagens orquestradas ou decisões em tempo real.

### Considerações técnicas

- A resolução de identidade em dados da Web, móveis e de fidelidade é necessária para criar perfis completos de clientes antes da ativação — perfis fragmentados reduzem a qualidade do público-alvo e as taxas de correspondência.
- Os conectores de destino devem ser configurados para cada plataforma de mídia paga, com sinalizadores de consentimento apropriados respeitados no nível do perfil para impedir que dados não consentidos sejam ativados.
- A frequência de atualização do segmento deve estar alinhada aos objetivos da campanha — os públicos-alvo de aquisição podem precisar de atualizações diárias, enquanto os públicos-alvo de redirecionamento se beneficiam de atualizações quase em tempo real para excluir compradores recentes.
- A análise de sobreposição entre os públicos-alvo de aquisição e retenção ajuda a evitar a contaminação cruzada em que os clientes existentes recebem mensagens de aquisição de novos clientes.


## Supressão de cliente para campanhas de aquisição

Suprima clientes existentes e conversores recentes do gasto de aquisição e exclusão, ativando públicos-alvo de exclusão para destinos de mídia paga, reduzindo o gasto desperdiçado. A sincronização contínua das listas de supressão garante que os orçamentos pagos tenham como alvo os novos clientes potenciais em vez de pessoas que já converteram ou que estejam ativamente envolvidas.

### Impacto no negócio

Suprimir clientes existentes das campanhas de aquisição reduz o gasto com mídia paga desperdiçado, melhora as métricas de custo por aquisição e impede que os clientes existentes recebam mensagens que são irrelevantes para o estágio de relacionamento.

### Como implementar o

Use o padrão [Audience Activation para Destinos](/help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md) para publicar públicos-alvo de exclusão — compradores recentes, assinantes ativos, clientes de alto valor — em cada destino de mídia paga com frequência. Esse é o padrão correto quando o objetivo é a publicação de segmentos para supressão, em vez de orquestrar uma jornada voltada para o cliente.

### Considerações técnicas

- Os públicos-alvo de supressão exigem uma definição clara de quem excluir: geralmente, clientes que compraram nos últimos 30 a 90 dias, membros de fidelidade ativos e conversões recentes de email.
- As listas de exclusão devem ser atualizadas com frequência suficiente para excluir compradores antes que os anúncios sejam veiculados; as listas de supressão obsoletas causam mais atrito de marca em períodos de varejo de alto volume.
- A qualidade da correspondência de identidade afeta diretamente a precisão da supressão — uma correspondência ruim de email ou ID de dispositivo resultará na visualização de anúncios de aquisição pelos clientes existentes.
- Certifique-se de que os públicos-alvo de supressão estejam separados dos públicos-alvo de retenção para que as campanhas de retorno ainda possam alcançar os clientes decorridos que não devem ser suprimidos.


## Experiências da Web personalizadas para visitantes conhecidos

Forneça banners personalizados, recomendações de produtos e conteúdo promocional para visitantes autenticados do site com base no perfil em tempo real, na associação do segmento e no histórico comportamental. Quando clientes recorrentes veem experiências personalizadas para seu status de fidelidade, histórico de compras e preferências, as taxas de engajamento e a conversão melhoram significativamente em comparação às experiências genéricas na página inicial.

### Impacto no negócio

Os varejistas que personalizam para visitantes conhecidos veem melhorias significativas nas métricas de envolvimento, incluindo tempo no site, páginas por sessão e taxa de conversão, com o maior impacto entre os membros de fidelidade que visitam com frequência.

### Como implementar o

Use o padrão [Personalization de Aplicativo/Web de Visitante Conhecido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) para fornecer experiências personalizadas orientadas por perfil no carregamento da página, usando a associação de segmento em tempo real e atributos de perfil. Esse é o padrão correto quando a experiência deve ser orientada por dados de perfil vinculados à identidade, em vez de sinais somente de sessão, e quando as decisões de conteúdo não exigem classificação complexa de ofertas ou restrições de negócios.

### Considerações técnicas

- A autenticação deve ocorrer antes que a personalização orientada por perfil possa ser ativada; o site precisa de um mecanismo para identificar o visitante e resolver sua ECID para um perfil conhecido.
- As pesquisas de perfil em tempo real devem ser concluídas dentro do orçamento de latência de carregamento da página, o que geralmente exige a avaliação do perfil implantado na borda, em vez de chamadas de API do lado do servidor, no caminho de renderização crítico.
- As variações de conteúdo devem ser projetadas para todos os segmentos de público-alvo que serão direcionados, incluindo uma experiência padrão para visitantes que não correspondem a nenhuma regra de personalização.
- As decisões do Personalization devem ser registradas para análise, permitindo testes A/B de variações de conteúdo e atribuição de melhorias de engajamento a segmentos específicos.


## Visitante anônimo - Web Personalization

Personalize o conteúdo para visitantes não identificados do site usando sinais comportamentais na sessão, como páginas visualizadas, categorias de produto navegadas e fonte de referência. Como a maioria do tráfego da Web de varejo é anônimo, personalizar para visitantes não reconhecidos expande significativamente o alcance da personalização no site para além do segmento autenticado.

### Impacto no negócio

Os varejistas que veiculam experiências personalizadas para visitantes anônimos observam taxas de conversão aprimoradas de envolvimento e primeira visita, com impacto particularmente forte nos visitantes que chegam de fontes específicas de campanha ou navegam em páginas de categoria de alta intenção.

### Como implementar o

Use o padrão [Anonymous Visitor Web Personalization](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md) para avaliar os sinais comportamentais na sessão na borda e fornecer variações de conteúdo relevantes sem exigir autenticação. Esse é o padrão correto quando a personalização deve funcionar imediatamente a partir da primeira interação, sem depender de um perfil persistente, especialmente para o tráfego de aquisição e visitantes que ainda não fizeram logon.

### Considerações técnicas

- A personalização na sessão depende dos dados do evento de transmissão coletados pelo Edge Network; as regras de avaliação da borda devem ser implantadas e testadas antes que o tráfego seja enviado para elas.
- As variações de conteúdo devem ser projetadas com base em comportamentos de alto sinal na sessão — fonte de referência, primeira página visualizada, categoria de produto explorada — em vez de atributos de baixo sinal que não preveem a intenção de maneira confiável.
- Os requisitos de privacidade devem ser avaliados com cuidado; algumas jurisdições tratam a personalização comportamental como exigência de consentimento, mesmo para visitantes anônimos.
- As regras do Personalization para visitantes anônimos devem ser avaliadas de forma mais simples e rápida do que as regras para visitantes conhecidos, já que as restrições de latência de borda são mais rigorosas.


## Jornada da série de boas-vindas

Orquestrar uma jornada de boas-vindas em várias etapas para clientes recém-registrados, fornecendo conteúdo de integração, treinamento de produtos e um incentivo de primeira compra em canais de email e push. Uma série de boas-vindas bem projetada define o tom do relacionamento com o cliente e aumenta significativamente a probabilidade de um novo registrando se converter em sua primeira compra.

### Impacto no negócio

Os programas da série Welcome promovem melhorias significativas nas taxas de ativação de novos clientes e na conversão de primeira compra, com o maior impacto quando a série combina conteúdo educacional com um incentivo oportuno e personalizado.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para criar uma sequência de integração de vários dias com etapas de espera, ramificação de canal com base em envolvimento e supressão quando a meta de primeira compra for atingida. Esse é o padrão correto quando o caso de uso requer um fluxo de comunicação sequenciado e espaçado no tempo com lógica condicional: uma única mensagem acionada é insuficiente para orientar um novo cliente durante a experiência de integração.

### Considerações técnicas

- A entrada de jornada deve ser acionada por eventos de registro de conta em tempo real, para que a primeira mensagem de boas-vindas chegue imediatamente enquanto a intenção de registro for alta.
- A jornada deve incluir condições de saída que suprimem as mensagens restantes quando um novo cliente conclui sua primeira compra — continuar a série de boas-vindas após a compra prejudica a relevância da mensagem.
- A preferência de canal deve ser respeitada em todo o; as etapas de notificação por push exigem a instalação do aplicativo e a aceitação por push, com fallback por email para clientes sem a aceitação.
- O Personalization na série de boas-vindas melhora a conversão, mas requer dados de perfil suficientes para serem significativos — novos perfis geralmente precisam de um fallback para os best-sellers ou produtos de tendências.


## Recuperação de abandono do carrinho

Acione notificações por email e por push em tempo real quando um cliente abandonar o carrinho de compras, com lembretes de produto personalizados e incentivos com limite de tempo para concluir a compra. O abandono do carrinho está entre os casos de uso de ROI mais alto no varejo, recuperando a receita de clientes que já demonstraram uma forte intenção de compra.

### Impacto no negócio

Os programas de abandono de carrinho bem executados recuperam uma parte significativa da receita abandonada, com as taxas de recuperação mais altas quando a primeira mensagem chega dentro de uma hora de abandono e inclui os itens exatos deixados no carrinho.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para responder ao evento de abandono de carrinho com uma comunicação acionada imediatamente enquanto a intenção de compra ainda estiver ativa. Esse é o padrão correto quando uma ação discreta do cliente é o acionador e o requisito principal é uma resposta oportuna e personalizada, em vez de uma sequência de criação de várias semanas ou uma decisão de oferta complexa com restrições de negócios.

### Considerações técnicas

- A detecção de abandono do carrinho requer um limite de inatividade definido (normalmente de 30 a 60 minutos) para evitar que os clientes de mensagens que ainda estejam navegando ativamente ou concluindo o fluxo de finalização da compra.
- O conteúdo do email deve renderizar dinamicamente as imagens atuais do produto, os preços e o status do inventário no momento do envio, pois os itens podem esgotar ou alterar o preço entre o abandono e a entrega de mensagens.
- A lógica de supressão deve excluir os clientes que concluíram a compra por meio de outro canal entre a detecção de abandono e o envio de mensagem.
- As regras de limite de frequência devem evitar mensagens de abandono de carrinho repetido em janelas curtas, especialmente para clientes que habitualmente abandonam carrinhos como um comportamento de navegação.


## Jornada de envolvimento pós-compra

Fornecer comunicações pós-compra, incluindo confirmação de pedido, atualizações de envio, recomendações de venda cruzada e solicitações de revisão, por meio de uma jornada orquestrada em várias etapas. A janela pós-compra é um dos momentos de maior envolvimento no ciclo de vida do cliente, tornando-o o momento ideal para criar fidelidade e apresentar produtos complementares relevantes.

### Impacto no negócio

Varejistas com jornadas pós-compra estruturadas observam melhores taxas de compra repetida e taxas de envio de análise do cliente, contribuindo para a fidelidade de longo prazo e para a prova social que suporta aquisições futuras.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para orquestrar uma sequência de comunicações pós-compra cronometradas para os principais marcos: confirmação de pedido, remessa, entrega e acompanhamento pós-entrega. Esse é o padrão correto quando o caso de uso abrange vários dias com vários objetivos — uma única mensagem acionada não pode acomodar o arco, desde a confirmação transacional até a criação de fidelidade e a solicitação de revisão.

### Considerações técnicas

- A integração do sistema de gerenciamento de pedidos é necessária para receber eventos de compra e remessa em tempo real; atrasos na assimilação de eventos criam um tempo estranho nas comunicações pós-compra.
- As recomendações de venda cruzada na sequência pós-compra exigem dados do catálogo de produtos em tempo real e inferência do modelo de recomendação no tempo de renderização da mensagem para refletir o estoque e os preços atuais.
- As mensagens de solicitação de revisão devem estar em conformidade com os termos de serviço da plataforma para revisões incentivadas e devem ser cronometradas após o cliente ter tido tempo suficiente para usar o produto.
- A coordenação de canais é importante: os clientes não devem receber email e push pelo mesmo marco, a menos que tenham interagido com o primeiro canal.


## Campanha de atualização do nível de fidelidade

Identifique clientes que se aproximam dos limites do nível de fidelidade e forneça campanhas direcionadas incentivando-os a alcançar o próximo nível com ofertas personalizadas com base no histórico de compras e preferências. Quando os clientes estão ao alcance de uma atualização de nível, mensagens direcionadas com incentivos personalizados criam urgência e impulsionam um comportamento de compra incremental.

### Impacto no negócio

As campanhas de atualização no nível de fidelidade impulsionam o volume de compras incremental e melhoram o engajamento no programa, com o maior impacto entre os membros intermediários que estão próximos do próximo limite e mostraram atividade de compra recente.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para criar uma campanha de proximidade de camada que insira clientes quando eles atingirem um limite de gastos definido abaixo do próximo nível de camada e os oriente por uma sequência de mensagens de benefícios e ofertas de incentivo. Este é o padrão correto quando o caso de uso requer o monitoramento de um atributo de perfil calculado ao longo do tempo e a orquestração de uma campanha em várias etapas vinculada ao progresso do cliente em direção a uma meta.

### Considerações técnicas

- Os dados da plataforma de fidelidade — equilíbrio entre pontos, status do nível, limites do nível — devem ser assimilados e mantidos atualizados no perfil do cliente para que os cálculos de proximidade do nível sejam precisos.
- As campanhas de atualização de camada devem ser suprimidas para clientes que já atingiram a camada de destino ou cujo status de fidelidade foi alterado desde a entrada da campanha.
- Os incentivos personalizados na campanha de atualização devem ser limitados às ofertas para as quais o cliente está realmente qualificado e que não comprometem o valor percebido da estrutura de nível.
- A campanha deve incluir condições de saída claras para os clientes que concluírem sua atualização de nível no meio da jornada, girando para uma mensagem de parabéns em vez de continuar a sequência de persuasão.


## Orquestração de campanha entre canais

Orquestrar campanhas de marketing coordenadas por email, SMS, push e canais da Web com ramificação de jornada, etapas de espera e limite de frequência para maximizar o engajamento sem fadiga. A orquestração coordenada entre canais garante que os clientes recebam uma experiência de campanha coerente, independentemente do canal ao qual respondam primeiro, eliminando mensagens duplicadas e ofertas conflitantes.

### Impacto no negócio

Varejistas com recursos de orquestração entre canais observam taxas de envolvimento e conversão de campanha mais altas do que campanhas de canal único, além de reduzir as taxas de cancelamento de inscrição impulsionadas pela fadiga do canal por mensagens não coordenadas.

### Como implementar o

Use o padrão [Jornada entre canais com decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para criar campanhas que encaminham os clientes por sequências de canal personalizadas com base no histórico de envolvimento, nas preferências do canal e nos sinais de resposta em tempo real. Este é o padrão correto quando a campanha requer seleção de oferta controlada, roteamento de preferência de canal e ramificação dinâmica com base no engajamento na jornada, em vez de uma sequência fixa enviada a todos os recipients da campanha.

### Considerações técnicas

- Os limites globais de frequência devem ser configurados em todos os canais para evitar que os clientes recebam comunicações excessivas quando várias jornadas estiverem sendo executadas simultaneamente.
- Os dados de preferência de canal devem ser atuais e acionáveis — perfis de preferência com meses de atraso encaminharão os clientes para canais com os quais não interagem mais.
- A lógica de orquestração de jornadas deve lidar com a reentrada com cuidado, evitando que os clientes entrem na mesma campanha duas vezes, garantindo que não sejam excluídos de campanhas genuinamente novas.
- Os sinais de engajamento em tempo real (aberturas de email, cliques em links, sessões da Web) devem alimentar a jornada para permitir a alternância de canais e a saída antecipada de clientes que já tenham convertido.


## Experiência de conversa do Brand Concierge

Implante um agente de conversação seguro para marcas e alimentado por IA em propriedades digitais para fornecer orientação personalizada do produto, ajuda de navegação do site e entrega contínua para agentes ativos. Um concierge de IA no local amplia o serviço personalizado em escala, ajudando os compradores a descobrir produtos, comparar opções e concluir compras sem exigir intervenção do agente humano para consultas comuns.

### Impacto no negócio

Os varejistas com recursos de concierge de IA informam que melhoraram as taxas de resolução de autoatendimento, reduziram o volume de suporte de entrada para perguntas sobre produtos e navegação e aumentaram a conversão entre clientes que interagem com orientação conversacional antes da compra.

### Como implementar o

Use o padrão [Brand Concierge Conversational Experience](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md) para implantar um agente de IA controlada com base nos dados do catálogo de produtos, nas diretrizes da marca e no contexto do perfil do cliente em tempo real. Este é o padrão correto quando o caso de uso requer interação de linguagem natural em um conjunto de produtos grande e dinâmico, em vez de um chatbot com scripts e intenções fixas ou um padrão que corresponde a um canal específico, como o email.

### Considerações técnicas

- O agente de IA deve se basear nos dados atuais do catálogo de produtos, incluindo descrições, especificações, disponibilidade e preços para fornecer orientação precisa; dados obsoletos do produto levam a recomendações incorretas.
- As medidas de proteção de segurança da marca devem ser configuradas para impedir que o agente discuta sobre produtos de concorrentes, assuma compromissos de preços que entrem em conflito com as promoções ou responda a consultas fora do tópico.
- A lógica de transferência para agentes ativos requer integração com a plataforma de serviço e deve ser acionada quando o agente de IA não puder resolver a consulta do cliente após um número definido de rodadas.
- A integração de dados de perfil permite que o agente personalize as respostas com base no histórico de compras e no status de fidelidade, mas isso requer a resolução de identidade antes do início da sessão de conversação.

## Lembrete de check-in com o CTA de download do aplicativo

Lembre os convidados de fazer o check-in e incentive-os a baixar o aplicativo para acessar as informações facilmente. Lembretes de check-in em tempo hábil, juntamente com prompts de download de aplicativos, impulsionam o engajamento móvel e permitem experiências mais avançadas no local.

### Impacto no negócio

Os varejistas que combinam lembretes de check-in com planos de ação para download de aplicativos veem maiores taxas de adoção de aplicativos e maior engajamento na loja, já que os clientes que usam o aplicativo móvel tendem a interagir com mais frequência com promoções e conteúdo do local.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para acionar um lembrete de check-in com o CTA de download de aplicativo com base na participação no evento ou nos dados de reserva. Este é o padrão correto quando uma única mensagem oportuna precisa ser enviada em resposta a um evento ou acionador de agendamento conhecido.

### Considerações técnicas

- Os lembretes de check-in devem ser cronometrados adequadamente em relação à data do evento ou da visita para maximizar o engajamento sem serem vistos como muito cedo ou muito tarde.
- Os deep links de download de aplicativos devem ser roteados para a loja de aplicativos correta com base na plataforma do dispositivo do cliente (iOS ou Android).
- Os clientes que já têm o aplicativo instalado devem receber uma variante de mensagem diferente que ignora o CTA de download e se concentra na funcionalidade de check-in.

## Campanhas de aniversário para fãs

Direcione os fãs em seu aniversário com uma mensagem de aniversário personalizada e uma oferta exclusiva. As campanhas de aniversário criam conexões emocionais com os fãs e impulsionam compras incrementais por meio de alcance imediato e personalizado.

### Impacto no negócio

As campanhas de aniversário oferecem consistentemente taxas de abertura e conversão acima da média, pois chegam a um momento de significado pessoal, criando boa vontade e incentivando os fãs a se tratarem com uma compra especial.

### Como implementar o

Use o padrão [Mensagens acionadas por evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para enviar uma mensagem de aniversário personalizada quando a data de aniversário do cliente chegar. Esse é o padrão correto quando uma única mensagem orientada por eventos é enviada com base em um acionador de data de atributo de perfil.

### Considerações técnicas

- A data de aniversário deve ser capturada no perfil do cliente e validada para evitar o envio de mensagens em datas incorretas.
- As ofertas devem ter uma janela de validade definida (como a semana de aniversário) para criar urgência, proporcionando aos clientes tempo razoável para resgatar.
- Os fãs sem um aniversário no arquivo devem ser excluídos da campanha em vez de enviar uma mensagem genérica.

## Campanhas de aniversário para compradores

Direcione os compradores em seu aniversário com uma mensagem de aniversário personalizada e uma oferta exclusiva. As campanhas de aniversário geram fidelidade à marca, reconhecendo pessoalmente os clientes e incentivando uma compra comemorativa.

### Impacto no negócio

As ofertas de aniversário personalizadas impulsionam taxas de resgate mais altas do que as promoções genéricas, pois se alinham a um momento em que os compradores já estão inclinados a fazer compras discricionárias para si mesmos.

### Como implementar o

Use o padrão [Mensagens acionadas por evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para acionar uma mensagem de aniversário e uma oferta com base no atributo de perfil da data de nascimento do comprador. Esse é o padrão correto quando uma única mensagem personalizada precisa ser entregue em uma data de calendário específica vinculada ao perfil do cliente.

### Considerações técnicas

- A data de aniversário deve ser armazenada como um atributo de perfil e deve ser coletada durante o registro ou a inscrição para fidelidade.
- A personalização da oferta deve considerar o histórico de compras e as preferências do comprador para apresentar sugestões de produto relevantes juntamente com o desconto de aniversário.
- A lógica de supressão duplicada é necessária para clientes que aparecem em vários sistemas para evitar o envio de várias mensagens de aniversário.

## Campanhas de promoção de dia do jogo

Direcione os fãs para comprar ingressos para um próximo jogo com promoções e ofertas personalizadas. As promoções de dias de jogos impulsionam as vendas de ingressos atingindo o público certo com mensagens oportunas e específicas do evento.

### Impacto no negócio

Promoções direcionadas de dias de jogos melhoram as taxas de venda de ingressos, alcançando os fãs com ofertas relevantes com base nas preferências da equipe, na presença anterior e na proximidade do local.

### Como implementar o

Use o padrão [Ativação de mensagem de saída em lote](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md) para enviar mensagens promocionais para públicos-alvo segmentados de fãs antes dos próximos jogos. Esse é o padrão correto quando um lote de mensagens personalizadas precisa ser enviado para um segmento de público-alvo pré-criado de forma programada.

### Considerações técnicas

- Os dados do cronograma de jogos devem ser integrados para acionar promoções no prazo certo antes de cada evento.
- A segmentação de público deve levar em conta a afinidade da equipe, a proximidade geográfica e os padrões de presença anteriores para maximizar a relevância.
- Os clientes que já compraram ingressos para o jogo promovido devem ser suprimidos das mensagens de aquisição e podem receber ofertas de venda adicional para atualizações ou complementos.

## Campanhas de promoção de produtos

Direcione os compradores para comprar produtos durante uma campanha de promoção contínua de produtos. As campanhas promocionais geram receita ao conectar os clientes certos com ofertas oportunas alinhadas a promoções ativas.

### Impacto no negócio

As campanhas de promoção de produtos direcionadas superam as promoções de amplo alcance, concentrando-se nos compradores com maior probabilidade de conversão, reduzindo o desperdício promocional e melhorando o retorno sobre os gastos com marketing.

### Como implementar o

Use o padrão [Ativação de Mensagem de Saída em Lote](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md) para enviar mensagens promocionais a segmentos de público qualificados durante as janelas ativas da campanha. Esse é o padrão correto quando um lote agendado de mensagens promocionais personalizadas precisa alcançar um público-alvo definido durante uma campanha com limite de tempo.

### Considerações técnicas

- As datas de início e término da promoção devem ser gerenciadas para garantir que as mensagens só sejam enviadas durante a janela de promoção ativa.
- A segmentação de público-alvo deve aproveitar o histórico de compras, o comportamento de navegação e a afinidade de produtos para direcionar os compradores mais propensos a se engajar com os produtos promovidos.
- O limite de frequência deve ser aplicado para evitar fadiga promocional, especialmente quando várias campanhas são executadas simultaneamente.

## Abandono de carrinho de compras

Reenvolva os clientes que abandonam o carrinho de compras com lembretes e incentivos personalizados para concluir a compra. A recuperação de abandono do carrinho é um dos casos de uso com ROI mais alto no marketing de varejo.

### Impacto no negócio

As campanhas de recuperação de abandono do carrinho recuperam uma porcentagem significativa da receita perdida de outra forma, envolvendo novamente os compradores no momento da maior intenção de compra com lembretes e incentivos personalizados.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para acionar uma mensagem de recuperação quando um evento de abandono de carrinho for detectado. Esse é o padrão correto quando uma única mensagem em tempo real precisa ser enviada em resposta a um evento comportamental, como deixar itens no carrinho sem concluir o check-out.

### Considerações técnicas

- A detecção de abandono do carrinho requer um limite de inatividade definido (normalmente de 30 a 60 minutos) para distinguir o abandono verdadeiro dos clientes que ainda estão navegando.
- O conteúdo do carrinho deve ser transmitido na carga do evento para habilitar lembretes de produto personalizados na mensagem de recuperação.
- Os clientes que concluírem sua compra entre o evento de abandono e o envio da mensagem devem ser suprimidos para evitar mensagens irrelevantes.
