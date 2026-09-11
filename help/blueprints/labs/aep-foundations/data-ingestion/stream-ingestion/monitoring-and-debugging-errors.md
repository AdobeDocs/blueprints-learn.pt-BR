---
hold: true
title: Monitoramento e erros de depuração
description: Use o painel de monitoramento Fim a Fim do Streaming para identificar e interpretar erros de ASSIMILAÇÃO, DCVS e MAPPER em um fluxo de dados de streaming.
doc-type: article
solution: Experience Platform
exl-id: 268abf15-14ac-45e3-8cd7-8d180ee5b1e3
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---


# Monitoramento e erros de depuração

>[!NOTE]
>
>O monitoramento da assimilação de streaming ocorre no nível do fluxo de dados, o que significa que, ao visualizá-lo na interface do usuário, você está visualizando o data lake.  Isso significa que você vê os lotes serem exibidos (os microlotes processando fora do pipeline de transmissão) a cada 60 minutos aproximadamente.  Portanto, se você não visualizar seus dados no Perfil do cliente em tempo real, será necessário aguardar até 60 minutos para diagnosticar o problema.



## Exibir painel de monitoramento

1. Navegue até **Monitoramento->Streaming de Ponta a Ponta** e localize seu **Fluxo de Dados**:

![Localizando o fluxo de dados de transmissão na seção de Monitoramento](assets/monitoring-and-debugging-errors-locate-your-dataflow-in-monitoring.png "Localize seu fluxo de dados no Monitoramento")



1. Talvez você queira visualizar a guia **painel** para ver as métricas de pipeline relacionadas aos fluxos de trabalho de assimilação em lote.

![Guia Painel mostrando métricas em todos os fluxos de trabalho de assimilação em lote](assets/monitoring-and-debugging-errors-dashboard-tab-metrics.png "A guia Painel mostra métricas em todos os fluxos de trabalho de assimilação em lote")

>[!NOTE]
>
>Essa tela de monitoramento permite que você veja o status das várias execuções de fluxo de dados.  Observe as várias métricas disponíveis no painel superior.  Essas métricas podem ser extremamente úteis para entender a integridade do pipeline de dados na Experience Platform



## Erros de depuração

1. Se o fluxo de dados tiver erros porque você não seguiu as instruções, você verá o seguinte.

![Falhas relatadas para um fluxo de dados de streaming com erros de mapeamento](assets/monitoring-and-debugging-errors-failures-reported.png "Falhas relatadas")



1. Se clicar em Falhas, você obtém a seguinte tela:

![Tela de diagnóstico de erro mostrando detalhes de erros de INGEST, DCVS e MAPPER](assets/monitoring-and-debugging-errors-preview-error-diagnostics.png "Visualizar diagnóstico de erro")

>[!NOTE]
>
>Um microlote bem-sucedido pode levar mais de 15 minutos, pois pode precisar de tempo para gravar os registros no data lake.



1. Analise a mensagem de erro, identifique os **campos de origem/destino** e procure o código:

- **INGEST XXXX** - Este é um erro grave devido à corrupção de dados ou a problemas de formatação, isto é, não seguir um formato regex.
- **DCVS XXXX** - Este erro é visto com os campos `required`. Se os valores não existirem ou forem mapeados incorretamente (não dentro da lista de enumerações), essas linhas serão ignoradas.
- **MAPPER XXXX** - Estes são avisos e nenhuma linha é ignorada. Mas os valores podem ter sido &quot;anulados&quot; - portanto, você deve verificar se eles não afetam as atividades downstream.

1. Para se recuperar dos erros, vá para **Fontes->Fluxos de Dados->Nome do Fluxo de Dados->Atualizar fluxo de dados** e corrija seus mapeamentos.

&#x200B;> [!NOTE]
>
>Você precisa recarregar o arquivo de amostra JSON excluindo-o e adicionando-o novamente para que o mapeador agora seja atualizado com uma nova cópia para validação.

![Navegando até Fontes > Fluxos de Dados > Nome do Fluxo de Dados > Atualizar fluxo de dados para corrigir mapeamentos](assets/monitoring-and-debugging-errors-update-dataflow-navigation.png "Clique em Atualizar fluxo de dados")
