---
title: Criar grupos de campos personalizados
description: Use a API de registro do esquema para criar um grupo de campos Detalhes da conta do cliente personalizado e salvar sua $id para uso em um esquema posterior.
doc-type: article
solution: Experience Platform
exl-id: d3262db9-7c0b-476a-843f-1a2c224ee792
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# Criar grupos de campos personalizados

## Estrutura do grupo de campos

Um grupo de campos é sempre composto pelos seguintes campos. Você verá isso na solicitação na próxima etapa.

| Valores obrigatórios | Descrição |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| título | O nome do grupo de campos que você deseja criar no registro do esquema. Observe que o nome DEVE SER ÚNICO. |
| descrição | Uma breve descrição sobre a finalidade do grupo de campos |
| type | Sempre um objeto |
| meta\:intendedToExtend | Define com quais classes o grupo de campos pode ser usado. As classes são sempre referenciadas por seu valor `$id` |
| allOf | Descreve os recursos que podem ser incluídos no grupo de campos. Para campos definidos pelo cliente, o caminho é sempre `#/definitions/customFields` |
| definitions.customFields... | Essa é a estrutura padrão do esquema JSON necessária para criar grupos de campos personalizados. Deve corresponder ao `allOf` de cima |
| \&lt;LOCATÁRIO\_NOME> | O nome do locatário (ou seja, nome exclusivo) é criado durante o processo de provisionamento. Isso garante que qualquer personalização feita não entre em conflito com alterações existentes ou futuras no registro do esquema do Adobe |



## Grupo de campos Criar Detalhes da Conta do Cliente

1. Clique na chamada à API `Step 2 - Create Customer Account Details Field Group` da solicitação na pasta `XDM Schema Lab -> Create Schema`



![Etapa 2 - Criar solicitação de API do Grupo de Campos de Detalhes da Conta do Cliente](assets/create-custom-field-groups-step-2-field-group-request.png "Etapa 2 - Criar Grupo de Campos de Detalhes da Conta do Cliente")



Revise o corpo da solicitação antes de executar. Observe que os campos obrigatórios mencionados na seção Estrutura do grupo de campos são exibidos da seguinte maneira:

![Campos obrigatórios de um grupo de campos personalizado, conforme mostrado no corpo da solicitação](assets/create-custom-field-groups-field-group-structure.png "Estrutura do grupo de campos")



![A propriedade allOf que faz referência ao caminho de definições de campo personalizado](assets/create-custom-field-groups-field-group-structure-allof.png "Estrutura do Grupo de Campos allOf")

>[!NOTE]
>
>Observe como na imagem à direita acima, o `allOf` faz referência ao caminho de &quot;/definitions/customFields&quot;.  Isso deve corresponder à estrutura definida no esquema (imagem à esquerda), pois informa ao sistema XDM onde localizar os objetos criados personalizados.
>
>![Comparação que destaca como o caminho allOf deve corresponder ao caminho de definições de campo personalizado](assets/create-custom-field-groups-allof-path-highlighted.png)



Observe também como cada campo específico da folha de mapeamento é fundamentado na estrutura XDM JSON.



![Notação de ponto do plano da planilha de mapeamento convertida em estrutura XDM JSON](assets/create-custom-field-groups-plan-dot-notation-to-xdm-json.png "Notação de ponto do plano em XDM JSON")



![Conta da planilha de mapeamento e notação de ponto da ID do cliente convertidas em XDM](assets/create-custom-field-groups-account-customer-id-dot-notation-to-xdm.png "Conta e ID do cliente em notação de ponto para XDM")



2. Atualize os `title` e `description` para o grupo de campos usando o seguinte formato: `Customer Account Details - Sandbox <your number here>`



   ![Exemplo de título e descrição preenchidos para o grupo de campos personalizado](assets/create-custom-field-groups-field-group-title-description-example.png "Título do Grupo de Campos e Exemplo de Descrição")



3. Execute clicando no botão `Send`.  Você deve ver uma resposta semelhante à captura de tela abaixo.

4. Copie o valor `$id` do grupo de campos Detalhes da Conta do Cliente recém-criado.

![Resposta de API bem-sucedida após a criação do grupo de campos personalizado](assets/create-custom-field-groups-step-2-create-custom-field-group-success.png "Etapa 2 - Êxito ao Criar Grupo de Campos Personalizado")

>[!WARNING]
>
>Não continue até que você tenha salvo o `$id` em algum lugar.  Será necessário posteriormente criar o esquema da Conta do cliente
>
>
