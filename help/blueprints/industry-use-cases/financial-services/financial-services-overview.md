---
title: Casos de uso de serviços financeiros
description: Descubra como as organizações de serviços financeiros usam o Adobe Experience Platform para personalizar ofertas de produtos, evitar churn e aprofundar os relacionamentos com os clientes.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: 1f22d684-11bd-473d-8b10-5f88cb0cd088
source-git-commit: 0236bd326730ee9a0be621ee0e60ddc3d352410d
workflow-type: tm+mt
source-wordcount: '4039'
ht-degree: 0%

---

# Casos de uso de serviços financeiros

As organizações de serviços financeiros confiam na Adobe Experience Platform para unificar os dados dos clientes em canais bancários, de concessão de empréstimos e de investimento, permitindo experiências personalizadas que fortalecem os relacionamentos e impulsionam o crescimento. Reunindo a atividade da conta, o histórico de transações e os sinais comportamentais, essas organizações podem fornecer a oferta certa no momento certo e, ao mesmo tempo, manter a confiança e a conformidade que seus clientes esperam.

## Fomento De Líderes De Alto Valor

Identifique prospetos de alto valor com base nos dados e no comportamento do perfil, depois nutre-os com conteúdo e ofertas personalizados por meio de jornadas automatizadas. Ao combinar detalhes demográficos, atividade de navegação e sinais de engajamento, as instituições financeiras podem priorizar os leads com maior probabilidade de conversão e orientá-los por um caminho personalizado para se tornarem clientes.

### Impacto no negócio

As organizações que implementam a criação de leads de alto valor observam melhores taxas de conversão de lead para cliente, enquanto criam um pipeline de vendas mais saudável e previsível.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para criar sequências de criação automatizadas que se adaptam com base nos sinais de envolvimento e disponibilidade do cliente potencial. Este é o padrão correto quando o caso de uso requer um fluxo sequenciado de várias mensagens ao longo de dias com ramificação condicional baseada em métricas de engajamento — uma única mensagem acionada não pode acomodar a lógica de criação adaptável ou a lógica de dependência entre as etapas de qualificação.

### Considerações técnicas

- Integre dados de pontuação de clientes potenciais do CRM e eventos comportamentais do site em perfis de prospecto unificados para potencializar a entrada de jornadas e a lógica de ramificação.
- Garanta que as preferências de consentimento e aceitação sejam aplicadas em todos os pontos de contato, especialmente para alcance por telefone e email regido por regulamentos de marketing financeiro.
- Configure a limitação de jornadas para evitar sobrecarregar os clientes potenciais com várias comunicações durante as janelas de avaliação curtas.
- Leve em conta a latência de dados entre as interações da filial ou do supervisor e o envolvimento digital para manter as mensagens de promoção relevantes.


## Recomendação de produto para clientes existentes

Recomendar produtos financeiros relevantes, como cartões de crédito, empréstimos e produtos de investimento, aos clientes existentes com base em seu perfil, histórico de transações e estágio de vida. Esse caso de uso transforma os dados diários da conta em insights acionáveis que mostram o próximo melhor produto para cada cliente.

### Impacto no negócio

As recomendações personalizadas de produtos impulsionam o aumento das taxas de adoção de produtos e aumentam mensuravelmente o valor vitalício do cliente, aprofundando o compartilhamento de carteiras.

### Como implementar o

Use o padrão [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) para avaliar cada cliente em relação às ofertas de produtos elegíveis em tempo real, classificando as recomendações por relevância e prioridade comercial. Esse é o padrão correto quando a seleção de ofertas deve levar em conta as regras de adequação financeira e as restrições de elegibilidade regulatórias — restrições que exigem lógica de decisão controlada em vez de classificação de afinidade comportamental sozinha.

### Considerações técnicas

- Unificar dados de transação, saldos de conta e ativos de produto em um único perfil de cliente para que os modelos de decisão tenham uma visão completa dos relacionamentos existentes.
- Aplicar regras de adequação financeira e restrições de qualificação regulamentar como medidas de proteção rígidas no mecanismo de decisão antes de classificar ofertas.
- Coordene a entrega de ofertas em canais de serviços bancários on-line, aplicativos móveis, email e consultores para evitar recomendações conflitantes ou duplicadas.
- Implemente o limite de frequência por categoria de produto para evitar a fadiga da recomendação, especialmente para produtos altamente considerados, como hipotecas e contas de investimento.


## Campanhas de prevenção de churn

Identifique os clientes em risco de churn usando a previsão de churn alimentada por IA e envolva-os com ofertas de retenção e comunicações personalizadas. A detecção precoce de sinais de desvinculação permite que as instituições financeiras intervenham antes que um cliente feche contas ou mova ativos para outro lugar.

### Impacto no negócio

As iniciativas proativas de prevenção de churn ajudam a reduzir o desgaste do cliente, protegendo fluxos recorrentes de receita e diminuindo o custo de substituição do cliente.

### Como implementar o

Use o padrão [Cross-Channel Jornada com Decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para acionar jornadas de retenção quando as pontuações de risco de churn excederem os limites definidos, com decisão incorporada para selecionar a oferta de retenção mais atraente. Esse é o padrão correto quando a jornada deve coordenar a entrega entre canais para evitar ofertas de retenção duplicadas e quando a seleção de ofertas requer limites de pontuação de risco e restrições de negócios — a orquestração de várias etapas sozinha não fornece a camada de decisão em tempo real necessária para selecionar a oferta de retenção ideal por cliente.

### Considerações técnicas

- Tendências de atividade da conta de feed, histórico de interação de serviço e frequência de envolvimento em [!DNL Customer AI] modelos de propensão de churn para gerar pontuações de risco.
- Defina limites de risco de churn específicos para linhas de produtos, já que os sinais de desvinculação para contas correntes diferem daqueles para portfólios de investimento.
- Analise os critérios de direcionamento e supressão com suas equipes jurídicas e de privacidade para garantir a conformidade com as regulamentações aplicáveis de concessão justa e igualdade de tratamento antes de ativar as ofertas de retenção.
- Crie uma lógica de supressão para excluir clientes que estão com churn devido a fraudes ou ações de conformidade, onde o alcance externo de retenção seria inadequado.


## Painel de conta personalizado

Personalize o painel de banco online e a experiência do aplicativo móvel com base nas atividades, preferências e metas financeiras de cada cliente. Um painel personalizado ajuda os clientes a encontrar o que é mais importante e exibe insights relevantes sem exigir que pesquisem.

### Impacto no negócio

Painéis personalizados aumentam as taxas de engajamento e melhoram significativamente as pontuações de satisfação do cliente, tornando o banco digital intuitivo e relevante.

### Como implementar o

Use o padrão [Personalization de Aplicativo/Web de Visitante Conhecido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) para fornecer blocos de conteúdo personalizados em tempo real, destaques do produto e insights financeiros em experiências digitais autenticadas. Esse é o padrão correto quando a personalização é orientada por atributos de perfil e atividade da conta, em vez de um modelo de afinidade comportamental, e quando a latência em subsegundos é crítica para a experiência do usuário.

### Considerações técnicas

- Aproveite o [!DNL Edge Network] para decisões de personalização em subsegundos em sessões bancárias autenticadas em que a latência afeta diretamente a experiência do usuário.
- Agregue dados de transações em atributos de perfil pré-calculados, como categorias de gastos e tendências de economia, para evitar o cálculo em tempo real de grandes conjuntos de dados.
- Estar em conformidade com os padrões de acessibilidade e garantir que o conteúdo personalizado atenda aos mesmos requisitos de divulgação normativa que o conteúdo estático.
- Coordene a lógica de personalização entre os canais da Web e móveis para que os clientes vejam uma experiência consistente, independentemente do dispositivo.


## Ofertas de produtos baseadas em estágios

Identifique os clientes que entram em novos estágios da vida, como casamento, compra de casa ou aposentadoria e ofereça proativamente produtos e serviços financeiros relevantes. A antecipação desses marcos permite que as instituições se posicionem como parceiros confiáveis durante momentos financeiros essenciais.

### Impacto no negócio

As ofertas acionadas por estágios de vida atingem taxas mais altas de adoção de produtos, superando as campanhas genéricas e fortalecendo os relacionamentos de longo prazo com os clientes.

### Como implementar o

Use o padrão [Cross-Channel Jornada with Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para detectar indicadores de estágio de vida e orquestrar jornadas multitoque com seleção de oferta incorporada personalizada para cada marco. Esse é o padrão correto quando a jornada deve coordenar a entrega entre canais durante momentos financeiros essenciais e quando a seleção da oferta requer verificações de adequação e regras de negócios — a orquestração em várias etapas não fornece, sozinha, a camada de decisão necessária para garantir a conformidade e a relevância.

### Considerações técnicas

- Combine sinais primários, como alterações de endereço, aberturas de conta conjuntas e grandes depósitos com dados de terceiros permitidos para inferir transições de estágio de vida.
- Lidar com eventos de vida confidenciais com cuidado no tom e na frequência das mensagens, já que marcos inferidos incorretamente podem corroer a confiança.
- Verificações de adequação normativa em camadas no Offer Decisioning para que os produtos recomendados se alinhem à situação financeira verificada do cliente.
- Crie períodos de incompatibilidade entre campanhas do estágio de vida útil para evitar sobreposição de alcance geral quando vários indicadores forem acionados em uma janela curta.


## Alertas e recomendações baseados em transações

Envie alertas em tempo real para transações e forneça recomendações personalizadas com base em padrões de gastos e atividade da conta. Notificações relevantes e oportunas mantêm os clientes informados e criam momentos naturais para fornecer orientação financeira útil.

### Impacto no negócio

Os alertas baseados em transações impulsionam um forte engajamento, melhorando o reconhecimento da segurança e criando pontos de contato de alto valor para recomendações personalizadas.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para responder a eventos de transação em tempo real com alertas e recomendações contextualmente relevantes. Esse é o padrão correto quando o acionador é um evento do sistema e não um comportamento do cliente e quando a comunicação necessária é imediata e reativa, em vez de uma sequência de ativação contínua — a latência de alerta afeta diretamente a eficácia da segurança.

### Considerações técnicas

- Assimilar eventos de transação por meio de um pipeline de transmissão com requisitos de entrega de baixa latência, já que os alertas de segurança perderão valor se atrasarem mais do que alguns minutos.
- Aplique preferências e limites de alerta definidos pelo cliente para que as notificações reflitam configurações individuais em vez de regras &quot;tamanho único para todos&quot;.
- Separe os alertas de segurança obrigatórios das mensagens de recomendação opcionais na arquitetura de mensagens para garantir que as notificações de conformidade nunca sejam suprimidas.
- Considere altos volumes de transações durante períodos de pico, como dias úteis e feriados, projetando uma capacidade de throughput que seja dimensionada de acordo com a demanda.


## Recuperação de Abandono de Aplicativo de Cartão de Crédito

Identifique os clientes que iniciaram, mas não concluíram as solicitações de cartão de crédito e envolva-os novamente com mensagens e ofertas personalizadas. O abandono de aplicativo representa um público-alvo de alta intenção que geralmente precisa de apenas um pequeno empurrão para concluir o processo.

### Impacto no negócio

As campanhas de recuperação de abandono melhoram as taxas de conclusão do aplicativo, aumentando diretamente a aquisição de novas contas de um público que já manifestou interesse.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para detectar eventos de abandono de aplicativo e acionar mensagens de acompanhamento pontuais que abordem os motivos comuns de devolução. Esse é o padrão correto quando uma ação distinta do cliente (abandono) é o acionador e a resposta necessária é uma mensagem sensível ao tempo entregue antes que os dados do aplicativo se tornem obsoletos — uma sequência em várias etapas não pode acomodar a urgência e a janela de recuperação limitada.

### Considerações técnicas

- Capture a etapa específica em que o aplicativo foi abandonado para adaptar as mensagens, já que alguém que parou na verificação de identidade precisa de garantias diferentes das de alguém que saiu na análise de termos.
- Trabalhe com suas equipes jurídica e de conformidade para confirmar se todas as comunicações de recuperação atendem aos requisitos de divulgação de marketing de crédito aplicáveis e às regras de consentimento específicas do canal antes da implantação.
- Implemente uma lógica de declínio de tempo para que o alcance de recuperação pare após uma janela definida, já que dados de aplicativos obsoletos podem não ser mais válidos para pré-qualificação.
- Coordene com o sistema de aplicativos para suprimir mensagens de recuperação para candidatos que concluíram por um canal diferente, como uma visita à filial ou uma chamada telefônica.


## Recommendations de investimento do Portfolio

Fornecer recomendações de investimento personalizadas com base no perfil de risco, histórico de investimento e metas financeiras de cada cliente. A orientação de portfólio orientada por dados ajuda os clientes a tomar decisões informadas, enquanto aprofunda o engajamento com os serviços de gerenciamento de patrimônio.

### Impacto no negócio

As recomendações de investimento personalizadas impulsionam uma maior adoção de produtos de investimento e melhoram a diversificação do portfólio em toda a base de clientes.

### Como implementar o

Use o padrão [Recomendação Comportamental](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) para analisar o comportamento e as preferências do investimento e, em seguida, exibir recomendações de portfólio relevantes por meio de canais digitais e ferramentas de supervisão. Este é o padrão correto quando o conjunto de itens (universo de investimento) é grande e a seleção é impulsionada por afinidade comportamental e alinhamento de risco — em vez de um conjunto limitado de ofertas regido por regras de elegibilidade estritas ou apenas por decisões de verificação de adequação.

### Considerações técnicas

- Integre os feeds de dados de corretagem e de custódia para manter uma exibição precisa e atualizada das participações e alocação atuais de cada cliente.
- Aplique requisitos de adequação exigidos pelas normas de valores mobiliários para que as recomendações se alinhem aos objetivos documentados de tolerância a riscos e investimento do cliente.
- Identifique claramente o conteúdo de investimento personalizado como educacional ou informativo, quando necessário, distinguindo-o do aconselhamento formal em matéria de investimento que comporta obrigações fiduciárias.
- Atualize modelos de recomendação regularmente para levar em conta mudanças de mercado, mudança de portfólio e alterações nas metas do cliente.


## Personalization de alerta de fraude

Personalize alertas de fraude e comunicações de segurança com base nas preferências de comunicação de cada cliente e no histórico de interação anterior. Alertas personalizados aumentam a probabilidade de os clientes notarem, compreenderem e agirem em notificações críticas de segurança.

### Impacto no negócio

Os alertas personalizados contra fraudes melhoram as taxas de resposta a alertas, fortalecendo a conformidade com a segurança e reduzindo a janela de exposição durante atividades suspeitas.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para fornecer alertas de fraude através do canal preferido de cada cliente com detalhes contextuais que facilitam a confirmação ou contestação da atividade. Esse é o padrão correto quando o acionador é um evento do sistema e não um comportamento do cliente e quando a comunicação necessária é imediata e reativa sem tempo para sequências de várias etapas — a latência de alerta correlaciona-se diretamente com a exposição a perdas financeiras.

### Considerações técnicas

- Priorize a velocidade e a confiabilidade da entrega acima de todas as outras considerações do projeto, já que a latência de alerta de fraude está diretamente correlacionada à exposição a perdas financeiras.
- Roteie alertas pelo canal preferido verificado do cliente, mantendo canais de fallback para garantir a entrega mesmo que o canal principal falhe.
- Armazene o histórico de interação de alertas para melhorar a relevância futura dos alertas e reduzir a fadiga falso-positiva para clientes que viajam com frequência ou fazem compras atípicas.
- Verifique se todo o conteúdo e os fluxos de trabalho dos alertas de fraude estão em conformidade com as regulamentações de segurança bancária e não exponha detalhes confidenciais da conta em visualizações de mensagens ou linhas de assunto.


## Envolvimento do programa de fidelidade

Personalize comunicações, recompensas e ofertas do programa de fidelidade orquestrando arbitragem de ofertas em tempo real em canais de banco online, aplicativo móvel, email e filial para evitar que ofertas de fidelidade duplicadas ou conflitantes cheguem ao mesmo membro simultaneamente. Regras de elegibilidade baseadas em níveis — que determinam quais recompensas, promoções e opções de resgate cada membro pode acessar — são aplicadas na camada de decisão em vez de serem resolvidas somente por meio da segmentação, garantindo que a seleção da oferta respeite as restrições do programa em cada canal. As jornadas de fidelidade são coordenadas com campanhas de marketing mais amplas para que as ofertas de produto e fidelidade não entrem em conflito, proporcionando aos membros uma experiência coerente em vez de mensagens concorrentes.

### Impacto no negócio

O engajamento de fidelidade personalizado aumenta a participação no programa e impulsiona o resgate de pontos mensuravelmente mais altos, fortalecendo a percepção de valor do programa.

### Como implementar o

Use o padrão [Cross-Channel Jornada com Decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para orquestrar comunicações de fidelidade entre canais, com decisão incorporada para selecionar a recompensa ou oferta mais relevante para cada membro. Esse é o padrão correto quando a jornada deve coordenar a entrega entre canais para evitar a fadiga da mensagem e ofertas conflitantes e quando a seleção da oferta requer regras baseadas em níveis e restrições de membros — a orquestração em várias etapas sozinha não fornece a camada de decisão em tempo real necessária para respeitar as regras de fidelidade e o tratamento diferenciado dos membros.

### Considerações técnicas

- Sincronize dados da plataforma de fidelidade, incluindo status da camada, saldos de pontos e histórico de resgate com os perfis do cliente em tempo quase real, para evitar a promoção de saldos expirados ou imprecisos.
- Segmente a lógica de jornada por nível para fornecer experiências diferenciadas, já que os membros de alto nível esperam tratamento exclusivo e acesso antecipado a promoções.
- Coordene as mensagens de fidelidade com campanhas de marketing mais amplas para evitar a fadiga da mensagem e ofertas conflitantes entre programas.
- Rastreie a atribuição de resgate em canais para medir quais comunicações personalizadas impulsionam o maior retorno sobre o investimento do programa.


## Campanhas de pré-aprovação de hipoteca

Direcione clientes que provavelmente estarão no mercado para uma hipoteca com base em dados de perfil, sinais comportamentais e indicadores de estágio de vida. O alcance pró-ativo da instituição antes da aprovação é uma escolha conveniente durante uma das maiores decisões financeiras que um cliente tomará.

### Impacto no negócio

As campanhas de pré-aprovação de hipotecas direcionadas aumentam as taxas de aplicação e melhoram o volume de concessão de empréstimos, atingindo clientes potenciais qualificados no momento certo.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para orientar os clientes potenciais de hipoteca por meio de uma sequência de criação multitoque, desde a conscientização até a pré-aprovação, adaptando-se com base em sinais de envolvimento e qualificação. Esse é o padrão correto quando o caso de uso requer um fluxo sequenciado de várias mensagens em uma linha do tempo estendida com ramificação condicional baseada em sinais de engajamento e qualificação. Uma única mensagem acionada não pode acomodar a lógica de criação adaptável ou a transferência para processos de aplicativo formais.

### Considerações técnicas

- Combine o comportamento de pesquisa de propriedade, as tendências de crescimento da economia e os sinais de expiração de leasing para criar um modelo de propensão que identifique os prováveis candidatos a hipoteca.
- Garantir que todas as mensagens de pré-aprovação estejam em conformidade com os regulamentos de publicidade de hipotecas, incluindo as divulgações necessárias, a precisão da taxa e o idioma de habitação igualitário.
- Coordenar o momento da campanha com as alterações do ambiente de taxas, de modo que o alcance externo se alinhe às condições favoráveis de empréstimo e evite referências de taxa desatualizadas.
- Crie fluxos de trabalho de entrega para funcionários de financiamento para que os clientes potenciais alimentados digitalmente façam a transição sem problemas para o processo formal de inscrição e subscrição.


## Conteúdo personalizado de educação financeira

Forneça conteúdo, dicas e recursos personalizados de educação financeira com base no perfil financeiro, nas metas e nos interesses de cada cliente. O conteúdo educacional relevante cria confiança, melhora a alfabetização financeira e cria oportunidades orgânicas para introduzir produtos relevantes.

### Impacto no negócio

O conteúdo personalizado de educação aumenta as taxas de envolvimento com o conteúdo e melhora a alfabetização financeira do cliente, o que, por sua vez, leva a uma adoção de produtos mais confiante.

### Como implementar o

Use o padrão [Cross-Channel Jornada with Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para fornecer uma sequência com curadoria de conteúdo educacional em todos os canais, usando a decisão para fazer a correspondência entre os tópicos e a situação financeira e os interesses de cada cliente. Esse é o padrão correto quando a jornada deve coordenar o delivery entre canais com caminhos de aprendizado progressivos e quando a seleção de tópicos requer regras de elegibilidade com base no perfil financeiro — a orquestração de várias etapas sozinha não fornece a camada de decisão necessária para corresponder o conteúdo à situação financeira do cliente ou evitar violações de pré-requisitos.

### Considerações técnicas

- Mapeie o conteúdo educacional para atributos de perfil financeiro, como proporção dívida/renda, taxa de poupança e experiência de investimento, para garantir a relevância do tópico.
- Marque o conteúdo com níveis de dificuldade e tópicos de pré-requisito para criar programações de aprendizado progressivas, em vez de fornecer artigos únicos desconectados.
- Acompanhe o envolvimento de conteúdo no nível do tópico para refinar modelos de personalização e identificar áreas de interesse emergentes na base de clientes.
- Garantir que o conteúdo educacional seja claramente diferenciado do marketing de produtos para manter a conformidade normativa e preservar a confiança do cliente na objetividade do programa.


## Guia do produto financeiro de IA

As organizações de serviços financeiros oferecem portfólios de produtos — contas de verificação e poupança, cartões de crédito, produtos de empréstimo, opções de seguro e veículos de investimento — que são difíceis para os clientes navegarem sem orientação personalizada. As restrições normativas impedem que as experiências digitais de linha de frente forneçam recomendações de investimento personalizadas, mas há um valor substancial em ajudar os clientes a entender como os produtos funcionam, quais contas atendem às suas necessidades declaradas e como dar o próximo passo em direção à aplicação. Um guia de produtos financeiros de IA envolve os clientes em conversas naturais, faz perguntas de qualificação sobre metas financeiras e estágio de vida e os orienta para os produtos certos — sem entrar no território de consultoria regulamentada.

### Impacto no negócio

A detecção conversacional guiada melhora as taxas de início do aplicativo do produto e reduz a queda entre o reconhecimento e o aplicativo, além de capturar sinais de intenção que melhoram os fluxos de trabalho de orientação do supervisor e da criação downstream.

### Como implementar o

Use o padrão [Brand Concierge Conversational Experience](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md). Essa abordagem implanta a Product Advisor Agent em relação à biblioteca de conteúdo de produtos aprovada e à base de conhecimento, usando os dados de perfil do cliente em tempo real e da AEP Agent Orchestrator para orientar os clientes em direção a produtos apropriados por meio de um diálogo de várias rodadas, com base em conteúdo revisado pela conformidade e regido pela marca. Esse é o padrão correto quando o objetivo é uma descoberta interativa e conversacional em várias ocasiões para ajudar os clientes a entender e selecionar produtos financeiros por conta própria — diferente de mensagens acionadas por eventos, que são unidirecionais e respondem a eventos de conta discretos, e de experiências personalizadas na Web, que exibem o conteúdo do produto de forma passiva sem envolver os clientes em um diálogo de qualificação. Ela requer a configuração do AEP Agent Orchestrator e do controle de marca.

### Considerações técnicas

- As medidas de proteção do controle de marca devem ser configuradas com conformidade e revisão legal para definir limites de conteúdo estritos: o agente deve orientar os clientes em direção a produtos adequados com base nas necessidades declaradas sem constituir consultoria de investimento, e os tópicos proibidos (projeções de retorno específicas, garantias, declarações de desempenho comparativas) devem ser explicitamente definidos e aplicados.
- A camada de integração de conteúdo deve estar fundamentada em descrições, divulgações e perguntas frequentes de produtos aprovados por conformidade, em vez de solicitações geradas dinamicamente, garantindo que cada resposta fornecida pelo agente tenha sido analisada por equipes jurídicas e normativas antes da implantação.
- A pesquisa de perfil do cliente em tempo real deve exibir dados de relacionamento — produtos existentes mantidos, mandato da conta e segmento do cliente — para que o agente possa evitar recomendar produtos que o cliente já detém e possa adaptar a orientação para o relacionamento existente do cliente com a instituição.
- A entrega do agente em tempo real deve ser configurada para cenários em que as necessidades do cliente excedam o escopo do guia de conversação — como situações complexas de empréstimo ou solicitações de planejamento financeiro personalizado — com contexto de conversação completo transferido para o consultor de recebimento para evitar que o cliente se repita.


## Adoção de produtos Funnel e análise do driver de churn

Analise onde os clientes caem durante a abertura de contas digitais, o aplicativo de empréstimo ou os fluxos de integração de investimento e identifique os sinais comportamentais que precedem o atrito do produto. As instituições financeiras que não conseguem ver esses pontos de devolução ou precursores de churn não conseguem distinguir entre falhas na experiência do produto e desqualificação, tornando imprecisos os esforços de remediação.

### Impacto no negócio

Entender exatamente onde os candidatos abandonam os fluxos digitais e quais comportamentos precedem os fechamentos de conta permite que as equipes de produto e marketing priorizem melhorias de experiência que reduzem o abandono e estendem o mandato do cliente.

### Como implementar o

Use o padrão [Customer Analytics &amp; Insight Generation](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md). Essa abordagem conecta dados de comportamento digital, registros de CRM e fluxos de eventos de produtos ao Customer Journey Analytics, onde as visualizações de fallout identificam etapas de devolução e superfícies de análise de coorte com diferenças de retenção em linhas de produtos e segmentos de aquisição. Esse é o padrão correto quando o objetivo é entender e diagnosticar — analisar onde as jornadas se quebram e o que causa atrito — em vez de ativar um público-alvo de supressão ou acionar uma mensagem de retenção.

### Considerações técnicas

- Os dados de eventos de aplicativos digitais devem capturar cada etapa do fluxo de integração ou de aplicativos como eventos distintos com identificadores de etapa consistentes, para que a análise de fallout da CJA possa isolar exatamente onde o volume é perdido.
- Os dados de estabilidade do produto do CRM e de status da conta devem ser unidos na conexão do CJA juntamente com dados comportamentais para que a análise de churn possa correlacionar os comportamentos de pré-atrito com os resultados reais de fechamento da conta.
- Os rótulos de governança de dados devem ser aplicados a qualquer campo financeiro ou de identidade confidencial incluído na conexão com o CJA para evitar a exposição às PII em painéis compartilhados acessados por analistas sem permissões de administrador de dados.
- A análise de coorte de retenção requer profundidade suficiente de dados históricos — normalmente de 12 a 24 meses — portanto, as políticas de retenção de conjuntos de dados na AEP devem ser configuradas para preservar o histórico de eventos necessário para comparações de coorte significativas.

## Próxima melhor Offer Decisioning

Use a lógica de decisão centralizada para selecionar a oferta mais relevante para cada cliente em todos os canais, combinando regras de elegibilidade, restrições de negócios e estratégias de classificação alimentadas por IA. A centralização da seleção de ofertas garante que cada cliente receba a oferta de produto financeiro mais contextualmente apropriada, respeitando os requisitos normativos de qualificação e as restrições comerciais.

### Impacto no negócio

As organizações de serviços financeiros que usam o próximo melhor Offer Decisioning centralizado observam melhores taxas de aceitação de produtos e maior receita por interação com o cliente, com o melhor desempenho quando a seleção de ofertas leva em conta as pontuações de propensão e as medidas de proteção de elegibilidade.

### Como implementar o

Use o padrão [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) para criar um mecanismo de decisão centralizado que avalie a qualificação do cliente, aplique restrições de negócios e use a classificação de IA para selecionar a oferta ideal para cada interação do cliente entre canais da Web, de aplicativos e de saída. Esse é o padrão correto quando a seleção de oferta é muito complexa para a personalização baseada em regras isoladamente, exigindo uma combinação de lógica de elegibilidade, regras de prioridade e classificação adaptável para fazer a seleção ideal de um catálogo de ofertas.

### Considerações técnicas

- As regras de elegibilidade da oferta devem ser mantidas no mecanismo de decisão e mantidas em sincronia com os critérios de elegibilidade do produto dos principais sistemas bancários ou de produtos para evitar a exibição de ofertas não qualificadas.
- Os modelos de classificação de IA exigem dados de treinamento suficientes das interações de ofertas anteriores para gerar pontuações de propensão confiáveis; os produtos recém-lançados precisam de estratégias de classificação de fallback até que dados suficientes sejam acumulados.
- Os requisitos normativos em serviços financeiros podem restringir o que pode ser oferecido a quem e por meio de qual canal; a lógica de decisão deve codificar essas restrições como regras rígidas em vez de preferências suaves.
- O rastreamento da fadiga da oferta é importante: os clientes que recebem repetidamente ofertas para o mesmo produto que não aceitaram devem ter essa oferta priorizada ou suprimida após um número definido de exposições.


## Painel do Customer Journey Analytics

Crie espaços de trabalho de análise entre canais combinando dados da Web, do aplicativo, do email e da central de atendimento para visualizar jornadas de clientes, identificar pontos de devolução e medir a atribuição da campanha. Um espaço de trabalho de análise unificada fornece às equipes de produto e marketing uma visão completa de como os clientes se movem entre canais e pontos de contato, permitindo decisões orientadas por dados sobre onde investir no aprimoramento das jornadas.

### Impacto no negócio

As organizações de serviços financeiros com análise de jornada entre canais reduzem o tempo de entrega ao insight para equipes de campanha e produtos, permitindo a identificação mais rápida de oportunidades de otimização de alto impacto em fluxos de integração, funis de aplicativos e jornadas de atendimento ao cliente.

### Como implementar o

Use o padrão [Customer Analytics &amp; Insight Generation](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md) para unir fluxos de eventos de todos os canais digitais e offline em um conjunto de dados de análise unificada e, em seguida, criar visualizações de espaço de trabalho que exponham fluxos de jornada, funnel drop-off e modelos de atribuição. Esse é o padrão correto quando o requisito principal é o insight analítico e a visualização, em vez da ativação em tempo real. Os dados são usados para informar as decisões, em vez de acionar ações voltadas para o cliente.

### Considerações técnicas

- A compilação de dados entre canais requer um identificador de cliente consistente em todos os sistemas de origem; organizações com estratégias de identidade fragmentadas verão jornadas incompletas que prejudicam a análise.
- Os dados de interação offline e da central de atendimento devem ser assimilados e carimbados com precisão de data e hora para colocá-los corretamente na sequência de jornadas em relação aos pontos de contato digitais.
- A latência de dados entre os sistemas de origem e o espaço de trabalho de análise afeta a rapidez com que os insights estão disponíveis; casos de uso de análise de alta frequência podem exigir assimilação quase em tempo real, em vez de feeds de lote diários.
- Os controles de governança de dados e privacidade devem ser aplicados aos conjuntos de dados de análise para impedir que informações de identificação pessoal apareçam em painéis acessíveis a analistas que não devem ter acesso a registros de clientes individuais.
