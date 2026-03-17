---
title: Casos de uso de telecomunicações
description: Descubra como as organizações de telecomunicações usam o Adobe Experience Platform para reduzir churn, impulsionar atualizações de dispositivos e melhorar o engajamento do cliente.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '2295'
ht-degree: 1%

---


# Casos de uso de telecomunicações

As organizações de telecomunicações usam o Adobe Experience Platform para criar uma visualização unificada de cada assinante e fornecer experiências personalizadas que reduzem o churn, aumentam as atualizações de planos e dispositivos e fortalecem os relacionamentos de longo prazo com os clientes. Conectando dados de uso da rede, informações de faturamento e interações com os clientes, os provedores de telecomunicações podem antecipar as necessidades dos assinantes e engajá-los no momento certo por meio de seus canais preferidos.

## Recomendações de atualização do dispositivo

Identifique os clientes qualificados para atualizações de dispositivos e apresente recomendações personalizadas de dispositivos e ofertas de atualização com base em padrões de uso e preferências. Analisando os cronogramas do contrato, a idade do dispositivo e o comportamento individual de navegação, os provedores de telecomunicações podem exibir os dispositivos e as opções de financiamento mais relevantes para cada assinante.

### Impacto no negócio

As organizações que implementam recomendações de atualização de dispositivos geralmente observam um aumento de 30 a 40% nas taxas de conversão de atualização, fornecendo a oferta certa no momento certo pelo canal preferido do cliente.

### Como implementar o

Use o padrão [Cross-Channel Jornada com Decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para orquestrar jornadas de atualização que avaliam a elegibilidade, as preferências de dispositivo e a afinidade de canal de cada assinante, a fim de fornecer ofertas de atualização personalizadas por email, notificações de aplicativos e experiências na loja.

### Considerações técnicas

- Integre o inventário de dispositivos e os sistemas de preços para garantir que as recomendações reflitam a disponibilidade atual e os preços promocionais.
- Conecte os dados de gerenciamento de contratos para identificar com precisão as janelas de qualificação de atualização e as ofertas de atualização antecipadas.
- Incorpore a telemetria de uso do dispositivo (capacidade de armazenamento, integridade da bateria, métricas de desempenho) para fortalecer a relevância da recomendação.
- Coordene com plataformas de varejo e comércio eletrônico para manter uma experiência de atualização consistente em canais digitais e na loja.


## Campanhas de otimização de plano

Analise os padrões de uso do cliente e recomende alterações de plano ideais para economizar dinheiro ou obter melhores recursos com base em suas necessidades reais. Alcançar proativamente o plano de recomendações cria confiança e reduz o risco de os assinantes deixarem os concorrentes com preços mais simples.

### Impacto no negócio

As campanhas de otimização de plano normalmente geram um aumento de 25 a 35% nas taxas de alteração do plano, melhorando a satisfação do cliente e, ao mesmo tempo, aumentando a receita média por usuário quando os assinantes mudam para planos que melhor correspondem ao seu consumo.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para criar uma campanha multitoque que identifique incompatibilidades de uso para planejar, instrua os assinantes sobre as melhores opções e os oriente pelo processo de alteração do plano com acompanhamento em tempo hábil.

### Considerações técnicas

- Assimilar dados de uso em tempo real e históricos (minutos de voz, consumo de dados, chamadas internacionais) para identificar com precisão as incompatibilidades do plano.
- Conecte os dados do sistema de faturamento para calcular a economia potencial ou os ganhos de recursos para cada alteração de plano recomendada.
- Conta para regras de precificação promocional e obrigações de contrato ao gerar recomendações de plano.
- Integre com portais de autoatendimento para que os assinantes possam concluir as alterações do plano diretamente dos pontos de contato da campanha.


## Prevenção de churn para clientes de alto valor

Identifique clientes de alto valor em risco de churn e envolva-os com ofertas de retenção personalizadas e atendimento pró-ativo ao cliente. Ao combinar sinais comportamentais, como uso decrescente, chamadas de serviço repetidas e navegação competitiva com dados de valor vitalício, os provedores podem intervir antes que um assinante decida sair.

### Impacto no negócio

Os programas de prevenção de churn direcionados a assinantes de alto valor normalmente alcançam uma redução de 20 a 30% no churn, protegendo uma receita recorrente significativa e reduzindo o custo de aquisição de clientes substitutos.

### Como implementar o

Use o padrão [Cross-Channel Jornada with Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para monitorar sinais de risco de churn em tempo real, determinar a melhor oferta de retenção para cada assinante e orquestrar alcance personalizado em canais digitais e na central de atendimento.

### Considerações técnicas

- Crie pontuações de propensão de churn combinando tendências de uso, histórico de interação de serviços e dados de sentimentos das transcrições da central de atendimento.
- Integre sistemas de call center e varejo para que os agentes tenham visibilidade das ofertas de retenção já apresentadas por meio de canais digitais.
- Conecte dados de inteligência competitiva (solicitações de exclusão, comparações de planos de concorrentes) para refinar a pontuação de riscos e oferecer estratégias.
- Estabeleça regras de governança para evitar o excesso de contatos com assinantes em risco, o que pode acelerar o churn em vez de impedi-lo.


## Jornada de integração de novo cliente

Automatize uma jornada de integração personalizada para novos clientes com informações de boas-vindas, orientação de configuração de conta e tutoriais de recursos. Uma experiência de integração estruturada ajuda os assinantes a descobrir rapidamente o valor total de seus planos e serviços, definindo a base para a retenção a longo prazo.

### Impacto no negócio

As jornadas de integração bem projetadas normalmente aumentam as taxas de ativação de recursos em 50 a 60%, resultando em pontuações de satisfação mais altas e menor churn antecipado entre os novos assinantes.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para criar uma experiência de integração sequenciada que se adapte com base no tipo de plano, no dispositivo e no envolvimento de cada assinante com as etapas de integração anteriores.

### Considerações técnicas

- Integre sistemas de provisionamento de conta para acionar a jornada de integração imediatamente após a ativação e personalize o conteúdo para o plano e o dispositivo específicos do assinante.
- Conecte os dados de engajamento do aplicativo para rastrear quais recursos o assinante explorou e ajuste as mensagens de integração subsequentes de acordo.
- Coordene com a plataforma de suporte ao cliente para garantir que os agentes estejam cientes do estágio de integração de um assinante se entrarem em contato com para fazer perguntas.
- Suporte a vários caminhos de integração para diferentes segmentos de clientes, como assinantes individuais, administradores de planos de família e contas de negócios.


## Alertas e recomendações de uso de dados

Envie alertas personalizados quando os clientes se aproximarem dos limites de dados e recomendar atualizações de plano ou complementos de dados com base em padrões de uso. Notificações úteis e oportunas transformam uma experiência potencialmente frustrante em um momento de envolvimento de criação de confiança.

### Impacto no negócio

Os alertas proativos de uso de dados geralmente geram um aumento de 40 a 50% nas compras de complementos de dados, além de reduzir as reclamações de impacto nas contas e melhorar a satisfação geral do cliente.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para enviar alertas em tempo real quando os limites de uso forem ultrapassados, com recomendações personalizadas com base nos padrões de consumo histórico e detalhes do plano do assinante.

### Considerações técnicas

- Conecte-se a feeds de dados de uso da rede que fornecem atualizações de consumo quase em tempo real para acionar alertas em limites significativos (75%, 90%, 100% dos limites do plano).
- Integre sistemas de gerenciamento de plano e cobrança para apresentar preços complementares precisos e permitir compras com um toque diretamente da mensagem de alerta.
- Conta para pools de dados compartilhados em planos familiares, alertando o usuário individual e o administrador do plano.
- Implemente o limite de frequência para evitar fadiga de alerta para assinantes que usam consistentemente quantidades altas de dados a cada ciclo de faturamento.


## Notificações de interrupção de serviço

Notifique proativamente os clientes sobre interrupções do serviço, manutenção ou problemas de rede em sua área com atualizações personalizadas e ofertas de compensação. Alcançar a frustração dos clientes demonstra responsabilidade e reduz significativamente o volume de suporte de entrada.

### Impacto no negócio

As notificações de interrupção proativa geralmente atingem uma taxa de confirmação de notificação de 60 a 70% e reduzem substancialmente o volume da central de atendimento durante interrupções do serviço, reduzindo os custos de suporte e, ao mesmo tempo, melhorando a percepção do cliente.

### Como implementar o

Use o padrão [Mensagens Acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para detectar eventos de rede e notificar imediatamente os assinantes afetados por meio de seus canais preferidos com detalhes relevantes, tempos de resolução estimados e remuneração apropriada, quando garantido.

### Considerações técnicas

- Integre-se aos sistemas de monitoramento do centro de operações de rede para receber dados de eventos de interrupção e manutenção em tempo real com informações geográficas de escopo.
- Use o endereço do assinante e os dados de localização para identificar com precisão os clientes afetados e evitar notificar aqueles fora da área afetada.
- Conecte-se ao sistema de faturamento e créditos para automatizar ofertas de crédito de serviço para interrupções estendidas com base no plano do assinante e na duração da interrupção.
- Coordene as mensagens entre canais para fornecer atualizações de status consistentes e evitar o envio de informações conflitantes conforme a situação evolui.


## Gerenciamento de Planos Familiares

Personalize comunicações e ofertas para administradores de planos de família com base em padrões de uso de família e necessidades individuais de membros. Os planos da família representam contas de várias linhas e de alto valor, nas quais o engajamento com o administrador do plano orienta a retenção em todas as linhas.

### Impacto no negócio

As comunicações personalizadas de gerenciamento de planos familiares geralmente aumentam o envolvimento com planos familiares em 30 a 40%, resultando em maior retenção de linha e maior valor vitalício por conta.

### Como implementar o

Use o padrão [Cross-Channel Jornada with Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para analisar o uso em todos os membros da família, identificar oportunidades como a adição de linhas ou o ajuste de limites individuais e fornecer recomendações personalizadas ao administrador do plano.

### Considerações técnicas

- Hierarquias de conta da família de modelos para distinguir entre o administrador do plano e os membros individuais, respeitando os níveis de permissão para comunicações e alterações de conta.
- Agregue dados de uso em todas as linhas na conta para identificar padrões e oportunidades no nível da família, como dados compartilhados subutilizados ou ciclos desiguais de atualização de dispositivos.
- Integre o controle dos pais e os sistemas de filtragem de conteúdo para oferecer suporte a recursos específicos da família na personalização.
- Verifique se os controles de privacidade estão em vigor para que os detalhes de uso de membros individuais sejam compartilhados adequadamente com o administrador do plano com base nas permissões da conta.


## Campanhas de atualização 5G

Clientes-alvo qualificados para atualizações de rede 5G com ofertas e benefícios personalizados com base em sua localização e padrões de uso. À medida que a cobertura 5G se expande, chegar aos assinantes em áreas recém-cobertas com mensagens relevantes acelera a adoção e aumenta a utilização da rede.

### Impacto no negócio

As campanhas de atualização 5G direcionadas geralmente geram um aumento de 25 a 35% nas taxas de adoção 5G entre os assinantes elegíveis, apoiando o retorno do investimento em rede e a diferenciação competitiva.

### Como implementar o

Use o padrão [Ativação de Mensagem de Saída em Lote](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md) para segmentar os assinantes com base na disponibilidade de cobertura 5G, na compatibilidade de dispositivos e na qualificação de planos. Em seguida, forneça campanhas de atualização personalizadas destacando os benefícios mais relevantes para o perfil de uso de cada assinante.

### Considerações técnicas

- Integrar mapas de cobertura de rede para identificar com precisão os assinantes em áreas com serviço 5G ativo e evitar a promoção de atualizações em que a cobertura ainda não está disponível.
- Conecte dados de compatibilidade de dispositivo para determinar quais assinantes precisam de um novo dispositivo em comparação com aqueles que já têm hardware compatível com 5G.
- Coordene com os sistemas de inventário de varejo para garantir que os dispositivos e planos promovidos estejam disponíveis na loja preferencial do assinante ou online.
- Segmente as mensagens por perfil de uso para que os usuários de dados pesados recebam benefícios focados no desempenho, enquanto os usuários casuais recebem mensagens de cobertura e confiabilidade.


## Lembretes de pagamento de contas

Envie lembretes personalizados sobre pagamento de contas por meio de canais preferenciais com opções de pagamento e informações sobre saldo da conta. Lembretes oportunos e convenientes reduzem os atrasos de pagamento e os custos de cobrança associados, mantendo o relacionamento com o cliente positivo.

### Impacto no negócio

Os lembretes de pagamento de contas personalizados geralmente melhoram as taxas de pagamento no prazo em 20-30%, reduzindo as despesas de cobrança e minimizando as suspensões de serviço que geram insatisfação do cliente.

### Como implementar o

Use o padrão [Mensagens Acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para enviar lembretes em momentos ideais antes da data de vencimento, personalizados com o saldo do assinante, o método de pagamento preferido e um link direto para concluir o pagamento.

### Considerações técnicas

- Integre com a plataforma de faturamento para acessar saldos de conta em tempo real, datas de vencimento e histórico de pagamento para obter conteúdo preciso de lembrete.
- Conecte-se a sistemas de processamento de pagamento para permitir o pagamento com um toque ou um clique diretamente da mensagem de lembrete.
- Implemente a lógica de escalonamento que ajusta a urgência e a frequência dos lembretes conforme a data de vencimento se aproxima, respeitando as preferências de comunicação.
- Ofereça suporte a vários métodos de pagamento (inscrição de pagamento automático, carteira digital, transferência bancária) e personalize as opções apresentadas com base no histórico do assinante.


## Recomendações do serviço complementar

Recomendar serviços complementares relevantes, como seguro de dispositivo, armazenamento em nuvem e pacotes de transmissão, com base no plano, no uso e nas preferências do cliente. As recomendações contextuais aumentam o valor que os assinantes recebem por sua relação com o provedor, enquanto aumentam a receita média por usuário.

### Impacto no negócio

As recomendações personalizadas de serviços complementares geralmente geram um aumento de 15 a 25% nas taxas de adoção de complementos, expandindo a receita da base de assinantes existente sem o custo da aquisição de novos clientes.

### Como implementar o

Use o padrão [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) para avaliar o perfil, os serviços atuais e os sinais comportamentais de cada assinante para determinar a oferta complementar mais relevante e apresentá-la pelo canal e momento ideais.

### Considerações técnicas

- Conecte-se ao catálogo de serviços atual do assinante para evitar a recomendação de serviços que já têm e para identificar complementos naturais ao plano existente.
- Integre dados de serviços de parceiros e de terceiros (provedores de transmissão contínua, operadoras de seguros) para apresentar preços precisos e ofertas agrupadas.
- Use dados de dispositivo e uso para informar as recomendações, como sugerir seguro de dispositivo para assinantes com novos dispositivos premium ou armazenamento em nuvem para aqueles que estão executando menos armazenamento no dispositivo.
- Coordene com a personalização no aplicativo e na Web para reforçar as recomendações complementares nos pontos de contato de autoatendimento.


## Personalization de desempenho de rede

Personalize as informações e recomendações de desempenho da rede com base no local, dispositivo e padrões de uso do cliente. Ajudar os assinantes a otimizar sua experiência de conectividade cria confiança e reduz os contatos de suporte associados a problemas de desempenho.

### Impacto no negócio

As experiências personalizadas de desempenho da rede normalmente aumentam o envolvimento do aplicativo em 35% a 45%, à medida que os assinantes retornam para verificar a cobertura, solucionar problemas e descobrir dicas de otimização adaptadas à sua situação.

### Como implementar o

Use o padrão [Personalization de Aplicativo/Web de Visitante Conhecido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) para fornecer painéis personalizados de desempenho de rede, informações de cobertura e recomendações de otimização no aplicativo do assinante e na experiência da conta da Web.

### Considerações técnicas

- Integre métricas de qualidade da rede e dados de cobertura para fornecer informações de desempenho específicas do local relevantes para a casa, o trabalho e as áreas visitadas com frequência do assinante.
- Conecte dados de diagnóstico do dispositivo para oferecer recomendações de solução de problemas personalizadas com base no modelo do dispositivo específico do assinante e na versão do software.
- Use os serviços de borda do [!DNL Adobe Experience Platform] para fornecer personalização de baixa latência dentro da experiência do aplicativo sem afetar o desempenho.
- Implemente loops de feedback para que os assinantes possam relatar problemas de cobertura, enriquecendo os dados da rede e demonstrando a capacidade de resposta à sua experiência.


## Envolvimento do programa de fidelidade

Personalize comunicações, recompensas e ofertas do programa de fidelidade com base no nível do cliente, no saldo de pontos e no histórico de resgate. Uma experiência de fidelidade bem personalizada fortalece a conexão emocional com a marca e cria custos de mudança significativos além dos termos do contrato.

### Impacto no negócio

O engajamento personalizado no programa de fidelidade normalmente aumenta a participação no programa e o resgate de prêmios em 30% a 40%, gerando taxas de retenção mais altas entre os assinantes inscritos.

### Como implementar o

Use o padrão [Jornada entre canais com decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para orquestrar comunicações de fidelidade personalizadas que destaquem recompensas relevantes, notifiquem os assinantes sobre o progresso do nível e apresentem oportunidades de resgate alinhadas com suas preferências e comportamentos.

### Considerações técnicas

- Integre a plataforma de fidelidade para acessar saldos de pontos em tempo real, status da camada e histórico de resgate para uma personalização precisa.
- Conecte os catálogos de premiação do parceiro para apresentar uma ampla variedade de opções de resgate personalizadas para os interesses demonstrados de cada assinante e resgates anteriores.
- Coordene as mensagens de fidelidade com outras jornadas do Campaign para garantir que as ofertas de retenção e as recompensas de fidelidade se complementem em vez de entrar em conflito entre si.
- Ofereça suporte aos empurrões de progressão de nível calculando a proximidade de um assinante com o próximo nível e apresentando etapas acionáveis para atingi-lo.
