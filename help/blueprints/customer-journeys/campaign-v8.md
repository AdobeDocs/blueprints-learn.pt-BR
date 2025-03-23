---
title: Blueprint do Campaign v8, Campaign e Platform
description: Saiba mais sobre o blueprint do Campaign v8.
solution: Campaign,Campaign v8
version: Campaign v8
exl-id: 89b3a761-9cb3-4e01-8da0-043e634fa61f
source-git-commit: 1d10727899aaae6b8cd339ce10d2a520c73bdaa2
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 41%

---

# Blueprint do Campaign v8

O Adobe Campaign v8 é a ferramenta de campanha de última geração criada para canais de marketing tradicionais, como email e correspondência direta, que oferece recursos sólidos de ETL e gerenciamento de dados para ajudar a arquitetar e organizar a campanha perfeita. Seu mecanismo de orquestração fornece programas de marketing multitoque avançados com foco principal em jornadas orientadas por lote.

Ele também vem emparelhado com um servidor de mensagens em tempo real escalável que permite às equipes de marketing enviar mensagens predefinidas com base em uma carga abrangente de qualquer sistema de TI para questões como redefinição de senha, confirmação de pedido, recibos eletrônicos e muito mais.

## Casos de uso

* Programas de mensagens em lote altamente complexos.
* Campanhas de integração e de remarketing.
* Campanhas de publicidade por correspondência direta, folheto e revista
* Mensagens transacionais simples (como redefinição de senha, recibos de email, confirmações de pedidos e assim por diante).
* Integração dos dados do Campaign ao Adobe Experience Platform para análise e criação de perfil.
* Compartilhamento de públicos-alvo da Real-time Customer Data Platform com o Campaign.

## Diagramas de arquitetura

Saiba mais sobre [modelos de implantação do Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/config/architecture/architecture.html#ac-deployment){target="_blank"}.

### Implantação do Campaign Enterprise (FFDA)

<img src="assets/P4-architecture.png" alt="Arquitetura de referência do Blueprint do Campaign v8 (P4)" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

### Implantação do FDA no Campaign v8

<img src="assets/P1-P3-architecture.png" alt="Arquitetura de referência do Blueprint do Campaign v8 (P1-P3)" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## Padrões de integração

| Cenário | Descrição | Recursos |
| :-- | :--- | :--- |
| [[!DNL Real-time Customer Data Platform] com Adobe [!DNL Campaign]](rtcdp-and-campaign-v8.md) | Mostra como a Adobe Experience Platform e seu Perfil do Cliente em Tempo Real e a ferramenta de segmentação centralizada podem ser utilizados com o Adobe [!DNL Campaign] para fornecer conversas personalizadas | <ul><li>Compartilhamento de perfis e públicos do [!DNL Real-Time CDP] para o Adobe [!DNL Campaign] por meio do uso da troca de arquivos de armazenamento em nuvem e dos fluxos de trabalho de assimilação do Adobe [!DNL Campaign] </li><li>Compartilhe facilmente dados de entrega e interação de conversas com clientes no [!DNL Real-Time CDP] a partir do Adobe [!DNL Campaign] para aprimorar o Perfil do cliente em tempo real e fornecer relatórios entre canais sobre campanhas de mensagens</li></ul> |
| [[!DNL Journey Optimizer] com Adobe [!DNL Campaign]](ajo-and-campaign.md) | Mostra como você pode usar o Adobe Journey Optimizer para orquestrar experiências individuais utilizando o Perfil de Cliente em Tempo Real e aproveitar o sistema de mensagens transacionais [!DNL Campaign] nativo do Adobe para enviar a mensagem | Aproveite o Perfil do Cliente em Tempo Real e o poder do [!DNL Journey Optimizer] para orquestrar experiências de momento, utilizando os recursos nativos de mensagens em tempo real do Adobe [!DNL Campaign] para fazer a comunicação da última milha<br><br>Considerações:<br><ul><li>Envia até 1 milhão de mensagens por hora por meio do servidor de mensagens em tempo real<li>Nenhuma limitação é executada a partir de [!DNL Journey Optimizer], portanto, garanta a verificação técnica por um arquiteto corporativo de pré-vendas</li><li>A gestão de decisões não é compatível com cargas para o Campaign v8</li></ul> |

## Pré-requisitos

Existem os seguintes pré-requisitos para este blueprint.

### Servidor de aplicativo e servidor de mensagens em tempo real

* O Console do Cliente do Adobe [!DNL Campaign] é necessário para interagir e usar o software [!DNL Campaign] v8. Trata-se de um cliente baseado em Windows que usa protocolos-padrão de Internet (SOAP, HTTP, etc.). Certifique-se de que as permissões necessárias para distribuir, instalar e executar o software estão ativas em sua organização

* Lista de permissões de endereço IP:
   * Identifique os intervalos IP que todos os usuários utilizam durante o acesso ao console do cliente.
   * Identifique quais sistemas corporativos têm permissão para se comunicar com o servidor de mensagens em tempo real e verifique se eles têm um IP atribuído estaticamente ou um intervalo que você possa incluir na lista de permissões.
   * A configuração e o controle podem ser feitos pelo Painel de controle do Campaign.
* Gerenciamento de chaves sFTP:
   * Tenha chaves públicas SSH disponíveis para serem usadas com o sFTP fornecido pelo Campaign. A configuração e o controle podem ser feitos pelo Painel de controle do Campaign.

### Email

* Ter um subdomínio pronto para ser usado para enviar mensagens.
* O subdomínio pode ser totalmente delegado à Adobe (recomendado) ou os CNAMEs podem ser usados para apontar para servidores DNS específicos da Adobe (personalizados).
* O registro TXT do Google é necessário para cada subdomínio para garantir uma boa capacidade de entrega.

### Push para publicação de conteúdo para dispositivos móveis

* Tenha um desenvolvedor móvel disponível para implantar, configurar e criar o aplicativo móvel.
* A Adobe oferece apenas um SDK para coletar as informações necessárias do FCM (Android) e do APNS (iOS) para enviar cargas de mensagem aos servidores deles. A forma como o aplicativo móvel precisa ser codificado, implantado, gerenciado e depurado é responsabilidade do cliente.

### Aplicativos web (opcional)

* Pode delegar um subdomínio adicional para páginas de destino e de cancelamento de inscrição hospedadas no Campaign.
* O certificado SSL é altamente recomendado.

## Medidas de proteção

As medidas de proteção são descritas abaixo.

### Dimensionamento do servidor de aplicativos

* O armazenamento pode ser dimensionado para até 200 milhões de perfis com potencial para dimensionar até 1 bilhão de perfis.
* Configure e controle o acesso do usuário via Adobe [!DNL Admin Console].
* Espera-se que o carregamento de dados para [!DNL Campaign] seja feito por meio de arquivos em lotes:
   * O suporte ao carregamento de dados de API serve principalmente para o gerenciamento de perfis ou objetos simples no banco de dados (ou seja, criar e atualizar). Não foi projetado para o carregamento de grandes volumes de dados ou operações semelhantes a lotes.
   * A utilização de APIs para ler dados para aplicativos personalizados não é compatível
   * Os dados carregados por meio de API são preparados no banco de dados do aplicativo e, em seguida, replicados a cada hora para o banco de dados na nuvem
* Os limites para chamadas de API se aplicam. Saiba mais na [Descrição do produto Adobe Campaign](https://helpx.adobe.com/br/legal/product-descriptions/adobe-campaign-managed-cloud-services.html){target="_blank"}.

### Dimensionamento do servidor de mensagens em lote

* Pode ser dimensionado para lidar com até 20 milhões de mensagens por hora

### Dimensionamento do servidor de mensagens em tempo real

* Pode enviar até 1 milhão de mensagens por hora
* Por padrão, são provisionados dois servidores de mensagens em tempo real. Capacidade de aumentar até chegar a um total de oito servidores de mensagens em tempo real.

### Configuração de SMS

* O Campaign oferece o recurso de se integrar a um provedor de SMS. O provedor é adquirido pelo cliente e integrado ao Campaign para envio de mensagens baseadas em SMS.
* O suporte é por meio do protocolo SMPP.
* Há três (3) tipos diferentes de SMS, e a Adobe é compatível com todos eles:
   * SMS MT (Terminado por Dispositivo Móvel): um SMS emitido pelo Adobe [!DNL Campaign] para telefones celulares por meio do provedor SMPP.
   * SMS MO (Originado por dispositivo móvel): um SMS enviado por um dispositivo móvel para o Adobe [!DNL Campaign] por meio do provedor SMPP.
   * SMS SR (Relatório de Status) ou DR ou DLR (Recibo de Entrega): um recibo de retorno enviado pelo dispositivo móvel ao Adobe [!DNL Campaign] por meio do provedor SMPP, indicando que o SMS foi recebido com êxito. O Adobe [!DNL Campaign] também pode receber um SR indicando que a mensagem não pôde ser entregue, geralmente com uma descrição do erro.

## Etapas de implantação

Consulte o guia de introdução para a [Implementação do Adobe Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/implement/implement.html?lang=pt-BR)

## Documentação relacionada

* [Documentação do Campaign v8](https://experienceleague.adobe.com/docs/campaign-v8.html)
* [Descrição do produto Campaign v8](https://helpx.adobe.com/br/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
* [Documentação de tags da Experience Platform](https://experienceleague.adobe.com/docs/launch.html)
* [Documentação do SDK móvel da Experience Platform](https://experienceleague.adobe.com/docs/mobile.html)
