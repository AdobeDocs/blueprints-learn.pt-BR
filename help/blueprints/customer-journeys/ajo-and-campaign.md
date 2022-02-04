---
title: Journey Optimizer com Adobe Campaign Blueprint
description: Demonstra como o Adobe Journey Optimizer pode ser usado com o Adobe Campaign para enviar mensagens nativamente utilizando o servidor de mensagens em tempo real no Campaign
solution: Experience Platform, Journey Optimizer, Campaign v8, Campaign Classic v7, Campaign Standard
source-git-commit: 1c46cbdfc395de4fc9139966cf869ba1feeceaaa
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 26%

---

# Journey Optimizer com Adobe Campaign

Demonstra como o Adobe Journey Optimizer pode ser usado com o Adobe Campaign para enviar mensagens nativamente utilizando o servidor de mensagens em tempo real no Campaign.

<br>

## Arquitetura

<img src="assets/ajo-campaign-architecture.svg" alt="Arquitetura de referência Journey Optimizer blueprint" style="width:100%; border:1px solid #4a4a4a" />

>[!IMPORTANT]
>É possível usar o Journey Optimizer e o Campaign para enviar mensagens independentemente umas das outras, mas há algumas considerações técnicas que precisam ser levadas em consideração. Se você quiser seguir essa rota, trabalhe com seu Arquiteto empresarial de pré-vendas para garantir que tenha uma compreensão do que será necessário para dar suporte à implementação.

<br>

## Pré-requisitos

### Adobe Experience Platform

* Os esquemas e conjuntos de dados devem ser configurados no sistema antes que você possa configurar as fontes de dados do Journey Optimizer
* Para esquemas baseados em classe do Experience Event, adicione o grupo de campos &#39;Orchestration eventID quando quiser que um evento seja acionado e não seja um evento baseado em regras
* Para esquemas baseados em classe de Perfil individual, adicione o grupo de campos &quot;Detalhes do teste de perfil&quot; para carregar perfis de teste para uso com o Journey Optimizer
* O Journey Optimizer e o Campaign são provisionados na mesma Organização IMS

### Campaign v7/v8 ou Campaign Standard

* A instância de execução do serviço de mensagens em tempo real (ou seja, o Centro de Mensagens) deve ser hospedada pelo Adobe Managed Cloud Services
* Toda a criação de mensagens é feita dentro da própria instância do Campaign

<br>

## Medidas de proteção

[Link de produto do Journey Optimizer Guardrails](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=pt-BR)

### Medidas de proteção adicionais do Journey Optimizer

* O limite está disponível por meio da API hoje, para garantir que o sistema de destino não esteja saturado até o ponto de falha. Isso significa que as mensagens que excedem a tampa serão descartadas completamente e nunca serão enviadas. Não há suporte para limitação.
   * Conexões máximas - número máximo de conexões http/s que um destino pode lidar
   * Contagem máxima de chamadas - número máximo de chamadas a serem feitas no parâmetro periodInMs
   * periodInMs - tempo em milissegundos
* Jornadas iniciadas por associação de segmentos podem operar em dois modos:
   * Segmentos em lote (atualizados a cada 24 horas)
   * Segmentos de transmissão (qualificação de &lt;5mins)
* Segmentos em lote – precisam assegurar que você entenda o volume diário de usuários qualificados e que o sistema de destino possa lidar com a taxa de transferência intermitente por jornada e em todas as jornadas
* Segmentos por streaming – precisam assegurar que a intermitência inicial de qualificações de perfis possam ser manipuladas com o volume de qualificações de streaming diárias por jornada e em todas as jornadas
* offer decisioning sem suporte
* Eventos de negócios não são suportados
* Integrações de saída para sistemas de terceiros
   * Não há suporte para um único IPs estáticos, pois nossa infraestrutura é de vários locatários (é necessário lista de permissões todos os IPs do data center)
   * Somente os métodos POST e PUT são compatíveis com ações personalizadas
   * Suporte de autenticação: token | senha | OAuth2
* Não é possível empacotar e mover componentes individuais do Adobe Experience Platform ou Journey Optimizer entre várias sandboxes. Deve reimplementar em novos ambientes

<br>

### Campanha (v7/v8)

* A instância de execução do Centro de Mensagens deve ser hospedada pelo Adobe Managed Cloud Services
* Precisa estar na build v7 >21.1 ou v8
* Taxa de transferência de mensagens
   * AC (v7) 50k por hora
   * AC (v8) até 1M por hora com base na embalagem
* AC (v7) suporta apenas jornadas iniciadas por eventos
   * Nenhuma Jornada iniciada por associação de segmento ou segmento
   * Ler público-alvo e a jornada baseada em evento comercial não são suportadas devido ao volume que pode ser enviado para as instâncias de execução
* O AC (v7) ou o AC (v8) não oferecem suporte ao Offer Decisioning nas mensagens
* Sem limitação de chamadas de API de saída feitas para o Campaign
* Os logs de mensagens transacionais não são nativamente sincronizados com o AEP. Requer esforço de consultoria. Recomendação para exportar logs no máximo a cada 4 horas

<br>

### Campaign Standard

* Suporta 14 tps (50k por hora) na taxa de transferência
* Só suporta jornadas iniciadas por eventos
   * Nenhuma Jornada iniciada por associação de segmento ou segmento
   * Ler público-alvo e a jornada baseada em evento comercial não são suportadas devido ao volume que pode ser enviado para as instâncias de execução
* As atividades de clique e abertura de mensagens transacionais enviadas para o Campaign Standard são nativamente expostas como &quot;Eventos de nova ação&quot; na tela de jornada do Journey Optimizer
* Os registros de mensagens transacionais não são nativamente sincronizados no Experience Platform. Requer esforço de consultoria. Recomendação para exportar logs no máximo a cada 4 horas

<br>

## Etapas de implementação

### Adobe Experience Platform

#### Esquemas/Conjuntos de dados

1. [Configure perfil individual, evento de experiência e esquemas de várias entidades](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) na Experience Platform com base nos dados fornecidos pelo cliente.
1. Crie esquemas baseados em classe do Experience Event para tabelas de endereços do Adobe Campaign broadLog, trackingLog e não entregues (opcional).
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
1. Configure as origens de dados externos
1. Configurar ações personalizadas para a instância do Campaign

### Campaign v7/v8 ou Campaign Standard

* Os templates de mensagem precisam ser configurados com o contexto de personalização apropriado
* Os workflows de exportação precisam ser configurados para exportar os logs de mensagens transacionais de volta para o Experience Platform. A recomendação é executada no máximo a cada 4 horas

### Configuração de push móvel (opcional)

1. Implemente o SDK do Experience Platform Mobile para coletar tokens de push e informações de logon para se vincular a perfis de clientes conhecidos
1. Aproveite as Tags do Adobe e crie uma propriedade móvel com a seguinte extensão:
   * Adobe Journey Optimizer | Adobe Campaign Classic | Adobe Campaign Standard
   * Rede de borda da Adobe Experience Platform
   * Identidade para rede Edge
   * Mobile Core
1. Certifique-se de ter um conjunto de dados dedicado para implantações de aplicativos móveis e implantações da Web
1. Para obter mais informações, siga as [Guia do Adobe Journey Optimizer Mobile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)

   >[!IMPORTANT]
   >Os tokens móveis podem precisar ser coletados no Journey Optimizer e no Campaign se desejar enviar comunicações em tempo real via Journey Optimizer e notificações por push em lote via Campaign. O Campaign v8 requer o uso exclusivo do SDK do Campaign para capturar tokens de push.

<br>

## Documentação relacionada

* [Documentação do Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Documentação de tags da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en)
* [Documentação do SDK móvel da Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
* [Documentação do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR)
* [Descrição do produto Journey Optimizer](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
* [Documentação do Campaign v8](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=en)
* [Documentação do Campaign v7](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=pt-BR)
* [Documentação do Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=pt-BR)