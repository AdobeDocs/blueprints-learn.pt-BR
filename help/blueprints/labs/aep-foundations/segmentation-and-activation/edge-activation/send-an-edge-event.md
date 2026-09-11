---
hold: true
title: Enviar um evento do Edge
description: Envie um evento da Web não autenticado para a Edge por meio do Postman e verifique se ele flui por meio do encaminhamento de eventos, da assimilação de perfis e da qualificação de público-alvo de borda.
doc-type: article
solution: Experience Platform
exl-id: 8d6e9552-1fa0-4f12-928c-03f836c1652e
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---


# Enviar um evento do Edge

Agora que tudo está configurado, envie um evento para a Edge para ver se tudo funciona.

Para fazer isso, use o Postman para enviar um Evento da Web para a sequência de dados criada.

Isso envia um evento **sem token OAuth** para simular uma exibição de página da Web para a Edge.  Certifique-se de ter o Postman aberto no computador para executar esse laboratório.

>[!NOTE]
>
>Como você não está transmitindo um token autenticado, não recupera nenhum atributo.

## Expectativas do laboratório

1. Evento de experiência para acessar o Edge
1. Configuração de sequência de dados para usar o Serviço de encaminhamento de eventos
1. Encaminhamento de eventos para enviar o Evento para o webhook
1. Configuração de sequência de dados para usar o serviço do AEP
   1. Público-alvo do Edge a ser executado
   1. Enviar evento para o hub
1. Resposta do Postman para incluir o público-alvo da Edge (mas sem atributos)
1. Armazenar perfis para receber eventos e adicionar um fragmento de perfil de evento
1. Repositório de Identidades para adicionar um relacionamento
1. Conjunto de dados para receber dados e armazenar no Data Lake



## Navegue até a chamada

1. **Barra Lateral Esquerda do Postman** -> Coleções
1. **Coleção** -> Inicializações do AEP Foundations (Labs)
1. **Pasta** -> Laboratório de perfis
1. **Solicitação de API** -> Criar Edge de Eventos da Web (Sem Autenticação)

![Navegação na barra lateral do Postman para a solicitação de API Criar Edge de Eventos da Web (Sem Autenticação) na pasta Profile Lab](assets/send-an-edge-event-navigate-to-the-postman-call.png)

## Modificar solicitação de API

Antes de executar a solicitação da API, é necessário adicionar algumas informações adicionais à solicitação. Comece reunindo os seguintes valores:

## Coletar a ID do fluxo de dados

1. No painel à esquerda, clique em **Fluxos de dados** (no cabeçalho Coleção de dados)
1. Selecione sua sequência de dados e copie o valor de **ID da sequência de dados**

![Lista de Datastreams com o valor de ID de Datastream realçado para cópia](assets/send-an-edge-event-gather-datastream-id.png)

## Atualizar parâmetro de consulta do Postman

1. Na própria solicitação, clique em **Params**
1. Atualize o **Valor** com a ID de sequência de dados da etapa anterior
1. Clique no botão **Salvar** para salvar sua atualização

![Guia Postman Params com o valor de ID de sequência de dados colado no campo Valor](assets/send-an-edge-event-update-datastream-id-param.png "Update dataStreamId")



Alterar email para seu email

![corpo da solicitação do Postman mostrando o valor do email atualizado para o próprio endereço de email do testador](assets/send-an-edge-event-change-email-param.png "Alterar email para seu email")

## Executar a API

Execute sua solicitação clicando no botão **Enviar**.

![Botão Enviar do Postman sendo clicado para executar a solicitação Criar Edge de Evento da Web](assets/send-an-edge-event-execute-request.png)

O que você deve ver na resposta é esse aspecto principal:

- Uma resposta 200 OK significa que os dados foram enviados e aceitos com êxito pelo Edge Network

>[!NOTE]
>
>Quaisquer segmentos em lote e de streaming não são exibidos até que sejam avaliados no hub primeiro

## Validar o encaminhamento de eventos

No webhook.site, você deve ver imediatamente o mesmo corpo de carga enviado por meio de sua solicitação do Postman exibido.

![Webhook.site mostrando a carga do evento encaminhado recebida do Encaminhamento de Eventos](assets/send-an-edge-event-webhook-payload.png)

>[!NOTE]
>
>Observe que a carga adicionou as informações de pesquisa geográfica solicitadas ao configurar o fluxo de dados usado na configuração do Edge

## Pesquisar o perfil

Na Adobe Experience Platform, procure o perfil que você acabou de enviar a partir do evento que acabou de enviar para a Edge Network. Navegue até Perfis -> Procurar para executar a pesquisa usando as seguintes informações:

- Política de mesclagem -> Baseada no tempo padrão
- Namespace de identidade -> Email
- Valor de identidade -> edge-email\@dep.com
  - Observação: altere para corresponder ao email que você usou na etapa *Atualizar parâmetro de consulta do Postman* acima

1. Clique em **Exibir** para pesquisar o perfil
1. Clique na **ID do Perfil** para abrir o perfil

![Resultados da pesquisa de Procura de Perfil com o link Exibir para abrir o perfil correspondente](assets/send-an-edge-event-lookup-profile.png "Perfil de pesquisa")

1. Clique em **Eventos** na navegação superior para ver o evento que acabou de enviar

![Guia Eventos de perfil mostrando o evento de experiência que acabou de ser enviado à Edge](assets/send-an-edge-event-view-profile-event.png "Exibir o evento de perfil")

1. Confirme se o Perfil se qualificou para os Públicos revisando a guia Associação de público-alvo na navegação superior. Você deve ver o seguinte:

- Qualquer Edge de evento (em 15 minutos)
- dep: Qualquer transmissão de evento (dentro de uma hora)

![Guia Associação de Público-Alvo mostrando qualificação para Qualquer Edge de Evento e dep: Qualquer Público-Alvo de Streaming de Eventos](assets/send-an-edge-event-any-event-streaming-within-the-last-hour.png)

## Como interpretar as verificações

1. Verifique a resposta 200 no Postman (carga adequadamente formatada)
1. Verifique se o webhook tem o evento (Encaminhamento de evento configurado corretamente)
1. Verifique se o perfil tem os eventos (serviço AEP corretamente configurado, evento recebido e evento processado no hub)
1. Verifique se o perfil tem duas identidades (o gráfico de identidade está vinculado ao Hub) após alguns minutos
1. Verifique se o Perfil se qualificou para os públicos-alvo (público-alvo definido corretamente)
1. Verifique se o Data Lake tem o evento.
