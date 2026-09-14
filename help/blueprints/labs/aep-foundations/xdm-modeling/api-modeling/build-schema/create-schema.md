---
title: Criar esquema
description: Use a API do registro de esquema para montar um esquema do cliente a partir de uma classe de perfil e referências de grupos de campos padrão e personalizado.
doc-type: article
solution: Experience Platform
exl-id: 78ebc5b8-d088-48e9-857f-87085a87a280
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%
---

# Criar esquema

## Modificar o corpo da API

>[!CAUTION]
>
>**Não executar a chamada ainda**

1. Clique na chamada à API `Step 4 - Create Customer Account Schema` na pasta `XDM Schema Lab -> Create Schema`.

   ![Etapa 4 - Criar chamada de API de Esquema de Conta de Cliente na coleção do Postman](assets/create-schema-click-on-the-step-4-create-customer-account-schema.png)



2. Abra o corpo da chamada e visualize a estrutura de como um esquema é definido. Lembre-se de que um esquema é sempre composto de apenas uma (1) classe e um ou mais grupos de campos.

3. Preencha os campos `title` e `description` no corpo do esquema com o seguinte:

   - Título -> `Sample Customer Schema - <your sandbox number>`
   - Descrição -> `Sample Customer Schema - <your sandbox number>`

4. Preencha os campos `$ref` com o `$ids` que você salvou das seções de laboratório anteriores que você concluiu: [Criar grupos de campos personalizados](./create-custom-field-groups.md) e [Obter classe de perfil](./get-profile-class.md). Você tem $ids para cada um dos seguintes itens:

   - Classe -> Perfil individual XDM
   - Grupo de campos -> Detalhes demográficos
   - Grupo de campos -> Detalhes de contato pessoal
   - Grupo de campos -> Detalhes de consentimento e preferência
   - Grupo de campos (personalizado) -> Detalhes da conta do cliente

   ![Corpo de solicitação de esquema vazio antes de adicionar referências de classe e grupo de campos](assets/create-schema-empty-schema-api-body.png "Corpo de API de Esquema vazio")



5. Revise seu corpo final e certifique-se de que seja semelhante a este

![Corpo concluído da solicitação de esquema com título, descrição e todos os valores $ref preenchidos](assets/create-schema-example-of-final-body-payload.png "Exemplo de carga do corpo final")

>[!NOTE]
>
>A ordem de `$refs` não importa nem a localização de `title` e `description` no corpo.



## Executar a API

1. Salve as modificações na solicitação de API antes de continuar.
1. Execute a API clicando no botão `Send`

Uma resposta bem-sucedida para criar o esquema deve resultar em um status `201 Created` e deve se parecer com a imagem abaixo

>[!WARNING]
>
>Não executar a solicitação novamente se for bem-sucedido

![201 Resposta criada após a criação com êxito do esquema por meio da API de Etapa 4](assets/create-schema-sample-response-from-executing-the-step-4-api.png "Resposta de exemplo da execução da API de Etapa 4")


## Localize e salve o esquema $id

1. Depois de executar a solicitação de API, copie o `$id` e `$meta:altId` da resposta
1. Salve os valores em algum lugar para reutilizá-los posteriormente

>[!WARNING]
>
>Não continue até que você tenha salvo `$id` e `$meta:altId` em algum lugar.  Eles serão necessários em etapas futuras do laboratório

>[!SUCCESS]
>
>**Parabéns! Você criou um esquema usando apenas as APIs**
