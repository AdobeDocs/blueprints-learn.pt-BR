---
title: Ativação com o blueprint de dados online e offline
description: Ativação de público-alvo online/offline.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
source-git-commit: c4adcc5d23bb0482a348d7b5b2b70b06ff2873e8
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 79%

---

# Ativação com o blueprint de dados online e offline

Use atributos e eventos offline, como pedidos, transações, CRM ou dados de fidelização offline, com comportamentos online para direcionamento e personalização online.

Ative públicos para destinos conhecidos com base no perfil, como provedores de email, redes sociais e destinos de publicidade.

A ativação com o blueprint de dados online e offline está em sintonia com o [Blueprint de ativação de público e perfil com aplicativos da Experience Cloud](platform-and-applications.md). Detalhes adicionais são fornecidos no [Blueprint de ativação de público e perfil com aplicativos da Experience Cloud](platform-and-applications.md), específico para integrações entre a Experience Platform e os aplicativos da Experience Cloud.

## Casos de uso

* Direcionamento de públicos para públicos conhecidos em destinos sociais e de publicidade.
* Personalização online com atributos online e offline.
* Ative públicos para canais conhecidos, como email e SMS.

## Aplicativos

* Adobe Experience Platform
* [!UICONTROL Real-time Customer Data Platform]

## Arquitetura

### Ativação com dados online e offline com destinos

<img src="assets/online_offline_activation.svg" alt="Arquitetura de referência para o blueprint de ativação de público-alvo online/offline" style="width:80%; border:1px solid #4a4a4a" />
<br>

## Medidas de proteção

[Consulte as medidas de proteção descritas na página de Visão geral de ativação de público e perfil.](overview.md)

## Etapas de implementação

1. [Crie esquemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) para que os dados sejam assimilados.
1. [Crie conjuntos de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) para que os dados sejam assimilados.
1. [Configure as identidades corretas e os namespaces de identidade](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=pt-BR) no esquema para assegurar que os dados assimilados possam aderir a um perfil unificado.
1. [Habilite os esquemas e conjuntos de dados para o perfil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=pt-BR).
1. [Assimile dados](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=pt-BR) na Experience Platform.
1. [Forneça compartilhamento de segmentos da [!UICONTROL Real-time Customer Data Platform]](https://www.adobe.com/go/audiences) entre a Experience Platform e o Audience Manager. Assim, os públicos definidos na Experience Platform podem ser compartilhados com o Audience Manager.
1. [Crie segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=pt-BR) na Experience Platform. O sistema decide automaticamente se o segmento é avaliado em lote ou por streaming.
1. [Configure destinos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html?lang=pt-BR) para compartilhar atributos de perfil e associações de públicos com destinos desejados.

## Considerações de implementação

* Compartilhar dados de perfil com destinos exige a inclusão de valor específico de identidade, usado pelo destino na carga de destino. Qualquer identidade necessária para um destino de público-alvo deve ser assimilada na Platform e configurada como uma identidade para o [!UICONTROL Perfil de cliente em tempo real].

### Compartilhamento de públicos do Real-time Customer Data Platform para o Audience Manager

* A associação de públicos do RTCDP é compartilhada com o Audience Manager de forma contínua assim que a avaliação de segmento é concluída e gravada no perfil do Cliente em tempo real, independentemente de a avaliação de segmento ter ocorrido em lote ou por streaming. Se o perfil qualificado contiver as informações de roteamento regional para dispositivos de perfil relacionados, a associação de públicos do RTCDP será qualificada de forma contínua no Audience Manager Edge associado. Se as informações de roteamento regional foram aplicadas a um perfil com um carimbo de data e hora nos últimos 14 dias, elas serão avaliadas no Audience Manager Edge em streaming. Se os perfis do RTCDP não contiverem informações de roteamento regional ou se as informações de roteamento regional tiverem mais de 14 dias, as associações de perfil serão enviadas para o local do hub Audience Manager para avaliação e ativação baseadas em lote. Os perfis qualificados para ativação do Edge serão ativados dentro de minutos da qualificação de segmento do RTCDP, os perfis que não se qualificarem para ativação do Edge serão qualificados no hub do Audience Manager e podem ter um período de 12 a 24 horas para processamento.

* As informações de roteamento regional para as quais o Edge do perfil do Audience Manager é armazenado podem ser coletadas para o Experience Platform a partir do Audience Manager, do Serviço de ID do visitante, do Analytics, do Launch ou diretamente do SDK da Web como um conjunto de dados de classe de registro de perfil separado usando o grupo de campos XDM &quot;informações da região de captura de dados&quot;.

* Para cenários de ativação em que os públicos são compartilhados da Experience Platform para o Audience Manager, as seguintes identidades são compartilhadas automaticamente: IDFA, GAID, AdCloud, Google, ECID e EMAIL_LC_SHA256. Atualmente, os namespaces personalizados não são compartilhados.

É possível compartilhar os públicos da Experience Platform por meio dos destinos do Audience Manager, quando as identidades de destino necessárias estiverem incluídas no [!UICONTROL Perfil de cliente em tempo real]. Ou também onde as identidades no [!UICONTROL Perfil de cliente em tempo real] possam ser relacionadas às identidades de destino vinculadas ao Audience Manager.

## Documentação relacionada

* Descrição do produto [[!UICONTROL Real-time Customer Data Platform]](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform.html)
* [Guias de perfil e segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)
* [Documentação de segmentação](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=pt-BR)
* [Documentação de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=pt-BR)

## Vídeos e tutoriais relacionados

* Visão geral da [[!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=pt-BR)
* [Demonstração da [!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=pt-BR)
* [Criação de segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
