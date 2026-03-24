---
title: Casos de uso de mídia e entretenimento
description: Descubra como as organizações de mídia e entretenimento usam o Adobe Experience Platform para personalizar a descoberta de conteúdo, reduzir a rotatividade do assinante e aumentar a participação do público.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: cfcf689f-9579-447f-9ef9-72e0c80c1f27
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '3363'
ht-degree: 0%

---

# Casos de uso de mídia e entretenimento

As organizações de mídia e entretenimento usam o Adobe Experience Platform para unificar os dados de público-alvo de plataformas de transmissão, bibliotecas de conteúdo e contas de assinantes em uma única visualização de cada visualizador ou ouvinte. Essa base permite a descoberta personalizada de conteúdo, a retenção proativa de assinantes e estratégias de engajamento que mantêm os públicos-alvo voltando para obter mais.

## Mecanismo de recomendação de conteúdo

Fornecer recomendações de conteúdo personalizado, incluindo filmes, programas de TV, músicas e artigos, com base no histórico de visualização e escuta, nas preferências e no comportamento do usuário semelhante. Quando os públicos-alvo veem conteúdo adaptado aos seus interesses, eles gastam mais tempo explorando o catálogo e descobrem títulos que, de outra forma, teriam perdido.

### Impacto no negócio

As organizações que implantam mecanismos de recomendação de conteúdo personalizado percebem um envolvimento aprimorado com o conteúdo e um aumento significativo no tempo total de observação ou escuta por usuário.

### Como implementar o

Use o padrão [Recomendação Comportamental](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Essa abordagem usa modelos de recomendação orientados por IA que aprendem continuamente com as interações do público-alvo para exibir o conteúdo mais relevante para cada indivíduo. Esse é o padrão correto quando o conjunto de itens é grande e muda continuamente (catálogos de conteúdo) e a seleção é orientada por afinidade comportamental aprendida ao visualizar o histórico, em vez de um conjunto limitado de ofertas regido por regras de elegibilidade.

### Considerações técnicas

- Os metadados do catálogo de conteúdo, incluindo gênero, elenco, diretor, tags de humor e classificações de conteúdo, devem ser assimilados e mantidos atualizados para garantir que as recomendações reflitam a amplitude completa de títulos disponíveis.
- A visualização e a escuta de sinais precisam fluir em tempo quase real para que as recomendações sejam atualizadas em uma única sessão de navegação enquanto um usuário assiste ou ignora o conteúdo.
- Os modelos de recomendação exigem uma estratégia de partida a frio para novos assinantes que não têm histórico de visualização, normalmente recorrendo a conteúdo com curadoria editorial ou popular regionalmente.
- As janelas de disponibilidade e licenciamento de conteúdo devem ser fatoradas na lógica de recomendação para que os usuários nunca sejam títulos recomendados que estejam indisponíveis em sua região ou que tenham sido removidos do catálogo.


## Prevenção de Churn de Assinatura

Identifique os assinantes que correm o risco de cancelar e envolva-os com recomendações de conteúdo personalizadas, ofertas e campanhas de retenção. A manutenção de assinantes existentes é muito mais econômica do que a aquisição de novos, e um alcance pró-ativo no momento certo pode evitar uma parte significativa dos cancelamentos.

### Impacto no negócio

Programas eficazes de prevenção de churn oferecem reduções significativas no churn do assinante, protegendo a receita recorrente e melhorando o valor do público-alvo de longo prazo.

### Como implementar o

Use a [Jornada entre canais com o padrão de decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). Essa abordagem combina a orquestração de jornadas com a decisão em tempo real para selecionar a melhor oferta de retenção ou recomendação de conteúdo para cada assinante em risco em cada canal. Esse é o padrão correto quando a jornada deve coordenar a entrega entre canais para evitar ofertas de retenção duplicadas e quando a seleção de ofertas exige regras de elegibilidade com base no valor do assinante e no nível de risco — a orquestração de várias etapas sozinha não fornece a camada de decisão em tempo real necessária.

### Considerações técnicas

- A pontuação de risco de churn deve incorporar sinais de engajamento, como tempo de observação decrescente, frequência de logon reduzida e quedas de conclusão de conteúdo para identificar assinantes em risco antes que eles cheguem à página de cancelamento.
- As ofertas de retenção devem ser hierarquizadas com base no valor do assinante e no nível de risco, variando de destaques de conteúdo personalizado a extensões de plano com desconto, para equilibrar a proteção da receita com o impacto da margem.
- A jornada deve suprimir as mensagens de retenção para assinantes que já renovaram ou atualizaram, o que requer integração em tempo real com o sistema de cobrança de assinaturas.
- As regras de decisão do [!DNL Journey Optimizer] devem levar em conta o tipo de plano, a duração e o histórico de resgate de ofertas passadas do assinante para evitar a apresentação de ofertas que se pareçam genéricas ou repetitivas.


## Notificações de lançamento de novo conteúdo

Notifique os assinantes sobre novas versões de conteúdo que correspondem a suas preferências e histórico de exibição. Notificações oportunas sobre conteúdo novo impulsionam engajamento imediato e lembram os assinantes do valor contínuo de suas assinaturas.

### Impacto no negócio

As notificações de versão personalizadas impulsionam o envolvimento aprimorado de novos conteúdos na primeira semana de lançamento, acelerando as visualizações e impulsionando as métricas de desempenho do conteúdo.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Essa abordagem responde aos eventos de lançamento de conteúdo, comparando novos títulos com perfis de preferência do assinante para fornecer notificações oportunas e relevantes. Esse é o padrão correto quando o acionador é um evento do sistema (versão de conteúdo) em vez do comportamento do cliente, e a comunicação necessária é imediata e reativa em vez de uma sequência de criação contínua.

### Considerações técnicas

- Os calendários de lançamento de conteúdo devem ser integrados para que as notificações possam ser agendadas ou acionadas no momento em que novos títulos forem disponibilizados, evitando alertas prematuros sobre conteúdo que ainda não está acessível.
- A correspondência de preferência do assinante deve considerar várias dimensões, incluindo afinidade de gênero, atores ou diretores favoritos, séries assistidas anteriormente e interesses de franquias, para garantir que as notificações se sintam pessoalmente relevantes.
- O volume de notificações deve ser gerenciado com cuidado por meio do limite de frequência para evitar que os assinantes se sintam sobrecarregados durante períodos de lançamentos de conteúdo pesado.
- O fuso horário e a visualização de dados de hábito devem informar o tempo de delivery para que as notificações cheguem quando cada assinante tiver mais probabilidade de se envolver, em vez de em um único horário de envio global.


## Experiência personalizada de página inicial

Personalize dinamicamente as páginas inicial e de descoberta de conteúdo para mostrar primeiro o conteúdo mais relevante com base no perfil e no comportamento de cada usuário. Quando os visualizadores veem o conteúdo alinhado a seus gostos imediatamente após abrirem o aplicativo, eles se engajam mais rápido e navegam por mais tempo.

### Impacto no negócio

Experiências personalizadas de página inicial promovem um melhor engajamento da página inicial e melhoram significativamente a descoberta de conteúdo, especialmente em plataformas com bibliotecas de conteúdo grandes e crescentes.

### Como implementar o

Use o padrão [Recomendação Comportamental](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Essa abordagem usa estratégias de seleção e modelos de classificação para reordenar linhas de conteúdo e títulos em destaque na página inicial com base no perfil de cada visitante e no comportamento em tempo real. Esse é o padrão correto quando o conjunto de itens é grande e muda continuamente, e a seleção é orientada por afinidade comportamental para classificar linhas de conteúdo dinamicamente, em vez de um conjunto estático preparado ou personalização baseada em atributos simples.

### Considerações técnicas

- A personalização da página inicial deve ser executada com rapidez suficiente para evitar atrasos de carga perceptíveis; a decisão baseada em borda ou a renderização no lado do servidor geralmente são necessárias para atender às expectativas de tempo de resposta em subsegundos.
- A lógica de personalização deve mesclar preferências individuais com prioridades editoriais e promocionais, garantindo que as versões de pré-lançamento, o conteúdo sazonal e os títulos promovidos por parceiros ainda recebam visibilidade apropriada.
- Estratégias de linhas de conteúdo, como &quot;Continuar assistindo&quot;, &quot;Porque você assistiu&quot; e &quot;Em tendência agora&quot;, exigem entradas de dados distintas e lógica de classificação que devem ser orquestradas em um layout de página coeso.
- A implementação do Web SDK [!DNL Experience Platform] deve capturar as interações da página inicial, incluindo rolagens de linha, cliques em blocos e comportamento de passar o mouse, para refinar continuamente os modelos de classificação.


## Lembretes da Lista de Interesse e Favoritos

Envie lembretes aos usuários sobre o conteúdo em sua lista de observação que eles ainda não assistiram, juntamente com recomendações personalizadas para títulos semelhantes. As listas de observação representam sinais de intenção fortes, e lembretes suaves podem converter essa intenção em visualização real.

### Impacto no negócio

Os programas de lembrete da lista de observação geram taxas de conclusão da lista de observação aprimoradas, transformando o propósito salvo em envolvimento ativo e aumentando o uso geral da plataforma.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Essa abordagem aciona lembretes com base na atividade da lista de observação e em sinais de inatividade, enviando toques oportunos quando o conteúdo foi salvo, mas ainda não foi iniciado. Este é o padrão correto quando um sinal comportamental discreto (inatividade da lista de observação) é o acionador e a resposta necessária é uma única mensagem sensível ao tempo, em vez de uma sequência de várias etapas ou um fluxo de recomendação contínuo.

### Considerações técnicas

- O tempo do lembrete deve ser calibrado com base no tempo em que o conteúdo está na lista de observação e se o usuário esteve ativo na plataforma recentemente, evitando lembretes durante períodos de grande engajamento quando são desnecessários.
- Os dados da lista de observação devem ser sincronizados entre os dispositivos em tempo real para que um título adicionado aos dispositivos móveis seja refletido imediatamente nos cálculos de qualificação de lembrete e não duplicado entre as plataformas.
- Os lembretes devem destacar detalhes contextuais, como janelas de disponibilidade que expiram ou novas estações das séries salvas, para criar urgência natural sem se sentir pressionado.
- O conteúdo que foi removido do catálogo ou que não está mais disponível na região do assinante deve ser automaticamente excluído das mensagens de lembrete e substituído por recomendações alternativas.


## Campanhas de conversão de avaliação gratuita

Envolva usuários de avaliação gratuita com recomendações e ofertas de conteúdo personalizado para incentivar a conversão de assinaturas antes do término do período de avaliação. A janela de avaliação é uma oportunidade essencial para demonstrar o valor suficiente que os usuários estão dispostos a pagar, e uma jornada de conversão estruturada supera significativamente um único lembrete de fim de avaliação.

### Impacto no negócio

Campanhas de conversão de avaliação bem projetadas oferecem melhorias significativas nas taxas de conversão de avaliação para pagamento, aumentando diretamente a eficiência da aquisição do assinante e reduzindo o custo por aquisição.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md). Essa jornada de nutrição multitoque orienta os usuários de avaliação por meio de uma sequência de descoberta de conteúdo, demonstração de valor e mensagens de conversão, adaptando-se com base em seu envolvimento durante a avaliação. Esse é o padrão correto quando o caso de uso exige um fluxo sequenciado de várias mensagens ao longo de dias com ramificação condicional com base em eventos de engajamento e tempo de avaliação restante — uma única mensagem acionada não pode acomodar a lógica de dependência entre as etapas ou a necessidade de ajustes de cadência.

### Considerações técnicas

- A jornada deve rastrear as datas de início e término da avaliação com precisão, com uma lógica de ramificação que ajusta a cadência de mensagens com base nos dias de avaliação restantes e nos níveis de engajamento observados.
- As recomendações de conteúdo na jornada devem priorizar os títulos mais envolventes e exclusivos da plataforma para maximizar o valor percebido de uma assinatura paga durante a janela de avaliação limitada.
- Os usuários que convertem antes do fim da avaliação devem ser movidos automaticamente da jornada de conversão para um novo fluxo de boas-vindas do assinante, impedindo o envio contínuo de mensagens focadas em avaliação.
- As condições de jornada do [!DNL Journey Optimizer] devem levar em conta o tipo de plano de avaliação, a fonte de referência e o uso do dispositivo para adaptar a abordagem de conversão para diferentes segmentos de público-alvo.


## Lembretes de exibição de evento ao vivo

Notifique os usuários sobre eventos futuros ao vivo, jogos esportivos ou estreias que correspondam a seus interesses e seu histórico de exibição. O conteúdo ao vivo orienta a visualização de compromissos, o que fortalece os hábitos do assinante, e os lembretes oportunos garantem que os públicos-alvo não percam os eventos importantes para eles.

### Impacto no negócio

Lembretes de eventos ao vivo personalizados promovem uma melhor visualização do evento ao vivo, maximizando o público-alvo para uma programação em tempo real de alto valor.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Essa abordagem aciona notificações com base nos dados do cronograma do evento, comparando eventos futuros com perfis de interesse do assinante para fornecer lembretes oportunos. Esse é o padrão correto quando o acionador é um evento do sistema (programação de eventos) em vez do comportamento do cliente, e a comunicação necessária é imediata e vinculada ao tempo, em vez de uma sequência de criação contínua.

### Considerações técnicas

- Os dados do cronograma do evento, incluindo horas de início, equipes ou talentos participantes e detalhes da transmissão, devem ser assimilados dos sistemas de programação e mantidos atualizados para lidar com alterações ou cancelamentos de agendamento de última hora.
- O tempo de entrega do lembrete deve levar em conta os fusos horários e os prazos de entrega pré-evento típicos; um lembrete enviado muito cedo é esquecido, enquanto um enviado muito tarde perde o início.
- A correspondência de interesses deve incorporar preferências explícitas, como equipes ou gêneros favoritos, e sinais implícitos, como padrões de visualização de eventos ao vivo anteriores, para identificar eventos relevantes para cada assinante.
- A coordenação de notificação de vários dispositivos é importante para que um assinante não receba lembretes redundantes em seu telefone, tablet e TV inteligente simultaneamente.


## Geração de lista de reprodução personalizada

Gera e atualiza automaticamente listas de reprodução personalizadas com base no histórico de escuta, preferências e indicadores de humor de cada usuário. Listas de reprodução com curadoria reduzem o esforço de seleção de conteúdo e mantêm os ouvintes envolvidos por sessões mais longas.

### Impacto no negócio

A geração de listas de reprodução personalizadas aumenta o engajamento das listas de reprodução e estende significativamente a duração média da sessão de escuta, fortalecendo os hábitos diários de uso da plataforma.

### Como implementar o

Use o padrão [Recomendação Comportamental](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Essa abordagem usa modelos orientados por IA que analisam os padrões de escuta, ignoram o comportamento e sinais contextuais para gerar e atualizar listas de reprodução personalizadas para cada usuário. Este é o padrão correto quando o conjunto de itens é grande e muda continuamente e a seleção é impulsionada pela afinidade comportamental da história de escuta e sinais de humor — em vez de um conjunto limitado de listas de reprodução regidas por regras editoriais.

### Considerações técnicas

- Os metadados do catálogo de música, incluindo ritmo, gênero, tags de humor, relacionamentos de artistas e recursos de áudio, devem ser marcados com riqueza para permitir a curadoria de listas de reprodução nuanceadas, que vai além da simples correspondência de gêneros.
- A frequência de atualização da lista de reprodução deve equilibrar a atualização com a familiaridade; os ouvintes esperam novas descobertas, mas também querem rever os favoritos, então os modelos devem combinar exploração com conforto.
- Sinais contextuais, como hora do dia, dia da semana e dispositivo de escuta, podem informar o humor da lista de reprodução e o nível de energia, criando listas de reprodução que se sentem apropriadas para o momento.
- [!DNL Experience Platform] dados comportamentais devem capturar eventos de escuta granulares, incluindo ignoradas, repetições, salvamentos e duração da sessão para refinar continuamente os modelos de recomendação.


## Sincronização de conteúdo entre plataformas

Ofereça uma experiência perfeita de conteúdo em todos os dispositivos sincronizando o histórico, as preferências e as recomendações do monitor em tempo real. Os visualizadores esperam fazer uma pausa em um dispositivo e retomá-lo em outro sem perder seu lugar, e uma experiência consistente em todas as plataformas reforça os hábitos de uso diário.

### Impacto no negócio

A sincronização de conteúdo entre plataformas aumenta o engajamento entre dispositivos e reduz significativamente o atrito que pode levar ao abandono da sessão quando os usuários alternam entre dispositivos.

### Como implementar o

Use o padrão [Personalization de Aplicativo/Web de Visitante Conhecido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md). Essa abordagem personaliza a experiência dos usuários identificados nas plataformas da Web e do aplicativo, garantindo um estado de conteúdo e recomendações consistentes, independentemente do dispositivo. Esse é o padrão correto quando a personalização é orientada por atributos de perfil (identidade entre dispositivos, estado de progresso da observação) e associação de segmento, em vez de um modelo de afinidade comportamental ou uma sequência de orquestração de jornada.

### Considerações técnicas

- A resolução de identidade entre dispositivos deve vincular de forma confiável as sessões de usuário em TVs inteligentes, aplicativos móveis, tablets e navegadores da Web para manter um único perfil unificado para cada assinante.
- Os dados de progresso do relógio, incluindo a posição exata de reprodução, o status de conclusão do episódio e as preferências de legenda ou trilha de áudio, devem ser sincronizados com latência mínima para fornecer uma experiência de retomada realmente contínua.
- Os modelos de recomendação devem levar em conta o contexto do dispositivo, pois as preferências de conteúdo podem diferir entre uma sessão de deslocamento móvel e uma sessão noturna da sala de estar em uma tela grande.
- As políticas de mesclagem de perfis do [!DNL Real-Time Customer Data Platform] devem ser configuradas para lidar com sessões simultâneas em vários dispositivos sem criar atualizações de estado conflitantes.


## Personalization de compartilhamento social

Personalize os prompts de compartilhamento social e as recomendações com base nas conexões sociais e preferências de conteúdo de cada usuário. Tornar fácil e atraente para os espectadores compartilhar o que amam transforma assinantes satisfeitos em defensores orgânicos que impulsionam a conscientização e aquisição.

### Impacto no negócio

O compartilhamento social personalizado incentiva a alcançar melhores taxas de compartilhamento social, amplificando o alcance orgânico e reduzindo os custos de aquisição pagos.

### Como implementar o

Use o padrão [Personalization de Aplicativo/Web de Visitante Conhecido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md). Essa abordagem personaliza experiências de compartilhamento no aplicativo para usuários identificados, encontrando prompts de compartilhamento contextualmente relevantes com base nas preferências do usuário e nos padrões de engajamento. Esse é o padrão correto quando a personalização é orientada por atributos de perfil e contexto de envolvimento conhecido, em vez de um modelo de afinidade comportamental, e o objetivo é aprimorar a experiência no momento sem orquestrar uma sequência de jornadas.

### Considerações técnicas

- Os prompts de compartilhamento devem ser acionados em momentos naturais de prazer, como completar uma série digna de farra ou descobrir um novo artista favorito, em vez de em intervalos arbitrários que se sintam intrusivos.
- As mensagens e imagens de compartilhamento pré-preenchidas devem ser geradas dinamicamente com base no conteúdo específico que está sendo compartilhado, incluindo miniaturas, descrições e deep links apropriados que direcionam os recipients de volta à plataforma.
- Os controles de privacidade devem garantir que a atividade de visualização só seja compartilhada quando o usuário iniciar explicitamente o compartilhamento. O compartilhamento passivo ou automático do histórico do relógio sem consentimento pode prejudicar a confiança.
- A integração da plataforma social deve estar em conformidade com as políticas de compartilhamento de cada rede e lidar com autenticação, limites de taxa e requisitos de formato de conteúdo para plataformas como Instagram, TikTok e X.


## Venda adicional de recursos premium

Identifique usuários que se beneficiariam de recursos premium e apresente ofertas de venda adicional personalizadas com base em seus padrões de uso. As mensagens de venda adicional direcionadas para usuários que já demonstram comportamentos alinhados ao valor premium são muito mais eficazes do que as campanhas de atualização em aberto.

### Impacto no negócio

As campanhas de venda adicional premium personalizadas promovem uma melhor adoção de recursos premium, aumentando a receita média por usuário e fornecendo recursos que realmente atendem às necessidades do assinante.

### Como implementar o

Use o padrão [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). Essa abordagem usa uma lógica de decisão centralizada para avaliar os padrões de uso de cada assinante e selecionar a oferta premium mais relevante no momento certo. Esse é o padrão correto quando a seleção da oferta deve levar em conta as restrições do padrão de uso e as regras de elegibilidade da camada premium — restrições que exigem lógica de decisão controlada em vez de classificação de afinidade comportamental sozinha.

### Considerações técnicas

- A análise de padrão de uso deve identificar comportamentos específicos que indiquem uma prontidão superior, como o uso frequente de recursos disponíveis de forma limitada no plano básico, o uso de vários dispositivos ou o alto volume de consumo de conteúdo.
- A apresentação da oferta deve destacar os benefícios premium específicos mais relevantes para o comportamento de cada usuário, em vez de listar todos os recursos premium genericamente; um usuário que baixa conteúdo com frequência deve ver a exibição offline enfatizada.
- O tempo de venda adicional deve evitar momentos de frustração, como imediatamente após um bloco de paywall, e, em vez disso, aproveitar momentos de engajamento positivo quando o assinante é mais receptivo.
- As regras de decisão do [!DNL Journey Optimizer] devem coordenar as ofertas de venda adicional nas mensagens no aplicativo, emails e notificações por push para apresentar uma oferta consistente sem sobrecarregar o assinante nos canais.


## Campanhas de conclusão de conteúdo

Lembre os usuários de terminarem de assistir ou ouvir o conteúdo que começaram, mas não concluíram, acompanhado de recomendações personalizadas sobre o que aproveitar em seguida. O conteúdo incompleto representa engajamento não realizado e uma leve cutucada geralmente converte uma sessão abandonada em uma experiência concluída.

### Impacto no negócio

As campanhas de conclusão de conteúdo promovem taxas de conclusão de conteúdo aprimoradas, aumentando o tempo total de engajamento e fortalecendo a percepção do assinante sobre o valor da plataforma.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Essa abordagem aciona lembretes com base em eventos de abandono de conteúdo, enviando mensagens oportunas quando um usuário pausa parcialmente em um título e não retorna em uma janela definida. Esse é o padrão correto quando um sinal comportamental discreto (abandono de conteúdo) é o acionador e a resposta necessária é uma única mensagem com reconhecimento de tempo com contexto, em vez de uma jornada de várias etapas ou seleção de oferta dinâmica.

### Considerações técnicas

- Os limites de abandono devem ser calibrados por tipo de conteúdo; um filme pausado na marca de 80% é um forte candidato a conclusão, enquanto um podcast interrompido após dois minutos pode indicar desinteresse em vez de escuta interrompida.
- As mensagens de lembrete devem incluir o título do conteúdo específico, uma miniatura visual e um deep link direto que retoma a reprodução no ponto exato em que o usuário parou.
- O limite de frequência deve evitar lembretes excessivos para os usuários que rotineiramente coletam amostras de conteúdo sem finalizar; empurrões repetidos para o conteúdo que um usuário optou por abandonar podem parecer intrusivos.
- A disponibilidade do conteúdo deve ser verificada no momento do envio, já que os títulos podem deixar a plataforma ou alterar regiões de disponibilidade entre o evento de abandono e o delivery de lembrete.


## Análise do driver de churn do assinante e do engajamento no conteúdo

Identifique quais padrões de consumo de conteúdo, alterações de frequência de engajamento e comportamentos de interação de catálogo precedem o cancelamento do assinante e meça como a afinidade de conteúdo varia entre os segmentos do assinante e os coortes de aquisição. Empresas de transmissão e publicação que não podem conectar o comportamento do conteúdo aos resultados de churn fazem com que as decisões de investimento em conteúdo baseadas em exibições agregadas sejam contadas em vez do impacto sobre a retenção.

### Impacto no negócio

Correlacionar os padrões de engajamento de conteúdo com os resultados de retenção do assinante fornece às equipes de produto, estratégia de conteúdo e marketing uma base fatual para priorizar investimentos em catálogos e projetar campanhas de reengajamento em torno dos comportamentos que realmente sustentam as assinaturas.

### Como implementar o

Use o padrão [Customer Analytics &amp; Insight Generation](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md). Essa abordagem conecta os dados do evento de transmissão, os metadados do conteúdo, os registros do ciclo de vida da assinatura e o histórico de interação da campanha ao Customer Journey Analytics, onde a análise de retenção de coorte mede como a afinidade do conteúdo se correlaciona com a estabilidade do assinante e a análise de fallout identifica os padrões de devolução de engajamento que precedem o cancelamento. Esse é o padrão correto quando o objetivo é entender os fatores comportamentais de churn e desempenho do conteúdo — em vez de acionar uma mensagem de retorno ou ativar um público-alvo de risco de churn para supressão.

### Considerações técnicas

- Os eventos de consumo de conteúdo devem incluir identificadores de conteúdo e metadados em nível de sessão — eventos de início, pausa, conclusão e ignorar — para que a profundidade do engajamento possa ser medida além das contagens brutas de reprodução no CJA.
- Os eventos do ciclo de vida da assinatura, incluindo início da avaliação, conversão, falha de pagamento, downgrade e cancelamento, devem ser assimilados como eventos discretos com carimbos de data e hora precisos para que as janelas comportamentais de pré-cancelamento possam ser definidas com precisão nos filtros do CJA.
- Os atributos do catálogo de conteúdo, como gênero, formato, associação de séries e recenticidade de versão, devem estar disponíveis como um conjunto de dados de pesquisa na conexão do CJA, para que a análise de envolvimento de conteúdo possa ser dividida pela dimensão do catálogo, em vez de exigir análise no nível de título individual.
- A análise de coorte que compara as curvas de retenção por canal de aquisição e conteúdo original visualizado exige que a origem de aquisição e o conteúdo visualizado pela primeira vez sejam capturados como dimensões de perfil ou de primeiro evento, disponíveis para definição de coorte no CJA.
