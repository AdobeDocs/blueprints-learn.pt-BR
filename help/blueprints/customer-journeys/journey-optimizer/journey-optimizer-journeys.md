---
title: '[!DNL Journey Optimizer] - Mensagens acionadas e Blueprint do Adobe Experience Platform'
description: Execute mensagens e experiências acionadas usando a Adobe Experience Platform como um hub central para dados de transmissão, perfis de clientes e segmentação.
solution: Journey Optimizer
exl-id: 70573eb9-cd69-4fe6-b2ae-dae81665a308
TQID: https://experienceleague.adobe.com/MuodOvJ52G9lmUAmsuj06q1aTXkRg7W0Bj6nxLp96N8
product_v2:
  - id: cb954087-f4fc-4456-afb9-e939cabcdc79
feature_v2:
  - id: a653cc2e-bc85-4353-a306-399e5b247978
  - id: d998adac-2f81-400b-a669-d07bb196e4eb
  - id: fe338112-e2ce-4876-8989-fc4d497613f1
  - id: fe96aceb-8194-4a8a-a6b0-75302d02804d
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: 357
ht-degree: 12%

---

# [!DNL Journey Optimizer] - Blueprint do Jornada

>[!TIP]
>Este blueprint também está disponível como um [padrão de caso de uso](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) em Gerenciamento e orquestração de campanhas.

As Jornadas do Adobe Journey Optimizer são fluxos de trabalho em tempo real orientados por eventos que fornecem experiências personalizadas em várias etapas com base em comportamentos individuais do cliente. Eles são compatíveis com uma grande variedade de canais, incluindo email, SMS, notificações por push, mensagens no aplicativo, experiências baseadas em código e integrações personalizadas baseadas em API, permitindo que as marcas envolvam os clientes de forma contextual em seus pontos de contato preferidos.

<br>

## Arquitetura

<img src="images/ajo-journeys-architecture.svg" alt="Arquitetura de referência Adobe Journey Optimizer - Blueprint do Jornada" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Considerações de arquitetura para Jornadas

- **Atualização do perfil**: o AJO Jornada depende de atualizações em tempo real para o perfil do cliente. Verifique se as fontes de dados que alimentam o Adobe Experience Platform (AEP) estão configuradas para assimilação de baixa latência para manter a precisão do perfil.
- **Processamento de Evento Escalável** Verifique se a infraestrutura pode manipular grandes volumes de disparadores de jornada e entrega de mensagens.
- **Integração modular:** crie APIs e ações personalizadas para conectar o AJO a sistemas externos para personalização dinâmica.
- **Resolução de identidade**: a compilação precisa de identidades de clientes entre dispositivos e canais é essencial. Identidades desalinhadas podem levar a jornadas quebradas ou mal direcionadas.
- **Tempo de qualificação de segmento**: as jornadas baseadas em público-alvo dependem da associação do segmento. Entenda a frequência com que os segmentos são avaliados e como esse tempo afeta a entrada e a personalização da jornada.
- **Condições de Entrada da Jornada**: os perfis devem atender a condições específicas para entrar em uma jornada. Essas condições devem ser cuidadosamente projetadas para evitar exclusões ou sobreposições não intencionais.
- **Avaliação de público-alvo e latência**: as etapas de leitura de público-alvo dependem das avaliações de segmento no Adobe Experience Platform, que podem não ocorrer em tempo real. Crie jornadas com percepção da frequência e latência de avaliação para evitar atrasos na qualificação do público-alvo e garantir a personalização oportuna.

<br>

## Medidas de proteção

[Link de produto das Medidas de proteção do [!DNL Journey Optimizer]](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails.html)

[Medidas de proteção e orientação de latência completa](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

<br>

## Documentação relacionada

- [Documentação do [!DNL Experience Platform]](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
- [Documentação de [!DNL Experience Platform] tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)
- [Documentação do [!DNL Experience Platform Mobile SDK]](https://experienceleague.adobe.com/docs/mobile.html)
- [Documentação do [!DNL Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html)
- [Descrição do produto [!DNL Journey Optimizer]](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html)
