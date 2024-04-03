---
title: Coleção de dados do Encaminhamento de eventos de várias sandboxes
description: Saiba como os dados coletados com os SDKs móveis e da Web da Experience Platform podem ser configurados para coletar um único evento e encaminhar para várias sandboxes da Experience Platform.
solution: Data Collection
kt: 7202
exl-id: ecc94fc8-9fad-4b88-a153-3d0fc00d8d58
source-git-commit: 72eb4e2ff276279a2fc88ead0b17d77cc8e99b97
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 55%

---

# Coleção de dados do Encaminhamento de eventos de várias sandboxes

Este blueprint mostra como os dados coletados com o [!DNL Experience Platform] Os SDKs da Web e móveis podem ser configurados para coletar um único evento e encaminhar para várias sandboxes da AEP. Este blueprint é específico para a coleção de dados de várias sandboxes que usa o [!UICONTROL Encaminhamento de eventos] para atingir esse objetivo.

Além de replicar o evento utilizando os recursos de [!UICONTROL Encaminhamento de eventos], você pode adicionar, filtrar ou manipular os dados coletados originais que atendam aos requisitos de outras sandboxes.

O [!UICONTROL Encaminhamento de eventos] usa uma propriedade independente que contém [!UICONTROL Elementos de dados], [!UICONTROL Regras] e [!UICONTROL Extensões] necessários para os seus requisitos de dados. Com um evento de entrada, a sua propriedade de [!UICONTROL Encaminhamento de eventos] pode coletar e gerenciar os dados, conforme necessário, antes do encaminhamento.

Sua sandbox de destino exige a configuração de um ponto de extremidade de transmissão HTTP, que é usado pela extensão do Adobe [!UICONTROL Cloud Connector].

## Casos de uso

* Relatórios de dados globais – em caso de utilização de várias sandboxes para isolar ambientes operacionais e da necessidade de consolidar a coleção de dados em uma sandbox para relatórios entre sandboxes. O roteamento de um evento da Experience Edge por meio do [!UICONTROL Encaminhamento de eventos] para uma sandbox de relatórios permite que cada ambiente operacional de sandbox envie dados em tempo real para uma sandbox de relatórios conforme eles são coletados.

* Gerencie a coleção de dados em sandboxes com base em regras de dados diferentes para cada ambiente operacional de sandbox.

## Aplicativos

* [!DNL Experience Platform] Coleção de dados
* [!UICONTROL Encaminhamento de eventos]
* [!UICONTROL Extensão] da AEP
* [!UICONTROL Extensão do Cloud Connector]

## Considerações

Ao usar a abordagem de [!UICONTROL Encaminhamento de eventos] para enviar dados para várias sandboxes, há considerações que devem ser levadas em conta quanto à arquitetura da solução.

### Sem dados de HIPAA

[!UICONTROL Encaminhamento de evento] O não é considerado HIPAA Ready e não deve ser usado em nenhum caso de uso de HIPAA em que os dados de HIPAA sejam coletados.

No entanto, a infraestrutura utilizada para [!UICONTROL Encaminhamento de evento] O está preparado para a HIPAA e fica a critério exclusivo do cliente. Enquanto a propriedade de Tag do [!UICONTROL Encaminhamento de eventos] estiver no sistema de [!UICONTROL Encaminhamento de eventos], todo o conteúdo de dados coletado será enviado para [!UICONTROL esse sistema] para processamento. Esse processo torna [!UICONTROL Encaminhamento de evento] referente aos casos de uso da HIPAA. Com toda a carga útil enviada para o [!UICONTROL Encaminhamento de evento] esse processo incluiria quaisquer valores de HIPAA. Embora a [!UICONTROL Encaminhamento de evento] As regras filtram esses dados antes de enviá-los ao destino; esses dados da HIPAA ainda são enviados para uma infraestrutura que não esteja pronta para a HIPAA. No entanto, os dados de payload nunca são armazenados e são simplesmente uma passagem.

### Diferentes sequências de dados e pontos de extremidade de transmissão

À medida que os dados fluem pelos fluxos de dados da [!DNL Platform Edge Network], ao usar [!UICONTROL Encaminhamento de evento] Para outra sandbox da AEP, um requisito é nunca usar o mesmo fluxo de dados ou ponto de extremidade de transmissão que a sequência de dados que faz a coleção original. Isso pode ser prejudicial para a instância da AEP e possivelmente acionar uma situação de DoS.

### Volumes de tráfego estimados

Os volumes de tráfego são necessários para análise, conforme cada caso de uso. Isso é importante porque grandes volumes podem resultar em uma situação de limitação, e os clientes serão notificados se isso ocorrer.

## Arquitetura

![Encaminhamento de eventos [!UICONTROL de várias sandboxes]](assets/multi-sandbox-data-collection.png)

1. Coleta e envio de dados do evento para o [!DNL Platform Edge Network] é necessário usar [!UICONTROL Encaminhamento de evento]. Você pode usar tags Adobe para o lado do cliente ou para o [!DNL Platform Edge Network Server API] para coleta de dados de servidor para servidor.

   A variável [!DNL Platform Edge Network API] O pode fornecer um recurso de coleção de servidor para servidor. Isso, no entanto, requer um modelo de programação diferente para ser implementado. Consulte [Visão geral da API de servidor da Edge Network](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=pt-BR).

1. As cargas coletadas são enviadas da implementação de tags para o [!DNL Platform Edge Network] para o [!UICONTROL Encaminhamento de evento] e processado pelo seu próprio [!UICONTROL Elementos de dados], [!UICONTROL Regras], e [!UICONTROL Ações]. Para ler mais sobre as diferenças, consulte [Tags e [!UICONTROL Encaminhamento de evento]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=pt-BR#differences-from-tags).

1. Um [!UICONTROL Encaminhamento de evento] propriedade também é necessária para receber dados de eventos coletados do [!DNL Platform Edge Network], se esses dados do evento foram enviados para o [!DNL Platform Edge Network] por uma implementação de Tags implantadas ou uma coleção de servidor para servidor.

   Os autores definem os elementos de dados, as regras e as ações usadas para enriquecer os dados do evento antes do encaminhamento para a segunda sandbox. Considere usar o elemento de dados [!DNL JavaScript] de código personalizado para ajudar a estruturar os dados para assimilação da sandbox. Combinado com os recursos de preparação de dados da Platform, você tem várias opções para gerenciar a estrutura de dados.

1. Atualmente, é necessário usar a [!UICONTROL extensão do Adobe Cloud Connector] na propriedade de [!UICONTROL Encaminhamento de eventos]. Depois que as regras processam ou enriquecem os dados do evento, a variável [!UICONTROL Cloud Connector] é usado em uma chamada de busca configurada para um POST, enviando o conteúdo para a segunda sandbox.

1. Um terminal de transmissão para assimilação de dados é necessário para a segunda sandbox. Você também pode considerar [!UICONTROL Preparação de dados] recursos na AEP para ajudar na assimilação e no mapeamento de [!UICONTROL Encaminhamento de evento] cargas para o XDM. Consulte a documentação da AEP: criar uma [Conexão de transmissão da API HTTP usando a interface do usuário](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/streaming/http.html?lang=pt-BR)
