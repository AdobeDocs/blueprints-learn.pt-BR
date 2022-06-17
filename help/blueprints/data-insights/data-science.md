---
title: Blueprint de ciência de dados personalizada para aprimoramento de perfis
description: Este blueprint apresenta como o Data Science Workspace, da Adobe Experience Platform, pode usar os dados contidos na Experience Platform para treinar, implantar e classificar modelos a fim de fornecer insights de aprendizado de máquina a partir dos dados.
solution: Data Collection
kt: 7203
exl-id: e5ec6886-4fa4-4c9b-a2d8-e843d7758669,f0efaf3c-6c4f-47c3-ab8a-e8e146dd071c
source-git-commit: 56ed25f8ed954126c3291559b7f67f04565c01d4
workflow-type: ht
source-wordcount: '505'
ht-degree: 100%

---

# Blueprint de ciência de dados personalizada para aprimoramento de perfis

O Blueprint de ciência de dados personalizada para aprimoramento de perfis ilustra como os dados na Adobe Experience Platform podem ser usados para treinar, implantar e pontuar modelos para fornecer insights de aprendizado de máquina para a Experience Platform e a Real-time Customer Data Platform a partir de ferramentas de aprendizado de máquina e ciência de dados. É possível assimilar insights modelados na Experience Platform para enriquecer o perfil do cliente em tempo real. Exemplos de insights de aprendizado de máquina incluem pontuação de valor vitalício, afinidade de categorias e produtos, propensão à conversão ou à rotatividade.

## Casos de uso

* Extraia insights e descubra padrões a partir de dados do cliente; treine e pontue modelos de acordo com esses dados.
* Aprimore o [!UICONTROL Perfil de cliente em tempo real] com insights e atributos orientados por modelos para uma personalização mais detalhada e jornadas aperfeiçoadas.
* Treine e classifique modelos para determinar insights do cliente, como valor vitalício do cliente, propensão à conversão ou à rotatividade, afinidade de conteúdos e produtos e classificação de engajamentos.

## Arquitetura

<img src="assets/data_science.svg" alt="Blueprint de arquitetura de referência para Ciência de dados personalizada para aprimoramento de perfis" style="width:90%; border:1px solid #4a4a4a" />

## Etapas de implementação

1. [Crie esquemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) para que os dados sejam assimilados.
1. [Crie conjuntos de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) para que os dados sejam assimilados.
1. [Assimile dados](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) na Experience Platform.

Para que os resultados do modelo sejam assimilados no Perfil do cliente em tempo real, faça o seguinte antes da assimilar dados:

1. [Configure as identidades corretas e os namespaces de identidade](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR) no esquema para assegurar que os dados assimilados possam aderir a um perfil unificado.
1. [Habilite os esquemas e conjuntos de dados para o perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=pt-BR).

## Considerações de implementação

* Na maioria dos casos, o resultado do modelo deve ser assimilado como atributos de perfil, e não como eventos de experiência. Os resultados do modelo podem ser uma cadeia de caracteres de atributo simples. Se houver vários resultados de modelo a assimilar, é recomendável usar um campo de tipo matriz ou mapa.
* O conjunto de dados de instantâneo de perfil diário, que é uma exportação diária dos dados de atributo de perfil unificado, pode ser aproveitado para treinar modelos em dados de atributo de perfil. A documentação do conjunto de dados de instantâneo de perfil pode ser acessada [aqui](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=pt-BR#profile-attribute-datasets).
* Para extrair dados da Experience Platform, os seguintes métodos podem ser usados:
   * SDK de acesso a dados
      * Os dados estão na forma de arquivo bruto
      * Os dados do evento de experiência de perfil permanecem em seu estado bruto e não unificado.
   * Destinos da RTCDP
      * Só é possível fazer a saída de atributos de perfil e associações de segmento.
   * Serviço de consulta
      * O acesso a grandes quantidades de dados brutos pode fazer com que o query atinja o tempo limite de 10 minutos. É recomendável consultar dados de forma progressiva.


## Documentação relacionada

* [Descrição do produto Adobe Experience Platform Intelligence](https://helpx.adobe.com/br/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Serviço de consulta da Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=pt-BR)

## Publicações do blog relacionadas

* [[!DNL Content and Commerce AI: Personalizing Your Interactions with Customers Through Content Intelligence]](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [[!DNL An Introductory Look at Exploratory Data Analysis on Adobe Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [[!DNL Cutting Across Adobe Experience Products with Machine Learning to Elevated User Experience]](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [[!DNL Segmentation.AI: Automated Audience-Clustering-as-a-Service in Adobe Experience Platform]](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)