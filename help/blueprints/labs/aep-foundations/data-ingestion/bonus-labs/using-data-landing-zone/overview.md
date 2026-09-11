---
hold: true
title: Uso da Landing Zone
description: Instale e configure o Azure Storage Explorer com um URL SAS para se conectar à Zona de aterrissagem de dados da Adobe Experience Platform.
doc-type: overview-page
solution: Experience Platform
exl-id: d61bef25-7039-450d-a8e7-01bb12e8df7c
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---


# Uso da Landing Zone

## Pré-requisitos

Se você não tiver baixado o Azure Storage Explorer, faça isso agora, pois ele é um requisito para este laboratório.  Você pode encontrar o download no link abaixo:

[Baixar o Azure Storage Explorer](https://azure.microsoft.com/en-us/blog/microsoft-azure-data-lake-storage-adls-in-storage-explorer-public-preview/)

1. Instalar o aplicativo
1. Na primeira inicialização, aceite o Contrato de licença de usuário final

![Tela do Contrato de Licença de Usuário Final no Azure Storage Explorer](assets/overview-end-user-license-agreement-screen.png "Tela do Contrato de Licença de Usuário Final")


## Configurar o Azure Storage Explorer com o Experience Platform

1. Abra o Azure Storage Explorer e clique no **ícone Selecionar Recurso** e selecione **Contêiner ou diretório Ger 2 do ADLS**

![Selecionando o Contêiner ou o diretório ADLS Gen2 como o recurso no Azure Storage Explorer](assets/overview-choose-the-resource-as-shown-above.png)



1. Selecione **SAS (URL de assinatura de acesso compartilhado)** e clique em **Avançar**

![Escolhendo a opção de URL SAS como modo de conexão](assets/overview-choose-the-sas-url-option-as-the-mode-of-connection.png "Escolha a opção de URL SAS como modo de conexão")



1. Insira o nome de Exibição como **Zona de Aterrissagem de Dados**

>[!NOTE]
>
>Você não pode continuar nesta etapa até fornecer o URL SAS.  Isso é obtido na Experience Platform, o que você verá na próxima etapa.

![Nomeando a Zona de Aterrissagem de Dados da conexão](assets/overview-name-the-connection.png "Nomear a conexão")



1. Vá para o Adobe Experience Platform e execute a navegação até a Data Landing zone fazendo o seguinte:

- Navegue até **Fontes -> Catálogo**
- Selecione **Armazenamento na nuvem** nas origens
- Em seguida, localize o cartão **Data Landing Zone**
- Clique no Cartão da Zona de Aterrissagem de Dados e em **Exibir Credenciais** no painel direito

![Cartão de origem da Zona de Aterrissagem de Dados com a opção Exibir Credenciais no Cartão Source da Zona de Aterrissagem de Dados do Adobe Experience Platform](assets/overview-data-landing-zone-view-credentials.png "Access Data Landing Zone na Adobe Experience Platform")



1. Copie o **SASUri** do modal exibido.

Navegue de volta para o Azure Storage Explorer e cole o **valor do SASUri** no **contêiner Blob ou na URL SAS do diretório** que você deixou em branco da etapa anterior

![Copiando o valor SASUri do Experience Platform para o Azure Storage Explorer](assets/overview-copy-sas-uri-into-azure-storage-explorer.png "Copie as credenciais de URL SAS do Adobe Experience Platform e copie-as para o Azure Storage Explorer")



1. Clique em **Avançar** para continuar

![Copiando credenciais de URL SAS na seção de URL SAS das informações de conexão](assets/overview-copy-sas-url-into-connection-info.png "Copiar credenciais de URL SAS na seção de URL SAS nas informações de conexão")



1. Na tela Resumo, clique em **Conectar**

![Tela Resumo com botão Conectar](assets/overview-connect-screen.png "Tela Conectar")



Agora você deve ver uma tela parecida com a exibida abaixo

![Azure Storage Explorer mostrando a conta da Zona de Aterrissagem de Dados](assets/overview-successfully-connected-account.png) conectada com êxito

&#x200B;> [!TIP]
>
>Parabéns!  O Azure Storage Explorer foi configurado com êxito
