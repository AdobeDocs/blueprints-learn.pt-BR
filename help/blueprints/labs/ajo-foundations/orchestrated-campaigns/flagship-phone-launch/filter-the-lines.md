---
title: Filtrar as linhas
description: Saiba como filtrar linhas de clientes que optaram por não participar com uma atividade Dividir e usar Alterar dimensão para alinhar uma dimensão de destino do fluxo de trabalho com a configuração do canal SMS.
doc-type: article
solution: Experience Platform
exl-id: fb556a27-5c73-4457-ae98-dba43d445c7f
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: f189618dc8bfa198b25d646faa3ca0e0f5af5916
workflow-type: tm+mt
source-wordcount: '443'
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



2. No painel direito, primeiro altere a opção Target para **Uma mensagem por dimensão secundária** e, em seguida, clique no botão **Editar mensagem móvel** para iniciar a configuração da mensagem SMS

   ![Botão Direcionar e Editar mensagem móvel no painel direito](assets/filter-the-lines-edit-sms-button.png)



3. Na navegação superior, clique no item de menu Ações e, no menu suspenso Configuração de mensagem móvel, selecione o canal criado anteriormente.

![Configuração de SMS mostrando com êxito o canal selecionado](assets/filter-the-lines-sms-configuration-selected.png)




## Recapitulação

Você filtrou todas as linhas que não podiam ser direcionadas com uma mensagem SMS devido à recusa, alterou a dimensão de linha para conta e adicionou uma atividade SMS para aqueles que podiam ser direcionados.
