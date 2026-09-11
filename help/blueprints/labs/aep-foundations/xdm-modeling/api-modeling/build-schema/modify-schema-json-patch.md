---
title: Modificar esquema - Patch JSON
description: Use uma chamada à API JSON PATCH para adicionar um novo campo a um grupo de campos de locatário existente e ver a alteração refletida no esquema.
doc-type: article
solution: Experience Platform
exl-id: c0313594-d998-4525-a0a4-d9d844bed5ef
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---


# Modificar esquema - Patch JSON

## Visão geral

Considere por um minuto que, depois de criar o esquema, você precisa voltar e adicionar outro campo ao objeto `plan` chamado `planDescription`, pois você esqueceu de adicioná-lo no momento da criação ou foi uma solicitação recebida meses depois.  Para executar esta tarefa, basta executar uma operação `PATCH` que atualiza o esquema com o novo campo.

Você pode saber mais sobre o JSON PATCH nos links abaixo, mas para os fins deste laboratório, suponha que você tenha algum conceito de como isso funciona 😄

- [https://jsonpatch.com/](https://jsonpatch.com/)
- [Fundamentos da API do Experience League](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-fundamentals.html?lang=en#json-patch)

![Diagrama de correção de um campo planDescription ausente em um esquema existente](assets/modify-schema-json-patch-patching-missing-plan-description-field.png "Patch em uma Descrição de Plano de Campo Ausente")

>[!NOTE]
>
>Lembre-se dos seguintes pontos:
>
>- Um esquema é composto de uma (1) classe e um (1) ou mais grupos de campos
>- Não é possível adicionar novos campos diretamente a um esquema sem primeiro adicionar a um grupo de campos. Isso garante a reutilização de um campo em qualquer esquema que utilize esse grupo de campos.



Para adicionar um novo campo a um esquema, é necessário executar as seguintes operações em ordem.  Isso é o que você faz nas seguintes etapas do laboratório.

- Identifique o grupo de campos no qual você deseja adicionar a nova propriedade
- Construir uma chamada JSON PATCH para atualizar o grupo de campos
- Executar a chamada JSON PATCH para atualizar o grupo de Campos (que o esquema herdará)



## Localizar e identificar o grupo de campos a ser atualizado

1. Selecione a chamada de API `Step 1 - Get Tenant Field groups` localizada na pasta `XDM Schema Lab -> Customize Schema`
1. Execute a solicitação clicando no botão `Send`

   ![Etapa 1 - Obter solicitação de API de Grupos de Campos de Locatários](assets/modify-schema-json-patch-step-1-get-tenant-field-groups.png "Etapa 1 - Obter Grupos de Campos de Locatários")

   >[!NOTE]
   >
   >Lembre-se de que você criou o objeto `plan` em um grupo de campos personalizados. Os objetos criados personalizados no registro de esquema XDM são chamados de &quot;locatário&quot;, portanto, a chamada de API utiliza o caminho `/schemaregistry/tenant/mixins/`.



1. Na resposta, pesquise a ID do esquema do grupo de campos personalizado que você criou com o título anterior `Customer Account Details - Sandbox <your number here> `

1. Copie o `$meta:altId` e salve-o em um local seguro, pois ele será necessário para a próxima etapa

![Localizando o grupo de campos Detalhes da Conta do Cliente na resposta da API](assets/modify-schema-json-patch-search-field-group-response.jpeg "Pesquisar a resposta do Grupo de Campos Detalhes da Conta do Cliente")

>[!CAUTION]
>
>Selecione o grupo de campos correto para copiar.  Existe um com o mesmo nome `dep: Customer Account Details` que você deve **não** usar

>[!WARNING]
>
>Não continue até que você tenha salvo o `$meta:altId ` em algum lugar.  Ele será necessário em etapas futuras do laboratório



## Pesquisar o grupo de campos por $meta\:altId

1. Selecione a chamada à API `Step 2 - Fetch path for the object to be modified` na pasta `XDM Schema Lab -> Customize Schema`
1. Na URL da solicitação, substitua o `<replace me>` pelo `$meta:altId` que você salvou da etapa da seção anterior até o fim da chamada, como mostrado abaixo
1. Salve as edições feitas na solicitação
1. Execute a solicitação clicando no botão `Send`

![Etapa 2 - Buscar caminho para o objeto a ser modificado Chamada de API](assets/modify-schema-json-patch-step-2-fetch-object-path.jpeg "Etapa 2 - Buscar caminho para o objeto a ser modificado etapas")



Revise a resposta e observe que o caminho do ponteiro JSON para o objeto **plan** é construído usando cada uma das propriedades destacadas abaixo.

![Propriedades destacadas que compõem o caminho do ponteiro JSON para o objeto de plano](assets/modify-schema-json-patch-customer-account-details-path-to-the-plan-object.png "Caminho dos Detalhes da Conta do Cliente para o objeto de Plano")



O caminho totalmente composto se parece com o que você vê abaixo.  Copie este caminho e salve em algum lugar para referência

```none
/definitions/customFields/properties/_devbc/properties/plan/properties
```

>[!NOTE]
>
>Lembre-se de atualizar o nome do locatário acima (\_devbc) com o seu próprio



## PATCH do grupo de campos

### Amostra do corpo da API JSON PATCH

```none
[
    {
        "op": "",
        "path": "",
        "value": {
            "title": "",
            "type": "",
            "description": ""
        }
    }
]
```

- **op (Operação)** -> fornece a instrução para qual ação o PATCH deve executar
- **Caminho** -> este é o caminho que você deseja criar, atualizar ou excluir (isto é, este é o ponteiro JSON para o local do novo campo)
- **Valor** -> este campo é opcional e é usado somente ao criar ou substituir um campo existente



### Executar a solicitação de API

1. Clique na chamada à API `Step 3 - Modify Tenant Field group` na pasta `XDM Schema Lab -> Customize Schema`

   ![Etapa 3 - Modificar chamada de API do Grupo de Campos de Locatário](assets/modify-schema-json-patch-step-3-modify-tenant-field-group.png "Etapa 3 - Modificar Grupo de Campos de Locatário")



2. Atualize o corpo da solicitação com as seguintes informações

   - **op** ->` add`
   - **caminho** -> `path from previous step +`` the new field name`
   - **valor** ->
     - **título** -> `Plan Description`
     - **tipo** -> `string`
     - **descrição** -> `High-level details about the plan`

   Quando você terminar, sua solicitação de API deverá ser semelhante a esta

   ![O corpo da solicitação JSON PATCH foi concluído adicionando o campo planDescription](assets/modify-schema-json-patch-step-3-final-call-example.png "Etapa 3 - Exemplo de Chamada Final")

   >[!WARNING]
   >
   >Certifique-se de incluir o novo nome de campo, **planDescription,** no caminho



3. Se tudo estiver bem `Save`, sua chamada

4. `Execute` a chamada para executar o PATCH

Você deve ver uma resposta `200 OK ` e agora deve ver o campo `planDescription` em seu grupo de campos da seguinte maneira:

Resposta OK ![200 após corrigir com êxito o grupo de campos com planDescription](assets/modify-schema-json-patch-step-3-200-ok-successful-patch.png "Etapa 3 - 200 OK PATCH com Êxito")

>[!TIP]
>
>Parabéns! Você atualizou com êxito um grupo/esquema de campos usando o JSON PATCH



## Visualizar a alteração na interface do usuário

Navegue pelo esquema na interface do usuário e observe o campo recém-adicionado.  Muito legal, não é?

![Campo Descrição do plano visível no esquema após o patch de JSON na interface do usuário do Experience Platform](assets/modify-schema-json-patch-plan-description-added-to-field-group.png "Campo Descrição do plano adicionado ao grupo de campos Detalhes da conta do cliente - Sandbox \&lt;seu número>. Modificar JSON de Esquema")
