---
title: Ativação de conta B2B para Advertising e destinos de arquivo
description: Use o envolvimento baseado em conta para criar públicos-alvo da conta e ativá-los para destinos de publicidade e armazenamento na nuvem.
solution: Real-Time Customer Data Platform
exl-id: 578c0019-6133-4508-ae9d-8a8a463376f0
source-git-commit: 7f0b624616480cf563142c08eb0598d1dd55d551
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 1%
---

# Ativação da conta B2B para destinos de anúncios e destinos de arquivos

O envolvimento baseado em conta permite que profissionais de marketing B2B criem públicos de contas (listas de empresas) no **Real-Time Customer Data Platform B2B edition** e ativem esses públicos para destinos de publicidade, como LinkedIn Matched Audiences, Bombora e Demandbase, bem como para destinos de armazenamento em nuvem. Esses públicos-alvo da conta podem ser usados para direcionamento, alcance de vendas e análise de downstream.

## Casos de uso

Usando o engajamento baseado em conta, os profissionais de marketing podem desbloquear três casos de uso importantes:

- **Preencha as lacunas do grupo de compras:** um profissional de marketing pode anunciar em contas em que ainda não tem contatos para as funções de CMO ou CIO. Primeiro, eles podem criar um público-alvo de contas sem um contato com o título &quot;CMO&quot; ou &quot;CIO&quot; e depois ativar o público-alvo no LinkedIn Matched Audiences ou outros destinos de publicidade compatíveis. Dentro do destino, eles podem lançar uma campanha direcionada a esse público-alvo e a pessoas específicas com títulos de trabalho de &quot;CMO&quot; ou &quot;CIO&quot; para alcançar esses novos contatos e destacar os benefícios de suas ofertas.
- **Venda adicional ou venda cruzada para outras divisões de uma empresa que seja um cliente existente:** um profissional de marketing pode criar um público-alvo de conta que comprou o produto X entre 3 e 9 meses atrás, mas ainda não possui o produto Y. Eles podem então ativar esse público-alvo da conta, destacando os benefícios do produto Y para esse público-alvo por meio de públicos correspondentes do LinkedIn, outras plataformas de publicidade ou exportações de armazenamento em nuvem para alcance de vendas e marketing.
- **Empresas de destino que estão usando produtos concorrentes:** um profissional de marketing pode vender para contas a fim de substituir os produtos de um concorrente, mesmo sem contatos nessas contas. Eles podem criar um público-alvo de contas com base em dados de parceiros ou de intenção que mostram a propriedade ou o uso do produto de um concorrente e, em seguida, ativar por meio de públicos correspondentes do LinkedIn ou outros destinos de publicidade compatíveis para fornecer contatos nas contas de destino para expansão.

## Aplicativos

- Real-Time Customer Data Platform B2B edition
- (Opcional) Customer Journey Analytics B2B edition

## Padrões de integração

Os padrões de integração típicos deste blueprint incluem:

- **Engajamento B2B e fontes de CRM → RTCDP B2B edition → públicos-alvo da conta → destinos**

  Os sistemas de envolvimento B2B e CRM, como Marketo Engage, Salesforce e Microsoft Dynamics, enviam clientes em potencial/contatos, contas e oportunidades para o **Real-Time CDP B2B edition** usando os esquemas e relações B2B padrão. Os públicos-alvo da conta são criados com base nesse modelo unificado de dados B2B e ativados para destinos de anúncios e arquivos.

- **Fontes de evento e intenção B2B → RTCDP B2B edition → públicos-alvo da conta → destinos**

  Fontes de evento e intenção B2B, como a Intenção Bombora e a Intenção Demandbase, enviam eventos de intenção e envolvimento para o Experience Platform. Esses conjuntos de dados são mapeados para os esquemas B2B padrão, permitindo que os profissionais de marketing criem públicos-alvo de conta (por exemplo, contas que surgem em tópicos de concorrentes) e os ativem para destinos de armazenamento de anúncios e em nuvem. Os públicos-alvo das contas podem ser ativados para parceiros de publicidade, como Bombora e Demandbase, onde houver suporte.

## Arquitetura

<img src="assets/b2b-account-activation.png" alt="Arquitetura de referência para o blueprint de ativação de conta B2B" style="border:1px solid #4a4a4a"  width="100%" />

## Destinos de público da conta

- **Públicos-alvo correspondentes do LinkedIn**
- **Bombora**
- **Demandbase**
- **Destinos de armazenamento na nuvem**
  - Armazenamento Azure Data Lake Gen2
  - Zona de aterrissagem de dados
  - SFTP
  - Blob do Azure
  - AWS S3

Consulte a documentação de destino para obter a lista mais recente de destinos que oferecem suporte a públicos-alvo da conta.

## Medidas de proteção

Consulte as seguintes medidas de proteção ao projetar e ativar públicos-alvo da conta:

- [Medidas de proteção para o Real-Time Customer Data Platform B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails?lang=en)
- [Públicos da conta](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/account-audiences?lang=en)
- [Ativar públicos-alvo da conta](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-account-audiences?lang=en)
- [Proteções de perfil e segmentação](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Atualização dos critérios de qualificação de segmentação de streaming](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/eligibility-criteria-update)

## Etapas de implementação do Real-Time Customer Data Platform B2B edition, criação e ativação de público-alvo da conta

- Para obter as etapas de implementação do Real-Time Customer Data Platform B2B edition, consulte a documentação: [Introdução ao Real-Time Customer Data Platform B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial?lang=en).
- Para conhecer as etapas de criação de um Público-alvo de conta, consulte a documentação de [Públicos-alvo de conta](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/account-audiences?lang=en).
- Para consultar as etapas de ativação de Público-alvo, consulte a documentação [Ativar públicos-alvo da conta](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-account-audiences?lang=en):

  - Mapeamento necessário para [Destino de públicos correspondentes do LinkedIn](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-account-audiences?lang=en#required-mappings).

## Considerações de implantação

Os públicos-alvo correspondentes do LinkedIn têm um requisito de tamanho mínimo de público-alvo (por exemplo, 300 membros correspondentes). Se o público-alvo da conta ativado para o LinkedIn Matched Audiences não atender a esse requisito, talvez seja necessário ampliar a definição do público-alvo para aumentar o tamanho do público-alvo correspondente antes de iniciar uma campanha.

## Documentação relacionada

- [blueprint de Audiência B2B e Ativação de perfil](b2bactivation.md) — blueprint principal que cobre ativação B2B no nível das pessoas e da conta.
- [B2B edition do Real-Time Customer Data Platform](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview?lang=en)
- [Criar e ativar público-alvo da conta - vídeo tutorial](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/audiences/create-audiences-with-b2b-data?lang=en)
- [Criar públicos-alvo da conta](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/account-audiences?lang=en)
- [Ativar públicos-alvo da conta](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-account-audiences?lang=en)
- [Adobe Experience Platform - Conector de destino do LinkedIn](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin?lang=en)
- [Esquemas no Real-Time CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Atualizações de arquitetura no Real-Time CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-architecture-upgrade)
- [Proteção de destino](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)
