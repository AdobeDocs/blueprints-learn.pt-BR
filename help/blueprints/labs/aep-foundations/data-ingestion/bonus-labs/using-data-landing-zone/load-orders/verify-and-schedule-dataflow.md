---
hold: true
title: Verificar e agendar fluxo de dados
description: Verifique o conjunto completo de mapeamento Pedidos, visualize a saída e programe o fluxo de dados para ser executado a cada 15 minutos.
doc-type: article
solution: Experience Platform
exl-id: b7f0c43b-092c-45ba-b95b-27cb4a49d110
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 7%

---


# Verificar e agendar fluxo de dados

## Verificar novamente o conjunto de mapeamento

| # | Coluna Source | Coluna XDM |
| -- | ------------------------------------------- | -------------------------------------------------------- |
| 1 | orderStatus | eventType |
| 2 | lastOrderStatusUpdate | carimbo de data e hora |
| 3 | orderID | order.orderID |
| 4 | orderDate | order.orderDate |
| 5 | orderTotal | order.priceTotal |
| 6 | paymentType | order.payment.paymentType |
| 7 | paymentAmount | order.payment.paymentAmount |
| 8 | paymentCurrencyCode | order.payment.currencyCode |
| 9 | paymentTransactionID | order.payment.transactionID |
| 10 | ID.plano | order.\_devbc.plan.planID |
| 11 | customerID | \_devbc.customerID |
| 12 | personalEmail | \_devbc.personalEmail |
| 13 | storeID | store.storeID |
| 14 | shippingStreetAddress | shipping.address.street1 |
| 15 | shipCity | shipping.address.city |
| 16 | shipState | shipping.address.state |
| 17 | shippingZip | shipping.address.postalCode |
| 18 | shippingMethod | shipping.shippingMethod |
| 19 | shippingAmount | shipping.shippingAmount |
| 20 | shippingDestination | shipping.shippingDestination |
| 21 | billingStreetAddress | billing.address.street1 |
| 22 | billingCity | billing.address.city |
| 23 | billingState | billing.address.state |
| 24 | billingZip | billing.address.postalCode |
| 25 | products\[\*] | productListItems\[\*] |
| 26 | products\[\*].productID | - productListItems\[\*].\_id - productListItems\[\*].SKU |
| 27 | products\[\*].make | productListItems\[\*].\_devbc.make |
| 28 | products\[\*].model | productListItems\[\*].\_devbc.model |
| 29 | products\[\*].price | productListItems\[\*].priceTotal |
| 30 | concat(orderID, &quot;-&quot;, lastOrderStatusUpdate) | \_id |
| 31 | &quot;inStore&quot; | order.\_devbc.acqSource |



## Visualizar a saída do mapeamento

1. Visualize a saída do mapeamento. Role por todos os atributos para garantir que não haja exclamação vermelha ao lado de nenhum dos atributos no lado direito.

![Visualizar a tela de mapeamento sem erros em nenhum atributo mapeado](assets/verify-and-schedule-dataflow-preview-mapping-screen.png "Visualizar a tela de mapeamento será assim")

1. No lado esquerdo da navegação de Visualização, selecione a matriz de objetos **productListItems**. O lado direito é atualizado para mostrar apenas os atributos nessa matriz de objetos.

>[!NOTE]
>
>Observe que **productListItems.currencyCode** e **productListItems.quantity** são preenchidos automaticamente (mesmo após a remoção dos mapeamentos). Isso acontece porque **productListItems** como um objeto pai são mapeados.

![Tela de mapeamento concluída para productListItems após remover substituições duplicadas](assets/verify-and-schedule-dataflow-completed-mapping-screenshot.png "O mapeamento concluído será semelhante à seguinte captura de tela")

## Agendar a execução

1. Defina o agendamento para executar **a cada 15 minutos** definindo Frequency como Minuto e Intervalo como 15. Revise o fluxo e clique em Concluir.

>[!CAUTION]
>
>Verifique se a programação está definida como 15 minutos. Se você agendar a execução como **Executar Uma Vez**, não poderá executá-la novamente, mesmo que faça alterações no mapeamento posteriormente.

1. A execução do fluxo de dados não é iniciada imediatamente e leva alguns minutos. Assim, o último Status de Execução do Fluxo de Dados está definido como &quot;*Nenhuma execução*&quot;.

1. Após alguns minutos, o fluxo de dados é bem-sucedido. Observe o **Status da Última Execução do Fluxo de Dados** e a **Data da Última Execução do Fluxo de Dados**.

1. Clique no nome do Fluxo de Dados para obter uma lista de Execuções de Fluxo de Dados. 10 Os registros devem ser assimilados.

1. Clique na hora de início da execução do fluxo de dados para ver os detalhes do diagnóstico de erro.

1. Na barra de navegação à esquerda, vá para Conjuntos de dados na Platform e clique em **Pedidos - SeuNomeAqui**

1. Clique no **Visualizar Conjunto de Dados.**
