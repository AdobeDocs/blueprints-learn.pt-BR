---
title: Visitante anônimo - Web Personalization
description: Saiba como fornecer conteúdo personalizado da Web para visitantes não identificados com base em sinais comportamentais na sessão.
solution: Journey Optimizer, Real-Time Customer Data Platform
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '8076'
ht-degree: 1%

---


# Personalização anônima da Web para visitantes

Este plano de referência fornece orientação de implementação para fornecer conteúdo personalizado da Web para visitantes anônimos (não identificados) com base em sinais comportamentais na sessão. Ele abrange o ciclo de vida completo da implementação — desde a configuração do [!DNL Web SDK] e a definição do público-alvo da borda até a entrega de conteúdo e a geração de relatórios de desempenho — e foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que trabalham com o [!DNL Adobe Journey Optimizer] (AJO), o [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP) e o [!DNL Adobe Experience Platform] (AEP).

Use este plano para entender a arquitetura, avaliar as opções de implementação, tomar decisões de configuração bem fundamentadas e localizar a documentação relevante do Experience League para cada fase da implementação.

O padrão opera com dados limitados — somente o que pode ser observado na sessão atual e qualquer perfil de borda anônimo acumulado de visitas anteriores com o mesmo dispositivo ou cookie. Isso o torna adequado para personalização de topo da funnel, em que o visitante não tem conta ou não foi autenticado.

## Visão geral do caso de uso

O Anonymous Visitor Web Personalization atende à necessidade comercial de fornecer conteúdo relevante e personalizado a visitantes do site que ainda não foram identificados — eles não estão conectados, não têm identidade conhecida e não podem ser resolvidos para um perfil de cliente unificado. Apesar dessa limitação, é possível realizar uma personalização significativa usando sinais comportamentais na sessão: páginas visualizadas, tempo no site, profundidade de rolagem, fonte de referência, localização geográfica, tipo de dispositivo e parâmetros de campanha UTM.

Esse padrão usa as superfícies do canal da Web do AJO e as experiências baseadas em código para modificar o conteúdo da página em tempo real. A segmentação do Edge é o principal método de avaliação, pois as decisões devem ser tomadas com latência de subsegundos enquanto o visitante navega no site. O [!DNL Web SDK] coleta sinais comportamentais e os envia para o [!DNL AEP Edge Network], onde as regras de público-alvo avaliadas por borda determinam qual variante de conteúdo fornecer.

Ao contrário da personalização da Web/aplicativo de visitante conhecido, que aproveita o perfil totalmente unificado e a associação de segmento, esse padrão é restrito aos dados observáveis na sessão atual e a qualquer perfil de borda anônimo associado à ECID do visitante ([!DNL Experience Cloud ID]). Essa distinção é crítica para o planejamento de implementação: os sinais comportamentais disponíveis para personalização são limitados ao que o [!DNL Web SDK] captura e ao que persiste no armazenamento de perfil de borda nas sessões por meio da ECID baseada em cookies.

## Principais objetivos de negócios

Os seguintes objetivos de negócios são compatíveis com esse padrão de caso de uso.

**[Aumentar o engajamento no site](../../business-objectives/acquisition-growth/increase-website-engagement.md)**

Melhore o tempo no site, as páginas por sessão e a interação com o conteúdo da Web por meio de experiências relevantes personalizadas para sinais de visitante anônimo.

| KPIs |
| --- |
| Tempo na página (Web) |
| Engajamento |
| Taxas de conversão |

**[Fornecer experiências personalizadas ao cliente](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**

Personalize o conteúdo, as ofertas e as mensagens de acordo com as preferências individuais, os comportamentos e os estágios do ciclo de vida, mesmo para visitantes que ainda não se identificaram.

| KPIs |
| --- |
| Engajamento |
| Taxas de conversão |
| Satisfação do cliente (CSAT) |

**[Aumentar taxas de conversão](../../business-objectives/revenue-monetization/increase-conversion-rates.md)**

Melhore a porcentagem de visitantes e prospetos que concluem as ações desejadas, como compras, inscrições ou envios de formulários, apresentando o conteúdo mais relevante com base no contexto comportamental.

| KPIs |
| --- |
| Taxas de conversão |
| Conversão de leads |
| Custo por lead |

## Exemplo de casos de uso tático

Os exemplos a seguir ilustram cenários específicos em que esse padrão pode ser aplicado.

- **Teste A/B de título de página de aterrissagem com base na fonte de referência** — teste títulos diferentes para visitantes que chegam da Google, de redes sociais ou do tráfego direto para otimizar o envolvimento pelo canal de aquisição
- **Recomendações de afinidade de categorias com base no comportamento de navegação** — Exibe recomendações de produto ou conteúdo com base nas páginas exibidas na sessão atual para aumentar a descoberta e a conversão
- **Oferta de intenção de saída para visitantes prestes a sair** — apresente uma oferta promocional ou um formulário de captura de cliente potencial quando sinais comportamentais indicarem que o visitante está prestes a abandonar o site
- **Banner promocional direcionado geograficamente** — Mostra promoções específicas de localização, conteúdo do localizador de lojas ou ofertas regionais com base na localização geográfica do visitante
- **Otimização do layout de conteúdo específico do dispositivo** — Adapte o layout de conteúdo, os tamanhos de imagem e a disposição do CTA com base no fato de o visitante estar em desktop, tablet ou dispositivo móvel
- **Mensagens de boas-vindas de visitante novo vs. recorrente** — Diferencie a experiência para visitantes novos versus visitantes anônimos recorrentes usando a persistência ECID em todas as sessões
- **Recomendações de conteúdo com base nas páginas visualizadas na sessão atual** — exiba dinamicamente artigos, produtos ou recursos relacionados com as páginas que o visitante já visualizou
- **Banner principal dinâmico com base nos parâmetros de campanha UTM** — Personalize o banner principal para corresponder às mensagens ou aos recursos criativos da campanha de referência

## Indicadores-chave de desempenho

Use os KPIs a seguir para medir a eficácia desse padrão de caso de uso.

| KPI | Descrição | Abordagem de medição |
| --- | --- | --- |
| Taxa de impressão do Personalization | Porcentagem de exibições de página qualificadas em que o conteúdo personalizado foi entregue | Relatório de campanha do AJO: impressões / total de exibições de página |
| Índice de click-through (CTR) | Porcentagem de impressões de conteúdo personalizadas que resultam em um clique | Relatório de campanha do AJO: cliques/impressões |
| Aumento de engajamento | Aumento no tempo na página, páginas por sessão ou profundidade de rolagem para conteúdo personalizado vs. padrão | Comparação do espaço de trabalho do CJA: coorte personalizada vs. controle |
| Índice de conversão | Porcentagem de visitantes expostos ao conteúdo personalizado que concluíram a ação desejada | Análise do CJA funnel: impressão > interação > conversão |
| Redução da taxa de rejeição | Redução nas sessões de página única para visitantes que recebem conteúdo personalizado | Análise de sessão do CJA: delta da taxa de rejeição para personalizado versus padrão |
| Taxa de Ganhos do Experimento | Porcentagem de testes A/B que produzem um vencedor estatisticamente significativo | Relatório de experimento do AJO: experimentos que atingem o limite de confiança |

## Padrão do caso de uso

A seguir estão descritos o padrão principal e a cadeia de função para esse caso de uso.

**Web Personalization de Visitante Anônimo**

Forneça conteúdo personalizado com base em sinais comportamentais na sessão para visitantes não identificados por meio do canal da Web do AJO.

**Cadeia de funções:** Configuração de Superfície da Web > Avaliação de Regra Comportamental > Entrega de Conteúdo > Rastreamento de Impressão > Relatórios

## Aplicativos

Os aplicativos a seguir são usados neste padrão de caso de uso.

- **[!DNL Adobe Journey Optimizer](AJO)** — Configuração da superfície de canal da Web, criação de conteúdo (experiências da Web e baseadas em código), execução de campanha, experimentação de conteúdo (teste A/B), decisão (seleção de conteúdo dinâmico) e relatórios
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)** — Segmentação Edge para avaliação de público-alvo em tempo real com base em sinais comportamentais na sessão; gerenciamento de perfil de borda anônimo
- **[!DNL Adobe Experience Platform](AEP)** — [!DNL Web SDK] para coleta de sinal comportamental, [!DNL Edge Network] para entrega de roteamento e personalização de dados em tempo real e configuração de sequência de dados

## Funções básicas

Os seguintes recursos básicos devem estar em vigor para esse padrão de caso de uso. Para cada função, o status indica se ele é tipicamente necessário, se presume ser pré-configurado ou se não é aplicável.

| Função de base | Status | O que deve estar em vigor | Referência do Experience League |
| --- | --- | --- | --- |
| Administração e governança | Presumido em vigor | sandbox da AJO com permissões de canal da Web configuradas. [!DNL Web SDK] permissões de implementação e acesso à sequência de dados concedidos à equipe de implementação. Usuários provisionados com funções que permitem a configuração de canais da Web, o gerenciamento de público-alvo e a execução de campanhas. | [Visão geral do controle de acesso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Preparação e modelagem de dados | Obrigatório | Esquema de evento de experiência que captura sinais comportamentais da Web (exibições de página, cliques, profundidade de rolagem, dados de referência, parâmetros UTM). O esquema deve incluir grupos de campos de interação na web padrão e ser ativado para que o perfil de borda seja compatível com a avaliação em tempo real. Um conjunto de dados correspondente deve ser criado e ativado para perfil. | [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home) |
| Fontes de dados e coleção | Obrigatório | [!DNL Web SDK] deve ser implementado em todas as propriedades da Web de destino com uma sequência de dados configurada para rotear dados para [!DNL AEP Edge Network]. A sequência de dados deve ter os serviços [!DNL Adobe Experience Platform] e [!DNL Adobe Journey Optimizer] habilitados. Esta é uma dependência crítica — sem [!DNL Web SDK], nenhuma coleta de sinal comportamental ou entrega de experiência é possível. | [Visão geral do SDK da Web](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) |
| Configuração de identidade e perfil | Obrigatório | ECID ([!DNL Experience Cloud ID]) configurada como o namespace de identidade principal para visitantes anônimos. A política de mesclagem do Edge deve ser configurada com `isActiveOnEdge: true` para resolver dados de perfil anônimos na borda. Somente uma política de mesclagem pode estar ativa na borda por sandbox. | [Visão geral do Serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home) |
| Definição e segmentação do público-alvo | Obrigatório | Segmentos de público avaliados pela Edge definidos com base em sinais comportamentais na sessão. A segmentação do Edge é obrigatória para a latência de avaliação em subsegundos. As regras de segmento devem usar somente expressões de regra de segmento qualificadas para borda (verificações de atributo simples e associação de segmento — sem consultas de série de tempo ou agregações complexas). | [Segmentação do Edge](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation) |

## Funções de suporte

Os recursos a seguir aumentam esse padrão de caso de uso, mas não são necessários para a execução principal.

| Função de suporte | Status | Por que é importante | Referência do Experience League |
| --- | --- | --- | --- |
| Criação de atributo calculado/derivado | Não se aplica | Valor limitado para visitantes anônimos, pois há poucos dados históricos de perfil a serem agregados. Pode se tornar aplicável se o perfil de borda acumular dados comportamentais significativos de visitas anônimas anteriores em várias sessões. | [Visão geral dos atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Gerenciamento do ciclo de vida dos dados | Recomendado | A expiração de perfil pseudônimo deve ser configurada para perfis de borda anônimos para gerenciar o armazenamento e atender aos requisitos de privacidade. Perfis somente ECID podem ser definidos para expirar entre 14 e 365 dias. As políticas de consentimento de cookies devem ser aplicadas para a coleta de dados comportamentais. | [Visão geral do Gerenciamento Avançado do Ciclo de Vida dos Dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| Rotulagem e aplicação de uso de dados | Recomendado | Os rótulos de governança em dados comportamentais garantem a conformidade, especialmente para geolocalização (rótulo geográfico sensível ao S2) e personalização baseada em dispositivos. Os rótulos impedem que dados comportamentais restritos sejam usados em contextos de personalização não autorizados. | [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| Monitoramento e capacidade de observação | Recomendado | O monitoramento do fluxo de dados de [!DNL Edge Network] e [!DNL Web SDK] ajuda a detectar problemas de entrega de personalização. Configure alertas para falhas de fluxo de dados, erros de assimilação e anomalias de entrega de borda. Crítico para implantações de produção em que as falhas de personalização prejudicam a experiência do visitante. | [Visão geral dos Insights de Capacidade de Observação](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| Relatórios e análise | Incluído | Os relatórios de desempenho do Personalization fazem parte da cadeia de funções (Fase 5). A análise da CJA da eficácia da personalização de visitantes anônimos permite uma análise detalhada do funnel, comparação de coorte e medição de impacto de conversão além do que os relatórios nativos do AJO fornecem. | [visão geral do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## Funções do aplicativo

Este plano exerce as seguintes funções do Catálogo de Funções da Aplicação. As funções são mapeadas para fases de implementação em vez de etapas numeradas.

### [!DNL Journey Optimizer] (AJO)

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Configuração de canais | Fase 1: Configuração da superfície da Web | Configurar superfícies de canal da Web definindo onde o conteúdo personalizado será entregue nas propriedades da Web de destino |
| Criação de mensagens | Fase 3: Criação de conteúdo e criação de variantes | Crie variantes de conteúdo personalizadas para superfícies da Web usando o designer da Web, o editor de experiência baseado em código ou modelos de conteúdo |
| Execução de campanha | Fase 4: Configuração de campanha e entrega | Criar e ativar campanhas da Web que vinculam públicos, conteúdo e configuração de entrega |
| Decisão. | Fase 3: Criação de conteúdo e criação de variantes (Opção C) | Configurar políticas de decisão, regras de qualificação e estratégias de classificação para a seleção de conteúdo dinâmico com base em sinais comportamentais |
| Experimentação de conteúdo | Fase 3: Criação de conteúdo e criação de variantes (Opção B) | Configure experimentos de conteúdo A/B e multivariado com alocação de tráfego, métricas de sucesso e limites de confiança |
| Relatórios e análise de desempenho | Fase 5: Relatórios e análise de desempenho | Monitorar métricas de entrega de personalização, eficácia das variantes, resultados de experimentos e impacto da conversão |

### [!DNL Real-Time CDP] (RT-CDP)

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Avaliação de público | Fase 2: Definição de público-alvo comportamental | Definir e avaliar segmentos de público-alvo baseados em borda usando sinais comportamentais na sessão para direcionamento de personalização em tempo real |

## Pré-requisitos

Conclua o seguinte antes de iniciar a implementação.

- [ ] [!DNL Web SDK] é implementado em todas as propriedades da Web de destino com `sendEvent` chamadas que capturam exibições de página, cliques e interações comportamentais relevantes
- [ A sequência de dados ] está configurada na interface da Coleção de dados com os serviços [!DNL Adobe Experience Platform] e [!DNL Adobe Journey Optimizer] habilitados
- [ O esquema Evento de Experiência ] existe com grupos de campos de interação da web (exibições de página, dados de referência, parâmetros UTM, contexto do dispositivo) e está habilitado para o Perfil
- [ ] O namespace de identidade da ECID está configurado e designado como identidade primária no esquema de evento comportamental da Web
- [ A política de mesclagem do Edge ] está configurada com `isActiveOnEdge: true` na sandbox de destino
- [ O canal da Web do AJO ] foi provisionado e está acessível na sandbox de destino
- [ ] As variantes de conteúdo (cópia, imagens, CTAs) foram projetadas e aprovadas para cada caso de uso de personalização
- [ ] Métricas de sucesso são definidas (o que constitui um evento de conversão ou envolvimento para medição)
- [ ] O mecanismo de consentimento de cookies é implementado no site para cumprir as regras de privacidade antes de coletar dados comportamentais

## Opções de implementação

Esta seção descreve três abordagens de implementação. Selecione a opção que melhor se adapta aos seus requisitos de personalização.

### Opção A: personalização da Web com base em regras

**Recomendado para:** Personalização determinística simples: banners direcionados geograficamente, títulos específicos de origem de referência, layouts específicos de dispositivos, mensagens novas vs. de visitantes recorrentes. Escolha esta opção quando a variante de conteúdo puder ser determinada por uma lógica condicional simples (se a condição X, mostrar conteúdo Y).

**Como funciona:**

A personalização baseada em regras usa segmentos de público-alvo avaliados por borda para determinar qual variante de conteúdo um visitante vê. Cada segmento de público mapeia para uma variante de conteúdo específica por meio de regras condicionais definidas na campanha. Quando um visitante carrega uma página, o [!DNL Web SDK] envia sinais comportamentais para o [!DNL Edge Network], que avalia o perfil de borda do visitante em relação às regras de público-alvo definidas em milissegundos. A variante de conteúdo correspondente é retornada na resposta [!DNL Edge Network] e renderizada na página.

Essa abordagem requer a definição de segmentos de público-alvo distintos na RT-CDP (por exemplo, &quot;visitantes da pesquisa do Google&quot;, &quot;visitantes na Califórnia&quot;, &quot;visitantes de dispositivos móveis&quot;) e a criação de variantes de conteúdo correspondentes no AJO. A campanha vincula cada público-alvo à sua variante de conteúdo usando regras de conteúdo condicionais ou campanhas separadas por segmento. Não há classificação de IA ou divisão de tráfego envolvida — a relação entre público e conteúdo é determinística.

**Principais considerações:**

- Requer critérios de público-alvo bem definidos que podem ser expressos como expressões de regra de segmento qualificadas para borda
- As variantes de conteúdo devem ser pré-criadas para cada segmento de público-alvo
- A adição de novas regras de personalização requer a criação de novos segmentos de público-alvo e variantes de conteúdo
- Não fornece medição estatística da eficácia das variantes de conteúdo

**Vantagens:**

- Simples de implementar e entender — relação clara de causa e efeito entre público e conteúdo
- Não é necessária nenhuma sobrecarga de experimentação ou divisão de tráfego
- O comportamento determinístico torna os testes e o controle de qualidade simples
- Baixa latência, pois a avaliação de borda é puramente baseada em regras
- Funciona bem quando a empresa já sabe qual conteúdo tem o melhor desempenho para cada segmento

**Limitações:**

- Nenhum mecanismo integrado para medir se a personalização melhora os resultados em relação ao conteúdo padrão
- Requer tomada de decisão manual sobre qual conteúdo mostrar para cada segmento
- Não se adapta ou otimiza ao longo do tempo — regras estáticas até serem alteradas manualmente
- O dimensionamento para muitos segmentos e variantes aumenta a complexidade da configuração

**Experience League:**

- [Introdução ao canal da Web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [Segmentação de borda](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### Opção B: personalização da Web com base em experimentação

**Recomendado para:** testes A/B e multivariados — teste de variantes de títulos, cores de botões do CTA, alternativas de layout, ofertas promocionais — com medição de significância estatística. Escolha essa opção quando precisar validar qual variante de conteúdo tem melhor desempenho antes de confirmar uma regra de personalização permanente.

**Como funciona:**

A personalização baseada em experimentação usa a Experimentação de conteúdo do AJO para alocar visitantes aleatoriamente em grupos de tratamento de conteúdo e medir qual variante tem melhor desempenho em relação a uma métrica de sucesso definida. O tráfego é dividido em variantes (por exemplo, 50/50 para A/B, 33/33/34 para A/B/C) e o desempenho é rastreado até que a significância estatística seja alcançada.

O experimento é incorporado a uma campanha da Web do AJO. Quando um visitante carrega uma página, o [!DNL Edge Network] os atribui a um grupo de tratamento com base na alocação de tráfego configurada. O visitante vê consistentemente o mesmo tratamento durante o experimento (persistência no nível da sessão ou no nível do visitante, dependendo da configuração). As métricas de sucesso (cliques, conversões, eventos de envolvimento) são rastreadas via [!DNL Web SDK] e relatadas no relatório de experimento do AJO.

Essa opção não requer segmentos de público-alvo predefinidos para direcionamento — todos os visitantes (ou um subconjunto direcionado) participam do experimento. O objetivo é descobrir qual conteúdo tem melhor desempenho, não direcionar segmentos conhecidos com conteúdo predeterminado.

**Principais considerações:**

- Requer um volume de tráfego suficiente para atingir significância estatística num prazo razoável
- Experimentos usam um modelo estatístico bayesiano com intervalos de confiança válidos a qualquer momento
- Um grupo de controle (não recebe nenhum conteúdo personalizado) é recomendado para medir o aumento incremental
- Somente um experimento pode estar ativo por campanha de cada vez
- Modificações no experimento exigem que a campanha seja interrompida e reiniciada

**Vantagens:**

- Fornece mensuração estatisticamente rigorosa da eficácia das variantes de conteúdo
- Remove a adivinhação das decisões de personalização — seleção de conteúdo orientada por dados
- Oferece suporte a grupos de controle para medição de aumento incremental real
- Relatórios de experimento incorporados com intervalos de confiança e declaração de vencedor
- Os resultados podem informar a personalização futura baseada em regras (Opção A) identificando variantes vencedoras

**Limitações:**

- Requer volume de tráfego significativo — páginas de tráfego baixo podem levar semanas para atingir significado
- A divisão de tráfego significa que alguns visitantes veem conteúdo abaixo do ideal durante o período de teste
- Não é possível personalizar por segmento durante o experimento (todos os visitantes ou um subconjunto participam igualmente)
- Máximo de 10 variantes de tratamento por experimento
- Sem otimização contínua — os experimentos são discretos com início e fim

**Experience League:**

- [Introdução ao experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Criar um experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Relatório de experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)

### Opção C: Personalização da Web com base em decisão

**Recomendado para:** Seleção de conteúdo dinâmico — recomendações de afinidade de categoria, ofertas de intenção de saída, recomendações comportamentais — em que uma política de decisão avalia os sinais da sessão e seleciona o conteúdo ideal de um catálogo de itens qualificados. Escolha essa opção quando a lógica de seleção de conteúdo for muito complexa para regras simples, quando você desejar otimização classificada por IA ou quando o conjunto de itens de conteúdo elegíveis for grande e dinâmico.

**Como funciona:**

A personalização baseada em decisão usa o AJO Decisioning para avaliar sinais comportamentais e selecionar a melhor variante de conteúdo para cada visitante de um catálogo gerenciado de itens de conteúdo (ofertas). Cada item de conteúdo tem regras de elegibilidade (quem se qualifica), representações (como o conteúdo se parece em cada posicionamento) e restrições de limite opcionais (com que frequência pode ser exibido). Uma política de decisão vincula disposições (onde o conteúdo aparece na página) a coleções de itens de conteúdo e aplica uma estratégia de classificação para selecionar a melhor opção.

Quando um visitante carrega uma página, o [!DNL Web SDK] envia uma solicitação [!DNL Edge Network] que inclui o escopo da decisão. O mecanismo de decisão avalia o perfil de borda do visitante em relação às regras de elegibilidade do item de conteúdo, aplica a estratégia de classificação (com base em prioridade, com base em fórmula ou com classificação de IA) e retorna o item de conteúdo vencedor. Isso acontece na borda com latência de subsegundos.

A estratégia de classificação determina como os itens de conteúdo elegíveis são ordenados. A classificação baseada em prioridade usa valores de prioridade atribuídos manualmente. A classificação baseada em fórmulas usa uma expressão personalizada (por exemplo, recenticidade de ponderação de exibições de página). A classificação classificada por IA usa um modelo de aprendizado de máquina que otimiza para a métrica de sucesso selecionada ao longo do tempo, mas requer no mínimo 1.000 eventos de conversão para treinamento.

**Principais considerações:**

- Requer a configuração dos componentes do Decisioning: disposições, regras de elegibilidade, itens de conteúdo, itens de fallback, coleções e políticas de decisão
- As estratégias classificadas por IA exigem volume de conversão suficiente (mais de 1.000 eventos) para treinar o modelo
- As decisões do Edge são limitadas aos atributos de perfil disponíveis na loja de perfis de borda
- Os itens de conteúdo devem ser gerenciados e mantidos na biblioteca de decisões
- O conteúdo de fallback deve ser definido para os casos em que nenhum item personalizado é qualificado

**Vantagens:**

- Pode ser dimensionado para grandes catálogos de conteúdo sem exigir mapeamento individual de público para conteúdo
- As estratégias classificadas em IA otimizam continuamente a seleção de conteúdo com base no desempenho observado
- Regras de elegibilidade e restrições de limite fornecem controle refinado sobre a entrega de conteúdo
- Suporta lógica de negócios complexa que seria difícil de expressar como segmentos de público-alvo
- Reutilizável em canais — a mesma política de decisão pode potencializar a personalização da Web, de e-mails e de dispositivos móveis

**Limitações:**

- Maior complexidade de implementação — requer a configuração da pilha completa de componentes do Decisioning
- A classificação de IA requer um volume de conversão e um tempo de treinamento significativos
- As limitações de dados de perfil do Edge restringem a complexidade da regra de elegibilidade para visitantes anônimos
- Despesas gerais de gerenciamento de itens de conteúdo — cada item precisa de representações, regras de elegibilidade e manutenção
- A lógica de decisão de depuração é mais complexa do que as abordagens baseadas em regras

**Experience League:**

- [Visão geral da Gestão de decisões](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Criar inserções](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Crie ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Criar decisões](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)

### Comparação de opções

A tabela a seguir compara as três opções de implementação entre os principais critérios.

| Critérios | Opção A: com base em regras | Opção B: experimentação | Opção C: Decisão |
| --- | --- | --- | --- |
| Melhor para | Mapeamentos conhecidos de segmento para conteúdo | Descobrir qual conteúdo funciona melhor | Seleção de conteúdo dinâmico de catálogos grandes |
| Complexo | Baixa | Médio | Alta |
| Latência | Subsegundo (borda) | Subsegundo (borda) | Subsegundo (borda) |
| Personalization precision | Nível de segmento (regras de público-alvo) | Nível do visitante (atribuição aleatória) | Nível do visitante (qualificação + classificação) |
| Otimização de conteúdo | Manual (sem medição) | Teste estatístico (A/B) | Contínuo (classificado por IA) ou manual (prioridade) |
| Exige segmentos de público | Sim (avaliada por borda) | Não (divisão de tráfego) | Opcional (para regras de elegibilidade) |
| Recurso de medição | Nenhum incorporado (requer CJA) | Relatórios de experimento incorporados | Relatórios de decisão incorporados |
| Tamanho do catálogo de conteúdo | Pequeno (1:1 segmento por conteúdo) | Pequeno (2-10 variantes) | Grande (itens elegíveis ilimitados) |
| Exige | Públicos-alvo da Edge, variantes de conteúdo | Campanha com experimento ativado | Componentes de decisão (disposições, ofertas, políticas) |

### Escolha a opção certa

Use a seguinte lógica de decisão para selecionar a opção de implementação apropriada:

1. **Você já sabe qual conteúdo deve ser exibido para cada segmento de visitante?**
   - Sim: Comece com **Opção A (Baseada em Regras)**. Você estabeleceu estratégias de conteúdo por segmento e precisa de uma entrega determinística.
   - Não: siga para a pergunta 2.

2. **Você precisa testar um pequeno número de variantes de conteúdo para encontrar o melhor desempenho?**
   - Sim: Escolha **Opção B (Experimentação)**. Você deseja a validação estatística antes de confirmar uma estratégia de conteúdo.
   - Não: siga para a pergunta 3.

3. **Você tem um grande catálogo de itens de conteúdo com qualificação complexa e requisitos de classificação?**
   - Sim: Escolha **Opção C (Decisão)**. Você precisa de uma seleção de conteúdo dinâmico que seja dimensionável além de regras simples.
   - Não: comece com a **Opção A (com base em regras)** para simplificar, depois evolua para a Opção B ou C conforme as necessidades aumentam.

**Combinando opções:** Estas opções não são mutuamente exclusivas. Uma progressão comum é começar com a opção B (experimentação) para descobrir o conteúdo vencedor e, em seguida, implantar os vencedores usando a opção A (baseada em regras) para a entrega contínua. A opção C (Decisão) pode ser colocada em camadas na parte superior para casos de uso que exigem seleção dinâmica baseada em catálogo, enquanto a opção A lida com regras determinísticas mais simples.

## Fases de implementação

As fases a seguir descrevem o fluxo de trabalho de implementação completo.

### Fase 1: configurar superfícies da Web

**Função do aplicativo:** AJO: configuração de canal

Defina as superfícies de canal da Web que especificam onde o conteúdo personalizado do site será entregue. Uma superfície da Web identifica um URL de página ou padrão de URL específico e o local na página (seletor de CSS ou superfície de experiência baseada em código) em que o AJO pode injetar ou substituir conteúdo.

**Pontos de decisão nesta fase:**

>[!NOTE]
>**Decisão: Tipo de superfície** — Como o conteúdo personalizado deve ser entregue à página?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Canal da Web (editor visual) | A personalização envolve modificar elementos de página visíveis (banners, títulos, imagens, CTAs) usando um editor visual de arrastar e soltar | Requer a extensão de navegador do web designer. Melhor para alterações de conteúdo orientadas por marketing. Limitado a modificações visuais de elementos de página existentes. |
| Experiência baseada em código | A personalização requer a inserção de dados estruturados (JSON) que o código do aplicativo do site consome e renderiza | Requer a implementação do desenvolvedor para consumir a carga JSON. Flexibilidade máxima para personalização complexa. Melhor para SPAs, componentes dinâmicos e renderização programática. |
| Ambos (híbrido) | Personalizações diferentes no mesmo site precisam de mecanismos de entrega diferentes | Use o canal da Web para alterações visuais simples e experiências baseadas em código para renderização programática. Aumenta a complexidade da implementação, mas maximiza a cobertura. |

>[!NOTE]
>**Decisão: Escopo da superfície** — Qual escopo de URL a superfície da web deve cobrir?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Correspondência exata de URL | O Personalization direciona uma página específica (por exemplo, página inicial, página de aterrissagem) | Direcionamento mais preciso. Requer superfícies separadas para cada página. |
| Padrão de URL com curingas | O Personalization se aplica a uma categoria de páginas (por exemplo, todas as páginas de produto, todos os artigos de blog) | Reduz a sobrecarga de gerenciamento de superfícies. As variantes de conteúdo devem ser projetadas para funcionar em todas as páginas correspondentes. |
| Superfície de aplicativo de página única (SPA) | O site é um SPA em que as alterações de URL não acionam recarregamentos de página completos | Exige configuração de [!DNL Web SDK] com reconhecimento de SPA com `sendEvent` chamadas em alterações de exibição. As definições de superfície usam o nome da exibição do SPA em vez do URL. |

Navegação da **UI:** [!DNL Journey Optimizer] > Administração > Canais > Configuração da Web

**Detalhes de configuração da chave:**

- Definir o URL da página ou o padrão de URL da superfície
- Especificar o seletor de CSS ou o URI de superfície para posicionamento de conteúdo
- Para experiências baseadas em código, defina o nome da superfície que o código do aplicativo referenciará
- Associe a superfície à sandbox da AJO em que as campanhas serão criadas

**Documentação do Experience League:**

- [Introdução ao canal da Web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [Criar experiências da Web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [Canal de experiência baseado em código](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/get-started-code-based)
- [Configuração de experiência baseada em código](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/code-based-configuration)

### Fase 2: definir públicos comportamentais

**Função do aplicativo:** RT-CDP: Avaliação de Público-Alvo

Defina segmentos de público-alvo avaliados por borda com base em sinais comportamentais na sessão que impulsionam o direcionamento de personalização. Esses públicos-alvo determinam quais visitantes se qualificam para cada experiência personalizada. A avaliação do Edge é obrigatória para esse padrão, pois as decisões de personalização devem ser tomadas em intervalos de subsegundos conforme o visitante navega no site.

**Pontos de decisão nesta fase:**

>[!NOTE]
>**Decisão: Seleção de sinal comportamental** — Quais sinais na sessão devem impulsionar o direcionamento de personalização?

| Sinal | Quando usar | Elegibilidade do Edge |
| --- | --- | --- |
| Fonte de referência / Parâmetros UTM | Personalização da página de aterrissagem específica da campanha | Elegível — verificação de atributo simples no evento atual |
| Localização geográfica (país, região, cidade) | Promoções regionais, conteúdo específico para o idioma, localizador de lojas | Elegível — verificação de atributo de perfil |
| Tipo de dispositivo (desktop, dispositivo móvel, tablet) | Layouts de conteúdo e CTAs otimizados para dispositivos | Elegível — verificação de atributo de perfil |
| Páginas visualizadas na sessão | Afinidade de categorias, recomendações de conteúdo | Elegível com restrições — somente verificações simples de contagem de eventos |
| Visitante novo vs. recorrente | Mensagens de boas-vindas, envolvimento progressivo | Elegível — A persistência ECID indica o visitante recorrente |
| Tempo no site/profundidade de rolagem | Ofertas de intenção de saída baseadas em participação | Pode exigir implementação personalizada — não é nativamente elegível para borda |

>[!NOTE]
>**Decisão: método de avaliação de público-alvo** — todos os públicos-alvo desse padrão devem usar a avaliação de borda. Confirme a qualificação antes de definir segmentos.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Avaliação da borda | Obrigatório para este padrão | As expressões de regra de segmento devem ser qualificadas para borda: comparações de atributos simples, verificações de associação de segmento, nenhuma consulta de série temporal ou funções de agregação. Latência de avaliação de subsegundos. |
| Avaliação de transmissão (fallback) | Quando a expressão de regra de segmento não é elegível para borda, mas o tempo quase real é aceitável | Latência de segundos a minutos. Suporta expressões de regra de segmento mais complexas. Pode apresentar um atraso notável na entrega da personalização. |

**Navegação da interface do usuário:** Cliente > Públicos-alvo > Criar público-alvo > Criar regra

**Detalhes de configuração da chave:**

- Use o Construtor de segmentos para definir regras de público-alvo usando atributos comportamentais
- Verifique a elegibilidade da borda confirmando se a expressão de regra de segmento usa apenas funções compatíveis (comparações de atributos simples, associação de segmento)
- Definir a política de mesclagem para a política de mesclagem edge-ative configurada em F4
- Visualize a população do público-alvo para validar se o segmento retorna os resultados esperados
- Para públicos-alvo com base em exibições de página na sessão, use atributos de nível de evento da sessão atual em vez de consultas de série temporal

**Onde as opções divergem:**

**Para a Opção A (Baseada em Regras):**
Crie segmentos distintos de público-alvo para cada variante de conteúdo. Cada segmento representa uma condição comportamental específica (por exemplo, &quot;Referência = Google E Geo = US&quot; é mapeado para a variante de conteúdo A). O número de públicos é igual ao número de regras de personalização.

**Para Opção B (Experimentação):**
A definição de público-alvo é opcional. Se o experimento segmentar todos os visitantes, nenhum público será necessário — a divisão de tráfego lida com a atribuição de variantes. Se o experimento segmentar um subconjunto específico (por exemplo, somente visitantes móveis), defina um único público-alvo de direcionamento para a qualificação do experimento.

**Para Opção C (Decisão):**
Defina os públicos-alvo para serem usados como regras de qualificação em itens de conteúdo. Esses públicos-alvo determinam quais visitantes se qualificam para quais itens de conteúdo na política de decisão. O mecanismo de decisão lida com a seleção de conteúdo entre os itens elegíveis.

**Documentação do Experience League:**

- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentação de borda](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Referência do Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)
- [Segmentação de transmissão](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)

### Fase 3: Criar conteúdo e variantes

**Função do aplicativo:** AJO: Criação de Mensagens, AJO: Experimentação de Conteúdo (Opção B), AJO: Decisão (Opção C)

Crie as variantes de conteúdo personalizadas que serão entregues aos visitantes com base na associação de público-alvo (Opção A), atribuição de experimento (Opção B) ou lógica de decisão (Opção C). Essa fase abrange a criação de conteúdo usando o web designer do AJO ou o editor de experiência baseado em código, bem como a configuração de experimento ou decisão que determina como o conteúdo é selecionado.

**Pontos de decisão nesta fase:**

>[!NOTE]
>**Decisão: abordagem de criação de conteúdo** — como as variantes de conteúdo da Web devem ser criadas?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| editor visual da Web | A equipe de marketing pode modificar visualmente os elementos da página sem código | Exige extensão de navegador. Melhor para modificações de texto, imagem e CTA. Limitado à modificação de elementos de página existentes. |
| Editor de experiência baseado em código | O conteúdo requer dados estruturados (JSON) que o código do aplicativo renderiza | Máxima flexibilidade. Requer implementação de desenvolvedor para consumir a carga. Melhor para componentes dinâmicos e SPAs. |
| Editor de código HTML/CSS | Modificações de conteúdo exigem HTML ou CSS personalizados | Controle de código direto. Requer experiência em HTML/CSS. Melhor para alterações complexas de layout. |

>[!NOTE]
>**Decisão: tokens do Personalization** — O conteúdo deve incluir personalização dinâmica usando atributos de perfil ou contextuais?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Variantes de conteúdo estático | Cada variante é um conteúdo fixo sem tokens dinâmicos | Abordagem mais simples. O conteúdo é previsível e fácil de controlar a qualidade. Não há risco de valores de atributos ausentes. |
| Conteúdo dinâmico com expressões de personalização | O conteúdo inclui tokens ao estilo Handlebars que são resolvidos para atributos de perfil ou evento (por exemplo, nome da cidade, origem de referência) | Conteúdo mais relevante. Exige valores de fallback para atributos que podem ser nulos em perfis anônimos. Use a sintaxe `{{profile.homeAddress.city}}` com auxiliares. |
| Blocos de conteúdo condicional | Blocos de conteúdo diferentes são renderizados com base nas condições do atributo em uma única variante | Reduz o número de variantes distintas necessárias. Aumenta a complexidade do conteúdo. Bom para pequenas variações em um layout compartilhado. |

**Navegação da interface do usuário:** [!DNL Journey Optimizer] > Campanhas > Selecionar campanha > Editar conteúdo

**Detalhes de configuração da chave:**

- Criar conteúdo usando o web designer (modificações visuais) ou o editor de experiência baseado em código (carga JSON)
- Usar o editor de expressão de personalização para inserir tokens dinâmicos de atributos de perfil de borda
- Configurar conteúdo de fallback para tokens de personalização que podem estar vazios em perfis anônimos
- Pré-visualização de conteúdo com perfis de teste para verificar a renderização entre cenários

**Onde as opções divergem:**

**Para a Opção A (Baseada em Regras):**
Crie uma variante de conteúdo distinta para cada segmento de público definido na Fase 2. Vincule cada variante ao público-alvo usando regras de conteúdo condicional na configuração da campanha. Verifique se existe uma variante de conteúdo padrão para visitantes que não correspondem a nenhuma regra de público-alvo.

**Para Opção B (Experimentação):**
Variantes de tratamento do autor (A, B, C etc.) para a experiência. Ative a experimentação de conteúdo na campanha, defina variantes de tratamento com seu conteúdo, defina porcentagens de alocação de tráfego e configure a métrica de sucesso.

- Definir 2-10 variantes de tratamento com conteúdo distinto
- Definir a alocação de tráfego (por exemplo, 50/50 para A/B ou divisão ponderada para testes de menor risco)
- Opcionalmente, inclua um grupo de controle (por exemplo, 10% recebe conteúdo padrão) para medir o aumento incremental
- Selecione a métrica de sucesso: aberturas exclusivas, cliques únicos, conversões ou métrica personalizada
- Defina o limite de confiança: 95% para testes padrão, 99% para decisões de alta complexidade, 90% para aprendizado direcional
- **Navegação da interface do usuário:** Campanha > Experimento de conteúdo > Adicionar tratamento > Alocação de tráfego > Métrica de sucesso

**Para Opção C (Decisão):**
Configure a pilha de componentes do Decisioning e integre-a à campanha.

1. **Criar inserções** — Defina onde os itens de conteúdo da página aparecerão (Web HTML, JSON da Web, imagem da Web)
   - Navegação da **UI:** [!DNL Journey Optimizer] > Componentes > Gerenciamento de decisão > Posicionamentos
2. **Definir regras de qualificação** — Crie regras com base nos atributos do perfil de borda que determinam quais visitantes se qualificam para cada item de conteúdo
   - Navegação da **UI:** [!DNL Journey Optimizer] > Componentes > Gerenciamento de decisão > Regras
3. **Criar itens de conteúdo (ofertas)** — Crie itens de conteúdo personalizados com representações para cada posicionamento, regras de elegibilidade, prioridade e limite opcional
   - Navegação da **UI:** [!DNL Journey Optimizer] > Componentes > Gerenciamento de decisão > Ofertas > Criar oferta
4. **Criar conteúdo de fallback** — Defina um item de fallback retornado quando nenhum item personalizado for qualificado
   - Navegação da **UI:** [!DNL Journey Optimizer] > Componentes > Gerenciamento de decisão > Ofertas > Criar oferta substituta
5. **Organizar em coleções** — Agrupe itens de conteúdo usando qualificadores de coleção (marcas) e crie coleções
   - Navegação da **IU:** [!DNL Journey Optimizer] > Componentes > Gerenciamento de decisão > Qualificadores de coleção / Coleções
6. **Criar política de decisão** — Vincule posicionamentos a coleções e selecione a estratégia de classificação (com base em prioridade, fórmula ou AI)
   - **Navegação da interface do usuário:** [!DNL Journey Optimizer] > Componentes > Gerenciamento de decisão > Decisões > Criar decisão

**Documentação do Experience League:**

- [Criar experiências da Web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [Canal de experiência baseado em código](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/get-started-code-based)
- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Criar um experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Crie ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Criar decisões](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estratégias de classificação](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Fase 4: configurar a campanha e o delivery

**Função do aplicativo:** AJO: Execução de Campanha

Crie e ative a campanha da Web do AJO que vincula a superfície da Web (Fase 1), o direcionamento de público-alvo ou a configuração de experimento (Fases 2-3) e as variantes de conteúdo (Fase 3) em uma unidade de entrega. A campanha controla quando e como o conteúdo personalizado é distribuído aos visitantes.

**Pontos de decisão nesta fase:**

>[!NOTE]
>**Decisão: Tipo de campanha** — Como a campanha deve ser acionada?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Campanha programada (sempre ativa) | O Personalization deve ser executado continuamente para todos os visitantes qualificados | Defina a data de início sem uma data de término para a personalização permanente. A avaliação de público-alvo acontece na borda em tempo real. Mais comum para personalização da Web. |
| Campanha programada (limite de tempo) | O Personalization está vinculado a um período de promoção ou evento sazonal específico | Defina datas de início e término explícitas. O Campaign é desativado automaticamente na data final. Bom para campanhas promocionais. |
| Campanha acionada por API | A entrega do Personalization deve ser acionada por um evento externo do sistema | Requer integração de API. Menos comum para personalização anônima da Web. Use quando um sistema de back-end deve controlar quando a personalização está ativa. |

**Navegação da interface do usuário:** [!DNL Journey Optimizer] > Campanhas > Criar campanha

**Detalhes de configuração da chave:**

- Selecione o canal da Web e a superfície da Web configurados na Fase 1
- Vincule o público-alvo (para a Opção A) ou defina as configurações do experimento (para a Opção B) ou incorpore a decisão (para a Opção C)
- Definir o agendamento da campanha (data inicial, data final ou sempre ativa)
- Configurar limite de frequência no nível da campanha, se aplicável
- Revisar todas as configurações e ativar a campanha

**Onde as opções divergem:**

**Para a Opção A (Baseada em Regras):**
Crie uma campanha por regra de personalização, cada uma direcionada a um público de borda diferente com sua variante de conteúdo correspondente. Como alternativa, use uma única campanha com regras de conteúdo condicionais que mapeiam a associação do público-alvo às variantes de conteúdo em uma campanha.

**Para Opção B (Experimentação):**
Crie uma única campanha com a experimentação de conteúdo ativada. A configuração do experimento (variantes, alocação de tráfego, métrica de sucesso) foi definida na Fase 3. Ative a campanha para iniciar o experimento.

**Para Opção C (Decisão):**
Crie uma campanha que incorpore a política de decisão configurada na Fase 3. A ação de conteúdo da campanha faz referência ao escopo de decisão, que aciona o mecanismo de decisão na borda. Ative a campanha para iniciar a entrega de conteúdo com base em decisão.

**Documentação do Experience League:**

- [Criar uma campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Introdução às campanhas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Entregar ofertas em mensagens](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### Fase 5: relatar e analisar o desempenho

**Função do aplicativo:** AJO: Relatórios e análise de desempenho

Monitore o desempenho da personalização usando relatórios integrados do AJO e, opcionalmente, estenda a análise com o CJA para obter insights mais profundos entre canais. Essa fase abrange acessar relatórios de campanha dinâmicos e históricos, revisar resultados de experimentos e criar espaços de trabalho de análise personalizados.

**Pontos de decisão nesta fase:**

>[!NOTE]
>**Decisão: profundidade dos relatórios** — que profundidade deve ter a análise de desempenho?

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Somente relatórios nativos do AJO | As métricas básicas de entrega e envolvimento são suficientes | Fornece métricas de impressões, cliques, CTR e conversão prontas para uso. Disponível imediatamente na interface do usuário da campanha. Personalização limitada. |
| Relatórios do AJO + análise do CJA | É necessária uma análise profunda do funnel, uma comparação de coorte ou uma medição de impacto entre canais | Exige conexão do CJA e visualização de dados vinculadas aos conjuntos de dados do AJO. Permite a análise de forma livre, métricas calculadas personalizadas, modelagem de atribuição e publicação de público-alvo. |

**Navegação da interface do usuário:** [!DNL Journey Optimizer] > Campanhas > Selecionar campanha > Exibir relatório

**Detalhes de configuração da chave:**

- Acesse o relatório ao vivo durante campanhas ativas para monitorar a entrega em tempo real (atualizações a cada 60 segundos, programas das últimas 24 horas)
- Acesse o relatório histórico (sempre) após a conclusão da campanha para obter uma análise abrangente (pode levar até 2 horas para ser totalmente preenchido)
- Para a Opção B (Experimentação): revise o relatório do experimento para obter comparação do desempenho do tratamento, intervalos de confiança e declaração do vencedor
- Para análise do CJA: verifique se uma conexão com o CJA inclui conjuntos de dados de eventos de experiência do AJO e se uma visualização de dados está configurada com métricas de personalização da Web

**Onde as opções divergem:**

**Para a Opção A (Baseada em Regras):**
Analise os relatórios de campanha de cada segmento de público-alvo para comparar as métricas de entrega e envolvimento entre variantes de conteúdo personalizadas. Use o CJA para criar um espaço de trabalho de comparação que mede o impacto da conversão de conteúdo personalizado em relação ao padrão.

**Para Opção B (Experimentação):**
Revise o relatório do experimento para obter confiança estatística, aumento do tratamento e identificação do vencedor. Aguarde o limite de confiança ser atingido antes de declarar um vencedor. Aplicar conteúdo vencedor como a variante permanente (transição para a Opção A para entrega contínua).

- **Navegação da interface do usuário:** Campanha > Experimento de conteúdo > Exibir relatório
- **Experience League:** [Relatório de experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)

**Para Opção C (Decisão):**
Revise as métricas de desempenho de decisão, incluindo taxas de impressão da oferta, frequência de seleção e atribuição de conversão por item de conteúdo. Analise o desempenho das estratégias de classificação e se o conteúdo de fallback está sendo distribuído com muita frequência (indicando que as regras de elegibilidade são muito restritivas).

**Documentação do Experience League:**

- [Relatório em tempo real da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Relatório global da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Trabalhar com o Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Visão geral do Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Cálculos estatísticos no experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

## Considerações de implantação

Esta seção aborda medidas de proteção, armadilhas comuns, práticas recomendadas e decisões de compensação para esse padrão de caso de uso.

### Medidas de proteção e limites

Revise as seguintes medidas de proteção antes e durante a implementação.

- Os segmentos do Edge estão limitados a verificações de atributos simples e associação de segmentos — sem consultas de série temporal ou agregações complexas — [Elegibilidade da segmentação do Edge](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- Somente uma política de mesclagem pode estar ativa na borda por sandbox — [Medidas de proteção do perfil](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Máximo de 4.000 definições de segmento por sandbox — [Medidas de proteção de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Máximo de 500 campanhas ativas por sandbox — [medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Máximo de 10 variantes de tratamento por experimento de conteúdo — [Limites de experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Máximo de 10.000 ofertas personalizadas aprovadas por sandbox (Opção C) — [Medidas de proteção do Gerenciamento de decisão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Máximo de 30 disposições por decisão (Opção C) — [medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Os modelos de classificação de IA exigem um mínimo de 1.000 eventos de conversão para treinamento (opção C)
- SLA de tempo de resposta do [!DNL Edge Network]: &lt; 200 ms para segmentos avaliados de borda
- Expiração de perfil pseudônimo: configurável de 14 a 365 dias para perfis somente ECID
- Os relatórios ao vivo são atualizados a cada 60 segundos e mostram as últimas 24 horas de dados
- Os relatórios históricos podem levar até 2 horas para serem totalmente preenchidos após a conclusão da campanha

### Armadilhas comuns

Evite os seguintes erros comuns de implementação.

- **[!DNL Web SDK]não está enviando sinais comportamentais para a AEP:** Verifique se a sequência de dados tem o serviço [!DNL Adobe Experience Platform] habilitado e se o conjunto de dados do evento está mapeado corretamente. Sem isso, os perfis de borda do não são preenchidos e a avaliação do público-alvo falha silenciosamente — o visitante recebe o conteúdo padrão sem nenhuma indicação de erro.
- **Público-alvo do Edge retornando zero qualificação:** a segmentação do Edge tem requisitos de qualificação estritos. Consultas de série temporal, funções de agregação e consultas de várias entidades não são qualificadas para borda. Substitua a expressão de regra de segmento usando comparações de atributos simples ou verificações de associação de segmento.
- **Política de mesclagem não ativa na borda:** Se a política de mesclagem usada pelo segmento de público-alvo não tiver `isActiveOnEdge: true`, as pesquisas de perfil de borda falharão e a personalização não será entregue. Somente uma política de mesclagem por sandbox pode estar ativa na borda — verifique se não existe conflito.
- **Cintilação do Personalization no carregamento da página:** A chamada [!DNL Web SDK] `sendEvent` que recupera propostas de personalização deve ser executada antes que a página renderize a área de conteúdo de destino. Implemente a pré-ocultação de trechos ou a renderização assíncrona para impedir que o conteúdo padrão pisque antes que o conteúdo personalizado seja carregado.
- **Conteúdo não renderizado nas alterações de rota de SPA:** aplicativos de página única exigem chamadas `sendEvent` explícitas com informações de exibição atualizadas quando a rota é alterada. Sem isso, o [!DNL Edge Network] não reavalia a personalização da nova exibição.
- **O experimento não está atingindo significância estatística:** Volume de tráfego insuficiente ou muitas variantes de tratamento diluem o tamanho da amostra por variante. Reduza o número de variantes ou aumente a duração do experimento. Não pare os experimentos prematuramente - os resultados podem ser enganosos.
- **Decisão de retornar somente o conteúdo de fallback:** verifique se os itens de conteúdo personalizados estão aprovados, dentro de seu intervalo de datas de validade, e se as regras de elegibilidade correspondem aos atributos de perfil de borda do visitante anônimo. Verifique também se os limites de limite não foram atingidos.

### Práticas recomendadas

Siga estas recomendações para uma implementação bem-sucedida.

- **Comece simples e depois repita:** Comece com a Opção A (Baseada em Regras) para personalização inicial e use a Opção B (Experimentação) para validar as hipóteses e a Opção C (Decisão) para casos de uso avançados. Cada opção se baseia na infraestrutura básica.
- **Usar pré-ocultação para prevenção de cintilação:** Implemente o trecho pré-ocultação do AEP nas páginas em que a personalização será entregue. Isso oculta a área de conteúdo de destino até que o conteúdo personalizado esteja pronto para ser renderizado, evitando cintilação visual.
- **Criar conteúdo de fallback deliberadamente:** o conteúdo padrão (não personalizado) deve ser uma experiência de alta qualidade por conta própria. Os visitantes que não se qualificam para personalização — ou quando a resposta do [!DNL Edge Network] é atrasada — não devem receber uma experiência degradada.
- **Valide a qualificação de borda antes de criar públicos-alvo:** Antes de investir no desenvolvimento de regras de público-alvo, confirme se a expressão de regras de segmento é qualificada para borda revisando os critérios de qualificação no Experience League. As expressões não qualificadas retornarão silenciosamente para a avaliação em lote ou por transmissão com latência inaceitável para esse padrão.
- **Monitorar desempenho de entrega de borda:** Configure alertas de monitoramento para [!DNL Edge Network] tempos de resposta e falhas de entrega de personalização. Problemas de entrega do Edge são invisíveis para o visitante (eles veem conteúdo padrão) e podem não ser detectados sem o monitoramento pró-ativo.
- **Configurar a expiração de perfis com pseudônimos:** Defina os períodos de expiração apropriados para perfis de borda anônimos para equilibrar a personalização entre sessões (reconhecendo visitantes recorrentes) com a conformidade de privacidade e o gerenciamento de armazenamento.
- **Testar com perfis representativos:** ao visualizar conteúdo personalizado, use perfis de teste que representem os cenários de visitante anônimo reais (sem dados de CRM, histórico comportamental limitado, várias localizações geográficas e dispositivos).

### Decisões de compensação

Considere as seguintes compensações ao planejar sua implementação.

>[!NOTE]
>**Contrapartida: amplitude do Personalization vs. complexidade da implementação**
>
>A personalização mais granular (muitos públicos-alvo, muitas variantes de conteúdo) produz experiências mais relevantes, mas aumenta a complexidade da configuração e a sobrecarga na produção de conteúdo.
>
>- **A ampla personalização favorece:** simplicidade, tempo de entrega mais rápido, menor custo de produção de conteúdo. Um pequeno número de públicos-alvo e variantes abrange a maioria dos visitantes com personalização significativa.
>- **A personalização granular favorece:** relevância máxima, aumento de engajamento maior, melhores taxas de conversão. Muitos públicos-alvo e variantes abordam sinais comportamentais específicos com conteúdo personalizado.
>- **Recomendação:** comece com 3 a 5 regras de personalização de alto impacto direcionadas aos segmentos de visitantes mais comuns (por exemplo, fonte de referência, tipo de dispositivo, região geográfica). Avalie o impacto e, em seguida, amplie para regras mais granulares com base no desempenho e no valor comercial observados.

>[!NOTE]
>**Contrapartida: determinismo baseado em regras vs. otimização orientada por IA**
>
>As abordagens baseadas em regras (Opção A) fornecem aos negócios controle total sobre qual conteúdo cada visitante visualiza. As abordagens classificadas por IA (Opção C) otimizam a seleção de conteúdo ao longo do tempo, mas reduzem a visibilidade do motivo pelo qual um conteúdo específico foi selecionado.
>
>- **Vantagens baseadas em regras:** Previsibilidade, auditoria, controle comercial. As equipes de marketing sabem exatamente qual conteúdo cada segmento recebe e podem explicar a lógica às partes interessadas.
>- **Favoritos orientados por IA:** Otimização de desempenho, escalabilidade, aprimoramento contínuo. O modelo de IA descobre afinidades de conteúdo-visitante que a escrita de regras humanas pode perder.
>- **Recomendação:** use baseada em regras para decisões de conteúdo de alto risco, nas quais a consistência da marca e a transparência das partes interessadas são fundamentais. Use a classificação de IA para grandes catálogos de conteúdo em que o gerenciamento manual de regras se torna difícil e a otimização contínua fornece um aumento mensurável.

>[!NOTE]
>**Contrapartida: persistência de perfil anônimo vs. conformidade com a privacidade**
>
>A expiração maior do perfil de pseudônimo permite uma melhor personalização entre sessões (reconhecendo visitantes recorrentes, criando contexto comportamental ao longo do tempo). A expiração menor melhora a conformidade com a privacidade e reduz os custos de armazenamento.
>
>- **A expiração mais longa favorece:** perfis anônimos mais avançados, melhor reconhecimento de visitantes, mais dados para decisões de personalização. Defina a expiração para 90-365 dias.
>- **A expiração mais curta favorece:** conformidade com a privacidade (GDPR, CCPA), custos de armazenamento reduzidos, risco minimizado de dados de perfil obsoletos. Defina a expiração para 14-30 dias.
>- **Recomendação:** Alinhe a expiração com a política de consentimento de cookies e os requisitos de privacidade de sua organização. Para a maioria das implementações, de 30 a 90 dias fornecem um equilíbrio razoável entre o valor de personalização e a conformidade com a privacidade.

## Documentação relacionada

Os seguintes recursos do Experience League fornecem detalhes adicionais sobre os recursos usados neste padrão de caso de uso.

**Canal da Web e experiências baseadas em código**

- [Introdução ao canal da Web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [Criar experiências da Web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [Canal de experiência baseado em código](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/get-started-code-based)
- [Configuração de experiência baseada em código](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/code-based-configuration)

**Públicos-alvo e segmentação**

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentação de borda](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Segmentação de transmissão](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Referência do Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

**Personalization e conteúdo**

- [Adicionar personalização](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Sintaxe do Personalization](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Trabalhar com modelos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Trabalhar com fragmentos de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)

**Experimentação de conteúdo**

- [Introdução ao experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Criar um experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Relatório de experimento de conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Cálculos estatísticos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

**Gerenciamento de decisão**

- [Visão geral da Gestão de decisões](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Criar inserções](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Criar regras de decisão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Crie ofertas personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Criar ofertas substitutas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Criar coleções](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Criar decisões](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Estratégias de classificação](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [Entregar ofertas em mensagens](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

**Campanhas**

- [Introdução às campanhas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Criar uma campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)

**[!DNL Web SDK]e coleta de dados**

- [Visão geral do Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Instalar o Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
- [Configurar sequências de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Visão geral das tags](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)

**Identidade e perfil**

- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Visão geral dos namespaces de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/namespaces)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [Visão geral do Perfil do cliente em tempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

**Modelagem de dados**

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Noções básicas de composição de esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)

**Relatórios e análises**

- [Relatório em tempo real da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Relatório global da campanha](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Trabalhar com o Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Visão geral do Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Visão geral do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)

**Privacidade e governança de dados**

- [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Visão geral do gerenciamento avançado do ciclo de vida dos dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)
- [Grupo de campos Consentimento e preferências](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)

**Medidas de proteção**

- [Medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Medidas de proteção do serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)
