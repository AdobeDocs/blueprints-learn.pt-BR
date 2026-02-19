---
title: Controlador de mídia paga B2B do AJO
description: Prioridade de campanhas e ativação de contas para destinos de Mídia paga
solution: Journey Optimizer B2B Edition
source-git-commit: dff5608af92fa1140419d6834d8374df75de98d3
workflow-type: tm+mt
source-wordcount: '1392'
ht-degree: 0%

---

# Visão geral

As equipes de marketing que executam mídia paga B2B em escala enfrentam um problema recorrente: **as contas acabam em várias campanhas de uma só vez** (persona, reconhecimento de categoria, liderança em soluções, busca), que dilui as mensagens, causa fadiga do público-alvo e força o trabalho manual de listagem — carregamentos, exclusões e supressão — na Correspondência de Conta do LinkedIn (Destino da Conta). Sem a **priorização em cascata** e a **atribuição automatizada de campanha**, não há um único local para decidir qual conta recebe qual mensagem e as operações não são dimensionadas.

O **Controlador de Mídia Paga** é a solução perfeita para resolver esse problema. Ele usa o **Adobe Journey Optimizer B2B edition (AJO B2B)** e o **Adobe Experience Platform (AEP)** juntos: uma **jornada de conta** lê um público-alvo de conta qualificada do Real-Time CDP, aplica a **lógica de divisão de caminho (cascata)** para atribuir cada conta a exatamente uma camada de campanha e o **ativa cada caminho diretamente** para destinos de mídia paga (**por exemplo, Públicos-alvo correspondentes do LinkedIn**), sem entregas de lista manuais. O resultado é o controle de precisão, menos sobreposição e um padrão repetível para a orquestração de mídia paga B2B multicanal.

## Caso de uso: a história de um profissional de marketing: por que um controlador é importante

*Maya lidera mídia paga para uma marca B2B global. Sua equipe realiza dezenas de campanhas — conscientização básica, intenção de categoria (Jornada, dados, conteúdo), programas liderados por soluções, campanhas pessoais e atividades vitoriosas. Ela tem um problema.*

**O problema:** As mesmas contas aparecem em várias campanhas. Uma conta de Jornada de alta intenção também está em uma lista ampla de conscientização; uma conta de busca ainda recebe anúncios de persona. Os uploads e exclusões de lista são manuais. Toda vez que a equipe de vendas atualiza uma lista de &quot;vitórias obrigatórias&quot; ou uma nova campanha pessoal, sua equipe reexporta públicos, reconcilia sobreposições em planilhas e faz upload novamente para o LinkedIn e outras plataformas. Ele é lento, sujeito a erros e não é dimensionável.

**O que ela deseja:** um local onde cada conta qualificada é avaliada uma vez, atribuída à campanha *mais relevante* usando regras de prioridade claras (cascata) e enviada para o destino de mídia paga correto, automaticamente. Nenhuma entrega de lista manual. Quando dados ou estratégias são alterados, o sistema reavalia e move contas entre campanhas sem que sua equipe entre em contato com listas.

**Resposta da Adobe:** com **o AJO B2B e o AEP trabalhando juntos**, Maya pode executar uma única jornada de **Controlador de mídia pago**: a AEP e o Real-Time CDP mantêm os dados e um público-alvo de &quot;contas qualificadas&quot; mestre; o AJO B2B executa uma jornada de conta que usa a **lógica de divisão de caminho** (cascata) para rotear cada conta para a camada correta — por exemplo, Contratos direcionados → Conduzido por solução → Persona → Consciência de categoria → Consciência de base — e **Ativar para destino** envia cada caminho para a campanha correta do LinkedIn (ou outra). Uma jornada, uma fonte de verdade, nenhuma exportação manual de listas. Este é o padrão do Controlador de mídia paga — e é assim que o Adobe permite a precisão e a escala para mídia paga B2B.

## Por que é importante para as empresas B2B:

As organizações que adotam esse padrão podem eliminar completamente a lógica manual de supressão e exclusão (por exemplo, 100% da resolução de sobreposição tratada na jornada), dimensionar para **dezenas de milhares de contas** por meio de um único controlador e manter uma **única fonte da verdade** para qual conta vai para qual campanha. O sistema **se adapta automaticamente** à medida que o foco da campanha, os públicos-alvo e as metas de vendas mudam, sem reexportar listas ou fazer upload para cada plataforma. Para qualquer empresa B2B que executa várias campanhas de mídia paga, o padrão Controlador de mídia paga fornece a clareza, o controle e a automação que os fluxos de trabalho de lista manual não podem.

Os seguintes KPIs estão bem alinhados à medição de sucesso:

- **Percepção:** as contas de destino estão vendo os anúncios certos e migrando para as campanhas certas a uma taxa mais alta?
- **Envolvimento:** O engajamento e a conversão são melhores quando a sobreposição é removida?
- **Eficiência:** quanto trabalho de lista manual (carregamentos, exclusões, supressão) diminuiu?
- **Custo:** Como o custo por conta ou oportunidade adquirida muda com a orquestração automatizada?

## Orquestração de Jornada de mídia paga

Um caso de uso comum, e o foco deste blueprint, é a **Orquestração de Jornada de mídia paga B2B**: garantir que cada conta qualificada seja atribuída exatamente a um nível de campanha e ativada para o destino de mídia paga correto, sem sobreposição ou transferências manuais.

A jornada do controlador **lê** um público-alvo de conta qualificado (integrado no Real-Time CDP a partir de dados do AEP), **avalia** cada conta através de condições de caminho dividido (cascata), por exemplo, busca → conduzido por solução → persona → intenção de categoria → fundacional, e **ativa** cada caminho para o destino correspondente (por exemplo, LinkedIn Matched Audiences para cada campanha).

**Solução focada em conta:** o foco do Controlador de Mídia Paga é **contas** e sua **atribuição de campanha**. A configuração técnica é compatível com dados e públicos-alvo que representam contas qualificadas e seus atributos (por exemplo, intenção, segmento, persona), necessários para uma segmentação bem-sucedida no nível da conta e uma orquestração baseada em jornadas.

## Requisitos

A solução focada em conta requer os seguintes aplicativos e serviços:

- **Adobe Journey Optimizer B2B edition** — jornadas de conta, lógica de divisão de caminho (cascata), Ativar para destino.
- **Adobe Real-time Customer Data Platform (RTCDP) B2B edition** — Perfis de conta, públicos de conta (por exemplo, contas qualificadas para mídia paga).

## Arquitetura

Fluxo de alto nível:

1. **Dados e públicos-alvo** — o AEP contém perfis e eventos; o Real-Time CDP B2B cria públicos-alvo de conta (por exemplo, &quot;Contas qualificadas de mídia paga&quot;) usados como público-alvo de entrada de jornada.
2. **Orquestração** — jornada de conta B2B da AJO: **Ler público** (contas qualificadas) → **Dividir caminho** (em cascata: por exemplo, Busca → Led por solução → Persona → Categoria → Funcional) → **Ativar para destino** (por caminho para o LinkedIn ou outra mídia paga).
3. **Destinos** — Os canais de mídia paga (por exemplo, Públicos-alvo correspondentes do LinkedIn) recebem ativação no nível da conta de cada caminho de jornada; não há carregamentos de lista manuais.

## Diagrama da arquitetura

<img src="assets/ajo-b2b-paid-media-activation-architecture.svg" alt="Arquitetura do AJO B2B Paid Media Controller" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## Modelagem de dados no AEP B2B

Com qualquer orquestração orientada por dados, o design do esquema é importante. Os perfis de conta e pessoa no AEP/RTCDP devem incluir os atributos usados em **condições de divisão de caminho** (por exemplo, sinalizador de busca, interesse em soluções, persona, categoria de intenção, pontuação de envolvimento). Os esquemas B2B (Conta comercial XDM, Perfil individual XDM, relacional) devem representar sua hierarquia e fontes de dados. Para obter detalhes, consulte a [documentação sobre esquemas B2B do RTCDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview) e a [documentação B2B do AJO](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/home).

**Observação:** a lógica de divisão de caminho na jornada usa dados de perfil e, quando houver suporte, dados relacionais; verifique se os campos necessários para a lógica de cascata estão disponíveis na jornada.

### Medidas de proteção

- **Journey Optimizer B2B edition** — Consulte a [descrição do produto](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer-b2b.html) para obter limites de jornada, limites de nó e suporte de destino.
- **Real-Time CDP** — Consulte [medidas de proteção da RTCDP](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/guardrails/overview) para obter limites de segmentação e ativação.

## Implementação

As etapas a seguir fornecem orientação para implementar o Controlador de mídia paga com o AJO B2B e o AEP.

### Etapas de pré-requisito

1. **Definir públicos-alvo da conta e Modelo de Dados no Real-Time CDP B2B.**

   Crie o **público-alvo qualificado da conta** (por exemplo, &quot;Contas qualificadas de mídia paga&quot;) que entrará na jornada do controlador. Use o Construtor de segmentos e os atributos de conta/pessoa que definem a elegibilidade (por exemplo, geografia, segmento, status de MQA). Esse público-alvo é o ponto de entrada único para a jornada.

2. **Definir hierarquia de campanha e lógica de divisão.**

   Documente a ordem da cascata (por exemplo, Caça → Solução-Led → Pessoa → Categoria → Fundacional) e as condições para cada caminho (quais atributos ou públicos qualificam uma conta). Verifique se as condições são **mutuamente exclusivas em ordem** (de cima para baixo): uma conta deve corresponder no máximo a um caminho, o primeiro que for considerado verdadeiro.

3. **Configurar destinos.**

   Configure destinos de mídia paga (por exemplo, Públicos correspondentes do LinkedIn) no AEP/RTCDP e verifique se eles estão disponíveis para ativação do AJO B2B. Mapeie identificadores de conta e atributos necessários para cada destino.

### Configuração do controlador de mídia paga

1. **Criar a jornada do controlador no AJO B2B.**

   - **Ler público-alvo:** selecione o público-alvo de conta qualificada da Real-Time CDP.
   - **Caminho dividido:** Adicione nós em ordem de cascata. Cada nó avalia as condições (por exemplo, &quot;no público-alvo da busca&quot;, &quot;interesse da solução = X&quot;, &quot;persona = Y&quot;, &quot;categoria de intenção = Z&quot;). Contas que correspondem saem para a ativação correspondente; outras continuam para a próxima divisão.
   - **Ativar para destino:** Para cada caminho, adicione um nó Ativar para destino à campanha/destino do LinkedIn (ou outra) correta.

2. **Validar exclusividade mútua.**

   - Confirme se cada conta insere apenas um caminho (a primeira condição correspondente).
   - Verificar ativação: as contas aparecem no destino certo e são excluídas das campanhas de prioridade mais baixa conforme planejado.

## Diagrama de implementação

<img src="assets/ajo-b2b-paid-media-controller-canvas.svg" alt="Tela do controlador de mídia paga B2B do AJO" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

### 4.2.3. Ativação do público

1. **Ativar para o LinkedIn (e outros destinos).**

   Use &quot;Ativar para destino&quot; na jornada para enviar cada caminho para o público-alvo de mídia paga correto. Nenhuma exportação ou upload de lista manual; a jornada direciona a ativação à medida que as contas fluem pelos caminhos.

2. **Monitorar e ajustar.**

   Use os relatórios do jornada para monitorar volumes por caminho.

## Resumo

O blueprint do **Controlador de mídia paga** mostra como o **AJO B2B e o AEP** trabalham juntos para fornecer aos profissionais de marketing B2B uma maneira única e automatizada de atribuir contas a campanhas e ativar para mídia paga: um público-alvo principal, uma jornada, lógica de divisão em cascata e ativação direta para destinos — sem entregas de lista manuais. Ele estabelece um padrão repetível para a orquestração de mídia paga B2B multicanal e ajuda a reduzir a sobreposição, melhorar a relevância e dimensionar as operações.

## Documentação relacionada

- [Blueprint de Marketing baseado em grupo e de Gerenciamento de Jornadas](https://experienceleague.adobe.com/pt-br/docs/blueprints-learn/architecture/b2b-activation/b2b-buying-group-journeys) — jornadas de conta e grupo de compras no AJO B2B.
- [Adobe Journey Optimizer B2B edition](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b) — Documentação do produto.
- [Real-time Customer Data Platform B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview) — Públicos-alvo e ativação de conta.
