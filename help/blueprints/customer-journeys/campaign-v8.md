---
title: Blueprint do Campaign v8, Campaign e Platform
description: O Adobe Campaign v8 é a ferramenta de campanha de última geração criada para canais de marketing tradicionais, como email e correspondência direta, que oferece recursos sólidos de ETL e gerenciamento de dados para ajudar a arquitetar e organizar a campanha perfeita. Seu mecanismo de orquestração alimenta sofisticados programas de marketing multitoques com foco em jornadas orientadas por lote.  Ele também vem emparelhado com um servidor de mensagens em tempo real escalável que permite às equipes de marketing enviar mensagens predefinidas com base em uma carga abrangente de qualquer sistema de TI para questões como redefinição de senha, confirmação de pedido, recibos eletrônicos e muito mais.
solution: Campaign,Campaign v8
exl-id: 89b3a761-9cb3-4e01-8da0-043e634fa61f
source-git-commit: dabb5ae0bf2fc186f67d4aa93a2e9e8c5bb04498
workflow-type: ht
source-wordcount: '1147'
ht-degree: 100%

---

# Blueprint do Campaign v8

O Adobe Campaign v8 é a ferramenta de campanha de última geração criada para canais de marketing tradicionais, como email e correspondência direta, que oferece recursos sólidos de ETL e gerenciamento de dados para ajudar a arquitetar e organizar a campanha perfeita. Seu mecanismo de orquestração alimenta sofisticados programas de marketing multitoques com foco em jornadas orientadas por lote.  Ele também vem emparelhado com um servidor de mensagens em tempo real escalável que permite às equipes de marketing enviar mensagens predefinidas com base em uma carga abrangente de qualquer sistema de TI para questões como redefinição de senha, confirmação de pedido, recibos eletrônicos e muito mais.

<br>

## Casos de uso

* Programas de mensagens baseadas em lote altamente complexos
* Campanhas de integração e de remarketing
* Campanhas de publicidade por correspondência direta, folheto e revista
* Mensagens transacionais simples (ou seja, redefinição de senha, recebimento de email, confirmação de pedidos, etc.)
* Integração dos dados do Campaign com o Adobe Experience Platform para análise e criação de perfis
* Compartilhamento de públicos-alvo da Real-time Customer Data Platform com o Campaign.

<br>

## Arquitetura

<img src="assets/campaign-v8-architecture.svg" alt="Blueprint de arquitetura de referência para o Campaign v8" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Padrões de integração

| Cenário | Descrição | Recursos |
| :-- | :--- | :--- |
| [Real time Customer Data Platform com Adobe Campaign](rtcdp-and-campaign-v8.md) | Mostra como a Adobe Experience Platform, seu Perfil do cliente em tempo real e sua ferramenta de segmentação centralizada podem ser usados com o Adobe Campaign para proporcionar conversas personalizadas | <ul><li>Compartilhamento de públicos-alvo e perfis da Real-Time CDP com o Adobe Campaign por meio da utilização de fluxos de trabalho tanto de troca de arquivos de armazenamento na nuvem como de assimilação do Adobe Campaign </li><li>Compartilhe facilmente com o Real-Time CDP da Adobe Campaign os dados de entrega e interação das conversas dos clientes para aprimorar o Perfil do cliente em tempo real e gerar relatórios entre canais sobre campanhas de mensagens</li></ul> |
| [Journey Optimizer com Adobe Campaign](ajo-and-campaign.md) | Mostra como usar o Adobe Journey Optimizer para organizar experiências individualizadas utilizando o Perfil do cliente em tempo real e aproveitar o sistema nativo de mensagens transacionais do Adobe Campaign para enviar a mensagem | Aproveite o Perfil do cliente em tempo real e o poder do Journey Optimizer para organizar as experiências na hora, enquanto utiliza os recursos nativos de mensagens em tempo real do Adobe Campaign para fazer a comunicação de última milha<br><br>Considerações:<br><ul><li>Envia até 1 milhão de mensagens por hora por meio do servidor de mensagens em tempo real<li>Não se faz regulagem a partir do Journey Optimizer, então providencie a avaliação técnica de um arquiteto empresarial de pré-vendas</li><li>A gestão de decisões não é compatível com cargas para o Campaign v8</li></ul> |

<br>

## Pré-requisitos


### Servidor de aplicativo e servidor de mensagens em tempo real

* O Adobe Campaign Client Console é necessário para a utilização do software Campaign v8 e interação. Trata-se de um cliente baseado em Windows que usa protocolos-padrão de Internet (SOAP, HTTP, etc.). Certifique-se de que as permissões necessárias para distribuir, instalar e executar o software estão ativas em sua organização

* Lista de permissões de endereço IP
   * Identifique os intervalos de IP que serão usados por todos os usuários durante o acesso ao console do cliente
   * Identifique os sistemas empresariais que serão autorizados a se comunicar com o servidor de mensagens em tempo real e garanta que eles tenham um IP ou intervalo atribuído estaticamente que possa ser incluído na lista de permissões
   * A configuração e o controle podem ser feitos pelo Painel de controle do Campaign
* Gerenciamento de chaves sFTP
   * Tenha chaves públicas SSH disponíveis para serem usadas com o sFTP fornecido pelo Campaign. A configuração e o controle podem ser feitos pelo Painel de controle do Campaign.

### Email

* Tenha um subdomínio pronto para ser usado no envio de mensagens
* O subdomínio pode ser totalmente delegado à Adobe (recomendado) ou podem ser usados CNAMEs para indicar servidores DNS específicos da Adobe (personalizado)
* É necessário registro TXT do Google para cada subdomínio, para garantir um boa capacidade de entrega

### Push para publicação de conteúdo para dispositivos móveis

* Tenha um desenvolvedor para dispositivos móveis disponível para implantar, configurar e criar o aplicativo móvel
* A Adobe oferece apenas um SDK para coletar as informações necessárias do FCM (Android) e do APNS (iOS) para enviar cargas de mensagem aos servidores deles. A forma como o aplicativo móvel precisa ser codificado, implantado, gerenciado e depurado é de responsabilidade do cliente

### Aplicativos web (opcional)

* Podem delegar um subdomínio adicional para as páginas de aterrissagem e de cancelamento de inscrição hospedadas no Campaign
* O certificado SSL é altamente recomendado

<br>

## Medidas de proteção

### Dimensionamento do servidor de aplicativos

* O armazenamento pode ser dimensionado para até 200 milhões de perfis com potencial para aumentar até alcançar um total de 1 bilhão de perfis
* Configure e controle o acesso do usuário por meio do Adobe Admin Console
* Espera-se que o carregamento de dados para o Campaign seja feito por meio de arquivos em lote
   * O suporte ao carregamento de dados de API serve principalmente para o gerenciamento de perfis ou objetos simples no banco de dados (ou seja, criar e atualizar). Não foi projetado para o carregamento de grandes volumes de dados ou operações semelhantes a lotes.
   * A utilização de APIs para ler dados para aplicativos personalizados não é compatível
   * Os dados carregados por meio de API são preparados no banco de dados do aplicativo e, em seguida, replicados a cada hora para o banco de dados na nuvem
* As chamadas de API são limitadas a 15 por segundo ou 150 mil por dia de forma escalável

### Dimensionamento do servidor de mensagens em lote

* Pode ser dimensionado para lidar com até 20 milhões de mensagens por hora

### Dimensionamento do servidor de mensagens em tempo real

* Pode enviar até 1 milhão de mensagens por hora
* Por padrão, são provisionados dois servidores de mensagens em tempo real. Capacidade de aumentar até chegar a um total de oito servidores de mensagens em tempo real.

### Configuração de SMS

* O Campaign oferece o recurso de se integrar a um provedor de SMS. O provedor é adquirido pelo cliente e integrado ao Campaign para enviar mensagens baseadas em SMS
* O suporte é feito por meio do protocolo SMPP
* Há três (3) tipos diferentes de SMS, e a Adobe é compatível com todos eles:
   * SMS MT (terminado no celular): SMSs emitidos pela Adobe Campaign para telefones celulares por meio do provedor SMPP.
   * SMS MO (originado no celular): SMSs enviados de celulares para o Adobe Campaign por meio do provedor SMPP.
   * SMS SR (relatório de status), DR ou DLR (recibo de entrega): um recibo de retorno enviado dos celulares para o Adobe Campaign por meio do provedor SMPP indicando que o SMS foi recebido. O Adobe Campaign também pode receber SRs indicando que a mensagem não pôde ser entregue, geralmente com uma descrição do erro.

### Configuração de push para publicação de conteúdo para dispositivos móveis

* O SDK do Campaign é o único compatível com o Campaign v8. Para ter acesso, entre em contato com o Atendimento ao cliente da Adobe
* Siga a [Documentação do SDK do Campaign](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/sending-push-notifications/integrating-campaign-sdk-into-the-mobile-application.html?lang=pt-BR) para saber como instalar e configurar o SDK

   >[!IMPORTANT]
   >Outros aplicativos da Experience Cloud exigirão o uso do SDK móvel da Experience Platform para coleção de dados. Trata-se de um SDK diferente que precisará ser instalado junto com o SDK do Campaign

<br>

## Etapas de implantação

Consulte o guia de introdução para a [Implementação do Adobe Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/implement/implement.html?lang=pt-BR)


## Documentação relacionada

* [Documentação do Campaign v8](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=pt-BR)
* [Descrição do produto Campaign v8](https://helpx.adobe.com/br/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
* [Documentação de tags da Experience Platform](https://experienceleague.adobe.com/docs/launch.html?lang=pt-BR)
* [Documentação do SDK móvel da Experience Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
