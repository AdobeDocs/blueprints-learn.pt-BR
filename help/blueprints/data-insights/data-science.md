---
title: Ciência de dados personalizados para o esquema de enriquecimento de perfil
description: Este blueprint mostra como o Data Science Workspace da Adobe Experience Platform pode usar os dados no Experience Platform para treinar, implantar e pontuar modelos para fornecer insights de aprendizado de máquina a partir dos dados.
solution: Experience Platform,Data Collection
kt: 7203
exl-id: e5ec6886-4fa4-4c9b-a2d8-e843d7758669,f0efaf3c-6c4f-47c3-ab8a-e8e146dd071c
translation-type: tm+mt
source-git-commit: e9e8473f62fa222e483f7aeed33148433f1ec427
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Ciência de dados personalizados para o esquema de enriquecimento de perfil

A Ciência de dados personalizados para o esquema de enriquecimento de perfil ilustra como os dados no Adobe Experience Platform podem ser usados no Data Science Workspace para treinar, implantar e pontuar modelos para fornecer insights de aprendizado de máquina. Esses modelos podem ser enviados diretamente para um conjunto de dados habilitado para o Perfil do cliente em tempo real para enriquecer ainda mais os perfis do cliente. Esses insights podem ser ativados para personalização. Exemplos de insights de aprendizado de máquina incluem pontuação de valor vitalício, afinidade de produto e categoria, propensão para conversão ou propensão para churn.

## Casos de uso

* Extraia padrões de insight e descoberta dos dados do cliente no Experience Platform. Treine e marque modelos a partir desses dados.
* Enriqueça o Perfil do cliente em tempo real com insights e atributos orientados por modelo para personalização mais granular e jornadas otimizadas.
* Treine e avalie modelos para determinar insights do cliente, como valor vitalício do cliente, propensão para converter ou churn, afinidades de produto e conteúdo e pontuações de engajamento.

## Arquitetura

<img src="assets/datascience.svg" alt="Arquitetura de referência para a ciência de dados personalizada para o esquema de enriquecimento de perfil" style="border:1px solid #4a4a4a" />

## Etapas da implementação

1. Crie esquemas e conjuntos de dados.
1. Assimilar dados no Experience Platform.
1. Crie um notebook DSW.
1. Escolha um idioma. Python e PySpark são compatíveis.
1. Modelo de autor em bloco de notas.
1. Treine o modelo.
1. Pontuação do modelo para gerar previsões com os dados do target.
1. Ative o conjunto de dados de resultados do modelo para perfil, caso envie os resultados do modelo para o Perfil do cliente em tempo real.

## Documentação relacionada

* [Descrição do produto Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Documentação do Data Science Workspace](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=en)
* [Tutoriais do Data Science Workspace](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/understanding-data-science-workspace.html)

## Publicações de blog relacionadas

* [Simplificação do ciclo de vida da ciência de dados com a experiência da plataforma Adobe](https://medium.com/adobetech/simplifying-the-data-science-lifecycle-with-adobe-platform-experience-8ea4f056d82f)
* [Content e Commerce AI: Personalização de suas interações com clientes por meio da inteligência de conteúdo](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [Saiba mais sobre o Churn usando o Data Science Workspace](https://medium.com/adobetech/gaining-a-deeper-understanding-of-churn-using-data-science-workspace-18a2190e0cf3)
* [Entendendo A Ciência De Dados No Adobe Experience Platform](https://medium.com/adobetech/understanding-data-science-in-adobe-experience-platform-5bce5a17b42)
* [Uma introdução à Análise de dados exploratórios no Adobe Experience Platform](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [Recortar produtos da Adobe Experience com aprendizado de máquina para uma experiência do usuário elevada](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [Modelagem de dados XDM para ciência de dados em escala no Adobe Experience Platform](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7)
* [Segmentação.AI: Cluster automatizado de público-alvo como um serviço no Adobe Experience Platform](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)
* [Reimaginando notebooks Júpiter para escala corporativa](https://medium.com/adobetech/reimagining-jupyter-notebooks-for-enterprise-scale-8bc6340d504a)
* [Acelere os insights inteligentes com o Adobe Experience Platform Data Science Workspace](https://medium.com/adobetech/accelerate-intelligent-insights-with-adobe-experience-platform-data-science-workspace-89538bacbbea)
* [Uma Pré-visualização da Previsão de Série de Tempo com o Adobe Experience Platform](https://medium.com/adobetech/preview-of-time-series-forecasting-with-adobe-experience-platform-38a2fc778e89)
* [Recortar produtos da Adobe Experience com aprendizado de máquina para uma experiência do usuário elevada](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
