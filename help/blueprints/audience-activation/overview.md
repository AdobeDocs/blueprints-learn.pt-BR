---
title: Público-alvo e ativação de perfil
description: Ofereça ao público-alvo experiências de cliente ativadas e centradas no perfil com a Plataforma de dados do cliente em tempo real.
solution: Experience Platform, Real-time Customer Data Platform
kt: null
thumbnail: null
exl-id: eeeb4325-d0e8-4fd8-86ab-0b8afdd0b69f
translation-type: tm+mt
source-git-commit: da21d1796eb9a2c9c0f087d82606874ca55bd4ea
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 16%

---


# Público-alvo e ativação de perfil

A ativação de público-alvo e perfil é a chave para o sucesso em um mundo de marketing orientado por dados. Contudo, muitas marcas ainda concentram seus esforços na ativação inicial pelo canal, que por vezes fornece alcance e personalização inconsistentes.

Com uma abordagem que prioriza os canais, cada canal age como um silo, no qual os esforços de personalização se concentram somente na interação do cliente com a marca naquele canal. Esta abordagem não reflete a realidade com que os clientes interagem com as marcas nos vários pontos de contato diferentes. A ativação de público-alvo e perfil permite que as marcas conectem as interações do cliente em vários canais, para fornecer um perfil centralizado e um público-alvo que podem ser ativados em todos os canais.

| Blueprint | Descrição | Aplicativos da Experience Cloud |
|---|---|---|
| **[Audience Activation anônimo](anonymous.md)** | <ul><li>Direcione públicos-alvos na Web e nos canais de publicidade para dados de clientes anônimos e comportamentais.</li><li>Integre a dados de público de terceiros para personalização aprimorada.</li></ul> | <ul><li>Adobe Audience Manager</li></ul> |
| **[Audience Activation online/offline](online-offline.md)** | <ul><li>Ative destinos conhecidos com base em perfis, como provedores de email, redes sociais e destinos de anúncios. </li><li>Use atributos e eventos offline, como pedidos offline, transações, CRM ou dados de fidelidade, juntamente com o comportamento online para direcionamento e personalização online.</li></ul> | <ul><li>Adobe Experience Platform</li><li> [!UICONTROL Plataforma de dados do cliente em tempo real]</li><li>Adobe Audience Manager (opcional)</li></ul> |
| **[Audience and Profile Ativation to Enterprise Destinations](enterprise-destinations.md)** | <ul><li>Replicação e atualização de alterações de perfil e público-alvo em armazenamentos de dados corporativos para casos de uso de ativação e relatórios. </li></ul><ul><li>Inicie uma ação de vendas ou suporte ao cliente por meio da notificação de uma ação do cliente da [!UICONTROL Real-time Customer Data Platform] para sistemas e aplicativos corporativos.</li></ul> | <ul><li>Adobe Experience Platform</li><li>[!UICONTROL Plataforma de dados do cliente em tempo real]</li><li>Ativação de Experience Platform</li><li>Adobe Audience Manager (opcional)</li></ul> |
| **[Hub de atividades do cliente](customer-activity.md)** | <ul><li>Forneça contexto aprofundado do consumidor nas interações com agentes, como suporte e experiências de vendas. Usando a pesquisa de perfil no Experience Platform, os agentes podem receber mais contexto sobre o consumidor, como compras recentes, interações de campanha, tendências, associações de público-alvo e outros atributos e insights armazenados no perfil do cliente em tempo real.</li></ul> | <ul><li>Adobe Experience Platform</li></ul> |

## Grades de proteção para o público-alvo e os planos de ativação de perfil

* [Guias de perfil e segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)

### Diagrama de Proteção

<img src="assets/activation_guardrails.svg" alt="Diagrama de proteção dos Blueprints de Ativação de público-alvo e perfil" style="border:1px solid #4a4a4a" />



### Grades de proteção para avaliação e ativação de segmentos

| Tipo de segmentação | Casos de uso | Frequência | Taxa de transferência | Latência (Avaliação de segmento) | Latência (Ativação de segmento) | Carga de ativação |
|--------------------------|------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Segmentação de borda | Personalização Web/Mobile (Mesma Página/Próxima Página) | A segmentação de borda está atualmente em beta e ainda não está disponível em geral. | - | Aproximadamente 100 milissegundos | Target e Journey Optimizer:<ul><li>Disponível imediatamente na mesma solicitação de personalização.</li></ul><br>Destinos baseados em cookies:<ul><li>Disponível para as decisões da próxima página.</li></ul> | Pesquisas do perfil de borda (Target e Journey Optimizer):<ul><li>Associações de público-alvo</li><li>Atributos do perfil</li></ul><br>Destinos baseados em cookies:<ul><li>Associações de público-alvo</li></ul> |
| Segmentação por streaming | Marketing baseado em acionador (streaming) | Toda vez que um novo evento ou registro de transmissão é assimilado no perfil do cliente em tempo real e a definição do segmento é um segmento de transmissão válido. <br>Consulte a documentação de segmentação para obter orientação sobre a documentação de  [segmentação de critérios de segmento de streaming](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=pt-BR) | Até 1500 eventos por segundo. | Aproximadamente 5 minutos, p95 | Destinos de transmissão:<ul><li>Aproximadamente 1 minuto para Audience Manager e Target</li><li>Aproximadamente 10 minutos para destinos externos ou em microlote, dependendo do destino.</li></ul><br>Destinos agendados:<ul><li>Ativado para destinos externos em lote com base no tempo de delivery do destino agendado.</li></ul> | Destinos de transmissão: <ul><li>Alterações na associação do público-alvo</li><li>Valores de identidade</li><li>Atributos do perfil</li></ul><br>Destinos agendados:<ul><li>Alterações na associação do público-alvo</li><li>Valores de identidade</li><li>Atributos do perfil</li></ul> |
| Segmentação incremental | <li>Mensagens em lote<li>Campanhas e experiências de direcionamento | Uma vez por hora para novos dados que foram assimilados no perfil do cliente em tempo real desde a última avaliação de segmento incremental ou em lote. | Não aplicável | Dependendo do número de perfis, do tamanho dos perfis e do número de segmentos que estão sendo avaliados. | Destinos de transmissão:<ul><li>Aproximadamente 1 minuto para Audience Manager e Target</li><li>Aproximadamente 10 minutos para destinos externos ou em microlote, dependendo do destino.</li></ul><br>Destinos agendados:<ul><li>Ativado para destinos externos em lote com base no tempo de delivery do destino agendado.</li></ul> | Destinos de transmissão: <ul><li>Alterações na associação do público-alvo</li><li>Valores de identidade</li></ul><br>Destinos agendados:<ul><li>Alterações na associação do público-alvo</li><li>Valores de identidade</li><li>Atributos do perfil</li></ul> |
| Segmentação em lote | <ul><li>Mensagens em lote</li><li>Campanhas e experiências de direcionamento</li></ul> | Uma vez por dia, com base em um agendamento predeterminado do conjunto de sistemas ou no início manual da ad hoc por meio da API. | Não aplicável | Dependendo do número de perfis, do tamanho dos perfis e do número de segmentos que estão sendo avaliados.<ul><li>Aproximadamente uma hora por trabalho para até 10 TB de tamanho de armazenamento de perfil</li><li>2 horas por trabalho para 10 TB a 100 TB de tamanho de armazenamento de perfil.</li></ul> | Destinos de transmissão:<ul><li>Aproximadamente 1 minuto para Audience Manager e Target</li><li>Aproximadamente 10 minutos para destinos externos ou em microlote, dependendo do destino.</li></ul><br>Destinos agendados:<ul><li>Ativado para destinos externos em lote com base no tempo de delivery do destino agendado.</li></ul> | Destinos de transmissão: <ul><li>Alterações na associação do público-alvo</li><li>Valores de identidade</li></ul><br>Destinos agendados:<ul><li>Alterações na associação do público-alvo</li><li>Valores de identidade</li><li>Atributos do perfil</li></ul> |

### Grades de proteção para compartilhamento de público em aplicativos cruzados

| Integrações de aplicativos de público-alvo | Casos de uso | Frequência | Taxa de transferência/volume | Latência (Avaliação de segmentos) | Latência (Ativação de segmento) |
|-|-|-|-|-|-|
| Plataforma de dados do cliente em tempo real para o Audience Manager | Enriquecer publicidade de terceiros com públicos de perfil conhecidos | Dependendo do tipo de segmentação - consulte a tabela de medidas de proteção de segmentação acima. | Dependendo do tipo de segmentação - consulte a tabela de medidas de proteção de segmentação acima. | Dependendo do tipo de segmentação - consulte a tabela de medidas de proteção de segmentação acima. | <ul><li>Em minutos da conclusão da avaliação do segmento.</li><li>A sincronização da configuração inicial do público-alvo entre a RTCDP e o AAM leva aproximadamente 4 horas.</li><li>As associações de público-alvo realizadas durante o período de 4 horas serão gravadas em AAM no trabalho de segmentação em lote subsequente como associações de público-alvo &quot;existentes&quot;.</li></ul> |
| Adobe Analytics para Audience Manager | Enriqueça a publicidade de terceiros com públicos baseados em comportamento granular |  | Por padrão, no máximo 75 públicos podem ser compartilhados para cada conjunto de relatórios do Adobe Analytics. Se uma licença de Audience Manager for usada, não há limite. |  |  |
| Adobe Analytics para a plataforma de dados do cliente em tempo real | Não disponível atualmente. | Não disponível atualmente | Não disponível atualmente | Não disponível atualmente | Não disponível atualmente |


### Ativação de atributos e identidades

* [!UICONTROL A ] Plataforma de dados do cliente em tempo real pode ativar associações de público-alvo, bem como alterações de atributo e de identidade que ocorrem para perfis que são membros de segmentos selecionados para ativação. Se o objetivo for ativar atributos ou identidades, você deve definir um segmento global que inclua todos os perfis para os quais as atualizações de atributo e identidade são enviadas. Nesse ponto, é possível selecionar o segmento e os atributos desejados para ativar como parte da configuração de destino.
* Observe que os destinos em lote não suportam a ativação de eventos de alteração somente de atributo. As associações de público-alvo completo ou incremental podem ser enviadas junto com os atributos selecionados para ativação, mas você não pode ativar eventos de alteração somente de atributo por meio de destinos em lote.

### Ativação de segmentos em lote para destinos de streaming

* A Ativação de segmentos em lote para destinos de transmissão é compatível. Os trabalhos de segmento em lote colocam mensagens no pipeline uma vez que o trabalho do segmento é concluído para ativação de streaming

### Ativação de segmentos de transmissão para destinos em lote

* A ativação de segmento de transmissão para destinos em lote é suportada. A programação de destino de lote exporta associações de segmento de perfil com base na programação de destino de lote. Isso inclui associações de segmento determinadas por meio de métodos de streaming e lote.

### Ativação de eventos de experiência

* Não há suporte para a ativação de eventos de experiência bruta. Para ativar em relação aos eventos de experiência, um segmento deve ser criado com as regras necessárias que incluem ou excluem a lógica do evento de experiência. Isso cria um segmento definido em relação aos eventos de experiência, e a associação de segmento pode ser ativada como um proxy para ativar eventos de experiência bruta. Além disso, considere usar [!UICONTROL o Lado do Servidor do Launch] para ativar eventos de experiência bruta coletados pelo SDK.


## Publicações do blog relacionadas

* [[!DNL Blueprints for Audience Activation in Adobe Experience Platform]](https://medium.com/adobetech/a-blueprint-for-audience-activation-in-adobe-experience-platform-b2b30fae90fd)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
