---
hold: true
title: Criação do item de decisão
description: Saiba como os atributos de item de decisão diferem das configurações de qualificação, além da proteção no nível da organização em itens de decisão e impressões em relação a eventos de decisão.
doc-type: article
solution: Experience Platform
exl-id: 28752ac1-118c-41d9-af6a-9907f854df1e
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---


# Criação do item de decisão

## Objetivo de aprendizado

Ao final desta lição, você será capaz de:

- Diferenciar os atributos de um item de decisão de suas configurações de qualificação
- Apresente a proteção sobre os itens de decisão por organização IMS e por que ela é no nível da organização, não no nível da sandbox
- Distinguir uma impressão de um evento de decisão
- Diferenciar regras de decisão de públicos por escopo, tempo e os dados que cada um pode acessar

## Materiais necessários

- 12 cartas de baralho (Jack, Queen, King de cada naipe)
- 12 notas adesivas, com nomes de atributos já escritos nelas na lição anterior

## Palestra

Esta é a lição mais prática até agora. Você anexará uma nota adesiva a cada cartão e fará uma pausa várias vezes para gravar valores de nível, capacidade, exibição, câmera, prioridade e qualificação à medida que cada conceito for introduzido.

>[!VIDEO](https://video.tv.adobe.com/v/3502207/)

## Principais pontos

- Um item de decisão tem duas metades: atributos (nome, descrição, atributos personalizados, tags, prioridade) e qualificação (datas, inclusão da regra de decisão, inclusão do público-alvo, limite)
- Um cliente pode ter até 10.000 itens de decisão — esse limite é por organização IMS, não por sandbox
- As pontuações de prioridade mais alta são retornadas primeiro
- Uma regra de decisão é uma condição if/true com escopo para uma única campanha ou jornada, avaliada no momento da decisão e pode usar atributos de item de decisão; um público-alvo é um grupo mais amplo de perfis, avaliado em lote/streaming/velocidade de borda e não pode acessar atributos de item de decisão
- Usar uma regra de decisão em vez de um público-alvo quando a qualificação depender dos próprios atributos do item de decisão
- Um item de decisão pode ter mais de um acionador de limite (impressões, cliques, eventos de decisão, eventos personalizados) ao mesmo tempo
- Uma impressão conta quando o item é realmente visualizado na borda; um evento de decisão conta sempre que a decisão avalia e retorna uma resposta, vista ou não
- O limite é redefinido diariamente, semanalmente ou mensalmente à meia-noite GMT — não no horário local
