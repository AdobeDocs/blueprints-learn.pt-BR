---
title: Blueprint de coleção de dados do Encaminhamento de eventos de várias sandboxes
description: Transmita dados coletados pelos SDKs do  [!DNL Experience Platform] (AEP) para várias sandboxes usando o encaminhamento de eventos
solution: Data Collection
kt: 7202
exl-id: c24a47fe-b3da-4170-9416-74d2b6a18f32
source-git-commit: 72eb4e2ff276279a2fc88ead0b17d77cc8e99b97
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 60%

---

# Blueprint da coleção de dados de encaminhamento de eventos de várias sandboxes

O blueprint da coleção de dados de encaminhamento de eventos de várias sandboxes mostra como os dados coletados com SDKs da Web e móvel do Adobe [!DNL Experience Platform] podem ser configurados para coletar um único evento e encaminhar para várias sandboxes do [!DNL Experience Platform] (AEP). Esse Blueprint é um caso de uso específico que usa o recurso Encaminhamento de eventos das tags da Adobe.

Além de replicar o evento, por meio da utilização dos recursos de Encaminhamento de eventos, você pode adicionar, filtrar ou manipular os dados coletados originais que atendam aos requisitos de outras sandboxes. Por exemplo, a Sandbox A precisa receber todos os elementos de dados do evento e a Sandbox B deve receber apenas dados não PII.

O encaminhamento de eventos usa uma propriedade de tag separada que contém os elementos de dados, as regras e as extensões necessárias para seus requisitos de dados. Com um Evento de entrada, a sua Propriedade de encaminhamento de eventos pode coletar e gerenciar os dados, conforme necessário, antes do encaminhamento.

Sua sandbox de destino precisaria de um Ponto de extremidade de transmissão HTTP configurado que seria usado pela extensão HTTPS do encaminhamento de eventos.

## Casos de uso

* Relatórios de dados globais - em caso de utilização de várias sandboxes para isolar ambientes operacionais e da necessidade de consolidar a coleção de dados em uma sandbox para relatórios entre sandboxes. O Encaminhamento de eventos para uma sandbox de relatórios permite que cada ambiente operacional de sandbox envie dados em tempo real para uma sandbox de relatórios conforme eles são coletados
* Gerencie a coleção de dados em sandboxes com base em regras de dados diferentes para cada ambiente operacional de sandbox. Ambientes operacionais que requerem a filtragem de dados confidenciais, tais como Serviços financeiros e de saúde

## Aplicativos

* Adobe [!DNL Experience Platform] Coleção de dados

## Arquitetura

<img src="assets/multi-Sandbox-Data-Collection.svg" alt="Arquitetura de referência para encaminhamento de eventos de várias sandboxes" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

1. Os Autores de tag definem uma Propriedade de tag e uma Propriedade de encaminhamento de eventos. Aqui, os autores definem os elementos de dados, as regras e as ações que gerenciam a coleta de dados. Lembre-se que o código de Propriedade de tag é executado no cliente e distribuído por um Host CDN. O código [!UICONTROL Propriedade de Encaminhamento de Eventos] é executado no Adobe [!DNL Edge Server].

1. Os dados coletados no cliente são enviados para o [!DNL Edge Network]. Os clientes também têm a opção de enviar dados para seu próprio servidor primeiro como um método de coleção do lado do servidor. O SDK da Web pode fornecer um recurso de coleta de servidor para servidor. Para isso, no entanto, é necessário implementar um modelo de programação diferente. Consulte a documentação **[!DNL Edge Network]Visão geral da API do servidor** abaixo

1. A plataforma [!DNL Edge Network] recebe cargas de coleta de dados e orquestra o fluxo de dados para os sistemas necessários, como Target e Analytics.

1. Os Elementos de dados da propriedade Encaminhamento de eventos são usados para acessar Dados do evento que chegam na carga. As Regras também podem ser usadas para, conforme seja necessário, manipular os dados do evento antes do encaminhamento. Como na formatação dos dados no XDM necessário para a assimilação de dados de transmissão

1. O Encaminhamento de eventos fornece a extensão HTTPS que possibilita encaminhar seus dados do evento para um ponto de extremidade HTTPS.

1. A Sandbox 2 é configurada com um Ponto final de transmissão que recebe o evento encaminhado.

## Documentação relacionada

* [Documentação de encaminhamento do evento](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=pt-BR)
* [Vídeos sobre encaminhamento de eventos](https://experienceleague.adobe.com/docs/launch-learn/tutorials/server-side/overview.html?lang=pt-BR)
* [Aula sobre encaminhamento de eventos](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding.html?lang=pt-BR) do tutorial do SDK da Web
* [[!DNL Experience Platform] Visão geral do SDK da Web](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR)
* [[!DNL Edge Network] Visão geral da API do servidor](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=pt-BR)

## Publicações do blog relacionadas

* [Aumentando o desempenho do site com o Adobe [!DNL Experience Platform] SDK da Web e [!DNL Edge Network]](https://medium.com/adobetech/boosting-website-performance-with-adobe-experience-platform-web-sdk-and-edge-network-329fcf70fdf9)
* [Resolvendo pontos problemáticos da implementação com o SDK da Web do Adobe [!DNL Experience Platform] e [!DNL Edge Network]](https://medium.com/adobetech/solving-implementation-pain-points-with-adobe-experience-platform-web-sdk-and-edge-network-880b635e6819)
* [Adobe [!DNL Experience Platform] SDK da Web para Gerenciamento de Público-Alvo](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [Adobe [!DNL Experience Platform] SDK da Web - Adobe Target](https://medium.com/adobetech/adobe-experience-platform-web-sdk-adobe-target-9b9f621d271)
* [Cenários de migração do SDK da Web do Adobe [!DNL Experience Platform] para Adobe Analytics](https://medium.com/adobetech/adobe-experience-platform-web-sdk-migration-scenarios-for-adobe-analytics-91c255ec82b0)
* [Unificar seus Serviços de Adobe [!DNL Experience Platform] Web com o SDK da Adobe [!DNL Experience Platform] Web](https://medium.com/adobetech/unify-your-adobe-experience-platform-services-with-adobe-experience-platform-web-sdk-75cf6851a9fc)
* [Acelere o desenvolvimento de aplicativos móveis com o Adobe [!DNL Experience Platform] Mobile SDK e o Launch](https://medium.com/adobetech/accelerate-your-mobile-application-development-with-adobe-experience-platform-mobile-sdk-and-launch-ed023536d611)
* [Simplifique fluxos de trabalhos de clientes com o SDK da Web da Adobe Experience Platform](https://medium.com/adobetech/simplifying-customer-workflows-with-adobe-experience-platform-web-sdk-4e54fe134f4a)
