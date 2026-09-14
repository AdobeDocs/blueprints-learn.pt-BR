---
title: Importar arquivo de ambiente
description: Importe o arquivo de ambiente do Postman e defina variáveis globais como EDGE_REGION necessárias para chamadas de API em toda a inicialização.
doc-type: article
solution: Experience Platform
exl-id: a5d45656-e3f5-4207-823c-ad33d4ef26a4
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%
---

# Importar arquivo de ambiente

## Objetivo

Nesta página, você importa o arquivo de ambiente do Postman.  Esse arquivo contém diversas variáveis globais usadas em várias chamadas de API feitas durante outros laboratórios por toda a inicialização.

## Importar arquivo de ambiente

1. Baixe o arquivo **AJO Bootcamp.postman\_environment.json**:

   Baixar arquivo — [AJO Bootcamp.postman_environment.json](assets/ajo-bootcamp.postman_environment.json)

2. Inicie o Postman no computador local.
3. Se necessário, alterne para o Workspace que você está usando nesses laboratórios e clique no botão **Importar**.

   ![Iniciar importação do Postman](assets/import-environment-file-click-import-button.png)

4. Cole a URL local do arquivo **AJO Bootcamp.postman\_environment.json** na caixa de texto modal de importação ou solte-a na caixa de diálogo de importação.  Essa ação aciona uma importação automática

   ![Caixa de diálogo de importação do Postman mostrando a opção de colar uma URL de arquivo](assets/import-environment-file-import-button-overlay.png "Importação do Postman via URL")

   ![Caixa de diálogo de importação do Postman aceitando um arquivo descartado via arrastar e soltar](assets/import-environment-file-drag-and-drop-import.png "Importação do Postman via arrastar e soltar")

5. Depois de importado, valide se o ambiente existe clicando na guia **Ambientes** na barra lateral esquerda. Você pode ver que o ambiente AJO Bootcamp agora está disponível para você.

![Validar importação de ambiente](assets/import-environment-file-validate-environment-imported.png)

## Definir variáveis de ambiente

O Postman foi projetado para testar e interagir com APIs. No entanto, esse laboratório o usa para simular ocorrências do AEP Web SDK de um navegador ou para chamadas de coleta de dados em tempo real do lado do servidor. Embora essas solicitações sejam tecnicamente chamadas de API, elas não são chamadas de API típicas que exigem coisas como tokens de autorização no cabeçalho. As variáveis de ambiente nesses laboratórios são usadas principalmente para variáveis em caminhos de URL (com uma sendo usada em um cabeçalho).

1. Se necessário, clique na guia **Ambientes** na barra lateral esquerda do Postman
2. Clique no arquivo de ambiente **AJO Bootcamp**. Você vê alguns valores que precisam ser preenchidos

   ![Variáveis de ambiente do Postman com valores vazios que precisam ser preenchidos](assets/import-environment-file-values-need-filling-in.png "Verificar variáveis do Postman em ambientes")

3. Ignore o valor DATASTREAM\_CONFIG por enquanto. Você cria uma configuração de sequência de dados em um laboratório posterior.
4. Atualize o campo **EDGE\_REGION** com o código de região que está mais próximo de onde você está fisicamente localizado para esta inicialização, usando a tabela abaixo como pesquisa.

   | **Região** | **Código da Região** |
   | ---------- | --------------- |
   | Oeste dos EUA | ou2 |
   | Leste dos EUA | va6 |
   | Europa | irl1 |
   | Austrália | aus3 |
   | Japão | jpn3 |
   | Ásia | spg3 |

   Quando concluído, seu arquivo de ambiente será semelhante a este:



   ![Verificar variável de região do Postman](assets/import-environment-file-region-variable-set.png)

5. Agora é necessário salvar as variáveis de ambiente; no entanto, não há um botão Salvar na interface do Postman. Use as teclas de atalho do Windows ou do Mac para salvar (ctrl+s no Windows, por exemplo). Você sabe que as alterações foram salvas ao visualizar a mensagem **Alterações salvas** no canto inferior direito da interface do usuário do Postman:

![Verificar alterações salvas](assets/import-environment-file-changes-saved-confirmation.png)

>[!SUCCESS]
>
>Parabéns! Você concluiu o arquivo de ambiente do Postman
