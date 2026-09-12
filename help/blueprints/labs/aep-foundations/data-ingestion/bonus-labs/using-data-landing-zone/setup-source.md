---
title: Configurar a origem
description: Faça upload de um exemplo de arquivo de Conta do cliente para a Data Landing Zone e configure um novo fluxo de dados de fonte de armazenamento na nuvem.
doc-type: article
solution: Experience Platform
exl-id: 1c80e71b-19a7-45e9-9961-d72b3f03ecae
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---


# Configurar a origem

## Carregar arquivo de amostra

Você precisa fazer upload de um arquivo de dados de amostra para sua Data Landing Zone no Azure Storage Explorer para poder usá-lo durante o laboratório.  Para fazer isso, faça o seguinte:

1. Baixe os [Arquivos de Exemplo](../../sample-files.md)
1. Arraste e/ou carregue o arquivo **Lab\_Customer\_Account.csv** para a Data Landing Zone salva na etapa anterior.

Quando carregada, sua tela deve ficar parecida com a captura de tela abaixo.

>[!WARNING]
>
>Certifique-se de não carregar o arquivo na pasta *projeto*. Ele contém dados pré-carregados que você não usa em nossos laboratórios.

![Navegador do arquivo da Zona de Aterrissagem de Dados mostrando o arquivo Lab_Customer_Account.csv carregado, não a pasta do projeto](assets/setup-source-make-sure-you-do-not-upload-the-file.png)

## Navegar até Origens

1. Vá para o Adobe Experience Platform e navegue até: **Fontes** -> **Catálogo** -> **Armazenamento na nuvem**
1. Clique em **Configuração** / **Adicionar dados** para a Data Landing Zone

![Configurar ou adicionar ação de dados para a fonte de armazenamento na nuvem da Zona de Aterrissagem de Dados](assets/setup-source-add-data-landing-zone-source.png "Acessar a Zona de Aterrissagem de Dados")

>[!NOTE]
>
>Se existir pelo menos uma conexão para essa origem, você verá **Adicionar dados** como a ação padrão. Se não houver conexões para essa origem, você verá **Configuração** como a ação padrão

## Pré-visualizar o arquivo

1. Selecione o **Lab\_Customer\_Account.csv**

   ![Selecionando o arquivo Lab_Customer_Account.csv para visualização no Azure Storage Explorer](assets/setup-source-select-lab-customer-account-csv.png "Acessando os arquivos do Azure Storage Explorer no Adobe Experience Platform")

1. No painel de visualização, observe os seguintes atributos e observe o seguinte:

   - **sms\_optIn** é um campo de consentimento que tem vários valores ausentes (mostrado na visualização como - )
   - **account\_create\_date** não tem o formato de data adequado. Ele tem valores de string junto com valores de data e hora em uma string.
   - **account\_end\_date** tem o formato de data adequado.



   Campo ![sms_optIn com vários valores ausentes mostrados na visualização do arquivo](assets/setup-source-sms-optin-missing-values.png "sms_optIn")



   ![campos account_create_date e account_end_date mostrados na visualização do arquivo](assets/setup-source-account-create-date-account-end-date.png "account_create_date e account_end_date")

   >[!NOTE]
   >
   >Você precisará lidar com os valores ausentes, datas e campos formatados incorretamente nas etapas de mapeamento posteriormente neste laboratório

1. Clique em **Avançar** no canto superior direito da tela para prosseguir para a próxima etapa



## Configurar o fluxo de dados

1. Na tela de detalhes do Fluxo de Dados, escolha **Novo conjunto de dados**.
1. Nomeie o conjunto de dados de saída como **Conta do Cliente - \&lt;Suas Iniciais>**
1. Selecione o esquema **dep: Conta do cliente** na lista suspensa.
1. Ative a caixa de alternância **Conjunto de dados de perfil**.
(Se você não ativar isso, o Armazenamento de perfis não poderá monitorar os novos dados que entram nesse conjunto de dados e, portanto, não assimilará esses dados no Perfil)
1. Ative a **Habilitar assimilação parcial**.
(Se você não ativar isso, a assimilação poderá falhar se um dos registros tiver erros)
1. Defina o nome do fluxo de dados como **Assimilação em lote da conta do cliente - \&lt;Suas iniciais>**
1. Ativar todos os alertas **Início/Sucesso/Falha do fluxo de dados de fontes**

![Tela de detalhes do fluxo de dados com as novas configurações de conjunto de dados, alternância de perfil e assimilação parcial definidas](assets/setup-source-dataflow-detail-screen-settings.png "Detalhes do fluxo de dados")

>[!CAUTION]
>
> Verifique se você **habilitou o conjunto de dados** para assimilação parcial e de perfil.

Clique em **Avançar** no canto superior direito da tela para continuar com a próxima etapa.

>[!NOTE]
>
>**Habilitar assimilação parcial** especifica o número de erros (**INGEST** e **DCVS**) como uma porcentagem do número total de registros que podem falhar antes que todo o fluxo de dados seja declarado como uma falha.
