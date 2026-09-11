---
hold: true
title: Parte 1 - Tipos de tabela restantes
description: Identifique e rotule tabelas de ponte e tabelas que exigem desnormalização nos ERDs Perfil individual, Evento de experiência e Pesquisa.
doc-type: article
solution: Experience Platform
exl-id: 742b58fa-3feb-4275-ab45-eb8d3aade22c
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---


# Parte 1 - Tipos de tabela restantes

## Palestra

Neste vídeo, você aprenderá a rotular as tabelas não rotuladas restantes com um tipo de desnormalização de D ou B, incluindo como a Regra de tabela de Bridge #1 transforma um lado muitos para um de uma tabela de ponte em uma pesquisa.

>[!VIDEO](https://video.tv.adobe.com/v/3459082/?quality=12&learn=on)



## Detalhes do laboratório

Identifique e rotule tabelas no warehouse 5G Connection e ERDs de transmissão que se encaixem em uma das categorias abaixo

- Tabela do Bridge (rotulada como &quot;**B**&quot;)
- Novas tabelas de pesquisa que existem devido a tabelas de ligação
- Tabelas que exigirão desnormalização (rotuladas como &quot;**D**&quot;)

>[!CAUTION]
>
>A ordem é muito importante aqui! Certifique-se de estar seguindo as etapas na ordem, pois cada etapa depende da anterior



## Etapa 1: identificar e rotular tabelas de perfis individuais XDM

1. Identifique todas as tabelas diretamente relacionadas às tabelas do Perfil individual XDM (a um salto de distância) que ainda não têm um rótulo. Marque-os com uma estrela &quot;**\***&quot;.
1. Somente os esquemas que você acabou de rotular com uma estrela executam as seguintes tarefas:
   1. **Adicione um rótulo &quot;B&quot; para a tabela de ponte** - uma tabela é considerada uma tabela de ponte quando duas ou mais tabelas estão relacionadas a ela com o muitos lados da relação de ambas as tabelas apontando para a tabela de ponte
   2. **Adicione um rótulo &quot;D&quot; para tabelas a serem desnormalizadas** - qualquer entidade que tenha uma cardinalidade 1\:M ou M:1 com o Perfil Individual XDM rotulado como tabela e ainda não esteja marcada

>[!NOTE]
>
>Lembrar regra de tabela do Bridge #1.
>
>Ao encontrar uma tabela de ponte diretamente relacionada a um &quot;P&quot; ou &quot;E&quot;, a relação M:1 atua como uma pesquisa. Caso contrário, siga as regras padrão de desnormalização.



## Etapa 2: identificar e rotular tabelas de eventos de experiência XDM

1. Identifique todas as tabelas diretamente relacionadas (a um salto de distância) ao Evento de experiência rotuladas como tabelas que ainda não têm um rótulo. Marque-os com uma estrela.
1. Somente as tabelas que você acabou de rotular com uma estrela executam as seguintes tarefas:
   1. **Adicione um rótulo &quot;B&quot; para tabelas de ponte** - uma tabela é considerada uma tabela de ponte quando duas ou mais tabelas estão relacionadas a ela com o muitos lados da relação apontando para a tabela de ponte
   2. **Adicione um rótulo &quot;D&quot; para tabelas a serem desnormalizadas** - qualquer tabela que tenha uma cardinalidade 1\:M ou M:1 com o Evento de Experiência XDM rotulado como tabela e ainda não esteja marcada

>[!NOTE]
>
>Lembrar regra de tabela do Bridge #1.
>
>Ao encontrar uma tabela de ponte diretamente relacionada a um &quot;P&quot; ou &quot;E&quot;, a relação M:1 atua como uma pesquisa. Caso contrário, siga as regras padrão de desnormalização.



## Etapa 3: Identificar e rotular Tabelas de pesquisa

1. Identifique todas as tabelas relacionadas a (não importa quantos saltos você tenha) qualquer uma das tabelas rotuladas de Pesquisa que ainda não tenham um rótulo. Marque-os com uma estrela &quot;**\***&quot;.
1. Somente as tabelas que você acabou de rotular com uma estrela executam as seguintes tarefas:
   1. Adicione um rótulo &quot;**B**&quot; para tabelas de ponte - uma tabela é considerada uma tabela de ponte quando duas ou mais tabelas estão relacionadas a ela com o lado muitos da relação apontando para a tabela de ponte
   2. Adicione um rótulo &quot;**D**&quot; para tabelas a serem desnormalizadas - qualquer tabela que tenha uma cardinalidade 1\:M ou M:1 com uma tabela de Pesquisa ou tabela de ponte relacionada a uma pesquisa

>[!NOTE]
>
>Lembrar regra de tabela do Bridge #1.
>
>Ao encontrar uma tabela de ponte diretamente relacionada a um &quot;P&quot; ou &quot;E&quot;, a relação M:1 atua como uma pesquisa. Caso contrário, siga as regras de desnormalização padrão **(dica, dica)**



## Revisão

O vídeo abaixo analisa os rótulos D e B corretos para o warehouse 5G da Connection e ERDs de transmissão contínua, incluindo por que o tipo de produto é uma tabela desnormalizada em vez de uma pesquisa.

>[!VIDEO](https://video.tv.adobe.com/v/3459064/?quality=12&learn=on)
