---
title: Customer Journey Analytics com a Real-time Customer Data Platform
description: Unifique e analise dados e comportamentos do cliente em toda a jornada dele no Customer Journey Analytics e publique o público do CJA para o RTCDP
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 9e1ba723-63f2-4622-ba67-f2a315c3ba0c
source-git-commit: 985f7320db7c77b8541ec4ef76b1eb7ad0caae56
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 48%

---

# Customer Journey Analytics com a Real-time Customer Data Platform

Crie e publique públicos identificados no Customer Journey Analytics (CJA) para o Perfil do cliente em tempo real na Adobe Experience Platform para direcionamento e personalização do cliente. Ideal para criar públicos usando dados históricos ou públicos mais refinados por meio da filtragem granular e campos calculados no Customer Journey Analytics.

## Guia de publicação do público do Customer Journey Analytics

Consulte a documentação a seguir para obter orientação sobre a implementação e a configuração na publicação de públicos do Customer Journey Analytics para a Real-time Customer Data Platform. [Documentação](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=pt-BR)

## Arquitetura de Blueprints do Customer Journey Analytics

![Diagrama da arquitetura](assets/CJA_RTCDP.svg)

## Diagrama de medidas de proteção para Blueprints do Customer Journey Analytics

* Para obter informações detalhadas e medidas de proteção para latências de ponta a ponta, consulte o [documento de medidas de proteção de implementação](../experience-platform/deployment/guardrails.md)

![Diagrama de medidas de proteção](../experience-platform/assets/CJA_guardrails.svg)

## Perguntas frequentes

* Se um perfil correspondente não existir no RTCDP enviado pelo CJA, um novo perfil será criado ou os públicos-alvo serão registrados somente no CJA para perfis que já estão presentes? Sim, um novo perfil será criado. Como resultado, se a implementação da RTCDP for somente para clientes conhecidos, as regras de público-alvo da CJA devem ser gravadas para filtrar somente perfis com identidades conhecidas. Isso garantirá que a contagem de perfis RTCDP não aumente a partir de perfis anônimos, se não desejar.

* O CJA envia os dados do público-alvo como eventos de pipeline ou um arquivo simples que também vai para o data lake? Os públicos-alvo do CJA são transmitidos por pipeline para o RTCDP Profile Service, no entanto, os dados também são armazenados no data lake como um conjunto de dados.

* Quais identidades o CJA envia? O CJA envia as identidades que foram configuradas como &quot;ID de pessoa&quot; durante a configuração do CJA.

* O que é definido como a identidade primária? Qualquer identidade que o usuário tenha selecionado ao configurar o CJA como a ID de &quot;pessoa&quot; principal.

* O serviço de identidade também processa as mensagens CJA? ou seja, o CJA pode adicionar identidades a um gráfico de identidade de perfil por meio do compartilhamento de público-alvo? Não, o serviço de identidade não processa as mensagens CJA.

## Publicações do blog relacionadas

* [[!DNL Blueprint for Multi-Channel Orchestration in Adobe Experience Platform]](https://medium.com/adobetech/blueprint-for-multi-channel-orchestration-in-adobe-experience-platform-c68317e94184)
* [[!DNL Leveraging External Data Platforms in Adobe Experience Platform Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17)
* [[!DNL Event-Based Triggering on Adobe Experience Platform Orchestration Service using Apache Airflow]](https://medium.com/adobetech/event-based-triggering-on-adobe-experience-platform-orchestration-service-using-apache-airflow-8607b28251f1)
* [[!DNL Adobe Campaign Classic Integration with Journey Orchestration]](https://medium.com/adobetech/adobe-campaign-classic-integration-with-journey-orchestration-ae577653281)
* [[!DNL Demonstrating the Power of Adobe’s New Journey Orchestration Service to Build Personalized Omnichannel Experiences in Real-Time]](https://medium.com/adobetech/demonstrating-the-power-of-adobes-new-journey-orchestration-service-to-build-personalized-aa60d88cd34)
* [[!DNL Journey Orchestration in an Omnichannel World]](https://medium.com/adobetech/journey-orchestration-in-an-omnichannel-world-3a2d32d556d9)
