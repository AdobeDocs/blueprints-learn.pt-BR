---
title: Ativação de mensagem de saída em lote
description: Saiba como avaliar um público-alvo e fornecer uma mensagem de saída agendada em uma única execução em lote.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 192853ce-02ab-46e6-9092-3db5354bc19c
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '8246'
ht-degree: 1%

---

# Ativação de mensagem de saída em lote

Este guia fornece uma referência completa de implementação para entrega de mensagens de saída agendadas a segmentos de público-alvo definidos usando o [!DNL Adobe Journey Optimizer] (AJO) e o [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP). Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam entender todas as abordagens de implementação viáveis, as considerações de decisão que orientam cada escolha e onde encontrar a documentação detalhada sobre o [!DNL Adobe Experience League].

A ativação de mensagens de saída em lote é o padrão de campanha fundamental para mensagens de saída de um para muitos. Ele abrange todo o ciclo de vida, desde a definição do público-alvo até a entrega de mensagens e a análise de desempenho. Este guia apresenta três opções de implementação — Campanha programada, Jornada acionada por público-alvo e Campanha acionada por API — e fornece orientação de decisão estruturada para selecionar a abordagem correta para cada caso de uso.

Ele fornece opções de implementação, análise de compensação, caminhos de navegação da interface do usuário e referências de documentação do [!DNL Experience League].

## Visão geral do caso de uso

As organizações geralmente precisam enviar uma única mensagem para um segmento de público-alvo conhecido em um momento específico ou em resposta a um evento do sistema. Este padrão atende a esse requisito combinando a avaliação de público em [!DNL RT-CDP] com a criação de mensagens e a execução de campanha em [!DNL Journey Optimizer].

O cenário de negócios é simples: definir quem deve receber a mensagem, criar o conteúdo da mensagem com personalização, vincular o público-alvo e a mensagem a uma campanha ou jornada e executar o envio de acordo com uma programação, por meio da qualificação de público-alvo ou por meio de um acionador do sistema. O resultado é uma mensagem entregue com relatórios completos sobre entrega, envolvimento e métricas de conversão.

Esse padrão se aplica sempre que um objetivo comercial pode ser avançado ao fornecer uma única mensagem a um público-alvo conhecido em uma execução. Ela é diferente das mensagens acionadas por eventos, que respondem a eventos comportamentais em tempo real, e das jornadas orquestradas em várias etapas, que orientam os perfis por vários pontos de contato ao longo do tempo. A ativação em lote é o padrão de campanha mais simples e o ponto de partida mais comum para casos de uso de mensagens de saída.

## Principais objetivos de negócios

Esta seção identifica os principais objetivos de negócios compatíveis com a ativação de mensagens de saída em lote.

### Aumentar o engajamento do email e da campanha

**Descrição:** Melhore as taxas de abertura, as taxas de click-through e a resposta geral da campanha por meio de conteúdo e direcionamento otimizados.

**KPIs:** Taxas de Abertura, Envolvimento, Taxas de Conversão

### Aumentar receita e vendas

**Descrição:** Impulsione o crescimento da receita principal por meio de canais digitais otimizados, campanhas e jornadas do cliente.

**KPIs:** Taxas de Conversão, Receita Incremental, Valor Médio de Pedido

**Objetivo comercial relacionado:** [Aumentar receita e vendas](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)

### Simplificar a execução da campanha

**Descrição:** reduza o tempo de compilação da campanha e simplifique a entrega de campanhas multicanal por meio de modelos, automação e processos padronizados.

**KPIs:** Velocidade de Comercialização, Eficiência, Conclusão no Prazo %

## Exemplo de casos de uso tático

Os cenários a seguir ilustram aplicativos comuns de ativação de mensagens de saída em lote.

- **Anúncio de venda ou explosão de email promocional** — Transmita uma oferta promocional para um segmento de clientes qualificados em uma data agendada
- **Notificação por push de lançamento de produto** — Notifique os clientes interessados sobre uma nova disponibilidade de produto por push
- **Email de resumo ou informativo** — forneça resumos periódicos de conteúdo aos públicos-alvo dos assinantes
- **Convite de registro em eventos** — Convide clientes potenciais qualificados para webinários, conferências ou eventos presenciais
- **Email de lembrete sobre a renovação da assinatura** — Lembrar os clientes que estão se aproximando das datas de renovação de tomar medidas
- **Notificação de marcos do programa de fidelidade** — parabenize os membros que atingem níveis de fidelidade ou limites de ponto
- **Email específico do call-to-action** — oriente uma ação direcionada, como concluir uma compra, atualizar preferências ou registrar-se em um programa
- **Campanha por SMS para promoção rápida ou oferta com limite de tempo** — envie promoções urgentes e com limite de tempo via SMS para públicos-alvo de aceitação

## Indicadores-chave de desempenho

A tabela a seguir define os KPIs usados para medir a eficácia da campanha.

| KPI | Descrição | Abordagem de medição |
| --- | --- | --- |
| Taxa de entrega | Porcentagem de mensagens entregues com êxito aos destinatários | Entregue/Enviado x 100 |
| Taxa de abertura | Porcentagem de mensagens entregues abertas por destinatários | Aberturas/Entregas únicas x 100 |
| Índice de click-through (CTR) | Porcentagem de mensagens entregues em que um link foi clicado | Cliques únicos/Entregue x 100 |
| Índice de clique para abrir (CTOR) | Porcentagem de mensagens abertas em que um link foi clicado | Cliques únicos / Aberturas únicas x 100 |
| Índice de conversão | Porcentagem de destinatários que concluíram a ação desejada | Conversões / Entregues x 100 |
| Taxa de cancelamento de inscrição | Porcentagem de destinatários que cancelaram a inscrição após receber a mensagem | Cancelamentos de assinatura/Enviado x 100 |
| Taxa de rejeição | Porcentagem de mensagens que não puderam ser entregues | Devoluções / Enviado x 100 |
| Receita por email enviado | Receita atribuída à campanha dividida pelas mensagens enviadas | Receita Total / Enviado |

## Padrão do caso de uso

**Ativação de mensagem de saída em lote**

Avalie um público-alvo e entregue uma mensagem de saída agendada (email, SMS, push) para todos os perfis qualificados em uma única execução em lote.

**Cadeia de funções:** Avaliação de público-alvo > Criação de mensagem > Execução de campanha > Relatórios

## Aplicativos

Os aplicativos a seguir são usados para implementar esse padrão.

- **[!DNL Adobe Journey Optimizer](AJO)** — Criação de mensagens, configuração de canal, execução de campanha, orquestração de jornadas, experimentação de conteúdo, regras de frequência e relatórios
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)** — Avaliação de público, consentimento e imposição de governança
- **[!DNL Adobe Experience Platform](AEP)** — Armazenamento de perfil, serviço de identidade, esquemas, conjuntos de dados, coleta de dados

## Funções básicas

Os seguintes recursos básicos devem estar em vigor para esse padrão de caso de uso. Para cada função, o status indica se ele é tipicamente necessário, se presume ser pré-configurado ou se não é aplicável.

| Função de base | Status | O que deve estar em vigor | Referência do Experience League |
| --- | --- | --- | --- |
| Administração e governança | Presumido em vigor | Sandbox da AJO provisionada com uma configuração de canal ativa. Envio de subdomínio delegado, pool de IP atribuído e aumento gradual de IP concluído. Funções de usuário com permissões de criação de campanha/jornada atribuídas. | [Visão geral das sandboxes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/home), [Visão geral do controle de acesso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Preparação e modelagem de dados | Obrigatório | Esquema de perfil individual XDM com atributos usados para segmentação e personalização (por exemplo, nome, email, preferências, nível). Esquema XDM ExperienceEvent que captura a ação de conversão de destino (por exemplo, `commerce.purchases`, `web.webInteraction`) para rastreamento de conversão pós-campanha. Conjuntos de dados habilitados para perfil para ambos os esquemas. | [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [noções básicas de composição de esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| Fontes de dados e coleção | Presumido em vigor | A marcação do Web SDK ou Analytics no destino do CTA deve estar ativa para capturar eventos de conversão. Os pipelines de transmissão ou assimilação em lote para atributos de perfil devem estar operacionais. | [Visão geral do Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home), [Visão geral das fontes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home) |
| Configuração de identidade e perfil | Presumido em vigor | Namespaces de identidade para email (e quaisquer identificadores entre dispositivos) configurados. Atributos de perfil necessários para personalização mapeada, assimilada e resolvível no momento do envio. Política de mesclagem configurada. | [Visão geral do Serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| Definição e segmentação do público-alvo | Obrigatório | Público-alvo definido na RT-CDP usando o Construtor de segmentos ou a Composição de público-alvo. Público publicado e avaliado com uma população diferente de zero. Abordado na Fase 1 da implementação por meio da avaliação de público-alvo da RT-CDP. | [Visão geral do Serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder) |

## Funções de suporte

Os recursos a seguir aumentam esse padrão de caso de uso, mas não são necessários para a execução principal.

| Função de suporte | Status | Por que é importante | Referência do Experience League |
| --- | --- | --- | --- |
| Criação de atributo calculado/derivado | Recomendado | Atributos computados, como dias desde a última compra, contagem de pedidos ao longo da vida útil ou pontuação de engajamento, melhoram a precisão do público-alvo e permitem uma personalização de mensagens mais avançada. | [Visão geral dos atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Gerenciamento do ciclo de vida dos dados | Recomendado | As políticas de retenção de dados (expiração) devem estar em vigor para conjuntos de dados de eventos que impulsionam o rastreamento de conversão. Os campos de esquema de consentimento devem ser configurados para imposição de aceitação/recusa em nível de canal. | [Visão geral do Gerenciamento Avançado do Ciclo de Vida dos Dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [Grupo de campos Consentimento e Preferências](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents) |
| Rotulagem e aplicação de uso de dados | Recomendado | Os rótulos de governança em campos PII usados na personalização garantem a conformidade durante a ativação. Evita o uso não autorizado de dados confidenciais do perfil em exportações de conteúdo de mensagem ou público-alvo. | [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [Visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview) |
| Monitoramento e capacidade de observação | Incluído | O monitoramento de envio em tempo real faz parte da fase de Relatório. Alertas em nível de plataforma sobre falhas de assimilação ou uso de licença fornecem visibilidade operacional além das métricas em nível de campanha. | [Visão geral dos Insights de Observabilidade](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home), [Visão geral dos alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview) |
| Relatórios e análise | Incluído | Os relatórios de campanha e jornada são abordados na fase de Relatórios. Para uma análise mais profunda entre canais, a integração do CJA fornece análise do funnel, modelagem de atribuição e análise de coorte além dos relatórios integrados do AJO. | [visão geral do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [guia de integração do AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo) |

## Funções do aplicativo

Este plano utiliza as seguintes funções do catálogo de funções do aplicativo. As funções são mapeadas para fases de implementação em vez de etapas numeradas.

### [!DNL Journey Optimizer] (AJO)

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Configuração de canais | Fase 2: configuração de canal | Configurar ou validar a superfície de canal (email, SMS ou push), incluindo subdomínio, pool de IP, configurações de remetente e lista de supressão |
| Criação de mensagens | Fase 3: Criação de mensagens | Criar conteúdo de mensagem usando modelos, o Designer de email, expressões de personalização, blocos de conteúdo condicional e fragmentos de conteúdo |
| Execução de campanha | Fase 4: Criação de campanha ou Jornada | Crie, configure e ative uma campanha agendada ou acionada por API que vincule o público-alvo, a mensagem e o agendamento de execução |
| Experimentação de conteúdo | Fase 4: Criação de campanha ou Jornada | Opcionalmente, configure experimentos de conteúdo A/B ou multivariado para otimizar o desempenho da mensagem |
| Frequência e regras de negócios | Fase 4: Criação de campanha ou Jornada | Opcionalmente, aplique regras de limite de frequência para evitar mensagens excessivas em campanhas simultâneas |
| Gerenciamento de conflitos e prioridades | Fase 4: Criação de campanha ou Jornada | Atribua pontuações de prioridade e configure a resolução de conflitos quando várias campanhas visam públicos sobrepostos |
| Relatórios e análise de desempenho | Fase 5: Relatórios e análise de desempenho | Monitore métricas de entrega por meio de relatórios em tempo real durante a execução e analise o desempenho da campanha por meio de relatórios históricos após a conclusão |

### [!DNL Real-Time CDP] (RT-CDP)

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Avaliação de público | Fase 1: Avaliação de público-alvo | Defina as regras de público-alvo usando o Construtor de segmentos ou a Composição de público-alvo, selecione o método de avaliação (lote, fluxo ou borda) e valide a população do público-alvo |
| Consentimento e aplicação de governança | Fase 1: Avaliação de público-alvo | Imponha preferências de consentimento e políticas de uso de dados para garantir que apenas perfis consentidos recebam a mensagem da campanha |

## Pré-requisitos

Conclua o seguinte antes de iniciar a implementação.

- [ A sandbox do AJO ] está provisionada e ativa
- [ ] O subdomínio de envio é delegado e verificado (SPF, DKIM, DMARC configurado)
- [ O pool de IP ] foi atribuído e aquecido para o volume de envio de produção
- [ ] Existe pelo menos uma superfície de canal ativa (email, SMS ou push)
- [ ] contas de usuário têm permissões de criação de campanha/jornada e conteúdo
- [ O esquema de perfil XDM ] inclui atributos necessários para a segmentação de público e personalização de mensagens
- [ O esquema de evento XDM ] captura eventos de conversão para rastreamento pós-campanha
- [ ] Os dados do perfil são assimilados e unificados pelo Serviço de identidade
- [ A marcação do Web SDK ou do Analytics ] está ativa na página de destino do CTA para capturar eventos de conversão
- [ ] Campos de consentimento são preenchidos em perfis para o canal de mensagens de destino
- [ ] Os recursos de conteúdo (imagens, logotipos, diretrizes de marca) estão disponíveis para o design da mensagem

## Opções de implementação

Esta seção descreve três opções de implementação para ativação de mensagens de saída em lote, juntamente com uma comparação e uma orientação de decisão.

### Opção A: campanha agendada (envio em lote único)

**Recomendado para:** envios ancorados por data — anúncios de venda, lançamentos de produtos, prazos de inscrição em eventos, lembretes de renovação, explosões de informativos e qualquer envio em que a data de execução seja conhecida antecipadamente.

**Como funciona:**

Uma campanha agendada é a variante mais simples de mensagens de saída em lote. O profissional de marketing define o público-alvo, cria o conteúdo da mensagem, define a data e a hora de envio e ativa a campanha. No tempo de execução agendado, o AJO avalia o público-alvo para determinar a população qualificada atual e, em seguida, entrega a mensagem a todos os perfis qualificados em um único lote.

Toda a configuração acontece na interface do AJO Campaigns — não há tela de jornada, lógica de ramificação e etapas de espera. Isso torna as campanhas agendadas as mais rápidas de configurar e fáceis de gerenciar. A campanha pode ser definida para execução imediata, uma data/hora futura específica ou um agendamento recorrente (diário, semanal, mensal).

**Principais considerações:**

- O público é avaliado no tempo de execução, de modo que os perfis qualificados entre o agendamento e a execução são incluídos
- Nenhuma lógica de ramificação, espera ou condição está disponível — a mensagem é entregue a todos os perfis qualificados
- Oferece suporte à experimentação de conteúdo (teste A/B) diretamente na configuração da campanha
- As propriedades da campanha incluem uma pontuação de prioridade para a resolução de conflitos com outras campanhas

**Vantagens:**

- Configuração mais simples com menos sobrecarga
- Lançamento mais rápido para envios simples em lote
- Suporte incorporado para agendamentos recorrentes
- Experimentação de conteúdo nativamente compatível
- O público-alvo foi reavaliado no tempo de execução para atualização

**Limitações:**

- Nenhuma etapa, condição ou ramificação de espera antes da entrega
- Não é possível reagir ao comportamento do perfil entre o agendamento e a execução
- Apenas ação de mensagem única — sem sequências de multitoque
- Não pode ser editado depois de ativado (deve ser duplicado e modificado)

**Experience League:**

- [Introdução às campanhas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Criar uma campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)

### Opção B: jornada acionada por público-alvo

**Recomendado para:** envios orientados por comportamento — notificações de carrinho abandonado, lembretes de expiração de avaliação, celebrações de marcos, alcance de qualificação e qualquer envio em que o acionador seja qualificação de público-alvo ou um evento comercial em vez de uma data de calendário.

**Como funciona:**

Uma jornada acionada pelo público-alvo usa a tela de jornada para enviar uma mensagem quando um perfil se qualifica para um público-alvo definido ou aciona um evento de qualificação. A entrada de jornada é acionada por alterações de associação de público-alvo (perfis que entram no público-alvo) em vez de um agendamento fixo. A tela de jornada permite etapas de espera opcionais, ramificações de condição e lógica de supressão antes da ação de mensagem, fornecendo mais flexibilidade do que uma campanha programada.

A jornada é configurada na interface do AJO Jornada usando o evento de entrada Ler público-alvo. Quando os perfis se qualificam para o público-alvo, eles entram na jornada e prosseguem pelos nós da tela. Uma implementação simples pode conter apenas um único nó de ação de email, tornando-a funcionalmente semelhante a uma campanha agendada, mas com tempo de entrada baseado em qualificação de público-alvo. Implementações mais complexas podem adicionar nós de espera (por exemplo, aguardar 24 horas após a qualificação), nós de condição (por exemplo, verificar se o perfil abriu um email anterior) ou lógica de supressão antes da entrega da mensagem.

**Principais considerações:**

- A entrada da jornada é acionada pela qualificação do público-alvo, não por uma data do calendário
- A tela de jornada é compatível com nós de espera, condição e divisão para lógica de pré-entrega
- As regras de reentrada do Jornada controlam se os perfis podem entrar na jornada várias vezes
- As configurações de arbitragem de jornada determinam o comportamento quando um perfil já está em uma jornada concorrente

**Vantagens:**

- Tempo de entrada flexível com base na qualificação do público-alvo em vez da programação fixa
- Os nós de espera e condição permitem a lógica de pré-entrega (por exemplo, atraso, verificação, supressão)
- Os controles de reentrada evitam envios duplicados para o mesmo perfil
- Pode ser estendido para uma jornada de várias etapas se o caso de uso evoluir
- Oferece suporte a relatórios em nível de jornada com métricas de entrada, saída e nó

**Limitações:**

- Mais sobrecarga de configuração do que uma campanha programada
- A tela de Jornada adiciona complexidade mesmo para casos de uso de mensagem única
- A Jornada deve ser publicada e não pode ser editada enquanto estiver ativa (é necessário criar uma nova versão)
- O limite de entrada pode limitar o número de perfis que entram em uma janela de tempo

**Experience League:**

- [Introdução ao jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Ler jornada de público-alvo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)

### Opção C: campanha acionada por API

**Recomendado para:** envios iniciados pelo sistema — confirmação de pedidos com conteúdo de venda adicional, acompanhamento da resolução de tíquetes de suporte, notificações transacionais com conteúdo de marketing e qualquer envio em que o evento de acionamento seja originado de um sistema externo em um momento específico.

**Como funciona:**

Uma campanha acionada pela API é ativada por meio de uma chamada à API REST no momento em que ocorre um evento do sistema de acionamento. A campanha é pré-configurada no AJO com configurações de conteúdo de mensagem e canal, mas em vez de vincular um público-alvo predefinido, a chamada de API especifica os perfis do recipient e pode enviar dados contextuais que preenchem parâmetros de mensagem dinâmicos.

Essa variante é ideal quando o tempo de envio é determinado por um sistema externo (por exemplo, um sistema de gerenciamento de pedidos, um fluxo de trabalho de CRM ou uma plataforma de suporte) em vez de pela avaliação do público-alvo ou um agendamento do calendário. Os dados contextuais transmitidos na carga do acionador da API — como detalhes do pedido, números de tíquete ou nomes de produtos — podem personalizar o conteúdo da mensagem usando atributos contextuais que não são armazenados no perfil.

**Principais considerações:**

- Nenhum público-alvo pré-vinculado é necessário — os destinatários são especificados na solicitação do acionador de API
- Os dados contextuais na carga do acionador permitem a personalização dinâmica além dos atributos do perfil
- A campanha deve ser do tipo &quot;acionada por API&quot; e deve ser ativada para receber solicitações de acionador
- Cada solicitação de acionador de API oferece suporte a até 20 recipients de perfil
- A Avaliação de público-alvo (Fase 1) pode ser ignorada, pois os recipients vêm da chamada da API

**Vantagens:**

- Acionamento em tempo real de sistemas externos no momento do evento
- Personalização contextual com dados não armazenados no perfil (detalhes do pedido, informações do tíquete)
- Nenhuma sobrecarga de avaliação de público — os destinatários são especificados diretamente
- Oferece suporte a mensagens transacionais + híbridas de marketing

**Limitações:**

- Requer integração externa do sistema para enviar o acionador de API
- Máximo de 20 destinatários por solicitação de acionador de API
- Nenhuma avaliação de público incorporada: o sistema de chamada deve determinar os recipients
- Maior complexidade técnica devido aos requisitos de integração da API
- A experimentação de conteúdo não é compatível com campanhas acionadas por API

**Experience League:**

- [Campanhas acionadas por API](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)
- [Acionar campanhas usando APIs](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)

### Comparação de opções

A tabela a seguir compara as três opções de implementação entre os principais critérios.

| Critérios | Opção A: Campanha Programada | Opção B: Jornada acionada pelo público-alvo | Opção C: campanha acionada por API |
| --- | --- | --- | --- |
| Melhor para | Envios ancorados por data (promoções, inicializações, boletins informativos) | Envios orientados por comportamento (eventos de qualificação, marcos) | Envios iniciados pelo sistema (confirmações de pedidos, transacional) |
| Complexo | Baixa | Médio | Medium-Alto |
| Tipo de acionador | Data/hora do calendário ou programação recorrente | Qualificação de público ou evento comercial | Chamada de API do sistema externo |
| Lógica de pré-entrega | Nenhum | Espera, condição, nós divididos disponíveis | Nenhum (lógica no sistema de chamada) |
| Vinculação de público | Público-alvo predefinido da RT-CDP | Público-alvo predefinido da RT-CDP | Recipients especificados na carga da API |
| Dados contextuais | Somente atributos de perfil | Somente atributos de perfil | Atributos de perfil + dados de carga da API |
| Experimentação de conteúdo | Compatível | Compatível (na ação da mensagem) | Não suportado |
| Limite de frequência | Compatível | Compatível | Compatível |
| Controle de reentrada | N/D (execução única) | Regras de reentrada configuráveis | N/D (por solicitação) |
| Interface de configuração | Campanhas do AJO | AJO Jornada | Campanhas do AJO + sistema externo |
| Exige | Público, superfície de canal, mensagem | Público, superfície de canal, mensagem, tela de jornada | Superfície de canal, mensagem, integração de API |

### Escolha a opção certa

Use o fluxo de decisão a seguir para selecionar a opção de implementação apropriada:

1. **O envio é disparado por um evento de sistema externo (por exemplo, pedido feito, tíquete resolvido)?** Em caso afirmativo, escolha **Opção C: Campanha acionada por API**. Essa é a única opção que oferece suporte a acionadores iniciados pelo sistema com dados de carga contextuais.

2. **O envio está ancorado em uma data de calendário específica ou em uma agenda recorrente?** Em caso afirmativo, escolha **Opção A: Campanha agendada**. É o mais simples e rápido de configurar para envios orientados por data.

3. **O envio precisa reagir à qualificação de público ou requer lógica de pré-entrega (espera, condição, supressão)?** Em caso afirmativo, escolha **Opção B: Jornada acionada por público-alvo**. A tela de jornada oferece a flexibilidade para entrada orientada por comportamento e lógica de decisão de pré-entrega.

4. **O envio é uma transmissão simples para um público conhecido sem requisitos especiais de tempo ou lógica?** Escolha a **Opção A: Campanha agendada** para a sobrecarga de configuração mais baixa.

## Fases de implementação

Esta seção aborda detalhadamente cada fase da implementação, incluindo pontos de decisão e orientação específica para cada opção.

### Fase 1: avaliar o público

**Função do aplicativo:** RT-CDP: Avaliação de Público-Alvo

Essa fase define e avalia o segmento do público-alvo que receberá a mensagem da campanha. Ele determina quais perfis se qualificam para o envio com base em atributos de perfil, sinais comportamentais e regras de supressão.

>[!NOTE]
>Para a Opção C (Campanha acionada pela API), essa fase pode ser ignorada se os recipients forem especificados totalmente na carga do acionador da API. No entanto, até mesmo campanhas acionadas por API se beneficiam de ter um público de supressão para filtrar perfis que não devem receber mensagens.

#### Decisão: critérios de público-alvo

Quais condições definem o público-alvo? Quais regras de supressão devem excluir perfis?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Público-alvo com base no atributo de perfil | O público-alvo é definido por atributos demográficos, de preferência ou de status | É mais simples de criar; oferece suporte a todos os métodos de avaliação |
| Público comportamental baseado em eventos | O público-alvo é definido por ações realizadas (ou não) em uma janela de tempo | Requer assimilação de dados do evento; as regras de janela de tempo podem limitar a qualificação de transmissão |
| Composição de público (público derivado) | O público-alvo requer operações de classificação, divisão, exclusão ou enriquecimento entre vários públicos-alvo de origem | Avaliação mais eficiente, mas somente em lote; limitado a 10 composições por sandbox |

#### Decisão: Método de avaliação

Com que rapidez o público-alvo deve ser atualizado para refletir novos perfis qualificados ou desqualificados?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Avaliação em lote | Campanhas programadas em que a atualização do público-alvo em um dia é aceitável; públicos-alvo grandes e complexos | Padrão, para a maioria dos tipos de segmento; processos em uma programação diária ou sob demanda; suporta todas as funções de regra de segmento |
| Avaliação de transmissão | Jornadas acionadas por público-alvo, nas quais os perfis devem entrar em tempo quase real à medida que se qualificam | Automático para expressões de regra de segmento elegíveis; nem todos os tipos de segmento se qualificam para transmissão; latência quase em tempo real (segundos a minutos) |
| Avaliação da borda | Não é típico para este padrão (usado para personalização de mesma página) | Suporte limitado a regras de segmento; latência de milissegundos; relevante somente se combinado a padrões de personalização da Web |

#### Decisão: política de mesclagem

Qual política de mesclagem o público-alvo deve usar para resolver fragmentos de perfil?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Política de mesclagem padrão (carimbo de data e hora ordenado) | Mais comum para casos de uso de campanha em lote | O valor de atributo mais recente vence; padrão para mensagens de saída |
| Política de mesclagem personalizada (precedência de conjunto de dados) | Quando uma fonte de dados específica deve ter prioridade para atributos-chave | Útil quando os dados do CRM devem substituir os dados coletados pela Web de determinados campos |

#### Navegação na interface

Cliente > Públicos > Criar público > Criar regra

#### Principais detalhes de configuração

- Defina o público-alvo usando o Construtor de segmentos com regras de segmento para atributos de perfil, eventos comportamentais e associação de segmento
- Aplicar regras de supressão para excluir perfis que já tenham convertido, recebido recentemente uma mensagem semelhante ou recusado
- Verifique se o público-alvo tem uma população diferente de zero antes de continuar
- Para campanhas em lote, verifique se uma programação de avaliação de segmento está ativa ou acione a avaliação sob demanda
- Confirmar campos de consentimento (`consents.marketing.email.val`, `consents.marketing.sms.val` etc.) são preenchidos e aplicados

#### Onde as opções divergem

**Para a Opção A (Campanha Agendada):**

A avaliação em lote é típica. O público é reavaliado no tempo de execução da campanha, portanto, a população qualificada mais atual é direcionada. Defina o público-alvo, verifique o público e prossiga para a criação da campanha.

**Para Opção B (Jornada Acionada Por Público-Alvo):**

A avaliação de transmissão é preferível, para que os perfis entrem na jornada conforme se qualificam. Verifique se a expressão da regra de segmento é qualificada para streaming (acionadores de eventos simples, comparações de atributos, janelas de tempo limitadas). Configure o público e verifique se a qualificação de transmissão está ativa.

**Para a Opção C (Campanha Acionada por API):**

A avaliação do público-alvo pode ser totalmente ignorada. Se usada, crie um público-alvo de supressão para filtrar perfis que não devem receber a mensagem (por exemplo, cancelamento de assinatura recente, já convertido). O sistema de chamada determina os recipients principais.

#### Documentação do Experience League

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentação de transmissão](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Composição de público](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Referência do Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### Fase 2: configurar o canal

**Função do aplicativo:** AJO: configuração de canal

Essa fase valida ou cria a superfície de canal (predefinição) que define a infraestrutura de envio da mensagem: subdomínio, pool de IP, identidade do remetente, endereço de resposta e configurações de cancelamento de assinatura. Uma superfície de canal válida deve existir para que o conteúdo da mensagem possa ser criado ou as campanhas possam ser ativadas.

#### Decisão: canal do Target

Qual canal de mensagens fornecerá a mensagem de campanha?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Email | A maioria dos tipos de campanha — boletins informativos, promoções, notificações, renovações | Requer subdomínio delegado, pool de IPs aquecido, identidade do remetente e configuração de cancelamento de inscrição |
| SMS | Mensagens breves ou sensíveis ao tempo — vendas rápidas, lembretes de compromissos, códigos OTP | Requer credenciais de provedor de SMS (Sinch, Twilio ou Infobip); custo por mensagem mais alto; requisitos de consentimento mais rigorosos |
| Notificação por push | Públicos envolvidos com dispositivos móveis: atualizações de aplicativos, ofertas baseadas em localização e anúncios de recursos no aplicativo | Requer credenciais APNs (iOS) e/ou FCM (Android); os usuários devem ter o aplicativo instalado com permissões de push concedidas |

#### Decisão: seleção da superfície de canal

Já existe uma superfície de canal adequada na sandbox ou é necessário criar uma nova?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Reutilizar superfície existente | Uma superfície ativa verificada corresponde ao subdomínio, à identidade do remetente e ao tipo de canal necessários | Caminho mais rápido; nenhuma configuração de DNS ou aquecimento é necessária |
| Criar nova superfície | Nenhuma superfície existente corresponde aos requisitos ou é necessária uma nova identidade de subdomínio/remetente | Requer delegação de subdomínio, verificação de DNS, atribuição de pool de IP e, possivelmente, aquecimento de IP (2 a 4 semanas para novos IPs) |

#### Decisão: cancelar inscrição e tratar

Como a recusa deve ser gerenciada na superfície de canal?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Cabeçalho list-unsubscribe com um clique | Padrão para todos os emails de marketing; exigido pelos principais ISPs (Gmail, Yahoo) para entrega | Adiciona um cabeçalho mailto: ou de cancelamento de inscrição baseado em URL que os ISPs exibem como um botão &quot;Cancelar inscrição&quot; |
| Link de cancelamento de inscrição no corpo do email | Obrigatório como fallback para clientes de email que não oferecem suporte a cabeçalhos de cancelamento de inscrição em lista | Incluir no rodapé do email um link para cancelar inscrição ao lado do cabeçalho list-unsubscribe |
| Ambos (recomendado) | Prática recomendada para todos os emails de marketing | Cobertura máxima de conformidade e melhor perfil de entrega |

#### Navegação na interface

Administração > Canais > Superfícies de canal > Criar superfície (ou selecionar existente)

#### Principais detalhes de configuração

- Para email: vincular o subdomínio de envio, pool de IP, nome do remetente, email do remetente, endereço para resposta e endereço CCO (se uma cópia de auditoria for necessária)
- Para SMS: configure as credenciais do provedor de SMS e as configurações de código curto ou código longo
- Para push: configure APNs e/ou credenciais FCM com o certificado do aplicativo ou a chave do servidor
- Verifique se a superfície de canal mostra o status &quot;Ativo&quot; antes de continuar
- Confirmar se os registros DNS (SPF, DKIM, DMARC) estão configurados corretamente para o subdomínio de envio
- Revise a lista de supressão para entradas obsoletas; limpe antes da ativação

#### Documentação do Experience League

- [Introdução à configuração de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegar subdomínios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Criar pools de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [Planos de aquecimento de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Configurações de superfície de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Configurar canal de SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configurar canal de notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [Gerenciar lista de supressão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Fase 3: Criação da mensagem

**Função do aplicativo:** AJO: Criação de Mensagens

Essa fase cria o conteúdo da mensagem que será entregue ao público-alvo. Ele inclui selecionar ou criar um modelo de conteúdo, projetar o layout da mensagem, adicionar personalização usando atributos de perfil, configurar blocos de conteúdo condicional para variações específicas do público-alvo, criar fragmentos de conteúdo reutilizáveis e visualizar/testar a mensagem com perfis de amostra.

#### Decisão: abordagem de conteúdo

Como o conteúdo da mensagem deve ser criado?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Iniciar com base em modelo existente | Existem modelos aprovados por marca que correspondem ao tipo de mensagem (promocional, transacional, informativo) | Caminho de criação mais rápido; garante a consistência da marca; os modelos são específicos da sandbox |
| Criar do zero | Não há modelo adequado ou a mensagem requer um layout exclusivo | Mais flexibilidade, mas mais esforço; considere economizar como um modelo para reutilização |
| Importar HTML | O design da mensagem foi criado externamente (por exemplo, em uma ferramenta de design) e o HTML está pronto para importação | Preserva o design externo; pode precisar de ajustes para os tokens de compatibilidade e personalização do AJO |

#### Decisão: profundidade do Personalization

Quais atributos de perfil devem personalizar a mensagem e os blocos de conteúdo condicional são necessários?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Personalização básica (nome, saudação) | Campanhas simples em que o conteúdo genérico com uma saudação personalizada é suficiente | Baixo esforço; risco mínimo de problemas de renderização; usa atributos de perfil padrão |
| Personalização baseada em atributos | O conteúdo da mensagem varia de acordo com os atributos do perfil (camada, preferência, local) | Requer caminhos XDM verificados; teste com vários perfis para garantir que todas as variações sejam renderizadas corretamente |
| Blocos de conteúdo condicional | Seções de conteúdo diferentes devem ser exibidas para segmentos de público diferentes na mesma mensagem | Criação mais complexa; cada condição precisa de um fallback padrão; testar todas as permutas |
| Personalização contextual (somente opção C) | As campanhas acionadas por API precisam renderizar os dados transmitidos na carga do acionador (detalhes do pedido, informações do tíquete) | Os atributos contextuais não são armazenados no perfil; defina espaços reservados na mensagem e mapeie para campos de carga |

#### Decisão: estratégia de fragmento

Os blocos de conteúdo compartilhado devem ser criados como fragmentos reutilizáveis?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Fragmentos reutilizáveis | Cabeçalhos, rodapés, avisos legais ou blocos de cancelamento de inscrição são compartilhados em várias campanhas | As alterações em um fragmento são propagadas para todas as mensagens que fazem referência a ele (ativas e de rascunho); máximo de 30 fragmentos por mensagem |
| Conteúdo integrado | Mensagem única sem elementos compartilhados em outras campanhas | Mais simples para conteúdo de uso único; sem risco de propagação |

#### Navegação na interface

Campanhas > Selecionar campanha > Editar conteúdo > Enviar email para o Designer (ou o editor de SMS/Push)

#### Principais detalhes de configuração

- Projete o layout de mensagem usando componentes de conteúdo de arrastar e soltar (texto, imagem, botão, divisor, colunas)
- Definir as propriedades do cabeçalho do email: linha de assunto, texto do pré-cabeçalho e superfície do remetente
- Inserir expressões de personalização usando a sintaxe Handlebars (por exemplo, `{{profile.person.name.firstName}}`)
- Configurar funções auxiliares para formatação (data, número, manipulação de sequência)
- Adicione regras de conteúdo condicional para exibir conteúdo diferente com base nos atributos do perfil ou na associação do segmento
- Configurar conteúdo de fallback padrão quando nenhuma condição for atendida
- Para SMS, escreva o corpo da mensagem dentro das considerações de limite de caracteres
- Para push, configure título, corpo, imagem e ação (deep link ou URL)
- Visualize a mensagem com perfis de amostra para verificar a renderização de personalização
- Enviar emails de prova aos participantes internos para revisão
- Testar a renderização entre clientes de email usando o recurso de renderização de email

#### Documentação do Experience League

- [Criar um email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [Criar conteúdo de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Usar componentes de conteúdo do Email Designer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/content-components)
- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxe do Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Funções auxiliares](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabalhar com modelos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabalhar com fragmentos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Visualizar e testar o conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [Enviar provas de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/proofs)
- [Renderização de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/email-rendering)
- [Criar uma mensagem SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/create-sms)
- [Criar uma notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/design-push)

### Fase 4: criar a campanha ou a jornada

**Função do aplicativo:** AJO: Execução de Campanha (Opções A e C) ou AJO: Journey Orchestration (Opção B)

Essa fase cria a campanha ou jornada que vincula o público-alvo, a mensagem e o mecanismo de execução em uma unidade do material de entrega. É neste ponto que as três opções de execução divergem mais significativamente.

#### Decisão: experimentação de conteúdo

A campanha deve incluir um teste A/B ou experimento multivariado para otimizar o desempenho da mensagem?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Nenhum experimento | Variante de mensagem única com alta confiança na eficácia do conteúdo | Configuração mais simples; ativação mais rápida |
| Teste A/B (2 variantes) | Teste de linhas de assunto, CTAs ou layouts de conteúdo com uma hipótese clara | Tráfego dividido 50/50 ou com alocação ponderada; requer tamanho de público suficiente para significância estatística |
| Teste multivariado (mais de 3 variantes) | Teste de vários elementos de conteúdo simultaneamente | Requer públicos-alvo maiores; duração mais longa para atingir o limite de confiança; máximo de 10 tratamentos por experimento |

#### Decisão: Limite de frequência

Essa campanha deve respeitar as regras globais de limite de frequência para evitar o excesso de mensagens?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Aplicar regras de frequência | A campanha faz parte de um programa de mensagens mais amplo com vários envios simultâneos | Evita a fadiga do cliente; perfis que excedem o limite são suprimidos da entrega |
| Isento de limite | A campanha é crítica ao tempo ou transacional e deve alcançar todos os perfis qualificados, independentemente do histórico de mensagens recentes | Uso com moderação; isentar campanhas de regras de frequência arrisca mensagens excessivas |

#### Decisão: pontuação de prioridade

Qual nível de prioridade essa campanha deve ter em relação a outras campanhas ativas?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Alta prioridade (75-100) | Campanhas críticas — principais lançamentos de produtos, ofertas por tempo limitado, notificações normativas | Terá precedência sobre campanhas de prioridade mais baixa quando surgirem conflitos |
| Prioridade do Medium (25-74) | Campanhas de marketing padrão — boletins informativos, campanhas de engajamento, promoções gerais | Equilibrado com outras campanhas; pode ser suprimido se uma campanha de prioridade mais alta entrar em conflito |
| Prioridade baixa (0-24) | Envios fáceis de ter — atualizações informativas, promoções secundárias | Será suprimido em favor de campanhas de prioridade mais alta |

#### Onde as opções divergem

**Para a Opção A (Campanha Agendada):**

**Navegação da interface do usuário:** Campanhas > Criar campanha > Agendado > Marketing

1. Criar uma nova campanha de marketing agendada
2. Selecionar o público-alvo no seletor de público
3. Selecione a superfície de canal e vincule o conteúdo da mensagem criada
4. Configure o agendamento de execução: imediato, data/hora específica ou recorrente
5. Ativar opcionalmente a experimentação de conteúdo e definir variantes de tratamento
6. Opcionalmente, configure o limite de frequência e a pontuação de prioridade
7. Revise a configuração completa da campanha
8. Ativar a campanha

**Para Opção B (Jornada Acionada Por Público-Alvo):**

**Navegação da interface do usuário:** Jornadas > Criar Jornada

1. Criar uma nova jornada com um evento de entrada &quot;Ler público-alvo&quot;
2. Selecione o público-alvo como a fonte de entrada
3. Configurar regras de reentrada (permitir reentrada, entrada única ou reentrada após o período de espera)
4. Opcionalmente, adicionar nós de espera (por exemplo, aguardar 24 horas após a qualificação)
5. Opcionalmente, adicionar nós de condição (por exemplo, verificar se o perfil atende a critérios adicionais)
6. Adicione o nó de ação da mensagem e selecione a superfície de canal e o conteúdo criado
7. Configurar critérios de saída (por exemplo, conversões de perfis, cancelamentos de assinatura de perfis)
8. Ativar opcionalmente a experimentação de conteúdo na ação de mensagem
9. Revisar e publicar a jornada

**Para a Opção C (Campanha Acionada por API):**

**Navegação da interface do usuário:** Campanhas > Criar campanha > Acionado por API

1. Criar uma nova campanha acionada por API
2. Selecione a superfície de canal e vincule o conteúdo da mensagem criada
3. Configurar tokens de personalização contextual para dados que serão transmitidos na carga do acionador da API
4. Revisar e ativar a campanha
5. Observe a ID da campanha para usar na integração do acionador de API do sistema externo
6. O sistema de chamada envia solicitações de acionador ao endpoint da campanha com perfis de destinatário e dados contextuais

#### Documentação do Experience League

- [Criar uma campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Introdução às campanhas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Campanhas acionadas por API](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)
- [Introdução ao jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Ler jornada de público-alvo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Introdução ao experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Criar um experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Regras de frequência](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Pontuações de prioridade](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Identificar possíveis conflitos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)

### Fase 5: analisar a geração de relatórios e o desempenho

**Função do aplicativo:** AJO: Relatórios e análise de desempenho

Essa fase monitora as métricas de entrega durante a execução por meio de relatórios em tempo real e analisa o desempenho da campanha após a conclusão por meio de relatórios históricos. Configurar opcionalmente a integração do CJA para uma análise mais profunda entre canais.

#### Decisão: método de relatório

Qual nível de relatório é necessário para esta campanha?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Somente relatórios nativos do AJO | As métricas padrão de entrega e envolvimento são suficientes (envio, entrega, aberturas, cliques, rejeições) | Nenhuma configuração adicional; os relatórios são incorporados à interface do usuário da campanha/jornada |
| Relatórios nativos do AJO + análise do CJA | Análise de impacto entre canais, modelagem de atribuição ou análise do funnel é necessária além das métricas de entrega | Requer uma conexão e uma visualização de dados do CJA vinculadas aos conjuntos de dados da AJO; fornece recursos analíticos mais profundos |
| Relatórios programáticos do CJA | Os painéis automatizados ou a entrega agendada de relatórios são necessários para as partes interessadas | Requer integração da API de relatórios do CJA; útil para painéis executivos e resumos de desempenho recorrentes |

#### Decisão: rastreamento de conversão

Como o sucesso da campanha será medido além das métricas de entrega e envolvimento?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Nenhum rastreamento de conversão | O objetivo da campanha é conscientização ou engajamento (aberturas, cliques) sem nenhuma ação de downstream específica | Mais simples; não é necessário nenhum rastreamento de evento adicional |
| Rastreamento de conversão da Web | Links do Campaign CTA para uma página da Web onde os eventos de conversão (compra, registro, envio de formulário) são rastreados | Exige marcação do Web SDK ou Analytics na página de destino; os eventos devem ser capturados nos conjuntos de dados do AEP |
| Evento de conversão personalizado | O sucesso da campanha é medido por um evento específico de negócios não capturado na Web (por exemplo, compra na loja, interação com a central de atendimento) | Exige que o evento personalizado seja assimilado na AEP e incluído nos conjuntos de dados de relatórios |

#### Navegação na interface

- Relatórios ao vivo: Campanhas > Selecionar campanha > Relatório ao vivo (ou Jornadas > Selecionar jornada > Relatório ao vivo)
- Relatórios históricos: Campanhas > Selecionar campanha > Relatório de todos os tempos (ou Jornadas > Selecionar jornada > Relatório de todos os tempos)

#### Principais detalhes de configuração

- Acesse relatórios ao vivo durante a execução da campanha para monitorar a entrega e o envolvimento em tempo real
- Revise as métricas principais: Enviado, Entregue, Devoluções, Aberturas, Cliques, Cancelamentos de assinatura (email); Enviado, Entregue, Cliques, Erros (SMS); Enviado, Entregue, Aberturas, Ações (push)
- Após a conclusão da campanha, acesse os relatórios históricos (sempre) para obter uma análise abrangente
- Analisar o funnel do delivery: Direcionado > Enviado > Entregue > Aberturas > Cliques
- Revise os motivos de erro e exclusão para identificar problemas de entrega
- Se a experimentação de conteúdo foi ativada, revise os resultados do experimento e aguarde a confiança estatística antes de declarar um vencedor
- Para integração com o CJA, verifique se a visualização de dados do AJO inclui os conjuntos de dados relevantes do AJO (Conjunto de dados de evento de feedback de mensagem, Conjunto de dados de evento de experiência de rastreamento de email)

#### Documentação do Experience League

- [Relatório em tempo real da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Relatório global da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Relatório em tempo real da jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Jornada relatório global](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Relatório de experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Trabalhar com o Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Guia de integração do AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## Considerações de implantação

Esta seção aborda medidas de proteção, armadilhas comuns, práticas recomendadas e decisões de compensação.

### Medidas de proteção e limites

- Máximo de 500 campanhas ativas por sandbox — [medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Máximo de 4.000 definições de segmento por sandbox — [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Máximo de 10 superfícies de canal por tipo de canal por sandbox
- Campanhas acionadas por API oferecem suporte a até 20 recipients de perfil por solicitação de acionador
- As campanhas não podem ser editadas depois de ativadas — duplique e modifique
- Os relatórios ao vivo são atualizados a cada 60 segundos e mostram as últimas 24 horas de dados
- Os relatórios históricos podem levar até 2 horas para serem totalmente preenchidos após a conclusão da campanha
- Máximo de 10 tratamentos (variantes) por experimento de conteúdo
- Máximo de 10 configurações de limite por sandbox
- Máximo de 30 fragmentos de conteúdo por mensagem
- O tamanho máximo do email de 100 KB é recomendado para a entrega ideal
- Os planos de aquecimento de IP devem aumentar gradualmente o volume em 2 a 4 semanas para novos IPs
- As entradas da lista de supressão são retidas por um período configurável (o padrão é 14 dias para rejeições temporárias)

### Armadilhas comuns

- **Envio antes da conclusão do aquecimento de IP:** Novos endereços IP que enviam grandes volumes imediatamente serão sinalizados por ISPs, resultando em uma entrega ruim e em uma possível inclusão na blacklist. Sempre conclua um plano de aquecimento de IP antes que a produção envie em novos IPs.

- **Não testar a personalização em vários perfis:** os tokens do Personalization que funcionam para um perfil de teste podem falhar para outros se o caminho XDM referenciado não existir ou for nulo em alguns perfis. Sempre visualize com vários perfis de teste que representam níveis diferentes de integridade dos dados.

- **Ignorando revisão da lista de supressão:** entradas obsoletas da lista de supressão podem bloquear a entrega para endereços válidos, enquanto entradas ausentes podem resultar na entrega para endereços inválidos que geram rejeições. Revise e limpe a lista de supressão antes de campanhas importantes.

- **Ignorar o limite de frequência para campanhas promocionais:** Enviar uma campanha promocional sem limite de frequência enquanto outras campanhas também estão ativas pode fazer com que perfis recebam várias mensagens em um curto período, gerando cancelamentos de assinatura e reclamações de spam.

- **Agendar campanhas sem verificar a população do público-alvo:** Ativar uma campanha antes de confirmar o público-alvo tem uma população avaliada diferente de zero resulta em zero mensagens entregues. Sempre verifique o tamanho do público-alvo antes da ativação.

- **Usando a avaliação em lote para jornadas acionadas pelo público-alvo:** Se a jornada usar uma entrada Ler Público com avaliação em lote, os perfis não serão inseridos em tempo quase real. Use a avaliação de transmissão para o público-alvo quando a entrada de jornada em tempo quase real for necessária.

- **Não configurar a imposição de consentimento:** Enviar mensagens a perfis sem consentimento de marketing válido viola as regulamentações e prejudica a reputação da capacidade de entrega. Verifique se os campos de consentimento estão preenchidos e aplicados no nível da superfície de canal.

### Práticas recomendadas

- Comece com a Opção A (Campanha programada) para casos de uso de transmissão simples e passe para a Opção B (Jornada acionada pelo público-alvo) somente quando a lógica de pré-entrega ou o tempo orientado pelo comportamento forem necessários
- Sempre inclua um cabeçalho list-unsubscribe com um clique e um link de cancelamento de inscrição no corpo do email para obter conformidade máxima
- Crie fragmentos de conteúdo reutilizáveis para cabeçalhos, rodapés e isenções de responsabilidade legal a fim de garantir a consistência em todas as campanhas
- Definir regras de limite de frequência antes de ativar campanhas para evitar mensagens excessivas em envios simultâneos
- Use a experimentação de conteúdo para otimizar linhas de assunto e CTAs, começando com testes A/B antes de avançar para experimentos multivariados
- Atribua pontuações de prioridade a todas as campanhas ativas para garantir uma resolução de conflitos consistente
- Agende a conclusão da avaliação de público-alvo em lote antes do tempo de execução da campanha para garantir novos dados de público-alvo
- Envie emails de prova e use o recurso de renderização de email para verificar se a mensagem é exibida corretamente nos clientes de email antes da ativação
- Monitore o relatório ao vivo imediatamente após a ativação da campanha para detectar problemas de entrega com antecedência
- Arquive configurações de campanha e experimente resultados para referência futura e otimização contínua

### Decisões de compensação

As soluções de compromisso a seguir devem ser avaliadas ao serem tomadas opções de implementação.

#### Simplicidade vs. flexibilidade

As campanhas programadas (Opção A) oferecem a configuração mais simples, mas sem lógica pré-entrega. As jornadas acionadas por público (Opção B) fornecem lógica de pré-entrega, mas adicionam complexidade de configuração.

- **A opção A favorece:** velocidade de lançamento, simplicidade operacional, autoatendimento para profissionais de marketing
- **A opção B favorece:** Direcionamento comportamental, supressão condicional, extensibilidade para jornadas de várias etapas
- **Recomendação:** comece com a Opção A para envios diretos. Mova para a Opção B somente quando o caso de uso realmente exigir espera, condição ou lógica de ramificação antes da entrega. Evite usar a tela do jornada para envios em lote simples que não se beneficiam dos recursos de orquestração.

#### Atualização do público vs. custo de avaliação

A avaliação de transmissão fornece atualizações de público-alvo quase em tempo real, mas tem restrições de regra de segmento. A avaliação em lote suporta todas as funções de regra de segmento, mas é avaliada em uma programação diária.

- **Favorecimento da transmissão:** atualidade, precisão orientada por comportamento, entrada de jornada acionada por público
- **O lote favorece:** lógica de público-alvo complexa, populações grandes, sobrecarga de avaliação mais baixa
- **Recomendação:** use a avaliação em lote para campanhas agendadas (Opção A) em que a atualização diária é suficiente. Use a avaliação de transmissão para jornadas acionadas pelo público (Opção B) em que os perfis devem entrar conforme se qualificam. Se a expressão de regra do segmento de público-alvo não for qualificada para transmissão, reestruturar as regras ou aceitar a latência no nível do lote.

#### Profundidade do Personalization versus complexidade de criação

A personalização mais profunda (blocos de conteúdo condicional, seções dinâmicas) melhora o engajamento, mas aumenta o esforço de criação e teste.

- **A personalização profunda favorece:** taxas de engajamento mais altas, experiência do cliente mais relevante, melhor conversão
- **A personalização simples favorece:** tempo de inicialização mais rápido, menor carga de testes, risco reduzido de erros de renderização
- **Recomendação:** comece com a personalização básica (nome, categoria de produto relevante) e crie uma camada nos blocos de conteúdo condicional com base nos ganhos de desempenho medidos. Sempre teste todas as variações de conteúdo em vários perfis de teste antes da ativação.

#### Controle de frequência vs. alcance da mensagem

O limite de frequência estrito impede o excesso de mensagens, mas pode suprimir o delivery de campanha para perfis que receberam outras mensagens recentemente.

- **O limite estrito favorece:** qualidade da experiência do cliente, taxas de cancelamento de inscrição mais baixas, reputação da marca
- **O limite relaxado favorece:** Alcance máximo da mensagem, total de impressões mais alto, cobertura da campanha
- **Recomendação:** sempre habilite o limite de frequência para campanhas de marketing. Defina limites específicos do canal (por exemplo, 3 a 5 emails por semana, 1 a 2 SMS por semana). Isentar de regras de limitação somente as mensagens transacionais ou que realmente são críticas em termos de tempo.

## Documentação relacionada

Esta seção fornece links abrangentes para a documentação do [!DNL Experience League], organizados por tópico.

### Campanhas

- [Introdução às campanhas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Criar uma campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Campanhas acionadas por API](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)

### Jornadas

- [Introdução ao jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Ler jornada de público-alvo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)

### Configuração de canais

- [Introdução à configuração de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegar subdomínios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Criar pools de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [Planos de aquecimento de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Configurações de superfície de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Configurar canal de SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configurar canal de notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [Gerenciar lista de supressão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Criação e personalização de mensagens

- [Criar um email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [Criar conteúdo de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Usar componentes de conteúdo do Email Designer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/content-components)
- [Importar ou codificar conteúdo de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/code-content)
- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxe do Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Funções auxiliares](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)

### Gestão de conteúdo

- [Trabalhar com modelos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabalhar com fragmentos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Visualizar e testar o conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [Enviar provas de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/proofs)
- [Renderização de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/email-rendering)

### Experimentação de conteúdo

- [Introdução ao experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Criar um experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Relatório de experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Cálculos estatísticos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

### Gerenciamento de frequência e conflitos

- [Regras de frequência](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Visão geral das regras de negócios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [Introdução ao gerenciamento de conflitos e prioridades](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Pontuações de prioridade](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Identificar possíveis conflitos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [Limite de jornada e arbitragem](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)

### Públicos-alvo e segmentação

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentação de transmissão](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentação de borda](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Composição de público](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Referência do Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### Relatório

- [Relatório em tempo real da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Relatório global da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Relatório em tempo real da jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Jornada relatório global](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabalhar com o Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Guia de integração do AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

### Governança e consentimento de dados

- [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview)
- [Grupo de campos Consentimento e preferências](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
- [Consentimento no Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### Modelagem de dados e identidade

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Noções básicas de composição de esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### Medidas de proteção

- [Medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Medidas de proteção de assimilação](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)

### Tutoriais e introdução

- [Introdução ao Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/get-started)
- [Criar sua primeira campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Criar a primeira jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
