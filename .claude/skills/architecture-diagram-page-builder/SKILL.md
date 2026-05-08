---
name: architecture-diagram-page-builder
description: 'Criação de guias de novas páginas de diagrama de arquitetura para o repositório de blueprints do Adobe Experience Platform. Use essa habilidade ao adicionar um novo diagrama de arquitetura de nível superior, uma página de arquitetura de integração ou uma visão geral da arquitetura do aplicativo. As páginas de arquitetura abordam o AEP de nível superior, as arquiteturas de aplicativos e os principais pontos de integração, e não casos de uso aprofundado (que pertencem ao construtor de padrões de casos de uso). Lida com o fluxo de trabalho completo: coleta de informações da página, geração do arquivo de marcação, colocação dele na pasta de tópico correta e atualização do TOC.md.'
source-git-commit: 83e85d946e455cde46001af0a2112637b7fe24cc
workflow-type: tm+mt
source-wordcount: '1396'
ht-degree: 2%

---


# Diagrama de arquitetura do Page Builder

Essa habilidade orienta a criação de novas páginas de diagrama de arquitetura para o repositório de blueprints do Adobe Experience Platform. As páginas de diagrama de arquitetura fornecem referências visuais de alto nível sobre como os aplicativos do AEP e do Adobe se encaixam, os dados principais fluem entre eles e os pontos de integração que os autores precisam estar cientes ao projetar soluções.

## Escopo

As páginas de diagrama de arquitetura são **páginas focalizadas, com estilo de referência** — normalmente entre 40 e 100 linhas de marcação — que contêm:

- Um ou mais diagramas de arquitetura com explicações resumidas da finalidade de cada diagrama
- Links para padrões de caso de uso que a arquitetura aceita (a página de arquitetura não duplica esse conteúdo)
- Uma pequena lista dos fluxos de dados principais e pontos de integração ilustrados
- Links do Experience League para obter mais informações sobre o domínio do aplicativo

Eles **não** o local para conteúdo de casos de uso detalhados. Os KPIs, os objetivos comerciais, os exemplos de caso de uso tático, as cadeias de função e as narrativas pessoais pertencem às páginas de padrão de caso de uso, geradas pela habilidade `use-case-pattern-builder`. Consulte `references/scope-guardrails.md` para obter as medidas de proteção completas.

## Leitura necessária antes de iniciar

Leia os seguintes arquivos de referência para modelos e regras:

- `references/diagram-template.md` — o modelo de marcação completa com valores de espaço reservado
- `references/toc-placement.md` — tabela de mapeamento de subseção e formato de entrada para TOC.md
- `references/scope-guardrails.md` — regras para o que pertence a uma página de arquitetura vs. uma página de padrão de caso de uso

## Fase 1: Coleta de informações

Entrevistar o usuário para coletar todas as informações necessárias antes de gerar quaisquer arquivos. Não prossiga para a geração de conteúdo até que cada item necessário seja fornecido ou explicitamente adiado.

### Informações necessárias

1. **Título da página** — o título legível (por exemplo, `Adobe Journey Optimizer architecture diagrams`).

2. **Pasta de tópico** — Onde a página está. Escolha exatamente um com base no domínio primário do diagrama:
   - `experience-platform/` — AEP de nível superior, vários aplicativos ou diagramas de nível de plataforma
   - `customer-journeys/` — Orquestração de AJO, Campanha, jornada
   - `customer-journey-analytics/` — Arquiteturas CJA
   - `audience-activation/` — RTCDP, público-alvo e ativação de perfil
   - `b2b/` — Arquiteturas específicas de B2B

3. **Filename** — Kebab-case, derivado do título da página (por exemplo, `Journey Optimizer architecture` -> `journey-optimizer-architecture.md`). Confirme com o usuário.

4. **Finalidade da página** — frases 1-2 que descrevem o que os diagramas ilustram coletivamente. Usado para o campo de primeiro plano `description` e o parágrafo de abertura.

5. **Soluções da Adobe** — Lista separada por vírgulas de produtos Adobe centrais para a página. Usado para o campo de interesse `solution`. Exemplos: `Experience Platform, Journey Optimizer, Customer Journey Analytics`.

6. **Diagramas** — Um ou mais diagramas. Para cada diagrama, colete:
   - **Nome do arquivo de imagem** (por exemplo, `aep_data_flow.svg`). SVG preferencial; PNG aceitável.
   - **Título da seção** — torna-se o cabeçalho H2 do diagrama (por exemplo, `Data flow diagram`, `Detailed architecture diagram`).
   - **Explicação de finalidade** — 1-2 frases descrevendo o que o diagrama mostra.
   - **Texto alternativo** — descrição curta acessível.

7. **Padrões de caso de uso com suporte** — 2-5 padrões existentes que esta arquitetura habilita.

   **Recomendar candidatos primeiro.** Antes de pedir ao usuário para fornecer padrões, verifique `/help/blueprints/use-case-patterns/` e proponha 3 a 6 correspondências prováveis com base no título da página, finalidade da página e soluções da Adobe coletadas acima. Para cada sugestão, apresente:
   - Nome do padrão (com o caminho vinculado)
   - Fundamentação de uma frase para o porquê de se encaixar nessa arquitetura

   Apresente as sugestões como uma lista restrita numerada e peça ao usuário para (a) aceitar qualquer, (b) rejeitar qualquer e (c) adicionar padrões que você perdeu. Gere apenas sugestões que apontem para arquivos reais — glob/read para confirmar antes de sugerir. Não alucinar nomes de padrões.

   Para cada padrão aceito, capture a categoria e o nome do arquivo. Validar se cada arquivo existe em `/help/blueprints/use-case-patterns/{category}/{pattern-file}.md` antes de gerar.

8. **Fluxos de dados primários/pontos de integração** — 3 a 7 marcadores que descrevem os fluxos principais e os limites de integração exibidos nos diagramas (por exemplo, `Real-time event ingestion from Web SDK to Edge Network`, `Profile synchronization between Experience Platform Hub and Edge`).

9. **Links do Experience League** — links 3-6 para a documentação relevante do Experience League para outras leituras. Cada um deve começar com `https://experienceleague.adobe.com/pt-br`.

   **Recomendar candidatos primeiro.** Com base nas soluções da Adobe e na finalidade da página, proponha de 4 a 8 artigos plausíveis do Experience League (por exemplo, as páginas de aterrissagem ou de visão geral canônicas de cada solução nomeada, os principais guias de integração e as referências de implantação). Para cada sugestão, apresente:
   - Título do artigo
   - URL
   - Fundamento em uma linha para o porquê de se ajustar à página

   Marque as sugestões como **não verificadas** a menos que você tenha buscado a URL — o usuário deve confirmar ou substituir cada uma antes que ela chegue ao arquivo gerado. Peça ao usuário para (a) aceitar, (b) substituir qualquer URL por um URL verificado que já tenha e (c) adicionar o seu próprio URL. Nunca invente URLs que você não tenha visto; se não tiver certeza, sugira o título do artigo e permita que o usuário forneça o URL.

### Opcional

- **Balão de conteúdo relacionado** — um único link renderizado como bloco `>[!MORELIKETHIS]` próximo à parte superior da página. Útil quando há uma integração irmã ou guia de configuração no Experience League do qual o leitor deve estar ciente.

Se o usuário não fornecer todos os itens necessários, peça os que estão faltando antes de continuar. Não fabrique diagramas, padrões ou links.

## Fase 2: Verificação do escopo

Antes de gerar, leia novamente as descrições do diagrama do usuário, os marcadores de fluxo de dados e qualquer proposta de rascunho. Aplicar as medidas de proteção de `references/scope-guardrails.md`.

Se qualquer um dos itens a seguir for exibido no conteúdo planejado, avise o usuário e se ofereça para redirecionar essa seção para uma página de padrão de caso de uso (ou apare-o da página de arquitetura):

- KPIs ou fórmulas de medição
- Objetivos ou narrativas de impacto nos negócios
- Exemplos de caso de uso tático (cenários de personalização específicos, exemplos de campanha etc.)
- Cadeias de funções (`A > B > C > D` estilo)
- Narrativa orientada por pessoas

Se o conteúdo planejado permanecer no escopo da página de arquitetura (arquitetura de nível superior, fluxo de dados do sistema, pontos de integração, topologia de implantação, borda versus hub), confirme com o usuário e prossiga para a Fase 3.

## Fase 3: Geração de conteúdo

Gere a página em:

```
/help/blueprints/{topic-folder}/{kebab-filename}.md
```

Use `references/diagram-template.md` como modelo de origem. Preencha todos os valores de espaço reservado com as informações coletadas. O arquivo gerado deve incluir:

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

Leia `references/toc-placement.md` para a tabela e as regras de mapeamento de subseção completas. Resumo:

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

## Fase 5: validação

Depois que todos os arquivos forem criados e atualizados, verifique o seguinte e relate qualquer falha ao usuário:

1. **Existência de ativos de imagem** — Para cada diagrama, verifique se `/help/blueprints/{topic-folder}/assets/{filename}` existe. **Avisar** se estiver ausente; não bloquear (o usuário pode estar criando em paralelo com o design do diagrama). Exiba uma lista clara dos arquivos ausentes para que o usuário saiba o que adicionar.

2. **Links padrão de caso de uso** — Cada link padrão no arquivo aponta para um arquivo de Markdown existente em `/help/blueprints/use-case-patterns/`. Use `Read` ou glob para confirmar se cada destino existe.

3. **Links do Experience League** — Verifique se cada URL na seção `## Further reading` começa com `https://experienceleague.adobe.com/pt-br`.

4. **Posicionamento da entrada do índice** — A nova entrada está dentro da subseção correta, usa recuo de quatro espaços e o caminho corresponde exatamente ao local do arquivo gerado.

5. **Nomeação do arquivo** — O nome do arquivo da página é kebab-case e corresponde ao caminho referenciado no TOC.md.

6. **Conclusão do Frontmatter** — A página inclui `title`, `description` e `solution`. Deve **não** incluir `exl-id`, `product_v2`, `feature_v2`, `role_v2`, `topic_v2`, `TQID`, `kt` ou `thumbnail`.

Corrija quaisquer problemas de validação antes de considerar a tarefa como concluída.

## Notas

- Sempre use a sintaxe `[!DNL ...]` para nomes de produtos do Adobe no corpo do texto e em marcadores, seguindo a convenção de páginas existentes.
- Os diagramas de arquitetura normalmente são SVG (preferidos para nitidez e dimensionamento), mas PNG é aceitável para arte-final raster.
- A cadeia de caracteres de estilo embutido `<img>` (`border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;`) e `class="modal-image"` são necessárias — elas habilitam a interação de zoom modal do Experience League.
- Se o usuário estiver criando uma página para uma pasta de tópico totalmente nova que ainda não existe, avise-o de que o TOC.md precisa de uma nova subseção de nível superior em `+ Architecture Diagrams and Blueprints{#architecture-diagrams}`. Trate isso como uma etapa separada com a aprovação explícita do usuário.
- Se o diagrama de arquitetura documenta extensivamente um *único caso de uso de ponta a ponta* (com KPIs, objetivos de negócios, cadeia de funções), redirecione o usuário para `use-case-pattern-builder` — essa não é uma página de arquitetura.
