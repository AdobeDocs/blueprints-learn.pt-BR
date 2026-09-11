---
hold: true
title: Acesso à sandbox
description: Verifique se o ambiente do Postman pode recuperar a sandbox do Experience Platform atribuída antes de iniciar os laboratórios.
doc-type: article
solution: Experience Platform
exl-id: c841e497-a695-4d3f-85e6-d653478cad1e
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---


# Acesso à sandbox

Antes de continuar, verifique se seu acesso é legítimo. Execute as seguintes etapas:

1. Abra a pasta `Check Sandbox Access` e clique na chamada `Retrieve Your Sandbox`
1. Em seguida, no canto superior direito do Postman, é exibida uma caixa suspensa Ambiente.  Certifique-se de selecionar o ambiente `AEP Bootcamp`
1. Execute a chamada clicando no botão `Send`

![Painel de solicitações do Postman para a chamada Recuperar sua sandbox antes de enviar](assets/sandbox-access-check-sandbox-request.png "Recuperar sua chamada de API de sandbox")



Uma resposta bem-sucedida tem a seguinte aparência:

![Resposta OK de {200 confirmando a recuperação bem-sucedida da sandbox atribuída](assets/sandbox-access-successful-response.png "Solicitação de sandbox bem-sucedida de ")

>[!NOTE]
>
>O valor **name** deve corresponder à variável sandbox\_name em seu ambiente do Postman

>[!TIP]
>
>Parabéns!  Você está pronto para começar a usar as APIs do Experience Platform
