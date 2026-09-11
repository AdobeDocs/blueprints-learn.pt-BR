---
hold: true
title: Configurar evento
description: Crie e configure um evento de Pedido enviado unitário, incluindo configurações de namespace de identidade, para servir como acionador de entrada de jornada.
doc-type: article
solution: Experience Platform
exl-id: 4d1c1d4d-0dc6-4ea1-aa3c-f959bb3b9aa8
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---


# Configurar evento

## Objetivo de aprendizado

Crie e configure um evento que acionará uma jornada do cliente quando a ação pós-compra (ordem entregue) ocorrer.

## Navegar até o Journey Optimizer

No canto superior direito do navegador, clique no **Cubo** e selecione **Journey Optimizer**

Menu ![Cubo com Journey Optimizer selecionado](assets/configure-event-select-journey-optimizer.png)



## Configurar evento de entrega da ordem

Para criar uma Jornada que use um Evento unitário, precisamos primeiro configurar o evento.

1. No painel esquerdo, no menu Administração, clique em **Configurações** e, no bloco Eventos, clique no botão **Gerenciar**

![Botão Gerenciar no bloco Eventos em Configurações](assets/configure-event-open-events-manage.png)

&#x200B;2. No canto superior direito, clique no botão **Criar evento**

![Botão Criar Evento no canto superior direito](assets/configure-event-click-create-event-button.png)

&#x200B;3. Atualize as configurações do evento da seguinte maneira:
   - **Nome** = `orderShipped`
   - **Tipo** = `Unitary`
   - **Tipo de ID do evento** = `Rule based`
   - **Esquema** = `dep: Orders v.1`

![evento orderShipped configurado com tipo Unitário e dep: Pedidos v.1 schema](assets/configure-event-set-name-type-schema.png)

&#x200B;4. Na caixa de entrada `Fields`, clique no **ícone de Lápis**

![Ícone de lápis na caixa de entrada Campos](assets/configure-event-click-fields-pencil-icon.png)

&#x200B;5. Selecione os campos a seguir para adicionar ao evento e, quando terminar, clique no botão **OK**
   - `Event Type (eventType)`
   - `Order ID (orderID)`

![Campos de Tipo de Evento e ID do Pedido selecionados para serem adicionados ao evento](assets/configure-event-select-eventtype-orderid-fields.png)

>[!NOTE]
>
>Selecione apenas o campo ID do Pedido e não todos os campos no Pedido 😁



&#x200B;6. No `Event Id condition input`, clique no **ícone de Lápis**

![Ícone de lápis na entrada de condição da ID de Evento](assets/configure-event-click-event-id-condition-pencil.png)

&#x200B;7. **Arraste** o campo `Event Type` para a tela

![Arraste o campo Tipo de Evento para a tela de condição](assets/configure-event-drag-event-type-field-onto-canvas.png)

&#x200B;8. Na caixa de seleção exibida, procure e verifique o valor intitulado **pedidos.remetidos.** Clique no botão **OK**.

![pedidos.valor enviado marcado na caixa de seleção](assets/configure-event-select-orders-shipped-value.png)

&#x200B;9. Em seguida, atualize os dois últimos valores de Namespace e Identificador de perfil com os valores mostrados abaixo:
   - **Namespace** —> `Email`
   - **Identificador de Perfil** —> `personalEmail`

![Namespace definido como Email e Identificador de Perfil definido como personalEmail](assets/configure-event-select-profile-identifier.png)

![Configuração final do identificador de perfil e namespace](assets/configure-event-namespace-profile-identifier-final.png)

>[!NOTE]
>
>**Para que o Namespace e o Identificador de Perfil são usados?**
>
>Para qualquer jornada que use um evento, você deve especificar qual namespace de identidade e identificador de perfil associado devem ser usados para pesquisar o perfil. É importante entender que escolher uma identidade em vez de outra pode afetar como a jornada funcionará.
>
>*Exemplo Rápido:*
>
>A carga do evento é uma visualização de página que contém identidades como: ECID (identidade principal) e ID do cliente (opcional)
>
>- ECID escolhida —> é provável que seja a primeira vez que o serviço de identidade visualiza essa relação, de modo que, quando uma jornada receber esse evento, ela tentará pesquisar o perfil usando a ECID e não localizará um perfil.  Por quê? A relação ainda não existe entre a ECID e a ID do cliente, e as características do perfil provavelmente são armazenadas em relação à ID do cliente do identificador conhecido
>- ID do cliente escolhida —> essa identidade não precisa ser preenchida e provavelmente estará vazia na maioria das exibições de página.  Portanto, se essa identidade tiver sido escolhida, a única vez que uma Jornada será acionada é quando houver uma exibição de página autenticada em que a ID do cliente esteja definida.
>
>Resposta curta: não há resposta certa, apenas compensações que você precisa fazer com base no caso de uso 😃



## Configuração do evento orderShipped final

Verifique abaixo a configuração final do evento.  Se tudo estiver bem, clique no botão **Salvar**

![Configuração de evento orderShipped final pronta para salvar](assets/configure-event-verify-final-configuration.png)

>[!TIP]
>
>Você configurou seu primeiro evento do AJO. Você mesmo!

## Recapitulação

Um evento de entrega de ordem configurado no Adobe Journey Optimizer que pode ser usado como ponto de entrada para uma jornada
