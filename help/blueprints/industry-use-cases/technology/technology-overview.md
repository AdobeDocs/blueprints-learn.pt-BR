---
title: Casos de uso de tecnologia
description: Descubra como as organizações de tecnologia usam o Adobe Experience Platform para unificar a coleta de dados, encaminhar eventos em tempo real, análise de energia e ativação em produtos digitais.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: a1b2c3d4-e5f6-7890-abcd-ef1234567890
source-git-commit: 77908fd8a9f4309cbe66063cd33f065424697e55
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# Casos de uso de tecnologia

As organizações de tecnologia usam o Adobe Experience Platform para centralizar a coleta de dados das superfícies da Web, móvel e de produtos e distribuir eventos em tempo real para os destinos de análise, data warehouse e ativação que potencializam seus produtos e programas de marketing. Ao consolidar a coleta de eventos na borda, as equipes de tecnologia reduzem a complexidade do lado do cliente, melhoram a qualidade dos dados e garantem que todos os sistemas downstream recebam dados comportamentais consistentes de uma única fonte autorizada.

## Encaminhamento de eventos em tempo real

Encaminhe eventos comportamentais em tempo real coletados por meio do Edge Network para análises de terceiros, data warehouses e plataformas de parceiros para enriquecimento e ativação. A centralização da coleta de eventos na borda e do encaminhamento para vários destinos reduz a sobrecarga de tags do lado do cliente, melhora a qualidade dos dados e garante que todos os sistemas downstream recebam dados de eventos consistentes de uma única fonte autorizada.

### Impacto no negócio

As organizações de tecnologia que implementam o encaminhamento de eventos em tempo real reduzem a carga de tags do lado do cliente e a sobrecarga de desempenho associada, ao mesmo tempo que melhoram a consistência dos dados do evento nos destinos de análise, data warehouse e ativação. O encaminhamento pelo lado do servidor também reduz o peso da página e melhora o desempenho da carga, beneficiando diretamente as métricas de experiência do usuário.

### Como implementar o

Use o padrão [Encaminhamento de Eventos](/help/blueprints/use-case-patterns/audience-building-activation/event-forwarding.md) para rotear eventos coletados pelo Adobe Experience Platform Web SDK por meio da Edge Network para destinos configurados do lado do servidor. Esse é o padrão correto quando o objetivo é a distribuição de eventos de servidor para servidor a partir de um único ponto de coleta, em vez de gerenciar tags separadas para cada destino no lado do cliente, o que aumenta o peso da página e cria inconsistência de dados entre os sistemas.

### Considerações técnicas

- O encaminhamento de eventos do Edge Network requer a migração da coleção de eventos para o Adobe Experience Platform Web SDK ou o Mobile SDK. As implementações existentes baseadas em tags devem ser avaliadas quanto à compatibilidade antes que os destinos de encaminhamento sejam configurados.
- As regras de encaminhamento devem ser configuradas para enviar somente os campos exigidos por cada destino — evite encaminhar cargas XDM completas para destinos que precisam apenas de um pequeno subconjunto de campos, pois isso aumenta os custos de transferência de dados e cria exposição à conformidade.
- Os conectores de destino devem lidar com a falha normalmente; os pipelines de encaminhamento de eventos devem implementar lógica de repetição e alertas para destinos que se tornam indisponíveis para evitar perda de dados durante interrupções.
- As políticas de governança de dados devem ser revisadas para cada destino de encaminhamento para garantir que as preferências de consentimento do usuário capturadas na borda sejam respeitadas na configuração de encaminhamento.
