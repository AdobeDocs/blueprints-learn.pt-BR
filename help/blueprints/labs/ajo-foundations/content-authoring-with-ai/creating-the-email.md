---
title: Criação do email
description: Saiba como aplicar um modelo de conteúdo de marca a um email de campanha no Adobe Journey Optimizer e substituir imagens herói e de produto.
doc-type: article
solution: Experience Platform
exl-id: bf823714-7298-48fc-a18b-9bf2462ae52e
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---


# Criação do email

## Criação de conteúdo com modelos

**Finalidade:** saiba como criar modelos reutilizáveis no Adobe Journey Optimizer e aplicá-los a um email real em uma campanha.

## Objetivos de aprendizagem

Ao final deste módulo, você será capaz de:

1. Crie uma nova campanha e use seu novo modelo de marca.
1. Atualize as imagens principais, as imagens do produto, os botões e o estilo de layout.

## Criar e atualizar o email em uma campanha

### Objetivo

Neste exercício, aprenderemos como aplicar o modelo criado a um email dentro de uma jornada. Em um cenário ideal, você pode usar qualquer jornada ou campanha existente e substituir seu conteúdo de email por um modelo padronizado para garantir a consistência da marca e uma execução mais rápida.

Esta etapa demonstra como os modelos podem ser reutilizados em jornadas, permitindo que as equipes atualizem designs sem recriar emails do zero.

## Criar nova campanha de email

1. Volte para a tela principal e clique em **Gerenciamento do Jornada → Campanhas**.
2. Clique em **Criar campanha**

   ![Botão Criar Campanha no Gerenciamento do Jornada](assets/creating-the-email-click-create-campaign-button.png)

3. Selecione &quot;**Orquestração - Marketing**&quot; e clique em **confirmar**

   ![Selecionar Orquestração - Marketing e clique em confirmar](assets/creating-the-email-select-orchestration-marketing.png)

4. Nomeie sua campanha `Flagship Phone Launch Branded`. Pressione o botão **Salvar**.

   ![Nomear a campanha como Inicialização Telefônica Flagrante com a marca e clicar em Salvar](assets/creating-the-email-name-campaign-save.png)

5. Clique no sinal **+** e selecione a atividade **Ler público**

   ![Sinal de adição para selecionar a atividade Ler Público](assets/creating-the-email-click-plus-read-audience.png)

6. A próxima etapa é selecionar a caixa **&quot;Ler público-alvo&quot;** e clicar no **ícone da pasta Público-alvo**

   ![Ler caixa de Público-alvo e ícone de pasta de Público-alvo](assets/creating-the-email-read-audience-folder-icon.png)

7. Selecione a **dep: Interessado no público-alvo do iPhone 17** e clique no botão &quot;**Adicionar público-alvo**&quot;

   ![Selecionando o público-alvo Interessado no iPhone 17 e clicando em Adicionar público-alvo](assets/creating-the-email-select-audience-add-button.png)

8. Selecione a Entidade - **dep-rel: Conta do Cliente - customer\_id** (ou qualquer uma, pois não importa para esta parte)
9. Adicione a **Atividade de email** clicando no sinal **+** e selecione **Email** nas atividades de Canal.

   ![Adicionando a atividade Email das atividades de Canal](assets/creating-the-email-add-email-channel-activity.png)

10. Clique em **Editar email**.

![Editar opção de email para a atividade de email da campanha](assets/creating-the-email-click-edit-email.png)

11. Clique na **guia Ação** e selecione **sua** configuração de email. Sua sandbox pode mostrar isso como Email relacional. (Selecione qualquer)

![Guia Ação com a configuração de email selecionada](assets/creating-the-email-action-tab-email-configuration.png)

12. Clique na **guia Conteúdo**

![Guia Conteúdo no editor de email](assets/creating-the-email-click-content-tab.png)

13. Clique em **Aplicar modelo de conteúdo**

![Aplicar a opção Modelo de Conteúdo no editor de email](assets/creating-the-email-click-apply-content-template.png)

14. Selecione o modelo **&quot;Modelo Promocional&quot;** que você criou e clique em **Confirmar**

![Selecionar o Modelo Promocional e clicar em Confirmar](assets/creating-the-email-select-promotional-template-confirm.png)

15. Clique em **Editar corpo do email**

![Editar opção de corpo de email após aplicar o modelo](assets/creating-the-email-click-edit-email-body.png)

16. Confirme se os novos blocos de cabeçalho, herói, rodapé e conteúdo são exibidos corretamente.

![Blocos de cabeçalho, cabeçalho, rodapé e conteúdo que aparecem corretamente no email](assets/creating-the-email-header-hero-footer-blocks-confirmed.png)


## Substituir imagem principal e imagens do produto

Alterar as imagens do herói e do telefone. Você precisa fazer upload do conteúdo para ativos da pasta do kit de ferramentas. Atualmente, a imagem do banner principal do seu produto é um espaço reservado.

1. Clique na imagem de banner principal quebrada.

   ![Clicando na imagem de banner principal do espaço reservado](assets/creating-the-email-click-broken-hero-banner-image.png)

2. Remova o URL de origem temporário.

   ![Removendo a URL de origem temporária da imagem](assets/creating-the-email-remove-temporary-source-url.png)

3. Clique em **Importar mídia**

   ![Botão Importar Mídia para a imagem herói](assets/creating-the-email-click-import-media.png)

4. Carregue `hero.png` do seu kit de ferramentas. (Você pode arrastar o arquivo)

   ![Carregando hero.png da pasta do kit de ferramentas](assets/creating-the-email-upload-hero-png-file.png)

5. Clique em **Avançar** Selecione **sua pasta para os ativos** e pressione **importar**

   ![Selecionar a pasta de ativos e clicar em Importar para a imagem herói](assets/creating-the-email-select-folder-import-hero.png)

6. Seu modelo de email está surgindo muito bem. Ela é exibida da seguinte forma. Clique em **&quot;Salvar&quot;** para salvar seu trabalho.

![Modelo de email atualizado com a nova imagem herói antes de salvar](assets/creating-the-email-save-updated-email-template.png)


## Exercício opcional

### Substituir imagens do produto

Vá em frente e atualize todas as imagens do produto (imagens fornecidas na pasta do kit de ferramentas) e também adicione borda arredondada ao seu gosto. Seu email fica melhor sem links quebrados, como mostrado abaixo. Repita o processo para todos os cartões de produto.

![Email com todas as imagens do produto atualizadas e sem links corrompidos](assets/creating-the-email-product-images-updated-no-broken-links.png)

## Recapitulação

Neste módulo, você:

- Criou uma nova campanha com email usando seu modelo de marca
- Imagens do herói e do produto atualizadas
- Estilo aprimorado

Agora você está pronto para seguir para o próximo módulo - **Assistente de IA e personalização de conteúdo**, em que você usará a IA para refinar o texto e gerar imagens automaticamente.
