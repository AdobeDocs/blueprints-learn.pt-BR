---
title: Audience Activation Blueprint online/offline
description: Audience Activation online/offline.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
translation-type: tm+mt
source-git-commit: 009a55715b832c3167e9a3413ccf89e0493227df
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 81%

---

# Audience Activation Blueprint online/offline

Use atributos e eventos offline, como pedidos, transações, dados de CRM ou de fidelização, com comportamentos online para direcionamento e personalização online.

Ative públicos para destinos conhecidos com base no perfil, como provedores de email, redes sociais e destinos de publicidade.

## Casos de uso

* Direcionamento de públicos para públicos conhecidos em destinos sociais e de publicidade.
* Personalização online com atributos online e offline.
* Ative públicos para canais conhecidos, como email e SMS.

## Aplicativos

* Adobe Experience Platform
* [!UICONTROL Plataforma de dados do cliente em tempo real]

## Arquitetura

<img src="assets/onoff.svg" alt="Arquitetura de referência para o Blueprint de Audience Activation online/offline" style="border:1px solid #4a4a4a" />

## Medidas de proteção

* [Guias de perfil e segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)
* Os trabalhos de segmentos em lote são executados uma vez ao dia, com base na programação pré-definida. Os trabalhos de exportação de segmentos são executados em seguida, antes da entrega programada do destino. Observe que os trabalhos de segmentos em lote e de entregas de destino são executados separadamente. O desempenho dos trabalhos de segmentos em lote e do trabalho de exportação depende da quantidade de perfis, do tamanho dos perfis e da quantidade de segmentos que estão sendo avaliados.
* Trabalhos de segmentos por streaming são avaliados em minutos, a partir da chegada dos dados por streaming ao perfil. Após isso, os trabalhos gravam imediatamente a associação dos segmentos ao perfil e enviam um evento ao qual os aplicativos devem se cadastrar.
* A associação de segmentos por streaming acontece imediatamente para destinos de streaming, e é entregue em eventos de associação de um só segmento ou eventos de um microlote de múltiplos perfis, dependendo dos padrões de assimilação do destino. Destinos programados inicializarão um trabalho de exportação de segmentos a partir do perfil, antes da entrega, para quaisquer segmentos avaliados na transmissão, fornecidos por meio de entrega programada de segmentos em lote.
* Para compartilhar [!UICONTROL Associação de segmento da Plataforma de dados do cliente em tempo real] no Audience Manager, isso acontece em minutos para segmentos de transmissão e em minutos após a conclusão da avaliação do segmento de lote para segmentação de lote.
* Segmentos são compartilhados da Experience Platform para o Audience Manager em minutos a partir da realização de segmentos, seja pelo método de streaming ou pelo método de avaliação por lote. Há uma sincronização de configuração de segmento inicial entre o Experience Platform e o Audience Manager depois que o segmento é criado inicialmente, após ~4 horas, as associações de segmento do Experience Platform podem começar a ser realizadas em perfis do Audience Manager. A Associação de públicos não será feita no Audience Manager até o próximo trabalho de segmento, em que associações de segmentos “existentes” estejam compartilhadas. Isso acontece no caso da associação realizada antes da configuração do compartilhamento de públicos da Experience Platform e do Audience Manager, ou antes de os metadados do público estarem sincronizados da Experience Platform para o Audience Manager.
* Trabalhos de destinos em lote ou por streaming podem compartilhar atualizações de atributos de perfil, assim como associações de segmentos.
* Trabalhos de segmentação por streaming para destinos de streaming compartilham somente atualizações de associação de segmentos.

## Etapas de implementação

1. Configure esquemas e conjuntos de dados na Experience Platform.
1. Configure as identidades certas e os namespaces de identidade no esquema para assegurar que os dados assimilados possam aderir a um perfil unificado.
1. Habilite esquemas e conjuntos de dados para o Perfil.
1. Assimile os dados na Platform.
1. Provisione [!UICONTROL Plataforma de dados do cliente em tempo real] o compartilhamento de segmentos entre o Experience Platform e o Audience Manager para que os públicos-alvo definidos no Experience Platform sejam compartilhados com o Audience Manager.
1. Crie Segmentos na Experience Platform para serem avaliados em lote ou por streaming. O sistema decide automaticamente se o segmento é avaliado em lote ou por streaming.
1. Configure destinos para compartilhar atributos de perfil e associações de públicos com destinos desejados.

## Considerações de implementação

* Compartilhar dados de perfil com destinos exige a inclusão de valor específico de identidade, usado pelo destino na carga de destino. Qualquer identidade necessária para um destino deve ser assimilada na Platform e configurada como uma identidade para o [!UICONTROL Perfil do cliente em tempo real].

* Para cenários de ativação em que os públicos são compartilhados da Experience Platform para o Audience Manager, todas as identidades incluídas no [!UICONTROL Perfil de cliente em tempo real] são compartilhadas com o Audience Manager. É possível compartilhar os públicos da Experience Platform por meio dos destinos do Audience Manager, quando as identidades de destino necessárias estiverem incluídas no [!UICONTROL Perfil de cliente em tempo real]. Ou também onde as identidades no [!UICONTROL Perfil de cliente em tempo real] possam ser relacionadas às identidades de destino vinculadas ao Audience Manager.

## Documentos relacionados

* [Descrição do produto Plataforma de dados do cliente em tempo real](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform.html)
* [Diretrizes de perfil e segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Documentação de segmentação](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=pt-BR)
* [Documentação de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=pt-BR)

## Vídeos e tutoriais relacionados

* [Visão geral da Plataforma de dados do cliente em tempo real](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=pt-BR)
* [[!UICONTROL Demonstração da Plataforma de dados do cliente em tempo real]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=pt-BR)
* [Criação de segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=pt-BR)
