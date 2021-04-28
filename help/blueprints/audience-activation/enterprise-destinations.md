---
title: Audience and Profile Ativation to Enterprise Destinations Blueprint
description: Audience and Profile Ativation to Enterprise Destinations
solution: Experience Platform,Real-time Customer Data Platform
kt: 7475
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5,None
translation-type: tm+mt
source-git-commit: 3a4a0e2387e72d378589edfdc5b0c27a50c42db5
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Audience and Profile Ativation to Enterprise Destinations Blueprint

Compartilhe alterações de perfil e público-alvo e eventos em streaming ou lote da [!UICONTROL Plataforma de dados do cliente em tempo real] para armazenamentos e aplicativos de dados corporativos. Esses eventos de perfil e público-alvo podem ser usados para iniciar uma ação de vendas ou suporte ao cliente, como acompanhar um processo de aplicativo abandonado ou registro de webinar ou atualizar aplicativos corporativos com os atributos e informações mais recentes do cliente da [!UICONTROL Plataforma de dados do cliente em tempo real].

## Casos de uso

* Ativação de perfil e público-alvo para destinos de armazenamento em nuvem ou destinos de fluxo para rastreamento, armazenamento, análise e ativação de dados e insights do cliente em empresas.

## Aplicativos

* Adobe Experience Platform Ativation

## Arquitetura

<img src="assets/enterprise_destination.svg" alt="Arquitetura de referência para o cenário de Ativação Empresarial" style="border:1px solid #4a4a4a" />

## Medidas de proteção

[Guias de perfil e segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)

### Grades de proteção para avaliação e ativação de segmentos

| Tipo de segmentação | Frequência | Taxa de transferência | Latência (Avaliação de segmento) | Latência (Ativação de segmento) | Carga de ativação |
|---|---|---|---|---|---|
| Segmentação de borda | A segmentação de borda está atualmente em beta e permite que a segmentação válida em tempo real seja avaliada na rede de borda do Experience Platform para obter decisões de página em tempo real e em tempo real, por meio do Adobe Target e do Adobe Journey Optimizer. |  | ~100 ms | Disponível imediatamente para personalização no Adobe Target, para pesquisas de perfil no Perfil do Edge e para ativação via destinos baseados em cookies. | Associações de público-alvo disponíveis no Edge para pesquisas de perfil e destinos com base em cookies.<br>Associações de público-alvo e atributos de perfil estão disponíveis para Adobe Target e Journey Optimizer. |
| Segmentação por streaming | Toda vez que um novo evento ou registro de transmissão é assimilado no perfil do cliente em tempo real e a definição do segmento é um segmento de transmissão válido. <br>Consulte a  [documentação ](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=pt-BR) de segmentação para obter orientação sobre os critérios de segmento de streaming | Até 1500 eventos por segundo. | ~ p95 &lt;5 min | Destinos de transmissão: As associações de público-alvo de streaming são ativadas em aproximadamente 10 minutos ou em microlote com base nos requisitos do destino.<br>Destinos agendados: As associações de público-alvo de streaming são ativadas em lote com base no tempo agendado de delivery do destino. | Destinos de transmissão: Alterações na associação do público-alvo, valores de identidade e atributos do perfil.<br>Destinos agendados: Alterações na associação do público-alvo, valores de identidade e atributos do perfil. |
| Segmentação incremental | Uma vez por hora para novos dados que foram assimilados no perfil do cliente em tempo real desde a última avaliação de segmento incremental ou em lote. |  |  | Destinos de transmissão: As associações de público-alvo incremental são ativadas em aproximadamente 10 minutos ou em microlote com base nos requisitos do destino.<br>Destinos agendados: As associações de público-alvo incremental são ativadas em lote com base no tempo agendado de entrega do destino. | Destinos de transmissão: Alterações de associação de público-alvo e valores de identidade somente.<br>Destinos agendados: Alterações na associação do público-alvo, valores de identidade e atributos do perfil. |
| Segmentação em lote | Uma vez por dia, com base em um agendamento predeterminado do conjunto de sistemas ou no início manual da ad hoc por meio da API. |  | Aproximadamente uma hora por trabalho para até 10 TB de tamanho de armazenamento de perfil, 2 horas por trabalho para 10 TB a 100 TB de tamanho de armazenamento de perfil. O desempenho do trabalho do segmento em lote depende do número de perfis, do tamanho dos perfis e do número de segmentos que estão sendo avaliados. | Destinos de transmissão: As associações de público-alvo em lote são ativadas aproximadamente 10 após a conclusão da avaliação de segmentação ou em microlote com base nos requisitos do destino.<br>Destinos agendados: As associações de público-alvo em lote são ativadas com base no tempo agendado de entrega do destino. | Destinos de transmissão: Alterações de associação de público-alvo e valores de identidade somente.<br>Destinos agendados: Alterações na associação do público-alvo, valores de identidade e atributos do perfil. |



## Etapas de implementação

1. Crie esquemas para os dados que serão assimilados.
1. Crie conjuntos de dados para que os dados sejam assimilados.
1. Configure as identidades certas e os namespaces de identidade no esquema para assegurar que os dados assimilados possam aderir a um perfil unificado.
1. Ative os esquemas e conjuntos de dados para processamento de perfis.
1. Configure quaisquer fontes para assimilação de dados.
1. Crie segmentos no Experience Platform, que serão avaliados em lote ou streaming. O sistema decide automaticamente se o segmento é avaliado em lote ou por streaming.
1. Configure destinos para compartilhar atributos de perfil e associações de públicos com destinos desejados.

## Considerações de implementação

Ativação de atributos e identidades

* [!UICONTROL A ] Plataforma de dados do cliente em tempo real pode ativar associações de público-alvo, bem como alterações de atributo e de identidade que ocorrem para perfis que são membros de segmentos selecionados para ativação. Se o objetivo for ativar atributos ou identidades, você deve definir um segmento global que inclua todos os perfis para os quais as atualizações de atributo e identidade são enviadas. Nesse ponto, é possível selecionar o segmento e os atributos desejados para ativar como parte da configuração de destino.
* Observe que os destinos em lote não suportam a ativação de eventos de alteração somente de atributo. As associações de público-alvo completo ou incremental podem ser enviadas junto com os atributos selecionados para ativação, mas você não pode ativar eventos de alteração somente de atributo por meio de destinos em lote.

Ativação de segmentos em lote para destinos de streaming

* A Ativação de segmentos em lote para destinos de transmissão é compatível. Os trabalhos de segmento em lote colocam mensagens no pipeline uma vez que o trabalho do segmento é concluído para ativação de streaming

Ativação de segmentos de transmissão para destinos em lote

* A ativação de segmento de transmissão para destino em lote é suportada. A programação de destino de lote exporta associações de segmento de perfil com base na programação de destino de lote. Isso inclui associações de segmento determinadas por meio de métodos de streaming e lote.

Ativação de eventos de experiência

* Não há suporte para a ativação de eventos de experiência bruta. Para ativar em relação aos eventos de experiência, um segmento deve ser criado com as regras necessárias que incluem ou excluem a lógica do evento de experiência. Isso cria um segmento definido em relação aos eventos de experiência, e a associação de segmento pode ser ativada como um proxy para ativar eventos de experiência bruta. Além disso, considere usar [!UICONTROL o Lado do Servidor do Launch] para ativar eventos de experiência bruta coletados pelo SDK.

## Documentos relacionados

* [Documentação de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=pt-BR)
* [Visão geral dos destinos de armazenamento na nuvem](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=en#catalog)
* [Destino HTTP](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/http-destination.html?lang=en#overview)
* [Descrição do produto Plataforma de dados do cliente em tempo real](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform.html)
* [Diretrizes de perfil e segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Documentação de segmentação](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)

## Vídeos e tutoriais relacionados

* [Visão geral da Plataforma de dados do cliente em tempo real](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=pt-BR)
* [[!UICONTROL Demonstração da Plataforma de dados do cliente em tempo real]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=pt-BR)
* [Criação de segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=pt-BR)
