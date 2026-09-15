---
title: Assimilação de fluxo
description: Carregue dados da conta do cliente por meio de uma fonte de transmissão no Data Lake e no Perfil usando uma entrada de transmissão e a API REST.
doc-type: overview-page
solution: Experience Platform
exl-id: 973a9cac-dc9d-4c5f-87c3-16a55efd1314
source-git-commit: 8b3391d41cd4a3ea6cb52d5167e627b7f6bd2c6e
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%
---

# Assimilação de fluxo

## Objetivos de aprendizagem

Neste exercício, carregaremos os dados da conta do cliente de uma fonte de transmissão para o Adobe Experience Platform Data Lake e o Perfil. O que você deveria ir embora depois de tomar este laboratório?

- Criando uma entrada de streaming
- Importação do conjunto de mapeamento de outro fluxo de dados
- Obter a ID de fluxo de dados e a ID de conjunto de dados da interface
- Utilização da API REST para assimilar um evento

>[!IMPORTANT]
>
>Conclua a [configuração do Postman](../../setup.md) antes de iniciar este laboratório.

>[!NOTE]
>
>Se você não concluiu a criação do esquema Contas do cliente nos laboratórios anteriores, é possível navegar até o catálogo de esquemas e usar **dep: Conta do cliente**
