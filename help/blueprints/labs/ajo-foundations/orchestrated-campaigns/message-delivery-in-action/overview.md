---
title: Entrega de mensagem em ação
description: Obtenha uma visão geral da criação de uma Campanha orquestrada que segmente os membros do plano básico e compare o comportamento do delivery entre o Perfil do AEP e os canais de email do esquema relacional.
doc-type: overview-page
solution: Experience Platform
exl-id: 84b16fff-f733-439a-9a93-726811e543ce
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%
---

# Entrega de mensagem em ação

## Pré-requisitos

>[!WARNING]
>
>Os laboratórios abaixo devem ter sido concluídos antes do início deste laboratório

- **Repositórios de Dados — Repositório Relacional em Ação** **—>** [Dimension de Destino de Perfil](../../data-stores/relational-store-in-action/profile-target-dimension.md)
- **Repositórios de Dados —>** [Configurar Canais de Email](../../data-stores/configure-email-channels/overview.md) *(esta etapa de instalação leva 3 horas para ser concluída)*

Se você não tiver concluído esses laboratórios, faça-o agora antes de continuar.

>[!CAUTION]
>
>Este laboratório requer um subdomínio delegado à Adobe em sua sandbox. Consulte [Configuração](../../setup.md) se você estiver no seu ritmo e ainda não tiver uma.

## Visão geral do laboratório

Neste vídeo, você aprenderá a criar a campanha orquestrada para este laboratório, incluindo a criação e bifurcação de um público-alvo membro do plano básico e a comparação dos resultados do delivery entre os canais de email Perfil e Relacional.

>[!VIDEO](https://video.tv.adobe.com/v/3486541/)

## Objetivos de aprendizagem

- Criar uma campanha orquestrada usando várias atividades de fluxo de trabalho
- Construir um público-alvo usando a atividade Criar público-alvo
- Bifurque o público para criar duas ramificações e usar os canais de email, criados no laboratório anterior, para enviar mensagens
- Teste a campanha e entenda a diferença de comportamento entre os canais de email

Para direcionar os membros do plano &quot;Básico&quot;, você cria uma campanha neste laboratório e explora como diferentes configurações do Orchestrated Campaign afetam as configurações do canal de email.
