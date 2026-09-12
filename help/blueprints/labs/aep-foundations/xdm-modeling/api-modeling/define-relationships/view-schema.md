---
title: Exibir esquema
description: Visualize a relação de pesquisa do esquema da Conta do cliente com o esquema do Plano por meio da interface do usuário do esquema e da API Obter esquema.
doc-type: article
solution: Experience Platform
exl-id: dae48ef4-f762-4173-8564-c1ad40c0109b
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Exibir esquema

## Visualização por meio da interface

1. Abra o navegador e navegue de volta para a seção `Schema -> Browse`.
1. Pesquisar o esquema `Sample Customer Schema - <your sandbox number>`
1. Observe que a relação com `dep: Plan [Lookup]` está definida

![Exemplo de esquema do cliente na interface do usuário do Experience Platform mostrando a profundidade: relação de Pesquisa de Plano](assets/view-schema-relationship-to-plan-lookup-schema.png)


## Visualização por meio da API

1. Selecione a API `Step 4 - Get Customer Account Schema and its descriptors` clicando nela

   ![Etapa 4 - Obter Esquema de Conta do Cliente e chamada à API de seus descritores](assets/view-schema-step-4-get-schema-and-descriptors.png "Etapa 4 - Obter Esquema de Conta do Cliente e seus descritores")



2. Na URL da solicitação, substitua `<replace me>` pelo `$meta:altId` que você salvou da seção anterior [Criar Esquema](../build-schema/create-schema.md), conforme mostrado abaixo

   ![Solicitação de Etapa 4 com o meta:altId anexado à URL](assets/view-schema-final-step-4-request.png "Solicitação de Etapa 4 Final")



3. Salve a solicitação usando o botão `Save`

4. Execute a solicitação clicando no botão `Send`

Agora você deve ver uma resposta de `200 OK` e navegar até o final do esquema criado para ver a Identidade através das lentes da estrutura JSON do XDM



![Descritor de relacionamento visível no JSON de esquema de Conta de Cliente](assets/view-schema-relationship-descriptor.png "Descritor de Relacionamento")



![Descritor de identidade de referência visível no JSON de esquema da conta do cliente](assets/view-schema-reference-identity-descriptor.png "Descritor de identidade de referência")
