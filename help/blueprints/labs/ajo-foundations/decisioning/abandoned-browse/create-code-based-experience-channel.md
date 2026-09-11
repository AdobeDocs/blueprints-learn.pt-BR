---
hold: true
title: Criar canal de experiência baseado em código
description: Configure um canal de Experiência baseado em código no Adobe Journey Optimizer que retorna dados de oferta JSON para qualquer sistema da Web, móvel ou IoT que solicite uma decisão.
doc-type: article
solution: Experience Platform
exl-id: c3353d3d-cd97-46b7-8ef8-c72fa9e7dfe5
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---


# Criar canal de experiência baseado em código

## Objetivo

Lembre-se de que os requisitos comerciais são que qualquer sistema da Connection 5G deve ser capaz de retornar uma oferta apropriada. Seja o computador de um agente do cliente, um quiosque na loja, um aplicativo móvel ou o site, o cliente deve receber a mesma experiência de oferta. O único canal do AJO que pode fazer isso é uma Experiência baseada em código (CBE), um dos canais de entrada do AJO. Embora um CBE possa retornar o HTML, sua função principal é retornar informações sobre qual oferta deve ser apresentada ao sistema receptor, com esse sistema sabendo o que fazer com essas informações de oferta. Ao contrário do canal da Web, os CBEs não são renderizados ou reportados automaticamente. Embora seja um pouco mais manual para o cliente, eles oferecem muita flexibilidade, pois podem ser configurados para retornar JSON que qualquer sistema móvel, da Web ou da IoT pode usar para executar decisões.

1. Se necessário, expanda o item de menu **Administração** no painel esquerdo (talvez seja necessário rolar a tela para baixo) e clique em **Canais**. Você chega à página &quot;Configurações de canal&quot;.
2. Clique no botão azul **Criar configuração de canal**
3. Na página &quot;Detalhes de configuração do canal&quot;, nomeie o canal **jsonOffer\_cbe**

>[!NOTE]
>
>Como um CBE pode ser chamado por qualquer número de clientes em *N* número de plataformas, vamos nomear esse CBE como algo genérico para localização, mas específico para o fato de que ele retorna ofertas no formato JSON.

4. Defina o menu suspenso **Selecionar canal** como **Experiência baseada em código.**

>[!WARNING]
>
>Não definiremos uma ação de marketing neste laboratório porque ela adiciona complexidade desnecessária para nossa demonstração, mas como os CBEs podem ser acessados por qualquer número de sistemas, em um caso de uso real, você definiria todas as ações de marketing possíveis para este canal para que os rótulos DULE fossem aplicados.

5. Marque a caixa **Web** na área &#39;Configurações de experiência baseadas em código&#39; e mantenha a opção **Página única** selecionada.
6. Na caixa de texto **URL da Página**, digite o texto `https://connection5g.com/home`
7. Na caixa de texto **Local na página**, insira o texto **jsonOfferContainer**

>[!NOTE]
>
>Nem todos os eventos de experiência enviados para a Edge acionam uma solicitação de ofertas personalizadas. Você criará uma Jornada na próxima seção, onde esse CBE será configurado com a estratégia de seleção que você acabou de configurar. A configuração &quot;Localização na página&quot; é o nome do parâmetro transmitido em Eventos de experiência que instrui o Experience Edge a retornar quaisquer ofertas atribuídas a esse CBE. Também é frequentemente chamada de superfície. Seja um aplicativo móvel, uma página da Web ou algum outro dispositivo da IoT, se o valor jsonOfferContainer for transmitido para a Edge, juntamente com o eventType correto por meio de um Evento de experiência, a Edge executará a lógica configurada até o momento no laboratório e retornará a oferta apropriada.

8. Clique no botão de opção **JSON** na seção &#39;Formatar&#39;. Quando terminar, a configuração do canal do CBE será semelhante a:

![Configuração de canal de Experiência Baseada em Código concluída com o formato JSON selecionado](assets/create-code-based-experience-channel-completed-config.png)

9. Quando tudo estiver correto, clique no botão azul **Enviar** no canto superior direito.

>[!TIP]
>
>Depois de salvar, você será levado de volta à página de configuração do Canal e verá seu CBE recém-criado.

## Recapitulação

Nesta página, você configurou um canal de Experiência baseada em código (CBE) e configurou um novo canal de entrada que pode retornar decisões de oferta no formato JSON para que os sistemas externos (como páginas da Web, aplicativos ou quiosques) possam solicitar e receber as ofertas apropriadas com base na estratégia de seleção criada anteriormente.
