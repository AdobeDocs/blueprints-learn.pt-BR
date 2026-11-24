---
title: Simulação de conteúdo
description: Saiba como usar a ferramenta de simulação do Adobe Journey Optimizer com dados de perfil de amostra para validar campos personalizados, variantes de conteúdo e comportamento de fallback.
doc-type: article
solution: Experience Platform
exl-id: 3e2b064f-5680-461c-a49e-2a61514e146f
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: c0adb1eab9b0a1315e2041c1f2cb89a4bfdae4b2
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%
---

# Simulação de conteúdo

**Finalidade:** valide a personalização, a lógica condicional e as variantes de conteúdo usando as ferramentas de Simulação e Prova do Adobe Journey Optimizer.

## Objetivos de aprendizagem

Ao final deste módulo, você será capaz de:

1. Carregue e use dados de perfil de teste para simulação.
1. Validar campos personalizados e lógica de variante.
1. Testar comportamento de fallback para dados ausentes ou sem correspondência.

## Introdução

Neste módulo, você testará seu email com **duas variantes condicionais** usando a ferramenta Simulação no Adobe Journey Optimizer.
Isso permite que você visualize como clientes diferentes experimentarão sua mensagem personalizada, garantindo a precisão antes de lançar a campanha.

Você usará o arquivo de perfil de teste de exemplo **sample.csv** do seu kit de ferramentas.

![Exemplo de arquivo de perfil de teste sample.csv do kit de ferramentas](assets/content-simulation-sample-csv-toolkit-file.png)

## Abrir a ferramenta de simulação

1. Abra o email preenchido.
2. No email, clique em **Simular Conteúdo**.

![Clicar em Simular conteúdo e selecionar Simular variação de conteúdo](assets/content-simulation-click-simulate-content-variation.png)

Um painel de simulação é aberto após alguns segundos.

## Fazer upload dos dados do perfil de teste

1. Clique em **Carregar** na parte inferior para carregar os dados de entrada.

   ![Botão Carregar para dados de entrada no painel de simulação](assets/content-simulation-click-upload-input-data.png)

&#x200B;3. Escolha **sample.csv** e clique em **Continuar**.

   ![Escolhendo sample.csv e clicando em Abrir](assets/content-simulation-choose-sample-csv-continue.png)

O AJO processa o arquivo e prepara visualizações a tempo.
![Visualizações da variação](assets/content-simulation-variation-previews.png)


## Revisar renderização da variante

Ao clicar em Simular conteúdo no email, o AJO mostra as variantes lado a lado com base nos perfis carregados.

**Resultados esperados:**

- **Alex** → Vê **Variante 1** (Idade acima de 40)
Clique no ícone de lápis acima da primeira variante para **Mostrar detalhes da variante**

![Clique no ícone de lápis para exibir os detalhes da variante](assets/content-simulation-click-pencil-icon.png)

O cartão se inverterá para mostrar os detalhes nos quais a personalização se baseia
![Variante 1 de renderização de perfil do Alex para uma idade acima de 40](assets/content-simulation-variant-1-age-above-40.png)

- **Jason** → Vê **Variante 2** (Idade abaixo de 40)
Clique no ícone de lápis acima da segunda variante para **Mostrar detalhes da variante**

![Clique no ícone de lápis para exibir os detalhes da variante](assets/content-simulation-click-pencil-icon-for-second-variant.png)

Mude a visualização lado a lado para **Verticalmente empilhada** para ver os detalhes e a personalização de Jason lado a lado

![Variante 2 de renderização do perfil Jason para idade inferior a 40](assets/content-simulation-swap-view-to-vertically-stacked.png)

Ao rolar pelo conteúdo do email, podemos ver o nome completo do Jason, bem como a imagem do conteúdo condicional que escolhemos. Como isso é legal!

![Campo personalizado de nome completo mostrado para Jason na Variante 2](assets/content-simulation-personalized-name-field-variant-2.png)



## Validar comportamento de fallback

**Fallbacks e Padrões:** Verifique se o seu email trata adequadamente todos os dados ausentes ou cenários sem correspondência. Por exemplo, simule um perfil com um campo de ano de nascimento vazio ou que não se qualifique para nenhuma oferta direcionada. A visualização deve mostrar um bloco de conteúdo padrão ou um espaço reservado adequado, em vez de conteúdo corrompido ou vazio. Se a simulação mostrar uma seção vazia onde o conteúdo deve ser exibido, isso indica que talvez seja necessário configurar uma oferta substituta ou um texto padrão no design.


## Recapitulação

Neste módulo, você:

- Conteúdo personalizado simulado usando perfis de amostra
- Lógica de alternância de variante validada
- Campos personalizados confirmados são preenchidos corretamente

Agora você está pronto para o próximo módulo - **Alinhamento da marca**,
onde você avaliará seu e-mail em relação às diretrizes da marca Connection 5G usando IA.
