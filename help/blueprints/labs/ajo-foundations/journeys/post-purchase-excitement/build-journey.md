---
title: Criar jornada
description: Crie uma jornada unitária que responda a um evento de Pedido enviado, chame uma ação personalizada para enviar ETA e envie um email personalizado.
doc-type: article
solution: Experience Platform
exl-id: 4dd15071-51e5-445a-932d-690d9a73a913
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 0%

---


# Criar jornada

## Objetivo de aprendizado

Crie uma jornada unitária que comece com o evento Pedido enviado configurado, obtenha o ETA de um serviço externo e envie um email.

## Criar jornada

Vá para **Jornada** e clique em **Criar Jornada - Criar do zero**

![Criar Jornada - Criar a partir da tela de rascunho no Adobe Journey Optimizer](assets/build-journey-create-journey-from-scratch.png)



## Propriedades da jornada

1. Atualize as Propriedades da Jornada no painel direito com o seguinte:
   - **Nome**: `Order Shipped Journey`
   - **Descrição**: `Notify customer that order has shipped. Include shipping details.`
   - **Marcas**: `Default`
   - **métricas de Jornada**: *deixe em branco*

     >[!NOTE]
     >
     >**Lista Suspensa Vazia?**
     >
     >Não se preocupe e siga em frente. A primeira jornada criada em uma caixa de areia precisa &quot;preparar a bomba&quot;.  Depois que publicarmos a jornada, este menu suspenso terá opções para escolher.

   - **Permitir reentrada**: `checked`

   - **Período de espera de reentrada:** `5 minutes`

   - **Rótulos de acesso**: *deixar em branco*

   - **Fuso Horário**: `Your Local timezone`

   - **Usar fuso horário do perfil em esperas e condições**: `NOT checked`

   - **Data de Início/Término**: *deixe em branco*

   - **Tempo limite ou erro**: `30`

   - **Regras de limitação:** *deixar em branco*

   - **Prioridade**: `0`



2. Se tudo estiver bem, clique no botão **Salvar**

![Botão Salvar do painel Propriedades da Jornada](assets/build-journey-save-journey-properties.png)




## Tela da jornada

### Adicionar um evento unitário

No painel esquerdo, no **menu Eventos**, arraste e solte o evento **orderShipped** na tela conforme mostrado abaixo

![Arraste o evento orderShipped do menu Eventos para a tela de jornada](assets/build-journey-drag-order-shipped-event-onto-canvas.png)



![Evento Pedido enviado colocado na tela de jornada](assets/build-journey-drag-order-shipped-event-onto-canvas--2.png)





### Adicionar uma ação personalizada

1. Se o painel esquerdo expandir o **menu Ações** e arrastar e soltar na tela a ação que você criou chamada **GetShippingDetails** após o evento orderShipped

   ![Arraste a ação personalizada GetShippingDetails para a tela após o evento orderShipped](assets/build-journey-drag-getshippingdetails-action-onto-canvas.png)

2. No painel direito, na lista suspensa Configuração de acesso e privacidade —> Ação de marketing, verifique se o valor está definido como **Nenhum**

   ![lista suspensa Ação de marketing definida como Nenhum na configuração de acesso e privacidade](assets/build-journey-set-marketing-action-to-none.png)

3. No menu Configuração de ponto de extremidade —> Parâmetros de consulta, clique no **ícone de lápis** ao lado de orderid

   ![Ícone de lápis para editar o parâmetro de consulta orderid na configuração de Ponto de Extremidade](assets/build-journey-edit-orderid-query-parameter.png)

4. No modal exibido, expanda **Contexto** -> **ordemEnviada** -> **Pedido**, selecione **ID do Pedido (orderID)** e clique em **OK**

   ![Selecione a ID da Ordem (orderID) dos campos de contexto orderShipped Order](assets/build-journey-select-order-id-context-field.png)

5. De volta ao painel direito, verifique se a opção Tempo limite ou erro está **desmarcada** e clique no **botão Salvar**

![Opção de tempo limite ou erro desmarcada com o botão Salvar realçado](assets/build-journey-uncheck-timeout-or-error.png)



### Adicionar ação de email

1. No menu Ações, arraste e solte a ação **Ação** na tela após a ação GetShippingDetails

   ![Arraste o nó Ação para a tela após a ação GetShippingDetails](assets/build-journey-drag-email-action-onto-canvas.png)

2. Selecione **Email** para a ação de marketing e **Adicionar**.

   ![Selecione Email como ação de marketing e clique em Adicionar](assets/build-journey-select-email-marketing-action.png)

3. No painel direito, clique em **Configurar ação**

   ![Configurar botão de ação no painel direito](assets/build-journey-click-configure-action.png)

4. defina a **Configuração do canal de email** como `Profile-Email` e clique em **Editar Conteúdo**

![Configuração do canal de email definida como Perfil-Email com link para Editar Conteúdo](assets/build-journey-set-profile-email-channel-configuration.png)



### Adicionar conteúdo do corpo do email

Para conteúdo, você vai manter as coisas simples. Como estúpido simples.

1. Atualize a linha de Assunto para `Order Shipped` e clique no **botão Editar corpo do email**

   ![Linha de assunto atualizada para Pedido enviado com o botão Editar corpo do email](assets/build-journey-update-subject-line-order-shipped.png)

2. Na barra superior, clique no bloco de conteúdo **Design do Zero**

   ![Criar a partir do bloco de conteúdo Scratch na barra superior](assets/build-journey-click-design-from-scratch.png)

3. Na barra esquerda, sob o contêiner Estrutura, arraste e solte a **Coluna 1:1** sobre a tela

   ![Arraste o elemento de estrutura de Coluna 1:1 para a tela de email](assets/build-journey-drag-1-1-column-onto-canvas.png)

4. Em seguida, no contêiner de Conteúdo, arraste e solte o componente **Texto** na sua **Coluna 1:1**

   ![Arraste o componente de Texto para a coluna 1:1](assets/build-journey-drag-text-component-into-column.png)

5. Clique no componente de Texto e **exclua o texto atual** e clique no ícone **Adicionar Personalization**

   ![Ícone Adicionar Personalization após excluir o texto padrão](assets/build-journey-click-add-personalization-icon.png)

6. No painel esquerdo, clique na pasta **Atributos Contextuais** e navegue pelo **Journey Orchestration** -> **Ações** e selecione **GetShippingDetails**

   ![Selecione GetShippingDetails em Atributos contextuais - Journey Orchestration - Ações](assets/build-journey-select-getshippingdetails-contextual-attribute.png)

7. No corpo principal do email agora **copie e cole** o JSON abaixo no **editor** do Personalization

   ```json
   {{profile.person.name.firstName}}, your order has shipped
   ETA: 
   Tracking Number: 
   ```

8. Adicione os campos de personalização da seguinte maneira (**clique no sinal de mais &#39;+&#39; ao lado do campo no painel esquerdo**):
   - **ETA:** `eta`
   - **Número de Acompanhamento:** `tracking_number`

   ![Campos de personalização de ETA e Número de Acompanhamento adicionados ao email](assets/build-journey-add-eta-tracking-number-fields.png)

   >[!NOTE]
   >
   >Clique no **+ símbolo** para adicionar atributos de personalização do painel à tela.  Ele os colocará onde o cursor está, para garantir que você esteja &quot;alinhado&quot; adequadamente

   >[!NOTE]
   >
   >Seu email usará uma combinação de atributos de contexto (ETA e número de rastreamento) e atributos de perfil (nome). Se quiser adicionar outros atributos de perfil, clique na guia Atributos de perfil e selecione qualquer item que desejar visualizar.
   >
   >![Guia Atributos do perfil para adicionar outros atributos de perfil](assets/build-journey-profile-attributes-tab.png)

9. Na parte inferior da tela, clique no botão **Validar** e verifique se não há erros

   ![Botão Validar sem erros na parte inferior da tela](assets/build-journey-click-validate-button.png)

10. Se tudo estiver bem, clique no **botão Salvar** na parte superior direita
11. Em seguida, clique no botão **Salvar** novamente na parte superior direita e clique na **\&lt;- seta para a esquerda** na parte superior esquerda

![Botão Salvar e seta para trás na parte superior direita e superior esquerda](assets/build-journey-save-and-back-arrow.png)

12. Finalmente, clique no **\&lt; ícone Voltar** na parte superior esquerda para voltar à Tela de Jornada

![Ícone Voltar na parte superior esquerda para retornar à Tela de Jornada](assets/build-journey-back-icon-to-journey-canvas.png)

>[!TIP]
>
>E clique novamente no botão **Voltar**... Brincadeira! Este é o último botão Voltar... nesta seção 😜



### Substituir parâmetros de email

De volta à tela principal da Jornada, no nó Email, verifique se você pode ver os campos somente leitura (talvez seja necessário clicar no ícone **Mostrar campos somente leitura**)

![Campos somente leitura mostrados no nó Email na Tela de Jornada](assets/build-journey-show-read-only-fields-email-node.png)

1. Role para baixo até **Parâmetros de email** e clique no ícone **Habilitar substituição de parâmetro**

   ![Habilitar o ícone de substituição de parâmetro em Parâmetros de Email](assets/build-journey-enable-parameter-override.png)

2. Clique na caixa de texto vazia e, em seguida, no painel à esquerda, detalhe o **Contexto** -> **orderShipped** -> **\_dep** e clique no campo **personalEmail**.  Clique no **botão OK**

   ![Selecione o campo personalEmail em orderShipped context _dep](assets/build-journey-select-personalemail-context-field.png)

   >[!WARNING]
   >
   >É perigoso evitar usá-lo, a menos que seja necessário em uma configuração de produção.  Isso substituirá o local padrão que o Jornada procura no perfil para executar mensagens.



3. Clique no **botão Salvar** na parte superior direita e clique na **seta para trás** \&lt;- na parte superior esquerda para **fechar** a Jornada

![Botão Salvar e seta para trás para fechar a Jornada](assets/build-journey-save-and-close-journey.png)

## Recapitulação

Uma jornada publicada capaz de responder ao acionador de evento Pedido enviado. Obtenha o ETA de um serviço externo e envie um email.
