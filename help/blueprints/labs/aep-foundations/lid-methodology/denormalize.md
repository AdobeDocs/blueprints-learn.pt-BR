---
title: Desnormalizar
description: Aplique as regras de desnormalização da metodologia LID para dobrar as tabelas de ponte e dependentes de um ERD de volta ao seu perfil pai, evento e tabelas de pesquisa.
doc-type: article
solution: Experience Platform
exl-id: c98c9f58-03bc-4b28-becb-f84f3de04300
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---


# Desnormalizar

## Palestra

Neste vídeo, você aprenderá as três regras de desnormalização para dobrar pesquisas e tabelas de ligação de volta às tabelas principais, além de como os requisitos de personalização e segmentação de transmissão afetam essas decisões.

>[!VIDEO](https://video.tv.adobe.com/v/3459083/?quality=12&learn=on)



## Detalhes do laboratório

>[!NOTE]
>
>Este laboratório concentra-se apenas na conexão 5G warehouse ERD

## Regras de desnormalização:

1. Qualquer tabela no modelo relacional rotulada como &quot;**D**&quot; com uma cardinalidade 1\:M ou como &quot;**B**&quot; será definida como uma matriz de objeto ou mapa na tabela pai
1. Acionado pela regra #1, antes de desnormalizar as tabelas &quot;**D**&quot; ou &quot;**B**&quot; que atuam como matrizes ou mapas, interrogue-as para determinar a melhor forma de desnormalizá-las novamente na tabela pai
1. Qualquer tabela no modelo relacional rotulada como &quot;**D**&quot; com uma cardinalidade de M:1 atuará como um objeto ou como uma lista de campos em sua tabela pai

## Desnormalização para regras de personalização:

Lembre-se sempre de analisar os casos de uso do cliente ao criar o modelo de dados.  Lembre-se do seguinte:

- A segmentação de transmissão não tem acesso a tabelas de pesquisa no momento da avaliação
- Somente as características e associações de segmento de um perfil estão acessíveis para personalizar o conteúdo

![Casos de uso de conexão 5G considerados ao aplicar desnormalização para personalização](assets/denormalize-connection-5g-use-cases.png "Casos de uso de conexão 5G")

>[!NOTE]
>
>Lembre-se de consultar o Scenario.pdf de treinamento 5G da Connection durante este laboratório!



## Etapa 1 - Preencher a tabela Perfil individual

1. Escreva nos campos que precisam ser desnormalizados na tabela Conta de Cliente de qualquer esquema &quot;**B**&quot; ou &quot;**D**&quot; relacionado
1. Analisar os casos de uso acima de quais campos adicionais são necessários para oferecer suporte à segmentação e/ou personalização por transmissão? Adicionar esses campos à tabela



## Etapa 2 - Preencher as tabelas de Eventos de experiência

1. Escreva os campos que precisam ser desnormalizados nas tabelas de Faturamento e Pedidos de qualquer tabela &quot;**B**&quot; ou &quot;**D**&quot; relacionada
1. Analisar os casos de uso acima de quais campos adicionais são necessários para oferecer suporte à segmentação e/ou personalização por transmissão? Adicionar esses campos à tabela



## Etapa 3 - Preencher as Tabelas de pesquisa

1. Escreva os campos que precisam ser desnormalizados de volta na tabela de pesquisa de Produto a partir de qualquer tabela &quot;**B**&quot; ou &quot;**D**&quot; relacionada
1. Analisar os casos de uso acima de quais campos adicionais são necessários para oferecer suporte à segmentação e/ou personalização por transmissão? Adicionar esses campos à tabela




## Revisão

O vídeo abaixo analisa como as tabelas 5G da Connection foram desnormalizadas em matrizes e objetos e como os casos de uso de aquisição e venda adicional exigiam a adição de campos adicionais às tabelas de perfil principal e de evento.

>[!VIDEO](https://video.tv.adobe.com/v/3459086/?quality=12&learn=on)
