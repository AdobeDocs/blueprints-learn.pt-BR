---
hold: true
title: Bifurque o resultado
description: Saiba como adicionar uma atividade de bifurcação a uma campanha orquestrada para ramificar um resultado a fim de salvar um público e enviar mensagens SMS.
doc-type: article
solution: Experience Platform
exl-id: 8f1d0839-e4ca-4b7c-bc97-4e271a457296
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# Bifurque o resultado

## Objetivo

Esta etapa é simples, pois tudo o que você deseja fazer é adicionar uma atividade Fork, de modo que possa duplicar o resultado para fazer duas coisas diferentes com ele em etapas futuras:

1. Salvar o público-alvo para que outras pessoas o usem para fins de publicidade ou entre canais
1. Envie mensagens SMS para linhas individuais.



## Criar a bifurcação

1. Na tela do fluxo de trabalho, clique no ícone **+** **3} após a atividade Criar público-alvo e selecione a** Atividade de bifurcação ****

![Adicionar uma atividade de bifurcação após a atividade de compilação de público-alvo](assets/fork-the-result-add-fork-activity.png)



2. Atualize os nomes de cada transição na bifurcação clicando na transição e atribuindo os nomes conforme descrito abaixo:
   - **Superior** —> `Save Audience`
   - **Inferior** —> `SMS`

![Transições de bifurcação renomeadas para Salvar Público e SMS](assets/fork-the-result-rename-transitions.png)



Quando terminar, sua tela agora deve parecer tão...

![Tela de fluxo de trabalho após adicionar a atividade de bifurcação](assets/fork-the-result-final-canvas.png)

>[!NOTE]
>
>Uma atividade fork essencialmente é apenas duplicar o resultado da atividade anterior em duas ramificações independentes



3. Clique em **Salvar** na parte superior da tela de fluxo de trabalho.

![Botão Salvar na barra de ferramentas da tela do fluxo de trabalho](assets/fork-the-result-click-save.png)

>[!TIP]
>
>Foi muito difícil, não foi 😁



## Recapitulação

Welp, você criou uma Bifurcação do resultado (ou seja, duplicar o resultado) que permite ditar claramente uma ramificação para processar um Público-alvo salvo, enquanto a outra pode ser usada para envio de SMS.

>[!NOTE]
>
>Você precisa usar Bifurcações, especialmente se planeja salvar o público-alvo como uma atividade Salvar público-alvo não permite que as atividades o sigam.
