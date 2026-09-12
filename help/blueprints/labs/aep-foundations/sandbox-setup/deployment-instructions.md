---
title: Instruções de implantação
description: Use a CLI da DEP para implantar os esquemas, conjuntos de dados, fluxos de dados e dados de perfil de amostra do pacote de laboratório do AEP Foundations em sua sandbox.
doc-type: article
solution: Experience Platform
exl-id: 9f2b6d4a-8e1c-4b7a-a3d5-6c9f0e2a4b8d
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 1%

---


# Instruções de implantação

>[!NOTE]
>
>Isso só é necessário se você estiver trabalhando nos laboratórios no seu próprio ritmo. Se você estiver em um curso ou evento de treinamento ao vivo, sua sandbox já foi implantada para você.

O pacote de laboratório do AEP Foundations é implantado em sua sandbox usando a DEP CLI, uma ferramenta de linha de comando que cria esquemas, conjuntos de dados, fluxos de dados e dados de amostra que você usará em todos os laboratórios.

## O que é implantado

- 4 namespaces de identidade
- 1 classe de esquema, 13 grupos de campos, 10 esquemas
- 12 descritores de identidade, 6 descritores de relacionamento/referência, 3 descritores de nome amigáveis
- 10 conjuntos de dados de catálogo
- 1 conexão de origem da API HTTP e 10 fluxos de dados
- Dados do perfil: um único perfil do Modo de detecção (três conjuntos de dados de características, sete conjuntos de dados de eventos) e três conjuntos de dados de pesquisa
- Duas políticas de mesclagem de perfis e um público-alvo (qualquer transmissão de evento, em uma hora)

>[!NOTE]
>
>A implantação completa leva cerca de 2 horas e 24 minutos, a maioria dos quais é tempo de espera autônomo entre as etapas. A CLI impõe essas esperas automaticamente, de modo que você mesmo não precisa cronometrar nada.

## Pré-requisitos

- **Direitos de licença.** Privilégios administrativos para uma Organização IMS com o Real-Time CDP (com segmentação por transmissão)
- **Direitos de Acesso.** Uma função Adobe Experience Platform com todas as permissões na sandbox de destino, incluindo a credencial de API que você criou a partir da [Instalação do Developer Console](developer-console-setup.md).
- **Credenciais do Developer Console.** Um projeto que inclui APIs do Adobe Experience Platform. Se você ainda não os tiver, siga a [Instalação do Developer Console](developer-console-setup.md) primeiro
- **Uma sandbox.** Vazio, do tipo `dev` e em um estado &quot;Pronto&quot; por pelo menos 60 minutos antes de você iniciar a implantação
- **Node.js.** Qualquer versão recente do LTS, no Windows ou no Mac

## &#x200B;1. Instalar a CLI

1. Clonar ou baixar o [repositório dep-cli](https://github.com/adobe/dep-cli)
1. No diretório `dep-cli`, execute `npm install`
1. Iniciar a CLI com `npm start`

>[!NOTE]
>
>O Node.js é necessário antes de executar os comandos acima. Se você ainda não tiver o Node.js instalado, consulte a página [Configuração do Node.js](https://github.com/adobe/dep-cli/wiki/Nodejs-Setup)da wiki. Para obter detalhes completos sobre a instalação, incluindo capturas de tela e como atualizar uma instalação existente, consulte a página wiki [Instalação](https://github.com/adobe/dep-cli/wiki/Installation)

## &#x200B;2. Configurar o arquivo de ambiente

A CLI é implantada na sandbox para a qual o arquivo de ambiente aponta. Portanto, isso deve ser configurado corretamente antes de você executar qualquer ação.

1. Copie `envFiles/sample-env.json` e dê a ele um novo nome, ex.: `my-env.json`
1. Abra o arquivo e preencha os seguintes campos usando os valores da [Instalação do Developer Console](developer-console-setup.md):

   | **Campo** | **Valor** |
   | --------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
   | `API_KEY` | ID do cliente |
   | `CLIENT_SECRET` | Segredo do cliente |
   | `IMS_ORG` | ID da organização |
   | `SCOPES` | Deve incluir escopos da API do Experience Platform (openid, session, AdobeID, read_organizations, additional_info.projectedProductContext) |
   | `SANDBOX_NAME` | A sandbox que você está direcionando — deve estar vazia e ser do tipo `dev` |

1. Salvar e fechar o arquivo

>[!NOTE]
>
>Você será solicitado a fornecer o nome desse arquivo sempre que executar um comando da CLI, para que possa reutilizá-lo em todas as etapas abaixo.

## &#x200B;3. Execute o menu AEP foundation

No menu principal, selecione **AEP foundation**. Há três etapas, que devem ser executadas em ordem.

>[!WARNING]
>
>A sandbox deve estar em um estado &quot;Pronto&quot; por pelo menos 60 minutos antes de você executar a Etapa 1.

| **Etapa** | **O que ele faz** | **Antes de executá-lo** |
| ----------------------- | ------------------------------------------------------------------------------------------ | ------------------------------- |
| &#x200B;1. Criar base de perfil | Implanta namespaces de identidade, esquemas, conjuntos de dados, políticas de mesclagem e públicos | Sandbox &quot;pronta&quot; por mais de 60 minutos |
| &#x200B;2. Carregar dados do perfil | Cria perfis e dados de pesquisa de fluxos de dados | Aguardar mais de 60 minutos após a Etapa 1 |
| &#x200B;3. Verificar integridade do perfil | Valida que todos os dados foram carregados corretamente | Aguardar mais de 15 minutos após a Etapa 2 |

A Etapa 1 leva cerca de 2 minutos para ser executada, a Etapa 2 cerca de 6 minutos e a Etapa 3 é uma validação rápida sem espera própria. Os intervalos de 60 e 15 minutos entre as etapas permitem que o AEP conclua a propagação de dados em segundo plano — é a maior parte do tempo de 2 horas.

>[!NOTE]
>
>A CLI verifica esses tempos de espera automaticamente. Se você executar uma etapa muito cedo, ela bloqueará e informará quantos minutos ainda restam — você não precisará rastrear o relógio por conta própria.

>[!NOTE]
>
>A etapa 2 pode ser executada novamente se algo der errado. Ele substitui registros de características existentes e ignora eventos duplicados.

## Solução de problemas

>[!WARNING]
>
>**Falha na verificação de integridade com eventos ausentes**. Alguns dados de perfil ainda não terminaram de ser propagados. Aguarde mais 15 minutos e execute novamente a Verificação de integridade do perfil. Se ainda falhar, execute novamente Load profile data, aguarde 15 minutos e verifique novamente.

**Algo mais parece errado.** Como último recurso, você pode redefinir a sandbox no menu de gerenciamento de sandbox da CLI e reimplantar a partir da Etapa 1.

>[!CAUTION]
>
>A redefinição de uma sandbox é destrutiva. A CLI solicita que você digite o nome da sandbox para confirmar antes de continuar.
