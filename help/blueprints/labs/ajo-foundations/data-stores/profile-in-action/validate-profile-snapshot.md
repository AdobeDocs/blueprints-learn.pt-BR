---
title: Validar instantâneo do perfil
description: Saiba como consultar o conjunto de dados Instantâneo de perfil e entenda por que uma atualização de perfil recém-transmitida não é exibida até a próxima tarefa em lote diária.
doc-type: article
solution: Experience Platform
exl-id: 1e7befcf-d952-47a2-86d9-33ef71eec57a
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---


# Validar instantâneo do perfil

## Objetivo de aprendizado

Confirme se o perfil ainda não é exibido no conjunto de dados Instantâneo do perfil.

## Usar o conjunto de dados Instantâneo do perfil

1. Na navegação à esquerda, na seção Gerenciamento de dados, clique em **Conjuntos de dados** e depois clique na **guia Procurar**, localizada no painel superior

   ![Guia Procurar Conjuntos de Dados na seção Gerenciamento de Dados](assets/validate-profile-snapshot-datasets-browse-tab.png)

2. Na **caixa de pesquisa**, digite `profile` e **clique na linha** com o título &quot;Instantâneo de Perfil...&quot;.   e, no painel direito **copie o nome da tabela** e cole-o em algum lugar que você possa referenciar na próxima etapa.

   >[!NOTE]
   >
   >Talvez seja necessário limpar os filtros se você não vir a mensagem &quot;Instantâneo de perfil...&quot; conjunto de dados.



   ![Resultados de pesquisa para o conjunto de dados Perfil-Instantâneo](assets/validate-profile-snapshot-dataset-search.png)

3. Navegue de volta para o Editor de consultas e copie e cole o SQL abaixo no editor

   ```sql
   select
     identityMap,
     segmentID,
     segmentMembershipUps[segmentID] ['lastQualificationTime'],
     segmentMembershipUps[segmentID] ['status'],
     current_timestamp
   from
     (
    select
      identityMap,
      explode (map_keys (segmentMembership['ups'])) as segmentID,
      segmentMembership['ups'] as segmentMembershipUps
    from
   
    where
      map_keys (segmentMembership['ups']) is not null
    limit 100
     )
     --where identityMap['email'][0].id = 'henry.creel@emailsim.io'
     limit 50
   ```

4. Atualize o nome da tabela e o endereço de email conforme descrito abaixo:
   - **Nome da tabela:** na linha 14, copie e cole o nome da tabela que você tem para a tabela Instantâneo de Perfil entre o `from` e o `where`
   - **Endereço de email:** por enquanto, na linha 19, digite o mesmo endereço de email que você costumava enviar no seu Evento da Web (usamos henry.creel\@emailsim.io, a menos que você o tenha alterado).
     - No momento, comentamos isso (deixe assim). Quando a consulta é executada e você procura Henry, você não o encontra.

   ![Editor de consultas com o nome e o endereço de email da tabela Instantâneo de Perfil a ser atualizada](assets/validate-profile-snapshot-update-query-table-name.png)

5. **Execute** a consulta clicando na seta na parte superior esquerda
6. Os resultados são como abaixo (mas se você procurar Henry, você não encontrá-lo)

![Os resultados da consulta não mostram nenhuma correspondência para o perfil transmitido no instantâneo](assets/validate-profile-snapshot-query-results-no-match.png)

>[!NOTE]
>
>**Por que nenhum resultado para o Henry?**
>
>**Lembrete**: o Instantâneo de Perfil é uma **reflexão** ou um instantâneo do que existia no Perfil em um **momento específico**. O trabalho é executado **diariamente** e é usado para fins downstream, como o AJO. Como você acabou de transmitir esses dados, o Instantâneo do perfil ainda não o tem.  Vai ser amanhã.

## Recapitulação

Entenda que os conjuntos de dados de instantâneo são atualizados em um processo em lote agendado, em vez de imediatamente.
