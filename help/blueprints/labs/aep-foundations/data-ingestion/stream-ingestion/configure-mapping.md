---
hold: true
title: Configurar mapeamento
description: Importe o conjunto de mapeamento do laboratório de assimilação em lote e atualize os campos de data calculada para corresponder ao formato de data da fonte de transmissão.
doc-type: article
solution: Experience Platform
exl-id: c05792af-5eab-4e62-a26e-a54478a988a8
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Configurar mapeamento

&#x200B;> [!NOTE]
>
>Siga esta seção somente se tiver concluído com êxito o laboratório de assimilação em lote.  Caso contrário, siga as etapas [Dados de mapeamento](../batch-ingestion/mapping-data/overview.md) encontradas no laboratório de assimilação em lote.

## Importar conjunto de mapeamento

Se você concluiu o laboratório de Assimilação em lote, é possível reutilizar o conjunto de mapeamento criado lá 😄🎉

Execute as seguintes etapas:

1. Clique no botão **Importar Mapeamento** na tela de mapeamento

![Botão Importar Mapeamento na tela de mapeamento](assets/configure-mapping-import-mapping-button.png)



1. Escolha o fluxo de dados criado na seção Assimilação em lote e selecione-o.  Ele deve ser nomeado como **Lote de contas de clientes v2 - \&lt;suas iniciais>.**

![Escolhendo o fluxo de dados de Assimilação em lote para importar seu conjunto de mapeamento de](assets/configure-mapping-choose-batch-ingestion-dataflow.png)



Após a importação, você verá erros serem exibidos.  Isso ocorre porque o formato de data usado para o campo birth\_Date no arquivo de amostra foi alterado.

- Arquivo de amostra em lote usado -> mm/dd/aaaa
- Arquivo de amostra de fluxo usado -> aaaa-mm-dd

Os campos calculados que usam funções **date** precisarão ser atualizados para levar em conta a alteração no formato de data usado.

![Erros de mapeamento exibidos após a importação do conjunto de mapeamento de assimilação em lote](assets/configure-mapping-mapping-after-the-import.png)



## Atualizar campos calculados

Atualize cada campo calculado clicando no ícone de seta ao lado de cada campo calculado e valide os mapeamentos

![Ícone de seta para clicar para editar a fórmula de um campo calculado](assets/configure-mapping-arrow-to-edit-calculated-field-formula.png)

| Campo de destino | Novo Campo Calculado |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| person.birthYear | date\_part(&quot;aaaa&quot;,date(birth\_Date,&quot;yyyy-M-d&quot;)) |
| person.birthDayAndMonth | concat(date\_part(&quot;mm&quot;, date(birth\_Date, &quot;aaaa-M-d&quot;)).toString(), &quot;-&quot;, date\_part(&quot;dd&quot;, date(birth\_Date, &quot;aaaa-M-d&quot;)).toString()) |
