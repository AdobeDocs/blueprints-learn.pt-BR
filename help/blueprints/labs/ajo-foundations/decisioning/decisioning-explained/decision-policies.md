---
hold: true
title: Políticas de decisão
description: Saiba como as políticas de decisão aplicam estratégias de seleção a um canal de entrega e como os métodos de combinação individuais versus agrupados alteram a ordem de oferta.
doc-type: article
solution: Experience Platform
exl-id: 21dc67fd-76ac-4b82-ae78-be024c7bfc55
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Políticas de decisão

## Objetivo de aprendizado

Ao final desta lição, você será capaz de:

- Explicar o que uma política de decisão configura e onde é aplicada
- Definir um pacote de decisões e o que ele contém
- Diferenciar os métodos individuais e agrupados de combinação de várias estratégias de seleção
- Explicar como o limite de frequência interage com o número de itens de decisão que uma política retorna

## Materiais necessários

- 12 cartas de baralho (Jack, Queen, King de cada naipe)
- 13 notas adesivas
  - 12 preenchido com o nome do atributo e os valores das lições anteriores
  - Uma nova nota adesiva para rastrear as solicitações

## Palestra

Este é o simulado mais longo e mais envolvido do curso. Você simulará o comportamento de políticas de decisão em tempo real (fazendo &quot;solicitações&quot; repetidas), rastreando impressões em relação a limites de frequência e observando os cartões serem descartados e substituídos) e, em seguida, aplicará tudo a um cenário de negócios real comparando a combinação de estratégia de seleção individual versus agrupada.

>[!VIDEO](https://video.tv.adobe.com/v/3502211/)

## Principais pontos

- Uma política de decisão aplica estratégias de seleção a um canal de delivery real do AJO, configurado em um nó de canal em uma jornada ou seção de canal de uma campanha
- Uma política pode usar estratégias de seleção &quot;nenhum&quot;, &quot;um&quot; ou &quot;muitos&quot;; com &quot;nenhum&quot;, ela retorna itens por pontuação de prioridade original, filtrados por elegibilidade no nível do item
- Uma política de decisão e seu canal de entrega são chamados de pacote de decisão, a configuração que fica no hub ou na borda
- Com a combinação individual, cada coleção de estratégia é ordenada separadamente, então as listas são empilhadas; com agrupadas, todos os itens são ordenados juntos em uma lista e as duplicatas usam a maior de suas duas pontuações
- As mesmas entradas podem produzir ordens finais drasticamente diferentes, dependendo de ordens individuais ou agrupadas
- O limite de frequência limita diretamente quantos itens estão disponíveis para retorno, portanto, planeje itens de fallback não limitados suficientes para preencher cada slot
