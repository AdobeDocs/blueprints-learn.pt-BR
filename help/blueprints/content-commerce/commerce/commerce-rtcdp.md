---
title: Adobe Commerce - Blueprint da RTCDP
description: Integração do Adobe Experience Platform com o Adobe Commerce para criar uma única visualização de clientes e personalizar experiências de forma inteligente em uma vitrine digital e em vários canais.
solution: Real-Time Customer Data Platform, Commerce
exl-id: e2fc5e1c-c865-4c24-9b82-861a34aba487
source-git-commit: 387ad59319f72adeff338880c7f168d3aeca86f8
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# ADOBE COMMERCE e RTCDP

A variável [!DNL Data Connection] A extensão ajuda os clientes do Adobe Commerce a se integrarem perfeitamente ao Adobe Experience Platform para enriquecer o perfil do cliente e personalizar experiências em vitrines digitais e outros canais.

## Recursos técnicos habilitados

* Os dados da vitrine (do lado do cliente, como adicionar ao carrinho, abandonos de carrinho e assim por diante) coletados e enviados para qualquer produto da Adobe Experience Cloud.
* Status de pedido de back office para qualquer produto da Adobe Experience Cloud
* Os pedidos de histórico do back office podem ser enviados para a Adobe Experience Platform
* Compartilhar e personalizar públicos-alvo da RTCDP para a Adobe Commerce

## Pré-requisitos

Para usar o [!DNL Data Connection] extensão, você deve ter o seguinte:

* Adobe Commerce 2.4.4 ou mais recente
* Adobe ID e ID da organização
* Adobe Experience Platform/RTCDP
* [Camada de dados de clientes Adobe (ACDL)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html). A ACDL é necessária para coletar dados do evento da loja.

## Etapas de integração

### Coleta de dados do Adobe Commerce para o Adobe Experience Platform

* [Instalar](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/install.html) o [!DNL Data Connection] extensão.
* [Fazer logon](https://helpx.adobe.com/manage-account/using/access-adobe-id-account.html) para sua conta Adobe e visualize para confirmar a ID da organização. A ID da organização é a ID associada à empresa de Experience Cloud provisionada. A ID é uma sequência de 24 caracteres alfanuméricos seguidos por (e deve incluir) @AdobeOrg.
* [Criar ou atualizar](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html) seu esquema XDM com grupos de campos específicos do Commerce.
* [Criar um conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset) com base no esquema criado ou atualizado. Esse conjunto de dados conterá os dados do Commerce enviados.
* [Criar um fluxo de dados](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/overview.html) e selecione o esquema XDM que contém os grupos de campos específicos do Commerce.
* [Conectar-se a Commerce Services](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html).
* [Conectar-se ao Adobe Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/connect-data.html).

### Conectar-se ao destino de comércio do Adobe Experience Platform para compartilhamento de público-alvo

Para se conectar ao destino do Adobe Commerce:

* No [Interface do Adobe Experience Platform](https://experience.adobe.com/platform/), acesse Destinos > Catálogo.
* Selecione Personalization.
* Selecione o destino do Adobe Commerce para realçá-lo e, em seguida, selecione Configurar.
* Siga as etapas descritas na seção [tutorial de configuração de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html).

## Dados prontos para uso

* Eventos da loja (navegador/aplicativo)
* Eventos de back office
* Dados históricos do pedido

Para obter uma lista completa de eventos compatíveis, consulte [Eventos de comércio](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/event-forwarding/events.html)

## Arquitetura

<img src="../commerce/assets/commerce_rtcdp.png" alt="Arquitetura Adobe Commerce RTCDP" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## Guias de implementação relacionados

| Guia  | Link |
|:----|:----|
| Conector da plataforma | [Visão geral do conector Experience Platform do Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/overview.html) |
| Destino do Commerce | [Conexão Adobe Commerce no RTCDP](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-commerce.html) |
| Personalização de borda | [Ativar públicos para destinos de personalização de borda](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations.html) | |
