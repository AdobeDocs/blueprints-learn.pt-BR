---
title: Experiência de conversa do Brand Concierge
description: Saiba como transformar propriedades digitais em experiências conversacionais habilitadas por IA e seguras para a marca, que orientam a descoberta do cliente.
solution: Experience Platform, Real-Time Customer Data Platform
exl-id: a9545328-316d-446a-9308-18af61c58d1c
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '7239'
ht-degree: 0%

---

# Experiência conversacional do Brand Concierge

Este guia fornece uma referência de implementação abrangente para experiências conversacionais habilitadas por IA usando o [!DNL Adobe Brand Concierge], integrado com o [!DNL Adobe Experience Platform] (AEP) e o [!DNL Real-Time Customer Data Platform] ([!DNL RT-CDP]). Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam implantar agentes conversacionais seguros para a marca em propriedades digitais.

Abrange todas as abordagens viáveis para implantar experiências conversacionais, desde chatbots de consultoria de produto até assistentes de navegação de site completo, com orientação sobre quando escolher cada opção. O plano aborda a configuração do agente, a governança da marca, a integração de conteúdo, as estratégias de implantação, o enriquecimento do perfil por sinais de conversa e a otimização de análises.

O [!DNL Brand Concierge] permite que as marcas implantem agentes de conversação inteligentes que entendam a voz da marca, acessem catálogos e conteúdo de produtos aprovados, forneçam recomendações personalizadas com base em dados de perfil em tempo real e capturem sinais de intenção e sentimento de volta no perfil unificado do cliente. O resultado é uma experiência de conversação que é natural e sobre a marca, enriquecendo a compreensão da organização de cada cliente.

## Visão geral do caso de uso

As organizações buscam cada vez mais transformar experiências digitais estáticas em conversas dinâmicas alimentadas por IA que orientam os clientes nas decisões de descoberta, seleção de produtos e compra. [!DNL Adobe Brand Concierge] A aborda isso fornecendo uma camada de IA conversacional orquestrada que fica no topo das propriedades digitais existentes, viabilizada pelo AEP Agent Orchestrator.

Esse padrão é diferente das implementações tradicionais de chatbot porque é integrado nativamente ao perfil unificado da AEP, usa medidas de proteção de governança da marca para garantir que cada resposta esteja alinhada aos padrões da marca e alimenta sinais de conversação de volta na plataforma de dados do cliente para personalização e ativação downstream.

O público-alvo inclui equipes de experiência digital, gerentes de comércio eletrônico, estrategistas de conteúdo e tecnólogos de marketing que precisam implantar experiências de conversação inteligentes que impulsionam o engajamento, a conversão e o enriquecimento do perfil.

## Principais objetivos de negócios

Os seguintes objetivos de negócios são compatíveis com esse padrão de caso de uso.

### Fornecer experiências personalizadas ao cliente

Personalize conteúdo, ofertas e mensagens para preferências individuais, comportamentos e estágios do ciclo de vida.

**KPIs:** Compromisso, Taxas de Conversão, Satisfação do Cliente (CSAT)

[Saiba mais sobre como fornecer experiências personalizadas ao cliente](/help/blueprints/business-objectives/customer-experience/deliver-personalized-customer-experiences.md)

### Melhorar o engajamento do cliente

Aumente a frequência e a profundidade da interação em todos os pontos de contato digitais e físicos.

**KPIs:** Envolvimento, Tempo na Página (Web), Taxas de Abertura

[Saiba mais sobre como melhorar o engajamento do cliente](/help/blueprints/business-objectives/qualification-sales-b2b/improve-customer-engagement.md)

### Aumentar as taxas de conversão

Melhore a porcentagem de visitantes e prospetos que concluem as ações desejadas, como compras, inscrições ou envios de formulários.

**KPIs:** Taxas de Conversão, Conversão de Cliente Potencial, Custo por Cliente Potencial

[Saiba mais sobre como aumentar as taxas de conversão](/help/blueprints/business-objectives/revenue-monetization/increase-conversion-rates.md)

### Adquirir novos clientes

Expanda a base de clientes por meio de campanhas de aquisição direcionadas, públicos semelhantes e otimização de mídia paga.

**KPIs:** Novos Clientes, Custo de Aquisição do Cliente, Conversão de Cliente Potencial/Cliente Potencial

[Saiba mais sobre como adquirir novos clientes](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

## Exemplo de casos de uso tático

Os cenários a seguir ilustram como esse padrão pode ser aplicado na prática.

- **Assistente de descoberta de produtos** — Implante um agente conversacional nas páginas de listagem de produtos que faz perguntas de qualificação e restringe as recomendações de produtos com base nas necessidades, preferências e orçamento do cliente
- **Consultor de comparação guiado** — ajude os clientes a comparar os produtos lado a lado através do diálogo natural, destacando as diferenças relevantes para as prioridades declaradas
- **Size and fit concierge** — oriente os compradores de vestuário ou calçados através da seleção de tamanhos usando perguntas e respostas conversacionais, reduzindo retornos e aumentando a confiança na compra
- **Assinatura ou seletor de plano** — oriente os clientes sobre as opções de camada de serviço ou plano de assinatura com recomendações personalizadas baseadas em padrões de uso e necessidades declaradas
- **Assistente de navegação do site** — ajude os visitantes a encontrar conteúdo, recursos de suporte ou categorias de produtos relevantes com base na intenção declarada, reduzindo as taxas de rejeição em sites complexos
- **Consulta pré-compra** — forneça orientação de compra altamente considerada (por exemplo, eletrônicos, produtos financeiros, seguros) por meio de conversas em várias voltas que são desenvolvidas para uma recomendação
- **Conversora do programa de fidelidade** — ajude os membros do programa de fidelidade a descobrir recompensas, entender os benefícios do nível e encontrar oportunidades de resgate por meio da interação conversacional
- **Conversação de reengajamento** — Inicie um alcance de conversação pró-ativo para visitantes recorrentes com base no histórico de navegação anterior ou em itens de carrinho abandonados
- **Escalonamento de agente em tempo real com contexto** — envie consultas complexas diretamente para agentes de suporte ou vendas em tempo real, preservando o contexto completo da conversa e os dados do perfil do cliente
- **Suporte e venda adicional pós-compra** — envolva os clientes após a compra com assistência de configuração, sugestões de produtos complementares e check-ins de satisfação por meio de canais de conversação

## Indicadores-chave de desempenho

Os KPIs a seguir ajudam a medir o sucesso desse padrão de caso de uso.

| KPI | Descrição | Abordagem de medição |
| --- | --- | --- |
| Taxa de Envolvimento da Conversa | Porcentagem de visitantes que iniciam e sustentam uma conversa | Conversas iniciadas/exibições de página qualificadas |
| Taxa de Conclusão da Conversa | Porcentagem de conversas que atingem uma resolução significativa | Conversas concluídas/conversas iniciadas |
| Índice de conversão de conversação | Porcentagem de conversas que levam a uma ação desejada (compra, inscrição, formulário de cliente potencial) | Conversões de conversas/total de conversas |
| Profundidade média da conversa | Número de voltas por conversa, indicando a qualidade do engajamento | Contagem média de mensagens por sessão |
| Satisfação do cliente (CSAT) | Pontuação de satisfação pós-conversa do feedback na experiência | Respostas da pesquisa ou classificações de aumento/diminuição |
| Taxa de Aceitação da Recomendação | Porcentagem de recomendações de produtos aceitas ou clicadas | Recomendações atendidas / recomendações atendidas |
| Taxa de transferência de agente ao vivo | Porcentagem de conversas escaladas para agentes ativos | Transmissões/total de conversas |
| Taxa de enriquecimento do perfil | Porcentagem de conversas que geram novos sinais de intenção ou preferência | Perfis enriquecidos/total de conversas |
| Receita influenciada pela conversa | Receita de compras nas quais uma conversa [!DNL Brand Concierge] precedeu a conversão | Análise de atribuição em jornadas de conversa para compra |
| Tempo até a solução | Duração média do início da conversa para resolução ou entrega | Análise de carimbo de data e hora em eventos de conversa |

## Padrão do caso de uso

**experiência de conversação do Brand Concierge**

Transforme propriedades digitais em experiências conversacionais habilitadas por IA e seguras para a marca, que orientam a descoberta do cliente por meio de um diálogo natural, enriquecem os perfis com sinais de intenção e sentimento e fornecem recomendações personalizadas do produto.

**Cadeia de funções:** Configuração do Agente > Configuração de Governança de Marca > Integração de Conteúdo > Implantação de Experiência de Conversação > Enriquecimento de Perfil > Analytics e Otimização

## Aplicativos

Os aplicativos a seguir são usados para implementar esse padrão de caso de uso.

- **[!DNL Brand Concierge]** — aplicativo de experiência de conversação habilitado por IA que fornece o orquestrador de agentes, o Product Advisor Agent, o Agente de Consultoria de Sites, a governança de marcas e a análise de conversação
- **[!DNL Adobe Experience Platform] (AEP)** — A Unified Data Foundation fornece esquemas XDM, resolução de identidade, perfis de clientes em tempo real e infraestrutura de coleta de dados para sinais de conversação
- **[!DNL Real-Time CDP] ([!DNL RT-CDP])** — Plataforma de dados do cliente que fornece pesquisa de perfil em tempo real para conversas personalizadas, segmentação de público a partir de sinais de conversação e enriquecimento de perfil com intenção e dados de sentimento

## Funções básicas

Os seguintes recursos básicos devem estar em vigor para esse padrão de caso de uso. Para cada função, o status indica se ele é tipicamente necessário, se presume ser pré-configurado ou se não é aplicável.

| Função de base | Status | O que deve estar em vigor | Referência do Experience League |
| --- | --- | --- | --- |
| Administração e governança | Obrigatório | Sandbox provisionada com o direito [!DNL Brand Concierge] habilitado; funções configuradas para administradores de experiência de conversação, gerentes de conteúdo e usuários de análise; políticas ABAC em vigor para dados de conversação contendo PII ou sinais sigilosos do cliente | [Visão geral do controle de acesso](https://experienceleague.adobe.com/pt-br/docs/experience-platform/access-control/home) |
| Preparação e modelagem de dados | Obrigatório | Esquemas XDM para eventos de conversação (classe ExperienceEvent com grupos de campos específicos de conversação capturando intenção, sentimento, interações de produto e eventos de entrega); esquema de perfil estendido com preferência de conversação e atributos de intenção; esquema de pesquisa do catálogo de produtos para recomendações de base | [Visão geral do sistema XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/home) |
| Fontes de dados e coleção | Obrigatório | [!DNL Web SDK] ou [!DNL Mobile SDK] configurado com sequências de dados roteando dados de eventos de conversação para conjuntos de dados do AEP; [!DNL Edge Network] integração para captura de eventos em tempo real durante conversas; dados de catálogo de produtos assimilados por conectores de origem ou assimilação em lote | [Visão geral do SDK da Web](https://experienceleague.adobe.com/pt-br/docs/experience-platform/web-sdk/home) |
| Configuração de identidade e perfil | Obrigatório | Namespaces de identidade configurados para identificação de visitantes (ECID para anônimo, ID de CRM ou email para autenticado); política de mesclagem configurada com ativação de borda para pesquisa de perfil em tempo real durante conversas; regras de vinculação de identidade para continuidade de conversa entre dispositivos | [Visão geral do Serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/home) |
| Definição e segmentação do público-alvo | Presumido em vigor | Públicos-alvo não necessários para implantação conversacional principal, mas necessários para estratégias de conversa personalizadas (por exemplo, segmentos de clientes de alto valor recebem fluxos de conversa diferentes); avaliação de streaming ou borda recomendada para personalização de conversa em tempo real | [Visão geral do Serviço de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/home) |

## Funções de suporte

Os recursos a seguir aumentam esse padrão de caso de uso, mas não são necessários para a execução principal.

| Função de suporte | Status | Por que é importante | Referência do Experience League |
| --- | --- | --- | --- |
| Criação de atributo calculado/derivado | Recomendado | Agregar sinais de conversação em atributos no nível do perfil (por exemplo, total de conversas, interesses dominantes do produto, pontuação média do sentimento) para uso na segmentação e personalização downstream | [Visão geral dos atributos computados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/computed-attributes/overview) |
| Gerenciamento do ciclo de vida dos dados | Recomendado | Configure políticas de retenção para dados de eventos de conversação, gerencie o consentimento para gravação e criação de perfil da conversação e dê suporte a solicitações de exclusão de privacidade para transcrições de conversação | [Visão geral do Gerenciamento Avançado do Ciclo de Vida dos Dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-lifecycle/home) |
| Rotulagem e aplicação de uso de dados | Recomendado | Rotular campos de dados de conversação que contenham sinais de PII, sentimento ou intenção; aplicar políticas de governança que impeçam que dados de conversação confidenciais cheguem a destinos não autorizados | [Visão geral da governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/home) |
| Monitoramento e capacidade de observação | Recomendado | Monitore pipelines de assimilação de eventos de conversação, rastreie as taxas de sucesso de enriquecimento do perfil e alerte sobre falhas no fluxo de dados que podem afetar a qualidade da personalização da conversação | [Visão geral dos Insights de Capacidade de Observação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/home) |
| Relatórios e análise | Incluído | Analise o desempenho da conversa, o feedback do cliente, a atribuição de conversão e a eficácia do agente usando a análise integrada do [!DNL Brand Concierge] e o [!DNL CJA] para a análise de impacto da conversa entre canais | [visão geral do CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-overview/cja-overview) |

## Funções do aplicativo

Este plano exerce as seguintes funções do Catálogo de Funções da Aplicação. As funções são mapeadas para fases de implementação em vez de etapas numeradas.

### [!DNL Brand Concierge]

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Configuração do agente | Fase 1: Configuração do agente | Configure o orquestrador de agentes [!DNL Brand Concierge] com especializações de agente (Supervisor de Produto, Site Advisory) e definições de comportamento de base |
| Configuração do controle de marca | Fase 2: Configuração de governança de marca | Defina a voz da marca, o tom, as medidas de proteção de mensagens, os limites de conteúdo aprovados e os tópicos proibidos que moldam todas as interações conversacionais |
| Integração de conteúdo | Fase 3: Integração de conteúdo | Conecte fontes de conteúdo aprovadas pela marca, incluindo conteúdo do AEM, catálogos de produtos, bases de conhecimento e outros dados confiáveis para obter respostas básicas |
| Configuração do Consultor de Produtos | Fase 3: Integração de conteúdo | Configure a Product Advisor Agent para obter recomendações personalizadas de produtos, comparações guiadas e entrega de resposta alinhada à marca |
| Configuração do site Advisory | Fase 3: Integração de conteúdo | Configure o Agente de Site Advisory para melhorar a navegação adaptando as interações com base no comportamento do visitante e nos sinais de intenção |
| Implantação de experiência de conversa | Fase 4: Implantação da experiência de conversa | Implante experiências de conversação em canais compatíveis (Web, aplicativo móvel, SDK personalizado) com suporte para interação de texto e voz |
| Gerenciamento de fluxo de baixo código | Fase 4: Implantação da experiência de conversa | Permitir que as equipes de marketing atualizem o tom de conversação, os fluxos e o conteúdo usando ferramentas de configuração de baixo código |
| Enriquecimento do perfil de conversa | Fase 5: Enriquecimento de perfil | Enriqueça os perfis de clientes do AEP com intenção, sentimento, afinidade de produtos e sinais comportamentais capturados durante as conversas |
| Análise de conversa | Fase 6: Analytics e otimização | Monitore métricas de engajamento, feedback de clientes, dados de conversão e qualidade da conversa por meio de painéis de análise integrados |
| Transmissão de agente ao vivo | Fase 4: Implantação da experiência de conversa | Configure uma entrega contínua para agentes de suporte ou de vendas em tempo real, preservando o contexto completo da conversa |

### [!DNL Real-Time CDP]

| Função | Fase de implementação | Descrição |
| --- | --- | --- |
| Pesquisa de perfil em tempo real | Fase 4: Implantação da experiência de conversa | Acesse atributos de perfil do cliente em tempo real e associações de segmento para personalizar respostas conversacionais com base em dados conhecidos do cliente |
| Enriquecimento de perfil | Fase 5: Enriquecimento de perfil | Enriquecer perfis com atributos computados derivados de eventos comportamentais conversacionais (pontuações de intenção, tendências de sentimento, afinidade de produtos) |
| Avaliação de público | Fase 5: Enriquecimento de perfil | Avaliar a associação de público com base em sinais conversacionais para permitir o direcionamento downstream de segmentos conversacionais engajados |

## Pré-requisitos

Os itens a seguir devem estar em vigor antes do início da implementação.

- [ O direito de ] [!DNL Adobe Brand Concierge] está ativo para a organização
- [ ] licenças do AEP e [!DNL RT-CDP] estão provisionadas com direitos de perfil e volume de evento suficientes
- [ ] documento de diretrizes de marca disponível definindo voz, tom, mensagens aprovadas e tópicos proibidos
- [ ] Catálogo de produtos ou repositório de conteúdo preparado para integração (ativos do AEM, dados PIM ou feed de produto estruturado)
- [ ] propriedades da Web identificadas para implantação de experiência de conversação com acesso técnico para integração com o SDK
- [ ] Infraestrutura de agente em tempo real disponível se a entrega for necessária (plataforma de centro de contato, integração de CRM)
- [ ] Estrutura de gerenciamento de consentimento em vigor para captura e definição de perfil de dados conversacionais
- [ ] [!DNL Web SDK] ou [!DNL Mobile SDK] já implantado nas propriedades de destino (ou planejado para implantação simultânea)
- [ ] Alinhamento das partes interessadas no escopo da conversa (somente consultoria de produto, navegação de site ou ambos)
- [ ] Revisão legal e de privacidade concluídas para uso e captura de dados de conversas alimentadas por IA

## Opções de implementação

As seções a seguir descrevem diferentes abordagens para implementar esse padrão de caso de uso.

### Opção A: implantação do Product Advisor

**Recomendado para:** organizações de comércio eletrônico e varejo focadas em experiências guiadas de descoberta, comparação e recomendação de produtos, que impulsionam a conversão e o valor médio de pedido.

**Como funciona:**

O Product Advisor Agent é configurado como a especialização conversacional principal. Ele se conecta ao catálogo de produtos, entende os atributos e os relacionamentos do produto e orienta os clientes por meio do diálogo natural para chegar a recomendações personalizadas. O agente usa medidas de proteção de controle de marca para garantir que as recomendações se alinhem às prioridades de negócios (por exemplo, promover itens em estoque, destacar produtos favoráveis à margem).

O Product Advisor integra-se ao perfil do cliente em tempo real para acessar o histórico de compras, o comportamento de navegação e os dados de preferências, permitindo recomendações que levam em conta o que o cliente já possui, já considerou ou provavelmente precisará com base em seu perfil. As conversas são capturadas como eventos de experiência e os sinais de intenção fluem de volta para o perfil para uso downstream.

**Principais considerações:**

- Requer um catálogo de produtos bem estruturado com dados de atributos avançados para recomendações eficazes
- Os dados do produto devem ser mantidos atualizados para evitar a recomendação de itens esgotados ou descontinuados
- O controle de marca deve definir como o agente lida com menções de produtos competitivos e comparações de preços

**Vantagens:**

- Gera diretamente um impacto mensurável na receita por meio da conversão guiada de compras
- Reduz as taxas de devolução de produtos através de decisões de compra mais bem informadas
- Captura sinais de alta afinidade e intenção do produto para personalização downstream
- Extensão natural das experiências de comércio eletrônico existentes

**Limitações:**

- Requer manutenção e sincronização contínuas do catálogo de produtos
- Limitado a conversas centradas em produtos; as perguntas de navegação do site podem não ser abordadas
- A eficácia depende da qualidade e da integridade dos dados do catálogo

**Experience League:**

- [Visão geral do Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [consultor de produtos da Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/product-advisor)

### Opção B: implantação do Site Advisory

**Recomendado para:** Organizações com propriedades digitais complexas (mídia, serviços financeiros, área de saúde, tecnologia) nas quais os visitantes precisam de assistência na navegação para encontrar conteúdo, recursos ou ferramentas de autoatendimento relevantes.

**Como funciona:**

O Site Advisory Agent está configurado como a especialização conversacional principal. Ele indexa a estrutura de conteúdo do site, entende os relacionamentos e as categorias de conteúdo da página e adapta sua orientação com base nos sinais de comportamento do visitante e na intenção declarada. Quando um visitante se envolve, o agente interpreta suas necessidades e as direciona para o conteúdo, as ferramentas ou os recursos mais relevantes.

O Site Advisory usa sinais comportamentais em tempo real (página atual, fonte de referência, caminho de navegação) combinados com dados de perfil (visitas anteriores, preferências de conteúdo, nível do cliente) para fornecer assistência de navegação contextualmente relevante. Isso é particularmente valioso em sites com hierarquias profundas de conteúdo, várias linhas de produtos ou fluxos de trabalho de autoatendimento complexos.

**Principais considerações:**

- Requer indexação de conteúdo abrangente e rastree regular à medida que o conteúdo do site é alterado
- Mais eficaz em sites com uma amplitude significativa de conteúdo, nos quais os visitantes geralmente têm dificuldades para encontrar o que precisam
- A governança da marca deve definir limites de escopo (para quais áreas do site o agente pode navegar)

**Vantagens:**

- Reduz as taxas de rejeição e melhora a descoberta de conteúdo em sites complexos
- Captura sinais de intenção de navegação que revelam lacunas de conteúdo e problemas de experiência do usuário
- Complexidade de implementação inferior à do Product Advisor (não é necessária integração com o catálogo de produtos)
- Fornece insights de análise sobre o que os visitantes estão procurando, mas não podem encontrar

**Limitações:**

- Menos diretamente vinculado à conversão de receita do que conversas focadas em produtos
- Requer que o conteúdo seja bem estruturado e atualizado regularmente para fornecer orientação precisa
- Pode precisar de retreinamento frequente à medida que a estrutura do site evolui

**Experience League:**

- [Visão geral do Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [supervisor de site do Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/site-advisor)

### Opção C: implantação combinada do Product Advisor + Site Advisory

**Recomendado para:** organizações que desejam uma experiência de conversação abrangente que abranja a descoberta de produtos e a navegação de sites, normalmente grandes marcas de varejo ou B2C com extensas propriedades digitais e diversas intenções de visitantes.

**Como funciona:**

O Product Advisor Agent e o Site Advisory Agent estão configurados no orquestrador [!DNL Brand Concierge]. O agent orchestrator usa a detecção de intenção para rotear conversas para a especialização apropriada — as consultas relacionadas ao produto vão para o Product Advisor enquanto as consultas de navegação e de descoberta de conteúdo vão para o Site Advisory. O orquestrador gerencia transições perfeitas entre especializações em uma única conversa.

Essa abordagem oferece a experiência de conversação mais completa, lidando com toda a variedade de necessidades do visitante, desde &quot;Ajude-me a encontrar um produto&quot; até &quot;Onde posso verificar o status do meu pedido?&quot; As medidas de proteção de governança de marca se aplicam uniformemente em ambas as especializações, garantindo uma voz de marca consistente, independentemente do tópico de conversa.

**Principais considerações:**

- Maior complexidade de implementação que requer integração de conteúdo e catálogo de produtos
- O roteamento de intenções entre especializações deve ser bem ajustado para evitar conversas mal direcionadas
- A configuração de governança da marca é mais abrangente para abranger os contextos do produto e da navegação

**Vantagens:**

- Fornece a experiência de conversação mais abrangente para visitantes
- Um único ponto de entrada lida com diversas intenções de visitantes sem exigir interfaces separadas
- Conversações de especialização cruzada (por exemplo, pergunta de produto que leva à navegação de suporte) manipuladas naturalmente
- Enriquecimento de perfil mais rico de sinais de conversa diversificados

**Limitações:**

- Maior esforço de implementação e manutenção contínua
- Requer coordenação entre equipes de catálogo de produtos e conteúdo
- Requisitos mais complexos de teste e controle de qualidade
- A configuração de governança de marca é mais abrangente

**Experience League:**

- [Visão geral do Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)

### Comparação de opções

| Critérios | Opção A: Consultor de produto | Opção B: Consultoria do site | Opção C: Combinado |
| --- | --- | --- | --- |
| Melhor para | Comércio eletrônico, conversão orientada por produtos | Sites com conteúdo intenso, navegação por autoatendimento | Experiência digital de escopo completo |
| Complexo | Médio | Low-Medium | Alta |
| Tempo de implantação | 4 a 6 semanas | 3 a 5 semanas | 6 a 10 semanas |
| Impacto na receita | Alta (influência da conversão direta) | Medium (indireta por meio de envolvimento) | Mais alto (conversão e envolvimento) |
| Requisitos de conteúdo | Catálogo de produtos com atributos avançados | Índice de conteúdo do site | Catálogo de produtos e índice de conteúdo |
| Enriquecimento de perfil | Afinidade de produtos, intenção de compra | Tentativa de navegação, preferências de conteúdo | Espectro de sinal completo |
| Esforço de manutenção | Sincronização do catálogo de produtos | Reindexação de conteúdo | Ambos em andamento |

### Escolha a opção certa

Comece avaliando seu objetivo comercial principal e as características da propriedade digital:

1. **Se a sua meta principal for impulsionar a conversão do produto** e sua propriedade digital for focada no comércio, escolha a **Opção A (Consultor de Produtos)**. Esse é o ponto de partida mais comum para marcas de varejo e comércio eletrônico.

2. **Se sua meta principal for melhorar a descoberta de conteúdo** e seu site tiver hierarquias de conteúdo profundas ou fluxos de trabalho de autoatendimento complexos, escolha **Opção B (Consultoria de Site)**. Isso é ideal para empresas de mídia, serviços financeiros, assistência médica e tecnologia.

3. **Se precisar de uma cobertura abrangente** e tiver necessidades de comércio de produtos e de navegação de conteúdo, escolha **Opção C (Combinada)**. Considere começar com uma especialização e adicionar o segundo após o primeiro ser estável e otimizado.

Uma abordagem em fases é recomendada para a maioria das organizações: implante uma especialização primeiro, valide o desempenho e colete aprendizados e, em seguida, expanda para a implantação combinada.

## Fases de implementação

As fases a seguir descrevem a sequência de implementação recomendada.

### Fase 1: configuração do agente

**Função de aplicativo:** [!DNL Brand Concierge]: configuração de agente

Configure o orquestrador de agentes [!DNL Brand Concierge] principal, incluindo a seleção de especializações do agente (Supervisor de Produto, Site Advisory ou ambos), a configuração do comportamento do agente base e o estabelecimento da conexão entre o [!DNL Brand Concierge] e o AEP para acesso ao perfil e captura de eventos.

#### Decisão: seleção de especialização do agente

Determine quais especializações de agente devem ser ativadas para esta implantação.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Somente Consultor de Produtos | Implantação com foco na Commerce voltada para descoberta e conversão de produtos | Requer integração do catálogo de produtos; caminho mais rápido para o impacto na receita |
| Somente Aviso do Site | Implantação focada em conteúdo e navegação | Menor complexidade de integração; ideal para sites não comerciais |
| Ambas as especializações | Abrangente cobertura conversacional entre produto e conteúdo | Maior complexidade; considere a implantação em fases, começando com uma |

#### Decisão: modelo de iniciação de conversa

Determine como as conversas devem começar na propriedade digital.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Iniciado pelo visitante (passivo) | Abordagem padrão em que o widget de chat está disponível, mas não se envolve proativamente | Reduz o risco de interrupção; depende da percepção do visitante sobre a opção de chat |
| Engajamento pró-ativo (acionado) | O agente inicia uma conversa com base em sinais comportamentais (por exemplo, tempo de permanência estendido, visitas repetidas à página, hesitação do carrinho) | Taxas de engajamento mais altas, mas correm o risco de incomodar os visitantes se os acionadores forem muito agressivos; requer ajuste de acionador comportamental |
| Híbrido (passivo com prompts contextuais) | O widget de chat é passivo, mas exibe prompts contextuais com base no conteúdo da página ou no comportamento do visitante | Abordagem equilibrada; guia de prompts sem forçar o engajamento |

#### Configurar o agente

**Navegação da interface do usuário:** [!DNL Experience Platform] > Assistente de IA > [!DNL Brand Concierge] > Configuração do agente

Principais detalhes de configuração:

- Defina o nome e a descrição do agente que aparecerá na interface conversacional
- Selecione qual sandbox da AEP contém o perfil do cliente e os dados do evento que o agente deve acessar
- Configure o orquestrador do agente para rotear consultas entre especializações com base na detecção de intenção
- Definir parâmetros de sessão de conversa (duração de tempo limite, duração máxima da conversa, limites de sessão simultânea)
- Habilite a integração de pesquisa de perfil em tempo real para que o agente possa acessar os dados de perfil do visitante durante as conversas

**Onde as opções divergem:**

**Para Opção A (Consultor de Produtos):**
Habilite a especialização do Product Advisor e configure sua conexão com a fonte de dados do catálogo de produtos. Defina parâmetros de recomendação do produto, incluindo máximo de recomendações por resposta, preferências de exibição do atributo do produto e regras de tratamento de comparação.

**Para a Opção B (Supervisão de Site):**
Habilite a especialização do Site Advisory e configure sua conexão com o índice de conteúdo do site. Defina parâmetros de navegação, incluindo limites de escopo de conteúdo, tratamento de categoria de página e preferências de geração de deep link.

**Para Opção C (Combinada):**
Habilite ambas as especializações e configure a lógica de roteamento de intenção do orchestrator. Defina regras de roteamento que determinem quando uma conversa deve ser tratada pelo Supervisor de Produto versus o Site Advisory e como as transições entre especializações devem ser gerenciadas em uma única conversa.

**Documentação do Experience League:**

- [Visão geral do Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [Visão geral do Assistente de IA](https://experienceleague.adobe.com/pt-br/docs/experience-platform/ai-assistant/home)
- [AEP Agent Orchestrator](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)

### Fase 2: configuração de governança da marca

**Função do aplicativo:** [!DNL Brand Concierge]: configuração de governança de marca

Configure as medidas de proteção da governança de marca que moldam todas as interações conversacionais. Isso inclui definições de voz e tom da marca, limites de conteúdo aprovados, tópicos proibidos, diretrizes de estilo de resposta e regras de escalonamento. A governança da marca garante que cada resposta gerada por IA esteja alinhada aos padrões da marca.

#### Decisão: nível de rigor da governança

Determine se as medidas de proteção da governança da marca devem restringir as respostas da conversa.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Governança rigorosa | Setores altamente regulamentados (serviços financeiros, saúde, seguros) ou marcas premium que exigem controle preciso de tom | Limita a flexibilidade de conversação; pode resultar em respostas mais frequentes &quot;Não posso ajudar com isso&quot;; maior segurança da marca |
| Governança moderada | A maioria das marcas de consumidor em que a consistência da voz da marca é importante, mas há alguma flexibilidade de conversação aceitável | Bom equilíbrio entre segurança da marca e naturalidade da conversa; ponto de partida recomendado para a maioria das implementações |
| Governança flexível | Marcas casuais ou de estilo de vida em que a personalidade de conversação e o engajamento são priorizados | Sensação de conversação mais natural; requer monitoramento mais contínuo para respostas fora da marca |

#### Decisão: estratégia de tratamento fora do tópico

Determine como o agente deve lidar com perguntas fora do escopo configurado.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Redirecionar para escopo | O agente reconhece a pergunta e redireciona para os tópicos com os quais pode ajudar | Mantém o engajamento, mas pode frustrar os visitantes com necessidades legítimas fora do tópico |
| Transmissão para o agente ativo | O agente oferece a opção de conectar o visitante a um agente humano para perguntas fora do tópico | A melhor experiência do cliente, mas requer infraestrutura e equipe de agente em tempo real |
| Declínio normal com recursos | O agente explica que não pode ajudar com esse tópico e fornece links para recursos relevantes ou canais de suporte | Fallback de baixo atrito; não requer disponibilidade do agente ativo |

#### Configurar a governança da marca

**Navegação da interface do usuário:** [!DNL Experience Platform] > Assistente de IA > [!DNL Brand Concierge] > Governança da marca

Principais detalhes de configuração:

- Definir os atributos da marca: nome da marca, slogan, missão, valores e características de personalidade que informam o tom de conversa
- Definir parâmetros de tom: nível de formalidade, tolerância ao humor, nível de empatia e assertividade para recomendações de produtos
- Configurar limites de conteúdo aprovados: tópicos que o agente está autorizado a discutir e tópicos que são explicitamente proibidos
- Definir diretrizes de formato de resposta: comprimento máximo da resposta, uso de listas versus prosa, política emoji e formatação de link
- Definir acionadores de escalonamento: condições que devem encaminhar automaticamente uma conversa para um agente ativo (por exemplo, detecção de reclamações, sinais de insatisfação repetidos, identificação de alto valor do cliente)
- Configurar o tratamento de menção da concorrência: como o agente deve responder quando os visitantes perguntarem sobre produtos de concorrentes
- Definir requisitos de aviso legal e de isenção de responsabilidade: divulgações obrigatórias para setores regulamentados

**Documentação do Experience League:**

- [Governança da marca Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [Insights operacionais do assistente de IA](https://experienceleague.adobe.com/pt-br/docs/experience-platform/ai-assistant/home)

### Fase 3: Integração de conteúdo

**Função do aplicativo:** [!DNL Brand Concierge]: Integração de Conteúdo, Configuração do Supervisor de Produto, Configuração do Site Advisory

Configure as fontes de conteúdo que fundamentam as respostas de conversas em informações precisas e aprovadas pela marca. Isso inclui a integração do catálogo de produtos, conexões de conteúdo do AEM, importações da base de conhecimento e agendamentos de atualização de conteúdo.

#### Decisão: método de integração do catálogo de produtos

Determine como os dados do produto devem ser fornecidos à Product Advisor Agent. (Apenas as opções A e C)

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Integração do conjunto de dados do AEP | O catálogo de produtos já está assimilado no AEP como um conjunto de dados de pesquisa por meio de conectores de origem | Aproveita a infraestrutura de dados existente; mantém os dados do produto sincronizados com os dados do perfil; requer coleta e modelagem de dados fundamentais para incluir o catálogo de produtos |
| Integração de feed direto | O catálogo de produtos existe em um PIM ou plataforma de comércio que pode fornecer um feed estruturado | Pode oferecer mais dados de inventário e preços em tempo real; requer configuração e programação do feed |
| Integração de conteúdo do AEM | O conteúdo do produto é gerenciado no AEM e deve servir como a fonte de dados autorizada do produto | Melhor para marcas em que o AEM é o hub de conteúdo; garante a consistência entre o conteúdo da Web e as respostas conversacionais |

#### Decisão: frequência de atualização de conteúdo

Determine com que frequência a base de conhecimento de conteúdo do agente deve ser atualizada.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Tempo real/quase em tempo real | Disponibilidade do produto, preços ou conteúdo são alterados com frequência (por exemplo, vendas rápidas, varejo sensível ao inventário) | Maior precisão, mas maior carga de infraestrutura; essencial para recomendações sensíveis ao inventário |
| Atualização diária | As alterações de conteúdo são planejadas e programadas (por exemplo, calendários editoriais, promoções semanais) | Bom equilíbrio entre precisão e desempenho; adequado para a maioria das implementações |
| Atualização sob demanda | As alterações de conteúdo são raras e podem ser acionadas manualmente quando ocorrerem atualizações | Menor sobrecarga; adequado para catálogos de produtos estáticos ou sites de conteúdo estáveis |

#### Configurar fontes de conteúdo

**Navegação da interface do usuário:** [!DNL Experience Platform] > Assistente de IA > [!DNL Brand Concierge] > Fontes de Conteúdo

Principais detalhes de configuração:

- Conectar fontes de dados do catálogo de produtos com mapeamento de campo para nome do produto, descrição, atributos, preço, disponibilidade, imagens e hierarquia de categoria
- Configurar a indexação de conteúdo para páginas do site, artigos da base de conhecimento, conteúdo de perguntas frequentes e documentação de suporte
- Definir limites de escopo de conteúdo que definem qual conteúdo o agente pode referenciar e qual será excluído
- Configure o comportamento de fallback do conteúdo quando o agente não encontrar conteúdo relevante para responder a uma pergunta
- Configurar regras de qualidade do conteúdo: limite mínimo de confiança do conteúdo para inclusão em respostas, requisitos de citação e atribuição de origem

**Onde as opções divergem:**

**Para Opção A (Consultor de Produtos):**
Concentre-se na integração do catálogo de produtos com o mapeamento de atributos de produtos avançados. Configure a lógica de recomendação do Product Advisor Agent, incluindo quantos produtos sugerir, como lidar com itens indisponíveis, como apresentar comparações de produtos e como incorporar dados de perfil do cliente (histórico de compras, comportamento de navegação) à classificação de recomendação.

**Para a Opção B (Supervisão de Site):**
Concentre-se na indexação de conteúdo do site com o mapeamento de hierarquia de página. Configure a lógica de navegação do Agente de consultoria de site, incluindo como interpretar a intenção do visitante, quais categorias de conteúdo priorizar, como lidar com solicitações de navegação ambíguas e como adaptar sugestões com base no contexto da página atual do visitante e no comportamento da sessão.

**Para Opção C (Combinada):**
Configure o catálogo de produtos e as fontes de conteúdo do site. Certifique-se de que a lógica de roteamento de conteúdo atribua o conteúdo corretamente à especialização apropriada e que as referências cruzadas entre o conteúdo do produto e o conteúdo de navegação do site sejam mapeadas corretamente.

**Documentação do Experience League:**

- [Configuração de conteúdo do Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [consultor de produtos da Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/product-advisor)
- [supervisor de site do Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/site-advisor)
- [Visão geral das fontes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/home)

### Fase 4: implantação da experiência de conversa

**Função do aplicativo:** [!DNL Brand Concierge]: Implantação de Experiência de Conversação, Gerenciamento de Fluxo de Baixo Código, Transferência de Agente em Tempo Real; [!DNL RT-CDP]: Pesquisa de Perfil em Tempo Real

Implante a experiência de conversação nas propriedades digitais do Target, incluindo configuração de canal, personalização de widget, integração de pesquisa de perfil para personalização, regras de handoff de agente ao vivo e ferramentas de baixo código para gerenciamento contínuo de conteúdo.

#### Decisão: canal de implantação

Determine em quais canais a experiência de conversação deve ser implantada.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Web (widget incorporado) | A propriedade principal da Web é o principal ponto de contato do cliente | Ponto de partida mais comum; requer integração de [!DNL Web SDK]; oferece suporte a visitantes anônimos e autenticados |
| Aplicativo móvel (integração com o SDK) | O aplicativo móvel é um canal importante de envolvimento do cliente | Requer integração de [!DNL Mobile SDK]; considere restrições de espaço físico na tela para a interface da conversa |
| Implantação personalizada do SDK | A experiência de conversa precisa ser incorporada em um aplicativo personalizado, quiosque ou propriedade digital não padrão | Máxima flexibilidade; requer mais esforço de desenvolvimento; adequado para quiosques na loja ou plataformas proprietárias |
| Implantação multicanal | Experiência de conversa necessária na Web, dispositivos móveis e outros canais simultaneamente | Maior alcance; requer governança de marca consistente em todos os canais; o contexto da conversa deve persistir entre os canais quando possível |

#### Decisão: profundidade do Personalization para conversas

Determine quantos dados de perfil do cliente o agente deve usar para personalizar conversas.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Somente anônimo (contexto de sessão) | Abordagem de privacidade primária ou quando a maioria dos visitantes não está identificada | Usa apenas sinais comportamentais na sessão; nenhuma pesquisa de perfil necessária; adequado para descoberta anônima de produtos |
| Reconhecimento de perfil (visitantes autenticados) | Normalmente, os visitantes fazem logon e personalizam recomendações com base no valor agregado do histórico | Requer pesquisa de perfil em tempo real via [!DNL RT-CDP]; qualidade de recomendação significativamente melhor para clientes conhecidos |
| Personalização progressiva | Combinação de anônimo e autenticado com a criação progressiva de perfis durante a conversa | Começa com o contexto da sessão; enriquece conforme o visitante fornece informações ou se autentica; equilibra a privacidade e a personalização |

#### Decisão: configuração de handoff do agente ativo

Determine se as conversas devem ser escalonáveis para agentes humanos vivos.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Sem entrega (somente autoatendimento) | O agente de IA pode lidar com todos os tipos de conversação esperados ou os agentes em tempo real não estão disponíveis | Implantação mais simples; pode frustrar visitantes com necessidades complexas; adequado para cenários de baixo risco de navegação por produtos |
| Entrega baseada em regras | Acionadores específicos devem ser escalonados para agentes ativos (por exemplo, detecção de reclamações, cliente de alto valor, consulta complexa) | Comportamento de escalonamento previsível; requer a definição de regras e acionadores de escalonamento; precisa da integração ativa da plataforma do agente |
| Transferência solicitada pelo visitante | Os visitantes podem solicitar um agente em tempo real em qualquer ponto da conversa | A melhor experiência do cliente; requer pessoal de agente sempre disponível ou gerenciamento de fila; o contexto de conversa deve ser transferido |

#### Implantar a experiência de conversação

**Navegação da interface do usuário:** [!DNL Experience Platform] > Assistente de IA > [!DNL Brand Concierge] > Implantação

Principais detalhes de configuração:

- Configurar a aparência do widget de conversa: posição, esquema de cor, avatar, mensagem de boas-vindas e estilo de interação (texto, voz ou ambos)
- Integrar com [!DNL Web SDK] ou [!DNL Mobile SDK] para captura de eventos e resolução de perfil
- Configure a pesquisa de perfil em tempo real para acessar atributos do cliente, associações de segmento e atividades recentes durante conversas
- Configurar a integração de entrega do agente ativo com a plataforma do centro de contato, incluindo o protocolo de transferência de contexto, o roteamento de fila e a notificação do agente
- Permita que as ferramentas de gerenciamento de fluxo de baixo código para equipes de marketing atualizem iniciadores de conversas, mensagens promocionais, conteúdo sazonal e variações de fluxo sem o envolvimento do desenvolvedor
- Configurar regras de persistência de sessão de conversa: quanto tempo o histórico da conversa é retido, se as conversas podem retomar entre sessões e continuidade de conversa entre dispositivos

**Documentação do Experience League:**

- [Implantação do Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [Visão geral do Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/web-sdk/home)
- [Visão geral da API do Edge Network Server](https://experienceleague.adobe.com/pt-br/docs/experience-platform/edge-network-server-api/overview)
- [Ponto de extremidade de entidades da API de perfil](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/api/entities)
- [Visão geral do Perfil do cliente em tempo real](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/home)

### Fase 5: Enriquecimento de perfil

**Função de aplicativo:** [!DNL Brand Concierge]: Enriquecimento de Perfil de Conversação; [!DNL RT-CDP]: Enriquecimento de Perfil, Avaliação de Público

Configure o pipeline de captura e enriquecimento que alimenta sinais de conversação de volta no perfil unificado do cliente do AEP. Isso inclui mapear eventos de conversa para o XDM, extrair sinais de intenção e sentimento, criar atributos computados de dados de conversação e criar públicos com base em comportamentos de conversação.

#### Decisão: escopo de captura de sinal de conversa

Determine quais sinais de conversação devem ser capturados e gravados no perfil do cliente.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Somente sinais de engajamento principais | Enriquecimento mínimo do perfil; capturar o início, o fim, a duração e o status de conclusão da conversa | Volume de dados mais baixo; suficiente para análises básicas; valor de personalização limitado |
| Sinais de intenção e preferência | Capturar interesses inferidos do produto, preferências declaradas e categorias de tópico discutidas | Alto valor de personalização, volume de dados moderado, recomendado com mais frequência |
| Captura de sinal completo | Intensidade de captura, sentimento, interações de produto, respostas de recomendação, eventos de entrega e pontuações de feedback | Enriquecimento de perfil mais amplo; maior volume de dados; permite análise avançada e personalização orientada por aprendizado de máquina |

#### Decisão: Criação de público a partir de dados de conversação

Determine se os públicos-alvo devem ser criados com base em comportamentos de conversação para ativação downstream.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Nenhum público-alvo de conversa | Dados de conversa usados apenas para análise, não para ativação de público-alvo | Abordagem mais simples; adequada se as conversas forem complementares aos canais de engajamento existentes |
| Públicos-alvo com base em intenção | Criar públicos-alvo com base em interesses de produto declarados ou intenções de navegação de conversas | Permite redirecionar visitantes que expressaram interesse, mas não converteram; alto valor para o comércio |
| Públicos comportamentais | Criar públicos com base em padrões de envolvimento de conversa (por exemplo, alto envolvimento, conversa abandonada, visitas repetidas) | Permite a orquestração de jornadas com informações de conversa e acompanhamento entre canais |

#### Configurar enriquecimento de perfil

**Navegação da interface do usuário:** [!DNL Experience Platform] > Cliente > Perfis > Atributos computados (para sinais derivados); Cliente > Públicos > Criar público (para públicos conversacionais)

Principais detalhes de configuração:

- Mapear eventos de conversação para campos de esquema XDM ExperienceEvent capturando ID de conversação, contagem de mensagens, tópicos discutidos, produtos referenciados, pontuações de sentimentos e status de resolução
- Configure o enriquecimento do perfil [!DNL Brand Concierge] para gravar sinais de intenção e preferência no perfil unificado
- Criar atributos computados dos dados do evento de conversação: total de conversas (duração), interesse dominante da categoria do produto (30 dias), pontuação média do sentimento (90 dias), taxa de conversão de conversa para compra
- Defina segmentos de público-alvo em lote ou por transmissão com base em sinais conversacionais para ativação downstream (por exemplo, &quot;Visitantes que discutiram a Categoria de produto X nos últimos 7 dias, mas não compraram&quot;)
- Valide o enriquecimento do perfil pesquisando perfis de amostra para confirmar se os atributos de conversação estão preenchidos

**Documentação do Experience League:**

- [Visão geral de atributos computados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/computed-attributes/overview)
- [Guia da interface de atributos computados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/computed-attributes/ui)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentação de transmissão](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Visão geral do Perfil do cliente em tempo real](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/home)

### Fase 6: Analytics e otimização

**Função do aplicativo:** [!DNL Brand Concierge]: Conversational Analytics

Configure painéis de análise e relatórios para medir o desempenho da experiência de conversação, identificar oportunidades de otimização e rastrear KPIs. Isso inclui análise interna do [!DNL Brand Concierge], integração opcional do [!DNL CJA] para análise de impacto de conversações entre canais e fluxos de trabalho de otimização em andamento.

#### Decisão: profundidade do Analytics

Determine qual nível de análise conversacional é necessário.

| Opção | Quando escolher | Considerações |
| --- | --- | --- |
| Análise [!DNL Brand Concierge] interna | Relatórios padrão sobre volume de conversação, engajamento, satisfação e conversão são suficientes | A ativação é mais rápida; abrange KPIs principais; correlação limitada entre canais |
| Integração do [!DNL Brand Concierge] + [!DNL CJA] | Análise entre canais necessária para entender como as conversas influenciam jornadas mais amplas do cliente | Requer conexão [!DNL CJA] e configuração de visualização de dados; habilita a análise de atribuição em conversações e outros canais |
| Pilha completa de análise ([!DNL Brand Concierge] + [!DNL CJA] + painéis personalizados) | Relatórios de nível executivo, modelagem de atribuição avançada e criação de público-alvo personalizado a partir de insights de análise | Maior capacidade analítica; exige experiência de [!DNL CJA]; habilita a otimização de conversa orientada por dados |

#### Configurar o Analytics e a otimização

Navegação da **UI:** [!DNL Experience Platform] > Assistente de IA > [!DNL Brand Concierge] > Analytics; [!DNL Analytics Platform] > Workspace (para [!DNL CJA])

Principais detalhes de configuração:

- Revise os painéis de análise integrados do [!DNL Brand Concierge]: tendências de volume de conversação, taxa de envolvimento, taxa de conclusão, pontuações CSAT, taxa de aceitação de recomendação e frequência de entrega
- Configure a conexão [!DNL CJA] para incluir conjuntos de dados de eventos de conversação para análise entre canais (se escolher a integração [!DNL CJA])
- Crie análise de espaço de trabalho [!DNL CJA] para atribuição de conversa a conversão, identificando quais tópicos de conversa estão correlacionados com o comportamento de compra
- Configurar o monitoramento da qualidade da conversa: rastrear tópicos em que o agente luta, perguntas comuns sem resposta e tendências de sentimento ao longo do tempo
- Definir fluxos de trabalho de otimização: cadência de revisão regular para atualizações de governança de marca, acionadores de atualização de conteúdo e melhorias no fluxo de conversa com base em insights de análise

**Documentação do Experience League:**

- [Brand Concierge Analytics](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [Visão geral do CJA Analysis Workspace](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/home)
- [Criar ou editar uma conexão do CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-connections/create-connection)
- [Criar ou editar uma visualização de dados do CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/create-dataview)

## Considerações de implantação

As seções a seguir abordam medidas de proteção, armadilhas comuns, práticas recomendadas e decisões de compensação que devem ser consideradas durante a implementação.

### Medidas de proteção e limites

- [!DNL Brand Concierge] experiências de conversação estão sujeitas a limites de taxa de geração de resposta de IA; a capacidade de conversação simultânea depende da camada de direito
- A pesquisa de perfil em tempo real durante conversas está sujeita aos limites de taxa da API de perfil por sandbox — [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/guardrails)
- A assimilação de dados de eventos de conversa segue os limites padrão de assimilação de streaming do AEP — [Medidas de proteção de assimilação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/ingestion/guardrails)
- O tamanho do catálogo de produtos e o volume do índice de conteúdo estão sujeitos aos limites de integração de conteúdo [!DNL Brand Concierge]
- Um máximo de 25 atributos computados por sandbox se aplica a agregações de sinal conversacional — [Medidas de proteção de atributos computados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/computed-attributes/overview)
- O máximo de 4.000 definições de segmento por sandbox se aplica a públicos conversacionais — [Medidas de proteção de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/guardrails)

### Armadilhas comuns

- **Definição insuficiente de governança de marca:** a implantação sem configuração completa de governança de marca resulta em respostas fora da marca que prejudicam a confiança do cliente. Invista um tempo significativo na Fase 2, definindo o tom, os limites e as regras de escalonamento antes da implantação.
- **Dados obsoletos do catálogo de produtos:** as recomendações do Product Advisor com base em dados desatualizados de inventário, preços ou disponibilidade frustram os clientes e reduzem a confiança. Estabeleça pipelines automatizados de atualização de conteúdo com verificações de validação.
- **Acionadores de engajamento pró-ativo excessivamente agressivos:** definir acionadores comportamentais muito agressivamente (por exemplo, acionar uma conversa após 3 segundos na página) incomoda os visitantes e aumenta as taxas de rejeição. Comece com acionadores conservadores e ajuste com base nos dados de engajamento.
- **Ignorando experiência de visitante anônimo:** Focar a personalização somente em visitantes autenticados ignora a maioria do tráfego. Projete fluxos de conversa que forneçam valor para visitantes anônimos usando sinais comportamentais na sessão.
- **Ignorando a configuração de enriquecimento do perfil:** a implantação de conversas sem capturar sinais de volta para o perfil desperdiça dados importantes de intenção e preferência. Configure o enriquecimento do perfil em paralelo com a implantação, não como uma reflexão posterior.
- **Ignorando experiência de transferência ao vivo do agente:** Experiências de transferência insatisfatórias (contexto perdido, perguntas repetidas, longos tempos de espera) prejudicam a experiência geral de conversação mais do que não oferecer a transferência. Teste o fluxo de entrega completo de ponta a ponta antes do lançamento.

### Práticas recomendadas

- Comece com uma especialização de agente único (Product Advisor ou Site Advisory) e expanda depois de estabelecer o desempenho básico.
- Realizar workshops de governança de marca com participantes de marketing, jurídicos e de experiência do cliente antes de configurar as medidas de proteção.
- Usar personalização progressiva: inicie conversas com respostas baseadas em contexto de sessão e aprofunde a personalização à medida que o visitante fornece informações ou se autentica.
- Implemente testes A/B de iniciadores de conversação, prompts e formatos de apresentação de recomendações usando as ferramentas de gerenciamento de fluxo de baixo código.
- Agende uma análise regular (semanal ou quinzenal) das conversas para identificar lacunas de conteúdo, pontos de falha comuns e oportunidades de otimização.
- Crie um ciclo de feedback entre as atualizações de análise conversacional e de governança da marca — use dados de conversa para refinar o tom, adicionar novos tópicos aprovados e ajustar as regras de escalonamento.
- Monitore tendências de sentimento de conversa como um sistema de aviso antecipado para problemas de produtos, problemas de site ou mudanças de percepção da marca.
- Desenvolva fluxos de conversação que capturem naturalmente sinais que enriquecem os perfis sem fazer com que a interação pareça um interrogatório.

### Decisões de compensação

>[!NOTE]
>As seguintes decisões de compensação devem ser avaliadas com base nos requisitos e restrições específicos da organização.

**Profundidade de personalização da conversa vs. simplicidade de privacidade**

A integração mais profunda do perfil permite conversas mais personalizadas e eficazes, mas aumenta a complexidade da coleta de dados, os requisitos de consentimento e a carga de conformidade com a privacidade.

- **A personalização profunda favorece:** taxas de conversão mais altas, melhor qualidade de recomendação, enriquecimento de perfil mais avançado e conversas mais envolventes para clientes recorrentes
- **A simplicidade da privacidade favorece:** implantação mais rápida, gerenciamento de consentimento mais simples, menor risco regulamentar e posicionamento de privacidade na primeira marca
- **Recomendação:** comece com uma personalização progressiva que funcione bem para visitantes anônimos e adicione uma personalização baseada em perfil para sessões autenticadas. Isso oferece valor em todos os níveis de identificação, mantendo a conformidade com a privacidade gerenciável. Implemente a captura de consentimento para a definição de perfil conversacional alinhada às estruturas de consentimento existentes.

**Rigor da governança de marca vs. naturalidade da conversa**

Medidas de proteção rigorosas de governança de marca garantem que cada resposta esteja alinhada aos padrões de marca, mas restrições rígidas demais fazem com que as conversas se sintam robóticas e reduzam o engajamento.

- **A governança rígida favorece:** Segurança da marca, conformidade regulatória, mensagens consistentes e comportamento previsível do agente
- **A governança flexível favorece:** Fluxo de conversação natural, maior engajamento, melhor satisfação do cliente e a capacidade de lidar com uma variedade maior de consultas
- **Recomendação:** Comece com uma governança moderada e aperte ou afrouxe com base na análise de conversa. Monitore a taxa de respostas &quot;Não posso ajudar com isso&quot; como um indicador de restrição excessiva. Use as ferramentas de gerenciamento de fluxo de baixo código para iterar rapidamente nas configurações de governança sem o envolvimento do desenvolvedor.

**Atualização de conteúdo em tempo real vs. desempenho do sistema**

A sincronização de conteúdo em tempo real garante que o agente sempre tenha dados atuais de produto e conteúdo, mas a atualização contínua consome mais recursos de infraestrutura e pode apresentar latência.

- **A atualização em tempo real favorece:** Precisão para recomendações sensíveis ao inventário, promoções sensíveis ao tempo e alteração rápida de conteúdo
- **A atualização agendada favorece:** estabilidade do sistema, consumo previsível de recursos e custos mais baixos de infraestrutura
- **Recomendação:** use a atualização diária de conteúdo como padrão, com atualização quase em tempo real apenas para dados de disponibilidade de estoque e preços que afetem materialmente a experiência do cliente. Monitore as métricas de precisão do conteúdo para determinar se a frequência de atualização é adequada.

**Captura de sinal abrangente vs. sobrecarga de gerenciamento de dados**

A captura de todos os sinais de conversação fornece o enriquecimento e a análise mais avançados do perfil, mas aumenta o volume de dados, os custos de armazenamento e a complexidade da governança.

- **A captura de sinal completo favorece:** Análise avançada, treinamento de modelo de ML, enriquecimento abrangente do perfil e valor máximo de personalização downstream
- **A captura seletiva favorece:** custos de armazenamento mais baixos, governança de dados mais simples, desempenho de pesquisa de perfil mais rápido e conformidade mais fácil com princípios de minimização de dados
- **Recomendação:** comece com a intenção e a captura do sinal de preferência (o meio-termo) e expanda para a captura do sinal completo somente após validar se os dados adicionais criam um valor downstream mensurável. Aplique políticas de expiração do conjunto de dados aos dados de eventos de conversação para gerenciar o crescimento do armazenamento.

## Documentação relacionada

Os recursos a seguir fornecem informações adicionais para implementar esse padrão de caso de uso.

**[!DNL Brand Concierge]**

- [Visão geral do Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [consultor de produtos da Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/product-advisor)
- [supervisor de site do Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/site-advisor)
- [Visão geral do Assistente de IA](https://experienceleague.adobe.com/pt-br/docs/experience-platform/ai-assistant/home)

**[!DNL Adobe Experience Platform]**

- [Visão geral do AEP](https://experienceleague.adobe.com/pt-br/docs/experience-platform/landing/home)
- [Visão geral do sistema XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/home)
- [Noções básicas de composição de esquema](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/schema/composition)
- [Visão geral do Perfil do cliente em tempo real](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/home)

**Integração e coleta de dados**

- [Visão geral do Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/web-sdk/home)
- [Visão geral do Mobile SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Configurar sequências de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/datastreams/configure)
- [Visão geral da API do Edge Network Server](https://experienceleague.adobe.com/pt-br/docs/experience-platform/edge-network-server-api/overview)
- [Visão geral das fontes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/home)

**Identidade e perfil**

- [Visão geral do serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/home)
- [Visão geral dos namespaces de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/namespaces)
- [Visão geral das políticas de mesclagem](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/merge-policies/overview)
- [Visão geral de atributos computados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/computed-attributes/overview)

**Públicos-alvo e segmentação**

- [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/home)
- [Guia da interface do usuário do Construtor de segmentos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/segment-builder)
- [Segmentação de transmissão](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/methods/streaming-segmentation)

**Privacidade e governança de dados**

- [Visão geral da governança de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/home)
- [Grupo de campos Consentimento e preferências](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/field-groups/profile/consents)
- [Visão geral do Privacy Service](https://experienceleague.adobe.com/pt-br/docs/experience-platform/privacy/home)
- [Visão geral do gerenciamento avançado do ciclo de vida dos dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-lifecycle/home)

**Monitoramento e observabilidade**

- [Visão geral dos Insights de observação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/home)
- [Visão geral de alertas](https://experienceleague.adobe.com/pt-br/docs/experience-platform/observability/alerts/overview)

**Analytics e relatórios**

- [Visão geral do CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-overview/cja-overview)
- [Visão geral das conexões do CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-connections/overview)
- [Visão geral das visualizações de dados do CJA](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/data-views)
- [Visão geral do Analysis Workspace](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/home)

**Medidas de proteção**

- [Medidas de proteção do Perfil do cliente em tempo real](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/guardrails)
- [Medidas de proteção de assimilação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/ingestion/guardrails)
- [Proteções de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/guardrails)
