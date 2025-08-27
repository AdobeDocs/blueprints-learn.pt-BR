---
title: '[!DNL Journey Optimizer] - Mensagens acionadas e Blueprint do Adobe Experience Platform'
description: Execute mensagens e experiências acionadas usando a Adobe Experience Platform como um hub central para dados de transmissão, perfis de clientes e segmentação.
solution: Journey Optimizer
source-git-commit: 0a3ebcbc6029df46bd988cb8f15ecf838f80c3c9
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 9%

---

# [!DNL Journey Optimizer] - Blueprint do Jornada

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

[[!DNL Journey Optimizer] Link de Produto de Medidas de Proteção](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails.html)

[Medidas de Proteção e Orientação de Latência de Ponta a Ponta](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=pt-BR)

<br>

## Documentação relacionada

- [[!DNL Experience Platform] documentação](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
- [[!DNL Experience Platform] Documentação de tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)
- [[!DNL Experience Platform Mobile SDK] documentação](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR)
- [[!DNL Journey Optimizer] documentação](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR)
- [[!DNL Journey Optimizer] descrição do produto](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html)