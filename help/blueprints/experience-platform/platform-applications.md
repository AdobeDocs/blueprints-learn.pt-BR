---
title: Diagramas da arquitetura de aplicativos e Experience Platform (AEP)
description: Visualizar diagramas de arquitetura que mostram como a Adobe Experience Platform (AEP) está relacionada a outros aplicativos Experience Cloud e serviços de aplicativos.
solution: Experience Platform, Campaign, Analytics, Target, Customer Journey Analytics, Journey Orchestration, Real-Time Customer Data Platform
kt: 7199
thumbnail: null
exl-id: 9b12cd7a-5e5f-443a-91a1-44273cdabc2d
source-git-commit: 9fe44d93dcc05711c77ce1325b6549bb6c27a860
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 89%

---

# Diagramas da arquitetura de aplicativos e Adobe Experience Platform

Esses diagramas de arquitetura mostram como o Experience Platform (AEP) está relacionado a outros aplicativos Experience Cloud e serviços de aplicativos.

>[!MORELIKETHIS]
>
>[Configurações de Integração para Integrações de Aplicativos Experience Cloud](https://experienceleague.adobe.com/docs/integrations-learn/experience-cloud/overview.html?lang=en).


## Diagrama de arquitetura

Este diagrama de arquitetura apresenta como a Adobe Experience Platform se relaciona com aplicativos e serviços de aplicativos da Adobe Experience Cloud.

<img src="assets/aep+apps.svg" alt="Experience Platform e aplicativos" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />

## Diagrama de visão geral

<img src="assets/aep+apps_overview.svg" alt="Experience Platform e aplicativos" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />

## Diagrama detalhado da arquitetura

<img src="assets/aep+apps_detailed.svg" alt="Experience Platform e aplicativos" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />

>[!VIDEO](https://video.tv.adobe.com/v/32456/?quality=12&learn=on)

## Integrações de aplicativos AEP e Experience Cloud

<table class="relative-table wrapped" style="width: 100%;">
<colgroup>
<col style="width: 16.0202%;" />
<col style="width: 29.3423%;" />
<col style="width: 33.5582%;" />
<col style="width: 21.0793%;" />
</colgroup>
<tbody>
<tr>
<th>Aplicativo</th>
<th>Experience Platform para Aplicativo</th>
<th>Aplicativo para Experience Platform</th>
<th>Blueprints relacionados</th>
</tr>
<tr>
<td colspan="1">Ad Cloud</td>
<td colspan="1">
<ul>
<li>Os públicos-alvos definidos na Real-time Customer Data Platform podem ser compartilhados com a Ad Cloud para direcionamento por meio do Audience Manager.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Sem integração atual</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/anonymous.html?lang=pt-BR">Ativação de público-alvo anônima</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=pt-BR">Ativação de cliente conhecido</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=pt-BR">Ativação com a Experience Platform e aplicativos</a></li>
</ul>
</td>
</tr>
<tr>
<td>Analytics</td>
<td>
<ul>
<li>Os dados coletados pelo SDK da Web/Móvel podem ser encaminhados ao Adobe Analytics.</li>
</ul>
</td>
<td>
<ul>
<li>É possível enviar os dados coletados pelo Analytics para o data lake e para o armazenamento de perfis da Experience Platform. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=pt-BR">Conector de dados do Analytics</a></li>
</ul>
</td>
<td>
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-data-flow.html?lang=pt-BR">Fluxos de dados da Experience Platform</a></li>
</ul>
</td>
</tr>
<tr>
<td>Audience Manager</td>
<td>
<ul>
<li>Os públicos-alvos definidos na Real-time Customer Data Platform podem ser compartilhados com o Audience Manager para ativação para destinos de cookies de terceiros.</li>
</ul>
</td>
<td>
<ul>
<li>Os dados coletados e avaliados em conjunto com a associação de público-alvo do Audience Manager podem ser compartilhados com o data lake e o armazenamento de perfis da Experience Platform. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=pt-BR">Conector de origem do Audience Manager</a></li>
</ul>
</td>
<td>
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/anonymous.html?lang=pt-BR">Ativação de público-alvo anônima</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=pt-BR">Ativação de cliente conhecido</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=pt-BR">Ativação com a Experience Platform e aplicativos</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Campaign Classic</td>
<td colspan="1">
<ul>
<li>Os públicos-alvos definidos na Real-time Customer Data Platform podem ser compartilhados com o Campaign Classic como público-alvo a iniciar campanhas.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Os dados de interação e de campanhas coletados pelo Campaign podem ser assimilados na Experience Platform como uma fonte de dados para uso adicional na criação de públicos-alvos e na análise. A criação de públicos-alvo se dá por meio da Real-time Customer Data Platform e a análise se dá por meio do Customer Journey Analytics e do Serviço de consulta da Experience Platform.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/overview.html?lang=pt-BR">Jornadas do cliente</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Campaign Standard</td>
<td colspan="1">
<ul>
<li>Os públicos-alvos definidos na Real-time Customer Data Platform podem ser compartilhados com o Campaign Standard como público-alvo a iniciar campanhas.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Os dados de interação e de campanhas coletados pelo Campaign podem ser assimilados na Experience Platform como uma fonte de dados para uso adicional na criação de públicos-alvos e na análise. A criação de públicos-alvo se dá por meio da Real-time Customer Data Platform e a análise se dá por meio do Customer Journey Analytics e do Serviço de consulta da Experience Platform.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/overview.html?lang=pt-BR">Jornadas do cliente</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Customer Journey Analytics</td>
<td colspan="1">
<ul>
<li>Os dados coletados e assimilados no data lake da Experience Platform são disponibilizados para processamento no Customer Journey Analytics. </li>
<li>Os dados de perfil e público da Real-time Customer Data Platform podem ser assimilados no CJA. <a href="Https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/ingest-aep-segments.html?lang=pt-BR">Integração de RTCDP com CJA</a>.
</li>
</ul>
</ul>
</td>
<td colspan="1">
<ul>
<li>Crie públicos-alvo no Customer Journey Analtyics e compartilhe os resultados do público-alvo na Real-time Customer Data Platform. <a href="https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=pt-BR">Publicação de público-alvo do CJA</a></li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journey-analytics/overview.html?lang=pt-BR">Customer Journey Analytics</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Experience Manager</td>
<td colspan="1">
<ul>
<li>O perfil da Experience Platform pode ser acessado diretamente do lado do servidor para potencializar experiências personalizadas fornecidas por meio do Experience Manager. Observe que as atividades de personalização são mais comumente fornecidas pelo Experience Manager por meio da integração do Target. </li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Nenhuma integração, comportamento e interações atuais executados nos sites do Experience Manager são coletados diretamente pelo SDK móvel e da Web da Experience Platform.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=pt-BR">Ativação de cliente conhecido</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Journey Optimizer</td>
<td colspan="1">
<ul>
<li>Os eventos de dados e os perfis assimilados na Experience Platform são disponibilizados para o Journey Optimizer para inicialização e potencialização de jornadas.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Os dados de interação e de campanhas produzidos pelo Journey Optimizer são coletados para a Experience Platform para uso adicional na criação de públicos-alvos e na análise. A criação de públicos-alvos se dá por meio da Real-time Customer Data Platform e a análise se dá por meio do Customer Journey Analytics e do Serviço de consulta da Experience Platform.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer.html?lang=pt-BR">Journey Optimizer</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Adobe Commerce</td>
<td colspan="1">
<ul>
<li>Perfis e públicos-alvo integrados ao Real-time Customer Data Platform podem ser disponibilizados para personalização no Adobe Commerce. </li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Os dados nativos do Adobe Commerce podem ser enviados para a Experience Platform por meio de um conector de fonte do Adobe Commerce. </li>
</ul>
</td>
<td colspan="1">Sem integração atual</td>
</tr>
<tr>
<td colspan="1">Marketo</td>
<td colspan="1">
<ul>
<li>Os públicos-alvos definidos na Real-time Customer Data Platform podem ser compartilhados com o Marketo como público-alvo a iniciar campanhas do Marketo e atualizar objetos do Marketo.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Contas, contatos e dados de oportunidade do Marketo, juntamente com dados de interação e de campanhas produzidos pelo Marketo são assimilados na Experience Platform para uso adicional na criação de público-alvo por meio de B2B-CDP e para análise por meio do Customer Journey Analytics e do Serviço de consulta da Experience Platform. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo.html?lang=pt-BR">Conector do Marketo Engage</a></li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/b2b-activation/b2bactivation.html?lang=pt-BR">Blueprint de ativação B2B</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Real-Time CDP</td>
<td colspan="1">
<ul>
<li>Os dados assimilados e coletados para a Experience Platform são a fonte de dados para a montagem de perfis de clientes em tempo real que alimentam a Real-time Customer Data Platform.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>As métricas de públicos-alvos e de perfis são enviadas para o data lake da Experience Platform para alimentar os painéis de relatórios de insights do perfil.</li>
<li>É possível usar os dados de públicos-alvos e de perfis no data lake para obter insights adicionais por meio do Serviço de consulta e do Customer Journey Analytics.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=pt-BR">Ativação de cliente conhecido</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=pt-BR">Ativação com a Experience Platform e aplicativos</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Target</td>
<td colspan="1">
<ul>
<li>Os atributos de públicos-alvos e perfil definidos na Real-time Customer Data Platform podem ser compartilhados com o Target e usados em experiências de personalização e direcionamento fornecidas pelo Target.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Os dados coletados para experiências e interações do Target podem ser coletados na Experience Platform por meio do SDK Mobile/Web da Experience Platform. É possível usar esses dados na criação de públicos-alvo por meio da Real-time Customer Data Platform e na análise por meio do Customer Journey Analytics e do Serviço de consulta da Experience Platform.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=pt-BR">Ativação de cliente conhecido</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=pt-BR">Ativação com a Experience Platform e aplicativos</a></li>
</ul>
</td>
</tr>
</tbody>
</table>