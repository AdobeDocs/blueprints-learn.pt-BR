---
source-git-commit: dfa21942ecf2a1db06df6f6cc945f5572811ca93
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 2%

---
# Referência do documento de blueprint — Guia detalhado

## Tipos de documento

| Tipo | Finalidade | Localização / Exemplo |
|------|---------|--------------------|
| **Visão geral/hub** | Apresenta um produto ou área; links para blueprints de cenário | ex.: `overview.md`, `journey-optimizer-overview.md` |
| **Blueprint do cenário** | Caso de uso único: arquitetura, etapas, medidas de proteção | ex.: `real-time-lookup.md`, `journey-optimizer-journeys.md` |
| **SUMÁRIO** | Navegação; não usar como modelo de conteúdo | `help/blueprints/TOC.md` |

&#x200B;---

## Referência de seção completa

### Título e descrição (assunto principal)

- **título**: curto, específico. Use `[!DNL Product Name]` para nomes de produtos (por exemplo, `[!DNL Journey Optimizer]`).
- **descrição**: uma frase. Descreva o que o blueprint mostra e o resultado (por exemplo, &quot;Acesso do perfil do cliente em tempo real na borda para personalização da Web e móvel&quot;).

### Seções do corpo

| Seção | Quando incluir | Orientação de conteúdo |
|---------|-----------------|-------------------|
| **Aplicativos** | Sempre para blueprints de cenário | Lista com marcadores dos produtos/soluções da Adobe envolvidos (por exemplo, Plataforma de dados do cliente em tempo real, Coleção de dados). |
| **Casos de uso** | Sempre | Lista com marcadores de casos de uso comercial/técnico compatíveis com este blueprint. |
| **Pré-requisitos** | Quando a configuração é obrigatória | Produtos, subdomínios, SDKs, configuração que deve estar em vigor. Link para o Experience League para etapas de configuração. |
| **Diagrama de Arquitetura** | Sempre | Diagrama principal único (SVG preferencial). Usar estilo consistente: `style="width:90%; border:1px solid #4a4a4a" class="modal-image"`. Forneça texto `alt` significativo. |
| **Medidas de proteção** | Sempre que o produto tiver medidas de proteção | Link para páginas oficiais de proteção do Experience League. Adicione limites específicos do blueprint (por exemplo, TTL, limites de taxa) como marcadores. |
| **Padrões de implementação** | Quando existem várias abordagens | Nomeie cada padrão (por exemplo, &quot;Padrão 1: Associação de público-alvo com base no Web SDK&quot;); use marcadores para quando usar e compensações. |
| **Etapas de implementação** | Para blueprints de cenário com um caminho definido | Lista numerada. Cada etapa: ação + link para o Experience League onde o procedimento está. Não copie procedimentos completos. |
| **Considerações de implementação** | Quando houver avisos importantes | Subseções (por exemplo, Considerações de identidade, Personalização baseada em atributos). Marcadores ou parágrafos curtos; vincule para fora quanto à profundidade. |
| **Documentação relacionada** | Sempre | Links agrupados para o Experience League (e, opcionalmente, developer.adobe.com). Consulte &quot;Grupos de links da Experience League&quot; abaixo. |

### Páginas Visão geral/hub

- Comece com 1-2 parágrafos sobre o produto/área e o que os blueprints abordam.
- **Casos de uso**: pode usar `>[!BEGINTABS]` / `>[!TAB ...]` / `>[!ENDTABS]` para várias categorias.
- **Arquitetura**: um diagrama principal.
- **Cenários de blueprint** ou **Padrões de integração**: tabela com nome de cenário, descrição curta e link para o blueprint do cenário.
- **Pré-requisitos**, **Medidas de Proteção**, **Documentação relacionada**: os mesmos mencionados acima; mantenha-se conciso.

&#x200B;---

## Adobe Experience League — Direções do agente

### Quando fazer referência ao Experience League

- **Documentação do produto**: como um produto funciona, fluxos da interface do usuário, conceitos.
- **APIs**: pontos de extremidade, parâmetros, exemplos (Experience Platform, Edge, etc.).
- **Medidas de proteção**: páginas de medidas de proteção oficiais para o produto ou serviço.
- **Tutoriais**: guias passo a passo (por exemplo, criar esquemas, ativar destinos).
- **Configuração**: sequências de dados, destinos, políticas de mesclagem, identidades, etc.

Não cole procedimentos longos do Experience League no blueprint. Resumir e vincular.

### Padrões de URL

| Tipo de conteúdo | URL base | Exemplo de caminho |
|--------------|----------|--------------|
| documentos do Experience Platform | `https://experienceleague.adobe.com/docs/experience-platform/` | `.../profile/home.html`, `.../destinations/catalog/...` |
| Experience League (EN) | `https://experienceleague.adobe.com/en/docs/` | Mesma estrutura acima com `/en/`. |
| Journey Optimizer   | `https://experienceleague.adobe.com/docs/journey-optimizer/` | `.../using/get-started/guardrails.html` |
| SDK da Web | `https://experienceleague.adobe.com/docs/experience-platform/web-sdk/` | `.../home.html`, `.../commands/command-responses.html` |
| API do servidor do Edge Network | `https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/` | `.../overview.html`, `.../guardrails.html` |
| SDK móvel | `https://developer.adobe.com/client-sdks/` | `.../home/`, `.../edge/adobe-journey-optimizer-decisioning/` |
| Tags | `https://experienceleague.adobe.com/docs/experience-platform/tags/` | `.../home.html` |
| Tutoriais da Platform | `https://experienceleague.adobe.com/docs/platform-learn/tutorials/` | `.../profiles/create-merge-policies.html` |

Use o caminho canônico que corresponde ao site atual do Experience League (prefira `/en/docs/` quando o caminho em inglês for conhecido).

### Formatação de link no Markdown

- **Texto do link descritivo**: `[Create schemas](https://experienceleague.adobe.com/...)` não &quot;clique aqui&quot;.
- **Nomes de produtos no texto**: use `[!DNL Product Name]` por estilo do Adobe (por exemplo, `[!DNL Real-time Customer Profile]`).
- **Links externos**: adicionar `{target="_blank"}` somente quando o modelo ou pipeline exigir (verificar blueprints existentes no repositório).

### Documentação relacionada — grupos sugeridos

Use estes grupos quando eles se aplicarem:

1. **Configurações de destino** (para blueprints de ativação/personalização de borda)
2. **Documentação do SDK** (Web SDK, Mobile SDK, API do Edge Network Server, Tags)
3. **Perfil e segmentação** (Perfil do cliente em tempo real, políticas de mesclagem, segmentação)
4. **Tutoriais** (guias passo a passo de aprendizagem da plataforma ou específicos do produto)
5. **Documentação do produto** (página inicial do documento principal do produto ou subseções principais)
6. **Medidas de proteção** (se ainda não estiver na seção Medidas de proteção)

Exemplo:

```markdown
## Related documentation

### Destination configurations
* [Custom Personalization Connection](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/custom-personalization)
* [Activate audiences to edge personalization destinations](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations)

### SDK documentation
* [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html)
* [Edge Network Server API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html)

### Profile and segmentation
* [Real-time Customer Profile](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html)
* [Profile Guardrails](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
```

&#x200B;---

## Acordo de recompra e índice

- **Caminho do conteúdo do blueprint**: `help/blueprints/` (com subpastas por área, por exemplo, `audience-activation/`, `customer-journeys/journey-optimizer/`).
- **Assets**: colocalize com o blueprint (por exemplo, `assets/`, `images/`) ou em uma pasta compartilhada (por exemplo, `experience-platform/assets/`).
- **TOC**: editar `help/blueprints/TOC.md` ao adicionar, renomear ou mover páginas de blueprint. Preservar o frontmatter (`user-guide-title`, `breadcrumb-title`, `user-guide-description`, `product`, `mini-toc-levels`, `role`) e a hierarquia `+`.

&#x200B;---

## Exemplo de referências neste repositório

- **Blueprint do cenário (formulário longo)**: `help/blueprints/audience-activation/real-time-lookup.md`
- **Visão geral/hub com guias e tabelas**: `help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-overview.md`
- **Foco nas grades de proteção**: `help/blueprints/experience-platform/guardrails.md`
- **Navegação**: `help/blueprints/TOC.md`, `help/blueprints/overview.md`

Use-os como padrões para a ordem da seção, o assunto principal, a inserção de diagramas e o uso de links do Experience League.
