---
title: Audience Activation B2B
description: Saiba como ativar públicos-alvo B2B baseados em conta nos canais da Web, de email e de anúncios.
solution: Real-Time Customer Data Platform
exl-id: 2b979159-37aa-41d4-a6b4-1105538f6546
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '7611'
ht-degree: 0%

---

# Ativação de público-alvo B2B

Este guia fornece uma referência de implementação abrangente para ativar públicos B2B baseados em conta usando o B2B edition [!DNL Adobe Real-Time Customer Data Platform] ([!DNL RT-CDP]). Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam criar, avaliar e ativar públicos-alvo no nível da conta em canais da Web, de email, de publicidade e de CRM.

Ele abrange o ciclo de vida completo da unificação do perfil da conta por meio da avaliação e ativação de público-alvo para destinos específicos B2B, como [!DNL Marketo Engage], [!DNL LinkedIn] e sistemas CRM. Todas as abordagens de implementação viáveis são apresentadas com compensações e orientação de decisão para ajudar você a selecionar o caminho certo para sua organização.

## Visão geral do caso de uso

As equipes de marketing B2B precisam direcionar e ativar públicos-alvo no nível da conta em vez do nível da pessoa individual. Diferentemente da ativação de público-alvo B2C, em que a unidade de direcionamento é um único perfil do consumidor, a ativação de público-alvo B2B requer a compreensão da relação entre as pessoas e as contas às quais elas pertencem, avaliando a associação de público-alvo com base em atributos de nível de conta combinados com sinais de envolvimento de nível de pessoa e fornecendo esses públicos-alvo para destinos que oferecem suporte ao direcionamento baseado em conta.

O B2B edition [!DNL RT-CDP] estende o padrão [!DNL Real-Time Customer Data Platform] com classes XDM especializadas para contas, oportunidades e campanhas, juntamente com a resolução de identidade B2B que mapeia relacionamentos entre pessoas e contas. Isso permite que os profissionais de marketing criem públicos-alvo de contas que combinem dados firmográficos (setor, receita, contagem de funcionários), dados tecnológicos (pilha de tecnologia, uso de produtos) e dados comportamentais (visitas da Web, envolvimento de email, presença em eventos) das pessoas associadas a essas contas.

Os públicos ativados da conta potencializam os casos de uso na funnel de geração de demanda: campanhas de conscientização sobre o topo da funnel em [!DNL LinkedIn] e anúncios de exibição, programas de nutrição mid-funnel em [!DNL Marketo Engage] e capacitação de vendas bottom-of-funnel por meio da integração de CRM. Os públicos-alvo de supressão de conta evitam o desperdício, excluindo clientes existentes, contas fechadas/perdidas ou contas que já estão nos ciclos de vendas ativos.

>[!NOTE]
>Se o seu caso de uso envolver a ativação de públicos-alvo no nível da pessoa (B2C) em vez do nível da conta, consulte [Ativação de público-alvo para destinos](audience-activation-to-destinations.md). Esse padrão usa o modelo de dados padrão RT-CDP e não requer o B2B edition.

## Principais objetivos de negócios

Os seguintes objetivos de negócios são compatíveis com esse padrão de caso de uso.

### Aumentar a geração de leads

Gerar clientes potenciais mais qualificados para o pipeline de vendas por meio de formulários, eventos, conteúdo e envolvimento de vários canais.

**KPIs:** Clientes Potenciais, Custo por Cliente Potencial, Conversão de Cliente Potencial

[Saiba mais sobre o aumento da geração de clientes potenciais](/help/blueprints/business-objectives/acquisition-growth/increase-lead-generation.md)

### Melhorar a qualificação e a conversão de clientes potenciais

Aumente a qualidade do lead e acelere a progressão do pipeline por meio de pontuação, estimulação e acompanhamento personalizado.

**KPIs:** Conversão de Cliente Potencial, Conversão de Cliente Potencial/Cliente Potencial, Eficiência

[Saiba mais sobre como melhorar a qualificação e a conversão de clientes potenciais](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

### Adquirir novos clientes

Expanda a base de clientes por meio de campanhas de aquisição direcionadas, públicos semelhantes e otimização de mídia paga.

**KPIs:** Novos Clientes, Custo de Aquisição do Cliente, Conversão de Cliente Potencial/Cliente Potencial

[Saiba mais sobre como adquirir novos clientes](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

### Otimizar os gastos com marketing e o ROI

Melhore o retorno sobre o investimento em marketing através de melhor direcionamento, atribuição, supressão de público-alvo e alocação de orçamento.

**KPIs:** Economia, Custo de Aquisição do Cliente, Receita Incremental

[Saiba mais sobre como otimizar o investimento e o ROI do marketing](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)

## Exemplo de casos de uso tático

Os cenários a seguir ilustram como esse padrão pode ser aplicado na prática.

- **Anúncio baseado em conta no[!DNL LinkedIn]** — Contas do Target que correspondem ao seu perfil de cliente ideal (ICP) com conteúdo patrocinado e campanhas do InMail no [!DNL LinkedIn], usando listas de contas ativadas do [!DNL RT-CDP] B2B edition
- **[!DNL Marketo Engage]direcionamento de programa de aprendizado** — Ative os públicos da conta para [!DNL Marketo Engage] para inscrever clientes potenciais e contatos associados em fluxos de aprendizado direcionados com base nos critérios de qualificação de nível de conta
- **Sincronização de lista de contas do CRM** — envie listas de contas qualificadas para [!DNL Salesforce] ou [!DNL Microsoft Dynamics] para visibilidade de equipe de vendas, atribuição de território e fluxos de trabalho de prospecção de saída
- **Supressão de conta para mídia paga** — Suprima clientes existentes, contas fechadas ou contas em ciclos de vendas ativos de campanhas de aquisição pagas para reduzir gastos desperdiçados
- **Direcionamento de conta baseado em intenção** — Combine sinais de intenção de terceiros com dados de envolvimento primário no nível da conta para identificar e ativar públicos de contas no mercado
- **Venda cruzada de produtos para contas existentes** — crie públicos-alvo de contas usando uma linha de produto, mas não outra, e ative para canais de email e publicidade para campanhas de venda cruzada
- **Direcionamento de eventos e webinários** — ative públicos-alvo da conta para canais de email e publicidade para impulsionar o registro de eventos das contas de destino
- **Campanhas de deslocamento competitivo** — contas do Target usando produtos concorrentes com mensagens personalizadas ativadas por meio de canais de email e publicidade
- **Engajamento de conta em camadas** — Segmente contas em camadas de engajamento (alto, médio, baixo) com base na atividade agregada em nível de pessoa e ative campanhas diferenciadas para cada camada
- **Públicos-alvo de co-marketing de parceiros** — compartilhe segmentos de público-alvo de conta com parceiros de canal ou programas de co-marketing por meio de destinos de armazenamento na nuvem

## Indicadores-chave de desempenho

Os KPIs a seguir ajudam a medir o sucesso desse padrão de caso de uso.

| KPI | Descrição | Abordagem de medição |
| --- | --- | --- |
| Alcance da conta | Número de contas de destino atingidas nos canais de ativação | Rastrear contas exclusivas ativadas por destino |
| Taxa de participação da conta | Porcentagem de contas ativadas que mostram sinais de envolvimento | Meça o envolvimento de nível de pessoa agregado à conta |
| Influência do pipeline | Pipeline de receita atribuído às campanhas de ativação baseadas em conta | Rastrear oportunidades criadas por meio de públicos ativados da conta |
| Custo por conta envolvida | Gasto de marketing dividido pelo número de contas que mostram engajamento | Calcule os custos entre canais de publicidade e de email |
| Índice de conversão de leads | Porcentagem de clientes potenciais de contas ativadas que são convertidas em oportunidades | Rastrear a conversão do lead em oportunidade para públicos ativados |
| Economia de supressão de público-alvo | Custo evitado ao suprimir contas inelegíveis de campanhas pagas | Medir a redução de gastos dos públicos-alvo de supressão |
| Cobertura da conta | Porcentagem do mercado endereçável total (TAM) coberto por públicos ativados | Comparar contas ativadas com o universo ICP total |

## Padrão do caso de uso

**Ativação de público B2B**

Ative públicos-alvo B2B baseados em conta nos canais da Web, de email e de publicidade.

**Cadeia de funções:** Enriquecimento de Perfil de Conta > Avaliação de Público de Conta > Configuração de Destino > Audience Activation > Monitoramento

## Aplicativos

Os aplicativos a seguir são usados para implementar esse padrão de caso de uso.

- **[!DNL Real-Time CDP]B2B edition** — Plataforma principal para unificação de perfil de conta, resolução de identidade B2B, avaliação de público-alvo de conta, configuração de destino específica para B2B e ativação de público-alvo de conta
- **[!DNL Adobe Experience Platform](AEP)** — Infraestrutura básica para modelagem de dados XDM B2B, assimilação de dados do CRM e fontes de automação de marketing, serviço de identidade e governança
- **[!DNL Marketo Engage]** — Destino principal de automação de marketing B2B para programas de criação de clientes potenciais, pontuação e execução de campanha alimentados por públicos-alvo de contas ativadas

## Funções básicas

Os seguintes recursos básicos devem estar em vigor para esse padrão de caso de uso. Para cada função, o status indica se ele é tipicamente necessário, se presume ser pré-configurado ou se não é aplicável.

| Função de base | Status | O que deve estar em vigor | Referência do Experience League |
| --- | --- | --- | --- |
| Administração e governança | Obrigatório | Sandbox provisionada com o [!DNL RT-CDP] B2B edition habilitado. Funções configuradas para gerenciamento de dados B2B, criação de público-alvo e ativação de destino. Políticas ABAC em vigor se os dados da conta contiverem campos restritos. | [Visão geral das sandboxes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/home), [Visão geral do controle de acesso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Preparação e modelagem de dados | Obrigatório | Esquemas XDM B2B configurados usando as classes Conta de negócios XDM, Oportunidade de negócios XDM, Campanha de negócios XDM e Perfil individual XDM. Grupos de campos B2B aplicados para atributos de conta, relacionamentos entre pessoas e contas e dados de oportunidade. Conjuntos de dados criados e habilitados para perfil para cada entidade B2B. Relacionamentos de esquema definidos entre entidades de conta, pessoa, oportunidade e campanha. | [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [esquemas B2B no Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b) |
| Fontes de dados e coleção | Obrigatório | Conectores do Source configurados para CRM ([!DNL Salesforce], [!DNL Microsoft Dynamics]) e automação de marketing ([!DNL Marketo Engage]) para assimilar dados de conta, pessoa, oportunidade e campanha. Pipelines de assimilação em lote ou por transmissão ativos. Mapeamentos de Preparo de dados configurados para transformar dados de origem em esquemas XDM B2B. | [Visão geral das fontes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home), [Conector do Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) |
| Configuração de identidade e perfil | Obrigatório | Namespaces de identidade B2B configurados para identificadores de conta (ID de conta, ID de conta do CRM) e identificadores de pessoa (Email, ID de contato do CRM, ID de lead da Marketo). Relacionamentos entre pessoa e conta resolvidos por meio da resolução de identidade B2B. Políticas de mesclagem configuradas para unificação de perfil de conta. | [Visão geral do Serviço de Identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [B2B edition da Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#rtcdp-b2b) |
| Definição e segmentação do público-alvo | Obrigatório | Definições de público-alvo no nível da conta criadas usando atributos de conta, atributos de pessoa e dados de atividade. Agendamentos de avaliação configurados para públicos-alvo da conta. Públicos-alvo de supressão definidos para excluir contas não qualificadas. | [Visão geral do Serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [Públicos-alvo da conta](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences) |

## Funções de suporte

Os recursos a seguir aumentam esse padrão de caso de uso, mas não são necessários para a execução principal.

| Função de suporte | Status | Por que é importante | Referência do Experience League |
| --- | --- | --- | --- |
| Criação de atributo calculado/derivado | Recomendado | Pontuações de engajamento agregadas, valor vitalício e métricas de atividade no nível da conta melhoram a precisão do público-alvo. Os atributos computados podem acumular eventos de nível de pessoa (aberturas de email, visitas da Web, downloads de conteúdo) no nível de conta para uso na segmentação. | [Visão geral dos atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Gerenciamento do ciclo de vida dos dados | Recomendado | As políticas de retenção de dados B2B garantem que os dados obsoletos da conta e da oportunidade sejam apagados. O gerenciamento de consentimento para contatos B2B garante a conformidade com as regulamentações de marketing por email. As políticas de expiração do conjunto de dados impedem o acúmulo de dados desatualizados de sincronização de CRM. | [Visão geral do Gerenciamento Avançado do Ciclo de Vida dos Dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| Rotulagem e aplicação de uso de dados | Incluído | Os dados da conta B2B geralmente contêm restrições contratuais (valores de receita, contagens de funcionários de provedores de terceiros). Os rótulos de uso de dados impedem que atributos de conta restritos sejam ativados para destinos não autorizados. As políticas de governança garantem que os campos de PII dos registros de contato sejam manipulados adequadamente durante a ativação. | [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| Monitoramento e capacidade de observação | Incluído | O monitoramento do CRM e dos fluxos de dados do conector de origem [!DNL Marketo Engage] garante que os dados da conta permaneçam atualizados. O monitoramento de ativação de destino confirma que os públicos-alvo foram entregues com êxito para [!DNL LinkedIn], [!DNL Marketo] e destinos de CRM. As regras de alerta capturam falhas de assimilação que causariam dados de conta obsoletos. | [Visão geral dos alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview), [Monitorar fluxos de dados de destino](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations) |
| Relatórios e análise | Recomendado | O B2B edition [!DNL CJA] fornece análises a nível de conta, incluindo alcance de público, envolvimento e influência do pipeline. A atribuição baseada em conta ajuda a medir o impacto das campanhas de ativação na progressão da oportunidade e na receita. | [visão geral do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## Funções do aplicativo

Este plano exerce as seguintes funções do Catálogo de Funções da Aplicação. As funções são mapeadas para fases de implementação em vez de etapas numeradas.

### [!DNL Real-Time CDP] B2B edition ([!DNL RT-CDP] B2B)

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Unificação de perfil da conta | Fase 1: Enriquecimento do perfil da conta | Consolidar dados de conta de CRM, automação de marketing e fontes de terceiros em perfis de conta unificados usando classes de esquema XDM B2B |
| Resolução de identidade B2B | Fase 1: Enriquecimento do perfil da conta | Resolver relacionamentos entre pessoas e contas usando identificadores principais, mapeando contatos e leads para suas contas associadas |
| Avaliação de público-alvo da conta | Fase 2: Avaliação de público-alvo da conta | Avaliar a associação de segmento no nível da conta combinando atributos da conta, atributos da pessoa e dados de atividade da pessoa |
| Configuração de destino da conta | Fase 3: configuração de destino | Configurar conexões para destinos específicos B2B ([!DNL Marketo Engage], [!DNL LinkedIn], CRM, armazenamento na nuvem) com mapeamento de campo no nível da conta |
| Audience Activation da conta | Fase 4: Audience Activation | Publicar públicos-alvo baseados em conta nos destinos configurados para direcionamento, supressão ou sincronização de CRM |
| Integração do [!DNL Marketo Engage] | Fase 3: configuração de destino | Configurar fluxo de dados bidirecional com [!DNL Marketo Engage] usando conectores de origem e destino B2B nativos |
| Governança de dados B2B | Fase 5: governança e monitoramento | Imponha políticas e consentimento de uso de dados na ativação de dados da conta B2B para impedir a exposição de dados não autorizados |

### [!DNL Real-Time CDP] ([!DNL RT-CDP]) — funções padrão

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Avaliação de público | Fase 2: Avaliação de público-alvo da conta | Mecanismo de avaliação subjacente para públicos-alvo da conta, que suporta a avaliação em lote das definições de segmento no nível da conta |
| Configuração de destino | Fase 3: configuração de destino | Infraestrutura de conexão de destino principal usada pela configuração de destino específica de B2B |
| Audience Activation | Fase 4: Audience Activation | Infraestrutura de fluxo de dados de ativação principal usada pela ativação de público-alvo da conta |
| Consentimento e aplicação de governança | Fase 5: governança e monitoramento | Aplicar preferências de consentimento e políticas de uso de dados no momento da ativação |

## Pré-requisitos

Conclua o seguinte antes de iniciar a implementação.

- [ ] [!DNL RT-CDP] licença do B2B edition provisionada e ativada na organização
- [ ] sistema do CRM ([!DNL Salesforce] ou [!DNL Microsoft Dynamics]) acessível com credenciais de API para configuração do conector de origem
- [ Instância ] [!DNL Marketo Engage] provisionada com acesso à API (Munchkin ID, ID do cliente, Segredo do cliente) se estiver usando [!DNL Marketo] como destino
- [ ] [!DNL LinkedIn] Conta de gerente do Campaign com capacidade de públicos correspondentes se estiver usando [!DNL LinkedIn] como destino
- [ ] esquemas XDM B2B criados com classes de conta, pessoa, oportunidade e campanha (F2)
- [ ] conectores do Source configurados e assimilando ativamente dados de automação de marketing e CRM (F3)
- [ ] Relações de identidade entre pessoas e conta resolvidas e perfis de conta unificados (F4)
- [ ] Convenções de nomenclatura de conta e taxonomia acordadas para definições de público-alvo
- [ ] Políticas de governança de dados definidas para classificações de confidencialidade de dados no nível da conta

## Opções de implementação

As opções a seguir descrevem diferentes abordagens para implementar esse padrão de caso de uso. Revise cada opção e selecione aquela que melhor atenda às suas necessidades.

### Opção A: Ativação de público-alvo de transmissão para [!DNL Marketo Engage]

**Recomendado para:** Organizações que usam [!DNL Marketo Engage] como sua principal plataforma de automação de marketing B2B, precisam de atualizações de associação de público quase em tempo real para acionar programas de criação, atualizar pontuações de cliente potencial ou modificar associação à campanha à medida que as contas são qualificadas ou desqualificadas.

**Como funciona:**

Esta opção usa o conector de destino [!DNL Marketo Engage] nativo em [!DNL RT-CDP] para transmitir as alterações de associação de público da conta diretamente para [!DNL Marketo Engage]. Quando uma conta é qualificada ou sai de um segmento de público-alvo, os clientes em potencial e contatos associados em [!DNL Marketo] são atualizados com atributos de associação de segmento. [!DNL Marketo] as campanhas inteligentes podem ser acionadas com base nessas alterações de associação.

O destino [!DNL Marketo Engage] é um destino de streaming, o que significa que as alterações na associação de público serão enviadas de forma incremental à medida que ocorrerem, em vez de em lotes agendados. Isso proporciona um tempo de ação mais rápido para campanhas que precisam responder a alterações de qualificação de conta. Os mapeamentos de campos conectam atributos de perfil [!DNL RT-CDP] a [!DNL Marketo] campos de cliente potencial/contato, permitindo o enriquecimento de [!DNL Marketo] registros com dados de nível de conta de [!DNL RT-CDP].

**Principais considerações:**

- Requer assinatura ativa do [!DNL Marketo Engage] com acesso à API
- A ativação de transmissão envia atualizações incrementais, não instantâneos completos do público-alvo
- Os registros de nível de pessoa em [!DNL Marketo] são atualizados, não os registros de nível de conta diretamente
- [!DNL Marketo] campanhas inteligentes devem ser configuradas para atuar nas atualizações do campo de associação do segmento

**Vantagens:**

- Atualizações de associação de público-alvo em tempo quase real no [!DNL Marketo]
- O conector bidirecional nativo simplifica a integração
- Atualizações incrementais minimizam volume de transferência de dados
- [!DNL Marketo] pode acionar imediatamente programas de criação com base em alterações de público

**Limitações:**

- Limitado a [!DNL Marketo Engage] como destino de ativação
- As restrições de qualificação de avaliação de transmissão se aplicam às definições de público-alvo subjacentes
- Requer mapeamento entre [!DNL RT-CDP] públicos-alvo da conta e [!DNL Marketo] registros de cliente potencial/contato
- Pode ser necessária uma lógica complexa do programa [!DNL Marketo] para traduzir atualizações no nível da pessoa em ações no nível da conta

**Experience League:**

- [Destino do Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/adobe/marketo-engage)
- [Ativar públicos para o destino do Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/adobe/marketo-engage#activate)

### Opção B: Ativação de público-alvo em lote para plataformas de publicidade

**Recomendado para:** campanhas de publicidade baseadas em conta no [!DNL LinkedIn], redes de exibição ou outras plataformas de publicidade nas quais as atualizações diárias de público-alvo são suficientes e a meta principal é o alcance e a conscientização no nível da conta, em vez da resposta em tempo real.

**Como funciona:**

Esta opção ativa os públicos-alvo da conta para anunciar destinos da plataforma ([!DNL LinkedIn] Públicos-alvo correspondentes, [!DNL Google] Correspondência do cliente, [!DNL Facebook] Públicos-alvo personalizados ou [!DNL The Trade Desk]) em uma cadência em lote agendada. O fluxo de dados de ativação exporta membros do público-alvo da conta com campos de identidade mapeados (normalmente endereços de email com hash de contatos associados) que a plataforma de publicidade usa para corresponder à sua base de usuários.

Para [!DNL LinkedIn] especificamente, o destino de [!DNL LinkedIn] Públicos-alvo correspondentes aceita o nome da empresa e a correspondência baseada em domínio, além da correspondência baseada em email, permitindo o direcionamento verdadeiro no nível da conta. Outras plataformas de publicidade normalmente exigem identificadores no nível da pessoa (email, telefone) dos contatos associados às contas qualificadas.

A ativação em lote é executada em um agendamento configurável (diariamente, a cada 6 horas etc.) O e o exportam instantâneos completos do público-alvo ou alterações incrementais dependendo do tipo de destino. Essa abordagem é adequada para campanhas de conscientização sustentada em que os requisitos de atualização do público-alvo são medidos em horas em vez de minutos.

**Principais considerações:**

- A atualização do público-alvo depende da programação em lote (normalmente diariamente)
- As plataformas Advertising têm suas próprias limitações de taxa de correspondência
- [!DNL LinkedIn] dá suporte à correspondência no nível da conta; outras plataformas exigem identificadores no nível da pessoa
- Os formatos de arquivo de exportação e os requisitos de identidade variam de acordo com o destino

**Vantagens:**

- Suporta várias plataformas de publicidade simultaneamente
- O processamento em lote lida com grandes volumes de público com eficiência
- Públicos-alvo de supressão de conta reduzem o desperdício de gastos com anúncios
- [!DNL LinkedIn] Públicos-alvo correspondentes habilitam direcionamento nativo no nível da conta

**Limitações:**

- As atualizações de público-alvo não são em tempo real; a latência depende da programação em lote
- As taxas de correspondência variam por plataforma e campos de identidade disponíveis
- Algumas plataformas não suportam a verdadeira correspondência no nível da conta, somente no nível da pessoa
- Requer configuração de destino separada para cada plataforma de publicidade

**Experience League:**

- [Destino de públicos correspondentes do LinkedIn](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)
- [Destino da Correspondência de clientes do Google](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/advertising/google-customer-match)
- [Catálogo de destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)

### Opção C: ativação baseada em arquivo para o armazenamento em nuvem

**Recomendado para:** organizações que precisam de flexibilidade máxima no modo como os públicos-alvo das contas são consumidos downstream, incluindo importações de CRM, enriquecimento do data warehouse, compartilhamento de dados de parceiros ou integrações personalizadas nas quais uma entrega baseada em arquivo é preferível.

**Como funciona:**

Essa opção exporta públicos-alvo de conta como arquivos CSV, JSON ou Parquet para destinos de armazenamento na nuvem ([!DNL Amazon S3], [!DNL Azure Blob Storage], [!DNL Google Cloud Storage], SFTP) em uma cadência agendada. A exportação inclui atributos de conta, campos de nível de pessoa de contatos associados e metadados de associação de público-alvo. Os sistemas downstream consomem esses arquivos por meio de seus próprios processos de importação.

A ativação baseada em arquivo oferece mais controle sobre o formato de exportação, a seleção de campo e o agendamento. Ele oferece suporte à exportação completa (instantâneo completo do público-alvo a cada execução) e à exportação incremental (somente alterações desde a última execução). Essa abordagem geralmente é usada quando o sistema de destino não tem um conector de destino [!DNL RT-CDP] nativo, ou quando a organização precisa pré-processar ou transformar os dados antes de carregá-los no sistema de destino.

**Principais considerações:**

- Requer infraestrutura de armazenamento na nuvem ([!DNL S3], [!DNL Azure Blob], [!DNL GCS] ou SFTP)
- Os processos de importação downstream devem ser criados e mantidos
- O formato de arquivo (CSV, JSON, Parquet) deve corresponder aos requisitos de sistema downstream
- A programação de exportação deve se alinhar com as janelas de processamento downstream

**Vantagens:**

- Flexibilidade máxima no modo como os dados do público-alvo são consumidos
- Suporta qualquer sistema downstream que possa ler arquivos
- Controle total sobre o formato de exportação, os campos e o agendamento
- Pode atender vários consumidores downstream de uma única exportação
- Suporta modos de exportação completos e incrementais

**Limitações:**

- Latência mais alta de todas as opções (somente lote)
- Requer a criação e a manutenção de fluxos de trabalho de importação downstream
- Sem integração nativa — é necessário um esforço adicional de desenvolvimento
- O gerenciamento de arquivos (limpeza, arquivamento) deve ser tratado separadamente

**Experience League:**

- [Destino do Amazon S3](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/cloud-storage/amazon-s3)
- [Destino do Azure Blob Storage](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/cloud-storage/azure-blob)
- [Ativar públicos para destinos em lote](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/api/connect-activate-batch-destinations)

### Opção D: Ativação de transmissão para sistemas CRM

**Recomendado para:** Casos de uso de alinhamento de marketing de vendas em que as alterações na qualificação da conta devem ser refletidas no CRM ([!DNL Salesforce] ou [!DNL Dynamics]) em tempo quase real para visibilidade da equipe de vendas, atualizações de atribuição de território ou fluxos de trabalho de vendas automatizados.

**Como funciona:**

Esta opção usa conectores de destino de transmissão ([!DNL Salesforce] CRM, [!DNL Microsoft Dynamics]) para enviar alterações de associação de público-alvo de conta diretamente para registros de conta ou contato do CRM. Quando uma conta é qualificada ou sai de um público-alvo, o registro do CRM é atualizado com um campo personalizado que indica a associação do segmento. As equipes de vendas podem criar relatórios, visualizações e alertas do CRM com base nesses campos.

O conector de transmissão envia atualizações incrementais conforme ocorrem alterações na associação do público-alvo. Os mapeamentos de campo conectam atributos de conta e pessoa do [!DNL RT-CDP] aos campos do CRM, permitindo o enriquecimento de registros do CRM com dados unificados do [!DNL RT-CDP]. Essa abordagem fecha o loop entre a inteligência de marketing (qualificação de conta) e a execução de vendas (workflows de CRM).

**Principais considerações:**

- Exige acesso à API do CRM com permissões de gravação apropriadas
- Campos personalizados do CRM devem ser criados para receber dados de associação de público
- O volume de transmissão deve estar dentro dos limites de taxa da API do CRM
- A automação do fluxo de trabalho do CRM deve ser configurada para atuar em atualizações de campo

**Vantagens:**

- Atualizações de CRM quase em tempo real para visibilidade da equipe de vendas
- Habilita fluxos de trabalho automatizados do CRM acionados por alterações no público-alvo
- Enriquece os registros do CRM com dados de conta unificados de [!DNL RT-CDP]
- Oferece suporte a atualizações de campo no nível da conta e no nível do contato

**Limitações:**

- Os limites de taxa da API do CRM podem limitar as atualizações de grandes volumes
- Requer personalização do CRM (campos personalizados, fluxos de trabalho)
- Limitado a [!DNL Salesforce] e [!DNL Microsoft Dynamics] como conectores nativos
- As restrições de avaliação de transmissão se aplicam aos públicos-alvo subjacentes

**Experience League:**

- [Destino do Salesforce CRM](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/crm/salesforce)
- [Destino do Microsoft Dynamics 365](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/crm/microsoft-dynamics-365)

### Comparação de opções

A tabela a seguir compara as principais características de cada opção de implementação.

| Critérios | Opção A: [!DNL Marketo] Streaming | Opção B: Advertising Batch | Opção C: armazenamento na nuvem | Opção D: Streaming de CRM |
| --- | --- | --- | --- | --- |
| Melhor para | Ativação do programa de nutrição | Publicidade baseada em conta | Integração flexível downstream | Alinhamento de vendas e marketing |
| Complexo | Baixa | Médio | Medium-Alto | Médio |
| Latência | Quase em tempo real (minutos) | Lote (horas) | Lote (horas) | Quase em tempo real (minutos) |
| Flexibilidade | Baixo (somente [!DNL Marketo]) | Medium (plataformas de publicidade) | Alto (qualquer sistema downstream) | Baixo (somente CRM) |
| Exige | [!DNL Marketo Engage] licença | Contas da plataforma Advertising | Infraestrutura de armazenamento na nuvem | Acesso à API do CRM |
| Direcionamento no nível da conta | Através de registros de pessoa | Somente [!DNL LinkedIn] (outros no nível de pessoa) | Configurável | Através de registros de conta/contato |
| Esforço de manutenção | Baixa | Low-Medium | Alta | Médio |

### Escolha a opção certa

Use a seguinte orientação de decisão para selecionar a abordagem de ativação correta:

1. **Se sua meta principal for a criação de clientes potenciais B2B e você usar[!DNL Marketo Engage]**, escolha a Opção A. O conector de transmissão nativo fornece o tempo de ação mais rápido para fluxos de trabalho de automação de marketing.

2. **Se a sua meta principal for a conscientização baseada em conta e a geração de demanda por meio de anúncios**, escolha a Opção B. [!DNL LinkedIn] Públicos-alvo correspondentes fornecem o direcionamento em nível de conta mais forte. Use outras plataformas de publicidade para maior alcance.

3. **Se precisar alimentar públicos-alvo de conta para sistemas sem [!DNL RT-CDP] conectores nativos**, ou se precisar de controle máximo sobre o formato de dados e o processamento downstream, escolha a Opção C. Essa também é a melhor opção para compartilhamento de dados de parceiros ou enriquecimento do data warehouse.

4. **Se sua principal meta for a capacitação de vendas e a visibilidade de CRM de contas qualificadas para marketing**, escolha a Opção D. Isso fecha o loop de entrega de marketing para vendas, atualizando os registros do CRM em tempo quase real.

A maioria das organizações B2B implementará várias opções simultaneamente — por exemplo, Opção A para programas de criação, Opção B para publicidade [!DNL LinkedIn] e Opção D para sincronização de CRM. Essas opções não são mutuamente exclusivas; o mesmo público-alvo da conta pode ser ativado para vários destinos simultaneamente.

## Fases de implementação

As fases a seguir descrevem o processo passo a passo para implementar esse padrão de caso de uso.

### Fase 1: Enriquecimento do perfil da conta

Essa fase estabelece perfis de conta unificados por meio da consolidação de dados de CRM, automação de marketing e fontes de terceiros.

**Função de aplicativo:** [!DNL RT-CDP] B2B: Unificação de Perfil de Conta, [!DNL RT-CDP] B2B: Resolução de Identidade B2B

**O que você configurará:** Essa fase estabelece perfis de conta unificados por meio da consolidação de dados do CRM, da automação de marketing e de fontes de terceiros. A resolução de identidade B2B mapeia relacionamentos entre pessoas e contas para que os dados de envolvimento no nível da pessoa (aberturas de email, visitas da Web, downloads de conteúdo) possam ser agregados e usados na avaliação do público-alvo no nível da conta. Essa fase se baseia nas funções fundamentais F2, F3 e F4 que já devem estar em vigor.

**Pontos de decisão nesta fase:**

>[!NOTE]
>**Decisão: estratégia do identificador da conta**
>
>Qual identificador serve como a chave de conta principal entre os sistemas?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| ID da conta do CRM (por exemplo, ID da conta [!DNL Salesforce]) | O CRM é o sistema de registro de contas | Abordagem mais comum. Garante o alinhamento entre o [!DNL RT-CDP] e o CRM. Exige que todos os sistemas de origem façam referência à mesma ID de conta do CRM. |
>| ID de conta personalizada | Várias instâncias do CRM ou uma conta proprietária principal | Requer uma camada de mapeamento entre as IDs do sistema de origem e a ID da conta canônica. Mais flexível, mas mais complexidade. |
>| Número ou domínio DUNS | O enriquecimento de dados de terceiros é a principal fonte de conta | Útil quando os provedores de dados firmográficos são a fonte principal. Pode exigir correspondência difusa para resolução baseada em domínio. |

>[!NOTE]
>**Decisão: modelo de relacionamento entre pessoas e conta**
>
>Como as pessoas (clientes potenciais, contatos) estão associadas às contas?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Um para um (cada pessoa pertence a uma conta) | Modelo B2B simples com dados CRM limpos | Resolução simples. Mais comum para B2B de médio porte. |
>| De muitos para muitos (as pessoas podem pertencer a várias contas) | Relações empresariais complexas, consultores ou redes de parceiros | [!DNL RT-CDP] O B2B edition oferece suporte nativo a isso. Aumenta a complexidade do público-alvo, mas reflete com precisão os relacionamentos do mundo real. |

**Navegação da interface do usuário:** Plataforma > Perfis > Procurar (para verificar perfis de conta unificados)

**Detalhes de configuração da chave:**

- Verifique se os esquemas XDM B2B (Conta comercial XDM, Conta de pessoa de negócios XDM) estão em vigor a partir de F2
- Confirme se o CRM e os conectores de origem [!DNL Marketo] estão assimilando ativamente dados de conta e pessoa da F3
- Validar se os relacionamentos entre pessoa e conta são resolvidos no gráfico de identidade de F4
- Revise a integridade do perfil da conta procurando perfis de conta de amostra

**Documentação do Experience League:**

- [Visão geral do Real-Time CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#rtcdp-b2b)
- [Esquemas B2B no Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Conector do Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Conector do Salesforce](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/crm/salesforce)

### Fase 2: Avaliação do público-alvo da conta

Essa fase define e avalia públicos-alvo no nível da conta usando uma combinação de atributos de conta, atributos de pessoa e dados de atividade de pessoa.

**Função de aplicativo:** [!DNL RT-CDP] B2B: Avaliação de Público-Alvo da Conta, [!DNL RT-CDP]: Avaliação de Público-Alvo

**O que você configurará:** esta fase define e avalia públicos-alvo no nível da conta usando uma combinação de atributos de conta, atributos de pessoa e dados de atividade de pessoa. Os públicos da conta no B2B edition [!DNL RT-CDP] permitem segmentar contas com base nas características firmográficas (setor, receita, contagem de funcionários) e no comportamento de envolvimento das pessoas associadas a essas contas.

**Pontos de decisão nesta fase:**

>[!NOTE]
>**Decisão: método de avaliação de público-alvo**
>
>Com que rapidez a associação de público-alvo da conta deve ser atualizada?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Avaliação em lote (diariamente) | Públicos-alvo do Campaign atualizados em uma cadência diária, ativações baseadas em arquivos, públicos-alvo da plataforma de publicidade | A maioria dos públicos-alvo da conta usa avaliação em lote. Lida com consultas complexas de várias entidades que combinam atributos de conta e pessoa. Suficiente para a maioria dos casos de uso B2B em que a atualização diária é aceitável. |
>| Avaliação de transmissão | [!DNL Marketo] ou ativação do CRM onde é necessária qualificação quase em tempo real | Os públicos-alvo da conta têm qualificação de transmissão limitada. Somente as condições de atributos de conta simples se qualificam para avaliação de streaming. As condições comportamentais no nível da pessoa normalmente exigem batch. |

>[!NOTE]
>**Decisão: abordagem de definição de público-alvo da conta**
>
>Como você definirá os critérios de público-alvo da conta?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Somente atributos da conta | Direcionamento firmográfico simples (setor, receita, região) | O mais rápido de implementar. Limitado aos dados a nível de conta. Use para direcionamento amplo. |
>| Atributos da conta + pessoa | Contas de direcionamento nas quais as pessoas associadas correspondem a critérios específicos (cargo, departamento) | Direcionamento mais preciso. Combina dados demográficos e firmográficos. |
>| Conta + atributos de pessoa + atividade de pessoa | Contas de direcionamento com contatos engajados (aberturas de email, visitas da Web, downloads de conteúdo) | Mais poderoso, mas mais complexo. Requer dados de evento comportamental de F3. Normalmente requer avaliação em lote. |
>| Composição de público | Lógica de público-alvo complexa que requer operações de classificação, divisão, exclusão ou enriquecimento | Use a tela Composição visual do público-alvo para públicos-alvo de conta derivados. Limitado à avaliação em lote. |

>[!NOTE]
>**Decisão: estratégia de supressão de público-alvo**
>
>Quais contas devem ser excluídas da ativação?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Supressão de cliente existente | Campanhas de aquisição para novas contas líquidas | Excluir contas com assinaturas ativas ou oportunidades fechadas |
>| Supressão de ciclo de vendas ativo | Evite interferir em contas no envolvimento de vendas ativo | Excluir contas com oportunidades abertas acima de um determinado estágio |
>| Supressão recente de engajamento | Evitar o excesso de mensagens de contas contatadas recentemente | Excluir contas envolvidas em uma janela de pesquisa (por exemplo, 30 dias) |
>| Sem supressão | Campanhas de reconhecimento de marca voltadas para todas as contas qualificadas | Use com cuidado; pode resultar em gasto desperdiçado em contas inelegíveis |

**Navegação da interface do usuário:** Cliente > Públicos-alvo > Criar público-alvo > Criar regra (selecione Conta como o tipo de público-alvo)

**Detalhes de configuração da chave:**

- Selecione &quot;Conta&quot; como o tipo de público-alvo ao criar um novo público-alvo no Construtor de segmentos
- Os atributos da conta aparecem na seção Conta do Construtor de segmentos (setor, receita, status da conta)
- Atributos de pessoa e atividades podem ser adicionados por meio do relacionamento &quot;Pessoas&quot; no construtor de público-alvo da conta
- Configurar o agendamento de avaliação em lote se ainda não existir um para a sandbox
- Criar públicos-alvo de direcionamento (contas a serem incluídas) e de supressão (contas a serem excluídas)

**Documentação do Experience League:**

- [Públicos da conta](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Composição de público](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)

### Fase 3: configuração de destino

Essa fase estabelece conexões autenticadas com os destinos de destino em que os públicos-alvo da conta serão entregues.

**Função de aplicativo:** [!DNL RT-CDP] B2B: Configuração de Destino de Conta, [!DNL RT-CDP] B2B: [!DNL Marketo Engage] Integração, [!DNL RT-CDP]: Configuração de Destino

**O que você configurará:** Essa fase estabelece conexões autenticadas aos destinos de destino nos quais os públicos-alvo das contas serão entregues. A configuração inclui selecionar o destino do catálogo, fornecer credenciais de autenticação, configurar mapeamentos de campo no nível da conta e no nível da pessoa e definir a programação de exportação. Cada tipo de destino tem requisitos e recursos exclusivos.

**Pontos de decisão nesta fase:**

>[!NOTE]
>**Decisão: seleção de destino**
>
>Quais destinos receberão os públicos-alvo da conta ativada?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| [!DNL Marketo Engage] | Promoção, pontuação e execução de campanha do lead B2B | Conector de transmissão nativo. Atualiza registros de cliente potencial/contato. Exige credenciais da API [!DNL Marketo] (Munchkin ID, ID do Cliente, Segredo do Cliente). |
>| [!DNL LinkedIn] Públicos-alvo correspondentes | Publicidade baseada em conta no [!DNL LinkedIn] | Suporta correspondência de nome de empresa e domínio para direcionamento em nível de conta. Ativação em lote. Requer acesso de [!DNL LinkedIn] ao Gerenciador de Campanha. |
>| [!DNL Salesforce] CRM | Ativação de vendas e sincronização da lista de contas de CRM | O conector de transmissão atualiza registros de conta ou contato. Requer acesso à API [!DNL Salesforce] com permissões de gravação. |
>| [!DNL Microsoft Dynamics 365] | Ativação de vendas para organizações baseadas em [!DNL Dynamics] | Conector de transmissão. Requer acesso à API [!DNL Dynamics 365]. |
>| Armazenamento na nuvem ([!DNL S3], [!DNL Azure Blob], [!DNL GCS], SFTP) | Integrações personalizadas, data warehouse, compartilhamento de parceiros | Exportação em lote baseada em arquivo. Flexibilidade máxima, mas requer processamento downstream. |
>| [!DNL Google] Correspondência de cliente | Pesquisar e exibir direcionamento de publicidade | Correspondência no nível de pessoa por email com hash. Ativação em lote. |
>| [!DNL The Trade Desk] | Exibição programática e publicidade em vídeo | Correspondência de nível de pessoa. Ativação em lote. |

>[!NOTE]
>**Decisão: estratégia de mapeamento de campo**
>
>Quais campos de conta e pessoa devem ser mapeados para o destino?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Somente campos de identidade | Plataformas Advertising que precisam apenas de identificadores correspondentes | Transferência mínima de dados. O destino corresponde no email ou no domínio da empresa. |
>| Identidade + atributos principais da conta | CRM ou [!DNL Marketo] onde o contexto da conta melhora o direcionamento | Incluir setor, receita, contagem de funcionários, nível de conta. Enriquecer registros downstream. |
>| Conjunto completo de atributos | Armazenamento em nuvem ou exportações de data warehouse | Incluir todos os atributos relevantes de conta e pessoa. Maior carga útil de exportação. |

Navegação da **IU:** Conexões > Destinos > Catálogo > Pesquisar destino > Configurar

**Detalhes de configuração da chave:**

- Navegue até o catálogo Destinos e selecione o destino
- Fornecer credenciais de autenticação específicas para o tipo de destino
- Configurar mapeamentos de campo conectando campos XDM [!DNL RT-CDP] a campos de destino
- Para [!DNL Marketo Engage]: fornecer ID do Munchkin, ID do Cliente e Segredo do Cliente
- Para [!DNL LinkedIn]: autorize via OAuth e selecione a conta de anúncio [!DNL LinkedIn]
- Para armazenamento na nuvem: forneça o nome do bucket/container, o caminho, o formato de arquivo e as credenciais
- Para CRM: forneça o URL da instância, as credenciais de API e o tipo de objeto de destino (Conta ou Contato)

**Onde as opções divergem:**

**Para Opção A ([!DNL Marketo Engage] Streaming):**

Navegue até Destinos > Catálogo > Adobe > [!DNL Marketo Engage]. Configure a Munchkin ID e as credenciais da API. Mapear [!DNL RT-CDP] campos de identidade (email) e atributos de perfil para [!DNL Marketo] campos de cliente potencial. O destino manipula automaticamente atualizações de transmissão incrementais.

**Para a Opção B (Lote da Advertising Platform):**

Navegue até Destinos > Catálogo > Advertising/Social > selecionar plataforma. Autorizar via OAuth. Configurar o cronograma de exportação (recomendado: diariamente). Mapeie identificadores de email com hash e quaisquer campos correspondentes compatíveis. Para [!DNL LinkedIn], mapeie também o nome da empresa e os campos de domínio para a correspondência no nível da conta.

**Para a Opção C (Baseada em Arquivo de Armazenamento em Nuvem):**

Navegue até Destinos > Catálogo > Armazenamento na nuvem > selecionar provedor. Configurar bucket/container, modelo de caminho de arquivo e formato de arquivo (CSV, JSON ou Parquet). Defina o cronograma de exportação e escolha exportação completa ou incremental. Mapeie todos os campos de atributo de conta e pessoa desejados.

**Para a Opção D (Streaming de CRM):**

Navegue até Destinos > Catálogo > CRM > selecione [!DNL Salesforce] ou [!DNL Dynamics]. Forneça as credenciais da API e o URL da instância. Mapeie os campos [!DNL RT-CDP] para campos de conta ou contato do CRM. Verifique se existem campos personalizados no CRM para receber dados de associação de público-alvo.

**Documentação do Experience League:**

- [Visão geral dos destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [Destino do Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/adobe/marketo-engage)
- [Destino de públicos correspondentes do LinkedIn](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)
- [Destino do Salesforce CRM](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/crm/salesforce)
- [Destino do Amazon S3](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/cloud-storage/amazon-s3)

### Fase 4: Ativação do público-alvo

Essa fase publica os públicos-alvo da conta avaliados nos destinos configurados.

**Função de aplicativo:** [!DNL RT-CDP] B2B: Audience Activation de Conta, [!DNL RT-CDP]: Audience Activation

**O que você configurará:** Essa fase publica os públicos avaliados da conta para os destinos configurados. A ativação cria o fluxo de dados conectando o público-alvo da conta (origem) ao destino externo (destino), aplica mapeamentos de atributos e inicia a exportação de acordo com o agendamento configurado ou o comportamento de streaming. Você também irá configurar públicos de supressão para excluir contas não qualificadas da ativação.

**Pontos de decisão nesta fase:**

>[!NOTE]
>**Decisão: Tipo de exportação**
>
>A ativação deve exportar instantâneos completos de público-alvo ou apenas alterações incrementais?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Exportação incremental | Destinos de transmissão ([!DNL Marketo], CRM) ou destinos em lote em que os sistemas downstream lidam com deltas | Volume de dados menor por exportação. Processamento mais rápido. Requer sistemas downstream para gerenciar o estado. Padrão para destinos de transmissão. |
>| Exportação completa | Destinos em lote em que o sistema downstream substitui o público-alvo completo de cada execução | Volume de dados maior, mas lógica downstream mais simples. Útil quando os sistemas downstream não mantêm o estado. Disponível para destinos baseados em arquivo. |

>[!NOTE]
>**Decisão: escopo de ativação**
>
>Quantos públicos-alvo devem ser ativados por destino?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Um único público por fluxo de dados | Ativação simples com mapeamento claro de público para destino | É mais fácil monitorar e solucionar problemas. Uma falha de público-alvo não afeta outros. |
>| Vários públicos-alvo por fluxo de dados | Vários públicos relacionados indo para o mesmo destino | Uso mais eficiente de conexões de destino. Todos os públicos-alvo compartilham o mesmo mapeamento de campo e agendamento. |

**Navegação da interface do usuário:** Conexões > Destinos > Procurar > Selecionar destino > Ativar públicos

**Detalhes de configuração da chave:**

- Selecionar o(s) público(s) alvo na lista de públicos
- Revise e confirme os mapeamentos de campo configurados na Fase 3
- Para destinos em lote: configurar o agendamento de exportação (hora, frequência)
- Para destinos de transmissão: a ativação começa imediatamente após a configuração
- Opcionalmente, adicione públicos-alvo de supressão usando a funcionalidade de exclusão
- Acionar uma execução de ativação de teste inicial para validar o fluxo de dados

**Onde as opções divergem:**

**Para Opção A ([!DNL Marketo Engage] Streaming):**

Selecione os públicos da conta a serem ativados. A ativação começa a transmitir imediatamente. Verifique em [!DNL Marketo] se os registros de cliente potencial/contato estão sendo atualizados com campos de associação de segmento. Configure as campanhas inteligentes [!DNL Marketo] para serem acionadas com base nessas alterações de campo.

**Para a Opção B (Lote da Advertising Platform):**

Selecione públicos-alvo da conta e configure o cronograma de exportação diário. Depois que a primeira exportação for concluída, verifique na plataforma de publicidade se o público-alvo aparece e se tem uma contagem de membros preenchida. Aguarde de 24 a 48 horas para que a plataforma processe o arquivo de público-alvo inicial.

**Para a Opção C (Baseada em Arquivo de Armazenamento em Nuvem):**

Selecione públicos-alvo da conta e configure o cronograma de exportação e o formato de arquivo. Após a primeira exportação, verifique se os arquivos aparecem no local de armazenamento de destino com o formato e o conteúdo esperados. Confirme se os processos de importação downstream consomem com êxito os arquivos exportados.

**Para a Opção D (Streaming de CRM):**

Selecione os públicos da conta a serem ativados. A ativação começa a transmitir imediatamente. Verifique no CRM se os registros de conta ou contato estão sendo atualizados com os campos mapeados. Configure relatórios do CRM, exibições de lista ou automação do fluxo de trabalho para atuar nos campos atualizados.

**Documentação do Experience League:**

- [Ativar públicos para destinos de transmissão](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Ativar públicos para destinos em lote](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Medidas de proteção de ativação](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)
- [Visão geral dos destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)

### Fase 5: governança e monitoramento

Essa fase garante que a ativação do público-alvo da conta esteja em conformidade com as políticas de governança de dados e as preferências de consentimento, e que os fluxos de dados de ativação em andamento sejam monitorados quanto à integridade.

**Função de aplicativo:** [!DNL RT-CDP] B2B: Governança de Dados B2B, [!DNL RT-CDP]: Consentimento e Imposição de Governança

**O que você configurará:** Essa fase garante que a ativação do público-alvo da conta esteja em conformidade com as políticas de governança de dados e as preferências de consentimento, e que os fluxos de dados de ativação em andamento sejam monitorados quanto à integridade. A governança de dados B2B impõe restrições aos atributos confidenciais da conta (receita, contagem de funcionários de provedores de terceiros), enquanto a aplicação do consentimento garante que as comunicações no nível da pessoa respeitem as preferências de recusa. O monitoramento confirma que os fluxos de dados de ativação estão sendo concluídos com êxito.

**Pontos de decisão nesta fase:**

>[!NOTE]
>**Decisão: nível de imposição de governança**
>
>Com que rigor a governança de dados deve ser aplicada para ativações B2B?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Imposição total (bloqueio em caso de violação) | Ativações de produção com dados confidenciais | Impede qualquer ativação que viole as políticas de governança. Pode exigir ajustes de mapeamento de campo iterativo para resolver violações. |
>| Avisar e continuar | Ambientes de desenvolvimento ou teste | Permite que a ativação continue, mas registra avisos. Útil durante a configuração inicial para identificar possíveis problemas. |

>[!NOTE]
>**Decisão: abordagem de monitoramento**
>
>Como a integridade da ativação deve ser monitorada?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Monitoramento baseado em alerta | Ambientes de produção onde as falhas devem ser detectadas rapidamente | Configure alertas para falhas de ativação de destino, falhas de fluxo de origem e atrasos de fluxo de dados. Requer configuração de assinatura de alerta. |
>| Monitoramento manual | Desenvolvimento ou ativações de baixo volume | Revise periodicamente as execuções do fluxo de dados na interface do usuário de Destinos. Menos sobrecarga, mas risco de detecção de falha atrasada. |
>| Ambos | Ambientes de produção com ativação complexa de vários destinos | Alertas de falhas críticas mais revisão periódica do painel de controle para tendências. Recomendado para a maioria das implementações B2B. |

**Navegação da interface do usuário:** Privacidade > Políticas (para governança), Conexões > Destinos > Procurar > Selecionar destino > Execuções de fluxo de dados (para monitoramento)

**Detalhes de configuração da chave:**

- Aplicar rótulos de uso de dados a conjuntos de dados B2B que contenham atributos restritos
- Verifique se as políticas de governança são aplicadas avaliando a ativação em relação à ação de marketing de destino
- Configurar alertas para falhas de ativação de destino e falhas no conector de origem
- Revise as métricas de execução do fluxo de dados (perfis exportados, registros com falha) após cada ciclo de ativação
- Configurar revisão do painel de uso de licença para rastrear o volume de perfil da conta em relação aos direitos

**Documentação do Experience League:**

- [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Consentimento e preferências](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)
- [Monitorar fluxos de dados de destino](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations)
- [Visão geral de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Medidas de proteção de ativação](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)

## Considerações de implantação

As seções a seguir fornecem orientação adicional para uma implementação bem-sucedida.

### Medidas de proteção e limites

Revise as medidas de proteção e os limites de plataforma a seguir que se aplicam a esse padrão de caso de uso.

- Máximo de 4.000 definições de segmento por sandbox, incluindo públicos-alvo da conta — [Medidas de proteção de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Os públicos-alvo da conta são avaliados principalmente usando a avaliação em lote; a qualificação da transmissão é limitada às condições simples do atributo da conta
- Máximo de 100 fluxos de dados por conexão de destino — [Medidas de proteção de destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)
- Os destinos em lote exportam até 5 milhões de perfis por segmento de arquivo
- Os destinos de transmissão têm limites de taxa de transferência por segundo definidos pelo parceiro de destino (por exemplo, limites de taxa de API [!DNL Marketo])
- Os públicos-alvo compostos (da Composição de público-alvo) estão limitados à avaliação em lote e não podem usar a transmissão
- Máximo de 10 blocos de composição por tela de Composição de público-alvo
- [!DNL LinkedIn] Públicos-alvo correspondentes requerem um tamanho mínimo de público-alvo (normalmente 300 membros) para ativação
- Os destinos de streaming do CRM estão sujeitos aos limites de taxa de API do provedor de CRM (por exemplo, [!DNL Salesforce] limites diários de API em massa)
- [!DNL RT-CDP] A licença do B2B edition controla o número total de perfis de contas corporativas — [Descrição do produto RT-CDP](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

### Armadilhas comuns

Esteja ciente dos seguintes problemas comuns ao implementar esse padrão de caso de uso.

- **Mapeamento incompleto de pessoa para conta:** se os registros de pessoa (clientes potenciais, contatos) não estiverem vinculados corretamente aos registros de conta por meio da resolução de identidade B2B, os públicos-alvo de conta que dependem dos atributos de pessoa ou das atividades não contarão as contas qualificadas. Valide os relacionamentos pessoa-para-conta em F4 antes de criar públicos-alvo da conta.

- **Dados obsoletos do CRM que causam descompasso de público-alvo:** Se os conectores de origem do CRM não estiverem em execução em um agendamento regular ou estiverem falhando silenciosamente, os atributos da conta (setor, receita, status) se tornarão obsoletos. Isso faz com que os públicos-alvo incluam contas que não se qualificam mais ou excluam contas que devem se qualificar. Monitorar integridade do fluxo de dados do conector de origem.

- **Expectativas de taxa de correspondência da plataforma Advertising:** Ao ativar públicos-alvo da conta para plataformas de publicidade diferentes de [!DNL LinkedIn], a taxa de correspondência dependerá de ter identificadores de nível de pessoa (email com hash) válidos para contatos associados a contas qualificadas. As contas sem contatos associados que têm endereços de email não corresponderão. Monitore as taxas de correspondência e considere enriquecer dados de contato.

- Desalinhamento de mapeamento de campo **[!DNL Marketo]:** Ao transmitir para [!DNL Marketo Engage], o mapeamento de campo [!DNL RT-CDP] deve direcionar campos de cliente potencial ou de contato [!DNL Marketo] existentes. Se o campo [!DNL Marketo] mapeado não existir, a atualização silenciosamente falhará. Pré-criar todos os campos de destino em [!DNL Marketo] antes de configurar o destino.

- **Ativação de bloqueio de política de governança:** Os rótulos de uso de dados em campos de atributo de conta (especialmente dados firmográficos de terceiros) podem disparar violações de governança ao ativar para destinos de publicidade. Avalie a conformidade de governança antes de ativar e ajustar os mapeamentos de campo para excluir campos restritos, se necessário.

- **Público-alvo da conta combinando dados de conta e de pessoa com avaliação somente em lote:** Os públicos-alvo da conta que fazem referência a eventos comportamentais no nível da pessoa (por exemplo, &quot;contas em que pelo menos um contato abriu um email nos últimos 30 dias&quot;) exigem avaliação em lote. Se o caso de uso esperar uma qualificação em tempo real, essa restrição poderá causar latência inesperada.

### Práticas recomendadas

Siga estas recomendações para obter os melhores resultados.

- Comece com um pequeno número de públicos-alvo de conta bem definidos (nível ICP, vertical do setor, nível de envolvimento) antes de expandir para definições complexas de vários atributos
- Crie públicos de supressão dedicados para clientes existentes, oportunidades ativas e contas engajadas recentemente para evitar gastos desperdiçados e conflitos de canais
- Use a Composição de público-alvo para criar públicos-alvo de conta em camadas (envolvimento alto/médio/baixo), classificando as contas nas pontuações de envolvimento agregadas
- Ative o mesmo público da conta para vários destinos simultaneamente para campanhas coordenadas de vários canais (por exemplo, [!DNL LinkedIn] para publicidade, [!DNL Marketo] para email, CRM para visibilidade de vendas)
- Implemente uma convenção de nomenclatura consistente para públicos-alvo da conta que inclua os critérios de direcionamento e o canal pretendido (por exemplo, &quot;B2B_ICP_Enterprise_Tech_LinkedIn&quot; ou &quot;B2B_Suppression_AtiveOpps&quot;)
- Agende a ativação em lote fora dos horários de pico para minimizar o impacto nos sistemas downstream e alinhar-se às janelas de processamento da plataforma de publicidade
- Monitorar taxas de correspondência por destino após a ativação inicial e iterar nos mapeamentos de campo de identidade para melhorar a correspondência
- Manter fluxo de dados bidirecional com [!DNL Marketo Engage]: assimilar dados de envolvimento de [!DNL Marketo] em [!DNL RT-CDP] (conector de origem) e ativar públicos de volta para [!DNL Marketo] (conector de destino) para um sistema de loop fechado

### Decisões de compensação

Considere as seguintes compensações ao tomar decisões de implementação.

>[!NOTE]
>**Contrapartida: atualização de público-alvo vs. complexidade da avaliação**
>
>Públicos-alvo de conta que combinam atributos de conta com dados comportamentais no nível da pessoa fornecem o direcionamento mais preciso, mas estão limitados à avaliação em lote (atualização diária). Públicos mais simples com base apenas nos atributos da conta podem se qualificar para avaliação de transmissão com atualizações quase em tempo real.
>
>- **O lote (critérios complexos) favorece:** precisão de direcionamento, combinação de sinais firmográficos e comportamentais, pontuação de conta abrangente
>- **A transmissão (critérios simples) favorece:** a velocidade das atualizações de público-alvo, a resposta em tempo real às alterações na conta, o tempo de ação mais rápido no [!DNL Marketo] e no CRM
>- **Recomendação:** Use a avaliação em lote para públicos-alvo de direcionamento primários nos quais a atualização diária é aceitável (a maioria dos casos de uso B2B). Reserve a avaliação de transmissão para acionadores sensíveis ao tempo, como alterações no status da conta ou alertas de conta de alto valor.

>[!NOTE]
>**Contrapartida: ativação centralizada vs. públicos-alvo específicos do destino**
>
>Você pode ativar um único público-alvo de conta unificada para vários destinos ou criar públicos-alvo específicos de destino personalizados para os recursos e requisitos de cada canal.
>
>- **O público-alvo centralizado favorece:** consistência entre canais, gerenciamento mais simples de público-alvo, relatórios unificados
>- **Públicos-alvo específicos de destino favorecem:** Direcionamento otimizado por canal (por exemplo, [!DNL LinkedIn] se beneficia de atributos no nível da empresa enquanto [!DNL Marketo] precisa de detalhes no nível de cliente potencial), regras de supressão específicas de canal
>- **Recomendação:** comece com públicos centralizados para fins de consistência e, em seguida, crie variantes específicas de destino somente quando os requisitos do canal forem significativamente diferentes (por exemplo, janelas de supressão diferentes para publicidade ou email).

>[!NOTE]
>**Contrapartida: sincronização do CRM em tempo real vs. atualizações do CRM em lote**
>
>A transmissão para o CRM oferece visibilidade de vendas imediata, mas consome a cota da API do CRM. As exportações de arquivos em lote são mais eficientes, mas introduzem latência.
>
>- **A sincronização de CRM de streaming favorece:** Capacidade de resposta de vendas, alertas de conta imediatos, visibilidade de pipeline em tempo real
>- **As atualizações de CRM em lote favorecem:** conservação de cota de API, eficiência de atualização em massa, alinhamento com as janelas de carregamento de dados do CRM
>- **Recomendação:** Use a sincronização de CRM de streaming para alterações de qualificação de conta de alta prioridade (por exemplo, a conta é movida para a camada &quot;Pronto para Vendas&quot;). Use exportações de arquivos em lote para atualizações em massa, como atualizações mensais de pontuação de conta ou listas de reatribuição de território.

## Documentação relacionada

Os recursos a seguir fornecem contexto adicional e orientação detalhada para os recursos usados neste padrão de caso de uso.

**[!DNL RT-CDP]B2B edition**

- [Visão geral do Real-Time CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#rtcdp-b2b)
- [Esquemas B2B no Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Públicos da conta](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences)
- [Descrição do produto RT-CDP B2B edition](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

**Avaliação e segmentação de público-alvo**

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Composição de público](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Segmentação de transmissão](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Proteções de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)

**Destinos e ativação**

- [Visão geral dos destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [Destino do Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/adobe/marketo-engage)
- [Destino de públicos correspondentes do LinkedIn](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)
- [Destino do Salesforce CRM](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/crm/salesforce)
- [Destino do Microsoft Dynamics 365](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/crm/microsoft-dynamics-365)
- [Destino do Amazon S3](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/cloud-storage/amazon-s3)
- [Ativar públicos para destinos de transmissão](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Ativar públicos para destinos em lote](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Medidas de proteção de ativação](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)

**Fontes de dados e conectores**

- [Visão geral das fontes](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Conector do Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Conector do Salesforce](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/crm/salesforce)

**Identidade e modelagem de dados**

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Visão geral do perfil](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

**Governança e privacidade de dados**

- [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview)
- [Consentimento e preferências](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)

**Monitoramento e observabilidade**

- [Visão geral de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Monitorar fluxos de dados de destino](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations)
- [Monitorar fluxos de dados de origem](https://experienceleague.adobe.com/en/docs/experience-platform/sources/api-tutorials/monitor)
- [Painel de uso da licença](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/license-usage-dashboard)

**Relatórios e análises**

- [Visão geral do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Visão geral das conexões](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [Visão geral das visualizações de dados](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)

**Tutoriais e guias**

- [Introdução ao Real-Time CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro)
- [Criar um esquema para fontes B2B](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Ferramentas de sandbox](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/overview)
