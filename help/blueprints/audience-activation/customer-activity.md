---
title: Blueprint do Hub de atividades do cliente
description: '[!UICONTROL Pesquisas de perfis de clientes em tempo real para fornecer contexto ao suporte e às vendas atendidas por agentes.]'
solution: Experience Platform,Data Collection
kt: 7195
exl-id: 3616cbf1-2e59-4e68-a1ff-1d2e3b344a1c,4f15aa5d-9ee3-4d92-8012-3e2f0c0d615f
translation-type: tm+mt
source-git-commit: 9e0954334e8b8a8c5bf52651611e7afa165f6d21
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 90%

---

# Blueprint do Hub de atividades do cliente

O Blueprint do Hub de atividades do cliente apresenta como aplicativos externos podem acessar o [!UICONTROL Perfil de cliente em tempo real] da Adobe Experience Platform.

Aplicativos externos podem acessar perfis com uma solicitação de GET de API. Atributos, eventos, associações de segmentos e funcionalidades orientadas por modelos armazenadas no perfil podem depois ser usados nesses aplicativos externos que não são da Adobe.

Com essa funcionalidade, é possível acessar conteúdo avançado durante chamadas de clientes à central de atendimento. Agentes de suporte teriam visibilidade do valor vitalício do cliente, da propensão à rotatividade ou exposição a campanhas de marketing, por exemplo. Os agentes de vendas também podem se beneficiar de conteúdos extras ou insights sobre os clientes.

>[!NOTE]
>
>A latência atual suportada pela API de pesquisa de perfil é de aproximadamente 500 milissegundos. Isso torna essa abordagem inadequada para a integração do perfil com mecanismos de decisão em tempo real, como Web de mesma página ou personalização de publicação de conteúdo para dispositivos móveis.

## Casos de uso

* Forneça contexto aprofundado do consumidor nas interações com agentes, como suporte e experiências de vendas. Ao usar a pesquisa de perfil na Experience Platform, os agentes podem receber mais contexto sobre o consumidor, como compras recentes, interações com campanhas, propensões, associações do público e outros atributos e insights que são armazenados no perfil do cliente em tempo real.

## Arquitetura

<img src="assets/customer_activity_hub.svg" alt="Blueprint de arquitetura de referência para o Hub de atividades do cliente" style="border:1px solid #4a4a4a" />

## Medidas de proteção

* [Medidas de proteção para dados de perfis de cliente em tempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)

## Etapas de implementação

1. Configure conjuntos de dados e esquemas.
1. Configure [!UICONTROL Perfil do cliente em tempo real]: configure o esquema e o conjunto de dados para [!UICONTROL Real-time Customer Profile] e configure uma política de mesclagem e identidades.
1. Assimile dados na Platform e processe-os no [!UICONTROL Perfil de cliente em tempo real].
1. Use a API de Entidade para pesquisar um atributo de perfil, seja da entidade de registro ou da entidade do evento da experiência.

## Documentos relacionados

* [Descrição do produto Adobe Experience Platform Activation](https://helpx.adobe.com/br/legal/product-descriptions/adobe-experience-platform0.html)
* [Documentação do Perfil de cliente em tempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=pt-BR)
* [Medidas de proteção de perfis](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
* [API de pesquisa de perfil](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
