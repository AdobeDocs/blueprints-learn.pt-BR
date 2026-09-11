---
hold: true
title: Validar evento assimilado
description: Confirme se um evento Pedido enviado foi assimilado em um perfil e o qualifica para os públicos esperados.
doc-type: article
solution: Experience Platform
exl-id: c04397dd-8b5c-48a8-82b5-78188b8374f1
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---


# Validar evento assimilado

## Objetivo de aprendizado

Confirme se o evento foi assimilado com êxito no Adobe Experience Platform.

## Validar evento no perfil

1. Vá para seus **Perfis** e procure seu Perfil para ver se o evento foi assimilado no Perfil.  Aparece em segundos.
   - **Namespace de identidade** -> `email`
   - **Valor de identidade** -> `henry.creel@emailsim.io`
2. Clique na guia **Eventos**. Procure o evento `orders.shipped`.

![pedidos.evento enviado mostrado na guia Eventos do perfil](assets/validate-event-ingested-orders-shipped-event.png)

>[!WARNING]
>
>Você recebeu **message.feedback** eventos.  Eles são de Jornadas e geralmente indicam uma falha ou exclusão.  Clique nelas e veja o `reason`.
>
>Alguns exemplos que você pode encontrar na produção podem ser:
>
>- EmailNoAddressFoundInProfile (você tentou enviar um email para um perfil que não tinha um email)
>- EmailNoConsent (você tentou enviar um email para um perfil que tinha o consentimento definido como não.



&#x200B;3. Validar se o Perfil se qualificou para os **Públicos-alvo** (pode levar alguns minutos).
   - Qualquer Edge de evento (em 15 minutos)
   - Qualquer transmissão de evento (em 15 minutos)

![Perfil qualificado para Qualquer Edge de Evento e Qualquer Público de Streaming de Eventos](assets/validate-event-ingested-profile-qualified-audiences.png)



## Tente com seu próprio email

Agora que você validou que o Perfil foi recebido, envie alguns eventos de pedido enviado usando seu próprio email.

1. Volte para a Postman e encontre o **Evento de envio de pedido**
2. clique no **Corpo** e altere o **endereço de email** para o seu.

![Endereço de email alterado no corpo da solicitação do Postman](assets/validate-event-ingested-change-email-in-postman-body.png)

&#x200B;3. **Salvar** e pressionar **Enviar**.
&#x200B;4. Retorne às etapas 1 a 3 e valide usando seu endereço de email.

## Recapitulação

O evento é exibido na loja de Perfis e o Perfil agora faz parte dos Públicos-alvo que estavam procurando pelo evento.
