---
title: Diagramas de arquitetura
description: Diagramas de referência de arquitetura visual e fluxo de dados para Adobe Experience Platform e aplicativos, abrangendo arquitetura de plataforma, ativação de público-alvo, marketing B2B, insights do cliente e jornadas do cliente.
solution: Experience Platform
doc-type: overview-page
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 1d6ba1444c119437eb8a86d5c4a1050d56d16023
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%
---
# Diagramas de arquitetura

Os diagramas de arquitetura são referências visuais e técnicas que mostram como o Adobe Experience Platform e os aplicativos se encaixam — pontos de integração do sistema, fluxos de dados e conteúdo e sequência de operações. Use-as para entender o design da solução antes de mergulhar na orientação passo a passo em [padrões de caso de uso](/help/blueprints/use-case-patterns/overview.md).

Os diagramas estão organizados nas seguintes categorias. Selecione um cartão para ir até a página de aterrissagem ou o diagrama de leads dessa categoria — use a navegação à esquerda para navegar em cada diagrama dentro de uma categoria.

<table style="table-layout:fixed; width:100%;">
<tr>
  <td style="width:33%; vertical-align:top; padding:10px; box-sizing:border-box;">
    <a href="architecture-overviews/overview.md">
      <img alt="Visão geral da arquitetura" src="architecture-overviews/assets/aep_apps_overview.png" style="display:block; width:100%; height:160px; object-fit:contain; background-color:#ffffff; border:1px solid #d3d3d3; padding:10px; box-sizing:border-box;" />
    </a>
    <div style="min-height:100px;">
      <a href="architecture-overviews/overview.md">
        <strong>Visão geral da arquitetura</strong>
      </a>
      <p>Como os aplicativos da Experience Cloud, o Experience Platform e os SDKs de implantação se encaixam, além de medidas de proteção e latências.</p>
    </div>
  </td>
  <td style="width:33%; vertical-align:top; padding:10px; box-sizing:border-box;">
    <a href="audience-profile-activation/overview.md">
      <img alt="Ativação de público-alvo e perfil" src="audience-profile-activation/assets/real_time_cdp_activation.png" style="display:block; width:100%; height:160px; object-fit:contain; background-color:#ffffff; border:1px solid #d3d3d3; padding:10px; box-sizing:border-box;" />
    </a>
    <div style="min-height:100px;">
      <a href="audience-profile-activation/overview.md">
        <strong>Ativação de público-alvo e perfil</strong>
      </a>
      <p>Como públicos e perfis são criados no Adobe Real-Time CDP e ativados para destinos e aplicativos.</p>
    </div>
  </td>
  <td style="width:33%; vertical-align:top; padding:10px; box-sizing:border-box;">
    <a href="b2b-activation-marketing/overview.md">
      <img alt="Ativação e marketing B2B" src="b2b-activation-marketing/assets/b2b-audience-profile-activation.png" style="display:block; width:100%; height:160px; object-fit:contain; background-color:#ffffff; border:1px solid #d3d3d3; padding:10px; box-sizing:border-box;" />
    </a>
    <div style="min-height:100px;">
      <a href="b2b-activation-marketing/overview.md">
        <strong>Ativação e marketing B2B</strong>
      </a>
      <p>Ativação de público com base em contas e pessoas com o Real-Time Customer Data Platform B2B edition em canais e destinos.</p>
    </div>
  </td>
</tr>
<tr>
  <td style="width:33%; vertical-align:top; padding:10px; box-sizing:border-box;">
    <a href="customer-insights/overview.md">
      <img alt="Insights do cliente" src="customer-insights/assets/cja.png" style="display:block; width:100%; height:160px; object-fit:contain; background-color:#ffffff; border:1px solid #d3d3d3; padding:10px; box-sizing:border-box;" />
    </a>
    <div style="min-height:100px;">
      <a href="customer-insights/overview.md">
        <strong>Insights do cliente</strong>
      </a>
      <p>Como o Customer Journey Analytics unifica e analisa dados comportamentais entre canais e se integra ao Real-Time CDP e ao Journey Optimizer.</p>
    </div>
  </td>
  <td style="width:33%; vertical-align:top; padding:10px; box-sizing:border-box;">
    <a href="customer-journeys/journey-optimizer/journey-optimizer-overview.md">
      <img alt="Jornadas do cliente" src="customer-journeys/journey-optimizer/images/ajo-architecture.png" style="display:block; width:100%; height:160px; object-fit:contain; background-color:#ffffff; border:1px solid #d3d3d3; padding:10px; box-sizing:border-box;" />
    </a>
    <div style="min-height:100px;">
      <a href="customer-journeys/journey-optimizer/journey-optimizer-overview.md">
        <strong>jornadas para clientes</strong>
      </a>
      <p>Orquestração de jornadas orientada por eventos com o Journey Optimizer, decisão sobre a borda e o hub e orquestração em lote com o Adobe Campaign.</p>
    </div>
  </td>
  <td style="width:33%; vertical-align:top; padding:10px; box-sizing:border-box;"></td>
</tr>
</table>

## Conteúdo relacionado

* [Padrões de caso de uso](/help/blueprints/use-case-patterns/overview.md) — abordagens de implementação repetíveis que utilizam essas arquiteturas
* [Principais objetivos comerciais](/help/blueprints/business-objectives/overview.md) — os resultados comerciais dessas arquiteturas o ajudam a alcançar
* [Casos de uso do setor](/help/blueprints/industry-use-cases/use-case-catalog.md) — aplicações específicas verticais desses padrões
