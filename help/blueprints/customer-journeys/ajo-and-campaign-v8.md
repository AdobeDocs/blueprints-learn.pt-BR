---
title: Blueprint do Journey Optimizer com Adobe Campaign v8
description: Demonstra como o Adobe Journey Optimizer pode ser usado com o Adobe Campaign para enviar mensagens utilizando o servidor de mensagens em tempo real no Campaign de forma nativa
solution: Journey Optimizer, Campaign, Campaign v8 Client Console
exl-id: 447a1b60-f217-4295-a0df-32292c4742b0
source-git-commit: 60a7785ea0ec4ee83fd9a1e843f0b84fc4cb1150
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 64%

---

# Blueprint do Journey Optimizer com Adobe Campaign v8

Demonstra como Adobe [!DNL Journey Optimizer] pode ser usado com o Adobe [!DNL Campaign] para enviar mensagens nativamente utilizando o servidor de mensagens em tempo real no [!DNL Campaign].

## Arquitetura

<img src="assets/ajo-campaign-architecture.svg" alt="Blueprint do Journey Optimizer com arquitetura de referência" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

>[!IMPORTANT]
>É possível usar o Journey Optimizer e o Campaign independentes um do outro para enviar mensagens, mas algumas considerações técnicas precisam ser ponderadas. Se quiser seguir esse roteiro, trabalhe com seu arquiteto empresarial de pré-vendas para garantir que você tenha conhecimento do que será necessário para comportar implementação.

## Pré-requisitos

Revise os seguintes pré-requisitos para cada aplicativo.

### Adobe Experience Platform  

* Os esquemas e conjuntos de dados devem ser configurados no sistema antes que você possa configurar as fontes de dados do Journey Optimizer
* Para esquemas do Experience Event baseados em classe, adicione o grupo de campos “eventID de orquestração” quando quiser acionar um evento que não seja baseado em regras
* Para esquemas de Perfil individual baseados em classe, adicione o grupo de campos “Detalhes do teste de perfil” para carregar perfis de teste a serem usados com o Journey Optimizer
* O Journey Optimizer e o Campaign são provisionados na mesma organização IMS

### Campaign v8

* A instância de execução do serviço de mensagens em tempo real (ou seja, o Centro de Mensagens) deve ser hospedada por Adobe Managed Cloud Services
* Toda a criação de mensagens é feita dentro da própria instância do Campaign

## Medidas de proteção

* [Limitações do produto Journey Optimizer Guardrails](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=pt-BR)

* [Medidas de proteção e orientação completa de latência](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

## Etapas de implementação

Siga as implementações de cada aplicativo descrito abaixo.

### Adobe Experience Platform

#### Esquema/Conjuntos de dados

1. [Configure perfil individual, evento de experiência e esquemas de várias entidades](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=pt-BR) na Experience Platform com base nos dados fornecidos pelo cliente.
1. (Opcional) Crie esquemas baseados em classe de Evento de experiência para as tabelas broadLog, trackingLog e endereços não entregues do Adobe Campaign.
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

1. [Assimilar dados em [!DNL Experience Platform]](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) uso de APIs de transmissão e conectores de origem.

### Journey Optimizer  

1. Configurar o [!DNL Experience Platform] fonte de dados e determinar quais campos devem ser armazenados em cache como parte do perfilOs dados de transmissão usados para iniciar uma jornada do cliente devem ser configurados no Journey Optimizer primeiro para obter uma ID de orquestração. Depois, essa ID de orquestração será fornecida ao desenvolvedor para usá-la na assimilação.
1. Configure as origens de dados externos.
1. Configure ações personalizadas para a instância do Campaign.

### Campaign v8

* Os templates de mensagens precisam ser configurados com o contexto de personalização apropriado.
* Para [!DNL Campaign] standard: os workflows de exportação precisam ser configurados para exportar os logs de mensagens transacionais de volta para o Experience Platform. A recomendação é executar no máximo a cada quatro horas.
* Para [!DNL Campaign] v8.4 é possível aproveitar o Adobe [!DNL Campaign] Conector de origem do Managed Services no Experience Platform para sincronizar eventos de entrega e rastreamento do Campaign para o Experience Platform. Consulte a [Conector de origem](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=pt-BR) para obter mais detalhes.

### Configuração de push para publicação de conteúdo para dispositivos móveis (opcional)

1. Implementar [!DNL Experience Platform] SDK móvel para coletar tokens de push e informações de logon para vincular a perfis de clientes conhecidos.
1. Aproveite as tags da Adobe e crie uma propriedade de publicação de conteúdo para dispositivos móveis com a seguinte extensão:
   * Adobe [!DNL Journey Optimizer] | Adobe [!DNL Campaign Classic] | Adobe [!DNL Campaign Standard]
   * Adobe [!DNL Experience Platform] [!DNL Edge Network]
   * Identidade de [!DNL Edge Network]
   * Mobile Core
1. Certifique-se de ter uma sequência de dados dedicada a implantações de aplicativos móveis em comparação a implantações da Web.
1. Para obter mais informações, siga as [Guia do Adobe Journey Optimizer Mobile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer).

   >[!IMPORTANT]
   >Pode haver a necessidade de coletar tokens móveis tanto no Journey Optimizer como no Campaign, caso se deseje enviar comunicações em tempo real por meio do Journey Optimizer e notificações por push em lote pelo Campaign. O Campaign v8 exige o uso exclusivo do SDK do Campaign na captura de tokens de push.

## Documentação relacionada

* [Documentação do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR)
* [Descrição do produto do Journey Optimizer](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html)
* [Documentação do Campaign v8](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=pt-BR)
