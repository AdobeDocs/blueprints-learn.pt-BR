---
source-git-commit: e0ecfa4d74b8fcc0bbaf35d44c33c725a1b1a539
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%
---
# Modelo da categoria overview.md

Toda pasta de categoria em `help/blueprints/architecture-diagrams/` precisa de um `overview.md` que se pareça com os outros cinco. Use essa estrutura exata.

## Frontmatter

```yaml
---
title: {Category Label}
description: {One-sentence summary of what this category covers.}
solution: {Primary Adobe solution(s), comma-separated}
doc-type: overview-page
---
```

Não inclua `exl-id`, `product_v2`, `feature_v2`, `role_v2`, `topic_v2`, `TQID`, `kt` ou `thumbnail` em uma nova página — o pipeline de publicação preenche isso automaticamente.

## Corpo

```markdown
# {Category Label}

{1-3 paragraph intro describing what this category of diagrams covers and why it matters.}

| Diagram | Description |
| --- | --- |
| [{Page title}]({filename}.md) | {One-sentence description of the page} |
| [{Page title}]({filename}.md) | {One-sentence description of the page} |
```

Regras:

- Liste cada página na categoria, na mesma ordem em que aparecem no TOC.md.
- Os destinos de links são nomes de arquivo relativos (sem prefixo `/help/blueprints/...`), já que a visão geral está ao lado de suas páginas irmãs.
- As descrições são uma frase, não é necessário qualquer ponto à direita se o texto for exibido como um rótulo.
- Se uma categoria tiver um subagrupamento natural (por exemplo, &quot;Diagramas obsoletos&quot; em jornadas do cliente), adicione um cabeçalho `## {Sub-group name}` seguido de sua própria tabela de duas colunas no mesmo formato — não misture miniaturas de diagrama ou colunas extras na tabela.
- Não inserir miniaturas de diagrama `<img>` nesta tabela. Mantenha em duas colunas: `Diagram` (link) e `Description` (texto). As miniaturas pertencem às páginas de conteúdo individuais, não à visão geral da categoria.
- Não use HTML `<ul><li>` aninhada dentro de células da tabela. Somente texto simples.

## Exemplo (insights do cliente)

```markdown
---
title: Customer Insights
description: Unify and analyze data and customer behaviors from across the customer journey
solution: Customer Journey Analytics
doc-type: overview-page
---
# Customer Insights

Customer Journey Analytics shows how brands can unify customer data and behavior from various interaction channels and sources to create a journey-based view of all customer interactions.

| Diagram | Description |
| --- | --- |
| [Adobe Customer Journey Analytics](cja.md) | Core Customer Journey Analytics architecture, including B2B and audience-sharing derivations |
| [Adobe Customer Journey Analytics & Adobe Journey Optimizer integration](cja-ajo-integration.md) | Campaign and journey insights integration between Customer Journey Analytics and Journey Optimizer |
```
