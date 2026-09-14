---
title: Objetos personalizados do modelo
description: Crie campos e objetos personalizados de conta, plano e customerID no editor de esquema, incluindo valores de enumeração, para modelar dados sem equivalente de grupo de campos padrão.
doc-type: article
solution: Experience Platform
exl-id: 8c39b226-05f3-458a-b023-c59221a6713a
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 0%
---

# Objetos personalizados do modelo

## Adição de campos personalizados

Conforme discutido na palestra, não há grupos de campos padrão pré-criados ou tipos de dados que modelem os campos personalizados da Conta do cliente.  Os campos abaixo atualmente são considerados personalizados e devem ser modelados dentro do esquema XDM.

- \_\&lt;nome-do-locatário>.account.createDate
- \_\&lt;nome-do-locatário>.account.endDate
- \_\&lt;nome-do-locatário>.account.acqSource
- \_\&lt;nome-do-locatário>.plan.planID
- \_\&lt;nome-do-locatário>.plan.name
- \_\&lt;nome-do-locatário>.customerID

>[!NOTE]
>
>Observe que \&lt;nome-do-locatário> é específico para o ambiente em que você está trabalhando



## Criação do objeto Account

1. Adicione um novo campo clicando no botão **+ (adicionar)** na parte superior do esquema

   ![Botão Adicionar (+) na parte superior do esquema para adicionar um campo personalizado](assets/model-custom-objects-add-a-custom-field-to-your-schema.png)

   >[!NOTE]
   >
   >Observe que o painel direito abre com alguns campos para você preencher



1. Crie o objeto de conta usando os detalhes abaixo. Quando terminar, clique no botão **Aplicar** no painel direito para ver a alteração no espaço de trabalho de esquema

| Nome do campo | Nome de exibição | Tipo | Atribuir a um novo grupo de campos |
| ---------- | ------------ | -------- | ----------------------------------------------------------------------------------------------------------------------------- |
| *conta* | *Conta* | *Objeto* | *Detalhes da Conta do Cliente - \[Suas Iniciais]*<br />*(digite isto e selecione a lista suspensa ou pressione Enter)* |

>[!WARNING]
>
>Os nomes de campo precisam seguir uma capitalização específica. O motivo é que o mesmo esquema que você está criando já foi pré-criado. Se sua caixa estiver desativada, isso causará um conflito com os caminhos de campo do esquema pré-existente na sandbox

![Adicionando o objeto de conta com seu grupo de campos atribuído](assets/model-custom-objects-adding-the-account-object.png "Adicionando o objeto de conta")

>[!NOTE]
>
>Observe que o campo personalizado criado automaticamente é colocado em um namespace de locatário, indicado por `_devbc` na captura de tela. O namespace do locatário pode ser diferente. Os namespaces do locatário são usados para diferenciar objetos personalizados dos objetos padrão do Adobe e garantir que adições/atualizações futuras nos padrões do Adobe não entrem em conflito com os objetos criados de forma personalizada.

>[!NOTE]
>
>Observe que o novo grupo de campos personalizados aparece no painel esquerdo sob `Field groups` sem um ícone de cadeado.  Esse ícone de bloqueio ausente indica que é um grupo de campos criado de forma personalizada.

>[!WARNING]
>
>Não é possível salvar seu esquema neste momento. Se você fizer isso, ocorrerá um erro porque não é possível criar um objeto vazio no esquema JSON, pois ele não descreve quais são seus conteúdos




1. Adicione os seguintes campos mostrados abaixo no objeto Account que você acabou de criar.

   | Nome do campo | Nome de exibição | Tipo |
   | ------------ | ------------- | ---------- |
   | *createDate* | *Criar Data* | *DateTime* |
   | *endDate* | *Data de término* | *DateTime* |

   >[!NOTE]
   >
   >Você percebe que, ao adicionar os novos campos, a opção **Atribuir a** já está preenchida e faz referência ao grupo de campos usado para o objeto da conta.



1. Quando concluído, o objeto da conta do esquema será semelhante ao mostrado abaixo. **Salve** seu esquema!



   ![Esquema de conta de cliente com objeto de conta e campos filho adicionados](assets/model-custom-objects-account-object-with-child-fields.png)



1. Adicione mais um campo personalizado ao objeto da conta. Clique no botão **+ (adicionar)** ao lado do objeto de conta.  Crie o seguinte campo:

   | Nome do campo | Nome de exibição | Tipo | Enumerações |
   | ----------- | ----------------- | -------- | --------------------------------------- |
   | *acqSource* | *Source adquirido* | *Cadeia de caracteres* | *Web :: Web *<br />*inStore :: InStore* |

   Este campo precisa de valores padronizados, portanto, use a opção **Enumerar &amp; Valores sugeridos** nas propriedades do campo. Selecione o botão de opção **Enumerar** para adicionar a validação para este campo na assimilação, bem como rótulos amigáveis. Adicione os valores de enumeração conforme mostrado abaixo:

   - *Web :: Web*
   - *inStore :: InStore*



   ![Valores de enumeração da Web e do inStore adicionados ao campo Source de aquisição](assets/model-custom-objects-enum-values-for-acquisition-source-field.png)

   >[!NOTE]
   >
   >A meta de Enumerar e Valores sugeridos é facilitar a segmentação para o usuário final. As enumerações impõem validação no momento da assimilação de dados, enquanto os valores sugeridos não. Para saber mais sobre este recurso, leia mais na documentação aqui -> [https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/enum.html?lang=en#enums-and-suggested-values](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/enum.html?lang=en#enums-and-suggested-values)



1. Quando terminar, clique no botão **Aplicar** para adicionar o novo campo ao esquema.

1. **Salvar** seu esquema

>[!SUCCESS]
>
>Você criou com sucesso seu primeiro objeto e campos personalizados no registro do esquema XDM.



## Criação do objeto de plano

Repita as etapas executadas acima e adicione o objeto **Plano** e os campos associados. Todos os novos campos devem ser adicionados no grupo de campos Detalhes da conta do cliente - \[suas iniciais].

Use os metadados na tabela abaixo para criar o objeto de plano e seus campos associados.

| Nome do campo | Nome de exibição | Tipo | Enumeração e valores sugeridos |
| ---------- | -------------- | -------- | ------------------------------------------------------------------------------------- |
| *plano* | *Detalhes do plano* | *Objeto* | - |
| *IDdoPlano* | *ID do Plano* | *Cadeia de caracteres* | - |
| *nome* | *Nome do Plano* | *Cadeia de caracteres* | Enum <br />*básico :: Básico *<br />*final :: Ultimate *<br />*pro :: Pro* |
| *tipo* | *Tipo* | *Cadeia de caracteres* | - |

>[!WARNING]
>
>Verifique se você está adicionando os novos campos criados ao grupo de campos Detalhes da conta do cliente - \[suas iniciais].  Uma maneira rápida de garantir que sejam adicionados automaticamente a esse grupo de campos é selecionar o grupo de campos no painel à esquerda antes de adicionar um campo personalizado.
>
>
>
>![Grupo de campos Detalhes da Conta do Cliente selecionado no painel esquerdo antes de adicionar um novo campo](assets/model-custom-objects-field-group-selected-before-adding-field.png)
>
>



Quando terminar de validar, seu esquema corresponderá à captura de tela abaixo. Se estiver bom **Salve** seu esquema



![Esquema de Conta de Cliente com objeto de plano e campos filho adicionados](assets/model-custom-objects-plan-object-with-child-fields.png)

>[!TIP]
>
>Legal!  Você adicionou seu próprio objeto e campos personalizados sem ajuda.



## Criação do campo ID do cliente

Adicionar o campo **customerID** como este campo é crítico porque ele serve como a identidade primária para o esquema, bem como um campo geral no qual manter os dados.

Siga as mesmas etapas descritas anteriormente e use a tabela abaixo para fazer referência aos metadados do campo.

| Nome do campo | Nome de exibição | Tipo | Grupo de campos |
| ------------ | ------------- | -------- | --------------------------------------------- |
| *customerID* | *ID do cliente* | *Cadeia de caracteres* | *Detalhes da Conta do Cliente - \[Suas Iniciais]* |

>[!NOTE]
>
>O `customerID` pode ser colocado em qualquer lugar no esquema de uma perspectiva hierárquica. Neste laboratório, o campo customerID permanece na raiz e não é aninhado dentro de um dos objetos personalizados criados anteriormente.  É nesse posicionamento que a arquitetura de dados tem opiniões
>
>😄



O resultado final é semelhante à captura de tela abaixo quando você está concluído

![Esquema de Conta de Cliente com campo customerID adicionado à raiz](assets/model-custom-objects-customerid-field-added.png)



## Resultado final do esquema



![Esquema final com todos os objetos e campos personalizados adicionados](assets/model-custom-objects-final-schema-with-custom-objects.jpeg "Esquema final com objetos personalizados")

>[!SUCCESS]
>
>Você criou seu primeiro esquema XDM! Na próxima seção, você configura o esquema para uso com o Perfil de cliente em tempo real.
