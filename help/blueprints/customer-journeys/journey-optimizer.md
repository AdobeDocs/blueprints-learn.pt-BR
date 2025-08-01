---
title: '[!DNL Journey Optimizer] - Mensagens acionadas e Blueprint do Adobe Experience Platform'
description: Execute mensagens e experiências acionadas usando a Adobe Experience Platform como um hub central para dados de transmissão, perfis de clientes e segmentação.
solution: Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: 75a0f2a77f39a4320dc4c4b0db918879be099dd3
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 50%

---

# [!DNL Journey Optimizer] blueprints

O Adobe [!DNL Journey Optimizer] é um sistema criado especificamente para que as equipes de marketing reajam em tempo real aos comportamentos dos clientes e os encontrem onde estiverem. Os recursos de gerenciamento de dados foram movidos para o Adobe [!DNL Experience Platform], permitindo que as equipes de marketing se concentrem no que fazem de melhor: criar jornadas de clientes de classe mundial e conversas personalizadas.

Este blueprint descreve os recursos técnicos do aplicativo e fornece um aprofundamento sobre os vários componentes de arquitetura que compõem o [!DNL Journey Optimizer].

## Casos de uso

* Mensagens acionadas
* Confirmações de boas-vindas e registro
* Carrinho de compras e abandonos de formulários de aplicação
* Mensagens acionadas de localização
* Experiências in loco
* Experiências de viagem e hospitalidade antes da chegada e durante a estadia

## Arquitetura

<img src="assets/ajo-architecture.svg" alt="Blueprint do Journey Optimizer com arquitetura de referência" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## Cenários do blueprint

| Cenário | Descrição | Recursos |
| :-- | :--- | :--- |
| [Mensagens de terceiros](3rd-party-messaging.md) | Demonstra como o Adobe [!DNL Journey Optimizer] pode ser utilizado com sistemas de mensagens de terceiros para orquestrar e enviar comunicações personalizadas | Forneça 1:1 comunicações personalizadas no momento para os clientes à medida que eles interagem com sua marca ou empresa<br><br>Considerações:<br><ul><li>O sistema de terceiros deve suportar tokens de portador para autenticação</li><li>Devido à arquitetura de vários locatários, não é compatível com IPs estáticos</li><li>Esteja ciente das restrições de arquitetura ao sistema de terceiros em matéria de chamadas de API por segundo.  Pode ser necessário que o cliente compre volume adicional do fornecedor terceirizado para dar suporte ao volume proveniente de [!DNL Journey Optimizer]</li><li>Não é compatível com a gestão de decisões em mensagens ou cargas</li></ul> |

<br>

## Padrões de integração

| Integração | Descrição | Recursos |
| :-- | :--- | :--- |
| [[!DNL Journey Optimizer] com Adobe Campaign](ajo-and-campaign.md) | Mostra como você pode usar o Adobe [!DNL Journey Optimizer] para orquestrar 1:1 experiências utilizando o Perfil de Cliente em Tempo Real e aproveitar o sistema de mensagens transacionais nativo do Adobe Campaign para enviar a mensagem | Aproveite o Perfil do Cliente em Tempo Real e o poder do [!DNL Journey Optimizer] para orquestrar experiências de momento, utilizando os recursos nativos de mensagens em tempo real do Adobe Campaign para fazer a comunicação da última milha<br><br>Considerações:<br><ul><li>O aplicativo do Campaign deve ser build v7 superior a 21.1 ou v8</li><li>Taxa de transferência de mensagens</li><ul><li>Campaign v7 - até 50 mil por hora</li><li>Campaign v8 - até 1 milhão por hora</li><li>Campaign Standard - até 50 mil por hora</li></ul><li>Como não é feita nenhuma regulagem, os casos de uso precisam da avaliação técnica de um arquiteto empresarial</li><li>Não há suporte para a utilização da gestão de decisões em mensagem enviada pelo Campaign</li></ul> |

<br>

## Pré-requisitos

Adobe [!DNL Experience Platform]:

* Esquemas e conjuntos de dados devem ser configurados no sistema antes que você possa configurar as fontes de dados do [!DNL Journey Optimizer]
* Para esquemas do Experience Event baseados em classe, adicione o grupo de campos “eventID de orquestração” quando quiser acionar um evento que não seja baseado em regras
* Para esquemas baseados em classe de Perfil Individual, adicione o grupo de campos &#39;Detalhes do teste de perfil&#39; para poder carregar perfis de teste para uso com [!DNL Journey Optimizer]

Email:

* Deve ter um subdomínio pronto para ser usado no envio de mensagens
* O subdomínio pode ser totalmente delegado à Adobe (recomendado) ou podem ser usados CNAMEs para indicar servidores DNS específicos da Adobe (personalizado)
* É necessário registro TXT do Google para cada subdomínio, para garantir um boa capacidade de entrega

Push para dispositivo móvel:

* O cliente deve ter um desenvolvedor de publicações de conteúdo para dispositivos móveis disponível para criar o aplicativo
* SDK móvel da Adobe Experience Platform

## Medidas de proteção

[[!DNL Journey Optimizer] Link de Produto de Medidas de Proteção](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)

[Medidas de Proteção e Orientação de Latência de Ponta a Ponta](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/guardrails.html)

## Documentação relacionada

* [[!DNL Experience Platform] documentação](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [[!DNL Experience Platform] Documentação de tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)
* [[!DNL Experience Platform Mobile SDK] documentação](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
* [[!DNL Journey Optimizer] documentação](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR)
* [[!DNL Journey Optimizer] descrição do produto](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html)
