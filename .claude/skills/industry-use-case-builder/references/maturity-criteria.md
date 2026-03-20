---
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---
# Critérios de avaliação de maturidade do caso de uso

## Níveis de maturidade

### Fundamentário

**Medalha:** `[!BADGE Foundational]{type=Neutral}`

Um caso de uso é o **Foundational** quando:

- Mapeia para um padrão de etapa única ou acionado por evento (Mensagens acionadas por evento, Ativação de mensagens de saída em lote)
- Tem requisitos de dados simples (tipo de evento único, atributos de perfil padrão)
- Requer o mínimo ou nenhum recurso de AI/ML
- Usa delivery de canal padrão (email, SMS, push) sem orquestração complexa
- Tem padrões de implementação bem estabelecidos com práticas recomendadas claras
- Requer menos integrações do sistema (geralmente de 1 a 2 fontes de dados)

**Padrões típicos:** Mensagens acionadas por eventos, Ativação de Mensagens de Saída em Lote

**Exemplos:** Recuperação de carrinho abandonado, lembretes de compromisso, notificações de serviço, alertas de queda de preço, lembretes de pagamento de fatura

### Emergentes

**Medalha:** `[!BADGE Emerging]{type=Informative}`

Um caso de uso é **Emergente** quando:

- Mapeia para um padrão de várias etapas ou personalização (Jornada orquestrada em várias etapas, Personalization de visitante conhecido, Recomendação comportamental, Personalization de visitante anônimo)
- Requer coleta e análise de dados comportamentais
- Usa modelos de recomendação ou resolução de perfil de visitante conhecido
- Envolve sequências de criação multitoque com lógica de ramificação
- Tem complexidade de integração moderada (2 a 4 fontes de dados)
- Pode exigir ativação de público ou segmentação baseada em segmentos

**Padrões típicos:** Jornada Orquestrada Em Várias Etapas, Personalization De Visitantes Conhecidos Da Web/Aplicativos, Recomendação Comportamental, Personalization Da Web De Visitantes Anônimos, Audience Activation B2B

**Exemplos:** série de boas-vindas, campanhas de adesão a medicamentos, painéis de conta personalizados, pontuação de clientes potenciais, recomendações de conteúdo

### Avançado

**Medalha:** `[!BADGE Advanced]{type=Caution}`

Um caso de uso é **Avançado** quando:

- Mapeia para um padrão de orquestração de decisão ou entre canais (Jornada entre canais com o Decisioning, Offer Decisioning)
- Exige previsão ou pontuação de propensão alimentada por IA
- Usa lógica de decisão centralizada em vários canais simultaneamente
- Envolve orquestração complexa com decisões em tempo real em vários pontos de jornada
- Tem alta complexidade de integração (mais de 4 fontes de dados, feeds de dados em tempo real)
- Requer regras de negócios sofisticadas, gerenciamento de prioridades e controle de frequência

**Padrões típicos:** Jornada entre canais com Decisioning, Offer Decisioning

**Exemplos:** Prevenção de churn com pontuação AI, recomendações de produtos para o estágio de vida, otimização de venda cruzada, personalização de programas de fidelidade, ofertas exclusivas da VIP

## Fluxo de trabalho de avaliação

1. Identificar para qual padrão de caso de uso o caso de uso é mapeado
2. Verifique a lista &quot;Padrões típicos&quot; acima para obter uma correspondência rápida
3. Se o padrão não indicar claramente a maturidade, avalie a complexidade dos dados, os requisitos de IA/ML e o escopo da integração
4. Apresente a avaliação ao usuário com o raciocínio: &quot;Com base no mapeamento de padrão ({pattern}) e {key factors}, eu classificaria como {level} porque {reasoning}.&quot;
5. Permitir que o usuário confirme ou substitua antes de continuar
