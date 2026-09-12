---
title: Criar um público
description: Saiba como usar a atividade Criar público-alvo para direcionar membros do plano básico de um esquema relacional e verificar as contagens de linhas resultantes.
doc-type: article
solution: Experience Platform
exl-id: 7576e64b-d99a-4864-b877-f4ae77e1d7bd
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# Criar um público

## Objetivo

No próximo conjunto de etapas, você criará um público-alvo do esquema relacional selecionando a Targeting dimension correta e definindo as condições apropriadas. Você também usará a opção de atualização para verificar o número esperado de contagens de linhas.

## Criar público-alvo

1. Depois que a campanha for renderizada, clique em **+** na tela para abrir o menu de opções e selecione **Criar público-alvo** nas **Atividades de direcionamento**

   ![Selecione Criar público-alvo a partir de atividades de Direcionamento](assets/build-an-audience-select-build-audience-activity.png)

2. A atividade **Criar público-alvo** abre o painel de detalhes à direita. Clique no ícone Pesquisar para selecionar a **Dimensão de direcionamento**.

   ![Selecionar Targeting dimension](assets/build-an-audience-select-targeting-dimension.png)

3. Selecione `dep-rel: Customer Account` na lista e clique em **Confirmar**

   ![Selecione dep-rel: esquema da conta do cliente](assets/build-an-audience-select-customer-account-schema.png)

4. Depois que a **Targeting dimension** estiver configurada, clique em Criar público-alvo para iniciar o processo de criação do público-alvo a partir do esquema relacional

   ![Clique no botão Criar audiência](assets/build-an-audience-create-audience-button.png)

5. O painel Criar detalhes do público-alvo é aberto. Clique em **Adicionar condição**

   ![Clique em Adicionar condição no painel Criar público-alvo](assets/build-an-audience-add-condition.png)

6. Role para baixo e expanda o `dep-rel: Plan Lookup` clicando no **>** ao lado dele

   ![Expandir dep-rel: Pesquisa de Plano](assets/build-an-audience-expand-plan-lookup.png)

7. Selecione `dep-rel: Plan Name` e clique em **Confirmar**

   ![Selecionar dep-rel: Nome do Plano](assets/build-an-audience-select-plan-name.png)

8. No painel Condição personalizada, deixe o operador como &quot;igual a&quot; e, para Valor, selecione Básico no menu suspenso.

   ![Condição personalizada com Nome de Plano igual a Básico](assets/build-an-audience-plan-name-equals-basic.png)

   >[!NOTE]
   >
   >Observe que todos os valores distintos disponíveis para a coluna selecionada são exibidos no menu suspenso, facilitando a criação das condições personalizadas.



9. Com a configuração Custom condition, clique no ícone Refresh para calcular e exibir a contagem. Há dois locais para ajudar no cálculo dos resultados

   ![Clique no ícone Atualizar para calcular as contagens de linhas esperadas](assets/build-an-audience-refresh-row-counts.png)

   >[!NOTE]
   >
   >A operação Atualizar avalia a condição em relação aos dados relacionais e exibe os resultados esperados. Normalmente, essa operação leva apenas alguns segundos e é extremamente útil para ajustar os critérios e garantir que atenda às expectativas.



10. As contagens (**38**) indicam o número de linhas no repositório relacional que correspondem à condição especificada. Clique em **Confirmar** para sair do painel **Criar público**

![Confirmar contagem de linhas e sair do painel Criar público-alvo](assets/build-an-audience-confirm-row-count.png)

>[!NOTE]
>
>Há opções na seção Propriedades da regra para obter mais detalhes. Clique em **Exibir resultados** para ver os resultados reais retornados. Use a opção **Visualização de código** para ver a consulta que está sendo executada.

## Recapitulação

Agora você viu como é fácil usar a atividade Criar público-alvo na campanha ao escolher o Targeting dimension correto no esquema relacional. Em seguida, você adicionou uma condição para refinar os critérios de criação do público-alvo e usou a opção de atualização para verificar o número esperado de linhas.

Você pode ler mais [aqui](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/campaigns/orchestrated-campaigns/design-campaigns/build-audience), se estiver interessado.
