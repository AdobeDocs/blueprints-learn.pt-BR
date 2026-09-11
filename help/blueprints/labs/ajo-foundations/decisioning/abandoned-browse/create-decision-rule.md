---
hold: true
title: Criar regra de decisão
description: Crie uma Regra de decisão que restrinja a qualificação para ofertas telefônicas premium a clientes em planos de nível superior.
doc-type: article
solution: Experience Platform
exl-id: 1c1e2d82-ca09-4074-813d-3b29af77388b
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---


# Criar regra de decisão

## Objetivo

Como a qualificação é um dos blocos fundamentais de uma oferta, a primeira etapa é criar as entidades necessárias para oferecer suporte a ela. Em muitos casos, a associação de público-alvo é o fator decisivo, mas, nesse caso, usaremos as Regras de decisão. Com a Connection 5G, os iPhone 17s de ponta só podem ser ativados para usuários com um plano de alto nível. Dessa forma, usaremos uma regra de decisão para garantir que as ofertas para telefones de ponta estejam disponíveis apenas para aqueles com um plano alto o suficiente.

## Criar a regra de decisão

1. Se necessário, faça logon na Adobe Experience Cloud e navegue até o **Adobe Journey Optimizer.**
2. Expanda o item de menu **Decisão** no painel esquerdo, se necessário, e clique em **Configuração de Estratégia.**

>[!WARNING]
>
>Certifique-se de estar no menu Decisão e NÃO no menu Gestão de decisões. Se o menu Gerenciamento de decisões for expandido, recolha-o para evitar confusão de navegação durante esse laboratório.

3. Clique em **Regras de Decisão** no menu &#39;Qualificação&#39;, seguido pelo botão **Criar regra** no canto superior direito.

![Página Regras de Decisão com o botão Criar regra](assets/create-decision-rule-create-rule-button.png)

&#x200B;4. Isso abre uma tela semelhante à interface do usuário do Construtor de segmentos. Adicione o atributo ID do plano à tela da regra clicando em **Perfil Individual XDM > DEP > Detalhes do plano** e arrastando o atributo **ID do plano** para a tela.
&#x200B;5. Altere o menu suspenso de igual a **contém.**
&#x200B;6. Insira o texto **2** na caixa, pressione a tecla **Tab** para aceitar o valor 2 e insira um **3,** pressione **Tab** novamente para que a regra procure IDs de Plano que contenham um 2 ou 3
&#x200B;7. Use a caixa de texto **Nome** no painel direito para nomear a Regra de decisão **Planos de camada superior**. Adicione uma descrição, se desejar. Quando terminar, sua Regra de decisão deverá ter esta aparência:

![Regra de decisão de Planos de Camada Superior concluída com ID de Plano contendo 2 ou 3](assets/create-decision-rule-upper-tier-plans-finished.png "Regra de decisão de Planos de Camada Superior concluída com ID de Plano contendo 2 ou 3")

&#x200B;8. Quando a regra estiver correta, clique no botão azul **Criar** no canto superior direito e você retornará à página Configuração de estratégia com a Regra de decisão que acabou de criar listada como a única regra de decisão.

>[!NOTE]
>
>Por que usar uma Regra de decisão em vez de um Público-alvo? Na prática, os principais motivos seriam a necessidade de critérios de elegibilidade específicos ao pacote de decisão ou de atributos das ofertas nos critérios. Os atributos da oferta não estão disponíveis nos campos do Construtor de público-alvo.
>
>A regra de decisão dos planos de nível superior usada nesse laboratório provavelmente seria um público-alvo real em uma implementação real, dada sua provável reutilização fora do Decisioning. No entanto, uma Regra de decisão foi usada aqui para fins educacionais e para mostrar sua funcionalidade e as várias maneiras das quais a elegibilidade pode ser aplicada.

## Recapitulação

Agora você criou uma Regra de decisão reutilizável, que será usada para qualificação de oferta.
