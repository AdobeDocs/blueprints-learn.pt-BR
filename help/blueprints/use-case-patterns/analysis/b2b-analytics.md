---
title: Análise B2B
description: Saiba como incluir informações a nível de conta B2B na análise de jornada de clientes entre canais.
solution: Customer Journey Analytics, Real-Time Customer Data Platform
exl-id: 9d576e5c-cbd2-4c60-a6b0-88f8b8b963b4
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '7528'
ht-degree: 1%

---

# Análise B2B

Este guia fornece uma referência de implementação abrangente para análise de nível de conta B2B usando o B2B edition [!DNL Customer Journey Analytics] ([!DNL CJA]) e o B2B edition [!DNL Real-Time Customer Data Platform] ([!DNL RT-CDP]). Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam incorporar informações de nível de conta B2B na análise de jornada de clientes entre canais.

Abrange todas as abordagens viáveis para a análise centrada em conta, desde estruturas de conta simples até hierarquias de conta globais complexas, com orientação sobre quando escolher cada opção. O plano aborda conexões de dados B2B, configuração da visualização de dados da conta, análise de espaço de trabalho e publicação do painel.

O B2B Analytics estende os recursos [!DNL CJA] padrão com conexões baseadas em conta, contêineres específicos B2B (Conta, Conta global, Oportunidade, Grupo de compras) e relatórios no nível da conta. Esse recurso permite que as organizações analisem o marketing e o envolvimento de vendas no nível da conta, rastreiem a progressão da oportunidade, avaliem a integridade do grupo de compras e atribuam a receita aos pontos de contato de marketing em ciclos de vendas B2B estendidos.

## Visão geral do caso de uso

As organizações B2B enfrentam um desafio fundamental de análise: seus clientes não são pessoas individuais, mas contas compostas por várias partes interessadas, grupos de compra e oportunidades. A análise padrão com base em pessoas não consegue responder perguntas como &quot;Quais contas são mais engajadas?&quot;, &quot;Qual é o nível de conclusão de nossos grupos de compra?&quot; ou &quot;Quais pontos de contato de marketing impulsionam a progressão da oportunidade?&quot;

A análise B2B aborda isso aproveitando o B2B edition [!DNL CJA] para criar exibições analíticas centradas em conta que combinam dados comportamentais no nível da pessoa com dimensões de conta, oportunidade e grupo de compra. [!DNL RT-CDP] O B2B edition fornece a unificação subjacente do perfil da conta e a resolução de identidade B2B que alimenta a camada de análise. Juntas, essas soluções permitem que as organizações criem análises de jornada entre canais no nível da conta, correlacionem o envolvimento de marketing com a progressão do pipeline e forneçam insights acionáveis para as equipes de marketing e de vendas.

O público-alvo inclui equipes de operações de marketing B2B, líderes de geração de demanda, analistas de operações de receita e líderes de vendas que precisam de visibilidade sobre o envolvimento no nível da conta e a integridade do pipeline.

## Principais objetivos de negócios

Os seguintes objetivos de negócios são compatíveis com esse padrão de caso de uso.

### Melhorar a análise e os relatórios

Aprimore os recursos de relatórios para obter insights de marketing mais rápidos e acionáveis por meio de painéis unificados e ferramentas de autoatendimento. A análise B2B permite que as organizações consolidem dados de envolvimento no nível da conta de várias fontes em um único ambiente analítico, fornecendo visibilidade entre canais sobre como os programas de marketing influenciam o pipeline e a receita.

**KPIs:** eficiência, produtividade

[Saiba mais sobre como melhorar o Analytics e os relatórios](/help/blueprints/business-objectives/analytics-insights/improve-analytics-reporting.md)

### Permita a tomada de decisões orientadas por dados

Capacite as equipes com análises de autoatendimento, insights do cliente em tempo real e previsões alimentadas por IA para orientar a estratégia. A análise no nível da conta equipe de marketing e vendas com os dados necessários para priorizar contas, otimizar estratégias de engajamento e alinhar-se às oportunidades de pipeline.

**KPIs:** eficiência, produtividade

[Saiba mais sobre como ativar a tomada de decisões orientadas por dados](/help/blueprints/business-objectives/analytics-insights/enable-data-driven-decision-making.md)

### Melhorar a qualificação e a conversão de clientes potenciais

Aumente a qualidade do lead e acelere a progressão do pipeline por meio de pontuação, estimulação e acompanhamento personalizado. O CJA B2B edition oferece janelas de pesquisa de conta estendidas por 13 meses, especificamente projetadas para ciclos de vendas B2B, permitindo uma atribuição precisa de multitoque em toda a jornada da conta.

**KPIs:** Eficiência, Receita Incremental

[Saiba mais sobre como melhorar a qualificação e a conversão de clientes potenciais](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

## Exemplo de casos de uso tático

Os cenários a seguir ilustram como esse padrão pode ser aplicado na prática.

- **Análise de pontuação de engajamento da conta** — meça e classifique as contas por seu envolvimento agregado na Web, email, eventos e interações de conteúdo para identificar contas de alta intenção para acompanhamento de vendas
- **Rastreamento da integridade do grupo de compras** — Analise a composição do grupo de compras entre contas para identificar lacunas na cobertura de funções e priorizar a aquisição de clientes potenciais para grupos de compras incompletos
- **Correlação do pipeline de oportunidade** — Correlacione os dados de envolvimento de marketing com a progressão do estágio de oportunidade para entender quais campanhas e pontos de contato impulsionam o avanço do pipeline
- **Atribuição B2B multitoque** — aplique modelos de atribuição com janelas de retrospectiva de 13 meses para creditar pontos de contato de marketing em toda a jornada de compra B2B, do primeiro contato ao fechado
- **Mapeamento de jornada de conta** — Visualize a jornada de conta entre canais desde a percepção inicial até a criação e o fechamento da oportunidade, identificando caminhos e pontos de atrito comuns
- **Influência da campanha no pipeline** — meça como campanhas específicas influenciam a criação de pipeline de conta, o avanço da oportunidade e a geração de receita
- **Progressão do engajamento do grupo de compras** — controle como as pontuações do engajamento do grupo de compras evoluem com o tempo e correlacione os limites de engajamento com os resultados da oportunidade
- **Desempenho do conteúdo baseado em conta** — Analise quais ativos e tópicos de conteúdo refletem em segmentos de conta, setores ou funções de grupo de compras específicos
- **Painéis de alinhamento de vendas e marketing** — crie painéis compartilhados que fornecem às equipes de marketing e vendas uma exibição unificada do envolvimento da conta, da integridade do pipeline e da atribuição de receita
- **Segmentação de conta para ativação** — crie segmentos B2B com base em análises no nível da conta (por exemplo, &quot;contas altamente engajadas sem oportunidades abertas&quot;) e publique-as para ativação downstream

## Indicadores-chave de desempenho

Os KPIs a seguir ajudam a medir o sucesso desse padrão de caso de uso.

| KPI | Descrição | Abordagem de medição |
| --- | --- | --- |
| Pontuação de engajamento da conta | Agregar métrica de envolvimento em todos os contatos de uma conta | Métrica calculada que combina visitas da Web, interações por email, participação em eventos e downloads de conteúdo no nível da conta |
| Integridade do Grupo de Compras | Porcentagem de funções necessárias preenchidas em um grupo de compra | Taxa de funções preenchidas para total de funções necessárias por grupo de compra, rastreadas ao longo do tempo |
| Pipeline influenciado pelo marketing | Receita no pipeline que foi afetada por atividades de marketing | Valor de oportunidade em que os contatos de conta associados têm pontos de contato de marketing dentro da janela de atribuição |
| Índice de conversão de conta em oportunidade | Porcentagem de contas envolvidas que geram oportunidades qualificadas | Contas com oportunidades divididas pelo total de contas envolvidas durante um período definido |
| Duração média do ciclo de negociações | Tempo desde o primeiro contato de marketing até as conclusões | Duração média desde o primeiro ponto de contato atribuído até a data de fechamento da oportunidade |
| Receita de atribuição de marketing | Receita atribuída aos pontos de contato de marketing | Receita de oportunidades fechadas com contatos de marketing, distribuída por modelo de atribuição |
| Alcance e penetração da conta | Número de contatos envolvidos por conta de público alvo | Contatos exclusivos com interações de marketing por conta, em comparação ao total de contatos conhecidos |
| Envolvimento de conteúdo por função de compra | Métricas de engajamento segmentadas pela função de grupo de compra | Exibições de página, downloads e tempo gasto detalhados por personalidade/função nos grupos de compra |

## Padrão do caso de uso

**Análise B2B**

Inclua informações a nível de conta B2B na análise de jornada de clientes entre canais.

**Cadeia de funções:** Conexão de Dados B2B > Configuração de Exibição de Dados da Conta > Workspace Analysis > Publicação de Painel

## Aplicativos

Os aplicativos a seguir são usados para implementar esse padrão de caso de uso.

- **[!DNL Customer Journey Analytics]B2B edition** — Fornece conexões baseadas em conta, contêineres de visualização de dados específicos B2B, análise de espaço de trabalho em nível de conta, análise de grupo de compras, análise de oportunidade, segmentação B2B e atribuição B2B com janelas de retrospectiva estendidas
- **[!DNL Real-Time CDP]B2B edition** — Fornece a base de dados B2B incluindo unificação de perfil de conta, resolução de identidade B2B, classes de esquema B2B (Conta, Oportunidade, Grupo de Compras) e integração [!DNL Marketo Engage] para assimilação de dados de envolvimento B2B

## Funções básicas

Os seguintes recursos básicos devem estar em vigor para esse padrão de caso de uso. Para cada função, o status indica se ele é tipicamente necessário, se presume ser pré-configurado ou se não é aplicável.

| Função de base | Status | O que deve estar em vigor | Referência do Experience League |
| --- | --- | --- | --- |
| Administração e governança | Obrigatório | Sandbox configurada com [!DNL CJA] direitos de B2B edition e [!DNL RT-CDP] B2B edition. Funções provisionadas para engenheiros de dados, analistas e usuários de operações de marketing com acesso ao [!DNL CJA] e ao modelo de dados B2B. | [Visão geral das sandboxes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/home) |
| Preparação e modelagem de dados | Obrigatório | Esquemas XDM B2B configurados usando classes B2B: conta de negócios XDM, oportunidade de negócios XDM, relação pessoal da conta de negócios XDM, relação pessoal da oportunidade de negócios XDM e membros da lista de marketing de negócios XDM. Os grupos de campos para atributos de conta, estágios de oportunidade e funções de grupo de compra devem ser definidos. Conjuntos de dados criados e ativados para Perfil. | [Visão geral do sistema XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/home), [esquemas do B2B edition](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/schemas/b2b) |
| Fontes de dados e coleção | Obrigatório | Fontes de dados B2B conectadas, normalmente por meio do conector de origem [!DNL Marketo Engage] ou do conector de origem do CRM [!DNL Salesforce]. Registros de conta, registros de oportunidade, relacionamentos entre pessoas e contas e eventos de envolvimento comportamental devem fluir para os conjuntos de dados da AEP. [!DNL Web SDK] ou a integração do [!DNL Marketo] deve capturar eventos comportamentais com a associação da conta. | [Visão geral das fontes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/home), [Conector do Marketo Engage](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) |
| Configuração de identidade e perfil | Obrigatório | Resolução de identidade B2B configurada para resolver relacionamentos entre pessoas e contas. A ID da conta, a ID da pessoa ([!DNL Marketo] ID de cliente potencial ou ID de contato do CRM) e as identidades entre dispositivos (ECID, email) devem ser vinculadas. O gráfico de identidade deve suportar o mapeamento de muitas para muitas pessoas para conta inerente aos modelos de dados B2B. | [Visão geral do Serviço de Identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/home), [Resolução de identidade B2B](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/schemas/b2b) |
| Definição e segmentação do público-alvo | Presumido em vigor | As definições de público-alvo no nível da conta devem estar disponíveis se os segmentos B2B forem publicados de [!DNL CJA] de volta para o AEP para ativação. Para casos de uso exclusivos do Analytics, esse não é um pré-requisito estrito, mas é recomendado para a análise baseada em segmentos. | [Visão geral do Serviço de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/home) |

## Funções de suporte

Os recursos a seguir aumentam esse padrão de caso de uso, mas não são necessários para a execução principal.

| Função de suporte | Status | Por que é importante | Referência do Experience League |
| --- | --- | --- | --- |
| Criação de atributo calculado/derivado | Recomendado | Atributos computados em perfis de conta (por exemplo, pontuação total de engajamento, dias desde a última atividade, contagem de oportunidades) enriquecem as dimensões analíticas disponíveis em [!DNL CJA] para análise em nível de conta. | [Visão geral dos atributos computados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/computed-attributes/overview) |
| Gerenciamento do ciclo de vida dos dados | Recomendado | Os conjuntos de dados B2B, especialmente os dados de eventos comportamentais de [!DNL Marketo Engage], podem crescer rapidamente. As políticas de expiração do conjunto de dados ajudam a gerenciar o armazenamento e a garantir a conformidade com os requisitos de retenção de dados. | [Gerenciamento Avançado do Ciclo de Vida dos Dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-lifecycle/home) |
| Rotulagem e aplicação de uso de dados | Recomendado | Os dados B2B geralmente contêm informações comerciais confidenciais (valores contratuais, inteligência competitiva). Os rótulos de uso de dados e as políticas de governança garantem que esses dados sejam usados adequadamente em workflows de análise e ativação. | [Visão geral da governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/home) |
| Monitoramento e capacidade de observação | Recomendado | Os conectores de origem B2B ([!DNL Marketo], [!DNL Salesforce]) exigem monitoramento para integridade da assimilação. O monitoramento da integridade da conexão em [!DNL CJA] garante a atualização de dados para o Analytics. As regras de alerta para falhas de assimilação impedem painéis obsoletos. | [Visão geral dos Insights de Capacidade de Observação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/home) |
| Relatórios e análise | Incluído | Esse padrão é, em si, um padrão de análise. Essa função é incluída inerentemente, pois a cadeia de funções principal fornece recursos de relatório e análise. | [visão geral do CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-overview/cja-overview) |

## Funções do aplicativo

Este plano exerce as seguintes funções do Catálogo de Funções da Aplicação. As funções são mapeadas para fases de implementação em vez de etapas numeradas.

### B2B edition [!DNL Customer Journey Analytics]

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Conexão baseada em conta | Fase 1: Conexão de dados B2B | Configure conexões usando Conta ou Conta global como o identificador principal para a análise no nível da organização |
| Configuração da visualização de dados B2B | Fase 2: configuração da visualização de dados da conta | Definir visualizações de dados com contêineres específicos B2B (Conta, Conta global, Oportunidade, Grupo de compras) junto com contêineres padrão Pessoa, Sessão e Evento |
| Análise da Workspace no nível da conta | Fase 3: Análise do Workspace | Crie análises de forma livre usando dimensões, métricas e contêineres B2B no nível da conta para obter insights de jornada no nível da organização |
| Análise do grupo de compras | Fase 3: Análise do Workspace | Analisar a composição, o envolvimento e a progressão do grupo de compras por meio do processo de decisão de compra |
| Análise de oportunidade | Fase 3: Análise do Workspace | Rastrear a progressão da oportunidade em estágios do funnel de vendas e correlacionar com os dados de envolvimento de marketing |
| Segmentação B2B | Fase 3: Análise do Workspace | Criar segmentos usando contêineres B2B para análise em nível de conta filtrada |
| Atribuição B2B | Fase 3: Análise do Workspace | Aplicar modelos de atribuição com janelas de pesquisa de conta estendidas de 13 meses para análise do ciclo de vendas B2B |
| Criação de métricas calculadas | Fase 3: Análise do Workspace | Definir métricas calculadas para KPIs B2B, como taxa de envolvimento da conta, integridade do grupo de compra e influência do pipeline |
| Publicação de painel e scorecard | Fase 4: Publicação do painel | Crie e compartilhe painéis e cartões de pontuação móveis para liderança de marketing e vendas |
| Publicação de público alvo | Fase 4: Publicação do painel | Publicar públicos-alvo baseados na conta definidos por [!DNL CJA] de volta no AEP para ativação downstream |

### [!DNL Customer Journey Analytics] — funções padrão

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Conexão de dados | Fase 1: Conexão de dados B2B | Associar conjuntos de dados B2B do AEP a [!DNL CJA] conexões para análise entre canais |
| Configuração da visualização de dados | Fase 2: configuração da visualização de dados da conta | Configurar dimensões, métricas, atribuição e configurações de persistência padrão na visualização de dados B2B |
| Análise do Workspace | Fase 3: Análise do Workspace | Criar análise de forma livre com visualizações de tabelas, fallout, fluxo, coorte e atribuição |
| Análise guiada | Fase 3: Análise do Workspace | Usar fluxos de trabalho guiados para análise de funnel, tendência e retenção no nível da conta |

### B2B edition [!DNL Real-Time CDP]

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Unificação de perfil da conta | Pré-requisito (F2/F4) | Consolidar dados B2B entre origens em perfis de conta unificados usando classes de esquema B2B XDM especializadas |
| Resolução de identidade B2B | Pré-requisito (F4) | Resolver relacionamentos pessoa-para-conta com suporte para hierarquias de contas de vários níveis e mapeamentos muitos-para-muitos |
| Integração do [!DNL Marketo Engage] | Pré-requisito (F3) | Assimilar dados de envolvimento comportamental e registros de conta/cliente potencial de [!DNL Marketo Engage] por meio de conectores de origem B2B nativos |

## Pré-requisitos

Os itens a seguir devem estar em vigor antes do início da implementação.

- [ ] [!DNL CJA] licença do B2B edition ativa e provisionada para a organização
- [ ] [!DNL RT-CDP] A licença do B2B edition está ativa com esquemas B2B e perfis de conta configurados
- [ ] esquemas XDM B2B são definidos (conta, oportunidade, relação pessoal da conta, relação pessoal da oportunidade, membros da lista de marketing)
- [ ] [!DNL Marketo Engage] e/ou conectores de origem do CRM estão configurados e assimilando dados ativamente
- [ ] Dados de evento comportamentais a nível de conta (visitas da Web, interações por email, envios de formulários) estão fluindo para a AEP com a associação da conta
- [ ] relações pessoa-conta são estabelecidas no gráfico de identidade
- [ ] Pelo menos 30 dias de dados históricos do engajamento B2B estão disponíveis para análise significativa
- [ ] As partes interessadas concordaram em comprar definições de função de grupo e mapeamentos de interesse de solução
- [ ] [!DNL CJA] contas de usuário são provisionadas com perfis de produto apropriados para os recursos do B2B edition
- [ ] Os KPIs do Target e os requisitos de relatórios foram definidos pela liderança de marketing e vendas

## Opções de implementação

As seções a seguir descrevem diferentes abordagens para implementar esse padrão de caso de uso.

### Opção A: análise centrada em conta

**Recomendado para:** Organizações que desejam analisar todos os dados de envolvimento e pipeline através da lente da conta. Essa abordagem usa o contêiner Conta como a unidade analítica principal, fornecendo uma visão de cima para baixo de como as contas avançam pela jornada de compra.

**Como funciona:**

Configure uma conexão B2B [!DNL CJA] com Account como o identificador principal. Todos os eventos comportamentais, oportunidades e dados do grupo de compras são acumulados no nível da conta. A visualização de dados usa Conta como o contêiner de nível mais alto, com Pessoa, Sessão e Evento aninhados. Isso permite a análise como &quot;Quantas contas visitaram a página de preços e criaram uma oportunidade em 30 dias?&quot;

A análise centrada em conta fornece a visualização mais natural para organizações B2B, onde a conta é a unidade de compra. Dimensões como setor, tamanho da empresa, nível da conta e proprietário da conta podem ser usadas para detalhar os padrões de envolvimento e as métricas do pipeline. A atribuição é aplicada no nível da conta com janelas de retrospectiva de 13 meses que acomodam longos ciclos de vendas B2B.

**Principais considerações:**

- Requer um mapeamento limpo de conta para pessoa no gráfico de identidade
- Todos os eventos de nível de pessoa devem ser atribuíveis a uma conta
- O tráfego da Web anônimo que não pode ser associado a uma conta não aparecerá na análise em nível de conta

**Vantagens:**

- Fornece uma visualização real em nível de conta de toda a jornada de compra
- Habilita atribuição baseada em conta que corresponde a como a receita B2B é gerada
- Oferece suporte à análise de grupos de compras e oportunidades como contêineres aninhados na conta
- Alinha a análise à estratégia de marketing baseado em conta (ABM)

**Limitações:**

- Requer uma resolução de identidade robusta de pessoa para conta
- Dados de engajamento anônimos ou sem correspondência são excluídos da análise
- Mais complexo de configurar do que a análise centrada em pessoas

**Experience League:**

- [Visão geral do CJA B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)
- [Esquemas do B2B edition](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/schemas/b2b)

### Opção B: análise global centrada em conta

**Recomendado para:** organizações empresariais com hierarquias de contas complexas nas quais uma empresa pai tem várias contas de subsidiária. Essa abordagem usa Conta Global como o identificador principal, totalizando todas as atividades da conta subsidiária no nível da organização-pai.

**Como funciona:**

Configure a conexão B2B [!DNL CJA] com a Conta Global como o identificador principal em vez da Conta. Isso agrega os dados de engajamento de todas as contas do subsidiário na organização principal. Por exemplo, se a &quot;Acme Corp&quot; tiver subsidiárias regionais &quot;Acme EMEA&quot; e &quot;Acme APAC&quot;, uma conexão de Conta global consolidará todos os engajamentos das três entidades em uma única visualização analítica.

A visualização de dados inclui Conta global como o contêiner de nível superior, com Conta, Pessoa, Sessão e Evento como contêineres aninhados. Isso permite a análise nos níveis de conta global e subsidiária no mesmo projeto do espaço de trabalho. As janelas de retrospectiva de atribuição se aplicam no nível da conta global, capturando todos os pontos de contato em toda a hierarquia corporativa.

**Principais considerações:**

- Requer dados de hierarquia de conta com relações pai-filho definidas no modelo de dados B2B
- A ID de conta global deve ser preenchida e precisa em todos os registros de conta
- As contas da subsidiária devem ser mapeadas corretamente ao pai

**Vantagens:**

- Oferece visibilidade consolidada em estruturas complexas de contas corporativas
- Evita análises fragmentadas quando um único cliente corporativo tem vários registros de conta
- Permite a comparação entre subsidiárias regionais em uma única conta global
- Oferece suporte a emissão de relatórios de receita e pipeline de nível corporativo

**Limitações:**

- Requer dados precisos de hierarquia de conta, que muitas organizações lutam para manter
- Pode obscurecer os padrões do nível subsidiário quando visualizados somente no nível global
- Esforço adicional de modelagem de dados para estabelecer e manter relações de hierarquia

**Experience League:**

- [Visão geral do CJA B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

### Opção C: Pessoa híbrida + análise de conta

**Recomendado para:** organizações que estão fazendo a transição de análises baseadas em pessoas para análises baseadas em contas, ou para aquelas que precisam de visualizações de nível de pessoa e nível de conta. Essa abordagem cria duas visualizações de dados da mesma conexão — uma centrada em pessoas e outra centrada em contas.

**Como funciona:**

Configure uma única conexão B2B [!DNL CJA] que inclua todos os conjuntos de dados B2B (evento, conta, oportunidade, grupo de compras, relações pessoa-conta). Em seguida, crie duas visualizações de dados: uma usando Pessoa como o contêiner principal (semelhante ao padrão [!DNL CJA]) e outra usando Conta como o contêiner principal. Os analistas podem alternar entre visualizações de dados dependendo da pergunta que está sendo feita.

A visualização de dados centrada em pessoas fornece análise de jornada tradicional em nível individual (por exemplo, &quot;Qual é o caminho de conversão para clientes potenciais que se tornam oportunidades?&quot;), enquanto a visualização de dados centrada em contas fornece análise em nível de organização (por exemplo, &quot;Quais contas têm a maior taxa de conversão de envolvimento para pipeline?&quot;). Ambas as exibições usam os mesmos dados subjacentes, garantindo a consistência.

**Principais considerações:**

- Requer duas visualizações de dados com configurações de dimensão e métrica possivelmente diferentes
- Os analistas precisam de treinamento sobre quando usar cada visualização
- As métricas calculadas podem precisar ser criadas separadamente para cada visualização de dados

**Vantagens:**

- Fornece flexibilidade para analisar dados no nível da pessoa e da conta
- Caminho de adoção mais fácil para equipes acostumadas à análise no nível da pessoa
- Permite a comparação entre métricas de nível de pessoa e nível de conta
- Suporta estratégias de marketing baseadas em leads e em contas

**Limitações:**

- Duas visualizações de dados para manter e manter em sincronia
- Possível confusão de analistas sobre qual visualização usar
- Métricas e filtros computados podem precisar de duplicação entre visualizações

**Experience League:**

- [Criar ou editar uma visualização de dados](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Visão geral das visualizações de dados](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/data-views)

### Comparação de opções

| Critérios | Opção A: centrada em conta | Opção B: centrada em conta global | Opção C: Pessoa híbrida + conta |
| --- | --- | --- | --- |
| Melhor para | B2B padrão com estrutura de conta simples | Empresa com hierarquias pai-filho | Organizações em transição ou necessidades duplas |
| Complexo | Médio | Alta | Medium-Alto |
| Requisitos de dados | Mapeamento de conta-pessoa | Hierarquia de conta + mapeamento | Mapeamento de conta-pessoa |
| Escopo da atribuição | Nível da conta (retrospectiva de 13 meses) | Nível de conta global (retrospectiva de 13 meses) | Nível da pessoa e da conta |
| Dados anônimos | Excluído da exibição de conta | Excluído da exibição global | Incluído na exibição pessoal, excluído da exibição conta |
| Exige | [!DNL RT-CDP] B2B edition, [!DNL CJA] B2B edition | [!DNL RT-CDP] B2B edition, [!DNL CJA] B2B edition, dados de hierarquia | [!DNL RT-CDP] B2B edition, [!DNL CJA] B2B edition |
| Esforço de manutenção | Visualização de dados única | Visualização de dados única | Duas visualizações de dados |

### Escolha a opção certa

- **Escolha a Opção A** se a sua organização tiver uma estrutura de conta simples (sem hierarquias pai-filho), a sua estratégia ABM funcionará no nível de conta individual e você desejará o caminho mais simples para a análise no nível de conta.
- **Escolha a Opção B** se as contas de destino forem grandes empresas com contas subsidiárias entre regiões ou divisões e você precisar de relatórios consolidados no nível pai corporativo. Essa opção requer dados de hierarquia de conta de alta qualidade.
- **Escolha a Opção C** se sua organização estiver fazendo a transição do marketing baseado em cliente potencial para o baseado em conta, seus analistas precisarão da análise de funnel no nível da pessoa e da análise de envolvimento no nível da conta, ou você terá uma combinação de linhas de negócios B2B e B2C.

## Fases de implementação

As fases a seguir descrevem a sequência de implementação recomendada.

### Fase 1: Conexão de dados B2B

**Função de aplicativo:** [!DNL CJA] B2B: Conexão Baseada em Conta, [!DNL CJA]: Conexão de Dados

Configure a conexão [!DNL CJA] que associa seus conjuntos de dados B2B do AEP a [!DNL CJA] para análise. Essa conexão define quais conjuntos de dados fluem para [!DNL CJA], o tipo de identificador principal (Conta ou Conta Global) e como os dados históricos e de transmissão são assimilados. A conexão é a base de todas as análises subsequentes.

#### Decisão: tipo de identificador principal

Determine se a conexão deve usar a ID de conta ou a ID de conta global como o identificador principal.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| ID da Conta | Estrutura de conta simples, sem hierarquias pai-filho | Configuração mais simples; cada conta é analisada independentemente. Opção mais comum para B2B focado em SMB. |
| ID da conta global | Contas empresariais com hierarquias subsidiárias | Requer dados de hierarquia; agrega todas as subsidiárias no pai. Melhor para os programas ABM empresariais. |

#### Decisão: seleção do conjunto de dados e designação do tipo

Determine quais conjuntos de dados B2B devem ser incluídos e como cada um deve ser digitado.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Conjuntos de dados de evento (comportamental) | Sempre incluir | Interações na Web, eventos de email, envios de formulários, downloads de conteúdo. Deve ter um campo de carimbo de data e hora. Estes são os sinais de engajamento. |
| Conjuntos de dados de registros de conta (perfil) | Sempre incluir | Atributos da conta como setor, tamanho, nível, proprietário. Fornece o contexto dimensional para a análise de conta. |
| Conjuntos de dados de oportunidade (pesquisa/perfil) | Incluir para análise de pipeline | Estágio da oportunidade, valor, data de fechamento. Necessário para análise de pipeline e atribuição de receita. |
| Conjuntos de dados do grupo de compras (pesquisa/perfil) | Incluir para análise de grupo de compras | Comprar funções de grupo, pontuações de engajamento, integridade. Necessário para análise de composição de grupo de compras. |
| Conjuntos de dados de relação pessoa-conta (pesquisa) | Sempre incluir | Mapeia pessoas para contas. Crítico para associar eventos de nível de pessoa à análise de nível de conta. |
| Conjuntos de dados de campanha/programa (pesquisa) | Incluir para atribuição | Metadados de campanha, tipos de programas, canais. Habilita a análise de influência da campanha. |

#### Decisão: intervalo de preenchimento retroativo

Determine quantos dados históricos devem ser importados para a conexão.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Todos os dados existentes | Os ciclos de vendas B2B são longos (6 a 18 meses) e você precisa de um histórico completo | Recomendado para B2B. O preenchimento retroativo pode levar dias para grandes conjuntos de dados, mas fornece dados de atribuição completos. |
| Intervalo de datas personalizado (últimos 2-3 anos) | A qualidade dos dados é degradada além de um determinado ponto | Equilibra integridade com qualidade dos dados. Comum quando os dados do CRM têm inconsistências históricas. |
| Sem preenchimento retroativo | Somente teste ou desenvolvimento | Somente os novos dados fluem no. Não adequado para análises B2B de produção. |

#### Configurar a conexão de dados B2B

**Navegação da interface do usuário:** [!DNL Customer Journey Analytics] > Conexões > Criar nova conexão

Principais detalhes de configuração:

- Selecione a sandbox do AEP que contém conjuntos de dados B2B
- Definir o número médio de eventos diários para planejamento de capacidade
- Adicionar cada conjunto de dados e designar seu tipo (evento, pesquisa ou perfil)
- Configure o campo ID de pessoa para usar a ID de conta ou a ID de conta global para conexões B2B
- Ative a transmissão para conjuntos de dados que exigem atualizações em tempo quase real
- Habilitar &quot;Importar todos os dados existentes&quot; para preenchimento retroativo histórico

**Onde as opções divergem:**

**Para Opção A (Centrada Em Conta):**
Defina o identificador principal como Account ID. Adicionar conjunto de dados de registro de conta, oportunidade, grupo de compras e relação pessoa-conta. Configure conjuntos de dados de evento de nível de pessoa com o campo ID da conta para associação entre conjuntos de dados.

**Para Opção B (Centrada Em Conta Global):**
Defina o identificador principal como Global Account ID. Verifique se os dados da hierarquia da conta incluem o campo ID da conta global. Todos os conjuntos de dados devem incluir ou poder ser associados à ID de conta global para o acúmulo adequado.

**Para Opção C (Híbrida):**
Crie uma única conexão com todos os conjuntos de dados B2B. Use a ID da conta como o identificador principal. A visualização centrada em pessoas será criada na Fase 2 usando uma configuração de visualização de dados diferente na mesma conexão.

**Documentação do Experience League:**

- [Visão geral das conexões](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-connections/overview)
- [Criar ou editar uma conexão](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-connections/create-connection)
- [Gerenciar conexões](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-connections/manage-connections)
- [Visão geral do CJA B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

### Fase 2: configuração da visualização de dados da conta

**Função de aplicativo:** [!DNL CJA] B2B: Configuração de Exibição de Dados B2B, [!DNL CJA]: Configuração de Exibição de Dados

Configure a visualização de dados que define como os dados da conexão aparecem na análise. Para a análise B2B, isso inclui configurar contêineres específicos para B2B (Conta, Oportunidade, Grupo de compra), mapear campos de esquema B2B para dimensões e métricas, definir modelos de atribuição com janelas de pesquisa apropriadas para B2B e criar campos derivados para a lógica de negócios B2B.

#### Decisão: configuração do contêiner

Determine quais contêineres B2B devem ser ativados e como eles devem ser nomeados.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Conta + Pessoa + Sessão + Evento | B2B padrão sem análise de grupo de compra ou oportunidade | Hierarquia de contêiner B2B mais simples. A conta é o contêiner de nível superior. |
| Conta + Oportunidade + Pessoa + Sessão + Evento | Análise de pipeline e receita necessária | Adiciona a oportunidade como um nível de contêiner, permitindo a análise no escopo da oportunidade. |
| Conta + Grupo de compras + Oportunidade + Pessoa + Sessão + Evento | Análise B2B completa, incluindo a composição do grupo de compra | Mais abrangente. Permite a análise em todos os níveis do modelo de dados B2B. |
| Conta global + Conta + Pessoa + Sessão + Evento | Análise de hierarquia de conta global | Adiciona Conta global como o contêiner de nível mais alto acima de Conta. |

#### Decisão: modelo de atribuição para métricas B2B

Determine qual modelo de atribuição deve ser o padrão para métricas de conversão.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Atribuição linear (retrospectiva de 13 meses) | Crédito igual a todos os pontos de contato na jornada B2B | Melhor para entender a combinação completa de atividades de marketing. Ponto de partida recomendado para B2B. |
| Atribuição em forma de U (retrospectiva de 13 meses) | Ênfase no primeiro e último contato com crédito para contatos intermediários | Destaca a criação de clientes potenciais e os momentos de conversão da oportunidade. Comum na análise de geração de demanda. |
| Declínio de tempo (retrospectiva de 13 meses) | Pontos de contato mais recentes devem receber mais crédito | Melhor quando a recenticidade do contrato é um sinal importante para a disponibilidade das vendas. |
| Último contato | Relatório simples do ponto de contato final antes da conversão | Fácil de entender, mas subestima o marketing em estágio inicial. Use apenas para relatórios operacionais rápidos. |

#### Decisão: definição de sessão para B2B

Determine como as sessões devem ser definidas para o envolvimento B2B.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Tempo limite de 30 minutos (padrão) | Comportamento padrão da sessão do Web Analytics | Padrão para análise de envolvimento da Web. Pode fragmentar longas sessões de consumo de conteúdo. |
| Tempo limite estendido (60-120 minutos) | Os usuários B2B se envolvem em sessões de pesquisa mais longas | Os compradores B2B geralmente gastam um tempo estendido revisando conteúdo técnico, preços e documentação. |
| Nova sessão baseada em eventos | Eventos específicos devem sempre iniciar uma nova sessão | Use quando click-throughs ou solicitações de demonstração da campanha precisarem sempre iniciar uma nova sessão analítica. |

#### Configurar a visualização de dados da conta

**Navegação da interface do usuário:** [!DNL Customer Journey Analytics] > Visualizações de dados > Criar nova visualização de dados

Principais detalhes de configuração:

- Selecione a conexão criada na Fase 1
- Configurar fuso horário e tipo de calendário apropriados para a organização
- Renomear contêineres para a terminologia relevante para B2B (por exemplo, Conta/Envolvimento/Ponto de contato)
- Mapear campos de esquema B2B para dimensões: nome da conta, ID da conta, setor, tamanho da empresa, camada da conta, proprietário da conta, estágio da oportunidade, valor da oportunidade, função do grupo de compras, interesse da solução
- Mapear métricas de engajamento: eventos (ocorrências), pessoas, sessões, exibições de página, envios de formulários, aberturas de email, cliques de email
- Configure a persistência para dimensões principais (por exemplo, o setor de conta persiste no nível de conta)
- Definir atribuição como linear com retrospectiva de 13 meses como padrão para métricas de conversão
- Criar campos derivados para classificação de canal de marketing, níveis de pontuação de engajamento e agrupamento de estágio de oportunidade

**Onde as opções divergem:**

**Para Opção A (Centrada Em Conta):**
Configure uma única visualização de dados com Conta como o contêiner de nível superior. Inclua contêineres de Oportunidade e Grupo de compra se a análise de pipeline e grupo de compra for necessária.

**Para Opção B (Centrada Em Conta Global):**
Configure a Conta global como o contêiner de nível superior. Inclua Conta como um subcontêiner para ativar a análise global e subsidiária.

**Para Opção C (Híbrida):**
Crie duas visualizações de dados da mesma conexão. A Visualização de dados 1 usa Pessoa como o contêiner principal (comportamento padrão [!DNL CJA]). A Visualização de dados 2 usa Conta como o contêiner principal com contêineres B2B. Mapeie métricas idênticas para ambas as exibições, quando aplicável.

**Documentação do Experience League:**

- [Visão geral das visualizações de dados](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/data-views)
- [Criar ou editar uma visualização de dados](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Visão geral das configurações de componente](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [Configurações de persistência](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [Configurações de atribuição](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [Campos derivados](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/derived-fields)
- [Configurações da sessão](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/session-settings)

### Fase 3: análise do Workspace

**Função do aplicativo:** [!DNL CJA] B2B: Análise Workspace no Nível da Conta, Análise de Grupo de Compra, Análise de Oportunidade, Segmentação B2B, Atribuição B2B, [!DNL CJA]: Análise Workspace, Criação de Métrica Computada, Análise Guiada

Crie projetos do espaço de trabalho que forneçam os insights analíticos definidos nos KPIs. Essa fase inclui a criação de tabelas de forma livre com dimensões e métricas B2B, a criação de métricas calculadas para KPIs B2B, a configuração de visualizações específicas para B2B (fluxo no nível da conta, funnel de oportunidade, envolvimento de grupo de compra), a criação de filtros/segmentos usando contêineres B2B e a aplicação de modelos de atribuição B2B.

#### Decisão: estrutura do Analysis Workspace

Determine como o projeto do Workspace deve ser organizado.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Um único projeto abrangente com vários painéis | Pequena equipe, todas as partes interessadas visualizam os mesmos relatórios | Mais fácil de manter. Use painéis para separar tópicos (envolvimento, pipeline, atribuição). Até 40 painéis por projeto. |
| Vários projetos focados por público-alvo | Partes interessadas diferentes precisam de visualizações diferentes | O marketing obtém engajamento/atribuição. As vendas obtêm integridade do pipeline/conta. As operações obtêm qualidade dos dados. Mais manutenção, mas mais direcionada. |
| Projetos baseados em modelo com análise guiada | Análise de autoatendimento para usuários não especialistas | Use a análise guiada para funnel e exibições de tendências. Salve como modelos para análise repetível. Melhor para ampla adoção. |

#### Decisão: métricas calculadas B2B

Determine quais métricas calculadas são necessárias para KPIs B2B.

| Métrica | Fórmula | Quando criar |
| --- | --- | --- |
| Taxa de participação da conta | (Total de eventos de conta / Total de contas) | Sempre — métrica B2B principal |
| % de Integridade do Grupo de Compras | (Funções Preenchidas / Funções Necessárias) * 100 | Quando a análise de grupo de compras está no escopo |
| Conversão de conta em oportunidade | Contas com Oportunidades / Contas Engajadas | Quando a análise de pipeline é necessária |
| % de influência do pipeline | Valor do pipeline influenciado/Valor total do pipeline | Quando a atribuição de marketing é obrigatória |
| Envolvimento médio por contato | Eventos / Pessoas únicas por conta | Quando a análise de inserção de conta é necessária |
| Engajamento de conteúdo por função | Eventos filtrados por função de grupo de compra | Quando a otimização de conteúdo para B2B é necessária |

#### Decisão: escopo do filtro/segmento B2B

Determine em qual nível de contêiner os filtros devem ser criados.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Filtros de nível de conta | Análise segmentada para critérios de correspondência de contas (por exemplo, contas corporativas, setores específicos) | Inclui todos os eventos de contas qualificadas. Mais comum para B2B. |
| Filtros de nível de oportunidade | Análise com escopo para tipos ou estágios de oportunidade específicos | Inclui todos os eventos associados a oportunidades de qualificação. |
| Comprar filtros de nível de grupo | Análise com escopo para estados específicos do grupo de compras | Inclui eventos de pessoas em grupos de compras qualificados. |
| Filtros de nível de pessoa | Análise segmentada para critérios de correspondência individuais (por exemplo, funções específicas, títulos) | Comportamento de filtro padrão. Use ao analisar o envolvimento individual no contexto B2B. |

#### Criar a análise do espaço de trabalho

Navegação da **UI:** [!DNL Customer Journey Analytics] > Workspace > Projetos > Criar projeto

Principais detalhes de configuração:

- Selecione a visualização de dados B2B criada na Fase 2
- Criar tabelas de forma livre com dimensões no nível da conta (nome da conta, setor, nível) detalhadas pelas métricas de envolvimento
- Criar visualizações do funnel de oportunidades que mostram a progressão da oportunidade em estágios
- Criar tabelas de composição de grupos de compras mostrando taxas de preenchimento de função e envolvimento por função
- Configurar painéis de atribuição B2B comparando modelos de atribuição (linear, forma de U, declínio de tempo) com retrospectiva de 13 meses
- Criar visualizações de fluxo de conta mostrando caminhos comuns por meio da jornada de compra
- Criar tabelas de coorte analisando a retenção e o reengajamento da conta ao longo do tempo
- Aplicar filtros B2B à análise de segmentos por nível de conta, setor ou nível de envolvimento
- Criar anotações para eventos significativos (lançamentos de campanha, lançamentos de produtos, alterações de preço)

**Documentação do Experience League:**

- [Visão geral do Workspace](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/home)
- [Criar um projeto](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [Tabela de forma livre](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [Painel de atribuição](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [Visualização de fluxo](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [Visualização Fallout](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [Tabela de coorte](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [Visão geral dos filtros](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [Visão geral das métricas calculadas](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [Criar métricas calculadas](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [Visão geral de anotações](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/annotations/overview)
- [Visão geral da análise guiada](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/guided-analysis/overview)
- [Detalhamento de dimensões](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)

### Fase 4: publicação do painel

**Função do aplicativo:** [!DNL CJA]: Publicação de Painel e Scorecard, [!DNL CJA]: Publicação de Público-Alvo

Crie painéis compartilháveis e cartões de pontuação móveis que fornecem insights de análise B2B às partes interessadas. Essa fase também abrange a publicação de públicos-alvo B2B definidos pelo [!DNL CJA] de volta ao AEP para ativação em casos de uso downstream, como ativação de públicos-alvo B2B.

#### Decisão: método de delivery do painel

Determine como os insights de análise B2B devem ser fornecidos às partes interessadas.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Projeto do Workspace (desktop) | Analistas e operações de marketing que precisam de exploração interativa | Interatividade completa, detalhamento, alternância de filtro. Requer acesso de [!DNL CJA]. |
| Cartão de pontuação para dispositivo móvel | Executivos e líderes de vendas que precisam de KPIs instantâneos | Números de resumo com linhas de tendência. Acessível através do aplicativo de painéis [!DNL Adobe Analytics]. Interatividade limitada. |
| Exportação programada de PDF/CSV | Partes interessadas sem acesso ao [!DNL CJA] que precisam de atualizações regulares | Entrega automatizada de acordo com um agendamento. Sem interatividade. Melhor para resumos executivos semanais/mensais. |
| Todas as anteriores | Grandes organizações com diversas necessidades das partes interessadas | Alcance máximo Maior esforço de manutenção. Recomendado para programas de análise B2B maduros. |

#### Decisão: publicação de público-alvo de [!DNL CJA]

Determine se os segmentos B2B devem ser publicados de volta no AEP para ativação.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Publicar públicos com base na conta | Os insights do Analytics devem informar sobre direcionamento e supressão | Habilita a ativação de segmentos definidos pelo [!DNL CJA] (por exemplo, &quot;contas altamente engajadas sem oportunidades abertas&quot;) via [!DNL RT-CDP]. Cadência de atualização: de 4 horas a semanais. |
| Não publicar | O Analytics é somente para relatórios, não para ativação | Configuração mais simples. Ativação tratada separadamente em [!DNL RT-CDP]. |

#### Publicar painéis e públicos

Navegação da **IU:** [!DNL Customer Journey Analytics] > Projetos > Compartilhar (para o Workspace), Projetos > Criar > Cartão de pontuação móvel (para cartões de pontuação), Componentes > Públicos > Publicar (para publicação de público)

Principais detalhes de configuração:

- Crie painéis de executivos com números de resumo para os principais KPIs B2B (total de contas envolvidas, valor do pipeline, integridade do grupo de compra)
- Configurar períodos de comparação (mês a mês, trimestre a trimestre) para indicadores de tendência
- Crie cartões de pontuação móveis com blocos para envolvimento da conta, integridade do pipeline e métricas de atribuição
- Adicione filtros para executivos para alternar exibições por região, setor ou nível de conta
- Configurar a entrega programada do projeto para relatórios executivos semanais
- Para publicação de público-alvo: selecione o filtro B2B, configure o namespace de identidade (ID da conta) e defina a cadência de atualização

**Documentação do Experience League:**

- [Criar um cartão de pontuação para dispositivos móveis](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [Compartilhar projetos](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [Agendar projetos](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [Configurar e preparar cartões de pontuação](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Painéis do Adobe Analytics — guia executivo](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dashboards/set-up-execs)
- [Visão geral dos públicos](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [Criar e publicar públicos-alvo](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/audiences/publish)

## Considerações de implantação

As seções a seguir abordam medidas de proteção, armadilhas comuns, práticas recomendadas e decisões de compensação que devem ser consideradas durante a implementação.

### Medidas de proteção e limites

- [!DNL CJA] conexões podem incluir conjuntos de dados de apenas uma sandbox da AEP — [medidas de proteção da CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-admin/guardrails)
- Máximo de 5.000 dimensões e 5.000 métricas por visualização de dados
- Máximo de 100 campos derivados por visualização de dados
- A atribuição B2B suporta janelas de pesquisa de até 13 meses para análise em nível de conta
- Máximo de 75 públicos-alvo publicados por [!DNL CJA] cliente em todas as sandboxes
- A cadência mínima de atualização da publicação de público-alvo é a cada 4 horas
- A latência de transmissão do AEP para [!DNL CJA] geralmente está abaixo de 90 minutos
- As tabelas de forma livre aceitam até 10 detalhamentos de dimensão
- Os cartões de pontuação móveis são compatíveis com até 16 blocos por cartão de pontuação
- Os projetos do Workspace aceitam até 40 painéis por projeto
- O preenchimento retroativo para grandes conjuntos de dados B2B (bilhões de registros) pode levar dias para ser concluído

### Armadilhas comuns

- **Mapeamento incompleto de pessoa para conta:** se não for possível associar eventos de nível de pessoa a uma conta, eles não aparecerão na análise de nível de conta. Certifique-se de que todos os conjuntos de dados do evento incluam um campo que possa ser unido à ID da conta, diretamente ou por meio de um conjunto de dados de pesquisa de relação pessoa-conta. Auditore a porcentagem de eventos com associação de conta ausente antes de criar a análise.
- **Designação incorreta de tipo de conjunto de dados:** conjuntos de dados de pesquisa B2B (oportunidade, grupo de compras, relações entre pessoas e contas) devem ser designados corretamente como tipo de pesquisa ou perfil na conexão [!DNL CJA]. Digitar incorretamente um conjunto de dados de pesquisa como um conjunto de dados de evento produzirá resultados incorretos porque [!DNL CJA] tentará tratar cada registro como um evento com carimbo de data e hora.
- **A janela de atribuição muito curta para B2B:** Usar janelas de atribuição padrão de 30 dias perderá pontos de contato de estágio inicial em jornadas B2B que normalmente abrangem de 6 a 18 meses. Sempre configure janelas de pesquisa de 13 meses para métricas de atribuição B2B.
- **Misturar métricas no nível da conta e no nível da pessoa incorretamente:** contar &quot;pessoas&quot; em uma análise no nível da conta pode induzir em erro. Verifique se as métricas calculadas estão definidas no nível de contêiner apropriado. Uma &quot;taxa de engajamento da conta&quot; deve usar eventos no nível da conta divididos por contas, não por pessoas.
- **Dados obsoletos do grupo de compras:** A composição do grupo de compras e as atribuições de função mudam ao longo do tempo. Se os conjuntos de dados do grupo de compra não forem atualizados regularmente, as métricas de integridade serão imprecisas. Verifique se o sistema de origem ([!DNL Marketo Engage] ou [!DNL AJO] B2B edition) está sincronizando ativamente os dados do grupo de compra.
- **Sobrecarregar um único projeto do espaço de trabalho:** o B2B Analytics abrange engajamento, pipeline, atribuição e grupos de compra. Tentar colocar tudo em um projeto resulta em carregamento lento e navegação confusa. Use vários projetos focados ou painéis claramente rotulados.

### Práticas recomendadas

- Comece com a Opção A (Centrada em conta) mesmo que planeje usar a Opção B (Conta global) posteriormente. A análise centrada em conta é mais simples e valida seu modelo de dados antes de adicionar complexidade de hierarquia.
- Crie um projeto dedicado do espaço de trabalho &quot;Qualidade de dados B2B&quot; que rastreia o percentual de eventos com associação de conta, o número de contas órfãs e as métricas de integridade do grupo de compras. Execute isso semanalmente para detectar problemas de dados antecipadamente.
- Use campos derivados para criar camadas de pontuação de envolvimento (Alta/Medium/Baixa) com base na contagem de eventos no nível da conta. Isso simplifica a análise e torna os painéis mais acionáveis para participantes não técnicos.
- Ao configurar a atribuição B2B, comece com a atribuição linear como uma linha de base e compare com modelos em forma de U e de declínio de tempo. As diferenças entre os modelos geralmente revelam se sua combinação de marketing é ponderada em relação a atividades de percepção ou conversão.
- Publique um cartão de pontuação móvel &quot;Resumo executivo B2B&quot; com até 8 blocos que cubram os KPIs mais importantes para a liderança. Mantenha o foco — os cartões de pontuação executivos devem responder &quot;Como estamos indo?&quot; não &quot;Por quê?&quot;
- Anote os principais eventos (lançamentos de produtos, lançamentos de campanhas importantes, alterações de preços, alterações no processo de vendas) para fornecer contexto para tendências de dados. Os dados B2B geralmente mostram picos e declínios que são inexplicáveis sem o contexto do evento.
- Ao publicar públicos-alvo B2B do [!DNL CJA], use a atualização diária para segmentos de ativação padrão e a atualização de 4 horas somente para segmentos sensíveis ao tempo. Atualizações frequentes consomem recursos de processamento.

### Decisões de compensação

>[!NOTE]
>As seguintes decisões de compensação devem ser avaliadas com base nos requisitos e restrições específicos da organização.

**Integridade de dados vs. precisão analítica**

A inclusão de todos os eventos de nível de pessoa na análise de conta (mesmo aqueles com associação de conta fraca) melhora a integridade dos dados, mas pode reduzir a precisão analítica se o mapeamento de conta não for confiável.

- **A inclusão de todos os eventos favorece:** medição abrangente de engajamento, pontuações mais altas de engajamento na conta, visibilidade mais ampla
- **A exclusão de eventos sem correspondência favorece:** métricas de nível de conta precisas, atribuição confiável, correlação de pipeline confiável
- **Recomendação:** exclua eventos sem correspondência da análise em nível de conta, mas inclua-os em uma visualização de dados em nível de pessoa separada (Opção C) para entender a imagem completa. Priorize a melhoria da qualidade dos dados de associação da conta como um fluxo de trabalho paralelo.

**Comprimento da janela de retrospectiva de atribuição B2B**

Janelas de pesquisa mais longas (13 meses) capturam mais pontos de contato, mas podem incluir atividades de marketing que não são mais relevantes para a decisão de compra atual.

- **A pesquisa mais longa (13 meses) favorece:** Captura da jornada B2B completa, crédito de atividades em estágio de conscientização, acomodando longos ciclos de vendas
- **A pesquisa mais curta (6 meses) favorece:** Foco em envolvimento recente, redução de ruídos de pontos de contato antigos, melhor reflexo da intenção de compra atual
- **Recomendação:** use retrospectiva de 13 meses para contas da empresa com ciclos de vendas longos (mais de 12 meses). Use a retrospectiva de 6 meses para contas de empresas de médio porte com ciclos mais curtos. Crie métricas calculadas separadas para cada janela a ser comparada.

**Uma única visualização de dados abrangente vs. várias visualizações de dados focalizadas**

Uma visualização de dados com todos os contêineres e dimensões B2B é mais simples de manter, mas pode sobrecarregar os analistas com complexidade. Visualizações de dados com foco múltiplo (envolvimento, pipeline, atribuição) são mais fáceis de usar, mas mais difíceis de manter.

- **A exibição única favorece:** Consistência, manutenção mais fácil, análise entre domínios dentro de um único projeto
- **Várias exibições favorecem:** Simplicidade para analistas, tempos de carregamento mais rápidos, listas de componentes personalizadas por caso de uso
- **Recomendação:** comece com uma única visualização de dados abrangente. Se os analistas relatarem dificuldade em encontrar as dimensões e métricas certas, crie grupos de componentes com curadoria na mesma visualização antes de dividir em várias visualizações. Use modelos do espaço de trabalho para orientar analistas para os componentes certos.

## Documentação relacionada

Os recursos a seguir fornecem informações adicionais para implementar esse padrão de caso de uso.

**[!DNL CJA]B2B edition**

- [Visão geral do CJA B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)
- [Visão geral do CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-overview/cja-overview)
- [Medidas de proteção do CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-admin/guardrails)

**Conexões**

- [Visão geral das conexões](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-connections/overview)
- [Criar ou editar uma conexão](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-connections/create-connection)
- [Gerenciar conexões](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-connections/manage-connections)

**Visualizações de dados**

- [Visão geral das visualizações de dados](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/data-views)
- [Criar ou editar uma visualização de dados](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Visão geral das configurações de componente](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [Configurações de persistência](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [Configurações de atribuição](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [Configurações de formato](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/format)
- [Campos derivados](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/derived-fields)
- [Configurações da sessão](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/session-settings)

**Workspace e análise**

- [Visão geral do Workspace](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/home)
- [Criar um projeto](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [Tabela de forma livre](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [Visualização de fluxo](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [Visualização Fallout](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [Tabela de coorte](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [Painel de atribuição](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [Compartilhar projetos](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [Agendar projetos](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [Detalhamento de dimensões](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)

**Componentes**

- [Visão geral dos filtros](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [Criar filtros](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [Visão geral das métricas calculadas](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [Criar métricas calculadas](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [Visão geral de anotações](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/annotations/overview)
- [Intervalos de datas](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)

**Públicos-alvo**

- [Visão geral dos públicos](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [Criar e publicar públicos-alvo](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/audiences/publish)
- [Gerenciar públicos](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-components/audiences/manage)

**Painéis e scorecards**

- [Criar um cartão de pontuação para dispositivos móveis](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [Configurar e preparar cartões de pontuação](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Painéis do Adobe Analytics — guia executivo](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dashboards/set-up-execs)

**Análise guiada**

- [Visão geral da análise guiada](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/guided-analysis/overview)
- [Visualização do funnel](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [Exibição de tendências](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/guided-analysis/trends/usage)
- [Exibição de retenção](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/guided-analysis/retention/retention-rates)

**[!DNL RT-CDP]B2B edition**

- [Visão geral da B2B edition da RT-CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#702702)
- [Esquemas do B2B edition](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/schemas/b2b)
- [Visão geral das fontes B2B](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/sources/b2b)

**AEP data foundation**

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/home)
- [Visão geral das fontes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/home)
- [Conector do Marketo Engage](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/home)
- [Visão geral de sandboxes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/home)

**Governança de dados e ciclo de vida**

- [Visão geral da governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/home)
- [Gerenciamento avançado do ciclo de vida dos dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-lifecycle/home)

**Tutoriais e guias**

- [Noções básicas de composição de esquema](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/schema/composition)
- [Visão geral de atributos computados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/computed-attributes/overview)
- [Visão geral dos Insights de observação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/home)
