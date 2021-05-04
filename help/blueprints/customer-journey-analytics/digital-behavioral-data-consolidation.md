---
title: Análise de Jornada entre canais
description: Analise e extraia insights de interações em toda a jornada do cliente.
solution: Experience Platform, Customer Journey Analytics, Data Collection
kt: 7208
exl-id: b042909c-d323-40d5-8b35-f3e5e3e26694
translation-type: tm+mt
source-git-commit: 58368eb06b9bbd6c332424bdcfa2789dde7d4c2f
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 98%

---

# Blueprint de análise de Jornada entre canais

Tenha uma visualização consolidada única do comportamento do cliente em vários canais ao unificar dados de várias propriedades da web, móveis e offline.

## Casos de uso

* Análise de interações com o cliente em desktops e dispositivos móveis para compreender o comportamento do cliente e extrair insights, aprimorando assim as experiências digitais do cliente.
* Análise de interações com o cliente em todos os canais,incluindo canais digitais e offline, como interações de suporte e compras na loja. Isso gera um melhor entendimento e aprimora a jornada do cliente. 

## Aplicativos

* Adobe Experience Platform
* Customer Journey Analytics
* Adobe Analytics (opcional)

## Padrões de integração

* Adobe Experience Platform → Customer Journey Analytics
* Adobe Analytics → Adobe Experience Platform → Customer Journey Analytics

## Arquitetura

<img src="assets/CJA.svg" alt="Blueprint de arquitetura de referência para o Customer Journey Analytics" style="border:1px solid #4a4a4a" />

## Etapas de implementação

1. Configure conjuntos de dados e esquemas.
1. Assimile os dados na Platform.
Os dados devem ser assimilados na Platform antes de processá-los no Customer Journey Analytics.
1. Analise em união conjuntos de dados de eventos entre canais para garantir que eles tenham uma ID de namespace comum ou sejam rechaveados por meio da funcionalidade de adesão com base nos campos do Customer Journey Analytics. 

   >[!NOTE]
   >
   >Atualmente, o Customer Journey Analytics não usa o perfil da Experience Platform ou serviços de identidade para adesão.

1. Execute a preparação de quaisquer dados personalizados ou use a adesão de identidades com base nos campos para garantir uma chave comum nos conjuntos de dados de série temporal a serem assimilados no Customer Journey Analytics.
1. Conceda aos dados de pesquisa uma ID primária que possa se unir a um campo nos dados de eventos. Conta como linhas no licenciamento.
1. Configure a mesma ID primária para dados de perfil como a ID primária dos dados do evento.
1. Configure uma conexão de dados para assimilar dados da Experience Platform no Customer Journey Analytics. Após a aterrissagem dos dados no data lake, eles são processados no Customer Journey Analytics dentro de 90 minutos.
1. Configure uma visualização de dados na conexão para selecionar dimensões e métricas específicas a serem incluídas na visualização. As configurações de atribuição e alocação também são configuradas na visualização de dados. Essas configurações são computadas na hora de criar o relatório.
1. Crie um projeto para configurar painéis e relatórios dentro do Analysis Workspace.

## Considerações de implementação

### Considerações sobre a adesão de identidades

* Dados de séries temporais a serem unificados devem ter o mesmo namespace de ID em cada registro.
* O processo de unificar conjuntos de dados discrepantes exige uma chave primária comum de pessoa/entidade nos conjuntos de dados.
* Atualmente, unificações secundárias com base nas chaves não são suportadas.
* O processo de adesão de identidades com base nos campos permite rechavear identidades em linhas de acordo com registros de ID temporários subsequentes, como uma ID de autenticação. Esse processo permite a solução de registros discrepantes para uma única ID para análise no nível de pessoa, em vez de no nível de dispositivo ou cookie.
* A compilação acontece uma vez por semana, com uma repetição após a adesão.

## FAQs

* Quais são os impactos descendentes de modelos de dados no Customer Journey Analytics?

   Objetos e atributos do mesmo campo XDM mesclam-se em uma dimensão no Customer Journey Analytics. Para mesclar vários atributos de vários conjuntos de dados na mesma dimensão do Customer Journey Analytics, os conjuntos de dados devem fazer referência ao mesmo campo ou esquema XDM.

## Documentos relacionados

* [Descrição do produto Customer Journey Analytics](https://helpx.adobe.com/br/legal/product-descriptions/customer-journey-analytics.html)
* [Documentação do Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics.html?lang=pt-BR)
* [Tutoriais do Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html?lang=pt-BR)
