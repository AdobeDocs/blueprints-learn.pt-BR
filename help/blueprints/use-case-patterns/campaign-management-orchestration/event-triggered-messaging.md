---
title: Mensagens acionadas por evento
description: Saiba como fornecer mensagens contextuais em tempo real em resposta a eventos comportamentais ou do sistema.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 75137990-9848-40c0-abf3-adbd21d2de52
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '9040'
ht-degree: 1%

---

# Mensagens acionadas por evento

Este guia fornece um blueprint de implementação abrangente para mensagens acionadas por eventos usando o [!DNL Adobe Journey Optimizer] (AJO), [!DNL Real-Time Customer Data Platform] (RT-CDP) e [!DNL Adobe Experience Platform] (AEP). Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam fornecer mensagens contextuais e em tempo real em resposta a eventos comportamentais ou do sistema.

Use este guia para entender o que configurar, onde existem opções de implementação e quais trade-offs impulsionam cada decisão.

O guia aborda o ciclo de vida completo, desde a assimilação de eventos e a criação de jornadas até a entrega de mensagens e a geração de relatórios de desempenho, com orientação de decisão detalhada para três opções de implementação distintas.

## Visão geral do caso de uso

As mensagens acionadas por eventos fornecem uma mensagem contextual em resposta a um evento comportamental ou do sistema em tempo real. Diferentemente da ativação de mensagem de saída em lote, que envia para um público-alvo pré-avaliado em uma programação, esse padrão escuta um evento qualificado — como um abandono de carrinho, uma sessão de navegação, um envio de formulário ou uma alteração de status do sistema — e insere imediatamente o perfil de acionamento em uma jornada que avalia as condições e entrega uma mensagem.

O padrão depende da transmissão de eventos em tempo real para o AEP (via Web SDK, Mobile SDK ou API do lado do servidor), de uma jornada com uma entrada de evento unitária no AJO e de uma lógica de avaliação de condição que determina se e o que enviar. Normalmente, a mensagem é enviada em minutos após o evento de acionamento, tornando esse padrão ideal para comunicações sensíveis ao tempo e contextualmente relevantes.

As organizações usam esse padrão para responder às ações do cliente em tempo real, aumentando a relevância e gerando taxas de participação e conversão mais altas em comparação às comunicações programadas em lote. Cenários comuns incluem recuperação de carrinho abandonado, acompanhamento pós-compra, mensagens de boas-vindas após o registro e notificações sensíveis ao tempo, como falhas de pagamento ou alertas de queda de preço.

## Principais objetivos de negócios

Os seguintes objetivos de negócios são compatíveis com esse padrão de caso de uso.

**[Recuperar carrinhos abandonados e jornadas](../../business-objectives/customer-experience/recover-abandoned-carts-journeys.md)**

Reenvolva os usuários que abandonaram o durante os fluxos de compra, aplicativo ou inscrição com acompanhamentos oportunos e personalizados.

| KPIs |
| --- |
| Taxas de conversão, receita incremental, envolvimento |

**[Aumentar taxas de conversão](../../business-objectives/revenue-monetization/increase-conversion-rates.md)**

Melhore a porcentagem de visitantes e prospetos que concluem as ações desejadas, como compras, inscrições ou envios de formulários.

| KPIs |
| --- |
| Taxas De Conversão, Conversão De Clientes Potenciais, Custo Por Cliente Potencial |

**[Fornecer experiências personalizadas ao cliente](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**

Personalize conteúdo, ofertas e mensagens para preferências individuais, comportamentos e estágios do ciclo de vida.

| KPIs |
| --- |
| Envolvimento, taxas de conversão, satisfação do cliente (CSAT) |

**[Melhore a integração do cliente](../../business-objectives/customer-experience/improve-customer-onboarding.md)**

Acelere o tempo de implantação para novos clientes com experiências de boas-vindas e jornadas de ativação simplificadas e personalizadas.

| KPIs |
| --- |
| Taxas de engajamento, retenção e conversão |

## Exemplo de casos de uso tático

Os cenários a seguir ilustram como as mensagens acionadas por eventos podem ser aplicadas em diferentes contextos de negócios.

- **Email de abandono de carrinho ou SMS** — Envie uma mensagem de lembrete quando um cliente adicionar itens ao carrinho, mas não concluir a compra em uma janela de tempo definida
- **Acompanhamento de abandono de navegação** — Reenvolva os visitantes que visualizaram produtos ou conteúdo, mas não realizaram uma ação de conversão
- **Venda cruzada ou agradecimento pós-compra** — forneça uma confirmação e uma recomendação de venda cruzada imediatamente após um evento de compra
- **Lembrete de expiração de avaliação** — Notifique os usuários que estão se aproximando do fim de uma avaliação gratuita com mensagens de renovação ou conversão
- **Mensagem de boas-vindas após o registro** — Enviar uma mensagem de integração imediata quando um novo usuário se registrar ou criar uma conta
- **Confirmação de envio de formulário** — Confirmar envios de formulário (solicitações de contato, inscrições, inscrições) com uma confirmação contextual
- **Notificação de falha de pagamento** — Alertar os clientes quando um pagamento recorrente falhar, solicitando que eles atualizem as informações de pagamento
- **Notificação por push de reversão de desinstalação de aplicativo** — Acionar uma mensagem de reversão quando um usuário desinstalar um aplicativo móvel
- **Confirmação de reserva ou compromisso** — Enviar confirmação imediata depois que uma reserva, reserva ou compromisso for agendado
- **Alerta de queda de preço para itens da lista de desejos** — Notifique os clientes quando um produto na lista de desejos cair no preço

## Indicadores-chave de desempenho

Os KPIs a seguir ajudam a medir a eficácia das implementações de mensagens acionadas por eventos.

| KPI | Descrição | Abordagem de medição |
| --- | --- | --- |
| Índice de conversão | Porcentagem de destinatários de mensagens acionadas que concluíram a ação desejada (compra, inscrição, renovação) | Conversões/Mensagens Entregues * 100 |
| Receita incremental | Receita adicional atribuível a mensagens acionadas por eventos em comparação a grupos de controle sem envio | Receita de envios acionados - Linha de base do grupo de controle |
| Taxa de abertura | Porcentagem de mensagens entregues abertas por destinatários | Aberturas/Entregues * 100 |
| Índice de click-through (CTR) | Porcentagem de mensagens entregues que geram pelo menos um clique | Cliques/Entregues * 100 |
| Tempo para conversão | Tempo médio decorrido entre a entrega de mensagens e o evento de conversão | Avg(carimbo de data e hora de conversão - carimbo de data e hora de entrega) |
| Taxa de conclusão da jornada | Porcentagem de perfis que entram na jornada e atingem a etapa de entrega de mensagens (não descartados por condições ou saídas) | Perfis que atingem o delivery/Perfis que entram no jornada * 100 |
| Taxa de supressão de mensagens | Porcentagem de perfis qualificados suprimidos devido a limites de frequência, consentimento ou avaliação de condição | Perfis suprimidos/Total de perfis qualificados * 100 |
| Taxa de rejeição | Porcentagem de mensagens que não puderam ser entregues devido a devoluções permanentes ou temporárias | Devoluções / Enviado * 100 |

## Padrão do caso de uso

Esta seção descreve o padrão principal e a cadeia de funções que direciona as mensagens acionadas por eventos.

**Mensagens acionadas por Evento**

Analise um evento comportamental ou de sistema em tempo real e entregue uma mensagem contextual ao perfil de acionamento.

**Cadeia De Funções:** Assimilação De Evento > Entrada De Jornada > Avaliação De Condição > Entrega De Mensagem > Relatórios

## Aplicativos

Os seguintes aplicativos da Adobe são usados neste padrão de caso de uso.

- **[!DNL Adobe Journey Optimizer] (AJO)** — Orquestração de Jornadas com entrada de evento unitária, avaliação de condição, etapas de espera, criação de mensagens, configuração de canal, governança de frequência e relatórios de entrega
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** — Avaliação de público-alvo para filtragem baseada em condição em jornadas, imposição de consentimento e governança, enriquecimento de perfil
- **[!DNL Adobe Experience Platform] (AEP)** — Assimilação de eventos em tempo real via Web SDK, Mobile SDK ou API do lado do servidor; modelagem de dados; resolução de identidade; Edge Network

## Funções básicas

Os seguintes recursos básicos devem estar em vigor para esse padrão de caso de uso. Para cada função, o status indica se ele é tipicamente necessário, se presume ser pré-configurado ou se não é aplicável.

| Função de base | Status | O que deve estar em vigor | Referência do Experience League |
| --- | --- | --- | --- |
| Administração e governança | Presumido em vigor | sandbox da AJO provisionada com configuração de canal ativa. Permissões de criação e publicação de jornada atribuídas à equipe de implementação. Funções de usuário configuradas para gerenciamento de jornadas, criação de conteúdo e administração de canais. | [Visão geral das sandboxes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/home), [Visão geral do controle de acesso](https://experienceleague.adobe.com/pt-br/docs/experience-platform/access-control/home) |
| Preparação e modelagem de dados | Obrigatório | Um esquema XDM ExperienceEvent deve capturar o evento de acionamento com todos os campos contextuais necessários para avaliação de condição e personalização de mensagem (por exemplo, `commerce.productListAdds` para eventos de carrinho, detalhes do produto, valor do carrinho). O esquema deve ser ativado para o Perfil de cliente em tempo real. Um conjunto de dados correspondente deve ser criado e ativado para perfil. | [Visão geral do sistema XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/home), [noções básicas de composição de esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| Fontes de dados e coleção | Obrigatório | A transmissão de eventos em tempo real deve ser configurada — Web SDK para eventos da Web, Mobile SDK para eventos de aplicativo ou API do Edge Network Server para eventos do sistema. Um fluxo de dados deve ser configurado com os serviços da AEP e da AJO ativados, roteando eventos para o conjunto de dados correto. Essa é uma dependência crítica, pois o padrão depende da assimilação de eventos em tempo real. | [Visão geral do Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/web-sdk/home), [Configurar sequências de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure) |
| Configuração de identidade e perfil | Obrigatório | O evento de acionamento deve estar associado a uma identidade conhecida (email, ID de CRM ou sessão autenticada) para que a jornada possa resolver o perfil e entregar a mensagem. Os namespaces de identidade devem existir para os identificadores usados pelo evento de acionamento. Eventos anônimos exigem a identificação por meio do gráfico de identidade antes que uma mensagem possa ser entregue. Uma política de mesclagem deve ser configurada. | [Visão geral do Serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| Definição e segmentação do público-alvo | Recomendado | Embora não seja estritamente necessário para jornadas acionadas por eventos (a entrada se baseie em eventos, não no público-alvo), os segmentos de público-alvo podem ser usados para avaliação de condição na jornada (por exemplo, enviar somente se o perfil estiver em um segmento de &quot;cliente de alto valor&quot;, ou suprimir se o perfil estiver em um segmento &quot;contatado recentemente&quot;). A avaliação de transmissão é recomendada para verificações de associação de segmento em tempo real no jornada. | [Visão geral do Serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [Segmentação de transmissão](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/methods/streaming-segmentation) |

## Funções de suporte

Os recursos a seguir aumentam esse padrão de caso de uso, mas não são necessários para a execução principal.

| Função de suporte | Status | Por que é importante | Referência do Experience League |
| --- | --- | --- | --- |
| Criação de atributo calculado/derivado | Recomendado | Atributos calculados, como contagem de abandono do carrinho, dias desde a última compra, valor médio de pedido e total de compra por vida útil, melhoram a avaliação da condição e a personalização nas jornadas acionadas. Esses agregados comportamentais permitem decisões de direcionamento mais precisas (por exemplo, diferenciar os abandonadores pela primeira vez dos abandonadores repetidos). | [Visão geral dos atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Gerenciamento do ciclo de vida dos dados | Recomendado | A expiração dos dados do evento deve ser configurada para eventos comportamentais transitórios (exibições de página, pesquisas, cliques) para gerenciar os custos de armazenamento e a conformidade. Os campos de esquema de consentimento devem estar presentes para a imposição de aceitação/recusa específica do canal durante a entrega da mensagem. | [Visão geral do Gerenciamento Avançado do Ciclo de Vida dos Dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [Expirações do conjunto de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-lifecycle/ui/dataset-expiration) |
| Rotulagem e aplicação de uso de dados | Recomendado | Os rótulos de governança nos campos de evento e perfil garantem a personalização em conformidade. Se as mensagens acionadas incluírem conteúdo personalizado usando PII ou dados comportamentais, os rótulos de uso de dados e as políticas de governança deverão ser revisados para evitar o uso não autorizado de dados no conteúdo da mensagem. | [Visão geral da governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/home), [Visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview) |
| Monitoramento e capacidade de observação | Incluído | O monitoramento da execução da jornada faz parte da fase de relatórios. Além disso, configure alertas para falhas de assimilação de eventos ou atrasos de processamento de jornadas para detectar problemas de pipeline que impediriam o envio de mensagens acionadas. | [Visão geral dos alertas](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/alerts/overview), [Visão geral dos Insights de observação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/home) |
| Relatórios e análise | Incluído | Os relatórios de desempenho da jornada são abordados na fase de relatórios. Para uma análise mais profunda da eficácia de mensagens acionadas em canais e ao longo do tempo, configure as conexões e os espaços de trabalho do CJA para analisar a atribuição de conversão, o tempo de conversão e o desempenho do canal. | [visão geral do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [guia de integração do AJO + CJA](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/reporting/channel-report/cja-ajo) |

## Funções do aplicativo

Este plano exerce as seguintes funções do Catálogo de Funções da Aplicação. As funções são mapeadas para fases de implementação em vez de etapas numeradas.

### [!DNL Journey Optimizer] (AJO)

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Journey Orchestration | Criação e configuração do Jornada | Crie uma jornada com entrada de evento unitária, configure o evento de qualificação, adicione nós de condição, etapas de espera, ações de mensagem, critérios de saída e regras de reentrada |
| Configuração de canais | Configuração da Superfície de Canal | Configurar ou validar superfícies dos canais (email, SMS, push) incluindo delegação de subdomínio, pools de IP, configurações de remetente e gerenciamento de lista de supressão |
| Criação de mensagens | Criação do conteúdo da mensagem | Crie conteúdo de mensagem contextual com personalização orientada por eventos, blocos de conteúdo condicional e fragmentos reutilizáveis |
| Frequência e regras de negócios | Criação e configuração do Jornada (Opção C) | Configure limites de frequência e regras de desduplicação para evitar mensagens excessivas de fontes de evento de alta frequência |
| Gerenciamento de conflitos e prioridades | Criação e configuração do Jornada | Atribuir pontuações de prioridade e configurar a detecção de conflitos para jornadas que competem pelos mesmos perfis |
| Relatórios e análise de desempenho | Relatórios e monitoramento | Monitore métricas de entrega de jornadas por meio de relatórios dinâmicos e históricos; acesse dados de desempenho programáticos por meio do CJA |

### [!DNL Real-Time CDP] (RT-CDP)

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Avaliação de público | Configuração Básica (F5) | Avaliar os segmentos de público-alvo usados para filtragem baseada em condições na jornada (por exemplo, segmentos de alto valor do cliente, segmentos de supressão) |
| Consentimento e aplicação de governança | Configuração básica (S2/S3) | Imponha preferências de consentimento e políticas de governança de uso de dados durante a entrega de mensagens para garantir comunicações em conformidade |

## Pré-requisitos

Conclua o seguinte antes de iniciar a implementação.

- [ ] sandbox do AJO provisionada com criação de jornada e permissões de publicação (F1)
- [ Esquema XDM ExperienceEvent ] capturando o evento de acionamento com campos contextuais, habilitado para Perfil de Cliente em Tempo Real (F2)
- [ ] Transmissão contínua de eventos em tempo real configurada via Web SDK, Mobile SDK ou API de servidor do Edge Network com eventos de roteamento de sequência de dados para o conjunto de dados correto do AEP (F3)
- [ ] Namespaces de identidade configurados para os identificadores no evento de acionamento; regras de vinculação de identidade em vigor (F4)
- [ ] Superfície de canal (email, SMS ou push) configurada e validada com um envio de teste bem-sucedido
- [ ] Conteúdo da mensagem criado, revisado e testado com perfis de exemplo
- [ ] Campos de consentimento preenchidos em perfis para o canal de destino (por exemplo, `consents.marketing.email.val`)
- [ ] Se estiver usando a filtragem de público com base em condições (Opção B/C), os segmentos de público avaliados por transmissão serão definidos e avaliados ativamente

## Opções de implementação

Esta seção descreve três opções de implementação para mensagens acionadas por eventos. Cada opção se baseia na anterior, adicionando recursos adicionais.

### Opção A: Mensagem simples acionada por evento

**Recomendado para:** respostas imediatas por mensagem única em que não é necessária nenhuma lógica condicional ou de atraso — confirmação de pedido, email de boas-vindas, confirmação de envio de formulário, confirmação de reserva.

**Como funciona:**

A jornada escuta um evento de qualificação por meio de um nó de entrada de evento unitário. Quando o evento é recebido, o perfil entra na jornada, passa pela avaliação mínima da condição (verificação de consentimento, verificação da existência do perfil) e recebe imediatamente uma única mensagem por meio do nó de ação do canal configurado.

Essa é a variante de implementação mais simples. A tela de jornada contém um nó de entrada de evento, um nó de condição opcional para verificações básicas de elegibilidade, um nó de ação de mensagem única e um nó final. Não há etapas de espera, ramificações complexas e verificações de conversão. Normalmente, a mensagem é entregue em segundos a minutos após o evento de acionamento.

Os dados do evento de acionamento (nome do produto, total do pedido, detalhes do formulário) podem ser usados para personalização da mensagem por meio de atributos contextuais no editor de personalização. Essa abordagem maximiza a velocidade de entrega e minimiza a complexidade da jornada.

**Principais considerações:**

- A mensagem é enviada independentemente de o cliente se autoconverter após o evento (sem verificação de conversão)
- Mais adequado para eventos que inerentemente exigem uma resposta imediata (confirmações, confirmações)
- As regras de reentrada devem ser configuradas cuidadosamente — para mensagens no estilo de confirmação, permita a reentrada para que cada evento gere uma mensagem; para mensagens no estilo de boas-vindas, impeça a reentrada

**Vantagens:**

- Tempo de entrega mais rápido (segundos a minutos após o evento)
- Configuração de jornada mais simples com peças móveis mínimas
- Menor risco de falhas na jornada ou perfis paralisados
- Fácil de testar e manter

**Limitações:**

- Impossibilidade de verificar se o cliente se converteu automaticamente antes de enviar
- Não é possível incorporar a lógica condicional de tempo atrasado
- Pode gerar mensagens desnecessárias se o evento ocorrer com frequência sem governança de frequência

**Experience League:**

- [Criar uma jornada](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Eventos gerais](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)

### Opção B: Mensagem condicional acionada por evento com espera

**Recomendado para:** Respostas condicionais atrasadas em que o cliente deve ter tempo para se autoconverter antes de receber a mensagem — abandono de carrinho (aguarde de 1 a 4 horas e, em seguida, verifique se o carrinho ainda está abandonado), abandono de navegação (aguarde 24 horas, verifique se a compra foi feita), expiração de avaliação (aguarde até a data de expiração se aproximar).

**Como funciona:**

A jornada escuta um evento de qualificação, insere o perfil e introduz um período de espera antes de avaliar as condições. Após a espera, um nó de condição verifica se o cliente se converteu automaticamente (por exemplo, concluiu a compra, renovou a assinatura) ou se o contexto original ainda é válido. Somente se a condição for atendida (por exemplo, o carrinho ainda abandonado) a jornada continuará para a entrega da mensagem.

A tela de jornada contém um nó de entrada de evento, um nó de espera (duração configurável ou data/hora específica), um nó de condição que verifica um evento de conversão ou alteração de estado do perfil, caminhos de ramificação (enviar mensagem versus sair sem enviar), um nó de ação de mensagem no caminho qualificado e um nó final em cada ramificação. Os critérios de saída podem ser configurados para remover perfis automaticamente da jornada se o evento de conversão ocorrer durante o período de espera, eliminando a necessidade da verificação de condição explícita.

Essa abordagem reduz as mensagens desnecessárias, pois dá aos clientes tempo para se autoconverter, melhorando a experiência do cliente e aumentando a relevância percebida das mensagens enviadas.

**Principais considerações:**

- A duração da espera afeta significativamente as taxas de conversão — esperas mais curtas (1 a 2 horas) produzem maior urgência, mas envios mais desnecessários; esperas mais longas (24 a 48 horas) reduzem o volume, mas podem perder a janela de relevância
- A avaliação de condição exige que o evento de conversão seja capturado no AEP e associado à mesma identidade de perfil
- Os critérios de saída fornecem uma alternativa mais limpa para nós de condição explícitos para verificação de conversão
- As regras de reentrada devem considerar o período de espera — um perfil não deve inserir novamente a jornada enquanto já está aguardando

**Vantagens:**

- Reduz mensagens desnecessárias verificando a autoconversão
- Produz comunicações de maior qualidade e mais relevantes
- Oferece suporte a casos de uso sensíveis ao tempo com janelas de atraso configuráveis
- Os critérios de saída permitem a remoção automática da jornada na conversão

**Limitações:**

- Maior complexidade de jornada com nós de espera e condição
- Os perfis ocupam slots do jornada durante períodos de espera (sujeitos ao tempo limite de jornada de 91 dias)
- Exige que o evento de conversão seja assimilado na AEP dentro da janela de espera para uma avaliação de condição precisa
- Tempo de entrega mais longo em comparação com a opção A

**Experience League:**

- [Atividade aguardar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Atividade de condição](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Critérios de saída](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)

### Opção C: acionado por eventos com governança de frequência

**Recomendado para:** fontes de evento de alta frequência em que a fadiga da mensagem é uma preocupação — exibições de página, exibições de produtos, consultas de pesquisa, adições repetidas do carrinho. Pode ser aplicada como uma sobreposição sobre a Opção A ou a Opção B.

**Como funciona:**

Essa opção adiciona o controle de frequência à Opção A ou à Opção B para evitar o excesso de mensagens. Eventos comportamentais de alta frequência (como visualizações de produto ou adições repetidas ao carrinho) podem acionar a jornada várias vezes em um curto período. Sem a governança de frequência, um perfil pode receber mensagens duplicadas ou em excesso.

A governança de frequência é implementada por meio de dois mecanismos complementares: regras de negócios do AJO (limites de frequência) que limitam quantas mensagens um perfil recebe por canal e por período de tempo, e regras de reentrada no nível da jornada que definem um período de controle antes que um perfil possa entrar novamente na mesma jornada. As regras de negócios operam no nível da organização e impõem limites em todas as campanhas e jornadas (por exemplo, máximo de 3 emails por semana), enquanto a lista suspensa de reentrada opera no nível de jornada individual (por exemplo, um perfil não pode inserir novamente essa jornada específica dentro de 72 horas após a última entrada).

Além disso, o gerenciamento de conflitos e prioridades pode ser configurado para atribuir pontuações de prioridade à jornada acionada, garantindo que, quando várias jornadas ou campanhas competem pelo mesmo perfil, a comunicação de maior prioridade vença.

**Principais considerações:**

- Os limites de frequência devem ser equilibrados entre evitar fadiga e garantir que mensagens acionadas importantes sejam entregues
- Recomendam-se limites específicos para canais — email, SMS e push têm limites de fadiga diferentes
- O resfriamento da reentrada do Jornada e os limites de frequência no nível da organização funcionam juntos; ambos devem ser configurados
- As pontuações de prioridade determinam qual comunicação vence quando os limites são atingidos — as jornadas de prioridade mais alta devem receber pontuações mais altas

**Vantagens:**

- Evita a fadiga de mensagens de fontes de eventos de alta frequência
- Mantém a reputação da marca e a satisfação do assinante
- Os limites a nível de organização fornecem uma rede de segurança em todas as campanhas e jornadas
- A pontuação de prioridade garante que as mensagens mais importantes sejam entregues quando as limitações forem atingidas

**Limitações:**

- Alguns perfis qualificados serão suprimidos, possivelmente com mensagens relevantes ausentes
- A configuração de limite de frequência adiciona complexidade administrativa
- Caps podem interagir inesperadamente com outras campanhas e jornadas ativas que compartilham o mesmo canal
- Requer monitoramento e ajuste contínuos à medida que o portfólio de mensagens muda

**Experience League:**

- [Regras de frequência](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Visão geral das regras de negócios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [Pontuações de prioridade](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Gerenciamento de entradas de jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)

### Comparação de opções

A tabela a seguir compara as três opções de implementação entre os principais critérios.

| Critérios | Opção A: acionado por evento simples | Opção B: Condicional com Espera | Opção C: governança de frequência |
| --- | --- | --- | --- |
| Melhor para | Confirmações e confirmações imediatas | Recuperação de abandono, respostas condicionais atrasadas | Fontes de eventos de alta frequência, ambientes com várias jornadas |
| Complexo | Baixa | Médio | Medium-Alto (adiciona a A ou B) |
| Latência da mensagem | Segundos a minutos | Minutos a horas/dias (espera configurável) | Idêntica à opção subjacente (A ou B) |
| Verificação de autoconversão | Não | Sim (por condição ou critério de saída) | Depende da opção subjacente |
| Proteção de frequência | Nenhuma (a menos que combinada com C) | Nenhuma (a menos que combinada com C) | Sim — tampas de canais e redução de reentrada |
| Jornada nós da tela de desenho | 3-4 (evento, condição opcional, ação, fim) | 5-7 (evento, espera, condição, ramificações, ação, finalizações) | Igual a A ou B, mais configuração de regra de negócios |
| Exige | Esquema de evento, superfície de canal, conteúdo da mensagem | Toda a opção A + assimilação do evento de conversão | Todas as opções A ou B + configuração da regra de frequência |

### Escolha a opção certa

Use a orientação de decisão a seguir para selecionar a opção de implementação correta.

1. **A mensagem precisa ser enviada imediatamente e sem atraso?** Em caso afirmativo, comece com **Opção A**. As mensagens de confirmação, os emails de boas-vindas e as confirmações normalmente não exigem um período de espera.

2. **O cliente deve ter tempo para realizar a autoconversão antes de receber a mensagem?** Em caso afirmativo, escolha **Opção B**. Os casos de uso de abandono do carrinho, abandono de navegação e expiração de avaliação se beneficiam de um período de espera que permite que os clientes concluam a ação por conta própria.

3. **O evento de acionamento é de alta frequência (ocorre várias vezes por sessão ou por dia para o mesmo perfil)?** Em caso afirmativo, adicione a **Opção C** como uma sobreposição sobre a Opção A ou B. Exibições de produtos, exibições de páginas e eventos de pesquisa podem gerar grandes volumes de acionadores que exigem proteção de frequência.

4. **Várias jornadas e campanhas acionadas estão ativas na sandbox?** Em caso afirmativo, adicione a **Opção C**, independentemente da frequência do evento, para gerenciar a carga de comunicação entre jornadas e evitar a fadiga do canal.

Na prática, a maioria das implementações de produção usa a opção B + C para casos de uso no estilo de abandono (espera condicional com governança de frequência) e a opção A + C para casos de uso no estilo de confirmação (envio imediato com governança de frequência como uma rede de segurança).

## Fases de implementação

As fases a seguir abordam a implementação completa de mensagens acionadas por eventos.

### Fase 1: configurar o esquema de evento e a coleta de dados

**Função do Aplicativo:** AEP: Modelagem de Dados (F2), AEP: Fontes de Dados e Coleção (F3)

**O que você configurará:** o esquema XDM ExperienceEvent que captura o evento de acionamento, o conjunto de dados que armazena esses eventos e o pipeline de coleta de dados em tempo real (Web SDK, Mobile SDK ou Server API) que transmite eventos para o AEP. Essa fase estabelece a base de dados que a jornada ouvirá.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: acionando tipo de evento**
>
>Que evento aciona a mensagem? O tipo de evento determina os campos de esquema necessários e o método de coleta.
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Evento do Commerce (adição, compra, check-out do carrinho) | Casos de uso de comércio eletrônico — abandono de carrinho, pós-compra | Requer o grupo de campos do Commerce com `productListItems`, `cart`, `order` campos |
>| Evento de interação na Web (exibição de página, exibição de produto) | Abandono de navegação, acionadores de engajamento de conteúdo | Requer o grupo de campos Detalhes da Web com `webPageDetails`, `webInteraction` campos |
>| Evento de aplicativo (instalação, desinstalação e ação no aplicativo) | Acionadores de engajamento móvel | Requer implementação do Mobile SDK e grupo de campos Aplicativo |
>| Evento do sistema (falha de pagamento, alteração de assinatura, atualização de status) | Notificações operacionais | Exige API do lado do servidor ou conector de origem para assimilar eventos do sistema |
>| Evento de envio de formulário | Geração de lead, confirmação da inscrição | Requer o grupo de campos personalizado para capturar campos de dados de formulário |

>[!NOTE]
>
>**Decisão: método de coleta**
>
>Como o evento de acionamento será capturado e transmitido para o AEP?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| SDK da Web | Eventos comportamentais baseados na Web (adições ao carrinho, exibições de página, envios de formulários) | Requer a instalação do Web SDK no site; os eventos são transmitidos em tempo real via Edge Network |
>| SDK móvel | Eventos de aplicativos para dispositivos móveis (aberturas de aplicativos, ações no aplicativo, registro de token de push) | Requer integração do Mobile SDK no aplicativo nativo ou no invólucro do React Native |
>| API do servidor do Edge Network | Eventos do sistema do lado do servidor (processamento de pagamentos, gerenciamento de assinaturas, acionadores de back-end) | Nenhuma dependência do lado do cliente; eventos enviados de sistemas de back-end da organização |
>| Conector do Source | Eventos de sistemas externos (CRM, automação de marketing, plataformas herdadas) | Normalmente baseada em lote; pode não ser compatível com o acionamento em tempo real, a menos que seja compatível com streaming |

**Navegação da interface do usuário:** Coleta de Dados > Datastreams > Novo Datastream (para configuração de datastream); Esquemas > Criar esquema (para esquema de evento); Conjuntos de Dados > Criar conjunto de dados a partir de esquema (para criação de conjunto de dados)

**Detalhes de configuração da chave:**

- O schema do evento deve incluir todos os campos necessários para a avaliação da condição de jornada e a personalização da mensagem
- A sequência de dados deve ter os serviços [!DNL Adobe Experience Platform] e [!DNL Adobe Journey Optimizer] habilitados
- O conjunto de dados deve ser ativado para o Perfil do cliente em tempo real para que os eventos sejam associados a perfis unificados
- Os dados do evento devem incluir um campo de identidade (email, ID de CRM, ECID) que possa ser resolvido para um perfil conhecido

**Documentação do Experience League:**

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/home)
- [Configurar sequências de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Visão geral do Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/web-sdk/home)
- [Visão geral da API do Edge Network Server](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [Visão geral da assimilação de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/streaming/overview)

### Fase 2: configurar identidade e perfil

**Função do Aplicativo:** AEP: Configuração de Identidade e Perfil (F4)

**O que você configurará:** Namespaces de identidade para os identificadores no evento de acionamento, designação de identidade principal no esquema do evento, regras de vinculação de identidade para resolução entre dispositivos e uma política de mesclagem para unificação de perfis. Isso garante que o evento de acionamento esteja associado a um perfil de cliente unificado, para que a jornada possa resolver as informações de contato e entregar a mensagem.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: identidade principal do esquema de evento**
>
>Qual campo de identidade no evento de acionamento deve servir como identidade principal para a resolução do perfil?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Endereço de email | Eventos de sessões da Web autenticadas ou formulários nos quais o email é capturado | Resolução direta para uma identidade contatável; caminho mais simples para a entrega de e-mail |
>| ID do CRM | Eventos de sistemas autenticados em que a ID do CRM é o identificador principal | Requer a criação de namespace da ID do CRM; o perfil deve ter um email ou telefone vinculado para entrega de mensagens |
>| ECID (Experience Cloud ID) | Eventos da Web ou do aplicativo anônimos em que nenhuma identidade autenticada está disponível | Requer a identificação de identidade para vincular a ECID a uma identidade conhecida; as mensagens não podem ser enviadas apenas para ECID |
>| Número de telefone | Eventos de interações móveis ou da central de atendimento | Suporta entrega de SMS; requer namespace de telefone |

**Navegação da interface do usuário:** Identidades > Criar namespace de identidade; Esquemas > Selecionar esquema > Selecionar campo > Identidade > Definir como identidade primária; Perfis > Políticas de mesclagem

**Detalhes de configuração da chave:**

- Eventos anônimos (somente ECID) não podem acionar a entrega de mensagens até que a ECID esteja vinculada a uma identidade contatável conhecida (email, telefone) por meio do gráfico de identidade
- A política de mesclagem usada pelo AJO deve ser consistente com a usada para a avaliação do público-alvo
- Para mensagens acionadas pela Web, verifique se o gráfico de identidade vincula a ECID a identidades autenticadas por meio de eventos de logon

**Documentação do Experience League:**

- [Visão geral dos namespaces de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/namespaces)
- [Regras de vinculação do gráfico de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### Fase 3: Configurar superfícies do canal

**Função do Aplicativo:** AJO: Configuração de Canal

**O que você configurará:** a superfície de canal (predefinição) que define a infraestrutura de envio da mensagem disparada: delegação de subdomínio, pool de IP, identidade do remetente, endereço para resposta, tratamento de cancelamento de inscrição e credenciais específicas de canal (provedor SMS, certificados push). Uma superfície de canal válida deve existir para que o conteúdo da mensagem possa ser criado ou as jornadas possam ser publicadas.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: canal de mensagem**
>
>Qual canal a mensagem acionada usará?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Email | Casos de uso de mensagens mais acionados: recuperação de abandono, confirmações, integração | Requer delegação de subdomínio, pool de IP, configuração do remetente; oferece suporte a conteúdo avançado de HTML e personalização |
>| SMS | Notificações sensíveis ao tempo, alertas concisos, públicos-alvo com alto engajamento de SMS | Requer integração do provedor de SMS (Sinch, Twilio, Infobip); está sujeito a limites de caracteres e requisitos de consentimento mais rigorosos |
>| Notificação por push | Engajamento no aplicativo móvel, reengajamento dos usuários do aplicativo | Requer configuração de credencial de push (APNs para iOS, FCM para Android); o usuário deve ter o aplicativo instalado com o push habilitado |
>| Vários canais | Estratégia abrangente de engajamento usando preferência de canal ou lógica de fallback | Requer várias superfícies de canal; a seleção de canal pode ser gerenciada por meio de nós de condição de jornada |

>[!NOTE]
>
>**Decisão: método de delegação de subdomínio (email)**
>
>Como o subdomínio de envio de email deve ser delegado à Adobe?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Delegação completa | A organização deseja que a Adobe gerencie todos os registros DNS para o subdomínio de envio | Configuração mais simples; o Adobe gerencia registros SPF, DKIM e DMARC automaticamente |
>| Delegação CNAME | A organização deseja manter o controle de DNS enquanto aponta para a infraestrutura da Adobe | Requer gerenciamento manual de registros DNS; oferece mais controle organizacional sobre DNS |

**Navegação da interface do usuário:** Administração > Canais > Subdomínios (para configuração de subdomínio); Administração > Canais > Pools de IP (para configuração de pool de IP); Administração > Canais > Superfícies de canal > Criar superfície (para criação de superfície)

**Detalhes de configuração da chave:**

- A verificação de subdomínio e a propagação de DNS podem levar até 48 horas
- Novos pools de IP exigem um plano de aquecimento (2 a 4 semanas de aumento gradual de volume)
- Configurar cabeçalhos de lista de cancelamento de inscrição com um clique para conformidade de email
- Para SMS, configure as credenciais do provedor antes de criar a superfície de canal SMS
- Para push, configure APNs e credenciais do FCM antes de criar a superfície de canal de push

**Documentação do Experience League:**

- [Introdução à configuração de email](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegar subdomínios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Criar pools de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [Configurar superfícies do canal](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Configurar canal de SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configurar canal de notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Fase 4: Criar conteúdo da mensagem

**Função do Aplicativo:** AJO: Criação de Mensagens

**O que você configurará:** o conteúdo da mensagem que será entregue pela jornada, incluindo design de layout, tokens de personalização usando atributos de perfil e evento, blocos de conteúdo condicionais, fragmentos reutilizáveis (cabeçalhos, rodapés, avisos de isenção legal) e pré-visualização e teste de conteúdo.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: abordagem de conteúdo**
>
>Como o conteúdo da mensagem deve ser criado?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Iniciar com base em um modelo existente | Existem modelos organizacionais e é necessária a consistência da marca | Caminho mais rápido para a criação de conteúdo; garante a conformidade com a marca; as alterações no modelo se propagam para novas mensagens |
>| Criar do zero no Email Designer | Layout personalizado necessário para esta mensagem específica acionada | Controle criativo completo; editor visual arrastar e soltar; mais lento, porém mais flexível |
>| Importar HTML | O conteúdo é projetado por uma equipe ou agência externa e fornecido como HTML | Requer experiência em codificação do HTML; pode não oferecer suporte total a todos os recursos do Designer de email |

>[!NOTE]
>
>**Decisão: Personalização de evento**
>
>Quais dados de evento devem ser usados no conteúdo da mensagem?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Atributos contextuais de evento | A mensagem deve incluir detalhes do evento de acionamento (nome do produto, valor do carrinho, campos de formulário) | Usar atributos de evento contextual no editor de personalização; os dados vêm da carga útil do evento de acionamento |
>| Atributos do perfil | A mensagem deve incluir dados a nível de perfil (nome, nível de fidelidade, local) | Use atributos de perfil por meio de caminhos XDM (por exemplo, `profile.person.name.firstName`); os dados vêm do perfil unificado |
>| Atributos de evento e perfil | A mensagem deve combinar o contexto do evento com a personalização do perfil | A abordagem mais comum para mensagens acionadas garante relevância (evento) e personalização (perfil) |

**Navegação da interface do usuário:** Gerenciamento de conteúdo > Modelos de conteúdo > Procurar (para seleção de modelo); Ação de campanha ou Jornada > Editar conteúdo > Email Designer (para design de conteúdo); Selecione componente de texto > ícone Personalization (para adicionar personalização)

**Detalhes de configuração da chave:**

- Usar atributos contextuais para personalizar com dados do evento de acionamento (por exemplo, nome do produto, valor do carrinho)
- Usar atributos de perfil para nome, preferências e dados de fidelidade
- Configurar blocos de conteúdo condicional para variar o conteúdo por segmento de perfil ou atributo (por exemplo, CTA diferente para membros do programa de fidelidade)
- Criar fragmentos reutilizáveis para cabeçalhos, rodapés e isenções de responsabilidade legal compartilhados entre mensagens acionadas
- Visualize com vários perfis de teste para verificar se a personalização é renderizada corretamente
- Enviar provas aos participantes internos antes de publicar a jornada

**Documentação do Experience League:**

- [Criar conteúdo de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxe do Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabalhar com modelos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabalhar com fragmentos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Visualizar e testar o conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### Fase 5: criar e configurar a jornada

**Função do Aplicativo:** AJO: Journey Orchestration, AJO: Frequência e Regras de Negócios (Opção C), AJO: Gerenciamento de Conflitos e Prioridades

**O que você configurará:** A jornada que escuta o evento de acionamento e orquestra a entrega de mensagens. Esta é a fase de implementação principal em que a tela de jornada é projetada com o nó de entrada do evento, nós de condição, etapas de espera (para a Opção B), nós de ação de mensagem e critérios de saída. Esta fase abrange também a governação da frequência (opção C) e a configuração de conflitos/prioridades.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: regras de reentrada**
>
>Um perfil pode inserir novamente essa jornada se o evento de acionamento ocorrer novamente?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Permitir reentrada (com controle) | O evento pode reaparecer legitimamente e cada ocorrência justifica uma mensagem (por exemplo, cada abandono de carrinho deve acionar uma mensagem de recuperação) | Defina um período de resfriamento (mínimo de 5 minutos) para evitar a reentrada rápida de eventos duplicados; o resfriamento típico varia de 1 hora a 72 horas |
>| Nenhuma reentrada | A mensagem deve ser enviada apenas uma vez por perfil, independentemente da recorrência do evento (por exemplo, mensagem de boas-vindas após o primeiro registro) | O perfil é excluído permanentemente após a conclusão da primeira jornada; apropriado para mensagens de ciclo de vida únicas |

>[!NOTE]
>
>**Decisão: Duração da espera (somente Opção B)**
>
>Por quanto tempo a jornada deve aguardar antes de avaliar as condições e enviar a mensagem?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Espera curta (1-4 horas) | Casos de uso de alta urgência, como abandono de carrinho, em que o acompanhamento imediato é eficaz | Maior volume de mensagens; pode capturar alguns autoconversores; melhor para recuperação de carrinho de alto valor |
>| Espera do Medium (12 a 24 horas) | Casos de uso de urgência moderada, como abandono de navegação ou envolvimento de conteúdo | Abordagem equilibrada; reduz envios desnecessários e mantém a relevância |
>| Longa espera (2-7 dias) | Casos de uso de baixa urgência como lembretes de expiração de avaliação ou check-ins periódicos | Menor volume de mensagens; maior risco de perda de relevância contextual |
>| Data/hora personalizada | Casos de uso vinculados a uma data específica (por exemplo, enviar 3 dias antes da data de expiração do teste) | Aguardar uma data/hora calculada; usa o editor de expressão personalizado |

>[!NOTE]
>
>**Decisão: critérios de saída**
>
>Sob quais condições um perfil deve ser removido da jornada antes de atingir a ação de mensagem?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Evento de conversão (por exemplo, compra concluída) | Abandono de carrinho ou navegação onde a meta é conversão | O perfil sai automaticamente quando o evento de conversão é detectado; abordagem mais limpa para a Opção B |
>| Alteração de associação de público | O perfil deve sair se eles deixarem um segmento qualificado | Requer um público avaliado por transmissão que é atualizado em tempo quase real |
>| Tempo limite da Jornada (máximo de 91 dias) | Comportamento padrão — o perfil sai após a duração máxima da jornada | Rede de segurança; não deve ser o principal mecanismo de saída para jornadas acionadas de curta duração |
>| Nenhum critério de saída explícito | Confirmações simples (opção A) em que cada perfil qualificado deve receber a mensagem | O perfil sai naturalmente após a ação da mensagem e o nó final |

>[!NOTE]
>
>**Decisão: governança de frequência (Opção C)**
>
>Quantas mensagens acionadas um perfil deve receber por período de tempo?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Limites específicos do canal (por exemplo, 3 emails/semana, 1 SMS/dia) | Canais diferentes têm limites de fadiga diferentes | Abordagem recomendada; respeita o nível de intrusividade de cada canal |
>| Limite global (por exemplo, 5 mensagens/semana em todos os canais) | Governança simplificada em todos os tipos de comunicação | Mais fácil de gerenciar, mas com menos nuances; pode restringir excessivamente os canais menos intrusivos |
>| Somente o controle de reentrada no nível da jornada | Governança de frequência necessária para essa jornada específica, mas não em toda a organização | Implementação mais simples; não protege contra fadiga entre jornadas |

Navegação da **interface do usuário:** Jornadas > Criar Jornada (para criação de jornada); tela de Jornada > Arrastar atividade do evento (para entrada de evento); tela de Jornada > Arrastar atividade &quot;Aguardar&quot; (para configuração de espera); tela de Jornada > Arrastar atividade &quot;Condição&quot; (para ramificação de condição); Propriedades de Jornada > Critérios de saída (para configuração de saída); Administração > Regras de negócios > Criar regra (para limites de frequência)

**Detalhes de configuração da chave:**

- Configure o evento de jornada selecionando o esquema de evento e definindo as condições de qualificação
- Para a Opção B, adicione o nó de espera imediatamente após a entrada do evento e antes de qualquer avaliação de condição
- Configure nós de condição usando atributos de perfil, dados de evento ou verificações de associação de público-alvo
- Vincule o nó de ação da mensagem à superfície de canal e ao conteúdo criado nas Fases 3 e 4
- Defina o tempo limite da jornada para uma duração apropriada (inferior a 91 dias para jornadas acionadas)
- Para a Opção C, crie regras de frequência por meio de Administração > Regras de negócios antes de publicar a jornada
- Atribua uma pontuação de prioridade à jornada se outras campanhas ou jornadas direcionarem públicos sobrepostos

**Onde as opções divergem:**

**Para Opção A (Acionado Por Evento Simples):**
A tela de jornada é mínima: entrada do evento > condição opcional de consentimento/elegibilidade > ação de mensagem > fim. Nenhuma etapa de espera ou verificação de conversão. Defina regras de reentrada com base no fato de o evento dever gerar uma mensagem sempre que ocorrer.

**Para a Opção B (Condicional com Espera):**
Adicione um nó de espera após a entrada do evento. Após a espera, adicione um nó de condição para verificar a conversão (por exemplo, verifique se o evento `commerce.purchases` ocorreu após a entrada da jornada) ou use os critérios de saída para remover automaticamente os perfis convertidos. Ramifique para a ação de mensagem no caminho &quot;não convertido&quot; e para um nó final no caminho &quot;convertido&quot;.

**Para a Opção C (Governança de Frequência):**
Configure limites de frequência no nível da organização por meio de Administração > Regras de negócios antes da publicação. Defina o controle de reentrada no nível da jornada nas propriedades da jornada. Como opção, atribua uma pontuação de prioridade por meio das propriedades do jornada para controlar qual comunicação vence quando as maiúsculas são atingidas. Isso pode ser aplicado sobre a Opção A ou a Opção B.

**Documentação do Experience League:**

- [Criar uma jornada](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Propriedades da jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Eventos gerais](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Atividade de condição](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Atividade aguardar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Adicionar uma mensagem em uma jornada](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Critérios de saída](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [Gerenciamento de entradas de jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Regras de frequência](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Pontuações de prioridade](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Identificar possíveis conflitos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)

### Fase 6: testar e implantar a jornada

**Função do Aplicativo:** AJO: Journey Orchestration

**O que você configurará:** Validação do modo de teste para verificar se a jornada se comporta conforme esperado com perfis de teste, seguida pela publicação da jornada para ativá-la.

Navegação da **UI:** tela de Jornada > alternância de modo de teste (para teste); tela de Jornada > Publicar (para implantação)

**Detalhes de configuração da chave:**

- Ative o modo de teste na tela de jornada para simular acionadores de eventos com perfis de teste
- Selecione perfis de teste que tenham informações de contato do canal válidas (endereço de email, número de telefone)
- Acione o evento de teste e verifique se o perfil de teste atravessa o caminho esperado
- Para a Opção B, verifique se a etapa de espera se comporta corretamente e se a avaliação da condição produz a ramificação esperada
- Verificar se os tokens de personalização são renderizados corretamente na mensagem de teste
- Após um teste bem-sucedido, publique a jornada para ativá-la
- Monitore o status da jornada e as métricas de entrada de perfil iniciais após a publicação

**Documentação do Experience League:**

- [Testar a jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [Publicar a jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

### Fase 7: monitorar e relatar o desempenho

**Função do Aplicativo:** AJO: Relatórios e Análise de Desempenho, S4: Monitoramento e Observabilidade, S5: Relatórios e Análise

**O que você configurará:** Relatórios de jornada ao vivo e históricos para monitoramento de entrega e envolvimento, alertas de plataforma para assimilação de eventos e falhas de processamento de jornadas e, opcionalmente, espaços de trabalho do CJA para uma análise mais profunda entre canais da eficácia do sistema de mensagens acionado.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: profundidade dos relatórios**
>
>Quanto de análise de relatórios é necessário para esse caso de uso?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Somente relatórios nativos do AJO | O monitoramento operacional das métricas de entrega é suficiente | Disponível imediatamente; capas enviadas, entregues, devolvidas, abertas, clicadas; nenhuma configuração adicional é necessária |
>| Integração nativa do AJO + CJA | Análise entre canais, atribuição de conversão e análise de tendências são necessárias | Requer conexão e visualização de dados do CJA vinculadas aos conjuntos de dados da AJO; fornece recursos analíticos mais profundos |

**Navegação da interface do usuário:** Jornada > Selecionar jornada > Relatório ao vivo (para monitoramento ao vivo); Jornada > Selecionar jornada > Relatório de todos os tempos (para análise histórica); Alertas > Regras de alerta > Assinar (para configuração de alerta)

**Detalhes de configuração da chave:**

- Acesse o relatório de jornada em tempo real durante a execução ativa para monitorar entradas de perfil, saídas e métricas de entrega
- Revise o relatório histórico depois que a jornada estiver ativa por tempo suficiente para acumular dados significativos
- Configurar alertas para falhas de execução do fluxo de origem (assimilação de eventos) e atrasos de processamento da jornada
- Para integração com o CJA, verifique se a conexão do CJA inclui conjuntos de dados de eventos de experiência do AJO (conjunto de dados de eventos de feedback de mensagem, conjunto de dados de eventos de experiência de rastreamento de email)

**Documentação do Experience League:**

- [Relatório em tempo real da jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Jornada relatório global](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Trabalhar com o Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Visão geral de alertas](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/alerts/overview)
- [Guia de integração do AJO + CJA](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## Considerações de implantação

Esta seção aborda medidas de proteção, armadilhas comuns, práticas recomendadas e decisões de compensação para implementações de mensagens acionadas por eventos.

### Medidas de proteção e limites

As medidas de proteção e os limites de plataforma a seguir se aplicam às implementações de mensagens acionadas por eventos.

- **Taxa de transferência de evento unitário:** Máximo de 5.000 eventos por segundo por sandbox para jornadas de eventos unitários — [Medidas de proteção da Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/get-started/guardrails)
- **Limite do Live jornada:** Máximo de 500 jornadas ativas por sandbox — [medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/get-started/guardrails)
- **Limite da tela de Jornada:** Máximo de 50 atividades por tela de jornada
- **Tempo limite da Jornada:** A duração máxima da jornada é de 91 dias (tempo limite global)
- **Reentrada do sistema de resfriamento:** Reentrada mínima de sistema de resfriamento é 5 minutos
- **Configurações de limite de frequência:** Máximo de 10 configurações de limite por sandbox
- **Superfícies de canal:** Máximo de 10 superfícies de canal por tipo de canal por sandbox
- **Assimilação de streaming:** Máximo de 20.000 registros por segundo por conexão HTTP — [Medidas de proteção de assimilação](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- **Atributos computados:** Máximo de 25 atributos computados por sandbox — [Medidas de proteção de atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview#guardrails)
- **Fragmentos de conteúdo:** Máximo de 30 fragmentos de conteúdo por mensagem
- **Atualização de relatório ao vivo:** Relatórios ao vivo são atualizados a cada 60 segundos e mostram as últimas 24 horas de dados
- **Latência histórica do relatório:** Relatórios históricos (todos os tempos) podem levar até 2 horas para serem totalmente preenchidos após o término da execução

### Armadilhas comuns

Esteja ciente dos seguintes problemas comuns ao implementar mensagens acionadas por eventos.

- **Eventos anônimos sem resolução de identidade:** Os eventos de acionamento que carregam apenas uma ECID (ID de cookie anônimo) não podem ser resolvidos em um perfil contatável para entrega de mensagens. Certifique-se de que o evento de acionamento inclua uma identidade autenticada ou que o gráfico de identidade vincule a ECID a um contato conhecido. Sem a resolução de identidade, os perfis entram na jornada, mas falham na etapa de delivery da mensagem.

- **Evento de conversão ausente para verificações de condição da Opção B:** Se o evento de conversão (por exemplo, compra) não for assimilado na AEP ou não estiver associado à mesma identidade de perfil que o evento de acionamento, a verificação de condição avaliará incorretamente como &quot;não convertido&quot; e enviará mensagens desnecessárias. Verifique se os eventos de conversão fluem para o AEP em tempo real e compartilhe uma identidade com o evento de acionamento.

- **Regras de reentrada excessivamente permissivas:** permitir a reentrada sem um período de controle em fontes de eventos de alta frequência pode fazer com que o mesmo perfil receba várias mensagens em minutos. Sempre defina um controle de reentrada que corresponda ao contexto comercial (por exemplo, controle de 4 horas para abandono do carrinho, controle de 24 horas para abandono do navegador).

- **Desalinhamento de fuso horário da etapa de espera:** processo de etapas de espera em UTC por padrão. Se a jornada for direcionada a perfis em vários fusos horários e a espera tiver que se alinhar à hora local do recipient, defina as configurações de fuso horário na jornada de maneira apropriada.

- **Limites de frequência em conflito com outras campanhas:** os limites de frequência no nível da organização se aplicam a todas as campanhas e jornadas. Uma nova jornada acionada pode ser suprimida se os perfis já tiverem atingido seu limite de outras campanhas ativas. Monitore a taxa de supressão e ajuste as pontuações de prioridade para garantir que mensagens acionadas importantes sejam priorizadas.

- **Falha na publicação do Jornada devido a dependências ausentes:** Todas as ramificações na tela de jornada devem terminar com uma atividade final. Todos os nós de ação devem fazer referência a superfícies de canal válidas com conteúdo de mensagem ativo. Verifique todas as dependências antes de publicar.

### Práticas recomendadas

Siga estas recomendações para implementações de mensagens acionadas por eventos bem-sucedidas.

- **Comece simples e depois repita:** Comece com a Opção A para novos casos de uso de mensagens disparadas. Adicione a lógica de espera e condição (Opção B) somente após validar o pipeline de evento e o delivery de mensagem. Adicione a governança de frequência (Opção C) quando várias jornadas acionadas estiverem ativas.

- **Use os critérios de saída em vez dos nós de condição para verificações de conversão:** Os critérios de saída removem automaticamente os perfis da jornada quando ocorre um evento qualificado (por exemplo, compra), eliminando a necessidade de um nó de condição explícito após a etapa de espera. Isso produz uma tela de jornada mais limpa e uma detecção de conversão mais responsiva.

- **Testar com dados de evento reais em uma sandbox de desenvolvimento:** Use o modo de teste com cargas de evento reais (não apenas perfis de teste) para validar se os campos de esquema de evento, tokens de personalização e expressões de condição funcionam corretamente com dados semelhantes a produção.

- **Definir detalhamentos de reentrada específicos do evento:** Corresponda o período de detalhamento ao contexto comercial do evento de disparo. As jornadas de abandono do carrinho normalmente usam um resfriamento de 4 a 24 horas; as jornadas de confirmação podem permitir a reentrada imediata; as jornadas de integração devem impedir totalmente a reentrada.

- **Monitore a taxa de supressão como uma métrica de integridade:** Se a taxa de supressão (perfis qualificados, mas que não recebem mensagens devido a limites de frequência ou condições) exceder 30-40%, verifique se os limites são muito restritivos ou se o evento de disparo é definido de forma muito ampla.

- **jornadas de versão em vez de editar as online:** Uma jornada online não pode ser editada diretamente. Crie uma nova versão duplicando a jornada, fazendo alterações, interrompendo a versão antiga e publicando a nova. Isso evita interromper os perfis que estão atualmente na jornada.

- **Incluir um caminho padrão/de fallback nos nós de condição:** Sempre configure um caminho padrão (else) nos nós de condição para lidar com estados de perfil inesperados. Os perfis que não correspondem a nenhuma ramificação de condição devem sair normalmente em vez de permanecerem presos.

### Decisões de compensação

Considere as seguintes compensações ao projetar a implementação de mensagens acionadas por eventos.

>[!NOTE]
>
>**Contrapartida: velocidade da mensagem vs. relevância da mensagem**
>
>A entrega imediata de mensagens (opção A) maximiza a velocidade, mas pode enviar mensagens para clientes que teriam se autoconvertido. A entrega condicional atrasada (Opção B) melhora a relevância ao filtrar autoconversores, mas introduz latência que pode reduzir a urgência.
>
>- **A opção A favorece:** Velocidade, simplicidade, casos de uso de estilo de confirmação em que cada evento justifica uma mensagem
>- **A opção B favorece:** Relevância, fadiga reduzida da mensagem, casos de uso de estilo de abandono em que a autoconversão é comum
>- **Recomendação:** Use a Opção A para mensagens transacionais e de confirmação nas quais a velocidade é o valor principal. Use a opção B para mensagens de recuperação e reengajamento quando a relevância ultrapassar a velocidade. Faça experimentos com durações de espera para encontrar o equilíbrio ideal para cada caso de uso.

>[!NOTE]
>
>**Contrapartida: proteção de frequência vs. cobertura de mensagem**
>
>Limites de frequência estritos (Opção C) impedem a fadiga, mas podem suprimir mensagens acionadas importantes quando os perfis estão próximos ao limite. Os limites permitidos ou nulos maximizam a cobertura, mas arriscam mensagens excessivas e fadiga do canal.
>
>- **Limites rígidos favorecidos:** experiência do cliente, reputação da marca, capacidade de entrega (menos reclamações de spam)
>- **Limites de permissão favorecidos:** Cobertura de mensagem, oportunidades de conversão, evitando disparadores perdidos
>- **Recomendação:** comece com limites padrão do setor (3-5 emails/semana, 1-2 SMS/semana, 2-3 push/dia) e ajuste com base nas métricas de envolvimento e taxas de cancelamento de inscrição. Atribua pontuações de prioridade mais altas às mensagens acionadas para que elas conquistem campanhas em lote quando as limitações forem atingidas.

>[!NOTE]
>
>**Contrapartida: simplicidade de Jornada vs. sofisticação de jornada**
>
>Jornadas simples (poucos nós, sem ramificação) são mais fáceis de criar, testar e manter, mas oferecem adaptação contextual limitada. Jornadas sofisticadas (várias condições, caminhos de ramificação, verificações de segmentos) permitem respostas mais suaves, mas aumentam a complexidade e o risco de erros.
>
>- **Favoritos a jornadas simples:** Implementação mais rápida, depuração mais fácil, menor carga de manutenção
>- **Favoritos de jornadas sofisticadas:** Direcionamento mais preciso, melhor personalização, envios desnecessários reduzidos
>- **Recomendação:** comece com a jornada mais simples que atenda aos requisitos comerciais. Aumente a complexidade de forma incremental com base nos dados de desempenho. Uma jornada simples que funciona de forma confiável é mais valiosa do que uma jornada complexa com erros não detectados.

## Documentação relacionada

Os recursos a seguir fornecem detalhes adicionais sobre os recursos usados nesta implementação.

### Jornada orquestração

- [Introdução ao jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Criar uma jornada](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Propriedades da jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Eventos gerais](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Eventos de qualificação de público-alvo](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [Atividade de condição](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Atividade aguardar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Adicionar uma mensagem em uma jornada](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Critérios de saída](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [Gerenciamento de entradas de jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Testar a jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [Publicar a jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

### Configuração de canais

- [Introdução à configuração de email](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegar subdomínios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Criar pools de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [Planos de aquecimento de IP](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Configurações de superfície de email](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Configurar canal de SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Configurar canal de notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [Gerenciar lista de supressão](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Criação e personalização de mensagens

- [Criar um email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [Criar conteúdo de email](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxe do Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Funções auxiliares](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabalhar com modelos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabalhar com fragmentos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Visualizar e testar o conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [Criar uma mensagem SMS](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/create-sms)
- [Criar uma notificação por push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/design-push)

### Frequência e regras de negócio

- [Regras de frequência](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Visão geral das regras de negócios](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [API de limite](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/channel-surfaces/capping)

### Gerenciamento de conflitos e prioridades

- [Introdução ao gerenciamento de conflitos e prioridades](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Identificar possíveis conflitos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [Pontuações de prioridade](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Limite de jornada e arbitragem](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)

### Relatórios e desempenho

- [Relatório em tempo real da jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Jornada relatório global](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Guia de integração do AJO + CJA](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

### Coleta e assimilação de dados

- [Visão geral do Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/web-sdk/home)
- [Visão geral do Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Visão geral da API do Edge Network Server](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [Configurar sequências de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Visão geral da assimilação de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/streaming/overview)

### Modelagem de dados e esquemas

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/home)
- [Noções básicas de composição de esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)

### Identidade e perfil

- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Visão geral dos namespaces de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/namespaces)
- [Regras de vinculação do gráfico de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [Visão geral do perfil](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### Segmentação e públicos

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentação de transmissão](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/methods/streaming-segmentation)

### Governança e consentimento de dados

- [Visão geral da governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/home)
- [Visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview)
- [Grupo de campos Consentimento e preferências](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
- [Consentimento no Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### Atributos computados

- [Visão geral de atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Guia da interface de atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)

### Monitorização e observabilidade

- [Visão geral de alertas](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/alerts/overview)
- [Visão geral dos Insights de observação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/home)

### Medidas de proteção

- [Medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/get-started/guardrails)
- [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Medidas de proteção de assimilação](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)

### Tutoriais e guias

- [Criar um tutorial do jornada](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Instalar o Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
