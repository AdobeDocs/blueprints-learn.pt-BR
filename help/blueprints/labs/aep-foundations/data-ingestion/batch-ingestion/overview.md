---
hold: true
title: Assimilação em lote
description: Carregue dados da conta do cliente por meio da assimilação em lote no Data Lake e no Perfil, corrigindo erros de mapeamento e qualidade de dados.
doc-type: overview-page
solution: Experience Platform
exl-id: 76830e79-8fc0-4fda-98b1-2c1de19e8158
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Assimilação em lote

## Objetivos de aprendizagem

Neste exercício, você carregará os dados da conta do cliente de um conector de origem baseado em arquivo para o AEP Data Lake e, em seguida, para o Perfil. Você aprenderá o seguinte:

1. Noções básicas sobre mapeamentos de passagem
1. Correção de mapeamentos de passagem gerados por ML
1. Uso da pré-visualização de dados de origem para verificar quaisquer problemas de qualidade de dados
1. Agendando uma execução de fluxo de dados
1. Lidar com erros provenientes de valores ausentes em campos obrigatórios
1. Tratamento de erros resultantes de erros de incompatibilidade de tipos de dados
1. Lidar com erros de assimilação de dados e recuperar-se dessa falha
1. Interativamente usando dados de teste para gerar um conjunto de mapeamento abrangente.

>[!NOTE]
>
>Se você não concluiu a criação do esquema da Conta do cliente nos laboratórios anteriores, é possível navegar até o catálogo de esquemas e usar **dep: Conta do cliente**
