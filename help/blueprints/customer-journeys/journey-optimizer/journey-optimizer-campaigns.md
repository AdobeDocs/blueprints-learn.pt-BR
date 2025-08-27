---
title: '[!DNL Journey Optimizer] - Orquestração de campanha'
description: Permite que os profissionais de marketing coordenem comunicações de marketing programadas, baseadas em públicos-alvo e em várias etapas em canais de mensagens de saída.
solution: Journey Optimizer
source-git-commit: 0a3ebcbc6029df46bd988cb8f15ecf838f80c3c9
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 2%

---

# [!DNL Journey Optimizer] - Blueprint da orquestração de campanha

O AJO Campaign Orchestration permite que os profissionais de marketing criem e executem comunicações programadas, baseadas em públicos, em várias etapas, entre canais de saída, como email, SMS, push e correspondência direta. Ao contrário do AJO Jornada, que reage a comportamentos individuais dos clientes usando dados em tempo real do Perfil do cliente em tempo real, as campanhas são esforços de marketing coordenados que direcionam os públicos em intervalos planejados. Juntas, campanhas e jornadas oferecem abordagens complementares — as campanhas impulsionam estratégias de envolvimento com a marca, enquanto as jornadas fornecem experiências personalizadas e responsivas.

<br>

## Arquitetura

<img src="images/ajo-campaigns-architecture.svg" alt="Arquitetura de referência Blueprint do Adobe Journey Optimizer Campaign Orchestration" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

### Arquitetura de execução de mensagens

<img src="images/ajo-campaigns-message-sending-architecture.png" alt="Arquitetura de referência Blueprint do Adobe Journey Optimizer Campaign Orchestration" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

### Armazenamento relacional - Latência de assimilação de dados

<img src="images/ajo-campaigns-data-ingestion-architecture.png" alt="Arquitetura de referência Blueprint do Adobe Journey Optimizer Campaign Orchestration" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Considerações de arquitetura para Jornadas

- **Arquitetura de dados**: a Orquestração do AJO Campaign utiliza um banco de dados relacional subjacente para a criação e a orquestração de públicos-alvo
- **Integração com o Audience Portal**: integrado nativamente ao Audience Portal dentro do Perfil do Cliente em Tempo Real para ler de públicos existentes e salvar novos públicos ao criar campanhas
- **Criação de público-alvo sob demanda**: compile, avalie e execute um público-alvo imediatamente para casos de uso urgentes de marketing
- **Integração do Perfil do Cliente em Tempo Real:** fonte da verdade para o histórico de consentimento e comunicação; oferece suporte ao design de &quot;perfil reduzido&quot; para personalização
- **Envio de Mensagens de Várias Entidades:** capacidade de enviar várias mensagens por perfil em uma única entrega (por exemplo, enviar uma mensagem por reserva para o endereço de email do cliente)
- **Segmentação de várias entidades**: comece a criar um público-alvo a partir de qualquer entidade dentro do armazenamento relacional (ou seja, produto, inventário, plano etc.)

<br>

## Medidas de proteção

[Link de Produto de Campanhas Orquestradas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/orchestrated-campaigns/guardrails)

[Medidas de Proteção e Orientação de Latência de Ponta a Ponta](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails)

<br>

## Documentação relacionada

- [[!DNL Journey Optimizer] Campanhas orquestradas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/orchestrated-campaigns/orchestrated-campaigns-landing-page.html)
- [[!DNL Experience Platform] documentação](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
- [[!DNL Experience Platform] Documentação de tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)
- [[!DNL Experience Platform Mobile SDK] documentação](https://experienceleague.adobe.com/docs/mobile.html)
- [[!DNL Journey Optimizer] documentação](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html)
- [[!DNL Journey Optimizer] descrição do produto](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html)