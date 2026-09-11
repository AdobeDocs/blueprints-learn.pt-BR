---
hold: true
title: Coleção de API
description: Baixe e importe a coleção de APIs do Postman do bootcamp que contém as solicitações usadas nos laboratórios do AEP Foundations.
doc-type: article
solution: Experience Platform
exl-id: 18d820c5-56ad-46b8-a9cf-f725555d2db3
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Coleção de API

## Arquivo de coleção da API do Postman

Baixar arquivo — [AEP Foundations Bootcamp (Labs).postman_collection.json](assets/aep-foundations-bootcamp-labs.postman_collection.json)



## Importar coleção de API

1. Abra o `Postman API Collection File` no navegador clicando no arquivo
1. Copie o URL do arquivo para a área de transferência
1. Inicie o Postman no computador local e clique no botão `Import` no espaço de trabalho
1. Cole a URL de `Postman API Collection File` na caixa de texto modal de importação na sobreposição.  Isso deve acionar uma importação automática

![Clicar no botão Importar no espaço de trabalho do Postman para importar a coleção de API](assets/api-collection-click-import-button.png "Botão Importar")



![Colando a URL do arquivo de coleção de API na caixa de texto modal de importação do Postman](assets/api-collection-import-modal-paste-url.png "Caixa de Texto Modal do Botão de Importação")

Agora você deve ver uma coleção preenchida na guia `Collections` da barra lateral esquerda chamada `AEP Foundations Bootcamp`



![Coleção Bootcamp do AEP Foundations preenchida na guia da barra lateral Coleções do Postman](assets/api-collection-imported-collection-in-sidebar.png)

## Visão geral da coleção AEP Foundations Bootcamp

A coleção de API importada contém todas as chamadas de API necessárias que serão necessárias para laboratórios em toda a inicialização.  Cada laboratório é organizado em uma pasta específica com seu próprio conjunto de APIs.  Esteja ciente disso ao trabalhar nos laboratórios esta semana.

Detalhes sobre cada pasta podem ser encontrados abaixo:

- **Autenticação do IMS** - contém uma única solicitação para gerar um access\_token que é necessário ao trabalhar com qualquer uma das APIs do Adobe Experience Platform
- **Laboratório de esquemas do XDM** - contém um conjunto de solicitações para criar os componentes XDM necessários para criar e configurar um esquema para o Perfil de cliente em tempo real
- **Laboratório de assimilação de dados** - contém um conjunto de solicitações para transmitir dados para a Experience Platform
- **Laboratório de perfis** - contém um conjunto de solicitações para visualizar as características e comportamentos do Perfil do cliente em tempo real

>[!TIP]
>
>Parabéns!  Você importou com êxito a coleção de Postman do bootcamp
