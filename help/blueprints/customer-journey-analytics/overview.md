---
title: Customer Journey Analytics    blueprints
description: Unificação e análise de dados e comportamentos do cliente a partir da jornada do cliente
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 3bb2dada-f4cd-43f7-a0d0-f276510ad224
source-git-commit: d7901280f1bc23e6d37bcb285f20343c5ed8b46e
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 100%

---

# Customer Journey Analytics    blueprints

O Customer Journey Analytics apresenta como as marcas podem unificar os dados e o comportamento do cliente oriundos de vários canais e fontes de interação. O objetivo é criar uma visualização com base na jornada de todas as interações com o cliente. É possível elaborar relatórios e análises no serviço de aplicativos do Customer Journey Analytics para avaliar e obter insights da interação com o cliente e de padrões de comportamento.

Uma lista completa de casos de uso do Customer Journey Analytics pode ser encontrada na documentação do Customer Journey Analytics localizada aqui.

## Casos de uso do Customer Journey Analytics

[Casos de uso comuns incluem:](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/cja-usecases.html?lang=pt-BR)

* Criar e publicar públicos na Real-time Customer Data Platform
* Caminhos de conversão do início ao fim
* Envolvimento e conversão de canal
* Conteúdo mais visualizado
* Principais categorias e produtos
* Quais campanhas resultaram em conversão e aumento de envolvimento
* Análise de uso de ferramentas para otimizar experiências de autoatendimento

## Arquitetura do Customer Journey Analytics

![Diagrama da arquitetura](assets/CJA.svg){zoomable=&quot;yes&quot;}

Os casos de uso principais de exemplo incluíram o seguinte.
| Blueprint | Descrição |  Aplicativos da Experience Cloud |
|---|---|---|
| **[Análise de jornada entre canais](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/cross-channel.html?lang=pt-BR)**  | <ul><li>Tenha uma visualização consolidada única do comportamento do cliente em vários canais ao unificar dados de várias propriedades da Web, móveis e offline.</li></ul> | <ul><li>Adobe Experience Platform</li><li>Customer Journey Analytics</li><li>Adobe Analytics (opcional)</li></ul>|
| **[Publicar públicos na Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=pt-BR)** | <ul><li>Crie e publique públicos identificados no Customer Journey Analytics (CJA) para o Perfil do cliente em tempo real na Adobe Experience Platform para direcionamento e personalização do cliente. Ideal para criar públicos-alvo usando dados históricos ou públicos-alvo mais refinados por meio da filtragem granular e campos calculados no Customer Journey Analytics.</li></ul> | <ul><li>Real-time Customer Data Platform</li><li>Customer Journey Analytics</li> |
| **[Análise da jornada da diminuição de chamadas](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/call-center.html?lang=pt-BR)** | <ul><li>Determine quais comportamentos são mais indicativos nos resultados de chamadas atendidas por agentes ao reunir dados da central de atendimento com dados da web, dispositivos móveis e outros dados de interação.</li><li>É possível usar esses insights para aprimorar a experiência do cliente e encurtar o caminho para interações atendidas por agentes por meio de conteúdo e ferramentas de autoatendimento.  </li></ul> | <ul><li>Adobe Experience Platform</li><li>Customer Journey Analytics</li> |

## Diagrama de medidas de proteção para blueprints do Customer Journey Analytics

* Para obter informações detalhadas e medidas de proteção para latências de ponta a ponta, consulte o [documento de medidas de proteção de implantação](../experience-platform/deployment/guardrails.md)

![Diagrama de medidas de proteção](../experience-platform/deployment/assets/CJA_guardrails.svg){zoomable=&quot;yes&quot;}

## Publicações do blog relacionadas

* [[!DNL Blueprint for Multi-Channel Orchestration in Adobe Experience Platform]](https://medium.com/adobetech/blueprint-for-multi-channel-orchestration-in-adobe-experience-platform-c68317e94184){target="_blank"}
* [[!DNL Leveraging External Data Platforms in Adobe Experience Platform Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17){target="_blank"}
* [[!DNL Event-Based Triggering on Adobe Experience Platform Orchestration Service using Apache Airflow]](https://medium.com/adobetech/event-based-triggering-on-adobe-experience-platform-orchestration-service-using-apache-airflow-8607b28251f1){target="_blank"}
* [[!DNL Adobe Campaign Classic Integration with Journey Orchestration]](https://medium.com/adobetech/adobe-campaign-classic-integration-with-journey-orchestration-ae577653281){target="_blank"}
* [[!DNL Demonstrating the Power of Adobe's New Journey Orchestration Service to Build Personalized Omnichannel Experiences in Real-Time]](https://medium.com/adobetech/demonstrating-the-power-of-adobes-new-journey-orchestration-service-to-build-personalized-aa60d88cd34){target="_blank"}
* [[!DNL Journey Orchestration in an Omnichannel World]](https://medium.com/adobetech/journey-orchestration-in-an-omnichannel-world-3a2d32d556d9){target="_blank"}
