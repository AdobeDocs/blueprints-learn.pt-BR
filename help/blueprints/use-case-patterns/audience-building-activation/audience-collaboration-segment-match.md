---
title: Audience Collaboration
description: Saiba como compartilhar e corresponder segmentos de público-alvo em sandboxes ou organizações usando a Correspondência de segmentos.
solution: Real-Time Customer Data Platform, Experience Platform
exl-id: 7014849c-5e32-4ec3-a531-c0e8ce896f44
source-git-commit: 27f7e230982807ec70ca96af7f737944a6588f27
workflow-type: tm+mt
source-wordcount: '6232'
ht-degree: 1%

---

# Audience Collaboration

Este guia fornece uma referência de implementação abrangente para colaboração de público usando o [!DNL Segment Match] em [!DNL Real-Time CDP] e [!DNL Adobe Experience Platform]. Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam compartilhar e corresponder segmentos de público-alvo em sandboxes ou organizações de maneira segura para a privacidade.

Use este plano para entender as abordagens disponíveis, avaliar compensações e navegar pelo [!DNL Adobe Experience League] para obter instruções detalhadas de configuração.

[!DNL Segment Match] habilita duas ou mais organizações [!DNL Experience Platform] (ou sandboxes dentro de uma organização) a colaborar em dados de público-alvo compartilhando informações de associação de segmento sem expor as PII subjacentes. Os participantes podem estimar sobreposições, compartilhar públicos e ativar perfis correspondentes para destinos downstream.

## Visão geral do caso de uso

As organizações precisam cada vez mais colaborar em dados de público-alvo com parceiros, subsidiárias ou em várias unidades de negócios, mantendo, ao mesmo tempo, controles rigorosos de privacidade. A colaboração de público-alvo atende a essa necessidade habilitando o compartilhamento seguro de segmentos por meio do [!DNL Segment Match] — um recurso no [!DNL Real-Time CDP] que permite que duas ou mais organizações do [!DNL Experience Platform] (ou sandboxes) troquem informações de associação de público usando identificadores com hash e seguros para privacidade.

O cenário de negócios normalmente envolve uma organização (o remetente) que criou um segmento de público-alvo valioso e deseja compartilhá-lo com uma organização parceira (o destinatário) para direcionamento, supressão ou enriquecimento em conjunto. Antes de compartilhar, ambas as partes podem estimar a sobreposição de público-alvo para avaliar o valor. Depois de compartilhado, a organização de recebimento pode ativar o público-alvo correspondente por meio de seus próprios destinos.

Esse padrão é diferente da ativação de público padrão, pois opera entre organizações ou sandboxes, em vez de destinos de publicidade ou marketing externos. Também é diferente de salas de limpeza de dados ou plataformas de colaboração de terceiros, pois opera nativamente dentro do ecossistema do Adobe usando a infraestrutura de identidade do [!DNL Experience Platform].

## Principais objetivos de negócios

Os seguintes objetivos de negócios são compatíveis com esse padrão de caso de uso.

### Adquirir novos clientes

Expanda a base de clientes por meio de campanhas de aquisição direcionadas, públicos semelhantes e otimização de mídia paga. A colaboração de público-alvo permite que as organizações descubram novos pools de clientes potenciais, comparando seus segmentos com os públicos-alvo de parceiros, identificando sobreposições de alto valor e atingindo novos clientes por meio da ativação conjunta.

- **KPIs:** Novos Clientes, Custo de Aquisição do Cliente, Conversão de Cliente Potencial/Cliente Potencial
- [Adquirir novos clientes](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

### Reduza o custo de aquisição do cliente

Melhore a eficiência do direcionamento, elimine clientes existentes das campanhas de aquisição e otimize os gastos com mídia. Ao compartilhar segmentos de supressão entre organizações ou unidades de negócios, as equipes podem evitar o desperdício de gastos em clientes já convertidos e concentrar os orçamentos em clientes realmente novos.

- **KPIs:** Custo de Aquisição do Cliente, Custo por Cliente Potencial, Eficiência
- [Reduza o custo de aquisição do cliente](/help/blueprints/business-objectives/cost-efficiency/reduce-customer-acquisition-cost.md)

### Otimizar o investimento e o ROI do marketing

Melhore o retorno sobre o investimento em marketing através de melhor direcionamento, atribuição, supressão de público-alvo e alocação de orçamento. [!DNL Segment Match] O permite a supressão de públicos-alvo entre organizações e o direcionamento conjunto, o que reduz a duplicação e melhora a precisão.

- **KPIs:** Economia, Custo de Aquisição do Cliente, Receita Incremental
- [Otimizar o investimento e o ROI do marketing](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)

## Exemplo de casos de uso tático

- **Correspondência de público-alvo de editor-anunciante** — Uma marca compartilha seu segmento de cliente de alto valor com um editor de mídia para estimar a sobreposição e direcionar usuários correspondentes com anúncios personalizados, melhorando a relevância da campanha sem expor as PII.
- **Supressão entre marcas em uma empresa controladora** — várias marcas em uma organização principal compartilham segmentos de clientes para impedir que clientes de marcas irmãs existentes façam campanhas de aquisição, reduzindo o desperdício de anúncios.
- **Enriquecimento do público-alvo da rede de mídia de varejo** — Uma retailer compartilha segmentos baseados em compras com parceiros de marca CPG, permitindo que as marcas direcionem compradores comprovados na rede de mídia da retailer com taxas de conversão mais altas.
- **Descoberta de público-alvo de parceiros de marketing conjunto** — Duas marcas não concorrentes avaliam a sobreposição de público-alvo para avaliar o potencial de parceria antes de lançar uma campanha conjunta, usando a estimativa de sobreposição para validar o alinhamento de público-alvo.
- **Compartilhamento de segmentos da cooperação de dados** — as organizações em uma cooperação de dados compartilham segmentos de público com hash para expandir o alcance do direcionamento, mantendo a conformidade com a privacidade e os controles de governança de dados.
- **Federação de público-alvo de várias sandboxes** — uma empresa global compartilha segmentos de público-alvo em sandboxes regionais para permitir o direcionamento consistente do cliente em todos os mercados, respeitando os requisitos regionais de residência de dados.
- **Ativação entre parceiros do programa de fidelidade** — uma coalizão de fidelidade compartilha segmentos de nível de fidelidade com comerciantes participantes, para que cada parceiro possa oferecer promoções apropriadas ao nível para a base de clientes compartilhada.
- **Colaboração de medição e atribuição** — um anunciante compartilha um segmento de conversão com um parceiro de mídia para que o parceiro possa medir a eficácia da campanha comparando os usuários expostos com os conversores.

## Indicadores-chave de desempenho

Os KPIs a seguir ajudam a medir o sucesso das implementações de colaboração de público-alvo.

| KPI | Descrição | Abordagem de medição |
| --- | --- | --- |
| Taxa de sobreposição de público-alvo | Porcentagem de perfis no segmento compartilhado que correspondem entre o remetente e o destinatário | [!DNL Segment Match] relatório de estimativa de sobreposição |
| Tamanho do público correspondente | Número de perfis correspondidos com sucesso e disponíveis para ativação | [!DNL Segment Match] status de compartilhamento e contagem da população de público |
| Aquisição de novos clientes a partir de públicos correspondentes | Novos clientes líquidos adquiridos por meio de campanhas direcionadas a segmentos correspondentes | Rastreamento de conversão em campanhas usando públicos correspondentes |
| Redução de custos de aquisição de clientes | Redução no custo por aquisição ao usar públicos correspondentes versus direcionamento amplo | Análise de custo da campanha comparando o desempenho do público-alvo correspondente com o não correspondente |
| Economias de supressão | Gastos com mídia salvos ao suprimir clientes conhecidos das campanhas de aquisição | Comparação de gastos com mídia antes/depois da supressão |
| Aumento de desempenho da campanha | Melhoria na taxa de conversão, na taxa de cliques ou no engajamento para campanhas usando públicos correspondentes | Teste A/B comparando campanhas de público correspondentes versus controle |
| Tempo para Collaboration | Tempo decorrido desde a iniciação do compartilhamento de segmento até a prontidão para ativação | [!DNL Segment Match] carimbos de data/hora do fluxo de trabalho |

## Padrão do caso de uso

Esse caso de uso segue o padrão do Audience Collaboration.

Compartilhe e associe segmentos de público-alvo em sandboxes ou organizações usando o [!DNL Segment Match].

**Cadeia de funções:** Seleção de Segmentos > Configuração de Correspondência > Estimativa de Sobreposição > Compartilhamento de Público > Ativação

## Aplicativos

Os aplicativos a seguir são usados neste padrão de caso de uso.

- **[!DNL Real-Time CDP]** — Fornece a funcionalidade [!DNL Segment Match] para compartilhamento de público-alvo com privacidade segura, avaliação de público-alvo para criação de segmento e ativação de destino para uso downstream de públicos-alvo correspondentes.
- **[!DNL Adobe Experience Platform]** — Fornece a infraestrutura de dados fundamental, incluindo resolução de identidade, unificação de perfil, governança de dados e imposição de consentimento da qual [!DNL Segment Match] depende.

## Funções básicas

Os seguintes recursos básicos devem estar em vigor para esse padrão de caso de uso. Para cada função, o status indica se ele é tipicamente necessário, se presume ser pré-configurado ou se não é aplicável.

| Função de base | Status | O que deve estar em vigor | Referência do Experience League |
| --- | --- | --- | --- |
| Administração e governança | Obrigatório | As organizações remetente e destinatário devem ter sandboxes provisionadas com funções e permissões apropriadas. Os usuários que gerenciam o [!DNL Segment Match] devem ter permissões para exibir e compartilhar segmentos, configurar conexões e gerenciar feeds de parceiros. As políticas ABAC devem ser configuradas para controlar quais usuários podem iniciar e aceitar compartilhamentos de segmentos. | [Visão geral do controle de acesso](https://experienceleague.adobe.com/pt-br/docs/experience-platform/access-control/home) |
| Preparação e modelagem de dados | Presumido em vigor | Esquemas XDM para perfis e eventos devem existir com os grupos de campos obrigatórios. Conjuntos de dados de perfil e evento devem ser criados e habilitados para [!DNL Real-Time Customer Profile]. O modelo de dados deve aceitar os namespaces de identidade usados para a correspondência de segmentos (normalmente email com hash ou telefone com hash). | [Visão geral do sistema XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/home) |
| Fontes de dados e coleção | Presumido em vigor | Os dados do cliente devem estar fluindo ativamente para [!DNL Experience Platform] por meio de fontes de dados configuradas (SDKs, conectores de origem, assimilação em lote). Os perfis devem ser preenchidos com os tipos de identidade usados para [!DNL Segment Match] (por exemplo, email com hash). | [Visão geral das fontes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/home) |
| Configuração de identidade e perfil | Obrigatório | Os namespaces de identidade devem ser configurados para os identificadores usados na correspondência de segmentos. O remetente e o destinatário devem usar namespaces de identidade compatíveis. As políticas de mesclagem devem ser configuradas para unificar os perfis corretamente. As regras de vinculação de identidade devem ser estabelecidas para garantir uma resolução de perfil precisa. | [Visão geral do Serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/home) |
| Definição e segmentação do público-alvo | Obrigatório | Os públicos da Source devem ser definidos e avaliados para que possam ser compartilhados via [!DNL Segment Match]. Os públicos devem ser compilados usando [!DNL Segment Builder] ou [!DNL Audience Composition] com a avaliação em lote concluída. Somente os públicos avaliados em lote estão qualificados para compartilhamento em [!DNL Segment Match]. | [Visão geral do Serviço de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/home) |

## Funções de suporte

Os recursos a seguir aumentam esse padrão de caso de uso, mas não são necessários para a execução principal.

| Função de suporte | Status | Por que é importante | Referência do Experience League |
| --- | --- | --- | --- |
| Criação de atributo calculado/derivado | Recomendado | Atributos computados como valor de compra vitalício, pontuação de engajamento ou afinidade de produto podem criar segmentos mais precisos para compartilhamento. Segmentos de entrada de maior qualidade resultam em uma colaboração de público-alvo mais valiosa. | [Visão geral dos atributos computados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/computed-attributes/overview) |
| Gerenciamento do ciclo de vida dos dados | Recomendado | As políticas de consentimento e retenção de dados garantem que os segmentos compartilhados cumpram com as regulamentações de privacidade. As políticas de expiração do conjunto de dados ajudam a gerenciar o ciclo de vida dos dados de público-alvo recebidos. A aplicação de consentimento impede o compartilhamento de perfis que recusaram. | [Visão geral do Gerenciamento Avançado do Ciclo de Vida dos Dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-lifecycle/home) |
| Rotulagem e aplicação de uso de dados | Incluído | As políticas de governança de dados devem ser avaliadas antes do compartilhamento de segmentos para garantir a conformidade. Os rótulos nos campos de identidade e atributos de perfil determinam o que pode ser compartilhado. A aplicação de governança impede que dados não autorizados sejam incluídos em compartilhamentos de segmento. | [Visão geral da governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/home) |
| Monitoramento e capacidade de observação | Recomendado | Monitorar o processo de compartilhamento [!DNL Segment Match], os trabalhos de estimativa de sobreposição e os fluxos de dados de ativação ajudam a detectar falhas antecipadamente. Os alertas podem ser configurados para falhas de compartilhamento ou taxas de correspondência inesperadamente baixas. | [Visão geral dos Insights de Capacidade de Observação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/home) |
| Relatórios e análise | Recomendado | Medir o desempenho de campanhas que usam públicos correspondentes valida o valor da colaboração. [!DNL Customer Journey Analytics] a análise pode comparar o desempenho da campanha de público correspondente com os grupos de controle. | [visão geral do CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-overview/cja-overview) |

## Funções do aplicativo

Este plano utiliza as seguintes funções do catálogo de funções do aplicativo. As funções são mapeadas para fases de implementação em vez de etapas numeradas.

### [!DNL Real-Time CDP]

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Avaliação de público | Fase 1: Seleção e preparação de segmentos | Avalie a associação do segmento usando a avaliação em lote para produzir os públicos que serão compartilhados via [!DNL Segment Match] |
| Composição de público | Fase 1: Seleção e preparação de segmentos | Opcionalmente, componha públicos derivados (classificar, dividir, excluir, enriquecer) para criar segmentos mais direcionados para compartilhamento |
| Consentimento e aplicação de governança | Fase 2: Combinar configuração e governança | Aplique políticas de uso de dados e preferências de consentimento antes de compartilhar segmentos para garantir a conformidade |
| Audience Activation | Fase 5: Audience Activation correspondente | Publicar públicos correspondentes recebidos via [!DNL Segment Match] para destinos externos para direcionamento ou supressão |
| Configuração de destino | Fase 5: Audience Activation correspondente | Configurar conexões com destinos externos onde os públicos correspondentes serão ativados |

## Pré-requisitos

- As organizações remetente e destinatário têm [!DNL Real-Time CDP] provisionado com [!DNL Segment Match] direito
- [!DNL Segment Match] está habilitado para as organizações ou sandboxes que participam da colaboração
- A conexão de parceiro foi estabelecida entre as organizações remetente e destinatário na interface do usuário [!DNL Segment Match]
- Ambas as organizações usam namespaces de identidade compatíveis (por exemplo, ambas têm emails com hash configurados)
- Os públicos do Source foram definidos e avaliados com populações diferentes de zero
- As políticas de governança de dados são configuradas e os rótulos de uso de dados são aplicados aos conjuntos de dados e campos relevantes
- Os usuários de ambos os lados têm as permissões necessárias para gerenciar conexões, compartilhamentos e feeds do [!DNL Segment Match]
- Os campos de consentimento são preenchidos em perfis para ativar a filtragem baseada em consentimento antes do compartilhamento

## Opções de implementação

As opções a seguir descrevem diferentes abordagens para implementar a colaboração de público-alvo com o [!DNL Segment Match]. Selecione a opção que melhor se adapta à sua estrutura organizacional e aos requisitos de colaboração.

### Opção A: participação direta no segmento (um para um)

Essa opção é mais adequada para parcerias bilaterais entre duas organizações específicas, como um anunciante e um editor, ou duas marcas em um acordo de co-marketing.

**Como funciona:**

Em um compartilhamento de segmento direto de um para um, a organização remetente seleciona um ou mais públicos-alvo avaliados, inicia um compartilhamento com uma organização parceira específica e o destinatário aceita o compartilhamento. A estimativa de sobreposição é executada automaticamente para mostrar a ambas as partes a porcentagem e o volume de perfis correspondentes antes que o compartilhamento seja finalizado.

O remetente define quais namespaces de identidade usar para correspondência e seleciona os segmentos a serem compartilhados. O receptor revisa o compartilhamento recebido, aceita-o e o público-alvo correspondente fica disponível na lista de públicos-alvo para ativação downstream. Somente a sobreposição de identidade com hash é trocada — nenhum PII subjacente ou dado de atributo de perfil ultrapassa os limites organizacionais.

Essa abordagem é simples e oferece controle total a ambas as partes. O remetente escolhe exatamente o que compartilhar e com quem, e o destinatário tem a opção de aceitar ou rejeitar cada compartilhamento.

**Principais considerações:**

- Requer configuração de conexão de parceiro explícita entre as duas organizações
- Ambas as organizações devem concordar sobre os namespaces de identidade para correspondência
- A estimativa de sobreposição fornece transparência antes do compromisso
- Cada compartilhamento deve ser gerenciado e monitorado individualmente

**Vantagens:**

- Fluxo de trabalho bilateral simples e bem compreendido
- Transparência total por meio de estimativa de sobreposição antes do compartilhamento
- Controle granular — o remetente escolhe exatamente quais segmentos compartilhar
- Seguro para privacidade — somente identificadores com hash são usados para correspondência
- O destinatário pode aceitar ou rejeitar compartilhamentos seletivamente

**Limitações:**

- Não é dimensionado com eficiência ao colaborar com muitos parceiros simultaneamente
- Cada parceria requer configuração e gerenciamento de conexão separados
- A configuração de compartilhamento deve ser repetida para cada novo segmento

**Experience League:**

- [Visão geral da correspondência de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-match/overview)
- [Solução de problemas de Correspondência de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-match/troubleshooting)

### Opção B: distribuição de segmentos com vários parceiros (um para muitos)

Essa opção é mais adequada para organizações que precisam compartilhar segmentos com vários parceiros simultaneamente, como uma rede de mídia de varejo que compartilha segmentos baseados em compras com vários anunciantes de marcas ou uma holding que distribui segmentos para marcas subsidiárias.

**Como funciona:**

Em um modelo de distribuição de um para muitos, a organização do remetente estabelece [!DNL Segment Match] conexões com várias organizações parceiras e compartilha os mesmos segmentos ou segmentos diferentes com cada uma. O remetente gerencia um portfólio de conexões de parceiros e pode compartilhar seletivamente diferentes segmentos de público com diferentes parceiros com base no relacionamento e caso de uso.

Cada conexão de parceiro opera independentemente — a estimativa de sobreposição, a aceitação de compartilhamento e a ativação são gerenciadas por parceiro. O remetente pode controlar quais segmentos cada parceiro recebe, permitindo estratégias de colaboração diferenciadas (por exemplo, parceiros premium recebem segmentos mais granulares, parceiros padrão recebem segmentos mais amplos).

Essa abordagem usa o mesmo mecanismo [!DNL Segment Match] subjacente da Opção A, mas a aplica em escala com uma estrutura operacional para gerenciar várias parcerias simultâneas.

**Principais considerações:**

- Requer processos operacionais robustos para gerenciar várias parcerias
- As políticas de governança devem levar em conta o compartilhamento dos mesmos segmentos com vários participantes externos
- Cada parceiro pode usar namespaces de identidade diferentes, o que requer configuração flexível
- As taxas de sobreposição variam de acordo com o parceiro, exigindo avaliação por parceiro

**Vantagens:**

- Dimensiona a colaboração do público-alvo em um ecossistema de parceiros
- Estratégias de compartilhamento diferenciadas por parceiro
- Gerenciamento centralizado de todos os compartilhamentos de segmentos de saída de uma organização
- Cada parceria mantém controles independentes de governança e consentimento

**Limitações:**

- A complexidade operacional aumenta com cada parceiro adicional
- O monitoramento e a solução de problemas devem ser feitos por parceiro
- Revisão de governança necessária para cada nova conexão de parceiro
- Os parceiros não veem os dados nem o status de compartilhamento um do outro

**Experience League:**

- [Visão geral da correspondência de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-match/overview)

### Opção C: federação de público-alvo entre sandboxes

Essa opção é melhor para grandes empresas com várias sandboxes do [!DNL Experience Platform] (por exemplo, sandboxes regionais, sandboxes específicas da marca ou sandboxes específicas do ambiente) que precisam compartilhar segmentos de público-alvo entre limites internos sem mover dados brutos.

**Como funciona:**

Em vez de compartilhar entre organizações separadas, a federação de público-alvo de sandbox cruzada usa [!DNL Segment Match] para compartilhar segmentos de público-alvo entre sandboxes na mesma organização. Isso permite que uma equipe de marketing global crie um segmento em uma sandbox central e o compartilhe com sandboxes regionais ou permite que sandboxes específicas da marca compartilhem listas de supressão entre si.

O fluxo de trabalho reflete o compartilhamento direto do segmento (Opção A), mas opera dentro do limite organizacional. As conexões de sandbox com sandbox são estabelecidas por meio do [!DNL Segment Match], e os segmentos são compartilhados usando o mesmo processo de correspondência seguro para privacidade. A sandbox de recebimento obtém o público correspondente como um novo público que pode ser ativado por meio de seus próprios destinos configurados localmente.

Essa abordagem é particularmente valiosa quando os requisitos de residência de dados impedem a movimentação de dados brutos do cliente entre regiões, mas a colaboração no nível do público-alvo é permitida.

**Principais considerações:**

- Requer o direito [!DNL Segment Match] que oferece suporte ao compartilhamento entre sandboxes
- Os namespaces de identidade devem ser consistentes em todas as sandboxes
- As políticas de mesclagem em cada sandbox podem resolver perfis de forma diferente, afetando potencialmente as taxas de correspondência
- As políticas de governança se aplicam independentemente por sandbox

**Vantagens:**

- Permite a colaboração do público-alvo sem mover dados brutos entre os limites da sandbox
- Oferece suporte a requisitos de residência de dados e conformidade regional
- Aproveita a infraestrutura de identidade organizacional existente
- Revisão de governança mais simples, pois o compartilhamento ocorre na mesma organização

**Limitações:**

- Requer configuração consistente de namespace de identidade em sandboxes
- As taxas de correspondência dependem da consistência da política de mesclagem entre sandboxes
- Não atende às necessidades de colaboração entre organizações
- Talvez seja necessário usar as ferramentas de sandbox para sincronizar o esquema e a configuração

**Experience League:**

- [Visão geral da correspondência de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-match/overview)
- [Visão geral de sandboxes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/home)

### Comparação de opções

A tabela a seguir compara as três opções de implementação entre os principais critérios.

| Critérios | Opção A: compartilhamento direto do segmento | Opção B: Distribuição com vários parceiros | Opção C: Federação entre sandboxes |
| --- | --- | --- | --- |
| Melhor para | Parcerias bilaterais | Colaboração em escala de ecossistema | Compartilhamento interno entre sandboxes |
| Complexo | Baixa | Alta | Médio |
| Número de parceiros | 1 | Muitos | Sandboxes internas |
| Sobrecarga de governança | Baixa | Alto (análise por parceiro) | Medium (dentro da organização) |
| Gerenciamento operacional | Simples | Exige estrutura de gerenciamento de parceiros | Moderado |
| Suporte para residência de dados | N/A | Depende da localização do parceiro | Forte |
| Exige | Configuração de conexão do parceiro | Várias conexões de parceiros | Cross-sandbox [!DNL Segment Match] |

### Escolha a opção certa

Use a seguinte orientação de decisão para selecionar a abordagem de implementação apropriada:

1. **Você está colaborando com uma organização externa ou dentro de sua própria organização?**
   - External organization: prossiga para a pergunta 2.
   - Em sua própria organização (em sandboxes): escolha **Opção C** (Federação entre sandboxes).

2. **Com quantos parceiros externos você colaborará?**
   - Um parceiro: escolha **Opção A** (Compartilhamento de segmento direto).
   - Vários parceiros: escolha **Opção B** (Distribuição Multisparceiros).

3. **Você tem restrições de residência de dados que impedem a movimentação de dados brutos entre regiões?**
   - Sim: escolha **Opção C** independentemente de os parceiros serem internos ou externos — use o compartilhamento entre sandboxes para manter a localidade dos dados.

## Fases de implementação

As fases a seguir descrevem o processo completo de implementação para colaboração de público com [!DNL Segment Match].

### Fase 1: Selecionar e preparar segmentos

**Função de aplicativo:** [!DNL Real-Time CDP]: Avaliação de público-alvo, [!DNL Real-Time CDP]: Composição de público-alvo

Esta fase envolve a definição e avaliação dos segmentos de público-alvo que serão compartilhados através de [!DNL Segment Match]. Os segmentos de origem devem ser totalmente avaliados com populações diferentes de zero para que possam ser selecionados para compartilhamento. Essa fase também abrange a composição opcional do público-alvo para refinar segmentos antes do compartilhamento.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: abordagem de definição de público-alvo**
>
>Como os públicos-alvo de origem para compartilhamento devem ser criados?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Construtor de segmentos (regras de segmento) | Definições de público-alvo padrão com base em atributos de perfil, eventos ou associação de segmento | Oferece suporte a avaliação de lote, fluxo e borda; mais flexível para definir critérios |
>| Composição de público | Públicos-alvo derivados que exigem operações de classificação, divisão, exclusão ou enriquecimento em segmentos existentes | Compatível apenas com avaliação em lote; limitado a 10 telas de composição por sandbox |
>| Composição de público-alvo federado | Públicos-alvo criados de consultas externas do data warehouse sem assimilar dados no [!DNL Experience Platform] | Requer o direito de [!DNL Federated Audience Composition]; os dados permanecem no depósito |

>[!NOTE]
>
>**Decisão: método de avaliação de público-alvo**
>
>[!DNL Segment Match] requer públicos avaliados em lote. Como a avaliação deve ser programada?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Lote agendado (diariamente) | Casos de uso padrão em que a atualização diária do público-alvo é suficiente | Calendário padrão de avaliação; mais simples de gerenciar |
>| Lote sob demanda | Necessidades de compartilhamento ad-hoc onde você deseja compartilhar o público mais atual imediatamente | Requer acionamento manual; útil para colaborações sensíveis ao tempo |
>| Agendamento personalizado | Requisitos de tempo específicos alinhados com as janelas de ativação do parceiro | Configurar um cronograma cron personalizado; mais complexo, porém preciso |

Navegação da **IU:** Cliente > Públicos > Criar público > Criar regra de compilação (para [!DNL Segment Builder]) ou Compor público (para [!DNL Audience Composition])

**Detalhes de configuração da chave:**

- Definir critérios de público-alvo usando atributos de perfil, eventos comportamentais e/ou associação de segmento
- Verifique se o público usa uma política de mesclagem compatível com os namespaces de identidade usados para [!DNL Segment Match]
- Verificar se a população do público-alvo é diferente de zero após a avaliação
- Aplique regras de supressão para excluir perfis que não devem ser compartilhados (por exemplo, perfis que recusaram o compartilhamento de dados)

**Onde as opções divergem:**

**Para A Opção A (Compartilhamento Direto De Segmentos):**
Prepare os segmentos específicos que você pretende compartilhar com seu único parceiro. Concentre-se na qualidade em vez da quantidade — prepare segmentos que forneçam um valor claro à parceria.

**Para Opção B (Distribuição Multisparceiros):**
Prepare um portfólio de segmentos que podem ser compartilhados com diferentes parceiros. Considere a criação de segmentos específicos do parceiro se parceiros diferentes precisarem de definições de público-alvo diferentes. Use convenções de nomenclatura consistentes para gerenciar segmentos em parcerias.

**Para Opção C (Federação Entre Sandboxes):**
Verifique se os públicos-alvo de origem na sandbox de envio usam namespaces de identidade que existem na sandbox de recebimento. Verifique se as políticas de mesclagem estão alinhadas nas sandboxes.

**Documentação do Experience League:**

- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-builder)
- [Visão geral da composição de público-alvo](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/audience-composition)
- [Métodos de avaliação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/home#evaluation-methods)
- [Referência do Profile Query Language](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/pql/overview)

### Fase 2: configurar correspondência e governança

**Função do aplicativo:** [!DNL Real-Time CDP]: Consentimento e Imposição de Governança

Essa fase estabelece a conexão [!DNL Segment Match] entre organizações ou sandboxes, configura os namespaces de identidade usados para correspondência e garante que as políticas de governança de dados permitam o compartilhamento. A aplicação de governança atua como uma porta de política que deve ser limpa antes que qualquer dado de segmento seja compartilhado.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: namespace de identidade para correspondência**
>
>Qual namespace de identidade será usado para corresponder perfis entre o remetente e o destinatário?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Email com hash (SHA-256) | Ambas as organizações coletam endereços de email e podem aplicá-los em hash de forma consistente | Chave de correspondência mais comum; altas taxas de correspondência para casos de uso do consumidor; ambos os lados devem usar o mesmo algoritmo de hash |
>| Número de telefone com hash | O email não está disponível de forma consistente, mas os números de telefone estão | Cobertura menor do que o email em muitos mercados; útil para públicos-alvo de publicação de conteúdo para dispositivos móveis |
>| Namespace personalizado (por exemplo, ID de fidelidade com hash) | As organizações compartilham uma ID de programa comum de fidelidade ou associação | Taxas de correspondência mais altas para bases de clientes compartilhadas conhecidas; requer infraestrutura de ID compartilhada pré-existente |
>| Vários namespaces | A maximização da taxa de correspondência é essencial e ambas as organizações têm vários identificadores consistentes | Aumenta as taxas de correspondência, mas adiciona complexidade; cada namespace deve ser configurado independentemente |

>[!NOTE]
>
>**Decisão: revisão da governança de dados**
>
>Quais verificações de governança devem ser concluídas antes do compartilhamento?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Avaliação de governança padrão | Caso de uso típico com rótulos e políticas padrão de uso de dados | Avaliar a ação de marketing &quot;Exportar para terceiros&quot; em relação aos rótulos do conjunto de dados; resolver quaisquer violações antes de compartilhar |
>| Governança aprimorada com filtragem de consentimento | Compartilhamento com parceiros externos em que o consentimento deve ser explicitamente verificado | Adicione filtragem baseada em consentimento para excluir perfis sem consentimento compartilhado (por exemplo, consentimentos.share.val = &#39;n&#39;); mais rigoroso, mas seguro |
>| Revisão da governança interna | Compartilhamento entre sandboxes na mesma organização | Requisitos de governança mais leves, pois os dados permanecem dentro dos limites organizacionais; verifique também os rótulos de uso de dados |

**Navegação da interface do usuário:** Cliente > Públicos-alvo > Correspondência de segmentos > Conexões de parceiros

**Detalhes de configuração da chave:**

- Estabeleça uma conexão de parceiro trocando identificadores de conexão entre as organizações remetente e destinatário
- Configurar os namespaces de identidade que serão usados para correspondência em ambos os lados
- Executar a avaliação da política de governança de dados em relação à ação de marketing associada ao compartilhamento de segmentos
- Verifique se os campos de consentimento estão preenchidos nos perfis e se os perfis sem consentimento de compartilhamento foram excluídos
- Revisar rótulos de uso de dados nos conjuntos de dados e campos de esquema incluídos no compartilhamento

**Onde as opções divergem:**

**Para A Opção A (Compartilhamento Direto De Segmentos):**
Estabeleça uma conexão de parceiro único. Configure namespaces de identidade com seu parceiro específico. A análise da governação centra-se na relação bilateral.

**Para Opção B (Distribuição Multisparceiros):**
Estabeleça e gerencie várias conexões de parceiros. Cada parceiro pode exigir uma análise de governança separada. Documente a aprovação de governança para cada parceria. Considere criar uma lista de verificação de governança para simplificar a integração de parceiros.

**Para Opção C (Federação Entre Sandboxes):**
Estabeleça conexões de sandbox com sandbox na organização. A governança normalmente é mais simples, pois o compartilhamento ocorre internamente. Verifique se os namespaces de identidade são consistentes em todas as sandboxes.

**Documentação do Experience League:**

- [Visão geral da correspondência de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-match/overview)
- [Visão geral da governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/home)
- [Aplicação de política](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/enforcement/overview)
- [Consentimento e preferências](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)

### Fase 3: Estimar sobreposição

**Função de aplicativo:** [!DNL Real-Time CDP]: Avaliação de público-alvo (para estimativa de sobreposição)

Essa fase executa a estimativa de sobreposição entre os segmentos do remetente e a base de perfil do receptor. A estimativa de sobreposição fornece a ambas as partes o volume e a porcentagem de correspondência esperados antes de se comprometerem com a participação total do segmento, permitindo decisões informadas sobre o valor da colaboração.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: Sobrepor limite para continuar**
>
>Qual taxa de sobreposição mínima justifica prosseguir com a participação total no segmento?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Sem limite mínimo | Parcerias exploratórias ou quando qualquer sobreposição fornece valor | Adequado para colaborações iniciais em que você está testando o relacionamento |
>| Limite baixo (1-5%) | Colaboração de público-alvo em grande escala, em que mesmo uma pequena sobreposição representa um volume significativo | Comum para relacionamentos editor-anunciante com grandes bases de público-alvo |
>| Limite do Medium (5-20%) | Parcerias padrão em que se espera uma sobreposição significativa | Típica para colaborações de co-marketing ou do mesmo setor |
>| Limite alto (mais de 20%) | Parcerias em que um forte alinhamento dos públicos-alvo é um pré-requisito | Comum para alianças de fidelidade ou parcerias de marca totalmente integradas |

**Navegação da interface do usuário:** Cliente > Públicos-alvo > Correspondência de segmentos > Compartilhamentos > Estimar sobreposição

**Detalhes de configuração da chave:**

- Selecionar os segmentos a serem incluídos na estimativa de sobreposição
- Revise o relatório de sobreposição mostrando a contagem e a porcentagem de perfis correspondidos
- Compartilhar os resultados da estimativa de sobreposição com as partes interessadas de ambos os lados para aprovação
- Documentar as métricas de sobreposição como uma linha de base para medir a eficácia da colaboração
- Se a sobreposição estiver abaixo do limite aceitável, considere ajustar as definições de segmento ou a configuração de correspondência de identidades antes de continuar

**Documentação do Experience League:**

- [Visão geral da correspondência de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-match/overview)

### Fase 4: Compartilhar públicos

**Função do aplicativo:** [!DNL Real-Time CDP]: Avaliação de público-alvo (para execução de compartilhamento)

Essa fase executa o compartilhamento real do segmento do remetente para o destinatário. O remetente inicia o compartilhamento para os segmentos selecionados e o destinatário aceita o compartilhamento recebido. Depois de aceito, o público-alvo correspondente aparece na lista de públicos-alvo do receptor como um novo público-alvo disponível para ativação downstream.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: Compartilhar direção**
>
>Qual é o modelo de compartilhamento dessa colaboração?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Compartilhamento unidirecional (remetente para destinatário) | Parceria assimétrica em que apenas uma parte fornece dados de público-alvo | Modelo mais simples; compartilhamentos de remetente, ativações do receptor; comum em relações anunciante-editor |
>| Compartilhamento bidirecional | Ambas as partes se beneficiam do compartilhamento de públicos entre si | Ambas as organizações atuam como remetente e destinatário simultaneamente; requer duas configurações de compartilhamento; comum em parcerias de co-marketing |

>[!NOTE]
>
>**Decisão: Compartilhar cadência de atualização**
>
>Com que frequência o público-alvo compartilhado deve ser atualizado com a associação de segmento atualizada?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Compartilhamento único | Testar a colaboração ou para uma campanha específica com um público-alvo fixo | Mais simples; sem manutenção contínua; o público-alvo se torna obsoleto com o tempo |
>| Compartilhamento recorrente (alinhado com a avaliação em lote) | Parcerias contínuas em que a associação ao público-alvo muda e precisa ser mantida atualizada | Requer monitoramento do status de atualização; mais comum para colaborações de produção |

**Navegação da interface do usuário:** Cliente > Públicos-alvo > Correspondência de segmentos > Compartilhamentos > Criar compartilhamento (remetente) ou Aceitar compartilhamento (destinatário)

**Detalhes de configuração da chave:**

- O remetente seleciona os segmentos a serem compartilhados e inicia o compartilhamento com o parceiro configurado
- O receptor analisa os detalhes do compartilhamento recebido (nomes de segmentos, tamanho estimado, namespaces de identidade usados)
- O destinatário aceita o compartilhamento para criar o público correspondente em sua sandbox
- Verifique se o público-alvo correspondente aparece na lista de públicos-alvo do receptor com a população esperada
- Confirme se o público-alvo correspondente está rotulado corretamente para rastreamento de governança

**Onde as opções divergem:**

**Para A Opção A (Compartilhamento Direto De Segmentos):**
Execute um único compartilhamento com seu parceiro. Monitore o status de compartilhamento e verifique o público correspondente no lado do receptor.

**Para Opção B (Distribuição Multisparceiros):**
Executar compartilhamentos para cada parceiro independentemente. Rastrear o status de compartilhamento em todas as parcerias. Considere uma iniciação de compartilhamento escalonada para gerenciar a carga de processamento.

**Para Opção C (Federação Entre Sandboxes):**
Execute o compartilhamento entre sandboxes. O público-alvo correspondente é exibido na lista de públicos-alvo da sandbox de recebimento. Verifique se a sandbox de recebimento tem as configurações de destino necessárias para ativação downstream.

**Documentação do Experience League:**

- [Visão geral da correspondência de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-match/overview)
- [Solução de problemas de Correspondência de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-match/troubleshooting)

### Fase 5: ativar públicos-alvo correspondentes

**Função de aplicativo:** [!DNL Real-Time CDP]: Configuração de Destino, [!DNL Real-Time CDP]: Audience Activation

Essa fase ativa o público-alvo correspondente (no lado do receptor) para destinos externos para uso de direcionamento, supressão ou downstream. O público-alvo correspondente é tratado como qualquer outro público-alvo na sandbox do receptor e pode ser ativado por meio do fluxo de trabalho de ativação de destino padrão.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: Tipo de destino para o público correspondente**
>
>Onde o público-alvo correspondente deve ser ativado?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Destinos do Advertising (Google, Meta, Trade Desk) | Uso de públicos-alvo correspondentes para direcionamento ou supressão de anúncios | Requer conexão e autenticação de destino; está sujeito a limites de taxa específicos de destino e requisitos de formato |
>| Destinos de armazenamento na nuvem (S3, Azure, GCS) | Exportação de públicos correspondentes como arquivos para uso em sistemas externos | Oferece suporte à personalização de formatos de arquivo; programação de exportação em lote necessária; flexível para processamento de downstream |
>| Destinos de automação de marketing/CRM | Enriquecimento de registros de CRM ou acionamento de workflows de marketing automatizado com dados de público correspondentes | Requer mapeamento de campo para esquema CRM; útil para alinhamento de vendas-marketing |
>| Destinos do Personalization (Web, aplicativo) | Uso da associação de público correspondente para personalização no site | Requer avaliação de borda do público correspondente ou ativação de transmissão; a latência varia de acordo com o destino |

>[!NOTE]
>
>**Decisão: Calendário de ativação**
>
>Com que frequência o público-alvo correspondente deve ser exportado para o destino?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Exportação incremental diária | Ativação padrão com atualizações regulares do público-alvo | Exporta somente perfis alterados, menor volume de dados, mais comum para campanhas em andamento |
>| Exportação completa diária | Destinos que exigem um arquivo de público-alvo completo todas as vezes | Maior volume de dados; garante que o destino tenha o estado completo do público-alvo; alguns destinos exigem exportações completas |
>| Ativação sob demanda | Inicializações de campanha ad-hoc ou ativações sensíveis ao tempo | Acionador manual; ignora a cadência agendada; disponível somente para destinos em lote |

**Navegação da interface do usuário:** Conexões > Destinos > Catálogo (para configuração de destino) ou Procurar > Selecionar destino > Ativar públicos (para ativação)

**Detalhes de configuração da chave:**

- Configure a conexão de destino com credenciais de autenticação apropriadas
- Mapear atributos de perfil do público-alvo correspondente para campos de destino (campos de identidade, atributos de perfil, associação de segmento)
- Configurar o agendamento de exportação (incremental vs. completo, diário vs. personalizado)
- Monitore o fluxo de dados de ativação para confirmar se os perfis de público-alvo correspondentes foram exportados com êxito
- Verificar métricas de ativação (perfis exportados, registros com falha) na exibição de monitoramento de destino

**Onde as opções divergem:**

**Para A Opção A (Compartilhamento Direto De Segmentos):**
O receptor ativa o público correspondente por meio de seu fluxo de trabalho de destino padrão. Nenhuma configuração especial é necessária além da ativação normal de destino.

**Para Opção B (Distribuição Multisparceiros):**
Cada organização recebedora ativa públicos-alvo correspondentes de maneira independente por meio de seus próprios destinos. O remetente não tem visibilidade sobre a ativação do lado do receptor.

**Para Opção C (Federação Entre Sandboxes):**
A sandbox de recebimento deve ter suas próprias configurações de destino. Os destinos não podem ser compartilhados entre sandboxes. Verifique se a sandbox de recebimento tem as conexões de destino necessárias estabelecidas.

**Documentação do Experience League:**

- [Visão geral dos destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/catalog/overview)
- [Monitorar fluxos de dados para destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/dataflows/ui/monitor-destinations)
- [Medidas de proteção de ativação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/guardrails)

## Considerações de implantação

Analise as seguintes considerações antes e durante a implementação para evitar problemas comuns e otimizar a colaboração do público-alvo.

### Medidas de proteção e limites

- [!DNL Segment Match] usa identificadores com hash para correspondência — nenhuma PII ultrapassa os limites organizacionais. Consulte [Visão geral da correspondência de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-match/overview).
- Somente públicos avaliados em lote podem ser compartilhados via [!DNL Segment Match]. Os segmentos de transmissão e avaliados de borda devem ser convertidos para avaliação em lote antes do compartilhamento.
- O máximo de 4.000 definições de segmento por sandbox se aplica aos segmentos de origem e recebidos. Consulte [Medidas de proteção de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/guardrails).
- A precisão da estimativa de sobreposição depende do volume de identificadores correspondentes. Pequenos públicos-alvo podem mostrar estimativas menos precisas.
- As medidas de proteção de ativação se aplicam a públicos-alvo correspondentes iguais a qualquer outro público-alvo — no máximo 100 fluxos de dados por destino. Consulte [Medidas de proteção de ativação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/guardrails).
- Os públicos-alvo compostos são avaliados em uma programação em lote e são limitados a 10 telas de composição por sandbox. Consulte [Medidas de proteção de composição de público-alvo](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails).

### Armadilhas comuns

- **Hash de identidade inconsistente entre o remetente e o destinatário:** se ambas as organizações usarem hash de endereços de email, mas usarem algoritmos de hash diferentes, regras de normalização ou valores de salt, as taxas de correspondência serão próximas a zero. Ambos os lados devem concordar com a especificação exata de hash (por exemplo, SHA-256 em emails em minúsculas e aparados) antes de estabelecer a conexão.
- **Compartilhamento de públicos sem revisão de governança:** iniciar um compartilhamento de segmento sem avaliar as políticas de uso de dados pode levar a violações de conformidade. Sempre execute a avaliação de política de governança em relação à ação de marketing &quot;Exportar para terceiros&quot; antes de compartilhar segmentos com organizações externas.
- **Baixas taxas de correspondência devido a falhas de cobertura de identidade:** Se o público-alvo do remetente for identificado principalmente pela ECID (cookie anônimo), mas o namespace correspondente for um email com hash, a taxa de correspondência será muito baixa porque os perfis anônimos não têm endereços de email. Verifique se os públicos-fonte têm cobertura suficiente do namespace de identidade correspondente configurado.
- **Esquecendo-se de aceitar o compartilhamento no lado do destinatário:** O público compartilhado não aparece na lista de públicos-alvo do destinatário até que o compartilhamento seja aceito explicitamente. Coordene com o receptor para garantir a aceitação em tempo hábil, especialmente para campanhas sensíveis ao tempo.
- **Públicos correspondentes obsoletos devido ao desalinhamento do agendamento de avaliação:** Se o público de origem do remetente for avaliado diariamente, mas a atualização do [!DNL Segment Match] for executada semanalmente, o público correspondente no lado do destinatário poderá não refletir a associação mais recente. Alinhe a avaliação e compartilhe as cadências de atualização.

### Práticas recomendadas

- Estabeleça um contrato formal de compartilhamento de dados entre organizações antes de configurar o [!DNL Segment Match]. Isso deve abranger casos de uso permitidos, requisitos de governança de dados, obrigações de consentimento e procedimentos de rescisão.
- Use a estimativa de sobreposição como uma ferramenta de validação antes de cada campanha principal — execute a estimativa antes de confirmar, para garantir que o público-alvo correspondente atenda aos limites mínimos de tamanho e qualidade.
- Aplique convenções de nomenclatura descritiva a segmentos compartilhados que incluem o nome do parceiro, o caso de uso e a data (por exemplo, &quot;PartnerX_HighValue_Suppression_2026Q1&quot;) para manter a clareza nas organizações.
- Monitorar taxas de correspondência ao longo do tempo. Taxas de correspondência decrescentes podem indicar degradação da cobertura de identidade, problemas de qualidade dos dados ou alterações na base de clientes do parceiro.
- Segmentar públicos de origem para excluir perfis sem o namespace de identidade correspondente preenchido. Isso melhora as porcentagens da taxa de correspondência e fornece estimativas de sobreposição mais precisas.
- Para parcerias de compartilhamento bidirecionais, designe uma propriedade clara da manutenção do segmento e das programações de atualização para evitar confusão sobre qual organização é responsável pelas atualizações.

### Decisões de compensação

>[!NOTE]
>
>**Contrapartida: taxa de correspondência vs. controle de privacidade**
>
>Usar mais namespaces de identidade (email com hash, telefone com hash, IDs de dispositivo) para correspondência aumenta as taxas de correspondência, mas amplia a área de superfície para possível reidentificação. Usar menos namespaces (somente email com hash) fornece proteção de privacidade mais forte, mas pode reduzir o tamanho do público correspondente.
>
>- **Vários namespaces favorecem:** Taxas de correspondência mais altas, públicos correspondentes maiores e mais valiosos para o direcionamento de campanha
>- **O namespace único favorece:** postura de privacidade mais forte, revisão de governança mais simples, menor risco de conformidade
>- **Recomendação:** comece com um único namespace (o mais comum é o email com hash) e adicione outros namespaces somente se as taxas de correspondência forem insuficientes para o caso de uso. Documente a avaliação de impacto de privacidade para cada namespace adicionado.

>[!NOTE]
>
>**Contrapartida: granularidade do segmento vs. simplicidade operacional**
>
>O compartilhamento de vários segmentos granulares e altamente direcionados com um parceiro oferece mais flexibilidade para o direcionamento de campanha, mas aumenta a complexidade operacional para o remetente e o destinatário. O compartilhamento de um número menor de segmentos mais amplos simplifica o gerenciamento, mas reduz a precisão do direcionamento.
>
>- **Segmentos granulares favorecem:** Direcionamento preciso, campanhas diferenciadas, maior relevância
>- **Segmentos amplos favorecem:** gerenciamento mais simples, menos compartilhamentos para monitorar, menor sobrecarga operacional
>- **Recomendação:** comece com um pequeno número de segmentos de alto valor (2-5) para uma nova parceria. Aumente a granularidade à medida que a parceria amadurece e os processos operacionais são estabelecidos. Use as convenções e a documentação de nomenclatura para gerenciar a complexidade à medida que a contagem de segmentos cresce.

>[!NOTE]
>
>**Contrapartida: Atualizar frequência vs. custo de processamento**
>
>Atualizar públicos-alvo compartilhados com mais frequência mantém o público-alvo correspondente atualizado, mas aumenta a carga de processamento e pode consumir mais capacidade de licença. Atualizações menos frequentes reduzem o custo, mas permitem que o público correspondente se torne obsoleto.
>
>- **A atualização frequente favorece:** associação de público atual, maior relevância de campanha, melhor precisão de supressão
>- **Atualizações pouco frequentes favorecem:** Menor custo de processamento, monitoramento mais simples, consumo reduzido de licenças
>- **Recomendação:** a atualização diária é apropriada para a maioria das colaborações de produção. Para casos de uso com detecção de tempo (por exemplo, vendas rápidas, campanhas baseadas em eventos), considere a reavaliação sob demanda e o compartilhamento imediatamente antes do lançamento da campanha.

## Documentação relacionada

Os recursos a seguir fornecem detalhes adicionais sobre os recursos usados neste padrão de caso de uso.

### [!DNL Segment Match]

- [Visão geral da correspondência de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-match/overview)
- [Solução de problemas de Correspondência de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-match/troubleshooting)

### Segmentação e públicos

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-builder)
- [Visão geral da composição de público-alvo](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/audience-composition)
- [Referência do Profile Query Language](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/pql/overview)
- [Segmentação de transmissão](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentação de borda](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/methods/edge-segmentation)

### Identidade e perfil

- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/home)
- [Visão geral dos namespaces de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/namespaces)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/merge-policies/overview)
- [Visão geral do Perfil do cliente em tempo real](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/home)

### Governança e consentimento de dados

- [Visão geral da governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/home)
- [Visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview)
- [Aplicação de política](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/enforcement/overview)
- [Consentimento e preferências](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)
- [Grupo de campos Consentimento e preferências](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/field-groups/profile/consents)

### Destinos e ativação

- [Visão geral dos destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/catalog/overview)
- [Monitorar fluxos de dados para destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/dataflows/ui/monitor-destinations)

### Modelagem de dados e esquema

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/home)
- [Noções básicas de composição de esquema](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/schema/composition)

### Administração e controle de acesso

- [Visão geral do controle de acesso](https://experienceleague.adobe.com/pt-br/docs/experience-platform/access-control/home)
- [Visão geral de sandboxes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/home)

### Monitorização e observabilidade

- [Visão geral de alertas](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/alerts/overview)
- [Visão geral dos Insights de observação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/home)

### Medidas de proteção

- [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/guardrails)
- [Proteções de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails)
- [Medidas de proteção de ativação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/guardrails)

### Tutoriais

- [Crie um esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/union-schema)
- [Ativar um conjunto de dados para o Perfil](https://experienceleague.adobe.com/pt-br/docs/experience-platform/catalog/datasets/enable-for-profile)
