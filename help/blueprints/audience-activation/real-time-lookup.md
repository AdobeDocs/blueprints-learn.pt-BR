---
title: Acesso ao perfil do Real-time Edge para Personalization da Web e móvel
description: Acesso de [!UICONTROL Perfil de cliente em tempo real] na borda para fornecer contexto para personalização da Web e móvel em tempo real.
solution: Real-Time Customer Data Platform, Data Collection
kt: 719
exl-id: 61b81d00-c4bd-41b2-8161-683814947b56
TQID: https://experienceleague.adobe.com/H59c3UBbNCQFs3H0VL5iVDKKZ5D3CFt4ri2RVwNlq7s
product_v2:
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
feature_v2:
  - id: ba929a52-9339-4154-9487-317dc875a3c7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: 631
ht-degree: 8%

---

# Acesso ao perfil do Real-time Edge para Personalization da Web e móvel

>[!TIP]
>Este blueprint também está disponível como um [padrão de caso de uso](/help/blueprints/use-case-patterns/personalization/edge-profile-access.md) no Personalization.

O blueprint do Real-time Edge Profile Access for Web and Mobile Personalization mostra como os aplicativos da Web e móveis podem acessar o [!UICONTROL Perfil do cliente em tempo real] da Adobe Experience Platform na borda para personalização de alta taxa de transferência e baixa latência.

Os aplicativos podem acessar atributos de perfil e públicos-alvo em tempo real na borda com latência de milissegundos. Atributos, associações de público-alvo e recursos orientados por modelo armazenados no perfil como atributos podem ser acessados em tempo real para personalização de mesma página e próxima página em canais móveis e da Web.

Com esse recurso, você pode fornecer experiências altamente personalizadas em seus sites e aplicativos móveis com base no Perfil do cliente em tempo real, incluindo públicos derivados de comportamentos em tempo real, atributos assimilados no Perfil do cliente em tempo real e insights calculados.

>[!NOTE]
>
>O acesso ao perfil do Edge foi projetado especificamente para casos de uso de alta taxa de transferência e baixa latência, como personalização de entrada da Web/dispositivos móveis e o Offer Decisioning em tempo real. Para cenários de taxa de transferência mais baixa, como suporte assistido por agente ou interações de vendas, a API de pesquisa de perfil de hub é mais apropriada. Consulte o [blueprint de Acesso a Perfil em Tempo Real para Suporte e Cenários de Vendas](customer-activity.md) para obter acesso a perfil com base em hub.

## Aplicativos

* Real-time Customer Data Platform
* Coleta de dados do Adobe Experience Platform (Web SDK/Mobile SDK)
* API do servidor do Edge Network

## Casos de uso

* Personalização em tempo real na Web e em canais móveis para experiências conhecidas do cliente
* Personalização de mesma página e próxima página com base em atributos de perfil e públicos-alvo em tempo real
* Personalização de conteúdo e oferta com base em perfis de clientes, incluindo dados comportamentais em tempo real, atributos e insights calculados
* Integração com mecanismos de personalização, sistemas de gerenciamento de conteúdo e aplicativos externos para decisões em tempo real
* Otimização de testes e conteúdo com o contexto de perfil em tempo real

## Diagrama da arquitetura

<img src="assets/real-time-edge-lookup.svg" alt="Arquitetura de referência para acesso ao perfil do Edge para Personalization da Web e móvel" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />

## Medidas de proteção

* [Medidas de proteção para dados do [!UICONTROL Perfil de cliente em tempo real]](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)
* [Medidas de proteção do Edge Network](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* Os perfis do Edge têm um TTL (time-to-live) de 14 dias. Se um usuário não estiver ativo na borda por 14 dias, o perfil da borda pode expirar e precisa ser buscado no hub, o que pode afetar a personalização da primeira página.
* A personalização do Edge oferece suporte à avaliação de associação de público-alvo em tempo real para públicos que atendem aos critérios de segmentação de borda. Os públicos-alvo de lote e transmissão do hub também estão disponíveis na borda com a configuração apropriada.

## Documentação relacionada

### Configurações de destino

* [Conexão personalizada com o Personalization](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/custom-personalization) - Guia de implementação principal
* [Visão geral dos destinos do Personalization](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/overview)
* [Ativar públicos para destinos de personalização de borda](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations)
* [Pesquisar atributos de perfil na borda em tempo real](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-profile-lookup)

### Documentação do SDK

* [Documentação do Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html)
* [Documentação do Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/)
* [Documentação da API do Edge Network Server](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=pt-BR)
* [Documentação de tags do Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)
* [Respostas de comando no Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/commands/command-responses.html)

### Documentação de perfil e segmentação

* [Documentação de [!UICONTROL Perfil de cliente em tempo real]](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html)
* [Proteções de perfil](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)

### Tutoriais

* [Personalização de próxima ocorrência com Real-Time CDP e Adobe Target](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html)
* [Configuração da sequência de dados](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=pt-BR)
