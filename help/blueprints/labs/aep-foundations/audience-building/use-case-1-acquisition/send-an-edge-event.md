---
hold: true
title: Enviar um evento do Edge
description: Envie um evento da Web não autenticado para a Edge por meio do Postman e rastreie-o pelo encaminhamento de eventos, assimilação de perfis, qualificação de público-alvo e ativação de destino.
doc-type: article
solution: Experience Platform
exl-id: 465d09da-e30f-404c-8778-5df06e5a199f
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 0%

---


# Enviar um evento do Edge

Agora que tudo está configurado, envie um evento para a Edge para ver se tudo funciona. Para fazer isso, use o Postman para enviar um Evento da Web para a sequência de dados criada. Isso envia um evento **sem token OAuth** para simular uma exibição de página da Web para a Edge.  Certifique-se de ter o Postman aberto no computador para executar esse laboratório.

>[!NOTE]
>
>Como você não está transmitindo um token autenticado, não recupera nenhum atributo.

## Expectativas do laboratório

1. Evento de experiência para acessar o Edge
1. Configuração de sequência de dados para usar o Serviço de encaminhamento de eventos
1. Encaminhamento de eventos para enviar o Evento para o webhook
1. Configuração de sequência de dados para usar o serviço do AEP
   1. Público-alvo do Edge a ser executado
   2. Enviar evento para o hub
1. Resposta do Postman para incluir o público-alvo da Edge (mas sem atributos)
1. Armazenar perfis para receber eventos e adicionar um fragmento de perfil de evento
1. Repositório de Identidades para adicionar um relacionamento
1. Conjunto de dados para receber dados e armazenar no Data Lake
1. Públicos-alvo de transmissão para avaliar e armazenar resultados no Perfil no Hub
1. Destinos personalizados do Personalization para enviar quaisquer &quot;entradas&quot; de públicos-alvo de transmissão de volta para a Edge
1. HTTP API Destinations para enviar quaisquer &quot;entradas&quot; de públicos-alvo de streaming para o webhook
1. Eventualmente, os destinos da API HTTP enviam quaisquer &quot;saídas&quot; de públicos-alvo de transmissão para o webhook
1. Eventualmente, os destinos personalizados do Personalization enviam quaisquer &quot;saídas&quot; de públicos-alvo de transmissão para a Edge



## Navegue até a chamada

1. **Barra Lateral Esquerda do Postman** -> Coleções
1. **Coleção** -> Inicializações do AEP Foundations (Labs)
1. **Pasta** -> Laboratório de perfis
1. **Solicitação de API** -> Criar Edge de Eventos da Web (Sem Autenticação)

![Abrir a solicitação Criar Edge de Eventos da Web (Sem Autenticação) no Postman](assets/send-an-edge-event-navigate-to-the-postman-call.png)

## Modificar solicitação de API

Se já tiver feito isso, você pode pular para Executar a API.

Antes de executar a solicitação da API, é necessário adicionar algumas informações adicionais à solicitação. Comece reunindo os seguintes valores:

## Coletar a ID do fluxo de dados

1. No painel à esquerda, clique em **Fluxos de dados** (no cabeçalho Coleção de dados)
1. Selecione sua sequência de dados e copie o valor de **ID da sequência de dados**

![Copiar o valor de ID da Sequência de Dados](assets/send-an-edge-event-gather-datastream-id.png)

## Atualizar parâmetro de consulta do Postman

1. Na própria solicitação, clique em **Params**
1. Atualize o **Valor** com a ID de sequência de dados da etapa anterior
1. Clique no botão **Salvar** para salvar sua atualização
1. Alterar email para seu email

![Atualize o valor Params com a ID de sequência de dados e clique em Salvar](assets/send-an-edge-event-update-datastreamid.png)

![Altere o valor do email no corpo da solicitação para seu próprio email](assets/send-an-edge-event-change-email-to-your-email.png)

## Executar a API

Execute sua solicitação clicando no botão **Enviar**.

![Resposta 200 OK bem-sucedida retornada da Edge Network](assets/send-an-edge-event-successful-response-from-edge.png)



O que você deve ver na resposta são estes itens principais:

- Uma resposta 200 OK significa que os dados foram enviados e aceitos com êxito pelo Edge Network
- Na resposta da carga útil, você também deve ver o seguinte:
  - o destinationId do destino do Personalization personalizado que você configurou
  - o nome do alias desse destino (o seu foi chamado de customPersonalization)
  - qualquer segmento para o qual o perfil se qualificou que exista na borda

>[!NOTE]
>
>Quaisquer segmentos em lote e de streaming não são exibidos até que sejam avaliados no hub primeiro

>[!NOTE]
>
>Se você enviasse para server.adobedc.net usando um token de portador, também veria o atributo configurado no Destino personalizado do Personalization

## Erros que você pode encontrar

Veja abaixo um exemplo de um erro que você pode encontrar. Isso significa que a avaliação da segmentação de borda ainda não está disponível para avaliar os dados que estão sendo enviados para a rede de borda.

```none
"errors": [
        {
            "type": "https://ns.adobe.com/aep/errors/EXEG-0203-502",
            "status": 502,
            "title": "The service call has failed.",
            "detail": "An error occurred while calling the 'com.adobe.experience_platform.edge_segmentation' service for this request. Try again.",
            "report": {
                "eventIndex": 0
            }
        }
    ]
```

## Validar o encaminhamento de eventos

No webhook.site, você deve ver imediatamente o mesmo corpo de carga enviado por meio de sua solicitação do Postman exibido.

![A carga aparece no webhook.site após o encaminhamento de eventos](assets/send-an-edge-event-payload-appears-on-webhook-site.png)

>[!NOTE]
>
>Observe que a carga adicionou as informações de pesquisa geográfica solicitadas ao configurar o fluxo de dados usado na configuração do Edge

## Pesquisar o perfil

Na Adobe Experience Platform, procure o perfil que você acabou de enviar a partir do evento que acabou de enviar para a Edge Network.  Navegue até Perfis -> Procurar para executar a pesquisa usando as seguintes informações:

- Política de mesclagem -> Baseada no tempo padrão
- Namespace de identidade -> Email
- Valor de identidade -> edge-email\@dep.com



1. Clique em **Exibir** para pesquisar o perfil
1. Clique na **ID do Perfil** para abrir o perfil

![Pesquise o perfil e clique na ID do Perfil para abri-lo](assets/send-an-edge-event-lookup-profile.png)



&#x200B;3. Clique em **Eventos** na navegação superior para ver o evento que acabou de enviar

![Exibir o evento na guia Eventos do perfil](assets/send-an-edge-event-view-the-profile-event.png)



&#x200B;4. Confirme se o Perfil se qualificou para os Públicos revisando a guia Associação de público-alvo na navegação superior.  Você deve ver o seguinte:

- Qualquer Edge de evento (nos últimos 15 minutos)
- Qualquer transmissão de evento (na última hora)
- No caso de uso #1, você também deve ver os públicos de:
  - Visitou a página 14 do iPhone, mas não é seu/o solicitou
  - Página do iPhone 14 visitada

![Perfil qualificado para os públicos-alvo de 14 páginas do iPhone visitados](assets/send-an-edge-event-visited-iphone-14-page.png)

## Validar ativação de destino de streaming

Verifique seu webhook para ver se o destino de transmissão configurado ativou segmentos.  Eles devem aparecer em \~5 minutos.

![Validar os segmentos ativados do destino de streaming no webhook](assets/send-an-edge-event-validate-streaming-destination-activation.png)

>[!NOTE]
>
>Os Destinos de transmissão podem enviar outra carga de qualificação de segmento se as duas identidades ainda não tiverem sido vinculadas.

Se a ECID e o email ainda não tiverem sido vinculados, alguns minutos depois disso, outra carga poderá aparecer com os mesmos valores, exceto que identityMap terá duas identidades (email e ecid)

Com o tempo, você deve começar a receber mais cargas no webhook para o status &quot;encerrado&quot;.

![Carga do Webhook mostrando um status &quot;encerrado&quot; para o destino de streaming](assets/send-an-edge-event-webhook-exited-status-payload.png)

## Como interpretar todas as verificações

1. Verifique a resposta 200 no Postman (carga adequadamente formatada)
1. Verifique se o webhook tem o evento (Encaminhamento de evento configurado corretamente)
1. Verifique se o perfil tem os eventos (serviço AEP corretamente configurado, evento recebido e evento processado no hub)
1. Verifique se o perfil tem duas identidades (o gráfico de identidade está vinculado no Hub)
1. Verifique se o Perfil se qualificou para os públicos-alvo (público-alvo definido corretamente)
1. Verifique se o webhook recebeu o Streaming Audiences (Destino da API HTTP configurado corretamente)
1. Verifique se a resposta do Postman inclui segmentos (Destino personalizado do Personalization configurado corretamente)
1. Verifique se o Data Lake tem um log de envio (Qualificação de público-alvo e Destino de transmissão corretamente configurados e enviados). Consulte Abaixo.

## &quot;Log&quot; de destinos do Data Lake

Após pelo menos 60 minutos, é possível até verificar se o conjunto de dados tem o evento enviado. Para fazer isso, execute a consulta a seguir usando o Serviço de consulta.

Altere o nome da tabela abaixo para o da sua sandbox. Para encontrá-lo, vá para a lista de conjuntos de dados e filtre por &quot;`dest`&quot;, abra o conjunto de dados e copie o nome da tabela no painel direito.

```sql
SELECT * FROM profile_export_for_destination_merge_policy_xxx
WHERE extSourceSystemAudit.LASTREFERENCEDDATE >= CURRENT_DATE
AND identitymap['email'][0].ID in ('edge-email@dep.com')
ORDER BY extSourceSystemAudit.LASTREFERENCEDDATE DESC
LIMIT 10
```
