---
title: Navegação abandonada
description: Saiba como criar um fluxo de trabalho completo de decisão de navegação abandonada que fornece ofertas telefônicas personalizadas e com reconhecimento de elegibilidade em todos os canais.
doc-type: overview-page
solution: Experience Platform
exl-id: 37b8a0b3-2820-4303-81d2-19890a3c5782
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%
---

# Navegação abandonada

## Pré-requisitos

>[!WARNING]
>
>Os laboratórios abaixo devem ter sido concluídos antes do início deste laboratório

- **Instalação do Postman** **—>** [Instalação do Postman](../../postman-setup/postman-installation.md)
- **Repositórios de Dados — Perfil em Ação** **—>** [Criar Sequência de Dados](../../data-stores/profile-in-action/create-datastream.md)

Se você não tiver concluído esses laboratórios, faça-o agora antes de continuar.

## Visão geral do laboratório

Neste vídeo, você aprende como a descrição do caso de uso de navegação abandonada revela seus elementos de decisão e o que você criará neste laboratório para fornecer uma oferta telefônica personalizada e com reconhecimento de elegibilidade em tempo real.

>[!VIDEO](https://video.tv.adobe.com/v/3491316/)

## Objetivos de negócios

Para este laboratório, a Connection 5G quer aumentar as vendas do novo telefone principal da Apple, o iPhone 17, direcionando os clientes que navegaram na página de visão geral do iPhone 17, mas não compraram. Os principais objetivos da campanha são os seguintes:

- **Identifique clientes de alta intenção** detectando quando um usuário exibe uma página de telefone principal várias vezes sem concluir uma compra.
- **Acione uma experiência personalizada em tempo real** em todas as superfícies digitais da Connection 5G quando esse comportamento ocorrer.
- **Forneça ofertas contextuais** com base nos principais atributos do cliente, como a **idade do titular da conta** e seu **plano de celular atual**.
- **Verifique se a qualificação de oferta é aplicada** para que os clientes só vejam ofertas telefônicas compatíveis com seus planos.
- **Ajuste dinamicamente a camada de telefone oferecida** (por exemplo, base, pro, ultra) com base no engajamento do cliente ou na resposta a ofertas anteriores.
- **Forneça personalização consistente em todos os canais** usando uma lógica de decisão centralizada para determinar a melhor oferta em tempo real.
- **Aumente a probabilidade de conversão** apresentando a principal oferta de telefone para cada cliente no momento certo.

## Objetivos de aprendizado de laboratório

Para atender aos objetivos de negócios acima neste laboratório, você aprenderá a:

- **Estenda o modelo de dados de oferta** adicionando atributos personalizados ao esquema de oferta para que eles possam ser usados na lógica de decisão.
- **Crie regras de qualificação** que determinam quais perfis se qualificam para ofertas específicas com base em atributos de perfil.
- **Crie e configure itens de oferta**, incluindo a definição de prioridades, a definição de condições de qualificação e a aplicação de limite de frequência.
- **Organize as ofertas em uma coleção** para que elas possam ser facilmente referenciadas e avaliadas durante a atividade de Decisão.
- **Crie uma fórmula de classificação** que ajuste dinamicamente a prioridade da oferta com base nas características do perfil.
- **Configure uma estratégia de seleção** que combine coleções de ofertas, regras de qualificação e lógica de classificação para determinar quais ofertas são consideradas e como são ordenadas.
- **Configure um canal de Experiência Baseada em Código (CBE)** para permitir que sistemas externos solicitem resultados de decisão e recebam ofertas no formato JSON.
- **Teste o fluxo de trabalho de decisão completo** enviando eventos de experiência e solicitações de decisão para validar a lógica de qualificação, o comportamento de classificação e o limite de frequência.

Ao concluir este laboratório, você obtém experiência prática ao projetar e validar um **fluxo de trabalho completo do Offer Decisioning no Adobe Journey Optimizer** para atender ao caso de uso comercial.
