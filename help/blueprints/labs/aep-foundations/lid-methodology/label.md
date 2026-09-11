---
hold: true
title: Rótulo
description: Rotular tabelas de data warehouse relacional como Perfil individual XDM, Evento de experiência ou Classes de pesquisa como parte da metodologia LID.
doc-type: article
solution: Experience Platform
exl-id: 332ead7a-ca6e-4e30-bb35-8419c060c596
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Rótulo

## Palestra

Neste vídeo, você aprenderá a rotular tabelas relacionais como uma tabela Perfil individual XDM (P), Evento de experiência (E) ou Pesquisa (L) usando a Conexão 5G ERD como exemplo.

>[!VIDEO](https://video.tv.adobe.com/v/3459087/?quality=12&learn=on)



## Detalhes do laboratório

Rotule as tabelas do ERD do Data Warehouse 5G Connection e do ERD de Streaming com o rótulo de classe XDM apropriado para as tabelas Perfil individual, Evento de experiência e Pesquisa.

Lembre-se do seguinte ao executar o laboratório:

- **Perfil Individual (características) -** descreve exclusivamente as características de uma pessoa (por exemplo, nome, email, endereço, preferências, etc.)
- **Evento de experiência (comportamentos) -** descreve as interações e os pontos de contato que uma pessoa tem com uma marca/empresa (por exemplo, visita a uma página da Web, compra, interações com a central de atendimento, envio de aplicativo etc.)
- **Pesquisas (suporte) -** fornecem informações contextuais adicionais de suporte ao Perfil Individual ou ao Evento de Experiência



## Etapa 1. Rotular tabelas de perfil individual XDM

1. Identifique todas as tabelas de origem que representam uma pessoa individual no ERD do data warehouse do cliente e no ERD de transmissão contínua do cliente.
1. Marcar cada tabela com um &quot;**P**&quot;, o que significa que ela faz parte da classe Perfil Individual XDM

>[!NOTE]
>
>Marcar somente as tabelas que representam exclusivamente as características de uma pessoa individual



## Etapa 2. Rotular tabelas de Evento de experiência XDM

1. Identifique todas as tabelas de origem que representam o comportamento de uma pessoa individual no ERD do data warehouse 5G da conexão e no ERD de transmissão.
1. Marque cada tabela com um &quot;**E**&quot;, significando que ela faz parte da classe de Evento de Experiência XDM.

>[!NOTE]
>
>Marcar somente as tabelas que representam exclusivamente o comportamento de uma pessoa individual



## Etapa 3. Tabelas de suporte XDM de rótulo

1. Identifique todas as tabelas de origem que representam dados de pesquisa e estão diretamente relacionadas a uma tabela **&quot;P&quot;** ou **&quot;E&quot;** que você marcou no ERD do Data Warehouse 5G de Conexão e no ERD de Streaming.
1. Marque cada tabela com um **&quot;L&quot;**, significando que ela faz parte de uma classe XDM personalizada que não seja de pessoa.

>[!NOTE]
>
>As tabelas de pesquisa só podem ter 1 nível de associação ou &quot;salto&quot; longe de uma tabela rotulada com &quot;P&quot; ou &quot;E&quot;



## Revisão

O vídeo abaixo analisa as etiquetas corretas para o warehouse 5G da Connection e os ERDs de transmissão, explicando por que as tabelas de conta do cliente, pedidos e demonstrativo de faturamento foram rotuladas como estavam.

>[!VIDEO](https://video.tv.adobe.com/v/3459081/?quality=12&learn=on)
