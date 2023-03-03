---
title: Customer Journey Analytics com a Real-time Customer Data Platform   blueprint
description: Unifique e analise dados e comportamentos do cliente em toda a jornada dele no Customer Journey Analytics e publique o público do CJA para o RTCDP
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 9e1ba723-63f2-4622-ba67-f2a315c3ba0c
source-git-commit: 2d7d2fff6c430b66e4a2935d4c68b5a8b9ecfae2
workflow-type: ht
source-wordcount: '398'
ht-degree: 100%

---

# Customer Journey Analytics com a Real-time Customer Data Platform   blueprint

Crie e publique públicos-alvo identificados no Customer Journey Analytics (CJA) para o Perfil do cliente em tempo real na Adobe Experience Platform para direcionamento e personalização do cliente. Ideal para criar públicos-alvo usando dados históricos ou públicos-alvo mais refinados por meio da filtragem granular e campos calculados no Customer Journey Analytics.

## Guia de publicação do público do Customer Journey Analytics

Consulte a documentação a seguir para obter orientação sobre a implementação e a configuração na publicação de públicos do Customer Journey Analytics para a Real-time Customer Data Platform. [Documentação](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=pt-BR)

## Arquitetura de blueprints do Customer Journey Analytics

![Diagrama da arquitetura](assets/CJA.svg){zoomable=&quot;yes&quot;}

## Diagrama de medidas de proteção para blueprints do Customer Journey Analytics

* Para obter informações detalhadas e medidas de proteção para latências de ponta a ponta, consulte o [documento de medidas de proteção de implantação](../experience-platform/deployment/guardrails.md)

![Diagrama de medidas de proteção](../experience-platform/assets/CJA_guardrails.svg){zoomable=&quot;yes&quot;}

## Perguntas frequentes

* Se não existir um perfil correspondente no RTCDP que tenha sido enviado pelo CJA, um novo perfil será criado ou os públicos-alvo somente serão registrados no CJA para os perfis que já estiverem presentes? Sim, um novo perfil será criado. Como resultado, se a implantação da RTCDP for somente para clientes conhecidos, as regras de público-alvo do CJA devem ser gravadas para filtrar somente perfis com identidades conhecidas. Dessa forma, será possível garantir que a contagem de perfis RTCDP não aumente com base em perfis anônimos, se isso não for desejado.

* O CJA envia os dados do público-alvo como eventos de pipeline ou como um arquivo simples que também vai para o data lake? Os públicos-alvo do CJA são transmitidos por meio de pipelines para o Serviço de perfis do RTCDP; porém, os dados também são armazenados no data lake como um conjunto de dados.

* Quais identidades são enviadas pelo CJA? O CJA envia as identidades que foram definidas como &quot;ID de pessoa&quot; durante a configuração do CJA.

* O que é definido como identidade primária? Qualquer identidade que o usuário tenha selecionado ao configurar o CJA como ID de &quot;pessoa&quot; principal.

* O serviço de identidade também processa as mensagens do CJA? Ou seja, o CJA pode adicionar identidades a um gráfico de identidade de perfil por meio do compartilhamento de público? Não, o serviço de identidade não processa as mensagens do CJA.

## Publicações do blog relacionadas

* [[!DNL Blueprint for Multi-Channel Orchestration in Adobe Experience Platform]](https://medium.com/adobetech/blueprint-for-multi-channel-orchestration-in-adobe-experience-platform-c68317e94184)
* [[!DNL Leveraging External Data Platforms in Adobe Experience Platform Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17)
* [[!DNL Event-Based Triggering on Adobe Experience Platform Orchestration Service using Apache Airflow]](https://medium.com/adobetech/event-based-triggering-on-adobe-experience-platform-orchestration-service-using-apache-airflow-8607b28251f1)
* [[!DNL Adobe Campaign Classic Integration with Journey Orchestration]](https://medium.com/adobetech/adobe-campaign-classic-integration-with-journey-orchestration-ae577653281)
* [[!DNL Demonstrating the Power of Adobe's New Journey Orchestration Service to Build Personalized Omnichannel Experiences in Real-Time]](https://medium.com/adobetech/demonstrating-the-power-of-adobes-new-journey-orchestration-service-to-build-personalized-aa60d88cd34)
* [[!DNL Journey Orchestration in an Omnichannel World]](https://medium.com/adobetech/journey-orchestration-in-an-omnichannel-world-3a2d32d556d9)
