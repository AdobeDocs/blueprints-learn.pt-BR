---
hold: true
title: Recapitulação
description: Revise as etapas do laboratório de modelagem de API, desde a criação do esquema da conta do cliente até a aplicação de patches JSON, marcação de identidades e criação de uma relação de pesquisa.
doc-type: article
solution: Experience Platform
exl-id: 0279cd68-af7b-43b4-8c6c-d8f8f96f0c0e
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# Recapitulação

O vídeo abaixo recapitula como você criou o esquema, as identidades e os descritores de relacionamento por meio de chamadas de API e demonstra como o Patch JSON é usado para modificar um esquema.

>[!VIDEO](https://video.tv.adobe.com/v/3459564/?quality=12&learn=on)

&#x200B;> [!TIP]
>
>Primeiro de parabéns! Criar coisas por meio da API não é fácil, mas entender como funciona ajudará você a entender o sistema como um todo. Parabéns!



## Criação do esquema de conta do cliente

Você criou o esquema por `$ref`, os grupos de campos criados pela Adobe e seu próprio grupo de campos criado de forma personalizada (ou seja, locatário).  Você também `$ref` a classe que o esquema deve representar (ou seja, Perfil individual XDM)

![Esquema de Conta de Cliente fazendo referência a grupos de campos e classe via $ref](assets/recap-customer-account-schema.png "Esquema de Conta de Cliente")


## Correção JSON do esquema da Conta do cliente

Você usou o método de patch de JSON para modificar o esquema da Conta do cliente para adicionar um novo campo ao objeto do plano. Você fez isso corrigindo o grupo de campos personalizados `$ref` chamado `Customer Account Details` que você definiu em [Criar grupos de campos personalizados](build-schema/create-custom-field-groups.md), em vez de corrigir o próprio esquema.

![Solicitação de patch JSON adicionando um campo planDescription ao grupo de campos Detalhes da Conta do Cliente](assets/recap-json-patch-plan-description-field.png "Patch JSON do campo planDescription")


## Campos de identidade marcados

Nesta etapa, você executou duas das mesmas chamadas de `POST` para criar `Identity Descriptors` para os campos `_devbc.customerID` e `personalEmail.address` no esquema da Conta do cliente.

1. O campo `_devbc.customerID` foi definido como a identidade **primária**
1. O campo `personalEmail.address` **não foi definido** como um campo principal

![Esquema da conta do cliente mostrando os descritores de identidade principal e não principal](assets/recap-marked-identity-fields.png "campos de identidade do esquema da conta do cliente")

## Relação de pesquisa criada

A última etapa foi criar a relação entre os esquemas de Conta do cliente e Plano do XDM ERD no Paper Lab.  Isso exigia que você criasse um descritor de relacionamento (ou seja, como relacionar o esquema `Customer Account` ao esquema `dep: Plan [Lookup]`) e um descritor de identidade de referência no esquema Conta de cliente.

![Descritor de relacionamento e descritor de identidade de referência que vinculam a conta do cliente ao esquema de pesquisa do plano](assets/recap-relationship-reference-identity-descriptors.png "Descritores de identidade de relacionamento e referência")

>[!NOTE]
>
>O descritor `referenceIdentity` informa ao Perfil de Cliente em Tempo Real qual campo do esquema `Customer Account` corresponde a qual namespace de identidade. Lembre-se de que, ao definir um esquema de pesquisa, você deve marcar um campo como uma identidade primária e atribuir a ele um namespace com um tipo de `non-person`.
