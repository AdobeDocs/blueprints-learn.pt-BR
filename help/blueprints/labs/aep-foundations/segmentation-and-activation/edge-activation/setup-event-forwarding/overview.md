---
hold: true
title: Configurar o encaminhamento de eventos
description: Saiba como o Encaminhamento de eventos usa propriedades, elementos de dados, regras e fluxos de dados para encaminhar eventos de borda para um endpoint de terceiros.
doc-type: overview-page
solution: Experience Platform
exl-id: da3d1c7f-3642-4de7-a297-fc36d09e7336
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Configurar o encaminhamento de eventos

O encaminhamento de eventos fica na Edge e permite criar um conjunto de regras e transformações leves para enviar eventos a qualquer endpoint.

Nesta etapa, vamos encaminhar todos os eventos enviados para a Edge para um webhook. O webhook atuará como um proxy para terceiros e permitirá que vejamos o que está acontecendo.

Para configurar isso, configuraremos:

- Uma Propriedade que contém todas as extensões, elementos de dados e regras necessários para decidir o que encaminhar e para onde
  - Um elemento de dados para fazer referência ao evento recebido ou analisá-lo em vários componentes individuais, se necessário
  - Uma regra para adicionar condições sobre o que encaminhar, transformar a carga e onde enviá-la
- Uma sequência de dados que configura quais serviços a utilizarão (por exemplo, encaminhamento de eventos e AEP)
  - Os dados enviados para esses Datastreams podem então realizar ações de acordo com o serviço configurado (por exemplo, encaminhar um evento e enviar dados para um Conjunto de dados)
