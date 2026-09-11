---
hold: true
title: Configuração do console do desenvolvedor
description: Crie um projeto do Adobe Developer Console com credenciais OAuth de servidor para servidor para a CLI da DEP para autenticar em sua sandbox.
doc-type: article
solution: Experience Platform
exl-id: 4a7c9e2b-1d3f-4a6e-8b9c-2d5e7f1a3c6b
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---


# Configuração do console do desenvolvedor

> [!NOTE]
>
>Isso só é necessário se você estiver trabalhando nos laboratórios no seu próprio ritmo. Se você estiver em um curso ou evento de treinamento ao vivo, sua sandbox já foi implantada para você.

A DEP CLI é autenticada em sua sandbox usando as credenciais de servidor para servidor do OAuth de um projeto do Adobe Developer Console. Esta página aborda a criação desse projeto. Você só precisa fazer isso uma vez — as mesmas credenciais funcionam nos controles do AEP Foundations e do AJO Architectural Foundations, desde que você adicione ambas as APIs descritas abaixo.

>[!NOTE]
>
>Se você já tiver um projeto do Developer Console com credenciais para o Adobe Experience Platform (e, se necessário, o Adobe Journey Optimizer), ignore esta seção e vá direto para [Instruções de implantação](deployment-instructions.md).

## Pré-requisitos

- Uma Adobe ID com acesso de desenvolvedor à sua organização
- Uma sandbox do Adobe Experience Platform que está vazia e é do tipo `dev`
- Uma função do Adobe Experience Platform com todas as permissões concedidas para essa sandbox (pergunte ao administrador do sistema se não tiver certeza)

## Criar o projeto

1. Ir para [Adobe Developer Console](https://developer.adobe.com/console) e entrar
1. Se você tiver acesso a mais de uma organização, use o alternador de organização na parte superior direita para selecionar a correta
1. Selecione **Criar novo projeto**
1. Renomeie o projeto para algo que você reconhecerá mais tarde (por exemplo, `DEP Sandbox`)

## Adicionar API do Experience Platform

1. Na visão geral do projeto, selecione **Adicionar API**
1. Escolha o ícone do produto **Adobe Experience Platform** e selecione **API Adobe Experience Platform**
1. Selecionar **Próximo**
1. Escolha **OAuth Server-to-Server** como o tipo de autenticação e selecione **Próximo**
1. Dê um nome à credencial e selecione **Próximo**
1. Selecione o perfil de produto que corresponde à sandbox que você usará e selecione **Salvar API configurada**

## Colete seus valores

Abra a página de visão geral do **Servidor para Servidor OAuth** da sua credencial. Você precisa de quatro valores para o arquivo de ambiente da CLI:

| **Valor do Console de Desenvolvimento** | **Campo do arquivo de ambiente** |
| --------------------- | ------------------------------- |
| ID do cliente | `API_KEY` |
| Segredo do cliente | `CLIENT_SECRET` |
| ID da organização | `IMS_ORG` (termina em `@AdobeOrg`) |
| Escopos | `SCOPES` |

>[!NOTE]
>
>Copie os escopos padrão mostrados na página de credenciais — não é necessário adicionar nada manualmente. Se você adicionou ambas as APIs acima, a lista de escopos inclui ambas automaticamente.

Mantenha essa página aberta ou copie esses quatro valores em um local seguro. Você as colará no arquivo de ambiente da CLI na próxima etapa do guia de configuração da sua faixa.
