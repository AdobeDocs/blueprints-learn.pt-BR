---
source-git-commit: c766cd3153efce4635089d008daf3eb426eb7a24
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%
---
# Referência de posicionamento do TOC.md

Quando a habilidade gera uma nova página de diagrama de arquitetura, ela deve adicionar uma entrada a `/help/blueprints/TOC.md` para que a página seja detectável na navegação do site. Este documento define exatamente onde e como essa entrada vai.

## Seção principal

Todas as páginas do diagrama de arquitetura estão na seção `+ Architecture Diagrams and Blueprints{#architecture-diagrams}` de nível superior no TOC.md. Nessa seção, várias subseções agrupam páginas por tópico.

Nomes de pastas, âncoras de índice e rótulos de índice para essas subseções devem seguir a regra de nomenclatura em `../../architecture-diagram-category-builder/references/naming-conventions.md` — veja esse arquivo se uma nova categoria for necessária (use a habilidade `architecture-diagram-category-builder` para isso, não esta).

## Mapeamento de subseção

Escolha a subseção que corresponde à pasta de tópicos da nova página:

| Pasta de tópico | Título da subseção do índice |
| --- | --- |
| `architecture-diagrams/architecture-overviews/` | `+ Architecture overviews{#architecture-overviews}` |
| `architecture-diagrams/audience-profile-activation/` | `+ Audience & Profile Activation{#audience-profile-activation}` |
| `architecture-diagrams/b2b-activation-marketing/` | `+ B2B activation & marketing{#b2b-activation-marketing}` |
| `architecture-diagrams/customer-insights/` | `+ Customer Insights{#customer-insights}` |
| `architecture-diagrams/customer-journeys/` | `+ Customer journeys{#customer-journeys}` |

Se o usuário propuser uma pasta de tópico que não esteja nessa tabela, trate-a como uma nova subseção de nível superior e faça uma pausa — peça ao usuário para confirmar se deseja criá-la. Não invente silenciosamente uma nova subseção.

## Formato de entrada

```
    + [{Page title}](/help/blueprints/{topic-folder}/{filename}.md)
```

Regras:

- **Recuo:** exatamente quatro espaços, em seguida `+ `. O analisador de índice depende disso; guias ou espaçamento diferente interromperão a navegação.
- **Texto do link:** o título da página, correspondendo exatamente ao `title` frontmatter. Use `[!DNL ...]` somente se os irmãos existentes na mesma subseção o usarem — corresponda à convenção local.
- **Destino do link:** caminho absoluto começando com `/help/blueprints/`. Sempre inclua a extensão `.md`.
- **Posição:** anexar como a última entrada na subseção correspondente, a menos que o usuário especifique uma posição diferente. Preservar a ordem existente de todas as entradas irmãs.

## Subseções aninhadas

`+ Architecture overviews{#architecture-overviews}` não tem agrupamentos aninhados — todas as páginas em `architecture-diagrams/architecture-overviews/` (incluindo páginas de implantação do SDK, por exemplo, `websdk.md`, `appsdk.md`) estão no mesmo nível de recuo de quatro espaços. Outras subseções (`Audience & Profile Activation`, `B2B activation & marketing` etc.) ainda pode conter agrupamentos aninhados — inspecione a seção antes de inserir a entrada. Se um agrupamento aninhado estiver presente e a nova página pertencer a ele, recue dois espaços adicionais; caso contrário, coloque a entrada no nível superior da subseção.

## Exemplos trabalhados

### Exemplo 1 — página do AEP de nível superior

- Pasta de Tópico: `architecture-diagrams/architecture-overviews/`
- Nome do arquivo: `mix-modeler-integration.md`
- Título da página: `Adobe Mix Modeler integration with Experience Platform`

Entrada:

```
    + [Adobe Mix Modeler integration with Experience Platform](/help/blueprints/architecture-diagrams/architecture-overviews/mix-modeler-integration.md)
```

Colocado em `+ Architecture overviews{#architecture-overviews}`.

### Exemplo 2 — Arquitetura do AJO jornada

- Pasta de Tópico: `architecture-diagrams/customer-journeys/`
- Nome do arquivo: `cross-channel-journey-architecture.md`
- Título da página: `Cross-channel journey architecture`

Entrada:

```
    + [Cross-channel journey architecture](/help/blueprints/architecture-diagrams/customer-journeys/cross-channel-journey-architecture.md)
```

Colocado em `+ Customer journeys{#customer-journeys}`.

### Exemplo 3 — Página de implantação do SDK

- Pasta de Tópico: `architecture-diagrams/architecture-overviews/`
- Nome do arquivo: `mobile-sdk-architecture.md`
- Título da página: `Mobile SDK deployment architecture`

Entrada (mesmo recuo de quatro espaços como outras páginas de visão geral da arquitetura):

```
    + [Mobile SDK deployment architecture](/help/blueprints/architecture-diagrams/architecture-overviews/mobile-sdk-architecture.md)
```

Colocado em `+ Architecture overviews{#architecture-overviews}`.

## Verificação

Após editar o TOC.md, leia novamente a subseção afetada e confirme:

1. A nova entrada usa exatamente quatro espaços de recuo (ou seis, se aninhados em um agrupamento específico de subseção, por exemplo, agrupamento RTCDP de `Audience & Profile Activation`).
2. O destino do link corresponde ao caminho do arquivo no disco — incluindo a extensão `.md`.
3. A entrada é agrupada na subseção correta — não está flutuando entre subseções.
4. Nenhuma entrada existente foi reordenada ou modificada.
