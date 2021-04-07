---
title: Blueprint de Análise de Deflexão de Chamadas
description: Analise o comportamento do cliente antes que ele entre em contato com a central de atendimento.
solution: Experience Platform, Customer Journey Analytics
kt: 7209
exl-id: 13593c1c-4c58-4b8a-aa6c-7530fd679a14
translation-type: tm+mt
source-git-commit: 844fff1cefe367575beb5c03aa0f0d026eb9f39b
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# Blueprint de Análise de Jornada de Detecção de Chamadas

Analise o comportamento de um cliente em computadores e dispositivos móveis antes de ele entrar em contato com a central de atendimento. Identifique oportunidades para melhorar a jornada do cliente, entendendo quais ações seus clientes tentam concluir, que conteúdo visualizam e quais termos pesquisam antes de entrar em contato com o suporte ao cliente. Determine o conteúdo e as ferramentas de autoatendimento que podem ser aprimorados para ajudar seus clientes a resolver problemas sem precisar entrar em contato com o .

## Casos de uso

* Analise o comportamento do cliente antes que os clientes entrem em contato com o suporte
* Descubra oportunidades para melhorar os recursos de autoatendimento

## Aplicativos

* Adobe Experience Platform
* Customer Journey Analytics

## Padrões de integração

* Adobe Experience Platform → Customer Journey Analytics

## Arquitetura

<img src="assets/CJA.svg" alt="Arquitetura de referência para o Customer Journey Analytics Blueprint" style="border:1px solid #4a4a4a" />

## Medidas de proteção

Assimilação de dados no Customer Journey Analytics:

* Assimilação de dados ao lago: API ~ 7 GB/hora, conector de origem ~ 200 GB/hora, streaming para lago ~ 15 minutos, conector de origem do Analytics para lago ~ 45 minutos.
* Depois que os dados são publicados no lago de dados, pode levar até 90 minutos para serem processados no Customer Journey Analytics.

## Etapas da implementação

1. Configurar conjuntos de dados e esquemas.
1. Assimilar dados na plataforma.
Os dados devem ser assimilados na Platform antes da assimilação no Customer Journey Analytics.
1. Analise conjuntos de dados de eventos entre canais.
Os conjuntos de dados analisados na união devem ter uma ID de namespace comum ou ser rechaveados por meio do recurso de compilação em campo do Customer Journey Analytics. 

   >[!NOTE]
   >
   >No momento, o Customer Journey Analytics não usa o Perfil do Experience Platform ou os serviços de identidade para compilar.

1. Execute qualquer preparação de dados personalizada ou uso da identificação baseada em campo que une os dados, para garantir que uma chave comum entre conjuntos de dados de séries de tempo seja assimilada no Customer Journey Analytics.
1. Forneça uma ID primária para dados de pesquisa, que podem se associar a um campo nos dados do evento. Conta como linhas no licenciamento.
1. Defina a mesma ID primária nos dados do perfil da ID primária dos dados do evento.
1. Configure uma conexão de dados para assimilar dados de Experience Platform para Customer Journey Analytics. Depois que os dados chegam ao lago de dados, ele se processa em Customer Journey Analytics em 90 minutos.
1. Configure uma visualização de dados na conexão para selecionar as dimensões e métricas específicas a serem incluídas na visualização. As configurações de atribuição e alocação também são definidas na visualização de dados. Essas configurações são calculadas no momento do relatório.
1. Crie um projeto para configurar painéis e relatórios no Analysis Workspace.

## Considerações sobre a implementação

### Considerações sobre a configuração de identidade

* Os dados da série de tempo a serem unificados devem ter o mesmo namespace de id em cada registro. Para conectar os dados da central de atendimento aos dados anônimos do dispositivo, a ID digital deve ser vinculada à ID de chamada. Essa vinculação pode ocorrer por meio de vários mecanismos possíveis:
   * O número de discagem é um número de discagem exclusivo para esse visitante naquela hora, juntamente com uma tabela de pesquisa para rastrear a relação.
   * Exigir que o usuário se autentique antes de solicitar suporte e vincular essa autenticação a um identificador determinado pelo agente de chamada (por exemplo, número de telefone ou email).
   * Use um parceiro de integração para ajudar a digitar identificadores de dispositivos online com identificadores conhecidos vinculados à solicitação de suporte.
* O processo de união de conjuntos de dados diferentes requer uma chave de pessoa/entidade primária comum em todos os conjuntos de dados.
* Atualmente, não há suporte para uniões baseadas em chave secundárias.
* O processo de identificação baseado em campo permite a criação de novas identidades em linhas com base em registros de ID transitórios subsequentes, como uma ID de autenticação. Esse processo permite resolver registros diferentes para uma única ID para análise no nível da pessoa, em vez de no nível do dispositivo ou do cookie.
* A costura ocorre uma vez por semana, com reprodução após a costura.

## Perguntas frequentes

* Quais são os impactos downstream de modelos de dados no Customer Journey Analytics?

   Objetos e atributos do mesmo campo XDM se mesclam em uma dimensão no Customer Journey Analytics. Para mesclar vários atributos de vários conjuntos de dados na mesma dimensão do CJA, os conjuntos de dados devem fazer referência ao mesmo campo ou esquema XDM.

## Documentação relacionada

* [Descrição do produto Customer Journey Analytics](https://helpx.adobe.com/legal/product-descriptions/customer-journey-analytics.html)
* [Documentação do Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics.html)
* [Tutoriais do Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html)
