---
title: Criar identidade principal
description: Use a API de registro do esquema para criar um descritor de identidade primário de customerID para o esquema de Conta de cliente.
doc-type: article
solution: Experience Platform
exl-id: db690081-e857-4875-8bb9-7ac197d73cab
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# Criar identidade principal

1. Clique na solicitação de API `Step 1 - Create Primary Identity for Customer Account Schema` na pasta `XDM Schema Lab -> Create Identity Descriptors`

   ![Etapa 1 - Criar identidade principal para solicitação Postman de esquema de conta do cliente](assets/create-primary-identity-step-1-postman-request.jpeg "Etapa 1 - Criar identidade principal para esquema de conta do cliente")

   >[!CAUTION]
   >
   >Não executar a solicitação ainda



1. Atualize o valor `xdm:sourceSchema` no corpo da solicitação usando o `$id` que você salvou da etapa do laboratório [Criar esquema](../build-schema/create-schema.md)

1. Atualize o valor `xdm:isPrimary` no corpo da solicitação para `true`

   SOMENTE EXEMPLO

   ```json
   {
     "@type": "xdm:descriptorIdentity",
     "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
     "xdm:sourceVersion": 1,
     "xdm:sourceProperty": "/_devbc/customerID",
     "xdm:namespace": "customerID",
     "xdm:property": "xdm:code",
     "xdm:isPrimary": true
   }
   ```

   >[!NOTE]
   >
   >Lembre-se de atualizar o nome do locatário acima (\_devbc) com seu próprio



1. Salve sua solicitação antes de continuar usando o botão `Save`

1. Execute a API clicando no botão `Send`. Agora você deve ver uma resposta de `201 Created` como a seguir

![201 Resposta criada após a criação bem-sucedida do descritor de identidade primário](assets/create-primary-identity-201-created-response.png "Descritor de identidade primário criado com êxito")

>[!TIP]
>
>Parabéns!  Você acabou de criar um descritor de identidade primário em seu esquema
