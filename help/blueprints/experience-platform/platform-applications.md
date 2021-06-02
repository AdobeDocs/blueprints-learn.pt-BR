---
title: Adobe Experience Platform e Diagrama de arquitetura de aplicativos
description: Este diagrama de arquitetura apresenta como a Adobe Experience Platform se relaciona com outros aplicativos e serviços de aplicativos da Adobe Experience Cloud.
solution: Experience Platform, Campaign, Analytics, Target, Customer Journey Analytics, Journey Orchestration, Offer Decisioning, Real-time Customer Data Platform
kt: 7199
thumbnail: null
exl-id: 9b12cd7a-5e5f-443a-91a1-44273cdabc2d
source-git-commit: 70b3bf294741888c3d109a2d4ef710d428800abf
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 11%

---

# Adobe Experience Platform e aplicativos

## Adobe Experience Platform e Diagrama de arquitetura de aplicativos

Este diagrama de arquitetura apresenta como a Adobe Experience Platform se relaciona com aplicativos e serviços de aplicativos da Adobe Experience Cloud.

<img src="assets/aep+apps_vertical.svg" alt="Experience Platform e Aplicativos" style="border:1px solid #4a4a4a" />

>[!VIDEO](https://video.tv.adobe.com/v/32456/?quality=12&learn=on)

## Adobe Experience Platform e diagrama detalhado de arquitetura de aplicativos

<img src="assets/aep+apps_horizontal.svg" alt="Experience Platform e Aplicativos" style="border:1px solid #4a4a4a" />

## Integrações de aplicativos Adobe Experience Platform e Experience Cloud

<table class="relative-table wrapped" style="width: 100%;" >
   <colgroup>
    <col style="width: 16.0202%;"/>
    <col style="width: 29.3423%;"/>
    <col style="width: 33.5582%;"/>
    <col style="width: 21.0793%;"/>
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
          <li>Os públicos-alvo definidos na Real-time Customer Data Platform podem ser compartilhados com a Ad Cloud para direcionamento via Audience Manager.</li>
        </ul>
      </td>
      <td colspan="1">Sem integração atual</td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/anonymous.html?lang=en">Ativação de público-alvo anônima</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">Ativação de público-alvo online/offline</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Ativação com Experience Platform e aplicativos</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>Analytics</td>
      <td>Sem integração atual</td>
      <td>
        <ul>
          <li>Os dados coletados pelo Analytics podem ser enviados para o data lake do Experience Platform e o armazenamento de perfis. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=en">Conector de dados do Analytics</a>
          </li>
        </ul>
      </td>
      <td>
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-data-flow.html?lang=en">Fluxos de dados Experience Platform</a>
          </li>
        </ul>
        <p>
          <br/>
        </p>
      </td>
    </tr>
    <tr>
      <td>Audience Manager</td>
      <td>
        <ul>
          <li>Os públicos-alvo definidos na Plataforma de dados do cliente em tempo real podem ser compartilhados com o Audience Manager para ativação para destinos de cookies de terceiros.</li>
        </ul>
      </td>
      <td>
        <ul>
          <li>Os dados coletados e avaliados da associação do público-alvo podem ser compartilhados com o Experience Platform data lake e o armazenamento de perfil. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=en">Conector de origem do Audience Manager</a>
          </li>
        </ul>
      </td>
      <td>
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/anonymous.html?lang=en">Ativação de público-alvo anônima</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">Ativação de público-alvo online/offline</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Ativação com Experience Platform e aplicativos</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Campaign Classic</td>
      <td colspan="1">
        <ul>
          <li>Os públicos-alvo definidos na Real-time Customer Data Platform podem ser compartilhados com o Campaign Classic como o público-alvo para iniciar campanhas.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>Os dados de interação e campanha coletados pelo Campaign podem ser assimilados ao Experience Platform como fonte de dados para uso adicional na criação de público-alvo por meio da Plataforma de dados do cliente em tempo real e da análise por meio do Serviço de consulta do Customer Journey Analytics e Experience Platform e do Data Science Workspace.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/multi-channel-message-orchestration/batch-messaging.html?lang=en">Mensagens em lote</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Campaign Standard</td>
      <td colspan="1">
        <ul>
          <li>Os públicos-alvo definidos na Real-time Customer Data Platform podem ser compartilhados com o Campaign Standard como o público-alvo para iniciar campanhas.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>Os dados de interação e campanha coletados pelo Campaign podem ser assimilados ao Experience Platform como fonte de dados para uso adicional na criação de público-alvo por meio da Plataforma de dados do cliente em tempo real e da análise por meio do Serviço de consulta do Customer Journey Analytics e Experience Platform e do Data Science Workspace.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/multi-channel-message-orchestration/batch-messaging.html?lang=en">Mensagens em lote</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Customer Journey Analytics</td>
      <td colspan="1">
        <ul>
          <li>Os dados coletados e assimilados no Experience Platform data lake são disponibilizados para processamento em Customer Journey Analytics. </li>
        </ul>
      </td>
      <td colspan="1">Não há integração atual disponível. A capacidade de compartilhar os resultados do público-alvo no Experience Platform a partir do Customer Journey Analytics está no roteiro.</td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journey-analytics/overview.html?lang=en">Customer Journey Analytics</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Experience Manager</td>
      <td colspan="1">
        <ul>
          <li>O perfil do Experience Platform pode ser acessado diretamente do lado do servidor para potencializar experiências personalizadas entregues por meio do Experience Manager. Observe que as atividades de personalização são mais comumente fornecidas via Experience Manager por meio da integração do Target. </li>
        </ul>
      </td>
      <td colspan="1">Nenhuma integração, comportamento e interações atuais executados em sites do Experience Manager são coletados diretamente pelo Experience Platform Web e Mobile SDK.</td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">Ativação de público-alvo online/offline</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Journey Optimizer</td>
      <td colspan="1">
        <ul>
          <li>Os eventos de dados e os perfis assimilados no Experience Platform são disponibilizados para a Journey Optimizer iniciar e ativar o jornada no Journey Optimizer.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>Os dados de interação e campanha produzidos pela Journey Optimizer são coletados no Experience Platform para uso adicional na criação de públicos-alvo por meio da Plataforma de dados do cliente em tempo real e da análise por meio do Customer Journey Analytics, do Experience Platform Query Service e do Data Science Workspace.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/multi-channel-message-orchestration/triggered-messaging.html?lang=en">Mensagens acionadas</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Magento</td>
      <td colspan="1">Sem integração atual</td>
      <td colspan="1">Sem integração atual</td>
      <td colspan="1">Sem integração atual</td>
    </tr>
    <tr>
      <td colspan="1">Marketo</td>
      <td colspan="1">
        <ul>
          <li>Os públicos-alvo definidos na Real-time Customer Data Platform podem ser compartilhados com o Marketo como o público-alvo para iniciar campanhas do Marketo e atualizar objetos do Marketo.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>Contas, contatos e dados de oportunidade do Marketo, juntamente com dados de interação e campanha produzidos pela Marketo são assimilados no Experience Platform para uso adicional na criação de público-alvo por meio da B2B-CDP e análise via Customer Journey Analytics, serviço de consulta do Experience Platform e espaço de trabalho da ciência de dados. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo.html?lang=en">Conector Marketo Engage</a>
          </li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>Ativação B2B - em desenvolvimento</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">CDP em tempo real</td>
      <td colspan="1">
        <ul>
          <li>Os dados assimilados e coletados no Experience Platform são a fonte de dados para a montagem de perfis de clientes em tempo real que alimentam a Plataforma de dados do cliente em tempo real.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>As métricas de Público-alvo e Perfil são enviadas para o lago de dados do Experience Platform para alimentar os painéis de relatório de insight de perfil.</li>
          <li>Os dados de Público-alvo e Perfil no lago de dados podem ser usados para obter mais insights por meio do Serviço de query, do Data Science Workspace e do Customer Journey Analytics.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">Ativação de público-alvo online/offline</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Ativação com Experience Platform e aplicativos</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Target</td>
      <td colspan="1">
        <ul>
          <li>Os públicos-alvo definidos na Plataforma de dados do cliente em tempo real podem ser compartilhados com o Target e usados em experiências de personalização e direcionamento fornecidas pelo Target. </li>
          <li>A integração do Direct Experience Edge com o Target para associação de segmento em tempo real e acesso a atributos de perfil está no roteiro.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>Os dados coletados para experiências e interações do Target podem ser coletados no Experience Platform por meio do SDK da Web do Experience Platform. Esses dados podem ser usados na criação de públicos-alvo por meio da Real-time Customer Data Platform e para análise via Customer Journey Analytics,  Experience Platform Query Service e Data Science Workspace.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">Ativação de público-alvo online/offline</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Ativação com Experience Platform e aplicativos</a>
          </li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>
