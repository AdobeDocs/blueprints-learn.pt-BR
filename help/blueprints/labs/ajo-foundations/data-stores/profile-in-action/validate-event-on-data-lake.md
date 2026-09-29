---
title: Validar evento no Data Lake
description: Saiba como consultar o Data Lake para verificar se um evento da Web transmitido foi gravado no conjunto de dados correto.
doc-type: article
solution: Experience Platform
exl-id: 14445089-aa3c-4cce-9d33-80032b6f9868
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 1d6ba1444c119437eb8a86d5c4a1050d56d16023
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%
---

# Validar evento no Data Lake

## Objetivo de aprendizado

Verifique se o evento da Web foi gravado no Experience Platform Data Lake.

## Validar evento

>[!NOTE]
>
>Por fim, os dados aparecerão no Data Lake.  **Isso pode levar até 60 minutos**.  Sabemos que o conjunto de dados está ativado para o perfil e, portanto, o evento criará um fragmento de perfil.
>
>Você pode localizar e consultar o conjunto de dados da Web.

1. Ir para **Consultas** e **Criar Consulta**

   ![Tela Criar Consulta na seção Consultas](assets/validate-event-on-data-lake-create-query.png)

2. Copiar este SQL e colá-lo em sua query

   ```sql
   SELECT identityMap['email'][0].id, * FROM dep_web
   where identityMap['email'][0].id = 'henry.creel@emailsim.io'
   ```

3. **Executar** Consulta

>[!NOTE]
>
>**Lembre-se**: os dados acabarão aparecendo no Data Lake.  **Isso pode levar até 60 minutos**.
>
>Não é necessário aguardar até que ele seja exibido. Fique à vontade para voltar a essa etapa e verificar mais tarde.



![Resultados da consulta mostrando o evento da Web transmitido no data lake](assets/validate-event-on-data-lake-query-results.png)

## Recapitulação

O registro do evento aparece no conjunto de dados apropriado.
