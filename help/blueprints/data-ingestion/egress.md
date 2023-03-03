---
title: Blueprint de acesso e exportação de dados
description: Este blueprint fornece uma visão geral de todos os métodos pelos quais os dados podem ser acessados e exportados da Adobe Experience Platform e dos aplicativos.
product: adobe experience platform
solution: Experience Platform, Journey Optimizer, Real-time Customer Data Platform, Data Collection
exl-id: 2ca51a29-2db2-468f-8688-fc8bc061b47b
source-git-commit: 730b73e56391b8f5ec49a7f570ca32c5cbc65aec
workflow-type: ht
source-wordcount: '1513'
ht-degree: 100%

---

# Blueprint de acesso e exportação de dados

O Blueprint de acesso e exportação de dados descreve todos os métodos possíveis pelos quais os dados podem ser acessados ou exportados da Adobe Experience Platform e dos aplicativos.

O Blueprint é dividido em duas categorias para acesso a dados da Experience Platform e dos aplicativos. Em primeiro lugar, abordagens para obtenção de dados da Experience Platform e dos aplicativos; este seria considerado um método de saída de dados do tipo push. Em segundo lugar, abordagens para acesso aos dados da Experience Platform e dos aplicativos; este seria considerado um método de acesso a dados do tipo pull.

Abordagens de acesso a dados:

* [API de acesso ao perfil do cliente em tempo real](#rtcp-profile-access-api)
* [API de acesso a dados](#data-access-api)
* [Serviço de consulta](#query-service)

Abordagens da exportação de dados:

* [Tags do lado do cliente](#client-side-tags-extensions)
* [Encaminhamento de eventos](#event-forwarding)
* [Destinos da Real-time Customer Data Platform](#RTCDP-destinations)
* [Ações personalizadas do Journey Optimizer](#jo-custom-actions)

## Arquitetura da visão geral de acesso e exportação de dados

<img src="../experience-platform/assets/aep_data_flow.svg" alt="Blueprint de arquitetura de referência para preparação e assimilação de dados" style="width:90%; border:1px solid #4a4a4a; margin-bottom: 15px;" class="modal-image" />

## Abordagens de acesso a dados

### API de acesso ao perfil do cliente em tempo real {#rtcp-profile-access-api}

Os clientes podem acessar perfis únicos unificados no armazenamento de Perfis do cliente em tempo real, incluindo todas as identidades de perfil, associações de público, atributos e eventos de experiência, usando a API de acesso ao perfil do cliente em tempo real.

Consulte a documentação da [API de acesso ao perfil do cliente em tempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html?lang=pt-BR) para obter mais informações.

#### Casos de uso

* Pesquise um perfil para adicionar contexto à interação entre cliente e agente, como interações de suporte por meio de chat e da central de atendimento ou uma interação de venda no ponto de venda.
* Permita maior contexto em uma descrição de personalização feita por um sistema externo, por exemplo, um sistema de personalização da Web ou um sistema de decisão de ofertas.

#### Considerações

* [Medidas de proteção](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR) do perfil do cliente em tempo real se aplicam.
* Projetado para pesquisa de um perfil único por vez. Não usado para acesso a perfis em massa ou para download de toda a população de perfis para fins de análise ou ciência de dados.
* O tempo de resposta da pesquisa de perfil cumpre as medidas de proteção do perfil. Requisitos de baixa latência em tempo real – por exemplo, para personalização na mesma página, os requisitos devem utilizar o perfil de borda da [Conexão do Adobe Target](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=pt-BR) ou da [Conexão de personalização personalizada](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=pt-BR) para acesso ao perfil em tempo real na personalização no navegador e no aplicativo.

### API de acesso a dados {#data-access-api}

Usando a API de acesso a dados, os clientes podem acessar diretamente os arquivos brutos do conjunto de dados armazenado no data lake da Experience Platform.

* Para obter mais informações sobre o uso da API de acesso a dados, consulte a [documentação](https://experienceleague.adobe.com/docs/experience-platform/data-access/home.html?lang=pt-BR).

#### Casos de uso

* Extraia arquivos de dados brutos e processados da Experience Platform para armazenamento e avaliação em ambientes corporativos.

#### Considerações

* À medida que os dados são acessados em um lote de forma assíncrona, o acesso a eles será inerentemente latente, em comparação com abordagens de saída de dados de streaming, como a utilização de Tags, Encaminhamento de eventos ou Destinos RTCDP.
* Os arquivos de dados, quando processados na Experience Platform, são armazenados como conjuntos de arquivos em lotes e são compactados e armazenados em formato parquet. Dessa forma, ao acessar e baixar os arquivos em um ambiente diferente, eles devem ser acessados sistematicamente por lote e arquivo, em vez de todo o conjunto de dados, e qualquer operação nos dados deve considerar os arquivos que estão sendo compactados em formato parquet.

### Serviço de consulta {#query-service}

Usando a Experience Platform, os clientes do Serviço de consulta podem consultar os conjuntos de dados na Experience Platform e manter os resultados da consulta. Um cliente SQL pode ser usado para consultar e manter a resposta da consulta em um destino de armazenamento desejado que seja compatível com o cliente SQL. A interface do usuário do Serviço de consulta pode ser usada para armazenar os resultados de SQL em um conjunto de dados de destino na Experience Platform ou os resultados podem ser salvos no computador local.

* Para obter mais informações sobre a conexão com clientes SQL para manter os resultados de SQL do Serviço de consulta da Experience Platform, consulte esta [documentação](https://experienceleague.adobe.com/docs/experience-platform/query/clients/overview.html?lang=pt-BR).

#### Casos de uso

* Consulte os dados brutos dos conjuntos de dados da Experience Platform e mantenha os resultados da consulta.
* Consulte o conjunto de dados de instantâneo do perfil para obter insights sobre o Perfil do cliente em tempo real. [Documentação](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=pt-BR#profile-attribute-datasets).
* Armazene os resultados da consulta em um conjunto de dados separado para acesso ou em um conjunto de dados habilitado para perfil que pode ser obtido posteriormente por meio da RTCDP e de outros aplicativos da Experience Cloud que acessam o Perfil do cliente em tempo real.

#### Considerações

* À medida que os dados são consultados em um lote de forma assíncrona, o acesso a eles será inerentemente latente, em comparação com abordagens de saída de dados de streaming, como a utilização de Tags, Encaminhamento de eventos ou Destinos RTCDP.
* Somente os dados disponíveis no data lake da Experience Platform podem ser consultados usando o Serviço de consulta. O armazenamento de Perfil do cliente em tempo real, o gráfico de identidade e o Customer Journey Analytics não podem ser consultados diretamente pelo Serviço de consulta. Os conjuntos de dados podem ser consultados somente depois de serem exportados para o data lake, como no exemplo do conjunto de dados de instantâneo de perfil.
* Observe que as medidas de proteção para o número de resultados da consulta e o tempo limite da consulta se aplicam conforme descrito na documentação de [Medidas de proteção dos Serviços de Consulta](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=pt-BR).

## Abordagens para exportação de dados

### Extensões de tags do lado do cliente {#client-side-tags-extensions}

As extensões podem ser implantadas usando a solução Adobe Tags. Quando uma extensão é implantada, as solicitações de dados são implantadas diretamente em um navegador ou aplicativo do cliente e uma solicitação pode ser assimilada para enviar dados e solicitações para o destino desejado.

Consulte a documentação de [Visão geral das tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR) para obter mais informações.

#### Casos de uso

* Colete informações brutas de streaming diretamente dos ambientes do lado do cliente usando tags.

#### Considerações

* Não há acesso direto a informações do lado do servidor, como o Perfil do cliente em tempo real da Experience Platform e as associações de público.
* A adição de tags de coleta de dados à página pode aumentar o tempo de carregamento da página.
* Capacidade de configurar regras para solicitar dados somente quando determinados critérios forem atendidos.
* Os dados são coletados diretamente do cliente, limitando os tipos de transformações e enriquecimento que podem ser executados antes da coleta de dados.

### Encaminhamento de eventos {#event-forwarding}

As solicitações de coleta de dados são coletadas diretamente na Edge Network da Adobe. Na Edge Network, as solicitações para endpoints RESTful externos podem ser configuradas para serem encaminhadas para o destino externo.

Para obter mais informações, consulte a seguinte documentação: [Encaminhamento de eventos](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=pt-BR).

#### Casos de uso

* Colete informações de streaming brutas diretamente de ambientes do lado do cliente para um endpoint empresarial usando o encaminhamento de eventos do lado do servidor da Adobe.

#### Considerações

* Para usar o Encaminhamento de eventos, os dados devem ser enviados para a Edge Network usando SDK da Web ou MobileSDK.
* A abordagem de encaminhamento de eventos reduz o tempo e o peso do carregamento da página devido à adição de tags na página.
* No momento, não há suporte ao enriquecimento do perfil de borda ou de outras fontes de dados.
* Há suporte limitado à filtragem de dados e a transformações de mapeamento simples.

### Destinos da Real-time Customer Data Platform {#RTCDP-destinations}

Os dados de atributo de perfil e de associação de público-alvo podem ser ativados para destinos empresariais e publicitários. Isso significa que os dados obtidos devem ser assimilados no Perfil do cliente em tempo real da Experience Platform.

Consulte a documentação de [Destinos da Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=pt-BR) para obter mais informações.

#### Casos de uso

* Ative as informações do atributo de perfil, incluindo a associação de público-alvo a armazenamentos de dados corporativos internos, ferramentas de análise, sistemas de email ou sistemas de suporte.
* Ative a associação de público-alvo de perfil a um fornecedor externo de publicidade para direcionar e personalizar o conteúdo ao perfil.

#### Considerações

* Atributos de perfil e associações de segmento podem ser ativados. Os eventos de experiência bruta não podem ser ativados no momento como parte dos Destinos da RTCDP.
* As ativações ocorrem por streaming ou em lote, dependendo da natureza da avaliação do segmento e da natureza do protocolo de assimilação aceito pelo destino.

### Ações personalizadas do Journey Optimizer {#jo-custom-actions}

O uso de clientes do Journey Optimizer pode invocar uma ação personalizada da tela de jornada para enviar uma carga ou mensagem para um endpoint da API externa que esteja configurado. Uma ação pode ser configurada para qualquer serviço de qualquer provedor que possa ser chamado por meio de uma API REST com uma carga formatada em JSON. Essa carga pode incluir informações de evento, atributos do perfil e dados de evento anterior, transformações e enriquecimentos configurados na jornada.

Consulte a documentação de [Ações personalizadas do Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html?lang=pt-BR) para obter mais informações.

#### Casos de uso

* Eventos de ativação da Experience Platform e do Journey Optimizer que incluem informações adicionais do Perfil do cliente em tempo real.
* Notificação de sistemas externos quando um cliente atinge um ponto específico de uma jornada.

#### Considerações

* O [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=pt-BR) oferece suporte a medidas de proteção na taxa de transferência e o [Perfil do cliente em tempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR) oferece suporte a enriquecimentos.
* As ações personalizadas podem ser executadas uma a uma por streaming para cada evento ou perfil em uma jornada. Não é possível executar operações em massa ou saídas de dados em massa na forma de arquivos ou solicitações agregadas nas jornadas do cliente.
* Acesso de streaming aos atributos e eventos de experiência do Perfil do cliente em tempo real que podem ser incluídos na carga de ativação.
* Os dados do evento podem ser filtrados e transformações de mapeamento simples podem ser aplicadas antes de enviar eventos para destinos externos.
