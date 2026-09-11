---
title: XDM do item de decisão
description: Saiba mais sobre o esquema XDM pré-criado que cada item de decisão compartilha e como os atributos personalizados são aninhados em um namespace de locatário.
doc-type: article
solution: Experience Platform
exl-id: c42503a2-24e7-4a5d-98bf-38c16fe69733
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# XDM do item de decisão

## Objetivo de aprendizado

Ao final desta lição, você será capaz de:

- Identificar o esquema XDM pré-criado usado para cada item de decisão
- Explicar onde os atributos personalizados residem no esquema e a limitação que se aplica a eles
- Reconhecer como o aninhamento de atributos em um objeto pai oferece suporte à reutilização

## Materiais necessários

- bloco de pelo menos 12 notas adesivas (mais no caso de você cometer erros)

## Palestra

No decorrer do vídeo, você fará uma pausa para escrever quatro nomes de atributos no topo das suas 12 notas adesivas — você preencherá os valores reais na próxima lição.

>[!VIDEO](https://video.tv.adobe.com/v/3502206/)

## Principais pontos

- Cada item de decisão usa o mesmo esquema pré-criado: itens de oferta personalizados - experience decisioning
- Tudo no nó \_experience é exigido pelo sistema e não pode ser editado
- Os atributos personalizados ficam no namespace de locatário da sua organização e são limitados a 100 por esquema
- Há apenas um esquema para cada item de decisão — sem duplicatas ou versões alternativas
