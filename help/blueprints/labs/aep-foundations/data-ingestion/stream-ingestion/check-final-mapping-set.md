---
hold: true
title: Verificar conjunto de mapeamento final
description: Compare seus mapeamentos de assimilação de streaming com a passagem final esperada e o conjunto de mapeamento de campo calculado.
doc-type: article
solution: Experience Platform
exl-id: 8802aaca-f566-4972-8bd6-41aca9fae9bf
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---


# Verificar conjunto de mapeamento final

## Mapeamentos de passagem

&#x200B;> [!NOTE]
>
>Verifique se o mapeamento final corresponde ao mostrado abaixo antes de continuar.

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



## Mapeamentos calculados

>[!NOTE]
>
>Esteja ciente de que os mapeamentos para `birth_Date` são diferentes dos mapeamentos do laboratório de assimilação em lote devido à forma como a data é formatada.  O lote está usando as barras `/`, enquanto a transmissão está usando os traços `-`

| Campos calculados | Campo XDM |
| ----------------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| iif(sms\_optIn == nulo ou sms\_optIn == &quot;&quot;, &#39;n&#39;, sms\_optIn) | consentimentos.marketing.sms.val |
| concat(date\_part(&quot;mm&quot;, date(birth\_Date, &quot;aaaa-M-d&quot;)).toString(), &quot;-&quot;, date\_part(&quot;dd&quot;, date(birth\_Date, &quot;aaaa-M-d&quot;)).toString()) | person.birthDayAndMonth |
| date\_part(&quot;aaaa&quot;,date(birth\_Date,&quot;yyyy-M-d&quot;)) | person.birthYear |

&#x200B;> [!NOTE]
>
>Verifique se o mapeamento final corresponde ao mostrado abaixo antes de continuar



## Finalizar fluxo de dados

Quando terminar, clique no botão **Avançar** e, em seguida, clique no botão Concluir para atualizar o fluxo de dados com a nova lógica de mapeamento.

![Revisando os detalhes do fluxo de dados antes de clicar em Concluir para salvá-lo](assets/check-final-mapping-set-review-and-finish-dataflow.png)



Agora você deve ver uma tela que exibe a conta da API HTTP criada com todos os fluxos de dados associados que usam essa conta. O fluxo de dados criado também deve ser exibido.
