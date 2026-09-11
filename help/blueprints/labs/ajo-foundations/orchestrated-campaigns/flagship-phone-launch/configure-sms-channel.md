---
title: Configurar canal de SMS
description: Saiba como configurar um canal de SMS baseado em Twilio e suas dimensões de execução para usar em Campanhas orquestradas.
doc-type: article
solution: Experience Platform
exl-id: 63c994f2-4b6b-42e9-aa82-cb6697390a08
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Configurar canal de SMS

## Objetivo

No próximo conjunto de etapas, você configurará o canal SMS. Isso é necessário para que você possa enviar mensagens a detentores de linha individuais posteriormente quando estiver criando sua campanha.



## Navegar até canais

1. No Adobe Journey Optimizer, vá para o menu **Administração** -> **Canais**.
1. Selecione **Configurações de SMS** → **Credenciais da API**.
1. Clique em **Criar credencial de API**.

![Navegue até Configurações de SMS e credenciais de API no menu Canais de Administração &quot;Navegar até Configurações de SMS&quot;](assets/configure-sms-channel-navigate-to-sms-settings.png "Navegar até Configurações de SMS")



## Definir as credenciais da API de SMS

Você começará criando o conector de API que o AJO usará para enviar solicitações de SMS de saída.

1. Em Fornecedor de SMS, escolha **Twilio**.
1. Insira os seguintes detalhes da credencial de API, usando sua própria [conta de avaliação do Twilio](https://www.twilio.com/try-twilio):
   - **Nome:** `DEP SMS`
   - **SID da conta:** encontrado no painel do Console do Twilio
   - **Token de Autenticação:** encontrado no painel do Console do Twilio (clique em **Exibir** para revelá-lo)
1. Clique em **Enviar** para registrar a credencial de API

>[!NOTE]
>
>Você precisará de uma conta de avaliação gratuita do Twilio com um número de telefone verificado antes de iniciar esta etapa. Cadastre-se em [twilio.com/try-twilio](https://www.twilio.com/try-twilio) e localize seu SID de Conta e o Token de Autenticação no painel do Console do Twilio.

![Campos de credencial de API de SMS para o fornecedor do Twilio](assets/configure-sms-channel-enter-api-credentials.png)



## Criar configuração de canal SMS

Agora, você mapeará essa credencial de API para uma configuração de canal que o jornada e as campanhas possam usar.

1. Navegue até **Canais** → **Configurações gerais** → **Configurações de canal**.

   ![Navegue até Configurações de canal em Configurações gerais](assets/configure-sms-channel-navigate-channel-configurations.png)



2. Clique em **Criar configuração de canal**.

   ![Botão Criar configuração de canal](assets/configure-sms-channel-click-create-configuration.png)



3. Preencha as Configurações do canal SMS com os seguintes valores:
   - **Nome:** `Relational-SMS-Multi-Entity`
   - **Canal:** `Mobile Message`
   - **Ação de marketing:** `SMS Targeting`

>[!NOTE]
>
>Se você receber um erro informando que o usuário não tem permissão, ignore-o e continue.

## Configurações de SMS

Ao selecionar Canal como Mensagem para dispositivo móvel, uma nova seção chamada Configurações de SMS é exibida. Preencha-o com os seguintes detalhes:

- **Tipo de mensagem móvel:** `Marketing`
- **Configuração da mensagem móvel:** `DEP SMS`
- **Número do remetente:** `01234567890`
- **Subdomínio:** `leave blank`
- **Número de recusa:** `leave blank`

![Configurações de SMS com número de remetente e tipo de mensagem móvel](assets/configure-sms-channel-sms-settings-fields.png)



## Detalhes da execução

1. Em Detalhes da execução, clique na guia **Campanha orquestrada**

   ![Guia de campanha orquestrada em Detalhes de execução](assets/configure-sms-channel-execution-details-tab.png)



2. Verifique se a caixa de seleção **Habilitado** está marcada

   ![Caixa de seleção habilitada marcada para campanhas orquestradas](assets/configure-sms-channel-enabled-checkbox.png)



3. Em seguida, na subseção **Execution dimension**, verifique se os itens a seguir estão configurados da seguinte maneira:
   - **Entregar uma mensagem por:** `Target + Secondary Dimension`
   - **Dimension de Destino do Perfil:** `dep-rel: Customer Account - customer_id`
   - **Dimension Secundário:** `Customer Line`

   ![Configurações da dimensão de execução com destino e dimensão secundária](assets/configure-sms-channel-execution-dimension-setup.png)

   ![Dimension Secundário definido como Linha do Cliente nas configurações de dimensão de execução &quot;Dimension Secundário&quot;](assets/configure-sms-channel-secondary-dimension-detail.png "Dimension Secundário")

   >[!NOTE]
   >
   >Isso informa ao Orchestrated Campaigns que, ao enviar mensagens, ele deve fornecer uma mensagem por registro que corresponde ao Dimension do Target de perfil.



4. No cabeçalho Endereço de Execução, selecione o botão de opção para **Dimension Secundário** e clique no botão de edição no **Campo de Execução do SMS**

   ![Endereço de execução definido como Dimension secundário com campo de edição](assets/configure-sms-channel-execution-address-selection.png)



5. Na janela pop-up, clique no esquema **dep-rel: Customer Line** e selecione **Celular**.

   ![Pop-up de esquema para dep-rel: Esquema de linha do cliente](assets/configure-sms-channel-customer-line-schema-popup.png)

   ![Campo de celular selecionado no dep-rel: Esquema de linha do cliente &quot;Campo de celular&quot;](assets/configure-sms-channel-mobile-phone-field-selected.png "Campo de celular")



6. Confirme as correspondências da seção de Detalhes da execução final abaixo

![Configuração de detalhes da execução final correspondente às configurações necessárias](assets/configure-sms-channel-final-execution-details.png)



## Enviar e revisar

1. Você pode clicar no botão **Enviar** para concluir a configuração e ver uma mensagem de sucesso ser exibida

   ![Mensagem de êxito após o envio da configuração de canal](assets/configure-sms-channel-submit-success-message.png)



2. Na página de inventário das configurações de canal, verifique se o status é exibido como **Ativo** antes de continuar

   ![Status de configuração do canal mostrado como Ativo](assets/configure-sms-channel-active-status.png)

   >[!CAUTION]
   >
   >Aguarde até que o status se torne **Ativo**, caso contrário, as etapas futuras do laboratório falharão para você



3. Quando o status se torna Ativo, você está concluído!

>[!TIP]
>
>🚀 Booyah! Seu canal de SMS agora está ativo e pronto para ação!



## Recapitulação

Agora você viu como configurar um canal SMS com êxito.  Observe que este é um SMS com base em API, portanto, dependendo do seu provedor, ele pode usar métodos alternativos de autenticação.

Você pode ler mais [aqui](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration), se estiver interessado.
