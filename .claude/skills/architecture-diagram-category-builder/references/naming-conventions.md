---
source-git-commit: c766cd3153efce4635089d008daf3eb426eb7a24
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%
---
# Convenções de nomenclatura: Diagramas de arquitetura e blueprints

Este documento é a fonte da verdade sobre como as categorias em `+ Architecture Diagrams and Blueprints{#architecture-diagrams}` são nomeadas. A habilidade `architecture-diagram-category-builder` (novas categorias) e a habilidade `architecture-diagram-page-builder` (novas páginas dentro de categorias existentes) devem seguir estas regras.

## A regra

**Nome da pasta = descrição da âncora do sumário = kebab-case do rótulo do sumário completo.** Todos os três devem corresponder exatamente, sem abreviação ou truncamento.

| Rótulo do sumário | Âncora | Pasta |
| --- | --- | --- |
| Visão geral da arquitetura | `#architecture-overviews` | `architecture-overviews/` |
| Ativação de público-alvo e perfil | `#audience-profile-activation` | `audience-profile-activation/` |
| Ativação e marketing B2B | `#b2b-activation-marketing` | `b2b-activation-marketing/` |
| Insights do cliente | `#customer-insights` | `customer-insights/` |
| Jornadas do cliente | `#customer-journeys` | `customer-journeys/` |

Este é o estado atual e corrigido de todas as cinco categorias (em 16 de setembro de 2026). No início do histórico deste repositório, alguns foram abreviados (`architecture-overview`, `audience-activation`, `b2b-activation`) — essa inconsistência foi corrigida. Não reintroduza nomes de pasta/âncora abreviados para categorias novas ou existentes.

## Por que isso é importante

- **Previsibilidade.** Um colaborador (humano ou agente) deve ser capaz de adivinhar o caminho da pasta do rótulo do índice, e vice-versa, sem abrir o TOC.md.
- **Automação segura.** As habilidades e os scripts que geram caminhos a partir de rótulos (ou rótulos de caminhos) só funcionam de forma confiável quando o mapeamento é exato e mecânico (kebab-case, sem abreviação).
- **Higiene de redirecionamento.** Toda renomeação requer novas entradas em `redirects.csv`. Manter os nomes estáveis e totalmente descritivos desde o início evita churn repetido de renomeação.

## Como derivar uma lesma de um rótulo

1. Letra minúscula do rótulo.
2. Solte `&` inteiramente e junte as palavras ao redor com um hífen (por exemplo: `Audience & Profile Activation` -> `audience-profile-activation`).
3. Substituir espaços por hifens.
4. Pontuação de faixa diferente de hifens.
5. Não abrevie, trunque ou solte palavras do rótulo (não `b2b-activation` para &quot;Ativação e marketing B2B&quot; — use `b2b-activation-marketing`).

## Ativos necessários por categoria

Cada pasta de categoria diretamente em `help/blueprints/architecture-diagrams/` deve conter:

1. **`overview.md`** — uma página de aterrissagem para a categoria. Consulte `./category-overview-template.md` para obter a estrutura necessária. Toda página de visão geral da categoria deve ser igual: parágrafo(s) de introdução, em seguida, uma única tabela `| Diagram | Description |` listando cada página na categoria (em ordem de índice). Não use células `<ul><li>` aninhadas, imagens de diagrama inseridas ou uma terceira coluna — corresponda exatamente às cinco categorias existentes.
2. **`assets/`** — pasta para imagens de diagrama, mesmo se estiver vazia no momento da criação (crie-a após adicionar o primeiro diagrama).

## Requisitos do TOC.md

- A entrada `+ [Overview](/help/blueprints/architecture-diagrams/{folder}/overview.md)` da categoria é sempre a entrada **first** no cabeçalho da categoria, antes de qualquer página de conteúdo.
- O cabeçalho da categoria e sua âncora vão imediatamente abaixo de `+ Architecture Diagrams and Blueprints{#architecture-diagrams}`, no mesmo nível de recuo de dois espaços que as outras cinco categorias.
- As páginas de conteúdo têm 4 espaços recuados (`+` prefixados com quatro espaços à esquerda). Os subagrupamentos aninhados (por exemplo, agrupamento do RTCDP em Audience &amp; Profile Ativation) são recuados em 6 espaços.

## Requisitos da landing page

`help/blueprints/architecture-diagrams/overview.md` (a página de aterrissagem de Diagramas e Blueprints de arquitetura de nível superior) deve ter exatamente um cartão por categoria, em ordem de índice. Cada cartão:

- Links para a `overview.md` da categoria (não uma página de conteúdo).
- Usa uma imagem de diagrama representativa da pasta `assets/` dessa categoria como miniatura, estilizada com o cartão CSS padrão (`background-color:#ffffff; border:1px solid #d3d3d3;` mais as regras de dimensionamento/preenchimento compartilhadas já existentes no arquivo).
- Inclui o nome da categoria (negrito/forte) e uma descrição de uma frase que corresponde à introdução da visão geral da categoria.

Quando o número de categorias é um múltiplo de 3, a tabela é renderizada como linhas completas e limpas (3 colunas, `table-layout:fixed`, `width:33%` por célula). Se não for um múltiplo de 3, adicione um `<td>` vazio por slot ausente na última linha (não deixe a tabela irregular/sem estilo).
