---
title: Configurar a origem
description: Faça upload de um arquivo JSON de pedidos históricos para a Data Landing Zone e configure um novo fluxo de dados direcionado para o schema Pedidos.
doc-type: article
solution: Experience Platform
exl-id: 046d50ad-687e-4cdb-a8b1-3c55ab39b68e
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# Configurar a origem

## Carregar arquivo de amostra

Você precisa fazer upload de um arquivo de dados de amostra para sua Data Landing Zone no Azure Storage Explorer para poder usá-lo durante o laboratório.  Para fazer isso, faça o seguinte:

1. Baixe os [Arquivos de Exemplo](../../../sample-files.md)
1. Arraste e/ou carregue o arquivo **Lab\_Historical\_Orders.json** para a Data Landing Zone da qual você salvou acima.



Quando carregada, sua tela deve ficar parecida com a captura de tela abaixo.

![Arquivo Lab_Historical_Orders.json carregado na Zona de Aterrissagem de Dados](assets/setup-source-lab-historical-orders-json-uploaded-to-dlz.png "Lab_Historical_Orders.json carregado na DLZ")

## Navegar até Origens

1. Vá para o Adobe Experience Platform e navegue até: **Fontes** -> **Catálogo** -> **Armazenamento na nuvem**
1. Clique em **Configuração** / **Adicionar dados** para a Data Landing Zone

![Navegando até Fontes > Catálogo > Armazenamento na nuvem para configurar a Zona de Aterrissagem de Dados](assets/setup-source-navigate-to-data-landing-zone-source.png "Fontes - Zona de Aterrissagem de Dados")

>[!NOTE]
>
>Você vê **Adicionar dados** como a ação padrão se já tiver configurado uma conexão do laboratório de assimilação em lote anterior



## Pré-visualizar o arquivo

1. Selecione o arquivo **Lab\_Historical\_Orders.json** e visualize seu conteúdo
1. Clique em **Avançar** no canto superior direito da tela para prosseguir para a próxima etapa

![Selecionar e visualizar o conteúdo do arquivo Lab_Historical_Orders.json](assets/setup-source-select-and-preview-lab-historical-orders.png "Selecionar e visualizar o arquivo Lab_Historical_Orders.json")

## Configurar o fluxo de dados

1. Na tela de detalhes do Fluxo de Dados, escolha **Novo conjunto de dados**
1. Nomeie o conjunto de dados de saída como **Pedidos - SeuNomeAqui**
1. Selecione o nome do esquema **dep: Pedidos**
1. Ative a caixa de alternância **Conjunto de dados de perfil**
(Se você não ativar isso, o Armazenamento de perfis não poderá monitorar os novos dados que entram nesse conjunto de dados e, portanto, não assimilará esses dados no Perfil)
1. Ativar a **Habilitar assimilação parcial**
(Se você não ativar isso, a assimilação poderá falhar se um dos registros tiver erros)
1. Defina o nome do fluxo de dados como **Pedidos - Preenchimento retroativo - SeuNomeAqui**
1. Ativar todos os alertas **Início/Sucesso/Falha do fluxo de dados de fontes**

![Tela de detalhes do fluxo de dados configurada para o conjunto de dados Pedidos](assets/setup-source-dataflow-details-for-orders.png "Detalhes do fluxo de dados para Pedidos")

>[!CAUTION]
>
>Verifique se você **habilitou** seu conjunto de dados para assimilação parcial e de perfil.

Clique em **Avançar** no canto superior direito da tela para prosseguir para a próxima etapa
