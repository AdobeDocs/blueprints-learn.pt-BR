---
title: Audience and Profile Ativation to Enterprise Destinations Blueprint
description: Audience and Profile Ativation to Enterprise Destinations
solution: Experience Platform,Real-time Customer Data Platform
kt: 7475
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5,None
translation-type: tm+mt
source-git-commit: a63da7d5da3038cf66b5f2c99e117d4aa5b21cc1
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Audience and Profile Ativation to Enterprise Destinations Blueprint

Replicação e atualização de alterações de perfil e público-alvo em armazenamentos de dados corporativos para casos de uso de ativação e relatórios. <!-- This sentence is difficult to mentally process because there's no verb. Describe what the customer can do with this feature. The first paragraph on a page should not be an abstract description.-->

Inicie uma ação de vendas ou suporte ao cliente por meio da notificação de uma ação do cliente da [!UICONTROL Real-time Customer Data Platform] para sistemas e aplicativos corporativos. <!-- What kinds of sales or support actions? You might add a "For example...." The content in these blueprints should be more simple and friendly.-->

## Casos de uso

* Ativação de perfil e público-alvo para destinos de armazenamento em nuvem ou destinos de fluxo para rastreamento, armazenamento, análise e ativação de dados e insights do cliente em empresas.

## Aplicativos

* Adobe Experience Platform Ativation

## Arquitetura

<img src="assets/enterprise_destination.svg" alt="Arquitetura de referência para o cenário de Ativação Empresarial" style="border:1px solid #4a4a4a" />

## Medidas de proteção

[Diretrizes de perfil e segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)

Limites de latência e de taxa de transferência:

Segmentação de streaming:

* Até 5 minutos para a segmentação de streaming, em até 1500 eventos por segundo
* Até 11 minutos para ativação de streaming

Segmentação em lote:
Uma vez por dia ou manualmente iniciada pela API.

* Aproximadamente 1 hora por trabalho para até 10 TB de tamanho de armazenamento de perfil
* Aproximadamente 2 horas por trabalho para 10 TB a 100 TB de tamanho de armazenamento de perfil

## Etapas da implementação

1. Crie esquemas para os dados que serão assimilados. <!-- Cross-references to these topics would be helpful -->
1. Crie conjuntos de dados para que os dados sejam assimilados.
1. Configure as identidades e os namespaces de identidade corretos no esquema para garantir que os dados assimilados possam se unir a um perfil unificado.
1. Ative os esquemas e conjuntos de dados para processamento de perfis.
1. Configure quaisquer fontes para assimilação de dados.
1. Crie segmentos no Experience Platform, que serão avaliados em lote ou streaming. O sistema determina automaticamente se o segmento é avaliado como lote ou streaming.
1. Configure destinos para compartilhar atributos de perfil e associações de público-alvo com os destinos desejados.

## Considerações sobre a implementação

Ativação de atributos e identidades

* [!UICONTROL A ] Plataforma de dados do cliente em tempo real pode ativar associações de público-alvo, bem como alterações de atributo e de identidade que ocorrem para perfis que são membros de segmentos selecionados para ativação. Se o objetivo for ativar atributos ou identidades, você deve definir um segmento global que inclua todos os perfis para os quais as atualizações de atributo e identidade são enviadas. Nesse ponto, é possível selecionar o segmento e os atributos desejados para ativar como parte da configuração de destino.
* Observe que os destinos em lote não suportam a ativação de eventos de alteração somente de atributo. As associações de público-alvo completo ou incremental podem ser enviadas junto com os atributos selecionados para ativação, mas você não pode ativar eventos de alteração somente de atributo por meio de destinos em lote.

Ativação de segmentos em lote para destinos de streaming

* A Ativação de segmentos em lote para destinos de transmissão é compatível. Os trabalhos de segmento em lote colocam mensagens no pipeline uma vez que o trabalho do segmento é concluído para ativação de streaming

Ativação de segmentos de transmissão para destinos em lote

* A ativação de segmento de transmissão para destino em lote é suportada. A programação de destino de lote exporta associações de segmento de perfil com base na programação de destino de lote. Isso inclui associações de segmento determinadas por meio de métodos de streaming e lote.

Ativação de eventos de experiência

* Não há suporte para a ativação de eventos de experiência bruta. Para ativar em relação aos eventos de experiência, um segmento deve ser criado com as regras necessárias que incluem ou excluem a lógica do evento de experiência. Isso cria um segmento definido em relação aos eventos de experiência, e a associação de segmento pode ser ativada como um proxy para ativar eventos de experiência bruta. Além disso, considere usar [!UICONTROL o Lado do Servidor do Launch] para ativar eventos de experiência bruta coletados pelo SDK.

## Documentação relacionada

* [Documentação de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)
* [Visão geral dos destinos de armazenamento na nuvem](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=en#catalog)
* [Destino HTTP](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/http-destination.html?lang=en#overview)
* [[!UICONTROL Descrição do produto da ] Plataforma de dados do cliente em tempo real](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Diretrizes de perfil e segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Documentação de segmentação](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)

## Vídeos e Tutorials relacionados

* [[!UICONTROL Visão geral da ] plataforma de dados do cliente em tempo real](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demonstração da plataforma de dados do cliente em tempo  [!UICONTROL real]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Criar segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
