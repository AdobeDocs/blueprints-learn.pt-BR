---
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---
# Modelo de linha do catálogo de casos de uso

## Formato de linha

Cada linha na tabela de catálogo de casos de uso segue este formato exato:

```
| <img src="assets/use-case-icons/{industry}/icon-{kebab-name}.png" alt="{Alt Text}" width="40"> | [{Use Case Title}]({industry}/{industry}-overview.md#{heading-anchor}) | {One-sentence description} | [!BADGE {Maturity}]{type={Type}} | [{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md) |
```

### Linha sem ícone (use quando o ícone ainda não estiver disponível)

```
| | [{Use Case Title}]({industry}/{industry}-overview.md#{heading-anchor}) | {One-sentence description} | [!BADGE {Maturity}]{type={Type}} | [{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md) |
```

## Referência do campo

| Campo | Formato | Exemplo |
| --- | --- | --- |
| indústria | nome do diretório do kebab-case | varejo, serviços financeiros, viagem e hospitalidade |
| kebab-name | kebab-case nome do caso de uso para o ícone | carrinho abandonado, criação de leads |
| Texto Alternativo | Primeira letra maiúscula, curta | Carrinho abandonado, criação de leads |
| âncora de cabeçalho | kebab-case do cabeçalho ## na visão geral | abandonou-cart-email-recovery |
| Maturidade + Tipo | Sintaxe do selo | `[!BADGE Foundational]{type=Neutral}`, `[!BADGE Emerging]{type=Informative}`, `[!BADGE Advanced]{type=Caution}` |

## Marcadores de guia do setor no catálogo

O arquivo de catálogo usa esta estrutura de guias:

- `>[!TAB Retail]`
- `>[!TAB Automotive]`
- `>[!TAB Financial Services]`
- `>[!TAB Healthcare]`
- `>[!TAB Insurance]`
- `>[!TAB Media & Entertainment]`
- `>[!TAB Telecommunications]`
- `>[!TAB Travel & Hospitality]`
- `>[!TAB B2B]`

## Ordenação em guias

As linhas são ordenadas por nível de maturidade:

1. **Funcional** linhas primeiro (type=Neutral)
2. **Emergentes** linhas por segundo (type=Informative)
3. **Avançado** linhas por último (type=Caution)

No mesmo nível de maturidade, adicione novas linhas no final desse grupo.
