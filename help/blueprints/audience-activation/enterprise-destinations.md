---
title: Blueprint de perfis e Audience Activation para destinos empresariais
description: Destinos de perfil e Audience Activation para empresas
solution: Experience Platform,Real-time Customer Data Platform,Target,Audience Manager,Analytics,Experience Cloud Services,Data Collection
kt: 7086
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5
translation-type: tm+mt
source-git-commit: 2fa5fc1def554713b057e1478bdd65a15913e0e4
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---


# Blueprint de perfis e Audience Activation para destinos empresariais

Replicação e atualização de alterações de perfil em armazenamentos de dados corporativos para ativação e casos de uso de relatórios.

Inicie uma ação de vendas ou suporte ao cliente por meio da notificação de uma ação do cliente da Plataforma de dados do cliente em tempo real para sistemas e aplicativos corporativos.

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
Uma vez por dia ou manualmente iniciada ad hoc por meio da API

* Aproximadamente 1 hora por trabalho para até 10 TB de tamanho de armazenamento de perfil
* Aproximadamente 2 horas por trabalho para 10 TB a 100 TB de tamanho de armazenamento de perfil

## Etapas da implementação

1. Criar esquemas para dados a serem assimilados
1. Criar conjuntos de dados para dados a serem assimilados
1. Configure as identidades e os namespaces de identidade corretos no esquema para garantir que os dados assimilados possam se unir a um perfil unificado.
1. Ative os esquemas e conjuntos de dados para processamento de perfis.
1. Configurar quaisquer fontes para assimilação de dados
1. Crie segmentos no Experience Platform, que serão avaliados em lote ou streaming. O sistema determina automaticamente se o segmento é avaliado como lote ou streaming.
1. Configure destinos para compartilhar atributos de perfil e associações de público-alvo com os destinos desejados.

## Considerações sobre a implementação

Ativação de atributos e identidades

* A Plataforma de dados do cliente em tempo real pode ativar associações de público-alvo, bem como alterações de atributo e de identidade que ocorrem para perfis que são membros de segmentos que foram selecionados para ativação. Sendo assim, se o caso de uso for ativar atributos e/ou identidades, um segmento global deve ser definido e incluir todos os perfis para os quais as atualizações de atributo/identidade serão enviadas devem ser definidas. Depois que isso estiver em vigor, o segmento e os atributos desejados para ativar poderão ser selecionados como parte da configuração de destino.
* Observe que os destinos em lote não suportam a ativação de atributos somente eventos de alteração. A associação de público-alvo cheia ou incremental pode ser enviada juntamente com os atributos selecionados para ativação, mas os eventos de alteração de atributo somente não podem ser ativados por destinos de lote.

Ativação de segmentos em lote para destinos de transmissão

* A Ativação de segmentos em lote para destinos de transmissão é compatível. Os trabalhos de segmento em lote colocam mensagens no pipeline uma vez que o trabalho do segmento é concluído para ativação de streaming

Ativação de segmento de transmissão para destinos em lote

* A ativação de segmento de transmissão para destino em lote é suportada. O agendamento de destino em lote exportará associações de segmentos dos perfis com base no agendamento de destino em lote. Isso inclui associações de segmento determinadas por meio de métodos de streaming e lote.

Ativação de eventos de experiência

* No momento, a ativação de eventos de experiência bruta não é compatível. Para ativar em relação aos eventos de experiência, um segmento deve ser criado com as regras necessárias que incluem/excluem a lógica do evento de experiência para ser ativada. Isso cria um segmento definido em relação aos eventos de experiência, e a associação de segmento pode ser ativada como um proxy para ativar eventos de experiência bruta. Além disso, considere o aproveitamento do lado do servidor do Launch para a ativação de eventos de experiência brutos coletados pelo SDK.

## Documentação relacionada

* [Descrição do produto da Plataforma de dados do cliente em tempo real](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Diretrizes de perfil e segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Documentação de segmentação](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Documentação de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)

## Vídeos e Tutorials relacionados

* [Visão geral da plataforma de dados do cliente em tempo real](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demonstração da plataforma de dados do cliente em tempo real](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Criar segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
