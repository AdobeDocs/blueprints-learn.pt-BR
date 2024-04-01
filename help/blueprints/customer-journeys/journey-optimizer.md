---
title: "[!DNL Journey Optimizer] - Blueprint do Adobe Experience Platform e mensagens acionadas"
description: Execute mensagens e experiências acionadas usando a Adobe Experience Platform como um hub central para dados de transmissão, perfis de clientes e segmentação.
solution: Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: a1f3aef5b508575019bd651b9706efc7d6db5306
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 53%

---

# [!DNL Journey Optimizer] blueprints

Adobe [!DNL Journey Optimizer] O é um sistema criado com propósitos específicos para que as equipes de marketing reajam em tempo real aos comportamentos dos clientes e os atendam onde estão. Os recursos de gerenciamento de dados foram movidos para o Adobe [!DNL Experience Platform] permitir que as equipes de marketing se concentrem no que fazem de melhor: criar jornadas de clientes de classe mundial e conversas personalizadas.

Este blueprint descreve as capacidades técnicas do aplicativo e fornece um aprofundamento sobre os vários componentes arquitetônicos que compõem [!DNL Journey Optimizer].

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
| [Mensagens de terceiros](3rd-party-messaging.md) | Demonstra como Adobe [!DNL Journey Optimizer] pode ser utilizado com sistemas de mensagens de terceiros para orquestrar e enviar comunicações personalizadas | Entrega imediata de comunicações individualizadas e personalizadas para os clientes enquanto eles interagem com sua marca ou empresa<br><br>Considerações:<br><ul><li>O sistema de terceiros deve suportar tokens de portador para autenticação</li><li>Devido à arquitetura de vários locatários, não é compatível com IPs estáticos</li><li>Esteja ciente das restrições de arquitetura ao sistema de terceiros em matéria de chamadas de API por segundo.  Pode ser necessário que o cliente compre volume adicional do fornecedor terceirizado para dar suporte ao volume proveniente de [!DNL Journey Optimizer]</li><li>Não é compatível com a gestão de decisões em mensagens ou cargas</li></ul> |

<br>

## Padrões de integração

| Integração | Descrição | Recursos |
| :-- | :--- | :--- |
| [[!DNL Journey Optimizer] com o Adobe Campaign](ajo-and-campaign.md) | Mostra como você pode usar o Adobe [!DNL Journey Optimizer] para orquestrar experiências 1:1 utilizando o Perfil do cliente em tempo real e aproveitar o sistema de mensagens transacionais nativo da Adobe Campaign para enviar a mensagem | Aproveite o Perfil do cliente em tempo real e o potencial do [!DNL Journey Optimizer] para orquestrar experiências do momento, utilizando os recursos nativos de mensagens em tempo real do Adobe Campaign para fazer a comunicação de última milha<br><br>Considerações:<br><ul><li>O aplicativo do Campaign deve ser build v7 superior a 21.1 ou v8</li><li>Taxa de transferência de mensagens</li><ul><li>Campaign v7 - até 50 mil por hora</li><li>Campaign v8 - até 1 milhão por hora</li><li>Campaign Standard - até 50 mil por hora</li></ul><li>Como não é feita nenhuma regulagem, os casos de uso precisam da avaliação técnica de um arquiteto empresarial</li><li>Não há suporte para a utilização da gestão de decisões em mensagem enviada pelo Campaign</li></ul> |

<br>

## Pré-requisitos

Adobe [!DNL Experience Platform]:

* Esquemas e conjuntos de dados devem ser configurados no sistema antes que você possa configurar [!DNL Journey Optimizer] fontes de dados
* Para esquemas do Experience Event baseados em classe, adicione o grupo de campos “eventID de orquestração” quando quiser acionar um evento que não seja baseado em regras
* Para esquemas baseados em classe de Perfil individual, adicione o grupo de campos &quot;Detalhes do teste de perfil&quot; para poder carregar perfis de teste para uso com o [!DNL Journey Optimizer]

Email:

* Deve ter um subdomínio pronto para ser usado no envio de mensagens
* O subdomínio pode ser totalmente delegado à Adobe (recomendado) ou podem ser usados CNAMEs para indicar servidores DNS específicos da Adobe (personalizado)
* É necessário registro TXT do Google para cada subdomínio, para garantir um boa capacidade de entrega

Push para dispositivo móvel:

* O cliente deve ter um desenvolvedor de publicações de conteúdo para dispositivos móveis disponível para criar o aplicativo
* SDK móvel da Adobe Experience Platform

## Medidas de proteção

[[!DNL Journey Optimizer] Link do produto Medidas de proteção](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html)

[Medidas de proteção e orientação de latência completa](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

## Documentação relacionada

* [[!DNL Experience Platform] documentação](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [[!DNL Experience Platform] Documentação de tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)
* [[!DNL Experience Platform Mobile SDK] documentação](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
* [[!DNL Journey Optimizer] documentação](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR)
* [[!DNL Journey Optimizer] descrição do produto](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html)
