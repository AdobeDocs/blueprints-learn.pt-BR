---
title: Blueprint de encaminhamento de eventos
description: Transmitir dados coletados por [!DNL Experience Platform] SDKs para destinos
solution: Data Collection
kt: 7202
exl-id: 8d6f0705-628b-44e4-a3fc-da6c5e308a5b
source-git-commit: 72eb4e2ff276279a2fc88ead0b17d77cc8e99b97
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 55%

---

# Blueprint do encaminhamento de eventos

O blueprint do encaminhamento de eventos mostra como os dados coletados com o Adobe [!DNL Experience Platform] Os SDKs da Web e móveis podem ser encaminhados de [!DNL Experience Platform] [!DNL Edge Network] para um destino desejado. É possível encaminhar todos os dados brutos coletados dos SDKs ou dados específicos com base em eventos e regras configurados nas propriedades de tag (antigo Launch).

## Casos de uso

* Colete dados da Web ou de dispositivos móveis usando um só rótulo de coleção, reduzindo o peso dos códigos nos navegadores e aplicativos do cliente. Propague os dados coletados a vários endpoints e obtenha uma só origem de coleção de dados.
* Encaminhe dados coletados para aplicativos de parceiros ou para locais de armazenamento de dados a fim de criar insights e aplicativos em relação aos dados coletados.

## Aplicativos

* Adobe [!DNL Experience Platform] Coleta de dados

## Arquitetura

<img src="assets/enterprise_collection.svg" alt="Arquitetura de referência para coleção de dados corporativos" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## Documentação relacionada

* [Documentação de encaminhamento do evento](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=pt-BR)
* [Vídeos sobre encaminhamento de eventos](https://experienceleague.adobe.com/docs/launch-learn/tutorials/server-side/overview.html?lang=pt-BR)
* [Aula sobre encaminhamento de eventos](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding.html?lang=pt-BR) do tutorial do SDK da Web

## Publicações do blog relacionadas

* [Aumento do desempenho do site com o Adobe [!DNL Experience Platform] SDK da Web e [!DNL Edge Network]](https://medium.com/adobetech/boosting-website-performance-with-adobe-experience-platform-web-sdk-and-edge-network-329fcf70fdf9)
* [Resolução de pontos problemáticos da implementação com o Adobe [!DNL Experience Platform] SDK da Web e [!DNL Edge Network]](https://medium.com/adobetech/solving-implementation-pain-points-with-adobe-experience-platform-web-sdk-and-edge-network-880b635e6819)
* [Adobe [!DNL Experience Platform] SDK da Web para gerenciamento de público-alvo](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [Adobe [!DNL Experience Platform] SDK da Web - Adobe Target](https://medium.com/adobetech/adobe-experience-platform-web-sdk-adobe-target-9b9f621d271)
* [Adobe [!DNL Experience Platform] Cenários de migração do SDK da Web para o Adobe Analytics](https://medium.com/adobetech/adobe-experience-platform-web-sdk-migration-scenarios-for-adobe-analytics-91c255ec82b0)
* [Unificar o Adobe [!DNL Experience Platform] Serviços com Adobe [!DNL Experience Platform] SDK da Web](https://medium.com/adobetech/unify-your-adobe-experience-platform-services-with-adobe-experience-platform-web-sdk-75cf6851a9fc)
* [Acelere o desenvolvimento de aplicativos móveis com o Adobe [!DNL Experience Platform] SDK móvel e Launch](https://medium.com/adobetech/accelerate-your-mobile-application-development-with-adobe-experience-platform-mobile-sdk-and-launch-ed023536d611)
* [Simplificação dos fluxos de trabalho do cliente com o Adobe [!DNL Experience Platform] SDK da Web](https://medium.com/adobetech/simplifying-customer-workflows-with-adobe-experience-platform-web-sdk-4e54fe134f4a)
