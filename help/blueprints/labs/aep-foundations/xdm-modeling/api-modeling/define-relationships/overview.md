---
hold: true
title: Definir Relações
description: Saiba como os descritores de relacionamento vinculam um esquema do cliente a um esquema de pesquisa no registro do esquema XDM por meio da API.
doc-type: overview-page
solution: Experience Platform
exl-id: be672c84-09ac-4941-b40e-da7bd3fd6704
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Definir Relações

## Descritores de relacionamento

Para criar uma relação de um esquema com outro, é necessário criar um Descritor de relacionamento no registro do esquema. Uma amostra do corpo do descritor de esquema é semelhante ao seguinte:

Descritor individualizado

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/_devbc/plan/planID",
  "xdm:destinationSchema": "https://ns.adobe.com/devbc/schemas/6470f71181cf87aa39c2c2c43824eaa15f523652f7f88ff7",
  "xdm:destinationVersion": 1
}
```

Descritor de identidade de referência

```json
{
  "@type": "xdm:descriptorReferenceIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/6470f71181cf87aa39c2c2c43824eaa15f523652f7f88ff7",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/_devbc/plan/planID",
  "xdm:identityNamespace": "planID"
}
```

## Seu objetivo

Criar identidades de relacionamento para o Esquema de conta do cliente. Depois de executar as etapas na próxima seção, seu esquema deve ter a aparência abaixo.

![Esquema da conta do cliente mostrando os descritores de identidade de referência e relacionamento](assets/overview-schema-with-relationship-identities.png)
