---
title: Cenário de consolidação de dados de comportamento digital
description: Analise e extraia insights das interações do cliente na jornada do cliente.
solution: Experience Platform, Customer Journey Analytics, Data Collection
kt: 7208
translation-type: tm+mt
source-git-commit: e1a9881996a181310bdc32cb083e4c5654139bf0
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---


# Cenário de consolidação de dados de comportamento digital

Tenha uma única visualização consolidada do comportamento do cliente em vários canais, unificando dados de várias propriedades da Web, móveis e offline.

## Casos de uso

* Analise as interações do cliente em computadores e dispositivos móveis para entender o comportamento do cliente e extrair insights para otimizar as experiências do cliente digital.
* Analise as interações do cliente em todos os canais, incluindo canais digitais e offline, como interações de suporte e compras na loja para entender melhor e otimizar a jornada do cliente. 

## Aplicativos

* Adobe Experience Platform
* Customer Journey Analytics
* Adobe Analytics (opcional)

## Padrões de integração

* Adobe Experience Platform → Customer Journey Analytics
* Adobe Analytics → Adobe Experience Platform → Customer Journey Analytics

## Arquitetura

<img src="assets/CJA.svg" alt="Arquitetura de referência para o Customer Journey Analytics Blueprint" style="border:1px solid #4a4a4a" />

## Medidas de proteção

Assimilação de dados no Customer Journey Analytics:

* Assimilação de dados ao lago: API ~ 7 GB/hora, conector de origem ~ 200 GB/hora, streaming para lago ~ 15 minutos, conector de origem Adobe Analytics para lago ~ 45 minutos.
* Depois que os dados são publicados no lago de dados, pode levar até 90 minutos para serem processados no Customer Journey Analytics.

## Etapas da implementação

1. Configurar conjuntos de dados e esquemas.
1. Assimilar dados na plataforma.
Os dados devem ser assimilados na Platform antes do processamento no Customer Journey Analytics.
1. Analise os conjuntos de dados de eventos entre canais que serão analisados na união para garantir que eles tenham uma ID de namespace comum ou sejam rechaveados por meio do recurso de compilação em campo do Customer Journey Analytics. 

   >[!NOTE]
   >
   >No momento, o Customer Journey Analytics não usa o Perfil do Experience Platform ou os serviços de identidade para compilar.

1. Execute qualquer preparação de dados personalizada ou uso da identificação baseada em campo nos dados para garantir uma chave comum em conjuntos de dados de séries de tempo que serão assimilados no Customer Journey Analytics.
1. Forneça aos dados de pesquisa uma ID primária que possa se associar a um campo nos dados do evento. Conta como linhas no licenciamento.
1. Defina a mesma ID primária para os dados do perfil que a ID primária dos dados do evento.
1. Configure uma conexão de dados para assimilar dados de Experience Platform para Customer Journey Analytics. Depois que os dados chegam ao lago de dados, ele se processa em Customer Journey Analytics em 90 minutos.
1. Configure uma visualização de dados na conexão para selecionar as dimensões e métricas específicas a serem incluídas na visualização. As configurações de atribuição e alocação também são definidas na visualização de dados. Essas configurações são calculadas no momento do relatório.
1. Crie um projeto para configurar painéis e relatórios no Analysis Workspace.

## Considerações sobre a implementação

### Considerações sobre a configuração de identidade

* Os dados da série de tempo a serem unificados devem ter o mesmo namespace de ID em cada registro.
* O processo de união de conjuntos de dados diferentes requer uma chave de pessoa/entidade primária comum em todos os conjuntos de dados.
* Atualmente, não há suporte para uniões baseadas em chave secundárias.
* O processo de identificação baseado em campo permite a criação de novas identidades em linhas com base em registros de ID transitórios subsequentes, como uma ID de autenticação. Isso permite resolver registros diferentes para uma única ID para análise no nível da pessoa, em vez de no nível do dispositivo ou do cookie.
* A costura ocorre uma vez por semana, com reprodução após a costura.

## Perguntas frequentes

* Quais são os impactos downstream de modelos de dados no Customer Journey Analytics?

   Objetos e atributos do mesmo campo XDM se mesclam em uma dimensão no Customer Journey Analytics. Para  mesclar vários atributos de vários conjuntos de dados na mesma dimensão do Customer Journey Analytics, os conjuntos de dados devem fazer referência ao mesmo campo ou esquema XDM.

## Documentação relacionada

* [Descrição do produto Customer Journey Analytics](https://helpx.adobe.com/legal/product-descriptions/customer-journey-analytics.html)
* [Documentação do Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics.html)
* [Tutoriais do Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html)




