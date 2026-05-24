---
source-git-commit: e79d9d6490e4f50c4611dd879b53f0e63a90cd65
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---
# Medidas de proteção de escopo: página de arquitetura versus página de padrão de caso de uso

O site de blueprints separa **páginas de diagrama de arquitetura** de **páginas de padrão de caso de uso** porque atendem a diferentes necessidades de leitores. Este documento define o que pertence a onde e como lidar com o conteúdo que ultrapassa o limite.

## A principal distinção

- **Páginas de diagrama de arquitetura** são referências visuais de nível superior. Eles respondem: *&quot;Como esses sistemas se encaixam? Onde estão os pontos de integração? Qual é a forma do fluxo de dados?&quot;* Os leitores vêm aqui para se orientar.
- **Páginas de padrão de caso de uso** são guias de implementação. Eles respondem: *&quot;Como crio esse recurso? Quais funções estão envolvidas? Quais KPIs avaliam o sucesso? Quais são minhas opções de implementação?&quot;* Os leitores vêm aqui quando têm um caso de uso e precisam enviá-lo.

## Pertence a uma página de arquitetura

| Categoria | Exemplos |
| --- | --- |
| Arquitetura de alto nível | Diagramas de visão geral do AEP e dos aplicativos, Experience Cloud marketecture, hub versus topologia de borda |
| Fluxo de dados do sistema | Caminhos de assimilação em tempo real vs. em lote, sincronização de perfil entre hub e borda, fluxos de pesquisa vs. ativação |
| Pontos de integração | Onde o AEP se integra ao AJO, CJA, Target, Campaign, Marketo, Workfront; limites do SDK; superfícies da API |
| Topologia de implantação | Web SDK versus implantação de SDK móvel, encaminhamento pelo lado do servidor, posicionamento do nó de borda |
| Arquitetura do aplicativo | Como um único aplicativo (AJO, CJA, RTCDP) é estruturado internamente em nível de sistema |
| Indicadores para padrões de caso de uso | &quot;Esta arquitetura aceita os padrões X, Y, Z&quot; com links — a página de arquitetura **não** duplica esse conteúdo |

## NÃO pertence a uma página de arquitetura

Se você estiver escrevendo qualquer um dos itens a seguir, redirecione para uma página de padrão de caso de uso (use a habilidade `use-case-pattern-builder`):

| Categoria | Por que ele pertence a outro lugar |
| --- | --- |
| KPIs e fórmulas de medição | Os padrões de caso de uso avaliam os resultados; as páginas de arquitetura não |
| Objetivos de negócios, impacto nos negócios | O conteúdo do KBO está em `/help/blueprints/business-objectives/`; os padrões fazem referência a ele |
| Exemplos de caso de uso tático | &quot;Lembrete de abandono do carrinho&quot;, &quot;Herói da página inicial personalizada&quot; etc. — estes são conteúdos padrão |
| Recursos (`A > B > C > D`) | A construção de recursos faz parte do modelo padrão de caso de uso |
| Narrativas pessoais | &quot;Maria, a comerciante quer...&quot; cenários de estilo pertencem a padrões, não a referências de arquitetura |
| Opções de implementação | A orientação de implementação de várias opções (Melhor para, Como funciona, Vantagens, Limitações) é uma construção de padrão |
| Tabelas de funções básicas/de suporte | Estas são seções de página padrão |
| Listas de verificação de pré-requisito por caso de uso | Os padrões rastreiam isso; as páginas de arquitetura vinculam-se aos padrões |

## Frases de acionamento a serem observadas

Se o usuário fornecer qualquer uma dessas frases ao descrever a nova página, pause e verifique novamente o escopo:

- &quot;KPIs&quot;
- &quot;impacto nos negócios&quot; / &quot;resultados dos negócios&quot;
- &quot;casos de uso tático&quot; / &quot;exemplos de cenários&quot;
- &quot;recursos&quot;
- &quot;opções de implementação&quot;
- &quot;melhor para&quot;
- &quot;vantagens e limitações&quot;
- &quot;pré-requisitos&quot;
- &quot;personas&quot; / &quot;participantes&quot;
- &quot;medição&quot;

Eles não desqualificam a página automaticamente, mas sinalizam que o usuário pode querer uma página padrão de caso de uso, não uma página de arquitetura. Confirme a intenção antes de gerar.

## O que fazer quando o conteúdo se desvia

1. **Identificar o desvio.** Aponte para a seção específica ou o marcador que cruzou o limite.
2. **Oferecer duas opções ao usuário:**
   - Cortar a seção da página de arquitetura (mais comum — mantém o foco na página de arquitetura).
   - Pare e alterne para `use-case-pattern-builder` para esse conteúdo (quando o usuário realmente desejar uma página padrão).
3. **Aguardar confirmação.** Não reescreva ou elimine silenciosamente o conteúdo.
4. **Se estiver mantendo somente conteúdo de arquitetura**, substitua o conteúdo profundo por um único marcador em `## Use case patterns supported`, vinculado ao padrão relevante (existente ou a ser criado).

## Casos do Edge

- **A página tem meia arquitetura e meio padrão.** Dividir em duas páginas — uma página de arquitetura (esta habilidade), uma página de padrão de caso de uso (a habilidade `use-case-pattern-builder`). Vincule-os.
- A página **Arquitetura descreve um único caso de uso de ponta a ponta.** Esse é um padrão de caso de uso, não uma página de arquitetura. Redirecionar para `use-case-pattern-builder`.
- **A página Arquitetura precisa mostrar fluxos de dados de exemplo para um cenário específico.** Aceitável se o cenário for apenas ilustrativo e a maior parte da página permanecer no nível da arquitetura do sistema. Mantenha o exemplo em um parágrafo e vincule ao padrão relevante para obter detalhes completos.

## Teste rápido

Antes de gerar, pergunte: *&quot;Se um leitor chegar a esta página esperando uma referência de arquitetura de nível superior, ele obterá uma — ou obterá uma apresentação de caso de uso meio concluída?&quot;* No último caso, a página pertence a `use-case-pattern-builder`.
