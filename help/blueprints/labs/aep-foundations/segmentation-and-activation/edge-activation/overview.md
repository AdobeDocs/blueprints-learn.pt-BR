---
hold: true
title: Ativação do Edge
description: Saiba como as velocidades de ativação do Edge, de transmissão e em lote são diferentes, e visualize as etapas do laboratório para criar um segmento de borda e configurar o encaminhamento de eventos.
doc-type: overview-page
solution: Experience Platform
exl-id: 9ecadff9-3838-4cd4-93b1-7c23a232f84c
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# Ativação do Edge

## Recapitulação da velocidade de ativação

O Adobe tem três velocidades de ativação destinadas a atender a diferentes necessidades:

1. Edge
1. Streaming
1. Lote

Vamos analisar como ativar o usando o Adobe Edge com o encaminhamento de eventos, os públicos-alvo da Edge e o Edge Personalization. Em seguida, mostraremos como usar Destinos de transmissão do Hub para a Edge e para um destino externo.

>[!NOTE]
>
>Não abordaremos a Ativação em lote neste laboratório. A Ativação em lote pode ser agendada em intervalos diferentes e o tempo dificulta a exibição em um ambiente de laboratório sem ter pelo menos de 3 a 24 horas.



## O que o laboratório vai cobrir

- Criar segmento do Edge
- Configurar o encaminhamento de eventos
- Enviar em um evento do Edge
- Isso aciona
  - Segmento do Edge a ser qualificado
  - Encaminhamento de eventos no Edge para enviar ao webhook
