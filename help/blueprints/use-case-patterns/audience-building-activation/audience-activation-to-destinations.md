---
title: Ativação de público-alvo para destinos
description: Saiba como avaliar e publicar segmentos de público-alvo em destinos externos para direcionamento ou supressão usando o Adobe Real-Time CDP.
solution: Real-Time Customer Data Platform, Experience Platform
exl-id: b0b9d937-45d2-48f9-ac4c-3611c6e35f58
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '7043'
ht-degree: 1%

---

# Ativação de público-alvo para destinos

Este guia fornece uma referência completa de implementação para ativar públicos-alvo do Adobe [!DNL Real-Time Customer Data Platform] (RT-CDP) para destinos externos. Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam avaliar segmentos de público-alvo e publicá-los em plataformas de anúncios, armazenamento em nuvem, sistemas de CRM ou parceiros de dados para direcionamento, supressão, modelagem por semelhança ou enriquecimento de análise.

Ele apresenta todas as opções de implementação viáveis com análise de compensação, orientação de decisão, caminhos de navegação da interface do usuário e referências de documentação do Experience League.

O guia aborda o ciclo de vida completo da ativação de público-alvo — desde a definição e avaliação de segmentos de público-alvo até a configuração de conexões de destino e públicos de publicação, passando pelo monitoramento da integridade da ativação e pela aplicação da conformidade de governança.

## Visão geral do caso de uso

As organizações precisam fornecer dados de público-alvo para sistemas externos a fim de alimentar campanhas de mídia paga, enriquecer registros de CRM, compartilhar dados com parceiros ou alimentar análises downstream. O Audience Activation para destinos é o padrão de ativação fundamental no RT-CDP: ele avalia quais perfis se qualificam para um público-alvo de destino, se conecta a um ou mais destinos externos, mapeia atributos de perfil para campos específicos de destino e publica o público-alvo para consumo downstream.

Esse padrão se aplica sempre que o objetivo é obter dados de público-alvo para um sistema externo no formato certo, na hora certa. Não envolve entrega de mensagens, personalização no site ou análise. É o ponto de partida mais comum para implementações da RT-CDP e serve como um bloco de construção que outros padrões compõem sobre.

As partes interessadas típicas incluem equipes de marketing digital que gerenciam mídia paga, equipes de dados que enriquecem depósitos, equipes de CRM que preparam listas de contato para campanhas e equipes de privacidade que garantem a conformidade da governança em fluxos de dados de saída.

>[!NOTE]
>Se sua organização usar o B2B edition [!DNL Real-Time CDP] e ativar para destinos baseados em conta, consulte [Ativação de público B2B](b2b-audience-activation.md). Esse padrão compartilha a mesma mecânica de ativação, mas usa um modelo de dados de conta e pessoa B2B e requer a licença do B2B edition.

## Principais objetivos de negócios

Os seguintes objetivos de negócios são compatíveis com esse padrão de caso de uso.

### Adquirir novos clientes

Expanda a base de clientes por meio de campanhas de aquisição direcionadas, públicos semelhantes e otimização de mídia paga.

**KPIs:** Novos Clientes, Custo de Aquisição do Cliente, Conversão de Cliente Potencial/Cliente Potencial

[Saiba mais sobre como adquirir novos clientes](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

### Reduza o custo de aquisição do cliente

Melhore a eficiência do direcionamento, elimine clientes existentes das campanhas de aquisição e otimize os gastos com mídia.

**KPIs:** Custo de Aquisição do Cliente, Custo por Cliente Potencial, Eficiência

[Saiba mais sobre como reduzir o custo de aquisição de clientes](/help/blueprints/business-objectives/cost-efficiency/reduce-customer-acquisition-cost.md)

### Otimizar o investimento e o ROI do marketing

Melhore o retorno sobre o investimento em marketing através de melhor direcionamento, atribuição, supressão de público-alvo e alocação de orçamento.

**KPIs:** Economia, Custo de Aquisição do Cliente, Receita Incremental

[Saiba mais sobre como otimizar os gastos com marketing e o ROI](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)

## Exemplo de casos de uso tático

- **Direcionamento de público-alvo da plataforma de publicidade** — Encaminhe segmentos qualificados para plataformas de mídia pagas para direcionamento de campanha
- **Supressão de mídia paga de clientes existentes** — exclua clientes conhecidos das campanhas de aquisição em plataformas de anúncios para eliminar gastos desnecessários
- **Públicos-alvo de propagação semelhantes** — Encaminhe segmentos de alto valor do cliente para o Facebook, Google Ads ou The Trade Desk como públicos-alvo de propagação para expansão por semelhança
- **Sincronização de CRM para habilitação de vendas** — ative públicos-alvo de alta intenção ou alto valor para que as equipes de vendas possam priorizar o alcance externo
- **Compartilhamento de público-alvo do parceiro de dados** — Compartilhe segmentos de público-alvo qualificados com parceiros de dados para segmentação ou medição cooperativa
- **Exportação do armazenamento na nuvem para enriquecimento do data warehouse** — Exportar associação de público-alvo e atributos de perfil para Amazon S3, Azure Blob, Google Cloud Storage ou SFTP para análise downstream
- **Ativação do público-alvo de redirecionamento** — Ative visitantes do site que não converteram em plataformas de redirecionamento
- **Sincronização da lista de contatos com provedores de serviços de email** — Encaminhe a associação de público-alvo para plataformas de email de terceiros para um alcance coordenado

## Indicadores-chave de desempenho

| KPI | Descrição | Abordagem de medição |
| --- | --- | --- |
| Custo de aquisição do cliente (CAC) | Custo para adquirir um novo cliente por meio de públicos ativados | Total de gastos com mídia/novos clientes atribuídos a públicos ativados |
| Taxa de correspondência do público-alvo | Porcentagem de perfis ativados correspondidos com êxito no destino | Perfis correspondentes no destino/perfis exportados da RT-CDP |
| Economias de supressão | Gastos com mídia evitados ao suprimir clientes existentes das campanhas de aquisição | Tamanho estimado do público-alvo do CPM x suprimido |
| Taxa de entrega de ativação | Porcentagem de perfis entregues com êxito ao destino | Perfis entregues/perfis no público-alvo de origem |
| Tempo até a ativação | Tempo decorrido desde a definição do público-alvo até a primeira entrega no destino | Medida desde a criação do segmento até a primeira execução confirmada do fluxo de dados |
| Precisão de preenchimento do público | Alinhamento entre os tamanhos de público esperado e real no destino | Contagem de público-alvo de destino / contagem de público-alvo RT-CDP |

## Padrão do caso de uso

**Audience Activation para Destinos** — Avalie e publique um segmento de público-alvo para destinos externos para direcionamento ou supressão.

**Cadeia De Funções:** Avaliação De Público-Alvo > Configuração De Destino > Audience Activation > Monitoramento

## Aplicativos

- **Adobe [!DNL Real-Time Customer Data Platform] (RT-CDP)** — Avaliação de público-alvo, gerenciamento de destino, ativação de público-alvo, consentimento e imposição de governança
- **Adobe [!DNL Experience Platform] (AEP)** — Armazenamento de perfis, serviço de identidade, mecanismo de segmentação, governança de dados

## Funções básicas

Os seguintes recursos básicos devem estar em vigor para esse padrão de caso de uso. Para cada função, o status indica se ele é tipicamente necessário, se presume ser pré-configurado ou se não é aplicável.

| Função de base | Status | O que deve estar em vigor | Referência do Experience League |
| --- | --- | --- | --- |
| Administração e governança | Presumido em vigor | Sandbox RT-CDP provisionada e ativa. Permissões de ativação e gerenciamento de destino atribuídas a funções de implementação. Credenciais de conta de destino disponíveis para as plataformas de destino. | [Visão geral das sandboxes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/home), [Visão geral do controle de acesso](https://experienceleague.adobe.com/pt-br/docs/experience-platform/access-control/home) |
| Preparação e modelagem de dados | Obrigatório | O esquema de perfil deve incluir atributos que serão mapeados para campos de destino (por exemplo, email, telefone, identificadores com hash, atributos demográficos). O esquema deve ser habilitado para perfis com conjuntos de dados recebendo dados ativamente. | [Visão geral do sistema XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/home), [noções básicas de composição de esquema](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/schema/composition) |
| Fontes de dados e coleção | Presumido em vigor | Os dados do perfil que possibilitam a avaliação do público-alvo devem ser assimilados e atuais. Os pipelines de assimilação em lote e/ou fluxo estão operacionais. Web SDK, conectores de origem ou assimilação em lote que fornecem dados em conjuntos de dados habilitados para perfil. | [Visão geral das fontes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/home), [Visão geral do Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/web-sdk/home) |
| Configuração de identidade e perfil | Obrigatório | Os namespaces de identidade para correspondência de destino devem ser configurados (por exemplo, email com hash para Públicos-alvo personalizados do Facebook, Correspondência de cliente do Google Ads). As políticas de mesclagem devem produzir perfis unificados com todos os atributos necessários para ativação. | [Visão geral do Serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/home), [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/merge-policies/overview) |
| Definição e segmentação do público-alvo | Obrigatório | Público-alvo definido usando o Construtor de segmentos, a Composição de público-alvo ou a Composição de público-alvo federado. Método de avaliação (lote, streaming ou borda) selecionado com base nas necessidades de latência de ativação. Esta função é exercida na Fase 1 deste plano. | [Visão geral do Serviço de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/home), [guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-builder) |

## Funções de suporte

Os recursos a seguir aumentam esse padrão de caso de uso, mas não são necessários para a execução principal.

| Função de suporte | Status | Por que é importante | Referência do Experience League |
| --- | --- | --- | --- |
| Criação de atributo calculado/derivado | Recomendado | Os atributos computados, como valor vitalício, pontuação de engajamento ou pontuação de propensão, melhoram a precisão do público-alvo e fornecem atributos de enriquecimento para mapear a destinos. Particularmente valioso quando os destinos se beneficiam da segmentação de público com base em valor ou em pontuação. | [Visão geral dos atributos computados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/computed-attributes/overview) |
| Gerenciamento do ciclo de vida dos dados | Recomendado | As políticas de expiração de conjuntos de dados e perfis garantem a atualização e a conformidade dos dados. A configuração do esquema de consentimento garante que apenas perfis consentidos sejam ativados. Essencial para a conformidade normativa ao exportar dados para sistemas externos. | [Visão geral do Gerenciamento Avançado do Ciclo de Vida dos Dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-lifecycle/home) |
| Rotulagem e aplicação de uso de dados | Recomendado | Os rótulos e políticas de governança impedem a ativação de dados restritos para destinos não autorizados (por exemplo, plataformas PII para anúncio, segmentos confidenciais para parceiros de dados). Especialmente importante para a ativação de públicos-alvo para sistemas externos de terceiros. | [Visão geral da governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/home), [Visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview) |
| Monitoramento e capacidade de observação | Incluído | O monitoramento de ativação faz parte da cadeia de funções (Fase 5). Abrange monitoramento de execução de fluxo de dados, alertas de status do delivery, rastreamento do público-alvo e visibilidade do uso de licença. | [Monitorar fluxos de dados de destino](https://experienceleague.adobe.com/pt-br/docs/experience-platform/dataflows/ui/monitor-destinations), [Visão geral dos alertas](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/alerts/overview) |
| Relatórios e análise | Recomendado | A análise do CJA da eficácia de ativação de público permite medir o desempenho de públicos ativados (por exemplo, aumento de conversão da supressão, ROAS de públicos semelhantes). | [visão geral do CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-overview/cja-overview) |

## Funções do aplicativo

Este plano exerce as seguintes funções do Catálogo de Funções da Aplicação. As funções são mapeadas para fases de implementação em vez de etapas numeradas.

### [!DNL Real-Time CDP] (RT-CDP)

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Avaliação de público | Fase 1: Avaliação de público-alvo | Defina regras de público-alvo e avalie a associação do segmento usando métodos de avaliação de lote, transmissão ou borda |
| Composição de público | Fase 1: Avaliação de público-alvo | Opcionalmente, compor públicos-alvo derivados por meio de operações de enriquecimento, classificação, divisão, exclusão e associação para uma lógica complexa de público-alvo |
| Configuração de destino | Fase 2: configuração de destino | Configurar conexões autenticadas para destinos externos com mapeamento de campo e parâmetros de agendamento |
| Audience Activation | Fase 3: Audience Activation | Publicar públicos avaliados em destinos configurados com mapeamento de atributos e agendamento de exportação |
| Consentimento e aplicação de governança | Fase 4: validação de governança | Aplicar preferências de consentimento e políticas de uso de dados antes e durante a ativação do público-alvo para sistemas externos |

## Pré-requisitos

- [ ] A licença da RT-CDP está ativa com direitos de ativação de público
- [ ] A sandbox do Target está provisionada e acessível à equipe de implementação
- [ ] As funções de usuário incluem gerenciamento de destino e permissões de ativação de público-alvo
- [ ] As credenciais de autenticação para cada destino estão disponíveis (tokens OAuth, chaves de API, chaves de acesso S3 ou credenciais de conta de serviço)
- [ ] O esquema de perfil inclui todos os atributos que precisam ser mapeados para campos de destino
- [ ] namespaces de identidade necessários para correspondência de destino estão configurados (por exemplo, email com hash, telefone, IDs de dispositivo)
- [ ] Os pipelines de assimilação de dados estão operacionais e os perfis estão preenchendo o repositório de perfis
- [ ] Rótulos e políticas de governança de dados são revisados para os atributos que estão sendo ativados (especialmente para destinos externos)
- [ ] Os campos de consentimento serão preenchidos nos perfis se a filtragem baseada em consentimento for necessária

## Opções de implementação

As seguintes opções de implementação estão disponíveis para este padrão de caso de uso. Analise cada opção e a tabela de comparação para determinar a melhor abordagem para suas necessidades.

### Opção A: Ativação do destino de transmissão

**Recomendado para:** Atualizações de associação de público-alvo em tempo real em plataformas de anúncios ou sistemas de parceiros — Públicos-alvo personalizados do Facebook, Correspondência de clientes do Google Ads, Públicos-alvo correspondentes do LinkedIn, A Trade Desk e destinos semelhantes baseados em API de transmissão.

**Como funciona:**

A ativação do destino de transmissão fornece alterações de associação de público-alvo no destino em tempo quase real, conforme os perfis se qualificam ou desqualificam do segmento. Quando um atributo de perfil é alterado ou ocorre um evento comportamental que faz com que um perfil entre ou saia de um público-alvo, a atualização de associação é transmitida para o destino em minutos.

Essa abordagem requer um conector de destino de transmissão (a maioria das principais plataformas de anúncio oferece suporte a isso) e um método de avaliação de público-alvo de transmissão ou borda. A avaliação de público-alvo monitora continuamente as alterações de perfil qualificadas e o fluxo de dados de ativação envia as atualizações à medida que elas ocorrem. O destino recebe alterações de associação incrementais em vez de instantâneos completos do público-alvo.

A ativação de transmissão é o padrão para a maioria dos destinos de plataforma de anúncios no catálogo RT-CDP. O conector de destino manipula a autenticação da API, a limitação de taxa e a lógica de repetição automaticamente.

**Principais considerações:**

- A avaliação do público-alvo deve usar a avaliação de streaming ou de borda (públicos somente em lote não podem alimentar destinos de streaming em tempo real)
- Nem todas as expressões de segmento se qualificam para avaliação de streaming — agregações complexas, consultas de várias entidades e determinadas funções baseadas em tempo exigem batch
- Os limites de taxa da API do parceiro de destino podem afetar a taxa de transferência durante eventos de qualificação de grande público
- As atualizações do atributo de perfil são enviadas junto com as alterações da associação, mantendo os dados de destino atualizados

**Vantagens:**

- Atualização quase em tempo real do público-alvo no destino (minutos, não horas)
- Atualizações incrementais reduzem o volume de transferência de dados em comparação a exportações completas
- Manuseio automático de eventos de qualificação e desqualificação
- A maioria dos destinos de plataformas de anúncios suporta transmissão nativamente

**Limitações:**

- Requer definições de segmento com qualificação de streaming (conjunto de funções de segmento limitado)
- Nenhum controle sobre o formato de arquivo ou a estrutura de exportação — formato de dados determinado pelo conector de destino
- Não é possível exportar para destinos de armazenamento baseados em arquivo (S3, Azure Blob, SFTP)
- Os limites de taxa da API de destino podem limitar as alterações de alto volume

**Experience League:**

- [Ativar públicos para destinos de transmissão](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Catálogo de destinos de transmissão](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/catalog/overview)

### Opção B: Ativação de destino em lote (exportação de arquivo)

**Recomendado para:** Exportações programadas de público-alvo para armazenamento na nuvem, data warehouses ou sistemas que consomem importações baseadas em arquivos — Amazon S3, Azure Blob Storage, Google Cloud Storage, SFTP, Data Landing Zone.

**Como funciona:**

A ativação do destino de lote avalia os públicos-alvo em uma cadência agendada e exporta os resultados como arquivos (CSV, JSON ou Parquet) para o destino de armazenamento configurado. A exportação pode incluir instantâneos completos do público-alvo ou alterações incrementais (novas qualificações e desqualificações desde a última exportação).

A implementação envolve a configuração de uma conexão de destino baseada em arquivo com credenciais de armazenamento, preferências de formato de arquivo (delimitador, compactação, convenção de nomenclatura) e um agendamento de exportação (diariamente, a cada 3 horas, a cada 6 horas etc.). Cada execução de exportação gera arquivos contendo a associação de público e quaisquer atributos de perfil mapeados.

Essa abordagem oferece suporte à mais ampla variedade de consumidores downstream, pois a troca de dados baseada em arquivos é universalmente compatível. Também é a única opção para casos de uso de armazenamento em nuvem e enriquecimento do data warehouse.

**Principais considerações:**

- A avaliação do público-alvo pode usar qualquer método (lote, streaming ou borda) — a própria exportação é executada em um agendamento, independentemente
- As convenções de formato de arquivo, compactação e nomenclatura podem ser configuradas por destino
- Oferece suporte a exportações incrementais (somente alterações) e exportações completas (instantâneo completo do público-alvo)
- Exportar intervalos de granularidade de agendamento de 3 horas para diariamente

**Vantagens:**

- Controle completo do formato de arquivo de exportação (CSV, JSON, Parquet), compactação e nomenclatura
- Compatível com qualquer sistema downstream que possa consumir arquivos
- Oferece suporte aos modos de exportação incremental e completo
- Pode exportar públicos-alvo com qualquer método de avaliação (incluindo segmentos somente em lote com lógica de segmentação complexa)
- Oferece suporte para execuções de exportação ad-hoc (sob demanda) fora do cronograma regular

**Limitações:**

- A latência é inerentemente maior — os dados do público-alvo chegam ao destino de acordo com uma programação, não em tempo real
- Exportações baseadas em arquivo exigem que o sistema de destino processe e assimile os arquivos
- Custos de armazenamento no destino para arquivos exportados
- Maiores volumes de dados por exportação em comparação às atualizações de transmissão incrementais

**Experience League:**

- [Ativar públicos para destinos de exportação de perfil em lote](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Catálogo de destinos baseado em arquivo](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/cloud-storage)

### Opção C: Ativação de vários destinos

**Recomendado para:** Ativar o mesmo público-alvo para vários destinos simultaneamente — por exemplo, enviar uma lista de supressão para todas as plataformas de anúncio, sincronizar um segmento de alto valor para as plataformas de CRM e de anúncio ou coordenar o alcance do público-alvo em vários parceiros de mídia.

**Como funciona:**

A ativação de vários destinos não é um mecanismo técnico separado, mas uma composição das Opções A e B aplicadas ao mesmo público-alvo em várias conexões de destino. O mesmo público é ativado para dois ou mais destinos, cada um com sua própria configuração de conexão, mapeamento de campo e agendamento.

Cada conexão de destino opera independentemente — uma ativação de transmissão para o Facebook e uma exportação em lote para o S3 podem ser executadas simultaneamente a partir do mesmo público-alvo de origem. Os mapeamentos de campo são configurados por destino, portanto, atributos diferentes podem ser enviados para sistemas diferentes com base no que cada destino requer e no que as políticas de governança permitem.

Esse é um padrão de produção comum para organizações que operam em várias plataformas de anúncios, mantêm a sincronização do CRM junto com a ativação de mídia ou precisam distribuir dados do público-alvo para sistemas operacionais e analíticos.

**Principais considerações:**

- Cada destino tem mapeamento de campo, programação e avaliação de governança independentes
- As políticas de controle são aplicadas por destino — diferentes atributos podem ser permitidos para diferentes tipos de destino
- Um único público-alvo pode ser ativado para uma combinação de destinos de streaming e lote simultaneamente
- A adição de um novo destino não requer alterações em ativações existentes

**Vantagens:**

- Distribuição coordenada de público em todos os sistemas externos a partir de uma única definição de público
- A configuração independente por destino permite mapeamentos e agendamentos otimizados
- A imposição de controle por destino garante a conformidade em diferentes tipos de destino
- Centraliza o gerenciamento de público-alvo ao mesmo tempo que suporta a ativação distribuída

**Limitações:**

- Mais conexões de destino para configurar, autenticar e manter
- A complexidade do monitoramento aumenta com cada destino — as falhas de ativação devem ser rastreadas por destino
- O uso de licenças (perfis ativados) pode contar por destino dependendo das autorizações
- A manutenção de mapeamento de campos em vários destinos requer coordenação

**Experience League:**

- [Visão geral dos destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/catalog/overview)

### Comparação de opções

| Critérios | Opção A: Streaming | Opção B: Lote (Exportação de arquivo) | Opção C: Vários destinos |
| --- | --- | --- | --- |
| Melhor para | Direcionamento e supressão de plataformas de anúncios em tempo real | Enriquecimento do data warehouse, integração do sistema baseado em arquivos | Distribuição coordenada de público em várias plataformas |
| Complexo | Baixa | Médio | Alta |
| Latência | Minutos (quase em tempo real) | Horas (agendadas) | Combinação de minutos e horas por destino |
| Controle de formato de arquivo | Nenhum (o destino determina o formato) | Completo (CSV, JSON, Parquet, compactação, nomenclatura) | Por destino |
| Avaliação de público | É necessário streaming ou borda | Qualquer método (lote, streaming, borda) | Requisitos por destino |
| Exige | Conector de destino de transmissão, segmento qualificado para transmissão | Conector de destino baseado em arquivo, credenciais de armazenamento | Vários conectores e credenciais de destino |
| Governança | Avaliação de destino único | Avaliação de destino único | Avaliação por destino |

### Escolha a opção certa

Use a seguinte lógica de decisão para selecionar a abordagem de implementação correta:

1. **Quantos destinos você precisa?** Se for necessário ativar o mesmo público-alvo para dois ou mais destinos, você estará implementando a Opção C (que compõe as Opções A e B por destino). Vá para as perguntas 2 e 3 para cada destino.

2. **O destino oferece suporte à transmissão?** Se o destino for uma plataforma de anúncios (Facebook, Google Ads, LinkedIn, The Trade Desk) ou integração de parceiros com uma API de transmissão, use a Opção A para esse destino. Se o destino for armazenamento na nuvem (S3, Azure Blob, GCS, SFTP) ou um sistema que consome arquivos, use a Opção B.

3. **Com que rapidez o público-alvo deve chegar ao destino?** Se a associação do público-alvo precisar refletir no destino em minutos (por exemplo, supressão em tempo real durante campanhas ativas), use a Opção A. Se a entrega diária ou de várias horas for suficiente (por exemplo, atualização semanal do data warehouse, sincronização em lote de CRM), use a Opção B.

4. **Seu público-alvo usa lógica de segmentação complexa?** Se a definição do público-alvo incluir agregações de vários eventos, janelas de tempo grandes ou funções que não se qualifiquem para avaliação de fluxo contínuo, use a Opção B (destinos em lote) ou garanta que os destinos da Opção A também recebam públicos-alvo avaliados em lote em uma programação.

## Fases de implementação

A implementação segue essas fases. Cada fase inclui detalhes de configuração, pontos de decisão e links para a documentação da Experience League.

### Fase 1: Avaliação do público-alvo

**Função do aplicativo:** RT-CDP: Avaliação de público-alvo, RT-CDP: Composição de público-alvo

**O que você configurará:** Defina o público-alvo que será ativado para destinos. Isso inclui especificar os critérios de público-alvo (quais perfis se qualificam), selecionar o método de avaliação (a rapidez com que as atualizações de associação são feitas) e validar a população do público-alvo. Esse é o ponto de partida para toda a ativação — sem um público-alvo definido e avaliado, não há nada para ser ativado.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: método de criação de público-alvo**
>
>Como o público-alvo deve ser definido?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Construtor de segmentos (com base em regras) | Definição de público-alvo padrão usando atributos de perfil, eventos comportamentais e condições de associação de segmento | A definição de regra mais flexível; oferece suporte à avaliação de streaming e borda para expressões elegíveis; ideal para públicos de condição única ou moderadamente complexos |
>| Composição de público | O público-alvo requer a combinação, classificação, divisão ou exclusão de públicos-alvo existentes | Tela visual para operações sequenciais; os resultados são avaliados somente em lote; máximo de 10 blocos de composição por tela |
>| Composição de público-alvo federado | Os critérios de público-alvo devem ser avaliados em relação aos dados em data warehouses externos sem assimilá-los na AEP | Consulta diretamente bancos de dados externos; evita a duplicação de dados; exige licença do Federated Audience Composition |

>[!NOTE]
>
>**Decisão: método de avaliação**
>
>Com que rapidez os perfis devem entrar e sair do público-alvo?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Lote | Campanhas programadas, atualizações diárias de público ou lógica de segmentação complexa que não se qualifica para transmissão | Processa até 24 milhões de perfis por trabalho; todas as funções de segmentação são compatíveis; é executado em um agendamento (padrão diário ou agendamento cron personalizado) |
>| Streaming | Alterações na associação do público-alvo em tempo real necessárias para ativação do destino de transmissão ou casos de uso acionados por eventos | Quase em tempo real (segundos a minutos); conjunto de funções de segmentação limitado — eventos simples, comparações de atributos e janelas de tempo limitadas somente; sem consultas de várias entidades |
>| Edge | Personalização de mesma página ou qualificação de público-alvo instantânea necessária na borda | Latência de milissegundos; conjunto de regras mais restritivo — somente atributos de perfil e verificações de associação de segmento simples; usado principalmente para personalização no site (menos comum para ativação de destino) |

>[!NOTE]
>
>**Decisão: política de mesclagem**
>
>Qual política de mesclagem a avaliação de público-alvo deve usar?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Carimbo de data e hora ordenado (padrão) | Na maioria dos casos de uso, os dados recentes devem ter prioridade quando os fragmentos de perfil estiverem em conflito | Mais comum; usa o valor de atributo atualizado mais recentemente |
>| Prioridade de conjunto de dados | Fontes de dados específicas devem substituir outras, independentemente do carimbo de data e hora | Exige a definição de uma ordem de prioridade do conjunto de dados; útil quando um sistema de registro de CRM deve sempre substituir os dados coletados na Web |

Navegação da **interface:** Cliente > Públicos-alvo > Criar público-alvo > Criar regra (para o Construtor de segmentos) ou Compor público-alvo (para a Composição de público-alvo)

**Detalhes de configuração da chave:**

- Defina critérios de público-alvo com base no caso de uso: atributos de perfil, eventos comportamentais, associação de segmento ou condições baseadas em tempo
- Aplique regras de supressão para excluir perfis que não devem ser ativados (por exemplo, recém-convertidos, inscrição cancelada globalmente)
- Validar o tamanho do público-alvo antes de prosseguir com a ativação
- Confirme se o método de avaliação está alinhado ao tipo de destino selecionado na Fase 2

**Onde as opções divergem:**

**Para Opção A (Ativação de Destino de Streaming):**
O público-alvo deve usar transmissão ou avaliação de borda para fornecer atualizações de associação em tempo real. Verifique se a expressão de regra de segmento se qualifica para avaliação de fluxo — evite funções de agregação com base em tempo, consultas de várias entidades e `inSegment()` referências a segmentos somente em lote.

**Para Opção B (Ativação de Destino de Lote):**
Qualquer método de avaliação funciona. A avaliação em lote é a opção mais comum, pois a própria exportação é executada de acordo com um agendamento. Confirme se existe um agendamento de avaliação em lote na sandbox ou crie um.

**Para Opção C (Ativação de Vários Destinos):**
O método de avaliação deve acomodar o destino mais exigente. Se qualquer destino exigir a transmissão, o público-alvo deverá usar a avaliação de transmissão. Se todos os destinos forem em lote, a avaliação em lote é suficiente.

**Documentação do Experience League:**

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-builder)
- [Referência do Profile Query Language](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/pql/overview)
- [Segmentação de transmissão](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentação de borda](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Visão geral da composição de público-alvo](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/audience-composition)
- [Métodos de avaliação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/home#evaluation-methods)


### Fase 2: configuração de destino

**Função do aplicativo:** RT-CDP: Configuração de Destino

**O que você configurará:** Estabeleça conexões autenticadas com os destinos externos onde os públicos-alvo serão publicados. Isso inclui selecionar o destino no catálogo, fornecer credenciais de autenticação e configurar parâmetros específicos do destino, como formato de arquivo, local de armazenamento e agendamento de exportação. Cada destino requer sua própria configuração de conexão.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: Tipo de destino**
>
>Onde os públicos-alvo devem ser entregues?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Destino do Advertising (transmissão) | Direcionamento ou supressão em plataformas de anúncios (Facebook, Google Ads, LinkedIn, The Trade Desk etc.) | Conectores de transmissão, atualizações de associação em tempo quase real, correspondência de identidade por email com hash, telefone ou IDs de dispositivo |
>| Destino de armazenamento na nuvem (lote) | Exportar para S3, Azure Blob, GCS, SFTP ou Zona de aterrissagem de dados para enriquecimento do data warehouse | Exportação baseada em arquivo; formato configurável (CSV, JSON, Parquet); cadência agendada |
>| Destino do CRM | Sincronizar públicos com o Salesforce, Microsoft Dynamics ou HubSpot para capacitação de vendas | Normalmente, transmissão contínua; requer mapeamento de campo específico de CRM; pode precisar de permissões de administrador do CRM |
>| Destino do parceiro de dados | Compartilhar dados do público-alvo com parceiros de medição ou direcionamento | Varia de acordo com o parceiro; analise as implicações de controle do compartilhamento externo de dados |
>| Destino personalizado (Destination SDK) | Sistema de destino não disponível no catálogo | Requer a criação de um destino personalizado usando a Destination SDK; maior esforço de implementação |

>[!NOTE]
>
>**Decisão: método de autenticação**
>
>Quais credenciais são necessárias para o destino?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| OAuth 2.0 | Plataformas de publicidade e destinos SaaS (Facebook, Google, Salesforce) | Requer fluxo de autorização inicial; tokens são atualizados automaticamente; mais comum para destinos de transmissão |
>| Chave de acesso / Chave secreta | Armazenamento na nuvem (S3, Azure Blob) | Credenciais estáticas; a rotação deve ser planejada; adequado para destinos baseados em arquivo |
>| Conta de serviço / Chave de API | APIs de parceiros e integrações personalizadas | Requer provisionamento de credenciais do parceiro de destino |
>| String de conexão | Destinos com base em Azure | Cadeia de caracteres única contendo todos os parâmetros de conexão |

>[!NOTE]
>
>**Decisão: Tipo de exportação (somente destinos em lote)**
>
>Como os dados do público-alvo devem ser empacotados para exportação?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Exportação incremental | Apenas novas qualificações e desqualificações desde a última exportação | Menores tamanhos de arquivo; processamento mais rápido no destino; requer que o sistema de destino mantenha o estado |
>| Exportação completa | Instantâneo completo do público em cada execução | Arquivos maiores; o destino obtém uma visão completa a cada vez; mais simples para sistemas que fazem uma substituição completa |

**Navegação da interface do usuário:** Conexões > Destinos > Catálogo > [Selecionar destino] > Configurar

**Detalhes de configuração da chave:**

- Procurar o catálogo de destino e selecionar o destino
- Fornecer credenciais de autenticação e testar a conexão
- Para destinos em lote: configurar o formato de arquivo (CSV, JSON, Parquet), compactação, modelo de nomenclatura de arquivo e programação de exportação
- Para destinos de transmissão: a conexão normalmente é estabelecida por meio do fluxo de autorização OAuth
- Verifique se o status da conexão de destino aparece como ativo antes de prosseguir para a ativação

**Onde as opções divergem:**

**Para Opção A (Ativação de Destino de Streaming):**
Selecione um destino de transmissão no catálogo (categorias Advertising ou Social). Conclua o fluxo de autorização OAuth. A conexão estará pronta para ativação assim que a autorização for confirmada.

**Para Opção B (Ativação de Destino de Lote):**
Selecione um destino baseado em arquivo no catálogo (categoria Armazenamento em nuvem). Configure o caminho de armazenamento, o formato de arquivo, a compactação, a convenção de nomenclatura e o agendamento de exportação. Teste a conexão verificando o acesso de gravação ao local de armazenamento.

**Para Opção C (Ativação de Vários Destinos):**
Repita essa fase para cada destino. Cada conexão é independente — você pode ter uma combinação de destinos de streaming e lote. Documente a autenticação e a configuração de cada conexão para referência operacional.

**Documentação do Experience League:**

- [Catálogo de destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/catalog/overview)
- [Visão geral dos destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/home)
- [Ativar públicos para destinos de exportação de perfil em lote](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Ativar públicos para destinos de transmissão](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Visão geral do Destination SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/destination-sdk/overview)
- [Opções de configuração do Destination SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/destination-sdk/functionality/configuration-options)


### Fase 3: Ativação do público-alvo

**Função do aplicativo:** RT-CDP: Audience Activation

**O que você configurará:** publique o público avaliado no destino configurado criando o fluxo de dados de ativação. Isso envolve selecionar quais públicos-alvo serão ativados, mapear atributos de perfil para campos de destino e configurar o cronograma de exportação. O fluxo de dados de ativação conecta o público-alvo de origem ao destino e gerencia a entrega de dados em andamento.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: Mapeamento de atributo**
>
>Quais atributos de perfil devem ser incluídos na ativação?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Somente campos de identidade | O destino só precisa corresponder aos perfis (por exemplo, associação de público-alvo em plataformas de anúncios) | Transferência mínima de dados; mais seguro quanto à privacidade; típico para direcionamento e supressão de plataforma de anúncios |
>| Identidade + atributos de perfil | O destino precisa de atributos de enriquecimento para personalização ou segmentação (por exemplo, sincronização de CRM, compartilhamento de parceiros) | Mais dados transferidos; exige análise de governança para cada atributo; verifique os rótulos de uso de dados em relação à ação de marketing de destino |
>| Identidade + atributos calculados | Os benefícios de destino derivam de pontuações ou agregações (por exemplo, nível de valor vitalício, pontuação de propensão para direcionamento de parceiros) | Requer a configuração de atributos computados; enriquecimento de alto valor para sistemas downstream |

>[!NOTE]
>
>**Decisão: exportar agendamento (somente destinos em lote)**
>
>Com que frequência os dados de público-alvo devem ser exportados?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Diariamente | Cadência de atualização padrão; a maioria dos casos de uso em lote | Equilibra a atualização com o custo de processamento; padrão mais comum |
>| A cada 3 a 6 horas | Casos de uso com maior frequência, como otimização de campanha intradiária | Geração de arquivos mais frequente; maior carga de armazenamento e processamento no destino |
>| Sob demanda (ad-hoc) | Exportação única ou ativação urgente fora do ciclo | O acionador manual ignora a programação; útil para testes ou necessidades urgentes de campanha |

**Navegação da interface do usuário:** Conexões > Destinos > Procurar > [Selecionar destino] > Ativar públicos

**Detalhes de configuração da chave:**

- Selecione um ou mais públicos-alvo para ativar para o destino
- Mapear atributos de perfil e campos de identidade para campos específicos de destino
- Para destinos de transmissão: confirmar o mapeamento de namespace de identidade (por exemplo, email com hash para extern_id do Facebook)
- Para destinos em lote: configurar o agendamento de exportação, selecionar o modo de exportação incremental ou completo e definir a primeira data de exportação
- Revise o resumo de ativação para confirmar todos os mapeamentos e agendamentos antes de publicar

**Onde as opções divergem:**

**Para Opção A (Ativação de Destino de Streaming):**
Selecione os públicos-alvo e mapeie os namespaces de identidade para os campos de identidade de destino. A ativação começa imediatamente após a publicação — a associação do público-alvo altera o fluxo para o destino em tempo quase real. Nenhuma programação de exportação é necessária; a ativação é contínua.

**Para Opção B (Ativação de Destino de Lote):**
Selecione os públicos, mapeie os atributos de perfil e configure o cronograma de exportação. Escolha entre os modos de exportação incremental e completo. Opcionalmente, acione uma exportação ad-hoc para entrega imediata fora do cronograma regular.

**Para Opção C (Ativação de Vários Destinos):**
Repita o fluxo de trabalho de ativação para cada destino. O mesmo público pode ser ativado para vários destinos com mapeamentos de atributos diferentes por destino. Por exemplo, envie somente emails com hash para plataformas de anúncio, mas inclua atributos demográficos ao CRM.

**Documentação do Experience League:**

- [Ativar públicos para destinos de transmissão](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Ativar públicos para destinos de exportação de perfil em lote](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Ativar públicos-alvo sob demanda para destinos em lote](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/api/ad-hoc-activation-api)
- [Monitorar fluxos de dados para destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/dataflows/ui/monitor-destinations)


### Fase 4: validação de governança

**Função do aplicativo:** RT-CDP: Consentimento e Imposição de Governança

**O que você configurará:** Verifique se as políticas de governança e as preferências de consentimento estão sendo aplicadas corretamente antes e durante a ativação. Essa fase garante que os dados restritos (PII, atributos confidenciais) não sejam enviados a destinos não autorizados e que os perfis sem consentimento válido sejam excluídos da ativação. A aplicação de governança ocorre automaticamente no momento da ativação, mas a validação proativa impede ativações bloqueadas e violações de conformidade.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: abordagem de imposição de governança**
>
>Quando a conformidade de governança deve ser validada?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Pró-ativo (pré-ativação) | Recomendado para todas as implementações, especialmente quando ativado para sistemas externos de terceiros | Revisar rótulos e políticas de uso de dados antes de configurar mapeamentos de campo; evitar falhas de ativação e garantir a conformidade desde o início |
>| Reativo (no momento da ativação) | Quando as políticas de governança já estão bem estabelecidas e a equipe está confiante na conformidade | A Platform impõe políticas automaticamente na ativação; as violações bloqueiam a ativação ou excluem atributos restritos; pode causar falhas inesperadas se as políticas não forem bem compreendidas |

>[!NOTE]
>
>**Decisão: filtragem por consentimento**
>
>Como as preferências de consentimento devem afetar a ativação?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Imposição de consentimento habilitada | Obrigatório ao ativar para destinos de publicidade ou marketing nos quais o consentimento é legalmente exigido | Perfis sem consentimento válido (consentimentos.marketing.{channel}.val = &#39;y&#39;) são excluídos automaticamente da ativação; requer que os dados de consentimento sejam assimilados |
>| Sem filtragem de consentimento | Destinos de uso interno ou exportações de análises em que o consentimento não se aplica à transferência de dados | Adequado somente quando o uso de dados não constitui uma ação de marketing que requer consentimento; consulte a equipe jurídica/de privacidade |

**Navegação da interface do usuário:** Privacidade > Políticas > Políticas de consentimento (para revisão de consentimento); Governança de dados > Políticas (para revisão de política de uso de dados)

**Detalhes de configuração da chave:**

- Revisar os rótulos de uso de dados aplicados aos conjuntos de dados e campos de esquema que estão sendo ativados
- Verifique se as políticas de governança estão ativas para a ação de marketing associada ao destino (por exemplo, &quot;Exportar para terceiros&quot; para plataformas de anúncios)
- Confirme se os campos de consentimento estão preenchidos nos perfis e se a imposição de consentimento está habilitada para os canais relevantes
- Se forem detectadas violações de política, resolva removendo campos restritos do mapeamento de destino ou selecionando um destino alternativo

**Documentação do Experience League:**

- [Visão geral da governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/home)
- [Aplicação de política](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/enforcement/overview)
- [Visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview)
- [Consentimento e preferências](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)
- [Aplicação da política de consentimento](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/policies/user-guide)


### Fase 5: Monitoramento e validação

**Função de aplicativo:** Monitoramento e Observação

**O que você configurará:** Configure o monitoramento contínuo para fluxos de dados de ativação, configure alertas para falhas, valide a população de público-alvo nos destinos e rastreie o uso de licenças. O monitoramento é essencial para ativações de produção em que as falhas de delivery afetam diretamente o desempenho da campanha e o gasto com mídia.

**Detalhes de configuração da chave:**

- Revise o status de execução do fluxo de dados para cada destino ativo para confirmar se os públicos-alvo estão sendo entregues com êxito
- Configure alertas para falhas de ativação de destino, atrasos de fluxo de dados e anomalias no preenchimento do público
- Rastrear perfis exportados vs. perfis que falharam por execução do fluxo de dados
- Monitorar as taxas de correspondência do público-alvo no destino (onde o relatório de destino está disponível)
- Revisar o uso da licença para rastrear o volume do perfil ativado em relação às autorizações

**Navegação da interface do usuário:** Conexões > Destinos > Procurar > [Selecionar destino] > Execuções de fluxo de dados (para monitoramento de ativação); Alertas > Regras de alerta > Assinar (para configuração de alerta); Administração > Uso de licença (para rastreamento de licença)

**Documentação do Experience League:**

- [Monitorar fluxos de dados para destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/dataflows/ui/monitor-destinations)
- [Visão geral de alertas](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/alerts/overview)
- [Visão geral dos Insights de observação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/home)
- [Painel de uso da licença](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/license-usage-dashboard)

## Considerações de implantação

Analise as seguintes considerações antes e durante a implementação.

### Medidas de proteção e limites

- **Limite de definição de segmento:** Máximo de 4.000 definições de segmento por sandbox — [Medidas de proteção de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/guardrails)
- **Fluxos de dados por destino:** Máximo de 100 fluxos de dados por conexão de destino — [Medidas de proteção de destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/guardrails)
- **Tamanho do arquivo de exportação em lote:** os destinos baseados em arquivo têm limites máximos de tamanho de arquivo de exportação; públicos-alvo grandes são automaticamente divididos em vários arquivos
- **Taxa de transferência de destino de streaming:** limites de taxa de transferência por segundo são definidos por cada parceiro de destino; alterações de alto volume de público podem ser limitadas
- **Capacidade de avaliação em lote:** Até 24 milhões de perfis por trabalho de avaliação de segmento por padrão
- **Composição de público-alvo:** Máximo de 10 blocos de composição por tela; públicos-alvo compostos são avaliados somente em lote
- **Gráfico de identidade:** Máximo de 50 identidades por gráfico — [Medidas de proteção do Serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/guardrails)
- **Atributos computados:** Máximo de 25 atributos computados por sandbox — [Medidas de proteção de atributos computados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/computed-attributes/overview#guardrails)
- **Visão geral das medidas de proteção de ativação:** [Medidas de proteção de ativação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/guardrails)

### Armadilhas comuns

- **Segmento de streaming com lógica de regra inelegível:** Definindo um público com funções de agregação complexas ou consultas de várias entidades e esperando avaliação de streaming. Esses segmentos retornam silenciosamente à avaliação em lote, causando latência inesperada. Prevenção: analise os requisitos de qualificação de transmissão antes de definir o público-alvo.

- **Nenhum perfil exportado devido à filtragem de consentimento:** Todos os perfis no público-alvo não têm valores de consentimento válidos, fazendo com que todo o público-alvo seja filtrado no momento da ativação. Prevenção: verifique se a assimilação de dados de consentimento está operacional e se os campos de consentimento estão preenchidos antes da ativação.

- **Ativação de bloqueio de política de governança inesperadamente:** Os rótulos de uso de dados em campos de esquema disparam violações de política que impedem a ativação. Prevenção: avalie a conformidade da governança de forma proativa (Fase 4) antes de configurar os mapeamentos de campo. Revise quais rótulos são herdados do esquema.

- **Expiração da credencial de destino:** tokens OAuth ou chaves de API expiram, causando falhas de ativação sem alerta imediato. Prevenção: configure alertas para falhas de ativação de destino e estabeleça um agendamento de rotação de credenciais.

- **Namespaces de identidade incompatíveis:** O namespace de identidade configurado no mapeamento de ativação não corresponde ao que o destino espera (por exemplo, enviar email de texto sem formatação quando o destino requer um email com hash SHA-256). Prevenção: analise a documentação de destino quanto aos formatos de identidade necessários antes de configurar o mapeamento.

- **Erros de mapeamento de campo que causam falhas de exportação:** Mapeamento de um atributo de perfil para um campo de destino com um tipo ou formato de dados incompatível. Prevenção: teste a ativação com um pequeno público-alvo primeiro e revise os detalhes da execução do fluxo de dados para mapear erros antes de dimensionar para públicos-alvo de produção.

- **Desvio de população de público entre RT-CDP e destino:** O contagem de público-alvo no RT-CDP não corresponde à contagem no destino devido a diferenças de correspondência de identidade, lógica de desduplicação de destino ou tempo. Esse é o comportamento esperado — prevenção: documente os referenciais da taxa de correspondência esperada por destino e monitore desvios significativos.

### Práticas recomendadas

- **Comece com um público-alvo de teste:** Ative um público-alvo de teste pequeno e bem compreendido para cada novo destino antes de ativar os públicos de produção. Validar mapeamentos de campo, correspondência de identidades e métricas de entrega com o público-alvo de teste.

- **Governança de camada mais cedo:** aplique rótulos de uso de dados e configure políticas de governança antes de configurar ativações de destino. Isso evita ativações bloqueadas e garante a conformidade desde o início.

- **Usar exportações incrementais para destinos em lote:** exportações incrementais reduzem o tamanho dos arquivos, aceleram o processamento no destino e minimizam os custos de armazenamento. Use exportações completas somente quando o sistema de destino exigir uma substituição completa do público-alvo.

- **Convenções de nomenclatura padronizadas:** Estabeleça uma nomenclatura consistente para públicos, conexões de destino e fluxos de dados em toda a organização. Inclua o caso de uso, destino e método de avaliação nos nomes (por exemplo, &quot;Suppression_ExistingCustomers_Facebook_Streaming&quot;).

- **Taxas de correspondência do monitor:** Rastreie a proporção de perfis exportados da RT-CDP para perfis correspondentes em cada destino. Quedas significativas na taxa de correspondência podem indicar problemas de resolução de identidade, problemas de credencial ou alterações na API de destino.

- **Coordenar a supressão entre destinos:** Ao usar públicos de supressão (por exemplo, excluir clientes existentes de campanhas de aquisição), ative o público de supressão para todas as plataformas de anúncios relevantes simultaneamente para manter a consistência.

- **Revisar e remover ativações inativas:** Revisar periodicamente os fluxos de dados de destino e desativar públicos que não são mais necessários. As ativações inativas consomem a capacidade da licença e adicionam a sobrecarga do monitoramento.

### Decisões de compensação

>[!NOTE]
>
>**Contrapartida: atualização de público-alvo vs. flexibilidade de segmentação**
>
>A avaliação de transmissão fornece atualizações de público-alvo quase em tempo real, mas restringe as funções da regra de segmento que você pode usar. A avaliação em lote oferece suporte ao conjunto completo de funções da regra de segmento, mas introduz a latência (horas em vez de minutos).
>
>- **Favorecimento da transmissão:** Casos de uso em tempo real nos quais a associação de público-alvo deve refletir no destino em minutos (supressão de campanha ativa, redirecionamento em tempo real)
>- **O lote favorece:** lógica de público-alvo complexa que requer funções de agregação, consultas de várias entidades ou condições de janela de tempo grandes (camadas de valor vitalício, segmentos comportamentais multitoque)
>- **Recomendação:** use a avaliação de streaming para públicos ativados para destinos de streaming em que a atualização em tempo real impulsiona o valor comercial. Use a avaliação em lote para públicos-alvo complexos ativados para destinos baseados em arquivo ou quando a atualização diária for suficiente. Para públicos-alvo que precisam de ambas, considere criar duas versões: um segmento de transmissão simplificado para ativação em tempo real e um segmento em lote abrangente para enriquecimento periódico.

>[!NOTE]
>
>**Contrapartida: exportação mínima de dados vs. mapeamento de atributos avançados**
>
>A exportação somente de campos de identidade (email com hash, ID de dispositivo) minimiza a exposição de dados e simplifica o controle. A exportação de atributos de perfil adicionais (demografia, nível de valor, pontuação de engajamento) enriquece o destino, mas aumenta a complexidade da governança e a responsabilidade pelos dados.
>
>- **Exportação mínima favorece:** abordagem de privacidade em primeiro lugar; menor risco de governança; mapeamento de campos mais simples; suficiente para a maioria dos casos de uso de direcionamento e supressão de plataforma de anúncios
>- **A exportação avançada favorece:** personalização downstream no destino; enriquecimento de CRM; compartilhamento de dados de parceiros que requer detalhes no nível de atributo
>- **Recomendação:** Use como padrão o mínimo de exportações somente de identidade para destinos de publicidade. Adicione atributos de perfil somente quando o caso de uso de destino exigir especificamente e a revisão da governança confirmar a conformidade. Use atributos computados para fornecer valores de enriquecimento agregados, menos sensíveis, em vez de PII brutas.

>[!NOTE]
>
>**Contrapartida: único público-alvo por destino vs. fluxos de dados consolidados de vários públicos-alvo**
>
>A ativação de cada público como um fluxo de dados separado fornece monitoramento granular e de isolamento. Ativar vários públicos-alvo por meio de um único fluxo de dados para um destino simplifica o gerenciamento, mas reduz o isolamento.
>
>- **Fluxos de dados separados favorecem:** Monitoramento independente, solução de problemas mais fácil, capacidade de pausar ativações de públicos individuais sem afetar os outros
>- **Os fluxos de dados consolidados favorecem:** Menos conexões para manter, gerenciamento simplificado de credenciais, redução da sobrecarga operacional
>- **Recomendação:** use fluxos de dados consolidados ao ativar vários públicos relacionados para o mesmo destino (por exemplo, todos os segmentos de supressão do Facebook). Use fluxos de dados separados quando os públicos-alvo tiverem SLAs diferentes, mapeamentos de atributos diferentes ou quando o isolamento de falha for crítico.

## Documentação relacionada

**Destinos**

- [Visão geral dos destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/catalog/overview)
- [Ativar públicos para destinos de transmissão](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Ativar públicos para destinos de exportação de perfil em lote](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Ativar públicos-alvo sob demanda para destinos em lote](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/api/ad-hoc-activation-api)
- [Medidas de proteção de destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/guardrails)
- [Visão geral do Destination SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/destination-sdk/overview)

**Públicos-alvo e segmentação**

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-builder)
- [Referência do Profile Query Language](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/pql/overview)
- [Segmentação de transmissão](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentação de borda](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Visão geral da composição de público-alvo](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/audience-composition)
- [Proteções de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/guardrails)

**Identidade e perfil**

- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/home)
- [Visão geral dos namespaces de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/namespaces)
- [Regras de vinculação do gráfico de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/identity-linking-logic)
- [Visão geral do perfil](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/home)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/merge-policies/overview)

**Modelagem de dados e esquemas**

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/home)
- [Noções básicas de composição de esquema](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/schema/composition)

**Governança de dados**

- [Visão geral da governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/home)
- [Visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview)
- [Políticas de governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/policies/overview)
- [Aplicação de política](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/enforcement/overview)
- [Consentimento e preferências](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)

**Monitoramento e observabilidade**

- [Monitorar fluxos de dados para destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/dataflows/ui/monitor-destinations)
- [Visão geral de alertas](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/alerts/overview)
- [Visão geral dos Insights de observação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/home)
- [Painel de uso da licença](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/license-usage-dashboard)

**Atributos computados**

- [Visão geral de atributos computados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/computed-attributes/overview)
- [Guia da interface de atributos computados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/computed-attributes/ui)

**Fontes e coleção de dados**

- [Visão geral das fontes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/home)
- [Visão geral do Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/web-sdk/home)
- [Configurar sequências de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/datastreams/configure)

**Administração**

- [Visão geral de sandboxes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/home)
- [Visão geral do controle de acesso](https://experienceleague.adobe.com/pt-br/docs/experience-platform/access-control/home)
- [Controle de acesso baseado em atributos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/access-control/abac/overview)

**Medidas de proteção**

- [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/guardrails)
- [Medidas de proteção do serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/guardrails)
- [Medidas de proteção de ativação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/guardrails)
- [Medidas de proteção de assimilação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/ingestion/guardrails)
