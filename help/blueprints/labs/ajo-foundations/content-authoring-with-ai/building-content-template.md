---
title: Criação do modelo de conteúdo
description: Saiba como criar um modelo de email reutilizável no Adobe Journey Optimizer importando o HTML e inserindo um fragmento de cabeçalho criado anteriormente.
doc-type: article
solution: Experience Platform
exl-id: e73f06b1-be8a-4096-949c-900db13db9f8
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---


# Criação do modelo de conteúdo

## Criação de conteúdo com modelos e fragmentos

**Finalidade:** Saiba como criar modelos reutilizáveis no Adobe Journey Optimizer

## Objetivos de aprendizagem

Ao final deste módulo, você será capaz de:

1. Crie um modelo de email completo usando o HTML e fragmentos importados.

## Por que os modelos são importantes

Os templates permitem criar conteúdo consistente e alinhado à marca, que pode ser reutilizado em emails, campanhas e jornadas.

### Modelos

Blueprints que estruturam:

- Posicionamento do cabeçalho
- Área de conteúdo do corpo
- Área de rodapé
- Estilo de layout padrão

Os modelos garantem a consistência da marca em todas as equipes e economizam tempo significativo de criação.


## Criar um novo modelo usando fragmentos

Os modelos ajudam os usuários a reutilizar layouts completos em campanhas. Os modelos de conteúdo no Adobe Journey Optimizer são ferramentas eficientes projetadas para simplificar e simplificar a maneira como você cria conteúdo reutilizável para campanhas e jornadas. Independentemente de você estar criando um email, SMS ou notificação por push, os modelos ajudam a economizar tempo, fornecendo estruturas pré-projetadas que podem ser facilmente personalizadas e compartilhadas entre projetos.

Para um processo de design acelerado e aprimorado, crie modelos independentes para reutilizar conteúdo personalizado facilmente em campanhas e jornadas do Journey Optimizer.

Essa funcionalidade permite que usuários orientados a conteúdo trabalhem em modelos fora de campanhas ou jornadas. Os usuários de marketing podem então reutilizar e adaptar esses modelos de conteúdo independentes em suas próprias jornadas ou campanhas.

## Criar modelo

1. Vá para **Gerenciamento de Conteúdo → Modelos de Conteúdo**.

   ![Navegando até Gerenciamento de Conteúdo e depois Modelos de Conteúdo](assets/building-content-template-navigate-content-templates.png)

2. Clique em **Criar Modelo** e preencha o seguinte:
   - **Nome:** `Promotional Template`
   - **Descrição:** `Promotional Template for phone products`
   - **Canal:** `Email`

   ![Criar formulário de modelo com nome, descrição e canal de email](assets/building-content-template-create-template-form-fields.png)

3. Clique em **Create**.

![Botão Criar para concluir a criação do Modelo Promocional](assets/building-content-template-click-create-button.png)


## Adicionar linha de assunto e abrir designer de email

1. Adicionar linha de assunto: `Promotional Template` e clique em **no corpo do email** para abri-lo para edição

   ![Adicionando a linha de assunto e abrindo o corpo do email para edição](assets/building-content-template-add-subject-line-open-editor.png)

2. Há três opções:
   1. Criar do zero
   2. Desenvolva o seu
   3. Importar HTML

Selecione a terceira opção. Clique em **Importar HTML**



![Selecionar a opção Importar HTML entre as três opções de design](assets/building-content-template-select-import-html-option.png)

## Importar modelo do HTML fornecido



1. Carregar o arquivo html de modelo da pasta do kit de ferramentas `promotional-template-final.html`

   ![Carregando promocional-modelo-final.html da pasta do kit de ferramentas](assets/building-content-template-upload-html-template-file.png)

2. Clique no botão Importar para **importar** o modelo.

   ![Botão Importar para importar o modelo HTML carregado](assets/building-content-template-click-import-button.png)

3. Aguarde a renderização do layout. Você percebe problemas como links de imagem quebrados e ausência de identidade visual. (Esse é o comportamento esperado, pois temos ativos de espaço reservado)

![Modelo renderizado mostrando links de imagens corrompidos e espaços reservados para marcas ausentes](assets/building-content-template-rendered-template-broken-images.png)


## Explorar estrutura do modelo

### Painel esquerdo

Os componentes de &quot;**Estruturas**&quot; e &quot;**Conteúdo**&quot; no Adobe Journey Optimizer (AJO) são elementos essenciais usados ao criar emails, páginas de aterrissagem e fragmentos de conteúdo. As estruturas definem a estrutura de layout, enquanto o Conteúdo fornece os blocos de construção reais colocados dentro desses layouts.

A seção do corpo no Adobe Journey Optimizer é o container principal do seu conteúdo de email ou página. Ele serve como a raiz do espaço de design visual, onde todos os componentes de estrutura (colunas, layouts) e componentes de conteúdo (texto, imagens, botões etc.) são aninhados.

### Painel direito

As opções &quot;**Configurações**&quot; e &quot;**Estilo**&quot; na seção do corpo do Adobe Journey Optimizer permitem definir a aparência e o layout fundamentais do seu email ou página. Esses controles afetam o design inteiro, pois o corpo é o pai de todos os componentes.

![Opções de Configurações e Estilo no painel direito da seção de corpo](assets/building-content-template-body-settings-style-panel.png)


Na barra do painel esquerdo, há seções para:

- Fragmentos
- Arquivos
- Estrutura do corpo
- URLs rastreados

Você verá que o fragmento do cabeçalho criado no exercício anterior aparece aqui, como mostrado abaixo. Certifique-se de que o fragmento de cabeçalho seja exibido como ativo com um ponto azul e não no modo de rascunho. Passe tempo verificando o restante das seções.

![Fragmento de cabeçalho mostrado ao vivo com um ponto azul na barra lateral esquerda](assets/building-content-template-header-fragment-live-sidebar.png)

>[!NOTE]
>
>Se você não vir seu fragmento aqui, significa que não o salvou corretamente e precisa carregá-lo novamente.



## Inserir fragmentos de cabeçalho

Agora, melhore o template. Você já criou o cabeçalho e o rodapé.

1. Arraste uma **Coluna 1:1** acima do conteúdo existente.

   ![Arrastando uma Coluna 1:1 acima do conteúdo do modelo existente](assets/building-content-template-drag-1-1-column-above-content.png)

   Você vê algo assim.

   ![Layout do modelo depois de adicionar a nova coluna acima do conteúdo](assets/building-content-template-column-added-above-content.png)

2. O plano de fundo usa a cor de plano de fundo do modelo, que atualmente é preta. Defina sua cor de fundo **para branco. Clique em** na guia Estilo no painel direito e use a cor branca do seletor de cores.

   ![Definindo a cor de plano de fundo da coluna para branco usando o seletor de cores](assets/building-content-template-set-background-color-white.png)

3. Abra **Fragmentos** e arraste o fragmento **Cabeçalho**.

   ![Arrastando o fragmento de cabeçalho para o modelo a partir do painel Fragmentos](assets/building-content-template-drag-header-fragment-into-template.png)

4. Observe que o fragmento do cabeçalho está alinhado perfeitamente ao seu modelo, conforme mostrado abaixo.

   ![Fragmento de cabeçalho perfeitamente alinhado no modelo](assets/building-content-template-header-fragment-aligned-template.png)

5. Clique no botão **Salvar** para salvar seu modelo e em **Voltar**.

![Botão Salvar para salvar o modelo antes de clicar em Voltar](assets/building-content-template-click-save-button-template.png)

>[!NOTE]
>
>Observe que você pode ver algumas imagens quebradas. Resolveremos isso mais tarde.


## Recapitulação

Neste módulo, você:

- HTML importado para criar um modelo promocional completo

Agora você está pronto para seguir para o próximo módulo - **Criando o email**
