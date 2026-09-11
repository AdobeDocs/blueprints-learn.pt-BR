---
title: Adicionar atividades de email
description: Saiba como adicionar e configurar duas atividades de email em ramificações bifurcadas separadas usando diferentes configurações de canal de email em uma Campanha orquestrada.
doc-type: article
solution: Experience Platform
exl-id: e911a251-9f9f-484c-a2de-101b0fc2c417
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---


# Adicionar atividades de email

## Objetivo

No próximo conjunto de etapas, você aproveitará a campanha para adicionar duas atividades de email às duas ramificações de atividades de bifurcação. Você configurará as duas atividades de Email para usar os canais de Email, criados anteriormente. Por fim, você também adicionará a configuração básica de email (assunto e corpo) a cada uma dessas atividades de email.

>[!CAUTION]
>
>Antes de continuar, você deve garantir que ambas as configurações de canal de email apareçam ativas em seus status.
>
>![Ambas as configurações de canal de email mostrando status ativo](assets/add-email-activities-email-channel-configs-active.png "Configurações de canal de email")



## Adicionar atividade de email da ramificação superior

1. Clique no **+** do fluxo superior e selecione **Email** das **Atividades de canal**

   ![Adicionar atividade de email](assets/add-email-activities-select-email-activity.png)

   O painel de detalhes do **Email** é aberto

   ![Painel de detalhes do email](assets/add-email-activities-email-details-pane.png)

2. Renomeie o rótulo para **Email usando o atributo de Perfil** para a atividade **Email** e clique em **Editar email**. Observe que a criação do corpo do email é somente para fins de teste

   ![Renomeie o rótulo de atividade de email e clique em Editar email](assets/add-email-activities-rename-and-edit-email.png)

3. Selecione a guia **Ações** e, na lista suspensa, selecione a configuração de canal **Perfil-Email**

   ![Selecionar configuração de canal Perfil-Email na guia Ações](assets/add-email-activities-select-profile-email-channel.png)

4. Em seguida, clique em **Editar conteúdo** para adicionar conteúdo de teste

   ![Clique em Editar conteúdo para adicionar conteúdo de teste](assets/add-email-activities-edit-content.png)

5. Forneça uma **Linha de Assunto** (&quot;Oferta de Atualização para membros do plano Básico&quot;) e clique no botão **Editar corpo do email**

   ![Adicionar linha de assunto e editar corpo do email](assets/add-email-activities-subject-line-edit-body.png)

6. Há muitas opções, para este teste, escolha **Codificar sua própria opção** do HTML

   ![Escolha a opção Codificar seu próprio HTML](assets/add-email-activities-code-your-own-html.png)

7. No **Designer de email**, insira uma linha de teste &quot;Oferta de atualização disponível!&quot; logo antes das tags `</body></html>` conforme mostrado e clique em **Salvar**

   ![Insira a linha de teste no Email Designer e clique em Salvar](assets/add-email-activities-email-designer-save.png)

8. Aguarde a mensagem de confirmação aparecer no canto inferior direito

   ![A mensagem de confirmação aparece](assets/add-email-activities-confirmation-message.png)

9. Clique na **seta para a esquerda** ao lado de **Designer de email** para sair

   ![Clique na seta para a esquerda para sair do Email Designer](assets/add-email-activities-exit-email-designer.png)

10. Uma caixa de diálogo de confirmação aparece, clique no botão **Salvar e fechar**

![Caixa de diálogo de confirmação com o botão Salvar e fechar](assets/add-email-activities-save-and-close-dialog.png)

11. Revise as propriedades e ações de Email, incluindo o texto adicionado ao corpo do Email. Clique na **seta para a esquerda** para voltar para a tela de campanha

![Voltar para a tela do Campaign](assets/add-email-activities-back-to-campaign-canvas.png)

## Adicionar atividade de email da ramificação inferior

De volta à tela da campanha, clique no **+** do fluxo inferior e selecione **Email** nas **Atividades do canal**. Siga as mesmas etapas descritas acima (Etapas 2 a 11), exceto para o seguinte:

- Renomeie o rótulo para **Email usando o Dimension de Destino** para a atividade **Email**
- Nas configurações de Email, escolha a configuração do canal de email **Relational-Email**

![Segunda atividade Email configurada com canal Relational-Email](assets/add-email-activities-bottom-branch-relational-email.png "Adicione a segunda atividade Email")

## Recapitulação

Agora você viu como configurar as atividades de Email com os canais de Email. Cada atividade foi configurada com um assunto e um corpo de email muito básicos. Toda a campanha será testada em seguida.
