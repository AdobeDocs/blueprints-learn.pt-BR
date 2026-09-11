---
title: Monitorar o evento
description: Use o Adobe Experience Platform Assurance para criar uma sessão de depuração, enviar um evento validado pelo Postman e inspecionar logs de processamento de eventos de borda.
doc-type: article
solution: Experience Platform
exl-id: 94b200c0-6714-4996-a266-119cc8f7f4e2
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 1%

---


# Monitorar o evento

## Navegar até o Assurance

O [Adobe Experience Platform Assurance](https://experienceleague.adobe.com/pt-br/docs/experience-platform/assurance/home) é um produto da Adobe Experience Cloud que ajuda a inspecionar, testar, simular e validar a maneira como você coleta dados no Adobe Experience Platform Edge.

1. Acesse Adobe Experience Platform -> Assurance -> Criar sessão

   ![Navegue até o Adobe Experience Platform Assurance e crie uma sessão](assets/monitor-your-event-navigate-to-assurance-create-session.png)



2. Clique no botão **Iniciar**

![Clique no botão Iniciar para começar a configurar a sessão do Assurance](assets/monitor-your-event-click-start-button.png)



## Configurar uma sessão

1. Nome —> \[Sandbox] Sessão do Edge
1. URL —> https\://www\.adobe.com
   - Observe que este URL seria substituído pelo site real do seu cliente
1. Clique no botão Avançar

   ![Clique em Avançar depois de inserir o nome da sessão e a URL](assets/monitor-your-event-click-next-button.png)

4. Copie o link em algum lugar que possa ser referenciado mais tarde

5. Clique no botão **Concluído**

   ![Copie o link da sessão do Assurance e clique em Concluído](assets/monitor-your-event-copy-link.png)



6. Navegue até **Configurações**

   ![Navegue até a guia Configurações na sessão do Assurance](assets/monitor-your-event-navigate-to-settings.png "Clique nas configurações")



7. Habilite **Transações de Evento** e **Edge Delivery** clicando no botão **+** e **Concluído**

![Habilite as Transações de Evento e o Edge Delivery e clique em Concluído](assets/monitor-your-event-enable-event-transactions-and-edge-delivery.png)


## Abrir Postman

Acesse Postman -> Criar Edge de evento da Web (Sem autenticação) -> Cabeçalhos

1. Adicione o **x-adobe-aep-validation-token** aos cabeçalhos com o link copiado acima do Assurance. Pegue **apenas o valor de ID** depois de = no link copiado do Assurance. ex.: [https://www.adobe.com/?adb\_validation\_sessionid=](https://www.adobe.com/?adb_validation_sessionid=efa4a9ed-02d8-4647-80fa-f01a5be273d0)[`efa4a9ed-02d8-4647-80fa-f01a5be273d0`](https://www.adobe.com/?adb_validation_sessionid=efa4a9ed-02d8-4647-80fa-f01a5be273d0)
1. Usaríamos apenas o valor [`efa4a9ed-02d8-4647-80fa-f01a5be273d0`](https://www.adobe.com/?adb_validation_sessionid=efa4a9ed-02d8-4647-80fa-f01a5be273d0), não a URL completa

   ![Adicione o cabeçalho x-adobe-aep-validation-token com a ID de sessão do Assurance no Postman](assets/monitor-your-event-populate-the-x-adobe-aep-validation-token.png)



3. No Postman, salve e execute a solicitação **Criar Edge de Eventos da Web (Sem Autenticação)**



## Exibir logs do Assurance

Volte para o Assurance e você verá vários eventos sendo exibidos. Filtre apenas os tipos de evento relevantes, colocando a ID da sequência de dados na pesquisa

![Filtre eventos do Assurance procurando pela ID da sequência de dados](assets/monitor-your-event-filter-using-search.png)



Selecione um evento e abra as mensagens, se necessário, no painel direito.

![Selecione um evento e expanda suas mensagens no painel direito](assets/monitor-your-event-expand-messages.png)

Tipos de evento a serem procurados:

- hitReceived (mostra a carga recebida pelo Edge)
- evaluationRule (se você configurar o SSF, mostra regras que estão sendo avaliadas)
- fireDestinations (para quais destinos isso foi enviado)
- segmentsDiscovered (qualificou-se para algum segmento de borda)
- com.adobe.experience\_platform.edge\_segmentation/response (com quais segmentos ele respondeu)

![Selecione cada tipo de evento para ver como o Assurance o interpreta](assets/monitor-your-event-select-each-event.png)

Explore-as e veja como cada etapa é interpretada pelo Assurance.
