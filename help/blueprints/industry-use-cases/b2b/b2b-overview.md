---
title: Casos de uso B2B
description: Descubra como as organizações B2B usam o Adobe Experience Platform para acelerar o pipeline, melhorar a qualidade dos leads e impulsionar a expansão do cliente.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '2269'
ht-degree: 1%

---


# Casos de uso B2B

As organizações B2B usam o Adobe Experience Platform para unificar dados de conta e nível de pessoa, permitindo que as equipes de marketing e vendas forneçam experiências coordenadas e relevantes em cada estágio da jornada de compra. Da aceleração do pipeline à expansão do cliente, esses casos de uso mostram como as equipes B2B transformam dados complexos em resultados mensuráveis para os negócios.

>[!NOTE]
>
>Para blueprints de arquitetura específicos B2B, incluindo ativação baseada em conta e gerenciamento de grupos de compra, consulte os [blueprints de ativação e marketing B2B](/help/blueprints/b2b/overview.md).

## Account-Based Marketing Personalization

Personalize as comunicações de marketing e o conteúdo das contas do público-alvo com base no perfil da conta, no histórico de engajamento e nos sinais de compra. Ao alinhar as mensagens ao contexto exclusivo de cada conta, as equipes de marketing podem superar o ruído e envolver as partes interessadas certas com o conteúdo certo.

### Impacto no negócio

As organizações que implementam personalização de marketing baseada em conta normalmente observam um aumento de 30 a 40% na taxa de envolvimento da conta, impulsionando um pipeline mais forte e uma progressão mais rápida dos negócios.

### Como implementar o

Use o padrão [B2B Audience Activation](/help/blueprints/use-case-patterns/audience-building-activation/b2b-audience-activation.md) para criar públicos-alvo no nível da conta e ativar conteúdo personalizado em todos os canais. Esse padrão é criado especificamente para estratégias baseadas em conta, oferecendo suporte para direcionamento no nível da conta e da pessoa.

### Considerações técnicas

- Integre os dados do CRM (por exemplo, [!DNL Salesforce] ou [!DNL Microsoft Dynamics]) para manter hierarquias de conta atualizadas, estágios de oportunidade e atribuições de propriedade.
- Configure esquemas de perfil no nível da conta para capturar atributos firmográficos, como setor, contagem de funcionários, intervalo de receita e pilha de tecnologia.
- Mapeie os relacionamentos entre pessoas e contas para garantir que os sinais de engajamento individuais atinjam a pontuação e a segmentação no nível da conta.
- Coordene com o [!DNL Marketo Engage] para alinhar campanhas de automação de marketing a públicos de contas orientados por plataforma.


## Pontuação e criação de leads

Pontuar leads automaticamente com base nos dados e no comportamento do perfil, e depois direcionar leads de alta pontuação para vendas com campanhas de nutrição personalizadas para outras pessoas. Essa abordagem garante que as equipes de vendas se concentrem nas oportunidades mais promissoras, enquanto o marketing continua a desenvolver clientes potenciais em estágio anterior.

### Impacto no negócio

As empresas que implementam pontuação comportamental de leads e criação automatizada normalmente atingem um aumento de 25 a 35% na conversão de lead em oportunidade, acelerando a velocidade do pipeline e melhorando a produtividade das vendas.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para projetar jornadas de criação de ramificações que respondam a alterações de pontuação de clientes potenciais e acionadores comportamentais. Esse padrão suporta a lógica condicional necessária para rotear leads entre os controles de nutrição e workflows de entrega de vendas.

### Considerações técnicas

- Estabeleça uma sincronização de CRM bidirecional (por exemplo, [!DNL Salesforce] ou [!DNL Microsoft Dynamics]) para que as pontuações dos clientes potenciais e os status de qualificação permaneçam consistentes entre os sistemas de marketing e vendas.
- Defina as dimensões de pontuação demográfica (função, tamanho da empresa, setor) e comportamental (downloads de conteúdo, participação em webinários, visitas à página do produto).
- Coordenar modelos de pontuação de clientes potenciais com [!DNL Marketo Engage] para evitar pontuações conflitantes entre plataformas.
- Defina as regras de declínio de pontuação para garantir que os leads que ficam quietos sejam priorizados ao longo do tempo.


## Personalization de conteúdo para clientes potenciais

Personalizar conteúdo, recursos e ofertas do site com base no setor, na função, no tamanho da empresa e no histórico de engajamento do cliente potencial. Quando os clientes potenciais veem conteúdo relevante para sua situação específica, eles se envolvem mais profundamente e navegam pelo funnel com mais rapidez.

### Impacto no negócio

As organizações B2B que personalizam as experiências da Web para clientes potenciais conhecidos normalmente observam um aumento de 20 a 30% no envolvimento de conteúdo, resultando em pipeline mais qualificado e ciclos de vendas mais curtos.

### Como implementar o

Use o padrão [Personalization de Aplicativo/Web de Visitante Conhecido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) para fornecer experiências de conteúdo personalizadas com base em perfis de prospecto unificados. Esse padrão aproveita os dados do perfil em tempo real para fornecer os recursos, estudos de caso e planos de ação mais relevantes para cada visitante.

### Considerações técnicas

- Implemente a resolução de identidades para corresponder o comportamento de navegação anônimo com registros de prospecto conhecidos depois de autenticar ou enviar um formulário.
- Defina regras de personalização com base nos atributos no nível da conta (setor, segmento, estágio de negociação), bem como atributos no nível individual (função, consumo de conteúdo anterior).
- Integre com seu sistema de gerenciamento de conteúdo para trocar dinamicamente banners originais, recomendações de recursos e planos de ação.
- Verifique se os feeds de dados de rastreamento web do [!DNL Marketo Engage] estão no perfil unificado para obter uma imagem comportamental completa.


## Inscrição no evento e acompanhamento

Automatize confirmações, lembretes e acompanhamento pós-evento personalizados de registro de eventos com base no tipo de evento e no perfil do participante. Isso mantém os clientes potenciais envolvidos antes, durante e após os eventos, liberando a equipe de marketing da coordenação manual.

### Impacto no negócio

Os fluxos de trabalho automatizados e personalizados de comunicação de eventos geralmente geram um aumento de 40 a 50% na participação no evento, maximizando o retorno sobre o investimento e fortalecendo os relacionamentos com clientes em potencial.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para orquestrar o ciclo de vida completo do evento, desde o registro até a criação pós-evento. Esse padrão oferece suporte a acionadores com base em tempo, ramificação condicional por tipo de evento e sequências de acompanhamento de vários canais.

### Considerações técnicas

- Integre dados de registro de plataformas de webinário (por exemplo, [!DNL ON24], [!DNL Zoom Webinar]) e sistemas de evento presenciais no perfil unificado.
- Capture sinais de presença e engajamento (duração da sessão, perguntas feitas, respostas da enquete) para personalizar as mensagens de acompanhamento.
- Coordene jornadas de eventos com os status do programa [!DNL Marketo Engage] para manter a consistência dos relatórios entre sistemas.
- Crie ramificações de jornada separadas para inscritos que participaram e não participaram, com conteúdo personalizado para cada um.


## Campanhas de conversão de avaliação de produto

Envolva usuários de avaliação com recomendações de produto personalizadas, recursos de treinamento e ofertas para incentivar a conversão para planos pagos. Ao se reunir com usuários de teste onde estão em sua exploração de produtos, as equipes podem remover atritos e acelerar o caminho para a compra.

### Impacto no negócio

As organizações que implantam campanhas personalizadas de conversão de avaliação geralmente observam um aumento de 25 a 35% na conversão de avaliação para pagamento, afetando diretamente a nova receita comercial e reduzindo os custos de aquisição do cliente.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para criar jornadas de conversão baseadas em tempo e comportamento para usuários de avaliação. Este padrão suporta caminhos condicionais com base nos marcos de uso do produto, permitindo chamadas de atenção direcionadas nos momentos corretos.

### Considerações técnicas

- Assimilar telemetria de uso do produto (adoção de recursos, frequência de logon, tempo no produto) para criar perfis de envolvimento de avaliação em tempo real.
- Defina marcos com base no uso (por exemplo, primeiro projeto criado, recurso principal usado, colaboração convidada) como acionadores do jornada para alcance oportuno.
- Sincronizar o status da avaliação e os eventos de conversão com [!DNL Salesforce] ou [!DNL Microsoft Dynamics] para que os representantes de vendas tenham visibilidade total sobre as atividades de avaliação.
- Coordene com os programas de criação do [!DNL Marketo Engage] para evitar sobreposição de comunicações durante o período de avaliação.


## Sucesso e integração do cliente

Personalize as jornadas de integração do cliente com treinamento, recursos e suporte relevantes com base no produto adquirido e no perfil do cliente. A integração eficaz reduz o tempo de implantação e cria a base para a retenção e o crescimento do cliente a longo prazo.

### Impacto no negócio

As organizações com programas de integração personalizados normalmente atingem um aumento de 50 a 60% na adoção de recursos nos primeiros 90 dias, contribuindo diretamente para uma maior receita de retenção e expansão.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para orquestrar sequências de integração personalizadas para o produto, o nível de plano e o segmento do cliente. Esse padrão oferece suporte para uma progressão baseada em marcos, garantindo que os clientes recebam a orientação certa em cada estágio da integração.

### Considerações técnicas

- Assimile telemetria de uso do produto para rastrear marcos de integração (primeiro logon, configuração inicial, primeiro fluxo de trabalho concluído) e acione a próxima etapa de jornada adequadamente.
- Mapeie os perfis do cliente para o rastreamento de integração correto com base no produto comprado, no nível de plano e no número de usuários licenciados.
- Integre os dados da plataforma de sucesso do cliente para exibir as pontuações de integridade e sinalizar as contas de risco para uma intervenção proativa.
- Sincronizar o status de integração e as métricas de adoção com [!DNL Salesforce] ou [!DNL Microsoft Dynamics] para que os gerentes de sucesso do cliente possam priorizar o alcance externo.


## Campanhas de renovação de contrato

Envolva proativamente os clientes que estão se aproximando da renovação do contrato com ofertas personalizadas, insights de uso e incentivos de renovação. O alcance de renovação orientado por dados e em tempo hábil reduz a rotatividade e protege a receita recorrente.

### Impacto no negócio

As empresas que implementam campanhas de renovação proativas e personalizadas geralmente observam um aumento de 30 a 40% na taxa de renovação, protegendo a receita recorrente e reduzindo o custo da reaquisição do cliente.

### Como implementar o

Use o padrão [Cross-Channel Jornada com Decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para fornecer a oferta de renovação correta pelo canal certo, na hora certa. Esse padrão combina a orquestração de jornadas com o offer decisioning, permitindo incentivos dinâmicos de renovação com base no valor e uso da conta.

### Considerações técnicas

- Puxe as datas de término do contrato, os termos de renovação e o valor da conta de [!DNL Salesforce] ou [!DNL Microsoft Dynamics] para acionar jornadas de renovação no prazo de entrega apropriado (por exemplo, 90, 60, 30 dias).
- Incorpore dados de uso do produto e pontuações de integridade do cliente para determinar o risco de renovação e adaptar a estratégia de oferta de acordo.
- Use a decisão para selecionar o incentivo de renovação ideal (desconto, prazos estendidos, atualização premium) com base no valor vitalício da conta e na probabilidade de churn.
- Coordene o alcance de renovação com as equipes de sucesso e vendas do cliente para evitar mensagens em conflito por meio da [!DNL Marketo Engage] e da atribuição de tarefas do CRM.


## Oportunidades de venda adicional e expansão

Identifique os clientes prontos para upgrades de produtos ou licenças adicionais com base em padrões de uso, indicadores de crescimento e dados de sucesso do cliente. O alcance pró-ativo da expansão transforma o ímpeto do cliente em crescimento de receita.

### Impacto no negócio

As organizações que identificam e agem sistematicamente com sinais de expansão normalmente geram um aumento de 20 a 30% na receita de expansão, melhorando a retenção da receita líquida e o valor vitalício do cliente.

### Como implementar o

Use o padrão [Cross-Channel Jornada with Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) para fornecer ofertas personalizadas de venda adicional e expansão com base no uso em tempo real e em sinais de conta. Esse padrão usa a decisão para corresponder cada conta com a oferta de expansão mais relevante entre canais.

### Considerações técnicas

- Assimilar a telemetria de uso do produto para detectar sinais de expansão, como limites de utilização de licença, ocorrências de teto de recursos e contagens crescentes de usuários.
- Crie modelos de propensão em nível de conta usando dados de expansão histórica, tendências de uso e atributos firmográficos.
- Sincronizar oportunidades de expansão e ofertas recomendadas para [!DNL Salesforce] ou [!DNL Microsoft Dynamics] para que as equipes de vendas possam acompanhar o pipeline gerado por marketing.
- Coordene com [!DNL Marketo Engage] para garantir que as mensagens de expansão não entrem em conflito com o suporte contínuo ou as comunicações de renovação.


## Campanhas de substituição competitivas

Direcione clientes potenciais usando produtos da concorrência com mensagens personalizadas, ofertas de migração e comparações competitivas. Ao abordar os pontos problemáticos específicos associados a cada concorrente, as equipes de marketing podem se diferenciar com mais eficiência e acelerar as decisões de alternância.

### Impacto no negócio

As organizações B2B que executam campanhas de substituição competitivas direcionadas normalmente atingem um aumento de 15 a 25% na taxa de ganhos competitivos, capturando participação no mercado e substituindo os fornecedores estabelecidos.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para orquestrar campanhas competitivas multitoque personalizadas para o perfil de concorrente e cliente potencial específico. Esse padrão oferece suporte à ramificação condicional com base na identificação do concorrente, permitindo a geração de mensagens que abordam os pontos problemáticos exclusivos de cada cenário competitivo.

### Considerações técnicas

- Integrar dados de inteligência competitiva (por exemplo, provedores de tecnologia, campos de concorrentes de CRM) ao perfil unificado para identificar qual concorrente um cliente potencial usa atualmente.
- Crie ativos de conteúdo específicos dos concorrentes (guias de migração, folhas de comparação, calculadoras de ROI) e mapeie-os para blocos de conteúdo de jornada.
- Coordene com o [!DNL Marketo Engage] para suprimir campanhas competitivas para clientes potenciais já em ciclos de vendas ativos ou clientes existentes.
- Acompanhe o pipeline de deslocamento competitivo em [!DNL Salesforce] ou [!DNL Microsoft Dynamics] com atribuição de campanha dedicada para medir a eficácia do programa.


## Agendamento de webinários e demonstração

Personalize os convites para o webinário e o agendamento de demonstração com base nos interesses do cliente potencial, no setor e no histórico de engajamento. Convites relevantes e oportunos aumentam a presença e geram pipeline de maior qualidade a partir de interações ao vivo.

### Impacto no negócio

Os programas personalizados de webinário e convite de demonstração normalmente atingem um aumento de 35 a 45% na taxa de participação no webinário, impulsionando um pipeline mais qualificado de oportunidades de envolvimento em tempo real.

### Como implementar o

Use o padrão [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) para enviar convites personalizados quando os clientes potenciais demonstrarem sinais de interesse alinhados com tópicos futuros do webinário ou da demonstração. Esse padrão responde em tempo real a acionadores comportamentais, garantindo que os convites sejam recebidos quando o interesse for mais alto.

### Considerações técnicas

- Defina eventos de acionador com base em interesses (por exemplo, visitar uma página de produto, baixar um recurso relacionado, participar de uma comparação com um concorrente) que se alinhem a tópicos programados de webinário ou demonstração.
- Integre dados da plataforma de webinário (por exemplo, [!DNL ON24], [!DNL Zoom Webinar]) para rastrear métricas de registro, participação e envolvimento no perfil unificado.
- Sincronize solicitações de demonstração e agende dados com [!DNL Salesforce] ou [!DNL Microsoft Dynamics] para garantir que as equipes de vendas recebam notificações e contexto oportunos.
- Coordene a cadência de convite com os limites de comunicação de [!DNL Marketo Engage] para evitar clientes potenciais com excesso de mensagens que se qualificam para vários eventos.


## Estudo de caso e Personalization de ROI

Forneça estudos de caso personalizados, calculadoras de ROI e histórias de sucesso com base no setor de clientes potenciais, no tamanho da empresa e nos casos de uso. Quando os clientes potenciais veem comprovações de organizações semelhantes às deles, a confiança é criada mais rapidamente e as decisões de compra são aceleradas.

### Impacto no negócio

As organizações que personalizam conteúdo de comprovação normalmente veem um aumento de 25 a 35% no envolvimento com o estudo de caso, contribuindo para aumentar a confiança dos negócios e acelerar as taxas de fechamento.

### Como implementar o

Use o padrão [Personalization de Aplicativo/Web de Visitante Conhecido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) para exibir dinamicamente os estudos de caso mais relevantes e evidências de ROI com base no perfil de cada cliente potencial. Esse padrão faz a correspondência dos atributos do visitante a uma biblioteca de conteúdo, garantindo que todos os clientes potenciais vejam os pontos de prova de seus setores e grupos de colegas.

### Considerações técnicas

- Marque estudos de caso e ativos de conteúdo de ROI com metadados (setor, tamanho da empresa, caso de uso, produto) para permitir a correspondência dinâmica com perfis de prospecto.
- Implemente regras de personalização que priorizem a correspondência do setor primeiro, depois o tamanho da empresa e o caso de uso, com conteúdo de fallback para clientes potenciais com dados de perfil limitados.
- Integre os sinais de envolvimento de conteúdo (downloads, tempo na página, compartilhamentos) de volta ao perfil unificado para informar a pontuação de clientes potenciais e o alcance de vendas.
- Coordene com o [!DNL Marketo Engage] para incluir conteúdo de comprovação personalizado em sequências de email de criação, não apenas experiências no site.


## Programas de Defesa do Cliente

Identifique e envolva clientes satisfeitos com oportunidades de defesa, como referências, estudos de caso e depoimentos com base em dados de uso e satisfação. Clientes satisfeitos são um poderoso mecanismo de crescimento quando são reconhecidos e convidados a compartilhar seu sucesso.

### Impacto no negócio

Os programas estruturados de defesa do cliente geralmente geram um aumento de 20 a 30% na participação de defesa, gerando um fluxo constante de referências, estudos de caso e depoimentos que apoiam a aquisição de novos negócios.

### Como implementar o

Use o padrão [Jornada Orquestrada em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) para criar fluxos de trabalho de identificação e envolvimento de defesa que respondam a sinais de satisfação e uso. Esse padrão apoia solicitações de defesa progressiva, começando com uma participação leve (por exemplo, uma revisão) e avançando para compromissos mais profundos (por exemplo, uma chamada de referência ou um estudo de caso).

### Considerações técnicas

- Assimilar resultados da pesquisa de satisfação (por exemplo, pontuação líquida de promotores, pontuações de satisfação do cliente) e dados de uso do produto para criar uma pontuação de prontidão de defesa para cada conta.
- Defina critérios de elegibilidade de defesa que combinem limites de satisfação, marcos de uso e estabilidade da conta para evitar alcance prematuro.
- Sincronizar status de defesa e histórico de participação com [!DNL Salesforce] ou [!DNL Microsoft Dynamics] para que as equipes de vendas possam fazer referência aos defensores dos clientes durante a prospecção.
- Coordenar com [!DNL Marketo Engage] para suprimir alcance de defesa durante escalonamentos de suporte ativos ou negociações de renovação.
