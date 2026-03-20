---
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 3%

---
# Guia de estilo do ícone do caso de uso

## Visão geral

Os ícones de caso de uso servem como identificadores visuais na tabela de catálogo de casos de uso. Eles devem ser imediatamente reconhecidos com uma largura de exibição de 40px, mantendo a qualidade em sua resolução original de 1024x1024.

## Especificações técnicas

| Propriedade | Valor |
| --- | --- |
| Dimensões | 1024 x 1024 pixels |
| Formato | PNG (RGB de 8 bits ou RGBA) |
| Tamanho do arquivo | 900 KB - 1,4 MB típico |
| Tamanho de exibição | Largura de 40px em tabelas de catálogo |
| Nomenclatura | `icon-{kebab-case-name}.png` |
| Caminho de armazenamento | `/help/blueprints/industry-use-cases/assets/use-case-icons/{industry}/` |

## Diretrizes de estilo visual

### Composição
- **Assunto central único** — cada ícone deve apresentar uma metáfora visual clara que represente o conceito de caso de uso
- **Composição centralizada** — O assunto principal deve ser centralizado com espaço em branco balanceado
- **Sem texto** — O texto é ilegível em 40px; confie totalmente na metáfora visual
- **Nenhuma cena complexa** — Evite composições de vários elementos, planos de fundo com muitos objetos ou cenas narrativas
- **Silhuetas em negrito** — A forma do ícone deve ser reconhecível, mesmo como uma silhueta pequena

### Cor e tom
- **Paleta limpa e moderna** — use cores profissionais apropriadas para a empresa
- **Coesão do setor** — Os ícones dentro do mesmo setor devem parecer como se fossem um todo
- **Alto contraste** — Verifique se o assunto principal se destaca claramente do plano de fundo
- **Evite neon ou cores excessivamente saturadas** — Mantenha a paleta refinada e profissional

### Estilo
- **Moderno e profissional** — linhas limpas, acabamento polido
- **Renderização consistente** — Todos os ícones devem parecer vir do mesmo sistema de design
- **3D ou plano é aceitável** — Mas seja consistente dentro de um negócio vertical
- **Evitar fotorealismo** — Estilo ilustrado ou renderizado preferido para consistência
- **Não há logotipos de marca nem imagens de marca comercial** — Use metáforas visuais genéricas

### Ensaio de legibilidade para pequenas dimensões
Antes de finalizar, dimensione mentalmente a imagem para 40px:
- É possível identificar o assunto principal?
- Há contraste suficiente entre o primeiro plano e o plano de fundo?
- Há algum detalhe fino que se transforme em ruído visual?
- A forma é lida claramente sem cor (em caso de acessibilidade)?

## Exemplos de metáforas visuais por setor

### Varejo
| Caso de uso | Metáfora visual |
| --- | --- |
| Carrinho abandonado | Carrinho de compras com itens |
| Recomendações de produto | Caixa de presente ou produtos preparados |
| Venda cruzada venda adicional | Itens de compra conectados |
| Série de boas-vindas | Cartão de boas-vindas ou presente |
| Queda de preço | Etiqueta de preço com seta para baixo |

### Automotivo
| Caso de uso | Metáfora visual |
| --- | --- |
| Lembretes de serviço | Chave inglesa ou calendário de serviço |
| Compra de Veículo | Carro com chaves |
| Trade-In | Setas de troca de carro |
| Carro conectado | Carro com conexão digital |

### Serviços de saúde
| Caso de uso | Metáfora visual |
| --- | --- |
| Lembrete de Compromisso | Calendário com estetoscópio |
| Aderência à medicação | Engarrafamento ou prescrição |
| Cuidados Preventivos | Escudo com símbolo de saúde |

### Serviços financeiros
| Caso de uso | Metáfora visual |
| --- | --- |
| Fomento de chumbo | Gráfico de crescimento ou plântula |
| Prevenção de churn | Símbolo de blindagem ou retenção |
| Estágio de vida | Cronograma de marcos de vida |

### B2B
| Caso de uso | Metáfora visual |
| --- | --- |
| ABM | Target com criação |
| Pontuação de lead | Medidor de pontuação ou termômetro |
| Renovação do contrato | Documento com símbolo de atualização |

### Viagens e hospitalidade
| Caso de uso | Metáfora visual |
| --- | --- |
| Abandono do carrinho | Mala ou reserva |
| Programa de fidelidade | Cartão-fidelidade ou selo de estrela |
| Lembretes de reserva | Calendário com avião/hotel |

### Seguro
| Caso de uso | Metáfora visual |
| --- | --- |
| Renovação da política | Documento com setas de renovação |
| Processo de reclamações | Área de transferência com marca de seleção |
| Venda cruzada | Documentos de política conectados |

### Mídia e entretenimento
| Caso de uso | Metáfora visual |
| --- | --- |
| Novo conteúdo | Botão Reproduzir ou destaque |
| Recomendações de conteúdo | Conteúdo com curadoria de lista de reprodução ou estrelado |
| Churn de assinatura | Cartão de assinatura corrompido |

### Telecomunicações
| Caso de uso | Metáfora visual |
| --- | --- |
| Otimização do plano | Barras de sinal com engrenagem |
| Atualização do dispositivo | Telefone com seta para cima |
| Prevenção de churn | Blindagem com sinal |

## Modelo de prompt de geração de imagem

Use esse modelo como ponto de partida, personalizando o assunto e os detalhes de cada caso de uso:

```
A clean, modern icon illustration of {visual metaphor} representing {use case concept}. Professional corporate design style with bold shapes and clean lines. Single centered subject on a {solid/gradient} background. High contrast, vibrant but refined color palette. No text, no fine details, no complex backgrounds. The icon must be clearly recognizable when scaled down to 40 pixels. Square format, 1024x1024 pixels.
```

### Dicas de Personalização de Prompt

- **Seja específico sobre o assunto** — &quot;Um carrinho de compras vermelho brilhante com duas caixas de presente coloridas no interior&quot; é melhor do que &quot;um carrinho de compras&quot;
- **Especificar tratamento de plano de fundo** — &quot;em um plano de fundo de gradiente azul suave&quot; ou &quot;em um plano de fundo branco limpo com sombra sutil&quot;
- **Mencione a iluminação** — a &quot;iluminação suave de estúdio&quot; ou o &quot;brilho suave de ambiente&quot; ajudam a obter consistência
- **Adicionar modificadores de estilo** — &quot;minimalista&quot;, &quot;geométrico&quot;, &quot;isométrico&quot; ou &quot;design plano&quot; para orientar a estética
- **Incluir prompts negativos, se suportado** — &quot;sem texto, sem marcas d&#39;água, sem bordas, sem elementos fotorrealistas&quot;

## Ícone de inventário existente

### Por setor

**Varejo (9 ícones):**
ícone-carrinho abandonado, ícone-inventário-urgência, ícone-preço-soltar, ícone-produto-recomendações, ícone-categoria-páginas, ícone-série-de-boas-vindas, ícone-reposição, ícone-pós-compra, ícone-venda-adicional

**Automotivo (12 ícones):**
icon-service-reminders, icon-recall-notifications, icon-test-drive, icon-model-launch, icon-trade-in, icon-parts-Accessing, icon-warranty, icon-connected-car, icon-crupier-network, icon-vehicle-purchase, financiamento de ícones, ícone-proprietário-fidelidade

**Serviços Financeiros (6 ícones):**
icon-lead-nurturing, icon-account-dashboard, icon-product-recommendation, icon-churn-prevention, icon-life-stage

**Assistência médica (4 ícones):**
ícone-compromisso-lembrete, ícone-pós-visita, ícone-cuidado preventivo, ícone-medicação-adesão

**Seguro (3 ícones):**
ícone-renovação-política, ícone-processo-reivindicações, ícone-venda-cruzada

**Mídia e entretenimento (3 ícones):**
icon-new-content, icon-content-recommendations, icon-churn

**Telecomunicações (3 ícones):**
icon-plan-otimization, icon-device-upgrade, icon-churn-prevention

**Viagem e hospitalidade (12 ícones):**
ícone-carrinho-abandono, ícone-reserva-lembretes, ícone-campanhas-sazonais, ícone-página-inicial personalizada, ícone-alto-propósito, ícone-pós-reserva-venda, ícone-ganho-volta, ícone-itinerário-dinâmico, ícone-navegado recentemente, ícone-grupo-reserva, ícone-intenção-saída-intenção, ícone-programa-fidelidade

**B2B (11 ícones):**
icon-webinar-demo, icon-abm, icon-lead-scoring, icon-content-personalization, icon-event-registration, icon-trial-conversion, icon-customer-onboarding, icon-competition-replacement, ícone de estudo de caso, ícone de renovação de contrato, icon-venda-expansão
