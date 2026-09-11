---
hold: true
title: Corrigir mapeamentos de passagem
description: Identifique e corrija mapeamentos de passagem de AI/ML incorretos, como atribuições de campo de destino duplicadas ou incompatíveis, antes de validar.
doc-type: article
solution: Experience Platform
exl-id: b06cc091-661e-4ff4-b6e5-f16bc5128b6b
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---


# Corrigir mapeamentos de passagem

## Soltar mapeamentos específicos

Alguns dos dados de origem que você tem precisam ser tratados usando campos calculados.  Para resolvê-los, remova-os dos mapeamentos e revalide-os.

1. Solte os seguintes dados de origem dos mapeamentos:
   - birth\_date
   - origem
   - sms\_optIn
1. Revalidar os mapeamentos clicando no botão validar

![Botão Validar usado para revalidar mapeamentos após descartar campos](assets/fix-passthrough-mappings-re-validate-mappings-using-validate-button.png "Revalidar mapeamentos usando o botão Validar")

>[!NOTE]
>
>Depois de clicar em Validar, talvez ainda haja erros



## Exemplos de mapeamento incorreto

Embora as recomendações de IA/ML sejam úteis, às vezes elas estão erradas.  Se você inspecionar suas recomendações, poderá encontrar esses tipos de erros que precisa corrigir

>[!NOTE]
>
>Abaixo estão alguns exemplos de mapeamentos inválidos que você pode ver em sua própria sandbox. Você também pode ver outros erros.

## Duplicar mapeamentos

Neste cenário, você vê que a recomendação do AI/ML mapeou dois campos de origem diferentes para o mesmo campo de destino **person.name.lastName**



![Dois campos de origem diferentes mapeados para o mesmo campo de destino person.name.lastName](assets/fix-passthrough-mappings-person-lastname-mapped-twice.png "person.name.lastName está mapeado para duas vezes neste mapeamento")

![Exemplo de mapeamento de passagem duplicado envolvendo o campo plan_name](assets/fix-passthrough-mappings-plan-name-duplicate-mapping.png)



## Mapeamentos incorretos

Este mapeamento parece correto, mas na inspeção mais detalhada, o **email** não é o mesmo que **emailFormat**

![O mapeamento onde o email está mapeado incorretamente em vez do emailFormat](assets/fix-passthrough-mappings-email-mapped-incorrectly.png "email parece estar mapeado corretamente, mas está incorreto conforme os requisitos")

E este aqui, onde **email\_optIn** está mapeando incorretamente para o objeto de consentimento errado

![email_optIn mapeado incorretamente para o objeto de consentimento errado](assets/fix-passthrough-mappings-email-optin-wrong-consent-object.png "email_optIn parece estar mapeado corretamente, mas está incorreto de acordo com os requisitos")



## Correção de mapeamentos de passagem

Para corrigir mapeamentos de passagem que apontam incorretamente para o campo de destino errado, execute as etapas a seguir.

### Exemplo

1. Comece com um mapeamento inválido e clique na caixa de campo de destino. Por exemplo, no mapeamento abaixo, o campo **person.name.lastName** não está mapeado corretamente e está mapeado para **planName**
1. No painel de esquema de destino que é aberto à direita, escolha o campo de destino apropriado e selecione **\_devbc.plan.name**
1. O campo de destino agora deve ser atualizado na caixa de campo de destino
1. Após corrigir cada erro, pressione o botão **Validar** para ter certeza de que está reduzindo esses tipos de erros e não introduzindo novos.



![Trabalhando na lista de mapeamento para corrigir cada erro de mapeamento](assets/fix-passthrough-mappings-work-through-mapping-errors.png "Percorra o mapeamento e corrija os erros de mapeamento")



![Painel de esquema de destino para selecionar o campo correto para corrigir um mapeamento de passagem](assets/fix-passthrough-mappings-choose-correct-target-field.png "Escolha o campo de destino correto e verifique se ele corresponde aos requisitos de passagem")

>[!WARNING]
>
>Não avance para a próxima etapa até resolver todos os seus erros de mapeamento
