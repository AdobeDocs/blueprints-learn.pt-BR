---
hold: true
title: Criação de fragmentos de conteúdo
description: Saiba como dividir um design de email em fragmentos reutilizáveis, como um bloco de cabeçalho, que permanecem consistentes entre modelos no Adobe Journey Optimizer.
doc-type: article
solution: Experience Platform
exl-id: 253a9332-dc08-420d-ac11-2bf342f0dc38
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 0%

---


# Criação de fragmentos de conteúdo

## Criação de conteúdo com modelos e fragmentos

**Finalidade:** saiba como criar fragmentos reutilizáveis no Adobe Journey Optimizer e aplicá-los a um email real em uma jornada.

## Objetivos de aprendizagem

Ao final deste módulo, você será capaz de:

1. Divida um design de email em fragmentos reutilizáveis.
1. Crie fragmentos de cabeçalho, rodapé, banner, corpo e CTA.

## Por que os fragmentos são importantes

Os fragmentos permitem criar conteúdo consistente e alinhado à marca que pode ser reutilizado em emails, campanhas e jornadas.

### Fragmentos

Blocos de construção reutilizáveis, como:

- Cabeçalhos
- Rodapés
- CTA
- Banners
- Isenções de responsabilidade legais

Sempre que um fragmento é atualizado, todos os emails que o usam são atualizados automaticamente.

## Como isso se encaixa na criação de emails

- **Crie fragmentos** para elementos que raramente mudam.
- **Crie um modelo** que use esses fragmentos.
- **Use o modelo** no email da campanha e personalize seu conteúdo.

Abaixo está o email final que você criará neste laboratório.

![Design de email final que você criou neste laboratório](assets/building-content-fragments-final-email-preview.png)

Mas a equipe de design normalmente fornece modelos como este:

![Modelo de design genérico fornecido pela equipe de design](assets/building-content-fragments-generic-design-template.png)


## Etapa 1: Criar fragmentos de conteúdo

O modelo abaixo é um modelo de design genérico e nosso objetivo é dividi-lo em blocos de conteúdo repetíveis. No Adobe jornada Otimizer, isso é chamado de **Fragmentos**.

A primeira etapa é identificar quantos fragmentos precisamos criar. Nesse modelo, faz sentido usar 5 fragmentos, como mostrado abaixo.



![Modelo dividido em cinco fragmentos identificados](assets/building-content-fragments-five-fragments-identified.png)

Identificamos os modelos que exigem 5 fragmentos, como demonstrado a seguir.

- Cabeçalho
- Banner
- CTA
- Corpo
- Rodapé

>[!NOTE]
>
>Para este exercício, você cria apenas um fragmento de cabeçalho para economizar tempo.



Crie um fragmento de cabeçalho para começar. No entanto, antes de criar o fragmento, configure uma pasta de ativos, já que o ambiente de ativos é compartilhado. Para fazer isso, primeiro crie sua própria pasta.

1. Na navegação à esquerda, localize a seção **Gerenciamento de Conteúdo** e clique em **Assets**.

![Seção de gerenciamento de conteúdo com a opção Assets na navegação à esquerda](assets/building-content-fragments-content-management-assets-nav.png)

2. Clique em **Assets** na seção Gerenciamento do Assets.

![Opção do Assets na seção Gerenciamento do Assets](assets/building-content-fragments-assets-under-assets-management.png)

3. Crie uma pasta clicando no botão **&quot;Criar Pasta&quot;**.

![Botão Criar pasta na área do Assets](assets/building-content-fragments-click-create-folder-button.png)

4. Nomeie como seu nome e sobrenome. ex.: Nish\_Pithia\_LabAssets (algo que você possa lembrar)

![Nomeando a nova pasta de ativos com seu nome e sobrenome](assets/building-content-fragments-name-asset-folder.png)

5. **Crie um novo fragmento:** Em Gerenciamento de Conteúdo, clique em **Fragmentos** e crie um novo fragmento.

   Opção ![Fragmentos em Gerenciamento de conteúdo para criar um novo fragmento](assets/building-content-fragments-click-fragments-create-new.png)

   Dê um nome amigável como mostrado abaixo. Adicione todos os detalhes da seguinte maneira:

   Cabeçalho **Nome:**

   **Descrição:** Cabeçalho de fragmento para o modelo

   **Tipo:** Selecionar fragmento visual

   ![Campos de tipo de fragmento Visual, nome e descrição do fragmento do cabeçalho](assets/building-content-fragments-fragment-name-type-details.png)

6. Clique no **Botão Criar** no canto superior direito.

![Botão Criar na parte superior direita da caixa de diálogo Novo fragmento](assets/building-content-fragments-click-create-button-top-right.png)

Isso abre uma tela em branco do criador de fragmentos.

7. Clique nas colunas 1:1 em Estruturas e arraste na tela como mostrado abaixo. (Clique na imagem abaixo para ver o gráfico animado)

![Demonstração animada de arrastar uma estrutura de Colunas 1:1 para a tela do fragmento](assets/building-content-fragments-drag-1-1-columns-structure.gif)

8. Em seguida, arraste &quot;**image**&quot; na linha 1:1 que acabamos de adicionar

![Arrastando um componente de imagem para a linha 1:1](assets/building-content-fragments-drag-image-onto-row.png)

9. Carregue a imagem do logotipo fornecida. Clique no **&quot;Botão Importar mídia&quot;**

![Botão Importar mídia para carregar a imagem de logotipo](assets/building-content-fragments-click-import-media-button.png)

10. **Carregue o logotipo:** Carregue o logotipo (*C5G-Logo.png*) da pasta de imagens do kit de ferramentas e clique em Avançar.

![Selecionando C5G-Logo.png da pasta do kit de ferramentas para carregar](assets/building-content-fragments-upload-logo-select-file.png)

![Clique em Avançar após selecionar o carregamento do logotipo](assets/building-content-fragments-upload-logo-click-next.png)

11. Selecione a **pasta de ativos** que você criou e clique em **Importar**. O arquivo é salvo na sua pasta.

![Selecionando a pasta de ativos criada e clicando em Importar](assets/building-content-fragments-select-asset-folder-import.png)

12. O logotipo é colocado corretamente, mas é muito grande e precisa ser redimensionado. Para redimensionar o logotipo, atualize suas propriedades. Clique na **guia Estilo** e defina a largura para 40% arrastando o controle deslizante, como mostrado abaixo.

>[!NOTE]
>
>Observe que quando o botão de alternância está ativado, o número 40 representa % e não pixels. Se quiser um valor absoluto de pixel perfeito, alterne o botão para px.



![Controle deslizante de largura da guia de estilo definido como 40% para redimensionar o logotipo](assets/building-content-fragments-resize-logo-width-slider.png)

13. Clique em **&quot;Salvar&quot;** e seu fragmento será salvo. Você recebe uma notificação de barra verde na confirmação.

![Barra de confirmação verde depois de salvar o fragmento](assets/building-content-fragments-save-fragment-confirmation.png)

14. O fragmento salvo está no modo de rascunho. Antes de usá-lo, você precisa publicá-lo. Clique no botão **voltar**.

![Botão Voltar para sair do fragmento de rascunho antes de publicar](assets/building-content-fragments-click-back-button-draft.png)

15. Clique no botão **Publicar**. Você verá a mensagem &quot;Publicando fragmento, isso pode levar algum tempo. Notificaremos quando a tarefa for concluída.&quot; na confirmação. O fragmento está pronto para ser usado para criação de modelo.

![Botão Publicar e mensagem de confirmação do fragmento de publicação](assets/building-content-fragments-click-publish-fragment-button.png)

Você verá a alteração de status para **&quot;Ao vivo&quot;**. Nesse ponto, você concluiu a criação de um fragmento de cabeçalho, que é usado na próxima etapa.

![Status do fragmento do cabeçalho alterado para Em tempo real](assets/building-content-fragments-fragment-status-live.png)

>[!NOTE]
>
>Observe que, neste exercício, você criou apenas um fragmento. Na prática, os arquitetos podem optar por criar vários fragmentos, como cabeçalhos, rodapés ou outros componentes reutilizáveis.

## Recapitulação

Neste módulo, você:

- Dividir um email em um fragmento de cabeçalho reutilizável
- Criação de blocos de conteúdo de cabeçalho

Agora você está pronto para seguir para o próximo módulo - **Criação de modelo de conteúdo**, onde você usará o fragmento criado para gerar um novo modelo.
