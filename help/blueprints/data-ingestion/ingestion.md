---
title: Preparação de dados e plano de assimilação
description: Este blueprint mostra todos os métodos pelos quais os dados podem ser assimilados e preparados no Adobe Experience Platform.
solution: Experience Platform, Data Collection
kt: 7204
thumbnail: null
exl-id: 5c3c94b6-c928-4d93-8b38-f8bd2aad2e68
translation-type: tm+mt
source-git-commit: f5d8b3fea11df0ffaeb59f0b53e93d76426ef252
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---

# Preparação de dados e plano de assimilação

O Plano de preparação e assimilação de dados abrange todos os métodos pelos quais os dados podem ser preparados e assimilados no Adobe Experience Platform.

A preparação de dados inclui o mapeamento dos dados de origem para o esquema do Experience Data Model (XDM). Também inclui a execução de transformações nos dados, incluindo formatação de data, divisão/concatenação/conversões de campo e união/mesclagem/rechaveamento de registros. A preparação de dados ajuda a unificar os dados do cliente para fornecer análises agregadas/filtradas, incluindo relatórios ou preparação de dados para montagem/ciência/ativação de dados do perfil do cliente.

## Arquitetura

<img src="assets/dataingest.svg" alt="Arquitetura de referência para o plano de preparação e assimilação de dados" style="border:1px solid #4a4a4a" />

## Métodos de assimilação de dados

| Métodos de ingestão | Descrição |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SDK Web/móvel | Latência:<ul><li>Tempo real - mesma coleção de páginas à rede de borda</li><li>Assimilação de streaming para o Perfil ~1 minuto</li><li>Assimilação de streaming para lago de dados (microlote ~15 minutos)</ul>Documentação: <ul><li>[Web SDK](https://experienceleague.corp.adobe.com/docs/web-sdk.html)</li><li>[SDK móvel](https://experienceleague.adobe.com/docs/mobile.html?lang=en)</li></ul> |
| Fontes de transmissão | Latência:<ul><li>Tempo real - mesma coleção de páginas à rede de borda</li><li>Assimilação de streaming para o Perfil ~1 minuto</li><li>Assimilação de streaming para lago de dados (microlote ~15 minutos)</li></ul>[Documentação](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors) |
| API de transmissão | Latência:<ul><li>Tempo real - mesma coleção de páginas à rede de borda</li><li>Assimilação de streaming para o Perfil ~1 minuto</li><li>Assimilação de streaming para lago de dados (microlote ~15 minutos)</li><li>7 GB/hora</li></ul>[Documentação](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=en#what-can-you-do-with-streaming-ingestion%3F) |
| Ferramenta ETL | Use ferramentas ETL para modificar e transformar dados corporativos antes da assimilação em Experience Platform.<br><br>Latência:<ul><li>O tempo depende do agendamento da ferramenta ETL externa, então as medidas de proteção de assimilação padrão são aplicadas com base no método usado para assimilação.</li></ul> |
| Fontes em lote | Busca agendada de fontes<br>Latência: ~ 200 GB/hora<br><br>[Documentação](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors)<br>[Tutorials de vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/overview.html) |
| API em lote | Latência:<ul><li>Assimilação em lote ao Perfil dependendo do tamanho e das cargas de tráfego ~45 minutos</li><li>Assimilação em lote ao lago de dados dependendo do tamanho e das cargas de tráfego</li></ul>[Documentação](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=en#batch) |
| Conectores de aplicativos Adobe | assimilar automaticamente dados provenientes de aplicativos Adobe Experience Cloud<ul><li>Adobe Analytics: [Documentação](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=en#connectors) e [Tutorial em vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html)</li><li>Audience Manager: [Documentação](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=en#connectors) e [Tutorial em vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-aam.html)</li></ul> |


## Métodos de preparação de dados

| Métodos de preparação de dados | Descrição |
|------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Data Science Workspace - Preparação de dados | Transformação orientada por modelo, transformação com script.<br>[Documentação](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=en) |
>[!NOTE]
>
>| Ferramenta ETL externa ([!DNL Snaplogic], [!DNL Mulesoft], [!DNL Informatica] e assim por diante) | Execute transformações complexas em ferramentas ETL e use APIs ou conectores de fonte de Experience Platform padrão para assimilar os dados resultantes.                                                                                                                                                               |

| Serviço de query - Preparação de dados                                  | Une, divide, mescla, transforma, consulta e filtre dados em um novo conjunto de dados. Usando Criar Tabela como Selecionar (CTAS) <br>[Documentação](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en#sql)                                                                       |
| Mapeador XDM e funções de preparação de dados (Streaming e lote)     | Mapeie os atributos de origem no formato CSV ou JSON em atributos XDM durante a assimilação do Experience Platform.<br>Calcular funções nos dados à medida que são assimilados; ou seja, formatação de dados, divisão, concatenação e assim por diante.<br>[Documentação](https://experienceleague.adobe.com/docs/experience-platform/data-prep/home.html?lang=en) |

## Publicações de blog relacionadas

* [Como aproveitar as plataformas de dados externos no Adobe Experience Platform Journey Orchestration](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17?source=your_stories_page-------------------------------------)
* [Assimilação de Alto Throughput com o Iceberg](https://medium.com/adobetech/high-throughput-ingestion-with-iceberg-ccf7877a413f?source=your_stories_page-------------------------------------)
* [Truques do serviço de query no Adobe Experience Platform (Gravando consultas e Armazenamento de conjuntos de dados derivados)](https://medium.com/adobetech/query-service-tricks-in-adobe-experience-platform-writing-queries-and-storing-derived-datasets-eaee0d6d683e?source=your_stories_page-------------------------------------)
* [Analisar o Experience Data Model da Adobe Experience Platform para entender mais completamente o poder do perfil do cliente em tempo real](https://medium.com/adobetech/digging-into-adobe-experience-platforms-experience-data-model-to-more-fully-understand-the-power-3e109271e04f?source=your_stories_page-------------------------------------)
* [Uma introdução à Análise de dados exploratórios no Adobe Experience Platform](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a?source=your_stories_page-------------------------------------)
* [Modelagem de dados XDM para ciência de dados em escala no Adobe Experience Platform](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7?source=your_stories_page-------------------------------------)