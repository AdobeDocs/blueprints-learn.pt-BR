---
title: Blueprint de ativação de público-alvo e perfil com aplicativos da Experience Cloud
description: Gerencie perfis e públicos-alvos na Experience Platform e compartilhe-os com aplicativos da Experience Cloud.
solution: Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services
kt: 7722
exl-id: f36014e8-170d-47e1-b4ec-10c0ea70612d
source-git-commit: 16ca42fdb944e658bfc1fb3e960e81cd67be049c
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 100%

---

# Blueprint de ativação de público-alvo e perfil com aplicativos da Experience Cloud

Gerencie perfis e públicos-alvos na Experience Platform e compartilhe-os com aplicativos da Experience Cloud. Crie e compartilhe segmentos e insights avançados de clientes na Experience Platform e compartilhe-os com aplicativos da Experience Cloud.

A ativação com aplicativos da Experience Cloud está em sintonia com o [blueprint de ativação de cliente conhecido](known.md).

## Casos de uso

* Personalize e direcione em canais de interação com o cliente impulsionados pela Experience Cloud.
* Compartilhe dados de públicos-alvos e perfis entre a Experience Platform e os aplicativos da Experience Cloud.
* Crie insights avançados a partir de dados de vários canais, incluindo dados comportamentais online e modelos de ciência de dados, para enriquecer o perfil do cliente em tempo real na Experience Platform que pode ser compartilhado com os aplicativos da Experience Cloud.

## Aplicativos

* Adobe Experience Platform
* [!UICONTROL Real-time Customer Data Platform]
* Experience Platform Activation
* Aplicativos da Experience Cloud
   * Adobe Audience Manager
   * Adobe Target
   * Adobe Campaign
   * Journey Optimizer
   * Marketo Engage
   * Adobe Commerce
   * Customer Journey Analytics

## Arquitetura

Consulte a seção [Experience Platform e Arquitetura de aplicativos](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=pt-BR) para obter diagramas de arquitetura adicionais relacionados a integrações da Experience Platform com aplicativos da Experience Cloud.

### Ativação de público-alvo e perfil com aplicativos da Experience Cloud

<img src="../experience-platform/assets/aep+apps.svg" alt="Arquitetura de referência para a ativação de público-alvo e perfil com aplicativos da Experience Cloud" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />
<br>

## Medidas de proteção

Consulte as [medidas de proteção na página de Visão geral de ativação de público-alvo e perfil](overview.md)   E a página de [medidas de proteção da implantação](../experience-platform/deployment/guardrails.md).

## Considerações de implementação

* Compartilhar dados de perfil com destinos exige a inclusão de valor específico de identidade, usado pelo destino na carga de destino. Qualquer identidade necessária para um destino de público-alvo deve ser assimilada na Platform e configurada como uma identidade para o [!UICONTROL Perfil de cliente em tempo real].

### Compartilhamento de públicos do Real-time Customer Data Platform para o Audience Manager

* Consulte a documentação a seguir para obter mais detalhes. [Compartilhamento de segmentos da Experience Platform com o Audience Manager e outras soluções da Experience Cloud](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=pt-BR).

* A associação de públicos do RTCDP é compartilhada com o Audience Manager de forma contínua assim que a avaliação de segmento é concluída e gravada no perfil do Cliente em tempo real, independentemente de a avaliação de segmento ter ocorrido em lote ou por transmissão.
* Se o perfil qualificado contiver as informações de roteamento regional para dispositivos de perfil relacionados, a associação de públicos do RTCDP será qualificada de forma contínua no Audience Manager Edge associado. Se as informações de roteamento regional foram aplicadas a um perfil com um carimbo de data e hora nos últimos 14 dias, elas serão avaliadas no Audience Manager Edge por transmissão. Se os perfis da RTCDP não contiverem informações de roteamento regional ou se tais informações tiverem mais de 14 dias, as associações de público serão enviadas para o local do hub do Audience Manager para avaliação e ativação baseadas em lote.
* Com informações de roteamento regional, esses perfis estão qualificados para ativação do Edge e serão ativados minutos depois da qualificação de segmento da RTCDP. Os perfis que não se qualificarem para ativação do Edge serão qualificados no hub do Audience Manager, e o processamento poderá levar de 12 a 24 horas.
* As informações de roteamento regional para as quais o Edge do perfil do Audience Manager é armazenado podem ser coletadas para a Experience Platform a partir do Audience Manager, do Serviço de ID de visitante, do Analytics, do Adobe Experience Platform Launch ou diretamente do SDK da Web como um conjunto de dados de classe de registro de perfil independente usando o grupo de campos XDM “informações da região de captura de dados”. Consulte o documento Obter informações regionais para saber mais [Link](https://experienceleague.adobe.com/docs/id-service/using/reference/regions.html?lang=pt-BR).
* Para cenários de ativação em que os públicos são compartilhados da Experience Platform para o Audience Manager, as seguintes identidades são compartilhadas automaticamente: ECID, IDFA, GAID, endereços de e-mail com hash (EMAIL_LC_SHA256), AdCloud ID. Atualmente, os namespaces personalizados não são compartilhados.
* É possível compartilhar os públicos da Experience Platform por meio dos destinos do Audience Manager, quando as identidades de destino necessárias estiverem incluídas no [!UICONTROL Perfil de cliente em tempo real]. Ou também onde as identidades no [!UICONTROL Perfil de cliente em tempo real] possam ser relacionadas às identidades de destino vinculadas ao Audience Manager.

### Compartilhamento de públicos-alvo da Real-time Customer Data Platform com o Target

* Consulte o [Blueprint de Personalização conhecida do cliente – Target e RTCDP](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/web-personalization/known-personalization.html?lang=pt-BR) para obter mais detalhes sobre o compartilhamento de públicos-alvo e perfis da Real-time Customer Data Platform com o Target.

### Compartilhamento de públicos-alvo da Real-time Customer Data Platform com o Campaign e o Journey Optimizer

* Consulte os [Blueprints de jornadas do cliente](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/b2b-activation/b2bactivation.html?lang=pt-BR) para obter mais detalhes sobre o compartilhamento de públicos-alvo e perfis da Real-time Customer Data Platform com o Campaign e o Journey Optimizer.

### Compartilhamento de públicos da Real-time Customer Data Platform para o Marketo Engage

* Consulte os [Blueprints de ativação B2B](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/b2b-activation/b2bactivation.html?lang=pt-BR) para obter mais informações sobre o compartilhamento de públicos e perfis da Real-time Customer Data Platform com o Marketo Engage.

### Compartilhamento de públicos da Real-time Customer Data Platform com o Customer Journey Analytics

* Consulte [Públicos da RTCDP compartilhados com o Customer Journey Analytics](Https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/ingest-aep-segments.html?lang=pt-BR) para obter mais informações sobre o compartilhamento de públicos da Real-time Customer Data Platform com o Customer Journey Analytics.

## Documentação relacionada

* Descrição do produto [[!UICONTROL Real-time Customer Data Platform]](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform.html)
* [Guias de perfil e segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)
* [Documentação de segmentação](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=pt-BR)
* [Documentação de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=pt-BR)

## Vídeos e tutoriais relacionados

* Visão geral da [[!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=pt-BR)
* [Demonstração da [!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=pt-BR)
* [Criação de segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=pt-BR)
