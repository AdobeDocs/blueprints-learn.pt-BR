---
source-git-commit: 2ed15399073fce5ebd1c2ba07b1cf70ec706452c
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 2%
---
# Blueprints de status de migração â€ para padrões de caso de uso

Este documento captura o estado do esforço de reorganização do blueprint para que ele possa ser retomado corretamente entre as sessões.

**Última atualização:** 24/09/2026

## Onde estamos agora

A seção B2B não está mais pausada. Seu escopo de arquitetura publicado agora está limitado às páginas de público-alvo/perfil e ativação de conta, com páginas removidas redirecionadas para a visão geral da categoria.

**Status atual:** A limpeza da arquitetura B2B foi concluída. As páginas de ativação de conta/público-alvo permanecem na categoria de diagramas de arquitetura; as outras páginas de arquitetura B2B foram removidas e redirecionadas para a visão geral da categoria.

## Método de trabalho

> A abordagem de trabalho abaixo é histórica; a seção B2B foi descartada desde então, como registrado acima.

O padrão de trabalho atual, acordado nesta sessão, é:

1. **Manter blueprints ativos** â€&quot; sem reprovação. Cada blueprint permanece no local como uma página com foco em arquitetura.
2. **Adicionar DICA de vínculo cruzado** a cada blueprint com um padrão de caso de uso relacionado/sobreposto, imediatamente após o H1:

   ```
   >[!TIP]
   >This blueprint is also available as a [use case pattern](<absolute path>) under <Category>.
   ```

3. **Migrar diagramas** â€&quot; se um blueprint tiver um diagrama de arquitetura ausente no padrão relacionado, adicione uma seção `## Architecture` ao padrão que faz referência ao mesmo SVG por meio de um caminho absoluto. O ativo permanece no local original (sem cópias de arquivo).
4. **Aparar etapas de implementação** do blueprint onde abordadas no padrão. As seções a serem removidas normalmente incluem: `## Implementation steps`, `## Implementation patterns`, `## Implementation considerations`, às vezes `## Prerequisites`. Use o julgamento por blueprint.
5. **Analise um por um** â€&quot; para propor alterações por blueprint, obter aprovação do usuário e, em seguida, aplicar.

### Regras universais

- O texto da DICA entre links é consistente: `>This blueprint is also available as a [use case pattern](...) under <Category>.`
- Novos arquivos (padrões de caso de uso criados durante a migração) **não incluem`exl-id`** â€&quot; que a publicação da Adobe atribui a eles.
- As referências de imagem em arquivos recém-criados usam caminhos absolutos (`/help/blueprints/...`), não relativos.
- Os valores `exl-id` existentes nas páginas existentes são preservados.
- Os redirecionamentos em `redirects.csv` seguem o formato `source,dest` com `/en/docs/...` caminhos (sem `.html`).

## Fases Aâ€&quot;E (trabalho estrutural inicial) â€&quot; COMPLETO

| Fase | Resultado |
| --- | --- |
| A | Criada categoria de padrão de caso de uso `B2B Activation & Marketing`. Realocados 3 padrões existentes (`b2b-audience-activation` â†’ `b2b/account-audience-activation`, `buying-group-based-marketing` â†’ `b2b/buying-group-marketing`, `b2b-analytics` â†’ `b2b/account-analytics`). 3 redirecionamentos adicionados. |
| B | Copiados 4 blueprints B2B para `use-case-patterns/b2b/` (`marketo-data-journeys`, `paid-media-orchestration`, `campaign-intake-and-creation`, `campaign-review-and-approval`). |
| C | Copiados 4 blueprints não B2B (`real-time-profile-lookup`, `data-science-profile-enrichment`, `edge-profile-access`, `campaign-v8-orchestration`). |
| D | Dois blueprints divididos (`audience-sharing-with-target`, `third-party-messaging`). |
| E | Adição da DICA de link cruzado a 9 blueprints classificados duplicados. |

Total de padrões de caso de uso após Aâ€&quot;E: **26 padrões** em 6 categorias.

## Apresentação seção a seção (em andamento)

A apresentação da seção aplica a abordagem cross-link/migração de diagrama/ajuste implícito a cada blueprint individualmente sob análise do usuário.

### âoe... Audience &amp; Profile Ativation â€&quot; 8/8 completo

| # | Blueprint | Ação executada |
| --- | --- | --- |
| 1 | `audience-manager.md` | DICA entre links + diagrama migrado para padrão (`anonymous-visitor-web-personalization`) + etapas impl do RTCDP removidas |
| 2 | `enterprise-destinations.md` | DICA entre links + diagrama migrado para o padrão (`audience-activation-to-destinations`) |
| 3 | `advertising-activation.md` | Etapas impl removidas (99 â†’ 35 linhas) |
| 4 | `customer-activity.md` | Etapas impl removidas (51 â†’ 40 linhas) |
| 5 | `data-science.md` | Considerações de impl removidas (46 â†’ 40 linhas) |
| 6 | `real-time-lookup.md` | Pré-requisitos + padrões/etapas/considerações de implementação removidos (156 â†’ 73 linhas) |
| 7 | `segment-match.md` | **Nenhuma alteração** (o usuário optou por deixar como está) |
| 8 | `rtcdp-target.md` | Padrões impl + considerações removidas (99 â†’ 74 linhas) |

### ðπ Ÿ Ativação e marketing B2B â€&quot; 1/10 em andamento

| # | Blueprint | Status |
| --- | --- | --- |
| 1 | `b2b/overview.md` | Concluído - Visão geral da categoria B2B atualizada |
| 2 | `b2b/b2bactivation.md` | Descontinuado - substituído pela página de perfil/público-alvo dos diagramas de arquitetura |
| 3 | `b2b/b2b-account-activation.md` | Retido - migrado para a categoria B2B de diagramas de arquitetura |
| 4 | `b2b/b2b-buying-group-journeys.md` | Aposentado |
| 5 | `b2b/b2b-journeys-with-marketo.md` | Aposentado |
| 6 | `b2b/ajo-b2b-paid-media-controller.md` | Aposentado |
| 7 | `b2b/marketo-engage-and-workfront-integration-blueprint/overview.md` | Aposentado |
| 8 | `b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md` | Aposentado |
| 9 | `b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md` | Aposentado |
| 10 | `b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md` | Aposentado |

### âšª Customer Journey Analytics â€&quot; 0/5 ainda não iniciado

Arquivos: `overview.md`, `b2b-cja.md` (Fase E Duplicada, link cruzado adicionado), `cja-rtcdp.md` (Grupo 2 â€&quot; recomenda o link cruzado para `customer-analytics-insight-generation`), `cja-ajo.md` (Grupo 2 â€&quot; mesmo), `analysis.md` (Grupo 3, possivelmente realocar para experience-platform/).

### âšª Cliente Jornada a limpeza de aposentadoria por €completo; migração de página retida pendente

Arquivos: `overview.md`; `journey-optimizer/` (4 arquivos: visão geral, jornada [Fase E], campanhas [Fase E], mensagens de terceiros [Fase D]); `campaign-v8/` (3 arquivos: visão geral [Fase C], rtcdp-and-v8, ajo-and-v8). `decision-management/` e `campaign-v7/` estão totalmente desativados; suas entradas históricas permanecem na auditoria e suas URLs redirecionam para as páginas de visão geral aprovadas.

### âšª Experience Platform â€&quot; 0/6 ainda não iniciado

Arquivos: `experience-cloud.md`, `platform-applications.md`, `platform-data-flow.md`, `guardrails.md`, `deployment/websdk.md`, `deployment/appsdk.md`. Todos pontuados como somente Diagrama com 0 sinais de padrão na auditoria. **Provavelmente, todos &quot;sem alteração&quot;** â€&quot; são arquiteturas fundamentais com as quais nenhum padrão de caso de uso se sobrepõe.

As decisões de aposentadoria do Gerenciamento de decisão e do Campaign v7 estão concluídas. Suas perguntas abertas relacionadas
são somente históricos e não devem bloquear o trabalho de migração restante.

## Arquivos de referência

| Arquivo | Finalidade |
| --- | --- |
| [blueprint-audit.md](blueprint-audit.md) | Tabela de auditoria por blueprint (43 linhas) com recomendações |
| [rubric.md](rubric.md) | Rubrica de pontuação usada para classificar blueprints |
| [migration-redirects.csv](migration-redirects.csv) | Redirecionamentos por etapas a partir da migração |
| [redirects.csv](../redirects.csv) | Arquivo de redirecionamentos canônicos (3 linhas adicionadas na Fase A) |

## Perguntas abertas ainda não resolvidas (da auditoria)

2. **`journey-optimizer-journeys.md`** â€&quot; sinalizado como duplicata incerta de `event-triggered-messaging`; verifique o escopo antes de cortar.
3. O conteúdo **`customer-journey-analytics/analysis.md`**€ refere-se ao Serviço de Consulta do Experience Platform, não ao CJA; considere realocar para `experience-platform/`.
4. Página somente links de **`customer-success-stories.md`** â€; confirme a classificação da Navegação.
5. Pergunta de âncora de índice histórica substituída pela disposição concluída da arquitetura B2B.

## Como retomar

Abra uma nova sessão do Claude Code neste repositório e diga:

> Vamos retomar a migração do blueprint. Leia `_evaluation/migration-status.md` para continuar de onde paramos.

A limpeza da arquitetura B2B foi concluída. Prossiga com a próxima categoria de arquitetura planejada após a validação.
