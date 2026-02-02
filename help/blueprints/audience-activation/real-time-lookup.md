---
title: Acesso ao perfil do Real-time Edge para Personalization da Web e móvel
description: Acesso de [!UICONTROL Perfil de cliente em tempo real] na borda para fornecer contexto para personalização da Web e móvel em tempo real.
solution: Real-Time Customer Data Platform, Data Collection
kt: 719
source-git-commit: 2fad3a8a9210d703130f251b0bd7cc4c0b7cbd32
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 6%

---

# Acesso ao perfil do Real-time Edge para Personalization da Web e móvel

O blueprint do Real-time Edge Profile Access for Web and Mobile Personalization mostra como os aplicativos da Web e móveis podem acessar o [!UICONTROL Perfil do cliente em tempo real] da Adobe Experience Platform na borda para personalização de alta taxa de transferência e baixa latência.

Os aplicativos podem acessar atributos de perfil e públicos-alvo em tempo real na borda com latência de milissegundos. Atributos, associações de público-alvo e recursos orientados por modelo armazenados no perfil como atributos podem ser acessados em tempo real para personalização de mesma página e próxima página em canais móveis e da Web.

Com esse recurso, você pode fornecer experiências altamente personalizadas em seus sites e aplicativos móveis com base no Perfil do cliente em tempo real, incluindo públicos derivados de comportamentos em tempo real, atributos assimilados no Perfil do cliente em tempo real e insights calculados.

>[!NOTE]
>
>O acesso ao perfil do Edge foi projetado especificamente para casos de uso de alta taxa de transferência e baixa latência, como personalização de entrada da Web/dispositivos móveis e o Offer Decisioning em tempo real. Para cenários de taxa de transferência mais baixa, como suporte assistido por agente ou interações de vendas, a API de pesquisa de perfil de hub é mais apropriada. Consulte o [blueprint de Acesso a Perfil em Tempo Real para Suporte e Cenários de Vendas](customer-activity.md) para obter acesso a perfil com base em hub.

## Aplicativos

* Real-time Customer Data Platform
* Coleta de dados do Adobe Experience Platform (Web SDK/Mobile SDK)
* API do servidor do Edge Network

## Casos de uso

* Personalização em tempo real na Web e em canais móveis para experiências conhecidas do cliente
* Personalização de mesma página e próxima página com base em atributos de perfil e públicos-alvo em tempo real
* Personalização de conteúdo e oferta com base em perfis de clientes, incluindo dados comportamentais em tempo real, atributos e insights calculados
* Integração com mecanismos de personalização, sistemas de gerenciamento de conteúdo e aplicativos externos para decisões em tempo real
* Otimização de testes e conteúdo com o contexto de perfil em tempo real

## Pré-requisitos

Este blueprint requer o uso de um dos seguintes métodos de coleção de dados se você quiser que o perfil seja atualizado em tempo real com dados de transmissão. É possível obter acesso em tempo real ao Perfil do Edge sem precisar coletar dados diretamente no Perfil do Edge; os dados também podem ser coletados no Hub e projetados no Perfil do Edge. Observe que haverá uma latência adicional para os dados coletados no Hub e depois projetados no Edge.

* Use o [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html) se desejar coletar dados do seu site.
* Use o [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/) se desejar coletar dados do seu aplicativo móvel.
* Use a [API do Edge Network Server](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=pt-BR) se não estiver usando o Web SDK ou o Mobile SDK, ou estiver implementando uma conexão mais direta de servidor para servidor.

>[!IMPORTANT]
>
>Antes de implementar a personalização de borda, leia o manual sobre como [ativar dados de público-alvo para destinos de personalização de borda](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations). Este guia aborda as etapas de configuração necessárias para casos de uso de personalização de mesma página e próxima página em vários componentes do Experience Platform.

## Diagrama da arquitetura

<img src="assets/real-time-edge-lookup.svg" alt="Arquitetura de referência para acesso ao perfil do Edge para Personalization da Web e móvel" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />

## Medidas de proteção

* [Medidas de proteção para dados de [!UICONTROL perfis de cliente em tempo real]](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)
* [Medidas de Proteção do Edge Network](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* Os perfis do Edge têm um TTL (time-to-live) de 14 dias. Se um usuário não estiver ativo na borda por 14 dias, o perfil da borda pode expirar e precisa ser buscado no hub, o que pode afetar a personalização da primeira página.
* A personalização do Edge oferece suporte à avaliação de associação de público-alvo em tempo real para públicos que atendem aos critérios de segmentação de borda. Os públicos-alvo de lote e transmissão do hub também estão disponíveis na borda com a configuração apropriada.

## Padrões de implantação

A personalização do Edge pode ser implementada usando o destino [Conexão personalizada com o Personalization](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/custom-personalization) na Plataforma de dados do cliente em tempo real. Esse destino oferece suporte a vários métodos de coleta de dados, dependendo do caso de uso.

### Padrão 1: Personalização baseada em associação de público-alvo com o Web SDK/SDK móvel

* Use o Adobe Experience Platform Web SDK ou o Mobile SDK com o Edge Network para personalização baseada em associação de público-alvo.
* Essa abordagem fornece baixa latência e melhor desempenho para personalização de borda com base em associações de público-alvo.
* A segmentação de borda em tempo real exige a implementação do SDK da Web/móvel.
* O Web SDK e o Mobile SDK **oferecem suporte à personalização apenas com base na associação de público-alvo**.
* [Consulte o Blueprint da Web e do SDK Móvel da Experience Platform](../experience-platform/deployment/websdk.md) para implementação com base no SDK.
* Para implementação do Mobile SDK, a [Adobe Journey Optimizer - Extensão de decisão](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/) deve ser instalada no Mobile SDK.

### Padrão 2: Personalização baseada em atributos com a API do servidor do Edge Network (obrigatório para atributos de perfil)

>[!IMPORTANT]
>
>**Requisitos de personalização baseados em atributos:** Se você quiser personalizar com base em atributos de perfil (não apenas na associação de público-alvo), **deverá** usar a [API do Edge Network Server](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=pt-BR) com integração autenticada no lado do servidor, independentemente de você também estar usando o Web SDK ou o Mobile SDK para coleta de dados.

* Permite a integração com mecanismos de personalização de terceiros e personalização baseada em CDN.
* A API do Edge Network Server é **necessária** para recuperar com segurança os atributos de perfil para personalização.
* Você pode recuperar atributos de perfil por meio da API do servidor do Edge Network adicionando uma integração do lado do servidor que utiliza o mesmo fluxo de dados que você já está usando para a implementação da Web ou do Mobile SDK.
* Todas as chamadas de API do Edge Network Server para atributos de perfil devem ser feitas em um contexto autenticado para proteger dados confidenciais.
* Esse padrão permite a personalização com base em associação de público-alvo e a personalização com base em atributos.
* Apropriado para casos de uso de personalização no lado do servidor, integrações baseadas em API e cenários que exigem acesso ao atributo de perfil.

## Etapas de implantação

1. [Crie esquemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&lang=pt-BR) para que os dados sejam assimilados.
1. [Crie conjuntos de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) para que os dados sejam assimilados.
1. [Configure as identidades e os namespaces de identidade corretos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR) no esquema para garantir que os dados assimilados possam se unir a um perfil unificado.
1. [Habilite os esquemas e conjuntos de dados para o perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=pt-BR).
1. [Assimile dados](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&lang=pt-BR) na Experience Platform.
1. [Configure as políticas de mesclagem](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=pt-BR) para garantir a identificação de identidade e a mesclagem de perfis corretas.
1. [Configure um fluxo de dados](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=pt-BR) na Coleção de dados da Experience Platform com a configuração de destino habilitada. A sequência de dados determina em qual sequência de dados da Coleção de dados os públicos-alvo serão incluídos na resposta à página.
1. Implemente o [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html) ou o [Mobile SDK](https://developer.adobe.com/client-sdks/home/) nas propriedades da Web e móveis para a coleta de dados.
1. Configure a segmentação de borda para públicos que exigem avaliação em tempo real. [Documentação de segmentação do Edge](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=pt-BR).
1. No catálogo de Destinos, configure o destino [Conexão Personalization Personalizada](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/custom-personalization):
1. [Ative públicos para o destino de personalização de borda](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations). Selecione quais públicos-alvo você deseja ativar para o destino.
1. (Opcional para personalização baseada em atributos) Se você precisar personalizar com base em atributos de perfil além da associação de público-alvo, implemente a [API do Edge Network Server](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=pt-BR) com integração autenticada do lado do servidor usando a mesma sequência de dados. Isto é **necessário** para acessar atributos de perfil.
1. Implemente a lógica de personalização em seu aplicativo da web/móvel para consumir os dados do público-alvo exportados e os atributos do perfil:
   * Se estiver usando Tags na Adobe Experience Platform, use a [funcionalidade de conclusão de evento de envio](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=pt-BR) para acessar a variável `event.destinations` com os dados exportados.
   * Se não estiver usando tags, use [respostas de comando](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/commands/command-responses.html) para analisar a resposta JSON do Adobe Experience Platform e recuperar IDs de público-alvo e atributos de perfil.

## Considerações de implantação

### Considerações de identidade

* Qualquer identidade principal pode ser usada para personalização de borda ao usar o Web SDK ou o SDK móvel com a Edge Network.
* Para a personalização do primeiro logon com dados conhecidos do cliente, a solicitação de personalização deve usar uma identidade principal que corresponda à identidade conhecida do cliente na Real-time Customer Data Platform. Se a ID primária for definida como ECID ou uma identidade anônima que ainda não foi compilada com o perfil de cliente conhecido, levará tempo para que a compilação de identidade seja realizada, o que pode afetar a disponibilidade de dados históricos do perfil para personalização.
* Os perfis do Edge devem ser inicializados antes de serem usados para personalização. Visitantes pela primeira vez ou visitantes recorrentes cujo perfil de borda expirou (TTL de 14 dias) podem experimentar personalização inicial com base em dados de perfil limitados até que o perfil de borda seja totalmente preenchido.

### Personalização baseada em atributos

>[!IMPORTANT]
>
>Os atributos do perfil podem conter dados confidenciais. Para proteger esses dados, você **deve** usar a [API do Edge Network Server](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=pt-BR) ao configurar o destino do Personalization Personalizado para personalização baseada em atributos. Todas as chamadas à API do Edge Network Server devem ser feitas em um contexto autenticado.

* Para personalização baseada em atributos usando atributos de perfil, você deve adicionar uma integração do lado do servidor com a API do Edge Network Server que utiliza o mesmo fluxo de dados que você está usando para a implementação da Web ou do Mobile SDK.
* Você deve configurar quais atributos de perfil incluir na projeção de borda por meio da configuração de destino do Custom Personalization Connection.
* **Somente o Web SDK e o Mobile SDK oferecem suporte à personalização com base na associação de público-alvo**. A API do Edge Network Server é **necessária** para recuperar com segurança os atributos de perfil para personalização.
* Se você não implementar a API do Edge Network Server para acessar atributos, a personalização será baseada somente na associação ao público-alvo.
* A resposta da API para o Personalization personalizado com atributos inclui uma seção `attributes`, além dos segmentos de público-alvo.

### Considerações sobre o público

* Os públicos avaliados por meio de transmissão ou segmentação em lote no hub são projetados para a borda e podem ser usados para personalização.
* Os públicos-alvo que atendem aos critérios de segmentação de borda são avaliados em tempo real na borda para personalização de mesma página.
* Configure os públicos-alvo apropriados para a avaliação de borda com base em seu uso em casos de uso de personalização em tempo real.

## Documentação relacionada

### Configurações de destino

* [Conexão personalizada com o Personalization](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/custom-personalization) - Guia de implementação principal
* [visão geral dos destinos do Personalization](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/overview)
* [Ativar públicos para destinos de personalização de borda](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations)
* [Pesquisar atributos de perfil na borda em tempo real](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-profile-lookup)

### Documentação do SDK

* [Documentação do SDK da Web da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html)
* [Documentação do SDK móvel da Experience Platform](https://developer.adobe.com/client-sdks/home/)
* [Documentação da API do Edge Network Server](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=pt-BR)
* [Documentação de tags da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)
* [Respostas de Comando no Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/commands/command-responses.html)

### Documentação de perfil e segmentação

* Documentação do [[!UICONTROL Perfil de cliente em tempo real]](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html)
* [Medidas de proteção de perfis](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)

### Tutoriais

* [Personalização de próxima ocorrência com Real-Time CDP e Adobe Target](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html)
* [Configuração da sequência de dados](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=pt-BR)
