---
title: Verificação e validação
description: Pré-visualize um conjunto de dados transmitido na interface e execute consultas SQL para verificar registros assimilados e campos de esquema aninhados.
doc-type: article
solution: Experience Platform
exl-id: fbdb0b6b-08b6-49b8-b6ab-d59d5941c678
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# Verificação e validação

## Visualizar o conjunto de dados

1. Clique em **Conjuntos de dados**
1. **Localize** e **clique** o nome do conjunto de dados que você criou.

   ![Acessando o conjunto de dados criado no painel Conjuntos de Dados](assets/verification-and-validation-access-the-dataset-in-the-datasets-pane.png "Acessar o conjunto de dados no painel Conjuntos de Dados")



1. Clique em **Visualizar conjunto de dados** no canto superior direito

   ![Botão Visualizar conjunto de dados, localizado no canto superior direito da tela do conjunto de dados](assets/verification-and-validation-preview-dataset-button.png "O conjunto de dados Visualizar está no canto superior direito ")



1. **Verifique** e **valide** os mesmos registros que você assimilou clicando no painel esquerdo que mostra a hierarquia do esquema.

![Verificando e validando registros assimilados usando o painel de hierarquia de esquema](assets/verification-and-validation-verify-and-validate-the-dataset.png "Verificar e validar o conjunto de dados")

>[!NOTE]
>
>**Visualizar conjunto de dados** mostrará apenas as primeiras linhas do conjunto de dados. Os objetos de matriz não são visualizáveis.



## Conjunto de dados de consulta

1. **Fechar** a Visualização
1. Na tela Conjunto de Dados, clique no ícone de cópia no **Nome da tabela**. Na tela de exemplo abaixo, o nome da tabela é `customer_account_sm`

   ![Copiando o nome da tabela da tela Conjunto de Dados para uso em uma consulta](assets/verification-and-validation-copy-the-table-name.png "Copiar o nome da tabela")



1. Navegue até a seção **Consultas**

1. Clique em **Criar consulta**

   ![Acessando o editor de consultas na seção Consultas](assets/verification-and-validation-access-the-query-editor.png "Acessar o editor de consultas")



1. Ative o alternador para **Editor de Consulta Aprimorado**

   ![Interface do editor de consultas com a opção Editor de consultas aprimorado habilitada](assets/verification-and-validation-enhanced-query-editor-toggle.png "Interface do editor de consultas")



1. Copiar e colar a seguinte consulta SQL no **Editor**. Lembre-se de substituir `<table_name>` pelo valor obtido na etapa 2.

   ```sql
   SELECT * FROM <table_name>
   ```



1. Pressione o botão **Reproduzir**.

1. **Visualizar** os resultados.

1. Além disso, execute a seguinte consulta SQL para recuperar o esquema XDM junto com os dados:

   ```sql
   SELECT to_json(shippingAddress) FROM <table_name>
   ```



1. Para acessar os dados no `postalCode` **nó**, digite:

```sql
SELECT shippingAddress.postalCode FROM <table_name>
```

>[!TIP]
>
>Parabéns!  Você assimilou e criou com sucesso um conjunto de amostras de Perfis de clientes em tempo real
