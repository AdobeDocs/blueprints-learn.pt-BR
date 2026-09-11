---
title: Criar fluxo de dados
description: Configure um fluxo de dados de origem em lote com um novo conjunto de dados, ative a Assimilação parcial e o Perfil, e faça upload de um arquivo CSV de amostra da conta do cliente.
doc-type: article
solution: Experience Platform
exl-id: 70145966-d6c0-4741-8216-903de0d61e1d
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---


# Criar fluxo de dados

## Navegar até Origens

1. Na interface do usuário do Adobe Experience Platform, navegue até o seguinte local:\
   **Fontes** -> **Catálogo** -> **Sistema local**
1. Clique no botão **Adicionar Dados** para o cartão **Carregamento de Arquivo Local**

![Botão Adicionar Dados para o cartão de carregamento Arquivo Local no catálogo Fontes](assets/create-dataflow-local-file-upload-add-data.png "Acessar a Zona de Aterrissagem de Dados")



## Configurar o fluxo de dados

1. Na tela de detalhes do Fluxo de Dados, escolha **Novo conjunto de dados**.
1. Nomeie o conjunto de dados de saída como **Conta do Cliente - \&lt;Suas Iniciais>**
1. Selecione o esquema **dep: Conta do cliente** na lista suspensa.
1. Ative a caixa de alternância **Conjunto de dados de perfil**.
(Se você não ativar isso, o Armazenamento de perfis não poderá monitorar os novos dados que entram nesse conjunto de dados e, portanto, não assimilará esses dados no Perfil)
1. Ative a **Habilitar assimilação parcial**.
(Se você não ativar isso, a assimilação inteira poderá falhar se apenas um dos registros tiver um erro)
1. Defina o nome do fluxo de dados como **Lote da conta do cliente - \&lt;Suas iniciais>**
1. Ativar todos os alertas **Início/Sucesso/Falha do fluxo de dados de fontes**

   ![Tela de detalhes do fluxo de dados com as novas configurações de conjunto de dados, Perfil e assimilação parcial definidas](assets/create-dataflow-new-dataset-flow-details.png "Detalhes do fluxo de dados")

   >[!NOTE]
   >
   >**Habilitar assimilação parcial** especifica o número de erros (**INGEST** e **DCVS**) como uma porcentagem do número total de registros que podem falhar antes que todo o fluxo de dados seja declarado como uma falha.

   >[!CAUTION]
   >
   >Verifique se você **habilitou o conjunto de dados** para assimilação parcial e de perfil antes de continuar.

1. Se tudo estiver bem, clique no botão **Avançar**, no canto superior direito da tela, para prosseguir para a próxima etapa.



## Carregar arquivo de amostra

1. Baixe os arquivos de exemplo dos [Arquivos de Exemplo](../sample-files.md) para usar com este laboratório
1. Arraste e/ou carregue o arquivo **Lab\_Customer\_Account.csv** na interface.  Quando terminar, sua tela deverá ficar parecida com a exibida abaixo.

   ![Visualização do arquivo CSV da Conta do Cliente carregado na tela de dados de origem](assets/create-dataflow-uploaded-csv-preview.png "Acessando os arquivos do Azure Storage Explorer no Adobe Experience Platform")

1. No painel de visualização, observe os seguintes atributos e observe as seguintes coisas:

   - **sms\_optIn** é um campo de consentimento com vários valores ausentes (mostrado na visualização como - )
   - **account\_create\_date** não tem o formato de data adequado. Ele tem valores de string junto com valores de data e hora em uma string.
   - **account\_end\_date** tem o formato de data adequado.



   ![Visualização mostrando o campo sms_optIn com vários valores de consentimento ausentes](assets/create-dataflow-sms-optin-missing-values.png "sms_optin")



   ![Visualização dos valores dos campos account_create_date e account_end_date mostrando formatação inconsistente](assets/create-dataflow-account-create-end-date-preview.png "account_create_date e account_end_date")

   >[!NOTE]
   >
   >Você precisará lidar com os valores ausentes, datas e campos formatados incorretamente nas etapas de mapeamento posteriormente neste laboratório

1. Clique no botão **Avançar**, no canto superior direito da tela, para prosseguir para a próxima etapa
