---
title: Encaminhamento de eventos
description: Saiba como encaminhar dados de eventos em tempo real coletados por meio do Edge Network para destinos que não sejam da Adobe para análise, armazenamento ou publicidade.
solution: Experience Platform
exl-id: 24964d27-db56-4fa4-a79f-1b6750564b34
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '6342'
ht-degree: 0%

---

# Encaminhamento de eventos

Este guia aborda a implementação do encaminhamento de eventos do lado do servidor usando o Edge Network [!DNL Adobe Experience Platform]. Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam distribuir dados de eventos em tempo real coletados pela Edge Network para destinos que não sejam da Adobe, como plataformas de análise de terceiros, endpoints de armazenamento em nuvem, redes de publicidade ou webhooks personalizados.

Ele apresenta todas as abordagens viáveis para configurar o encaminhamento de eventos, explica as compensações entre elas e oferece links para a documentação do [!DNL Adobe Experience League] para orientação de procedimento detalhada.

## Visão geral do caso de uso

As organizações que coletam dados comportamentais por meio do [!DNL Adobe Experience Platform] Web SDK, Mobile SDK ou API de servidor geralmente precisam compartilhar esse mesmo fluxo de eventos com sistemas que não sejam da Adobe — plataformas de análise como [!DNL Google Analytics] ou [!DNL Snowflake], redes de publicidade para rastreamento de conversão, data warehouses para armazenamento de longo prazo ou serviços internos personalizados. Tradicionalmente, isso exigia a proliferação de tags do lado do cliente, o que aumenta o peso da página, introduz latência e cria riscos de privacidade e governança.

O encaminhamento de eventos resolve isso operando no lado do servidor no Edge Network. Quando uma interação do visitante aciona um evento por meio do Web SDK ou da API do servidor, esse evento é roteado por meio de um fluxo de dados para a Edge Network. As regras de encaminhamento de eventos — configuradas em uma propriedade dedicada de encaminhamento de eventos — avaliam os dados de evento recebidos e os encaminham seletivamente para um ou mais destinos configurados. Essa abordagem do lado do servidor reduz o aumento excessivo de tags do lado do cliente, melhora o desempenho da página, centraliza a governança de dados e fornece à organização controle sobre exatamente quais dados deixam o ecossistema da Adobe.

O público-alvo deste padrão inclui organizações que já implantaram (ou planejam implantar) a API de Servidor ou Web SDK do [!DNL Adobe Experience Platform] para coleta de dados e desejam estender esse investimento distribuindo dados do evento para pontos de extremidade que não sejam da Adobe sem adicionar marcas JavaScript do lado do cliente.

## Principais objetivos de negócios

Os seguintes objetivos de negócios são compatíveis com esse padrão de caso de uso.

### Melhorar a qualidade e a governança dos dados

Garanta dados limpos, completos e em conformidade para a definição precisa de metas, a redução de desperdício e análises confiáveis. O encaminhamento de eventos centraliza a distribuição de dados no lado do servidor, dando à organização um único ponto de controle para quais dados são compartilhados com sistemas externos, reduzindo o risco de vazamento de dados e garantindo que as políticas de governança sejam aplicadas antes que os dados deixem o Edge Network [!DNL Adobe].

**KPIs:** Eficiência, economia

Para obter mais informações, consulte [Melhorar a qualidade e a governança dos dados](../../business-objectives/cost-efficiency/improve-data-quality-governance.md).

### Consolidar e modernizar a tecnologia de marketing

Reduza a fragmentação de ferramentas e o débito técnico migrando para plataformas unificadas e dimensionáveis. O encaminhamento de eventos permite que as organizações substituam várias tags de fornecedor do lado do cliente por um único mecanismo de distribuição de dados do lado do servidor, reduzindo a sobrecarga de carregamento da página e simplificando a pilha de tecnologia.

**KPIs:** Economia, Eficiência, Velocidade de Comercialização

Para obter mais informações, consulte [Consolidar e modernizar a tecnologia de marketing](../../business-objectives/cost-efficiency/consolidate-modernize-marketing-technology.md).

## Exemplo de casos de uso tático

A seguir estão cenários táticos comuns em que esse padrão de caso de uso se aplica.

- **Enriquecimento de análise de terceiros** — Encaminhe eventos de exibição de página, clique e conversão para [!DNL Google Analytics], [!DNL Snowflake] ou outras plataformas de análise em tempo real sem adicionar marcas do lado do cliente
- **Rastreamento de conversão do Advertising** — Envie eventos de compra e de geração de clientes potenciais para a API de conversões [!DNL Meta], [!DNL Google Ads], [!DNL TikTok] ou [!DNL Snap] do lado do servidor para medição e otimização de conversão
- **Transmissão de data warehouse** — Encaminhe dados brutos de evento para um data warehouse de nuvem ([!DNL Google BigQuery], [!DNL Amazon S3], [!DNL Azure Event Hubs]) para armazenamento de longo prazo e análise offline
- **Integração de webhook personalizada** — Encaminhar dados de evento filtrados ou transformados para microsserviços internos, sistemas CRM ou plataformas de parceiros por meio de pontos de extremidade HTTP
- **Redução de tags e melhoria no desempenho da página** — substitua várias tags JavaScript do fornecedor do lado do cliente por uma única implementação do Web SDK, além de regras de encaminhamento de eventos do lado do servidor, reduzindo o peso da página e melhorando o Core Web Vitals
- **Compartilhamento de dados compatível com privacidade** — Aplique a filtragem de dados e as regras de redação em nível de campo no lado do servidor antes de compartilhar dados do evento com terceiros, garantindo que a PII seja removida ou tenha hash antes que atinja sistemas externos
- **Distribuição de eventos de várias nuvens** — Encaminha simultaneamente o mesmo fluxo de eventos para vários destinos (por exemplo, analytics, publicidade e data warehouse) de um único conjunto de regras do lado do servidor
- **Encaminhamento de sinal de fraude em tempo real** — encaminhe eventos de transação de alto valor para sistemas de detecção de fraude para pontuação e alerta de riscos em tempo real

## Indicadores-chave de desempenho

Os KPIs a seguir ajudam a medir o sucesso desse padrão de caso de uso.

- **Redução do tempo de carregamento da página** — melhoria medida na velocidade de carregamento da página e no Core Web Vitals após a migração das tags do lado do cliente para o encaminhamento de eventos do lado do servidor
- **Taxa de êxito de entrega de dados** — Porcentagem de eventos encaminhados com êxito para pontos de extremidade de destino sem erros ou tempos limite
- **Redução da contagem de marcas** — Número de marcas de fornecedor do lado do cliente removidas após a implementação de equivalentes do lado do servidor
- **Atualidade/latência de dados** — Tempo entre a ocorrência do evento no cliente e a chegada do evento ao ponto de extremidade de destino (destino: subsegundos a segundos)
- **Taxa de conformidade de governança** — Porcentagem de compartilhamentos de dados de saída que passam pelas regras de filtragem do lado do servidor, garantindo que nenhum PII ou dado restrito atinja destinos não autorizados
- **Eficiência operacional** — redução no número de horas de desenvolvedores gasto gerenciando implantações de marcas do lado do cliente e solucionando conflitos de marcas

## Padrão do caso de uso

Esta seção descreve o padrão e a cadeia de função usados para implementar o encaminhamento de eventos.

**Encaminhamento de Eventos** — Encaminhe dados de eventos em tempo real coletados via Edge Network para destinos que não sejam da Adobe para fins de análise, armazenamento ou publicidade.

**Cadeia De Funções:** Configuração De Sequência De Dados > Definição De Regra De Evento > Mapeamento De Destino > Execução De Encaminhamento > Monitoramento

## Aplicativos

Os aplicativos a seguir são usados neste padrão de caso de uso.

- **[!DNL Adobe Experience Platform](Edge Network)** — Recebe e roteia dados de eventos em tempo real do Web SDK, Mobile SDK ou API de servidor por meio de sequências de dados configuradas
- **[!DNL Adobe Experience Platform](Encaminhamento de Eventos)** — Fornece o mecanismo de regras do lado do servidor para avaliação, filtragem, transformação e encaminhamento de dados de eventos para destinos externos
- **[!DNL Adobe Experience Platform](Marcas/Coleção de Dados)** — Gerencia o ciclo de vida, as extensões, as regras e o fluxo de trabalho de publicação da propriedade de encaminhamento de eventos

## Funções básicas

Os seguintes recursos básicos devem estar em vigor para esse padrão de caso de uso. Para cada função, o status indica se ele é tipicamente necessário, se presume ser pré-configurado ou se não é aplicável.

| Função de base | Status | O que deve estar em vigor | Referência do Experience League |
| --- | --- | --- | --- |
| Administração e governança | Obrigatório | Uma sandbox deve estar ativa com funções e permissões de usuário apropriadas configuradas. Os usuários que gerenciam o encaminhamento de eventos precisam de permissões de Coleta de Dados no [!DNL Adobe Admin Console], incluindo direitos para gerenciar propriedades, extensões e regras de encaminhamento de eventos. | [Visão geral do controle de acesso](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Preparação e modelagem de dados | Obrigatório | Os esquemas XDM devem ser definidos para os dados do evento que fluem pela Edge Network. O fluxo de dados deve fazer referência a um esquema XDM ExperienceEvent válido para que as regras de encaminhamento de eventos possam acessar campos estruturados para filtragem, transformação e mapeamento. | [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home) |
| Fontes de dados e coleção | Obrigatório | Um mecanismo de coleta de dados deve estar ativo — Web SDK, Mobile SDK ou API do Edge Network Server — enviando eventos por meio de um fluxo de dados configurado. A sequência de dados é a camada de roteamento fundamental que conecta a coleção do lado do cliente ao encaminhamento de eventos do lado do servidor. | [Configurar sequências de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure) |
| Configuração de identidade e perfil | Não se aplica | O encaminhamento de eventos opera em dados de evento brutos na camada do Edge Network, antes da resolução de identidade ou unificação de perfil ocorrer. Os namespaces de identidade e as políticas de mesclagem não são necessários, a menos que os eventos encaminhados também precisem contribuir para o Perfil do cliente em tempo real (que é uma configuração de serviço de sequência de dados separada, não uma preocupação de encaminhamento de eventos). | |
| Definição e segmentação do público-alvo | Não se aplica | O encaminhamento de eventos processa eventos individuais em tempo real e não avalia a associação de público-alvo. A filtragem com base no público-alvo não faz parte da cadeia de funções de encaminhamento de eventos. Se a ativação baseada no público-alvo for necessária, consulte o plano de referência Audience Activation para destinos. | |

## Funções de suporte

Os recursos a seguir aumentam esse padrão de caso de uso, mas não são necessários para a execução principal.

| Função de suporte | Status | Por que é importante | Referência do Experience League |
| --- | --- | --- | --- |
| Criação de atributo calculado/derivado | Não se aplica | O encaminhamento de eventos opera em dados brutos de eventos, não em atributos computados no nível do perfil. Os atributos computados não estão disponíveis no contexto de encaminhamento de eventos. | |
| Gerenciamento do ciclo de vida dos dados | Recomendado | Se os dados do evento também estiverem sendo assimilados nos conjuntos de dados da AEP (por meio do mesmo fluxo de dados), as políticas de retenção de dados (expiração) deverão ser configuradas para esses conjuntos de dados para gerenciar os custos de armazenamento e a conformidade normativa. O encaminhamento de eventos em si não armazena dados, mas o caminho de assimilação paralelo do AEP armazena. | [Visão geral do Gerenciamento Avançado do Ciclo de Vida dos Dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| Rotulagem e aplicação de uso de dados | Recomendado | Embora as regras de encaminhamento de eventos forneçam filtragem em nível de campo (permitindo excluir dados confidenciais de cargas úteis encaminhadas), a aplicação de rótulos de uso de dados aos esquemas e conjuntos de dados subjacentes garante que as políticas de governança sejam aplicadas se os mesmos dados forem usados para ativação ou personalização de público-alvo. | [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| Monitoramento e capacidade de observação | Incluído | O monitoramento é essencial para o encaminhamento de eventos. O painel de Monitoramento de encaminhamento de eventos oferece visibilidade sobre taxas de sucesso de encaminhamento, taxas de erro e códigos de resposta de destino. Os alertas devem ser configurados para falhas de destino. | [Monitoramento do encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/monitoring) |
| Relatórios e análise | Recomendado | Se os eventos encaminhados alimentarem uma plataforma de análise de terceiros, considere conectar os mesmos conjuntos de dados de eventos do AEP à CJA para obter uma visualização unificada entre canais. Isso permite a comparação entre as análises do Adobe e de terceiros. | [visão geral do CJA](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## Funções do aplicativo

Este plano exerce as seguintes funções do Catálogo de Funções da Aplicação. As funções são mapeadas para fases de implementação em vez de etapas numeradas.

### [!DNL Adobe Experience Platform] (AEP)

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Configuração da sequência de dados | Fase 1: configuração da sequência de dados | Configure um fluxo de dados para receber eventos do Edge Network e habilitar o serviço de encaminhamento de eventos |
| Configuração da propriedade de encaminhamento de eventos | Fase 2: propriedade e extensões do encaminhamento de eventos | Criar uma propriedade de encaminhamento de eventos e instalar extensões específicas de destino |
| Definição da regra de evento | Fase 3: Definição da regra de evento | Defina regras que avaliam os dados de entrada do evento e determinam o que encaminhar e onde |
| Mapeamento de destinos | Fase 3: Definição da regra de evento | Mapear elementos de dados do evento para formatos de carga útil específicos do destino nas regras de encaminhamento |
| Execução de encaminhamento | Fase 4: Publicação e ativação | Publique a configuração do encaminhamento de eventos na Edge Network para execução em tempo real |
| Monitoramento | Fase 5: monitoramento e validação | Monitorar taxas de sucesso de encaminhamento, códigos de erro e integridade de destino |

## Pré-requisitos

Verifique se os itens a seguir estão em vigor antes de iniciar a implementação.

- [ ] [!DNL Adobe Experience Platform] licença com direito à Edge Network e ao Encaminhamento de Eventos
- [ ] Permissões de coleção de dados configuradas em [!DNL Adobe Admin Console] (gerencie propriedades, extensões, regras e publicações para encaminhamento de eventos)
- [ ] Pelo menos um mecanismo de coleta de dados ativo (Web SDK, Mobile SDK ou API de servidor) enviando eventos por meio de uma sequência de dados
- [ ] esquema XDM ExperienceEvent definido para os dados do evento que estão sendo coletados
- [ ] Sequência de dados criada e vinculada ao mecanismo de coleta
- [ ] Credenciais de ponto de extremidade de destino e documentação disponíveis (por exemplo, [!DNL Meta] Token de acesso da API de conversões, [!DNL Google Analytics] ID de medição, URL do webhook, credenciais de armazenamento na nuvem)
- [ ] Noções básicas sobre o modelo de dados de evento e quais campos/eventos cada destino requer

## Opções de implementação

Esta seção descreve as abordagens disponíveis para implementar o encaminhamento de eventos e fornece orientação sobre a escolha da opção correta.

### Opção A: encaminhamento de eventos com base em extensão

**Recomendado para:** Equipes que usam plataformas de destino com suporte adequado ([!DNL Meta], [!DNL Google], [!DNL AWS], [!DNL Azure], [!DNL Snowflake], etc.) que têm extensões de encaminhamento de eventos pré-criadas disponíveis no catálogo Coleção de dados.

**Como funciona:**

O encaminhamento de eventos baseado em extensão aproveita integrações pré-criadas mantidas pela Adobe ou por parceiros de terceiros. Cada extensão é criada para um destino específico e lida com autenticação, formatação de carga útil e comunicação de ponto de extremidade. O implementador instala a extensão na propriedade de encaminhamento de eventos, configura credenciais de autenticação e cria regras que mapeiam elementos de dados XDM para os campos de ação da extensão.

Essa abordagem minimiza o desenvolvimento personalizado, pois a extensão abstrai os requisitos da API do destino. Por exemplo, a extensão de API de conversões [!DNL Meta] traduz eventos de comércio XDM no formato esperado [!DNL Meta], lidando com hash de campos PII, parâmetros de desduplicação e gerenciamento de token de acesso. Da mesma forma, as extensões [!DNL Google Cloud Platform] ou [!DNL AWS] lidam com autenticação e formatação de carga para seus respectivos serviços de nuvem.

A compensação é que a disponibilidade da extensão determina quais destinos são compatíveis. Se não houver extensão para um destino, a Opção B (Webhook personalizado) deverá ser usada.

**Principais considerações:**

- A disponibilidade da extensão varia — verifique o [catálogo de extensões da Coleção de Dados](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/overview) antes do planejamento
- As extensões são mantidas pela Adobe ou por parceiros; as atualizações podem introduzir alterações importantes que exigem ajustes de regras
- Algumas extensões oferecem suporte somente a tipos de evento específicos ou exigem mapeamentos de campo XDM específicos
- As extensões tratam da autenticação e do gerenciamento de credenciais em sua interface do usuário de configuração

**Vantagens:**

- Implementação mais rápida para destinos compatíveis
- A formatação de carga pré-criada reduz os erros de mapeamento
- Gerenciamento de autenticação e credencial manipulado pela extensão
- Mantido e atualizado pela Adobe ou por parceiros certificados
- Código personalizado reduzido e menor carga de manutenção

**Limitações:**

- Limitado a destinos com extensões disponíveis
- Menos flexibilidade na personalização de payload em comparação aos webhooks personalizados
- Atualizações de extensão podem exigir reconfiguração de regra
- Algumas extensões podem não suportar todos os recursos da API de destino

**Experience League:**

- [Catálogo de extensões do encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/overview)
- [Extensão da API de conversões do Meta](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/meta/overview)
- [Extensão da Google Cloud Platform](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/google-cloud-platform/overview)
- [Extensão do AWS](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/aws/overview)
- [Extensão do Snowflake](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/snowflake/overview)

### Opção B: encaminhamento de eventos de webhook personalizado (Buscar API)

**Recomendado para:** equipes que precisam encaminhar eventos para destinos sem uma extensão pré-criada ou que exigem controle total sobre a carga, os cabeçalhos e o mecanismo de autenticação da solicitação HTTP.

**Como funciona:**

O encaminhamento de eventos baseado em webhook personalizado usa a extensão [!DNL Adobe Cloud Connector] (incluída por padrão) para fazer solicitações HTTP arbitrárias para qualquer ponto de extremidade. O implementador define elementos de dados para extrair e transformar valores do evento XDM de entrada e configura uma ação de regra usando o tipo de ação &quot;Fazer chamada de busca&quot; do Cloud Connector. Essa ação permite o controle total do método HTTP, URL, cabeçalhos e corpo da solicitação.

O corpo da solicitação geralmente é construído usando elementos de dados e código personalizado para formatar o payload de acordo com a especificação da API do destino. Essa abordagem é compatível com qualquer endpoint acessível por HTTP — APIs REST, webhooks, funções de nuvem ou serviços internos — tornando-o a opção mais flexível.

A solução de compromisso é um maior esforço de implementação e manutenção contínua. O implementador deve entender a API de destino, manipular a autenticação manualmente (por exemplo, definir cabeçalhos de autorização, gerenciar a atualização de token) e manter o formato do payload se a API de destino evoluir.

**Principais considerações:**

- Requer compreensão da especificação da API de destino (método HTTP, estrutura de URL, formato de carga útil, autenticação)
- As credenciais de autenticação devem ser gerenciadas manualmente em elementos de dados ou segredos
- O código personalizado pode ser necessário para transformação da carga (hash, codificação, reestruturação)
- Não há atualizações automáticas quando a API de destino é alterada — manutenção manual necessária
- O recurso Segredos na Coleção de dados pode armazenar com segurança chaves e tokens de API

**Vantagens:**

- Suporta qualquer terminal acessível por HTTP — sem dependência de extensão
- Controle total sobre carga, cabeçalhos e autenticação da solicitação
- Pode encaminhar para serviços internos, APIs personalizadas ou plataformas de nicho
- Permite transformações complexas de conteúdo usando código personalizado
- Pode implementar lógica de repetição e tratamento de erros no código personalizado

**Limitações:**

- Maior esforço de implementação inicial
- Responsabilidade de manutenção contínua do formato e da autenticação da carga útil
- Nenhum tratamento de erros ou rotação de credenciais pré-criados — devem ser implementados manualmente
- Requer conhecimento do desenvolvedor em protocolos HTTP e especificações da API de destino

**Experience League:**

- [Extensão do Adobe Cloud Connector](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/cloud-connector/overview)
- [Segredos do encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/secrets)

### Opção C: Híbrido (extensões + webhooks personalizados)

**Recomendado para:** organizações que encaminham eventos para vários destinos em que algumas têm extensões pré-criadas e outras exigem integração personalizada.

**Como funciona:**

A abordagem híbrida combina o encaminhamento com base em extensão para destinos compatíveis com ações de webhook personalizadas para destinos que não têm extensões. Uma única propriedade de encaminhamento de eventos contém várias regras, algumas usando ações de extensão (por exemplo, [!DNL Meta] Extensão da API de conversões para rastreamento de conversão de publicidade) e outras usando ações de busca do Cloud Connector (por exemplo, encaminhamento para um ponto de extremidade interno do data lake).

Essa abordagem maximiza a cobertura, minimizando o desenvolvimento personalizado desnecessário. Cada regra opera de forma independente, de modo que as regras baseadas em extensão se beneficiam da formatação de carga pré-criada, enquanto as regras personalizadas mantêm flexibilidade total.

**Principais considerações:**

- A complexidade da propriedade aumenta com o número de regras e destinos
- O teste e a depuração podem exigir abordagens diferentes para regras baseadas em extensão em comparação com regras personalizadas
- A publicação de alterações afeta todas as regras na propriedade — use bibliotecas e ambientes para preparar alterações com segurança
- Considere organizar regras com convenções de nomenclatura claras para distinguir ações personalizadas das baseadas em extensão

**Vantagens:**

- Melhor cobertura em diferentes tipos de destino
- Aproveita extensões pré-criadas onde estão disponíveis, reduzindo o esforço
- Mantém flexibilidade para destinos personalizados
- A propriedade de encaminhamento de eventos únicos gerencia toda a lógica de encaminhamento

**Limitações:**

- Maior complexidade de propriedade com vários tipos de regras
- Modelo de manutenção mista — algumas regras são atualizadas automaticamente por meio de extensões, outras exigem manutenção manual
- A depuração requer familiaridade com configurações de extensão e padrões de chamada de busca personalizada

**Experience League:**

- [Visão geral do encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview)
- [Introdução ao encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started)

### Comparação de opções

A tabela a seguir compara as três opções de implementação.

| Critérios | Opção A: Com Base Em Extensão | Opção B: Webhook personalizado | Opção C: híbrido |
| --- | --- | --- | --- |
| Melhor para | Destinos com suporte ([!DNL Meta], [!DNL Google], [!DNL AWS] etc.) | Endpoints personalizados, plataformas de nicho, serviços internos | Vários destinos com suporte misto |
| Complexo | Baixa | Medium-Alto | Médio |
| Tempo de implementação | Dias | Dias-Semanas | Varia de acordo com a combinação de destinos |
| Flexibilidade | Limitado aos recursos de extensão | Controle total | Controle total onde necessário |
| Manutenção | Baixo (gerenciado por extensão) | Alta (manutenção manual) | Misto |
| Exige | Extensão disponível para destino | Documentação da API de destino | Ambos, dependendo do destino |
| É necessário um código personalizado | Mínimo | Moderado-significativo | Varia |

### Escolha a opção certa

Comece inventariando os destinos e verificando se existem extensões de encaminhamento de eventos pré-criadas para cada um.

1. **Se todos os destinos tiverem extensões** — Escolha a Opção A. Isso proporciona a implementação mais rápida com a menor carga de manutenção. As extensões lidam com autenticação, formatação de carga e gerenciamento de versão da API.

2. **Se nenhum destino tiver extensões ou se você precisar de controle total de conteúdo** — Escolha a Opção B. Use a extensão Cloud Connector para fazer solicitações HTTP personalizadas para qualquer endpoint. Essa também é a escolha certa quando você precisa aplicar transformações complexas, hash personalizado ou enviar para serviços internos.

3. **Se você tiver uma combinação de destinos com e sem suporte** — Escolha a Opção C. Use extensões para plataformas como [!DNL Meta], [!DNL Google] e [!DNL AWS], e webhooks personalizados para todo o resto. Este é o cenário de produção mais comum para organizações com diversas análises e pilhas de publicidade.

## Fases de implementação

As fases a seguir descrevem o processo completo de implementação do encaminhamento de eventos.

### Fase 1: configuração da sequência de dados

**Função do Aplicativo:** AEP: Configuração de Sequência de Dados

**O que você configurará:** uma sequência de dados que recebe eventos da sua implementação do Web SDK, Mobile SDK ou API de servidor e os encaminha para a Edge Network, onde as regras de encaminhamento de eventos podem processá-los. Se o encaminhamento de eventos estiver sendo adicionado a uma implantação de coleção de dados existente, você ativará o encaminhamento de eventos no fluxo de dados existente.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: nova sequência de dados vs. sequência de dados existente**
>
>Você deve criar uma nova sequência de dados para o encaminhamento de eventos ou habilitar o encaminhamento de eventos em uma sequência de dados existente?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Usar sequência de dados existente | Você já tem o Web SDK ou a API do servidor enviando eventos por meio de uma sequência de dados | Cenário mais comum; o encaminhamento de eventos é simplesmente habilitado como um serviço adicional no fluxo de dados. Não são necessárias alterações no lado do cliente. |
>| Criar novo fluxo de dados | Essa é uma implementação de greenfield sem coleta de dados existente ou você precisa de um fluxo de dados separado para tipos de evento específicos | Exige a configuração do SDK do lado do cliente para apontar para a nova ID de sequência de dados. Permite configuração isolada. |

>[!NOTE]
>
>**Decisão: quais serviços da AEP habilitar junto com o encaminhamento de eventos**
>
>O fluxo de dados pode rotear eventos para vários serviços da AEP simultaneamente. O encaminhamento de eventos é um serviço; outros (assimilação de dados AEP, [!DNL Target], [!DNL Analytics]) podem ser executados em paralelo.
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Somente encaminhamento de eventos | Você só precisa encaminhar eventos para destinos que não sejam da Adobe e não precisa dos dados nos conjuntos de dados do AEP | Minimiza os custos de processamento de dados. Os eventos fluem pela Edge Network para regras de encaminhamento, mas não são assimilados no data lake da AEP. |
>| Encaminhamento de eventos + assimilação de AEP | Você precisa dos mesmos eventos no AEP (para perfis, públicos, jornadas) e encaminhados para sistemas externos | Mais comum para organizações que usam [!DNL RT-CDP] ou [!DNL AJO] com análises de terceiros. A sequência de dados envia eventos para os conjuntos de dados da AEP e para as regras de encaminhamento de eventos. |
>| Encaminhamento de eventos + vários serviços da Adobe | Você precisa que os eventos sejam roteados para o AEP, [!DNL Target], [!DNL Analytics], e destinos externos simultaneamente | Habilite todos os serviços necessários na sequência de dados. Cada serviço recebe o evento independentemente. |

Navegação da **UI:** [!DNL Experience Platform] > Coleção de dados > Fluxos de dados > Selecionar ou criar fluxo de dados

**Detalhes de configuração da chave:**

- A sequência de dados deve ter o encaminhamento de eventos habilitado em suas Configurações avançadas ou na configuração do serviço
- Vincule a propriedade de encaminhamento de eventos (criada na Fase 2) ao fluxo de dados
- Confirme se o esquema XDM atribuído ao fluxo de dados corresponde à estrutura de eventos enviada pelo mecanismo de coleção

**Documentação do Experience League:**

- [Configurar sequências de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Visão geral dos fluxos de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview)
- [Visão geral do encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview)

### Fase 2: propriedade e extensões do encaminhamento de eventos

**Função do Aplicativo:** AEP: Instalação da Propriedade de Encaminhamento de Eventos

**O que você configurará:** uma propriedade de encaminhamento de eventos na interface da Coleção de Dados, juntamente com as extensões necessárias para os destinos de destino. A propriedade de encaminhamento de eventos é o container de todas as regras, elementos de dados e extensões que definem a lógica de encaminhamento do lado do servidor.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: uma única propriedade vs. várias propriedades**
>
>Você deve usar uma propriedade de encaminhamento de eventos para todos os destinos ou propriedades separadas?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Propriedade única | A maioria das implementações; todas as regras de encaminhamento compartilham o mesmo fluxo de eventos | Mais simples de gerenciar, fluxo de trabalho de publicação único, todas as regras são avaliadas em relação a cada evento. Use as condições da regra para filtrar quais eventos direcionam para quais destinos. |
>| Várias propriedades | Você precisa de equipes diferentes para gerenciar integrações de destino diferentes de maneira independente ou tem requisitos rigorosos de isolamento de ambiente | Cada propriedade tem seu próprio fluxo de trabalho de publicação e pode ser vinculada a fluxos de dados diferentes. Aumenta a sobrecarga do gerenciamento, mas melhora os limites de controle de acesso. |

>[!NOTE]
>
>**Decisão: quais extensões instalar**
>
>Selecione extensões com base nos destinos e na opção de implementação escolhida (A, B ou C da parte superior).
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Extensões específicas de destino ([!DNL Meta], [!DNL Google], [!DNL AWS] etc.) | O destino tem uma extensão pré-criada e você deseja configuração personalizada mínima (Opção A ou C) | Cada extensão exige credenciais específicas de destino (tokens de API, IDs de medição, IDs de conta). Consulte a documentação da extensão para ver os tipos de evento compatíveis e os campos obrigatórios. |
>| Somente extensão do Cloud Connector | Todos os destinos usarão solicitações HTTP personalizadas (Opção B) | A extensão Cloud Connector é instalada por padrão. Use o recurso Segredos para armazenar com segurança as chaves de API e os tokens de autenticação. |
>| Específico ao destino e Conector de nuvem | Você tem uma combinação de destinos compatíveis e personalizados (Opção C) | Instale extensões específicas para destinos com suporte e use o Cloud Connector para o restante. |

Navegação da **UI:** [!DNL Experience Platform] > Coleção de dados > Encaminhamento de eventos > Criar propriedade (ou selecionar existente)

**Detalhes de configuração da chave:**

- Nomeie a propriedade com uma convenção clara (por exemplo, &quot;Encaminhamento de evento - Produção&quot; ou &quot;EF - Analytics &amp; Advertising&quot;)
- Instalar a extensão [!DNL Adobe Cloud Connector] (incluída por padrão para ações de webhook personalizadas)
- Instalar extensões específicas do destino e configurar suas credenciais
- Use o recurso Segredos (Coleção de dados > Encaminhamento de eventos > Segredos) para armazenar com segurança as chaves, os tokens e as credenciais da API
- Configurar ambientes (desenvolvimento, armazenamento temporário, produção) para fluxos de trabalho de publicação seguros

**Documentação do Experience League:**

- [Introdução ao encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started)
- [Catálogo de extensões do encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/overview)
- [Segredos do encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/secrets)
- [Extensão do Adobe Cloud Connector](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/cloud-connector/overview)

### Fase 3: definição da regra de evento

**Função do Aplicativo:** AEP: Definição de Regra de Evento, AEP: Mapeamento de Destino

**O que você configurará:** Regras que avaliam os dados de entrada do evento, aplicam condições para filtrar quais eventos devem ser encaminhados e definem ações que enviam os dados para pontos de extremidade de destino. Cada regra consiste em condições (quando acionar) e ações (o que fazer). Os elementos de dados extraem e transformam valores da carga do evento XDM para usar em condições de regra e configurações de ação.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: estratégia de filtragem de eventos**
>
>Como você deve determinar quais eventos são encaminhados para cada destino?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Encaminhar todos os eventos | O destino precisa de um fluxo de eventos completo (por exemplo, data warehouse para armazenamento de eventos brutos) | Configuração mais simples — nenhuma condição necessária. Alto volume de dados no destino. Considere os limites de custo e taxa de destino. |
>| Filtrar por tipo de evento | Destinos diferentes precisam de tipos de evento diferentes (por exemplo, compras para publicidade, exibições de página para análises) | Use condições baseadas em `arc.event.xdm.eventType` ou campos XDM semelhantes. Reduz dados desnecessários no destino. |
>| Filtrar por atributos de evento | Somente eventos específicos que atendam a determinados critérios devem ser encaminhados (por exemplo, compras acima de um limite, eventos de caminhos de página específicos) | Use valores de elementos de dados em condições de regra. Mais complexo, mas reduz o ruído no destino. |

>[!NOTE]
>
>**Decisão: abordagem de transformação de dados**
>
>Como os dados do evento XDM devem ser transformados para a carga útil de destino?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Mapeamento de campo XDM direto por meio de elementos de dados | Os campos de destino são mapeados perfeitamente para campos XDM (comum com o encaminhamento baseado em extensão) | Crie elementos de dados que fazem referência a caminhos XDM (por exemplo, `arc.event.xdm.commerce.order.priceTotal`). As extensões geralmente fornecem uma interface de mapeamento. |
>| Transformação de código personalizado | O destino requer um formato de carga significativamente diferente do XDM, ou os campos precisam de hash, concatenação ou reestruturação | Use elementos de dados de código personalizado ou código personalizado em nível de ação para transformar a carga. Mais flexível, mas mais difícil de manter. |
>| Combinação de elementos de dados e código personalizado | Alguns campos são mapeados diretamente, enquanto outros precisam de transformação | Use elementos de dados para mapeamentos simples e blocos de código personalizados para transformações complexas. Capacidade de manutenção equilibrada com flexibilidade. |

>[!NOTE]
>
>**Decisão: tratamento de PII em dados encaminhados**
>
>Como as informações de identificação pessoal devem ser tratadas antes do encaminhamento?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Excluir campos PII completamente | O destino não precisa de PII e as políticas de governança restringem o compartilhamento | Configure regras para omitir campos PII da carga útil encaminhada. Abordagem mais simples para conformidade com a privacidade. |
>| Campos PII de hash antes do encaminhamento | O destino requer identificadores com hash (por exemplo, [!DNL Meta] requer email com hash SHA -256 para API de Conversões) | Use elementos de dados de código personalizado para aplicar hash SHA-256. Algumas extensões lidam com o hash automaticamente. |
>| Encaminhar PII com base contratual | O destino tem um contrato de processamento de dados e a base legal existe para compartilhar PII | Garantir que os rótulos de uso de dados e as políticas de governança (S3) permitam o compartilhamento. Documente a base legal. |

Navegação da **UI:** [!DNL Experience Platform] > Coleção de dados > Encaminhamento de eventos > Selecionar propriedade > Elementos de dados / Regras

**Detalhes de configuração da chave:**

- **Os elementos de dados** fazem referência ao evento XDM de entrada usando o prefixo de caminho `arc.event.xdm.` (por exemplo, `arc.event.xdm.web.webPageDetails.URL` para a URL da página)
- **As condições da regra** avaliam os valores dos elementos de dados para determinar se a regra deve ser acionada
- **As ações de regra** usam ações específicas de extensão (para a Opção A) ou ações &quot;Fazer chamada de busca&quot; do Cloud Connector (para a Opção B) para enviar dados aos destinos
- Cada regra pode ter várias ações, permitindo que um único evento seja encaminhado a vários destinos
- Use a ordenação de regras para controlar a sequência da avaliação quando várias regras puderem ser acionadas para o mesmo evento
- Teste as regras completamente no ambiente de desenvolvimento antes de publicar na produção

**Onde as opções divergem:**

**Para Opção A (Baseada Em Extensão):**

Configure as ações da regra usando os tipos de ação pré-criados da extensão de destino. Por exemplo, a extensão de API de conversões [!DNL Meta] fornece uma ação &quot;Enviar evento&quot; em que você mapeia campos XDM para [!DNL Meta] parâmetros de evento (event_name, event_time, user_data, custom_data). A extensão lida com a formatação de carga, hash e comunicação da API.

**Para Opção B (Webhook Personalizado):**

Configure as ações de regra usando a ação &quot;Fazer chamada de busca&quot; da extensão Cloud Connector. Especifique o URL de destino, o método HTTP (normalmente POST), os cabeçalhos de solicitação (incluindo Autorização) e crie o corpo da solicitação usando elementos de dados e/ou código personalizado. Você é responsável por fazer a correspondência exata do formato de conteúdo esperado da API de destino.

**Para Opção C (Híbrida):**

Crie regras separadas para cada destino. As regras baseadas em extensão usam os tipos de ação da extensão; as regras personalizadas usam chamadas de busca do Cloud Connector. Todas as regras coexistem na mesma propriedade e são avaliadas independentemente em relação a cada evento recebido.

**Documentação do Experience League:**

- [Regras de encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview)
- [Elementos de dados no encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/data-elements)
- [Regras na coleção de dados](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules)
- [Extensão do Adobe Cloud Connector](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/cloud-connector/overview)

### Fase 4: publicação e ativação

**Função do Aplicativo:** AEP: Execução de Encaminhamento

**O que você configurará:** o fluxo de trabalho de publicação que promove suas regras de encaminhamento de eventos do Desenvolvimento ao Preparo para Produção. O encaminhamento de eventos usa o mesmo modelo de publicação baseado em biblioteca que as tags, com ambientes e artefatos de build que controlam qual configuração está ativa no Edge Network.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: rigor do fluxo de trabalho de publicação**
>
>Quão rigoroso deve ser o processo de publicação?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Direto para Produção (Desenvolvimento > Produção) | Pequenas equipes, destinos de baixo risco ou implementações de prova de conceito | Implantação mais rápida, mas maior risco de problemas de produção. Adequado para testes iniciais com destinos não críticos. |
>| Progressão completa do ambiente (Desenvolvimento > Preparo > Produção) | Implementações de produção com destinos críticos (plataformas de publicidade, data warehouses) | Recomendado para todos os casos de uso de produção. O armazenamento temporário permite a validação com tráfego real antes da implantação de produção. |

Navegação da **UI:** [!DNL Experience Platform] > Coleta de Dados > Encaminhamento de Eventos > Selecionar Propriedade > Fluxo de Publicação

**Detalhes de configuração da chave:**

- Crie uma biblioteca contendo todas as regras, elementos de dados e configurações de extensão para publicar
- Primeiro, crie e teste o ambiente de desenvolvimento usando a ferramenta de monitoramento do encaminhamento de eventos para verificar se os eventos estão sendo encaminhados corretamente
- Promover para preparo para validação de pré-produção com tráfego ativo
- Publicar na produção somente após confirmar a entrega bem-sucedida do evento no ambiente de preparo
- Usar o controle de versão da biblioteca para rastrear alterações e ativar a reversão se necessário

**Documentação do Experience League:**

- [Visão geral da publicação](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/overview)
- [Bibliotecas](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/libraries)
- [Ambientes](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/environments)
- [Builds](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/builds)

### Fase 5: Monitoramento e validação

**Função do aplicativo:** AEP: monitoramento

**O que você configurará:** Os painéis de monitoramento e os processos de validação para confirmar eventos estão sendo encaminhados com êxito, diagnosticam falhas e mantêm a integridade operacional da implantação do encaminhamento de eventos.

**Pontos de decisão nesta fase:**

>[!NOTE]
>
>**Decisão: profundidade do monitoramento**
>
>Com que profundidade o encaminhamento de eventos deve ser monitorado?
>
>| Opção | Quando escolher | Considerações |
>| --- | --- | --- |
>| Painel de monitoramento do encaminhamento de eventos somente | Monitoramento básico para destinos não críticos ou implantações iniciais | Fornece uma visão geral das taxas de sucesso/falha do encaminhamento e dos códigos de resposta de destino. Suficiente para a maioria das implementações. |
>| Monitoramento de encaminhamento de eventos + validação do lado do destino | Destinos críticos em que a integridade dos dados afeta diretamente os resultados dos negócios (rastreamento de conversão de publicidade, integridade do data warehouse) | Faça referência cruzada das métricas de encaminhamento pelo lado do Adobe com a confirmação de recebimento do lado do destino. Captura casos de borda em que o destino aceita a solicitação, mas não processa os dados. |
>| Pilha de observabilidade completa (Monitoramento de encaminhamento de eventos + validação de destino + Alertas do AEP) | Implantações em escala corporativa com requisitos do SLA sobre entrega de dados | Combine o monitoramento do encaminhamento de eventos com alertas da plataforma AEP para obter uma visualização abrangente. Configure notificações de alerta para limites de falha de encaminhamento. |

Navegação da **UI:** [!DNL Experience Platform] > Coleta de Dados > Encaminhamento de Eventos > Selecionar Propriedade > Monitoramento

**Detalhes de configuração da chave:**

- A ferramenta de Monitoramento de encaminhamento de eventos mostra o volume do evento, as taxas de sucesso e os detalhes de erros por regra e por destino
- Monitorar códigos de resposta HTTP de destinos — 2xx indica sucesso, 4xx indica erros de cliente (provavelmente problemas de carga ou autenticação), 5xx indica falhas no lado do destino
- Use a extensão de navegador [!DNL Adobe Experience Platform Debugger] para inspecionar eventos que fluem do cliente por meio da Edge Network para regras de encaminhamento de eventos
- Valide de ponta a ponta verificando se os eventos encaminhados aparecem no sistema de destino (por exemplo, verifique [!DNL Google Analytics] relatórios em tempo real, [!DNL Meta] gerenciador de eventos ou tabelas do data warehouse)
- Configurar alertas do AEP para falhas de origem e fluxo de dados para capturar problemas de upstream que impediriam os eventos de atingir as regras de encaminhamento de eventos

**Documentação do Experience League:**

- [Monitoramento do encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/monitoring)
- [Adobe Experience Platform Debugger](https://experienceleague.adobe.com/en/docs/experience-platform/debugger/home)
- [Visão geral de alertas](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)

## Considerações de implantação

Esta seção aborda medidas de proteção, armadilhas comuns, práticas recomendadas e decisões de compensação que devem ser consideradas durante a implementação.

### Medidas de proteção e limites

- O encaminhamento de eventos processa eventos em tempo real na Edge Network — por padrão, não há modo de lote ou fila de tentativas para deliveries com falha
- Os limites de taxa do Edge Network se aplicam ao volume total de eventos processados por sequência de dados — [medidas de proteção do Edge Network](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/guardrails)
- As regras de encaminhamento de eventos executam no lado do servidor e não podem acessar recursos do lado do cliente (DOM, cookies, localStorage)
- O código personalizado nas regras de encaminhamento de eventos é executado em um ambiente em sandbox — nem todas as APIs do JavaScript do navegador estão disponíveis
- A chamada de busca do Cloud Connector tem limites de tempo limite — destinos que respondem lentamente podem causar tempos limite
- O encaminhamento de eventos está sujeito ao roteamento geográfico do Edge Network — os eventos são processados no local do Edge mais próximo
- O tamanho máximo do conteúdo para solicitações encaminhadas é regulado pelos limites do Edge Network

### Armadilhas comuns

- **Encaminhamento de todos os campos XDM sem filtragem:** O envio de toda a carga do evento XDM para um destino que precisa apenas de alguns campos desperdiça largura de banda, aumenta os custos de destino e pode, inadvertidamente, compartilhar PII. Sempre mapeie apenas os campos obrigatórios nas regras de encaminhamento.

- **Não proteger credenciais com Segredos:** Codificar chaves de API ou tokens em elementos de dados ou ações de regras cria um risco de segurança. Sempre use o recurso Segredos da coleção de dados para armazenar credenciais com segurança e fazer referência a elas nas regras.

- **Ignorando limites de taxa de destino:** Destinos de terceiros geralmente têm limites de taxa de API. Se o volume de eventos exceder a capacidade de um destino, os eventos poderão ser descartados ou o acesso à API poderá ser limitado. Consulte a documentação de destino para obter limites de taxa e implementar a filtragem para reduzir o volume de eventos, se necessário.

- **Publicar diretamente na Produção sem preparo:** Ignorar o ambiente de preparo significa que os erros são descobertos apenas na Produção, possivelmente causando perda de dados em destinos críticos. Sempre valide em Preparo com tráfego ativo primeiro.

- **Não monitorando códigos de resposta HTTP:** Uma regra que é acionada sem erros não garante que o destino processou os dados com êxito. Monitorar códigos de resposta de destino (disponível na ferramenta de Monitoramento de encaminhamento de eventos) e investigar respostas que não sejam 2xx.

- **Referências de caminho XDM mal configuradas:** os elementos de dados usam o prefixo `arc.event.xdm.` para fazer referência aos campos de evento de entrada. Um caminho incorreto (por exemplo, falta de um nível de aninhamento) produz silenciosamente valores nulos em vez de gerar erros. Valide valores de elementos de dados usando o Debugger.

### Práticas recomendadas

- **Comece com um único destino e expanda gradualmente** — Valide o encaminhamento de eventos de ponta a ponta com um destino antes de adicionar outras regras e destinos. Isso simplifica a depuração e cria confiança na infraestrutura.

- **Usar convenções de nomenclatura consistentes** — Nomeie elementos de dados, regras e bibliotecas com uma convenção clara que identifique o destino, o tipo de evento e o ambiente (por exemplo, &quot;Regra: Meta - Eventos de Compra&quot;, &quot;DE: Total de Pedidos&quot;).

- **Implementar filtragem em nível de campo para privacidade** — mesmo que o destino afirme tratar as PII de forma adequada, aplique a filtragem no lado do servidor para remover ou hash de campos confidenciais antes de sair da Edge Network. Essa é a principal vantagem de governança do encaminhamento de eventos em relação às tags do lado do cliente.

- **Versão de suas configurações** — Use o fluxo de trabalho de publicação da biblioteca para manter instantâneos com versão da sua configuração de encaminhamento de eventos. Documente o que cada versão da biblioteca contém para fins de auditoria e reversão.

- **Testar com o Platform Debugger** — a extensão [!DNL Adobe Experience Platform Debugger] fornece visibilidade sobre o ciclo de vida do evento, desde o SDK do lado do cliente até o processamento do Edge Network. Use-o durante o desenvolvimento e a solução de problemas.

- **Alinhar as regras de encaminhamento de eventos ao seu design de esquema XDM** — Se o encaminhamento de eventos for um requisito conhecido, crie seu esquema XDM e a taxonomia de eventos para incluir os campos que os destinos precisarão. O reajuste de alterações de esquema após a implantação causa mais interrupções.

### Decisões de compensação

>[!NOTE]
>
>**Contrapartida: simplicidade de extensão vs. flexibilidade de webhook**
>
>As extensões pré-criadas minimizam o esforço de implementação e manutenção, mas limitam você aos recursos e formatos de carga útil compatíveis com a extensão. Os webhooks personalizados fornecem controle total, mas exigem mais desenvolvimento e manutenção contínua.
>
>- **A opção A (baseada em extensão) favorece:** velocidade de entrada no mercado, dependência reduzida de desenvolvedor, gerenciamento automático de credenciais, manutenção mais baixa
>- **A opção B (baseada em Webhook) favorece:** Controle de carga total, suporte para qualquer ponto de extremidade HTTP, lógica de transformação personalizada, independência dos ciclos de versão da extensão
>- **Recomendação:** Use extensões quando disponíveis e suficientes. Retorne aos webhooks personalizados somente quando o destino não tiver uma extensão ou quando a extensão não for compatível com os recursos de API específicos necessários. A abordagem híbrida (opção C) é a opção pragmática para a maioria das organizações.

>[!NOTE]
>
>**Marcação: encaminhar todos os eventos vs. filtragem seletiva**
>
>O encaminhamento de todos os eventos para um destino garante a integridade, mas aumenta o volume de dados, os custos de destino e a exposição da privacidade. A filtragem seletiva reduz o ruído, mas corre o risco de perder eventos que podem ser valiosos.
>
>- **Encaminhar todos os eventos favorece:** integridade de dados, simplicidade, prova de obsolescência (os dados estão lá, se necessário, posteriormente)
>- **A filtragem seletiva favorece:** eficiência de custo, risco de privacidade reduzido, dados de destino mais limpos, conformidade com os princípios de minimização de dados
>- **Recomendação:** usar filtragem seletiva como padrão com base no tipo de evento e relevância comercial. Encaminhe somente os eventos e campos que cada destino realmente precisa. Isso se alinha aos princípios de minimização de dados (artigo 5 do GDPR) e reduz os custos operacionais.

>[!NOTE]
>
>**Contrapartida: uma única propriedade vs. várias propriedades**
>
>Uma única propriedade de encaminhamento de eventos é mais simples de gerenciar, mas significa que todas as regras compartilham um fluxo de trabalho de publicação. Várias propriedades fornecem isolamento, mas aumentam a sobrecarga de gerenciamento.
>
>- **Uma única propriedade favorece:** simplicidade, publicação unificada, elementos de dados compartilhados, depuração mais fácil
>- **Várias propriedades favorecem:** Controle de acesso em nível de equipe, cadências de publicação independentes, isolamento de falhas de destino
>- **Recomendação:** comece com uma única propriedade para a maioria das implementações. Somente divididos em várias propriedades se diferentes equipes tiverem integrações de destino diferentes e precisarem de ciclos de lançamento independentes, ou se os requisitos normativos exigirem isolamento rigoroso entre os fluxos de dados.

## Documentação relacionada

Os recursos a seguir fornecem detalhes adicionais sobre os tópicos abordados neste guia.

**Encaminhamento de eventos**

- [Visão geral do encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview)
- [Introdução ao encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started)
- [Monitoramento do encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/monitoring)
- [Segredos do encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/secrets)

**Extensões de encaminhamento de eventos**

- [Catálogo de extensões do lado do servidor](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/overview)
- [Extensão do Adobe Cloud Connector](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/cloud-connector/overview)
- [Extensão da API de conversões do Meta](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/meta/overview)
- [Extensão da Google Cloud Platform](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/google-cloud-platform/overview)
- [Extensão do AWS](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/aws/overview)
- [Extensão do Snowflake](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/snowflake/overview)
- [Extensão de conversões aprimoradas do Google Ads](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/google-ads-enhanced-conversions/overview)
- [Extensão do Mailchimp](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/mailchimp/overview)

**Coleta de dados e Edge Network**

- [Configurar sequências de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Visão geral dos fluxos de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview)
- [Visão geral do Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Visão geral da API do Edge Network Server](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [Visão geral das tags](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)
