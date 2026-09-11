---
title: Criar propriedade
description: Crie uma propriedade de encaminhamento de eventos com um elemento de dados e uma regra que encaminhe eventos de experiência recebidos para um ponto de extremidade de webhook.
doc-type: article
solution: Experience Platform
exl-id: eabd5f75-7706-4c96-982e-2512509bdc55
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 0%

---


# Criar propriedade

Normalmente, queremos encaminhar um Evento de experiência para terceiros (embora ele não precise ser). Normalmente, isso é usado quando uma cópia de um Evento é necessária em tempo real para notificar um terceiro em circunstâncias específicas (por exemplo, notificar a Google, a Meta ou a TikTok sobre uma compra).

>[!NOTE]
>
>Lembrete: uma propriedade contém todas as extensões, elementos de dados e regras necessários para decidir o que encaminhar e para onde

1. No painel à esquerda, clique em Encaminhamento de evento
2. Em seguida, clique em Nova propriedade

   ![A seção Encaminhamento de Eventos com o botão Nova Propriedade realçado](assets/create-property-new-property-button.png "Criar uma nova propriedade de encaminhamento de eventos")

3. Atualize o nome da propriedade usando a seguinte fórmula: `Event Forward Property SB + [sandbox number]`. Seu nome final seria mais ou menos assim: **Propriedade de Encaminhamento de Eventos SB01**

4. Clique em **Salvar** ao concluir

![Campo de nome da propriedade de Encaminhamento de Eventos preenchido com o botão Salvar realçado](assets/create-property-name-property-form.png)

## Instalar extensão

1. Clique na propriedade de encaminhamento de eventos que você acabou de criar

   ![Lista de propriedades de Encaminhamento de Eventos com a propriedade recém-criada realçada](assets/create-property-open-new-property.png "Abra a propriedade do evento")



2. Você deve ver uma tela como a abaixo.  Clique em **Extensões**.

   ![Tela de visão geral da propriedade de Encaminhamento de Eventos com a guia Extensões realçada](assets/create-property-click-extensions-tab.png)



3. Instale a extensão Adobe Cloud Connector fazendo o seguinte:

4. Clique em **Catálogo** na navegação superior
5. Clique no cartão **Adobe Cloud Connector**
6. No painel direito, clique no botão **Instalar**

![Catálogo de extensões com a placa do Adobe Cloud Connector e o botão Instalar realçados](assets/create-property-install-cloud-connector-extension.png)



Depois de clicar em Instalar, você deve ver a exibição da extensão nas extensões Instaladas da propriedade, como mostrado abaixo

![Lista de extensões instaladas mostrando a extensão do Adobe Cloud Connector instalada com êxito](assets/create-property-extension-installed-confirmation.png "Extensão totalmente instalada")

## Criar elemento de dados

>[!NOTE]
>
>Um elemento de dados faz referência ao evento recebido e pode analisá-lo em vários componentes individuais, se necessário

1. No painel à esquerda, clique em **Elementos de Dados**



   ![Navegação no painel esquerdo com o link de Elementos de Dados realçado](assets/create-property-navigate-to-data-elements.png "Navegar até os elementos de dados")



2. Clique no botão **Criar novo elemento de dados**

   ![A página Elementos de dados com o botão Criar novo elemento de dados realçado](assets/create-property-create-new-data-element-button.png "Criar novo elemento de dados")



3. Configure o novo elemento de dados com as seguintes informações:

   | Tipo de elemento | Valor a ser configurado |
   | ----------------- | ------------------ |
   | Nome | Objeto de dados |
   | Extensão | Núcleo |
   | Tipo de elemento de dados | Custom Code |

   ![Configuração do elemento de dados com os campos Nome, Extensão e Tipo de Elemento de Dados definidos](assets/create-property-data-element-config-step-1.png "Etapa 1 da configuração do elemento de dados")



4. Clique no botão **Abrir Editor** para adicionar o seguinte código personalizado:

   ![Configurações do elemento de dados com o botão Abrir Editor realçado para código personalizado](assets/create-property-open-custom-code-editor.png "Abrir o editor")



5. Adicione o código personalizado ao editor assim como e salve

   ```none
   var xdm = arc?.event || '';
   return xdm;
   ```

   ![Editor de código personalizado mostrando o script que retorna o objeto de evento XDM de entrada](assets/create-property-custom-code-added.png "Código personalizado")

   >[!NOTE]
   >
   >Isso está capturando todo o objeto xdm sem fazer qualquer tradução na carga útil.  Se necessário, podemos analisar cada parte individual do objeto XDM (por exemplo, nome da página, valor de compra) em um elemento de dados por campo.  A razão para fazer isso pode ser se houver transformação da estrutura para uma estrutura diferente





6. Clique no botão **Salvar** para salvar seu elemento de dados.

![Editor de elementos de dados com o botão Salvar realçado](assets/create-property-save-data-element-button.png)



Quando terminar, você deve ver a tela a seguir confirmando que o elemento de dados foi adicionado:

![Lista de Elementos de Dados mostrando o elemento de dados recém-salvo adicionado à propriedade](assets/create-property-data-element-saved-confirmation.png)


## Criar regras

>[!NOTE]
>
>Uma regra contém:
>
>1. Condições sobre o que enviar
>2. Ações que podem transformar a carga e definir para onde enviá-la



1. No painel esquerdo, clique em **Regras**

   ![Navegação no painel esquerdo com o link Regras realçado](assets/create-property-navigate-to-rules.png)



2. Em seguida, clique em **Criar nova regra**

   A página ![Regras com o botão Criar Nova Regra realçado](assets/create-property-new-rule-button.png)



3. Atualize o nome da regra usando a seguinte fórmula: `"EF Rule SB" + [your sandbox number]` (ou seja, Regra EF SB01). Você pode encontrar seu número de sandbox na parte superior direita da janela do navegador, como mostrado abaixo\...

   ![Canto superior direito da janela do navegador mostrando o número da sandbox usado no nome da regra](assets/create-property-sandbox-number-location.png)

4. Clique em **Salvar** ao concluir

   >[!NOTE]
   >
   >Verifique se o nome da regra segue o padrão de fórmula de `"EF Rule SB" + [sandbox number]`

   ![Campo de nome de regra preenchido com o padrão de nomenclatura da sandbox da Regra EF](assets/create-property-add-rule-name.png "Adicionar nome à regra")



5. Adicione uma Ação à regra clicando no sinal (+) para adicionar uma nova ação

![Editor de regras com o ícone de adição realçado para adicionar uma nova ação](assets/create-property-add-action-button.png "Adicionar uma ação")

## Obter URL do webhook (para usar em ação)

>[!NOTE]
>
>Este laboratório usa um webhook aqui para que você possa ver se os dados chegaram ao destino para o qual você está enviando. Em um cenário real, você faria logon nesse destino e usaria suas ferramentas para ver o que chegou.



1. Abra o link a seguir em uma nova guia do navegador -> [https://webhook.site](https://webhook.site/)
2. Copie o URL exclusivo que você vê e salve-o em algum lugar seguro

   Página ![Webhook.site com a URL exclusiva realçada para cópia](assets/create-property-webhooksite-copy-url.png)



3. Configure sua ação com as seguintes informações:

| Configuração | Valor |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Extensão | Adobe Cloud Connector |
| Tipo de ação | Fazer chamada de busca |
| Método | Publicar |
| URL | Use o mesmo URL do webhook que você usou ao configurar o destino de streaming. Você pode encontrá-la abrindo uma nova guia no navegador e navegando até Destinos -> Navegar |
| Corpo | Brutos |
| Dados do corpo | \{ &quot;data&quot;: \{ &quot;event&quot;: &quot;\{\{Data Object\}\}&quot; } } |

>[!NOTE]
>
>O \{\{Data Object\}\} referenciado aqui é o elemento de dados criado anteriormente. Aqui, o requisito do sistema downstream era que ele quisesse envolver o evento em um objeto de dados com um objeto de evento. Você pode colocar qualquer formatação aqui.
>
>Se tivéssemos dividido \{\{Data Object\}\} em vários campos (por exemplo, nome da página, compra etc.), poderíamos transformar a estrutura JSON colocando cada campo no local desejado, dando-nos mais controle sobre a correspondência do destino.





Quando você terminar, valide sua tela com aparência semelhante à mostrada abaixo e clique em **Manter alterações**

![Ação de regra configurada com as configurações Fazer busca da chamada do Adobe Cloud Connector e URL do webhook](assets/create-property-configure-action-settings.png "Configurar a ação")



4. Quando terminar, você deverá ver sua ação adicionada à regra. Clique em **Salvar** para continuar.

![O editor de regras mostra a ação configurada com o botão Salvar realçado](assets/create-property-save-rule-button.png "Salvar sua regra")

>[!WARNING]
>
>Ao enviar um Evento de experiência, você está enviando o Evento, não o Perfil, nem qualquer um de seus atributos, incluindo qualquer Qualificação de público-alvo (mesmo se for um público-alvo da Edge).
>
>Isso acontece para fins de velocidade.



## Publicar as alterações

1. No painel esquerdo, clique em **Fluxo de publicação**

   ![Navegação no painel esquerdo com o link Fluxo de publicação destacado](assets/create-property-navigate-to-publishing-flow.png "Navegar até o Fluxo de publicação")



2. Clique no botão **Adicionar Biblioteca**

   ![Página de Fluxo de Publicação com o botão Adicionar Biblioteca realçado](assets/create-property-add-library-button.png "Adicionar biblioteca")



3. Configure a biblioteca com as seguintes informações:

   - Nome -> **EF Biblioteca**
   - Ambiente -> **Desenvolvimento**
   - Clique em **Adicionar todos os recursos alterados**


   Quando terminar, sua tela deve ser semelhante à captura de tela abaixo.  Se tudo estiver bem, clique no botão **Salvar e criar no desenvolvimento**

   ![Configuração de biblioteca com nome, ambiente de desenvolvimento e botão Salvar e criar no desenvolvimento](assets/create-property-configure-library-save-and-build.png)



4. Você deve ver a build de desenvolvimento ficar verde, declarando que está pronta para uso

![Fluxo de Publicação mostrando o status da compilação de desenvolvimento como verde e pronto para uso](assets/create-property-development-build-ready.png)
