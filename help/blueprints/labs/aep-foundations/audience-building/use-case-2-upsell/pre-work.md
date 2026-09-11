---
hold: true
title: Trabalho prévio
description: Investigue campos de esquema para uso de faturamento e nome do plano, destacando como as descrições ausentes e os campos duplicados podem confundir os construtores de público-alvo.
doc-type: article
solution: Experience Platform
exl-id: c26de19e-82da-4070-a918-2d2c8ef2c116
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# Trabalho prévio

Neste caso de uso, não há muito trabalho prévio a ser feito. Basicamente, temos duas coisas que estamos procurando: 1) Uso, 2) Plano.  Descubra onde eles estão.

## Uso de dados de cobrança

1. Criar um novo público-alvo
1. Procure por &quot;uso&quot; em Atributos. Clique no &quot;i&quot; para analisar a descrição (não há nenhuma).

![Pesquisar por uso em Atributos - nenhuma descrição mostrada](assets/pre-work-search-usage-in-attributes.png)



&#x200B;3. Procure por &quot;uso&quot; em Eventos.  Clique no &quot;i&quot; para analisar a descrição (não há nenhuma).

![Procurar uso em Eventos - nenhuma descrição mostrada](assets/pre-work-search-usage-in-events.png)

&#x200B;> [!NOTE]
>
>Nenhum deles tem descrição, portanto, o profissional de marketing pode fazer algumas suposições e adivinhar errado.
>
>As descrições são importantes.  Sem descrições, como o profissional de marketing saberá:
>
>- Qual usar?
>- Latência dos dados?
>- Recomendado/preferencial em casos de uso específicos?
>
>Ao fornecer essas informações em descrições, podemos orientá-las melhor.
> [!NOTE]
>
>Tente pesquisar por &quot;Faturamento&quot;.  Observe que ele não é exibido como um Atributo de perfil.  Ele é exibido como um Cartão de tipo de evento, juntamente com o campo &quot;Uso de dados de faturamento&quot;.
>
>Existem convenções de nomenclatura para seu profissional de marketing também.  Dependendo do que pesquisam ou se estão procurando/esperando que seja um Evento ou um Perfil, isso afeta o que encontram e eventualmente usam.

## Plano

Procure por &quot;Plano&quot; em Atributos.  Observe que temos várias opções disponíveis.  Restrinja-o ao &quot;Nome do plano&quot;.  Nós temos dois nomes de planos?!



![Atributo Nome do Primeiro Plano encontrado ao pesquisar o Plano](assets/pre-work-duplicate-plan-name-field.png)



![Atributo Second Plan Name encontrado ao pesquisar o Plano](assets/pre-work-duplicate-plan-name-field--2.png)

O Nome do Plano (Nome do Plano) parece ser o que precisamos com base na descrição e o outro não tem uma descrição.
