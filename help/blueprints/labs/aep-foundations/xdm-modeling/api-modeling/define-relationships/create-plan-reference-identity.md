---
title: Criar Identidade de Referência do Plano
description: Use a API do registro do esquema para criar um descritor de identidade de referência no esquema de pesquisa para que ele possa ser usado na segmentação em lote.
doc-type: article
solution: Experience Platform
exl-id: b3b8f480-af3b-4bf8-b74e-3842f59691b6
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%
---

# Criar Identidade de Referência do Plano

1. Clique na solicitação de API `Step 3 - Reference Descriptor for Plan` na pasta `XDM Schema Lab -> Create Relationship Descriptors`

   >[!CAUTION]
   >
   >Não executar a solicitação...ainda

   ![Etapa 3 - Descritor de Referência para a solicitação de API de esquema de Plano](assets/create-plan-reference-identity-step-3-descriptor-request.jpeg "Etapa 3 - Descritor de Referência para o esquema de Plano")



2. Atualize as seguintes propriedades no corpo da chamada de API.

- Atualize o valor da propriedade `xdm:sourceSchema` para o `$id` do esquema `Customer Account` salvo da etapa [Criar Esquema](../build-schema/create-schema.md)
- Atualize o valor de `xdm:sourceProperty` para o caminho do campo `planID` do esquema `Customer Account`

>[!NOTE]
>
>Use o valor da notação de pontos do campo `planId` do esquema `dep: Lookup Plan` e substitua `.` por `/`
>
>Não esqueça o `/` principal 😄

SOMENTE EXEMPLO

```json
{
  "@type": "xdm:descriptorReferenceIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/_devbc/plan/planID",
  "xdm:identityNamespace": "planID"
}
```

>[!NOTE]
>
>Lembre-se de atualizar o nome do locatário acima (\_devbc) com seu próprio



&#x200B;3. Salve sua solicitação antes de continuar usando o botão `Save`

&#x200B;4. Execute a API clicando no botão `Send`

Agora você verá uma resposta de `201 Created` como a seguir

![201 Resposta criada após a criação da dep: Descritor de identidade de referência de Pesquisa de Plano](assets/create-plan-reference-identity-dep-plan-descriptor-result.png "dep: Descritor de identidade de referência de Pesquisa de Plano")

>[!NOTE]
>
>Um descritor de identidade de referência é sempre definido no esquema de pesquisa (ou seja, sourceSchema)

>[!NOTE]
>
>Os descritores de identidade de referência são criados automaticamente no servidor ao criar relações a partir da interface do usuário de esquema. **Você só precisa criá-los explicitamente ao utilizar as APIs para criar esquemas**

>[!SUCCESS]
>
>Fantástico! Para relacionar o esquema `dep: Lookup Plan` ao esquema `Customer Account` e permitir que ele seja referenciado durante a segmentação em lote, você criou todos os descritores necessários
