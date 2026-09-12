---
title: Transmitir um evento de pedido
description: Pratique a criação de um fluxo de dados de transmissão da API HTTP para enviar um evento de pedido de amostra e vinculá-lo a um perfil de cliente existente.
doc-type: article
solution: Experience Platform
exl-id: 558c21d1-f9b7-489b-9153-5f10d0b8448a
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Transmitir um evento de pedido

## Pré-requisitos

1. Você baixou os [Arquivos de Exemplo](../sample-files.md) e viu o arquivo chamado —> **Lab\_Single\_Order\_sample.json**
1. Você concluiu com êxito o laboratório [Using Data Landing Zone](./using-data-landing-zone/overview.md) e tem um mapeamento válido definido para importar

## Desafio

Execute o seguinte conjunto de tarefas da mesma forma que fazia no laboratório anterior.

1. Criar uma nova conta usando o conector de origem da API HTTP
1. Configurar um fluxo de dados usando a nova conta para transmitir dados para seu próprio conjunto de dados de Pedidos do cliente
1. Reutilize o conjunto de mapeamento do laboratório [Using Data Landing Zone](./using-data-landing-zone/overview.md)
1. Na Postman, preencha o **Criar evento de pedido** com as informações necessárias para transmitir os dados com êxito e anexá-los ao registro de Conta de cliente criado anteriormente
1. Verifique se o pedido está vinculado ao seu perfil

>[!TIP]
>
>Boa sorte e que os deuses da Adobe Experience Platform estejam com você!
