---
title: Blueprint de coleção de dados do Encaminhamento de eventos de várias sandboxes
description: Transmitir dados coletados pelos SDKs da Experience Platform para várias sandboxes por meio da utilização do Encaminhamento de eventos
solution: Data Collection
kt: 7202
exl-id: c24a47fe-b3da-4170-9416-74d2b6a18f32
source-git-commit: 793a92218999185f8a993be528c4830fa07f4865
workflow-type: ht
source-wordcount: '608'
ht-degree: 100%

---

# Blueprint de coleção de dados do Encaminhamento de eventos de várias sandboxes

O Blueprint de coleção de dados do Encaminhamento de eventos de várias sandboxes mostra como os dados coletados com os SDKs móveis e da Web da Adobe Experience Platform podem ser configurados para coletar um único evento e encaminhar para várias sandboxes da AEP. Esse Blueprint é um caso de uso específico que usa o recurso Encaminhamento de eventos das tags da Adobe.

Além de replicar o evento, por meio da utilização dos recursos de Encaminhamento de eventos, você pode adicionar, filtrar ou manipular os dados coletados originais que atendam aos requisitos de outras sandboxes. Por exemplo, a Sandbox A precisa receber todos os elementos de dados do evento e a Sandbox B deve receber apenas dados não PII.

O Encaminhamento de eventos usa uma propriedade de tag independente que contém as Regras, extensões e elementos de dados necessários para os seus requisitos de dados. Com um Evento de entrada, a sua Propriedade de encaminhamento de eventos pode coletar e gerenciar os dados, conforme necessário, antes do encaminhamento.

Sua sandbox de destino precisaria de um Ponto de extremidade de transmissão HTTP configurado que fosse usado pela Extensão HTTPS de encaminhamento de eventos.



## Casos de uso

* Relatórios de dados globais - em caso de utilização de várias sandboxes para isolar ambientes operacionais e da necessidade de consolidar a coleção de dados em uma sandbox para relatórios entre sandboxes. O Encaminhamento de eventos para uma sandbox de relatórios permite que cada ambiente operacional de sandbox envie dados em tempo real para uma sandbox de relatórios conforme eles são coletados
* Gerencie a coleção de dados em sandboxes com base em regras de dados diferentes para cada ambiente operacional de sandbox. Ambientes operacionais que requerem a filtragem de dados confidenciais, tais como Serviços financeiros e de saúde

## Aplicativos

* Coleção da Adobe Experience Platform

## Arquitetura

<img src="assets/multi-Sandbox-Data-Collection.svg" alt="Arquitetura de referência para encaminhamento de eventos de várias sandboxes" style="width:90%; border:1px solid #4a4a4a" />

1. Os Autores de tag definem uma Propriedade de tag e uma Propriedade de encaminhamento de eventos. Aqui, os autores definem as Regras, ações e elementos de dados que gerenciam a coleção de dados. Lembre-se que o código de Propriedade de tag é executado no cliente e distribuído por um Host CDN. O código de Propriedade de encaminhamento de eventos é executado no servidor do Adobe Edge.

1. Os dados coletados no cliente são enviados para o Servidor do Edge. Os clientes também têm a opção de enviar os dados primeiro para o seu próprio servidor como uma forma de coleção do lado do servidor.
O WebSDK pode fornecer um recurso de coleção de Servidor para servidor. Para isso, no entanto, é necessário implementar um modelo de programação diferente. Consulte a documentação **Visão geral da API de Servidor da Edge Network** abaixo

1. O Platform Edge Server recebe cargas de coleção de dados e organiza o fluxo de dados para os sistemas necessários, como o Target e o Analytics.

1. Os Elementos de dados da propriedade Encaminhamento de eventos são usados para acessar Dados do evento que chegam na carga. As Regras também podem ser usadas para, conforme seja necessário, manipular os dados do evento antes do encaminhamento. Como na formatação dos dados no XDM necessário para a assimilação de dados de transmissão

1. O Encaminhamento de eventos fornece a extensão HTTPS que possibilita encaminhar seus dados do evento para um ponto de extremidade HTTPS.

1. A Sandbox 2 é configurada com um Ponto final de transmissão que recebe o evento encaminhado.

## Documentação relacionada

* [Documentação de encaminhamento do evento](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=pt-BR)
* [Vídeos sobre encaminhamento de eventos](https://experienceleague.adobe.com/docs/launch-learn/tutorials/server-side/overview.html?lang=pt-BR)
* [Aula sobre encaminhamento de eventos](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding.html?lang=pt-BR) do tutorial do SDK da Web
* [Visão geral do WebSDK da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR)
* [Visão geral da API de servidor da Edge Network](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=pt-BR)

## Publicações do blog relacionadas

* [[!DNL Boosting Website Performance with Adobe Experience Platform Web SDK and Edge Network]](https://medium.com/adobetech/boosting-website-performance-with-adobe-experience-platform-web-sdk-and-edge-network-329fcf70fdf9)
* [[!DNL Solving Implementation Pain Points with Adobe Experience Platform Web SDK and Edge Network]](https://medium.com/adobetech/solving-implementation-pain-points-with-adobe-experience-platform-web-sdk-and-edge-network-880b635e6819)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Adobe Experience Platform Web SDK — Adobe Target]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-adobe-target-9b9f621d271)
* [[!DNL Adobe Experience Platform Web SDK Migration Scenarios for Adobe Analytics]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-migration-scenarios-for-adobe-analytics-91c255ec82b0)
* [[!DNL Unify Your Adobe Experience Platform Services with Adobe Experience Platform Web SDK]](https://medium.com/adobetech/unify-your-adobe-experience-platform-services-with-adobe-experience-platform-web-sdk-75cf6851a9fc)
* [[!DNL Accelerate Your Mobile Application Development with Adobe Experience Platform Mobile SDK and Launch]](https://medium.com/adobetech/accelerate-your-mobile-application-development-with-adobe-experience-platform-mobile-sdk-and-launch-ed023536d611)
* [[!DNL Simplifying Customer Workflows with Adobe Experience Platform Web SDK]](https://medium.com/adobetech/simplifying-customer-workflows-with-adobe-experience-platform-web-sdk-4e54fe134f4a)
