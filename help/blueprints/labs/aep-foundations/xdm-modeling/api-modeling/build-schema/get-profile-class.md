---
title: Obter Classe de Perfil
description: Chame a API do registro do esquema global para recuperar e salvar a $id da classe Perfil individual XDM para uso em um esquema personalizado.
doc-type: article
solution: Experience Platform
exl-id: d87c21a2-dad4-4666-b917-cdf8e16058d4
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# Obter Classe de Perfil

## Execute a etapa 3 - Obter classe de perfil

1. Clique na solicitação `Step 3 - Get Profile Class` na pasta `XDM API Lab -> Create Schema`
1. Executar clicando no botão `Send`

![Etapa 3 - Obter solicitação de API de Classe de Perfil](assets/get-profile-class-step-3-api-request.jpeg "Etapa 3 - Obter Solicitação de API de Classe de Perfil")

>[!NOTE]
>
>Observe que na solicitação GET, o caminho `global`: .../schemaregistry/**global**/classes. Lembre-se de que o uso de `global` informa ao registro do esquema que queremos retornar apenas objetos XDM padrão do Adobe


## Localize e salve a classe $id

Depois de executar a solicitação de API, execute as seguintes etapas para localizar e salvar o `$id` para a classe de Perfil Individual XDM.

1. Pesquisar a classe `XDM Individual Profile` na resposta
1. Copie o `$id` da classe `XDM Individual Profile` e salve-o em algum lugar que você possa fazer referência mais tarde.

![Classe de Perfil Individual XDM localizada na resposta da API](assets/get-profile-class-xdm-individual-profile-class.png "Classe de Perfil Individual XDM")

>[!WARNING]
>
>Não continue até que você tenha salvo o `$id` em algum lugar.  Será necessário posteriormente criar o esquema da Conta do cliente
