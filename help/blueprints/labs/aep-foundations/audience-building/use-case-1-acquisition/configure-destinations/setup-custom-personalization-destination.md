---
hold: true
title: Configurar destino do Personalization personalizado
description: Configure um destino do Personalization personalizado para enviar atributos de perfil à Edge Network para uso em tempo real por um sistema de personalização de terceiros.
doc-type: article
solution: Experience Platform
exl-id: 46073f7c-00f4-4a4f-9fa3-8827ef15ec4a
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---


# Configurar destino do Personalization personalizado

Usar um [Destino personalizado do Personalization](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/custom-personalization) é uma maneira de disponibilizar públicos-alvo no Edge para uso por terceiros, geralmente usando a API do Servidor de Rede, para uso na Personalização.

Esse laboratório configura o Destino personalizado do Personalization para que possamos enviar Atributos de perfil para a Edge.



## Procurar catálogo de destino

>[!NOTE]
>
>Para personalizar usando o Adobe Target, usaríamos o [Destino do Adobe Target.](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/adobe-target-v2) O comportamento é idêntico ao do Personalization personalizado.

1. No painel à esquerda, clique em **Destinos**
1. No painel superior, clique em **Catálogo**
1. Em seguida, selecione a categoria de **Personalization**
1. No meio da tela, você deverá ver o destino intitulado **Personalization Personalizado com Atributos.** Clique no botão **Configurar** nesse cartão.

![Procurar catálogo de destino para destino Personalization Personalizado](assets/setup-custom-personalization-destination-browse-destination-catalog.png "Procurar catálogo de destino para destino Personalization Personalizado")



## Configurar destino

### Configurar conta

Nomeie sua conta `DEP Labs Custom PZN` e clique no **botão Conectar ao destino**

![Criar conta PZN e conectar-se à tela de destino](assets/setup-custom-personalization-destination-create-pzn-account.png)



### Adicionar detalhes do destino

Preencha os seguintes detalhes do destino:

1. Nome -> **Destino Edge**
1. Alias de Integração -> **edgeAlias**
1. ID da sequência de dados -> *selecione o nome da sequência de dados criado anteriormente*
1. Quando terminar, clique no botão **Avançar**

![Preencher detalhes do destino](assets/setup-custom-personalization-destination-fill-destination-details.png "Preencher detalhes do destino")

>[!CAUTION]
>
>Depois de clicar em Avançar, você não poderá alterar o **Nome** nem o **Alias de integração**.  Esses itens aparecerão posteriormente nas respostas do Edge Network



### Selecionar política de governança

Selecione **Personalization no site** e clique no botão **Criar**

![Selecionar política de governança](assets/setup-custom-personalization-destination-select-governance-policy.png "Selecionar política de governança")

>[!NOTE]
>
>Embora essa etapa seja opcional, é altamente recomendável que qualquer destino criado tenha uma política de governança atribuída para evitar a ativação incorreta de perfis



Quando terminar, você deverá ver esta tela observando seu sucesso!

![Criação bem-sucedida do destino PZN](assets/setup-custom-personalization-destination-successful-creation-screen.png "Criação bem-sucedida do destino PZN")



## Ativar destino

### Selecionar públicos

Selecione o destino que acabou de criar clicando na linha para realçá-la e clique no botão **Avançar**

![Selecionar destino PZN](assets/setup-custom-personalization-destination-select-destination-row.png "Selecionar destino PZN")



Selecione **Todos os públicos** e clique em **Avançar**

![Selecionar Públicos-Alvo da PZN](assets/setup-custom-personalization-destination-select-all-audiences.png "Selecionar Públicos-Alvo da PZN")



### Mapeamento

Adicione um **novo mapeamento** da seguinte maneira:

| Campo do Source | Campo de destino |
| ---------------------- | ------------ |
| \_tenantName.plan.name | Nome do plano |

> [!NOTE]
>
>Lembre-se de substituir **\_tenantName** pelo seu nome de locatário

>[!NOTE]
>
>O Campo de público-alvo permite fornecer um nome amigável que pode ser diferente do nome XDM



Quando terminar, sua tela deve ficar parecida com a imagem abaixo.  Você pode clicar no **botão**

![Criar Mapeamento PZN](assets/setup-custom-personalization-destination-create-mapping.png "Criar Mapeamento PZN")

>[!NOTE]
>
>Como os atributos de perfil podem conter dados confidenciais, todas as chamadas da [API do Edge Network Server](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview) devem ser feitas em um contexto autenticado para recuperar o atributo após sua inclusão na Edge.


### Revisão

Na tela final, é possível revisar os detalhes da configuração e clicar no botão Finish.

![Revisar e Publicar Destino PZN](assets/setup-custom-personalization-destination-review-and-publish.png "Revisar e Publicar Destino PZN")

>[!NOTE]
>
>Este é o ponto em que a [Imposição Automática](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/enforcement/auto-enforcement) verifica as [Políticas de Uso de Dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/policies/overview). Ele verificará suas Ações de marketing com as Regras que você criou e gerará erros.
