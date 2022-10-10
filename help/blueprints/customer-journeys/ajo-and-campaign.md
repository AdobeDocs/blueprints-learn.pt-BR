---
title: Blueprint do Journey Optimizer com Adobe Campaign
description: Demonstra como o Adobe Journey Optimizer pode ser usado com o Adobe Campaign para enviar mensagens utilizando o servidor de mensagens em tempo real no Campaign de forma nativa
solution: Journey Optimizer, Campaign, Campaign v8, Campaign Classic v7, Campaign Standard
exl-id: 076446a9-dfb9-464c-a04f-6864b8cb7b48
source-git-commit: 6901596cbb661ffa8cf57c6ae958db1978bf1520
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 92%

---

# Journey Optimizer com Adobe Campaign

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

### Campaign v7/v8 ou Campaign Standard

* A instância de execução do serviço de mensagens em tempo real (ou seja, o Centro de Mensagens) deve ser hospedada por Adobe Managed Cloud Services
* Toda a criação de mensagens é feita dentro da própria instância do Campaign

<br>

## Medidas de proteção

[Link do produto medidas de proteção do Journey Optimizer](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=pt-BR)

### Medidas de proteção adicionais do Journey Optimizer

* O limite agora está disponível por meio de API para garantir que o sistema de destino não esteja saturado ao ponto de falha. Isso significa que as mensagens que excederem o limite serão completamente removidas sem ser enviadas. A regulagem não é compatível.
   * Conexões máximas - número máximo de conexões http/s com que um destino pode lidar
   * Contagem máxima de chamadas - número máximo de chamadas a serem realizadas no parâmetro periodInMs
   * periodInMs - tempo em milissegundos
* Jornadas iniciadas por associação de segmentos podem operar em dois modos:
   * Segmentos em lote (atualizados a cada 24 horas)
   * Segmentos de transmissão (qualificação de &lt;5 minutos)
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

### Integrações da campanha

Para obter orientação sobre a integração com sua versão específica do Adobe Campaign e do Adobe Journey Optimizer, consulte o guia correspondente para cada versão do Adobe Campaign.

* [Adobe Journey Optimizer &amp; Campaign v7](ajo-and-campaign-v7.md)
* [Adobe Journey Optimizer &amp; Campaign v8](ajo-and-campaign-v8.md)