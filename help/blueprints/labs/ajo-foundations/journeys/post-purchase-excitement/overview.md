---
title: Emoção pós-compra
description: Saiba como criar uma jornada pós-compra orientada por evento que aciona um email de notificação de envio com detalhes de rastreamento dinâmico de uma API de terceiros.
doc-type: overview-page
solution: Experience Platform
exl-id: 570dc378-e7a3-4895-8f14-89d420b6b340
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# Emoção pós-compra

## Pré-requisitos

>[!WARNING]
>
>Os laboratórios abaixo devem ter sido concluídos antes do início deste laboratório

Estes laboratórios devem ter sido concluídos antes de iniciar este laboratório:

- **Repositórios de Dados — Repositório Relacional em Ação** **—>** [Dimension de Destino de Perfil](../../data-stores/relational-store-in-action/profile-target-dimension.md)
- **Repositórios de Dados — Configurar Canais de Email —>** [Configurar para Perfil](../../data-stores/configure-email-channels/configure-for-profile.md)
  *(isso pode levar até 3 horas para ser concluído)*

Se ainda não tiver feito, conclua agora

## Visão geral do laboratório

Neste vídeo, você aprenderá como o caso de uso de excitação pós-compra mapeia uma jornada, abordando as perguntas de pensamento crítico e a arquitetura para enviar uma notificação de envio personalizada assim que um pedido for enviado.

>[!VIDEO](https://video.tv.adobe.com/v/3491146/)

## Objetivos de aprendizagem

- Criar uma Jornada que comece com um evento unitário
- Definir e configurar uma ação personalizada para chamar um sistema de terceiros para retornar informações usadas em uma Jornada
- Executar uma jornada por transmissão em uma carga do evento
- Testar e depurar perfis e Jornadas
- Validar a experiência desejada por meio de relatórios e logs
- Configure a personalização em um email simples e veja-o em ação



## Descrição do caso de uso

Quando um cliente faz um pedido, você deseja enviar uma mensagem de confirmação com os detalhes do pedido.  Depois que o pedido for enviado, você desejará acionar uma segunda mensagem com informações de rastreamento recuperadas dinamicamente de uma API de terceiros.

**Principais chamadas:**

- O pedido inicial feito normalmente seria implementado como uma mensagem transacional, já que as pessoas não querem esperar por uma confirmação de que apenas solicitam algo.
- A notificação de envio de pedido também pode ser implementada usando mensagens transacionais, mas pode ser incorporada em uma jornada, permitindo uma ação personalizada para recuperar as informações de envio e aprimorar a comunicação com o cliente.

>[!NOTE]
>
>Neste laboratório, você só desenvolverá a mensagem Pedido enviado e ignorará a mensagem de Confirmação do pedido.
