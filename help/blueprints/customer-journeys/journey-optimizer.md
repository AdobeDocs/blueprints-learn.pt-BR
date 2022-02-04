---
title: Journey Optimizer – Blueprint de mensagens acionadas e da Adobe Experience Platform
description: Execute mensagens e experiências acionadas usando a Adobe Experience Platform como um hub central para dados de transmissão, perfis de clientes e segmentação.
solution: Experience Platform, Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: 2ead62f94e761cd9453be284a9fde3c5803879eb
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 42%

---

# Journey Optimizer

O Adobe Journey Optimizer é um sistema criado para as equipes de marketing reagirem em tempo real aos comportamentos dos clientes e atendê-los onde quer que eles estejam. Os recursos de gerenciamento de dados foram transferidos para a Adobe Experience Platform, permitindo que as equipes de marketing se concentrem no que fazem de melhor: criar jornadas de clientes de alto nível e conversas personalizadas.  Este blueprint descreve os recursos técnicos do aplicativo e fornece detalhes sobre os diferentes componentes de arquitetura que compõem o Adobe Journey Optimizer.

<br>

## Casos de uso

* Mensagens acionadas
* Confirmações de boas-vindas e registro
* Carrinho de compras e abandonos de formulários de aplicação
* Mensagens acionadas de localização
* Experiências no estádio
* Experiências de viagem e hospitalidade antes da chegada e de estada

<br>

## Arquitetura

<img src="assets/ajo-architecture.svg" alt="Arquitetura de referência Journey Optimizer blueprint" style="width:100%; border:1px solid #4a4a4a" />

<br>

## Cenários de blueprint

| Cenário | Descrição | Capacidades |
| :-- | :--- | :--- |
| [Mensagens de terceiros](3rd-party-messaging.md) | Demonstra como o Adobe Journey Optimizer pode ser usado com sistemas de mensagens de terceiros para orquestrar e enviar comunicações personalizadas | Fornecer 1:1 no momento em que as comunicações personalizadas são enviadas aos clientes, conforme eles interagem com sua marca ou empresa<br><br>Considerações:<br><ul><li>O sistema de terceiros deve suportar tokens de portador para autenticação</li><li>Não há suporte para IPs estáticos devido à arquitetura de vários locatários</li><li>Esteja ciente das restrições de arquitetura do sistema de terceiros quando se trata de chamadas de API por segundo.  Pode ser uma necessidade do cliente comprar volume adicional do fornecedor terceirizado para suportar o volume proveniente da Journey Optimizer</li><li>Não suporta Offer Decisioning em mensagens ou cargas</li></ul> |

<br>

## Padrões de integração

| Integração | Descrição | Capacidades |
| :-- | :--- | :--- |
| [Journey Optimizer com Adobe Campaign](ajo-and-campaign.md) | Mostra como você pode usar o Adobe Journey Optimizer para orquestrar experiências 1:1 utilizando o Perfil do cliente em tempo real e aproveitar o sistema de mensagens transacionais nativo do Adobe Campaign para enviar a mensagem | Aproveite o Perfil do cliente em tempo real e o poder do Journey Optimizer para orquestrar as experiências atuais, ao mesmo tempo em que utiliza os recursos nativos de mensagens em tempo real do Adobe Campaign para fazer a comunicação da última milha<br><br>Considerações:<br><ul><li>O aplicativo do Campaign deve estar na build v7 >21.1 ou v8</li><li>Taxa de transferência de mensagens</li><ul><li>Campaign v7 - até 50 mil por hora</li><li>Campanha v8 - até 1M por hora</li><li>Campaign Standard - até 50 mil por hora</li></ul><li>Nenhum controle é executado, portanto, os casos de uso precisam de uma verificação técnica por um Arquiteto da empresa</li><li>Não há suporte para utilizar o Offer Decisioning na mensagem enviada pelo Campaign</li></ul> |

<br>

## Pré-requisitos

Adobe Experience Platform

* Os esquemas e conjuntos de dados devem ser configurados no sistema antes que você possa configurar as fontes de dados do Journey Optimizer
* Para esquemas baseados em classe do Experience Event, adicione o grupo de campos &#39;Orchestration eventID quando quiser que um evento seja acionado e não seja um evento baseado em regras
* Para esquemas baseados em classe de Perfil individual, adicione o grupo de campos &quot;Detalhes do teste de perfil&quot; para carregar perfis de teste para uso com o Journey Optimizer

Email

* Deve ter um subdomínio pronto para ser usado no envio de mensagens
* O subdomínio pode ser totalmente delegado ao Adobe (recomendado) ou os CNAMEs podem ser usados para apontar para servidores DNS específicos do Adobe (personalizados)
* O registro TXT do Google é necessário para cada subdomínio para garantir um bom deliverability

Push para publicação de conteúdo para dispositivos móveis

* O cliente deve ter um desenvolvedor de publicações de conteúdo para dispositivos móveis disponível para criar o aplicativo
* SDK móvel da Adobe Experience Platform

<br>

## Medidas de proteção

[Link de produto do Journey Optimizer Guardrails](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=pt-BR)

Esteja ciente desses itens não listados no link acima:

* Segmentos em lote – precisam assegurar que você entenda o volume diário de usuários qualificados e que o sistema de destino possa lidar com a taxa de transferência intermitente por jornada e em todas as jornadas
* Segmentos por streaming – precisam assegurar que a intermitência inicial de qualificações de perfis possam ser manipuladas com o volume de qualificações de streaming diárias por jornada e em todas as jornadas
* Oferece suporte nativo ao Offer Decisioning somente em mensagens (sem ações personalizadas)
* Tipos de mensagem compatíveis:
   * Email
   * Push (FCM/APNS)
   * Ações personalizadas (por meio da API Rest)
* Integrações de saída para sistemas de terceiros
   * Não há suporte para um único IPs estáticos, pois nossa infraestrutura é de vários locatários (é necessário lista de permissões todos os IPs do data center)
   * Somente os métodos POST e PUT são compatíveis com ações personalizadas
   * Autenticação por usuário/senha ou token de autorização
* Não é possível empacotar e mover componentes individuais do Adobe Experience Platform ou Journey Optimizer entre várias sandboxes. Deve reimplementar em novos ambientes

### Medidas de proteção da assimilação de dados

<img src="assets/aep-data-ingestion-details-latency.svg" alt="Arquitetura de referência Journey Optimizer blueprint" style="width:80%; border:1px solid #4a4a4a" />

<br>

### Medidas de Proteção de Ativação

<img src="assets/ajo-activation-details-latency.svg" alt="Arquitetura de referência Journey Optimizer blueprint" style="width:80%; border:1px solid #4a4a4a" />

<br>

## Etapas de implementação

### Adobe Experience Platform

#### Esquemas/Conjuntos de dados

1. [Configure perfil individual, evento de experiência e esquemas de várias entidades](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) na Experience Platform com base nos dados fornecidos pelo cliente.
1. [Crie conjuntos de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) na Experience Platform para que os dados sejam assimilados.
1. [Adicione rótulos de uso de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=pt-BR) na Experience Platform para o conjunto de dados para governança.
1. [Crie políticas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=pt-BR) que apliquem governança nos destinos.

#### Perfil/Identidade

1. [Crie qualquer namespace específico para clientes](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR).
1. [Adicione identidades a esquemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Habilite os esquemas e conjuntos de dados para o Perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=pt-BR).
1. [Configure políticas de mesclagem](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=pt-BR) para visualizações diferentes do [!UICONTROL Perfil de cliente em tempo real] (opcional).
1. Crie segmentos para uso da Jornada.

#### Origens/Destinos

1. [Assimile dados na Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) usando APIs de streaming e conectores de origem.

### Journey Optimizer

1. Configure sua fonte de dados do Experience Platform e determine quais campos devem ser armazenados em cache como parte dos dados profileStreaming usados para iniciar uma jornada do cliente devem ser configurados no Journey Optimizer primeiro para obter uma ID de orquestração. Depois, essa ID de orquestração será fornecida ao desenvolvedor para usá-la na assimilação
1. Configure as origens de dados externos.
1. Configure as ações personalizadas.

### Configuração de push móvel

1. Implemente o SDK do Experience Platform Mobile para coletar tokens de push e informações de logon para se vincular a perfis de clientes conhecidos
1. Aproveite as Tags do Adobe e crie uma propriedade móvel com a seguinte extensão:
1. Adobe Journey Optimizer
1. Rede de borda da Adobe Experience Platform
1. Identidade para rede Edge
1. Mobile Core
1. Certifique-se de ter um conjunto de dados dedicado para implantações de aplicativos móveis e implantações da Web
1. Para obter mais informações, siga as [Guia do Adobe Journey Optimizer Mobile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)


## Documentação relacionada

* [Documentação do Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Documentação de tags da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en)
* [Documentação do SDK móvel da Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
* [Documentação do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR)
* [Descrição do produto Journey Optimizer](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
