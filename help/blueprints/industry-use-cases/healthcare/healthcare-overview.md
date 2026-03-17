---
title: Casos de uso da área de saúde
description: Descubra como as organizações de saúde usam o Adobe Experience Platform para melhorar o envolvimento dos pacientes, simplificar a coordenação do atendimento e gerar melhores resultados de saúde.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: 8da82711-a783-488d-a0ed-070b33ecbbc4
source-git-commit: ccfd8c987a0090ca690e15a4bd89f4d96ec9c01f
workflow-type: tm+mt
source-wordcount: '2356'
ht-degree: 1%

---

# Casos de uso da área de saúde

As organizações de saúde usam o Adobe Experience Platform para criar perfis unificados de pacientes e fornecer comunicações personalizadas e oportunas em todos os pontos de contato. Conectando dados clínicos, comportamentais e de preferência em um único local, as equipes de atendimento podem envolver os pacientes de maneira mais eficaz e, ao mesmo tempo, manter os mais altos padrões de privacidade e conformidade.

## Automação de Lembrete de Compromisso

Envie lembretes de compromisso personalizados por email, mensagem de texto e notificações por push com base nas preferências de comunicação e no tipo de compromisso de cada paciente. Os lembretes automatizados reduzem as consultas perdidas e mantêm os cronogramas em execução sem problemas, liberando a equipe para se concentrar no atendimento ao paciente.

### Impacto no negócio

As organizações que implementam lembretes de compromisso automatizado normalmente veem uma melhoria de 30 a 40% nas taxas de visitas e uma redução significativa nas caras não comparências.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). A criação de compromissos e os eventos de atualização do sistema de agendamento servem como acionadores naturais para mensagens de lembrete oportunas e relevantes.

### Considerações técnicas

- Garantir que todas as informações de contato do paciente e os detalhes da consulta sejam transmitidos e armazenados em conformidade com os requisitos da HIPAA, usando rótulos de uso de dados apropriados para restringir o acesso não autorizado.
- Integre-se ao sistema de programação de registros eletrônicos de saúde para capturar eventos de criação, cancelamento e reprogramação de compromissos em tempo real.
- Aplique políticas de gerenciamento de consentimento para que os lembretes só sejam enviados por canais em que o paciente tenha optado explicitamente.
- Configure regras de supressão para evitar lembretes duplicados ou excessivos quando os compromissos forem reagendados em sucessão rápida.


## Campanhas de adesão à medicação

Envie lembretes personalizados e conteúdo educacional para ajudar os pacientes a manter o controle de seus cronogramas de medicação e planos de tratamento. Mensagens personalizadas com base no tipo de medicamento, no cronograma de dosagem e no histórico do paciente promovem melhor adesão e melhores resultados de saúde.

### Impacto no negócio

As campanhas personalizadas de adesão à medicação normalmente promovem uma melhora de 20 a 30% nas taxas de adesão, resultando em resultados de saúde mensuravelmente melhores e menos reinternações hospitalares.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). A adesão à medicação requer uma abordagem contínua e multitoque com lembretes cada vez maiores, pontos de contato educacionais e check-ins de acompanhamento durante o curso de um plano de tratamento.

### Considerações técnicas

- Aplique rótulos rigorosos de uso de dados a todas as informações de saúde protegidas relacionadas aos dados de medicação e diagnóstico para impedir a ativação downstream não autorizada.
- Integre-se aos sistemas de farmácia e registros eletrônicos de saúde para receber dados de preenchimento e recarga de prescrição que acionam etapas de jornada.
- Implemente um gerenciamento de consentimento robusto para garantir que os pacientes concordem em receber comunicações relacionadas a medicamentos e possam retirar o consentimento a qualquer momento.
- Projete a lógica de jornada para detectar padrões de não engajamento e encaminhe para notificações da equipe de atendimento quando um paciente estiver em risco de não aderir.


## Lembretes de cuidados preventivos

Lembrar proativamente os pacientes sobre os cuidados preventivos recomendados, como vacinas, exames preventivos e check-ups anuais com base na idade, histórico médico e fatores de risco. Lembretes de cuidados preventivos oportunos ajudam a fechar lacunas nos cuidados e melhorar a saúde geral da população.

### Impacto no negócio

O alcance pró-ativo dos cuidados preventivos geralmente resulta em um aumento de 25 a 35% nas taxas de conclusão dos cuidados preventivos, contribuindo para a melhoria da saúde da população e redução dos custos dos tratamentos de longo prazo.

### Como implementar o

Use o padrão [Ativação de Mensagem de Saída em Lote](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md). Os lembretes de cuidados preventivos são melhor entregues por meio de campanhas em lote programadas que avaliam a elegibilidade do paciente em relação às diretrizes clínicas regularmente.

### Considerações técnicas

- Crie segmentos de público-alvo usando critérios de diretrizes clínicas (idade, gênero, histórico familiar, datas de triagem anteriores) e, ao mesmo tempo, aplique rótulos de uso de dados a todas as informações de saúde protegidas usadas na segmentação.
- Coordenar com as equipes clínicas para garantir que o conteúdo de lembretes se alinhe às atuais diretrizes de cuidados preventivos baseadas em evidências e protocolos organizacionais.
- Implemente o limite de frequência para evitar sobrecarregar os pacientes que se qualificam para várias recomendações de cuidados preventivos simultaneamente.
- Mantenha uma trilha de auditoria de todas as comunicações de cuidados preventivos enviadas para relatórios normativos e documentação de medida de qualidade.


## Campanhas de acompanhamento pós-visita

Envie automaticamente pesquisas pós-visita, instruções de atendimento e lembretes de consulta de acompanhamento com base no tipo de visita e nas necessidades específicas de cada paciente. O acompanhamento em tempo hábil melhora a satisfação do paciente e garante a continuidade do atendimento após cada encontro.

### Impacto no negócio

As campanhas de acompanhamento pós-visita automatizadas normalmente atingem uma melhora de 40 a 50% nas taxas de resposta da pesquisa e pontuações mensuravelmente mais altas de satisfação do paciente.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Os eventos de conclusão de visitas do sistema de registros eletrônicos de saúde fornecem um acionador natural e oportuno para comunicações de acompanhamento personalizadas de acordo com o tipo de encontro.

### Considerações técnicas

- Integre-se ao sistema de registros eletrônicos de saúde para receber eventos de despejo de visitas que incluem o tipo de visita, o provedor e instruções relevantes de atendimento sem expor as anotações clínicas completas.
- Aplique rótulos de uso de dados a qualquer conteúdo de instrução sobre o tratamento para garantir que as informações protegidas de saúde sejam compartilhadas somente por canais seguros e autorizados pelo paciente.
- Configure regras de tempo que levem em conta o tipo de visita — por exemplo, acompanhamentos pós-cirúrgicos podem exigir um tempo diferente das pesquisas de check-up de rotina.
- Inclua links seguros no portal do paciente para a conclusão da pesquisa e agendamento de consultas, em vez de coletar informações de saúde por canais não seguros.


## Programas de gerenciamento de doenças crônicas

Personalize as comunicações de gerenciamento de doenças crônicas, o conteúdo educacional e os lembretes de monitoramento com base na condição e no plano de tratamento específicos de cada paciente. O engajamento sustentado e relevante ajuda os pacientes a ter um papel ativo no gerenciamento de sua saúde ao longo do tempo.

### Impacto no negócio

Os programas personalizados de gerenciamento de doenças crônicas geralmente observam um aumento de 30 a 40% nas taxas de engajamento no programa, resultando em melhores resultados no gerenciamento de doenças e na redução da utilização dos cuidados de emergência.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). O gerenciamento de doenças crônicas é inerentemente uma experiência de longa duração com vários pontos de contato que requer mensagens adaptáveis com base no envolvimento do paciente e nos marcos de saúde.

### Considerações técnicas

- Projetar uma lógica de ramificação da jornada que se adapta com base em métricas específicas da condição (por exemplo, tendências de glicose no sangue para o tratamento do diabetes ou leituras da pressão arterial para programas de hipertensão).
- Implemente uma governança de dados rigorosa com rótulos de uso de dados [!DNL Adobe Experience Platform] para classificar e proteger dados de integridade específicos da condição em toda a jornada.
- Integre com dispositivos de monitoramento remoto de pacientes e sistemas de resultados relatados pelo paciente para alimentar dados de saúde em tempo real nos pontos de decisão da jornada.
- Crie caminhos de escalonamento da equipe de atendimento na jornada para que o não engajamento ou as tendências de saúde acionem alertas para a equipe clínica apropriada.


## Jornada de integração de novos pacientes

Automatize uma jornada de integração em várias etapas para novos pacientes, que inclui informações de boas-vindas, instruções de acesso ao portal do paciente e orientação de agendamento de consultas. Uma experiência de integração tranquila dá o tom para um relacionamento de longo prazo com o paciente.

### Impacto no negócio

As novas jornadas automatizadas de integração de pacientes geralmente geram uma melhora de 50 a 60% nas taxas de ativação do portal e um engajamento antecipado do paciente significativamente maior.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). A integração do paciente é um processo naturalmente sequencial, em várias etapas, em que cada comunicação se baseia na anterior e se adapta caso o paciente tenha completado as ações principais.

### Considerações técnicas

- Integrar ao sistema de registro do paciente para acionar a jornada de integração imediatamente após a criação do novo registro do paciente, garantindo uma primeira impressão oportuna.
- Use a resolução de identidade para mesclar todos os registros pré-existentes (por exemplo, de uma visita ao site ou solicitação de compromisso) com o novo perfil do paciente para evitar comunicações duplicadas.
- Garanta que os links e as credenciais de ativação do portal sejam entregues por meio de canais seguros, compatíveis com HIPAA, e expirem após um período definido.
- Projete a jornada para detectar eventos de ativação do portal e de conclusão do formulário de modo que as etapas subsequentes se adaptem em vez de repetir as informações nas quais o paciente já atuou.


## Entrega de conteúdo de saúde personalizada

Forneça conteúdo personalizado de educação em saúde, dicas de bem-estar e recursos adaptados às condições, interesses e metas de saúde de cada paciente. O conteúdo relevante cria confiança, melhora a alfabetização em saúde e capacita os pacientes a tomar decisões informadas sobre seus cuidados.

### Impacto no negócio

A entrega personalizada de conteúdo de saúde normalmente atinge um aumento de 35 a 45% nas taxas de engajamento de conteúdo, levando a uma melhoria mensurável na educação do paciente e na alfabetização em saúde.

### Como implementar o

Use a [Jornada entre canais com o padrão de decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). A entrega de conteúdo de saúde se beneficia da decisão em tempo real, que seleciona o conteúdo mais relevante para cada paciente com base em suas condições, preferências e envolvimento anterior, fornecido por meio de seu canal preferido.

### Considerações técnicas

- Aplique classificação de conteúdo e rótulos de uso de dados a todos os materiais de educação em saúde para garantir que o conteúdo específico da condição seja entregue somente aos pacientes que consentiram em receber informações de saúde sobre esse tópico.
- Integrar o mecanismo de decisão a um repositório de conteúdo que é regularmente revisado e aprovado pelas equipes clínicas para garantir a precisão médica.
- Implemente regras de fadiga do conteúdo para evitar a entrega excessiva de conteúdo em um único tópico e para equilibrar o material educacional entre as várias necessidades de saúde de um paciente.
- Rastreie os sinais de envolvimento de conteúdo (aberturas, cliques, tempo gasto) para refinar continuamente a relevância do conteúdo sem coletar ou armazenar informações adicionais protegidas de integridade.


## Notificação de resultados do laboratório

Notifique os pacientes quando os resultados do laboratório estiverem disponíveis por meio de seu canal de comunicação preferido com mensagens personalizadas e seguras. A notificação imediata incentiva os pacientes a revisar os resultados rapidamente e acompanhar a equipe de atendimento quando necessário.

### Impacto no negócio

As notificações automatizadas de resultados laboratoriais geralmente geram um aumento de 60 a 70% nas taxas de visualização de resultados, melhorando a comunicação com os pacientes e permitindo um acompanhamento clínico mais rápido quando os resultados exigirem alguma ação.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). A disponibilidade dos resultados do laboratório é um evento distinto que requer uma notificação imediata e única através do canal preferido do paciente.

### Considerações técnicas

- Nunca inclua valores reais de resultados de laboratório em mensagens de notificação — notifique apenas o paciente de que os resultados estão disponíveis e direcione-os para o portal seguro do paciente para obter detalhes.
- Integre ao sistema de informações do laboratório para receber eventos prontos para resultados, aplicando rótulos rigorosos de uso de dados para evitar que quaisquer dados clínicos fluam para os canais de marketing.
- Implemente uma lógica de retenção do provedor para que as notificações só sejam enviadas depois que o médico responsável pelo pedido tiver revisado e divulgado os resultados para visualização do paciente.
- Garantir que todos os links de notificação apontem para sessões autenticadas e criptografadas do portal do paciente que atendam aos requisitos de segurança da HIPAA.


## Verificação de Cobertura de Seguro

Verificar e comunicar proativamente informações de cobertura de seguro aos pacientes antes de suas consultas para reduzir surpresas de faturamento e melhorar a experiência geral do paciente. A comunicação de cobertura clara e inicial cria confiança e reduz as disputas de faturamento pós-visita.

### Impacto no negócio

A verificação proativa da cobertura do seguro geralmente resulta em uma melhora de 25 a 35% nas taxas de confirmação da cobertura pré-visita e em uma redução significativa nas disputas de cobrança e nas reclamações dos pacientes.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Os eventos de agendamento de consultas servem como acionadores para iniciar a verificação de cobertura e comunicar os resultados ao paciente antes da visita.

### Considerações técnicas

- Integre-se aos sistemas de verificação de qualificação de seguro para recuperar o status de cobertura em tempo real sem armazenar dados completos de solicitações de seguro na plataforma de dados do cliente.
- Aplique rótulos de uso de dados a todas as informações financeiras e de seguros para restringir seu uso somente a comunicações relacionadas a faturamento.
- Configure a sincronização da mensagem para permitir um prazo de entrega suficiente antes da consulta para que os pacientes resolvam quaisquer problemas de cobertura ou entrem em contato com o fornecedor do seguro.
- Inclua instruções claras e informações de contato para o departamento de faturamento, para que os pacientes possam fazer perguntas ou fornecer detalhes atualizados sobre o seguro antes de sua visita.


## Lembretes de Compromisso do Telehealth

Envie lembretes personalizados para compromissos de telessaúde que incluam instruções de conexão, dicas de preparação e informações de suporte técnico. Lembretes eficazes de telessaúde reduzem visitas virtuais perdidas e ajudam os pacientes a se sentirem confiantes usando ferramentas de atendimento digital.

### Impacto no negócio

Os lembretes personalizados de consulta em telessaúde normalmente promovem uma melhora de 40 a 50% nas taxas de exibição de visitas virtuais e aceleram a adoção geral da telessaúde na população de pacientes.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Os eventos de agendamento de compromisso de telessaúde fornecem um acionador natural para lembretes oportunos que incluem detalhes de conexão e orientação de preparação.

### Considerações técnicas

- Inclua instruções de conexão específicas da plataforma (desktop versus dispositivos móveis) com base nas preferências conhecidas do dispositivo do paciente ou nos dados de sessão de telesaúde anteriores.
- Garanta que todos os links de conexão e identificadores de sessão de teleintegridade sejam entregues por meio de canais criptografados compatíveis com HIPAA e expirem após a janela de compromisso agendada.
- Integrar com a plataforma de telessaúde para detectar quando um paciente se conectou com êxito para que as mensagens de lembrete secundárias possam ser suprimidas.
- Forneça um caminho de fallback para as informações de contato do suporte técnico para os pacientes que não se conectaram em uma janela definida antes da hora de início da consulta.


## Engajamento no programa de bem-estar

Personalize as comunicações, os desafios e as recompensas do programa de bem-estar com base nas metas de saúde, no nível de atividade e nas preferências de cada paciente. Programas de bem-estar envolventes motivam os pacientes a adotar hábitos mais saudáveis e manter o bem-estar a longo prazo.

### Impacto no negócio

As campanhas de engajamento personalizadas do programa de bem-estar normalmente atingem um aumento de 30 a 40% nas taxas de participação no programa, contribuindo para melhores resultados de saúde e maior fidelidade do paciente.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Os programas de bem-estar são experiências de engajamento sustentado com vários marcos, desafios e pontos de contato de recompensa que exigem orquestração adaptativa com base na participação e no progresso do paciente.

### Considerações técnicas

- Integre com dispositivos vestíveis e feeds de dados de aplicativos de condicionamento físico, aplicando rótulos claros de uso de dados para distinguir dados de bem-estar de dados de saúde clínica sujeitos a requisitos regulatórios mais rigorosos.
- Implementar um gerenciamento de consentimento que permita aos pacientes conceder e revogar permissões para coleta de dados de bem-estar independentemente de suas preferências de comunicação clínica.
- Projetar uma lógica de jornada que ajuste a dificuldade de desafio e a frequência de comunicação com base nos padrões de engajamento de cada paciente para evitar desânimo ou fadiga.
- Garantir que o rastreamento de recompensas e incentivos esteja em conformidade com as normas aplicáveis da área de saúde em relação aos requisitos de incentivo e antirretorno do paciente.


## Coordenação da equipe de atendimento

Permitir a comunicação e a coordenação personalizadas entre os pacientes e os membros de sua equipe de atendimento com base no plano de atendimento e nas preferências individuais. Uma melhor coordenação leva a transições de cuidados mais perfeitas e melhores resultados para pacientes com necessidades de cuidados complexas.

### Impacto no negócio

Comunicações eficazes de coordenação da equipe de cuidados normalmente resultam em uma melhora de 35 a 45% no envolvimento da equipe de cuidados e resultados mensuráveis de melhor coordenação dos cuidados em planos de cuidados de vários provedores.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). A coordenação da equipe de atendimento envolve várias partes interessadas e fluxos de comunicação contínuos que devem se adaptar com base nos marcos do plano de atendimento, nas alterações do status do paciente e nas ações do provedor.

### Considerações técnicas

- Implemente controles de acesso com base em funções e rótulos de uso de dados para garantir que cada membro da equipe de atendimento receba apenas informações do paciente relevantes para sua função no plano de atendimento.
- Integre-se à gestão de cuidados e aos sistemas de registros eletrônicos de saúde para receber atualizações de planos de cuidados, conclusões de encaminhamento e eventos de transição de cuidados que acionam mensagens de coordenação.
- Projete caminhos de comunicação separados para mensagens direcionadas ao paciente e ao provedor, garantindo que a terminologia clínica seja usada adequadamente para os provedores, enquanto as mensagens do paciente permanecem claras e acessíveis.
- Manter uma trilha de auditoria completa de todas as comunicações de coordenação de cuidados para conformidade com as regulamentações de continuidade de cuidados e os requisitos de capacitação.
