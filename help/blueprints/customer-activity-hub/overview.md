---
title: Blueprint do Activity Hub do cliente
description: Pesquisas de Perfil do cliente em tempo real para fornecer contexto para o suporte assistido por agentes e vendas.
solution: Experience Platform, Data Collection
kt: 7195
translation-type: tm+mt
source-git-commit: c4bd4bbd40f2ae6b9ab980c5274a6e2007d976d3
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# Blueprint do Activity Hub do cliente

O Blueprint do Activity Hub do cliente mostra como os aplicativos externos podem acessar o [!UICONTROL Perfil do cliente em tempo real] da Adobe Experience Platform.

Aplicativos externos podem acessar Perfis do cliente em tempo real] com uma solicitação de GET de API. [!UICONTROL  Atributos, eventos, associações de segmentos e recursos orientados por modelo armazenados no perfil podem ser usados nesses aplicativos externos não-Adobe.

Com esse recurso, você pode superá-lo quando um cliente chamar sua central de atendimento. Os agentes de suporte podem ter visibilidade sobre o valor vitalício do cliente, a propensão ao churn ou a exposição às campanhas de marketing, por exemplo. Os agentes de vendas também podem se beneficiar de mais contexto ou insights sobre seus clientes.

>[!NOTE]
>
>A latência atual compatível com a API de pesquisa de perfil é de aproximadamente 500 milissegundos, tornando essa abordagem inadequada para a integração do perfil com mecanismos de decisão em tempo real, como a personalização da mesma página da Web ou móvel.

## Casos de uso

* Forneça um contexto de consumidor mais profundo para interações compatíveis com o agente, como experiências de suporte e de vendas. Usando a pesquisa de perfil no Experience Platform, os agentes podem receber mais contexto no consumidor, como compras recentes, interações de campanha, tendências, associações de público-alvo e outros atributos e insights armazenados no perfil do cliente em tempo real.

## Arquitetura

<img src="assets/cah.svg" alt="Arquitetura de referência para o Blueprint do Activity Hub do cliente" style="border:1px solid #4a4a4a" />

## Medidas de proteção

* [Grades de proteção para dados de perfil do cliente em tempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)

## Etapas da implementação

1. Configurar conjuntos de dados e esquemas.
1. Configure [!UICONTROL Perfis de cliente em tempo real]: configure o esquema e o conjunto de dados para [!UICONTROL Real-time Customer Profile] e configure uma política de mesclagem e identidades.
1. Assimile dados na plataforma e processe-os para [!UICONTROL Real-time Customer Profile].
1. Use a API de entidade para buscar um atributo de perfil, da entidade de registro ou da entidade de evento de experiência.

## Documentação relacionada

* [Descrição do produto Adobe Experience Platform Ativation](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html)
* [Documentação de Perfil do cliente em tempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en)
* [Medidas de proteção de perfil](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
* [API de pesquisa de perfil](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
