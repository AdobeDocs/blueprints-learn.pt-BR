---
hold: true
title: Configurar para relacional
description: Saiba como configurar um canal de email usando o atributo de email de um esquema relacional somente para Campanhas orquestradas.
doc-type: article
solution: Experience Platform
exl-id: 6f299942-79a6-42c2-8a5b-dd4bccd6aad4
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 10%

---


# Configurar para relacional

## Objetivo

No próximo conjunto de etapas, você criará uma Configuração de Canal de email para uso somente com Campanhas Orquestradas, usando o atributo `email` do esquema Relacional `dep-rel: Customer Account`

## Criar configuração de canal

1. Navegue até **Configurações de Canal** encontradas no menu **Administração → Canais → Configurações gerais**
2. Clique no botão **Criar configuração**

![Criar configuração de canal](assets/configure-for-profile-create-configuration-button.png)

3. No assistente Criar, defina os seguintes valores:
   - **Nome:** `Relational-Email`
   - **Canal:** `Email`
   - **Ação de marketing:** `Email Targeting`

![Detalhes de configuração do canal](assets/configure-for-relational-channel-configuration-name-values.png)

>[!NOTE]
>
>Ao selecionar Email como canal, uma nova seção Configurações de email é exibida.





## Configurar tipo de email

Defina o **Tipo de email** como **Marketing**

![Configurações de email](assets/configure-for-profile-set-email-type-marketing.png)

## Configurar subdomínio

Na lista suspensa **Subdomínio**, selecione **email.dep-labs.com**

![Subdomínio suspenso com email.dep-labs.com selecionado](assets/configure-for-profile-select-email-subdomain.png "Configurar Subdomínio")

## Configurar detalhes do pool de IPs

Na lista suspensa **Pool de IP**, selecione **marketing**

![Lista suspensa de pools de IP com marketing selecionado](assets/configure-for-profile-select-marketing-ip-pool.png "Configurar detalhes do pool de IP")

## Configurar cancelamento de inscrição da lista

1. Verifique se o botão de alternância está **habilitado** para list-unsubscribe
1. Na área de preferência List unsubscribe, verifique se todas as caixas de seleção estão **marcadas**
1. Em Gerenciamento de link, verifique se **Adobe managed** está selecionado
1. Para o nível de Consentimento, verifique se está definido como **Canal**

![Configurar cancelamento de inscrição na lista](assets/configure-for-profile-configure-list-unsubscribe-settings.png)

## Configurar parâmetros de cabeçalho

1. Defina os seguintes campos da seguinte maneira:
   - **De nome:** `DEP Labs`
   - **Do prefixo de email:** `dep`
   - **Responder ao nome:** `DEP Labs Support`
   - **Responder ao email:** `reply@email.dep-labs.com`
   - **Prefixo do email de erro:** `error`

![Parâmetros de cabeçalho](assets/configure-for-profile-email-header-parameters.png)

## Configurar email com CCO

Deixe em branco

>[!NOTE]
>
>Você pode manter uma cópia dos emails enviados enviando-os para uma caixa de entrada CCO. Digite o endereço de email de sua escolha para que cada email enviado seja copiado para o CCO. Observe que o domínio de endereço CCO deve ser distinto de qualquer subdomínio delegado à Adobe. Esse recurso é opcional. *Como usar Cco para emails*

## Configurar parâmetros de nova tentativa de email

Deixar com as configurações padrão de **Horas** definidas como **84**

## Configurar parâmetros de rastreamento de URL

Manter as configurações padrão

## Detalhes da execução

1. Na guia Campanha orquestrada e **marque** a caixa de seleção Habilitado.

![Configurar campanha orquestrada](assets/configure-for-profile-enable-orchestrated-campaign-tab.png)

2. Em Execution dimension, configure o seguinte:
   - **Entregar uma mensagem por:** `Target Dimension `
   - **Dimension de Destino do Perfil:** `dep-rel: Customer Account - customer_id`

![Dimensão de execução](assets/configure-for-relational-execution-dimension-target-settings.png)

3. Em Endereço de execução, configure o seguinte:
   - **Source:** `Target Dimension`
   - **Endereço de entrega:** `click on the Edit button`

![Dimension de Destino](assets/configure-for-relational-execution-address-source-target-dimension.png)

4. Na janela pop-up, clique na pasta **dep-rel: Conta de cliente**

![Configurar endereço de entrega](assets/configure-for-relational-customer-account-folder.png)

5. Selecione **Email** e clique no botão **Selecionar**

![Enviar email como endereço de entrega](assets/configure-for-relational-select-email-as-delivery-address.png)

6. Quando terminar, seus detalhes de Execução finais serão semelhantes à captura de tela abaixo

![Dimensão de execução configurada](assets/configure-for-relational-execution-details-final-result.png)

>[!NOTE]
>
>Para Campanhas orquestradas, você direciona a conta do cliente com um email para que só seja necessário enviar uma mensagem por Dimension do Target.  O Endereço de execução que você usa vem do próprio Target Dimension (isto é, o que está armazenado na tabela **dep-rel: Conta de cliente** para o endereço de **email**)


## Revisar e salvar

1. Revise todos os detalhes novamente para garantir que correspondam.
1. Role para cima e clique em **Enviar**.
1. Quando terminar, você verá duas configurações de canal de email, ambas provavelmente em um estado de &quot;processamento&quot;.

>[!WARNING]
>
>Observou-se que o processamento da configuração do canal de email leva até 2h!

## Recapitulação

Agora você viu como criar uma Configuração de canal de email para usar o atributo de esquema Relacional para Campanhas orquestradas.
