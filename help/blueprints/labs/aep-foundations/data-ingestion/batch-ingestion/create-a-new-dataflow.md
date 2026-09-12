---
title: Criar um novo fluxo de dados
description: Crie um fluxo de dados de origem em lote com base em um conjunto de dados existente e importe mapeamentos de um fluxo de dados anterior para acelerar a configuração.
doc-type: article
solution: Experience Platform
exl-id: 6f26f742-27e8-445a-8005-21d4e59dc3d0
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# Criar um novo fluxo de dados

## Navegar até Origens

1. Na interface do usuário do Adobe Experience Platform, navegue até o seguinte local:\
   **Fontes** -> **Catálogo** -> **Sistema local**
1. Clique no botão **Adicionar Dados** para o cartão **Carregamento de Arquivo Local**

![Botão Adicionar Dados para o cartão de carregamento Arquivo Local no catálogo Fontes](assets/create-a-new-dataflow-local-file-upload-add-data.png "Acessar a Zona de Aterrissagem de Dados")



## Configurar o fluxo de dados

1. Na tela de detalhes do Fluxo de Dados, escolha **Conjunto de dados existente**.
1. Use o conjunto de dados criado anteriormente com o nome **Conta do cliente - \&lt;Suas iniciais>**
1. Verifique se o **Conjunto de dados de perfil** está ativado.
(Se você não ativar isso, o Armazenamento de perfis não poderá monitorar os novos dados que entram nesse conjunto de dados e, portanto, não assimilará esses dados no Perfil)
1. Ative a opção **Habilitar assimilação parcial**
(Se você não ativar isso, a assimilação inteira poderá falhar se apenas um dos registros tiver um erro)
1. Defina o nome do fluxo de dados como **Lote de contas de clientes v2 - \&lt;Suas iniciais>**
1. Ativar todos os alertas **Início/Sucesso/Falha do fluxo de dados de fontes**
1. Se tudo estiver bem, clique no botão **Avançar**, no canto superior direito da tela, para prosseguir para a próxima etapa.

![Tela de detalhes do fluxo de dados configurada com o conjunto de dados existente para o segundo fluxo de dados](assets/create-a-new-dataflow-existing-dataset-flow-details.png "Detalhes do fluxo de dados")



## Carregar arquivo de amostra

1. Arraste e/ou carregue o arquivo **Lab\_Customer\_Account.csv** na interface.  Quando terminar, sua tela deverá ficar parecida com a exibida abaixo.

![Visualização do arquivo CSV da Conta do Cliente carregado para o segundo fluxo de dados](assets/create-a-new-dataflow-uploaded-csv-preview.png "Acessando os arquivos do Azure Storage Explorer no Adobe Experience Platform")



## Importar mapeamentos

Na tela de mapeamento, em vez de configurar todos os mapeamentos novamente, você pode importar os que criou anteriormente.

1. Clique no botão **Importar mapeamento**
1. Selecione o fluxo de dados que tem o mapeamento criado anteriormente



![Botão Importar mapeamento na tela de mapeamento](assets/create-a-new-dataflow-import-mapping-button.png "Botão Importar mapeamento")



![Caixa de diálogo para seleção do fluxo de dados do qual importar mapeamento](assets/create-a-new-dataflow-select-dataflow-to-import-mapping-from.png "Selecione o fluxo de dados do qual importar mapeamento")

>[!NOTE]
>
>A importação de mapeamentos é uma maneira útil de reutilizar mapeamentos de outros fluxos de dados e reduzir a quantidade de trabalho de mapeamento necessário
