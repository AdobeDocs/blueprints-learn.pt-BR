---
title: Criar estratégia de seleção
description: Configure uma estratégia de seleção que vincule uma coleção de ofertas, regras de elegibilidade e uma fórmula de classificação para a tomada de decisão.
doc-type: article
solution: Experience Platform
exl-id: 066ad087-6845-4ab5-9a6e-8dad1aa848f8
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---


# Criar estratégia de seleção

## Objetivo

Até o momento, você criou ofertas, definiu a qualificação da oferta com uma regra de decisão, as reuniu em uma coleção e criou uma fórmula que as reorganiza dinamicamente com base nos atributos do perfil que solicita a personalização. Como estamos usando apenas um único conjunto de 4 ofertas para um único caso de uso, é tentador pensar que cada um desses elementos está relacionado, especialmente quando os nomeamos de forma semelhante. No entanto, é importante pensar de forma mais abstrata ao considerar uma estratégia de longo prazo e um escopo de tamanho empresarial. As ofertas podem ser classificadas em uma ou várias coleções. Fórmulas de classificação podem ser aplicadas a qualquer coleção de ofertas. Na realidade, a primeira vez que você realmente conecta esses elementos é ao criar uma Estratégia de seleção.

Imagine que tivéssemos centenas de ofertas utilizadas em quarenta coleções e uma dúzia de fórmulas de classificação. Como um pacote de decisão saberia qual fórmula de classificação aplicar a qual coleção de ofertas? A estratégia de seleção faz essa conexão. Ao adicionar a Decisão a um canal, o que você está adicionando é uma (ou várias) Estratégia(ões) de seleção.

## Criar a estratégia de seleção

1. Se necessário, expanda **Decisão** no painel esquerdo e clique em **Configuração de estratégia**. Você será direcionado para a página &quot;Regras de decisão&quot;, onde verá a Regra de decisão &quot;Planos de nível superior&quot; criada anteriormente e usada como requisitos de qualificação para os itens de oferta telefônica de nível superior.
2. Clique em **Estratégias de seleção** logo abaixo do menu &#39;Métodos de classificação&#39;. Sem estratégias de seleção disponíveis, clique no botão azul **Criar estratégia de seleção**.

   ![Página de Estratégias de Seleção com o botão Criar estratégia de seleção](assets/create-selection-strategy-create-button.png)

3. Nomeie a estratégia de seleção **Estratégia de seleção do iPhone 17**
4. Você pode ver que uma estratégia de seleção requer 3 itens.
   - Uma coleção de ofertas
   - Requisitos de elegibilidade
   - Um método de classificação

   Clique no botão **Selecionar coleção**, marque a caixa ao lado da única coleção que você tem (**coleção do iPhone 17**) e clique em **Salvar**.

5. Deixe a lista suspensa &quot;Elegibilidade&quot; definida como Todos visitantes.

   >[!NOTE]
   >
   >A elegibilidade pode ser aplicada no nível da oferta, do nível da estratégia de seleção ou do nível de Jornada/Campanha por meio dos critérios para inserção da Jornada ou Campanha. Tudo depende do caso de uso que você está tentando perceber. Se você clicar no menu suspenso **Qualificação**, verá as mesmas opções de Público-alvo e Regra de decisão que viu no nível da oferta. No nosso caso de uso, queríamos apenas limitar ofertas específicas, portanto, fazia sentido fazer a qualificação no nível da oferta.

6. Defina o **Método de classificação** como **fórmula** e clique no botão **Selecionar fórmula**

   >[!NOTE]
   >
   >Você pode ter notado as opções &quot;Prioridade da oferta&quot; e &quot;Modelo de IA&quot; no menu suspenso Método de classificação. Se você realmente deseja retornar ofertas usando apenas sua prioridade original, escolha a opção &quot;Prioridade de oferta&quot;.
   >
   >A opção Modelo de IA usa um modelo de IA que analisa impressões, cliques e conversões de ofertas retornadas para determinar qual oferta exibir para o indivíduo. Não os usaremos neste laboratório, pois há limites mínimos de dados e duas semanas necessárias para treinar os modelos.

7. Marque a caixa ao lado da única fórmula de Classificação que você tem (**Fórmula de Classificação do iPhone 17**) e clique em **Salvar**. Quando terminar, sua estratégia de seleção terá esta aparência:

   ![Estratégia de seleção concluída com coleção, qualificação e conjunto de fórmulas de classificação](assets/create-selection-strategy-completed-configuration.png)

8. Quando a estratégia de seleção estiver correta, clique no botão azul **Criar**.

>[!TIP]
>
>Agora você vê sua Estratégia de seleção do iPhone 17 no menu &quot;Estratégia de seleção&quot;

>[!NOTE]
>
>A decisão permite a seleção e a ordenação de ofertas muito simples ou muito complexas. No final simples, você pode ter uma coleção de ofertas com sua prioridade padrão, uma elegibilidade definida para todos os visitantes e o método de classificação de &quot;Prioridade de oferta&quot;, e todos os usuários finais veriam as ofertas na ordem de suas pontuações de prioridade originais. No outro extremo, você pode ter uma enorme coleção com pontuações de prioridade iniciais complexas, uma fórmula de classificação personalizada e regras de elegibilidade em camadas no nível da oferta e da estratégia de seleção. O que você criou nesse laboratório fica no meio e foi projetado para demonstrar as diferentes maneiras das configurações dos pacotes de decisão.

## Recapitulação

Nesta página, você criou uma estratégia de seleção que vincula os componentes principais criados até agora: a coleção de ofertas, as regras de elegibilidade e a fórmula de classificação.
