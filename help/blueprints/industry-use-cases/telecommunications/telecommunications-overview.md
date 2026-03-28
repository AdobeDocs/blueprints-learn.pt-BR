---
title: Casos de uso de telecomunicações
description: Descubra como as organizações de telecomunicações usam o Adobe Experience Platform para reduzir churn, impulsionar atualizações de dispositivos e melhorar o engajamento do cliente.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: 653632f0-81be-435c-a703-56c5bc132794
source-git-commit: 3542d76106fada9019b70a8cc9fd4c74872d4995
workflow-type: tm+mt
source-wordcount: '3533'
ht-degree: 0%

---

# Casos de uso de telecomunicações

As organizações de telecomunicações usam o Adobe Experience Platform para criar uma visualização unificada de cada assinante e fornecer experiências personalizadas que reduzem o churn, aumentam as atualizações de planos e dispositivos e fortalecem os relacionamentos de longo prazo com os clientes. Conectando dados de uso da rede, informações de faturamento e interações com os clientes, os provedores de telecomunicações podem antecipar as necessidades dos assinantes e engajá-los no momento certo por meio de seus canais preferidos.

## Recomendações de atualização do dispositivo

Identifique os clientes qualificados para atualizações de dispositivos e apresente recomendações personalizadas de dispositivos e ofertas de atualização com base em padrões de uso e preferências. Analisando os cronogramas do contrato, a idade do dispositivo e o comportamento individual de navegação, os provedores de telecomunicações podem exibir os dispositivos e as opções de financiamento mais relevantes para cada assinante.

### Impacto no negócio

As organizações que implementam recomendações de atualização de dispositivos veem taxas de conversão de atualização aprimoradas, fornecendo a oferta certa no momento certo pelo canal preferido do cliente.

### Como implementar o

Use o padrão [Cross-Channel Jornada com Decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para orquestrar jornadas de atualização que avaliam a elegibilidade, as preferências de dispositivo e a afinidade de canal de cada assinante, a fim de fornecer ofertas de atualização personalizadas por email, notificações de aplicativos e experiências na loja. Esse é o padrão correto quando a seleção da oferta deve levar em conta as janelas de qualificação de dispositivo, as preferências de canal e as restrições do inventário — restrições que exigem lógica de decisão controlada em vez de recomendações comportamentais simples sozinhas.

### Considerações técnicas

- Integre o inventário de dispositivos e os sistemas de preços para garantir que as recomendações reflitam a disponibilidade atual e os preços promocionais.
- Conecte os dados de gerenciamento de contratos para identificar com precisão as janelas de qualificação de atualização e as ofertas de atualização antecipadas.
- Incorpore a telemetria de uso do dispositivo (capacidade de armazenamento, integridade da bateria, métricas de desempenho) para fortalecer a relevância da recomendação.
- Coordene com plataformas de varejo e comércio eletrônico para manter uma experiência de atualização consistente em canais digitais e na loja.


## Campanhas de otimização de plano

Analise os padrões de uso do cliente e recomende alterações de plano ideais para economizar dinheiro ou obter melhores recursos com base em suas necessidades reais. Alcançar proativamente o plano de recomendações cria confiança e reduz o risco de os assinantes deixarem os concorrentes com preços mais simples.

### Impacto no negócio

As campanhas de otimização de plano geram taxas de alteração de plano aprimoradas, melhorando a satisfação do cliente e, ao mesmo tempo, aumentando a receita média por usuário quando os assinantes mudam para planos que melhor correspondem ao seu consumo.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para criar uma campanha multitoque que identifique incompatibilidades de uso para planejar, instrua os assinantes sobre as melhores opções e os oriente pelo processo de alteração do plano com acompanhamento em tempo hábil. Esse é o padrão correto quando o caso de uso exige um fluxo sequenciado de várias mensagens ao longo de dias com ramificação condicional baseada no engajamento do assinante e na adoção do plano — uma única mensagem acionada não pode acomodar a jornada educacional e a lógica de dependência entre as etapas de educação e conversão.

### Considerações técnicas

- Assimilar dados de uso em tempo real e históricos (minutos de voz, consumo de dados, chamadas internacionais) para identificar com precisão as incompatibilidades do plano.
- Conecte os dados do sistema de faturamento para calcular a economia potencial ou os ganhos de recursos para cada alteração de plano recomendada.
- Conta para regras de precificação promocional e obrigações de contrato ao gerar recomendações de plano.
- Integre com portais de autoatendimento para que os assinantes possam concluir as alterações do plano diretamente dos pontos de contato da campanha.


## Prevenção de churn para clientes de alto valor

Identifique clientes de alto valor em risco de churn e envolva-os com ofertas de retenção personalizadas e atendimento pró-ativo ao cliente. Ao combinar sinais comportamentais, como uso decrescente, chamadas de serviço repetidas e navegação competitiva com dados de valor vitalício, os provedores podem intervir antes que um assinante decida sair.

### Impacto no negócio

Os programas de prevenção de churn direcionados a assinantes de alto valor alcançam reduções significativas no churn, protegendo a receita recorrente significativa e reduzindo o custo de aquisição de clientes de substituição.

### Como implementar o

Use o padrão [Cross-Channel Jornada with Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para monitorar sinais de risco de churn em tempo real, determinar a melhor oferta de retenção para cada assinante e orquestrar alcance personalizado em canais digitais e na central de atendimento. Esse é o padrão correto quando a jornada deve coordenar a entrega em canais digitais e assistidos por agente para evitar ofertas de retenção duplicadas e quando a seleção de ofertas requer pontuação de riscos e restrições de negócios — a orquestração de várias etapas sozinha não fornece a camada de decisão em tempo real ou a coordenação de agente necessária.

### Considerações técnicas

- Crie pontuações de propensão de churn combinando tendências de uso, histórico de interação de serviços e dados de sentimentos das transcrições da central de atendimento.
- Integre sistemas de call center e varejo para que os agentes tenham visibilidade das ofertas de retenção já apresentadas por meio de canais digitais.
- Conecte dados de inteligência competitiva (solicitações de exclusão, comparações de planos de concorrentes) para refinar a pontuação de riscos e oferecer estratégias.
- Estabeleça regras de governança para evitar o excesso de contatos com assinantes em risco, o que pode acelerar o churn em vez de impedi-lo.


## Jornada de integração de novo cliente

Automatize uma jornada de integração personalizada para novos clientes com informações de boas-vindas, orientação de configuração de conta e tutoriais de recursos. Uma experiência de integração estruturada ajuda os assinantes a descobrir rapidamente o valor total de seus planos e serviços, definindo a base para a retenção a longo prazo.

### Impacto no negócio

As jornadas de integração bem projetadas impulsionam taxas de ativação de recursos aprimoradas, resultando em pontuações de satisfação mais altas e menor rotatividade no início da vida útil entre os novos assinantes.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para criar uma experiência de integração sequenciada que se adapte com base no tipo de plano, no dispositivo e no envolvimento de cada assinante com as etapas de integração anteriores. Esse é o padrão correto quando o caso de uso requer um fluxo sequenciado de várias mensagens ao longo de dias com ramificação condicional baseada na descoberta e no engajamento de recursos — uma única mensagem acionada não pode acomodar a lógica de dependência adaptável entre as etapas de integração com base no plano do assinante e no tipo de dispositivo.

### Considerações técnicas

- Integre sistemas de provisionamento de conta para acionar a jornada de integração imediatamente após a ativação e personalize o conteúdo para o plano e o dispositivo específicos do assinante.
- Conecte os dados de engajamento do aplicativo para rastrear quais recursos o assinante explorou e ajuste as mensagens de integração subsequentes de acordo.
- Coordene com a plataforma de suporte ao cliente para garantir que os agentes estejam cientes do estágio de integração de um assinante se entrarem em contato com para fazer perguntas.
- Suporte a vários caminhos de integração para diferentes segmentos de clientes, como assinantes individuais, administradores de planos de família e contas de negócios.


## Alertas e recomendações de uso de dados

Envie alertas personalizados quando os clientes se aproximarem dos limites de dados e recomendar atualizações de plano ou complementos de dados com base em padrões de uso. Notificações úteis e oportunas transformam uma experiência potencialmente frustrante em um momento de envolvimento de criação de confiança.

### Impacto no negócio

Os alertas proativos de uso de dados impulsionam compras aprimoradas de complementos de dados, além de reduzir as reclamações de choque na fatura e melhorar a satisfação geral do cliente.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para enviar alertas em tempo real quando os limites de uso forem ultrapassados, com recomendações personalizadas com base nos padrões de consumo histórico e detalhes do plano do assinante. Esse é o padrão correto quando o acionador é um evento do sistema (ultrapassagem de limite de uso) em vez do comportamento do cliente, e a comunicação necessária é imediata e reativa em vez de uma sequência de criação contínua.

### Considerações técnicas

- Conecte-se a feeds de dados de uso da rede que fornecem atualizações de consumo quase em tempo real para acionar alertas em limites significativos (75%, 90%, 100% dos limites do plano).
- Integre sistemas de gerenciamento de plano e cobrança para apresentar preços complementares precisos e permitir compras com um toque diretamente da mensagem de alerta.
- Conta para pools de dados compartilhados em planos familiares, alertando o usuário individual e o administrador do plano.
- Implemente o limite de frequência para evitar fadiga de alerta para assinantes que usam consistentemente quantidades altas de dados a cada ciclo de faturamento.


## Notificações de interrupção de serviço

Notifique proativamente os clientes sobre interrupções do serviço, manutenção ou problemas de rede em sua área com atualizações personalizadas e ofertas de compensação. Alcançar a frustração dos clientes demonstra responsabilidade e reduz significativamente o volume de suporte de entrada.

### Impacto no negócio

As notificações de interrupção proativa atingem altas taxas de reconhecimento de notificação e reduzem substancialmente o volume da central de atendimento durante interrupções do serviço, reduzindo os custos de suporte e, ao mesmo tempo, melhorando a percepção do cliente.

### Como implementar o

Use o padrão [Mensagens Acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para detectar eventos de rede e notificar imediatamente os assinantes afetados por meio de seus canais preferidos com detalhes relevantes, tempos de resolução estimados e remuneração apropriada, quando garantido. Esse é o padrão correto quando o acionador é um evento do sistema (interrupção da rede) em vez do comportamento do cliente, e a comunicação necessária é imediata e reativa, em vez de uma sequência sustentada de criação.

### Considerações técnicas

- Integre-se aos sistemas de monitoramento do centro de operações de rede para receber dados de eventos de interrupção e manutenção em tempo real com informações geográficas de escopo.
- Use o endereço do assinante e os dados de localização para identificar com precisão os clientes afetados e evitar notificar aqueles fora da área afetada.
- Conecte-se ao sistema de faturamento e créditos para automatizar ofertas de crédito de serviço para interrupções estendidas com base no plano do assinante e na duração da interrupção.
- Coordene as mensagens entre canais para fornecer atualizações de status consistentes e evitar o envio de informações conflitantes conforme a situação evolui.


## Gerenciamento de Planos Familiares

Personalize comunicações e ofertas para administradores de planos de família com base em padrões de uso de família e necessidades individuais de membros. Os planos da família representam contas de várias linhas e de alto valor, nas quais o engajamento com o administrador do plano orienta a retenção em todas as linhas.

### Impacto no negócio

As comunicações personalizadas de gerenciamento de planos familiares geram um envolvimento aprimorado de planos familiares, resultando em maior retenção de linha e maior valor vitalício por conta.

### Como implementar o

Use o padrão [Cross-Channel Jornada with Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para analisar o uso em todos os membros da família, identificar oportunidades como a adição de linhas ou o ajuste de limites individuais e fornecer recomendações personalizadas ao administrador do plano. Esse é o padrão correto quando a seleção de ofertas deve levar em conta as permissões de hierarquia da família, a agregação de uso de vários membros e as restrições de privacidade, restrições que exigem lógica de decisão controlada em vez de recomendações de assinantes individuais.

### Considerações técnicas

- Hierarquias de conta da família de modelos para distinguir entre o administrador do plano e os membros individuais, respeitando os níveis de permissão para comunicações e alterações de conta.
- Agregue dados de uso em todas as linhas na conta para identificar padrões e oportunidades no nível da família, como dados compartilhados subutilizados ou ciclos desiguais de atualização de dispositivos.
- Integre o controle dos pais e os sistemas de filtragem de conteúdo para oferecer suporte a recursos específicos da família na personalização.
- Verifique se os controles de privacidade estão em vigor para que os detalhes de uso de membros individuais sejam compartilhados adequadamente com o administrador do plano com base nas permissões da conta.


## Campanhas de atualização 5G

Clientes-alvo qualificados para atualizações de rede 5G com ofertas e benefícios personalizados com base em sua localização e padrões de uso. À medida que a cobertura 5G se expande, chegar aos assinantes em áreas recém-cobertas com mensagens relevantes acelera a adoção e aumenta a utilização da rede.

### Impacto no negócio

As campanhas de atualização 5G direcionadas impulsionam melhores taxas de adoção 5G entre os assinantes elegíveis, apoiando o retorno do investimento em rede e a diferenciação competitiva.

### Como implementar o

Use o padrão [Ativação de Mensagem de Saída em Lote](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md) para segmentar os assinantes com base na disponibilidade de cobertura 5G, na compatibilidade de dispositivos e na qualificação de planos. Em seguida, forneça campanhas de atualização personalizadas destacando os benefícios mais relevantes para o perfil de uso de cada assinante. Esse é o padrão correto quando o público-alvo é predefinido e grande, o tempo de entrega é agendado em vez de ser orientado por eventos, e nenhuma ramificação ou decisão em tempo real é necessária — a campanha pode ser totalmente planejada com antecedência, com base nos cronogramas de implementação da cobertura.

### Considerações técnicas

- Integrar mapas de cobertura de rede para identificar com precisão os assinantes em áreas com serviço 5G ativo e evitar a promoção de atualizações em que a cobertura ainda não está disponível.
- Conecte dados de compatibilidade de dispositivo para determinar quais assinantes precisam de um novo dispositivo em comparação com aqueles que já têm hardware compatível com 5G.
- Coordene com os sistemas de inventário de varejo para garantir que os dispositivos e planos promovidos estejam disponíveis na loja preferencial do assinante ou online.
- Segmente as mensagens por perfil de uso para que os usuários de dados pesados recebam benefícios focados no desempenho, enquanto os usuários casuais recebem mensagens de cobertura e confiabilidade.


## Lembretes de pagamento de contas

Envie lembretes personalizados sobre pagamento de contas por meio de canais preferenciais com opções de pagamento e informações sobre saldo da conta. Lembretes oportunos e convenientes reduzem os atrasos de pagamento e os custos de cobrança associados, mantendo o relacionamento com o cliente positivo.

### Impacto no negócio

Os lembretes de pagamento de contas personalizados melhoram as taxas de pagamento no prazo, reduzindo as despesas de cobrança e minimizando as suspensões de serviço que geram insatisfação do cliente.

### Como implementar o

Use o padrão [Mensagens Acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para enviar lembretes em momentos ideais antes da data de vencimento, personalizados com o saldo do assinante, o método de pagamento preferido e um link direto para concluir o pagamento. Esse é o padrão correto quando o acionador é um evento do sistema com base no tempo (data de vencimento da cobrança) em vez do comportamento do cliente, e a comunicação necessária é imediata e transacional em vez de uma sequência de envolvimento de várias etapas.

### Considerações técnicas

- Integre com a plataforma de faturamento para acessar saldos de conta em tempo real, datas de vencimento e histórico de pagamento para obter conteúdo preciso de lembrete.
- Conecte-se a sistemas de processamento de pagamento para permitir o pagamento com um toque ou um clique diretamente da mensagem de lembrete.
- Implemente a lógica de escalonamento que ajusta a urgência e a frequência dos lembretes conforme a data de vencimento se aproxima, respeitando as preferências de comunicação.
- Ofereça suporte a vários métodos de pagamento (inscrição de pagamento automático, carteira digital, transferência bancária) e personalize as opções apresentadas com base no histórico do assinante.


## Recomendações do serviço complementar

Recomendar serviços complementares relevantes, como seguro de dispositivo, armazenamento em nuvem e pacotes de transmissão, com base no plano, no uso e nas preferências do cliente. As recomendações contextuais aumentam o valor que os assinantes recebem por sua relação com o provedor, enquanto aumentam a receita média por usuário.

### Impacto no negócio

As recomendações personalizadas de serviços complementares impulsionam taxas aprimoradas de adoção de complementos, expandindo a receita da base de assinantes existente sem o custo da aquisição de novos clientes.

### Como implementar o

Use o padrão [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) para avaliar o perfil, os serviços atuais e os sinais comportamentais de cada assinante para determinar a oferta complementar mais relevante e apresentá-la pelo canal e momento ideais. Esse é o padrão correto quando a seleção da oferta deve levar em conta a propriedade do serviço atual e as regras de negócios que regem a elegibilidade do serviço complementar, regras que exigem uma lógica de decisão controlada em vez de somente a classificação de afinidade comportamental.

### Considerações técnicas

- Conecte-se ao catálogo de serviços atual do assinante para evitar a recomendação de serviços que já têm e para identificar complementos naturais ao plano existente.
- Integre dados de serviços de parceiros e de terceiros (provedores de transmissão contínua, operadoras de seguros) para apresentar preços precisos e ofertas agrupadas.
- Use dados de dispositivo e uso para informar as recomendações, como sugerir seguro de dispositivo para assinantes com novos dispositivos premium ou armazenamento em nuvem para aqueles que estão executando menos armazenamento no dispositivo.
- Coordene com a personalização no aplicativo e na Web para reforçar as recomendações complementares nos pontos de contato de autoatendimento.


## Personalization de desempenho de rede

Personalize as informações e recomendações de desempenho da rede com base no local, dispositivo e padrões de uso do cliente. Ajudar os assinantes a otimizar sua experiência de conectividade cria confiança e reduz os contatos de suporte associados a problemas de desempenho.

### Impacto no negócio

Experiências personalizadas de desempenho da rede impulsionam um engajamento aprimorado do aplicativo, à medida que os assinantes retornam para verificar a cobertura, solucionar problemas e descobrir dicas de otimização adaptadas à sua situação.

### Como implementar o

Use o padrão [Personalization de Aplicativo/Web de Visitante Conhecido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) para fornecer painéis personalizados de desempenho de rede, informações de cobertura e recomendações de otimização no aplicativo do assinante e na experiência da conta da Web. Esse é o padrão correto quando a personalização é orientada por atributos de perfil e dados de localização, em vez de um modelo de afinidade comportamental.

### Considerações técnicas

- Integre métricas de qualidade da rede e dados de cobertura para fornecer informações de desempenho específicas do local relevantes para a casa, o trabalho e as áreas visitadas com frequência do assinante.
- Conecte dados de diagnóstico do dispositivo para oferecer recomendações de solução de problemas personalizadas com base no modelo do dispositivo específico do assinante e na versão do software.
- Use os serviços de borda do [!DNL Adobe Experience Platform] para fornecer personalização de baixa latência dentro da experiência do aplicativo sem afetar o desempenho.
- Implemente loops de feedback para que os assinantes possam relatar problemas de cobertura, enriquecendo os dados da rede e demonstrando a capacidade de resposta à sua experiência.


## Consultor de plano de IA

Os assinantes de telecomunicações enfrentam um desafio persistente: compreender como seu plano atual se compara às opções disponíveis e se um plano diferente se encaixaria melhor em seu uso real. As páginas de comparação de plano estático exigem que os assinantes interpretem automaticamente os dados que talvez não entendam totalmente, resultando em seleções de plano aquém do ideal, choque na conta e churn evitável. Um consultor de planos de IA envolve os assinantes em conversas naturais, analisa seus padrões de uso a partir de seu perfil em tempo real, faz perguntas de qualificação sobre as necessidades do dispositivo e os requisitos da residência e os orienta para o plano — ou combinação de planos e complementos — que melhor se adapta à sua situação.

### Impacto no negócio

A orientação do plano de conversa reduz o churn orientado pelo plano, aumenta o anexo da atualização para assinantes que não estão satisfeitos com seu plano atual e diminui o volume do centro de contato para consultas de cobrança e alteração de plano.

### Como implementar o

Use o padrão [Brand Concierge Conversational Experience](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md). Essa abordagem implanta o Product Advisor Agent em relação ao plano e ao catálogo complementar, usando os dados de perfil do cliente em tempo real e da AEP Agent Orchestrator, incluindo o histórico de uso e os detalhes do plano atual, para orientar os assinantes pela seleção do plano personalizado por meio da caixa de diálogo natural. Esse é o padrão correto quando a meta é uma descoberta interativa conversacional em várias voltas, que ajuda os assinantes a avaliar e selecionar ativamente o plano correto, diferentemente das mensagens acionadas por eventos, que notificam os assinantes reativamente sobre limites de uso ou alterações no plano, e das experiências personalizadas na Web, que exibem comparações de planos passivamente, sem envolver os assinantes em diálogos de qualificação. Ela requer a configuração do AEP Agent Orchestrator e do controle de marca.

### Considerações técnicas

- A pesquisa de perfil do cliente em tempo real deve mostrar os detalhes do plano atual, os padrões de uso de dados e voz, a compatibilidade do dispositivo e o status do contrato para que o consultor possa fornecer orientação precisa e específica da conta, em vez de descrições do plano genéricas que exigem que o assinante se aplique à sua situação.
- O plano e o catálogo complementar devem ser mantidos atualizados por meio da integração com o sistema de gerenciamento de produtos, pois recomendar um plano ou preço promocional que não esteja mais disponível — ou omitir uma opção recém-lançada — mina diretamente a confiança do assinante e pode criar problemas de expectativa de serviço.
- As medidas de proteção de controle de marca devem definir como o agente lida com comparações de operadoras competitivas, solicitações de preços promocionais e discussões de compromisso de contrato, garantindo que as respostas do agente estejam alinhadas aos padrões regulatórios e de marca sem criar compromissos enganosos que o assinante possa contestar posteriormente.
- Os sinais de conversa — incluindo tamanho doméstico declarado, contagem de dispositivos, interesse de uso internacional e intenção de alteração do plano expressa durante o diálogo — devem ser capturados como XDM ExperienceEvents e transmitidos de volta para o AEP, enriquecendo os perfis do assinante para informar sobre prevenção de churn, atualização e campanhas de venda cruzada downstream.


## Propensão de churn e Análise de experiência de rede

Correlacione as métricas de experiência de rede — quedas de chamadas, degradação da taxa de transferência de dados, exposição a paralisações — com as taxas de contato do atendimento ao cliente e os resultados de churn do assinante para identificar onde os problemas de qualidade da rede se traduzem em riscos mensuráveis de atrito. Os provedores de telecomunicações que analisam o desempenho da rede e o comportamento do cliente em sistemas separados não podem determinar quais falhas de qualidade de serviço realmente geram churn versus quais são absorvidas sem consequências.

### Impacto no negócio

Conectar os dados de experiência da rede aos resultados comportamentais e de churn do cliente permite que as equipes de operações, produtos e retenção da rede priorizem investimentos de remediação com base no impacto do atrito demonstrado, em vez de somente na gravidade técnica.

### Como implementar o

Use o padrão [Customer Analytics &amp; Insight Generation](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md). Essa abordagem conecta dados de eventos da rede, registros de interação do atendimento ao cliente, sinais de comportamento digital e eventos de ciclo de vida do assinante ao Customer Journey Analytics, onde a análise correlacionada identifica os limites de experiência da rede e os padrões de contato que são estatisticamente associados à não renovação de churn e contrato. Esse é o padrão correto quando a meta é a geração de insight e a análise de causas básicas — compreender quais eventos de qualidade de serviço geram desgaste — em vez de acionar uma oferta de retenção ou ativar um público-alvo com risco de churn em uma CDP.

### Considerações técnicas

- Os eventos de experiência de rede devem ser associados a registros de assinantes usando identificadores de dispositivo ou de conta consistentes com a ID de pessoa configurada na conexão do CJA, já que os sistemas de telemetria de rede normalmente usam identificadores de equipamento em vez de identificadores de clientes nativamente.
- Os dados de contato do atendimento ao cliente — incluindo códigos de motivo de contato, canal usado e status de resolução — devem ser assimilados como eventos com carimbos de data e hora que permitem que os analistas criem caminhos sequenciais a partir de incidentes de rede por meio do contato com o serviço por meio de churn em visualizações de fallout ou fluxo do CJA.
- Os dados do plano e do contrato do assinante, incluindo datas de término do contrato, nível do plano e estabilidade, devem estar disponíveis como dimensões de pesquisa na visualização de dados do CJA, para que a análise de churn possa ser segmentada pela proximidade do contrato e camada de valor, em vez de tratar a base do assinante como homogênea.
- Os volumes de dados de telemetria da rede podem ser extremamente grandes; as estratégias de amostragem do conjunto de dados ou a pré-agregação no AEP devem ser consideradas para manter o desempenho da consulta de conexão do CJA dentro de intervalos aceitáveis para uso de autoatendimento do analista.

## Prevenção de churn e reversão

Use modelos preditivos e sinais comportamentais para identificar clientes em risco e acionar campanhas de retenção personalizadas com ofertas personalizadas antes do churn. Os provedores de telecomunicações enfrentam uma pressão de churn persistente, e alcançar assinantes em risco com a oferta certa antes que eles entrem em contato com a fila de cancelamento é significativamente mais econômico do que as campanhas de retorno após o fato.

### Impacto no negócio

Os provedores de telecomunicações com programas proativos de prevenção de churn observam reduções significativas no churn voluntário para segmentos direcionados, com o maior impacto entre os clientes de médio porte, onde as ofertas de retenção direcionadas são mais econômicas do que os descontos gerais.

### Como implementar o

Use o padrão [Jornada entre canais com decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para criar uma jornada de retenção que identifique assinantes em risco com base nas pontuações de propensão de churn, selecione a oferta de retenção apropriada usando a lógica de decisão e a entregue nos canais preferenciais do assinante com etapas de acompanhamento se o primeiro alcance externo for ignorado. Esse é o padrão correto quando a seleção de ofertas e a orquestração de jornadas são necessárias — uma única mensagem acionada não pode acomodar a lógica de classificação de ofertas e o acompanhamento por multitoque necessários para uma retenção eficaz.

### Considerações técnicas

- Os modelos de propensão de churn devem ser treinados em dados históricos de churn que incluam experiência em rede, eventos de faturamento, chamadas de serviço e idade do dispositivo — os modelos treinados somente em dados de engajamento geralmente têm baixo desempenho em relação aos drivers de churn específicos de telecomunicação.
- As ofertas de retenção devem ser restritas pelos limites de custo a reter por segmento de valor do cliente; o mecanismo de decisão deve impedir que ofertas de retenção de alto custo sejam aplicadas a assinantes de baixo valor.
- O processamento do sinal de churn em tempo real deve detectar eventos de consulta de contrato e visitas de página de cancelamento de serviço para acionar respostas urgentes de retenção antes que o assinante seja escalonado.
- A integração do atendimento ao cliente é essencial: os assinantes que chamam a fila de retenção devem ser reconhecidos como participantes do jornada para que os agentes tenham o contexto de oferta de retenção pronto antes do início da chamada.
