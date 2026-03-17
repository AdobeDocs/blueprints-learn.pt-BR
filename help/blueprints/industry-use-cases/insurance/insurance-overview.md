---
title: Casos de uso de seguro
description: Descubra como as organizações de seguros usam o Adobe Experience Platform para personalizar o gerenciamento de políticas, melhorar as experiências com solicitações e impulsionar a retenção do cliente.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '2494'
ht-degree: 0%

---


# Casos de uso de seguro

As organizações de seguros usam o Adobe Experience Platform para unificar os dados dos segurados em sistemas de gerenciamento de políticas, solicitações e contratos, a fim de fornecer comunicações personalizadas em cada estágio do relacionamento com o cliente. Conectando sinais comportamentais a informações de políticas e avisos de sinistro, as seguradoras podem envolver proativamente os clientes com ofertas relevantes, atualizações oportunas de serviços e suporte significativo que impulsiona a retenção e o valor vitalício.

## Campanhas de renovação de política

Envie lembretes e ofertas personalizados de renovação de política com base no histórico de políticas, registro de solicitações e preferências de cobertura de cada cliente. O alcance atempado e relevante da renovação reduz as taxas de descontinuidade das políticas e reforça as relações a longo prazo com os clientes, facilitando aos tomadores de seguros a compreensão das suas opções e a tomada de medidas.

### Impacto no negócio

As organizações que implementam campanhas personalizadas de renovação de políticas geralmente observam uma melhoria de 25% a 35% nas taxas de renovação, reduzindo diretamente a rotatividade do cliente e protegendo a receita de prêmios recorrentes.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). As datas de renovação das apólices são acionadores de eventos naturais que iniciam um alcance personalizado e em tempo hábil no momento em que os tomadores de seguros tomam a sua decisão de renovação.

### Considerações técnicas

- Integre-se ao sistema de gerenciamento de políticas para receber eventos de data de renovação e detalhes de políticas atuais, garantindo que as mensagens reflitam uma cobertura precisa e informações premium.
- Aplique rótulos de governança de dados a todos os dados de política financeira e de identificação pessoal para cumprir com as regulamentações estaduais de seguro e os requisitos de privacidade de dados.
- Configure regras de supressão para impedir que mensagens de renovação sejam enviadas a segurados que já renovaram ou que têm reivindicações ativas que podem afetar seus termos de renovação.
- Coordene o tempo com atribuições de agente ou corretor para que as mensagens diretas para o cliente se alinhem a qualquer alcance que o agente atribuído também possa estar realizando.


## Recomendações de produtos de venda cruzada

Recomendar produtos de seguro adicionais, como seguro de vida, residencial ou cobertura automática, com base nas políticas, no estágio de vida e no perfil de risco existentes de cada cliente. Recomendações personalizadas de produtos ajudam os segurados a descobrir lacunas de cobertura e a criar um portfólio de proteção mais completo.

### Impacto no negócio

As recomendações personalizadas de venda cruzada normalmente promovem uma melhoria de 20 a 30% nas taxas de conversão de venda cruzada, aumentando as políticas por residência e o valor total do cliente.

### Como implementar o

Use o padrão [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). A Decisão em tempo real avalia a cobertura, o estágio de vida e os sinais comportamentais existentes de cada cliente para selecionar a recomendação de produto mais relevante no catálogo disponível.

### Considerações técnicas

- Integre dados de políticas de todas as linhas de produtos em um perfil de cliente unificado para que o mecanismo de decisão tenha uma visão completa da cobertura existente ao selecionar recomendações.
- Configure regras de elegibilidade no modelo de decisão para excluir produtos que um cliente já detém ou que entrem em conflito com diretrizes de subscrição para seu perfil de risco.
- Aplique regras de conformidade normativa para garantir que as recomendações de produtos estejam em conformidade com os requisitos de adequação e marketing de seguros específicos do estado.
- Coordene o resultado da decisão com o portal do agente para que os produtos recomendados fiquem visíveis para os agentes atribuídos que podem estar conversando diretamente com o cliente.


## Personalization do processo de solicitações

Personalize as comunicações dos processos de reclamações, as atualizações de status e os recursos de suporte com base no tipo de reclamação, nas preferências do cliente e no histórico de reclamações. Uma experiência de sinistro transparente e bem comunicada reduz a ansiedade durante momentos estressantes e constrói uma confiança duradoura com os tomadores de seguros.

### Impacto no negócio

As comunicações personalizadas de reivindicações normalmente atingem uma melhoria de 40 a 50% nas pontuações de satisfação das reivindicações, reduzindo as reclamações e fortalecendo a probabilidade de renovação da política após uma reivindicação.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). O processo de solicitações é uma experiência em vários estágios com fases distintas — arquivamento, investigação, ajuste e liquidação — em que cada uma requer comunicações personalizadas e tempo adaptável.

### Considerações técnicas

- Integre-se ao sistema de gerenciamento de solicitações para receber eventos de alteração de status em tempo real que promovam o cliente durante o estágio de jornada apropriado.
- Projete uma lógica de ramificação de jornada que adapta o tom e o conteúdo das mensagens com base no tipo de solicitação, como colisão automática versus danos à propriedade versus solicitações de responsabilidade.
- Implemente regras de supressão durante investigações de reclamações ativas para impedir que mensagens de marketing ou venda cruzada cheguem aos clientes em momentos delicados.
- Garantir que todos os dados relacionados às reclamações que fluem para o perfil do cliente sejam rotulados com restrições apropriadas de governança de dados para impedir seu uso fora das comunicações de serviço.


## Avaliação e prevenção de riscos

Fornecer informações personalizadas sobre avaliação de riscos e dicas de prevenção com base no tipo de política, na localização geográfica e nos fatores de risco específicos de cada cliente. A educação proativa sobre riscos ajuda os segurados a reduzir a exposição à perda, beneficiando tanto o cliente quanto a seguradora.

### Impacto no negócio

O alcance personalizado da prevenção de riscos geralmente leva a uma melhoria de 30 a 40% no envolvimento de prevenção, contribuindo para a redução da frequência das solicitações e o aumento da satisfação do cliente.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). O treinamento em prevenção de riscos é mais eficaz como uma jornada multitoque contínua que fornece orientação relevante ao longo do tempo e se adapta com base no engajamento do cliente e nos fatores de risco sazonais.

### Considerações técnicas

- Integre com provedores de dados de risco de terceiros informações de clima, risco geográfico e risco de propriedade que enriquecem os perfis do cliente com pontuações de risco específicas do local.
- Projete uma lógica de jornada sazonal que forneça conteúdo de prevenção relevante antes dos períodos de alto risco, como a preparação para segurados costeiros da temporada de furacões ou dicas meteorológicas de inverno para clientes com clima frio.
- Aplicar rótulos de governança de dados para distinguir os dados de avaliação de risco usados para a educação do cliente dos dados usados nas decisões atuariais de tomada firme.
- Coordenar o conteúdo de prevenção de riscos com a cobertura específica do tomador de seguro, de modo a que as recomendações sejam relevantes para os riscos que a sua política cobre efetivamente.


## Notificações de Alteração de Política

Envie notificações personalizadas sobre alterações de política, atualizações de cobertura e novas opções com base na política específica e nas preferências de comunicação de cada cliente. Notificações claras e oportunas mantêm os segurados informados e reduzem a confusão sobre seu status de cobertura.

### Impacto no negócio

As notificações personalizadas de alteração de política normalmente atingem uma melhoria de 50 a 60% nas taxas de confirmação de notificação, reduzindo as consultas de atendimento ao cliente e melhorando a compreensão geral do segurado.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Os eventos de alteração de políticas do sistema de administração servem como acionadores naturais para notificações imediatas e relevantes por meio do canal preferido de cada cliente.

### Considerações técnicas

- Integrar ao sistema de administração de políticas para capturar eventos de endosso, alteração e renovação em tempo real, garantindo que as notificações reflitam o estado mais atual das políticas.
- Aplique regras de conformidade normativa para garantir que as notificações atendam aos requisitos de comunicação exigidos pelo estado para alterações de políticas, incluindo idioma e prazos de entrega necessários.
- Configure a lógica de prioridade de canal com base na urgência e no tipo de alteração — por exemplo, reduções de cobertura podem garantir canais mais imediatos do que atualizações informativas.
- Manter uma trilha de auditoria de entrega para todas as notificações de alteração de política para oferecer suporte à documentação de conformidade normativa e à resolução de conflitos.


## Recuperação de Abandono da Cotação

Reenvolva os clientes que começaram, mas não concluíram uma cotação de seguro com mensagens de acompanhamento personalizadas e ofertas personalizadas. O alcance da recuperação em tempo hábil traz os clientes em potencial de volta ao processo de cotação e aborda os obstáculos comuns à conclusão.

### Impacto no negócio

As campanhas de recuperação de abandono de cotações geralmente geram uma melhora de 20 a 30% nas taxas de conclusão de cotações, convertendo mais prospetos em segurados e reduzindo os custos de aquisição de clientes.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). O abandono da cotação é um evento comportamental que aciona um acompanhamento oportuno enquanto o interesse e a intenção do cliente potencial ainda estão novos.

### Considerações técnicas

- Integrar à plataforma de cotação online para capturar eventos de abandono, juntamente com os detalhes da cotação que o cliente já forneceu, permitindo um reengajamento personalizado.
- Configure regras de tempo que equilibram a urgência com respeito — acompanhamento inicial em horas, com um número limitado de lembretes subsequentes nos dias seguintes.
- Aplique regras de consentimento e privacidade para garantir que o acompanhamento só seja enviado a clientes potenciais que optaram por comunicações de marketing, especialmente para clientes que ainda não estabeleceram uma relação de política.
- Inclua deep links que retornam o cliente potencial diretamente para a cotação salva, em vez de exigir que ele reinicie o processo desde o início.


## Ofertas de produtos baseadas em estágios

Identifique os clientes que entram em novos estágios da vida — como casamento, compra de casa, família em crescimento ou aposentadoria — e ofereça produtos de seguro relevantes que correspondam às suas necessidades de proteção em evolução. O direcionamento para o estágio de vida ajuda os segurados a construírem a cobertura certa na hora certa.

### Impacto no negócio

As ofertas de produtos baseados em estágios da vida normalmente atingem uma melhoria de 35 a 45% nas taxas de adoção de produtos em estágios da vida, aprofundando o relacionamento com o cliente durante momentos importantes de tomada de decisão.

### Como implementar o

Use a [Jornada entre canais com o padrão de decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). As transições de estágio de vida se beneficiam da orquestração entre canais combinada com decisões em tempo real para selecionar o produto mais relevante e entregá-lo pelo canal preferido do cliente no momento ideal.

### Considerações técnicas

- Crie modelos de detecção de estágios da vida usando sinais comportamentais, como alterações de endereço, atualizações de beneficiários e padrões de pesquisa online, combinados com eventos de alteração de política.
- Configure o mecanismo de decisão com regras de elegibilidade e adequação do produto que correspondam cada estágio da vida útil às recomendações de cobertura apropriadas.
- Coordene as ofertas do estágio de vida com o agente ou corretor atribuído para que eles estejam preparados para oferecer suporte ao cliente com uma conversa consultiva quando a oferta for entregue.
- Aplique rótulos de governança de dados a qualquer fonte de dados de terceiros usada para inferência do estágio da vida útil para garantir a conformidade com as regulamentações de privacidade de dados e práticas de marketing justas.


## Oportunidades de Desconto e Economia

Identifique e comunique oportunidades de desconto personalizadas — como pacotes, driver seguro, fidelidade e descontos de cobrança sem papel — com base no perfil e no comportamento de cada cliente. As comunicações proativas sobre poupanças demonstram valor e reforçam a relação preço-valor.

### Impacto no negócio

As comunicações personalizadas de desconto e economia normalmente promovem uma melhoria de 25 a 35% nas taxas de utilização de desconto, melhorando a satisfação do cliente e reduzindo a variação impulsionada pelo preço.

### Como implementar o

Use o padrão [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). O Real-time Decisioning avalia a qualificação de cada cliente para descontos disponíveis e seleciona a oportunidade de economia mais impactante para apresentar no momento certo.

### Considerações técnicas

- Integre-se aos sistemas de classificação de políticas e faturamento para calcular a elegibilidade precisa para descontos e os valores potenciais de economia para cada cliente em tempo real.
- Configure regras de decisão que levam em conta as limitações de empilhamento de descontos e garantem que os valores de economia comunicados sejam precisos na atualidade e aprovados pela equipe de preços.
- Aplique regras regulatórias específicas do estado para comunicações de descontos, já que alguns estados têm restrições sobre como os descontos de seguro podem ser comercializados e aplicados.
- Acompanhe os resultados da adoção de descontos para refinar continuamente o modelo de decisão e priorizar as mensagens de economia que mais refletem nos diferentes segmentos de clientes.


## Prevenção de Fraude de Reclamações

Use a detecção inteligente de fraudes para identificar padrões de reclamações suspeitas e personalizar as comunicações de investigação, mantendo a confiança do cliente. Uma prevenção eficaz da fraude protege os tomadores de seguros honestos, mantendo os prêmios justos e garantindo que as reclamações legítimas sejam processadas rapidamente.

### Impacto no negócio

Os programas inteligentes de prevenção contra fraudes de avisos de sinistro geralmente alcançam uma melhoria de 15 a 25% nas taxas de detecção de fraudes, reduzindo os pagamentos fraudulentos e diminuindo os custos gerais com avisos de sinistro.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Os eventos de pontuação de risco de fraude acionam comunicações de investigação apropriadas e ajustes de processos em tempo real, garantindo que as solicitações sinalizadas recebam atenção imediata.

### Considerações técnicas

- Integre pontuações de risco de fraude do sistema de análise de reclamações ao perfil do cliente, aplicando rótulos rigorosos de governança de dados para evitar que os dados de investigação de fraude apareçam em comunicações voltadas para o cliente.
- Crie caminhos de comunicação que mantenham um tom profissional e respeitoso para os clientes cujas solicitações estão sendo analisadas, preservando o relacionamento independentemente do resultado da investigação.
- Implemente controles de acesso com base em funções para garantir que os indicadores de fraude sejam visíveis apenas para equipes de investigação autorizadas e nunca sejam exibidos em visualizações padrão de agente ou atendimento ao cliente.
- Coordene com o serviço de resolução de identidade do [!DNL Adobe Experience Platform] para detectar padrões em perfis relacionados, como endereços compartilhados ou números de telefone vinculados a várias declarações suspeitas.


## Programas de prevenção e bem-estar

Personalize as comunicações do programa de bem-estar, os lembretes de participação e as notificações de recompensa para clientes de seguro de saúde e vida com base em suas metas e nível de engajamento. Programas de bem-estar ativos melhoram os resultados de saúde dos tomadores de seguros e criam uma base de clientes mais forte e engajada.

### Impacto no negócio

As comunicações personalizadas do programa de bem-estar e prevenção normalmente promovem uma melhoria de 30 a 40% nas taxas de participação no programa, contribuindo para melhores resultados de saúde e frequência reduzida de solicitações.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Programas de bem-estar são experiências de engajamento sustentado com marcos, desafios e recompensas que exigem orquestração adaptativa com base na atividade e progresso de cada participante.

### Considerações técnicas

- Integre com dispositivos vestíveis e feeds de dados de aplicativos de integridade usando a assimilação por streaming do [!DNL Adobe Experience Platform], aplicando rótulos de governança de dados claros para distinguir dados de integridade de dados de substituição ou de declaração.
- Implemente mecanismos de consentimento separados para a coleta de dados de bem-estar a fim de garantir que os participantes entendam como seus dados de atividade de saúde são usados e podem recusar sem afetar suas políticas.
- Projete uma lógica de jornada que ajuste a intensidade do programa e a frequência de comunicação com base no nível de engajamento de cada participante para evitar fadiga e incentivar a participação sustentada.
- Garantir que o incentivo ao bem-estar e o rastreamento de recompensas estejam em conformidade com as regulamentações de seguro aplicáveis em relação aos incentivos aos segurados e aos programas de desconto de prêmio.


## Coordenação de Agente e Agente

Permita a comunicação e a coordenação personalizadas entre os clientes e seus agentes ou agentes atribuídos com base nas necessidades de política, no histórico de serviços e nas preferências. Uma melhor coordenação cria uma experiência perfeita em que os clientes se sentem apoiados por um consultor qualificado que entende seu relacionamento completo.

### Impacto no negócio

As comunicações eficazes de coordenação de agentes e corretores normalmente resultam em uma melhora de 35 a 45% no envolvimento do agente, resultando em relacionamentos mais sólidos com o cliente e maior retenção impulsionada por interações de consultoria confiáveis.

### Como implementar o

Use o padrão [Ativação de Mensagem de Saída em Lote](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md). A coordenação do agente é melhor fornecida por meio de ativações em lote programadas que fornecem aos agentes listas de alcance priorizadas do cliente, pontos de contato e ações recomendadas regularmente.

### Considerações técnicas

- Integrar ao sistema de gerenciamento de agentes para manter atribuições precisas de agente-cliente e garantir que as comunicações reflitam o relacionamento correto, especialmente durante as transições de agentes.
- Projete a ativação de dados no portal de agentes para que os agentes recebam uma visualização consolidada dos insights do cliente, renovações futuras e ações recomendadas sem expor dados comportamentais brutos.
- Aplique rótulos de governança de dados para restringir quais elementos de dados do cliente são compartilhados com parceiros de corretores externos em relação a agentes cativos, respeitando os limites de compartilhamento de dados contratuais e regulamentares.
- Implemente loops de feedback das interações do agente de volta ao perfil do cliente para que os insights das conversas presenciais ou telefônicas enriqueçam a visualização unificada e melhorem a personalização futura.


## Resposta a eventos catastróficos

Comunique-se proativamente com os clientes nas áreas afetadas durante desastres naturais ou eventos catastróficos com informações personalizadas de suporte, orientação para o arquivamento de avisos de sinistro e recursos de emergência. O alcance rápido e solidário durante uma crise demonstra o compromisso da seguradora de estar lá quando os clientes mais precisam.

### Impacto no negócio

As comunicações proativas de resposta a eventos catastróficos geralmente atingem uma melhora de 60 a 70% nas taxas de comunicação do cliente durante os eventos, acelerando significativamente o arquivamento de solicitações e fortalecendo a confiança e a fidelidade do cliente a longo prazo.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). As declarações de acontecimentos catastróficos servem como fatores desencadeantes de alta prioridade para uma ação imediata e personalizada de sensibilização de todos os tomadores de seguros na área geográfica afetada.

### Considerações técnicas

- Integre-se a serviços de monitoramento de catástrofes e feeds de declaração de desastres do governo para acionar comunicações rapidamente quando eventos forem declarados para áreas geográficas específicas.
- Crie segmentos geográficos de público-alvo usando dados de endereço do segurado e informações de localização da propriedade para identificar com precisão os clientes na área afetada sem comunicação excessiva com os clientes não afetados.
- Configure o roteamento de mensagens de alta prioridade, substituindo as regras padrão de limitação e supressão de frequência, para garantir que as informações críticas de segurança e de avisos de sinistro cheguem aos clientes imediatamente.
- Pré-crie modelos de mensagem e configurações de jornada para tipos de evento catastróficos comuns, para que as comunicações possam ser ativadas horas após uma declaração de evento, em vez de exigir a criação de conteúdo durante a crise.
