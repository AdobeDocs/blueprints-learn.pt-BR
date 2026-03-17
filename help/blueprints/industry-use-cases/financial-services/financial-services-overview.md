---
title: Casos de uso de serviços financeiros
description: Descubra como as organizações de serviços financeiros usam o Adobe Experience Platform para personalizar ofertas de produtos, evitar churn e aprofundar os relacionamentos com os clientes.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '2209'
ht-degree: 1%

---


# Casos de uso de serviços financeiros

As organizações de serviços financeiros confiam na Adobe Experience Platform para unificar os dados dos clientes em canais bancários, de concessão de empréstimos e de investimento, permitindo experiências personalizadas que fortalecem os relacionamentos e impulsionam o crescimento. Reunindo a atividade da conta, o histórico de transações e os sinais comportamentais, essas organizações podem fornecer a oferta certa no momento certo e, ao mesmo tempo, manter a confiança e a conformidade que seus clientes esperam.

## Fomento De Líderes De Alto Valor

Identifique prospetos de alto valor com base nos dados e no comportamento do perfil, depois nutre-os com conteúdo e ofertas personalizados por meio de jornadas automatizadas. Ao combinar detalhes demográficos, atividade de navegação e sinais de engajamento, as instituições financeiras podem priorizar os leads com maior probabilidade de conversão e orientá-los por um caminho personalizado para se tornarem clientes.

### Impacto no negócio

As organizações que implementam a criação de leads de alto valor normalmente observam um aumento de 25 a 35% nas taxas de conversão entre lead e cliente, enquanto criam um pipeline de vendas mais saudável e previsível.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para criar sequências de criação automatizadas que se adaptam com base nos sinais de envolvimento e disponibilidade do cliente potencial.

### Considerações técnicas

- Integre dados de pontuação de clientes potenciais do CRM e eventos comportamentais do site em perfis de prospecto unificados para potencializar a entrada de jornadas e a lógica de ramificação.
- Garanta que as preferências de consentimento e aceitação sejam aplicadas em todos os pontos de contato, especialmente para alcance por telefone e email regido por regulamentos de marketing financeiro.
- Configure a limitação de jornadas para evitar sobrecarregar os clientes potenciais com várias comunicações durante as janelas de avaliação curtas.
- Leve em conta a latência de dados entre as interações da filial ou do supervisor e o envolvimento digital para manter as mensagens de promoção relevantes.


## Recomendação de produto para clientes existentes

Recomendar produtos financeiros relevantes, como cartões de crédito, empréstimos e produtos de investimento, aos clientes existentes com base em seu perfil, histórico de transações e estágio de vida. Esse caso de uso transforma os dados diários da conta em insights acionáveis que mostram o próximo melhor produto para cada cliente.

### Impacto no negócio

As recomendações personalizadas de produtos promovem um aumento de 20 a 30% nas taxas de adoção de produtos e aumentam mensuravelmente o valor vitalício do cliente, aprofundando o compartilhamento de carteiras.

### Como implementar o

Use o padrão [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) para avaliar cada cliente em relação às ofertas de produtos elegíveis em tempo real, classificando as recomendações por relevância e prioridade comercial.

### Considerações técnicas

- Unificar dados de transação, saldos de conta e ativos de produto em um único perfil de cliente para que os modelos de decisão tenham uma visão completa dos relacionamentos existentes.
- Aplicar regras de adequação financeira e restrições de qualificação regulamentar como medidas de proteção rígidas no mecanismo de decisão antes de classificar ofertas.
- Coordene a entrega de ofertas em canais de serviços bancários on-line, aplicativos móveis, email e consultores para evitar recomendações conflitantes ou duplicadas.
- Implemente o limite de frequência por categoria de produto para evitar a fadiga da recomendação, especialmente para produtos altamente considerados, como hipotecas e contas de investimento.


## Campanhas de prevenção de churn

Identifique os clientes em risco de churn usando a previsão de churn alimentada por IA e envolva-os com ofertas de retenção e comunicações personalizadas. A detecção precoce de sinais de desvinculação permite que as instituições financeiras intervenham antes que um cliente feche contas ou mova ativos para outro lugar.

### Impacto no negócio

As iniciativas proativas de prevenção de churn geralmente reduzem o desgaste do cliente em 15 a 25%, protegendo fluxos de receita recorrentes e reduzindo o custo de substituição do cliente.

### Como implementar o

Use o padrão [Cross-Channel Jornada com Decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para acionar jornadas de retenção quando as pontuações de risco de churn excederem os limites definidos, com decisão incorporada para selecionar a oferta de retenção mais atraente.

### Considerações técnicas

- Tendências de atividade da conta de feed, histórico de interação de serviço e frequência de envolvimento em [!DNL Customer AI] modelos de propensão de churn para gerar pontuações de risco.
- Defina limites de risco de churn específicos para linhas de produtos, já que os sinais de desvinculação para contas correntes diferem daqueles para portfólios de investimento.
- Garantir que as ofertas de retenção estejam em conformidade com as normas justas de concessão de empréstimos e igualdade de tratamento para que os segmentos de alto risco recebam tratamento equitativo.
- Crie uma lógica de supressão para excluir clientes que estão com churn devido a fraudes ou ações de conformidade, onde o alcance externo de retenção seria inadequado.


## Painel de conta personalizado

Personalize o painel de banco online e a experiência do aplicativo móvel com base nas atividades, preferências e metas financeiras de cada cliente. Um painel personalizado ajuda os clientes a encontrar o que é mais importante e exibe insights relevantes sem exigir que pesquisem.

### Impacto no negócio

Os painéis personalizados aumentam as taxas de engajamento em 30% a 40% e melhoram significativamente as pontuações de satisfação do cliente, tornando o banco digital intuitivo e relevante.

### Como implementar o

Use o padrão [Personalization de Aplicativo/Web de Visitante Conhecido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) para fornecer blocos de conteúdo personalizados em tempo real, destaques do produto e insights financeiros em experiências digitais autenticadas.

### Considerações técnicas

- Aproveite o [!DNL Edge Network] para decisões de personalização em subsegundos em sessões bancárias autenticadas em que a latência afeta diretamente a experiência do usuário.
- Agregue dados de transações em atributos de perfil pré-calculados, como categorias de gastos e tendências de economia, para evitar o cálculo em tempo real de grandes conjuntos de dados.
- Estar em conformidade com os padrões de acessibilidade e garantir que o conteúdo personalizado atenda aos mesmos requisitos de divulgação normativa que o conteúdo estático.
- Coordene a lógica de personalização entre os canais da Web e móveis para que os clientes vejam uma experiência consistente, independentemente do dispositivo.


## Ofertas de produtos baseadas em estágios

Identifique os clientes que entram em novos estágios da vida, como casamento, compra de casa ou aposentadoria e ofereça proativamente produtos e serviços financeiros relevantes. A antecipação desses marcos permite que as instituições se posicionem como parceiros confiáveis durante momentos financeiros essenciais.

### Impacto no negócio

As ofertas acionadas por estágios de vida atingem uma taxa de adoção de produto de 35% a 45%, superando significativamente as campanhas genéricas e fortalecendo os relacionamentos de longo prazo com os clientes.

### Como implementar o

Use o padrão [Cross-Channel Jornada with Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para detectar indicadores de estágio de vida e orquestrar jornadas multitoque com seleção de oferta incorporada personalizada para cada marco.

### Considerações técnicas

- Combine sinais primários, como alterações de endereço, aberturas de conta conjuntas e grandes depósitos com dados de terceiros permitidos para inferir transições de estágio de vida.
- Lidar com eventos de vida confidenciais com cuidado no tom e na frequência das mensagens, já que marcos inferidos incorretamente podem corroer a confiança.
- Verificações de adequação normativa em camadas no Offer Decisioning para que os produtos recomendados se alinhem à situação financeira verificada do cliente.
- Crie períodos de incompatibilidade entre campanhas do estágio de vida útil para evitar sobreposição de alcance geral quando vários indicadores forem acionados em uma janela curta.


## Alertas e recomendações baseados em transações

Envie alertas em tempo real para transações e forneça recomendações personalizadas com base em padrões de gastos e atividade da conta. Notificações relevantes e oportunas mantêm os clientes informados e criam momentos naturais para fornecer orientação financeira útil.

### Impacto no negócio

Os alertas baseados em transações atingem uma taxa de engajamento de 50 a 60%, melhorando drasticamente o reconhecimento da segurança e criando pontos de contato de alto valor para recomendações personalizadas.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para responder a eventos de transação em tempo real com alertas e recomendações contextualmente relevantes.

### Considerações técnicas

- Assimilar eventos de transação por meio de um pipeline de transmissão com requisitos de entrega de baixa latência, já que os alertas de segurança perderão valor se atrasarem mais do que alguns minutos.
- Aplique preferências e limites de alerta definidos pelo cliente para que as notificações reflitam configurações individuais em vez de regras &quot;tamanho único para todos&quot;.
- Separe os alertas de segurança obrigatórios das mensagens de recomendação opcionais na arquitetura de mensagens para garantir que as notificações de conformidade nunca sejam suprimidas.
- Considere altos volumes de transações durante períodos de pico, como dias úteis e feriados, projetando uma capacidade de throughput que seja dimensionada de acordo com a demanda.


## Recuperação de Abandono de Aplicativo de Cartão de Crédito

Identifique os clientes que iniciaram, mas não concluíram as solicitações de cartão de crédito e envolva-os novamente com mensagens e ofertas personalizadas. O abandono de aplicativo representa um público-alvo de alta intenção que geralmente precisa de apenas um pequeno empurrão para concluir o processo.

### Impacto no negócio

As campanhas de recuperação de abandono melhoram as taxas de conclusão de aplicativos em 20% a 30%, aumentando diretamente a aquisição de novas contas de um público que já manifestou interesse.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para detectar eventos de abandono de aplicativo e acionar mensagens de acompanhamento pontuais que abordem os motivos comuns de devolução.

### Considerações técnicas

- Capture a etapa específica em que o aplicativo foi abandonado para adaptar as mensagens, já que alguém que parou na verificação de identidade precisa de garantias diferentes das de alguém que saiu na análise de termos.
- Cumprir as regulamentações de marketing de crédito, incluindo as divulgações necessárias e as regras de empréstimo justas em todas as comunicações de recuperação.
- Implemente uma lógica de declínio de tempo para que o alcance de recuperação pare após uma janela definida, já que dados de aplicativos obsoletos podem não ser mais válidos para pré-qualificação.
- Coordene com o sistema de aplicativos para suprimir mensagens de recuperação para candidatos que concluíram por um canal diferente, como uma visita à filial ou uma chamada telefônica.


## Recommendations de investimento do Portfolio

Fornecer recomendações de investimento personalizadas com base no perfil de risco, histórico de investimento e metas financeiras de cada cliente. A orientação de portfólio orientada por dados ajuda os clientes a tomar decisões informadas, enquanto aprofunda o engajamento com os serviços de gerenciamento de patrimônio.

### Impacto no negócio

As recomendações personalizadas de investimento promovem um aumento de 25 a 35% na adoção de produtos de investimento e melhoram a diversificação do portfólio em toda a base de clientes.

### Como implementar o

Use o padrão [Recomendação Comportamental](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) para analisar o comportamento e as preferências do investimento e, em seguida, exibir recomendações de portfólio relevantes por meio de canais digitais e ferramentas de supervisão.

### Considerações técnicas

- Integre os feeds de dados de corretagem e de custódia para manter uma exibição precisa e atualizada das participações e alocação atuais de cada cliente.
- Aplique requisitos de adequação exigidos pelas normas de valores mobiliários para que as recomendações se alinhem aos objetivos documentados de tolerância a riscos e investimento do cliente.
- Identifique claramente o conteúdo de investimento personalizado como educacional ou informativo, quando necessário, distinguindo-o do aconselhamento formal em matéria de investimento que comporta obrigações fiduciárias.
- Atualize modelos de recomendação regularmente para levar em conta mudanças de mercado, mudança de portfólio e alterações nas metas do cliente.


## Personalization de alerta de fraude

Personalize alertas de fraude e comunicações de segurança com base nas preferências de comunicação de cada cliente e no histórico de interação anterior. Alertas personalizados aumentam a probabilidade de os clientes notarem, compreenderem e agirem em notificações críticas de segurança.

### Impacto no negócio

Os alertas personalizados contra fraudes melhoram as taxas de resposta a alertas em 40 a 50%, reforçando significativamente a conformidade com a segurança e reduzindo a janela de exposição durante atividades suspeitas.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para fornecer alertas de fraude através do canal preferido de cada cliente com detalhes contextuais que facilitam a confirmação ou contestação da atividade.

### Considerações técnicas

- Priorize a velocidade e a confiabilidade da entrega acima de todas as outras considerações do projeto, já que a latência de alerta de fraude está diretamente correlacionada à exposição a perdas financeiras.
- Roteie alertas pelo canal preferido verificado do cliente, mantendo canais de fallback para garantir a entrega mesmo que o canal principal falhe.
- Armazene o histórico de interação de alertas para melhorar a relevância futura dos alertas e reduzir a fadiga falso-positiva para clientes que viajam com frequência ou fazem compras atípicas.
- Verifique se todo o conteúdo e os fluxos de trabalho dos alertas de fraude estão em conformidade com as regulamentações de segurança bancária e não exponha detalhes confidenciais da conta em visualizações de mensagens ou linhas de assunto.


## Envolvimento do programa de fidelidade

Personalize as comunicações, recompensas e ofertas do programa de fidelidade com base no nível de cada cliente, no saldo de pontos e no histórico de resgate. Comunicações de fidelidade relevantes e oportunas mantêm os membros envolvidos e impulsionam uma maior participação no programa.

### Impacto no negócio

O engajamento de fidelidade personalizado aumenta a participação no programa em 30 a 40% e impulsiona o resgate de pontos mensuravelmente mais alto, fortalecendo a percepção de valor do programa.

### Como implementar o

Use o padrão [Cross-Channel Jornada com Decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para orquestrar comunicações de fidelidade entre canais, com decisão incorporada para selecionar a recompensa ou oferta mais relevante para cada membro.

### Considerações técnicas

- Sincronize dados da plataforma de fidelidade, incluindo status da camada, saldos de pontos e histórico de resgate com os perfis do cliente em tempo quase real, para evitar a promoção de saldos expirados ou imprecisos.
- Segmente a lógica de jornada por nível para fornecer experiências diferenciadas, já que os membros de alto nível esperam tratamento exclusivo e acesso antecipado a promoções.
- Coordene as mensagens de fidelidade com campanhas de marketing mais amplas para evitar a fadiga da mensagem e ofertas conflitantes entre programas.
- Rastreie a atribuição de resgate em canais para medir quais comunicações personalizadas impulsionam o maior retorno sobre o investimento do programa.


## Campanhas de pré-aprovação de hipoteca

Direcione clientes que provavelmente estarão no mercado para uma hipoteca com base em dados de perfil, sinais comportamentais e indicadores de estágio de vida. O alcance pró-ativo da instituição antes da aprovação é uma escolha conveniente durante uma das maiores decisões financeiras que um cliente tomará.

### Impacto no negócio

As campanhas de pré-aprovação de hipotecas direcionadas aumentam as taxas de aplicação em 20-30% e melhoram o volume de concessão de empréstimos, alcançando clientes potenciais qualificados no momento certo.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para orientar os clientes potenciais de hipoteca por meio de uma sequência de criação multitoque, desde a conscientização até a pré-aprovação, adaptando-se com base em sinais de envolvimento e qualificação.

### Considerações técnicas

- Combine o comportamento de pesquisa de propriedade, as tendências de crescimento da economia e os sinais de expiração de leasing para criar um modelo de propensão que identifique os prováveis candidatos a hipoteca.
- Garantir que todas as mensagens de pré-aprovação estejam em conformidade com os regulamentos de publicidade de hipotecas, incluindo as divulgações necessárias, a precisão da taxa e o idioma de habitação igualitário.
- Coordenar o momento da campanha com as alterações do ambiente de taxas, de modo que o alcance externo se alinhe às condições favoráveis de empréstimo e evite referências de taxa desatualizadas.
- Crie fluxos de trabalho de entrega para funcionários de financiamento para que os clientes potenciais alimentados digitalmente façam a transição sem problemas para o processo formal de inscrição e subscrição.


## Conteúdo personalizado de educação financeira

Forneça conteúdo, dicas e recursos personalizados de educação financeira com base no perfil financeiro, nas metas e nos interesses de cada cliente. O conteúdo educacional relevante cria confiança, melhora a alfabetização financeira e cria oportunidades orgânicas para introduzir produtos relevantes.

### Impacto no negócio

O conteúdo personalizado de educação aumenta as taxas de engajamento no conteúdo em 25% a 35% e melhora a alfabetização financeira do cliente, o que, por sua vez, leva a uma adoção de produtos mais confiante.

### Como implementar o

Use o padrão [Cross-Channel Jornada with Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para fornecer uma sequência com curadoria de conteúdo educacional em todos os canais, usando a decisão para fazer a correspondência entre os tópicos e a situação financeira e os interesses de cada cliente.

### Considerações técnicas

- Mapeie o conteúdo educacional para atributos de perfil financeiro, como proporção dívida/renda, taxa de poupança e experiência de investimento, para garantir a relevância do tópico.
- Marque o conteúdo com níveis de dificuldade e tópicos de pré-requisito para criar programações de aprendizado progressivas, em vez de fornecer artigos únicos desconectados.
- Acompanhe o envolvimento de conteúdo no nível do tópico para refinar modelos de personalização e identificar áreas de interesse emergentes na base de clientes.
- Garantir que o conteúdo educacional seja claramente diferenciado do marketing de produtos para manter a conformidade normativa e preservar a confiança do cliente na objetividade do programa.
