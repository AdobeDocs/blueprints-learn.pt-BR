---
title: Configuração
description: Conclua as etapas de implantação da sandbox e configuração do Postman necessárias antes de iniciar os laboratórios do AJO Foundations.
doc-type: article

solution: Experience Platform
exl-id: 7c1a9e3d-5b8f-4a2e-9c6d-3f7b0e4a8c2d
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 1%
---

# Configuração

Antes de iniciar os laboratórios do AJO Foundations, conclua as etapas de configuração abaixo. Quais etapas você precisa dependem de como você está tomando este treinamento de inicialização.

## Configuração de sandbox

>[!NOTE]
>
>Se você estiver em um curso ou evento de treinamento ao vivo, sua sandbox já foi implantada para você. Ignore esta seção e vá diretamente para a configuração do Postman abaixo.

Se você ainda não tiver uma sandbox de trabalho com os ativos de laboratório implantados, conclua as seguintes etapas:

- [Configuração do Developer Console](sandbox-setup/developer-console-setup.md)
- [Instruções de implantação](sandbox-setup/deployment-instructions.md)

## Configuração do Postman

A Postman é necessária para os laboratórios neste curso, independentemente de como sua sandbox foi provisionada. Conclua o seguinte antes de continuar:

- [Instalação do Postman](postman-setup/postman-installation.md)
- [Importar arquivo de ambiente](postman-setup/import-environment-file.md)
- [Importar coleção de API](postman-setup/import-api-collection.md)

## Pré-requisitos do canal

Dois laboratórios posteriormente neste treinamento de inicialização dependem de contas externas que somente os alunos individualizados precisam organizar — se você estiver em um curso ou evento de treinamento ao vivo, eles já estão provisionados para você.

### Subdomínio delegado

O laboratório [Configurar canais de email](data-stores/configure-email-channels/overview.md) — e tudo o que depende dele ([Entrega de mensagens em ação](orchestrated-campaigns/message-delivery-in-action/overview.md), [Excitação pós-compra](journeys/post-purchase-excitement/overview.md) e [Marcas da AJO](content-authoring-with-ai/overview.md)) — requer um subdomínio delegado à Adobe para enviar emails. Se você ainda não tiver um domínio, registre-o com qualquer registrador de domínio (por exemplo, Namecheap). Em seguida, para delegar um subdomínio dele (por exemplo, `email.yourdomain.com`) ao Adobe, siga as [instruções de delegação de subdomínio](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/configuration/delegate-subdomains/delegate-subdomain) da Adobe.

>[!NOTE]
>
>A delegação de subdomínio pode levar tempo para se propagar. Inicie essa delegação bem antes de planejar acessar o laboratório Configurar canais de email.

### Credenciais de SMS

O laboratório [Flagship phone launch](orchestrated-campaigns/flagship-phone-launch/overview.md) configura um canal de SMS por meio do Twilio. Nenhuma mensagem é enviada, mas você precisa de credenciais de trabalho para concluir a configuração. A opção mais simples é uma [conta de avaliação do Twilio](https://www.twilio.com/try-twilio) gratuita — consulte o [guia de introdução](https://www.twilio.com/docs/usage/tutorials/how-to-use-your-free-trial-account) do Twilio para saber como se inscrever e encontrar o SID da conta e o Token de autenticação.
