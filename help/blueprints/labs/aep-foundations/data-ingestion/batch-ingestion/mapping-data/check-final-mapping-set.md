---
hold: true
title: Verificar conjunto de mapeamento final
description: Compare os mapeamentos de campo simples e calculado do esquema Conta do cliente com o conjunto de mapeamento final esperado.
doc-type: article
solution: Experience Platform
exl-id: d1521d08-1ccb-405f-b728-a2777598cb9f
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---


# Verificar conjunto de mapeamento final

&#x200B;> [!NOTE]
>
>Se você vem do laboratório de assimilação de streaming, clique no link abaixo para prosseguir para a próxima etapa desse laboratório:
>
>[Laboratório de assimilação de fluxo contínuo - Verificar conjunto final de mapeamento](../../stream-ingestion/check-final-mapping-set.md)



## Mapeamentos simples

>[!NOTE]
>
>Substitua o \&lt;nome do locatário> pelo valor da sua sandbox

| Campo do Source | Campo de destino |
| ------------------------- | --------------------------------- |
| account\_create\_date | \&lt;nome-do-locatário>.conta.createDate |
| account\_end\_date | \&lt;nome-do-locatário>.account.endDate |
| customer\_id | \&lt;nome-do-locatário>.customerID |
| plan\_name | \&lt;nome-do-locatário>.plan.name |
| plan\_id | \&lt;nome-do-locatário>.plan.planID |
| billing\_city | billingAddress.city |
| billing\_zip\_code | billingAddress.postalCode |
| billing\_state | billingAddress.state |
| billing\_street\_address | billingAddress.street1 |
| email\_optIn | consentimentos.marketing.email.val |
| celular\_phone | mobilePhone.number |
| firstName | person.name.firstName |
| lastName | person.name.lastName |
| email | personalEmail.address |
| createDate | repo.createDate |
| modifyDate | repo.modifyDate |
| shipping\_city | shippingAddress.city |
| delivery\_zip\_code | shippingAddress.postalCode |
| shipping\_state | shippingAddress.state |
| delivery\_street\_address | shippingAddress.street1 |

&#x200B;> [!NOTE]
>
>Verifique se o mapeamento final corresponde ao mostrado abaixo antes de continuar.



## Mapeamentos calculados

| Campos calculados | Campo XDM |
| ------------------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| iif(sms\_optIn == nulo ou sms\_optIn == &quot;&quot;, &#39;n&#39;, sms\_optIn) | consentimentos.marketing.sms.val |
| concat(date\_part(&quot;month&quot;, date(birth\_Date,&quot;M/d/yyyy&quot;)).toString(), &quot;-&quot;, date\_part(&quot;day&quot;, date(birth\_Date,&quot;M/d/yyyy&quot;)).toString()) | person.birthDayAndMonth |
| date\_part(&quot;aaaa&quot;,date(birth\_Date,&quot;M/d/aaaa&quot;)) | person.birthYear |

&#x200B;> [!NOTE]
>
>Verifique se o mapeamento final corresponde ao mostrado abaixo antes de continuar
