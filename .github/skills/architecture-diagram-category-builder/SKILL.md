---
name: architecture-diagram-category-builder
description: 'Criação de guia de uma categoria de nível superior totalmente nova (subseção) em Diagramas de arquitetura e blueprints no repositório de blueprints do Adobe Experience Platform. Use essa habilidade quando um diagrama de arquitetura proposto não se encaixar em nenhuma das categorias existentes (visões gerais de arquitetura, Público-alvo e ativação de perfil, Ativação e marketing B2B, Insights do cliente, jornadas do cliente) e for necessário um novo. Lida com o fluxo de trabalho completo: confirmar uma nova categoria é realmente garantido, aplicando convenções de nomenclatura de pasta/âncora, criando a estrutura de pastas e a página de aterrissagem overview.md, adicionando a subseção TOC.md e atualizando a grade do cartão da página de aterrissagem de diagramas de arquitetura. Para adicionar uma página a uma categoria *existente*, use architecture-diagrama-page-builder.'
source-git-commit: c766cd3153efce4635089d008daf3eb426eb7a24
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%
---

# Criador de categorias do diagrama de arquitetura

Esta habilidade orienta a criação de uma nova categoria de nível superior em `+ Architecture Diagrams and Blueprints{#architecture-diagrams}` em `/help/blueprints/TOC.md`. Uma categoria é uma pasta como `customer-insights/` ou `b2b-activation-marketing/` — um grupo de páginas de diagrama de arquitetura relacionadas com sua própria página de aterrissagem `overview.md` e sua própria subseção do índice.

**Esta é uma operação rara.** Existem cinco categorias hoje. A adição de um sexto só deve ocorrer quando um domínio genuinamente novo do conteúdo de arquitetura não se encaixar em nenhum existente, não como um atalho para evitar a organização de uma página em uma categoria existente.

## Leitura necessária antes de iniciar

- `./references/naming-conventions.md` — a regra de nomenclatura de pasta/âncora/rótulo e por que ela é importante. Leia isso completamente; é a única fonte da verdade sobre como as categorias devem ser nomeadas.
- `./references/category-overview-template.md` — a estrutura exata necessária para a `overview.md` da nova categoria.
- Se você ainda não tiver feito isso, limpe também `../architecture-diagram-page-builder/SKILL.md` — uma vez que a categoria exista, páginas individuais dentro dela serão adicionadas usando essa habilidade, não esta aqui.

## Fase 1: confirmar se uma nova categoria é realmente necessária

Antes de fazer mais nada, liste as cinco categorias existentes e seu escopo para o usuário:

| Categoria | Pasta | Escopo |
| --- | --- | --- |
| Visão geral da arquitetura | `architecture-overviews/` | Arquitetura de nível superior da Experience Cloud/Experience Platform, medidas de proteção, SDKs de implantação |
| Ativação de público-alvo e perfil | `audience-profile-activation/` | Criação e ativação de público-alvo/perfil via Real-Time CDP, Audience Manager |
| Ativação e marketing B2B | `b2b-activation-marketing/` | Ativação baseada em conta, jornadas de grupos de compra, Marketo/Workfront |
| Insights do cliente | `customer-insights/` | Customer Journey Analytics e suas integrações |
| Jornadas do cliente | `customer-journeys/` | Journey Optimizer, Gestão de decisões, Campaign v7/v8 |

Peça ao usuário para confirmar se o conteúdo proposto não se encaixa em nenhum desses itens. Se for um ajuste direto (por exemplo, um novo diagrama B2B, um novo diagrama de personalização), redirecione para `architecture-diagram-page-builder` dessa categoria existente em vez de criar um novo. Prossiga para a Fase 2 somente se o usuário confirmar que uma categoria genuinamente nova é justificada.

## Fase 2: coletar informações de categoria

Use um formulário de pergunta para coletar, em uma rodada:

1. **Rótulo de categoria** — o rótulo do índice completo legível (por exemplo, &quot;Arquitetura do Commerce&quot;, não uma abreviação). Apresentar 2-3 frases sugeridas mais &quot;Outros&quot;.
2. **Descrição em uma frase** — o que esta categoria cobre, para o material de frente e para o cartão de página de aterrissagem do `overview.md`.
3. **Solução(ões) principal(is) da Adobe** — para o campo de destaque `solution`.
4. **Páginas iniciais** — o usuário já tem mais de 1 página pronta para colocar nesta categoria, ou este é apenas o andaime da categoria que as páginas deverão seguir mais tarde?

Derive o nome e a âncora da pasta do rótulo da categoria usando a regra de espaçador em `./references/naming-conventions.md` (minúsculas, soltar `&`, hifenizar, sem abreviação). Mostre ao usuário a pasta/âncora derivada e confirme antes de continuar — este é o detalhe que custa corrigir mais tarde.

## Fase 3: criar a estrutura de pastas

```
help/blueprints/architecture-diagrams/{new-folder}/
help/blueprints/architecture-diagrams/{new-folder}/assets/
help/blueprints/architecture-diagrams/{new-folder}/overview.md
```

Gerar `overview.md` usando `./references/category-overview-template.md`. Se o usuário tiver páginas iniciais prontas, liste-as na tabela agora (usando `architecture-diagram-page-builder` para gerar os próprios arquivos de página — essa habilidade cria apenas o scaffold de categoria e sua página de visão geral, não páginas de diagrama individuais). Se ainda não houver páginas, a tabela pode ficar vazia ou ser omitida até que a primeira página seja adicionada. Observe isso para o usuário, em vez de inventar linhas de espaço reservado.

A pasta `assets/` pode estar vazia no momento da criação; ela existe de modo que a primeira página de diagrama adicionada à categoria tenha um local para colocar suas imagens.

## Fase 4: Adicionar a subseção TOC.md

Insira a nova categoria como uma entrada de nível superior em `+ Architecture Diagrams and Blueprints{#architecture-diagrams}`, posicionada após a última categoria existente, a menos que o usuário especifique o contrário:

```
  + {Category Label}{#{folder-slug}}
    + [Overview](/help/blueprints/architecture-diagrams/{new-folder}/overview.md)
    + [{Page title}](/help/blueprints/architecture-diagrams/{new-folder}/{filename}.md)
```

Regras:

- Recuo de 2 espaços para o cabeçalho da categoria, correspondendo aos outros cinco.
- A âncora `{#{folder-slug}}` deve ser exatamente igual ao nome da pasta (consulte naming-agreements.md).
- `+ [Overview]` é sempre a primeira entrada, com recuo de 4 espaços, antes de qualquer página de conteúdo.
- Preservar a ordem e o conteúdo existentes de todas as outras entradas do TOC.md — apenas inserir, nunca reordenar ou reescrever seções não relacionadas.

## Fase 5: atualizar a página de aterrissagem de diagramas e blueprints de arquitetura

Adicione um novo cartão a `help/blueprints/architecture-diagrams/overview.md`, na mesma grade `<table style="table-layout:fixed; width:100%;">` usada pelos outros cinco cartões. O novo cartão:

- Links para `{new-folder}/overview.md`.
- Usa uma miniatura de diagrama representativa de `{new-folder}/assets/` (ou uma nota de espaço reservado neutra se nenhum diagrama ainda existir — sinalize isso para o usuário em vez de inventar um caminho de imagem).
- Usa exatamente o mesmo bloco de estilo embutido dos cartões existentes (`width:100%; height:160px; object-fit:contain; background-color:#ffffff; border:1px solid #d3d3d3; padding:10px; box-sizing:border-box;` na imagem, `min-height:100px;` na div de texto).

**Recalcular o layout da grade.** Os cinco cartões existentes preenchem uma grade de 3 colunas (duas linhas, uma célula vazia à direita). Adicionar um sexto cartão preenche exatamente essa célula vazia — nenhuma alteração de layout é necessária. Se esta for a 7ª, 8ª, etc. categoria, adicione uma nova `<tr>` com a(s) nova(s) placa(s) e preencha todas as células vazias restantes nessa linha com `<td style="width:33%; ...;"></td>` elementos em branco para que a linha não seja processada de forma irregular.

## Fase 6: validação

Confirmar e relatar ao usuário:

1. **Consistência de nomenclatura** — o nome da pasta, a âncora do índice e a descrição de rótulo da categoria são idênticos (por naming-agreements.md).
2. Estrutura **overview.md** — corresponde a `category-overview-template.md` (intro + tabela `Diagram | Description` de duas colunas, nenhuma imagem inserida ou lista aninhada na tabela).
3. **Posicionamento do TOC.md** — nova subseção está em Diagramas de Arquitetura e Blueprints, `+ [Overview]` é o primeiro, o recuo está correto e nenhuma outra entrada foi alterada.
4. **Cartão da página de aterrissagem** — adicionado na posição de grade correta, usa o estilo de cartão padrão e vincula ao novo `overview.md`.
5. **Redirecionamentos** — se esta categoria consolidar ou renomear conteúdo que vivia em outro lugar (raro para uma categoria totalmente nova, mas de verificação), adicione entradas a `redirects.csv` seguindo o formato `source,dest` existente usado para renomeações anteriores de diagramas de arquitetura.

Corrija quaisquer problemas de validação antes de considerar a tarefa como concluída.

## Notas

- Se posteriormente o usuário renomear uma categoria (rótulo, pasta ou âncora), que é uma operação de renomeação, não uma operação de nova categoria — siga a regra naming-agreements.md para o novo nome, atualize cada link interno (TOC.md, ambas as páginas de visão geral, links relativos irmãos, documentos de habilidade) e adicione entradas de redirecionamento. Trate-o da mesma forma que as renomeações de categoria foram tratadas anteriormente neste repositório: `git mv` a pasta e, em seguida, uma pesquisa e substituição em todo o repositório dos formulários de caminho antigos, nunca uma substituição de cadeia de caracteres global cega que pudesse colidir com URLs externas não relacionadas (por exemplo, `experienceleague.adobe.com/docs/experience-platform/...` links de documento de produto).
- Manter esta habilidade e `architecture-diagram-page-builder` em sincronia: se a tabela de mapeamento de subseção em `references/toc-placement.md` de `architecture-diagram-page-builder` ainda não listar a nova categoria, adicione-a lá também.
