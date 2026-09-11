---
title: Opção
description: Crie um público-alvo de transmissão total usando atributos de uso pré-agregados calculados upstream em vez de agregar eventos dentro da regra de público-alvo.
doc-type: article
solution: Experience Platform
exl-id: fe6ee041-814f-41c1-91cf-c3473cbca0c2
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---


# Opção #2 - use pré-agregados

O desafio com os Agregados em nosso Público-alvo é que nosso Público-alvo (durante a transmissão) é construído com base em agregações feitas dentro de Públicos-alvo que são Públicos-alvo em lote. Como o Marketing determinou que é necessária uma abordagem em tempo real, fizemos três coisas para incluir isso no design:

- Calcule as agregações antes de transmitir os dados no

>[!NOTE]
>
>Isso é bastante incomum, pois a maioria dos dados transmitidos é projetada em torno de um único evento em vez de um agregado

- Usar o Nome do Plano desnormalizado
- Transmitir os dados em

## Criar o público-alvo

Crie um público-alvo de todos os perfis cujo uso de dados de faturamento é alto, mas que atualmente não têm um plano de telefone definitivo.

1. Criar um novo público-alvo
1. Procure por &quot;Agg&quot; na guia Atributos, não Evento, e arraste as duas Agregações para a tela. Defina os operadores e valores apropriados para cada um.

   ![Definir os operadores e valores apropriados para cada agregação](assets/option-2-use-pre-aggregates-set-operators-and-values.png)



3. Procure o Nome do plano no Perfil e adicione-o (Perfil individual XDM > Devbc > Detalhes do plano > Nome do plano). Select Does Not Equal &quot;Ultimate&quot; (Não é igual a &quot;&quot;)

   ![Selecionar Nome do Plano Não É Igual a Ultimate](assets/option-2-use-pre-aggregates-select-does-not-equal-ultimate.png)



4. Forneça uma descrição.  O método de avaliação de validação é Streaming.

5. Salve o Público como &quot;*Uso alto de dados de cobrança, mas sem plano Ultimate (Agg)*&quot;

>[!NOTE]
>
>Lembre-se, mudamos a lógica agregada para nossa camada de Streaming ETL upstream.
>
>Essa escolha é uma compensação entre ter um Público-alvo em lote, em que o profissional de marketing controla a lógica em relação a um Público-alvo de streaming, mas enviando a definição e o controle para a camada ETL, na qual a engenharia deve estar envolvida.

>[!TIP]
>
>**Laboratório de desafio opcional**
>
>Terminou cedo?
>
>Gostaríamos de entrar em contato com nossos VIPs em tempo real com uma mensagem especial quando eles comprarem.  Crie um público-alvo com &quot;VIPs&quot;.  Um VIP é alguém que comprou mais de US$ 1.000 no mês passado.
