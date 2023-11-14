---
title: Adobe Commerce - Blueprint da RTCDP
description: Integração do Adobe Experience Platform com o Adobe Commerce para criar uma única visualização de clientes e personalizar experiências de forma inteligente em uma vitrine digital e em vários canais.
solution: Real-Time Customer Data Platform, Commerce
source-git-commit: abb946358ceeee1af427c5b362ed2f48f733a6c9
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# ADOBE COMMERCE e RTCDP

Essa experiência integrada ajuda os clientes da Adobe Commerce a se integrarem perfeitamente ao Adobe Experience Platform para enriquecer o perfil do cliente e personalizar experiências em vitrines digitais e outros canais.

## Recursos técnicos habilitados

* Dados da vitrine (lado do cliente) coletados e enviados para qualquer produto da Adobe Experience Cloud. (adicionar ao carrinho, abandonos de carrinho etc.)
* Status de pedido de back office para qualquer produto da Adobe Experience Cloud
* Os pedidos de histórico do back office podem ser enviados para a Adobe Experience Platform
* Compartilhar e personalizar públicos-alvo da RTCDP para a Adobe Commerce

## Pré-requisitos

Para usar o conector Experience Platform, você deve ter o seguinte:

* Adobe Commerce 2.4.4 ou mais recente
* Adobe ID e ID da organização
* Adobe Experience Platform/RTCDP
* [Camada de dados de clientes Adobe (ACDL)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html?lang=en). A ACDL é necessária para coletar dados do evento da loja.

## Etapas de integração

### Coleta de dados do Adobe Commerce para o Adobe Experience Platform

* [Instalar](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/install.html?lang=en) a extensão do conector Experience Platform.
* [Fazer logon](https://helpx.adobe.com/manage-account/using/access-adobe-id-account.html) para sua conta Adobe e visualize para confirmar a ID da organização. A ID da organização é a ID associada à empresa de Experience Cloud provisionada. A ID é uma sequência de 24 caracteres alfanuméricos seguidos por (e deve incluir) @AdobeOrg.
* [Criar ou atualizar](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html?lang=en) seu esquema XDM com grupos de campos específicos do Commerce.
* [Criar um conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=en#create-a-dataset) com base no esquema criado ou atualizado. Esse conjunto de dados conterá os dados do Commerce enviados.
* [Criar um fluxo de dados](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/overview.html?lang=en) e selecione o esquema XDM que contém os grupos de campos específicos do Commerce.
* [Conectar-se a Commerce Services](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html?lang=en).
* [Conectar-se ao Adobe Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/connect-data.html?lang=en).

### Conectar-se ao destino de comércio do Adobe Experience Platform para compartilhamento de público-alvo

Para se conectar ao destino do Adobe Commerce:

* No [Interface do Adobe Experience Platform](https://experience.adobe.com/platform/), acesse Destinos > Catálogo.
* Selecione Personalization.
* Selecione o destino do Adobe Commerce para realçá-lo e, em seguida, selecione Configurar.
* Siga as etapas descritas na seção [tutorial de configuração de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en).

## Dados prontos para uso

* Eventos da loja (navegador/aplicativo)
* Eventos de back office
* Dados históricos do pedido

Para obter uma lista completa de eventos compatíveis, consulte [Eventos de comércio](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/event-forwarding/events.html?lang=en)

## Arquitetura

<img src="../commerce/assets/commerce_rtcdp.png" alt="Arquitetura Adobe Commerce RTCDP" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## Guias de implementação relacionados

| Guia  | Link |
|:----|:----|
| Conector da plataforma | [Visão geral do conector Experience Platform do Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/overview.html?lang=en) |
| Destino do Commerce | [Conexão Adobe Commerce no RTCDP](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-commerce.html?lang=en) |
| Personalização de borda | [Ativar públicos para destinos de personalização de borda](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations.html?lang=en) | |
