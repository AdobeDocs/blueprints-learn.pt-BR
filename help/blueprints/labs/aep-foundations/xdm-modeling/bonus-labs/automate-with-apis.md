---
title: Automatizar com APIs
description: Execute uma coleção do Postman que automatiza a criação de esquemas, grupos de campos, descritores de identidade e relacionamento e conjuntos de dados em uma única passagem.
doc-type: article
solution: Experience Platform
exl-id: a490f93f-19da-4de3-81c8-4569c49c5354
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Automatizar com APIs

## Introdução

Para ver como você pode automatizar implantações usando APIs, execute uma pasta de APIs que cria os seguintes objetos:

- Conta e plano do cliente \[Pesquisa] esquema(s)
- Grupos de campos que compõem os esquemas acima
- Descritores de identidade necessários para o perfil
- Descritores de relacionamento e referência necessários para criar os relacionamentos entre a Conta do Cliente e o Plano \[Pesquisa]
- Dois conjuntos de dados correspondentes a cada esquema criado



## Executar a pasta

1. No Postman, navegue até a pasta **Automação com APIs** na pasta **XDM Schema Lab**

   ![Automação com a pasta APIs na pasta XDM Schema Lab no Postman](assets/automate-with-apis-postman-automation-folder.png)



1. Clique na pasta **Automação com APIs** e, no espaço de trabalho, clique no botão **Executar**

   >[!NOTE]
   >
   >O botão Executar está no canto superior direito do espaço de trabalho do Postman

   ![Botão Executar no canto superior direito do espaço de trabalho do Postman para a pasta Automação com APIs](assets/automate-with-apis-click-folder-run-button.png "Clique na pasta Executar")



1. Uma nova janela que mostra todas as chamadas de API na pasta deve ser exibida. Defina o **Atraso** como **500ms** e clique no botão **Executar**.

   ![Caixa de diálogo Executar Automação com Atraso definido como 500 ms antes de clicar em Executar](assets/automate-with-apis-execute-automation-dialog.png "Executar automação")



1. Você vê as chamadas de API começarem a ser executadas em ordem e, quando concluído, deve ver 32 testes aprovados.

   ![Automação bem-sucedida executada com 32 testes bem-sucedidos](assets/automate-with-apis-successful-automation-32-passed-tests.png "Automação bem-sucedida")



1. Vá para a interface do Experience Platform e você deverá ver dois esquemas e dois conjuntos de dados criados e habilitados para o perfil com o prefixo **postman:**

![Dois esquemas criados e habilitados para o perfil com o postman: prefixo](assets/automate-with-apis-schemas-created-in-ui.png "Esquemas de automação")



![Dois conjuntos de dados criados com o postman: prefixo que corresponde aos esquemas automatizados](assets/automate-with-apis-datasets-created-in-ui.png "Conjuntos de dados de automação")

>[!TIP]
>
>Parabéns!  Você acabou de automatizar a implantação de namespaces de identidade, grupos de campos, esquemas, descritores de identidade/relacionamento e ativar um esquema para criar um perfil e gerar um conjunto de dados utilizando o esquema
