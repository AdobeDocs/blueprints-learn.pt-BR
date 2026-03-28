---
title: Casos de uso de seguro
description: Descubra como as organizações de seguros usam o Adobe Experience Platform para personalizar o gerenciamento de políticas, melhorar as experiências com solicitações e impulsionar a retenção do cliente.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: a082598f-555b-49a4-b201-a55bee793959
source-git-commit: 3542d76106fada9019b70a8cc9fd4c74872d4995
workflow-type: tm+mt
source-wordcount: '3016'
ht-degree: 0%

---

# Casos de uso de seguro

As organizações de seguros usam o Adobe Experience Platform para unificar os dados dos segurados em sistemas de gerenciamento de políticas, solicitações e contratos, a fim de fornecer comunicações personalizadas em cada estágio do relacionamento com o cliente. Conectando sinais comportamentais a informações de políticas e avisos de sinistro, as seguradoras podem envolver proativamente os clientes com ofertas relevantes, atualizações oportunas de serviços e suporte significativo que impulsiona a retenção e o valor vitalício.

## Campanhas de renovação de política

Envie lembretes e ofertas personalizados de renovação de política com base no histórico de políticas, registro de solicitações e preferências de cobertura de cada cliente. O alcance atempado e relevante da renovação reduz as taxas de descontinuidade das políticas e reforça as relações a longo prazo com os clientes, facilitando aos tomadores de seguros a compreensão das suas opções e a tomada de medidas.

### Impacto no negócio

As organizações que implementam campanhas personalizadas de renovação de políticas observam melhores taxas de renovação, reduzindo diretamente a rotatividade do cliente e protegendo a receita de prêmios recorrentes.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Esta abordagem constrói uma sequência de renovação cronometrada que avança desde o aviso inicial até lembretes escalonados e, se necessário, uma mensagem de urgência final, adaptando a cadência e a oferta com base no fato de o tomador de seguro ter tido contatos anteriores. Este é o padrão correto quando o tempo é determinado por uma data de contrato, em vez de um evento discreto do cliente, e a intenção de negócios exige um fluxo sequenciado de várias mensagens durante 30 ou mais dias com ramificação condicional baseada em engajamento — as mensagens acionadas por evento lidam com respostas reativas para eventos discretos, mas não podem acomodar a lógica de programação baseada em calendário ou as dependências de escalonamento necessárias para uma campanha de renovação.

### Considerações técnicas

- Integre-se ao sistema de gerenciamento de políticas para receber eventos de data de renovação e detalhes de políticas atuais, garantindo que as mensagens reflitam uma cobertura precisa e informações premium.
- Aplique rótulos de governança de dados a todos os dados de política financeira e de identificação pessoal para cumprir com as regulamentações estaduais de seguro e os requisitos de privacidade de dados.
- Configure regras de supressão para impedir que mensagens de renovação sejam enviadas a segurados que já renovaram ou que têm reivindicações ativas que podem afetar seus termos de renovação.
- Coordene o tempo com atribuições de agente ou corretor para que as mensagens diretas para o cliente se alinhem a qualquer alcance que o agente atribuído também possa estar realizando.


## Recomendações de produtos de venda cruzada

Recomendar produtos de seguro adicionais, como seguro de vida, residencial ou cobertura automática, com base nas políticas, no estágio de vida e no perfil de risco existentes de cada cliente. Recomendações personalizadas de produtos ajudam os segurados a descobrir lacunas de cobertura e a criar um portfólio de proteção mais completo.

### Impacto no negócio

As recomendações personalizadas de venda cruzada impulsionam taxas de conversão de venda cruzada aprimoradas, aumentando as políticas por residência e o valor geral do tempo de vida do cliente.

### Como implementar o

Use o padrão [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). A Decisão em tempo real avalia a cobertura, o estágio de vida e os sinais comportamentais existentes de cada cliente para selecionar a recomendação de produto mais relevante no catálogo disponível. Esse é o padrão correto quando a seleção de produtos deve levar em conta regras de qualificação, diretrizes de subscrição e requisitos de adequação regulatórios — restrições que exigem lógica de decisão controlada em vez de classificação de afinidade comportamental sozinha.

### Considerações técnicas

- Integre dados de políticas de todas as linhas de produtos em um perfil de cliente unificado para que o mecanismo de decisão tenha uma visão completa da cobertura existente ao selecionar recomendações.
- Configure regras de elegibilidade no modelo de decisão para excluir produtos que um cliente já detém ou que entrem em conflito com diretrizes de subscrição para seu perfil de risco.
- Envolva suas equipes jurídicas e de conformidade para validar se as regras de elegibilidade da recomendação do produto estão alinhadas aos requisitos de marketing e adequação aplicáveis do seguro estadual antes da ativação.
- Coordene o resultado da decisão com o portal do agente para que os produtos recomendados fiquem visíveis para os agentes atribuídos que podem estar conversando diretamente com o cliente.


## Personalization do processo de solicitações

Personalize as comunicações dos processos de reclamações, as atualizações de status e os recursos de suporte com base no tipo de reclamação, nas preferências do cliente e no histórico de reclamações. Uma experiência de sinistro transparente e bem comunicada reduz a ansiedade durante momentos estressantes e constrói uma confiança duradoura com os tomadores de seguros.

### Impacto no negócio

As comunicações personalizadas de reivindicações atingem pontuações de satisfação de reivindicações aprimoradas, reduzindo as reclamações e fortalecendo a probabilidade de renovação da política após uma reivindicação.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). O processo de solicitações é uma experiência em vários estágios com fases distintas — arquivamento, investigação, ajuste e liquidação — em que cada uma requer comunicações personalizadas e tempo adaptável. Este é o padrão correto quando o caso de uso requer um fluxo sequenciado de várias mensagens ao longo de dias com ramificação condicional baseada em eventos de status de solicitações: uma única mensagem acionada não pode acomodar a lógica de dependência entre fases sequenciais de solicitações.

### Considerações técnicas

- Integre-se ao sistema de gerenciamento de solicitações para receber eventos de alteração de status em tempo real que promovam o cliente durante o estágio de jornada apropriado.
- Projete uma lógica de ramificação de jornada que adapta o tom e o conteúdo das mensagens com base no tipo de solicitação, como colisão automática versus danos à propriedade versus solicitações de responsabilidade.
- Implemente regras de supressão durante investigações de reclamações ativas para impedir que mensagens de marketing ou venda cruzada cheguem aos clientes em momentos delicados.
- Garantir que todos os dados relacionados às reclamações que fluem para o perfil do cliente sejam rotulados com restrições apropriadas de governança de dados para impedir seu uso fora das comunicações de serviço.


## Avaliação e prevenção de riscos

Fornecer informações personalizadas sobre avaliação de riscos e dicas de prevenção com base no tipo de política, na localização geográfica e nos fatores de risco específicos de cada cliente. A educação proativa sobre riscos ajuda os segurados a reduzir a exposição à perda, beneficiando tanto o cliente quanto a seguradora.

### Impacto no negócio

O alcance externo personalizado de prevenção de riscos promove um melhor envolvimento na prevenção, contribuindo para reduzir a frequência das solicitações e aumentar a satisfação do cliente.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). O treinamento em prevenção de riscos é mais eficaz como uma jornada multitoque contínua que fornece orientação relevante ao longo do tempo e se adapta com base no engajamento do cliente e nos fatores de risco sazonais. Esse é o padrão correto quando a jornada precisa fornecer conteúdo por longos períodos com ajustes sazonais de tempo e ramificação baseada em envolvimento — as mensagens acionadas por eventos não podem lidar com a programação preditiva ou com a cadência em várias etapas necessária para uma educação contínua.

### Considerações técnicas

- Integre com provedores de dados de risco de terceiros informações de clima, risco geográfico e risco de propriedade que enriquecem os perfis do cliente com pontuações de risco específicas do local.
- Projete uma lógica de jornada sazonal que forneça conteúdo de prevenção relevante antes dos períodos de alto risco, como a preparação para segurados costeiros da temporada de furacões ou dicas meteorológicas de inverno para clientes com clima frio.
- Aplicar rótulos de governança de dados para distinguir os dados de avaliação de risco usados para a educação do cliente dos dados usados nas decisões atuariais de tomada firme.
- Coordenar o conteúdo de prevenção de riscos com a cobertura específica do tomador de seguro, de modo a que as recomendações sejam relevantes para os riscos que a sua política cobre efetivamente.


## Notificações de Alteração de Política

Envie notificações personalizadas sobre alterações de política, atualizações de cobertura e novas opções com base na política específica e nas preferências de comunicação de cada cliente. Notificações claras e oportunas mantêm os segurados informados e reduzem a confusão sobre seu status de cobertura.

### Impacto no negócio

As notificações personalizadas de alteração de política alcançam taxas de confirmação de notificação aprimoradas, reduzindo as consultas de atendimento ao cliente e melhorando a compreensão geral sobre os titulares de políticas.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Os eventos de alteração de políticas do sistema de administração servem como acionadores naturais para notificações imediatas e relevantes por meio do canal preferido de cada cliente. Este é o padrão correto quando o acionador é um evento do sistema (alteração de política) em vez do comportamento do cliente, e a comunicação necessária é imediata e reativa em vez de uma sequência sustentada de criação.

### Considerações técnicas

- Integrar ao sistema de administração de políticas para capturar eventos de endosso, alteração e renovação em tempo real, garantindo que as notificações reflitam o estado mais atual das políticas.
- Trabalhe com sua equipe jurídica para confirmar se as notificações de alteração de política atendem aos requisitos aplicáveis de tempo, idioma e canal de entrega exigidos pelo estado antes de ativar as comunicações automatizadas.
- Configure a lógica de prioridade de canal com base na urgência e no tipo de alteração — por exemplo, reduções de cobertura podem garantir canais mais imediatos do que atualizações informativas.
- Manter uma trilha de auditoria de entrega para todas as notificações de alteração de política para oferecer suporte à documentação de conformidade normativa e à resolução de conflitos.


## Recuperação de Abandono da Cotação

Reenvolva os clientes que começaram, mas não concluíram uma cotação de seguro com mensagens de acompanhamento personalizadas e ofertas personalizadas. O alcance da recuperação em tempo hábil traz os clientes em potencial de volta ao processo de cotação e aborda os obstáculos comuns à conclusão.

### Impacto no negócio

As campanhas de recuperação de abandono de cotações geram melhores taxas de conclusão de cotações, convertendo mais prospetos em tomadores de seguros e reduzindo os custos de aquisição de clientes.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). O abandono da cotação é um evento comportamental que aciona um acompanhamento oportuno enquanto o interesse e a intenção do cliente potencial ainda estão novos. Esse é o padrão correto quando um comportamento distinto do cliente (abandono) é o acionador e a resposta necessária é um reengajamento com reconhecimento de tempo, em vez de uma sequência de criação de várias etapas ou um offer decisioning complexo.

### Considerações técnicas

- Integrar à plataforma de cotação online para capturar eventos de abandono, juntamente com os detalhes da cotação que o cliente já forneceu, permitindo um reengajamento personalizado.
- Configure regras de tempo que equilibram a urgência com respeito — acompanhamento inicial em horas, com um número limitado de lembretes subsequentes nos dias seguintes.
- Aplique regras de consentimento e privacidade para garantir que o acompanhamento só seja enviado a clientes potenciais que optaram por comunicações de marketing, especialmente para clientes que ainda não estabeleceram uma relação de política.
- Inclua deep links que retornam o cliente potencial diretamente para a cotação salva, em vez de exigir que ele reinicie o processo desde o início.


## Oportunidades de Desconto e Economia

Identifique e comunique oportunidades de desconto personalizadas — como pacotes, driver seguro, fidelidade e descontos de cobrança sem papel — com base no perfil e no comportamento de cada cliente. As comunicações proativas sobre poupanças demonstram valor e reforçam a relação preço-valor.

### Impacto no negócio

As comunicações personalizadas de desconto e economia geram melhores taxas de utilização de desconto, melhorando a satisfação do cliente e reduzindo o churn orientado por preços.

### Como implementar o

Use o padrão [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). O Real-time Decisioning avalia a qualificação de cada cliente para descontos disponíveis e seleciona a oportunidade de economia mais impactante para apresentar no momento certo. Este é o padrão correto quando a seleção de descontos deve levar em conta as limitações de empilhamento, as restrições normativas e os cálculos atuariais precisos — restrições que exigem uma lógica de decisão controlada em vez de verificações de elegibilidade simples sozinhas.

### Considerações técnicas

- Integre-se aos sistemas de classificação de políticas e faturamento para calcular a elegibilidade precisa para descontos e os valores potenciais de economia para cada cliente em tempo real.
- Configure regras de decisão que levam em conta as limitações de empilhamento de descontos e garantem que os valores de economia comunicados sejam precisos na atualidade e aprovados pela equipe de preços.
- Aplique regras regulatórias específicas do estado para comunicações de descontos, já que alguns estados têm restrições sobre como os descontos de seguro podem ser comercializados e aplicados.
- Acompanhe os resultados da adoção de descontos para refinar continuamente o modelo de decisão e priorizar as mensagens de economia que mais refletem nos diferentes segmentos de clientes.


## Prevenção de Fraude de Reclamações

Use a detecção inteligente de fraudes para identificar padrões de reclamações suspeitas e personalizar as comunicações de investigação, mantendo a confiança do cliente. Uma prevenção eficaz da fraude protege os tomadores de seguros honestos, mantendo os prêmios justos e garantindo que as reclamações legítimas sejam processadas rapidamente.

### Impacto no negócio

Os programas inteligentes de prevenção contra fraudes de avisos de sinistro melhoram as taxas de detecção de fraudes, reduzindo os pagamentos fraudulentos e os custos gerais com avisos de sinistro.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Os eventos de pontuação de risco de fraude acionam comunicações de investigação apropriadas e ajustes de processos em tempo real, garantindo que as solicitações sinalizadas recebam atenção imediata. Esse é o padrão correto quando um evento derivado do sistema (pontuação de risco de fraude) é o acionador e a ação necessária é o ajuste imediato do processo interno com comunicação cuidadosa com o cliente, em vez de um cenário de jornada ou decisão em várias etapas.

### Considerações técnicas

- Integre pontuações de risco de fraude do sistema de análise de reclamações ao perfil do cliente, aplicando rótulos rigorosos de governança de dados para evitar que os dados de investigação de fraude apareçam em comunicações voltadas para o cliente.
- Crie caminhos de comunicação que mantenham um tom profissional e respeitoso para os clientes cujas solicitações estão sendo analisadas, preservando o relacionamento independentemente do resultado da investigação.
- Implemente controles de acesso com base em funções para garantir que os indicadores de fraude sejam visíveis apenas para equipes de investigação autorizadas e nunca sejam exibidos em visualizações padrão de agente ou atendimento ao cliente.
- Coordene com o serviço de resolução de identidade do [!DNL Adobe Experience Platform] para detectar padrões em perfis relacionados, como endereços compartilhados ou números de telefone vinculados a várias declarações suspeitas.


## Programas de prevenção e bem-estar

Personalize as comunicações do programa de bem-estar, os lembretes de participação e as notificações de recompensa para clientes de seguro de saúde e vida com base em suas metas e nível de engajamento. Programas de bem-estar ativos melhoram os resultados de saúde dos tomadores de seguros e criam uma base de clientes mais forte e engajada.

### Impacto no negócio

As comunicações personalizadas do programa de bem-estar e prevenção impulsionam taxas de participação do programa aprimoradas, contribuindo para melhores resultados de saúde e frequência reduzida de solicitações.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Programas de bem-estar são experiências de engajamento sustentado com marcos, desafios e recompensas que exigem orquestração adaptativa com base na atividade e progresso de cada participante. Este é o padrão correto quando o caso de uso requer um fluxo de várias mensagens de longo prazo com ramificação baseada em envolvimento e ajustes de tempo adaptáveis — as mensagens acionadas por eventos não podem lidar com a lógica complexa de marcos ou com a necessidade de ajustar a cadência de comunicação com base no rastreamento sustentado de atividades.

### Considerações técnicas

- Integre com dispositivos vestíveis e feeds de dados de aplicativos de integridade usando a assimilação por streaming do [!DNL Adobe Experience Platform], aplicando rótulos de governança de dados claros para distinguir dados de integridade de dados de substituição ou de declaração.
- Implemente mecanismos de consentimento separados para a coleta de dados de bem-estar a fim de garantir que os participantes entendam como seus dados de atividade de saúde são usados e podem recusar sem afetar suas políticas.
- Projete uma lógica de jornada que ajuste a intensidade do programa e a frequência de comunicação com base no nível de engajamento de cada participante para evitar fadiga e incentivar a participação sustentada.
- Entre em contato com suas equipes jurídicas e de conformidade para analisar as estruturas de incentivo de bem-estar e os programas de desconto premium visando a conformidade com as regulamentações estaduais de seguro aplicáveis antes do lançamento.


## Coordenação de Agente e Agente

Permita a comunicação e a coordenação personalizadas entre os clientes e seus agentes ou agentes atribuídos com base nas necessidades de política, no histórico de serviços e nas preferências. Uma melhor coordenação cria uma experiência perfeita em que os clientes se sentem apoiados por um consultor qualificado que entende seu relacionamento completo.

### Impacto no negócio

Comunicações eficazes de coordenação de agentes e corretores resultam em melhor envolvimento do agente, resultando em relacionamentos mais sólidos com o cliente e maior retenção impulsionada por interações de consultoria confiáveis.

### Como implementar o

Use o padrão [Ativação de Mensagem de Saída em Lote](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md). A coordenação do agente é melhor fornecida por meio de ativações em lote programadas que fornecem aos agentes listas de alcance priorizadas do cliente, pontos de contato e ações recomendadas regularmente. Esse é o padrão correto quando o público-alvo é grande e predefinido, o tempo de entrega é agendado de forma recorrente em vez de ser orientado por eventos, e nenhuma ramificação ou decisão em tempo real é necessária.

### Considerações técnicas

- Integrar ao sistema de gerenciamento de agentes para manter atribuições precisas de agente-cliente e garantir que as comunicações reflitam o relacionamento correto, especialmente durante as transições de agentes.
- Projete a ativação de dados no portal de agentes para que os agentes recebam uma visualização consolidada dos insights do cliente, renovações futuras e ações recomendadas sem expor dados comportamentais brutos.
- Aplique rótulos de governança de dados para restringir quais elementos de dados do cliente são compartilhados com parceiros de corretores externos em relação a agentes cativos, respeitando os limites de compartilhamento de dados contratuais e regulamentares.
- Implemente loops de feedback das interações do agente de volta ao perfil do cliente para que os insights das conversas presenciais ou telefônicas enriqueçam a visualização unificada e melhorem a personalização futura.


## Resposta a eventos catastróficos

Comunique-se proativamente com os clientes nas áreas afetadas durante desastres naturais ou eventos catastróficos com informações personalizadas de suporte, orientação para o arquivamento de avisos de sinistro e recursos de emergência. O alcance rápido e solidário durante uma crise demonstra o compromisso da seguradora de estar lá quando os clientes mais precisam.

### Impacto no negócio

As comunicações proativas de resposta a eventos catastróficos alcançam melhores taxas de comunicação do cliente durante eventos, acelerando o arquivamento de solicitações e fortalecendo a confiança e a fidelidade do cliente a longo prazo.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). As declarações de acontecimentos catastróficos servem como fatores desencadeantes de alta prioridade para uma ação imediata e personalizada de sensibilização de todos os tomadores de seguros na área geográfica afetada. Esse é o padrão correto quando um evento externo de alta prioridade é o acionador e a resposta necessária é imediata e abrangente alcance geográfico com informações críticas em termos de tempo, em vez de padrões individuais de comportamento do cliente ou sequenciamento complexo.

### Considerações técnicas

- Integre-se a serviços de monitoramento de catástrofes e feeds de declaração de desastres do governo para acionar comunicações rapidamente quando eventos forem declarados para áreas geográficas específicas.
- Crie segmentos geográficos de público-alvo usando dados de endereço do segurado e informações de localização da propriedade para identificar com precisão os clientes na área afetada sem comunicação excessiva com os clientes não afetados.
- Configure o roteamento de mensagens de alta prioridade, substituindo as regras padrão de limitação e supressão de frequência, para garantir que as informações críticas de segurança e de avisos de sinistro cheguem aos clientes imediatamente.
- Pré-crie modelos de mensagem e configurações de jornada para tipos de evento catastróficos comuns, para que as comunicações possam ser ativadas horas após uma declaração de evento, em vez de exigir a criação de conteúdo durante a crise.


## Personalization de conteúdo do portal do segurado

Personalize o portal de autoatendimento autenticado e a experiência de aplicativo móvel para segurados ao encontrar as informações de cobertura, as ferramentas e os recursos mais relevantes com base no comportamento de navegação, no portfólio de políticas e nas interações de serviço recentes. Um portal que se adapta ao contexto atual de cada segurado reduz o atrito e facilita para os clientes encontrar o que precisam, quando precisam.

### Impacto no negócio

A personalização da experiência do portal do segurado impulsiona melhorias mensuráveis na conclusão de tarefas de autoatendimento e envolvimento digital, reduzindo o volume de entrada do centro de contato e fortalecendo a satisfação do cliente com o canal digital.

### Como implementar o

Use o padrão [Recomendação Comportamental](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Sinais comportamentais de sessões autenticadas de portal — uso da calculadora de cobertura, visualizações de documentos de política, verificações de status de solicitações e envolvimento de tópicos de perguntas frequentes — treinam um modelo de recomendação que exibe dinamicamente o conteúdo e as ferramentas mais relevantes para o contexto atual de cada segurado. Esse é o padrão correto quando a personalização é orientada por sinais comportamentais implícitos em uma sessão autenticada e o objetivo é a classificação de relevância de um conteúdo ou catálogo de recursos, em vez do Offer Decisioning, que requer qualificação controlada e aprovação atuarial antes de apresentar uma oferta de produto, ou Cross-Channel com Decisão, que é mais apropriado ao coordenar uma oferta de produto em vários canais.

### Considerações técnicas

- Aplique rótulos de governança de dados a sinais comportamentais coletados no portal de segurados para distinguir a análise de engajamento dos dados de seguros regulamentados e restringir que quaisquer sinais derivados do histórico de solicitações fluam para modelos de personalização sem revisão atuarial e de conformidade explícita.
- Integrar o modelo comportamental ao sistema de gerenciamento de políticas para garantir que as recomendações de conteúdo e ferramentas reflitam o portfólio ativo de políticas de cada segurado — voltando ferramentas de cobertura automática para segurados automáticos e recursos de propriedade para proprietários de imóveis — sem expor dados brutos de políticas ao modelo de recomendação além da classificação da linha de produtos.
- Implemente controles de conformidade específicos do estado para garantir que a personalização comportamental não constitua uma recomendação de seguro ou solicitação de marketing de acordo com as regulamentações estaduais aplicáveis, especialmente quando os sinais comportamentais puderem implicar a detecção de lacunas de cobertura.
- Coordene os sinais de personalização do portal com o portal do agente para que os agentes que atendem aos segurados que mostraram um forte comportamento de pesquisa de autoatendimento recebam uma visualização consolidada do envolvimento digital do cliente junto com seu histórico de serviço.
