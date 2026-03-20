---
name: industry-use-case-builder
description: 'Criação de guias de novos casos de uso do setor para o repositório de blueprints da Adobe Experience Platform. Use essa habilidade ao adicionar um novo caso de uso a um setor vertical (varejo, automotivo, saúde, serviços financeiros, seguros, mídia e entretenimento, telecomunicações, viagens e hospitalidade, B2B), quando o usuário quiser adicionar cenários de negócios a páginas do setor ou ao atualizar o catálogo de casos de uso. Lida com o fluxo de trabalho completo: coletar detalhes do caso de uso, avaliar o nível de maturidade, gerar conteúdo, atualizar a página de visão geral do setor e o catálogo de casos de uso e chamar a habilidade use-case-icon-generator para a criação de ícones.'
source-git-commit: ed8928687806b619e95d8d320478d27c13722a80
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 1%

---


# Construtor de casos de uso do setor

Essa habilidade orienta a criação de novos casos de uso do setor para o repositório de blueprints da Adobe Experience Platform. Siga cada fase sequencialmente. Leia os arquivos de referência antes de começar:

- `references/use-case-template.md` — modelo exato para seções de caso de uso
- `references/catalog-row-template.md` — formato exato para linhas de tabela de catálogo
- `references/maturity-criteria.md` — rubrica detalhada para avaliação de maturidade

## Fase 1: Coleta de informações

Entrevistar o usuário para coletar todos os detalhes necessários antes de gerar qualquer conteúdo.

### Campos obrigatórios

1. **Vertical do setor** — Deve ser um de:
   - automotivo
   - b2b
   - serviços financeiros
   - saúde
   - seguro
   - media-entertainment
   - varejo
   - telecomunicações
   - viagem-hospitalidade

2. **Nome do caso de uso** — Um título claro e descritivo (por exemplo, &quot;Recuperação de email de carrinho abandonado&quot;, &quot;Campanhas de adesão à medicação&quot;).

3. **Descrição** — Frases 1 a 2 que descrevem o cenário comercial e a importância dele.

4. **Impacto nos negócios** — resultados quantificados com métricas específicas (por exemplo, &quot;aumento de 20 a 30% nas taxas de click-through&quot;, &quot;melhoria de 15 a 25% nas taxas de reabastecimento&quot;).

5. **Padrão de caso de uso** — É necessário mapear exatamente para um destes padrões existentes:
   - Audience Activation para destinos
   - Audience Collaboration com correspondência de segmentos
   - Encaminhamento de eventos
   - Audience Activation B2B
   - Visitante anônimo - Web Personalization
   - Personalization de aplicativo/Web de visitante conhecido
   - Offer Decisioning
   - Recomendação comportamental
   - Ativação de mensagem de saída em lote
   - Mensagens acionadas por evento
   - Jornada orquestrada em várias etapas
   - Jornada entre canais com decisão
   - Compra de marketing baseado em grupo e gerenciamento de Jornadas
   - Análise do cliente e geração de Insight
   - Análise B2B
   - Experiência de conversa do Brand Concierge

6. **Considerações técnicas** — de 4 a 8 pontos que abrangem requisitos de dados, integrações, necessidades normativas/de conformidade, considerações de desempenho e notas de arquitetura.

Solicite os campos ausentes antes de continuar. Não assuma nem fabrique detalhes.

## Fase 2: Avaliação da maturidade

Leia `references/maturity-criteria.md` para obter a rubrica completa. Atribua um dos três níveis de maturidade:

- **Básico** `[!BADGE Foundational]{type=Neutral}` — Padrões de etapa única ou acionados por eventos (Mensagens Acionadas por Eventos, Saída em Lote), requisitos simples de dados, IA/ML mínima, integrações padrão.
- **Emergente** `[!BADGE Emerging]{type=Informative}` — jornadas em várias etapas, dados comportamentais, modelos de recomendação, personalização de visitantes conhecidos, complexidade de integração moderada.
- **Avançado** `[!BADGE Advanced]{type=Caution}` — Decisão entre canais, previsão baseada em IA, decisão de ofertas, orquestração complexa e várias integrações de sistemas.

### Fluxo de trabalho de avaliação

1. Identificar a qual padrão de caso de uso o caso de uso é mapeado.
2. Verifique a lista &quot;Padrões típicos&quot; nos critérios de maturidade para uma correspondência rápida.
3. Se o padrão não indicar claramente a maturidade, avalie a complexidade dos dados, os requisitos de IA/ML e o escopo da integração.
4. Apresente a avaliação ao usuário com o raciocínio: &quot;Com base no mapeamento de padrão ({pattern}) e {key factors}, eu classificaria como {level} porque {reasoning}.&quot;
5. Aguarde a confirmação ou substituição do usuário antes de prosseguir para a geração de conteúdo.

## Fase 3: Geração de conteúdo

Gerar ou atualizar conteúdo em dois arquivos.

### A. Ficheiro com uma visão geral do setor

**Caminho do arquivo:** `/help/blueprints/industry-use-cases/{industry}/{industry}-overview.md`

Leia o arquivo existente primeiro para entender a estrutura e o conteúdo atuais. Em seguida, adicione uma nova seção seguindo o modelo exato de `references/use-case-template.md`:

```markdown
## {Use Case Title}

{1-2 sentence description of the business scenario and why it matters}

### Business impact

{Quantified business outcomes, e.g., "Retailers typically see a 20-30% increase in click-through rates..."}

### How to implement

Use the [{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md) pattern. {1-2 sentence explanation of why this pattern applies}

### Technical considerations

- {4-8 bullet points covering data integration, regulatory, performance, or architectural considerations}
```

Coloque a nova seção após as seções de caso de uso existentes, mantendo a formatação consistente.

### B. Catálogo de casos de uso

**Caminho do arquivo:** `/help/blueprints/industry-use-cases/use-case-catalog.md`

Leia o arquivo de catálogo existente primeiro. Adicione uma nova linha à guia correta do setor. O catálogo usa uma estrutura de guias com `>[!TAB {Industry}]` marcadores. Cada guia contém uma tabela com estas colunas:

| Coluna | Conteúdo |
| --- | --- |
| Ícone | `<img src="assets/use-case-icons/{industry}/icon-{kebab-name}.png" alt="{Alt Text}" width="40">` (deixe vazio se nenhum ícone ainda) |
| Caso de uso | `[{Use Case Title}]({industry}/{industry}-overview.md#{anchor})` onde âncora é o cabeçalho no caso kebab |
| Descrição | Resumo em uma frase |
| Maturidade | Sintaxe de selo para o nível atribuído |
| Padrão | `[{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md)` |

**Regra de posicionamento:** Em cada guia do setor, as linhas são agrupadas por maturidade, nesta ordem: Primeiros fundamentos, Novos e Avançados. Coloque a nova linha no final do grupo de maturidade correto.

Os caminhos de arquivo padrão são:
- `audience-building-activation/audience-activation-to-destinations.md`
- `audience-building-activation/audience-collaboration-segment-match.md`
- `audience-building-activation/event-forwarding.md`
- `audience-building-activation/b2b-audience-activation.md`
- `personalization/anonymous-visitor-web-personalization.md`
- `personalization/known-visitor-web-app-personalization.md`
- `personalization/offer-decisioning.md`
- `personalization/behavioral-recommendation.md`
- `campaign-management-orchestration/batch-outbound-message-activation.md`
- `campaign-management-orchestration/event-triggered-messaging.md`
- `campaign-management-orchestration/multi-step-orchestrated-journey.md`
- `campaign-management-orchestration/cross-channel-journey-with-decisioning.md`
- `campaign-management-orchestration/buying-group-based-marketing.md`
- `analysis/customer-analytics-insight-generation.md`
- `analysis/b2b-analytics.md`
- `conversational-experience/brand-concierge-conversational-experience.md`

## Fase 4: Geração de ícones

Após a criação do conteúdo, chame a habilidade `use-case-icon-generator` para gerar uma especificação de ícone para o novo caso de uso. Forneça à habilidade:
- O nome do caso de uso
- O setor vertical
- Uma breve descrição do caso de uso

Depois que o usuário tiver o arquivo de ícone gerado, atualize a linha de catálogo para incluir a referência do ícone:

```
<img src="assets/use-case-icons/{industry}/icon-{kebab-name}.png" alt="{Alt Text}" width="40">
```

## Fase 5: validação

Antes de terminar, verifique todos os itens a seguir:

1. **Conformidade de modelos** — A seção de visão geral do setor segue o modelo exatamente (## título, descrição, ### Impacto nos negócios, ### Como implementar, ### Considerações técnicas).
2. **Posicionamento do catálogo** — A linha do catálogo está na guia correta do setor e no grupo de maturidade correto (Funcional, Emergente e Avançado).
3. **Validade do link de padrão** — O link de padrão na visão geral e no catálogo usa um caminho de arquivo de padrão válido da lista acima.
4. **Consistência de âncora** — A âncora no link do catálogo (por exemplo, `#abandoned-cart-email-recovery`) corresponde ao cabeçalho `##` no arquivo de visão geral convertido em maiúsculas e minúsculas.
5. **Convenções de caminho de ícone** — O caminho de ícone segue `assets/use-case-icons/{industry}/icon-{kebab-name}.png`.

Relate quaisquer problemas encontrados durante a validação e corrija-os antes de concluir.
