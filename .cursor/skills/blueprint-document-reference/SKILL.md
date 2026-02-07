---
name: blueprint-document-reference
description: Referência para criar e editar documentos do Blueprint de experiência digital do Adobe. Use ao criar novos blueprints, adicionar páginas de blueprint ou quando o usuário perguntar sobre a estrutura do blueprint, seções, modelos ou fazer referência à Adobe Experience League.
source-git-commit: dfa21942ecf2a1db06df6f6cc945f5572811ca93
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 1%

---


# Referência do documento de blueprint

Use esta habilidade ao criar ou editar documentos de blueprint neste repositório. Os blueprints são implementações repetíveis que abordam problemas comerciais estabelecidos e incluem diagramas de arquitetura, considerações técnicas e links para a documentação da Adobe Experience League.

## Quando aplicar

- Criar um novo documento de blueprint ou página de visão geral do blueprint
- Adicionar ou reestruturar seções em um blueprint existente
- Vincular ou citar a documentação da Adobe Experience League
- Alinhamento do novo conteúdo com as convenções do blueprint (frente, cabeçalhos, diagramas)

## Referência rápida

1. **Finalidade do documento**: os blueprints fornecem arquitetura de fluxo de dados e sistema para mostrar como a Adobe Experience Platform e os aplicativos são integrados. Elas são visuais e técnicas, não de marketing.
2. **Seções**: usar as seções padrão do modelo; omitir somente quando não aplicável (consulte [reference.md](reference.md)).
3. **Experience League**: prefira vincular ao Experience League para documentos de produto, APIs, medidas de proteção e tutoriais. Use URLs completos. Consulte [reference.md](reference.md) para obter padrões e formatação de URL.
4. **Estrutura do repositório**: os blueprints ficam em `help/blueprints/`. Atualizar `help/blueprints/TOC.md` ao adicionar ou mover páginas de blueprint.

## Modelo de documento

Cada página do blueprint deve seguir essa estrutura. Inclua somente as seções que se aplicam.

```markdown
---
title: [Short descriptive title]
description: "[One sentence: what this blueprint shows and why it matters.]"
solution: [Product name, e.g. Real-Time Customer Data Platform, Journey Optimizer]
exl-id: [UUID - leave blank if new, this will be auto-generated as part of the Experience League publishing flow]
---
# [H1 - same as title or expanded]

[1–3 paragraphs: what the blueprint covers, key capabilities, and who it’s for.]

## Applications

* [Product 1]
* [Product 2]

## Use cases

* [Use case 1]
* [Use case 2]

## Prerequisites

[Bullets or short paragraphs: required products, config, or setup.]

## Architecture Diagram

<img src="[path to SVG/image]" alt="[Descriptive alt]" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## Guardrails

[Link to Experience League guardrails and any blueprint-specific limits.]

## Implementation patterns

[Optional: named patterns with bullets.]

## Implementation steps

1. [Step with link to Experience League where relevant]
2. ...

## Implementation considerations

[Optional: identity, performance, security, etc.]

## Related documentation

[Grouped links to Experience League: product docs, APIs, tutorials.]
```

Para obter uma visão geral ou páginas de hub, use uma estrutura mais curta: introdução, casos de uso (ou guias), imagem da arquitetura, tabela de cenários/padrões, pré-requisitos, medidas de proteção e documentação relacionada. Veja as visões gerais existentes em `help/blueprints/` para ver exemplos.

## Frontmatter

| Campo | Obrigatório | Observações |
|-------|----------|--------|
| `title` | Sim | Abreviado; use `[!DNL Product Name]` para nomes de produtos por estilo do Adobe |
| `description` | Sim | Uma frase; usada em pesquisas e cartões |
| `solution` | Sim | Produto principal (por exemplo, Real-Time Customer Data Platform, Journey Optimizer) |
| `exl-id` | Sim | UUID; deixe em branco para novas páginas |
| `doc-type` | Para visões gerais | Usar `overview-page` para as páginas principais de visão geral do blueprint |
| `kt` | Opcional | ID do artigo da knowledge base, se vinculado |

## Referência à Adobe Experience League

- **Quando vincular**: vincular à Experience League para obter a documentação do produto, referências de API, medidas de proteção, tutoriais e etapas de configuração. Não duplique procedimentos longos; resuma e vincule.
- **Formato de URL**: usar URLs completas. Prefira `https://experienceleague.adobe.com/docs/...` ou `https://experienceleague.adobe.com/en/docs/...`. Para documentos do desenvolvedor, `https://developer.adobe.com/...` também é válido.
- **Texto do link**: use texto descritivo (por exemplo, &quot;[Criar esquemas] (url)&quot; e não &quot;Clique aqui&quot;). Para nomes de produtos no texto do link, use `[!DNL Product Name]` quando apropriado.
- **Seção de documentação relacionada**: encerre blueprints com uma seção de &quot;Documentação relacionada&quot; agrupando links por categoria (por exemplo, configurações de destino, documentação do SDK, Perfil e segmentação, Tutoriais).

Para obter padrões detalhados de URL, agrupamento de links e exemplos, consulte [reference.md](reference.md).

## Lista de verificação antes de enviar

- [ ] O Frontmatter tem `title`, `description`, `solution`, `exl-id`
- [ ] H1 corresponde ou expande apropriadamente o título
- [ Diagrama de arquitetura ] presente e texto alternativo descritivo
- [ ] Link das etapas de implementação para a Experience League onde os procedimentos estão
- [ A seção ] Medidas de proteção está vinculada aos documentos oficiais da Experience League
- [ ] A seção de documentação relacionada inclui links relevantes do Experience League
- [ ] páginas novas ou movidas são refletidas em `help/blueprints/TOC.md`

## Recursos adicionais

- Modelo completo e notas de seção: [reference.md](reference.md)
- Blueprints existentes: `help/blueprints/` (por exemplo, `audience-activation/real-time-lookup.md`, `customer-journeys/journey-optimizer/journey-optimizer-overview.md`)
- Sumário e navegação: `help/blueprints/TOC.md`
