---
title: Blueprint de Ciência de dados personalizada para enriquecimento de perfis
description: Saiba como os insights baseados em ciência de dados podem ser assimilados na [!DNL Experience Platform] para enriquecer o Perfil do cliente em tempo real.
solution: Data Collection
kt: 7203
exl-id: e5ec6886-4fa4-4c9b-a2d8-e843d7758669,f0efaf3c-6c4f-47c3-ab8a-e8e146dd071c
source-git-commit: 7f3bc307f74aa88a7a73f3e50cc48bd16f58b37f
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 69%

---

# Ciência de dados personalizada para blueprint de enriquecimento de perfil

O blueprint de ciência de dados personalizada para enriquecimento de perfil ilustra como os dados podem ser usados para treinar, implantar e pontuar modelos a fim de fornecer insights de aprendizado de máquina no [!DNL Experience Platform] e a variável [!DNL Real-Time Customer Data Platform] da ciência de dados e das ferramentas de aprendizado de máquina.

Os insights modelados podem ser assimilados em [!DNL Experience Platform] para enriquecer o perfil do cliente em tempo real. Exemplos de insights de aprendizado de máquina incluem pontuação de valor vitalício, afinidade de categorias e produtos, propensão à conversão ou ao churn.

## Casos de uso

* Extraia insights e descubra padrões a partir de dados do cliente; treine e pontue modelos de acordo com esses dados.
* Aprimore o [!UICONTROL Perfil de cliente em tempo real] com insights e atributos orientados por modelos para uma personalização mais detalhada e jornadas aperfeiçoadas.
* Treine e classifique modelos para determinar insights do cliente, como valor vitalício do cliente, propensão à conversão ou à rotatividade, afinidade de conteúdos e produtos e classificação de engajamentos.

## Arquitetura

<img src="assets/data_science.svg" alt="Blueprint de arquitetura de referência para Ciência de dados personalizada para enriquecimento de perfis" style="width:90%; border:1px solid #4a4a4a" />

## Medidas de proteção

* Para obter medidas de proteção detalhadas e latências completas na assimilação de resultados de ciência de dados em [!DNL Experience Platform] e o Perfil do cliente em tempo real referem-se às medidas de proteção de assimilação de dados e ao diagrama de latência referenciado no [documento de medidas de proteção para implantação](../experience-platform/deployment/guardrails.md).

## Etapas de implantação

1. [Crie esquemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=pt-BR) para que os dados sejam assimilados.
1. [Crie conjuntos de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) para que os dados sejam assimilados.
1. [Assimilar dados](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) em [!DNL Experience Platform].

Para que os resultados do modelo sejam assimilados no Perfil do cliente em tempo real, faça o seguinte antes da assimilar dados:

1. [Configure as identidades corretas e os namespaces de identidade](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR) no esquema para assegurar que os dados assimilados possam aderir a um perfil unificado.
1. [Habilite os esquemas e conjuntos de dados para o perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=pt-BR).

## Considerações de implantação

* Na maioria dos casos, o resultado do modelo deve ser assimilado como atributos de perfil, e não como eventos de experiência. Os resultados do modelo podem ser uma cadeia de caracteres de atributo simples. Se houver vários resultados de modelo a assimilar, é recomendável usar um campo de tipo matriz ou mapa.
* O conjunto de dados de instantâneo de perfil diário, que é uma exportação diária dos dados de atributo de perfil unificado, pode ser aproveitado para treinar modelos em dados de atributo de perfil. A documentação do conjunto de dados de instantâneo de perfil pode ser acessada [aqui](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=pt-BR#profile-attribute-datasets).
* Para extrair dados de [!DNL Experience Platform] os métodos a seguir podem ser usados
   * SDK de acesso a dados
      * Os dados estão na forma de arquivo bruto
      * Os dados do evento de experiência de perfil permanecem em seu estado bruto e não unificado.
   * Destinos da RTCDP
      * É possível fazer a saída de atributos de perfil e associações de segmento.

## Documentação relacionada

* [Adobe [!DNL Experience Platform] Descrição do produto de inteligência](https://helpx.adobe.com/br/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Adobe [!DNL Experience Platform] Serviço de consulta](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=pt-BR)

## Publicações do blog relacionadas

* [IA de conteúdo e comércio: A personalização de suas interações com clientes por meio da inteligência de conteúdo](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [Introdução à análise exploratória de dados no Adobe [!DNL Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [Caminho direto para os produtos da Adobe Experience: aprendizado de máquina para experiência do usuário elevada](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [Segmentação.AI: Geração de cluster de público-alvo automatizado-como-um-serviço no Adobe [!DNL Experience Platform]](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)