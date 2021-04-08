---
title: Blueprint de análise e inteligência de dados
description: Esse blueprint mostra a capacidade do Adobe Experience Platform de realizar consultas exploratórias e análise dos dados existentes no lago de dados.
solution: Experience Platform
kt: 7207
thumbnail: null
exl-id: 3b22dfdd-3fbe-40b3-b798-1ee983723039,a972ea56-d1c8-45da-9044-ed31222a2441
translation-type: tm+mt
source-git-commit: cd98c46d948af9026449c947496df82fd1be6718
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Blueprint de análise e inteligência de dados

A Análise de dados e a Inteligência incluem a capacidade do Adobe Experience Platform de realizar consultas exploratórias e análises dos dados existentes no lago de dados.

O Serviço de Consulta permite que o SQL seja executado nos dados. O Data Science Workspace permite que a exploração de dados, a ciência de dados e as cargas de trabalho de aprendizado de máquina sejam executadas nos dados.

Além disso, o Experience Platform permite que conexões com clientes SQL, interfaces e ferramentas de Business Intelligence (BI) de terceiros se conectem, acessem e consultem diretamente os dados no Experience Platform, usando o protocolo PostgreSQL.

Determinadas medidas de proteção se aplicam ao tempo limite da consulta e à quantidade de dados incluídos no resultado da consulta, conforme observado nos detalhes do cenário.

## Casos de uso

* Consulta interativa e agregação de dados
* Acesso de linha e coluna a dados assimilados para exploração e validação
* Dashboarding and visualization data via ferramenta de Business Intelligence

## Aplicativos

* Adobe Experience Platform

## Arquitetura

<img src="assets/dataexplore.svg" alt="Arquitetura de referência para o Enterprise Data Exploration and Reporting Blueprint" style="border:1px solid #4a4a4a" />

## Medidas de proteção

* Limite de tempo de 10 minutos para consultas interativas
* Limite de 100 registros retornado na interface do usuário
* Limite de 50.000 registros retornado pelo conector SQL

## Etapas da implementação

1. Configure os conjuntos de dados e esquemas para a assimilação de dados no lago de dados.
1. Assimilar dados.
1. Confirme se os dados estão disponíveis para o Serviço de query e o Data Science Workspace para acesso e consulta brutos.
1. Conecte ferramentas do Business Intelligence e clientes SQL ao Serviço de query para visualização, consulta de dados e exploração.

## Documentação relacionada

* [Descrição do produto Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Documentação do Serviço de query](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en)
