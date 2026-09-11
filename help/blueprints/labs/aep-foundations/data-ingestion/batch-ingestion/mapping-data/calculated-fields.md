---
hold: true
title: Campos calculados
description: Crie expressões de campo calculado para preencher retroativamente valores de consentimento de SMS ausentes e dividir uma data de nascimento em campos de dia, mês e ano.
doc-type: article
solution: Experience Platform
exl-id: ea5d006b-11c5-439c-af01-bc00b919851f
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Campos calculados

## Visão geral

O campo sms\_optIn é um campo obrigatório no esquema Conta do cliente. O problema é que o campo sms\_optIn em nossa fonte de streaming pode enviar valores *null*, portanto, um campo calculado é necessário para resolver isso; caso contrário, esses registros serão ignorados na assimilação, o que é uma perda.

![O campo consents.marketing.sms.val como mostrado no esquema de destino](assets/calculated-fields-consents-marketing-sms-val-schema-field.png "consents.marketing.sms.val como mostrado no esquema")



## Criar campo calculado

1. Crie um campo calculado clicando no ícone **Novo tipo de campo** e selecione **Adicionar Campo Calculado**. Para todos os valores ausentes, presume-se que o consentimento não foi dado e está marcado como **&quot;n&quot;**. Observe que os campos calculados aparecem na coluna à esquerda, pois a transformação por meio do campo calculado é a entrada para esse novo mapeamento.

![Menu de ícone de novo tipo de campo com a opção Adicionar Campo Calculado selecionada](assets/calculated-fields-add-a-calculated-field.png "Adicionar um campo calculado")



1. Na caixa de diálogo Criar campo calculado, adicione a seguinte expressão e clique em **Visualizar**

```none
iif(sms_optIn == null or sms_optIn == "", 'n', sms_optIn)
```

![Criar caixa de diálogo de Campo Calculado com a expressão sms_optIn e Visualizar resultado](assets/calculated-fields-sms-optin-calculated-field.png "campo calculado sms_optIn")



1. Você deve ver uma marca de seleção verde no canto superior direito da caixa preta, indicando a validade da expressão, e a Visualização de dados deve mostrar apenas **&quot;n&quot;** ou **&quot;y&quot;** como valores. Se tudo estiver bem, clique em **Salvar**.



## Mapear para destino

Um novo campo é adicionado à tela de mapeamento, mas com um caminho de campo de destino não mapeado.

![Novo campo calculado sms_optin adicionado à tela de mapeamento com um campo de destino não mapeado](assets/calculated-fields-sms-optin-unmapped.png "sms_optin não mapeado")

1. Clique no **Campo de destino do mapa** para o novo campo calculado criado
1. No painel direito, agora é possível ver o painel Esquema de destino aberto. Digite **sms** na caixa de pesquisa
1. Selecione o campo **val**

![Painel de esquema de destino com o campo sms.val selecionado para o mapeamento de campo calculado](assets/calculated-fields-map-calculated-field-to-target-xdm-field.png)



O mapeamento final deve ficar assim:

![Tela de mapeamento final com o campo calculado sms_optin mapeado para o esquema de destino](assets/calculated-fields-final-mapping-screen.png)



1. Valide seu mapeamento para garantir que ele fique bom

![O botão Validar confirma que o mapeamento sms_optin é válido](assets/calculated-fields-validate-mappings.png)

>[!NOTE]
>
>Quaisquer linhas sem um valor de SMS válido são rejeitadas durante a assimilação. Se a assimilação parcial não estiver ativada, a falha de assimilação com essa linha falhará a assimilação do lote ou arquivo inteiro no nosso caso. Com a assimilação parcial ativada, as linhas com campos obrigatórios com valores ausentes são rejeitadas, mas as outras linhas são assimiladas.



## Lidar com aniversários

Há um requisito para separar o dia, mês e ano de nascimento em campos separados, de modo que alguns deles não possam ser usados em atividades downstream. É necessário criar dois campos calculados para resolver isso.

### Criar mapeamento para dia e mês de nascimento

1. Adicione um novo campo calculado para capturar o dia e o mês de nascimento dos perfis
1. Use o seguinte código para o campo calculado:

>[!NOTE]
>
>Em vez de apenas copiar o código acima, tente entender o que está acontecendo executando as partes de código separadamente para ver como ele foi composto para criar campos calculados mais complexos em uma única linha, pois não é permitido usar várias linhas. Tente o seguinte:
>
>1. `date(birth_Date,"M/d/yyyy")`
>2. `date_part("day", date(birth_Date,"M/d/yyyy")).toString()`
>3. `date_part("month", date(birth_Date,"M/d/yyyy")).toString()`
>4. `concat(date_part("month", date(birth_Date,"M/d/yyyy")).toString(),`
>   `"-", date_part("day", date(birth_Date,"M/d/yyyy")).toString())`



1. Clique em visualizar e você deverá ver o seguinte resultado. Se tudo estiver bem, clique em **Salvar**

![Visualizar o resultado da expressão de campo calculado de dia e mês de nascimento](assets/calculated-fields-birth-day-month-preview.png)



1. Mapear o campo calculado para **person.birthDayAndMonth**

1. Validar seu mapeamento



### Criar mapeamento para o ano de nascimento

1. Crie um novo campo calculado para capturar o ano de nascimento do perfil usando o código abaixo

```none
date_part("yyyy",date(birth_Date,"M/d/yyyy"))
```

1. Mapeie o campo calculado para o local de destino de **person.birthYear**

1. Validar seu mapeamento

>[!NOTE]
>
>Observe que as datas estão no formato **MM/DD/AAAA**, mas os dados **birth\_Date** da amostra estão vindo como dígitos simples ou duplos para o dia e mês. Para que a função **date** funcione, é necessário especificar o formato de entrada dos dados, como **M/d/aaaa**, para que você possa considerar de 1 a 2 dígitos para o mês e o dia. Sem essa especificação de formato de entrada de data, a validação desses mapeamentos falha.
