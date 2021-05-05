---
title: Blueprint de análise e inteligência de dados
description: Este blueprint apresenta a capacidade da Adobe Experience Platform de realizar consulta e análise exploratória dos dados existentes no data lake.
solution: Experience Platform
kt: 7207
thumbnail: null
exl-id: 3b22dfdd-3fbe-40b3-b798-1ee983723039,a972ea56-d1c8-45da-9044-ed31222a2441
translation-type: tm+mt
source-git-commit: 6365fa00a77ba22774b2d6de3e882a3e09dcae0f
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 31%

---

# Blueprint de análise e inteligência de dados

A Análise de dados e a Inteligência incluem a capacidade do Adobe Experience Platform de realizar consultas exploratórias e análises dos dados existentes no lago de dados.

O Experience Platform [!UICONTROL Query Service a1/> permite que consultas SQL sejam executadas nos dados. ] [!UICONTROL O Data Science ] Workspace permite que a exploração de dados, a ciência de dados e as cargas de trabalho de aprendizado de máquina sejam executadas nos dados.

Além disso, o Experience Platform permite que conexões com clientes SQL, interfaces e ferramentas de Business Intelligence (BI) de terceiros se conectem, acessem e consultem diretamente os dados no Experience Platform, usando o protocolo [!DNL PostgreSQL].

Determinadas medidas de proteção se aplicam ao tempo limite da consulta e à quantidade de dados incluídos no resultado da consulta, conforme observado nos detalhes do blueprint.

## Casos de uso

* Consulta interativa e agregação de dados
* Acesso de linhas e colunas a dados assimilados para exploração e validação
* Painéis e visualização de dados por meio de ferramentas de Business Intelligence

## Aplicativos

* Adobe Experience Platform

## Arquitetura

<img src="assets/data_exploration.svg" alt="Blueprint de arquitetura de referência para Relatórios e exploração de dados corporativos" style="border:1px solid #4a4a4a" />

## Medidas de proteção

Consulte a Documentação do produto do Serviço de query para obter detalhes sobre práticas recomendadas e medidas de proteção.
[Diretrizes do Serviço de query](https://experienceleague.adobe.com/docs/experience-platform/query/best-practices/writing-queries.html?lang=en#best-practices)

## Etapas de implementação

1. [Crie ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html) esquemas para os dados que serão assimilados.
1. [Crie ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) conjuntos de dados para que os dados sejam assimilados.
1. [Assimile os dados na Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion).
1. Confirme se os dados estão disponíveis para [!UICONTROL Serviço de consulta] e [!UICONTROL Data Science Workspace] para acesso e consulta brutos.
1. Conecte as ferramentas do Business Intelligence e os clientes SQL a [!UICONTROL Serviço de Consulta] para visualização, consulta de dados e exploração.

## Documentos relacionados

* [Descrição do produto Adobe Experience Platform Intelligence](https://helpx.adobe.com/br/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Documentação do Serviço de consulta](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=pt-BR)
