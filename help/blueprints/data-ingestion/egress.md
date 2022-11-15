---
title: Acesso aos dados e exportação do blueprint
description: Este blueprint fornece uma visão geral de todos os métodos pelos quais os dados podem ser acessados e exportados do Adobe Experience Platform e de aplicativos.
product: adobe experience platform
solution: Experience Platform, Journey Optimizer, Real-time Customer Data Platform, Tags
exl-id: 2ca51a29-2db2-468f-8688-fc8bc061b47b
source-git-commit: c0fe0e94e30351f593e32ea0e6809dd832f976ad
workflow-type: tm+mt
source-wordcount: '1513'
ht-degree: 5%

---

# Acesso aos dados e exportação do blueprint

O Blueprint de acesso e exportação de dados descreve todos os métodos possíveis pelos quais os dados podem ser acessados ou exportados do Adobe Experience Platform e de aplicativos.

O Blueprint é dividido em duas categorias para acesso a dados do Experience Platform e de aplicativos. Em primeiro lugar, abordagens para recolha de dados a partir de Experience Platform e aplicações; isso seria considerado um método do tipo push de saída de dados. Em segundo lugar, abordagens para acesso aos dados do Experience Platform e das aplicações; isso seria considerado um método do tipo pull do acesso aos dados.

Abordagens de acesso a dados

* [API de acesso ao perfil do cliente em tempo real](#rtcp-profile-access-api)
* [API de acesso a dados](#data-access-api)
* [Serviço de consulta](#query-service)

Abordagens da exportação de dados

* [Tags do lado do cliente](#client-side-tags-extensions)
* [Encaminhamento de eventos](#event-forwarding)
* [Destinos do Real-time Customer Data Platform](#RTCDP-destinations)
* [Ações personalizadas do Journey Optimizer](#jo-custom-actions)

## Arquitetura da visão geral do acesso e exportação de dados

<img src="../experience-platform/assets/aep_data_flow.svg" alt="Blueprint de arquitetura de referência para preparação e assimilação de dados" style="width:90%; border:1px solid #4a4a4a" />

## Abordagens para o acesso a dados

### API de acesso ao perfil do cliente em tempo real {#rtcp-profile-access-api}

Os clientes podem acessar perfis únicos unificados na loja de Perfis do cliente em tempo real, incluindo todas as identidades de perfil, associações de público-alvo, atributos e eventos de experiência, usando a API de acesso ao perfil do cliente em tempo real.

Consulte a [API de acesso ao perfil do cliente em tempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html?lang=en) documentação para obter informações adicionais.

#### Casos de uso

* Pesquise um único perfil para adicionar contexto à interação do cliente agente, como interações de suporte por meio de chat e call center ou uma interação de vendas no ponto de venda.
* Permitir contexto adicionado a uma descrição de personalização feita por um sistema externo, por exemplo, um sistema de personalização da Web ou um sistema de decisão de oferta.

#### Considerações

* Perfil do cliente em tempo real [medidas de proteção](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) aplicar.
* Projetado para pesquisa de perfil único de cada vez. Não usado para acesso a perfis em massa ou download de toda a população de perfis para o uso de análise ou ciência de dados.
* O tempo de resposta da pesquisa de perfil é atualizado para as medidas de proteção do perfil. Requisitos de latência baixa em tempo real - por exemplo, para os mesmos requisitos de personalização de página devem utilizar o Perfil de borda do para [Conexão Adobe Target](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=pt-BR) ou [Conexão de personalização personalizada](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en) para acesso a perfil em tempo real no navegador e na personalização do aplicativo.

### API de acesso a dados {#data-access-api}

Usando a API de acesso a dados, os clientes podem acessar diretamente os arquivos brutos do conjunto de dados armazenados no lago de dados do Experience Platform.

* Para obter mais detalhes sobre o uso da API de acesso a dados, consulte o [documentação](https://experienceleague.adobe.com/docs/experience-platform/data-access/home.html?lang=en).

#### Casos de uso

* Puxe arquivos de dados brutos e processados do Experience Platform para armazenamento e avaliação em ambientes corporativos.

#### Considerações

* À medida que os dados são acessados de forma assíncrona em lote, o acesso aos dados será inerentemente latente, em comparação com abordagens de saída de dados de streaming, como Tags de personalização, Encaminhamento de eventos ou Destinos RTCDP.
* Os arquivos de dados, quando processados no Experience Platform, são armazenados como coleções de arquivos em lotes e são compactados e armazenados em formato de parâmetro. Dessa forma, ao acessar e baixar os arquivos em um ambiente diferente, eles devem ser acessados sistematicamente por seu lote e arquivo, em vez de um conjunto de dados inteiro, e qualquer operação nos dados deve contabilizar os arquivos que estão sendo compactados em formato de parâmetro.

### Serviço de consulta {#query-service}

Usando a Experience Platform, os clientes do Serviço de query podem consultar os conjuntos de dados no Experience Platform e manter os resultados da query. Um SQL Client pode ser usado para consultar e manter a resposta da consulta no destino de armazenamento desejado que o cliente SQL pode suportar. A interface do usuário do Serviço de query pode ser usada para armazenar o resultado SQL em um conjunto de dados de target no Experience Platform ou os resultados podem ser salvos no computador local.

* Para obter detalhes adicionais sobre a conexão com clientes SQL para persistir os resultados SQL do Experience Platform Query Service, consulte o seguinte [documentação](https://experienceleague.adobe.com/docs/experience-platform/query/clients/overview.html?lang=en).

#### Casos de uso

* Consultar dados brutos dos conjuntos de dados do Experience Platform e manter os resultados da consulta.
* Consulte o conjunto de dados de instantâneo do perfil para extrair insights sobre o Perfil do cliente em tempo real. [Documentação](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=en#profile-attribute-datasets).
* Armazene os resultados da consulta em um conjunto de dados separado para acesso ou em um conjunto de dados habilitado para perfil que pode ser destacado posteriormente por meio de RTCDP e outros aplicativos do Experience Cloud que acessam o Perfil do cliente em tempo real.

#### Considerações

* À medida que os dados são consultados de forma assíncrona em lote, o acesso aos dados será inerentemente latente, em comparação com abordagens de saída de dados de fluxo, como Tags de personalização, Encaminhamento de eventos ou Destinos RTCDP.
* Somente os dados disponíveis no lago de dados do Experience Platform podem ser consultados usando o Serviço de query. O repositório Perfil do cliente em tempo real, o gráfico de identidade, não pode ser consultado diretamente pelo Serviço de query. Somente quando os conjuntos de dados são exportados para o lago de dados esses conjuntos de dados podem ser consultados, como no exemplo do conjunto de dados do instantâneo de perfil.
* Observe que as medidas de proteção para o número de resultados da consulta e o tempo limite da consulta se aplicam conforme descrito na [Medidas de proteção dos Serviços de Consulta](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=en) documentação.

## Abordagens para a exportação de dados

### Extensões de Tags do lado do cliente {#client-side-tags-extensions}

As extensões podem ser implantadas usando a solução Adobe Tags. Quando uma extensão é implantada, as solicitações de dados são implantadas diretamente em um navegador ou aplicativo do cliente e uma solicitação pode ser invocada para enviar dados e solicitações para o destino desejado.

Consulte a [Visão geral das tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en) documentação para obter informações adicionais.

#### Casos de uso

* Colete informações brutas de transmissão diretamente de ambientes do lado do cliente usando marcação.

#### Considerações

* Não há acesso direto a informações do lado do servidor, como o Perfil do cliente em tempo real do Experience Platform e associações de público-alvo.
* A adição de outras tags de coleta de dados à página pode aumentar o tempo de carregamento da página.
* Capacidade de configurar regras para solicitar dados somente quando determinados critérios forem atendidos.
* Os dados são coletados diretamente do cliente, limitando os tipos de transformações e enriquecimento que podem ser executados antes da coleta dos dados.

### Encaminhamento de eventos {#event-forwarding}

As solicitações de coleta de dados são coletadas diretamente na Rede Adobe Edge. Das solicitações de Rede de borda para endpoints RESTful externos, elas podem ser configuradas para encaminhar essas solicitações para o destino externo.

Consulte o seguinte [Encaminhamento de evento](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=en) documentação para obter informações adicionais.

#### Casas de uso

* Colete informações de transmissão brutas diretamente de ambientes do lado do cliente da empresa de endpoint usando encaminhamento de eventos do lado do servidor Adobe.

#### Considerações

* Para usar o Encaminhamento de eventos, os dados devem ser enviados para a Rede de borda usando o WebSDK ou MobileSDK.
* A abordagem de encaminhamento de eventos reduz o tempo e o peso do carregamento da página devido à adição de tags adicionais na página.
* No momento, não há suporte para enriquecimento do perfil de borda ou de outras fontes de dados.
* Filtragem de dados limitada e transformações de mapeamento simples são compatíveis.

### Destinos do Real-time Customer Data Platform {#RTCDP-destinations}

Os dados de atributo de perfil e de associação de público-alvo podem ser ativados para destinos empresariais e de anúncios. Isso significa que os dados coletados devem ser assimilados no Experience Platform Real-time Customer Profile.

Consulte a [Destinos do Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en) documentação para obter informações adicionais.

#### Casos de uso

* Ative as informações do atributo de perfil, incluindo a associação do público-alvo a armazenamentos de dados internos da empresa, ferramentas de análise, sistemas de email ou sistemas de suporte.
* Ative a associação de público-alvo de perfil a um fornecedor externo de anúncios para direcionar e personalizar o conteúdo para o perfil.

#### Considerações

* Atributos de perfil e associações de público-alvo podem ser ativados. Os eventos de experiência bruta não podem ser ativados no momento como parte dos Destinos RTCDP.
* As ativações ocorrem em streaming ou lote, dependendo da natureza da avaliação do segmento e da natureza do protocolo de ingestão que o destino aceita.

### Ações personalizadas do Journey Optimizer {#jo-custom-actions}

O uso de clientes do Journey Optimizer pode invocar uma ação personalizada da tela de jornada para enviar uma carga ou mensagem para um endpoint da API externa que está configurado. Uma ação pode ser configurada para qualquer serviço de qualquer provedor que possa ser chamado por meio de uma REST API com uma carga útil formatada em JSON. Essa carga útil pode incluir informações do evento, atributos do perfil e dados do evento anterior, transformações e enriquecimentos configurados na jornada.

Consulte a [Ações personalizadas do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html?lang=en) documentação para obter informações adicionais.

#### Casos de uso

* Eventos de ativação do Experience Platform e Journey Optimizer que incluem informações adicionais do Perfil do cliente em tempo real.
* Notificar sistemas externos quando um cliente atingir um ponto específico de uma jornada.

#### Considerações

* Grades de proteção na taxa de transferência suportada por [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=pt-BR) e os enriquecimentos apoiados pela [Perfil do cliente em tempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) aplicar.
* As ações personalizadas podem ser executadas de forma contínua e de uma forma para cada evento ou perfil em uma jornada. Não é possível executar operações em massa ou saídas de dados em massa na forma de arquivos ou solicitações agregadas nas jornadas do cliente.
* Acesso contínuo aos atributos do Perfil do cliente em tempo real e aos eventos de experiência que podem ser incluídos no payload de ativação.
* Os dados do evento podem ser filtrados e transformações de mapeamento simples aplicadas antes de enviar eventos para destinos externos.
