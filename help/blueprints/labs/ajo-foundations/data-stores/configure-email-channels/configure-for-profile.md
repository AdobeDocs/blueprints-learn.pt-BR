---
hold: true
title: Configurar para perfil
description: Saiba como configurar um canal de email usando o atributo personalEmail.address do perfil do AEP para Jornada e Campanhas orquestradas.
doc-type: article
solution: Experience Platform
exl-id: bb85e0aa-554e-4527-bf91-e7fd4f69ce71
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 8%

---


# Configurar para perfil

## Objetivo

No próximo conjunto de etapas, você criará uma Configuração de canal de email com Jornadas e Campanhas orquestradas usando o atributo de Perfil do AEP `personalEmail.address`

## Criar configuração de canal

1. Navegue até **Configurações de Canal** encontradas no menu **Administração → Canais → Configurações gerais**
2. Clique no botão **Criar configuração**

![Criar configuração de canal](assets/configure-for-profile-create-configuration-button.png)

&#x200B;3. No assistente Criar, defina os seguintes valores:
   - **Nome:** `Profile-Email`
   - **Canal:** `Email`
   - **Ação de marketing:** `Email Targeting`

![Detalhes de configuração do canal](assets/configure-for-profile-channel-configuration-name-values.png)

>[!NOTE]
>
>Ao selecionar Email como canal, uma nova seção **Configurações de email** é exibida.

## Configurar tipo de email

Defina o **Tipo de email** como **Marketing**

![Tipo de email](assets/configure-for-profile-set-email-type-marketing.png)

## Configurar subdomínio

Na lista suspensa **Subdomínio**, selecione **email.dep-labs.com**

![Subdomínio suspenso com email.dep-labs.com selecionado](assets/configure-for-profile-select-email-subdomain.png "Configurar Subdomínio")

## Configurar detalhes do pool de IPs

Na lista suspensa **Pool de IP**, selecione **marketing**

![Lista suspensa de pools de IP com marketing selecionado](assets/configure-for-profile-select-marketing-ip-pool.png "Detalhes do pool de IP")

## Configurar cancelamento de inscrição da lista

1. Verifique se o botão de alternância está **habilitado** para list-unsubscribe
1. Na área de preferência List unsubscribe, verifique se todas as caixas de seleção estão **marcadas**
1. Em Gerenciamento de link, verifique se **Adobe managed** está selecionado
1. Para o nível de Consentimento, verifique se está definido como **Canal**

![Cancelar inscrição da lista de configuração](assets/configure-for-profile-configure-list-unsubscribe-settings.png)

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

1. Conclua a seção **Detalhes da execução**. Na guia **Jornada e Ação** -> **Dimensão de execução**, selecione **Perfil** como **Source** e clique no ícone Editar para **Endereço de entrega** na seção **Endereço de execução**

![Detalhes da execução](assets/configure-for-profile-execution-details-journey-tab.png)

&#x200B;2. Clique na pasta denominada **Email Pessoal** para abri-lo

![Endereço de entrega](assets/configure-for-profile-personal-email-folder.png)

&#x200B;3. Clique na **caixa de seleção** no campo `Address` e no botão **Selecionar**

![Email Pessoal como Endereço de Entrega](assets/configure-for-profile-select-address-checkbox-journeys.png)

&#x200B;4. Para **Perfil**, `personalEmail.address` agora está configurado como o **Endereço de entrega** na seção **Endereço de Execução**

![Endereço de entrega configurado](assets/configure-for-profile-delivery-address-configured-journeys.png)

&#x200B;5. Clique na guia Campanha orquestrada e **marque** a caixa de seleção Habilitado.

![Configuração de campanha orquestrada](assets/configure-for-profile-enable-orchestrated-campaign-tab.png)

&#x200B;6. No cabeçalho Execution dimension, configure o seguinte:
   - **Entregar uma mensagem por:** `Target Dimension`
   - **Dimension de Destino do Perfil:** `dep-rel: Customer Account - customer_id`

![Dimension de Destino](assets/configure-for-profile-target-dimension-settings.png)

&#x200B;7. Em Endereço de execução, configure o seguinte:
   - **Source:** `Profile`
   - **Endereço de entrega:** `click on the Edit icon`

![Endereço de Execução](assets/configure-for-profile-execution-address-source-profile.png)

&#x200B;8. Procure por e clique na pasta `Personal Email` para abri-la

![Atributo de perfil de email pessoal](assets/configure-for-profile-search-personal-email-folder.png)

&#x200B;9. Selecione o campo `Address` na pasta Email Pessoal e clique em **Selecionar**

![Email Pessoal como Endereço de Entrega](assets/configure-for-profile-select-address-field-orchestrated.png)

&#x200B;10. Para a **campanha orquestrada**, a **dep-rel: Conta de Cliente - customer\_id** está configurada como **Dimension de Destino de Perfil** para a **Dimensão de Execução** com **Endereço de Execução** tendo uma **Source** do **Perfil** e `personalEmail.address` como **Endereço de entrega**

![Dimensão de execução configurada](assets/configure-for-profile-orchestrated-execution-dimension-configured.png)

>[!NOTE]
>
>Para Campanhas Orquestradas, você direciona a conta do cliente com um email para que envie apenas *uma mensagem por Perfil*.  O Endereço de execução que você usa vem do próprio Perfil (ou seja, o que é armazenado no Perfil do AEP sob o atributo **personalEmail.address**)


## Revisar e salvar

1. Revise todos os detalhes novamente para garantir que correspondam.
1. Role para cima e clique em **Enviar**.

&#x200B;> [!NOTE]
>
>Observou-se que o processamento da configuração do canal de email leva até 2h!  Uau!
>
>Prossiga para o próximo exercício enquanto aguarda o processamento dessa configuração de canal.

>[!TIP]
>
>🚀 Assim que o status de configuração do canal de email for **Ativo**, ele estará pronto e poderá ser selecionado diretamente nas **Atividades de email** dentro das Campanhas Orquestradas.

## Recapitulação

Agora você viu como criar uma Configuração de canal de email para usar o atributo de Perfil do AEP para Campanhas do Jornada e Orquestradas.
