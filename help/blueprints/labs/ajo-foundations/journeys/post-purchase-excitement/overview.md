---
title: Emoção pós-compra
description: Saiba como criar uma jornada pós-compra orientada por evento que aciona um email de notificação de envio com detalhes de rastreamento dinâmico de uma API de terceiros.
doc-type: overview-page
solution: Experience Platform
exl-id: 570dc378-e7a3-4895-8f14-89d420b6b340
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%
---

# Emoção pós-compra

## Pré-requisitos

>[!WARNING]
>
>Os laboratórios abaixo devem ter sido concluídos antes do início deste laboratório

- **Instalação do Postman** **—>** [Instalação do Postman](../../postman-setup/postman-installation.md)
- **Repositórios de Dados — Repositório Relacional em Ação** **—>** [Dimension de Destino de Perfil](../../data-stores/relational-store-in-action/profile-target-dimension.md)
- **Repositórios de Dados — Configurar Canais de Email —>** [Configurar para Perfil](../../data-stores/configure-email-channels/configure-for-profile.md)
  *(esta etapa leva até 3 horas para ser concluída)*

Se ainda não tiver feito isso, conclua agora

>[!CAUTION]
>
>Este laboratório requer um subdomínio delegado à Adobe em sua sandbox. Consulte [Configuração](../../setup.md) se você estiver no seu ritmo e ainda não tiver uma.

## Visão geral do laboratório

Neste vídeo, você aprenderá como o caso de uso de excitação pós-compra mapeia uma Jornada, abordando as perguntas de pensamento crítico e a arquitetura para enviar uma notificação de envio personalizada assim que um pedido for enviado.

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

- A confirmação inicial do pedido normalmente seria implementada como uma mensagem transacional, pois os clientes não querem esperar por uma confirmação depois de fazerem um pedido.
- A notificação de envio de pedido também pode ser implementada usando mensagens transacionais, mas pode ser incorporada em uma jornada, permitindo uma ação personalizada para recuperar as informações de envio e aprimorar a comunicação com o cliente.

>[!NOTE]
>
>Neste laboratório, você só desenvolve a mensagem Pedido enviado e ignora a mensagem de Confirmação do pedido.
