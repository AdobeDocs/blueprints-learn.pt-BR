---
title: Blueprint do Campaign v8
description: O Adobe Campaign v8 é a ferramenta de campanha da próxima geração criada para canais de marketing tradicionais, como email e mala direta. Ele oferece recursos avançados de ETL e gerenciamento de dados para ajudar a criar e preparar a campanha perfeita. Seu mecanismo de orquestração fornece programas de marketing multitoque avançados com foco principal em jornadas orientadas por lote.  Ele também vem junto com um servidor de mensagens em tempo real escalável que permite que as equipes de marketing enviem mensagens predefinidas com base em uma carga abrangente de qualquer sistema de TI para coisas como redefinição de senha, confirmação de pedido, e-receipt's e muito mais.
solution: Campaign v8
exl-id: 89b3a761-9cb3-4e01-8da0-043e634fa61f
source-git-commit: 0c072465c2cac954631fe3a8dbdcef280ee397ab
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 3%

---

# Blueprint do Campaign v8

O Adobe Campaign v8 é a ferramenta de campanha da próxima geração criada para canais de marketing tradicionais, como email e mala direta. Ele oferece recursos avançados de ETL e gerenciamento de dados para ajudar a criar e preparar a campanha perfeita. Seu mecanismo de orquestração fornece programas de marketing multitoque avançados com foco principal em jornadas orientadas por lote.  Ele também vem junto com um servidor de mensagens em tempo real escalável que permite que as equipes de marketing enviem mensagens predefinidas com base em uma carga abrangente de qualquer sistema de TI para coisas como redefinição de senha, confirmação de pedido, e-receipt&#39;s e muito mais.

<br>

## Casos de uso

* Programas de mensagens em lote altamente complexos
* Campanhas de integração e de remarketing
* Campanhas de publicidade por correspondência direta, brochura e revista
* Mensagens transacionais simples (ou seja, redefinição de senha, recebimentos de email, confirmações de pedidos etc.)

<br>

## Arquitetura

<img src="assets/campaign-v8-architecture.svg" alt="Arquitetura de referência para o Campaign v8 Blueprint" style="width:100%; border:1px solid #4a4a4a" />

<br>

## Padrões de integração

| Cenário | Descrição | Capacidades |
| :-- | :--- | :--- |
| [Journey Optimizer com Adobe Campaign](ajo-and-campaign.md) | Mostra como você pode usar o Adobe Journey Optimizer para orquestrar experiências 1:1 utilizando o Perfil do cliente em tempo real e aproveitar o sistema de mensagens transacionais nativo do Adobe Campaign para enviar a mensagem | Aproveite o Perfil do cliente em tempo real e o poder do Journey Optimizer para orquestrar as experiências atuais, ao mesmo tempo em que utiliza os recursos nativos de mensagens em tempo real do Adobe Campaign para fazer a comunicação da última milha<br><br>Considerações:<br><ul><li>Pode enviar até 1 M de mensagens por hora através do servidor de mensagens em tempo real<li>Nenhum controle é executado da Journey Optimizer, portanto, garanta a verificação técnica por um arquiteto corporativo de pré-vendas</li><li>O Offer Decisioning não é compatível em cargas para o Campaign v8</li></ul> |

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

* O armazenamento pode ser dimensionado para até 200 M de perfis com potencial para dimensionar até 1 B de perfis
* Configurar e controlar o acesso do usuário via Adobe Admin Console
* Espera-se que o carregamento de dados para o Campaign seja feito por meio de arquivos em lote
   * O suporte ao carregamento de dados de API é principalmente para o gerenciamento de perfis ou objetos simples no banco de dados (ou seja, criar e atualizar). Não se destina a ser usado para carregar grandes volumes de dados ou operações semelhantes a lotes.
   * Não há suporte para o uso de APIs para ler dados para fins de aplicativo personalizados
   * Os dados carregados por meio da API são preparados no banco de dados do aplicativo e, em seguida, replicados a cada hora para o banco de dados do Cloud
* As chamadas de API são limitadas a 15 por segundo ou 150k por dia na escala

### Dimensionamento do servidor de mensagens em lote

* Pode ser dimensionado para lidar com até 20 milhões de mensagens por hora

### Dimensionamento do servidor de mensagens em tempo real

* Pode enviar até 1 M de mensagens por hora
* Por padrão, dois servidores de mensagens em tempo real são provisionados. Capacidade de dimensionar até oito servidores de mensagens em tempo real.

### Configuração de SMS

* O Campaign oferece a capacidade de integrar com um provedor SMS. O provedor é adquirido pelo cliente e integrado à campanha para enviar mensagens baseadas em SMS
* Suporte por meio do protocolo SMPP
* Há três (3) tipos diferentes de SMS, todos os quais o Adobe pode suportar:
   * SMS MT (Mobile Terminated): um SMS emitido pela Adobe Campaign para telefones celulares através do provedor SMPP.
   * SMS MO (Remoto Originado): um SMS enviado por um dispositivo móvel para o Adobe Campaign por meio do provedor SMPP.
   * SMS SR (Relatório de Status) ou DR ou DLR (Recebimento de Delivery): um recibo de retorno enviado pelo celular para a Adobe Campaign por meio do provedor SMPP, indicando que o SMS foi recebido com êxito. O Adobe Campaign também pode receber SR indicando que a mensagem não pôde ser entregue, geralmente com uma descrição do erro.

### Configuração de push móvel

* Somente o SDK do Campaign é compatível com o Campaign v8. Entre em contato com o Atendimento ao cliente do Adobe para obter acesso
* Siga as [Documentação do SDK do Campaign](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/sending-push-notifications/integrating-campaign-sdk-into-the-mobile-application.html?lang=en) para saber como instalar e configurar o SDK

   >[!IMPORTANT]
   >Outros aplicativos Experience Cloud exigirão o uso do SDK móvel do Experience Platform para coleta de dados. Este é um SDK diferente e precisará ser instalado junto com o SDK do Campaign

<br>

## Etapas de implementação

Consulte o guia de introdução para [Implementação do Adobe Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/implement/implement.html?lang=en)


## Documentação relacionada

* [Documentação do Campaign v8](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=en)
* [Descrição do produto Campaign v8](https://helpx.adobe.com/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
* [Documentação de tags da Experience Platform](https://experienceleague.adobe.com/docs/launch.html?lang=pt-BR)
* [Documentação do SDK móvel da Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
