---
name: use-case-icon-generator
description: Gerar especificações de ícones e prompts de geração de imagens para ícones de casos de uso no repositório de blueprints do Adobe Experience Platform. Use essa habilidade ao criar ícones para novos casos de uso do setor, quando a habilidade do construtor de casos de uso do setor precisar de um ícone ou quando o usuário perguntar sobre a criação ou atualização de ícones de casos de uso. Gera um prompt detalhado de geração de imagem que o usuário pode usar com ferramentas do Midjourney, DALL-E, Adobe Firefly ou semelhantes, juntamente com o nome e o posicionamento corretos dos arquivos.
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---


# Gerador de ícone do caso de uso

Gerar especificações detalhadas de ícones e prompts de geração de imagem de IA para ícones de caso de uso no repositório de blueprints.

## Quando usar esta habilidade

- Criar um novo caso de uso que precise de um ícone
- Chamado pela habilidade do construtor de casos de uso do setor para gerar uma especificação de ícone
- O usuário pergunta sobre como criar, atualizar ou substituir um ícone de caso de uso
- O usuário deseja gerar um lote de ícones para um novo negócio vertical

## Etapa 1: Coletar entradas

Obtenha as seguintes informações do usuário ou da habilidade de chamada:

**Obrigatório:**
- **Nome do caso de uso** — O nome legível do caso de uso (por exemplo, &quot;Carrinho Abandonado&quot;, &quot;Pontuação de cliente potencial&quot;)
- **Setor vertical** — Um dos seguintes: automotivo, b2b, serviços financeiros, saúde, seguro, entretenimento de mídia, varejo, telecomunicações, viagem e hospitalidade
- **Breve descrição** — 1-2 frases descrevendo o que o caso de uso faz

**Opcional:**
- **Metáfora visual ou assunto preferencial** — Se o usuário tiver uma ideia específica sobre o que o ícone deve descrever

Se alguma entrada necessária estiver ausente, pergunte ao usuário antes de continuar.

## Etapa 2: ler o guia de estilo

Leia o arquivo `references/icon-style-guide.md` (relativo ao diretório desta habilidade) para carregar o guia de estilo completo, incluindo:

- Especificações técnicas
- Diretrizes de estilo visual
- Exemplos de metáforas visuais por setor
- O modelo de prompt
- O inventário de ícones existente

Use o guia de estilo para garantir a consistência com os ícones existentes.

## Etapa 3: Gerar a especificação do ícone

Produza todas as três partes da especificação do ícone:

### A. Especificação do arquivo

Derive o nome do arquivo e o caminho do nome do caso de uso e do setor:

- **Nome do arquivo:** `icon-{kebab-case-name}.png`
   - Converter o nome do caso de uso em kebab-case (minúsculas, hifens para espaços)
   - Exemplos: &quot;Carrinho abandonado&quot; torna-se `icon-abandoned-cart.png`, &quot;Venda cruzada adicional&quot; torna-se `icon-cross-sell-upsell.png`
- **Caminho:** `/help/blueprints/industry-use-cases/assets/use-case-icons/{industry}/`
- **Dimensões:** 1024 x 1024 pixels
- **Formato:** PNG, RGB de 8 bits ou RGBA
- **Tamanho do arquivo de destino:** 900 KB - 1,4 MB

### B. Prompt de geração de imagem

Crie um prompt detalhado e pronto para cópia para as ferramentas de geração de imagem da IA. O prompt deve:

1. **Descreva uma metáfora visual clara** — Escolha uma única metáfora visual forte que comunique imediatamente o conceito de caso de uso. Se o usuário tiver fornecido uma metáfora preferencial, use-a. Caso contrário, selecione um com base nos exemplos de guia de estilo e na descrição do caso de uso.

2. **Especificar o estilo artístico** — Incluir estas diretivas de estilo:
   - Estilo de ilustração de ícone limpo e moderno
   - Estética de design corporativo profissional
   - Formas em Negrito e linhas limpas
   - Acabamento polido, renderizado (não fotorrealista)
   - Consistente com um sistema de design unificado

3. **Incluir especificações técnicas:**
   - Formato quadrado, 1024x1024 pixels
   - Assunto centralizado único
   - Fundo de gradiente sólido ou sutil
   - Alto contraste entre assunto e plano de fundo

4. **Aplicar legibilidade de tamanho pequeno:**
   - Nenhum texto ou letra de nenhum tipo
   - Sem detalhes finos ou padrões complexos
   - Nenhum plano de fundo complexo ou cenas com vários elementos
   - Silhueta em negrito com leitura nítida em 40px
   - Forte reconhecimento de forma mesmo sem cor

5. **Guia da paleta de cores:**
   - Cores profissionais adequadas para a empresa
   - Vibrante, mas refinado (não neon ou excessivamente saturado)
   - Alto contraste para acessibilidade
   - Coeso com outros ícones na mesma vertical do setor

Estruture o prompt como um único parágrafo, pronto para ser colado em qualquer ferramenta de geração de imagem.

### C. Trecho de referência do catálogo

Gere o trecho do HTML para uso na tabela de catálogo:

```
<img src="assets/use-case-icons/{industry}/icon-{name}.png" alt="{Alt Text}" width="40">
```

Onde `{Alt Text}` é o nome de caso de uso legível.

## Etapa 4: Listar ícones existentes no mesmo setor

Verifique a seção de inventário do ícone existente do guia de estilo e liste todos os ícones atuais do mesmo setor. Isso ajuda o usuário a:
- Garanta consistência visual ao gerar o novo ícone
- Evite duplicar um ícone que já existe
- Referência a ícones existentes como exemplos de estilo

## Etapa 5: apresentar a saída

Formate a saída claramente com estas seções:

&#x200B;---

### Especificação do ícone: &lbrace;Use Case Name&rbrace;

**Setor:** {Industry}

**Detalhes do arquivo:**
- Nome do arquivo: `icon-{kebab-case-name}.png`
- Caminho: `/help/blueprints/industry-use-cases/assets/use-case-icons/{industry}/`
- Dimensões: 1024 x 1024 pixels
- Formato: PNG (RGB/RGBA de 8 bits)

**Prompt de Geração de Imagem:**

> {O prompt completo e detalhado — formatado como uma aspa de bloqueio para que seja fácil copiar}

**Catálogo HTML:**

```html
<img src="assets/use-case-icons/{industry}/icon-{name}.png" alt="{Use Case Name}" width="40">
```

**Ícones Existentes em {Industry}:**
- {list of existing icon names}

**Próximas etapas:**
1. Copie o prompt de geração de imagem acima.
2. Cole-o na ferramenta de geração de imagem de sua preferência (Adobe Firefly, Midjourney, DALL-E ou similar).
3. Gere a imagem e selecione o melhor resultado.
4. Redimensionar/exportar para exatamente 1024x1024 pixels, se necessário.
5. Salve como `{filename}` no caminho mostrado acima.
6. Verifique se o ícone parece limpo e reconhecível no tamanho de exibição de 40px.
7. Use o trecho HTML do catálogo ao adicionar esse caso de uso à tabela do catálogo.

&#x200B;---

## Diretrizes

- **Nunca gerar a imagem real** — Esta habilidade produz somente a especificação e o prompt. O usuário deve usar uma ferramenta de geração de imagem externa.
- **Um ícone por caso de uso** — cada caso de uso recebe exatamente um ícone.
- **Verificar duplicatas** — Se já existir um ícone com o mesmo nome ou um nome muito semelhante no inventário, avise o usuário.
- **Priorizar legibilidade** — Na dúvida entre uma metáfora detalhada e uma simples, escolha sempre a opção mais simples que tenha boa leitura, a 40px.
- **Seja específico em prompts** — prompts vagos produzem resultados inconsistentes. Inclua detalhes visuais concretos (por exemplo, &quot;um carrinho de compras com duas caixas coloridas&quot; em vez de &quot;um conceito de compras&quot;).
- **Evite cliques quando possível** — Tente encontrar metáforas visuais novas, mas imediatamente reconhecíveis. Uma lâmpada para cada caso de uso &quot;inteligente&quot; se torna repetitiva.
