---
title: Verificação e validação
description: Visualize um conjunto de dados assimilado na interface e execute consultas SQL para verificar registros assimilados em lote e campos de esquema aninhados.
doc-type: article
solution: Experience Platform
exl-id: 7e7cd43d-cc24-4a40-a175-2c651436ab79
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Verificação e validação

## Visualizar o conjunto de dados

1. Clique em **Conjuntos de dados**
1. **Localize** e **clique** o nome do conjunto de dados que você criou.

   ![Localizando e clicando no nome do conjunto de dados no painel Conjuntos de Dados](assets/verification-and-validation-access-dataset-in-datasets-pane.png "Acesse o conjunto de dados no painel Conjuntos de Dados")



1. Clique em **Visualizar conjunto de dados** no canto superior direito

   ![O local do botão Visualizar conjunto de dados no canto superior direito da tela do conjunto de dados](assets/verification-and-validation-preview-dataset-button-location.png "A visualização do conjunto de dados está no canto superior direito")



1. **Verifique** e **valide** os mesmos registros que você assimilou clicando no painel esquerdo que mostra a hierarquia do esquema.

![Visualização do conjunto de dados com o painel de hierarquia de esquema mostrando registros assimilados](assets/verification-and-validation-verify-and-validate-the-dataset.png)

>[!NOTE]
>
>**Visualizar conjunto de dados** exibe o lote bem-sucedido mais recente neste conjunto de dados. Não é possível ver os lotes anteriores. Além disso, dados complexos, como matrizes e mapas, não podem ser visualizados atualmente e são exibidos como colunas vazias. Não entre em pânico! Para obter uma visualização mais abrangente, é necessário usar o SQL para explorar o conjunto de dados, conforme explicado abaixo.



## Conjunto de dados de consulta

1. **Fechar** a Visualização
1. Na tela Conjunto de Dados, clique no ícone de cópia no **Nome da tabela**. Na tela de exemplo abaixo, o nome da tabela é `customer_account_sm`

   ![Ícone Copiar ao lado do nome da tabela na tela Conjunto de Dados](assets/verification-and-validation-copy-table-name.png "Copiar o nome da tabela")



1. Navegue até a seção **Consultas**

1. Clique em **Criar consulta**

   ![Botão Criar consulta na seção Consultas](assets/verification-and-validation-access-the-query-editor.png)



1. Copiar e colar a seguinte consulta SQL no **Editor**. Lembre-se de substituir `<table_name>` pelo valor obtido na etapa 6.

   ```sql
   SELECT * FROM <table_name>
   ```



1. Pressione o botão **Reproduzir**.

   ![Interface do editor de consultas com consulta SQL e botão Reproduzir](assets/verification-and-validation-query-editor-interface.png "Interface do editor de consultas")



1. **Visualizar** os resultados

1. Além disso, execute a seguinte consulta SQL para recuperar o esquema XDM junto com os dados:

```sql
SELECT to_json(shippingAddress) FROM <table_name>
```

Para acessar os dados no `postalCode` **nó**, digite:

```sql
SELECT shippingAddress.postalCode FROM <table_name>
```

>[!TIP]
>
>Parabéns!  Você assimilou e criou com sucesso um conjunto de amostras de Perfis de clientes em tempo real
