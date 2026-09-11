---
title: Criar sequência de dados
description: Crie e configure um fluxo de dados com os serviços Encaminhamento de eventos e Adobe Experience Platform para rotear eventos de borda de entrada.
doc-type: article
solution: Experience Platform
exl-id: f7ada451-2f87-48f4-8673-7bfa0df9d0d3
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---


# Criar sequência de dados

Uma sequência de dados define quais serviços a utilizarão.

- Ao enviar dados para a Edge, você especifica qual sequência de dados usar
- Os dados enviados para esses Datastreams podem agir de acordo com o serviço configurado
  - Encaminhamento de eventos
  - Adobe Experience Platform

## Criar um novo fluxo de dados

1. No painel esquerdo, em **Coleção de dados**, clique em **Sequências de dados**
1. Em seguida, clique em **Novo Datastream** para criar um

![Lista de Datastreams com o botão Novo Datastream realçado](assets/create-datastream-new-datastream-button.png)

## Configurar sequência de dados

Configure o fluxo de dados com as seguintes informações:

1. Nome -> **Datastream SB + \&lt;sandbox name> (ou seja, Datastream SB01)**
1. Esquema de Evento -> **dep: Web**
1. Alternar **em** todas as opções em **Geolocalização e Pesquisa de Rede**
1. Clique no botão **Salvar** quando terminar

>[!WARNING]
>
>Não clique em Salvar e Adicionar Mapeamento.  Se você acidentalmente, apenas cancele

![Formulário de configuração de sequência de dados com nome, esquema de evento e opções de pesquisa de localização geográfica definidos](assets/create-datastream-configure-datastream-form.png "Configurar a sequência de dados")



Depois de salvar o fluxo de dados, você verá a seguinte tela:

![Tela de confirmação exibida imediatamente após salvar a nova sequência de dados](assets/create-datastream-created-confirmation-screen.png "Tela final criada pela sequência de dados")

## Adicionar serviço de encaminhamento de eventos

Isso permite usar o encaminhamento de eventos para dados recebidos por essa sequência de dados.



1. Clique em **Adicionar serviço**

   ![Página de detalhes da sequência de dados com o botão Adicionar Serviço realçado](assets/create-datastream-add-service-button.png "Adicionar Serviço")

1. Configure os seguintes itens:

   - Serviço -> Encaminhamento de eventos
   - Propriedade -> Selecione a propriedade que você criou na etapa anterior.  Ele deve ser nomeado assim: Propriedade de encaminhamento de eventos SB + \&lt;número da sandbox>
   - Ambiente -> Desenvolvimento

1. Quando terminar, clique em **Salvar**

![Configuração do serviço de Encaminhamento de Eventos com propriedade e ambiente de Desenvolvimento selecionados](assets/create-datastream-event-forwarding-service-config.png "Tela de Configuração de Encaminhamento de Eventos")



## Adicionar serviço Adobe Experience Platform

Isso permite enviar dados para o Hub e chegar a um conjunto de dados para os dados recebidos por esse fluxo de dados.



1. Clique em **Adicionar serviço**

   ![A página de detalhes da sequência de dados com o botão Adicionar Serviço foi realçada para adicionar o serviço do Adobe Experience Platform](assets/create-datastream-add-second-service-button.png "Adicionar um novo serviço")

1. Configure os seguintes itens:

   - Serviço -> Adobe Experience Platform
   - Conjunto de dados do evento -> profundidade: Web
   - Conjunto de dados do perfil -> dep: Conta do cliente
   - Marque a caixa de seleção -> Segmentação do Edge
   - Marque a caixa de seleção -> Destino do Personalization

   ![Configuração do serviço Adobe Experience Platform com conjunto de dados do evento, conjunto de dados do perfil e caixas de seleção de segmentação definidas](assets/create-datastream-aep-service-config.png "Configurar Serviço")

1. Quando terminar, clique em **Salvar**.

1. A tela final deve ficar parecida com abaixo, com dois serviços presentes. **Copiar** e **salvar** a **ID da sequência de dados** no computador local (você a usará posteriormente no Postman)

![Configuração da sequência de dados final com os serviços Encaminhamento de Eventos e Adobe Experience Platform listados](assets/create-datastream-final-configuration-both-services.png "Configuração da sequência de dados final")
