---
title: Caso de uso
description: Defina um caso de uso de venda adicional direcionado a clientes com alto uso de dados sem um plano telefônico definitivo, comparando as abordagens de agregação de público-alvo para ativação.
doc-type: overview-page
solution: Experience Platform
exl-id: d0268de8-87eb-4dd9-b699-99d42716f20c
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Caso de uso #2 - Venda adicional

## Visão geral

Neste vídeo, você aprenderá a abordar o caso de uso de venda adicional, que tem como alvo clientes com alto uso de dados para ativação por meio de canais de correspondência paga e direta.

>[!VIDEO](https://video.tv.adobe.com/v/3459487/?quality=12&learn=on)



**Definição de caso de uso**

Encontre todos os clientes que têm um uso total de dados de cobrança nos últimos 6 meses >140 GB, uma média contínua de 6 meses. uso mensal de dados de >=20 GB e que não têm um plano telefônico definitivo.

Ative nos canais Facebook / Google e Mala direta.

Campos de personalização de correspondência direta:

- Nome → usado para saudação
- Endereço de correio → usado para correio
- Nome do plano → usado para declaração de mala direta (por exemplo, &quot;Eric, atualize para um plano final hoje!&quot;)



## Tarefas de análise

Analise os itens acima e anote:

1. Quais campos você acha que são necessários para lidar com esse caso de uso?
1. O método de avaliação precisa ser Streaming?
1. O que precisamos ter em mente com os dados de faturamento?
1. Que outras informações você gostaria de saber?

Lembre-se: quando recebemos requisitos dos participantes do negócio, eles tendem a estar incompletos, usam outra terminologia e fazem suposições sem saber. É seu trabalho trazer tanto disso para a superfície e orientá-los para algo que possa ser feito.



## Abordagem

Nesse caso de uso, vamos avaliar duas opções:

- Opção #1 (Use o Audience para agregar)
  - O público-alvo fará a agregação
    - Uso de dados de faturamento Soma >140 GB (últimos 6 meses)
    - Uso de dados de faturamento Médio >20 GB (últimos 6 meses)
    - O Uso De Dados De Faturamento É Alto, Mas Não Há Plano Da Ultimate
- Opção #2 (Usar pré-agregações)
  - Isso utilizará a agregação que foi feita antes de colocar os dados no Perfil
    - Uso De Dados De Faturamento Alto, Mas Sem Plano Da Ultimate (Agg)
