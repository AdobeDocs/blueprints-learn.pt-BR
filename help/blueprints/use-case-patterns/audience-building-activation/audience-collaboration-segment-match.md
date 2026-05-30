---
title: Audience Collaboration
description: Saiba como compartilhar e corresponder segmentos de público-alvo em sandboxes ou organizações usando a Correspondência de segmentos.
solution: Real-Time Customer Data Platform, Experience Platform
exl-id: 7014849c-5e32-4ec3-a531-c0e8ce896f44
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1351'
ht-degree: 3%

---

# Audience Collaboration

Este guia descreve o padrão de caso de uso de colaboração de público-alvo, que usa [!DNL Segment Match] em [!DNL Real-Time CDP] e [!DNL Adobe Experience Platform] para compartilhar e corresponder segmentos de público-alvo em sandboxes ou organizações de uma maneira segura para a privacidade. Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam entender o que esse padrão faz, os objetivos de negócios que ele aceita, os casos de uso táticos que ele permite e os aplicativos Adobe envolvidos.

[!DNL Segment Match] habilita duas ou mais organizações [!DNL Experience Platform] (ou sandboxes dentro de uma organização) a colaborar em dados de público-alvo compartilhando informações de associação de segmento sem expor as PII subjacentes. Os participantes podem estimar sobreposições, compartilhar públicos e ativar perfis correspondentes para destinos downstream.

## Padrão do caso de uso

Esse caso de uso segue o padrão do Audience Collaboration.

Compartilhe e associe segmentos de público-alvo em sandboxes ou organizações usando o [!DNL Segment Match].

**Plano de execução:** Seleção de segmento > Configuração de correspondência > Estimativa de sobreposição > Compartilhamento de público > Ativação

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

Melhore o retorno sobre o investimento em marketing através de melhor direcionamento, atribuição, supressão de público-alvo e alocação de orçamento. O [!DNL Segment Match] habilita a supressão de público-alvo entre organizações e o direcionamento conjunto, o que reduz a duplicação e melhora a precisão.

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

## Aplicativos

Os aplicativos a seguir são usados neste padrão de caso de uso.

- **[!DNL Real-Time CDP]** — Fornece a funcionalidade [!DNL Segment Match] para compartilhamento de público-alvo com privacidade segura, avaliação de público-alvo para criação de segmento e ativação de destino para uso downstream de públicos-alvo correspondentes.
- **[!DNL Adobe Experience Platform]** — Fornece a infraestrutura de dados fundamental, incluindo resolução de identidade, unificação de perfil, governança de dados e imposição de consentimento da qual [!DNL Segment Match] depende.

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
