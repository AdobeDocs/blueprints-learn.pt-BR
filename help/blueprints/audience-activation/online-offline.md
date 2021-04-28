---
title: Audience Activation Blueprint online/offline
description: Audience Activation online/offline.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
translation-type: tm+mt
source-git-commit: 24b6ffe3021389d33e84688a8f1a90711ca4b772
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

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

### Grades de proteção para avaliação e ativação de segmentos

| Tipo de segmentação | Frequência | Taxa de transferência | Latência (Avaliação de segmento) | Latência (Ativação de segmento) | Carga de ativação |
|---|---|---|---|---|---|
| Segmentação de borda | A segmentação de borda está atualmente em beta e permite que a segmentação válida em tempo real seja avaliada na rede de borda do Experience Platform para obter decisões de página em tempo real e em tempo real, por meio do Adobe Target e do Adobe Journey Optimizer. |  | ~100 ms | Disponível imediatamente para personalização no Adobe Target, para pesquisas de perfil no Perfil do Edge e para ativação via destinos baseados em cookies. | Associações de público-alvo disponíveis no Edge para pesquisas de perfil e destinos com base em cookies.<br>Associações de público-alvo e atributos de perfil estão disponíveis para Adobe Target e Journey Optimizer. |
| Segmentação por streaming | Toda vez que um novo evento ou registro de transmissão é assimilado no perfil do cliente em tempo real e a definição do segmento é um segmento de transmissão válido. <br>Consulte a  [documentação ](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=pt-BR) de segmentação para obter orientação sobre os critérios de segmento de streaming | Até 1500 eventos por segundo. | ~ p95 &lt;5 min | Destinos de transmissão: As associações de público-alvo de streaming são ativadas em aproximadamente 10 minutos ou em microlote com base nos requisitos do destino.<br>Destinos agendados: As associações de público-alvo de streaming são ativadas em lote com base no tempo agendado de delivery do destino. | Destinos de transmissão: Alterações na associação do público-alvo, valores de identidade e atributos do perfil.<br>Destinos agendados: Alterações na associação do público-alvo, valores de identidade e atributos do perfil. |
| Segmentação incremental | Uma vez por hora para novos dados que foram assimilados no perfil do cliente em tempo real desde a última avaliação de segmento incremental ou em lote. |  |  | Destinos de transmissão: As associações de público-alvo incremental são ativadas em aproximadamente 10 minutos ou em microlote com base nos requisitos do destino.<br>Destinos agendados: As associações de público-alvo incremental são ativadas em lote com base no tempo agendado de entrega do destino. | Destinos de transmissão: Alterações de associação de público-alvo e valores de identidade somente.<br>Destinos agendados: Alterações na associação do público-alvo, valores de identidade e atributos do perfil. |
| Segmentação em lote | Uma vez por dia, com base em um agendamento predeterminado do conjunto de sistemas ou no início manual da ad hoc por meio da API. |  | Aproximadamente uma hora por trabalho para até 10 TB de tamanho de armazenamento de perfil, 2 horas por trabalho para 10 TB a 100 TB de tamanho de armazenamento de perfil. O desempenho do trabalho do segmento em lote depende do número de perfis, do tamanho dos perfis e do número de segmentos que estão sendo avaliados. | Destinos de transmissão: As associações de público-alvo em lote são ativadas aproximadamente 10 após a conclusão da avaliação de segmentação ou em microlote com base nos requisitos do destino.<br>Destinos agendados: As associações de público-alvo em lote são ativadas com base no tempo agendado de entrega do destino. | Destinos de transmissão: Alterações de associação de público-alvo e valores de identidade somente.<br>Destinos agendados: Alterações na associação do público-alvo, valores de identidade e atributos do perfil. |

### Grades de proteção para compartilhamento de público em aplicativos cruzados

| Integrações do aplicativo de público-alvo | Frequência | Throughput/Volume | Latência (Avaliação de segmento) | Latência (Ativação de segmento) |
|---|---|---|---|---|
| Plataforma de dados do cliente em tempo real para o Audience Manager | Dependendo do tipo de segmentação - consulte a tabela de medidas de proteção de segmentação acima. | Dependendo do tipo de segmentação - consulte a tabela de medidas de proteção de segmentação acima. | Dependendo do tipo de segmentação - consulte a tabela de medidas de proteção de segmentação acima. | Em minutos da conclusão da avaliação do segmento.<br>A sincronização da configuração inicial do público-alvo entre a Plataforma de dados do cliente em tempo real e o Audience Manager demora aproximadamente 4 horas.<br>Todas as associações de público-alvo realizadas durante o período de 4 horas serão gravadas no Audience Manager no trabalho subsequente de segmentação em lote como associações de público-alvo &quot;existentes&quot;. |
| Adobe Analytics para Audience Manager |  | Por padrão, um máximo de 75 públicos-alvo pode ser compartilhado para cada conjunto de relatórios do Adobe Analytics. Se uma licença do Audience Manager for usada, não há limite para o número de públicos-alvo que podem ser compartilhados entre o Adobe Analytics e o Adobe Target ou Adobe Audience Manager e Adobe Target. |  |  |
| Adobe Analytics para a plataforma de dados do cliente em tempo real | Não disponível no momento | Não disponível no momento | Não disponível no momento | Não disponível no momento |





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
* [Documentação de segmentação](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Documentação de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=pt-BR)

## Vídeos e tutoriais relacionados

* [Visão geral da Plataforma de dados do cliente em tempo real](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=pt-BR)
* [[!UICONTROL Demonstração da Plataforma de dados do cliente em tempo real]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=pt-BR)
* [Criação de segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=pt-BR)
