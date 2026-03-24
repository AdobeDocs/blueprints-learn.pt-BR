---
title: Casos de uso da área de saúde
description: Descubra como as organizações de saúde usam o Adobe Experience Platform para melhorar o envolvimento dos pacientes, simplificar a coordenação do atendimento e gerar melhores resultados de saúde.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: 8da82711-a783-488d-a0ed-070b33ecbbc4
source-git-commit: 0236bd326730ee9a0be621ee0e60ddc3d352410d
workflow-type: tm+mt
source-wordcount: '3818'
ht-degree: 0%

---

# Casos de uso da área de saúde

As organizações de saúde usam o Adobe Experience Platform para criar perfis unificados de pacientes e fornecer comunicações personalizadas e oportunas em todos os pontos de contato. Conectando dados clínicos, comportamentais e de preferência em um único local, as equipes de atendimento podem envolver os pacientes de maneira mais eficaz e, ao mesmo tempo, manter os mais altos padrões de privacidade e conformidade.

>[!IMPORTANT]
>Os casos de uso da área de saúde envolvem PHI (Protected Health Information, informações protegidas de saúde) sujeitas à HIPAA e a outras regulamentações aplicáveis. Antes de implementar qualquer um desses padrões, verifique se [!DNL Adobe Experience Platform] está provisionado como um serviço qualificado para HIPAA e se um BAA (Business Associate Agreement, contrato de parceiro comercial) está em vigor com a Adobe. As considerações técnicas em cada seção destacam os principais requisitos de conformidade, mas não são exaustivas. Trabalhe com suas equipes jurídicas, de conformidade e de segurança para validar sua implementação em relação a todos os requisitos normativos aplicáveis.

## Automação de Lembrete de Compromisso

Envie lembretes de compromisso personalizados por email, mensagem de texto e notificações por push com base nas preferências de comunicação e no tipo de compromisso de cada paciente. Os lembretes automatizados reduzem as consultas perdidas e mantêm os cronogramas em execução sem problemas, liberando a equipe para se concentrar no atendimento ao paciente.

### Impacto no negócio

As organizações que implementam lembretes de compromissos automatizados veem melhorias mensuráveis nas taxas de compromissos e uma redução significativa nos custos de não comparência.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). A criação de compromissos e os eventos de atualização do sistema de agendamento servem como acionadores naturais para mensagens de lembrete oportunas e relevantes. Esse é o padrão correto quando um evento de compromisso discreto é o acionador e a resposta necessária é uma única notificação com detecção de tempo, em vez de uma sequência de engajamento contínuo, já que os pacientes precisam de confirmação imediata sem etapas de acompanhamento.

### Considerações técnicas

- Garantir que todas as informações de contato do paciente e os detalhes da consulta sejam transmitidos e armazenados em conformidade com os requisitos da HIPAA, usando rótulos de uso de dados apropriados para restringir o acesso não autorizado.
- Integre-se ao sistema de programação de registros eletrônicos de saúde para capturar eventos de criação, cancelamento e reprogramação de compromissos em tempo real.
- Aplique políticas de gerenciamento de consentimento para que os lembretes só sejam enviados por canais em que o paciente tenha optado explicitamente.
- Configure regras de supressão para evitar lembretes duplicados ou excessivos quando os compromissos forem reagendados em sucessão rápida.


## Campanhas de adesão à medicação

Envie lembretes personalizados e conteúdo educacional para ajudar os pacientes a manter o controle de seus cronogramas de medicação e planos de tratamento. Mensagens personalizadas com base no tipo de medicamento, no cronograma de dosagem e no histórico do paciente promovem melhor adesão e melhores resultados de saúde.

### Impacto no negócio

Campanhas personalizadas de adesão à medicação ajudam a impulsionar melhorias nas taxas de adesão, levando a melhores resultados de saúde e menos reinternações hospitalares.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). A adesão à medicação requer uma abordagem contínua e multitoque com lembretes cada vez maiores, pontos de contato educacionais e check-ins de acompanhamento durante o curso de um plano de tratamento. Esse é o padrão correto porque o gerenciamento de medicamentos requer um fluxo sequenciado de várias mensagens em dias ou semanas com ramificação condicional baseada em eventos de reabastecimento e sinais de engajamento — uma única mensagem acionada não pode acomodar a lógica de dependência entre etapas educacionais e caminhos de encaminhamento.

### Considerações técnicas

- Aplique rótulos rigorosos de uso de dados a todas as informações de saúde protegidas relacionadas aos dados de medicação e diagnóstico para impedir a ativação downstream não autorizada.
- Integre-se aos sistemas de farmácia e registros eletrônicos de saúde para receber dados de preenchimento e recarga de prescrição que acionam etapas de jornada.
- Implemente um gerenciamento de consentimento robusto para garantir que os pacientes concordem em receber comunicações relacionadas a medicamentos e possam retirar o consentimento a qualquer momento.
- Projete a lógica de jornada para detectar padrões de não engajamento e encaminhe para notificações da equipe de atendimento quando um paciente estiver em risco de não aderir.


## Lembretes de cuidados preventivos

Lembrar proativamente os pacientes sobre os cuidados preventivos recomendados, como vacinas, exames preventivos e check-ups anuais com base na idade, histórico médico e fatores de risco. Lembretes de cuidados preventivos oportunos ajudam a fechar lacunas nos cuidados e melhorar a saúde geral da população.

### Impacto no negócio

O alcance pró-ativo dos cuidados preventivos resulta em melhores taxas de conclusão dos cuidados preventivos, contribuindo para melhorar a saúde da população e reduzir os custos de tratamento a longo prazo.

### Como implementar o

Use o padrão [Ativação de Mensagem de Saída em Lote](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md). Os lembretes de cuidados preventivos são melhor entregues por meio de campanhas em lote programadas que avaliam a elegibilidade do paciente em relação às diretrizes clínicas regularmente. Esse é o padrão correto quando o público-alvo é predefinido por critérios de diretrizes clínicas, o tempo de entrega é agendado em uma cadência regular em vez de ser orientado por eventos, e nenhuma ramificação ou decisão em tempo real é necessária.

### Considerações técnicas

- Crie segmentos de público-alvo usando critérios de diretrizes clínicas (idade, gênero, histórico familiar, datas de triagem anteriores) e, ao mesmo tempo, aplique rótulos de uso de dados a todas as informações de saúde protegidas usadas na segmentação.
- Coordenar com as equipes clínicas para garantir que o conteúdo de lembretes se alinhe às atuais diretrizes de cuidados preventivos baseadas em evidências e protocolos organizacionais.
- Implemente o limite de frequência para evitar sobrecarregar os pacientes que se qualificam para várias recomendações de cuidados preventivos simultaneamente.
- Mantenha uma trilha de auditoria de todas as comunicações de cuidados preventivos enviadas para relatórios normativos e documentação de medida de qualidade.


## Campanhas de acompanhamento pós-visita

Envie automaticamente pesquisas pós-visita, instruções de atendimento e lembretes de consulta de acompanhamento com base no tipo de visita e nas necessidades específicas de cada paciente. O acompanhamento em tempo hábil melhora a satisfação do paciente e garante a continuidade do atendimento após cada encontro.

### Impacto no negócio

As campanhas de acompanhamento automatizadas pós-visita alcançam melhores taxas de resposta de pesquisa e pontuações mais altas de satisfação do paciente.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Os eventos de conclusão de visitas do sistema de registros eletrônicos de saúde fornecem um acionador natural e oportuno para comunicações de acompanhamento personalizadas de acordo com o tipo de encontro. Esse é o padrão correto quando um evento de conclusão de visita discreta é o acionador e a resposta necessária é um acompanhamento imediato adaptado ao tipo de encontro, em vez de uma sequência de várias etapas, já que cada visita gera sua própria necessidade de acompanhamento independente.

### Considerações técnicas

- Integre-se ao sistema de registros eletrônicos de saúde para receber eventos de despejo de visitas que incluem o tipo de visita, o provedor e instruções relevantes de atendimento sem expor as anotações clínicas completas.
- Aplique rótulos de uso de dados a qualquer conteúdo de instrução sobre o tratamento para garantir que as informações protegidas de saúde sejam compartilhadas somente por canais seguros e autorizados pelo paciente.
- Configure regras de tempo que levem em conta o tipo de visita — por exemplo, acompanhamentos pós-cirúrgicos podem exigir um tempo diferente das pesquisas de check-up de rotina.
- Inclua links seguros no portal do paciente para a conclusão da pesquisa e agendamento de consultas, em vez de coletar informações de saúde por canais não seguros.


## Programas de gerenciamento de doenças crônicas

Personalize as comunicações de gerenciamento de doenças crônicas, o conteúdo educacional e os lembretes de monitoramento com base na condição e no plano de tratamento específicos de cada paciente. O engajamento sustentado e relevante ajuda os pacientes a ter um papel ativo no gerenciamento de sua saúde ao longo do tempo.

### Impacto no negócio

Programas personalizados de gerenciamento de doenças crônicas observam maiores taxas de engajamento no programa, resultando em melhores resultados no gerenciamento de doenças e menor utilização de cuidados de emergência.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). O gerenciamento de doenças crônicas é inerentemente uma experiência de longa duração com vários pontos de contato que requer mensagens adaptáveis com base no envolvimento do paciente e nos marcos de saúde. Este é o padrão correto porque o gerenciamento de doenças crônicas requer mensagens adaptáveis por um período estendido com ramificação condicional baseada em métricas clínicas e padrões de engajamento — as mensagens acionadas por eventos não podem lidar com a reavaliação contínua e dinâmica necessária para ajustar intervenções com base em dados de saúde em evolução.

### Considerações técnicas

- Projetar uma lógica de ramificação da jornada que se adapta com base em métricas específicas da condição (por exemplo, tendências de glicose no sangue para o tratamento do diabetes ou leituras da pressão arterial para programas de hipertensão).
- Implemente uma governança de dados rigorosa com rótulos de uso de dados [!DNL Adobe Experience Platform] para classificar e proteger dados de integridade específicos da condição em toda a jornada.
- Integre com dispositivos de monitoramento remoto de pacientes e sistemas de resultados relatados pelo paciente para alimentar dados de saúde em tempo real nos pontos de decisão da jornada.
- Crie caminhos de escalonamento da equipe de atendimento na jornada para que o não engajamento ou as tendências de saúde acionem alertas para a equipe clínica apropriada.


## Jornada de integração de novos pacientes

Automatize uma jornada de integração em várias etapas para novos pacientes, que inclui informações de boas-vindas, instruções de acesso ao portal do paciente e orientação de agendamento de consultas. Uma experiência de integração tranquila dá o tom para um relacionamento de longo prazo com o paciente.

### Impacto no negócio

As jornadas automatizadas de integração de novos pacientes ajudam a impulsionar melhorias nas taxas de ativação do portal e um engajamento antecipado mais forte dos pacientes.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). A integração do paciente é um processo naturalmente sequencial, em várias etapas, em que cada comunicação se baseia na anterior e se adapta caso o paciente tenha completado as ações principais. Esse é o padrão correto, pois a integração exige um fluxo sequenciado e dependente ao longo de vários dias com ramificação baseada nas ações do paciente (ativação do portal, conclusão do formulário) — uma única mensagem ou abordagem em lote não pode acomodar as interdependências entre as etapas ou se adaptar à conclusão progressiva.

### Considerações técnicas

- Integrar ao sistema de registro do paciente para acionar a jornada de integração imediatamente após a criação do novo registro do paciente, garantindo uma primeira impressão oportuna.
- Use a resolução de identidade para mesclar todos os registros pré-existentes (por exemplo, de uma visita ao site ou solicitação de compromisso) com o novo perfil do paciente para evitar comunicações duplicadas.
- Garanta que os links e as credenciais de ativação do portal sejam entregues por meio de canais seguros, compatíveis com HIPAA, e expirem após um período definido.
- Projete a jornada para detectar eventos de ativação do portal e de conclusão do formulário de modo que as etapas subsequentes se adaptem em vez de repetir as informações nas quais o paciente já atuou.


## Entrega de conteúdo de saúde personalizada

Forneça conteúdo personalizado de educação em saúde, dicas de bem-estar e recursos adaptados às condições, interesses e metas de saúde de cada paciente. O conteúdo relevante cria confiança, melhora a alfabetização em saúde e capacita os pacientes a tomar decisões informadas sobre seus cuidados.

### Impacto no negócio

A entrega personalizada de conteúdo de saúde atinge taxas mais altas de engajamento de conteúdo, levando a uma melhor educação do paciente e alfabetização em saúde.

### Como implementar o

Use a [Jornada entre canais com o padrão de decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). A entrega de conteúdo de saúde se beneficia da decisão em tempo real, que seleciona o conteúdo mais relevante para cada paciente com base em suas condições, preferências e envolvimento anterior, fornecido por meio de seu canal preferido. Esse é o padrão correto quando a seleção de conteúdo precisa levar em conta as condições do paciente, as preferências de consentimento e as preferências de canal, evitando a entrega duplicada ou fatigante — a orquestração de várias etapas sozinha não fornece a camada de decisão em tempo real necessária para corresponder o inventário de conteúdo dinâmico às necessidades individuais do paciente.

### Considerações técnicas

- Aplique classificação de conteúdo e rótulos de uso de dados a todos os materiais de educação em saúde para garantir que o conteúdo específico da condição seja entregue somente aos pacientes que consentiram em receber informações de saúde sobre esse tópico.
- Integrar o mecanismo de decisão a um repositório de conteúdo que é regularmente revisado e aprovado pelas equipes clínicas para garantir a precisão médica.
- Implemente regras de fadiga do conteúdo para evitar a entrega excessiva de conteúdo em um único tópico e para equilibrar o material educacional entre as várias necessidades de saúde de um paciente.
- Rastreie os sinais de envolvimento de conteúdo (aberturas, cliques, tempo gasto) para refinar continuamente a relevância do conteúdo sem coletar ou armazenar informações adicionais protegidas de integridade.


## Notificação de resultados do laboratório

Notifique os pacientes quando os resultados do laboratório estiverem disponíveis por meio de seu canal de comunicação preferido com mensagens personalizadas e seguras. A notificação imediata incentiva os pacientes a revisar os resultados rapidamente e acompanhar a equipe de atendimento quando necessário.

### Impacto no negócio

As notificações automatizadas de resultados de laboratório ajudam a aumentar as taxas de visualização de resultados, melhorando a comunicação com o paciente e permitindo um acompanhamento clínico mais rápido quando os resultados exigem ação.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). A disponibilidade dos resultados do laboratório é um evento distinto que requer uma notificação imediata e única através do canal preferido do paciente. Esse é o padrão correto quando um evento de resultado discreto de laboratório é o acionador e a resposta necessária é uma única notificação imediata — em vez de uma sequência de várias mensagens, já que os pacientes precisam de um alerta imediato para verificar seu portal sem comunicações adicionais de acompanhamento.

### Considerações técnicas

- Nunca inclua valores reais de resultados de laboratório em mensagens de notificação — notifique apenas o paciente de que os resultados estão disponíveis e direcione-os para o portal seguro do paciente para obter detalhes.
- Integre ao sistema de informações do laboratório para receber eventos prontos para resultados, aplicando rótulos rigorosos de uso de dados para evitar que quaisquer dados clínicos fluam para os canais de marketing.
- Implemente uma lógica de retenção do provedor para que as notificações só sejam enviadas depois que o médico responsável pelo pedido tiver revisado e divulgado os resultados para visualização do paciente.
- Garantir que todos os links de notificação apontem para sessões autenticadas e criptografadas do portal do paciente que atendam aos requisitos de segurança da HIPAA.


## Verificação de Cobertura de Seguro

Verificar e comunicar proativamente informações de cobertura de seguro aos pacientes antes de suas consultas para reduzir surpresas de faturamento e melhorar a experiência geral do paciente. A comunicação de cobertura clara e inicial cria confiança e reduz as disputas de faturamento pós-visita.

### Impacto no negócio

A verificação proativa da cobertura do seguro resulta em melhores taxas de confirmação da cobertura pré-visita e uma redução significativa nas disputas de cobrança e reclamações de pacientes.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Os eventos de agendamento de consultas servem como acionadores para iniciar a verificação de cobertura e comunicar os resultados ao paciente antes da visita. Esse é o padrão correto quando um evento de agendamento de compromisso discreto é o acionador e a resposta necessária é uma única notificação sobre cobertura sensível ao tempo, em vez de uma sequência de engajamento de várias etapas, já que o paciente precisa de uma mensagem clara antes da visita.

### Considerações técnicas

- Integre-se aos sistemas de verificação de qualificação de seguro para recuperar o status de cobertura em tempo real sem armazenar dados completos de solicitações de seguro na plataforma de dados do cliente.
- Aplique rótulos de uso de dados a todas as informações financeiras e de seguros para restringir seu uso somente a comunicações relacionadas a faturamento.
- Configure a sincronização da mensagem para permitir um prazo de entrega suficiente antes da consulta para que os pacientes resolvam quaisquer problemas de cobertura ou entrem em contato com o fornecedor do seguro.
- Inclua instruções claras e informações de contato para o departamento de faturamento, para que os pacientes possam fazer perguntas ou fornecer detalhes atualizados sobre o seguro antes de sua visita.


## Lembretes de Compromisso do Telehealth

Envie lembretes personalizados para compromissos de telessaúde que incluam instruções de conexão, dicas de preparação e informações de suporte técnico. Lembretes eficazes de telessaúde reduzem visitas virtuais perdidas e ajudam os pacientes a se sentirem confiantes usando ferramentas de atendimento digital.

### Impacto no negócio

Lembretes personalizados de consulta em telessaúde ajudam a impulsionar melhorias nas taxas de exibição de visitas virtuais e acelerar a adoção geral de telessaúde na população de pacientes.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Os eventos de agendamento de compromisso de telessaúde fornecem um acionador natural para lembretes oportunos que incluem detalhes de conexão e orientação de preparação. Este é o padrão correto quando um evento discreto de consulta de telessaúde é o acionador e a resposta necessária é um lembrete único e imediato com orientação técnica — em vez de uma sequência de várias etapas, uma vez que os pacientes precisam de instruções claras antes da consulta sem mensagens de acompanhamento subsequentes.

### Considerações técnicas

- Inclua instruções de conexão específicas da plataforma (desktop versus dispositivos móveis) com base nas preferências conhecidas do dispositivo do paciente ou nos dados de sessão de telesaúde anteriores.
- Garanta que todos os links de conexão e identificadores de sessão de teleintegridade sejam entregues por meio de canais criptografados compatíveis com HIPAA e expirem após a janela de compromisso agendada.
- Integrar com a plataforma de telessaúde para detectar quando um paciente se conectou com êxito para que as mensagens de lembrete secundárias possam ser suprimidas.
- Forneça um caminho de fallback para as informações de contato do suporte técnico para os pacientes que não se conectaram em uma janela definida antes da hora de início da consulta.


## Engajamento no programa de bem-estar

Personalize as comunicações, os desafios e as recompensas do programa de bem-estar com base nas metas de saúde, no nível de atividade e nas preferências de cada paciente. Programas de bem-estar envolventes motivam os pacientes a adotar hábitos mais saudáveis e manter o bem-estar a longo prazo.

### Impacto no negócio

As campanhas personalizadas de engajamento no programa de bem-estar atingem taxas maiores de participação no programa, contribuindo para melhores resultados de saúde e maior fidelidade do paciente.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Os programas de bem-estar são experiências de engajamento sustentado com vários marcos, desafios e pontos de contato de recompensa que exigem orquestração adaptativa com base na participação e no progresso do paciente. Este é o padrão correto porque os programas de bem-estar exigem um fluxo sequenciado de várias mensagens durante um longo período com ramificação condicional baseada em marcos de participação e padrões de engajamento — as mensagens acionadas por eventos não podem lidar com a orquestração adaptativa contínua necessária para ajustar desafios e recompensas com base no rastreamento contínuo do progresso.

### Considerações técnicas

- Integre com dispositivos vestíveis e feeds de dados de aplicativos de condicionamento físico, aplicando rótulos claros de uso de dados para distinguir dados de bem-estar de dados de saúde clínica sujeitos a requisitos regulatórios mais rigorosos.
- Implementar um gerenciamento de consentimento que permita aos pacientes conceder e revogar permissões para coleta de dados de bem-estar independentemente de suas preferências de comunicação clínica.
- Projetar uma lógica de jornada que ajuste a dificuldade de desafio e a frequência de comunicação com base nos padrões de engajamento de cada paciente para evitar desânimo ou fadiga.
- Garantir que o rastreamento de recompensas e incentivos esteja em conformidade com as normas aplicáveis da área de saúde em relação aos requisitos de incentivo e antirretorno do paciente.


## Coordenação da equipe de atendimento

Permitir a comunicação e a coordenação personalizadas entre os pacientes e os membros de sua equipe de atendimento com base no plano de atendimento e nas preferências individuais. Uma melhor coordenação leva a transições de cuidados mais perfeitas e melhores resultados para pacientes com necessidades de cuidados complexas.

### Impacto no negócio

Comunicações eficazes de coordenação da equipe de atendimento resultam em melhor envolvimento da equipe de atendimento e melhores resultados de coordenação de atendimento em planos de atendimento de vários provedores.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). A coordenação da equipe de atendimento envolve várias partes interessadas e fluxos de comunicação contínuos que devem se adaptar com base nos marcos do plano de atendimento, nas alterações do status do paciente e nas ações do provedor. Esse é o padrão correto porque a coordenação de cuidados requer fluxos de mensagens adaptáveis e em várias etapas que se ramificam com base nos marcos do plano de cuidados e nas ações do provedor em várias partes interessadas — uma única mensagem ou padrão mais simples não pode acomodar as interdependências complexas e o roteamento de mensagens baseado em funções necessários em equipes clínicas.

### Considerações técnicas

- Implemente controles de acesso com base em funções e rótulos de uso de dados para garantir que cada membro da equipe de atendimento receba apenas informações do paciente relevantes para sua função no plano de atendimento.
- Integre-se à gestão de cuidados e aos sistemas de registros eletrônicos de saúde para receber atualizações de planos de cuidados, conclusões de encaminhamento e eventos de transição de cuidados que acionam mensagens de coordenação.
- Projete caminhos de comunicação separados para mensagens direcionadas ao paciente e ao provedor, garantindo que a terminologia clínica seja usada adequadamente para os provedores, enquanto as mensagens do paciente permanecem claras e acessíveis.
- Manter uma trilha de auditoria completa de todas as comunicações de coordenação de cuidados para conformidade com as regulamentações de continuidade de cuidados e os requisitos de capacitação.


## Funnel de Jornada de pacientes e Análise de lacunas de atendimento

Mapeie a jornada completa do paciente desde a pesquisa inicial na Web até a programação de consulta, prestação de cuidados e acompanhamento para identificar onde os pacientes se desenvolvem e quais populações têm lacunas nos cuidados preventivos ou crônicos recomendados. Os sistemas de saúde que não têm visibilidade de jornadas entre canais não conseguem distinguir entre o atrito programado e o desengajamento do paciente — limitando sua capacidade de melhorar o acesso e fechar as lacunas de atendimento em escala.

### Impacto no negócio

Entender onde os pacientes abandonam as vias de atendimento e quais segmentos de membros têm a maior concentração de lacunas de atendimento permite que as equipes de gerenciamento de atendimento e marketing concentrem recursos de alcance nas populações e pontos de atrito que produzirão a maior melhoria na adesão ao atendimento.

### Como implementar o

Use o padrão [Customer Analytics &amp; Insight Generation](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md). Essa abordagem conecta dados comportamentais da Web e do portal, registros do sistema de compromissos e dados de solicitações de atendimento ao Customer Journey Analytics, onde a análise de fallout mede a queda em cada etapa de agendamento ou atendimento e a análise de coorte identifica quais segmentos de membro têm as taxas de adesão ao atendimento mais baixas. Esse é o padrão correto quando a meta é a geração de insight e a análise no nível da população — compreender onde as jornadas são detalhadas e quem está mais em risco — em vez de acionar o alcance externo ou ativar uma lista de supressão.

### Considerações técnicas

- Os dados de compromissos e declarações de sistemas clínicos devem ser mapeados para esquemas XDM compatíveis com a HIPAA antes da assimilação no AEP, e os rótulos de uso de dados devem ser aplicados para restringir o acesso a informações de saúde protegidas nas visualizações de dados da CJA.
- Os identificadores de pacientes ou membros no portal da Web, no sistema de agendamento e no EHR devem ser resolvidos como uma ID de pessoa consistente na conexão do CJA para produzir uma visualização de jornada coerente entre sistemas, sem duplicar indivíduos.
- A análise de lacuna de atendimento exige conjuntos de dados de pesquisa que codifiquem definições de diretrizes clínicas — como intervalos de triagem recomendados por idade e condição — para que campos derivados do CJA possam sinalizar membros que não concluíram o atendimento recomendado na janela de diretrizes.
- A análise de agendamento do funnel deve capturar sessões de agendamento concluídas e abandonadas, incluindo pontos de saída em fluxos de agendamento de várias etapas, para que os pontos de atrito estejam visíveis no nível da etapa, em vez de taxas de devolução agregadas.


## Personalization de conteúdo do portal do paciente

Personalize a experiência autenticada no portal do paciente, detectando o conteúdo de saúde, as ferramentas e os recursos mais relevantes com base no comportamento de navegação e no histórico de engajamento de cada paciente na sessão. Um portal que se adapte ao que um paciente está pesquisando ativamente — em vez de apresentar a mesma experiência estática para cada visitante — facilita aos pacientes encontrar o que precisam e incentiva um engajamento mais profundo com os recursos de saúde disponíveis.

### Impacto no negócio

Personalizar a experiência do portal do paciente com base no comportamento de engajamento melhora a descoberta de conteúdo e as taxas de conclusão de autoatendimento, ajudando os pacientes a navegar com mais confiança sem a necessidade de intervenção da equipe de atendimento.

### Como implementar o

Use o padrão [Recomendação Comportamental](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Os sinais comportamentais na sessão provenientes do portal autenticado — incluindo exibições de página de conteúdo, uso de ferramentas de saúde, participação em tópicos de perguntas frequentes e atividade de agendamento de compromissos — treinam um modelo de recomendação que exibe os recursos mais relevantes para cada paciente com base no que está explorando ativamente, sem a necessidade de dados clínicos como entrada. Esse é o padrão correto quando a personalização é orientada por sinais comportamentais implícitos em uma sessão autenticada e o objetivo é a classificação de relevância de um catálogo de conteúdo e recursos, em vez de decisões de elegibilidade controladas, que é mais apropriado quando os critérios clínicos precisam observar o que um paciente vê.

### Considerações técnicas

- Limite os sinais comportamentais usados para recomendações aos dados de interação do portal — exibições de conteúdo, uso de ferramentas e padrões de navegação — e implemente rótulos de uso de dados que impeçam que quaisquer interesses de integridade inferidos fluam fora da sessão do portal autenticada ou para canais de marketing.
- Implemente uma biblioteca de conteúdo com análise clínica como o pool de recomendações para que o modelo possa exibir apenas materiais de educação médica pré-aprovados, garantindo que cada recurso recomendado tenha sido validado quanto à precisão antes da implantação.
- Garantir que o sistema de recomendações atenda aos requisitos técnicos de proteção da HIPAA para o ambiente de portal autenticado, incluindo controles de tempo limite de sessão e registro de auditoria de qual conteúdo foi apresentado a cada paciente e quando.
- Fornecer aos pacientes controles visíveis para limpar o histórico de navegação no portal e recusar a personalização comportamental, mantendo a transparência e a confiança em como os dados de engajamento são usados na experiência do portal.

## Lembretes de Envolvimento e Compromisso do Paciente

Envie lembretes de compromisso personalizados, dicas de saúde e comunicações de acompanhamento do atendimento por meio de jornadas multicanais compatíveis com reconhecimento de consentimento. Os lembretes de compromisso personalizados e automatizados reduzem as taxas de não comparência, garantindo ao mesmo tempo que as comunicações estejam em conformidade com as regulamentações de privacidade da área de saúde e as preferências de consentimento do paciente.

### Impacto no negócio

As organizações de saúde com programas automatizados de lembrete de compromissos percebem reduções significativas nas taxas de não comparência e cancelamento tardio, melhorando a utilização da programação do provedor e os resultados de saúde do paciente por meio de uma melhor adesão aos compromissos.

### Como implementar o

Use o padrão [Mensagens Acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para responder a eventos de agendamento de compromisso com lembretes oportunos e personalizados cronometrados em intervalos ideais antes da data do compromisso. Esse é o padrão correto quando a comunicação é acionada por um evento específico de interação do paciente e a resposta é uma mensagem individualizada e sensível ao tempo, em vez de uma sequência de criação de várias semanas ou uma seleção complexa de ofertas.

### Considerações técnicas

- Todas as comunicações dos pacientes devem estar em conformidade com as normas de privacidade aplicáveis; o conteúdo das mensagens deve evitar incluir informações de saúde protegidas além do estritamente necessário para a comunicação.
- O gerenciamento do consentimento deve ser aplicado no nível do canal — os pacientes que não optaram por lembretes de SMS não devem receber textos, mesmo quando o SMS seria o canal de lembrete mais eficaz para sua demografia.
- A integração com o sistema de agendamento deve fornecer eventos de compromisso em tempo quase real para habilitar o tempo de lembrete preciso para o agendamento de compromisso real, incluindo reagendamentos e cancelamentos no mesmo dia.
- As sequências de lembrete multicanal devem incluir lógica de supressão para que os pacientes que confirmam sua consulta não continuem a receber mensagens de lembrete para essa consulta.
