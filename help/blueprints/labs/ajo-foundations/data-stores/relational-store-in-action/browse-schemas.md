---
hold: true
title: Procurar esquemas
description: Saiba como procurar esquemas relacionais e visualizar diagramas de relacionamento de entidade no Adobe Experience Platform para entender os relacionamentos de esquema usados em campanhas.
doc-type: article
solution: Experience Platform
exl-id: ac0e6743-4a83-4a8b-9bc6-f012b636312e
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---


# Procurar esquemas

## Objetivo

No próximo conjunto de etapas, você navegará pela interface do usuário para visualizar os Esquemas e seus relacionamentos.  Isso é importante para se familiarizar com os esquemas e relacionamentos disponíveis ao criar sua campanha.

## Exibir esquemas

O modelo de dados relacionais 5G da Connection já foi criado para você. Você pode ver os esquemas por si mesmo navegando até a página **Esquemas -> Procurar** na interface.

Na caixa de pesquisa, digite `dep-rel` para ver todos os esquemas.

![Resultados de pesquisa mostrando todos os esquemas relacionais dep-rel](assets/browse-schemas-search-results.png)

>[!NOTE]
>
>Observe que o tipo de todos os esquemas é *Relacional*



## Exibir diagrama de relacionamento

Com esquemas XDM relacionais, você pode visualizar facilmente o diagrama de relacionamento de entidade (ERD) selecionando qualquer esquema e clicando no botão Exibir diagrama de relacionamento.

Faça o seguinte:

1. Clique na guia **Relações** e clique no botão **Exibir diagrama de relações**

![Guia Relações com o botão Exibir diagrama de relações](assets/browse-schemas-relationships-tab.png)



2. Clique em **Selecionar esquemas**
3. Na janela pop-up, selecione `dep-rel: Customer Account` e clique em **Confirmar**

![Pop-up Selecionar esquemas com dep-rel: Conta do Cliente escolhida](assets/browse-schemas-select-schema-popup.png)



4. No ERD, clique nos **3 pontos** e selecione **Mostrar entidades relacionadas**

![Opção Mostrar entidades relacionadas no menu de contexto ERD](assets/browse-schemas-show-related-entities.png)



5. Veja o ERD com todas as tabelas diretamente relacionadas ao dep-rel: Conta do Cliente. Como opção, você pode baixar o ERD como um arquivo PNG.

![Diagrama de relacionamento de entidade mostrando tabelas relacionadas à Conta do Cliente](assets/browse-schemas-erd-diagram.png)

>[!TIP]
>
>Muito legal, hein?!

## Recapitulação

Agora você viu como é fácil navegar pela interface do usuário de Esquema e Relações.  Você pode selecionar um ou mais esquemas específicos e navegar para ver os relacionamentos para ajudar a entender e usar os dados na orquestração de campanha.

Você pode ler mais [aqui](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/data-management/get-started-schemas), se estiver interessado.
