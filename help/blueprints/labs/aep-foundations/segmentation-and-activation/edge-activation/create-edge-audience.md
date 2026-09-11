---
title: Criar público-alvo do Edge
description: Crie e publique um público avaliado pela Edge junto com um lote equivalente para comparar como cada um responde aos eventos recebidos em tempo real.
doc-type: article
solution: Experience Platform
exl-id: 79265a8f-81dd-41a3-89c5-c6646e435328
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# Criar público-alvo do Edge

Este público-alvo será usado para qualificar alguém quando uma carga (por exemplo, exibição de página) vier do cliente (por exemplo, Web SDK) para a Edge.

>[!NOTE]
>
>Avaliamos um público-alvo na Edge geralmente para que possamos reverter e usá-lo no Personalization. Se não estivermos fazendo o Personalization na Edge, podemos apenas ter o público-alvo avaliado como Streaming no Hub.

## Criar público

1. No painel à esquerda, clique em Públicos-alvo
1. Clique em Criar público-alvo no canto superior direito da tela
1. Clique em Criar regra



A página ![Públicos-alvo com o botão Criar público-alvo e a opção Criar regra foi realçada](assets/create-edge-audience-create-audience-step-1.png)



![Tela Criar Regra aberta para criar um novo público-alvo](assets/create-edge-audience-create-audience-step-2.png)



## Converter público-alvo em regras

1. Vá para **Audiences** e clique na pasta **Experience Platform**
1. Arraste e solte o público-alvo chamado **dep: Qualquer fluxo de evento (em uma hora)** na tela

   ![Arrastando a profundidade: Qualquer público-alvo de Streaming de Eventos (em uma hora) para a tela do construtor de regras](assets/create-edge-audience-drag-audience-to-canvas.png)



1. Converta o público em um conjunto de regras na tela ao clicar no **ícone** abaixo e clicar em **Converter**

![Ícone Converter na tela usada para converter o público em um conjunto de regras](assets/create-edge-audience-convert-to-rules-icon.png)

## Atualizar regras de evento

Faça as seguintes alterações nas regras de evento (talvez seja necessário expandir o evento para vê-lo)

1. No(s) último(s)
1. 15
1. Minutes

![Regra de eventos configurada para disparar nos Últimos 15 Minutos](assets/create-edge-audience-update-event-rules.png)

## Publicar segmento

1. Atualize o nome do segmento para **Qualquer Edge de Evento (em 15 minutos)**
1. Atualizar o método de avaliação para Edge
1. Publicar o segmento

![Detalhes do segmento que mostram o método de avaliação do Edge antes da publicação](assets/create-edge-audience-publish-segment.png)

## Criar segmento avaliado em lote

Repita as mesmas etapas que você acabou de fazer para o segmento de borda criado, mas use as seguintes informações:

>[!NOTE]
>
>Criaremos um público-alvo em lote para que você possa ver que, mesmo que um evento seja transmitido para a Edge, os públicos-alvo salvos como avaliação em lote não serão avaliados de forma streaming.

Regras de evento:

- No(s) último(s)
- 1
- Dia



Detalhes do segmento:

- Nome -> **Qualquer Lote de Eventos (em 1 dia)**
- Método de avaliação -> Lote
