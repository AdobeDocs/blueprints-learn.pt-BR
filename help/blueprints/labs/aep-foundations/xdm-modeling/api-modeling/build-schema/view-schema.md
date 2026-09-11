---
hold: true
title: Exibir esquema
description: Visualize um esquema de cliente recém-criado na interface do usuário do Experience Platform e por meio de uma chamada da API Obter esquema.
doc-type: article
solution: Experience Platform
exl-id: 29302546-46dc-4c97-8fd8-deab6977635c
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# Exibir esquema

## Visualização por meio da interface

1. Abra o navegador e navegue de volta para a seção `Schema -> Browse`.

>[!NOTE]
>
>Atualize a interface do usuário para visualizá-la, já que você acabou de criá-la e precisa consultar novamente o registro do esquema

2. Pesquisar o esquema `Sample Customer Schema - <your sandbox number>`

3. Observe que a classe necessária e os grupos de campos associados são adicionados ao esquema

![Exemplo de Esquema do Cliente exibido na interface do Experience Platform com seus grupos de classe e campo](assets/view-schema-ui-view-of-sample-customer-schema.png "Exibição da Interface do Usuário do Exemplo de Esquema do Cliente")


## Visualização por meio da API

1. Selecione a API `Step 5 - Get Customer Account Schema` clicando nela.
1. Na URL da solicitação, substitua `<replace me>` pelo `$meta:altId` que você salvou da seção anterior (Criar seu Esquema) ao final da chamada, como mostrado abaixo
1. Salve as edições feitas na solicitação
1. Execute a solicitação clicando no botão `Send`

![Etapa 5 - Obter chamada de API do Esquema da Conta do Cliente](assets/view-schema-step-5-get-customer-account-schema.jpeg "Etapa 5 - Obter Esquema da Conta do Cliente")



Exemplo de sua solicitação final após adicionar o `$meta:altId`

![Solicitação de Etapa 5 com o meta:altId anexado à URL](assets/view-schema-final-step-5-request.png "Solicitação de Etapa 5 Final")



Se você recebeu uma resposta `200 OK`, poderá navegar pelo esquema criado apenas através das lentes da estrutura XDM JSON

![Resposta OK de 200 mostrando o JSON do esquema completo da Conta do Cliente de Exemplo](assets/view-schema-sample-customer-account-schema.png "Esquema da Conta do Cliente de Exemplo")
