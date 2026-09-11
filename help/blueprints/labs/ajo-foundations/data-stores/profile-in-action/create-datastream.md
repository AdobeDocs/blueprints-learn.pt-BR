---
hold: true
title: Criar sequência de dados
description: Saiba como criar e configurar um fluxo de dados com os serviços do Adobe Experience Platform, Offer Decisioning e Journey Optimizer para habilitar o processamento de eventos do Edge.
doc-type: article
solution: Experience Platform
exl-id: 37873340-476a-4303-886d-de4835bba8df
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---


# Criar sequência de dados

## Objetivo de aprendizado

Crie e configure uma sequência de dados com os serviços necessários para habilitar o processamento de eventos do Edge.

Uma sequência de dados define quais serviços a utilizarão.

- Ao enviar dados para a Edge, você especifica qual sequência de dados usar
- Os dados enviados para esses Datastreams podem agir de acordo com o serviço configurado
  - Adobe Experience Platform

## Criar um novo fluxo de dados

1. No painel esquerdo, em **Coleção de dados**, clique em **Sequências de dados**
1. Em seguida, clique em **Novo Datastream** para criar um

![Lista de Datastreams com o botão Novo Datastream realçado](assets/create-datastream-new-datastream-button.png)

## Configurar sequência de dados

Configure o fluxo de dados com as seguintes informações:

1. Nome -> **Datastream SB + \&lt;sandbox name> (ou seja, Datastream SB01)**
1. Esquema de Mapeamento -> **dep: Web**
1. Ative **em** todas as opções em **Geolocalização e Pesquisa de Rede** se desejar capturar essas informações.
1. Clique no botão **Salvar** quando terminar

>[!WARNING]
>
>Não clique em Salvar e Adicionar Mapeamento.  Se você acidentalmente fizer isso, basta cancelar

![Formulário de configuração de sequência de dados com campos de nome e esquema de mapeamento](assets/create-datastream-configure-datastream-form.png "Configurar a sequência de dados")



Depois de salvar o fluxo de dados, você verá a seguinte tela:

![Tela de confirmação após salvar a nova sequência de dados](assets/create-datastream-created-confirmation.png "Tela final criada pela sequência de dados")

## Adicionar serviço Adobe Experience Platform

Isso permite enviar dados para o Hub e chegar a um conjunto de dados para os dados recebidos por esse fluxo de dados.

1. Clique no botão azul **Adicionar serviço** localizado no meio da tela

![Botão Adicionar Serviço na tela de configuração da sequência de dados](assets/create-datastream-add-service-button.png)

&#x200B;2. Configure os seguintes itens:
   - **Serviço** -> `Adobe Experience Platform`
   - **Conjunto de Dados do Evento** -> `dep: Web`
   - **Conjunto de Dados de Perfil** -> `dep: Customer Account`
   - **Marcar Caixa de Seleção** -> `Offer Decisioning`
   - **Marcar Caixa de Seleção** -> `Adobe Journey Optimizer`
&#x200B;3. Quando terminar, clique em **Salvar**

![Caixa de diálogo de configuração do serviço Adobe Experience Platform com campos de conjunto de dados de evento e perfil](assets/create-datastream-configure-aep-service.png)

Você vê o serviço agora adicionado ao seu fluxo de dados

![Serviço Adobe Experience Platform adicionado à sequência de dados](assets/create-datastream-aep-service-added.png "Serviço Adobe Experience Platform adicionado à sequência de dados")

**Copiar** e **salvar** a **ID da sequência de dados** no computador local (vamos usá-la posteriormente no Postman)

![Campo de ID da sequência de dados a ser copiado e salvo para uso posterior](assets/create-datastream-copy-datastream-id.png)

## Recapitulação

Você deve ter uma sequência de dados em funcionamento com o serviço Adobe Experience Platform configurado.
