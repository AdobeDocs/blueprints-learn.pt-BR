---
title: Compor o SMS
description: Saiba como compor e personalizar uma mensagem SMS em Campanhas orquestradas usando atributos de modelo e criação de telefone da loja relacional.
doc-type: article
solution: Experience Platform
exl-id: 3deb822b-8374-4537-a260-f4f6f4d67569
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# Compor o SMS

## Objetivo

Nas próximas etapas, você escreverá uma mensagem SMS MUITO simples.  Você verá como é possível adicionar conteúdo facilmente em um nível EXTREMAMENTE básico e personalizar a mensagem com base nos dados na loja relacional.



## Navegar até o conteúdo

Clique no botão **Editar conteúdo** ou navegue diretamente para a guia **Conteúdo**

![Botão Editar conteúdo e navegação da guia Conteúdo &quot;Editar conteúdo&quot;](assets/compose-the-sms-navigate-to-content-tab.png "Editar conteúdo")



## Criar a mensagem

1. Clique no botão **Personalization** para criar sua mensagem.

   ![Botão do Personalization para criar a mensagem SMS](assets/compose-the-sms-click-personalization-button.png)

   >[!NOTE]
   >
   >A opção &quot;varinha mágica&quot; usa IA para ajudar você a escrever uma mensagem. Dê uma olhada se quiser, mas não vamos cobri-lo neste laboratório.



2. Copie e cole o texto abaixo no corpo da mensagem SMS.

   ```none
   Hi from Connection 5G! Your phone_make phone_model is eligible for a free upgrade to one of the new iPhone 17 models. Shop online or come into a store today to take advantage of this offer.
   ```

   >[!NOTE]
   >
   >Certifique-se de ativar a Quebra de texto para **Ligado** no editor de mensagens.  Você pode encontrar no painel inferior direito da janela.



3. Atualize os dois campos na mensagem chamada **phone\_make** e **phone\_model** abaixo usando a opção **Atributos de destino** no painel esquerdo.  Quando terminar, sua mensagem deverá corresponder à captura de tela.

   ![Mensagem SMS final com modelo personalizado e criação de telefone](assets/compose-the-sms-final-message-text.png)

   >[!NOTE]
   >
   >Por que você está fazendo isto?  Bem, você deseja personalizar a mensagem com o modelo e a marca do telefone dos clientes, e essas informações estão na tabela Linha do cliente na loja relacional.  Isso demonstra como você pode usar dados de Campanhas orquestradas para personalizar mensagens.



4. Clique em **Validar** no editor e verifique se não há erros de validação. Se estiver correto, clique no botão **Salvar**

   ![Botões Validar e Salvar no editor de mensagens](assets/compose-the-sms-validate-and-save.png)



5. Clique na **seta para trás (\&lt;-)** quando terminar para retornar à tela de fluxo de trabalho

![Seta para trás para retornar à tela do fluxo de trabalho](assets/compose-the-sms-return-to-canvas.png)



## Recapitulação

Você acabou de criar uma mensagem e, espero, agora esteja um pouco mais familiarizado com o funcionamento do editor de mensagens.  Lembre-se de que você pode personalizar usando dados da Loja relacional, mas também pode personalizar usando dados do Perfil do cliente em tempo real.

>[!NOTE]
>
>Se você usar os atributos do Perfil do cliente em tempo real para personalizar mensagens em campanhas orquestradas, basta lembrar que ele está extraindo do conjunto de dados Instantâneo do perfil no data lake para que os atributos possam ter até 24 horas. O Instantâneo do perfil é atualizado apenas uma vez por dia após o trabalho diário de segmentação em lote.
