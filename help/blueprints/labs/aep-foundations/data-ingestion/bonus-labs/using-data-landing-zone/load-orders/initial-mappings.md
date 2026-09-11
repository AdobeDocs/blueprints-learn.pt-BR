---
hold: true
title: Mapeamentos iniciais
description: Mapeie manualmente os campos _id e carimbo de data e hora necessários para um conjunto de dados de Evento de experiência usando expressões de campo calculado.
doc-type: article
solution: Experience Platform
exl-id: 4052d104-bf0c-4b2d-a298-8075279aeaf8
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---


# Mapeamentos iniciais

Como no exercício anterior, será necessário verificar o mapeamento e, em alguns casos, modificá-lo.

## Verificar recomendações de ML

1. Na etapa Mapeamento, o ML Recommendations mapeia automaticamente a maioria dos atributos. No entanto, você também vê vários erros. A tela inicial pode ser semelhante à exibida abaixo.

![Tela de mapeamento mostrando _id e carimbo de data/hora como campos não mapeados não recomendados pelo ML](assets/initial-mappings-id-timestamp-unmapped-fields.png "_id, carimbo de data/hora são dois campos para os quais o ML Recommender não gerará o mapeamento para ")

>[!NOTE]
>
>Como estamos mapeando um conjunto de dados de Evento de Experiência pela primeira vez, observe que **\_id** e **timestamp** nunca são recomendados ou mapeados por padrão para Eventos de Experiência. É necessário garantir manualmente que eles sejam mapeados corretamente.

## Mapear campos \_id, carimbo de data e hora e ordem.\_devbc.acqSource

1. Para mapear **\_id,** grave a seguinte expressão de campo calculado e clique em visualizar

```none
concat(orderID, "-", lastOrderStatusUpdate)
```

![Campo calculado para _id de mapeamento, pronto para salvar](assets/initial-mappings-calculated-field-for-id-mapping.png "O campo calculado para _id de mapeamento será semelhante a este. Clique em Salvar para salvar o campo calculado")

![Mapeando o campo calculado para o atributo _id](assets/initial-mappings-map-calculated-field-to-id.png "Mapear o campo calculado para _id")

1. Verifique se o campo **carimbo de data/hora** no esquema de destino está mapeado para o seguinte campo calculado:

```none
lastOrderStatusUpdate
```

![Visualização da expressão de campo calculada para o mapeamento de carimbo de data/hora](assets/initial-mappings-expression-preview.png "Grave a seguinte expressão e clique em Visualizar. OBSERVE que esse valor diferencia maiúsculas de minúsculas e deve ser escrito exatamente dessa forma")

![Mapeando a expressão de campo calculado &quot;inStore&quot; para order._devbc.acqSource](assets/initial-mappings-map-instore-expression-to-acqsource.png)

1. Mapear a expressão de campo calculado **&quot;inStore&quot;** para **order.\_devbc.acqSource**

![Gravando a expressão de campo calculado &quot;inStore&quot; e clicando em Preview](assets/initial-mappings-write-instore-expression-preview.png "Gravar a seguinte expressão e clicar em Preview. OBSERVE que esse valor diferencia maiúsculas de minúsculas e deve ser escrito exatamente dessa forma")

## Manuseio de mapeamentos duplicados

Se a tela de mapeamento reclamar agora, há um mapeamento duplicado, como **orderStatus** mapeado para **order.\_devbc.acqSource,** clique no ícone &quot;-&quot; para remover o mapeamento.

> [!NOTE]
>
>Lembre-se de que vários campos de entrada não podem ser mapeados para o mesmo campo de saída, pois isso torna o mapeamento ambíguo. Mas um único campo de entrada pode ser mapeado para vários campos de saída no esquema XDM.

![Aviso de mapeamento duplicado para orderStatus mapeado para order._devbc.acqSource](assets/initial-mappings-duplicate-mapping-warning.png "Mapeamento duplicado para orderStatus mapeado para order._devbc.acqSource")



![Aviso de mapeamento duplicado para order._devbc.acqSource após a criação do campo calculado](assets/initial-mappings-duplicate-mapping-for-acqsource.png "Duplique o mapeamento para order._devbc.acqSource, pois criamos um campo calculado e já mapeamos para ele. ")
