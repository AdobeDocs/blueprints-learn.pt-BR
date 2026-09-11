---
hold: true
title: Marcar campos de identidade
description: Saiba como os descritores de identidade marcam campos de esquema como identidades primárias ou não primárias usando a API do registro do esquema XDM.
doc-type: overview-page
solution: Experience Platform
exl-id: f6498584-0f4d-4baf-86b5-b00cc78e2ba7
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# Marcar campos de identidade

## Descritores de identidade

Para marcar um campo como uma identidade, você precisa criar um Descritor de identidade no registro do esquema. Uma amostra do corpo do descritor de esquema é semelhante ao seguinte:

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

- **@type** -> sempre definido como `xdm:descriptorIdentity`
- **xdm\:sourceSchema** -> o `$id` do esquema em que o campo existe
- **xdm\:sourceVersion** -> sempre 1
- **xdm\:sourceProperty** -> caminho do campo dentro do esquema
- **xdm\:namespace** -> o código do namespace de identidade em que o campo deve ser armazenado
- **xdm\:property** -> sempre `xdm:code`
- **xdm\:isPrimary** -> se for uma identidade primária, `true` caso contrário será `false`


## Seu objetivo

Crie as identidades primária e não primária para o Esquema da conta do cliente. Depois de executar as etapas na próxima seção, seu esquema deve ter a aparência abaixo.

![Esquema da conta do cliente após criar descritores de identidade primários e não primários](assets/overview-schema-with-primary-and-non-primary-identities.png)
