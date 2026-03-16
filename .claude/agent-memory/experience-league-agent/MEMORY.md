---
source-git-commit: a632042b3a7434dd88f52804e15e30fa06057e3b
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---
# Memória do agente Experience League

## Arquivos de Referência Chave neste Repositório
- `/Users/nick/Library/CloudStorage/OneDrive-Adobe/Documents/GitHub/blueprints-learn.en/metadata.md` — padrões de metadados no nível do repositório
- `/Users/nick/Library/CloudStorage/OneDrive-Adobe/Documents/GitHub/blueprints-learn.en/help/blueprints/TOC.md` — metadados de nível de guia
- `/Users/nick/Library/CloudStorage/OneDrive-Adobe/Documents/GitHub/blueprints-learn.en/.cursor/skills/blueprint-document-reference/reference.md` — padrões de criação de blueprint

## Regras de metadados (consulte metadata-fields.md para referência completa)
- Conteúdo principal do artigo NECESSÁRIO: `title`, `description`, `exl-id`
- O assunto principal do artigo É ALTAMENTE RECOMENDADO: `solution`
- `exl-id` deve ser um UUID válido; excluir/deixar em branco ao copiar arquivos (autoatribuído pelo sistema)
- `description` deve começar com &quot;Saiba como...&quot; ou &quot;Saiba mais sobre...&quot; de acordo com as diretrizes da Adobe
- `title` máx. ~60 caracteres para SEO; use `[!DNL ProductName]` para nomes de produtos no título
- `solution` valores diferenciam maiúsculas de minúsculas e devem corresponder a enum aprovada (consulte metadata-fields.md)
- `thumbnail: null` ou `thumbnail:` (em branco) são usados; vazio é aceitável
- `kt:` é um campo herdado (número JIRA do artigo da base de dados de conhecimento); ainda visto neste repositório; branco é aceitável
- Arquivos do sumário usam: `user-guide-title`, `breadcrumb-title`, `user-guide-description`, `product`, `mini-toc-levels`, `role`
- O nível de repositório `metadata.md` usa: `cloud`, `solution`, `product`, `type`, `doc-type`, `mini-toc-levels`, `git-repo`, `index`

## Padrões comuns neste repositório (blueprints-learn.en)
- A maioria dos arquivos de blueprint tem: `title`, `description`, `solution`, `exl-id`
- Alguns arquivos mais antigos também incluem: `kt`, `thumbnail`
- Alguns arquivos usam `version` (blueprints do Campaign v8)
- Páginas de visão geral usam `doc-type: overview-page`
- `solution` frequentemente contém vários valores separados por vírgula: ex.: `Real-Time Customer Data Platform, Campaign`
- Os arquivos SEM `solution` ainda passarão na validação se `exl-id` estiver presente

## Extensões do Adobe Markdown usadas neste repositório
- `>[!NOTE]`, `>[!TIP]`, `>[!IMPORTANT]`, `>[!WARNING]`, `>[!CAUTION]`
- `>[!BEGINTABS]` / `>[!TAB Name]` / `>[!ENDTABS]` para conteúdo com guias
- `[!DNL ProductName]` — Não traduzir marcas para nomes de produtos
- `[!UICONTROL Label]` — Referências de controle da interface do usuário
- `{zoomable="yes"}` — atributo de zoom de imagem
- `{width="1000"}` — atributo de largura da imagem
- `{target="_blank"}` — destino do link externo

## Referências detalhadas
- Referência de campo de metadados completa: `metadata-fields.md`
- Guia de criação rastreado: https://experienceleague.adobe.com/en/docs/authoring-guide-exl/using/home (fevereiro de 2026)
