---
title: Casos de uso de viagem e hospitalidade
description: Descubra como as organizações de viagem e hospitalidade usam o Adobe Experience Platform para personalizar experiências de reserva, recuperar reservas abandonadas e criar fidelidade do visitante.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: fbdcc015-96a4-4015-93e2-3fc7db375c13
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '3648'
ht-degree: 0%

---

# Casos de uso de viagem e hospitalidade

As organizações de viagem e hospitalidade usam o Adobe Experience Platform para reunir dados de visitantes de mecanismos de reserva, programas de fidelidade, sistemas de gerenciamento de propriedade e pontos de contato digitais em uma única visualização de cada viajante. Essa fundação unificada capacita experiências personalizadas que inspiram reservas, recuperam reservas abandonadas e criam o tipo de fidelidade do convidado que impulsiona visitas repetidas.

## Página inicial personalizada para novos visitantes

Mostre recomendações personalizadas de cruzeiro, hotel e destino na página inicial com base na localização geográfica do visitante e no comportamento de navegação. Os visitantes que visitam pela primeira vez e veem opções de viagem relevantes imediatamente têm muito mais probabilidade de explorar mais e iniciar o processo de reserva.

### Impacto no negócio

A personalização da página inicial para novos visitantes impulsiona taxas de conversão aprimoradas, apresentando opções de viagem que correspondem à localização e aos interesses do visitante, em vez de conteúdo genérico.

### Como implementar o

Use o padrão [Web Personalization de Visitante Anônimo](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md). Essa abordagem fornece conteúdo personalizado para visitantes que ainda não se identificaram, usando sinais disponíveis, como geolocalização, tipo de dispositivo e fonte de referência, para personalizar a experiência desde a primeira página. Esse é o padrão correto quando o visitante ainda não se identificou e a personalização deve depender dos sinais disponíveis, como geolocalização, tipo de dispositivo e fonte de referência — a personalização de visitante conhecido requer um perfil autenticado que ainda não existe.

### Considerações técnicas

- Os dados de geolocalização devem ser resolvidos com precisão na borda para atender destinos, moedas e portas de partida apropriados para a região, sem adicionar latência à carga da página inicial.
- As regras do Personalization devem levar em conta as tendências de viagens sazonais por região, enfrentando destinos de clima quente para visitantes em climas frios durante os meses de inverno, por exemplo.
- As estratégias de conteúdo de fallback são essenciais para visitantes cuja localização não pode ser determinada ou que chegam por meio de serviços de anonimato.
- A integração com o feed de disponibilidade do sistema de reservas garante que as propriedades e os itinerários em destaque sejam realmente reserváveis, evitando a frustração de promover opções esgotadas.


## Jornada de recuperação de abandono do carrinho

Detecte automaticamente quando um cliente abandona o carrinho de reserva e acione uma jornada de email de várias etapas com ofertas personalizadas para incentivar a conclusão. Reservas abandonadas representam um dos maiores vazamentos de receita em viagens e hospitalidade, e acompanhamento oportuno, enquanto a intenção de viagem ainda é recente e recupera uma parcela significativa dessas reservas.

### Impacto no negócio

Os programas eficazes de recuperação de reservas atingem taxas significativas de recuperação do carrinho e podem gerar receita incremental significativa, dependendo do volume de reservas e do valor médio do percurso.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Essa abordagem responde a um evento de abandono de carrinho em tempo real, enviando um lembrete em tempo hábil enquanto a intenção de viagem do cliente ainda é alta. Esse é o padrão correto quando o acionador é um evento de comportamento do cliente em tempo real e a resposta necessária é uma mensagem única e sensível ao tempo, em vez de uma sequência de criação de várias etapas ou seleção de oferta dinâmica que muda com base na resposta do cliente.

### Considerações técnicas

- Os limites de detecção de abandono do carrinho devem levar em conta os ciclos de consideração mais longos típicos em compras de viagem; um atraso de 2 a 4 horas antes do primeiro lembrete geralmente é mais apropriado do que os 30 a 60 minutos usados no varejo.
- O conteúdo do email deve obter dinamicamente os preços atuais, a disponibilidade de quartos ou cabines e imagens do sistema de reservas no momento do envio, já que o inventário e as taxas de viagem mudam com frequência.
- Incentivos personalizados, como atualizações complementares ou créditos de resort, devem ser gerenciados por meio de regras de negócios que contabilizam margem, sazonalidade e o nível de fidelidade do cliente.
- A lógica de supressão deve excluir clientes que concluíram sua reserva por meio de outro canal, como uma central de atendimento ou agente de viagens, para evitar mensagens de acompanhamento irrelevantes.


## Direcionamento de visitantes de alta intenção

Identifique visitantes com alta intenção de compra usando a pontuação de propensão alimentada por IA e direcione-os com ofertas e conteúdo personalizados. Reconhecer quais visitantes têm maior probabilidade de reservar permite que a organização concentre suas ofertas e alcance de vendas mais atraentes nos viajantes que estão mais próximos de tomar uma decisão.

### Impacto no negócio

Direcionar visitantes de alta intenção com ofertas personalizadas resulta em uma conversão aprimorada para esses segmentos, concentrando o investimento em marketing onde ele oferece maior retorno.

### Como implementar o

Use o padrão [Personalization de Aplicativo/Web de Visitante Conhecido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md). Essa abordagem usa dados de perfil em tempo real e sinais comportamentais para personalizar a experiência da Web de visitantes identificados, fornecendo conteúdo personalizado e ofertas que correspondem ao nível de preparação para compra. Esse é o padrão correto quando a personalização é orientada por atributos de perfil e pontuações de propensão para clientes identificados, em vez de um modelo de afinidade comportamental, e quando o cliente já está autenticado, disponibilizando seus sinais de associação e intenção de segmento.

### Considerações técnicas

- Os modelos de propensão devem ser treinados em sinais de intenção específicos de viagem, como pesquisas de data, preços de exibições de página, atividade de comparação de sala e visitas repetidas ao mesmo destino em uma janela curta.
- Intervenções de alta intenção, como prompts de bate-papo ao vivo ou ofertas por tempo limitado, devem aparecer em pontos de decisão naturais no fluxo de reserva, em vez de interromper a experiência de navegação.
- O modelo de pontuação deve distinguir entre a intenção de pesquisa e a intenção de reserva, já que os viajantes muitas vezes pesquisam meses antes de estarem prontos para comprar.
- [!DNL Real-Time Customer Data Platform] atributos computados podem agregar sinais comportamentais entre sessões para manter uma pontuação de intenção atualizada para cada visitante.


## Campanhas de venda adicional pós-reserva

Depois que um cliente concluir uma reserva, acione automaticamente campanhas de venda adicional para atualizações de cabine, excursões em terra, pacotes de refeições e outros auxiliares. O período entre a reserva e a viagem é quando os hóspedes estão mais animados com a sua próxima viagem e mais receptivos a melhorar a sua experiência.

### Impacto no negócio

As campanhas de venda adicional pós-reserva aumentam o valor médio de pedido e aumentam a receita auxiliar, transformando uma única reserva em uma transação significativamente mais valiosa.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Este guia de jornada de várias etapas reservou clientes por meio de uma sequência cronometrada de oportunidades de venda adicional, adaptando as ofertas com base no que o convidado já comprou e seu envolvimento com mensagens anteriores. Esse é o padrão correto quando o caso de uso requer um fluxo sequenciado de várias mensagens ao longo de dias com ramificação condicional com base nos eventos de engajamento e na disponibilidade do inventário — uma única mensagem acionada não pode acomodar a lógica de dependência entre momentos de venda adicional ou ajustes de tempo com base na proximidade da data da viagem.

### Considerações técnicas

- A jornada deve se integrar ao sistema de reservas para saber exatamente o que o convidado reservou, quais atualizações estão disponíveis para seu itinerário específico e os preços atuais para cada opção auxiliar.
- O horário de venda adicional deve ser escalonado estrategicamente; as atualizações da cabine podem ser oferecidas logo após a reserva, enquanto as excursões e os pacotes de refeições têm melhor desempenho à medida que a data da viagem se aproxima.
- O inventário e a disponibilidade de produtos auxiliares devem ser verificados no momento da apresentação da oferta, uma vez que a capacidade de deslocamento e a disponibilidade de atualização mudam continuamente.
- A personalização do [!DNL Journey Optimizer] deve levar em conta o número de viajantes na reserva, recomendando excursões apropriadas para a família em reservas familiares e experiências orientadas para casais em reservas para duas pessoas.


## Campanhas de retorno para clientes obsoletos

Identifique os clientes que não reservaram em doze ou mais meses e envolva-os com ofertas de retorno personalizadas e conteúdo com base em suas preferências de viagem anteriores. Reengajar os hóspedes lapsados é significativamente mais econômico do que adquirir clientes totalmente novos, e os viajantes anteriores já têm familiaridade com a marca que reduz a barreira para o reagendamento.

### Impacto no negócio

Campanhas de retorno bem direcionadas alcançam taxas de reativação significativas entre clientes antigos, recuperando a receita de clientes que podem nunca retornar.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Essa jornada de várias etapas reenvolve clientes antigos com uma série progressiva de mensagens que evoluem de inspiração para incentivo com base na resposta do cliente. Esse é o padrão correto quando não há evento de acionamento discreto e o tempo deve ser calculado a partir dos modelos de ciclo de vida do cliente e dos padrões de reserva sazonal — as mensagens acionadas por evento não podem lidar com a lógica de escalonamento progressivo ou com a necessidade de cronometrar as ofertas em torno das janelas de planejamento de viagem típicas.

### Considerações técnicas

- A segmentação do cliente cancelada deve levar em conta a frequência típica de reserva na categoria de viagem; um cliente que faz reservas anualmente não deve ser sinalizado como cancelado após apenas seis meses de inatividade.
- O conteúdo de retorno deve fazer referência às preferências de viagem anteriores do cliente, como destinos preferenciais, tipos de cabine ou temporadas de viagem, para demonstrar que a marca se lembra e os valoriza.
- As ofertas devem escalar ao longo da jornada, começando com conteúdo inspirador e progredindo para incentivos monetários somente se mensagens anteriores não gerarem engajamento.
- Os registros do cliente devem ser verificados em relação ao sistema de reservas para quaisquer reservas feitas por canais offline, como agências de viagens ou centrais de atendimento, para evitar o envio de mensagens de retornos para clientes que estejam realmente ativos.


## Recomendações dinâmicas de Itinerário

Mostre itinerários e destinos de cruzeiro personalizados com base nas reservas passadas, no histórico de navegação e nas preferências declaradas do cliente. Quando os viajantes veem itinerários adaptados aos seus interesses e estilo de viagem, eles se envolvem mais profundamente com a experiência de planejamento e avançam para a reserva mais rapidamente.

### Impacto no negócio

As recomendações de itinerário personalizadas promovem um engajamento aprimorado com páginas de itinerário, ajudando os clientes a encontrar a viagem certa mais rápido e reduzindo a queda que ocorre quando os viajantes se sentem sobrecarregados com muitas opções.

### Como implementar o

Use o padrão [Personalization de Aplicativo/Web de Visitante Conhecido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md). Essa abordagem personaliza o conteúdo do site para visitantes identificados, usando os dados de perfil e o histórico comportamental para mostrar os itinerários e destinos mais relevantes. Esse é o padrão correto quando a personalização é orientada por atributos de perfil e histórico de reservas, em vez de um modelo de afinidade comportamental, permitindo que a lógica baseada em regras considere a logística de viagens, como portas de partida e datas, juntamente com as preferências do cliente.

### Considerações técnicas

- A lógica de recomendação de itinerário deve incorporar datas de navegação ou estadia, portos de partida e preferências de duração juntamente com o interesse de destino para apresentar opções que são atraentes e práticas para o cliente.
- A integração com o sistema central de reservas garante que os itinerários recomendados tenham inventário disponível e reflitam os preços atuais, evitando a frustração de promover viagens esgotadas ou propriedades totalmente reservadas.
- Os fatores sazonais devem influenciar fortemente as recomendações; os clientes que reservaram anteriormente cruzeiros mediterrânicos de verão devem ver opções sazonais semelhantes em vez de alternativas fora da estação.
- As políticas de mesclagem de perfis do [!DNL Experience Platform] devem unificar corretamente o comportamento de navegação de vários dispositivos para que a pesquisa realizada em dispositivos móveis seja refletida nas recomendações da área de trabalho.


## Produtos procurados recentemente na página inicial

Exiba cruzeiros, hotéis ou destinos visualizados recentemente na página inicial para lembrar os visitantes de seu interesse e incentivar as visitas de retorno. Os viajantes muitas vezes pesquisam em várias sessões antes da reserva, e descobrir seus interesses anteriores elimina a fricção de iniciar sua pesquisa cada vez que retornam.

### Impacto no negócio

Mostrar produtos de viagem navegados recentemente na página inicial aumenta o envolvimento de visita de retorno, ajudando os clientes a retomar de onde pararam e encurtando o caminho para a reserva.

### Como implementar o

Use o padrão [Personalization de Aplicativo/Web de Visitante Conhecido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md). Essa abordagem usa os dados de perfil armazenados do visitante para renderizar itens visualizados anteriormente na página inicial, criando continuidade entre as sessões de navegação. Esse é o padrão correto quando a personalização depende de dados de perfil persistentes entre sessões e dispositivos em vez de afinidade comportamental em tempo real e quando as regras de relevância são baseadas em tempo (recenticidade) em vez de classificação algorítmica.

### Considerações técnicas

- Os dados visualizados recentemente devem persistir entre dispositivos e sessões que usam a resolução de identidade, para que um cliente que navega em seu telefone veja os mesmos itens quando retorna em um desktop.
- Os itens exibidos devem mostrar o preço atual e o status de disponibilidade, com indicadores claros se uma opção visualizada anteriormente não estiver mais disponível ou se o preço tiver sido alterado desde a última visita.
- A janela de recenticidade dos itens exibidos deve ser ajustada aos ciclos de reserva de viagem; mostrar um cruzeiro visualizado há três meses pode ainda ser relevante, ao contrário de um produto de varejo visualizado há tanto tempo.
- As considerações de privacidade exigem que o conteúdo visualizado recentemente seja vinculado ao status de consentimento do cliente, e uma opção para limpar o histórico de navegação deve ser facilmente acessível.


## Modal de intenção de saída com ofertas direcionadas

Quando um visitante mostrar a intenção de saída, exibir um modal personalizado com ofertas relevantes com base em seu comportamento de navegação durante a sessão. Pegar um visitante que parte com uma oferta atraente e relevante contextualmente fornece uma oportunidade final de converter os juros em uma reserva antes de eles saírem.

### Impacto no negócio

Os modais de intenção de saída com ofertas de viagem personalizadas recuperam conversões significativas entre visitantes que, de outra forma, sairiam sem reserva, capturando receita que seria totalmente perdida.

### Como implementar o

Use o padrão [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). Essa abordagem usa uma lógica de decisão centralizada para avaliar todas as ofertas disponíveis e selecionar a mais relevante para o visitante que está partindo com base no comportamento da sessão e nos dados do perfil. Esse é o padrão correto quando a seleção de oferta deve levar em conta a elegibilidade do nível de fidelidade e as restrições de negócios em torno do limite de frequência, restrições que exigem lógica de decisão controlada em vez de uma recomendação comportamental simples ou uma mensagem acionada única.

### Considerações técnicas

- A detecção de intenção de saída em sites de reserva de viagens deve levar em conta o comportamento de navegação em várias guias, já que os viajantes frequentemente abrem vários itinerários ou propriedades em guias separadas sem realmente pretenderem sair.
- A seleção da oferta deve refletir o que o visitante navegou durante a sessão, apresentando um desconto no destino ou propriedade específica explorada em vez de uma promoção genérica.
- A frequência modal deve ser estritamente limitada para impedir que os visitantes vejam a mesma oferta em cada visita, o que corrói a urgência e a exclusividade percebida da promoção.
- As regras de elegibilidade da oferta do [!DNL Journey Optimizer] devem considerar o nível de fidelidade e o histórico de reserva do visitante para apresentar incentivos com valor adequado, oferecendo aos hóspedes premium benefícios significativos em vez de pequenos descontos.


## Programa de fidelidade Personalization

Personalize a experiência do site, as ofertas e as comunicações com base no nível de fidelidade, no saldo de pontos e no histórico de engajamento do cliente. Os membros da fidelidade que veem seu status refletido em todos os pontos de contato se sentem reconhecidos e valorizados, o que fortalece seu compromisso com a marca e incentiva o avanço do nível.

### Impacto no negócio

A personalização baseada em níveis impulsiona um melhor engajamento dos membros de fidelidade, aprofundando o relacionamento e acelerando os comportamentos de ganho e resgate que sustentam a receita de longo prazo.

### Como implementar o

Use a [Jornada entre canais com o padrão de decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). Essa abordagem combina a orquestração de jornadas com decisões em tempo real para fornecer a oferta certa pelo canal certo para cada membro da fidelidade, adaptando-se ao nível, às preferências e à atividade recente. Esse é o padrão correto quando a jornada deve coordenar a entrega entre canais para evitar ofertas duplicadas e quando a seleção de ofertas exige regras de elegibilidade baseadas em níveis e restrições de resgate — somente a orquestração de jornadas não fornece a camada de decisão de vários canais necessária.

### Considerações técnicas

- Os dados do programa de fidelidade, incluindo status do nível, saldos de pontos e histórico de ganhos, devem ser assimilados e mantidos atualizados para garantir que a personalização e as ofertas do site reflitam a posição real do cliente.
- Benefícios específicos do nível, como acesso antecipado a reservas, atualizações complementares e preços exclusivos, devem ser aplicados no ponto de resgate, exigindo uma integração estreita com os sistemas de reservas e preços.
- As alterações no saldo de pontos de reservas, estadas e transações de parceiros devem acionar o recálculo das regras de personalização em tempo quase real, para que um cliente que ganhou pontos suficientes por uma recompensa veja essa opção imediatamente.
- [!DNL Real-Time Customer Data Platform] públicos-alvo devem ser estruturados em níveis de fidelidade e marcos-chave de engajamento, como aproximar-se do próximo nível ou correr o risco de rebaixamento do nível.


## Lembretes de reserva de vários canais

Envie lembretes de reserva personalizados por email, mensagem de texto e notificações por push aos clientes que iniciaram, mas não concluíram suas reservas. Os viajantes frequentemente começam o processo de reserva e são interrompidos, e chegam até eles através de seus canais preferidos com um lembrete e seus detalhes de viagem salvos os trazem de volta para concluir a reserva.

### Impacto no negócio

Lembretes de reserva multicanal melhoram as taxas de conclusão de reserva, recuperando receita significativa de clientes que pretendiam reservar, mas foram desviados antes de terminar.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Essa abordagem aciona lembretes automaticamente quando um evento de reserva incompleto é detectado, fornecendo mensagens oportunas nos canais preferidos do cliente. Esse é o padrão correto quando o acionador é uma ação discreta do cliente (iniciar uma reserva) e a resposta necessária é uma entrega sensível ao tempo em canais preferenciais, em vez de uma sequência de várias etapas em que cada mensagem depende de alterações anteriores de envolvimento ou disponibilidade.

### Considerações técnicas

- A lógica de seleção de canais deve respeitar as preferências de comunicação do cliente e otimizar o delivery com base em padrões de engajamento anteriores, enviando notificações por push a clientes que respondem bem a dispositivos móveis e emails para aqueles que preferem isso.
- O conteúdo do lembrete deve incluir um deep link que retorna o cliente diretamente para a reserva salva com todas as seleções intactas, eliminando o atrito de inserir novamente as datas de viagem, as preferências de quarto e os detalhes do convidado.
- As regras de tempo e frequência devem coordenar entre canais para evitar sobrecarregar o cliente; um email e uma notificação por push sobre a mesma reserva devem ser espaçados adequadamente, em vez de enviados simultaneamente.
- A integração com o gerenciamento de propriedade ou sistema de reserva central deve verificar se o tipo de quarto, a tarifa e as datas selecionadas originalmente ainda estão disponíveis antes de enviar o lembrete, atualizando a mensagem se a disponibilidade tiver sido alterada.


## Campaign Personalization sazonal

Personalize campanhas e ofertas com base em preferências sazonais, reservas sazonais anteriores e tendências sazonais atuais. Os viajantes são altamente influenciados pelas estações, e campanhas que se alinham com seus interesses sazonais demonstrados e tendências atuais de viagens são muito mais atraentes do que promoções genéricas.

### Impacto no negócio

Campanhas personalizadas sazonais aumentam a conversão de reservas sazonais, garantindo que o investimento em marketing se concentre nos destinos e produtos de viagem com maior probabilidade de repercutir com cada cliente.

### Como implementar o

Use o padrão [Ativação de Mensagem de Saída em Lote](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md). Essa abordagem fornece mensagens de campanha sazonais personalizadas para grandes públicos-alvo de forma programada, segmentando os clientes de acordo com seus padrões e preferências de viagem sazonais. Esse é o padrão correto quando o público-alvo é grande e predefinido pelo histórico de reservas sazonais, o tempo de entrega é agendado com base nas janelas de planejamento sazonais, em vez de ser orientado por eventos, e nenhuma ramificação ou decisão em tempo real é necessária.

### Considerações técnicas

- Os perfis de preferência sazonal do cliente devem ser criados a partir de dados históricos de reserva, identificando padrões como férias de praia de verão consistentes ou viagens de esqui de inverno para informar o direcionamento de campanha.
- A programação da campanha deve levar em conta os prazos de entrega do setor de viagens; as campanhas de férias de verão devem ser lançadas no início da primavera, quando as famílias estiverem planejando, e não em junho, quando a maioria das reservas já estiver sendo feita.
- Os preços e os feeds de disponibilidade para o inventário sazonal devem ser integrados para que as ofertas promovidas reflitam as taxas em tempo real e a disponibilidade real de quartos ou cabines durante os períodos de viagem apresentados.
- [!DNL Experience Platform] públicos-alvo devem combinar dados de preferência sazonais com indicadores de recenticidade para priorizar os clientes que estão em sua janela de planejamento típica para a próxima temporada.


## Recomendações de Reserva de Grupo

Identifique os clientes que reservam com frequência viagens em grupo e recomende proativamente pacotes de grupo, opções familiares ou reservas de vários quartos. As reservas de grupo representam receita significativamente maior por transação, e os clientes com um padrão demonstrado de viagem em grupo respondem bem às opções selecionadas que simplificam o processo de planejamento.

### Impacto no negócio

As recomendações proativas de reserva de grupo aumentam o valor médio de pedido por reserva, capturando o valor total das transações de viagem em grupo que podem ser divididas em várias reservas individuais.

### Como implementar o

Use o padrão [Recomendação Comportamental](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Essa abordagem usa modelos orientados por IA que aprendem com os padrões e o comportamento de reserva do cliente para recomendar as opções de viagem em grupo mais relevantes para cada cliente. Esse é o padrão correto quando o conjunto de itens é grande e está em constante mudança — os pacotes de grupo evoluem com preços e disponibilidade — e a seleção é orientada por padrões comportamentais do histórico de reservas do grupo, em vez de um conjunto limitado de ofertas regido por regras de elegibilidade.

### Considerações técnicas

- A identificação de viagens em grupo requer a análise do histórico de reservas para padrões como reservas de vários quartos, reservas com vários passageiros e reservas coordenadas feitas em conjunto para as mesmas datas e destino.
- Os preços de pacotes em grupo devem ser obtidos dinamicamente do sistema de reservas, já que as taxas em grupo geralmente diferem das taxas individuais e podem exigir tamanhos mínimos de partes ou janelas de reserva antecipada.
- O conteúdo da recomendação deve atender às necessidades exclusivas dos organizadores do grupo, incluindo informações sobre opções de jantar do grupo, espaços de reunião, descontos de reserva em bloco e disponibilidade de excursões em grupo.
- O enriquecimento do perfil do [!DNL Real-Time Customer Data Platform] deve sinalizar os clientes como organizadores de viagens em grupo com base em seus padrões de reserva, permitindo campanhas direcionadas durante os períodos de pico de planejamento de grupos, como a temporada de reunião familiar ou as janelas de retirada corporativa.


## Concierge de reserva de IA

As organizações de viagem e hospitalidade oferecem jornadas de compra complexas e de alta consideração, nas quais os hóspedes devem navegar por voos, quartos, categorias de quartos, serviços auxiliares e benefícios de fidelidade antes de se comprometerem com uma reserva. As interfaces estáticas de navegação e filtro criam fadiga de decisão e aumentam a queda. Um concierge de reserva de IA envolve os hóspedes em conversação natural para entender sua intenção de viagem, tamanho da festa, preferências e orçamento e, em seguida, os orienta passo a passo pelo planejamento de itinerários, seleção de acomodação e opções complementares — tudo isso enquanto encontra benefícios de fidelidade relevantes para o nível do convidado.

### Impacto no negócio

A orientação de reserva conversacional melhora as taxas de conclusão de itinerário e anexos auxiliares, enquanto reduz o volume da central de atendimento para os hóspedes que, de outra forma, telefonariam para esclarecer as opções.

### Como implementar o

Use o padrão [Brand Concierge Conversational Experience](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md). Essa abordagem implanta o Product Advisor Agent em relação ao catálogo de propriedade e itinerário, usando dados de perfil do cliente em tempo real e do AEP Agent Orchestrator para exibir opções personalizadas e recomendações relevantes de fidelidade por meio de uma caixa de diálogo guiada de várias rodadas. Este é o padrão correto quando o objetivo é uma descoberta interativa e conversacional em várias direções, que se baseia em uma decisão de reserva complexa — distinta das mensagens acionadas por eventos, que reagem a ações distintas do viajante com alcance unidirecional, e de experiências personalizadas na Web, que exibem recomendações passivamente sem envolver o convidado no diálogo. Ela requer a configuração do AEP Agent Orchestrator e do controle de marca.

### Considerações técnicas

- Os dados de disponibilidade e taxa devem ser mantidos atualizados por meio da integração em tempo quase real entre o sistema de reservas e a camada de conteúdo do Brand Concierge, já que recomendar tipos de quarto indisponíveis ou preços incorretos em uma conversa reduz imediatamente a confiança.
- A pesquisa de perfil do cliente em tempo real deve mostrar o nível de fidelidade, o histórico de permanência e as preferências declaradas para que o agente possa reconhecer proativamente o status do convidado e adaptar as recomendações sem exigir que o convidado explique novamente suas preferências em cada visita.
- A governança da marca deve definir como o agente processa as consultas de correspondência de classificação, referências de concorrentes e situações em que as datas preferidas dos hóspedes ou o tipo de quarto não estão disponíveis, garantindo que o agente responda normalmente com a voz da marca em vez de apresentar um beco sem saída.
- Os sinais de intenção de conversa — incluindo o interesse de destino, a composição do grupo de viagem e as preferências auxiliares expressas durante o diálogo — devem fluir de volta para o AEP como dados do ExperienceEvent, enriquecendo os perfis de convidados para informar emails downstream, campanhas de fidelidade e reengajamento.
