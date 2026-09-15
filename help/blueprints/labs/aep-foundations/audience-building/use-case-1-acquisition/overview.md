---
title: Caso de uso #1 - Acquisition
description: Defina um caso de uso de aquisição que segmente os visitantes da página 14 do iPhone que não compraram ou não são proprietários do dispositivo e planeje a abordagem de criação de público-alvo.
doc-type: overview-page
solution: Experience Platform
exl-id: a85b1eb1-88f4-41b2-acce-2e34dbe6aff8
source-git-commit: 8b3391d41cd4a3ea6cb52d5167e627b7f6bd2c6e
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%
---

# Caso de uso #1 - Aquisição

## Visão geral

Neste vídeo, você aprenderá a criar o público-alvo para o caso de uso de aquisição do iPhone 14.

>[!VIDEO](https://video.tv.adobe.com/v/3459402/?quality=12&learn=on)



**Definição de caso de uso**

Ative todos os perfis que visitaram uma página de produto do iPhone 14 e não há pedidos para um iPhone 14 ou que não têm um iPhone 14 ativo.

>[!IMPORTANT]
>
>Conclua a [configuração do Postman](../../setup.md) antes de iniciar este laboratório. Você também precisa de acesso ao [webhook.site](https://webhook.site/) para capturar os dados do público-alvo ativado.



## Tarefas de análise

Analise os itens acima e anote:

1. Quais campos você acha que são necessários para lidar com esse caso de uso?
1. O método de avaliação precisa ser Streaming?
1. Quais são as ramificações da transmissão quando os eventos que estão sendo usados no Público-alvo chegam em momentos diferentes?
1. Como sabemos o que significa &quot;ativo&quot;?
1. Que outras informações você gostaria de saber?

**Lembre-se**: quando recebemos requisitos das partes interessadas da empresa, eles tendem a ser incompletos, usam outra terminologia e fazem suposições sem sabê-lo. É seu trabalho trazer tanto disso para a superfície e orientá-los para algo que possa ser feito.



## Abordagem

Nesse caso de uso, vamos dividi-lo em vários Públicos-alvo:

1. Não existe nenhum pedido iPhone/Pixel
1. Sem iPhone/Pixel Ativo
1. IPhone/Pixel visitado e sem pedido existe iPhone/Pixel e sem iPhone/Pixel ativo
