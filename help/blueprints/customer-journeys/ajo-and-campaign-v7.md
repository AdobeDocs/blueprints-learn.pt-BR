---
title: Blueprint do Journey Optimizer com Adobe Campaign v7
description: Demonstra como o Adobe Journey Optimizer pode ser usado com o Adobe Campaign para enviar mensagens utilizando o servidor de mensagens em tempo real no Campaign de forma nativa
solution: Journey Optimizer, Campaign, Campaign Classic v7, Campaign Standard
exl-id: 6d9bc65c-cca0-453f-8106-d2895d005ada
source-git-commit: 7547cdc57e50d63f4a7949c00a77b82c86da831e
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 97%

---

# Blueprint do Journey Optimizer com Adobe Campaign v7

Demonstra como o Adobe Journey Optimizer pode ser usado com o Adobe Campaign para enviar mensagens utilizando o servidor de mensagens em tempo real no Campaign de forma nativa.

<br>

## Arquitetura

<img src="assets/ajo-campaign-architecture.svg" alt="Blueprint do Journey Optimizer com arquitetura de referência" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

>[!IMPORTANT]
>É possível usar o Journey Optimizer e o Campaign independentes um do outro para enviar mensagens, mas algumas considerações técnicas precisam ser ponderadas. Se quiser seguir esse roteiro, trabalhe com seu arquiteto empresarial de pré-vendas para garantir que você tenha conhecimento do que será necessário para comportar implementação.

<br>

## Pré-requisitos

### Adobe Experience Platform

* Os esquemas e conjuntos de dados devem ser configurados no sistema antes que você possa configurar as fontes de dados do Journey Optimizer
* Para esquemas do Experience Event baseados em classe, adicione o grupo de campos “eventID de orquestração” quando quiser acionar um evento que não seja baseado em regras
* Para esquemas de Perfil individual baseados em classe, adicione o grupo de campos “Detalhes do teste de perfil” para carregar perfis de teste a serem usados com o Journey Optimizer
* O Journey Optimizer e o Campaign são provisionados na mesma organização IMS

### Campaign v7

* A instância de execução do serviço de mensagens em tempo real (ou seja, o Centro de Mensagens) deve ser hospedada por Adobe Managed Cloud Services
* Toda a criação de mensagens é feita dentro da própria instância do Campaign

<br>

## Medidas de proteção

[Link do produto de medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/get-started/guardrails)

[Medidas de Proteção e Orientação de Latência de Ponta a Ponta](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=pt-BR)

## Etapas de implementação

### Adobe Experience Platform

#### Esquema/Conjuntos de dados

1. [Configure perfil individual, evento de experiência e esquemas de várias entidades](https://experienceleague.adobe.com/?lang=pt-br&recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=pt-BR) na Experience Platform com base nos dados fornecidos pelo cliente.
1. Crie esquemas baseados em classe do Experience Event para tabelas de broadLog, trackingLog e endereços sem entrega do Adobe Campaign (opcional).
1. [Crie conjuntos de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) na Experience Platform para que os dados sejam assimilados.
1. [Adicione rótulos de uso de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=pt-BR) na Experience Platform para o conjunto de dados para governança.
1. [Crie políticas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=pt-BR) que apliquem governança nos destinos.

#### Perfil/identidade

1. [Crie qualquer namespace específico para clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR).
1. [Adicione identidades a esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR).
1. [Habilite os esquemas e conjuntos de dados para o Perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=pt-BR).
1. [Configure políticas de mesclagem](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=pt-BR) para visualizações diferentes do [!UICONTROL Perfil de cliente em tempo real] (opcional).
1. Crie segmentos para o uso do Journey.

#### Origens/destinos

1. [Assimile dados na Experience Platform](https://experienceleague.adobe.com/?lang=pt-br&recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) usando APIs de transmissão e conectores de origem.

### Journey Optimizer

1. Configure sua fonte de dados da Experience Platform e determine quais campos que devem ser armazenados em cache como parte dos dados de profileStreaming usados para iniciar uma jornada do cliente têm que ser primeiro configurados no Journey Optimizer para obter uma ID de orquestração. Depois, essa ID de orquestração será fornecida ao desenvolvedor para usá-la na assimilação
1. Configure as origens de dados externos
1. Configure ações personalizadas para a instância do Campaign

### Campaign v7

* Os modelos de mensagens precisam ser configurados com o contexto de personalização apropriado
* Para o Campaign v7 – Os fluxos de trabalho de exportação precisam ser configurados para exportar os logs de mensagens transacionais de volta para a Experience Platform. A recomendação é executar no máximo a cada quatro horas.

### Configuração de push para publicação de conteúdo para dispositivos móveis (opcional)

1. Implemente o SDK móvel da Experience Platform para coletar tokens de push e informações de logon a serem vinculadas a perfis de clientes conhecidos
1. Aproveite as tags da Adobe e crie uma propriedade de publicação de conteúdo para dispositivos móveis com a seguinte extensão:
   * Adobe Journey Optimizer | Adobe Campaign Classic | Adobe Campaign Standard
   * Adobe Experience Platform [!DNL Edge Network]
   * Identidade para [!DNL Edge Network]
   * Mobile Core
1. Certifique-se de ter um fluxo de dados dedicado para implantações de aplicativos móveis e implantações da Web
1. Para mais informações, siga o [Manual do Adobe Journey Optimizer Mobile](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer/push-notification/)

   >[!IMPORTANT]
   >Pode haver a necessidade de coletar tokens móveis tanto no Journey Optimizer como no Campaign, caso se deseje enviar comunicações em tempo real por meio do Journey Optimizer e notificações por push em lote pelo Campaign. O Campaign v8 exige o uso exclusivo do SDK do Campaign na captura de tokens de push.

<br>

## Documentação relacionada

* [Documentação do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR)
* [Descrição do produto do Journey Optimizer](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html)
* [Documentação do Campaign v7](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=pt-BR)
