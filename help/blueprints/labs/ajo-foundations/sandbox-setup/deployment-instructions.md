---
title: Instruções de implantação
description: Use a CLI da DEP para implantar os esquemas, os conjuntos de dados, os fluxos de dados e os dados de amostra do pacote de laboratório do AJO Architectural Foundations em sua sandbox.
doc-type: article
solution: Experience Platform
exl-id: 3d6e9a1c-7b2f-4e8a-9d0c-1f5a8b6c2e3d
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 1%

---


# Instruções de implantação

>[!WARNING]
>
>Isso só é necessário se você estiver trabalhando nos laboratórios no seu próprio ritmo. Se você estiver em um curso ou evento de treinamento ao vivo, sua sandbox já foi implantada para você.

O pacote de laboratórios do AJO Architectural Foundations é implantado em sua sandbox usando a DEP CLI, uma ferramenta de linha de comando que cria os esquemas, conjuntos de dados, fluxos de dados e dados de amostra que você usará em todos os laboratórios — cobrindo a loja de perfis e a loja relacional da AJO usada para campanhas orquestradas.

## O que é implantado

**Rastreamento de perfil**

- Namespaces de identidade (customerID, planID, productID)
- Grupos de campos XDM padrão, descritores e esquemas habilitados para perfil
- Conjuntos de dados do catálogo habilitados para o perfil
- Mesclar políticas e públicos
- Dados de perfil de três conjuntos de dados de amostra: Modo de profundidade (características + eventos), Coisas estranhas (características) e Decisão (características)

**Faixa relacional**

- O namespace da identidade da customerID
- 11 esquemas XDM relacionais com chave primária, chave estrangeira e descritores de versão
- 11 conjuntos de dados habilitados para campanhas orquestradas do AJO
- 11 fluxos de dados carregando dados da Data Landing Zone

>[!NOTE]
>
>A implantação completa leva cerca de 2 horas e 23 minutos. O perfil e as trilhas relacionais são executados em paralelo e, na maioria das vezes, o tempo de espera autônomo é aplicado automaticamente pela CLI.

## Pré-requisitos

- **Direitos de licença.** Privilégios administrativos para uma Organização IMS com Real-Time CDP (com segmentação por transmissão) e Adobe Journey Optimizer (com Campanhas orquestradas)
- **Direitos de Acesso.** Uma função Experience Platform com todas as permissões na sandbox de destino, incluindo a credencial de API que você criou a partir da [instalação do Developer Console](developer-console-setup.md).
- **Credenciais do Developer Console.** Um projeto que inclui APIs do Adobe Experience Platform e do Adobe Journey Optimizer. Se você ainda não os tiver, siga a [configuração do Developer Console](developer-console-setup.md) primeiro
- **Uma sandbox.** Vazio, do tipo `dev` e em um estado &quot;Pronto&quot; por pelo menos 120 minutos antes de você iniciar a implantação
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
2. Abra o arquivo e preencha os seguintes campos usando os valores da [configuração do Developer Console](developer-console-setup.md):

   | **Campo** | **Valor** |
   | ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
   | `API_KEY` | ID do cliente |
   | `CLIENT_SECRET` | Segredo do cliente |
   | `IMS_ORG` | ID da organização |
   | `SCOPES` | Deve incluir os escopos API do Experience Platform e API do Adobe Journey Optimizer <br />*(por exemplo, cjm.suppression\_service.client.delete, cjm.suppression\_service.client.all, openid, session, AdobeID, read\_organizations, additional\_info.projectedProductContext)* |
   | `SANDBOX_NAME` | A sandbox que você está direcionando — deve estar vazia e ser do tipo `dev` |

3. Salvar e fechar o arquivo

>[!NOTE]
>
>Você será solicitado a fornecer o nome desse arquivo sempre que executar um comando da CLI, para que possa reutilizá-lo em todas as etapas abaixo.

## &#x200B;3. Execute o menu AJO Architectural Foundations

No menu principal, selecione **AJO arch foundation**. Há seis etapas divididas em duas faixas.

### Rastreamento de perfil (execução em ordem)

>[!WARNING]
>
>A sandbox deve estar em um estado &quot;Pronto&quot; por pelo menos 60 minutos antes de você executar a Etapa 1.

| **Etapa** | **O que ele faz** | **Antes de executá-lo** |
| ------------------------ | ------------------------------------------------------------------------------------------- | ---------------------------------- |
| &#x200B;1. Criar base de perfil | Implanta namespaces de identidade, esquemas, conjuntos de dados, políticas de mesclagem e públicos | Sandbox &quot;pronta&quot; por mais de 60 minutos |
| &#x200B;2. Carregar dados do perfil | Cria fluxos de dados e transmite dados de perfil do Modo de detecção, Coisas de estranhos e Decisão | Aguardar mais de 60 minutos após a Etapa 1 |
| &#x200B;3. Verificar integridade do perfil | Valida se todos os dados do perfil foram carregados corretamente | Aguardar mais de 15 minutos após a Etapa 2 |

A etapa 1 leva aproximadamente 2 minutos, a etapa 2, aproximadamente 6 minutos.

>[!NOTE]
>
>A etapa 2 poderá ser executada novamente com segurança se algo falhar — ela substitui as características existentes e ignora eventos duplicados.

### Faixa relacional

>[!WARNING]
>
>A sandbox deve estar em um estado &quot;Pronto&quot; por pelo menos 120 minutos antes de você executar a Etapa 4 ou a Etapa 6.

| **Etapa** | **O que ele faz** | **Antes de executá-lo** |
| ----------------------------------- | -------------------------------------------------------------------------------- | ---------------------------------------------------- |
| &#x200B;4. Criar base relacional | Cria o namespace da customerID e os esquemas/descritores/conjuntos de dados relacionais | Sandbox &quot;pronta&quot; por mais de 120 minutos |
| &#x200B;5. Carregar dados relacionais | Faz upload de 11 arquivos CSV e cria os fluxos de dados que os carregam | É executado logo após a Etapa 4 — não é necessária espera manual |
| &#x200B;6. Implantar base relacional e dados | Combina as etapas 4 e 5 em uma única execução de ~5 minutos | Sandbox &quot;pronta&quot; por mais de 120 minutos |

>[!NOTE]
>
>Use a Etapa 6 em vez de executar as Etapas 4 e 5 separadamente — ela faz a mesma coisa em uma passagem com a espera de propagação tratada para você.

>[!NOTE]
>
>Todos os tempos de espera acima são verificados automaticamente pela CLI. Se você executar uma etapa muito cedo, ela será bloqueada e informará o tempo de espera.

## Solução de problemas

>[!WARNING]
>
>**Falha na verificação de integridade do perfil com eventos ausentes.** Alguns dados de perfil ainda não terminaram de ser propagados. Aguarde mais 15 minutos e execute novamente a Verificação de integridade do perfil. Se ainda falhar, execute novamente Load profile data, aguarde 15 minutos e verifique novamente.

>[!WARNING]
>
>**Falha de carregamento de dados relacionais.** Cada chamada de API do tenta novamente até 3 vezes. Se ainda falhar, a limpeza removerá as conexões de origem, as conexões de destino e os fluxos de dados criados para que você possa executar novamente a Etapa 5 (ou a Etapa 6) corretamente. Os conjuntos de mapeamento não podem ser excluídos por meio da API e podem ser deixados para trás — isso não afeta a reimplantação.

**Algo mais parece errado.** Como último recurso, você pode redefinir a sandbox no menu de gerenciamento de sandbox da CLI e reimplantar a partir da Etapa 1.

>[!CAUTION]
>
>A redefinição de uma sandbox é destrutiva. A CLI solicita que você digite o nome da sandbox para confirmar antes de continuar.
