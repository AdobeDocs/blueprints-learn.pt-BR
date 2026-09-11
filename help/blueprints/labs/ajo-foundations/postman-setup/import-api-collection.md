---
hold: true
title: Importar coleção de API
description: Importe a coleção de APIs do Postman do bootcamp e valide se suas variáveis de ambiente resolvem corretamente em relação à sua sandbox.
doc-type: article
solution: Experience Platform
exl-id: 7562c7f1-0d60-4a3a-8bce-fa42bda08962
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---


# Importar coleção de API

## Objetivo

Nesta etapa, você importará a coleção da API que contém todas as várias solicitações que precisarão ser feitas durante a inicialização.  Essas solicitações de API dependem do arquivo de ambiente que você acabou de importar.



## Importar coleção de solicitações

1. Baixe o arquivo **AJO Bootcamp (Labs).postman\_collection.json**:

Baixar arquivo — [AJO Bootcamp (Labs).postman_collection.json](assets/ajo-bootcamp-labs.postman_collection.json)

2. Como antes, clique no botão **Importar**.
3. Cole a URL local do arquivo **AJO Bootcamp (Labs).postman\_collection.json** na caixa de texto importar modal ou solte-a na caixa de diálogo importar.  Isso aciona uma importação automática.
4. Após a conclusão do processo de importação, clique em **Coleções** na barra de navegação à esquerda, expanda a pasta **AJO Bootcamp (Labs)** e veja a coleção recém-importada

![verificar importação da coleção do postman](assets/import-api-collection-verify-collection-imported.png)

>[!TIP]
>
>Parabéns!  Você importou com êxito a coleção de Postman do bootcamp



## Validar variáveis de ambiente

A coleção importada contém todas as chamadas de API necessárias que serão necessárias para laboratórios em toda a inicialização.  Cada laboratório é organizado em uma pasta específica com seu próprio conjunto de solicitações.

Detalhes sobre cada pasta podem ser encontrados abaixo:

- **Laboratórios de Jornada e Perfil** - Contém um conjunto de solicitações para enviar um Evento da Web e um evento que simula uma confirmação de remessa.
- **Laboratórios de decisão** - Contém solicitações para 3 visitantes que simulam as chamadas de página superior e inferior que normalmente seriam encontradas em um site com marcas AEP Web SDK.

Para garantir que o ambiente e a coleção estejam funcionando corretamente juntos, siga estas etapas.

1. Se necessário, clique em **Coleções** no painel à esquerda e expanda a pasta **Perfil e Laboratórios de Jornada**.
2. Clique na solicitação **Criar evento da Web** e veja que as variáveis de ambiente são **vermelhas**

![Solicitação do Postman mostrando variáveis de ambiente realçadas em vermelho porque nenhum ambiente está selecionado](assets/import-api-collection-environment-variables-shown-red.png "Verifique se as variáveis de ambiente do Postman estão em vermelho")

3. Clique na **Lista suspensa de Ambiente** no canto superior direito e escolha o ambiente **AJO Bootcamp**.

![Selecione o ambiente correto do Postman](assets/import-api-collection-select-postman-environment.png)

4. Com o ambiente adequado selecionado, você vê que a variável EDGE\_REGION agora fica com uma cor azul mais clara. Isso indica que a variável agora tem um valor para o ambiente selecionado. A variável DATASTREAM\_CONFIG permanece vermelha porque você ainda não criou a sequência de dados, portanto, você ainda não tem um valor para essa variável de ambiente. Passar o mouse sobre EDGE\_REGION mostra qual é o valor do ambiente.

![A variável EDGE_REGION do Postman agora está preenchida e não é mais exibida em vermelho](assets/import-api-collection-environment-works-with-collection.png "Verifique se o ambiente do Postman funciona com a coleção")

## Recapitulação

Agora você tem os arquivos de Ambiente e Coleção importados e sabe como usá-los.
