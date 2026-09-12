---
title: Configurar a origem
description: Crie uma conta de transmissão da API HTTP e configure um fluxo de dados para transmitir dados JSON da conta do cliente para um conjunto de dados habilitado para perfil.
doc-type: article
solution: Experience Platform
exl-id: a5c02337-8af3-45dc-82a0-fa9731892fe4
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---


# Configurar a origem

## Navegar para fontes de transmissão

1. Vá para a interface do Adobe Experience Platform e navegue até **Fontes**
1. Clique em **Catálogo** na navegação superior
1. Selecione **Streaming** na lista de fontes (verifique se o botão de opção Todas as fontes está selecionado)
1. Clique em **Configuração** / **Adicionar dados** para a API HTTP

![Sequência de etapas para criar uma nova conta de origem da API HTTP](assets/setup-source-sequence-of-steps-to-create-a-http-api-account.png)



## Criar conta da API HTTP

A primeira coisa a fazer é criar uma nova conta. Essa conta contém os detalhes sobre como a autenticação é tratada e se os dados que estão sendo transmitidos são compatíveis com XDM (ou seja, já correspondem à estrutura do esquema XDM subjacente)

Execute as seguintes tarefas:

1. Selecione **Nova conta** e adicione os seguintes detalhes:
   - Nome da Conta -> `Streaming Ingestion - <Your Initials>`
1. Deixe a opção para **Habilitar autenticação** desabilitada
1. Deixe desmarcada a caixa de seleção para **XDM compatível**
1. Clique no botão **Conectar à origem** para continuar

>[!CAUTION]
>
>NÃO alterne a **Habilitar autenticação** ou marque a caixa para **compatível com XDM**. Isso quebra o laboratório

Sua tela deve ter esta aparência:

![Tela depois de clicar em Conectar à origem da nova conta da API HTTP](assets/setup-source-connect-to-source-screen.png)



Agora você deve ver uma caixa de seleção verde com a mensagem &quot;Conectado&quot;. Clique no botão **Avançar** no canto superior direito para continuar configurando seu fluxo de dados:

![Caixa de seleção verde com mensagem Conectado após configurar a conta da API HTTP](assets/setup-source-green-checkbox-with-connected-message.png "Você deve ver uma caixa de seleção verde com Conectado")



## Carregar dados de amostra

>[!NOTE]
>
>Caso ainda não o tenha feito, baixe os [Arquivos de Exemplo](../sample-files.md)



1. Na seção Esquema de dados do Source da tela, carregue o arquivo JSON **Lab\_Single\_Customer\_sample.json** do sistema de arquivos local que você baixou do laboratório anterior.
1. Depois que o arquivo for carregado, uma visualização será exibida da seguinte maneira. Clique no botão **Avançar** no canto superior direito para continuar. Observe como o campo birth_Date está em um formato AAAA-MM-DD diferente do formato MM/DD/AAAA visto anteriormente no laboratório de assimilação em lote.

![Visualização do registro carregado de Lab_Single_Customer_sample.json para design e validação de pipeline](assets/setup-source-sample-customer-record-for-pipeline-design-and-validation.png)

>[!NOTE]
>
>O arquivo de amostra JSON contém um único registro para projetar e validar o pipeline. Se quiser rolar, clique nos nós XDM para fazer com que os nós rolem.



## Configurar detalhes do fluxo de dados

Nesta tela, você está criando um fluxo de dados específico que aproveita a conta da API HTTP configurada.  Você pode ter muitos fluxos de dados por conta.  Nesse cenário, é necessário criar um fluxo de dados para transmitir dados da conta do cliente. Um fluxo de dados requer uma associação entre uma conta de origem, um conjunto de dados com um esquema associado e detalhes de configuração.

Execute as seguintes etapas:

1. Crie um Novo conjunto de dados e nomeie-o como -> `Customer Account Stream - <Your Initials>`
1. Escolha o **Esquema** como ->`dep: Customer Account`
1. Verifique se a opção **Conjunto de dados de perfil** está **habilitada**.  Caso contrário, **habilite**.
1. Atualize o **nome do fluxo de dados** da seguinte maneira:
   - `Customer Account Stream - <Your Initials>`
1. Clique no botão **Avançar** para continuar

![Configurando os detalhes do fluxo de dados para o conjunto de dados de transmissão da conta do cliente](assets/setup-source-configuring-a-dataflow.png)

>[!NOTE]
>
>Se você não ativar o conjunto de dados para o Perfil, os dados serão transmitidos somente para o Data Lake. Você não vê seus eventos de transmissão no Perfil ou no Gráfico de identidade.
