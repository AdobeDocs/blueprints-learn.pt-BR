---
title: Testar jornada
description: Use o simulador do Modo de teste de jornada para acionar um evento de envio do pedido e confirmar a execução correta do acionador e da lógica de ação antes da publicação.
doc-type: article
solution: Experience Platform
exl-id: fc3dbfb9-b44b-4866-acc9-398a8b52f2b9
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---


# Testar jornada

## Objetivo de aprendizado

Use as ferramentas de teste do jornada para verificar se o acionador do evento e a lógica de jornada estão configurados corretamente.

## Testar a jornada

1. Clique em **Jornadas** no painel esquerdo e na **guia Procurar** se não vir uma lista de Jornadas
2. Clique na sua **Jornada** para abri-la
3. Clique em **Alertas** e verifique se não há erros (avisos ok)

   ![O painel Alertas não mostra erros após abrir a jornada](assets/test-journey-alerts-no-errors.png)

   >[!NOTE]
   >
   >**O que é CJMMAS - 2001-200**
   >
   >Indica que o link para opção de não participação está ausente em uma variante de email

4. Clique em **Simular** e, no lado esquerdo, selecione **Modo de Teste**

   ![Modo de Teste selecionado em Simular no lado esquerdo](assets/test-journey-select-test-mode.png)



   >[!NOTE]
   >
   >Pode levar um minuto para ficar pronto. Durante esse tempo, o botão Acionar um evento não estará disponível.



5. Clique em **Acionar um Evento** e preencha estas propriedades:
   - **Tipo de evento**: `orders.shipped`
   - **Email Pessoal**: `henry.creel@emailsim.io`
   - **ID do pedido**: `123`
6. Clique em **Enviar** (observe que demora alguns segundos para responder depois de clicar em enviar)

   ![Acionar um Formulário de evento preenchido e Enviar clicado](assets/test-journey-trigger-event-send.png)

   >[!WARNING]
   >
   >Alguns alunos recebem erros e precisam enviar isso algumas vezes. Talvez seja necessário fazer isso **várias** vezes.
   >
   >**Às vezes** o primeiro envio fornece um erro de:
   >
   >**A entrada não existe (ID de referência: 3216a850-c40d-11f0-8fa5-73d1522cc9a2)**
   >
   >Se você receber um erro, clique em **Acionar um Evento** e **enviar** novamente.  Talvez seja necessário fazer isso **várias vezes**.



7. Em **Resultados** -> Clique em **Mostrar Log** no lado esquerdo

![Opção Mostrar Log em Resultados após disparar o evento de teste](assets/test-journey-show-log-results.png)

>[!NOTE]
>
>Alguns alunos que receberam erros às vezes recebem logs diferentes mostrando uma matriz de instâncias vazia `{"instances": []}`. Isso não é um bloqueador, vá em frente e vá para a próxima etapa.

Você deve ver algo como isso no log:

>[!NOTE]
>
>Estamos procurando os campos-chave usados: **actionsHistory**, **transitionsHistory**, **eta**, **tracking_number**, **eventType**, **personalEmail** e **orderID**.

```json
{
  "actionsHistory": {
    "8919055f-1b00-4a43-8bd6-c8af894474b2": {
      "eta": "11/27/2025",
      "tracking_number": "091204404",
      "jo_status_code": "http_200"
    }
  },
  "transitionsHistory": {
    "orderShipped (1158856989)": {
      "eventType": "orders.shipped",
      "_id": "joTestModeEvent_5abbfdcd-561d-45a7-ba42-d0640539831a",
      "_dep": {
        "personalEmail": "henry.creel@emailsim.io"
      },
      "order": {
        "orderID": "123"
      },
      "timestamp": "2025-11-17T23:30:49.576289372Z"
    }
  }
}
```



8. **Fechar** a **guia** do Navegador
9. **Fechar Modo de Teste** no canto superior direito

   ![Botão Fechar Modo de Teste na parte superior direita](assets/test-journey-close-test-mode.png)

10. Clique em **Publicar** a Jornada no canto superior direito

![Botão Publicar para a Jornada na parte superior direita](assets/test-journey-publish-journey.png)

11. **Feche** a **Jornada** clicando na seta \&lt;- na parte superior esquerda

![Seta para trás na parte superior esquerda para fechar a Jornada](assets/test-journey-close-journey-back-arrow.png)

Em seguida, enviaremos um evento pedido enviado real para o AEP

## Recapitulação

A jornada passou na validação de configuração e está pronta para receber eventos
