---
title: Blueprint de análise de dados e inteligência
description: Use Adobe [!DNL Experience Platform] (AEM) para realizar query exploratória e análise dos dados existentes no data lake.
solution: Experience Platform
kt: 7207
thumbnail: null
exl-id: a972ea56-d1c8-45da-9044-ed31222a2441
source-git-commit: 7f3bc307f74aa88a7a73f3e50cc48bd16f58b37f
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 59%

---

# Análise de dados e blueprint de inteligência

A análise e a inteligência de dados incluem a capacidade em [!DNL Experience Platform] de realizar uma consulta exploratória e uma análise dos dados existentes no data lake.

O [!UICONTROL Serviço de consulta] de [!DNL Experience Platform] permite que consultas SQL sejam executadas nos dados.

[!DNL Experience Platform] permite conexões com clientes SQL, interfaces e ferramentas Business Intelligence (BI) de terceiros para conectar-se diretamente, acessar e consultar os dados em [!DNL Experience Platform], usando o protocolo [!DNL PostgreSQL].

## Casos de uso

* Consulta interativa e agregação de dados
* Acesso de linhas e colunas a dados assimilados para exploração e validação
* Painéis e visualização de dados por meio de ferramentas de Business Intelligence

Outros casos de uso comuns para o serviço de consulta estão descritos aqui [Casos de uso do serviço de consulta](https://experienceleague.adobe.com/docs/experience-platform/query/use-cases/abandoned-browse.html?lang=pt-BR)

## Aplicativos

* Adobe [!DNL Experience Platform]

## Arquitetura

<img src="assets/data_exploration.svg" alt="Blueprint de arquitetura de referência para Relatórios e exploração de dados corporativos" style="width:90%; border:1px solid #4a4a4a" />

## Medidas de proteção

Consulte a documentação do produto Serviço de consulta para detalhes sobre práticas recomendadas e medidas de proteção.
[Guia do Serviço de consulta](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=pt-BR)

## Etapas de implementação

1. [Crie esquemas](https://experienceleague.adobe.com/?lang=pt-br&recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=pt-BR) para que os dados sejam assimilados.
1. [Crie conjuntos de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) para que os dados sejam assimilados.
1. [Assimilar dados](https://experienceleague.adobe.com/?lang=pt-br&recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) em [!DNL Experience Platform].
1. Confirme se os dados estão disponíveis para [[!UICONTROL Serviço de consulta]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=pt-BR).
1. [Conecte as ferramentas de Business Intelligence e os clientes SQL ao [!UICONTROL Serviço de consulta]](https://experienceleague.adobe.com/docs/experience-platform/query/clients/overview.html?lang=pt-BR) para visualização, consulta de dados e exploração.

## Documentação relacionada

* [Adobe [!DNL Experience Platform] Descrição do produto de inteligência](https://helpx.adobe.com/br/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* Documentação do [[!UICONTROL Serviço de consulta]](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=pt-BR)
