---
source-git-commit: 8b3391d41cd4a3ea6cb52d5167e627b7f6bd2c6e
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 48%
---
# Modelo do padrão de caso de uso

Esse arquivo contém o modelo de marcação completo para uma página de padrão de caso de uso. Substituir todos os valores de `{{placeholder}}` pelo conteúdo real ao gerar um novo padrão.

&#x200B;---

## Modelo

&grave;&grave;&grave;&grave;markdown
---
title: {{Pattern Title}}
description: {{One-sentence description of what this pattern teaches}}
solution: {{Comma-separated Adobe solutions}}
exl-id: {{generate-uuid-placeholder}}
---
&#x200B;# {{Pattern title}}

This guide provides an overview of {{pattern name}} using {{solutions with [!DNL ...] formatting}}. It is designed for solution architects, marketing technologists, and implementation engineers who need to {{primary capability description}}.

## Use case pattern

**{{Pattern Name}}**

{{One-two sentence description of what the pattern does and enables.}}

**Execution plan:** {{Step 1}} > {{Step 2}} > {{Step 3}} > {{Step 4}} > {{Step 5}}

## Use case overview

{{Paragraph 1: Define the pattern. What does it do? How does it differ from related patterns? Provide a clear, specific definition.}}

{{Paragraph 2: Describe the typical trigger or starting condition. When does this pattern apply? What event, schedule, or condition initiates it?}}

{{Paragraph 3: Describe what the pattern delivers. What is the end result for the customer or business? What channels or touchpoints does it affect?}}

{{Paragraph 4: Clarify scope boundaries. What does this pattern NOT cover? What adjacent patterns handle those needs? Reference other patterns by name if relevant.}}

{{Paragraph 5 (optional): Identify typical stakeholders and teams involved in implementation. Who owns what?}}

## Key business objectives

The following business objectives are supported by this use case pattern.

**[{{Objective Name}}](../../business-objectives/{{category}}/{{objective-file}}.md)**

{{Brief description of how this pattern supports the objective -- 1-2 sentences.}}

| KPIs |
| --- |
| {{KPI1}}, {{KPI2}}, {{KPI3}} |

{{Repeat the above block for each supported business objective.}}

## Example tactical use cases

The following scenarios illustrate how {{pattern name}} can be applied across different business contexts.

- **{{Scenario name}}** -- {{Description of the scenario and how it uses this pattern}}
- **{{Scenario name}}** -- {{Description}}
- **{{Scenario name}}** -- {{Description}}
- **{{Scenario name}}** -- {{Description}}
- **{{Scenario name}}** -- {{Description}}
- **{{Scenario name}}** -- {{Description}}
{{Include 6-10 scenarios total}}

## Key performance indicators

| KPI | Description | Measurement |
| --- | --- | --- |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |

## Applications

The following Adobe applications are used in this use case pattern.

- **[!DNL {{Application Name}}] ({{Abbreviation}})** -- {{Description of the application's role in this pattern}}
- **[!DNL {{Application Name}}] ({{Abbreviation}})** -- {{Description of the application's role in this pattern}}
- **[!DNL {{Application Name}}] ({{Abbreviation}})** -- {{Description of the application's role in this pattern}}

## Related documentation

The following resources provide additional detail on the capabilities used in this pattern. Group the reference links to primary Experience League documents under descriptive subheadings.

### &lbrace;Topic group&rbrace;

- [{{Link text}}] ({{URL}})
- [{{Link text}}] ({{URL}})

### &lbrace;Topic group&rbrace;

- [{{Link text}}] ({{URL}})
- [{{Link text}}] ({{URL}})
&grave;&grave;&grave;&grave;

&#x200B;---

## Observações sobre o uso deste modelo

- **Interface do YAML:** `exl-id` deve ser um UUID de espaço reservado (por exemplo, `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`). O pipeline de publicação atribui o valor real.
- **Ordem da seção:** A seção `Use case pattern` vem imediatamente após a introdução de abertura, antes de `Use case overview`. Ele oferece aos leitores uma definição rápida e de uma linha e um plano de execução de alto nível antecipadamente.
- **Nomes de produtos do Adobe:** sempre use a sintaxe `[!DNL ...]` para nomes de produtos do Adobe no corpo de texto e em tabelas (por exemplo, `[!DNL Journey Optimizer]`). Essa é uma convenção do Experience League que impede a tradução de nomes de produtos.
- **Links de objetivo comercial:** Use caminhos relativos do arquivo padrão para o diretório de objetivos comerciais: `../../business-objectives/{{category}}/{{filename}}.md`.
- **Nomes de arquivo com caixa de kebab:** o nome de arquivo padrão deve ter caixa de kebab derivada do título do padrão. Exemplo: &quot;Mensagens Acionadas por Evento&quot; torna-se `event-triggered-messaging.md`.
- **Plano de execução:** Use ` > ` (espaço, maior que, espaço) como separador entre as etapas. Mantenha o rótulo exatamente `**Execution plan:**`.
- **Documentação relacionada:** Agrupe os links de referência em subtítulos `###` descritivos (por exemplo, por área de aplicativo ou recurso). Estas são as referências do Experience League para os aplicativos e recursos usados no padrão.
- **Arquitetura (opcional):** Se um padrão se beneficiar de um diagrama de arquitetura de referência, uma seção `## Architecture` opcional poderá ser colocada entre `Applications` e `Related documentation`.
- **Escopo:** este modelo exclui intencionalmente as seções de implementação detalhadas (recursos de base/suporte/aplicativo, pré-requisitos, opções de implementação e etapas de implementação em fases). Esses detalhes estão na documentação do Experience League vinculada de `Related documentation`.