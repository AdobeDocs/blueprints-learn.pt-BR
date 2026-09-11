---
hold: true
title: Validar perfil no hub
description: Saiba como pesquisar um perfil no Real-time Customer Profile Hub e verificar seus eventos e associação de segmento após um evento transmitido.
doc-type: article
solution: Experience Platform
exl-id: f1c8b1ac-e57c-48c6-aa91-5c83f79ce7e3
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# Validar perfil no hub

## Objetivo de aprendizado

Verifique se o evento resultou em uma atualização de perfil e qualificação de segmento no Perfil em tempo real no Hub.

## Pesquisar o perfil no hub

Na Adobe Experience Platform, procure o perfil que você acabou de enviar a partir do evento que acabou de enviar para a Edge Network.

1. Navegue até **Cliente** -> **Perfis** -> **Procurar** para realizar a pesquisa usando estas informações:
   - **Política de mesclagem** -> `Default Timebased`
   - **Namespace de Identidade** -> `Email`
   - **Valor de Identidade** -> `henry.creel@emailsim.io`
1. Clique em **Exibir** para pesquisar o perfil

![Procurar tela de perfil com campos de pesquisa de identidade e política de mesclagem](assets/validate-profile-on-hub-browse-profile-lookup.png)



## Verifique o perfil do hub

1. Clique na **ID do Perfil** para abrir o perfil
1. Clique primeiro na guia **Atributos** e depois no botão de opção **Hub** para ver o **Perfil de Hub**

![Perfil de Hub mostrado na guia Atributos](assets/validate-profile-on-hub-attributes-tab.png)


## Validar eventos

1. Clique em **Eventos** na navegação superior para ver o evento que acabou de enviar

![Guia Eventos mostrando o evento transmitido no perfil](assets/validate-profile-on-hub-events-tab.png)

## Validar segmentos

### Via JSON

1. Clique no cabeçalho **Atributos** e exiba **JSON**

![Exibição JSON de atributos de perfil mostrando segmentMembership](assets/validate-profile-on-hub-json-view.png)

2. Localizar **segmentMembership**.  Deve ficar assim (suas IDs serão diferentes)

```json
  "segmentMembership": {
    "ups": {
      "ce0b8386-ef2a-4244-8ad0-1a72d6494181": {
        "status": "realized",
        "lastQualificationTime": "2025-12-15T23:11:49Z"
      },
      "8ce516fe-920a-4f9d-b92b-0403890a8491": {
        "status": "realized",
        "lastQualificationTime": "2025-12-12T15:01:01Z"
      }
    }
```

>[!NOTE]
>
>**Como ler segmentMembership?**
>
>[https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/segmentation](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/segmentation)
>
>**ups:** esta é a chave de mapa para diferentes tipos de públicos suportados pelo AEP.  A chave ups contém públicos-alvo criados pelo Construtor de regras.  Outros públicos-alvo estarão contidos em outras chaves (por exemplo, AAM).
>
>**lastQualificationTime** Um carimbo de data/hora da última vez que esse perfil se qualificou para o segmento
>
>**status**
>
>*realizado*: o perfil se qualifica para o segmento.
>*encerrado*: o perfil está saindo do segmento como parte da solicitação atual.
>
>

### Via IU

1. Uma maneira mais fácil de validar o Perfil qualificado para os Públicos é observar a guia **Associação de público-alvo** (você deve ver pelo menos isso):
   - dep: Qualquer transmissão de evento (dentro de uma hora)
   - dep: Qualquer Edge de evento (em uma hora)

![Guia Associação de público-alvo mostrando segmentos qualificados](assets/validate-profile-on-hub-audience-membership-tab.png)

>[!NOTE]
>
>**Por que nenhum público-alvo em lote?**
>
>Você não deve ver **dep: qualquer lote de eventos (dentro do dia)** qualificado para, pois transmitimos dados e a avaliação em lote acontece uma vez por dia.

## Recapitulação

Existe um perfil no Hub que está qualificado para o público-alvo esperado.
