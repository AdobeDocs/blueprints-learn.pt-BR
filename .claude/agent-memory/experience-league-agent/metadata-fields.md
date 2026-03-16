---
source-git-commit: a632042b3a7434dd88f52804e15e30fa06057e3b
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 1%

---
# Adobe Experience League — Referência de campos de metadados aprovados

*Originado no Guia de Criação do Adobe ExL (rastreado em fevereiro de 2026) + análise de repositório de blueprints-learn.en*

---

## Hierarquia de metadados

Os metadados ficam em cascata nessa ordem (o artigo substitui o índice, o índice substitui o repositório):
1. Assunto principal do artigo (prioridade mais alta)
2. TOC.md no guia do usuário
3. metadata.md na raiz do repositório (prioridade mais baixa)

---

## Campos de nível de artigo

### OBRIGATÓRIO

| Campo | Descrição | Formato / Restrições |
|-------|-------------|----------------------|
| `title` | Título da página de SEO. Aparece nos resultados da pesquisa. | Máximo de ~60 caracteres; primeira letra maiúscula; use `[!DNL Product]` para nomes de produtos; NÃO duplique H1 exatamente, a menos que pretendido |
| `description` | Descrição do Meta para mecanismos de pesquisa e recomendações do ExL. | 150 a 160 caracteres; o ideal é iniciar com &quot;Aprenda a...&quot; ou &quot;Saiba mais sobre...&quot;; a validação falha se ausente/nulo |
| `exl-id` | Identificador exclusivo atribuído pelo sistema. Usado para rastreamento de conteúdo. | Formato UUID (por exemplo, `70573eb9-cd69-4fe6-b2ae-dae81665a308`); **excluir ao copiar um arquivo** — ele será atribuído automaticamente; nunca duplicar entre arquivos |

### ALTAMENTE RECOMENDADO

| Campo | Descrição | Valores válidos |
|-------|-------------|--------------|
| `solution` | Produtos Adobe que o artigo abrange. Usado para pesquisa/filtragem do ExL e recomendações de conteúdo. | Separado por vírgulas; diferencia maiúsculas de minúsculas; deve corresponder a enum aprovada (consulte Valores de solução válidos abaixo) |

### OPCIONAL — COMUM

| Campo | Descrição | Valores/Observações Válidos |
|-------|-------------|----------------------|
| `kt` | Número JIRA do artigo de conhecimento herdado. Usado para rastreamento de análise. | Inteiro (por exemplo, `7207`); aceitável em branco; aceitável `null` |
| `thumbnail` | Referência de imagem em miniatura para recommendations/analytics. | Cadeia de caracteres de nome de arquivo ou `null` ou em branco |
| `version` | Filtro da versão do produto. Usado principalmente para blueprints do AEM e do Campaign. | E.g. `Campaign v8`, `Campaign v8 Client Console`; deve corresponder a version.yml |
| `doc-type` | Classificação de conteúdo usada em acordos de recompra/análises. | `blueprint`, `overview-page`, `Video`, `Tutorial`, `Troubleshooting` (preferencial minúsculas) |
| `feature` | Tags de tópico exibidas como &quot;Tópicos&quot; nas páginas ExL. | 1 a 2 por artigo; primeira letra maiúscula; deve corresponder a feature.yml; separado por vírgulas |
| `feature-set` | Aplicativo pai para validação de recursos. | Deve corresponder aos valores de feature.yml |
| `role` | Função do público-alvo. Exibido como &quot;Criado para&quot; no ExL. | `Admin`, `Architect`, `Data Architect`, `Data Engineer`, `Developer`, `Leader`, `User` |
| `level` | Nível de experiência do usuário. Exibido como &quot;Criado para&quot; no ExL. | `Beginner`, `Intermediate`, `Experienced` (letra maiúscula) |
| `topic` | Tópicos entre produtos para pesquisa/filtragem. | Caixa do título; deve corresponder a topic.yml; separada por vírgulas |
| `type` | Classificação do guia. | `Documentation` (padrão), `Tutorial`, `Troubleshooting` |
| `last-substantial-update` | Exibe o conteúdo em widgets &quot;Novidades&quot;. | Formato: `YYYY-MM-DD` |
| `hide` | Exclui a página de todas as pesquisas e recomendações; também define o índice como não. | `yes` ou `no` |
| `hidefromtoc` | Remove da navegação do sumário, mas a página ainda pode ser acessada por meio de um link direto. | `yes` ou `no` |
| `index` | Controla se a página aparece na pesquisa/mapa de site externo. | `yes`/`no` ou `y`/`n`; padrão: `no` (indexado) |
| `recommendations` | Controla o comportamento do widget &quot;Mais ajuda sobre este recurso&quot;. | `noDisplay` (impede a exibição do widget), `noCatalog` (exclui do pool de recomendações) |
| `internal` | Marca a página como somente interna do Adobe. Impede a sinalização de links internos. | `yes` |
| `short-description` | Descrição condensada para páginas de aterrissagem do ExL. Usa `description`, se omitido. | Uma frase; máx. ~20 palavras |
| `activity` | Classificação de uso da página. | `understand`, `implement`, `troubleshoot` (minúsculas) |
| `sub-product` | Subcomponente do produto. Trabalhar com equipes de soluções para enumerações válidas. | Minúsculas; por exemplo: `search`, `assets`, `sites` |
| `team` | Atribuição de equipe para análise. | E.g. `TM` |
| `landing-page-name` | Links para página de aterrissagem para navegação estrutural. | E.g. `experience-manager` |
| `landing-page-breadcrumb-title` | Texto de navegação estrutural para link de página inicial. | E.g. `AEM` |
| `auto-video-transcripts` | Ativa as transcrições de vídeo por padrão. | `true` |
| `badgeType` | Medalha para status do conteúdo. | Varia; por exemplo, `informative`, `positive` |
| `badgePremium` | Indicador de selo Premium. | Por especificação do selo da Adobe |
| `badgeLabel` | Texto do rótulo da medalha. | String curta |
| `source-git-url` | URL do repositório do Source. | URL completo do GitHub |
| `cloud` | Substituição de categoria na nuvem no nível do artigo. | Caixa do título; deve corresponder a cloud.yml |

---

## Campos TOC.md

| Campo | Descrição | Notas |
|-------|-------------|-------|
| `user-guide-title` | Nome do guia exibido em navegações estruturais e páginas de aterrissagem do ExL. | Obrigatório para arquivos de índice |
| `breadcrumb-title` | Nome de guia mais curto para navegações estruturais quando o título do guia do usuário é muito longo. | Opcional |
| `user-guide-description` | Resumo do guia da página de aterrissagem do ExL. | Uma frase; máximo de ~20 palavras recomendado |
| `product` | Rastreamento do Analytics para o guia. Somente valor único. | Deve corresponder a product.yml (consulte Valores válidos do produto) |
| `mini-toc-levels` | Número de níveis de cabeçalho mostrados no miniTOC de navegação à direita. | Inteiro 1-6; padrão 2 |
| `role` | Função de público-alvo padrão do guia. | Mesmos valores que o artigo `role`; separados por vírgulas |
| `index` | Se o guia é indexado. | `yes`/`no` |

---

## Campos metadata.md no nível do repositório

| Campo | Notas |
|-------|-------|
| `cloud` | Categoria de nuvem padrão para todos os artigos no repositório |
| `solution` | Solução padrão para todos os artigos |
| `product` | Produto padrão para rastreamento de análise |
| `type` | Tipo de guia padrão |
| `doc-type` | Tipo de documento padrão |
| `mini-toc-levels` | Níveis padrão de miniTOC |
| `git-repo` | URL do repositório GitHub; ativa os botões &quot;Editar esta página&quot; e &quot;Registrar problema&quot; |
| `index` | Configuração de índice padrão |

---

## Valores de Solução Válidos (Diferencia Maiúsculas de Minúsculas)

Valores comuns usados neste repositório:
- `Experience Platform`
- `Real-Time Customer Data Platform`
- `Journey Optimizer`
- `Journey Optimizer B2B Edition`
- `Customer Journey Analytics`
- `Campaign`
- `Campaign v8`
- `Campaign Classic v7`
- `Campaign Standard`
- `Audience Manager`
- `Target`
- `Analytics`
- `Data Collection`
- `Commerce`
- `Marketo Engage`
- `Experience Cloud`
- `Journey Orchestration`

Valores múltiplos: separados por vírgulas, ex.: `Real-Time Customer Data Platform, Campaign`

---

## Valores de Produto Válidos (para o campo `product` — rastreamento de análise)

Consulte o prompt do sistema para obter a lista completa. Valores de chave:
- `adobe experience platform` / `experience platform` / `aem`
- `adobe analytics` / `analytics` / `aa`
- `adobe journey optimizer` / `journey optimizer` / `jo`
- `adobe customer journey analytics` / `customer journey analytics` / `cja`
- `adobe real time customer data platform` / `real time cdp` / `rtcdp`
- `adobe marketo` / `marketo` / `amk`
- `adobe campaign` / `campaign` / `ac`
- `adobe target` / `target` / `at`

---

## Valores de Função Válidos

- `Admin`
- `Architect`
- `Data Architect`
- `Data Engineer`
- `Developer`
- `Leader`
- `User`

---

## Regras de validação de chave

1. Nunca deixe `exl-id` com a mesma UUID em um arquivo copiado — exclua-o e permita que o sistema atribua um novo.
2. `thumbnail` e `kt` em branco/nulos são aceitáveis; esses são campos herdados.
3. `solution` valores devem corresponder exatamente a enum aprovada — diferencia maiúsculas de minúsculas.
4. A validação `description` falha se estiver ausente ou for nula; sempre forneça um valor significativo.
5. Envolva `title` valores entre aspas se eles contiverem dois-pontos, colchetes ou caracteres especiais à esquerda.
6. Vários valores `solution` são separados por vírgulas dentro de um único valor de cadeia de caracteres.
7. `product` é somente valor único (para rastreamento de análise); não use valores separados por vírgula.
8. Para solicitar novos valores de enumeração, registre um tíquete JIRA UGP com o componente &quot;Marcação de conteúdo&quot;.
