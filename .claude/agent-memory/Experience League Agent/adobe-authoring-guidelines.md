---
name: Adobe Experience League Authoring Guidelines
description: Referência completa das regras de criação do Markdown da Adobe Experience League, rastreada do guia de criação oficial em março de 2026.
type: reference
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 0%

---


# Diretrizes de criação da Adobe Experience League

Source: https://experienceleague.adobe.com/en/docs/authoring-guide/using/home
Rastreado: 15/03/2026

---

## &#x200B;1. METADADOS / MATÉRIA PRINCIPAL

### Campos obrigatórios
| Campo | Requisito | Regras |
|---|---|---|
| `title` | Obrigatório | Máximo de 60 caracteres (inglês). Caixa do título. Nenhum nome de produto, a menos que seja necessário para maior clareza. Anexos do sistema &quot; | ProductName&quot; automaticamente. Coloque aspas se contiver dois pontos ou colchetes. |
| `description` | Obrigatório | 150-160 caracteres no máximo. Não pode ser vazio/nulo. Os conceitos começam com &quot;Saiba mais sobre...&quot; As tarefas começam com &quot;Saiba como...&quot; ou imperativo. |

### Campos opcionais usados com frequência
| Campo | Valores válidos | Notas |
|---|---|---|
| `feature` | Deve corresponder aos valores YAML do recurso; letra maiúscula ou minúscula com espaços (por exemplo, &quot;Fragmento de conteúdo&quot;) | 1 a 2 por artigo; exibições em Tópicos |
| `feature-set` | Deve validar em relação ao recurso YAML | Aplicativo principal do recurso |
| `role` | Usuário, Desenvolvedor, Líder, Administrador, Arquiteto, Arquiteto de dados, Engenheiro de dados | Diferencia maiúsculas de minúsculas; é exibido como &quot;Criado para&quot; |
| `level` | Iniciante, intermediário, experiente | O padrão é Iniciante, se não especificado |
| `solution` | Deve corresponder à solução YAML (por exemplo, &quot;Campaign, Campaign Standard v7&quot;) | Vários valores permitidos; usados para filtragem de pesquisa |
| `topic` | Deve corresponder ao tópico YAML; capitalização do título com espaços | Para filtragem entre produtos (por exemplo, &quot;Integrações&quot;) |
| `type` | Documentação, tutorial, solução de problemas | Nível do repositório; o padrão é Documentação |
| `short-description` | Uma frase, máx. 20 palavras | Para páginas de aterrissagem ExL quando a descrição é muito longa |
| `badgePremium` | `label="Premium" type="Positive" url="..."` | Selo de nível de página |
| `mini-toc-levels` | 1-6 (padrão 2) | Controla a profundidade de exibição do cabeçalho de navegação à direita |
| `hidefromtoc` | verdadeiro/falso | Exclui da navegação à esquerda, mas mantém o URL acessível |

### Posicionamento de metadados
- Nível do artigo: parte superior do arquivo do Markdown como assunto principal do YAML
- Nível de índice: no arquivo TOC.md
- Nível do repositório: no arquivo metadata.md

### Regras-chave de formatação
- Quebrar valores contendo vírgulas ou colchetes entre aspas
- Vários valores separados por vírgulas
- Correspondência de diferenciação entre maiúsculas e minúsculas em relação a definições YAML
- Valores de tag vazios/em branco causam falha na validação

### Campos obsoletos
seo-title, seo-description, público-alvo, dificuldade, uuid (da era de migração)

---

## &#x200B;2. SINTAXE DO MARKDOWN (COM SABOR DE ADOBE)

### Formatação de texto
- Negrito: `**text**`
- Itálico: `*text*`
- Negrito + Itálico: `***text***`
- Evitar caracteres especiais: usar a barra invertida `\` antes de `# { } [ ] * + - . !`
- Entidades HTML: `&lt;` `&gt;` `&amp;` `&mdash;` `&ndash;`

### Cabeçalhos
- Usar estilo ATX (somente sintaxe `#`, nunca sublinhado/estilo setext)
- Um H1 por documento (geralmente o título da página que corresponde aos metadados `title`)
- Todos os títulos subsequentes H2 (`##`) ou inferior
- Linhas em branco necessárias antes e depois das rubricas (exceto a primeira rubrica)
- Máximo de 69 caracteres (inglês) / 120 caracteres (localizado)
- Máximo de ~5 palavras preferidas
- Primeira letra maiúscula para todos os cabeçalhos (colocar apenas a primeira palavra e os substantivos próprios em maiúscula)
- Caso de título SOMENTE para o campo de metadados `title`
- Sem pontuação final (pontos de interrogação permitidos nos cabeçalhos de perguntas frequentes)
- IDs de âncora personalizadas: `## Title {#custom-id}` — use hifens, não pontos
- Nenhuma ID de âncora de cabeçalho duplicada em um documento
- Evite nomes de âncora reservados: pesquisa, resultados, facetas, paginação, classificação, consulta, caixa de pesquisa, conteúdo, cabeçalho, rodapé, principal, navegação, barra lateral, página, contêiner, invólucro
- Siga cada cabeçalho com pelo menos um parágrafo do corpo de texto (não coloque listas/tabelas diretamente após um cabeçalho)
- Cabeçalhos do conceito: frases substantivas/substantivas
- Cabeçalhos de tarefas: verbos imperativos (NÃO gerúndios — &quot;Criar um segmento&quot; e não &quot;Criar um segmento&quot;)
- Estrutura paralela em níveis de cabeçalho

### Listas
- Marcador (não ordenado): `*`, `-` ou `+` — use de forma consistente em um documento
- Encomendado: `1.` para cada item (números automáticos)
- Linhas em branco antes e depois das listas
- Recuar itens numerados aninhados 3 espaços; marcadores aninhados 2 espaços
- Pontuação com marcadores: omita ponto e vírgula/vírgulas/conjunções no final; adicione pontos somente para frases completas
- Não adicione pontos se todos os itens tiverem ≤ 3 palavras ou forem rótulos/cabeçalhos de interface do usuário

### Links
- Externo: `[text](https://url.com)`
- Relativo (mesmo nível): `[text](file.md)`
- Relativo de raiz: `[text](/help/path/file.md)` — deve começar com `/`
- Deep links (mesma página): `[text](#heading-anchor)`
- Deep links entre documentos: `[text](file.md#heading-id)`
- Forçar nova guia: `[text](url){target="_blank"}`
- URLs simples: quebrar entre colchetes `<https://example.com>` para tornar clicável
- Links de referência: somente links absolutos funcionam para links de estilo de referência
- Não inclua o mesmo arquivo em vários locais do índice por meio de links relativos
- Usuários do Windows: converter barras invertidas em barras invertidas em caminhos

### Imagens
- Básico: `![alt text](image.png "hover tooltip")`
- Redimensionar: `{width="300"}`
- Alinhar: `{align="center"}` ou `{align="right"}`
- Zoom: `{zoomable="yes"}` ou `{modal="regular"}`
- Tamanho máximo do arquivo: 100 MB (recomendado abaixo de 5 MB)
- O texto alternativo é OBRIGATÓRIO para todas as imagens (para SEO e acessibilidade)
- Nomes de arquivo de imagem: minúsculas com hifens
- Armazenar imagens em uma pasta de ativos designada

### Blocos de código
- Inline: backticks `` `code` ``
- Usar para: nomes de arquivos, URLs, termos definidos pelo usuário, comandos
- Blocos de código cercados: três backticks com identificador de linguagem

  ```
  ```javascript
  code here
  ```

  ```
  
  
- Opções: `{line-numbers="true"}`, `{start-line="7"}`, `{highlight="11-13, 16"}`
- Sempre incluir um identificador de idioma em blocos de código cercados

### Tabelas
- A linha separadora requer pelo menos 3 hifens por coluna: `|---|---|---|`
- Alinhamento: esquerda `|---|`, centro `|:---:|`, direita `|---:|`
- Escape de barras literais: `\|` ou use `&vert;`
- Tabelas HTML permitidas; use `<table style="table-layout:auto">` ou `table-layout:fixed`
- Alinhamento da tabela do HTML: `<td align="left|center|right">`
- Evitar a sintaxe do Markdown dentro de tabelas do HTML (por exemplo, `[!NOTE]` não funciona em tabelas do HTML)
- Remover bordas: `<tr style="border: 0;">`
- Opção de layout de tabela do Markdown: adicionar `{style="table-layout:auto"}` após tabela com linhas em branco
- Evite tabelas muito largas/altas devido a problemas de visibilidade da barra de rolagem horizontal

---

## &#x200B;3. EXTENSÕES ESPECIAIS DO ADOBE SYNTAX

### Chamadas/Avisos

```
>[!NOTE]
>
>Text here.

>[!TIP]
>
>Text here.

>[!IMPORTANT]
>
>Text here.

>[!WARNING]
>
>Text here.

>[!CAUTION]
>
>Text here.

>[!ADMIN]
>[!AVAILABILITY]
>[!PREREQUISITES]
>[!INFO]
>[!ERROR]
>[!SUCCESS]
```
- CRÍTICO: Nenhum espaço entre `>` e `[!` — use `>[!NOTE]` NOT `> [!NOTE]`
- Adicionar linha em branco entre `>[!NOTE]` e a linha de texto do corpo

### Guias

```
>[!BEGINTABS]

>[!TAB iOS]
Content here

>[!TAB Android]
Content here

>[!ENDTABS]
```

### Seções flexíveis (acordeões)

```
+++Click to expand
Content inside
+++
```
Observação: NÃO há suporte para seções agrupáveis aninhadas.

### Sombrear Caixas

```
>[!BEGINSHADEBOX "Optional Title"]
Content here
>[!ENDSHADEBOX]
```

### Vídeos

```
>[!VIDEO](https://video.tv.adobe.com/v/ID/?quality=12&learn=on)
```
Adicionar `{transcript=true}` para transcrições.

### Mais artigos como este

```
>[!MORELIKETHIS]
>* [Article 1](url)
>* [Article 2](url)
```

### Ajuda contextual

```
>[!CONTEXTUALHELP]
>id="..."
>title="..."
>abstract="..."
>additional-url="..."
```

### Medalhas (em linha)

```
[!BADGE Label]{type=Informative url="https://example.com" tooltip="text"}
```
Tipos: `Informative` (azul), `Positive` (verde), `Negative` (vermelho), `Neutral` (cinza), `Caution` (amarelo)

### Realce do Texto (Visualização)

```html
<span class="preview">highlighted text</span>
```

### Inclusões e trechos
- Incluir todo o arquivo: `{{$include /help/_includes/legal-blurb.md}}`
- Trecho (nenhum cabeçalho): `{{snippet-id}}`
- Armazenar arquivos reutilizáveis na pasta `help > _includes/`
- Trechos armazenados em `help > _includes/snippets.md`
- Inclui pode ter cabeçalhos; trechos NÃO PODEM
- Funciona somente no mesmo repositório (não entre repositórios)
- Evitar `{{` ou `}}` caracteres em arquivos sem referência

### Tag DNL (Do Not Localize)
- `[!DNL ProductName]` — envolve nomes de produtos/marcas que não devem ser traduzidos
- Usar na primeira menção ou em menção de destaque em uma página

### Tag UICONTROL
- `[!UICONTROL Button Label]` — envolve o texto do elemento da interface do usuário (botões, menus, nomes de campos)
- Garante que as sequências de caracteres da interface do usuário sejam extraídas dos bancos de dados de produtos em vez de serem traduzidas automaticamente
- Sem apóstrofos, aspas ou pontuação nas tags UICONTROL
- Usar formatação em negrito para elementos da interface referenciados em etapas

### Recursos não suportados
- Listas de tarefas (caixas de seleção)
- Emoji
- Réguas horizontais
- Seções recolhíveis aninhadas

---

## &#x200B;4. NOMEAÇÃO DE ARQUIVOS E ESTRUTURA DE PASTAS

### Regras de nomenclatura de arquivo
- Somente nomes de arquivo em minúsculas com hifens
- Sem maiúsculas, sublinhados, pontos ou espaços
- Nomes descritivos compatíveis com SEO (por exemplo, `calculated-metric-overview.md` não `cmo.md`)
- Evite números em nomes de arquivo; use palavras descritivas
- Evite nomes reservados/conflitantes: `metadata.md`, `search.md`
- A renomeação de arquivos ativos requer o gerenciamento de redirecionamento (alterações de URL)

### Estrutura de pastas
- Nomes de diretório/pasta NÃO afetam URLs (somente nomes de repositório e nomes de arquivo afetam URLs)
- O TOC.md controla a hierarquia de navegação, não o local da pasta Git
- Armazenar imagens/ativos em uma pasta de ativos designada
- Inclusões reutilizáveis armazenadas em `help/_includes/`
- Trechos armazenados em `help/_includes/snippets.md`

### Regras do TOC.md
- Todos os artigos devem ser listados no TOC.md para renderização no Experience League
- Formato H1: `# Guide Title {#anchor-id}` — a âncora gera um caminho de URL base
- Os cabeçalhos de seção devem ter IDs de âncora: `+ Section Name {#section-id}`
- Os cabeçalhos de seção (itens principais) não podem ser links em si
- Links de artigo: `+ [Title](path/file.md)`
- A alteração das IDs de âncora da seção altera todos os URLs de artigo aninhados (requer redirecionamentos)
- Usar estilo de marcador consistente em todo o (`+`, `*` ou `-`)
- Metadados do sumário: `user-guide-description`, opcionalmente `breadcrumb-title`
- `mini-toc-levels`: controla a exibição do cabeçalho de navegação à direita (1-6, padrão 2)

---

## &#x200B;5. QUALIDADE DO CONTEÚDO E PADRÕES EDITORIAIS

### Voz e Tom
- Voz ativa preferida sobre passiva
- O tempo presente sobre o tempo futuro
- Segunda pessoa (&quot;você&quot;) para conteúdo instrutivo
- Frases com menos de 35 palavras
- Verbos fortes e precisos - evite advérbios fracos (&quot;muito&quot;, &quot;extremamente&quot;)

### Etapas / Procedimentos
- Cada etapa é UM único comando conciso (uma frase)
- As informações adicionais vão para a próxima linha (recuadas abaixo da etapa)
- Iniciar cada etapa com um verbo imperativo
- Limite os procedimentos em aproximadamente 7 etapas (máx. ~10 antes de dividir em subtarefas)
- Colocar informações conceituais ANTES das etapas
- Coloque capturas de tela APÓS a etapa relevante
- Repetir nomes de página/guia para orientação do leitor
- Formatação de UICONTROL em negrito para elementos de UI em etapas

### Terminologia da interface
- **Abrir/Fechar**: aplicativos e programas
- **Ir para**: menus, guias ou locais da interface
- **Selecionar**: texto, células ou opções de listas
- **Clique**: ações do mouse (evite especificar o tipo de controle, a menos que seja essencial)
- **Menu suspenso** (não &quot;lista suspensa&quot;)

### Nomes de produto
- Não adicione o nome do produto a títulos/cabeçalhos, a menos que isso seja necessário por motivos de clareza
- Omitir &quot;o&quot; antes dos nomes de produtos
- Incluir &quot;Adobe&quot; na primeira menção no nível do guia (requisito de marca comercial)
- Solte &quot;Adobe&quot; em menções secundárias, a menos que seja legalmente exigido
- Usar tags DNL para nomes de produtos para evitar erros de tradução

### Ênfase e Formatação
- Negrito: elementos da interface do usuário e ações do teclado
- Itálico: mensagens de erro, palavras estrangeiras, ênfase
- Código (backticks): Nomes de arquivos, URLs, termos definidos pelo usuário
- Não há aspas nos elementos da interface do usuário (use a tag UICONTROL )

### Uso de maiúsculas
- Primeira letra da frase para cabeçalhos, navegação, subcabeçalhos
- Caso de título SOMENTE para o campo de metadados `title`
- Substantivos próprios sempre com inicial maiúscula

---

## &#x200B;6. PRÁTICAS RECOMENDADAS DA SEO

- Um H1 por página — deve ser conciso, descritivo, informar aos usuários sobre o que se trata a página
- Hierarquia de cabeçalho sequencial (h1 → h2 → h3, nunca ignore níveis)
- Incluir palavras-chave em H1, corpo de texto e metadados (não a meta tag `keywords` — a Google a ignora)
- Evite o uso de palavras-chave (intenção > frequência)
- Título: máx. de 50 a 60 caracteres; anexos de sistema &quot;| Adobe&quot; automaticamente
- Descrição: 150-160 caracteres; deve ser um call to action, não uma repetição de conteúdo
- Adicionar texto alternativo descritivo a todas as imagens
- Incluir transcrições de vídeo (os mecanismos de pesquisa só podem ler o texto)
- Vincular estrategicamente a páginas relacionadas (evitar páginas órfãs)
- Incluir elementos estruturados: listas numeradas, subtítulos, blocos de código
- Use ferramentas como AnswerThePublic e Google Trends para pesquisar palavras-chave
- O conteúdo deve demonstrar o E-E-A-T (experiência, conhecimento, capacidade de autoridade, confiabilidade)

---

## &#x200B;7. LOCALIZAÇÃO

### Tradução automática primeiro
- Inglês source content autogenerated versions localized
- Idiomas suportados: alemão, francês, japonês, italiano, espanhol, português brasileiro, chinês simplificado, chinês tradicional, coreano, holandês, sueco

### Gravação para localização
- Terminologia consistente no
- Frases curtas e voz ativa
- Ordem de palavras padrão em inglês (sujeito → verbo → objeto)
- Usar pronomes relativos (&quot;that&quot;, &quot;which&quot;)
- Evite: humor, expressões idiomáticas, jargão, frases regionais, metáforas, palavras desnecessárias

### Tags de localização
- `[!UICONTROL Label]` — garante que as cadeias de caracteres da interface do usuário sejam extraídas do banco de dados do produto, não traduzidas por máquina
- `[!DNL ProductName]` — impede que os nomes de produtos/marcas sejam traduzidos
- As imagens em uma pasta &quot;não traduzir&quot; são excluídas da localização

---

## &#x200B;8. TIPOS DE CONTEÚDO

- **Guia**: coleção online de páginas referenciadas em um índice; aborda as práticas recomendadas oficiais
- **Tutorial**: conteúdo instrucional (vídeo ou texto) para casos de uso específicos; publicado em aprender repositórios
- **Guia de Referência**: APIs/SDKs de desenvolvedor; geralmente formato de tabela; publicado em developer.adobe.com
- **Curso**: coleção de lições com curadoria de especialistas que direcionam funções de usuário específicas
- **Artigos da Base de Dados de Conhecimento**: conteúdo de solução de problemas breve e temporariamente relevante
- **Página de aterrissagem/Página inicial**: gerenciado separadamente (SCCM)

---

## &#x200B;9. ERROS COMUNS DE VALIDAÇÃO A SEREM EVITADOS

- `title` ou `description` metadados ausentes ou em branco
- `description` não começa com &quot;Saiba mais sobre...&quot; ou &quot;Saiba como...&quot;
- Espaço entre `>` e `[!` na sintaxe de texto explicativo (`> [!NOTE]` em vez de `>[!NOTE]`)
- Espaços em negrito: `**text **` (espaço à direita quebra negrito)
- Sintaxe de Markdown dentro de tabelas do HTML (por exemplo, chamadas de retorno não funcionam lá)
- IDs de âncora de cabeçalho duplicadas em um documento
- IDs de âncora contendo pontos (use hifens)
- Uso de nomes de âncora reservados (pesquisa, resultados, cabeçalho, rodapé etc.)
- `role`, `level`, `feature`, `topic` valores que não correspondem às definições YAML
- Cabeçalhos empilhados sem corpo de texto entre eles
- H1 usado mais de uma vez por documento
- Níveis de cabeçalho ignorados (por exemplo, H1 → H3)
- Nomeação de arquivo com maiúsculas, sublinhados ou espaços
- Texto alternativo ausente em imagens
- Gerar cabeçalhos de tarefa (&quot;Criando...&quot;) em vez de &quot;Criar...&quot;)
