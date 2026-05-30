---
title: Visitante anônimo - Web Personalization
description: Saiba como fornecer conteúdo personalizado da Web para visitantes não identificados com base em sinais comportamentais na sessão.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: e2446801-ffce-40e6-bfe9-abec623c9201
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 4%

---

# Personalização anônima da Web para visitantes

Este guia descreve o padrão de caso de uso de personalização da Web de visitante anônimo, que usa [!DNL Adobe Journey Optimizer] (AJO), [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP) e [!DNL Adobe Experience Platform] (AEP) para fornecer conteúdo da Web personalizado a visitantes anônimos (não identificados) com base em sinais comportamentais na sessão. Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam entender o que esse padrão faz, os objetivos de negócios que ele aceita, os casos de uso táticos que ele permite e os aplicativos Adobe envolvidos.

O padrão opera com dados limitados — somente o que pode ser observado na sessão atual e qualquer perfil de borda anônimo acumulado de visitas anteriores com o mesmo dispositivo ou cookie. Isso o torna adequado para personalização de topo da funnel, em que o visitante não tem conta ou não foi autenticado.

## Padrão do caso de uso

A seguir estão descritos o padrão principal e o plano de execução para esse caso de uso.

**Web Personalization de Visitante Anônimo**

Forneça conteúdo personalizado com base em sinais comportamentais na sessão para visitantes não identificados por meio do canal da Web do AJO.

**Plano de execução:** Configuração de superfície da Web > Avaliação de regra comportamental > Entrega de conteúdo > Rastreamento de impressão > Relatórios

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

## Aplicativos

Os aplicativos a seguir são usados neste padrão de caso de uso.

- **[!DNL Adobe Journey Optimizer] (AJO)** — Configuração da superfície de canal da Web, criação de conteúdo (experiências da Web e baseadas em código), execução de campanha, experimentação de conteúdo (teste A/B), decisão (seleção de conteúdo dinâmico) e relatórios
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** — Segmentação Edge para avaliação de público-alvo em tempo real com base em sinais comportamentais na sessão; gerenciamento de perfil de borda anônimo
- **[!DNL Adobe Experience Platform] (AEP)** — [!DNL Web SDK] para coleta de sinal comportamental, [!DNL Edge Network] para entrega de roteamento e personalização de dados em tempo real e configuração de sequência de dados

## Arquitetura

A arquitetura de referência a seguir ilustra como os sinais anônimos de visitantes são coletados na borda, avaliados em relação às regras de público-alvo e usados para fornecer conteúdo personalizado.

![Arquitetura de referência para ativação e personalização de público anônimo](/help/blueprints/audience-activation/assets/anonymous_activation.png)

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
