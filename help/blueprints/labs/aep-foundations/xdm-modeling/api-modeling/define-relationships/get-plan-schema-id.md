---
hold: true
title: Obter ID do Esquema do Plano
description: Consulte a API do registro do esquema do locatário para localizar e salvar a $id do esquema de pesquisa Plano para uso em um descritor de relacionamento.
doc-type: article
solution: Experience Platform
exl-id: f66e0483-b5b3-4493-b752-c4e00211a8bd
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# Obter ID do Esquema do Plano

## Listar todos os esquemas de locatário

1. Clique na solicitação de API `Step 1 - Get Lookup Schemas` na pasta `XDM Schema Lab -> Create Relationship Descriptors`
1. Execute a API clicando no botão `Send`

![Etapa 1 - Obter solicitação da API de Esquemas de Pesquisa](assets/get-plan-schema-id-step-1-get-lookup-schemas.jpeg "Etapa 1 - Obter Esquemas de Pesquisa")

>[!NOTE]
>
>Essa chamada GET busca todos os esquemas existentes na parte &quot;locatário&quot; do registro do esquema (ou seja, esquemas criados personalizados). Precisamos pesquisar apenas pelo esquema **Plano** para que possamos relacioná-lo ao esquema Conta do Cliente.



## Identificar o esquema de plano

1. Pesquisar o esquema `dep: Plan [Lookup] ` na resposta de chamadas
1. Copie o `$id` do esquema e salve-o em algum lugar para referência futura

![A $id do esquema de Pesquisa de Plano localizada na resposta da API](assets/get-plan-schema-id-dep-lookup-plan-schema-sid.png "dep: $id do esquema de Plano de Pesquisa")

>[!NOTE]
>
>Este esquema já deve estar pré-implantado em sua sandbox

>[!WARNING]
>
>Não continue até que tenha salvo `$id` do esquema em algum lugar.  Será necessário criar posteriormente o Descritor de relacionamento
