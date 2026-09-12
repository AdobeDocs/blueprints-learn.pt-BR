---
title: Corrigir erros de MAPPER para CreateDate
description: Solucione e resolva um erro de MAPPER causado por um valor createDate mal formatado que estava se transformando em um campo vazio.
doc-type: article
solution: Experience Platform
exl-id: e3f7ef23-6fd1-4f7a-8dc7-db82445322b0
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Corrigir erros de MAPPER para CreateDate

Neste exercício, você precisará descobrir como remover o erro de MAPPER que vimos no laboratório de assimilação em lote. O erro precisa ser corrigido porque, mesmo que createDate não seja um campo obrigatório, os registros ainda serão assimilados porque a data mal formatada será transformada em um campo vazio.

Valor ![createDate com formato inválido causando o erro MAPPER](assets/fix-mapper-errors-for-createdate-invalid-format-mapper-error.png)
