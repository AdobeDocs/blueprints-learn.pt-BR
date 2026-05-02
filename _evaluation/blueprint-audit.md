---
source-git-commit: 7511cc0e5c099d5d3ee1275a374cd9ffdc972335
workflow-type: tm+mt
source-wordcount: '3505'
ht-degree: 6%

---
# Auditoria e recomendações do blueprint

Esta auditoria aplica a [rubrica de avaliação](rubric.md) a todos os documentos sob a
seção &quot;Diagramas e blueprints de arquitetura&quot; do [TOC.md](../help/blueprints/TOC.md) (linhas 76-133) e
A recomenda se cada blueprint deve se tornar um caso de uso **Padrão**, uma arquitetura
**Diagrama**, ambos (**Split**), ou ser sinalizado como **Duplicado** de um padrão existente.

Esta é apenas uma auditoria — nenhum conteúdo foi movido. O backlog de migração (Ações A-D em lote)
será elaborado como um plano de acompanhamento distinto, uma vez analisadas as recomendações.

## Resumo

**Total de documentos auditados:** 43

| Recomendação | Contagem | Ação |
| --- | --- | --- |
| Padrão | 8 | Criar um novo padrão de caso de uso; aparar original em um diagrama. |
| Duplicar | 9 | O padrão existente abrange o escopo; simplifique o blueprint em um diagrama e o link cruzado. |
| Divisão | 2 | Extrair conteúdo do padrão; reduzir original para um diagrama; criar um link cruzado de ambos. |
| Diagrama | 16 | Manter como diagrama de arquitetura; aparar narrativa se necessário. |
| Navegação | 8 | Página de aterrissagem de seção (overview.md ou links-only); refaça a visita após as migrações aterrarem. |

### Calibração do grupo de controlo

Todos os 6 `experience-platform/` arquivos pontuaram Pattern=0, Diagram=3 → unanimemente **Diagram**.
A rubrica é calibrada; os resultados das outras sub-áreas podem ser confiáveis como pontuados.

### Nova categoria de padrão de caso de uso: Ativação B2B e marketing

Uma nova categoria `use-case-patterns/b2b/` (exibir rótulo **Ativação e marketing B2B**, âncora do índice)
proposto `{#b2b-patterns}`) abrigará todos os padrões específicos B2B. O rótulo reflete o atual
Subseção &quot;Ativação e marketing B2B&quot; na área de diagramas de arquitetura do [TOC.md](../help/blueprints/TOC.md),
simetria visual entre as duas seções.

Quando totalmente preenchida, a categoria conterá **7 padrões**:

| Origem | Ação | Caminho de destino |
| --- | --- | --- |
| `use-case-patterns/audience-building-activation/b2b-audience-activation.md` | **Realocar** padrão existente | `use-case-patterns/b2b/account-audience-activation.md` |
| `use-case-patterns/campaign-management-orchestration/buying-group-based-marketing.md` | **Realocar** padrão existente | `use-case-patterns/b2b/buying-group-marketing.md` |
| `use-case-patterns/analysis/b2b-analytics.md` | **Realocar** padrão existente | `use-case-patterns/b2b/account-analytics.md` |
| `b2b/b2b-journeys-with-marketo.md` | **Novo autor** (linha de Padrão de auditoria) | `use-case-patterns/b2b/marketo-data-journeys.md` |
| `b2b/ajo-b2b-paid-media-controller.md` | **Novo autor** (linha de Padrão de auditoria) | `use-case-patterns/b2b/paid-media-orchestration.md` |
| `b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md` | **Novo autor** | `use-case-patterns/b2b/campaign-intake-and-creation.md` |
| `b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md` | **Novo autor** | `use-case-patterns/b2b/campaign-review-and-approval.md` |

> **Estado de transição inicial — portão de coordenação do gravador.** A &quot;Ativação e marketing B2B&quot; existente> a subseção na área de diagramas de arquitetura do [TOC.md](../help/blueprints/TOC.md) (linhas 95-106) **permanece intacta> durante a transição**. Cada conversão de blueprint e realocação de padrão existente requer> fazer logoff do gravador proprietário antes que o conteúdo seja migrado. O novo padrão de caso de uso `b2b/`> coexiste com a seção existente do blueprint enquanto as migrações ocorrem página por página, com> entre eles.

Quando todas as realocações e novos padrões caíram:

- A seção [TOC.md](../help/blueprints/TOC.md) `Use Case Patterns` ganhará um `B2B Activation & Marketing{#b2b-patterns}`
subseção (inserção TBD com o gravador).
- [use-case-patterns/overview.md](../help/blueprints/use-case-patterns/overview.md) obterá uma tabela de categoria B2B.
- Os padrões realocados serão removidos de `audience-building-activation`,
  `campaign-management-orchestration` e `analysis` tabelas de visão geral; suas URLs antigas são mantidas
ativo via redirecionamentos em [migration-redirects.csv](migration-redirects.csv).

### Duplicatas identificadas (9)

O escopo do blueprint já está coberto por um padrão de caso de uso existente. A ação de migração é
**simplificar para diagrama de arquitetura + link cruzado**.

| Blueprint | Padrão existente |
| --- | --- |
| `audience-activation/advertising-activation.md` | `use-case-patterns/audience-building-activation/audience-activation-to-destinations.md` |
| `audience-activation/segment-match.md` | `use-case-patterns/audience-building-activation/audience-collaboration-segment-match.md` |
| `b2b/b2bactivation.md` | `use-case-patterns/audience-building-activation/b2b-audience-activation.md` |
| `b2b/b2b-buying-group-journeys.md` | `use-case-patterns/campaign-management-orchestration/buying-group-based-marketing.md` |
| `customer-journey-analytics/b2b-cja.md` | `use-case-patterns/analysis/b2b-analytics.md` |
| `customer-journeys/journey-optimizer/journey-optimizer-journeys.md` | `use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md` |
| `customer-journeys/journey-optimizer/journey-optimizer-campaigns.md` | `use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md` |
| `customer-journeys/decision-management/decision-management-edge.md` | `use-case-patterns/personalization/offer-decisioning.md` |
| `customer-journeys/decision-management/decision-management-hub.md` | `use-case-patterns/personalization/offer-decisioning.md` |

> Observação: `decision-management-edge.md` e `decision-management-hub.md` mapeiam para o mesmo> padrão `offer-decisioning.md` existente. Considere a consolidação de ambos os blueprints em um único> diagrama de opções de implantação ou aumento do padrão existente com implantação edge-vs-hub> variantes. Sinalizador para revisão do gravador.

### Padrões para criação (8 novos + 2 de Divisões = total de 10)

| blueprint do Source | Categoria proposta | Título do padrão proposto |
| --- | --- | --- |
| `audience-activation/customer-activity.md` | audience-building-ativation | Pesquisa de perfil em tempo real para suporte e vendas |
| `audience-activation/data-science.md` | audience-building-ativation | Assimilação do modelo de ciência de dados para enriquecimento de perfil |
| `audience-activation/real-time-lookup.md` | personalização | Acesso ao perfil do Edge para Personalization da Web/móvel |
| `b2b/b2b-journeys-with-marketo.md` | **b2b** (novo) | Jornadas de conta B2B com integração de dados do Marketo |
| `b2b/ajo-b2b-paid-media-controller.md` | **b2b** (novo) | Orquestração de mídia paga B2B por meio da lógica de divisão de caminho em cascata |
| `b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md` | **b2b** (novo) | Entrada de solicitação de campanha e criação automatizada de programa |
| `b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md` | **b2b** (novo) | Fluxo de trabalho de revisão e aprovação de ativos da campanha |
| `customer-journeys/campaign-v8/campaign-v8-overview.md` | campaign-management-orchestration | Orquestração em lote e mensagens transacionais do Campaign v8 |
| `audience-activation/rtcdp-target.md` *(Split)* | personalização | Compartilhamento de público-alvo em tempo real com a Adobe Target |
| `customer-journeys/journey-optimizer/3rd-party-messaging.md` *(Split)* | campaign-management-orchestration | Integração de mensagens de terceiros com o Journey Optimizer |

### Nova categoria de padrão proposta

- **`b2b/`** (exibir rótulo **Ativação e marketing B2B**) — consulte a seção dedicada acima. A variável
Padrões Marketo + Workfront (`intake-and-create`, `review-and-approve-blueprint`) são roteados
aqui em vez de em uma categoria `marketing-resource-management` separada, já que elas representam
Operações de marketing B2B na prática. A nova categoria agrega 7 padrões no total: 3 realocados
de categorias existentes e 4 recém-criados de blueprints.

### Redirecionamentos de migração

Cada alteração de URL introduzida por essa migração adiciona uma linha à variável
[`redirects.csv`](../redirects.csv) na raiz do repositório (formato: `source,dest`). Confirmado
os redirecionamentos são preparados em [migration-redirects.csv](migration-redirects.csv) e mesclados na
arquivo canônico à medida que cada movimentação correspondente realmente acontece.

**Confirmado (3 entradas, preparado):** Relocações de padrão existentes para `b2b/`. Consulte
[migration-redirects.csv](migration-redirects.csv).

**Pendente — adicionado quando um blueprint é *excluído* (não quando reduzido ao diagrama no local):** se um
O blueprint da linha Padrão, Dividida ou Duplicada for removido posteriormente por completo, adicione um redirecionamento do
URL do blueprint para o URL do padrão canônico. Abordagem de migração padrão (simplificar para diagrama)
mantém a URL do blueprint ativa e **não requer** esses redirecionamentos. Listado abaixo para
integridade se qualquer blueprint for totalmente retirado:

```
# Pattern blueprints — if deleted, redirect to the new pattern URL
# (slugs are placeholders; finalize when each pattern is authored)
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/customer-activity → use-case-patterns/audience-building-activation/<new-pattern-slug>
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/data-science → use-case-patterns/audience-building-activation/<new-pattern-slug>
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/real-time-lookup → use-case-patterns/personalization-patterns/<new-pattern-slug>
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/b2b-journeys-with-marketo → use-case-patterns/b2b-patterns/marketo-data-journeys
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/ajo-b2b-paid-media-controller → use-case-patterns/b2b-patterns/paid-media-orchestration
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/marketo-engage-and-workfront-integration-blueprint/intake-and-create → use-case-patterns/b2b-patterns/campaign-intake-and-creation
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint → use-case-patterns/b2b-patterns/campaign-review-and-approval
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/campaign-v8/campaign-v8-overview → use-case-patterns/campaign-orchestration-patterns/<new-pattern-slug>

# Duplicate blueprints — if deleted, redirect to the existing pattern URL
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/advertising-activation → use-case-patterns/audience-building-activation/audience-activation-to-destinations
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/segment-match → use-case-patterns/audience-building-activation/audience-collaboration-segment-match
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/b2bactivation → use-case-patterns/b2b-patterns/account-audience-activation  (after b2b/ relocation)
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/b2b-buying-group-journeys → use-case-patterns/b2b-patterns/buying-group-marketing  (after b2b/ relocation)
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journey-analytics/b2b-cja → use-case-patterns/b2b-patterns/account-analytics  (after b2b/ relocation)
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/journey-optimizer/journey-optimizer-journeys → use-case-patterns/campaign-orchestration-patterns/event-triggered-messaging
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/journey-optimizer/journey-optimizer-campaigns → use-case-patterns/campaign-orchestration-patterns/batch-outbound-message-activation
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/decision-management/decision-management-edge → use-case-patterns/personalization-patterns/offer-decisioning
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/decision-management/decision-management-hub → use-case-patterns/personalization-patterns/offer-decisioning

# Optional one-off — if customer-journey-analytics/analysis.md is relocated to experience-platform/
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journey-analytics/analysis → architecture-diagrams/architecture-overview/analysis
```

Ao converter qualquer uma das linhas acima em linhas de redirecionamento ativas, formatar como separadas por vírgula `source,dest`
com caminhos `/en/docs/...` completos (sem sufixo `.html`), correspondendo ao padrão existente em
[`redirects.csv`](../redirects.csv).

### Política de criação de redirecionamento (regra durável)

Para cada etapa de migração, siga estas regras:

1. **Arquivo movido ou renomeado** → adicione o redirecionamento da URL antiga para a nova URL.
2. **Arquivo excluído** (blueprint substituído; nenhum diagrama retido) → adicione o redirecionamento da URL excluída a
URL de substituição canônica.
3. **Arquivo simplificado no local** (URL inalterado) → sem redirecionamento.
4. **Âncora de índice renomeada** (por exemplo, alteração de cabeçalho de seção) → adicione redirecionamentos para cada página em
essa âncora, já que o URL muda.

### Perguntas abertas para o autor

1. **Borda do Gerenciamento de Decisão vs. hub** — ambos mapeiam para o mesmo existente `offer-decisioning.md`
padrão. Consolidar em um único diagrama com variantes de implantação ou tratar como separados
diagramas que cruzam ambos os links para o mesmo padrão?
2. **Journey Optimizer jornada vs. mensagens disparadas por eventos** — o agente sinalizou esta duplicata
classificação como incerta. Verifique o alinhamento do escopo antes de reduzir o blueprint.
3. **`customer-journey-analytics/analysis.md`** — o conteúdo na verdade é sobre o Experience Platform
Serviço de consulta, não CJA. Considere realocar para a pasta `experience-platform/`. (Um redirecionamento
seria adicionado em caso afirmativo — consulte [migration-redirects.csv](migration-redirects.csv).)
4. **Campaign v7 (desaprovado)** — três arquivos v7 descontinuados foram classificados como Diagrama /
Navegação. Confirme se deseja migrar, deixar como está ou remover do sumário completamente.
5. **`customer-success-stories.md`** — página de referência somente links (não é uma `overview.md`).
Classificado como Navegação. Confirmar ou reclassificar.
6. **Âncora de índice de seção B2B** — proposta `{#b2b-patterns}`. Outros padrões que as subseções usam
   `-patterns` sufixo (`{#personalization-patterns}`, `{#analysis-patterns}`,
   `{#campaign-orchestration-patterns}`). Confirme ou escolha outra âncora antes de criar redirecionamentos.
7. Posicionamento da seção **B2B no sumário** — proposto em `+ Use Case Patterns{#use-case-patterns}`.
Faça pedidos entre irmãos (Audience Building &amp; Ativation, Personalization, Campaign Management
e Orquestração, Análise, Ativação e Marketing B2B, Experiência de conversação) é a principal
chamada do escritor.
8. **Coordenação de gravador proprietário** — cada conversão de blueprint e realocação de padrão existente
precisa de aprovação do gravador antes que o conteúdo seja movido. A tabela de auditoria é o estado de destino, não um
plano de sequenciamento; a sequência ocorre em um plano de migração de acompanhamento após a coordenação.

## Tabela de auditoria

| caminho | título | resumo | tipo_dominante | recomendação | proposed_pattern_category | título_padrão_proposto | título_de_diagrama_proposto | duplicate_of | pattern_score | pontuação_do_diagrama | notas |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| help/blueprints/experience-platform/experience-cloud.md | Diagramas de arquitetura da Adobe Experience Cloud | Arquitetura corporativa que mostra como os aplicativos e serviços da Experience Cloud se integram à base do AEP. | Diagrama | Diagrama |  |  | Visão geral da arquitetura do Experience Cloud |  | 0 | 3 | Substituir 3 (sem objetivo comercial). Três diagramas complementares (marketecture, integração, cenário corporativo). Grupo de controle: conforme esperado. |
| help/blueprints/experience-platform/platform-applications.md | Diagramas da arquitetura de aplicativos e Adobe Experience Platform | Diagramas de arquitetura que mostram como o Experience Platform está relacionado a outros aplicativos da Experience Cloud. | Diagrama | Diagrama |  |  | Arquitetura do AEP e de aplicativos |  | 0 | 3 | Substituir 3. Dois diagramas de visão geral/detalhados; sem orientação de implementação. Links cruzados para integrações - documentos de aprendizado. Grupo de controle: conforme esperado. |
| help/blueprints/experience-platform/platform-data-flow.md | Diagramas da arquitetura de fluxo de dados da Adobe Experience Platform Diagramas | Diagrama da arquitetura de fluxo de dados mostrando os caminhos de assimilação e saída da Experience Platform. | Diagrama | Diagrama |  |  | Arquitetura de fluxo de dados do AEP |  | 0 | 3 | Substituir 3. Diagrama de fluxo de dados único com referência aos documentos de coleção de dados. Artefato puro de arquitetura. Grupo de controle: conforme esperado. |
| help/blueprints/experience-platform/guardrails.md | Experience Platform e medidas de proteção de aplicativos | Restrições do sistema, expectativas de desempenho e medidas de proteção de latência para AEP e aplicativos. | Diagrama | Diagrama |  |  | Proteções e latências do AEP e dos aplicativos |  | 0 | 3 | Substituir 3. Diagrama de latência mais tabelas de referência. Orientado a arquiteto (edge vs hub). Documentação de restrições, não de instruções. Grupo de controle: conforme esperado. |
| help/blueprints/experience-platform/deployment/websdk.md | Diagrama da arquitetura do Experience Platform Web SDK e Edge Network | Arquitetura de implantação do Web SDK e Edge Network mostrando fluxos de coleta de dados. | Diagrama | Diagrama |  |  | Implantação do Web SDK e Edge Network |  | 0 | 3 | Substituir 3. Dois diagramas (fluxo e sequência). Tutoriais de referências, mas sem instruções no documento. Focado em arquiteto. Grupo de controle: conforme esperado. |
| help/blueprints/experience-platform/deployment/appsdk.md | Diagrama da arquitetura de implantação do SDK específico do aplicativo | Caminhos de integração do SDK específicos do aplicativo e diagrama da arquitetura de coleta de dados. | Diagrama | Diagrama |  |  | Implantação do SDK específica do aplicativo |  | 0 | 3 | Substituir 3. Diagrama de implantação único com narrativa mínima. Artefato puro de arquitetura. Grupo de controle: conforme esperado. |
| help/blueprints/audience-activation/advertising-activation.md | Audience Activation para destinos sociais e Advertising | Ative públicos para redes de anúncios do Facebook e Google por meio do RTCDP com configuração de identidade e configuração de destino. | Padrão | Duplicar |  |  |  | help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md | 4 | 1 | O padrão existente abrange esse escopo. Substituição duplicada. Ação: simplificar para criar um diagrama puro e um link cruzado. |
| help/blueprints/audience-activation/audience-manager.md | Baseado em dispositivo - Direcionamento de público anônimo com o Audience Manager | Ativação de público-alvo anônima usando Audience Manager ou RTCDP para direcionamento baseado em dispositivos em canais. | Diagrama | Diagrama |  |  | Direcionamento de público com base em dispositivo anônimo |  | 1 | 2 | Narrativa mínima. Diagrama da arquitetura presente, topologia do sistema mostrada. Sem enquadramento de objetivo comercial; SDKs de implantação e conceitos de hub/borda. |
| help/blueprints/audience-activation/customer-activity.md | Acesso ao perfil em tempo real para cenários de suporte e vendas | Habilite o contexto de cliente em tempo real do suporte e dos agentes de vendas por meio da API de pesquisa de perfil. | Padrão | Padrão | audience-building-ativation | Pesquisa de perfil em tempo real para suporte e vendas |  |  | 3 | 1 | Enquadra o resultado de negócios (contexto do agente). Tem lista de verificação de pré-requisitos; etapas de implementação > 30 linhas. Caso de uso único: acesso ao perfil do hub (não personalização de borda). Distinto de padrões de personalização existentes. |
| help/blueprints/audience-activation/data-science.md | Blueprint de Ciência de dados personalizada para enriquecimento de perfis | Assimile pontuações do modelo de aprendizado de máquina no RTCDP para enriquecer perfis para personalização e segmentação. | Padrão | Padrão | audience-building-ativation | Assimilação do modelo de ciência de dados para enriquecimento de perfil |  |  | 3 | 1 | Enquadra o resultado de negócios (enriquecimento para personalização). Tem casos de uso e considerações; considerações de implementação >30 linhas. Concentre-se em fluxos de trabalho de ciência de dados, não em mensagens/ativação. |
| help/blueprints/audience-activation/enterprise-destinations.md | Ativação de público-alvo e perfil para destinos corporativos | Alterações de perfil e público-alvo ou em lote no armazenamento na nuvem e em aplicativos corporativos para vendas, suporte e análise. | Diagrama | Diagrama |  |  | Público-alvo corporativo e ativação de perfil |  | 1 | 2 | Nenhum enquadramento de objetivo comercial. Orientação de implementação esparsa. Diagrama de arquitetura + topologia de sistema para aplicativos corporativos/de armazenamento na nuvem. Visual-dominante. |
| help/blueprints/audience-activation/real-time-lookup.md | Acesso ao perfil do Real-time Edge para Personalization da Web e móvel | Acesse o perfil unificado na borda em milissegundos para personalização da Web e móvel em tempo real. | Padrão | Padrão | personalização | Acesso ao perfil do Edge para Personalization da Web/móvel |  |  | 5 | 2 | Forte estrutura empresarial (personalização de baixa latência). Dois padrões de implementação (Web SDK versus API Edge). Pré-requisitos e etapas abrangentes (>30 linhas). KPIs implícitos (latência, taxa de transferência). |
| help/blueprints/audience-activation/rtcdp-target.md | Personalization do cliente conhecido com Target | Compartilhe públicos e perfis da RTCDP com a Adobe Target para personalização da Web e móvel de visitantes conhecidos. | Misto | Divisão | personalização | Compartilhamento de público-alvo em tempo real com a Adobe Target | Arquitetura de integração do Target | help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md | 3 | 2 | Sobrepõe-se ao padrão de visitante conhecido existente, mas com escopo mais restrito (somente Target). Três padrões de integração. Diagramas de arquitetura + implantação de borda considerada. Conteúdo padrão + diagrama substancial → Dividir. |
| help/blueprints/audience-activation/segment-match.md | Audience Collaboration com correspondência de segmentos | Ative a colaboração segura do público-alvo do parceiro por meio da Correspondência de segmentos com controles de privacidade. | Padrão | Duplicar |  |  |  | help/blueprints/use-case-patterns/audience-building-activation/audience-collaboration-segment-match.md | 4 | 1 | O padrão existente cobre isso exatamente. Substituição duplicada. Conteúdo exclusivo a ser preservado no diagrama: configuração detalhada de RBAC/consentimento/governança e fluxo de trabalho de anúncio programático. |
| help/blueprints/b2b/overview.md | Blueprints de análise, ativação e marketing B2B | Página de navegação que lista análises B2B, ativação de público-alvo, grupo de compra, Marketo e blueprints do Workfront. | Navegação | Navegação |  |  |  |  |  |  | Substituir 1: arquivo chamado overview.md. Excluído da migração. |
| help/blueprints/b2b/b2bactivation.md | Blueprint da ativação de público-alvo e perfil B2B | Ative públicos-alvo B2B baseados em conta nos canais da Web, de email e de anúncios usando dados de conta e perfil. | Padrão | Duplicar |  |  |  | help/blueprints/use-case-patterns/audience-building-activation/b2b-audience-activation.md | 3 | 1 | Substituição 2: existe um padrão equivalente. O blueprint é um subconjunto mais restrito com foco em arquitetura. |
| help/blueprints/b2b/b2b-account-activation.md | Ativação de conta B2B para destinos Advertising e destinos de arquivos | Contas B2B do Target por meio do LinkedIn e destinos de armazenamento em nuvem usando criação e ativação de público-alvo da conta. | Diagrama | Diagrama |  |  | Audience Activation da conta B2B |  | 1 | 2 | Estrutura mínima de negócios, sem KPIs, narrativa mínima. Diagrama de arquitetura presente; topologia LinkedIn/cloud-storage descrita. Manter como diagrama. |
| help/blueprints/b2b/b2b-buying-group-journeys.md | Blueprint de marketing baseado em grupo e de gerenciamento de Jornadas | Projetar jornadas de conta que qualificam clientes potenciais para grupos de compra com funções definidas e interesses de solução. | Padrão | Duplicar |  |  |  | help/blueprints/use-case-patterns/campaign-management-orchestration/buying-group-based-marketing.md | 5 | 2 | Substituição 2: existe um padrão equivalente. O blueprint tem conteúdo padrão avançado, mas o padrão existente é mais abrangente. |
| help/blueprints/b2b/b2b-journeys-with-marketo.md | Jornadas B2B usando o blueprint de dados do Marketo | Implante o Journey Optimizer B2B edition com dados do Marketo para orquestrar jornadas de grupos de compra e envolvimento com a conta. | Padrão | Padrão | b2b | Jornadas de conta B2B com integração de dados do Marketo |  |  | 4 | 1 | Forte enquadramento empresarial. KPIs listados; várias opções de implementação; considerações abrangentes (>30 linhas). Diferenciado do padrão existente pela profundidade da integração de dados do Marketo (configuração XDM, compilação de identidade, bloqueio de campo). Rotas para a nova categoria b2b/. |
| help/blueprints/b2b/ajo-b2b-paid-media-controller.md | AJO B2B - Account Journey Orchestration - Controlador de mídia paga | Orquestrar campanhas de mídia paga B2B usando a lógica de cascata para atribuir contas a campanhas e ativar para destinos. | Padrão | Padrão | b2b | Orquestração de mídia paga B2B por meio da lógica de divisão de caminho em cascata |  |  | 4 | 2 | Forte enquadramento empresarial. KPIs explícitos; várias opções de implementação; pré-requisitos; narrativa com mais de 30 linhas. Distinto do padrão existente de grupos de compra (concentra-se na priorização de mídia paga, não na criação). Rotas para a nova categoria b2b/. |
| help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/overview.md | Visão geral do blueprint de integração do Marketo Engage e do Workfront | Visão geral do planejamento de campanha para a automação de execução usando o Marketo Engage e o Workfront com Fusion. | Navegação | Navegação |  |  |  |  |  |  | Substituir 1: arquivo chamado overview.md. Excluído da migração. |
| help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md | Blueprint de entrada e criação | Automatize a entrada de solicitação de campanha de marketing B2B para criação usando os formulários do Workfront e os modelos de programa do Marketo Engage. | Padrão | Padrão | b2b | Entrada de solicitação de campanha e criação automatizada de programa |  |  | 4 | 1 | Forte estrutura de negócios na velocidade da campanha. KPIs implícitos (erros/redução de retrabalho); etapas do fluxo de trabalho >30 linhas; lista de verificação de preparação. Rotas para a nova categoria b2b/ (Marketo+Workfront ops são predominantemente B2B). |
| help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md | Revisão e aprovação de blueprint | Integre workflows de prova e aprovação do Workfront a ativos de email do Marketo Engage usando a automação do Fusion. | Padrão | Padrão | b2b | Fluxo de trabalho de revisão e aprovação de ativos da campanha |  |  | 3 | 2 | Forte estrutura de negócios em conformidade e precisão; KPIs implícitos (velocidade de aprovação); narrativa >30 linhas; seção de planejamento de fluxo de trabalho. Rotas para a nova categoria b2b/. |
| help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md | Histórias de sucesso do cliente | Links para estudos de caso de clientes e webinários que mostram os resultados da integração do Marketo e do Workfront. | Navegação | Navegação |  |  |  |  |  |  | Conteúdo mínimo (6 hiperlinks). Nenhum enquadramento comercial, KPIs, arquitetura ou narrativa. Tratado como Navegação. O gravador deve confirmar. |
| help/blueprints/customer-journey-analytics/overview.md | blueprints da Customer Journey Analytics | Unifique e analise os dados e o comportamento do cliente em vários canais para criar visualizações baseadas em jornada. | Navegação | Navegação |  |  |  |  |  |  | Substituir 1: overview.md. Página de aterrissagem estilo TOC. Excluído da migração. |
| help/blueprints/customer-journey-analytics/b2b-cja.md | Blueprint do Customer Journey Analytics B2B | Relatórios e análises do CJA com base em conta para organizações B2B usando a conta como modelo de dados principal. | Padrão | Duplicar |  |  |  | help/blueprints/use-case-patterns/analysis/b2b-analytics.md | 4 | 2 | Substituição 2: o padrão equivalente abrange a análise de nível de conta B2B com o CJA B2B edition. Ação: simplificar para diagrama, link cruzado. |
| help/blueprints/customer-journey-analytics/cja-rtcdp.md | Customer Journey Analytics com o blueprint da Real-time Customer Data Platform | Crie e publique públicos do CJA no RTCDP para direcionamento e personalização. | Diagrama | Diagrama |  |  | Integração de publicação de público do CJA para o RTCDP |  | 1 | 3 | Forte foco na arquitetura (integração entre sistemas, forma de implantação). Narrativa mínima. Conteúdo exclusivo: medidas de proteção de latência de publicação de público do CJA. |
| help/blueprints/customer-journey-analytics/cja-ajo.md | Blueprint do Customer Journey Analytics com Journey Optimizer | Analise a entrega do AJO e os dados de interação no CJA; publique públicos do CJA na AJO. | Diagrama | Diagrama |  |  | Integração e análise do CJA com o AJO |  | 1 | 3 | Forte foco na arquitetura. Narrativa mínima. Conteúdo exclusivo: padrão bidirecional de compartilhamento de dados CJA-AJO. |
| help/blueprints/customer-journey-analytics/analysis.md | Blueprint de análise de dados e inteligência | Use o Serviço de consulta da Experience Platform para análise exploratória de dados do data lake. | Diagrama | Diagrama |  |  | Integração do Experience Platform Query Service e da ferramenta de BI |  | 1 | 3 | Abrange o Serviço de consulta, NÃO específico do CJA. Pode estar no local errado na pasta do CJA; considere realocar para a experience-platform/. Público-alvo forte de arquitetos (PostgreSQL, ferramentas de BI). |
| help/blueprints/customer-journeys/overview.md | Planos de jornada do cliente | Plataformas de marketing modernas que oferecem suporte a jornadas orientadas por eventos e campanhas iniciadas por marcas em todos os canais. | Navegação | Navegação |  |  |  |  |  |  | Substituir 1: overview.md. Índice para subcategorias de jornada; descreve o posicionamento do Journey Optimizer e do Campaign. |
| help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-overview.md | Blueprints da Journey Optimizer | Orquestração de perfis :1 orientada por eventos e comunicações de marca baseadas em público-alvo em todos os canais. | Navegação | Navegação |  |  |  |  |  |  | Substituir 1: overview.md. Página de aterrissagem com guias de caso de uso e padrões de integração. |
| help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-journeys.md | Journey Optimizer - Mensagens acionadas e Blueprint do Adobe Experience Platform | Fluxos de trabalho orientados por eventos em tempo real que fornecem experiências personalizadas em várias etapas com base nos comportamentos do cliente. | Padrão | Duplicar |  |  |  | help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md | 4 | 2 | Substituir 2 com aviso: agente sinalizado como provavelmente duplicado, mas incerto. Verifique o alinhamento do escopo antes de reduzir. As considerações de arquitetura podem ser exclusivas (atualização do perfil, tempo de qualificação do segmento) e merecem ser preservadas no diagrama. |
| help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-campaigns.md | Journey Optimizer - Orquestração de campanha | Comunicações programadas com base no público-alvo em várias etapas nos canais de saída: email, SMS, push, correspondência direta. | Padrão | Duplicar |  |  |  | help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md | 3 | 2 | Substituir 2: padrão equivalente. Vários diagramas de arquitetura; preservar como diagrama. Conteúdo exclusivo: banco de dados relacional/portal de público-alvo/detalhes da arquitetura de perfil fino. |
| help/blueprints/customer-journeys/journey-optimizer/3rd-party-messaging.md | Journey Optimizer - Blueprint de mensagens de terceiros | Demonstra a integração do Journey Optimizer com sistemas de mensagens de terceiros para comunicações orquestradas. | Misto | Divisão | campaign-management-orchestration | Integração de mensagens de terceiros com o Journey Optimizer | Arquitetura de mensagens de terceiros |  | 2 | 2 | Pontuações empatadas → Dividir. Diagrama (topologia de sistema para sistema) mais conteúdo de padrão (etapas de implementação, restrições de integração: autenticação do portador, sem IPs estáticos, limites de taxa). Vale a pena preservar ambos. |
| help/blueprints/customer-journeys/decision-management/decision-management-overview.md | Projetos da Gestão de decisões | Forneça ofertas personalizadas nas jornadas do cliente por meio de uma biblioteca de ofertas centralizada e um mecanismo de decisão. | Navegação | Navegação |  |  |  |  |  |  | Substituir 1: overview.md. Descreve os componentes e as abordagens de implantação de borda vs. hub do Gerenciamento de decisão. |
| help/blueprints/customer-journeys/decision-management/decision-management-edge.md | Gestão de decisões no blueprint do Edge | Forneça ofertas personalizadas em experiências da Web e móveis em tempo real com latência de subsegundos na rede de borda. | Misto | Duplicar |  |  |  | help/blueprints/use-case-patterns/personalization/offer-decisioning.md | 2 | 3 | Substituição 2: mapeia para a decisão de oferta. Variante de implantação do Edge — considere a consolidação com o blueprint do hub em um único diagrama de opções de implantação. |
| help/blueprints/customer-journeys/decision-management/decision-management-hub.md | Gestão de decisões no blueprint do Hub | Forneça ofertas personalizadas em canais, incluindo quiosques, experiências assistidas por agente e entregas de saída. | Misto | Duplicar |  |  |  | help/blueprints/use-case-patterns/personalization/offer-decisioning.md | 2 | 3 | Substituição 2: mapeia para a decisão de oferta. Variante de implantação de hub — considere a consolidação com um blueprint de borda em um único diagrama de opções de implantação. |
| help/blueprints/customer-journeys/campaign-v8/campaign-v8-overview.md | Blueprint, campanha e plataforma do Campaign v8 | Plataforma de gerenciamento de campanhas em lote de última geração com recursos de ETL, segmentação e mensagens transacionais. | Padrão | Padrão | campaign-management-orchestration | Orquestração em lote e mensagens transacionais do Campaign v8 | Modelos de implantação da arquitetura do Campaign v8 |  | 4 | 3 | Abordagem técnica distinta (Campaign v8 nativo, não AJO). Vários diagramas de arquitetura, enquadramento comercial, KPIs implícitos em medidas de proteção (lote de 20 M msg/h, 1 M/h em tempo real). Nenhum equivalente no catálogo de padrões existente. Observação: as pontuações se qualificam como Divisão também — proponha Padrão, mas o gravador pode desejar que o diagrama seja retido. |
| help/blueprints/customer-journeys/campaign-v8/rtcdp-and-campaign-v8.md | Padrão de integração do Real-Time CDP com o Adobe Campaign v8 | Mostra a integração de público e perfil do RTCDP com o Campaign v8 para conversas personalizadas. | Diagrama | Diagrama |  |  | RTCDP - Audiência e troca de perfil do Campaign v8 |  | 1 | 2 | Blueprint do conector de integração, não caso de uso independente. Diagrama + pré-requisitos/medidas de proteção breves. Orientada a arquitetos. |
| help/blueprints/customer-journeys/campaign-v8/ajo-and-campaign-v8.md | Blueprint do Journey Optimizer com Adobe Campaign v8 | Demonstra a orquestração do AJO com mensagens transacionais do Campaign v8 para 1:1 experiências. | Diagrama | Diagrama |  |  | Journey Optimizer - Integração de mensagens transacionais do Campaign v8 |  | 1 | 2 | Conector de integração. Diagrama + etapas de implementação + restrições técnicas (controle de 4.000 msg/5 min, apenas iniciado pelo evento). Link cruzado para padrões do AJO e do Campaign v8. |
| help/blueprints/customer-journeys/campaign-v7/campaign-v7-overview.md | Blueprint do Campaign v7 | Obsoleto: mensagens baseadas em lote, integração, remarketing, correspondência direta, mensagens transacionais simples. | Navegação | Navegação |  |  |  |  |  |  | PRODUTO OBSOLETO (links de destaque para a v8). Conteúdo mínimo (somente diagrama de arquitetura). Não migrar. |
| help/blueprints/customer-journeys/campaign-v7/rtcdp-and-campaign-v7.md | Padrão de integração do Real-Time CDP com Campaign v7 e Campaign Standard | Apresenta a integração do RTCDP e do Perfil do cliente em tempo real com o Campaign v7/Standard para conversas personalizadas. | Diagrama | Diagrama |  |  | RTCDP - Campaign v7/Intercâmbio de públicos e perfis Standard |  | 1 | 2 | OBSOLETO. Conector de integração. Diagrama + etapas abrangentes de implementação. Não migre para um novo padrão; deixe como está. |
| help/blueprints/customer-journeys/campaign-v7/ajo-and-campaign-v7.md | Blueprint do Journey Optimizer com Adobe Campaign v7 | Demonstra a orquestração do AJO com mensagens transacionais do Campaign v7 para 1:1 experiências. | Diagrama | Diagrama |  |  | Journey Optimizer - Integração de mensagens transacionais do Campaign v7 |  | 1 | 2 | OBSOLETO. Conector de integração. Diagrama + etapas de implementação + restrições. Não migrar; deixar como está. |
