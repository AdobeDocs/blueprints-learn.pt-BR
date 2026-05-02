---
source-git-commit: 7511cc0e5c099d5d3ee1275a374cd9ffdc972335
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 2%

---
# Status da migração — blueprints para padrões de caso de uso

Este documento captura o estado do esforço de reorganização do blueprint para que ele possa ser retomado corretamente entre as sessões.

**Última atualização:** 2026-04-29

## Onde estamos agora

**Pausa no momento em:** `b2b/overview.md` (blueprint da seção B2B #1 de 10) — aguardando decisão sobre deixar como está, adicionar uma referência cruzada à nova seção Padrões de ativação e marketing B2B ou atualizar a tabela para listar todos os blueprints + adicionar referência cruzada.

**Para retomar:** responda com **A** (deixar como está, recomendado), **B** (adicionar referência cruzada) ou **C** (atualizar tabela + adicionar referência cruzada). Em seguida, continue com o blueprint #2 (`b2b/b2bactivation.md`).

## Método de trabalho

O padrão de trabalho atual, acordado nesta sessão, é:

1. **Manter blueprints ativos** — sem reprovação. Cada blueprint permanece no local como uma página com foco em arquitetura.
2. **Adicionar DICA de vínculo cruzado** a cada blueprint com um padrão de caso de uso relacionado/sobreposto, imediatamente após o H1:

   ```
   >[!TIP]
   >This blueprint is also available as a [use case pattern](<absolute path>) under <Category>.
   ```

3. **Migrar diagramas** — se um blueprint tiver um diagrama de arquitetura que não esteja relacionado ao padrão relacionado, adicione uma seção `## Architecture` ao padrão que faz referência ao mesmo SVG via caminho absoluto. O ativo permanece no local original (sem cópias de arquivo).
4. **Aparar etapas de implementação** do blueprint onde abordadas no padrão. As seções a serem removidas normalmente incluem: `## Implementation steps`, `## Implementation patterns`, `## Implementation considerations`, às vezes `## Prerequisites`. Use o julgamento por blueprint.
5. **Analisar um por um** — proponha alterações por blueprint, obtenha aprovação do usuário e aplique.

### Regras universais

- O texto da DICA entre links é consistente: `>This blueprint is also available as a [use case pattern](...) under <Category>.`
- Novos arquivos (padrões de caso de uso criados durante a migração) **não incluem`exl-id`** — a publicação da Adobe atribui esses arquivos.
- As referências de imagem em arquivos recém-criados usam caminhos absolutos (`/help/blueprints/...`), não relativos.
- Os valores `exl-id` existentes nas páginas existentes são preservados.
- Os redirecionamentos em `redirects.csv` seguem o formato `source,dest` com `/en/docs/...` caminhos (sem `.html`).

## Fases A-E (trabalho estrutural inicial) — CONCLUÍDAS

| Fase | Resultado |
| --- | --- |
| A | Criada categoria de padrão de caso de uso `B2B Activation & Marketing`. Realocados 3 padrões existentes (`b2b-audience-activation` → `b2b/account-audience-activation`, `buying-group-based-marketing` → `b2b/buying-group-marketing`, `b2b-analytics` → `b2b/account-analytics`). 3 redirecionamentos adicionados. |
| B | Copiados 4 blueprints B2B para `use-case-patterns/b2b/` (`marketo-data-journeys`, `paid-media-orchestration`, `campaign-intake-and-creation`, `campaign-review-and-approval`). |
| C | Copiados 4 blueprints não B2B (`real-time-profile-lookup`, `data-science-profile-enrichment`, `edge-profile-access`, `campaign-v8-orchestration`). |
| D | Dois blueprints divididos (`audience-sharing-with-target`, `third-party-messaging`). |
| E | Adição da DICA de link cruzado a 9 blueprints classificados duplicados. |

Total de Padrões de Caso de Uso após A-E: **26 padrões** em 6 categorias.

## Apresentação seção a seção (em andamento)

A apresentação da seção aplica a abordagem cross-link/migração de diagrama/ajuste implícito a cada blueprint individualmente sob análise do usuário.

### ✅ Público-alvo e ativação de perfil — 8/8 concluídos

| # | Blueprint | Ação executada |
| --- | --- | --- |
| 1 | `audience-manager.md` | DICA entre links + diagrama migrado para padrão (`anonymous-visitor-web-personalization`) + etapas impl do RTCDP removidas |
| 2 | `enterprise-destinations.md` | DICA entre links + diagrama migrado para o padrão (`audience-activation-to-destinations`) |
| 3 | `advertising-activation.md` | Etapas impl removidas (99 → 35 linhas) |
| 4 | `customer-activity.md` | Etapas impl removidas (51 → 40 linhas) |
| 5 | `data-science.md` | Considerações de impl removidas (46 → 40 linhas) |
| 6 | `real-time-lookup.md` | Pré-requisitos + padrões/etapas/considerações de impl removidos (156 → 73 linhas) |
| 7 | `segment-match.md` | **Nenhuma alteração** (o usuário optou por deixar como está) |
| 8 | `rtcdp-target.md` | Padrões impl + considerações removidas (99 → 74 linhas) |

### 🟡 Ativação e marketing B2B — 1/10 em andamento

| # | Blueprint | Status |
| --- | --- | --- |
| 1 | `b2b/overview.md` | **PAUSADO** — aguardando decisão A/B/C (consulte &quot;Onde estamos agora&quot; acima) |
| 2 | `b2b/b2bactivation.md` | Pendente — Duplicação da Fase E; adição de link cruzado; necessidade de revisão para diagrama + corte implícito |
| 3 | `b2b/b2b-account-activation.md` | Pendente — classificado por diagrama; precisa de link cruzado para `b2b/account-audience-activation.md` + consideração de migração de diagrama |
| 4 | `b2b/b2b-buying-group-journeys.md` | Pendente — Duplicação da fase E; adição de link cruzado; necessidade de revisão |
| 5 | `b2b/b2b-journeys-with-marketo.md` | Pendente — cópia da Fase B; o padrão é uma cópia; precisa de acabamento em etapas simples |
| 6 | `b2b/ajo-b2b-paid-media-controller.md` | Pendente — cópia da fase B; precisa de acabamento em etapas simples |
| 7 | `b2b/marketo-engage-and-workfront-integration-blueprint/overview.md` | Pendente — Página de aterrissagem de seção |
| 8 | `b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md` | Pendente — cópia da fase B; precisa de acabamento em etapas simples |
| 9 | `b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md` | Pendente — cópia da fase B; precisa de acabamento em etapas simples |
| 10 | `b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md` | Pendente — Página somente links (auditoria sinalizada como Navegação) |

### ⚪ Customer Journey Analytics — 0/5 ainda não iniciado

Arquivos: `overview.md`, `b2b-cja.md` (Fase E Duplicada, link cruzado adicionado), `cja-rtcdp.md` (Grupo 2 — recomenda-se o link cruzado para `customer-analytics-insight-generation`), `cja-ajo.md` (Grupo 2 — mesmo), `analysis.md` (Grupo 3, possivelmente realocar para experience-platform/).

### ⚪ Jornadas do cliente — 0/14 ainda não iniciado

Arquivos: `overview.md`; `journey-optimizer/` (4 arquivos: visão geral, jornada [Fase E], campanhas [Fase E], mensagens de terceiros [Fase D]); `decision-management/` (3 arquivos: visão geral, borda [Fase E], hub [Fase E]); `campaign-v8/` (3 arquivos: visão geral [Fase C], rtcdp-and-v8, ajo-and-v8); `campaign-v7/` (3 arquivos obsoletos).

### ⚪ Experience Platform — 0/6 ainda não iniciado

Arquivos: `experience-cloud.md`, `platform-applications.md`, `platform-data-flow.md`, `guardrails.md`, `deployment/websdk.md`, `deployment/appsdk.md`. Todos pontuados como somente Diagrama com 0 sinais de padrão na auditoria. **Provavelmente todos &quot;sem alteração&quot;** — são arquiteturas fundamentais com as quais nenhum padrão de caso de uso se sobrepõe.

## Arquivos de referência

| Arquivo | Finalidade |
| --- | --- |
| [blueprint-audit.md](blueprint-audit.md) | Tabela de auditoria por blueprint (43 linhas) com recomendações |
| [rubric.md](rubric.md) | Rubrica de pontuação usada para classificar blueprints |
| [migration-redirects.csv](migration-redirects.csv) | Redirecionamentos por etapas a partir da migração |
| [redirects.csv](../redirects.csv) | Arquivo de redirecionamentos canônicos (3 linhas adicionadas na Fase A) |

## Perguntas abertas ainda não resolvidas (da auditoria)

1. **Borda do Gerenciamento de Decisão + hub** — ambos têm um vínculo cruzado com `offer-decisioning`. Considerar a consolidação em um diagrama único de opções de implantação?
2. **`journey-optimizer-journeys.md`** — sinalizado como duplicado incerto de `event-triggered-messaging`; verifique o escopo antes de cortar.
3. **`customer-journey-analytics/analysis.md`** — o conteúdo é sobre o Serviço de Consulta do Experience Platform, não sobre o CJA; considere realocar para `experience-platform/`.
4. **Campaign v7 (3 arquivos obsoletos)** — migrar, sair ou remover do sumário?
5. **`customer-success-stories.md`** — página somente links; confirme a classificação da Navegação.
6. A **âncora do índice** para a nova seção B2B é `{#b2b-patterns}` — confirme antes de qualquer criação de redirecionamento de produção.

## Como retomar

Abra uma nova sessão do Claude Code neste repositório e diga:

> Vamos retomar a migração do blueprint. Leia `_evaluation/migration-status.md` para continuar de onde paramos.

A próxima etapa concreta: responder à decisão `b2b/overview.md` (A/B/C). Em seguida, continue com o blueprint #2 (`b2b/b2bactivation.md`) e prossiga pela seção B2B, depois pelo Customer Journey Analytics, Customer Jornada e Experience Platform.
