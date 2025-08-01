---
title: Blueprint de Ciência de dados personalizada para enriquecimento de perfis
description: Saiba como os insights baseados em ciência de dados podem ser assimilados no [!DNL Experience Platform] para enriquecer o Perfil do cliente em tempo real.
solution: Data Collection
kt: 7203
exl-id: e5ec6886-4fa4-4c9b-a2d8-e843d7758669,f0efaf3c-6c4f-47c3-ab8a-e8e146dd071c
source-git-commit: 75a0f2a77f39a4320dc4c4b0db918879be099dd3
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 63%

---

# Ciência de dados personalizada para blueprint de enriquecimento de perfil

O blueprint de ciência de dados personalizada para enriquecimento de perfil ilustra como os dados podem ser usados para treinar, implantar e pontuar modelos para fornecer insights de aprendizado de máquina sobre o [!DNL Experience Platform] e o [!DNL Real-Time Customer Data Platform] a partir de ciência de dados e ferramentas de aprendizado de máquina.

Os insights modelados podem ser assimilados em [!DNL Experience Platform] para enriquecer o perfil do cliente em tempo real. Exemplos de insights de aprendizado de máquina incluem pontuação de valor vitalício, afinidade de categorias e produtos, propensão à conversão ou ao churn.

## Casos de uso

* Extraia insights e descubra padrões a partir de dados do cliente; treine e pontue modelos de acordo com esses dados.
* Aprimore o [!UICONTROL Perfil de cliente em tempo real] com insights e atributos orientados por modelos para uma personalização mais detalhada e jornadas aperfeiçoadas.
* Treine e classifique modelos para determinar insights do cliente, como valor vitalício do cliente, propensão à conversão ou à rotatividade, afinidade de conteúdos e produtos e classificação de engajamentos.

## Arquitetura

<img src="assets/data_science.svg" alt="Blueprint de arquitetura de referência para Ciência de dados personalizada para enriquecimento de perfis" style="width:90%; border:1px solid #4a4a4a" />

## Medidas de proteção

* Para obter medidas de proteção detalhadas e latências de ponta a ponta ao assimilar resultados de ciência de dados no [!DNL Experience Platform] e o Perfil do Cliente em Tempo Real, consulte as medidas de proteção de assimilação de dados e o diagrama de latência referenciado no [documento de medidas de proteção de implantação](../experience-platform/guardrails.md).

## Considerações de implantação

* Na maioria dos casos, o resultado do modelo deve ser assimilado como atributos de perfil, e não como eventos de experiência. Os resultados do modelo podem ser uma cadeia de caracteres de atributo simples. Se houver vários resultados de modelo a assimilar, é recomendável usar um campo de tipo matriz ou mapa.
* O conjunto de dados de instantâneo de perfil diário, que é uma exportação diária dos dados de atributo de perfil unificado, pode ser aproveitado para treinar modelos em dados de atributo de perfil. A documentação do conjunto de dados de instantâneo de perfil pode ser acessada [aqui](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=pt-BR#profile-attribute-datasets).

## Documentação relacionada

* [Adobe [!DNL Experience Platform] Descrição do produto de inteligência](https://helpx.adobe.com/br/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Adobe [!DNL Experience Platform] Serviço de consulta](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=pt-BR)

## Publicações do blog relacionadas

* [IA de conteúdo e comércio: A personalização de suas interações com clientes por meio da inteligência de conteúdo](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [Uma Introdução à Análise de Dados Exploratórios no Adobe [!DNL Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [Caminho direto para os produtos da Adobe Experience: aprendizado de máquina para experiência do usuário elevada](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [Segmentation.AI: Automated Audience-Clustering-as-a-Service no Adobe [!DNL Experience Platform]](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)