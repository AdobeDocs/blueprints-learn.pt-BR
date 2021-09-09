---
title: Blueprint de análise de dados e inteligência
description: Este blueprint apresenta a capacidade da Adobe Experience Platform de realizar consultas e análises exploratórias dos dados existentes no data lake.
solution: Experience Platform
kt: 7207
thumbnail: null
exl-id: 3b22dfdd-3fbe-40b3-b798-1ee983723039
source-git-commit: 3c950cebaa25901ae50433775c510ed834d8bcd5
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 91%

---

# Blueprint de análise de dados e inteligência

A Análise de dados e Inteligência consiste na capacidade da Adobe Experience Platform de realizar consultas e análises exploratórias dos dados existentes no data lake.

Com o [!UICONTROL Serviço de consulta] da Experience Platform é possível realizar consultas SQL nos dados. O [!UICONTROL Data Science Workspace] habilita a execução de exploração de dados, ciência de dados e cargas de trabalho de aprendizado de máquina.

Além disso, a Experience Platform permite conexões com clientes SQL de terceiros, interfaces e ferramentas de Business Intelligence (BI) para conectar, acessar e consultar os dados diretamente na Experience Platform, usando o protocolo [!DNL PostgreSQL].

Algumas medidas de proteção se aplicam pelo tempo limite de consulta e pela quantidade de dados incluídos no resultado da consulta, conforme observado nos detalhes do blueprint.

## Casos de uso

* Consulta interativa e agregação de dados
* Acesso de linhas e colunas a dados assimilados para exploração e validação
* Painéis e visualização de dados por meio de ferramentas de Business Intelligence

## Aplicativos

* Adobe Experience Platform

## Arquitetura

<img src="assets/data_exploration.svg" alt="Blueprint de arquitetura de referência para Relatórios e exploração de dados corporativos" style="border:1px solid #4a4a4a" />

## Medidas de proteção

Consulte a documentação do produto Serviço de consulta para detalhes sobre práticas recomendadas e medidas de proteção.
[Guia do Serviço de consulta](https://experienceleague.adobe.com/docs/experience-platform/query/best-practices/writing-queries.html?lang=pt-BR#best-practices)

## Etapas de implementação

1. [Crie esquemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) para que os dados sejam assimilados.
1. [Crie conjuntos de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) para que os dados sejam assimilados.
1. [Assimile dados](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) na Experience Platform.
1. Confirme se os dados estão disponíveis para o [[!UICONTROL Serviço de consulta]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=en) e o [[!UICONTROL Data Science Workspace] para acesso e consulta brutos.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/load-data-in-jupyterlab-notebooks.html?lang=en)
1. [Conecte as ferramentas de Business Intelligence e os clientes SQL ao [!UICONTROL Serviço de consulta] para visualização, consulta de dados e exploração.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.qsvc.dash)

## Documentação relacionada

* [Descrição do produto Adobe Experience Platform Intelligence](https://helpx.adobe.com/br/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* Documentação do [[!UICONTROL Serviço de consulta]](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=pt-BR)
