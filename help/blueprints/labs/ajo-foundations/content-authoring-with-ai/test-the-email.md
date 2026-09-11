---
title: Testar o email
description: Saiba como enviar e verificar emails de prova no Adobe Journey Optimizer para validar conteúdo personalizado e variantes condicionais antes da ativação.
doc-type: article
solution: Experience Platform
exl-id: 1abab39e-811c-4010-a4f5-a7adc9e4e0a4
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Testar o email

## Objetivos de aprendizagem

Ao final deste módulo, você será capaz de:

- Envie emails de prova do editor de email do Adobe Journey Optimizer.
- Valide o conteúdo personalizado e as variantes condicionais usando emails de prova.
- Verifique a entrega do email de prova em sua caixa de entrada, incluindo o tratamento de spam e mensagens recortadas.
- Revise logs do delivery de prova, carimbos de data e hora e variantes no Adobe Journey Optimizer.
- Confirme se o conteúdo de e-mail está preciso, personalizado e pronto para ativação.


## Enviar emails de prova (opcional, mas recomendado)

Neste ponto, você aprendeu que podemos não apenas personalizar os atributos do perfil, mas também usar atributos para criar uma lógica condicional que determinaria o conteúdo que você deseja mostrar. O Adobe Journey Optimizer é extremamente eficiente e oferece muita flexibilidade aos profissionais de marketing.

1. Clique em **Simular Conteúdo**.
2. Selecione **Simular variação de conteúdo**.

   ![Clicar em Simular conteúdo e selecionar Simular variação de conteúdo](assets/content-simulation-click-simulate-content-variation.png)

   Um painel de simulação é aberto.

3. Clique em **Enviar prova**.

   ![Botão Enviar prova no painel de simulação](assets/test-the-email-click-send-proof-button.png)

4. Adicione seu próprio endereço de email pessoal.

   >[!NOTE]
   >
   >Observe que, às vezes, o email corporativo bloqueará emails da sandbox. Eu recomendaria que você usasse seu email pessoal.



5. Selecione ambas as variantes.
6. Adicionar prefixo da linha de assunto
   1. Variante 1: acima de 40
   2. Variante 2: Abaixo de 40
7. Clique em **Enviar prova**. Você recebe uma mensagem de confirmação verde &quot;**Provas enviadas com êxito**&quot;

![Mensagem de confirmação verde mostrando provas enviadas com êxito](assets/test-the-email-proofs-sent-successfully-confirmation.png)

Verifique se ambos os emails chegaram à sua caixa de entrada.

>[!NOTE]
>
>Os emails de prova podem chegar ao **Spam**, dependendo dos filtros.



![Email de prova que chegou à pasta de spam](assets/test-the-email-proof-email-in-spam-folder.png)

Você pode ver a mensagem recortada, mas não há problema, pois alguns links de rodapé não são reais. Se clicar no link, você verá que ambos os emails com variantes foram recebidos.

![Email de prova recortado mostrando ambas as variantes depois de clicar no link](assets/test-the-email-clipped-proof-email-variants.png)

### Verificar a entrega da prova no AJO

Por fim, você também pode ver o delivery de prova no Adobe Journey Optimizer.

1. Retorne ao editor de email.
2. Volte para a tela de criação de email e clique em **Exibir Prova**.
3. Revisar logs do delivery, carimbos de data e hora e variantes enviadas.

![Botão Exibir prova na tela de criação de email](assets/test-the-email-click-view-proof-button.png)

Você percebe os detalhes do email de prova.

![Logs de entrega de email de prova, carimbos de data/hora e variantes enviadas no AJO](assets/test-the-email-proof-email-delivery-details.png)


## Recapitulação

Neste módulo, você:

- Emails de prova enviados e verificados no AJO

Agora você concluiu a Jornada completa do Connection 5G AJO Lab e validou que seu email é preciso, personalizado e pronto para ser ativado.
