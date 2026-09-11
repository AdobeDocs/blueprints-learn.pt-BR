---
title: Criar outras identidades
description: Use a API de registro de esquema para criar um descritor de identidade de endereço de email não primário para o esquema Conta do cliente.
doc-type: article
solution: Experience Platform
exl-id: 22c40299-fb93-4d41-a23b-f8629df3e7b9
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Criar outras identidades

1. Clique na chamada à API `Step 2 - Create Email Address Identity for Customer Account Schema` na pasta `XDM Schema Lab -> Create Identity Descriptors`

   >[!CAUTION]
   >
   >Não executar a solicitação...ainda

   ![Etapa 2 - Criar identidade de endereço de email para solicitação do Postman de esquema de conta do cliente](assets/create-other-identities-step-2-postman-request.jpeg "Etapa 2 - Criar descritor de identidade de endereço de email")



1. Atualize o valor `xdm:sourceSchema` no corpo da solicitação usando o `$id` que você salvou da etapa do laboratório [Criar esquema](../build-schema/create-schema.md)

1. Atualize o valor `xdm:isPrimary` no corpo da solicitação para `false`

   SOMENTE EXEMPLO

   ```json
   {
     "@type": "xdm:descriptorIdentity",
     "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
     "xdm:sourceVersion": 1,
     "xdm:sourceProperty": "/personalEmail/address",
     "xdm:namespace": "Email",
     "xdm:property": "xdm:code",
     "xdm:isPrimary": false
   }
   ```

   >[!NOTE]
   >
   >Lembre-se de atualizar o nome do locatário acima (\_devbc) com seu próprio



1. Salve sua solicitação antes de continuar usando o botão `Save`

1. Execute a API clicando no botão `Send`. Agora você deve ver uma resposta de `201 Created` como a seguir

![Resposta criada após a criação bem-sucedida do descritor de identidade de endereço de email](assets/create-other-identities-201-created-response.png "Descritor de Identidade Bem-sucedido do Endereço de Email")
