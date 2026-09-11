---
hold: true
title: Fórmulas de classificação
description: Saiba como as fórmulas de classificação ajustam dinamicamente a pontuação de prioridade de um item de decisão por perfil usando expressões matemáticas condicionais.
doc-type: article
solution: Experience Platform
exl-id: 08183f1a-8db6-43c5-8b2e-05fa3d9c0f8d
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# Fórmulas de classificação

## Objetivo de aprendizado

Ao final desta lição, você será capaz de:

- Definir uma fórmula de classificação e explicar o que ela ajusta
- Explicar a estrutura if/then de uma regra de fórmula de classificação
- Explicar por que cada configuração de fórmula de classificação requer uma fórmula padrão
- Determine o resultado quando dois itens de decisão chegam à mesma pontuação de prioridade ajustada

## Materiais necessários

- 12 cartas de baralho (Jack, Queen, King de cada naipe)
- 12 notas adesivas, preenchidas com o nome do atributo e valores de lições anteriores

## Palestra

Esta lição tem várias rodadas de reordenação manual de seus cartões — primeiro por prioridade original e, em seguida, por duas fórmulas de classificação diferentes aplicadas a perfis de amostra diferentes — para que você possa ver como o mesmo conjunto de itens se reorganiza dependendo de quem está perguntando.

>[!VIDEO](https://video.tv.adobe.com/v/3502209/)

## Principais pontos

- Uma fórmula de classificação ajusta dinamicamente a pontuação de prioridade de um item de decisão por perfil, com base nos atributos do perfil ou no evento de experiência de acionamento
- As fórmulas suportam matemática básica (adicionar, subtrair, multiplicar, dividir) e podem fazer referência à pontuação de prioridade original do item de decisão como uma variável
- A lógica da regra: se uma condição sobre o perfil ou a ocorrência for verdadeira, ajuste a prioridade para itens de decisão que atendam a determinados critérios de item
- Toda configuração de fórmula de classificação precisa de uma fórmula padrão para itens de decisão que nenhuma regra de ajuste afete
- Quando dois itens de decisão chegam à mesma pontuação de prioridade ajustada, a decisão os ordena aleatoriamente
