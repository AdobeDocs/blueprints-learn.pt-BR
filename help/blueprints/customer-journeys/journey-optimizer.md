---
title: Journey Optimizer – Blueprint de mensagens acionadas e da Adobe Experience Platform
description: Execute mensagens e experiências acionadas usando a Adobe Experience Platform como um hub central para dados de transmissão, perfis de clientes e segmentação.
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: f323d2deee5547abd0ccc8247a23ac7a144b2f07
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 100%

---

# Journey Optimizer

O Adobe Journey Optimizer é um sistema criado para as equipes de marketing reagirem em tempo real aos comportamentos dos clientes e atendê-los onde quer que eles estejam. Os recursos de gerenciamento de dados foram transferidos para a Adobe Experience Platform, permitindo que as equipes de marketing se concentrem no que fazem de melhor: criar jornadas de clientes de alto nível e conversas personalizadas.  Este blueprint descreve os recursos técnicos do aplicativo e fornece detalhes sobre os diferentes componentes de arquitetura que compõem o Adobe Journey Optimizer.

## Casos de uso

* Mensagens acionadas
* Confirmações de registro
* Carrinho de compras e abandonos de formulários de aplicação
* Mensagens acionadas de localização

## Arquitetura

<img src="assets/journey-optimizer.png" alt="Arquitetura de referência para o blueprint de mensagens acionadas e Adobe Experience Platform" style="width:80%; border:1px solid #4a4a4a" />

## Padrões de integração

* Adobe Experience Platform -> Journey Optimizer

## Pré-requisitos

1. O cliente deve ser provisionado para a Experience Cloud com uma Organização IMS válida
1. Push para publicação de conteúdo para dispositivos móveis

* O cliente deve ter um desenvolvedor de publicações de conteúdo para dispositivos móveis disponível para criar o aplicativo
* SDK móvel da Adobe Experience Platform
* Coleção de dados
   * Propriedade de tags de dispositivo móvel
      * Extensões:
         * Extensão do Adobe Journey Optimizer
         * Rede de borda da Adobe Experience Platform
         * Identidade
         * Mobile Core
         * Perfil
   * Configurações do aplicativo
   * Fluxos de dados
      * Habilitado para a Experience Platform
      * Conjunto de dados de eventos – usado para coletar o comportamento móvel geral
      * Conjunto de dados de perfil – conjunto de dados do perfil de push do AJO (não pode ser diferente)

## Medidas de proteção

* Consulte o link para obter mais detalhes sobre as medidas de proteção para o Journey Optimizer [LINK](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=pt-BR)
* Segmentos em lote – precisam assegurar que você entenda o volume diário de usuários qualificados e que o sistema de destino possa lidar com a taxa de transferência intermitente por jornada e em todas as jornadas
* Segmentos por streaming – precisam assegurar que a intermitência inicial de qualificações de perfis possam ser manipuladas com o volume de qualificações de streaming diárias por jornada e em todas as jornadas
* Atividade de atualização de perfil – o Perfil do cliente em tempo real pode ser atualizado nativamente a partir de uma jornada.  Há um atraso de até 1 minuto no processamento da atualização na loja de perfis
* Eventos de negócios – uma jornada baseada em segmento de leitura pode ser acionada para iniciar com base em uma chamada externa para o sistema JO
* Oferece suporte nativo ao Offer Decisioning somente em mensagens. Suporte futuro por meio de ação nativa
* Canais compatíveis:
   * Email
   * Push (FCM/APNS)
   * Endpoints de API Rest
* Processa 5 mil eventos por segundo com dimensionamento horizontal (a limitação é a carteira)
* O teste A/B é executado usando dois deliveries, e os resultados são determinados usando QS ou CJA
* Integração com o Litmus – é preciso ter uma conta Litmus para usar a integração

## Etapas de implementação

### Adobe Experience Platform

#### Esquemas/Conjuntos de dados

1. [Configure perfil individual, evento de experiência e esquemas de várias entidades](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) na Experience Platform com base nos dados fornecidos pelo cliente.
1. Crie esquemas do Adobe Campaign para broadLog, trackingLog, endereços sem entrega e preferências de perfil (opcional).
1. [Crie conjuntos de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) na Experience Platform para que os dados sejam assimilados.
1. [Adicione rótulos de uso de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=pt-BR) na Experience Platform para o conjunto de dados para governança.
1. [Crie políticas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=pt-BR) que apliquem governança nos destinos.

#### Perfil/Identidade

1. [Crie qualquer namespace específico para clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR).
1. [Adicione identidades a esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Habilite os esquemas e conjuntos de dados para o Perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=pt-BR).
1. [Configure políticas de mesclagem](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=pt-BR) para visualizações diferentes do [!UICONTROL Perfil de cliente em tempo real] (opcional).
1. Crie segmentos para o uso do Campaign.

#### Origens/Destinos

1. [Assimile dados na Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) usando APIs de streaming e conectores de origem.1. Configure o destino de armazenamento do [!DNL Azure] blob para usar com o Adobe Campaign.

#### Implantação de aplicativo para dispositivos móveis

1. Implemente o SDK do Adobe Campaign para o Adobe Campaign Classic ou o SDK da Experience Platform para o Adobe Campaign Standard. Se o Experience Platform Launch estiver presente, recomenda-se usar a extensão do Adobe Campaign Classic ou o Adobe Campaign Standard com o SDK da Experience Platform.


### Journey Orchestration

1. Dados de streaming usados para inicializar uma jornada do cliente devem estar configurados primeiro dentro do Journey Optimizer para obter uma ID de orquestração. Depois, essa ID de orquestração será fornecida ao desenvolvedor para usá-la na assimilação.
1. Configure as origens de dados externos.
1. Configure as ações personalizadas.

## Documentação relacionada

* [Documentação da Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Documentação do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR)
* [Documentação do Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html?lang=pt-BR)
* [Documentação do SDK móvel da Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
