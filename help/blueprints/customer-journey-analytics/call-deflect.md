---
title: Blueprint de Análise de Deflexão de Chamadas
description: Analise o comportamento do cliente antes que ele entre em contato com a central de atendimento.
solution: Experience Platform, Customer Journey Analytics
kt: 7209
exl-id: 13593c1c-4c58-4b8a-aa6c-7530fd679a14
translation-type: tm+mt
source-git-commit: 9fe9d67c5f97b633e45155bd54e2006f1b797332
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 93%

---

# Blueprint de Análise de Jornada de Detecção de Chamadas

Analise o comportamento do cliente no desktop e em publicações de conteúdo para dispositivos móveis antes que ele entre em contato com a central de atendimento. Identifique oportunidades para aprimorar a jornada de seus clientes ao entender que ações eles tentam finalizar, que conteúdo visualizam e que termos eles pesquisam antes de entrarem em contato com o suporte ao cliente. Determine o conteúdo e as ferramentas de autoatendimento que podem ser melhoradas para ajudar seus clientes a solucionarem problemas sem a necessidade de telefonar.

## Casos de uso

* Analise o comportamento do cliente antes que ele entre em contato com o suporte
* Descubra oportunidades de aprimorar funcionalidades de autoatendimento

## Aplicativos

* Adobe Experience Platform
* Customer Journey Analytics

## Padrões de integração

* Adobe Experience Platform → Customer Journey Analytics

## Arquitetura

<img src="assets/CJA.svg" alt="Blueprint de arquitetura de referência para o Customer Journey Analytics" style="border:1px solid #4a4a4a" />

## Etapas de implementação

1. [Crie ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html) esquemas para os dados que serão assimilados.
1. [Crie ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) conjuntos de dados para que os dados sejam assimilados.
1. [Assimile dados na Experience Platform.
](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion)
Os dados devem ser assimilados na Platform antes de assimilá-los no Customer Journey Analytics.
1. Analise conjuntos de dados de eventos entre canais.
Conjuntos de dados analisados juntos devem ter uma ID de namespace comum ou ser rechaveados por meio da funcionalidade de adesão com base nos campos do Customer Journey Analytics. 

   >[!NOTE]
   >
   >Atualmente, o Customer Journey Analytics não usa o perfil da Experience Platform ou serviços de identidade para adesão.

1. Execute a preparação de quaisquer dados personalizados ou use a adesão de identidades com base nos campos, para garantir uma chave comum nos conjuntos de dados de série temporal a serem assimilados no Customer Journey Analytics.
1. Forneça uma ID primária para dados de pesquisa, que pode se unir a um campo nos dados de evento. Conta como linhas no licenciamento.
1. Configure a mesma ID primária nos dados de perfil como ID primária dos dados do evento.
1. Configure uma conexão de dados para assimilar dados da Experience Platform no Customer Journey Analytics. Após a aterrissagem dos dados no data lake, eles são processados no Customer Journey Analytics dentro de 90 minutos.
1. Configure uma visualização de dados na conexão para selecionar dimensões e métricas específicas a serem incluídas na visualização. As configurações de atribuição e alocação também são configuradas na visualização de dados. Essas configurações são computadas na hora de criar o relatório.
1. Crie um projeto para configurar painéis e relatórios dentro do Analysis Workspace.

## Considerações de implementação

### Considerações sobre a adesão de identidades

* Dados de séries temporais a serem unificados devem ter o mesmo namespace de ID em cada registro. Para conectar dados da central de atendimento a dados anônimos de dispositivos, a ID digital deve estar vinculada à ID de chamada. Esse vínculo pode ocorrer por meio de vários mecanismos possíveis:
   * O número de discagem sendo um número de discagem única para o visitante naquele momento, junto a uma tabela de pesquisa para rastrear o relacionamento.
   * Requerer que o usuário autentique antes de solicitar suporte e vincule essa autenticação a um identificador determinado pelo agente de chamada (por exemplo, número de telefone ou email).
   * Uso de um parceiro de integração para ajudar a digitar identificadores de dispositivos online com identificadores conhecidos vinculados à solicitação de suporte.
* O processo de unificar conjuntos de dados discrepantes exige uma chave primária comum de pessoa/entidade nos conjuntos de dados.
* Atualmente, unificações secundárias com base nas chaves não são suportadas.
* O processo de adesão de identidades com base nos campos permite rechavear identidades em linhas de acordo com registros de ID temporários subsequentes, como uma ID de autenticação. Esse processo permite a solução de registros discrepantes para uma única ID para análise no nível de pessoa, em vez de no nível de dispositivo ou cookie.
* A compilação acontece uma vez por semana, com uma repetição após a adesão.

## FAQs

* Quais são os impactos descendentes de modelos de dados no Customer Journey Analytics?

   Objetos e atributos do mesmo campo XDM mesclam-se em uma dimensão no Customer Journey Analytics. Para mesclar vários atributos de vários conjuntos de dados na mesma dimensão do CJA, os conjuntos de dados devem fazer referência ao mesmo campo ou esquema XDM.

## Documentos relacionados

* [Descrição do produto Customer Journey Analytics](https://helpx.adobe.com/br/legal/product-descriptions/customer-journey-analytics.html)
* [Documentação do Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics.html?lang=pt-BR)
* [Tutoriais do Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html?lang=pt-BR)
