---
title: Ativação de público-alvo para destinos
description: Saiba como avaliar e publicar segmentos de público-alvo em destinos externos para direcionamento ou supressão usando o Adobe Real-Time CDP.
solution: Real-Time Customer Data Platform, Experience Platform
exl-id: b0b9d937-45d2-48f9-ac4c-3611c6e35f58
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 4%

---

# Ativação de público-alvo para destinos

Este guia descreve a ativação de público-alvo para o padrão de caso de uso de destinos, que avalia segmentos de público-alvo no Adobe [!DNL Real-Time Customer Data Platform] (RT-CDP) e os publica em plataformas de anúncios, armazenamento na nuvem, sistemas CRM ou parceiros de dados para direcionamento, supressão, modelagem por semelhança ou enriquecimento de análise. Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam entender o que esse padrão faz, os objetivos de negócios que ele aceita, os casos de uso táticos que ele permite e os aplicativos Adobe envolvidos.

Esse padrão abrange o ciclo de vida completo da ativação de público-alvo — desde a definição e avaliação de segmentos de público-alvo até a configuração de conexões de destino e públicos de publicação, passando pelo monitoramento da integridade da ativação e pela aplicação da conformidade de governança.

## Padrão do caso de uso

**Audience Activation para Destinos** — Avalie e publique um segmento de público-alvo para destinos externos para direcionamento ou supressão.

**Plano de execução:** Avaliação de público-alvo > Configuração de destino > Audience Activation > Monitoramento

## Visão geral do caso de uso

As organizações precisam fornecer dados de público-alvo para sistemas externos a fim de alimentar campanhas de mídia paga, enriquecer registros de CRM, compartilhar dados com parceiros ou alimentar análises downstream. O Audience Activation para destinos é o padrão de ativação fundamental no RT-CDP: ele avalia quais perfis se qualificam para um público-alvo de destino, se conecta a um ou mais destinos externos, mapeia atributos de perfil para campos específicos de destino e publica o público-alvo para consumo downstream.

Esse padrão se aplica sempre que o objetivo é obter dados de público-alvo para um sistema externo no formato certo, na hora certa. Não envolve entrega de mensagens, personalização no site ou análise. É o ponto de partida mais comum para implementações da RT-CDP e serve como um bloco de construção que outros padrões compõem sobre.

As partes interessadas típicas incluem equipes de marketing digital que gerenciam mídia paga, equipes de dados que enriquecem depósitos, equipes de CRM que preparam listas de contato para campanhas e equipes de privacidade que garantem a conformidade da governança em fluxos de dados de saída.

>[!NOTE]
>Se sua organização usar o B2B edition [!DNL Real-Time CDP] e ativar para destinos baseados em conta, consulte [Ativação de público B2B](../b2b/account-audience-activation.md). Esse padrão compartilha a mesma mecânica de ativação, mas usa um modelo de dados de conta e pessoa B2B e requer a licença do B2B edition.

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

## Aplicativos

- **Adobe [!DNL Real-Time Customer Data Platform] (RT-CDP)** — Avaliação de público-alvo, gerenciamento de destino, ativação de público-alvo, consentimento e imposição de governança
- **Adobe [!DNL Experience Platform] (AEP)** — Armazenamento de perfis, serviço de identidade, mecanismo de segmentação, governança de dados

## Arquitetura

A arquitetura de referência a seguir ilustra como o público-alvo e os dados de perfil fluem do Real-Time CDP para destinos corporativos, incluindo armazenamento em nuvem, endpoints de transmissão e aplicativos SaaS.

![Arquitetura de referência para ativação de públicos e perfis para destinos corporativos](/help/blueprints/audience-activation/assets/known_activation.png)

## Documentação relacionada

**Destinos**

- [Visão geral dos destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [Catálogo de destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [Ativar públicos para destinos de transmissão](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Ativar públicos para destinos de exportação de perfil em lote](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Ativar públicos-alvo sob demanda para destinos em lote](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/api/ad-hoc-activation-api)
- [Medidas de proteção de destinos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)
- [Visão geral do Destination SDK](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/destination-sdk/overview)

**Públicos-alvo e segmentação**

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Referência do Profile Query Language](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)
- [Segmentação de transmissão](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Segmentação de borda](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Visão geral da composição de público-alvo](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Proteções de segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)

**Identidade e perfil**

- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Visão geral dos namespaces de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/namespaces)
- [Regras de vinculação do gráfico de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [Visão geral do perfil](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

**Modelagem de dados e esquemas**

- [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Noções básicas de composição de esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)

**Governança de dados**

- [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview)
- [Políticas de governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/policies/overview)
- [Aplicação de política](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/enforcement/overview)
- [Consentimento e preferências](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)

**Monitoramento e observabilidade**

- [Monitorar fluxos de dados para destinos](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations)
- [Visão geral de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Visão geral dos Insights de observação](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)
- [Painel de uso da licença](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/license-usage-dashboard)

**Atributos computados**

- [Visão geral de atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Guia da interface de atributos computados](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)

**Fontes e coleção de dados**

- [Visão geral das origens](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Visão geral do Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Configurar sequências de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)

**Administração**

- [Visão geral de sandboxes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/home)
- [Visão geral do controle de acesso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home)
- [Controle de acesso baseado em atributos](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/abac/overview)

**Medidas de proteção**

- [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Medidas de proteção do serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)
- [Medidas de proteção de ativação](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)
- [Medidas de proteção de assimilação](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
