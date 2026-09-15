---
title: APIs de perfil e identidade
description: Use a API de entidade de perfil e a API de cluster do serviço de identidade no Postman para pesquisar atributos de perfil, eventos e identidades vinculadas.
doc-type: article
solution: Experience Platform
exl-id: 1db55c5b-fdf8-4c63-b435-477626bb0450
source-git-commit: 8b3391d41cd4a3ea6cb52d5167e627b7f6bd2c6e
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 1%
---

# APIs de perfil e identidade

>[!IMPORTANT]
>
>Conclua a [configuração do Postman](../../setup.md) antes de iniciar os exercícios da API de Perfil e Identidade.

## API da entidade de perfil

Saber como utilizar as APIs de perfil é essencial para trabalhar com o Perfil do cliente em tempo real. Ela permite uma triagem e depuração rápidas, além de expor você a várias integrações de sistema possíveis, de call centers a quiosques.

Uma das APIs mais importantes é a API da entidade de perfil. Essa API permite pesquisar um perfil individual, como você viu na interface do usuário do. Ele usa parâmetros para determinar se você deseja ver os atributos ou eventos do perfil.

Abaixo está a especificação completa do método GET para a API de entidade de perfil


## Visão geral da API

Abaixo estão as informações mínimas necessárias para chamar a API da entidade de perfil.

`GET https://platform.adobe.io/data/core/ups/access/entities`

### Parâmetro de consulta obrigatório

Envie este parâmetro com cada solicitação. O valor depende se você está pesquisando os atributos de um perfil ou seus eventos:

| Parâmetro | Tipo | Descrição | Exemplo |
| ------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------ |
| `schema.name` | string | Nome da classe de esquema XDM da entidade que você está pesquisando. | `_xdm.context.profile` |
| `schema.name` | string | Em vez disso, use esse valor para pesquisar os eventos de um perfil. Emparelhe-o com `relatedSchema.name=_xdm.context.profile` para definir o escopo dos eventos para um perfil. | `_xdm.context.experienceevent` |

### Identificação da entidade a ser pesquisada

A maioria das solicitações usa `entityId` e `entityIdNS` para identificar a entidade por qualquer valor de identidade conhecido — como um endereço de email, ID de CRM ou ID de fidelidade — em vez de exigir que você já saiba seu XID. Um XID é um identificador codificado na base64 que o Serviço de Identidade gera e atribui internamente para representar uma identidade, consolidando seu namespace e valor de ID em um único token compacto (consulte [XID Nativo](https://experienceleague.adobe.com/docs/experience-platform/identity/api/list-native-id.html?lang=pt-BR) para obter detalhes):

| Parâmetro | Tipo | Descrição | Exemplo |
| ------------ | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| `entityId` | string | O valor do identificador a ser pesquisado. Se você já conhece o XID da entidade, use-o aqui sozinho e omita `entityIdNS`. | `depeche.mode@dep.com` |
| `entityIdNS` | string | Código de namespace de identidade ao qual `entityId` pertence (por exemplo, `email`, `crmid`, `ECID`). Necessário sempre que `entityId` ainda não for um XID. | `email` |

>[!NOTE]
>
>As solicitações do Postman deste laboratório procuram o perfil do Modo de profundidade pelo seu endereço de email (`entityIdNS=email`, `entityId=depeche.mode@dep.com`) em vez de seu XID.

### Cabeçalhos obrigatórios

Cada solicitação também precisa destes cabeçalhos:

| Cabeçalho | Tipo | Descrição | Exemplo |
| ----------------- | ------ | ---------------------------------------------- | --------------------- |
| `x-gw-ims-org-id` | string | IMS Organization ID. | `<your IMS org>` |
| `x-api-key` | string | Chave de API do projeto/credencial registrado. | `<your API key>` |
| `Authorization` | string | Token de portador da solicitação. | `Bearer <your token>` |

>[!NOTE]
>
>Consulte a [Referência da API de Entidades de Perfil](https://developer.adobe.com/experience-platform-apis/references/profile#tag/Entities) para obter a lista completa de parâmetros de consulta, incluindo opções adicionais de pesquisa de identidade, filtragem de eventos (`startTime`, `endTime`, `property`, `orderby`, `limit`), seleção de campos e substituições de políticas de mesclagem.

>[!WARNING]
>
>Lembre-se de que todas as solicitações de API são específicas da sandbox, portanto, é importante, ao trabalhar com as APIs, garantir que o parâmetro de cabeçalho em cada solicitação chamada `x-sandbox-name` seja definido corretamente como a sandbox apropriada.
>
>Para este laboratório, você já tem o `x-sandbox-name` definido em seu arquivo de ambiente

## Pesquisa de entidade (atributos)

Para se familiarizar com a API de pesquisa de entidade, use o perfil Modo de profundidade do laboratório anterior.

1. Abra o **Postman** e navegue até a pasta **Laboratório de Perfis**
1. Clique na solicitação **Pesquisa de Entidade (atributos)** para abri-la
1. Execute a chamada clicando no botão **Enviar**

   ![Painel de solicitações do Postman para a chamada Pesquisa de Entidade (atributos) antes de enviar](assets/profile-and-identity-apis-entity-lookup-attributes-request.png "API de Pesquisa de Entidade de Perfil (atributos)")

   Uma solicitação bem-sucedida deve responder com um `200 OK` e você deve ver um resultado que contenha todos os atributos do perfil Modo de profundidade.

   ![Resposta OK 200 contendo todos os atributos para o perfil do Modo de Execução](assets/profile-and-identity-apis-successful-attributes-api-response.png "Resposta de API (atributos) de Entidade de Perfil com Êxito")

   >[!NOTE]
   >
   >Por padrão, se nenhuma política de mesclagem for especificada em uma solicitação de entidade de perfil, ela usará a política de mesclagem padrão na sandbox

   Com a API de entidade, use os parâmetros de consulta para alterar o que é retornado em resposta.

1. Na solicitação de Pesquisa de Entidade (atributos), clique na opção **Params** para a solicitação
1. Marque a caixa ao lado de **Chave** chamada **campos**
1. Execute a solicitação clicando no botão **Enviar**

![Solicitação de Pesquisa de Entidade (atributos) com o parâmetro fields habilitado para filtrar a resposta](assets/profile-and-identity-apis-entity-lookup-attributes-with-filter-enabled.png)

>[!NOTE]
>
>Observe que também há um parâmetro para especificar o `mergePolicyId`. Para localizar o valor desse, use outras APIs ou procure a ID usando a interface do.

Uma solicitação bem-sucedida deve responder com um `200 OK` e você deve ver apenas os campos especificados no filtro de parâmetros que acabou de habilitar: Nome, Sobrenome e uma matriz de Produtos Ativos.

![Resposta 200 OK filtrada mostrando apenas campos de Nome, Sobrenome e Produtos Ativos](assets/profile-and-identity-apis-successful-filtered-attributes-response.png "Pesquisa de Entidade de Perfil com Êxito (atributos) Resposta de API com filtro habilitado")

>[!SUCCESS]
>
>Parabéns!  Você pesquisou com êxito os atributos de um perfil usando a API de entidade de perfil

## Pesquisa de entidade (eventos)

Para pesquisar os eventos de um perfil, use a mesma API de entidade de perfil exata.  A única diferença é que você precisa informar ao serviço de perfil que deseja alterar o tipo de classe a ser usado na resposta.

1. Clique na solicitação **Pesquisa de Entidade (eventos)** para abri-la
1. Execute a chamada clicando no botão **Enviar**

![Painel de solicitações do Postman para a chamada de Pesquisa de Entidade (eventos) antes de enviar](assets/profile-and-identity-apis-entity-lookup-events-request.png)

Uma solicitação bem-sucedida deve responder com um `200 OK` e você deve ver um resultado que contenha todos os eventos do perfil Modo de espera.



![Resposta OK 200 contendo todos os eventos para o perfil do Modo de Execução](assets/profile-and-identity-apis-successful-events-api-response.png "Pesquisa de Entidade de Perfil Bem-sucedida (eventos) Resposta de API")

Quando você pesquisa atributos de perfil, a API de entidade tem ainda mais parâmetros de consulta que alteram o que é retornado em resposta.

Experimente alguns deles, ativando-os na seção Params e executando a solicitação. Veja como funciona!

![Solicitação de Pesquisa de Entidade (eventos) com parâmetros de consulta adicionais habilitados na seção Params](assets/profile-and-identity-apis-entity-lookup-events-query-params.png "Pesquisa de Entidade de Perfil para Eventos de Experiência")

**Definições do parâmetro de consulta de exemplo**

| Chave | Valor | Descrição |
| ------------- | ------------------------------- | ------------------------------------------------------------------------------------------------------- |
| mergePolicyId | \&lt;blank> | Alterna a política de mesclagem usada para a pesquisa. Deixá-lo em branco usa a política de mesclagem padrão da sandbox |
| campos | eventType,timestamp,identityMap | Exibe somente esses campos de cada evento, tenham ou não um valor |
| propriedade | eventType=&quot;order.placement&quot; | Filtra os eventos somente para aqueles do tipo especificado |
| orderby | +carimbo de data e hora | Classifica eventos em ordem crescente |
| limite | 5 | Mostra apenas 5 eventos na resposta |

>[!NOTE]
>
>Saiba mais sobre todas as opções de Parâmetro de Consulta aqui -> [https://developer.adobe.com/experience-platform-apis/references/profile/#tag/Entities/operation/retrieveEntity](https://developer.adobe.com/experience-platform-apis/references/profile/#tag/Entities/operation/retrieveEntity)



## API do cluster do serviço de identidade

Em algum momento, você pode ter uma pergunta sobre quais identidades fazem parte de um cluster de identidades de um perfil específico no gráfico de identidade.  Essa API permite passar um único namespace/valor de identidade e, em resposta, você recebe o cluster de identidade completo para esse perfil.

Experimente você mesmo:

1. Clique na solicitação **Listar identidades vinculadas** para abri-la
1. Execute a chamada clicando no botão **Enviar**

>[!NOTE]
>
>Observe que os parâmetros na solicitação são o namespace e a id de identidade (ou seja, o valor)



![Painel de solicitações do Postman para a chamada de Listar Identidades Vinculadas antes de enviar](assets/profile-and-identity-apis-list-linked-identities-request.png "API de Identidades Vinculadas da Lista")

Uma resposta bem-sucedida deve se parecer com a captura de tela abaixo



![Resposta de Identidades Vinculadas da Lista Bem-sucedida mostrando todas as identidades do perfil do Modo de Execução](assets/profile-and-identity-apis-successful-list-linked-identities-response.png)

>[!NOTE]
>
>Observe que a resposta contém todas as identidades do perfil Modo de detecção
