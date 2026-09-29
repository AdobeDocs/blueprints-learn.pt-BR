---
title: Tentar novamente um fluxo de dados com falha
description: Repita uma execução de fluxo de dados com falha para que os dados de origem sejam reprocessados em relação às regras de mapeamento atualizadas em um novo fluxo de dados.
doc-type: article
solution: Experience Platform
exl-id: 83ecf037-e524-4887-b833-5ed96af40419
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 1d6ba1444c119437eb8a86d5c4a1050d56d16023
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%
---

# Tentar novamente um fluxo de dados com falha

Para repetir um fluxo de trabalho, faça o seguinte:

1. Navegue até **Fontes -> Fluxos de Dados -> \[Nome do Fluxo de Dados] -> \[Execução com Falha]**
1. Realce a execução do fluxo de dados que falhou ao ativar o painel direito.
1. Clique em **Repetir**. A nova tentativa capturará a cópia dos dados associados à execução com falha e aplicará as novas regras de mapeamento a ela

![Tentando novamente uma execução de fluxo de dados com falha no painel direito](assets/retry-a-failed-dataflow.png)

>[!NOTE]
>
>Observe que, quando você tenta novamente um fluxo de dados com falha, um novo fluxo de dados é criado e executado. Ele aparecerá na parte superior da lista de fluxos de dados
