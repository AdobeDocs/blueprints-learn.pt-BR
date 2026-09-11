---
hold: true
title: Lançamento de telefone emblemático
description: Obtenha uma visão geral da criação de uma Campanha Orquestrada direcionada a titulares de conta e linhas individuais com uma oferta de atualização de SMS após um lançamento de telefone emblemático.
doc-type: overview-page
solution: Experience Platform
exl-id: 04c509f1-aa10-4d29-aa59-5e627b79e498
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# Lançamento de telefone emblemático

## Pré-requisitos

>[!WARNING]
>
>Os laboratórios abaixo devem ter sido concluídos antes do início deste laboratório

- **Repositórios de Dados — Repositório Relacional em Ação** **—>** [Dimension de Destino de Perfil](../../data-stores/relational-store-in-action/profile-target-dimension.md)
- **Repositórios de Dados — Configurar Canais de Email —>** [Configurar para Relacional](../../data-stores/configure-email-channels/configure-for-relational.md)
  *(esta etapa de instalação leva até 3 horas para ser concluída)*

Se você não concluiu esses laboratórios, faça-o agora antes de continuar.

## Visão geral do laboratório

Neste vídeo, você aprenderá como o principal caso de uso de lançamento de telefone mapeia campanhas orquestradas, recapitulando as perguntas críticas e a arquitetura antes de criar os titulares de conta de direcionamento de campanha e linhas individuais.

>[!VIDEO](https://video.tv.adobe.com/v/3486217/)

## Objetivos de aprendizagem

- Criar uma campanha orquestrada usando uma variedade de atividades de fluxo de trabalho
- Construir um público-alvo usando uma atividade Criar público-alvo
- Saiba como configurar um canal de SMS
- Salvar um público-alvo no portal de públicos-alvo
- Direcionar a conta do cliente e linhas individuais com mensagens de email e SMS



## Descrição do caso de uso

Imediatamente após o lançamento do mais recente dispositivo principal de um fabricante, envie uma mensagem direcionada aos titulares de contas e usuários da linha com modelos mais antigos — convidando-os a atualizar e experimentar o futuro dos dispositivos móveis.

**Principais chamadas:**

- Salvar o público-alvo de todas as linhas do cliente no Portal de público-alvo
- Direcione linhas individuais e titulares de conta com uma mensagem (você usará SMS)

>[!NOTE]
>
>Este cenário simula uma **campanha de atualização de contrato de telecom**, em que linhas secundárias (dependentes) recebem mensagens de atualização direcionadas.
