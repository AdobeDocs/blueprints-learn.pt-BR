---
source-git-commit: 83e85d946e455cde46001af0a2112637b7fe24cc
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---
# Referência de posicionamento do TOC.md

Quando a habilidade gera uma nova página de diagrama de arquitetura, ela deve adicionar uma entrada a `/help/blueprints/TOC.md` para que a página seja detectável na navegação do site. Este documento define exatamente onde e como essa entrada vai.

## Seção principal

Todas as páginas do diagrama de arquitetura estão na seção `+ Architecture Diagrams and Blueprints{#architecture-diagrams}` de nível superior no TOC.md. Nessa seção, várias subseções agrupam páginas por tópico.

## Mapeamento de subseção

Escolha a subseção que corresponde à pasta de tópicos da nova página:

| Pasta de tópico | Título da subseção do índice |
| --- | --- |
| `experience-platform/` | `+ Architecture overviews{#architecture-overview}` |
| `experience-platform/deployment/` | `+ Deployment{#deployment}` (uma subseção aninhada dentro de `Architecture overviews`) |
| `audience-activation/` | `+ Audience & Profile Activation{#audience-activation}` |
| `b2b/` | `+ B2B activation & marketing{#b2b-activation}` |
| `customer-journey-analytics/` | `+ Customer Journey Analytics{#customer-journey-analytics}` |
| `customer-journeys/` | `+ Customer journeys{#customer-journeys}` |

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

`+ Architecture overviews{#architecture-overview}` contém um bloco `+ Deployment{#deployment}` aninhado para páginas do SDK. Se a nova página estiver em `experience-platform/deployment/`, coloque a entrada dentro de `Deployment` com **seis** espaços de recuo:

```
      + [{Page title}](/help/blueprints/experience-platform/deployment/{filename}.md)
```

Outras subseções (`Audience & Profile Activation`, `B2B activation & marketing` etc.) também pode conter agrupamentos aninhados — inspecione a seção antes de inserir a entrada. Se um agrupamento aninhado estiver presente e a nova página pertencer a ele, recue dois espaços adicionais; caso contrário, coloque a entrada no nível superior da subseção.

## Exemplos trabalhados

### Exemplo 1 — página do AEP de nível superior

- Pasta de Tópico: `experience-platform/`
- Nome do arquivo: `mix-modeler-integration.md`
- Título da página: `Adobe Mix Modeler integration with Experience Platform`

Entrada:

```
    + [Adobe Mix Modeler integration with Experience Platform](/help/blueprints/experience-platform/mix-modeler-integration.md)
```

Colocado em `+ Architecture overviews{#architecture-overview}`.

### Exemplo 2 — Arquitetura do AJO jornada

- Pasta de Tópico: `customer-journeys/`
- Nome do arquivo: `cross-channel-journey-architecture.md`
- Título da página: `Cross-channel journey architecture`

Entrada:

```
    + [Cross-channel journey architecture](/help/blueprints/customer-journeys/cross-channel-journey-architecture.md)
```

Colocado em `+ Customer journeys{#customer-journeys}`.

### Exemplo 3 — Página Deployment SDK

- Pasta de Tópico: `experience-platform/deployment/`
- Nome do arquivo: `mobile-sdk-architecture.md`
- Título da página: `Mobile SDK deployment architecture`

Entrada (observe o recuo de seis espaços):

```
      + [Mobile SDK deployment architecture](/help/blueprints/experience-platform/deployment/mobile-sdk-architecture.md)
```

Colocado em `+ Deployment{#deployment}` dentro de `+ Architecture overviews{#architecture-overview}`.

## Verificação

Após editar o TOC.md, leia novamente a subseção afetada e confirme:

1. A nova entrada usa exatamente quatro espaços de recuo (ou seis, se aninhados em `Deployment`).
2. O destino do link corresponde ao caminho do arquivo no disco — incluindo a extensão `.md`.
3. A entrada é agrupada na subseção correta — não está flutuando entre subseções.
4. Nenhuma entrada existente foi reordenada ou modificada.
