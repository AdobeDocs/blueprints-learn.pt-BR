---
title: Audience Activation B2B
description: Saiba como ativar públicos-alvo B2B baseados em conta nos canais da Web, de email e de anúncios.
solution: Real-Time Customer Data Platform
exl-id: 2b979159-37aa-41d4-a6b4-1105538f6546
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 2%

---

# Ativação de público-alvo B2B

Este guia descreve o padrão de caso de uso de ativação de público-alvo B2B, que usa o B2B edition [!DNL Adobe Real-Time Customer Data Platform] ([!DNL RT-CDP]) para compilar, avaliar e ativar públicos-alvo no nível da conta nos canais da Web, de email, de publicidade e CRM. Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam entender o que esse padrão faz, os objetivos de negócios que ele aceita, os casos de uso táticos que ele permite e os aplicativos Adobe envolvidos.

Esse padrão abrange o ciclo de vida completo da unificação do perfil da conta por meio da avaliação e ativação de público-alvo para destinos específicos B2B, como [!DNL Marketo Engage], [!DNL LinkedIn] e sistemas CRM.

## Padrão do caso de uso

**Ativação de público B2B**

Ative públicos-alvo B2B baseados em conta nos canais da Web, de email e de publicidade.

**Plano de execução:** Enriquecimento do Perfil da Conta > Avaliação do Público-Alvo da Conta > Configuração de Destino > Audience Activation > Monitoramento

## Visão geral do caso de uso

As equipes de marketing B2B precisam direcionar e ativar públicos-alvo no nível da conta em vez do nível da pessoa individual. Diferentemente da ativação de público-alvo B2C, em que a unidade de direcionamento é um único perfil do consumidor, a ativação de público-alvo B2B requer a compreensão da relação entre as pessoas e as contas às quais elas pertencem, avaliando a associação de público-alvo com base em atributos de nível de conta combinados com sinais de envolvimento de nível de pessoa e fornecendo esses públicos-alvo para destinos que oferecem suporte ao direcionamento baseado em conta.

O B2B edition [!DNL RT-CDP] estende o padrão [!DNL Real-Time Customer Data Platform] com classes XDM especializadas para contas, oportunidades e campanhas, juntamente com a resolução de identidade B2B que mapeia relacionamentos entre pessoas e contas. Isso permite que os profissionais de marketing criem públicos-alvo de contas que combinem dados firmográficos (setor, receita, contagem de funcionários), dados tecnológicos (pilha de tecnologia, uso de produtos) e dados comportamentais (visitas da Web, envolvimento de email, presença em eventos) das pessoas associadas a essas contas.

Os públicos ativados da conta potencializam os casos de uso na funnel de geração de demanda: campanhas de conscientização sobre o topo da funnel em [!DNL LinkedIn] e anúncios de exibição, programas de nutrição mid-funnel em [!DNL Marketo Engage] e capacitação de vendas bottom-of-funnel por meio da integração de CRM. Os públicos-alvo de supressão de conta evitam o desperdício, excluindo clientes existentes, contas fechadas/perdidas ou contas que já estão nos ciclos de vendas ativos.

>[!NOTE]
>Se o seu caso de uso envolver a ativação de públicos-alvo no nível da pessoa (B2C) em vez do nível da conta, consulte [Ativação de público-alvo para destinos](../audience-building-activation/audience-activation-to-destinations.md). Esse padrão usa o modelo de dados padrão RT-CDP e não requer o B2B edition.

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

## Aplicativos

Os aplicativos a seguir são usados para implementar esse padrão de caso de uso.

- **[!DNL Real-Time CDP]B2B edition** — Plataforma principal para unificação de perfil de conta, resolução de identidade B2B, avaliação de público-alvo de conta, configuração de destino específica para B2B e ativação de público-alvo de conta
- **[!DNL Adobe Experience Platform] (AEP)** — Infraestrutura básica para modelagem de dados XDM B2B, assimilação de dados do CRM e fontes de automação de marketing, serviço de identidade e governança
- **[!DNL Marketo Engage]** — Destino principal de automação de marketing B2B para programas de criação de clientes potenciais, pontuação e execução de campanha alimentados por públicos-alvo de contas ativadas

## Documentação relacionada

Os recursos a seguir fornecem contexto adicional e orientação detalhada para os recursos usados neste padrão de caso de uso.

**[!DNL RT-CDP]B2B edition**

- [Visão geral do Real-Time CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#rtcdp-b2b)
- [Esquemas B2B no Real-Time CDP](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/schemas/b2b)
- [Públicos da conta](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/types/account-audiences)
- [Descrição do produto RT-CDP B2B edition](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

**Avaliação e segmentação de público-alvo**

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-builder)
- [Composição de público](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/audience-composition)
- [Segmentação de transmissão](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Proteções de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/guardrails)

**Destinos e ativação**

- [Visão geral dos destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/catalog/overview)
- [Destino do Marketo Engage](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/catalog/adobe/marketo-engage)
- [Destino de públicos correspondentes do LinkedIn](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/catalog/social/linkedin)
- [Destino do Salesforce CRM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/catalog/crm/salesforce)
- [Destino do Microsoft Dynamics 365](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/catalog/crm/microsoft-dynamics-365)
- [Destino do Amazon S3](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/catalog/cloud-storage/amazon-s3)
- [Ativar públicos para destinos de transmissão](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Ativar públicos para destinos em lote](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Medidas de proteção de ativação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/guardrails)

**Fontes de dados e conectores**

- [Visão geral das origens](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/home)
- [Conector do Marketo Engage](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Conector do Salesforce](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/crm/salesforce)

**Identidade e modelagem de dados**

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/home)
- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/home)
- [Visão geral do perfil](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/home)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/merge-policies/overview)

**Governança e privacidade de dados**

- [Visão geral da governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/home)
- [Visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview)
- [Consentimento e preferências](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)

**Monitoramento e observabilidade**

- [Visão geral de alertas](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/alerts/overview)
- [Monitorar fluxos de dados de destino](https://experienceleague.adobe.com/pt-br/docs/experience-platform/dataflows/ui/monitor-destinations)
- [Monitorar fluxos de dados de origem](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/api-tutorials/monitor)
- [Painel de uso da licença](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/license-usage-dashboard)

**Relatórios e análises**

- [Visão geral do CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-overview/cja-overview)
- [Visão geral das conexões](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-connections/overview)
- [Visão geral das visualizações de dados](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/data-views)

**Tutoriais e guias**

- [Introdução ao Real-Time CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro)
- [Criar um esquema para fontes B2B](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/schemas/b2b)
- [Ferramentas de sandbox](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/sandbox-tooling-api/overview)
