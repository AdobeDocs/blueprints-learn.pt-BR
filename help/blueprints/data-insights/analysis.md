---
title: Enterprise Data Exploration and Reporting Blueprint
description: Esse blueprint mostra a capacidade do Adobe Experience Platform de realizar consultas exploratórias e análise dos dados existentes no lago de dados.
solution: Experience Platform
kt: 7207
thumbnail: null
exl-id: 3b22dfdd-3fbe-40b3-b798-1ee983723039
translation-type: tm+mt
source-git-commit: f5d8b3fea11df0ffaeb59f0b53e93d76426ef252
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Enterprise Data Exploration and Reporting Blueprint

A exploração e o relatório de dados empresariais compreendem a capacidade da Adobe Experience Platform de realizar consultas exploratórias e análises dos dados existentes no lago de dados.

O Serviço de Consulta permite que o SQL seja executado nos dados. O Data Science Workspace permite que a exploração de dados, a ciência de dados e as cargas de trabalho de aprendizado de máquina sejam executadas nos dados.

Além disso, o Experience Platform permite que conexões com clientes SQL, interfaces e ferramentas de Business Intelligence (BI) de terceiros se conectem, acessem e consultem diretamente os dados no Experience Platform, usando o protocolo PostgreSQL.

Determinadas medidas de proteção se aplicam ao tempo limite da consulta e à quantidade de dados incluídos no resultado da consulta, conforme observado nos detalhes do cenário.

## Casos de uso

* Consulta interativa e agregação de dados
* Acesso de linha e coluna a dados assimilados para exploração e validação
* Dashboarding and visualization data via ferramenta de Business Intelligence

## Aplicativos

* Adobe Experience Platform

## Cenários

| Cenário | Descrição | Aplicativos/Serviços do Experience Cloud |
|---|---|---|
| **Exploração de dados - consulta bruta de dados** | <ul><li>Escreva e execute consultas SQL no lago de dados usando a interface de usuário de consulta interativa ou um cliente SQL conectado. O Data Science Workspace também pode ser usado para consultar e obter informações dos dados brutos no Experience Platform.</li></ul> | <ul><li>Adobe Experience Platform</li></ul> |
| **Dashboarding empresarial** | <ul><li>Conecte as ferramentas do Business Intelligence ao Experience Platform para visualizar dados para painéis e casos de uso de relatórios.</li></ul> | <ul><li>Adobe Experience Platform</li></ul> |

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
