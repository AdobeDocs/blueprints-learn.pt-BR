---
source-git-commit: 83e85d946e455cde46001af0a2112637b7fe24cc
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---
# Modelo da página de diagrama de arquitetura

Este é o modelo de marcação completo de uma página de diagrama de arquitetura. Substitua a cada `{placeholder}` com o valor coletado durante a Fase 1 do fluxo de trabalho de habilidade. Remova qualquer seção opcional que não se aplique (por exemplo, o bloco `>[!MORELIKETHIS]`) — não deixe espaços reservados vazios no arquivo gerado.

&#x200B;---

```markdown
---
title: {Page title}
description: {1-2 sentence page purpose, used for search snippets and previews}
solution: {Comma-separated Adobe solutions, e.g. Experience Platform, Journey Optimizer, Customer Journey Analytics}
---
# {Page title}

{Opening paragraph -- 1-2 sentences describing what the diagrams collectively illustrate. Frame the page as a top-level architecture reference, not a use case walkthrough.}

>[!MORELIKETHIS]
>
>[{Related-content link text}]({Related-content URL}).

## {Diagram 1 section title}

{1-2 sentence explanation of what the diagram shows and why it matters.}

<img src="assets/{filename-1}" alt="{Alt text for diagram 1}" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />

## {Diagram 2 section title}

{1-2 sentence explanation.}

<img src="assets/{filename-2}" alt="{Alt text for diagram 2}" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />

## Primary data flows and integration points

- {Flow or integration 1 -- e.g., "Real-time event ingestion from [!DNL Web SDK] to [!DNL Edge Network]"}
- {Flow or integration 2 -- e.g., "Profile sync between [!DNL Experience Platform] Hub and Edge"}
- {Flow or integration 3}
- {Flow or integration 4}
- {Flow or integration 5}

## Use case patterns supported

The architecture above supports the following use case patterns:

- [{Pattern 1 name}](/help/blueprints/use-case-patterns/{category}/{pattern-1-file}.md) -- {1-line note on why this architecture enables the pattern}
- [{Pattern 2 name}](/help/blueprints/use-case-patterns/{category}/{pattern-2-file}.md) -- {1-line note}
- [{Pattern 3 name}](/help/blueprints/use-case-patterns/{category}/{pattern-3-file}.md) -- {1-line note}

## Further reading

- [{Article 1 title}]({Experience League URL 1})
- [{Article 2 title}]({Experience League URL 2})
- [{Article 3 title}]({Experience League URL 3})
```

&#x200B;---

## Regras do Frontmatter

- **Campos obrigatórios:** `title`, `description`, `solution`.
- **Campos proibidos** (autoatribuídos no momento da publicação): `exl-id`, `product_v2`, `feature_v2`, `role_v2`, `topic_v2`, `TQID`, `kt`, `thumbnail`. Não os inclua em arquivos recém-criados.

## Convenções do corpo

- **One H1** — o título da página. Corresponder exatamente ao objeto de destaque `title`.
- **Um H2 por diagrama.** Sem H3 dentro das seções do diagrama; mantenha-as em uma introdução de uma a duas frases mais a imagem.
- **`<img>`incorporado** — o estilo embutido e `class="modal-image"` são obrigatórios. Eles impulsionam a interação modal-zoom do Experience League.
- **Caminho da imagem** — sempre `assets/{filename}` (relativo à pasta de tópicos da página). Não use caminhos absolutos.
- **nomes de produtos do Adobe** — quebrar em `[!DNL ...]` com corpo de texto e marcadores. Exemplo: `[!DNL Real-Time CDP]`, `[!DNL Journey Optimizer]`, `[!DNL Experience Platform]`.
- **Links padrão de caso de uso** — sempre use o formulário `/help/blueprints/use-case-patterns/{category}/{file}.md` absoluto para que o link seja resolvido a partir de qualquer página que possa transpor este conteúdo.
- **Links do Experience League** — URLs absolutas começando com `https://experienceleague.adobe.com/pt-br`. Prefira o URL do documento canônico a uma variante localizada.

## Ordenação de seção

Mantenha a ordem consistente em todas as páginas de arquitetura para que os leitores possam digitalizar de forma previsível:

1. Frontmatter
2. H1 + parágrafo de abertura
3. (Opcional) `>[!MORELIKETHIS]` texto explicativo
4. Um H2 por diagrama (em ordem especificada pelo usuário)
5. `## Use case patterns supported`
6. `## Primary data flows and integration points`
7. `## Further reading`

## Expectativas de comprimento

40 a 100 linhas de marcação são típicas. Se a página exceder 150 linhas, é provável que o conteúdo tenha se direcionado para o território do padrão de caso de uso — verifique novamente `scope-guardrails.md` e considere a divisão.
