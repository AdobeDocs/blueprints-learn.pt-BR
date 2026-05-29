---
title: Experiência de conversa do Brand Concierge
description: Saiba como transformar propriedades digitais em experiências conversacionais habilitadas por IA e seguras para a marca, que orientam a descoberta do cliente.
solution: Experience Platform, Real-Time Customer Data Platform
exl-id: a9545328-316d-446a-9308-18af61c58d1c
source-git-commit: fe4353cfe34855ad91ccb5698e30030322246c08
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 1%

---

# Experiência conversacional do Brand Concierge

Este guia fornece uma referência de implementação abrangente para experiências conversacionais habilitadas por IA usando o [!DNL Adobe Brand Concierge], integrado com o [!DNL Adobe Experience Platform] (AEP) e o [!DNL Real-Time Customer Data Platform] ([!DNL RT-CDP]). Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam implantar agentes conversacionais seguros para a marca em propriedades digitais.

Abrange todas as abordagens viáveis para implantar experiências conversacionais, desde chatbots de consultoria de produto até assistentes de navegação de site completo, com orientação sobre quando escolher cada opção. O plano aborda a configuração do agente, a governança da marca, a integração de conteúdo, as estratégias de implantação, o enriquecimento do perfil por sinais de conversa e a otimização de análises.

O [!DNL Brand Concierge] permite que as marcas implantem agentes de conversação inteligentes que entendam a voz da marca, acessem catálogos e conteúdo de produtos aprovados, forneçam recomendações personalizadas com base em dados de perfil em tempo real e capturem sinais de intenção e sentimento de volta no perfil unificado do cliente. O resultado é uma experiência de conversação que é natural e sobre a marca, enriquecendo a compreensão da organização de cada cliente.

## Visão geral do caso de uso

As organizações buscam cada vez mais transformar experiências digitais estáticas em conversas dinâmicas alimentadas por IA que orientam os clientes nas decisões de descoberta, seleção de produtos e compra. O [!DNL Adobe Brand Concierge] aborda isso fornecendo uma camada de IA conversacional orquestrada que fica no topo das propriedades digitais existentes, viabilizada pelo AEP Agent Orchestrator.

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
- **[!DNL Adobe Experience Platform](AEP)** — A Unified Data Foundation fornece esquemas XDM, resolução de identidade, perfis de clientes em tempo real e infraestrutura de coleta de dados para sinais de conversação
- **[!DNL Real-Time CDP]([!DNL RT-CDP])** — Plataforma de dados do cliente que fornece pesquisa de perfil em tempo real para conversas personalizadas, segmentação de público a partir de sinais de conversação e enriquecimento de perfil com intenção e dados de sentimento

## Documentação relacionada

Para obter orientação sobre implementação e mais informações, consulte a [visão geral do Brand Concierge](https://experienceleague.adobe.com/en/docs/brand-concierge/content/documentation/overview) na Adobe Experience League.
