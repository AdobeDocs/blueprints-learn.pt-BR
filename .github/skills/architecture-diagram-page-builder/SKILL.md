---
name: architecture-diagram-page-builder
description: 'Criação de guias de novas páginas de diagrama de arquitetura para o repositório de blueprints do Adobe Experience Platform. Use essa habilidade ao adicionar um novo diagrama de arquitetura de nível superior, uma página de arquitetura de integração ou uma visão geral da arquitetura do aplicativo. As páginas de arquitetura abordam o AEP de nível superior, as arquiteturas de aplicativos e os principais pontos de integração, e não casos de uso aprofundado (que pertencem ao construtor de padrões de casos de uso). Lida com o fluxo de trabalho completo: coleta de informações da página, geração do arquivo de marcação, colocação dele na pasta de tópico correta e atualização do TOC.md.'
source-git-commit: 8b3391d41cd4a3ea6cb52d5167e627b7f6bd2c6e
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 1%
---

# Diagrama de arquitetura do Page Builder

Essa habilidade orienta a criação de novas páginas de diagrama de arquitetura para o repositório de blueprints do Adobe Experience Platform. As páginas de diagrama de arquitetura fornecem referências visuais de alto nível sobre como os aplicativos do AEP e do Adobe se encaixam, os dados principais fluem entre eles e os pontos de integração que os autores precisam estar cientes ao projetar soluções.

## Escopo

As páginas de diagrama de arquitetura são **páginas focalizadas, com estilo de referência** — normalmente entre 40 e 100 linhas de marcação — que contêm:

- Um ou mais diagramas de arquitetura com explicações resumidas da finalidade de cada diagrama
- Links para padrões de caso de uso que a arquitetura aceita (a página de arquitetura não duplica esse conteúdo)
- Uma pequena lista dos fluxos de dados principais e pontos de integração ilustrados
- Links do Experience League para obter mais informações sobre o domínio do aplicativo

Eles **não** o local para conteúdo de casos de uso detalhados. Os KPIs, os objetivos comerciais, os exemplos de caso de uso tático, os recursos e as narrativas pessoais pertencem às páginas de padrão de caso de uso, geradas pela habilidade `use-case-pattern-builder`. Consulte `./references/scope-guardrails.md` para obter as medidas de proteção completas.

## Leitura necessária antes de iniciar

Leia os seguintes arquivos de referência para modelos e regras:

- `./references/diagram-template.md` — o modelo de marcação completa com valores de espaço reservado
- `./references/toc-placement.md` — tabela de mapeamento de subseção e formato de entrada para TOC.md
- `./references/scope-guardrails.md` — regras para o que pertence a uma página de arquitetura vs. uma página de padrão de caso de uso

## Fase 1: Coleta de informações

**Use o formulário de pergunta disponível, não uma entrevista linear.** Colete todas as informações necessárias em rodadas lógicas em lote, em vez de fazer uma pergunta de cada vez. Isso mantém a experiência rápida e verificável para o usuário.

### Restrições do formulário de pergunta

- Máximo de **4 perguntas** por formulário.
- Máximo de **4 opções** por pergunta.
- Se uma pergunta tiver mais de quatro opções plausíveis, divida-a em duas chamadas (por exemplo, faça as primeiras quatro opções e siga com um sim/não na quinta).
- Use o `multiSelect: true` para perguntas nas quais várias respostas se aplicam (soluções, padrões, fluxos de dados).

### Rodada 1 — Informações da página principal (formulário de uma pergunta, até 4 perguntas)

Solicite todos os itens a seguir em um único formulário:

1. **Título da página** — apresente de 2 a 3 variantes sugeridas que derivam do que o usuário já lhe disse, além de uma escotilha de escape &quot;Outros&quot;.
2. **Pasta de tópico** — apresente as 5 pastas válidas como opções; recomende a mais provável com base na entrada do usuário.
3. **soluções da Adobe** — seleção múltipla; sugira os candidatos mais prováveis com base no tópico da página.
4. **Contagem de diagramas** — quantos diagramas a página incluirá (1/2/3/4+).

### Rodada 2 — Detalhes do diagrama (formulário de uma pergunta, até 4 perguntas)

Pergunte o nome do arquivo de imagem de cada diagrama e a finalidade da página em um formulário:

- Para cada diagrama (até 2 em uma única rodada de formulário), pergunte pelo **nome do arquivo de imagem** como uma pergunta com 2-3 nomes de arquivo sugeridos (derivados do título da página) mais uma opção &quot;Outros&quot;.
- Pergunte pela **finalidade da página** (descrição de uma a duas frases) como uma pergunta com 2 a 3 frases sugeridas, além de &quot;Outros&quot;.
- Pergunte se é necessário um **`>[!MORELIKETHIS]`texto explicativo** (Sim/Não). Se a resposta for Sim, colete o URL e o texto do link em uma mensagem de acompanhamento.

> **Títulos de seção e texto alternativo:** Quando o nome do arquivo de imagem é descritivo (por exemplo, `fac-architecture.svg`, `fac-dataflow.svg`), inferir o título da seção H2 e o texto alternativo dele — não é necessário perguntar ao usuário. Use o nome de arquivo base, com base em título e humanizado, como o título da seção (por exemplo, `Architecture diagram`, `Data flow diagram`). Pergunte somente se o nome do arquivo é ambíguo.

### Rodada 3 — Padrões de caso de uso (formulário de pergunta após verificação)

Antes de apresentar este formulário, pesquise `/help/blueprints/use-case-patterns/` e identifique 3-5 padrões que provavelmente correspondam com base no título da página, finalidade e soluções. Confirme se cada arquivo existe antes de sugeri-lo.

Apresente os 4 principais candidatos como uma pergunta `multiSelect`. Se existir um quinto candidato forte, siga com uma pergunta sim/não separada para esse candidato. Convide também o usuário a nomear qualquer padrão perdido.

Inclua somente padrões cujos arquivos estejam confirmados. Não alucinar nomes de padrões.

### Rodada 4 — Fluxos de dados e links Experience League (formulário de uma pergunta)

**Fluxos de dados:** Proponha de 3 a 5 marcadores de fluxo de dados pré-gravados como uma pergunta `multiSelect` (derivado do tópico da página). O usuário seleciona qual se aplica. Mantenha cada opção em uma frase concisa. Se o usuário precisar de fluxos personalizados que não estejam em sua lista, ele poderá fornecê-los em um acompanhamento.

**Links do Experience League:** depois do formulário, apresente uma tabela de Markdown de 4 a 6 links sugeridos com o título do artigo, URL e uma lógica de uma linha. Marcar cada URL como **não verificado**. Peça ao usuário para (a) aceitar, (b) substituir por um URL verificado ou (c) adicionar o seu próprio URL. Use um formulário de pergunta complementar com até 4 opções se a lista for longa; caso contrário, aceite a confirmação em texto simples.

Nunca invente URLs que você não tenha buscado. Se não tiver certeza, sugira o título do artigo e permita que o usuário forneça o URL.

### Quando todas as rodadas estiverem concluídas

Confirme o conjunto completo de informações com o usuário antes de gerar quaisquer arquivos. Se algum item obrigatório ainda estiver ausente ou marcado como &quot;Outros&quot; sem um valor, peça-o antes de continuar. Não fabrique diagramas, padrões ou links.

## Fase 2: Verificação do escopo

Antes de gerar, leia novamente as descrições do diagrama do usuário, os marcadores de fluxo de dados e qualquer proposta de rascunho. Aplicar as medidas de proteção de `./references/scope-guardrails.md`.

Se qualquer um dos itens a seguir for exibido no conteúdo planejado, avise o usuário e se ofereça para redirecionar essa seção para uma página de padrão de caso de uso (ou apare-o da página de arquitetura):

- KPIs ou fórmulas de medição
- Objetivos ou narrativas de impacto nos negócios
- Exemplos de caso de uso tático (cenários de personalização específicos, exemplos de campanha etc.)
- Recursos (`A > B > C > D` estilo)
- Narrativa orientada por pessoas

Se o conteúdo planejado permanecer no escopo da página de arquitetura (arquitetura de nível superior, fluxo de dados do sistema, pontos de integração, topologia de implantação, borda versus hub), confirme com o usuário e prossiga para a Fase 3.

## Fase 3: Geração de conteúdo

Gere a página em:

```
/help/blueprints/{topic-folder}/{kebab-filename}.md
```

Use `./references/diagram-template.md` como modelo de origem. Preencha todos os valores de espaço reservado com as informações coletadas. O arquivo gerado deve incluir:

1. **YAML frontmatter** — `title`, `description`, `solution` somente.
   - **NÃO inclua`exl-id`** — o pipeline de publicação o atribui automaticamente.
   - **NÃO inclua** `product_v2`, `feature_v2`, `role_v2`, `topic_v2`, `TQID`, `kt` ou `thumbnail` — eles também são preenchidos automaticamente.

2. **Cabeçalho H1** — o título da página.

3. **Abrindo parágrafo** — 1-2 frases derivadas da entrada de finalidade de página.

4. **Opcional `>[!MORELIKETHIS]` bloco** — somente se o usuário tiver fornecido um link de conteúdo relacionado.

5. **Uma seção H2 por diagrama** — na ordem em que o usuário as forneceu. Cada seção contém:
   - O título da seção como o cabeçalho H2
   - 1-2 frases explicando o propósito do diagrama
   - A imagem é incorporada usando a convenção padrão:

     ```html
     <img src="assets/{filename}" alt="{Alt Text}" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />
     ```

6. **`## Use case patterns supported`** — lista com marcadores. Cada marcador:

   ```
   - [{Pattern name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md) -- {1-line note on why this architecture enables the pattern}
   ```

7. **`## Primary data flows and integration points`** — lista com marcadores de 3 a 7 itens de fluxo/integração.

8. **`## Further reading`** — lista com marcadores de links do Experience League:

   ```
   - [{Article title}]({Experience League URL})
   ```

Use a sintaxe `[!DNL ...]` para nomes de produtos Adobe no corpo do texto e nos marcadores, correspondendo à convenção das páginas existentes.

## Fase 4: atualizações de referência cruzada

Atualize **`/help/blueprints/TOC.md`** para adicionar a nova página à navegação. Esta é a única página de referência cruzada a ser atualizada.

Leia `./references/toc-placement.md` para a tabela e as regras de mapeamento de subseção completas. Resumo:

| Pasta de tópico | Subseção do índice |
| --- | --- |
| `experience-platform/` | `+ Architecture overviews{#architecture-overview}` |
| `experience-platform/deployment/` | `+ Deployment{#deployment}` (subseção de visões gerais de Arquitetura) |
| `audience-activation/` | `+ Audience & Profile Activation{#audience-activation}` |
| `b2b/` | `+ B2B activation & marketing{#b2b-activation}` |
| `customer-journey-analytics/` | `+ Customer Journey Analytics{#customer-journey-analytics}` |
| `customer-journeys/` | `+ Customer journeys{#customer-journeys}` |

Formato de entrada (recuo de 4 espaços + `+`):

```
    + [{Page title}](/help/blueprints/{topic-folder}/{filename}.md)
```

Anexe a nova entrada como o último item na subseção correspondente, a menos que o usuário especifique uma posição diferente. Preservar o recuo exato de 4 espaços — A análise do índice depende dele.

**Inspecionar subgrupos aninhados antes de posicionar.** Algumas subseções (notadamente `Audience & Profile Activation`) contêm agrupamentos aninhados (por exemplo, `Real-Time Customer Data Platform (RTCDP) {#known-customer-audience-activation}`). Leia a subseção afetada do TOC.md antes de editar. As novas páginas de arquitetura de nível superior pertencem ao nível de recuo de quatro espaços da subseção — **não** dentro de um subgrupo aninhado (que usa recuo de seis espaços). Coloque a nova entrada após a última entrada de subgrupo aninhada e antes do cabeçalho da próxima subseção de nível superior.

## Fase 5: validação

Depois que todos os arquivos forem criados e atualizados, verifique o seguinte e relate qualquer falha ao usuário:

1. **Existência de ativos de imagem** — Para cada diagrama, verifique se `/help/blueprints/{topic-folder}/assets/{filename}` existe. **Avisar** se estiver ausente; não bloquear (o usuário pode estar criando em paralelo com o design do diagrama). Exiba uma lista clara dos arquivos ausentes para que o usuário saiba o que adicionar.

2. **Links padrão de caso de uso** — Cada link padrão no arquivo aponta para um arquivo de Markdown existente em `/help/blueprints/use-case-patterns/`. Use a pesquisa de espaço de trabalho ou a leitura de arquivo para confirmar se cada destino existe.

3. **Links do Experience League** — Verifique se cada URL na seção `## Further reading` começa com `https://experienceleague.adobe.com/`.

4. **Posicionamento da entrada do índice** — A nova entrada está dentro da subseção correta, usa recuo de quatro espaços e o caminho corresponde exatamente ao local do arquivo gerado.

5. **Nomeação do arquivo** — O nome do arquivo da página é kebab-case e corresponde ao caminho referenciado no TOC.md.

6. **Conclusão do Frontmatter** — A página inclui `title`, `description` e `solution`. Deve **não** incluir `exl-id`, `product_v2`, `feature_v2`, `role_v2`, `topic_v2`, `TQID`, `kt` ou `thumbnail`.

Corrija quaisquer problemas de validação antes de considerar a tarefa como concluída.

## Notas

- Sempre use a sintaxe `[!DNL ...]` para nomes de produtos do Adobe no corpo do texto e em marcadores, seguindo a convenção de páginas existentes.
- Os diagramas de arquitetura normalmente são SVG (preferidos para nitidez e dimensionamento), mas PNG é aceitável para arte-final raster.
- A cadeia de caracteres de estilo embutido `<img>` (`border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;`) e `class="modal-image"` são necessárias — elas habilitam a interação de zoom modal do Experience League.
- Se o usuário estiver criando uma página para uma pasta de tópico totalmente nova que ainda não existe, avise-o de que o TOC.md precisa de uma nova subseção de nível superior em `+ Architecture Diagrams and Blueprints{#architecture-diagrams}`. Trate isso como uma etapa separada com a aprovação explícita do usuário.
- Se o diagrama de arquitetura documenta extensivamente um *único caso de uso de ponta a ponta* (com KPIs, objetivos de negócios, recursos), redirecione o usuário para `use-case-pattern-builder` — essa não é uma página de arquitetura.
