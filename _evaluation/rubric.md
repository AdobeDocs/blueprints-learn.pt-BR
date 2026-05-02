---
source-git-commit: 7511cc0e5c099d5d3ee1275a374cd9ffdc972335
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---
# Rubrica de avaliação do blueprint

Esta rubrica é aplicada a todos os documentos na seção &quot;Diagramas de arquitetura e blueprints&quot;
de [TOC.md](../help/blueprints/TOC.md) (linhas 76-133) para recomendar se cada blueprint deve se tornar um
**Padrão de Caso de Uso**, um **Diagrama de Arquitetura**, ambos (**Split**), ou ser sinalizado como um
**Duplicar** de um padrão existente.

A saída da aplicação desta rubrica é [blueprint-audit.md](blueprint-audit.md).

## Definições

- **Padrão de caso de uso** — um documento que descreve um objetivo técnico ou comercial específico e
definir possíveis abordagens de execução e considerações para alcançar esse objetivo.
Forma canônica: `.claude/skills/use-case-pattern-builder/references/pattern-template.md`.
- **Diagrama de Arquitetura** — um diagrama visual que representa a funcionalidade de um sistema, o
integrações e fluxos de dados. Narrativa mínima; o diagrama é o artefato.
Exemplo canônico: [platform-data-flow.md](../help/blueprints/experience-platform/platform-data-flow.md).

## Pontuação

Cada blueprint é lido de ponta a ponta e pontuado contra oito sinais binários. Cada sinal contribui
+1 para a pontuação do padrão ou a pontuação do diagrama.

### Sinais de padrão (cada = +1 Padrão)

1. **Enquadramento do objetivo comercial** — quadros de receita, retenção, aquisição, geração de leads, custo
redução, experiência do cliente ou resultado comercial semelhante.
2. **KPIs ou métricas de sucesso** — nomeia explicitamente métricas, taxas de conversão, taxas de correspondência, ROI ou
medidas de resultado semelhantes.
3. **Várias opções de implementação ou níveis de maturidade** — apresenta a Opção A/Opção B, básica versus
alternativas avançadas ou comparáveis que o leitor escolher entre.
4. **Lista de verificação de pré-requisitos ou preparação** — lista o que deve estar em vigor antes da implementação.
5. **Etapas de implementação da narrativa > ~30 linhas** — orientação substantiva de como implementar, não
apenas uma breve visão geral.

### Sinais de diagrama (cada = +1 Diagrama)

&#x200B;6. **Imagem de arquitetura/fluxo de dados presente** — `.svg`, `.png` ou `.jpg` mostrando a topologia do sistema,
fluxo de dados ou setas de integração.
&#x200B;7. **Topologia de integração entre sistemas, forma de implantação ou medidas de proteção** — descreve como
conexão de componentes, onde os dados estão, modelos de implantação (borda vs. hub) ou limites de capacidade.
&#x200B;8. **O público-alvo são arquitetos de soluções** — a estrutura usa implantação, SDK, borda, hub ou semelhante
terminologia orientada por arquiteto em vez de enquadramento orientado por profissionais de marketing (campanhas, jornadas,
públicos-alvo).

## Lógica de recomendação

Aplique as regras de substituição primeiro. Se nenhuma substituição for acionada, derive a recomendação das pontuações.

### Regras de substituição (prioridade mais alta)

1. **O nome do arquivo é`overview.md`** → recomendação = `Navigation`. Excluído da migração; a variável
é uma página de aterrissagem no estilo do sumário que será revisada após a conclusão dos arquivos filho.
2. **Um padrão equivalente já existe em`help/blueprints/use-case-patterns/`** →
recomendação = `Duplicate`. A ação de migração é simplificar o blueprint para um
e adicione um link cruzado &quot;Ver padrão do caso de uso&quot; ao padrão existente.
Registre o caminho padrão existente na coluna `duplicate_of`.
3. **O arquivo está em `experience-platform/` e não tem sinal de objetivo comercial (#1)** → padrão para
   `Diagram` independentemente das outras pontuações. Esta pasta é a camada de visão geral da arquitetura.

### Recomendação baseada em pontuação (quando nenhuma substituição é acionada)

| Pontuação do padrão | Pontuação do diagrama | Recomendação | Raciocínio |
| --- | --- | --- | --- |
| ≥ 3 | ≤ 1 | `Pattern` | Sinais de padrão fortes, sinais de diagrama fracos → migre para o padrão. |
| ≤ 1 | ≥ 2 | `Diagram` | Sinais de padrão fracos, foco visual/topologia dominante → manter como diagrama. |
| ≥ 3 | ≥ 2 | `Split` | Tanto o conteúdo de padrão rico e um diagrama significativo → padrão de extração, reduzir original para diagrama, link cruzado. |
| 2 | 2 | `Split` | Gravata em força moderada → divisão. |
| 2 | ≤ 1 | `Pattern` | Inclinação do padrão, sem valor de diagrama significativo. |
| ≤ 1 | ≤ 1 | `Diagram` | Thin no geral — é provavelmente uma página de arquitetura mínima existente. |

## Como aplicar a rubrica

Para cada arquivo de marcação de blueprint no escopo:

1. Leia o arquivo completo de ponta a ponta.
2. Marque cada um dos oito sinais presentes/ausentes.
3. Aplicar regras de substituição em ordem. Se um for acionado, essa é a recomendação.
4. Caso contrário, calcule a pontuação do padrão e a pontuação do diagrama e procure a recomendação.
5. Para `Pattern` e `Split` recomendações, proponha:
   - `proposed_pattern_category` — um de:
     `audience-building-activation`, `personalization`, `campaign-management-orchestration`,
     `analysis`, `conversational-experience` ou uma nova categoria denominada `(new) <name>`.
   - `proposed_pattern_title` — um título curto e orientado a ações seguindo o padrão existente
estilo de nomenclatura.
6. Para `Diagram` e `Split` recomendações, proponha:
   - `proposed_diagram_title` — normalmente, o título existente é cortado do enquadramento comercial.
7. Capturar quaisquer duplicatas encontradas comparando o escopo do blueprint com o catálogo de padrões existente
em `duplicate_of`.
8. Registre as perguntas abertas, o conteúdo técnico exclusivo que vale a pena preservar ou o risco de migração em `notes`.

## Catálogo de padrões de casos de uso existente (para detecção de duplicidades)

| Categoria | Padrões |
| --- | --- |
| audience-building-ativation | audience-ativation-to-destinations, audience-collaboration-segment-match, b2b-audience-ativation, encaminhamento de eventos |
| personalização | anonymous-visitor-web-personalization, known-visitor-web-app-personalization, offer-decisioning, recomendação comportamental |
| campaign-management-orchestration | batch-outbound-message-ativation, event-triggered-messaging, multi-step-orchestrated-jornada, cross-channel-jornada-with-decisioning, marketing baseado em grupo de compra |
| análise | customer-analytics-insight-generation, análise b2b |
| conversational-experience | brand-concierge-conversational-experience |
