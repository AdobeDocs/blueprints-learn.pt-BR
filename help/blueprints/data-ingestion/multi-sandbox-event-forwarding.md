---
title: Coleta de dados de encaminhamento de eventos de várias sandboxes
description: Saiba como os dados coletados com os SDKs da Web e móvel do Experience Platform podem ser configurados para coletar um único evento e encaminhados para várias sandboxes Experience Platform.
solution: Data Collection
kt: 7202
source-git-commit: e9a9abeaa722bb2f9a232f4e861b1b5eae86edd1
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 21%

---


# Coleta de dados de encaminhamento de eventos de várias sandboxes

Este blueprint mostra como os dados coletados com SDKs da Web e móveis do Experience Platform podem ser configurados para coletar um único evento e encaminhar para várias sandboxes da AEP. Este blueprint é específico para a coleção de dados de várias sandboxes que usa [!UICONTROL Encaminhamento de evento] para atingir esse objetivo.

Além de replicar o evento com [!UICONTROL Encaminhamento de evento] recursos, você pode adicionar, filtrar ou manipular os dados coletados originais que atendem aos requisitos de outras sandboxes.

[!UICONTROL Encaminhamento de evento] O usa uma propriedade separada que contém a variável [!UICONTROL Elementos de dados], [!UICONTROL Regras], e [!UICONTROL Extensões] necessário para seus requisitos de dados. Com um evento de entrada, o [!UICONTROL Encaminhamento de evento] pode coletar os dados e gerenciar conforme necessário antes do encaminhamento.

Sua sandbox de destino requer um ponto final de transmissão HTTP configurado que é usado pelo Adobe [!UICONTROL Cloud Connector] extensão.

## Casos de uso

* Relatórios de dados globais - ao usar várias sandboxes para isolar ambientes operacionais e a necessidade de consolidar a coleta de dados em uma sandbox para relatórios entre sandboxes. Roteamento de um evento da Experience Edge por meio de [!UICONTROL Encaminhamento de evento] O para uma sandbox de relatórios permite que cada ambiente operacional da sandbox envie dados conforme são coletados em tempo real para uma sandbox de relatórios.

* Gerencie a coleção de dados em sandboxes com base em regras de dados diferentes para cada ambiente operacional de sandbox.

## Aplicativos

* [!DNL Experience Platform] Coleção de dados
* [!UICONTROL Encaminhamento de eventos]
* AEP [!UICONTROL Extensão]
* [!UICONTROL Extensão do Cloud Connector]

## Considerações

Com [!UICONTROL Encaminhamento de evento] como a abordagem para enviar dados para várias sandboxes, há considerações que devem ser levadas em conta na arquitetura da solução.

### Sem dados de HIPAA

[!UICONTROL O Encaminhamento de eventos não é considerado pronto para HIPAA e não deve ser usado para coletar dados de HIPAA. ] No entanto, a infraestrutura utilizada para [!UICONTROL Encaminhamento de evento] O está preparado para a HIPAA e depende exclusivamente do cliente. Embora o seu [!UICONTROL Encaminhamento de evento] A propriedade Tag reside no estado [!UICONTROL Encaminhamento de evento] sistema, toda a carga de dados coletada é enviada para o [!UICONTROL Encaminhamento de evento] sistema de processamento. É esse processo que torna [!UICONTROL Encaminhamento de evento] referente aos casos de uso da HIPAA. Com toda a carga útil enviada para o [!UICONTROL Encaminhamento de evento] sistema, isso incluiria quaisquer valores de HIPAA. Embora a [!UICONTROL Encaminhamento de evento] As regras filtrarão esses dados antes de enviá-los ao destino; esses dados da HIPAA ainda serão enviados para uma infraestrutura que não esteja pronta para a HIPAA. No entanto, os dados de conteúdo nunca são armazenados, apenas transferidos.

### Diferentes fluxos de dados e pontos finais de transmissão

À medida que os dados fluem pelos fluxos de dados da [!UICONTROL Rede de borda da plataforma], ao usar [!UICONTROL Encaminhamento de evento] Para outra sandbox da AEP, um requisito é nunca usar o mesmo fluxo de dados ou ponto de extremidade de transmissão que a sequência de dados que faz a coleção original. Isso pode ser prejudicial para a instância da AEP e possivelmente acionar uma situação de DoS.

### Volumes de tráfego estimados

Os volumes de tráfego são necessários para análise, conforme cada caso de uso. Isso é importante, pois grandes volumes podem resultar em uma situação de limitação, e os clientes serão notificados se isso ocorrer.

## Arquitetura

![Várias sandboxes [!UICONTROL Encaminhamento de evento]](assets/multi-sandbox-data-collection.png)

1. Coleta e envio de dados do evento para o [!UICONTROL Rede de borda da plataforma] é necessário para usar o [!UICONTROL Encaminhamento de evento]. Os clientes podem usar as tags Adobe para o lado do cliente ou [!UICONTROL API do servidor de rede de borda da plataforma] para coleta de dados de servidor para servidor. A variável [!UICONTROL API de rede de borda de plataforma] O pode fornecer um recurso de coleção de servidor para servidor. No entanto, isso requer um modelo de programação diferente para ser implementado. Consulte [Visão geral da API de servidor da Edge Network](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=pt-BR).

1. As cargas coletadas são enviadas da implementação de tags para o [!UICONTROL Rede de borda da plataforma] para o [!UICONTROL Encaminhamento de evento] e processado pelo seu próprio [!UICONTROL Elementos de dados], [!UICONTROL Regras] e [!UICONTROL Ações]. Saiba mais sobre as diferenças entre [[!UICONTROL Tags e Encaminhamento de eventos]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=pt-BR#differences-from-tags).

1. Um [!UICONTROL Encaminhamento de evento] propriedade também é necessária para receber dados de Evento coletados do [!UICONTROL Rede de borda da plataforma]. Se esses dados do evento foram enviados para a Rede de borda da Platform por uma implementação de tags implantadas ou uma coleção de servidor para servidor. Os autores definem os elementos de dados, as regras e as ações usadas para enriquecer os dados de eventos antes do encaminhamento para a segunda sandbox. Considere usar o código personalizado [!DNL JavaScript] elemento de dados para ajudar na estruturação dos dados para assimilação da sandbox. Combinado aos recursos de preparação de dados da Platform, você tem várias opções para gerenciar a estrutura de dados.

1. Atualmente, a utilização do Adobe [!UICONTROL Extensão do Cloud Connector] é obrigatório dentro de [!UICONTROL Encaminhamento de evento] Propriedade. Depois que as regras processam ou enriquecem os dados do evento, o Cloud Connector é usado em uma chamada de busca configurada para um POST enviando a carga para a segunda sandbox

1. Um ponto final de transmissão para assimilação de dados é necessário para a segunda sandbox. Você também pode considerar os recursos de Preparo de dados na AEP para ajudar na assimilação e no mapeamento de [!UICONTROL Encaminhamento de evento] cargas para o XDM. Consulte a documentação da AEP: criar uma [Conexão de transmissão da API HTTP usando a interface do usuário](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/streaming/http.html?lang=pt-BR)
