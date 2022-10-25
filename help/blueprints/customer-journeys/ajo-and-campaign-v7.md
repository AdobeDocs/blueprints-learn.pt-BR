---
title: Blueprint do Journey Optimizer com Adobe Campaign v7
description: Demonstra como o Adobe Journey Optimizer pode ser usado com o Adobe Campaign para enviar mensagens utilizando o servidor de mensagens em tempo real no Campaign de forma nativa
solution: Journey Optimizer, Campaign, Campaign v8, Campaign Classic v7, Campaign Standard
source-git-commit: 6901596cbb661ffa8cf57c6ae958db1978bf1520
workflow-type: ht
source-wordcount: '1128'
ht-degree: 100%

---

# Journey Optimizer com Adobe Campaign  v7

Demonstra como o Adobe Journey Optimizer pode ser usado com o Adobe Campaign para enviar mensagens utilizando o servidor de mensagens em tempo real no Campaign de forma nativa.

<br>

## Arquitetura

<img src="assets/ajo-campaign-architecture.svg" alt="Blueprint do Journey Optimizer com arquitetura de referência" style="width:100%; border:1px solid #4a4a4a" />

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

[Link do produto medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=pt-BR)

### Medidas de proteção adicionais do Journey Optimizer

* O limite agora está disponível por meio de API para garantir que o sistema de destino não esteja saturado ao ponto de falha. Isso significa que as mensagens que excederem o limite serão completamente removidas sem ser enviadas. A regulagem não é compatível.
   * Conexões máximas – número máximo de conexões http/s com que um destino pode lidar
   * Contagem máxima de chamadas – número máximo de chamadas a serem realizadas no parâmetro periodInMs
   * periodInMs – tempo em milissegundos
* Jornadas iniciadas por associação de segmentos podem operar em dois modos:
   * Segmentos em lote (atualizados a cada 24 horas)
   * Segmentos de transmissão (qualificação de &lt; 5 minutos)
* Segmentos em lote – precisam assegurar que você entenda o volume diário de usuários qualificados e que o sistema de destino possa lidar com a taxa de transferência intermitente por jornada e em todas as jornadas
* Segmentos de transmissão – precisam assegurar que a intermitência inicial de qualificações de perfis possam ser manipuladas com o volume de qualificações de transmissão diárias por jornada e em todas as jornadas
* A gestão de decisões não é compatível
* Eventos de negócios não são compatíveis
* Integrações de saída para sistemas de terceiros
   * Não há suporte para um único IP estático, pois nossa infraestrutura é multilocatária (é necessário incluir todos os IPs do data center na lista de permissões)
   * Somente os métodos POST e PUT são compatíveis com ações personalizadas
   * Suporte de autenticação: token | senha | OAuth2
* Não é possível empacotar e mover componentes individuais da Adobe Experience Platform ou do Journey Optimizer entre várias sandboxes. Em ambientes novos, deve ser implementado outra vez

<br>

### Campaign (v7)

* A instância de execução do Centro de Mensagens deve ser hospedada por Adobe Managed Cloud Services
* Precisa ter build v7 superior a 21.1 ou v8
* Taxa de transferência de mensagens
   * AC (v7) 50 mil por hora
   * AC (v8) até 1 milhão por hora com base no pacote
* AC (v7) é compatível apenas com mensagens de jornadas iniciadas por evento
   * Não é compatível com mensagens de Jornadas iniciadas por segmento ou associação de segmentos
   * Mensagens de jornadas baseadas em eventos de Empresas e de Read audience não são compatíveis, devido ao volume que pode ser enviado para as instâncias de execução
* O AC (v7) e o AC (v8) não são compatíveis com a gestão de decisões nas mensagens
* Não é feita regulagem de chamadas de API de saída feitas para o Campaign
* Com o Campaign v8.4, é possível aproveitar o Adobe Campaign Managed Services Source Connector na Experience Platform para sincronizar eventos de rastreamento e de entrega do Campaign na Experience Platform. Para mais detalhes, consulte a Documentação do Source Connector. [Link](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=pt-BR)

<br>

## Etapas de implementação

### Adobe Experience Platform

#### Esquemas/Conjuntos de dados

1. [Configure perfil individual, evento de experiência e esquemas de várias entidades](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) na Experience Platform com base nos dados fornecidos pelo cliente.
1. Crie esquemas baseados em classe do Experience Event para tabelas de broadLog, trackingLog e endereços sem entrega do Adobe Campaign (opcional).
1. [Crie conjuntos de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) na Experience Platform para que os dados sejam assimilados.
1. [Adicione rótulos de uso de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=pt-BR) na Experience Platform para o conjunto de dados para governança.
1. [Crie políticas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=pt-BR) que apliquem governança nos destinos.

#### Perfil/Identidade

1. [Crie qualquer namespace específico para clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR).
1. [Adicione identidades a esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR).
1. [Habilite os esquemas e conjuntos de dados para o Perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=pt-BR).
1. [Configure políticas de mesclagem](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=pt-BR) para visualizações diferentes do [!UICONTROL Perfil de cliente em tempo real] (opcional).
1. Crie segmentos para o uso do Journey.

#### Origens/Destinos

1. [Assimile dados na Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) usando APIs de transmissão e conectores de origem.

### Journey Optimizer

1. Configure sua fonte de dados da Experience Platform e determine quais campos que devem ser armazenados em cache como parte dos dados de profileStreaming usados para iniciar uma jornada do cliente têm que ser primeiro configurados no Journey Optimizer para obter uma ID de orquestração. Depois, essa ID de orquestração será fornecida ao desenvolvedor para usá-la na assimilação
1. Configure as origens de dados externos
1. Configure ações personalizadas para a instância do Campaign

### Campaign v7

* Os modelos de mensagens precisam ser configurados com o contexto de personalização apropriado
* Para o Campaign Standard – Os fluxos de trabalho de exportação precisam ser configurados para exportar os logs de mensagens transacionais de volta para a Experience Platform. A recomendação é executar no máximo a cada quatro horas.
* Para o Campaign v8.4, é possível aproveitar o Adobe Campaign Managed Services Source Connector na Experience Platform para sincronizar eventos de rastreamento e de entrega do Campaign na Experience Platform. Para mais detalhes, consulte a Documentação do Source Connector. [Link](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=pt-BR)

### Configuração de push para publicação de conteúdo para dispositivos móveis (opcional)

1. Implemente o SDK móvel da Experience Platform para coletar tokens de push e informações de logon a serem vinculadas a perfis de clientes conhecidos
1. Aproveite as tags da Adobe e crie uma propriedade de publicação de conteúdo para dispositivos móveis com a seguinte extensão:
   * Adobe Journey Optimizer | Adobe Campaign Classic | Adobe Campaign Standard
   * Rede de borda da Adobe Experience Platform
   * Identidade  para Edge Network
   * Mobile Core
1. Certifique-se de ter um fluxo de dados dedicado para implantações de aplicativos móveis e implantações da Web
1. Para mais informações, siga o [Manual do Adobe Journey Optimizer Mobile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)

   >[!IMPORTANT]
   >Pode haver a necessidade de coletar tokens móveis tanto no Journey Optimizer como no Campaign, caso se deseje enviar comunicações em tempo real por meio do Journey Optimizer e notificações por push em lote pelo Campaign. O Campaign v8 exige o uso exclusivo do SDK do Campaign na captura de tokens de push.

<br>

## Documentação relacionada

* [Documentação da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Documentação de tags da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)
* [Documentação do SDK móvel da Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
* [Documentação do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR)
* [Descrição do produto do Journey Optimizer](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html)
* [Documentação do Campaign v8](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=pt-BR)
* [Documentação do Campaign v7](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=pt-BR)
* [Documentação do Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=pt-BR)
