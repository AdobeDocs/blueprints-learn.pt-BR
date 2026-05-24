---
title: Casos de uso da orquestração de experiência do cliente, diagramas de arquitetura e blueprints
description: Explore os principais objetivos de negócios, padrões de casos de uso e casos de uso do setor para Adobe Experience Platform e aplicativos. Os diagramas e blueprints da arquitetura visual fornecem referências técnicas para integração do sistema, fluxos de dados e design da solução, conectando o valor comercial à implementação.
doc-type: overview-page
exl-id: 52898310-9723-4ec2-ba10-f45fefe29e93
TQID: https://experienceleague.adobe.com/hScp-97-JZqFMfBJdM6820M95dVE7YoagKJYfruEdao
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: daec7ead-f475-492a-a3b3-02ae08565d6f
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e79d9d6490e4f50c4611dd879b53f0e63a90cd65
workflow-type: tm+mt
source-wordcount: 333
ht-degree: 4%

---

# Casos de uso e diagramas de arquitetura do Customer Experience Orchestration

Este site contém **Objetivos Comerciais Principais**, que descrevem o exemplo de valor comercial principal e os objetivos que podem ser alcançados com o Adobe Experience Platform e os Aplicativos. **Os padrões de caso de uso** descrevem recursos comuns de plataforma e aplicativo com abordagens de implementação repetíveis. **Exemplos de casos de uso do setor** aplicam padrões a cenários comerciais específicos de vertical. **Diagramas e blueprints de arquitetura** são diagramas de referência de fluxo de dados e arquitetura visual que ilustram os pontos de integração do sistema, os fluxos de dados e conteúdo e a sequência de operações, fornecendo uma referência técnica para o design da solução. Juntas, essas camadas conectam o valor comercial à arquitetura e às dependências da implementação.

## Principais objetivos de negócios

Resultados estratégicos que as organizações buscam alcançar por meio de iniciativas de experiência digital. Cada objetivo mapeia para padrões de casos de uso que descrevem como implementar o Adobe Experience Platform e os aplicativos.

<table>
<tr>
  <td><a href="business-objectives/overview.md#acquisition--growth"><strong>Aquisição e crescimento</strong></a></td>
  <td><a href="business-objectives/overview.md#revenue--monetization"><strong>Receita e monetização</strong></a></td>
  <td><a href="business-objectives/overview.md#cost--efficiency"><strong>Custo e eficiência</strong></a></td>
</tr>
<tr>
  <td><a href="business-objectives/overview.md#customer-experience"><strong>Experiência do cliente</strong></a></td>
  <td><a href="business-objectives/overview.md#analytics--insights"><strong>Analytics &amp; Insights</strong></a></td>
  <td><a href="business-objectives/overview.md#qualification--sales-b2b"><strong>Qualificação e vendas (B2B)</strong></a></td>
</tr>
</table>

[Exibir todos os objetivos de negócios](business-objectives/overview.md)

## Padrões de caso de uso

Abordagens de implementação repetíveis que descrevem como alcançar resultados específicos com os recursos associados e os componentes de aplicativos que os fornecem.

<table>
<tr>
  <td><a href="use-case-patterns/overview.md#audience-building--activation"><strong>Criação e ativação de público</strong></a></td>
  <td><a href="use-case-patterns/overview.md#personalization"><strong>Personalização</strong></a></td>
  <td><a href="use-case-patterns/overview.md#campaign-management--orchestration"><strong>Orquestração e gerenciamento de campanhas</strong></a></td>
</tr>
<tr>
  <td><a href="use-case-patterns/overview.md#analysis"><strong>Análise</strong></a></td>
  <td><a href="use-case-patterns/overview.md#conversational-experience"><strong>Experiência de conversa</strong></a></td>
  <td></td>
</tr>
</table>

[Exibir todos os padrões de caso de uso](use-case-patterns/overview.md)

## Veja exemplos de casos de uso por setor

Casos de uso personalizados para setores específicos, cada um mapeado para padrões de implementação e objetivos de negócios.

<table>
<tr>
  <td><a href="industry-use-cases/retail/retail-overview.md"><strong>Varejo</strong></a></td>
  <td><a href="industry-use-cases/financial-services/financial-services-overview.md"><strong>Serviços financeiros</strong></a></td>
  <td><a href="industry-use-cases/healthcare/healthcare-overview.md"><strong>Serviços de saúde</strong></a></td>
</tr>
<tr>
  <td><a href="industry-use-cases/automotive/automotive-overview.md"><strong>Automotivo</strong></a></td>
  <td><a href="industry-use-cases/travel-hospitality/travel-hospitality-overview.md"><strong>Viagens e hospitalidade</strong></a></td>
  <td><a href="industry-use-cases/telecommunications/telecommunications-overview.md"><strong>Telecomunicações</strong></a></td>
</tr>
<tr>
  <td><a href="industry-use-cases/media-entertainment/media-entertainment-overview.md"><strong>Mídia e entretenimento</strong></a></td>
  <td><a href="industry-use-cases/insurance/insurance-overview.md"><strong>Seguro</strong></a></td>
  <td><a href="industry-use-cases/b2b/b2b-overview.md"><strong>B2B</strong></a></td>
</tr>
</table>

[Ver todos os casos de uso do setor](industry-use-cases/use-case-catalog.md)

## Diagramas e blueprints de arquitetura

Diagramas de referência de arquitetura visual e fluxo de dados que ilustram os pontos de integração do sistema, os fluxos de dados e conteúdo e a sequência de operações para o Adobe Experience Platform e os aplicativos.

<table>
<tr>
  <td>
    <a href="experience-platform/guardrails.md">
      <img alt="Arquitetura Experience Platform Hub e Edge" src="experience-platform/assets/aep_edge_hub_latency_v1.svg" />
    </a>
    <div>
      <a href="experience-platform/guardrails.md">
    <strong>Diagrama de Arquitetura e Medidas de Proteção do Experience Platform Hub e Edge</strong>
    </a>
    </div>
  </td>
   <td>
    <a href="experience-platform/deployment/websdk.md">
      <img alt="Diagrama de sequência do Edge" src="experience-platform/deployment/assets/web_sdk_sequence.svg" />
    </a>
    <div>
      <a href="experience-platform/deployment/websdk.md">
    <strong>Diagrama de Sequência do Web SDK e Edge Network</strong>
    </a>
    </div>
  </td>
  <td>
    <a href="customer-journeys/journey-optimizer/journey-optimizer-overview.md">
      <img alt="Diagrama de visão geral do Journey Optimizer" src="customer-journeys/journey-optimizer/images/ajo-architecture.svg" />
    </a>
    <div>
      <a href="customer-journeys/journey-optimizer/journey-optimizer-overview.md">
    <strong>Diagrama de Visão Geral do Adobe Journey Optimizer</strong>
    </a>
    </div>
  </td>
</tr>
</table>