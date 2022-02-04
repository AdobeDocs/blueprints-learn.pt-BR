---
title: Blueprint do Campaign v7
description: O Adobe Campaign v7 é uma ferramenta de campanha criada para canais de marketing tradicionais, como email e mala direta. Ele oferece recursos avançados de ETL e gerenciamento de dados para ajudar a criar e preparar a campanha perfeita. Seu mecanismo de orquestração fornece programas de marketing multitoque avançados com foco principal em jornadas orientadas por lote.  Ele também é fornecido junto com um servidor de mensagens em tempo real que permite que as equipes de marketing enviem mensagens predefinidas com base em uma carga abrangente de qualquer sistema de TI para coisas como redefinição de senha, confirmação de pedido, recibo eletrônico e muito mais.
solution: Campaign Classic v7
hidefromtoc: true
exl-id: d8cae05f-cf29-45f6-8ee0-1d670a31bdcc
source-git-commit: 13f750c0ff820ab01ed4fc615aba864bc2dc7b75
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 3%

---

# Blueprint do Campaign v7

O Adobe Campaign v7 é uma ferramenta de campanha criada para canais de marketing tradicionais, como email e mala direta. Ele oferece recursos avançados de ETL e gerenciamento de dados para ajudar a criar e preparar a campanha perfeita. Seu mecanismo de orquestração fornece programas de marketing multitoque avançados com foco principal em jornadas orientadas por lote.  Ele também é fornecido junto com um servidor de mensagens em tempo real que permite que as equipes de marketing enviem mensagens predefinidas com base em uma carga abrangente de qualquer sistema de TI para coisas como redefinição de senha, confirmação de pedido, recibo eletrônico e muito mais.

<br>

## Casos de uso

* Programas de mensagens em lote
* Campanhas de integração e de remarketing
* Campanhas de publicidade por correspondência direta, brochura e revista
* Mensagens transacionais simples de baixo volume (ou seja, redefinição de senha, recebimentos de email, confirmações de pedidos etc.)

<br>

## Arquitetura

<img src="assets/campaign-v7-architecture.svg" alt="Arquitetura de referência para o Campaign v7 Blueprint" style="width:100%; border:1px solid #4a4a4a" />

<br>

## Cenários de blueprint

| Cenário | Descrição | Capacidades |
| :-- | :--- | :--- |
| [Journey Optimizer com Adobe Campaign](ajo-and-campaign.md) | Mostra como você pode usar o Adobe Journey Optimizer para orquestrar experiências 1:1 utilizando o Perfil do cliente em tempo real e aproveitar o sistema de mensagens transacionais nativo do Adobe Campaign para enviar a mensagem | Aproveite o Perfil do cliente em tempo real e o poder do Journey Optimizer para orquestrar as experiências atuais, ao mesmo tempo em que utiliza os recursos nativos de mensagens em tempo real do Adobe Campaign para fazer a comunicação da última milha<br><br>Considerações:<br><ul><li>Pode enviar até 50 mil mensagens por hora por meio do servidor de mensagens em tempo real<li>Nenhum controle é executado da Journey Optimizer, portanto, garanta a verificação técnica por um arquiteto corporativo de pré-vendas</li><li>O Offer Decisioning não é compatível em cargas para o servidor de mensagens em tempo real do Campaign v7</li></ul> |
| [Real-Time CDP com Adobe Campaign](rtcdp-and-campaign.md) | Mostra como a Real-Time CDP da Adobe Experience Platform e sua ferramenta de segmentação centralizada podem ser usadas com o Adobe Campaign para fornecer conversas personalizadas | <ul><li>Compartilhamento de públicos-alvo do Experience Platform nativamente com o Adobe Campaign v8 por meio de um destino produzido</li><li>Suporte nativo para assimilar os dados de delivery e interação das conversas com o cliente de volta ao Experience Platform para aprimorar o Perfil do cliente em tempo real e fornecer relatórios entre canais sobre campanhas de mensagens</li></ul> |

<br>

## Pré-requisitos

### Servidor de aplicativos e servidor de mensagens em tempo real

* O Console do Cliente Adobe Campaign é necessário para interagir e usar o software Campaign v8. É um cliente baseado em windows e usa protocolos de Internet padrão (SOAP, HTTP, etc.). Certifique-se de ter as permissões necessárias habilitadas em sua organização para distribuir, instalar e executar o software

* Lista de permissões de endereço IP
   * Identifique os intervalos IP que todos os usuários aproveitarão durante o acesso ao console do cliente
   * Identifique quais sistemas empresariais poderão se comunicar com o servidor de mensagens em tempo real e garantir que eles tenham um IP ou intervalo atribuído estaticamente que você possa lista de permissões
   * Isso pode ser configurado e controlado pelo Painel de controle do Campaign
* Gerenciamento de chaves sFTP
   * Ter chaves públicas SSH disponíveis para uso com o sFTP fornecido pelo Campaign. Isso pode ser configurado e controlado pelo Painel de controle do Campaign.

### Email

* Ter um subdomínio pronto para ser usado no envio de mensagens
* O subdomínio pode ser totalmente delegado ao Adobe (recomendado) ou os CNAMEs podem ser usados para apontar para servidores DNS específicos do Adobe (personalizados)
* O registro TXT do Google é necessário para cada subdomínio para garantir um bom deliverability

### Push para publicação de conteúdo para dispositivos móveis

* Ter um desenvolvedor móvel disponível para implantar, configurar e criar o aplicativo móvel
* O Adobe fornece apenas um SDK para coletar as informações necessárias do FCM (Android) e do APNS (iOS) para enviar cargas de mensagem aos servidores. A forma como o aplicativo móvel precisa ser codificado, implantado, gerenciado e depurado é responsabilidade do cliente

### Webapps (opcional)

* Pode delegar um subdomínio adicional para o cancelamento de inscrição e landing pages hospedadas no Campaign
* O certificado SSL é altamente recomendado

<br>

## Medidas de proteção

### Dimensionamento do servidor de aplicativos

* O armazenamento pode ser dimensionado para até 100 M perfis
* Configurar e controlar o acesso do usuário via Adobe Admin Console (recomendado) ou localmente no próprio aplicativo
* Espera-se que o carregamento de dados para o Campaign seja feito por meio de arquivos em lote
   * O suporte ao carregamento de dados de API é principalmente para o gerenciamento de perfis ou objetos simples no banco de dados (ou seja, criar e atualizar). Não se destina a ser usado para carregar grandes volumes de dados ou operações semelhantes a lotes.
   * Não há suporte para o uso de APIs para ler dados para fins de aplicativo personalizados
* As chamadas de API são limitadas a 15 por segundo ou 150k por dia na escala

### Dimensionamento do servidor de mensagens em lote

* Pode ser dimensionado para lidar com até 2,5 M de mensagens por hora

### Dimensionamento do servidor de mensagens em tempo real

* Pode enviar até 50 mil mensagens por hora
* Por padrão, apenas um (1) servidor de mensagens em tempo real é provisionado. Isso garante que qualquer comunicação com o servidor seja feita por meio de um token de sessão que expira em 24 horas
* Como opção, você pode implantar até oito (8) servidores de mensagens em tempo real, mas a autenticação só oferece suporte a usuário/passagem
* A abordagem recomendada é sempre utilizar um servidor de mensagens em tempo real para aproveitar o auth baseado em token de sessão sempre que possível

### Configuração de SMS

* O Campaign oferece a capacidade de integrar com um provedor SMS. O provedor é adquirido pelo cliente e integrado à campanha para enviar mensagens baseadas em SMS
* Suporte por meio do protocolo SMPP
* Há três (3) tipos diferentes de SMS, todos os quais o Adobe pode suportar:
   * SMS MT (Mobile Terminated): um SMS emitido pela Adobe Campaign para telefones celulares através do provedor SMPP.
   * SMS MO (Remoto Originado): um SMS enviado por um dispositivo móvel para o Adobe Campaign por meio do provedor SMPP.
   * SMS SR (Relatório de Status) ou DR ou DLR (Recebimento de Delivery): um recibo de retorno enviado pelo celular para a Adobe Campaign por meio do provedor SMPP, indicando que o SMS foi recebido com êxito. O Adobe Campaign também pode receber SR indicando que a mensagem não pôde ser entregue, geralmente com uma descrição do erro.

### Configuração de push móvel

* Duas abordagens compatíveis para integração com dispositivos móveis para notificações por push:
   * SDK do Experience Platform Mobile (recomendado)
   * SDK do Campaign Mobile
* Rota do SDK do Experience Platform Mobile:
   * Aproveite as Tags do Adobe e a extensão do Campaign Classic para configurar sua integração com o SDK do Experience Platform Mobile
   * Precisa de um conhecimento prático de Tags de Adobe e coleta de dados
   * Precisa de experiência de desenvolvimento móvel com notificações por push no Android e no iOS para implantar o SDK, integrar com FCM (Android) e APNS (iOS) para obter o token por push, configurar o aplicativo para receber notificações por push e manipular interações por push
* SDK do Campaign Mobile
   * Entre em contato com o Atendimento ao cliente do Adobe para obter acesso
   * Siga as [Documentação do SDK do Campaign](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/sending-push-notifications/integrating-campaign-sdk-into-the-mobile-application.html?lang=en) para saber como instalar e configurar o SDK

   >[!IMPORTANT]
   >Se você implantar o SDK do Campaign e estiver trabalhando com outros aplicativos do Experience Cloud, eles exigirão o uso do SDK do Experience Platform Mobile para coleta de dados. Este é um SDK diferente e precisará ser instalado junto com o SDK do Campaign

<br>

## Etapas de implementação

Consulte a [Guia de Introdução](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html?lang=en) para implementar o Adobe Campaign v7


## Documentação relacionada

* [Documentação do Campaign v7](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=pt-BR)
* [Descrição do produto Campaign v7](https://helpx.adobe.com/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
* [Documentação de tags da Experience Platform](https://experienceleague.adobe.com/docs/launch.html?lang=pt-BR)
* [Documentação do SDK móvel da Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
