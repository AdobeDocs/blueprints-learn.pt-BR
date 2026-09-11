---
title: Medidas de proteção, modelos de IA e o futuro da Decisão
description: Saiba mais sobre as principais medidas de proteção da decisão, como os modelos de classificação de IA diferem das fórmulas e como os componentes básicos do decisioning se conectam de ponta a ponta.
doc-type: article
solution: Experience Platform
exl-id: 90902f6e-ba3c-4852-ab82-ad852698b227
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# Medidas de proteção, modelos de IA e o futuro da Decisão

## Objetivo de aprendizado

Ao final desta lição, você será capaz de:

- Lembre-se das duas medidas de proteção mais comumente encontradas na prática
- Diferenciar a otimização automática dos modelos de IA de otimização personalizada
- Explicar como a decisão se estende além do produto ODE herdado
- Resumir como os oito elementos se encaixam de ponta a ponta

## Palestra

O vídeo abaixo aborda as duas medidas de proteção de decisão mais comuns, como os modelos de classificação de IA diferem das fórmulas de classificação manuais, como a decisão se estende além do mecanismo herdado do Offer Decisioning e um resumo de como os oito blocos fundamentais se conectam de ponta a ponta.

>[!VIDEO](https://video.tv.adobe.com/v/3502212/)

## Principais pontos

- As duas medidas de proteção mais acessadas são: 10.000 itens de decisão por organização IMS (não por sandbox) e 100 atributos personalizados por esquema; verifique a documentação do produto em busca de números atuais, pois eles estão sujeitos a alterações
- Os modelos de IA podem ser usados em fórmulas de classificação; a otimização automática não é personalizada e otimiza o desempenho global, enquanto a otimização personalizada serve itens para metas comerciais específicas por perfil
- As pontuações do modelo computadas fora do AEP podem ser trazidas como atributos de perfil e usadas em regras de elegibilidade ou fórmulas de classificação
- A decisão vai além do mecanismo herdado do Offer Decisioning: usa o XDM para reutilização, fornece JSON para aplicativos headless e separa o item de decisão do tratamento
- A decisão pode condicionar a definição do caminho da jornada e a prioridade de entrada em uma resposta de decisão
- Fim ao fim: o item de decisão XDM define atributos → criação de item de decisão atribui valores e elegibilidade → itens de grupo de coleções → fórmulas de classificação ajustam prioridade por perfil → estratégias de seleção classificam e filtram uma coleção → políticas de decisão aplicam estratégias a um canal → pacotes de decisão ativos no hub ou borda
