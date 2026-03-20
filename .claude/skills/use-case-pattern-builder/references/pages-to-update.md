---
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---
# Páginas para atualizar ao adicionar um padrão de caso de uso

Quando um novo padrão de caso de uso é criado, as seguintes páginas devem ser atualizadas para garantir que o padrão seja detectável e vinculado corretamente.

## Atualizações necessárias

### 1. TOC.md
- **Arquivo:** `/help/blueprints/TOC.md`
- **Ação:** Adicione uma nova entrada na seção de categoria correta
- **Formato:** `    + [{{Pattern Title}}](/help/blueprints/use-case-patterns/{{category}}/{{filename}}.md)`
- **Localização por categoria:**
   - Criação e ativação de público-alvo: após a linha ~47 (após entradas existentes nessa seção)
   - Personalization: após a linha ~52
   - Gerenciamento e orquestração de campanhas: após a linha ~58
   - Análise: após a linha ~61
   - Experiência de conversa: após a linha ~63

#### Mapeamento de categoria para índice

| Lesma da categoria | Cabeçalho da seção do índice | Âncora |
| --- | --- | --- |
| `audience-building-activation` | `+ Audience Building & Activation` | `{#audience-building-activation}` |
| `personalization` | `+ Personalization` | `{#personalization-patterns}` |
| `campaign-management-orchestration` | `+ Campaign Management & Orchestration` | `{#campaign-orchestration-patterns}` |
| `analysis` | `+ Analysis` | `{#analysis-patterns}` |
| `conversational-experience` | `+ Conversational Experience` | `{#conversational-experience-patterns}` |

#### Regras de recuo

- Os cabeçalhos de categoria usam dois espaços + `+` (por exemplo, `  + Personalization{#personalization-patterns}`)
- As entradas padrão usam quatro espaços + `+` (por exemplo, `    + [Pattern Title](path)`)

### &#x200B;2. Visão geral dos padrões de caso de uso
- **Arquivo:** `/help/blueprints/use-case-patterns/overview.md`
- **Ação:** Adicione uma nova linha à tabela de categorias correta
- **Formato:** `| [{{Pattern Title}}]({{category}}/{{filename}}.md) | {{Primary capability description}} | [!DNL {{Solution1}}], [!DNL {{Solution2}}] |`
- **Categorias na visão geral:**
   - Criação e ativação de público (linha ~18)
   - Personalization (linha ~29)
   - Gerenciamento e orquestração de campanhas (linha ~40)
   - Análise (linha ~52)
   - Experiência de conversa (linha ~61)

#### Exemplo de formato de linha

```
| [Event-Triggered Messaging](campaign-management-orchestration/event-triggered-messaging.md) | Listen for a real-time behavioral or system event, then deliver a contextual message to the triggering profile | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
```

## Lista de verificação de validação

- [ ] Arquivo de marcação de padrão criado no diretório de categoria correto
- [ ] O Frontmatter inclui título, descrição, solução e exl-id
- [ ] entrada TOC.md adicionada na categoria correta
- [ ] Linha da tabela Overview.md adicionada na categoria correta
- [ ] Todos os links de objetivos de negócios apontam para arquivos existentes
- [ ] O arquivo usa a convenção de nomenclatura kebab-case
- [ ] Todos os links do Experience League são URLs válidas
- [ Os nomes de produtos do Adobe ] usam a sintaxe `[!DNL ...]`
- [ A cadeia de funções ] usa o formato de separador ` > `
- [ O arquivo de padrão ] inclui todas as seções necessárias (consulte pattern-template.md)
