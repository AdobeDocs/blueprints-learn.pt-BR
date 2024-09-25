---
title: Customer Journey Analytics com blueprint do Real-time Customer Data Platform
description: Unifique e analise dados e comportamentos do cliente em toda a jornada dele no Customer Journey Analytics e publique o público-alvo do CJA para o RTCDP
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 9e1ba723-63f2-4622-ba67-f2a315c3ba0c
source-git-commit: 9fe44d93dcc05711c77ce1325b6549bb6c27a860
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 94%

---

# Customer Journey Analytics com blueprint do Real-time Customer Data Platform

Crie e publique públicos-alvo identificados no Customer Journey Analytics (CJA) para o Perfil do cliente em tempo real na Adobe Experience Platform para direcionamento e personalização do cliente. Ideal para criar públicos-alvo usando dados históricos ou públicos-alvo mais refinados por meio da filtragem granular e campos calculados no Customer Journey Analytics.

## Guia de publicação do público do Customer Journey Analytics

Consulte a documentação a seguir para obter orientação sobre a implementação e a configuração na publicação de públicos do Customer Journey Analytics para a Real-time Customer Data Platform. [Documentação](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=pt-BR)

## Arquitetura de blueprints do Customer Journey Analytics

![Diagrama da arquitetura](assets/CJA.svg){zoomable="yes"}

## Diagrama de medidas de proteção para blueprints do Customer Journey Analytics

* Para obter informações detalhadas e medidas de proteção para latências de ponta a ponta, consulte o [documento de medidas de proteção de implantação](../experience-platform/deployment/guardrails.md)

![Diagrama de medidas de proteção](../experience-platform/deployment/assets/CJA_guardrails.svg){zoomable="yes"}

## Perguntas frequentes

* Se não existir um perfil correspondente no RTCDP que tenha sido enviado pelo CJA, um novo perfil será criado ou os públicos-alvo somente serão registrados no CJA para os perfis que já estiverem presentes? Sim, um novo perfil será criado. Como resultado, se a implantação da RTCDP for somente para clientes conhecidos, as regras de público-alvo do CJA devem ser gravadas para filtrar somente perfis com identidades conhecidas. Dessa forma, será possível garantir que a contagem de perfis RTCDP não aumente com base em perfis anônimos, se isso não for desejado.

* Quais identidades são enviadas pelo CJA? O CJA envia as identidades que foram definidas como &quot;ID de pessoa&quot; durante a configuração do CJA.

* O que é definido como identidade primária? Qualquer identidade que o usuário tenha selecionado ao configurar o CJA como ID de &quot;pessoa&quot; principal.

* O serviço de identidade também processa as mensagens do CJA? Ou seja, o CJA pode adicionar identidades a um gráfico de identidade de perfil por meio do compartilhamento de público? Não, o serviço de identidade não processa as mensagens do CJA.