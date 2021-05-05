---
title: Blueprint de Ciência de dados personalizada para aprimoramento de perfis
description: Este blueprint apresenta como o Data Science Workspace, da Adobe Experience Platform, pode usar os dados contidos na Experience Platform para treinar, implantar e classificar modelos a fim de fornecer insights de aprendizado de máquina a partir dos dados.
solution: Experience Platform,Data Collection
kt: 7203
exl-id: e5ec6886-4fa4-4c9b-a2d8-e843d7758669,f0efaf3c-6c4f-47c3-ab8a-e8e146dd071c
translation-type: tm+mt
source-git-commit: 9fe9d67c5f97b633e45155bd54e2006f1b797332
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 63%

---

# Blueprint de Ciência de dados personalizada para aprimoramento de perfis

A Ciência de dados personalizados para o esquema de enriquecimento de perfil ilustra como os dados no Adobe Experience Platform podem ser usados no [!UICONTROL Data Science Workspace] para treinar, implantar e pontuar modelos para fornecer insights de aprendizado de máquina. Esses modelos podem ser enviados diretamente para um conjunto de dados habilitado para [!UICONTROL Real-time Customer Profile] para enriquecer ainda mais os perfis de clientes. Esses insights podem ser ativados para personalização. Exemplos de insights de aprendizado de máquina incluem pontuação de valor vitalício, afinidade de produto e categoria, propensão para conversão ou propensão para churn.

## Casos de uso

* Extraia insights e descubra padrões a partir de dados do cliente na Experience Platform. Treine e classifique modelos com esses dados.
* Enriqueça o [!UICONTROL Perfil do cliente em tempo real] com insights e atributos orientados por modelo para personalização mais granular e jornadas otimizadas.
* Treine e classifique modelos para determinar insights do cliente, como valor vitalício do cliente, propensão à conversão ou à rotatividade, afinidade de conteúdos e produtos e classificação de engajamentos.

## Arquitetura

<img src="assets/data_science.svg" alt="Blueprint de arquitetura de referência para Ciência de dados personalizada para aprimoramento de perfis" style="border:1px solid #4a4a4a" />

## Etapas de implementação

1. [Crie ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html) esquemas para os dados que serão assimilados.
1. [Crie ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) conjuntos de dados para que os dados sejam assimilados.
1. [Assimile dados na Experience Platform.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion)
1. Crie um DSW notebook.
1. Escolha um idioma. Python e PySpark são compatíveis.
1. Crie um modelo no notebook.
1. Treine o modelo.
1. Classifique o modelo para gerar predições com os dados do público-alvo.
1. Ative o conjunto de dados de resultados do modelo para o perfil, caso envie os resultados do modelo para o [!UICONTROL Real-time Customer Profile].

## Documentos relacionados

* [Descrição do produto Adobe Experience Platform Intelligence](https://helpx.adobe.com/br/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Documentação do Data Science Workspace](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=pt-BR)
* [Tutoriais do Data Science Workspace](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/understanding-data-science-workspace.html?lang=pt-BR)

## Publicações do blog relacionadas

* [[!DNL Simplifying the Data Science Lifecycle with Adobe Platform Experience]](https://medium.com/adobetech/simplifying-the-data-science-lifecycle-with-adobe-platform-experience-8ea4f056d82f)
* [[!DNL Content and Commerce AI: Personalizing Your Interactions with Customers Through Content Intelligence]](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [[!DNL Gaining a Deeper Understanding of Churn Using Data Science Workspace]](https://medium.com/adobetech/gaining-a-deeper-understanding-of-churn-using-data-science-workspace-18a2190e0cf3)
* [[!DNL Understanding Data Science In Adobe Experience Platform]](https://medium.com/adobetech/understanding-data-science-in-adobe-experience-platform-5bce5a17b42)
* [[!DNL An Introductory Look at Exploratory Data Analysis on Adobe Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [[!DNL Cutting Across Adobe Experience Products with Machine Learning to Elevated User Experience]](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [[!DNL Modeling XDM Data for Data Science at Scale on Adobe Experience Platform]](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7)
* [[!DNL Segmentation.AI: Automated Audience-Clustering-as-a-Service in Adobe Experience Platform]](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)
* [[!DNL Reimagining Jupyter Notebooks for Enterprise Scale]](https://medium.com/adobetech/reimagining-jupyter-notebooks-for-enterprise-scale-8bc6340d504a)
* [[!DNL Accelerate Intelligent Insights with Adobe Experience Platform Data Science Workspace]](https://medium.com/adobetech/accelerate-intelligent-insights-with-adobe-experience-platform-data-science-workspace-89538bacbbea)
* [[!DNL A Preview of Time Series Forecasting with Adobe Experience Platform]](https://medium.com/adobetech/preview-of-time-series-forecasting-with-adobe-experience-platform-38a2fc778e89)
* [[!DNL Cutting Across Adobe Experience Products with Machine Learning to Elevated User Experience]](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
