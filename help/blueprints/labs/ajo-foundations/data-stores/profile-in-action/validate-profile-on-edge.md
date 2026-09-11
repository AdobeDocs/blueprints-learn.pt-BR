---
hold: true
title: Validar perfil no Edge
description: Saiba como verificar a loja de perfis do Edge e a guia Associação de público-alvo para confirmar o status de um perfil na rede do Edge.
doc-type: article
solution: Experience Platform
exl-id: f82ceba7-6916-49ff-8776-2d0238560df8
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---


# Validar perfil no Edge

## Objetivo de aprendizado

Confirme se o perfil não existe no armazenamento de perfis de rede do Edge.

## Verifique o perfil do Edge

1. Clique na guia **Atributos** e no botão de opção **Edge** para ver o Perfil do Edge

![Perfil do Edge exibido na guia Atributos](assets/validate-profile-on-edge-attributes-tab.png)

>[!NOTE]
>
>É possível que você veja uma versão &quot;reduzida&quot; do perfil que consiste apenas nas identidades, dependendo de quanto tempo passou.



2. Clique na guia Associação de público-alvo.  Estará **em branco**.

![Guia de Associação de Público-Alvo vazia no perfil do Edge](assets/validate-profile-on-edge-empty-audience-membership-tab.png)

>[!NOTE]
>
>**Por que nenhuma associação à Edge?**
>
>Não deveríamos ter visto **dep: Qualquer Edge de Evento (dentro de uma hora)** qualificado?
>
>Mesmo que tenhamos um público-alvo com uma avaliação do Edge, ele não existe no Edge porque não temos motivo para isso... ainda.
>
>Se usássemos esse público-alvo (por exemplo, Decisioning ou Destinations), as regras de público-alvo seriam enviadas para a Edge e, na próxima vez que um evento fosse transmitido para a Edge, ela avaliaria esse público-alvo.
>
>Além disso, não ativamos os Serviços de segmentação da Edge.



## Recapitulação

O perfil não existe no Edge (ainda)
