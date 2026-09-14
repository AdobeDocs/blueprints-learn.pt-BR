---
title: Token de acesso
description: Gere um token de acesso OAuth de servidor para servidor no Postman e entenda os cabeçalhos necessários para autenticar chamadas de API do AEP.
doc-type: article
solution: Experience Platform
exl-id: e38a1bd4-5a09-40c6-8303-c3770801c864
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%
---

# Token de acesso

## Visão geral da segurança da API



Para estabelecer uma conexão de API segura com um produto Adobe, a Adobe fornece a criação de uma credencial OAuth de servidor para servidor. Para fazer isso, primeiro você deve criar um projeto de desenvolvedor no Adobe Developer Console. Para ter acesso ao Developer Console, você deve ter recebido Direitos de desenvolvedor no Adobe Admin Console. Depois de ter esses direitos, você criará projetos de desenvolvedor que utilizam várias APIs relacionadas ao produto do Adobe. Você usa a credencial OAuth de servidor para servidor neste ponto. Para gerar um token de acesso, você deve passar um determinado conjunto de declarações para o Identity Management Service (IMS) da Adobe. Para credenciais de servidor para servidor do OAuth, um exemplo de chamada tem esta aparência:

```curl
curl -X POST 'https://ims-na1.adobelogin.com/ims/token/v3?client_id={CLIENT_ID}' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d 'client_secret={CLIENT_SECRET}&grant_type=client_credentials&scope={SCOPE}'
```

>[!NOTE]
>
>Saiba mais sobre o processo e2e para criar o projeto do desenvolvedor usando as credenciais de servidor para servidor do OAuth [aqui](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/#generate-access-tokens). Para o bootcamp, essa etapa é intencionalmente simplificada.



## Adobe Experience Platform + Adobe IMS

Todas as solicitações para qualquer serviço da Adobe devem incluir o token de acesso no cabeçalho de autorização junto com o segredo do cliente gerado durante a criação do projeto do desenvolvedor. Além disso, o Experience Platform e seus aplicativos associados exigem dois outros parâmetros de cabeçalho em cada solicitação.

- `x-gw-ims-org-id` - esse parâmetro especifica o `IMS Org` ao qual a solicitação pertence e garante que o processamento das solicitações seja resolvido para o ambiente SaaS apropriado
- `x-sandbox-name` - esse parâmetro especifica em qual sandbox processar a solicitação na Experience Platform

Agora que você entende um pouco sobre como o Adobe protege suas APIs e o que é necessário para trabalhar com elas, use-as agora.

>[!CAUTION]
>
>Não especificar o parâmetro `x-sandbox-name` não causa falha na solicitação. Em vez disso, o padrão é que a solicitação seja processada na sandbox `default` que é provisionada automaticamente com qualquer ambiente do Experience Platform

>[!NOTE]
>
>Esta inicialização inclui um projeto de desenvolvedor e um arquivo de Ambiente Postman com todos os valores necessários para solicitar um `access_token`. Esse arquivo de ambiente é o que você carregou nas etapas anteriores do laboratório

## Autenticar com o Postman

1. Inicie o Postman e navegue até o diretório intitulado `IMS Authenticate` e abra a solicitação clicando nele
1. Em seguida, no canto superior direito do Postman, você verá uma lista suspensa de ambientes. Selecione o ambiente `AEP Bootcamp` no menu suspenso
1. Agora execute a chamada clicando no botão &quot;Send&quot;

![Solicitação do Postman após o envio da chamada de Autenticação IMS para gerar um token de acesso](assets/access-token-execute-ims-authenticate-request.png)

Uma resposta bem-sucedida deve ser semelhante a:

```none
200 OK Successful Authentication
```

Resposta bem-sucedida

```json
{
    "token_type": "bearer",
    "access_token": "<value>",
    "expires_in": 86399979
}
```

`token_type` - é sempre do tipo portador

`access_token` - comprova a autorização e é necessária no cabeçalho de autorização de todas as chamadas de API

`expires_in` - milissegundos até que o token de acesso expire (período de expiração de 24 horas hoje)

>[!SUCCESS]
>
>Parabéns! Você foi autenticado com sucesso e seu access\_token foi salvo no arquivo de ambiente



## Erros comuns

### Token inválido

Este erro ocorre quando o `private_key` no arquivo de ambiente está malformado ou não é mais válido. Se você vir esse erro, verifique se copiou toda a chave, incluindo as quebras de linha

Exemplo:

```none
-----BEGIN PRIVATE KEY----- 
some uber long varchar set is here
-----END PRIVATE KEY----- 
```

```none
400 invalid_token
```

>[!NOTE]
>
>Aplicável somente ao usar autenticação baseada em JWT

### IMS\_ORG inválido

Esse erro ocorre quando você esquece de definir o ambiente do Postman na lista suspensa

![IMS_ORG não encontrado no erro de ambiente ativo quando nenhum ambiente do Postman é selecionado](assets/access-token-forgot-to-select-postman-environment.png)

>[!NOTE]
>
>Não se esqueça de definir seu ambiente Postman ao executar chamadas de API
>
>![Selecionando o ambiente AEP Bootcamp no menu suspenso de ambiente Postman](assets/access-token-set-postman-environment.png)
