---
title: Identificar
description: Saiba mais sobre a etapa Identificar da metodologia de TAMPA, que consiste em rotular os tipos de tabela restantes e identificar os campos de identidade principais.
doc-type: overview-page
solution: Experience Platform
exl-id: 83657cf0-db35-4d4d-8cfb-1934ff40baca
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---


# Identificar

## Objetivos de aprendizagem

A etapa **Identificar** da metodologia LID está dividida em duas partes distintas:

1. Parte 1 - Tipos de tabela restantes -> identifique as tabelas não rotuladas restantes e rotule o tipo de desnormalização
1. Parte 2 — Campos-chave —> identificar os campos-chave das entidades primária e de apoio



Isso o ensinará a identificar os seguintes itens em um modelo relacional que serão necessários para criar o Perfil do cliente em tempo real:

- Tabelas do Bridge (tabelas que lidam com relações muitos para muitos)
- Tabelas que exigirão desnormalização
- Identidades principais no Perfil do cliente em tempo real
- Identidades com base em pessoas nas classes de entidade principais que podem ser usadas para identificar exclusivamente uma pessoa
- Identificadores de relação entre tabelas de Perfil individual/Evento de experiência e tabelas de pesquisa associadas
- Campos obrigatórios necessários para os esquemas de evento de experiência
- Campos recomendados para Perfil individual e esquemas de pesquisa
