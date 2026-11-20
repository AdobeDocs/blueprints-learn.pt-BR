---
title: Filtrar as linhas
description: Saiba como filtrar linhas de clientes que optaram por não participar com uma atividade Dividir e usar Alterar dimensão para alinhar uma dimensão de destino do fluxo de trabalho com a configuração do canal SMS.
doc-type: article
solution: Experience Platform
exl-id: fb556a27-5c73-4457-ae98-dba43d445c7f
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 8d5a87f094e2fba7abd7f5a9acf8e9e775d9b534
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%
---

# Filtrar as linhas

## Objetivo

No próximo conjunto de etapas, você filtrará todas as linhas que realmente não têm permissão para serem direcionadas com uma mensagem SMS devido à recusa no nível da linha.  Você não pode confiar aqui no consentimento do Perfil porque este é um público alvo em nível de linha.



## Configurar atividade de divisão

1. Clique no ícone **+** na transição inferior da atividade Fork e selecione a atividade **Split** no pop-up.

   ![Adicionar uma atividade Split à ramificação inferior](assets/filter-the-lines-add-split-activity.png)



2. No painel direito, atualize o Rótulo para informar o seguinte: `Filter out opt'd out lines`

   ![Dividir rótulo de atividade definido para Filtrar linhas recusadas](assets/filter-the-lines-set-split-label.png)



3. No painel direito, expanda a seção do segmento padrão **Subconjunto** e clique no botão **Criar filtro**

   ![Botão Criar filtro na seção Subconjunto](assets/filter-the-lines-create-filter-button.png)



4. Adicione uma condição para garantir que você remova todas as Linhas de Clientes que recusaram mensagens SMS e clique em **Confirmar**.

   ![Condição ao remover Linhas de Cliente recusadas pelo SMS](assets/filter-the-lines-sms-optin-condition.png)

   >[!NOTE]
   >
   >Você precisa descobrir como criar a condição, mas o resultado final corresponde à captura de tela acima.  Você conseguiu isso!



5. Clique no botão Salvar no canto superior direito para salvar seu trabalho.  Sua tela se parece agora...

![Tela de fluxo de trabalho após salvar a atividade de Split](assets/filter-the-lines-canvas-after-split-save.png)



## Adicionar dimensão de alteração

1. Na tela do fluxo de trabalho, clique no ícone **+** após a condição de divisão adicionada e selecione a atividade **Alterar dimensão**

   ![Adicionar a atividade Change dimension após a condição de divisão](assets/filter-the-lines-add-change-dimension-activity.png)

2. Atualize as propriedades da dimensão de alteração conforme descrito abaixo e clique em **Confirmar**:
Etiqueta: `Convert Line to Account`
Nova dimensão de destino: `dep-rel: Customer Account`

   ![Editar dimensão de destino](assets/filter-the-lines-add-edit-target-dimension.png)

   ![Editar dimensão de destino](assets/filter-the-lines-add-select-target-dimension.png)



## Adicionar a atividade de SMS

1. Clique no ícone **+** após a dimensão Change que você adicionou e selecione a **Atividade de mensagem móvel**

   ![Adicionar a atividade de mensagem móvel após a condição de divisão](assets/filter-the-lines-add-sms-activity.png)

   ![Atividade de SMS adicionada à tela do fluxo de trabalho](assets/filter-the-lines-sms-activity-on-canvas.png)



2. No painel direito, clique no botão **Editar mensagem móvel** para iniciar a configuração da mensagem SMS

   ![Botão Editar mensagem móvel no painel direito](assets/filter-the-lines-edit-sms-button-only.png)



3. Na navegação superior, clique no item de menu Ações e, no menu suspenso Configuração de mensagem móvel, selecione o canal criado anteriormente.

![Menu suspenso de configuração de SMS não mostrando nenhum erro de resultados](assets/filter-the-lines-sms-configuration-no-results.png)

>[!CAUTION]
>
>Oh, não 🫨!  Por que você não está obtendo nenhum resultado?  Você já não configurou seu canal de SMS?  O produto está quebrado?
>
>ABERRAÇÃO!!!!!!!!



## Momento de surtar

A configuração do canal para SMS já foi definida por você antecipadamente e atualmente parece que sim...

![Configuração de detalhes da execução definida durante o laboratório Configurar canal de SMS](assets/configure-sms-channel-final-execution-details.png)

**A forma como você lê isso é a seguinte:**

- Enviar uma mensagem por dimensão de destino (ou seja, Conta de Cliente) no número de registros relacionados encontrados na dimensão secundária (ou seja, Linha de Cliente)
- Execute cada delivery de SMS usando o número do celular encontrado na dimensão secundária (ou seja, Linha do cliente)

Essa capacidade exclusiva de enviar muitas mensagens para um perfil é um dos recursos principais do Orchestrated Campaigns, que o torna diferente do Jornada. No entanto, sua transição para a atividade de Mensagem móvel é definida como Conta do cliente. Isso permite que você o associe de volta ao Perfil de cliente em tempo real no momento do envio, para que as informações de delivery e rastreamento das mensagens sejam atribuídas a um perfil.


Então como você faz isso funcionar? Altere o destino de execução da mensagem para corresponder à configuração do canal 😀



## Alterar o Target e concluir a configuração da mensagem SMS

1. Clique no botão Voltar na tela de edição do SMS

   ![Botão Voltar para sair da tela de edição de SMS](assets/filter-the-lines-exit-sms-editor.png)



2. Com a atividade de mensagem móvel selecionada, no painel direito, primeiro altere a opção Target da opção padrão uma mensagem por perfil para a opção **Uma mensagem por dimensão secundária** e clique novamente em **Editar mensagem móvel**

   ![Alterar destino e depois botão Editar Mensagem Móvel no painel direito](assets/filter-the-lines-edit-sms-button.png)



3. Na navegação superior, clique no item de menu **Ações** e, no menu suspenso Configuração de mensagem móvel, selecione o canal criado anteriormente.

   ![Configuração de SMS mostrando com êxito o canal selecionado](assets/filter-the-lines-sms-configuration-selected.png)



## Recapitulação

Você filtrou todas as linhas que não podiam ser direcionadas com uma mensagem SMS devido à recusa, alterou a dimensão de linha para conta e, no final, configurou com êxito a atividade de SMS para aqueles que tinham permissão para ser direcionados.
Esperamos que você também tenha aprendido algo muito importante - **seu público-alvo deve corresponder à configuração de canal que você deseja usar**
