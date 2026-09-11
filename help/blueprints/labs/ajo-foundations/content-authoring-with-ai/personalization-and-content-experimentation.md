---
title: Personalization e experimentação de conteúdo
description: Saiba como personalizar conteúdo de email com atributos de perfil e sintaxe Handlebars, e criar variantes de conteúdo condicional com base na idade no Adobe Journey Optimizer.
doc-type: article
solution: Experience Platform
exl-id: b79327e0-dfc4-49bf-a112-3675c825c479
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '1238'
ht-degree: 0%

---


# Personalization e experimentação de conteúdo

**Finalidade:** saiba como personalizar conteúdo de email usando atributos de perfil, criar variantes de conteúdo dinâmico e aplicar lógica condicional no Adobe Journey Optimizer.

## Objetivos de aprendizagem

Ao final deste módulo, você será capaz de:

1. Adicione campos de personalização usando atributos de perfil.
1. Use o Editor de personalização e a sintaxe Handlebars.
1. Crie variantes de conteúdo dinâmico com base na lógica do perfil.
1. Crie regras condicionais para blocos de conteúdo personalizados.
1. Teste a alternância de variante com base em atributos, como ano de nascimento.

## Introdução

A personalização no Adobe Journey Optimizer permite experiências individuais em escala.
Neste módulo, você deverá:

- Inserir texto personalizado (nome e sobrenome)
- Criar variantes de conteúdo com base na idade
- Aplicar lógica condicional usando atributos de perfil
- Preparar conteúdo para simulação no Módulo 7

O Personalization no Adobe Journey Optimizer permite criar experiências personalizadas e impactantes do cliente, personalizando dinamicamente o conteúdo com base em perfis individuais, comportamentos e dados contextuais. Quer você esteja criando emails, notificações ou ofertas personalizados, as ferramentas e técnicas fornecidas facilitam a conexão da mensagem certa à pessoa certa, na hora certa. Saiba como o Editor do Personalization, a sintaxe Handlebars e os dados do Adobe Experience Platform trabalham juntos para dar vida às suas ideias, explorar blocos de conteúdo reutilizáveis com fragmentos de expressão e mergulhar em funções avançadas de ajuda para explorar possibilidades mais profundas. Cada tópico desenvolve passo a passo suas habilidades, garantindo que você esteja pronto para projetar jornadas personalizadas com confiança.

## Adicionar personalização básica

Essa parte do exercício simplifica a personalização. Adicione o nome e o sobrenome ao email com base no perfil. O Personalization é baseado nos dados de perfil gerenciados pelo esquema do Perfil individual XDM definido. O esquema do Perfil individual XDM é o único esquema que você pode usar para personalizar conteúdo no Journey Optimizer.

1. Abra o email criado em módulos anteriores.
2. Adicione um bloco de texto acima do título herói com o conteúdo: **Olá,**
3. Clique no ícone **Personalização**.

   ![Ícone de personalização na barra de ferramentas de texto de email](assets/personalization-and-content-experimentation-click-personalization-icon.png)

4. Pesquisar **F****Nome**.

   ![Procurando o atributo First Name no painel de personalização](assets/personalization-and-content-experimentation-search-first-name-field.png)

5. Clique em **+** para adicioná-lo à área de expressão.
6. Adicione um **espaço** após o campo **Nome**.

   ![Adicionando um espaço após o campo Nome na área de expressão](assets/personalization-and-content-experimentation-add-space-after-first-name.png)

7. Repita o processo acima, mas desta vez pesquise e adicione **Sobrenome**.

   A sintaxe final mostra as variáveis de nome e sobrenome claramente separadas.

   ![Variáveis de nome e sobrenome claramente separadas na sintaxe de expressão](assets/personalization-and-content-experimentation-first-last-name-syntax-separated.png)

8. Valide o fragmento. Observe que há uma opção para salvar o conteúdo como fragmento. Esta é uma ótima oportunidade para fazer se estiver usando o Nome completo para outras criações de conteúdo de email. Pule isso e vá para a próxima etapa.
9. Clique em **Salvar**

Sua visualização fica assim. As chaves consistem em variáveis e cada indivíduo recebe um email com seu nome.

![Personalização salva mostrando variáveis de nome de chaves](assets/personalization-and-content-experimentation-curly-bracket-variables.png)

Nesse ponto, você sabe como adicionar personalização para perfis individuais.


## Introdução ao conteúdo dinâmico

O conteúdo dinâmico no Adobe Journey Optimizer permite criar mensagens personalizadas que se adaptam perfeitamente ao seu público-alvo. Usando regras condicionais, você pode adaptar emails, SMS e notificações por push com base em atributos de perfil, associação de público-alvo ou eventos em tempo real. Esteja você criando uma mensagem de fallback para quando critérios específicos não forem atendidos ou salvando regras reutilizáveis para fins de consistência, o editor de personalização e o Email Designer oferecem ferramentas intuitivas para dar vida às suas ideias.

Este é um caso de uso perfeito para adicionar conteúdo condicional ao email e personalizá-lo com base na idade do usuário.

Consulte seu esquema: Você tem **&quot;person.birthYear&quot;** como ano de nascimento. Esse atributo pode ser útil. Direcione e configure uma campanha com base na idade.

Para este exercício, você criará duas variantes com base na idade. Uma variante é direcionada a usuários com mais de 40 anos e a outra é direcionada a usuários com menos de 40 anos (talvez em meados de 20 e 30 anos). Qualquer pessoa nascida antes do ano de 1986 é considerada acima de 40, enquanto qualquer pessoa nascida em 1986 ou depois é considerada abaixo de 40.

**Lógica de idade**

Você usará o atributo de perfil `person.birthYear`.

| Grupo alvo | Condição |
| ------------ | ----------------- |
| Acima de 40 | birthYear \&lt; 1986 |
| Abaixo de 40 | birthYear >= 1986 |


## Criar duas variantes de imagem

Lembrar deste bloco que criamos no módulo anterior? Sua imagem é diferente da minha.

![Bloco de imagens criado no módulo anterior](assets/personalization-and-content-experimentation-existing-image-block.png)

Crie outra imagem para pessoas com menos de 40 anos (lembre-se, você criou uma imagem do Firefly de uma pessoa com 40 e poucos anos) e use-a para este exercício.

1. Selecione o bloco de imagem existente. (Clique na imagem) e clique em **Bloco Condicional**.
2. Clique em **Adicionar variante**.

   ![Botão Adicionar variante no bloco de imagem condicional](assets/personalization-and-content-experimentation-click-add-variant-button.png)

3. Renomeie a primeira variante para **Idade acima de 40**.

   ![Renomeando a primeira variante para Idade acima de 40](assets/personalization-and-content-experimentation-rename-variant-age-above-40.png)

4. Crie uma nova Variante clicando no botão **&quot;Adicionar Variante&quot;** e Renomeie-a para **Idade abaixo de 40.**

   ![Criação e renomeação de uma nova variante para Idade inferior a 40](assets/personalization-and-content-experimentation-create-variant-age-below-40.png)

5. É possível criar uma imagem usando o Firefly usando um prompt como &quot;mid-20-year-old&quot;. Entretanto, para economizar tempo, já temos uma imagem no kit de ferramentas chamada &quot;**variant-age-below-40.jpg**.
6. Clique na imagem e em Importar mídia.

   ![Clicar na imagem e importar mídia para a variante abaixo de 40](assets/personalization-and-content-experimentation-click-image-import-media.png)

7. Selecione a imagem **variant-age-below-40.jpg**. Importe-o clicando em **Próximo** e, por fim, pressione **Importar** na pasta (você já deve estar na pasta por padrão).

   ![Selecionar e importar a imagem variant-age-below-40.jpg](assets/personalization-and-content-experimentation-select-below-40-image.png)

8. Tente alternar entre variantes e verá uma imagem diferente aplicada.

Até agora, você criou o design, mas ainda não aplicou a lógica. A próxima etapa aplica a lógica.


## Aplicar lógica condicional a variantes

Ambas as variantes estão prontas, mas você ainda não aplicou a lógica condicional.

![Ambas as variantes de idade prontas antes da lógica condicional ser aplicada](assets/personalization-and-content-experimentation-variants-ready-no-logic-applied.png)

## Lógica para &quot;Idade acima de 40&quot;

1. Selecione e passe o mouse sobre a **Idade acima da variante 40**.
2. Clique no ícone **Lógica condicional**.

   ![Ícone de Lógica Condicional para a Idade acima de 40 variantes](assets/personalization-and-content-experimentation-click-conditional-logic-icon.png)

3. Crie uma nova condição.

   ![Criando uma nova condição para a Idade acima de 40 variantes](assets/personalization-and-content-experimentation-create-new-condition.png)

4. Pesquisar **ano** na lista de atributos.
5. Arraste **Ano de Nascimento** para a tela.
6. Definir condição para:
   - **birthYear \&lt; 1986**

   ![Condição definida como birthYear anterior a 1986](assets/personalization-and-content-experimentation-birthyear-lt-1986.png)

7. Nomeie a condição: **Idade acima de 40**
8. Adicionar uma descrição - &quot;**Variante de imagem para pessoas acima de 40**&quot;
9. Clique em **Adicionar → Selecionar**.

![Clicar em Adicionar e Selecionar para uma Idade acima de 40 condição](assets/personalization-and-content-experimentation-click-add-select-age-above-40.png)


## Lógica para &quot;Idade abaixo de 40&quot;

1. Selecione e passe o mouse sobre a seção **Idade abaixo de 40**.
2. Repita as etapas, mas altere a lógica para:
   - **birthYear >= 1986**

   ![Condição alterada para birthYear maior ou igual a 1986](assets/personalization-and-content-experimentation-condition-birthyear-greater-1986.png)

3. Nomear a condição: **Idade abaixo de 40**
4. Adicionar descrição. &quot;**Variante de imagem para pessoas abaixo de 40**&quot;
5. Clique em **Adicionar → Selecionar**.

![Clicar em Adicionar e Selecionar para a condição Idade abaixo de 40](assets/personalization-and-content-experimentation-click-add-select-age-below-40.png)


## Validar alternância de variante

Alterne entre as duas variantes para garantir:

- As imagens corretas são exibidas
- A lógica foi aplicada corretamente
- Nenhuma variante é exibida como &quot;Nenhuma condição aplicada&quot;

Variante: **Idade acima de 40**

![Validando a Idade acima de 40 variantes com lógica correta aplicada](assets/personalization-and-content-experimentation-validate-variant-age-above-40.png)

Variante: **Idade abaixo de 40**

![Validando a Idade abaixo de 40 variantes com lógica correta aplicada](assets/personalization-and-content-experimentation-validate-variant-age-below-40.png)



Clique no botão &quot;**Salvar**&quot; para salvar o email.

![Botão Salvar para salvar o email com ambas as variantes](assets/personalization-and-content-experimentation-click-save-button-email.png)


## Recapitulação

Neste módulo, você aprendeu com sucesso a:

- Adicionar campos de personalização para mensagens individuais
- Criar variantes de imagem dinâmicas
- Aplicar regras condicionais com base na idade

Agora você está pronto para o próximo módulo - **Simulação de conteúdo**, para testar ambas as variantes.
