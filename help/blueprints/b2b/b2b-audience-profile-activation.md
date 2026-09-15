---
title: Público-alvo B2B e ativação de perfil
description: Forneça públicos com base em conta e pessoas com o Real-Time Customer Data Platform B2B edition para ativação em canais e destinos.
solution: Real-Time Customer Data Platform
source-git-commit: 7f0b624616480cf563142c08eb0598d1dd55d551
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 5%
---

# Público-alvo B2B e ativação de perfil

Use o **Real-Time Customer Data Platform B2B edition** para reunir dados de conta, oportunidade e pessoa em perfis B2B unificados e, em seguida, ativar públicos de pessoas e contas em destinos como LinkedIn, Marketo Engage e armazenamento na nuvem. Este blueprint descreve como projetar esquemas B2B, criar públicos de várias entidades e exportá-los para ativação em vários canais e destinos, bem como para orquestração e análise em aplicativos como o **Journey Optimizer B2B edition** e o **Customer Journey Analytics B2B edition**.

## Casos de uso

- Crie públicos-alvo de pessoas para direcionamento e personalização em canais com base em dados B2B, incluindo contas, oportunidades e leads.
- Crie públicos-alvo de várias entidades que combinam atributos de nível de conta e oportunidade com comportamento de nível de pessoa usando uma abordagem de **segmento de segmentos** (por exemplo, &quot;Pessoas que visitaram a página de preços nos últimos 3 dias e são tomadores de decisão em oportunidades no estágio X para contas no setor Y&quot;).
- Ative pessoas e públicos-alvo de contas para destinos de armazenamento na Experience Platform e na nuvem, como Marketo Engage, LinkedIn Matched Audiences, Google Customer Match, DV360, The Trade Desk, Amazon Ads, Bombora e Demandbase, para direcionamento, personalização, alcance de vendas e análise.

## Aplicativos

- Real-Time Customer Data Platform B2B edition
- (Opcional) **Customer Journey Analytics B2B edition**
- (Opcional) **Journey Optimizer B2B edition**

## Padrões de integração

Os padrões típicos de integração B2B para este blueprint incluem:

- **Engajamento B2B e fontes de CRM → RTCDP B2B → destinos**

  Os sistemas de envolvimento B2B e CRM, como Marketo Engage, Salesforce e Microsoft Dynamics, enviam clientes em potencial/contatos, contas e oportunidades para o **Real-Time CDP B2B edition** usando os esquemas B2B padrão. A partir daí, públicos de pessoas e contas são ativados para destinos que incluem:

  - Marketo Engage
  - Públicos correspondentes do LinkedIn/LinkedIn
  - Correspondência de cliente da Google e DV360
  - A Trade Desk
  - Anúncios do Amazon
  - Trade Desk CRM, Critério, Bing e outras plataformas de publicidade
  - Destinos de armazenamento na nuvem, como Amazon S3, ADLS e Snowflake, para uso downstream

- **Fontes de evento e intenção B2B → RTCDP B2B → públicos → destinos**

  Fontes de evento e intenção B2B, como intenção Bombora, intenção Demandbase, PathFactory e eventos de envolvimento de fluxo RainFocus no RTCDP B2B. Esses eventos são mapeados para esquemas B2B padrão e usados para criar pessoas e públicos-alvo de contas que podem ser ativados para destinos de publicidade e marketing.

Várias fontes de dados B2B podem ser usadas para mapear dados de conta, cliente potencial, oportunidade e pessoa para a B2B edition do Real-Time Customer Data Platform usando os **esquemas e relações B2B** padrão.

## Arquitetura

<img src="assets/b2b-audience-profile-activation.png" alt="Arquitetura de referência para o público-alvo B2B e o blueprint de ativação de perfil" style="border:1px solid #4a4a4a"  width="100%" />

## Medidas de proteção

Consulte as seguintes medidas de proteção e documentação de qualificação ao criar públicos-alvo e perfis B2B:

- [Medidas de proteção para o Real-Time Customer Data Platform B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails?lang=en)
- [Casos de uso de segmentação para o Real-Time CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/segmentation/b2b)
- [Proteções de perfil e segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Atualização dos critérios de qualificação de segmentação de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/eligibility-criteria-update)

### Suporte a várias instâncias e organizações IMS

A seguir, são descritos os padrões suportados de instâncias de mapeamento da Experience Platform e do Marketo Engage.

#### Marketo como fonte de dados para o Experience Platform

- Há suporte para várias instâncias do Marketo Engage para uma instância do Experience Platform.
- Não há suporte para uma instância do Marketo Engage para muitas instâncias da Experience Platform.
- Há suporte para uma instância do Marketo Engage para uma instância da Experience Platform e várias sandboxes.

#### Marketo como destino do Experience Platform

- O Experience Platform para muitas instâncias do Marketo Engage é compatível.
- Muitas instâncias do Experience Platform para uma instância do Marketo Engage são compatíveis.

#### Proteções de perfil e segmentação do Experience Platform

Consulte o perfil do Experience Platform e as medidas de proteção de segmentação aqui: [Medidas de proteção de perfil e segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails).

Os segmentos que incluem entidades B2B, como contas, clientes potenciais ou oportunidades, dependem de relacionamentos de várias entidades e são avaliados em **lote**. Por outro lado, a **segmentação por transmissão** tem suporte para públicos-alvo limitados a pessoas e eventos que não incorporam entidades B2B. Para cenários de ativação B2B quase em tempo real, considere usar públicos B2B avaliados em lote como entradas para públicos de streaming ou de borda, quando suportado.

#### Experience Platform - Conector Source do Marketo Engage

- Consulte a documentação [aqui](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo).

#### Experience Platform - Conector de destino do Marketo

- Consulte a documentação [aqui](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/adobe/marketo-engage-connection).

#### Proteção de destino

- Consulte a documentação de destino para obter orientação específica sobre cada destino: [Medidas de proteção de destino](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails).
- Para destinos de publicidade, como Facebook, Google Customer Match &amp; DV360, Microsoft Bing, The Trade Desk, Amazon Ads, Bombora, Demandbase e outros, verifique se os identificadores escolhidos no esquema e na estratégia de identidade (email, IDs de publicidade móvel, campos de endereço, IDs de conta) estão alinhados aos recursos de mapeamento e identidades suportadas para esses destinos.

## Etapas de implementação

Para obter orientação sobre como implementar e configurar a B2B edition da Real-Time Customer Data Platform, consulte a documentação do Real-Time CDP B2B edition: [B2B edition da Real-Time Customer Data Platform](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview).

Dois padrões de implementação são comuns:

- Assimilar dados e perfis B2B do Marketo Engage (e seu CRM conectado) no RTCDP B2B edition.
- Assimilar dados B2B diretamente do CRM ou outros sistemas B2B no RTCDP B2B edition usando os conectores de origem relevantes.

Como parte das atualizações de arquitetura B2B do RTCDP, alguns padrões usados anteriormente agora estão obsoletos para entidades B2B. Para obter detalhes mais detalhados, consulte a documentação detalhada [aqui](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-architecture-upgrade).

## Considerações de implantação

Orientações sobre as principais considerações e configurações do blueprint.

- **Integração do CRM com e sem o Marketo**

  - Se a implementação usar o Marketo Engage como uma origem e o Marketo Engage estiver conectado ao CRM, os dados do CRM sincronizados com o Marketo (por exemplo, clientes potenciais/contatos, contas, oportunidades) fluirão para o RTCDP B2B edition por meio do conector de origem do Marketo.
  - Se houver tabelas ou atributos adicionais do CRM que não passem pelo Marketo (por exemplo, objetos personalizados ou campos adicionais), conecte a origem do CRM diretamente ao Experience Platform usando os conectores de origem do CRM e mapeie essas tabelas para os esquemas e relacionamentos padrão B2B.
  - Projete a assimilação de CRM + Marketo para evitar representações duplicadas ou conflitantes de entidades B2B no RTCDP B2B e garantir que todas as entidades B2B estejam em conformidade com os esquemas padrão.

## Documentação relacionada

- [B2B edition do Real-Time Customer Data Platform](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview)
- [Introdução ao Real-Time Customer Data Platform B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial?lang=en)
- [Medidas de proteção para o Real-Time Customer Data Platform B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails?lang=en)
- [Esquemas no Real-Time Customer Data Platform B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Atualizações de arquitetura no Real-Time CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-architecture-upgrade)
- [Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform)
- [Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home)
- [Adobe Experience Platform - Conector Source do Marketo](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Adobe Experience Platform - Conector de destino do Marketo](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list)
- [Proteção de destino](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)
