---
title: Criar relação do esquema
description: Use a API de registro do esquema para criar um descritor de relacionamento individualizado vinculando o esquema de Conta do cliente a um esquema de plano de pesquisa.
doc-type: article
solution: Experience Platform
exl-id: c9079585-fff1-4ee1-8992-93825fcde759
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---


# Criar relação do esquema

1. Clique na solicitação de API `Step 2 - Relationship Descriptor Customer Account To Plan` na pasta `XDM Schema Lab -> Create Relationship Descriptors`

   >[!CAUTION]
   >
   >Não executar a solicitação...ainda

   ![Etapa 2 - Conta do Cliente do Descritor de Relacionamento para a Solicitação de API do Plano](assets/create-schema-relationship-step-2-descriptor-request.png "Etapa 2 - Conta do Cliente do Descritor de Relacionamento para o Plano")



2. Atualize as seguintes propriedades no corpo da chamada de API.

- Defina o valor da propriedade `xdm:sourceSchema` como `$id` do esquema da Conta do cliente que você salvou da etapa do laboratório [Criar esquema](../build-schema/create-schema.md)
- Defina o valor de `xdm:sourceProperty` para o caminho do campo `planID` do Esquema de Conta de Cliente.
- Defina o valor da propriedade `xdm:destinationSchema` como `$id` do esquema `dep: Lookup Plan` que você salvou na primeira etapa

>[!NOTE]
>
>Use o valor da notação de pontos do campo planId do Esquema de Conta de Cliente e substitua `.` por `/`
>
>
>Não esqueça o `/` principal 😄

SOMENTE EXEMPLO

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/_devbc/plan/planID",
  "xdm:destinationSchema": "https://ns.adobe.com/devbc/schemas/6470f71181cf87aa39c2c2c43824eaa15f523652f7f88ff7"
,
  "xdm:destinationVersion": 1
}
```

>[!NOTE]
>
>Lembre-se de atualizar o nome do locatário acima (\_devbc) com o seu próprio



3. Salve sua solicitação antes de continuar usando o botão `Save`

4. Execute a API clicando no botão `Send`

Agora você deve ver uma resposta de `201 Created` como a seguir

![201 Resposta criada após a criação do descritor de relacionamento Conta do Cliente para Plano](assets/create-schema-relationship-customer-account-plan-descriptor.png "Conta do Cliente - Descritor de Relacionamento do Plano")

>[!NOTE]
>
>Lembre-se de que o Perfil de cliente em tempo real (e toda a Experience Platform) é compatível apenas com o que chamamos de **uma (1) associação de salto** dos esquemas Perfil individual XDM ou Evento de experiência XDM (ou seja, você só pode criar uma (1) relação de pesquisa de nível)

>[!NOTE]
>
>Você observou que o descritor de relacionamento `@type` está definido com um valor de `OneToOne`? A relação entre a conta do cliente e a tabela Plano no XDM ERD on Paper não é uma 1\:N?  O que está acontecendo?
>
>
>O Perfil do cliente em tempo real é criado para descrever as características e os comportamentos de uma pessoa individual.  Portanto, de uma lente de pessoa individual, uma tabela de pesquisa é **only** **ever** definida como uma relação 1:1 durante a segmentação.
>
>Tudo bem se seu cérebro dói...
