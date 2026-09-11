---
title: Criar um público
description: Saiba como usar a atividade Build Audience em uma campanha orquestrada para direcionar linhas ativas do cliente com uma criação de telefone específica usando condições de esquema relacional.
doc-type: article
solution: Experience Platform
exl-id: 697d3edb-2b63-4038-a934-3587495e17f7
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---


# Criar um público

## Objetivo

Nas próximas etapas, você criará o público-alvo que deseja direcionar para a campanha, que são todos os titulares de linha ativos que têm uma marca que corresponde ao telefone principal que está sendo lançado.  O objetivo é o grupo que você deseja direcionar com uma mensagem SMS incentivando-os a atualizar seus telefones.



## Adicionar atividade Criar público-alvo

1. Na tela, clique no símbolo **+** e selecione a atividade **Criar público** para adicioná-lo ao fluxo de trabalho

   ![Adicionar a atividade Criar público à tela do fluxo de trabalho](assets/build-an-audience-add-activity.png)



2. No painel direito, você verá as propriedades Criar público-alvo. Atualize o Rótulo para indicar o seguinte: `Active Lines with Apple`

![Criar rótulo de público definido como Linhas Ativas com o Apple](assets/build-an-audience-set-label.png)


## Selecionar targeting dimension

A próxima etapa é selecionar a **Targeting dimension** (ou seja, qual tabela você deseja consultar). Execute as seguintes etapas:

1. Clique no **ícone de pesquisa** na caixa Targeting dimension

   ![Ícone Pesquisar na caixa Dimensão de direcionamento](assets/build-an-audience-search-targeting-dimension.png)

2. No pop-up, procure e selecione a tabela denominada **dep-rel: Customer Line** e clique no botão **Confirm**.

![Selecione a tabela dep-rel: Customer Line e clique em Confirmar](assets/build-an-audience-select-customer-line-table.png)

>[!NOTE]
>
>Lembre-se sempre da **dimensão de direcionamento** de cada público-alvo criado. Você aprenderá o significado dela nas próximas etapas.

>[!NOTE]
>
>se você já tiver selecionado um esquema criado pela Adobe, observe que o esquema começa com -> *(caas)*. Este é apenas um namespace aplicado às tabelas no armazenamento relacional e significa Campaign as a Service :)



## Criar público

Agora que você selecionou o targeting dimension (qual esquema relacional você vai consultar), é possível começar a criar sua definição.

1. No painel direito, clique no botão **Criar Público**

   ![Botão Criar público-alvo no painel direito](assets/build-an-audience-click-create-audience.png)

2. Clique no botão **Adicionar condição**

![Botão Adicionar condição para a definição de público-alvo](assets/build-an-audience-click-add-condition.png)



## Criar condição(ões)

Agora é hora de escrever a lógica do público-alvo usando os atributos encontrados no esquema. O objetivo é encontrar todas as linhas de clientes que estão ativas e usando uma marca do Apple.

### Criar condição #1

1. Defina a condição usando as seguintes informações:
   - **Atributo**: `Active Line`
   - **Valor**: `true`

   ![Condição 1 definida como Linha Ativa igual a verdadeiro](assets/build-an-audience-condition-active-line-true.png)

2. Clique no ícone **Atualizar** para exibir as contagens qualificadas na condição.

![Ícone Atualizar mostrando a contagem qualificada de 241 para a condição 1](assets/build-an-audience-condition-1-refresh-count.png)

>[!TIP]
>
>Você verá um resultado de 241 se criar a condição corretamente



### Criar condição #2

1. Clique no botão **Adicionar condição** e selecione o esquema **dep-rel:** **Product \[Lookup]** clicando no ícone **>**

   ![Selecione o esquema dep-rel: Product [Lookup] clicando no ícone >](assets/build-an-audience-select-product-lookup-schema.png)


2. Procure o campo **Marca**, clique nos três pontos e selecione **Distribuição de valores**

   ![Opção de distribuição de valores para o campo Criar](assets/build-an-audience-make-distribution-of-values.png)



3. Observe os vários valores. Você só quer `Apple` e, felizmente, ele não tem 100 grafias diferentes. Clique no **campo do Apple** para selecioná-lo e, em seguida, clique no **botão Selecionar atributo e valor** no canto superior direito.

   ![Valor do Apple selecionado com o botão Selecionar atributo e valor](assets/build-an-audience-select-apple-attribute-value.png)

   >[!NOTE]
   >
   >Este é um exemplo excelente de onde o arquiteto de dados deve ter projetado o esquema com enumerações.  Dessa forma, um profissional de marketing não precisa selecionar/digitar manualmente o valor.  Que vergonha, arquiteto de dados!



4. O campo `Make` é adicionado automaticamente com as condições mostradas abaixo.
   - **Operador:** `Equal to`
   - **Valor:** `Apple`
   - **Diferenciação de maiúsculas e minúsculas:** `Enabled`

5. Clique no **ícone calcular** e você verá 85 como o resultado.

![Contagem calculada da Condição 2 de 85](assets/build-an-audience-condition-2-final-count.png)

>[!NOTE]
>
>Observe o uso do operador AND no grupo. Independentemente de você criar isso em um único grupo, como mostrado, ou em vários grupos, AND é importante, pois informa às Campanhas orquestradas que ambas as condições devem ser verdadeiras.



## Verificar contagens

1. Clique no **ícone Calcular** localizado no painel direito sob o título Perfis direcionados para obter uma estimativa exata do tamanho do público. Você vê **65** como a **contagem final**.

   ![Ícone Calcular mostrando o tamanho final do público de 65](assets/build-an-audience-calculate-final-audience-size.png)

   >[!NOTE]
   >
   >Observe como cada condição individual retornou um número diferente (condição #1 —> 241 e condição #2 —> 85), mas o tamanho do público final foi o menor das duas condições.  Isso é devido a esse operador AND.



2. Se você vir a contagem final de **65**, clique no botão **Confirmar**, na parte superior direita da tela, e clique no botão **Salvar**, na parte superior direita, para salvar seu trabalho.



## Desafio

Considere por um momento que você digitou a última condição de forma que `Make` fosse igual a `apple` (em minúsculas) e você tenha deixado a opção de configuração para `Case sensitive` alternada `on`.  Isso faria com que o registro de condições fosse igual a 0.  Então você teria 241 linhas ativas e 0 onde a marca é apple.



**Qual seria o tamanho final do público neste caso?**

![Última condição mostrando uma contagem de registro de 0 &quot;Última condição é 0&quot;](assets/build-an-audience-challenge-zero-count-condition.png "Última condição é 0")

## Resposta

É zero. Você sabe por quê?

![Explicação do motivo da contagem final ser zero](assets/build-an-audience-answer-zero-count-explanation.png)



## Recapitulação

Você criou seu primeiro público-alvo com sucesso e agora deve ver como é fácil desenvolver e validar suas contagens na atividade Criar público-alvo.

![Atividade Criar público concluída após a recapitulação](assets/build-an-audience-recap-completed-audience.png)
