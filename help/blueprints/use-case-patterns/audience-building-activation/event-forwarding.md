---
title: Encaminhamento de eventos
description: Saiba como encaminhar dados de eventos em tempo real coletados por meio do Edge Network para destinos que não sejam da Adobe para análise, armazenamento ou publicidade.
solution: Experience Platform
exl-id: 24964d27-db56-4fa4-a79f-1b6750564b34
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---

# Encaminhamento de eventos

Este guia descreve o padrão de caso de uso do encaminhamento de eventos, que usa o processamento do lado do servidor no Edge Network [!DNL Adobe Experience Platform] para distribuir dados do evento em tempo real para destinos que não são da Adobe — como plataformas de análise de terceiros, pontos de extremidade de armazenamento em nuvem, redes de publicidade ou webhooks personalizados. Ele foi projetado para arquitetos de soluções, tecnólogos de marketing e engenheiros de implementação que precisam entender o que esse padrão faz, os objetivos de negócios que ele aceita, os casos de uso táticos que ele permite e os aplicativos Adobe envolvidos.

## Padrão do caso de uso

Esta seção descreve o padrão e o plano de execução usados para implementar o encaminhamento de eventos.

**Encaminhamento de Eventos** — Encaminhe dados de eventos em tempo real coletados via Edge Network para destinos que não sejam da Adobe para fins de análise, armazenamento ou publicidade.

**Plano de execução:** Configuração de sequência de dados > Definição de regra de evento > Mapeamento de destino > Execução de encaminhamento > Monitoramento

## Visão geral do caso de uso

As organizações que coletam dados comportamentais por meio do [!DNL Adobe Experience Platform] Web SDK, Mobile SDK ou API de servidor geralmente precisam compartilhar esse mesmo fluxo de eventos com sistemas que não sejam da Adobe — plataformas de análise como [!DNL Google Analytics] ou [!DNL Snowflake], redes de publicidade para rastreamento de conversão, data warehouses para armazenamento de longo prazo ou serviços internos personalizados. Tradicionalmente, isso exigia a proliferação de tags do lado do cliente, o que aumenta o peso da página, introduz latência e cria riscos de privacidade e governança.

O encaminhamento de eventos resolve isso operando no lado do servidor no Edge Network. Quando uma interação do visitante aciona um evento por meio do Web SDK ou da API do servidor, esse evento é roteado por meio de um fluxo de dados para a Edge Network. As regras de encaminhamento de eventos — configuradas em uma propriedade dedicada de encaminhamento de eventos — avaliam os dados de evento recebidos e os encaminham seletivamente para um ou mais destinos configurados. Essa abordagem do lado do servidor reduz o aumento excessivo de tags do lado do cliente, melhora o desempenho da página, centraliza a governança de dados e fornece à organização controle sobre exatamente quais dados deixam o ecossistema da Adobe.

O público-alvo deste padrão inclui organizações que já implantaram (ou planejam implantar) a API de Servidor ou Web SDK do [!DNL Adobe Experience Platform] para coleta de dados e desejam estender esse investimento distribuindo dados do evento para pontos de extremidade que não sejam da Adobe sem adicionar marcas JavaScript do lado do cliente.

## Principais objetivos de negócios

Os seguintes objetivos de negócios são compatíveis com esse padrão de caso de uso.

### Melhorar a qualidade e a governança dos dados

Garanta dados limpos, completos e em conformidade para a definição precisa de metas, a redução de desperdício e análises confiáveis. O encaminhamento de eventos centraliza a distribuição de dados no lado do servidor, dando à organização um único ponto de controle para quais dados são compartilhados com sistemas externos, reduzindo o risco de vazamento de dados e garantindo que as políticas de governança sejam aplicadas antes que os dados deixem o Edge Network [!DNL Adobe].

**KPIs:** Eficiência, economia

Para obter mais informações, consulte [Melhorar a qualidade e a governança dos dados](../../business-objectives/cost-efficiency/improve-data-quality-governance.md).

### Consolidar e modernizar a tecnologia de marketing

Reduza a fragmentação de ferramentas e o débito técnico migrando para plataformas unificadas e dimensionáveis. O encaminhamento de eventos permite que as organizações substituam várias tags de fornecedor do lado do cliente por um único mecanismo de distribuição de dados do lado do servidor, reduzindo a sobrecarga de carregamento da página e simplificando a pilha de tecnologia.

**KPIs:** Economia, Eficiência, Velocidade de Comercialização

Para obter mais informações, consulte [Consolidar e modernizar a tecnologia de marketing](../../business-objectives/cost-efficiency/consolidate-modernize-marketing-technology.md).

## Exemplo de casos de uso tático

A seguir estão cenários táticos comuns em que esse padrão de caso de uso se aplica.

- **Enriquecimento de análise de terceiros** — Encaminhe eventos de exibição de página, clique e conversão para [!DNL Google Analytics], [!DNL Snowflake] ou outras plataformas de análise em tempo real sem adicionar marcas do lado do cliente
- **Rastreamento de conversão do Advertising** — Envie eventos de compra e de geração de clientes potenciais para a API de conversões [!DNL Meta], [!DNL Google Ads], [!DNL TikTok] ou [!DNL Snap] do lado do servidor para medição e otimização de conversão
- **Transmissão de data warehouse** — Encaminhe dados brutos de evento para um data warehouse de nuvem ([!DNL Google BigQuery], [!DNL Amazon S3], [!DNL Azure Event Hubs]) para armazenamento de longo prazo e análise offline
- **Integração de webhook personalizada** — Encaminhar dados de evento filtrados ou transformados para microsserviços internos, sistemas CRM ou plataformas de parceiros por meio de pontos de extremidade HTTP
- **Redução de tags e melhoria no desempenho da página** — substitua várias tags JavaScript do fornecedor do lado do cliente por uma única implementação do Web SDK, além de regras de encaminhamento de eventos do lado do servidor, reduzindo o peso da página e melhorando o Core Web Vitals
- **Compartilhamento de dados compatível com privacidade** — Aplique a filtragem de dados e as regras de redação em nível de campo no lado do servidor antes de compartilhar dados do evento com terceiros, garantindo que a PII seja removida ou tenha hash antes que atinja sistemas externos
- **Distribuição de eventos de várias nuvens** — Encaminha simultaneamente o mesmo fluxo de eventos para vários destinos (por exemplo, analytics, publicidade e data warehouse) de um único conjunto de regras do lado do servidor
- **Encaminhamento de sinal de fraude em tempo real** — encaminhe eventos de transação de alto valor para sistemas de detecção de fraude para pontuação e alerta de riscos em tempo real

## Indicadores-chave de desempenho

Os KPIs a seguir ajudam a medir o sucesso desse padrão de caso de uso.

- **Redução do tempo de carregamento da página** — melhoria medida na velocidade de carregamento da página e no Core Web Vitals após a migração das tags do lado do cliente para o encaminhamento de eventos do lado do servidor
- **Taxa de êxito de entrega de dados** — Porcentagem de eventos encaminhados com êxito para pontos de extremidade de destino sem erros ou tempos limite
- **Redução da contagem de marcas** — Número de marcas de fornecedor do lado do cliente removidas após a implementação de equivalentes do lado do servidor
- **Atualidade/latência de dados** — Tempo entre a ocorrência do evento no cliente e a chegada do evento ao ponto de extremidade de destino (destino: subsegundos a segundos)
- **Taxa de conformidade de governança** — Porcentagem de compartilhamentos de dados de saída que passam pelas regras de filtragem do lado do servidor, garantindo que nenhum PII ou dado restrito atinja destinos não autorizados
- **Eficiência operacional** — redução no número de horas de desenvolvedores gasto gerenciando implantações de marcas do lado do cliente e solucionando conflitos de marcas

## Aplicativos

Os aplicativos a seguir são usados neste padrão de caso de uso.

- **[!DNL Adobe Experience Platform](Edge Network)** — Recebe e roteia dados de eventos em tempo real do Web SDK, Mobile SDK ou API de servidor por meio de sequências de dados configuradas
- **[!DNL Adobe Experience Platform](Encaminhamento de Eventos)** — Fornece o mecanismo de regras do lado do servidor para avaliação, filtragem, transformação e encaminhamento de dados de eventos para destinos externos
- **[!DNL Adobe Experience Platform](Marcas/Coleção de Dados)** — Gerencia o ciclo de vida, as extensões, as regras e o fluxo de trabalho de publicação da propriedade de encaminhamento de eventos

## Documentação relacionada

Os recursos a seguir fornecem detalhes adicionais sobre os tópicos abordados neste guia.

**Encaminhamento de eventos**

- [Visão geral do encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview)
- [Introdução ao encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started)
- [Monitoramento do encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/monitoring)
- [Segredos do encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/secrets)

**Extensões de encaminhamento de eventos**

- [Catálogo de extensões do lado do servidor](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/overview)
- [Extensão do Adobe Cloud Connector](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/cloud-connector/overview)
- [Extensão da API de conversões do Meta](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/meta/overview)
- [Extensão da Google Cloud Platform](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/google-cloud-platform/overview)
- [Extensão do AWS](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/aws/overview)
- [Extensão do Snowflake](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/snowflake/overview)
- [Extensão de conversões aprimoradas do Google Ads](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/google-ads-enhanced-conversions/overview)
- [Extensão do Mailchimp](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/mailchimp/overview)

**Coleta de dados e Edge Network**

- [Configurar sequências de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Visão geral dos fluxos de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview)
- [Visão geral do Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Visão geral da API do Edge Network Server](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [Visão geral das tags](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)
