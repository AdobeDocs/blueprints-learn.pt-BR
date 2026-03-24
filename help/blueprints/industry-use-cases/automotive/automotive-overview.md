---
title: Casos de uso automotivo
description: Descubra como as organizações automotivas usam o Adobe Experience Platform para personalizar a jornada de compra do veículo, melhorar a retenção de serviços e criar a fidelidade do proprietário.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: ee83c739-0907-481d-ba3f-358af4e03c67
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '1941'
ht-degree: 4%

---

# Casos de uso automotivo

As organizações automotivas usam o Adobe Experience Platform para unificar os dados dos clientes provenientes de interações com concessionárias, pesquisa online de veículos, registros de serviços e sistemas de carro conectados em uma única visualização de cada proprietário. Essa base permite experiências personalizadas em todo o ciclo de vida da propriedade, desde a pesquisa inicial do veículo até a compra, o serviço e a fidelidade.

## Resumo do caso de uso

| Caso de uso | Descrição | Impacto no negócio | Padrão de implementação |
| --- | --- | --- | --- |
| [Jornada Personalization de Compra de Veículos](#vehicle-purchase-journey-personalization) | Personalize a jornada de compra de veículo da pesquisa para comprar com recomendações de veículo relevantes, opções de financiamento e informações do revendedor. Quando os possíveis compradores recebem orientação personalizada em cada estágio, eles se movimentam pelo funnel de vendas mais rapidamente e com mais confiança. | Melhores taxas de conversão de lead para compra e pipeline de vendas mais robusto | [Jornada entre canais com decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) |
| [Lembretes de Compromissos do Serviço](#service-appointment-reminders) | Envie lembretes de serviço personalizados com base na quilometragem do veículo, no histórico de serviço e nas preferências do cliente. O alcance pró-ativo mantém os veículos mantidos e garante que os clientes retornem à concessionária em vez de buscar fornecedores terceirizados. | Compromisso de serviço aprimorado mostra taxas e maior receita de serviços | [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| [Campanhas com Valor de Troca](#trade-in-value-campaigns) | Ofereça avaliações de valor de troca de forma proativa a clientes que estejam prontos para atualização. Alcançar os proprietários no ponto certo do ciclo de propriedade acelera o caminho para a compra de um novo veículo. | Maior envolvimento comercial e maiores vendas de veículos novos | [Jornada Orquestrada Em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| [Recomendações sobre peças e acessórios](#parts-and-accessories-recommendations) | Recomendar peças, acessórios e atualizações relevantes com base no modelo do veículo, duração da propriedade e preferências do cliente. As recomendações personalizadas de serviços pós-venda geram receita incremental e, ao mesmo tempo, ajudam os proprietários a obter mais de seus veículos. | Melhores taxas de compra de peças e acessórios e maior receita pós-venda | [Recomendação comportamental](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| [Notificações de Cancelamento de Veículo](#vehicle-recall-notifications) | Envie notificações personalizadas de recuperação com opções de agendamento de serviço e informações de segurança. Comunicações de recuperação claras e oportunas protegem a segurança do cliente e demonstram o compromisso da marca com o suporte responsável de propriedade. | Melhores taxas de resposta de recuperação e conformidade de segurança reforçada | [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| [Novas Campanhas de Inicialização de Modelo](#new-model-launch-campaigns) | Direcione clientes que podem estar interessados em novos lançamentos de modelo com base em seu veículo atual, preferências e histórico de compras. O direcionamento focado do público-alvo maximiza o impacto do lançamento e cria um impulso inicial para o pedido. | Melhor envolvimento na campanha de lançamento e maior interesse no novo modelo | [Ativação de mensagem de saída em lote](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md) |
| [Ofertas de Financiamento e Seguro](#financing-and-insurance-offers) | Apresentar ofertas personalizadas de financiamento e seguro com base no perfil de crédito, seleção de veículo e cronograma de compra. Os produtos financeiros personalizados removem as barreiras de compra e ajudam os clientes a se sentirem confiantes em seus termos. | Melhores taxas de aceitação de financiamento e maior receita por venda | [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) |
| [Agendamento da Unidade de Teste](#test-drive-scheduling) | Habilite a programação personalizada do teste com recomendações do revendedor e disponibilidade do veículo. Fazer com que seja fácil para os compradores interessados para chegar ao volante acelera o caminho para a compra. | Taxas de conclusão de test drive aprimoradas e maior conversão de vendas | [Mensagens acionadas por Evento](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| [Programas de Fidelidade do Proprietário](#owner-loyalty-programs) | Coordene comunicações de fidelidade entre canais de carro conectados, digitais de OEM e revendedores, aplicando regras de elegibilidade baseadas em nível para determinar quais proprietários recebem ofertas exclusivas, acesso antecipado ao veículo e recompensas do parceiro. A arbitragem de oferta impede que promoções conflitantes de revendedores e canais OEM cheguem ao mesmo proprietário simultaneamente. | Maior engajamento no programa de fidelidade e mais compras repetidas | [Jornada entre canais com decisão](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) |
| [Garantia e planos de serviços estendidos](#warranty-and-extended-service-plans) | Recomendar planos de garantia e serviço estendido em épocas ideais com base na idade do veículo, quilometragem e padrões de compra. O alcance bem cronometrado captura a receita antes que as garantias da fábrica expirem. | Melhores taxas de adoção de garantia estendida e maior receita de serviços | [Jornada Orquestrada Em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| [Ativação do recurso Connected Car](#connected-car-feature-activation) | Personalize as recomendações de recursos de carro conectado com base nos recursos do veículo e nas preferências de tecnologia. Ajudar os proprietários a descobrir recursos não utilizados aumenta a satisfação e fortalece o relacionamento digital. | Taxas de ativação de recursos aprimoradas e melhor experiência para o cliente | [Jornada Orquestrada Em Várias Etapas](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| [Coordenação da rede do revendedor](#dealer-network-coordination) | Habilite recomendações personalizadas de revendedores com base no local do cliente, preferências e inventário de revendedores. Conectar os clientes com a concessionária certa melhora a experiência de compra e serviço. | Melhores taxas de engajamento do revendedor e maior coordenação de vendas | [Personalization de Aplicativo/Web de Visitante Conhecido](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) |

## Considerações técnicas por caso de uso

### Personalização da jornada de compra de veículo

- Os dados de inventário de veículos dos sistemas de gerenciamento de revendedores devem ser integrados e atualizados com frequência para que as recomendações reflitam a disponibilidade real nas concessionárias próximas.
- O comportamento de pesquisa do cliente em todo o site, incluindo a atividade de configuração do veículo, o uso da ferramenta de comparação e os downloads do folheto, deve ser capturado para identificar com precisão os sinais da intenção de compra.
- Os modelos de pontuação de clientes potenciais devem levar em conta o envolvimento online e os sinais offline, como visitas a concessionárias e consultas por telefone para priorizar os clientes potenciais de maior intenção.
- [!DNL Real-Time Customer Data Platform] perfis devem mesclar sessões anônimas de pesquisa da Web com identidades de clientes conhecidas assim que um cliente potencial se registrar ou visitar uma concessionária.

### Lembretes de compromisso de serviço

- A quilometragem do veículo e os dados telemáticos de sistemas de carro conectados ou registros de serviço do revendedor devem fluir para os perfis do cliente para acionar lembretes nos intervalos de serviço corretos.
- As mensagens de lembrete devem incluir links de agendamento com um clique, que preenchem previamente as informações do veículo do cliente e itens de serviço recomendados para minimizar o atrito da reserva.
- Os registros do histórico de serviço devem ser integrados para evitar a recomendação de serviços que foram concluídos recentemente e para personalizar o lembrete com os itens de manutenção específicos devidos.
- [!DNL Journey Optimizer] tempo de mensagem deve considerar a capacidade do serviço de revendedor e horas de operação para garantir que os clientes possam reservar compromissos quando receberem o lembrete.

### Campanhas de valor de troca

- Os dados de avaliação de veículos de fornecedores terceirizados devem ser integrados e atualizados regularmente para garantir que as estimativas de troca compartilhadas com os clientes sejam precisas e competitivas.
- Os modelos de ciclo de vida de propriedade devem considerar fatores como datas de expiração do leasing, cronogramas de pagamento de empréstimo e duração média da propriedade por segmento de veículo para identificar a janela de alcance ideal.
- As mensagens de campanha devem fazer referência, de forma dinâmica, ao veículo atual do cliente e sugerir opções de atualização específicas que se alinhem às suas preferências e orçamento.
- [!DNL Experience Platform] segmentos devem excluir clientes que compraram um veículo recentemente ou que estão atualmente em uma contestação de serviço ativa para evitar alcance com tempo inadequado.

### Recomendações sobre peças e acessórios

- Os dados do catálogo de produtos devem incluir informações de compatibilidade do veículo para que as recomendações mostrem apenas as peças e os acessórios que se encaixam no ano, na marca e no modelo do veículo específico do cliente.
- Fatores sazonais e regionais devem influenciar as recomendações; acessórios de inverno devem ser promovidos em climas mais frios, enquanto as atualizações de desempenho podem repercutir mais em regiões com comunidades de entusiastas ativos.
- O comportamento de navegação nas páginas de peças e acessórios deve ser capturado e associado aos perfis do cliente para refinar as recomendações com base no interesse expresso.
- A implementação do Web SDK [!DNL Experience Platform] deve capturar os dados do número de identificação do veículo de sessões autenticadas para garantir que a filtragem de compatibilidade seja precisa.

### Notificações de retirada de veículos

- Os registros do número de identificação do veículo devem ser mantidos com precisão nos perfis do cliente para que as notificações de recuperação cheguem a cada proprietário afetado e não cheguem aos clientes não afetados.
- As mensagens de recuperação devem estar em conformidade com os requisitos normativos para conteúdo de notificação de segurança, cronograma e confirmação de entrega em cada mercado aplicável.
- O delivery multicanal (email, mensagem de texto, notificação por push e email físico) deve ser usado para maximizar o alcance, pois as comunicações críticas de segurança exigem maior garantia de delivery do que as mensagens de marketing.
- [!DNL Journey Optimizer] deve rastrear o status de resposta de recuperação em nível individual e encaminhar comunicações de acompanhamento para os proprietários que não agendaram o serviço dentro de um prazo definido.

### Novo modelo de campanhas de lançamento

- Os segmentos de público-alvo das campanhas de lançamento devem considerar o modelo atual de veículo, a duração da propriedade, os sinais de interesse do modelo anterior e a adequação demográfica para identificar as perspectivas de maior propensão.
- O conteúdo do Launch deve ser personalizado para fazer referência ao veículo atual do cliente e destacar melhorias ou recursos específicos que atendam às prováveis prioridades.
- O cronograma da campanha deve ser coordenado com as datas de embargo e os cronogramas de lançamento regionais para garantir que os clientes recebam informações no momento adequado para seus mercados.
- A ativação do público-alvo do [!DNL Real-Time Customer Data Platform] deve sincronizar os segmentos de lançamento com as plataformas de publicidade para obter suporte coordenado a mídia paga e alcançar o alcance de seus próprios canais.

### Ofertas de financiamento e seguro

- As regras de elegibilidade da oferta financeira devem ser cuidadosamente configuradas para cumprir as regulamentações de empréstimo, garantindo que as ofertas apresentadas aos clientes sejam aquelas para as quais eles realmente podem se qualificar.
- A integração de dados de perfis de crédito exige controle de acesso rigoroso e controle seguro, já que as informações financeiras estão sujeitas a requisitos normativos e de privacidade ampliados.
- A apresentação da oferta deve divulgar claramente os termos, as taxas e as condições em conformidade com as regulamentações financeiras do consumidor em cada mercado aplicável.
- As regras de decisão do [!DNL Journey Optimizer] devem considerar o preço do veículo, o pagamento antecipado e as preferências de termos de empréstimo para classificar as ofertas por relevância em vez de simplesmente por taxa.

### Agendamento do drive de teste

- Os sistemas de inventário do revendedor devem ser integrados para confirmar que o modelo e o acabamento do veículo específico em que o cliente está interessado estão disponíveis para o teste de direção na concessionária recomendada.
- As recomendações do revendedor com base no local devem considerar o endereço do cliente, as classificações do revendedor e a disponibilidade do compromisso atual para sugerir a opção mais conveniente.
- As mensagens de confirmação e lembrete da unidade de teste devem incluir instruções, informações de contato do revendedor e o que esperar, reduzindo as taxas de não exibição.
- Os dados comportamentais [!DNL Experience Platform] devem identificar o momento ideal para sugerir um teste dinâmico, evitando alcance prematuro a pesquisadores em fase inicial que ainda não estejam prontos.

### Programas de fidelidade do proprietário

- Os cálculos de nível de fidelidade devem incorporar várias dimensões do envolvimento, incluindo visitas de serviço, compras de peças, indicações e presença no evento, não apenas o histórico de compra de veículos.
- As regras de elegibilidade baseadas em níveis devem ser configuradas na decisão [!DNL Journey Optimizer] para determinar quais proprietários se qualificam para ofertas exclusivas, o acesso antecipado a revelações de veículos novos e os resgates de prêmios de parceiros, garantindo que apenas os membros elegíveis recebam cada categoria de benefício.
- A lógica de arbitragem de oferta deve avaliar as comunicações pendentes dos canais revendedores e OEM antes que qualquer mensagem seja enviada, suprimindo promoções de prioridade mais baixa ou em conflito para evitar que o mesmo proprietário receba ofertas contraditórias simultaneamente.
- A coordenação entre canais deve abranger sistemas CRM de revendedores, propriedades digitais de OEM, canais de notificação de carro conectados e pontos de contato de serviço para que as interações de fidelidade sejam consistentes, independentemente de onde o proprietário interage.
- Os sistemas de atendimento de recompensas em concessionárias e centros de serviços devem ser integrados para que os benefícios de fidelidade possam ser resgatados sem problemas no ponto de serviço.
- As comunicações devem se adaptar com base no estágio do ciclo de vida da propriedade, fornecendo propostas de valor diferentes para novos proprietários em seu primeiro ano em comparação aos proprietários de longo prazo que se aproximam de uma possível atualização.
- A lógica de jornada do [!DNL Journey Optimizer] deve detectar alterações de camada em tempo real e acionar mensagens de parabéns ou reengajamento quando os clientes se moverem entre níveis de fidelidade.

### Garantia e planos de serviços estendidos

- As datas de expiração da garantia e os detalhes da cobertura devem ser rastreados com precisão nos perfis do cliente para acionar o alcance na hora certa, normalmente de 60 a 90 dias antes da expiração.
- A quilometragem e os padrões de utilização dos veículos a partir de dados de veículos conectados ou registros de serviço devem informar as recomendações do plano, já que os motoristas de quilometragem elevada se beneficiam de uma cobertura diferente dos proprietários de quilometragem baixa.
- O conteúdo de comparação do plano deve ser claro e livre de jargões, ajudando os clientes a entender exatamente o que é coberto e o valor relativo aos custos potenciais de reparo imediato.
- [!DNL Real-Time Customer Data Platform] segmentos devem distinguir entre clientes com garantias de fábrica em vencimento, aqueles com planos estendidos existentes que estão se aproximando da renovação e aqueles sem cobertura no momento.

### Ativação de recurso de carro conectado

- Os dados da plataforma do veículo ligado devem ser integrados de modo a identificar quais as características disponíveis em cada veículo e quais as que o proprietário já ativou ou utilizou.
- O rastreamento da adoção de recursos deve capturar os eventos de ativação, a frequência de uso e a profundidade de engajamento para personalizar a sequência e o ritmo das recomendações de recursos.
- Os canais de notificação no veículo devem ser coordenados com as notificações por email e por aplicativo para fornecer prompts de recursos no momento mais relevante contextualmente, como sugerir recursos de navegação quando uma viagem em estrada é detectada.
- Os perfis do [!DNL Experience Platform] devem armazenar dados de configuração de tecnologia do veículo, incluindo pacotes instalados e versões de software, para garantir que as recomendações de recursos sejam compatíveis com o veículo específico do proprietário.

### Coordenação da rede do distribuidor

- Os feeds de inventário do revendedor devem ser integrados e atualizados com frequência para garantir que a disponibilidade do veículo mostrada aos clientes reflita com precisão o que está no lote de cada revendedor.
- A lógica de atribuição de cliente para revendedor deve considerar a proximidade, a especialização do revendedor, as preferências de idioma e qualquer relacionamento de revendedor existente para fornecer a melhor correspondência.
- As regras de roteamento de clientes potenciais devem garantir que, quando um cliente manifestar interesse de compra online, a consulta chegue rapidamente ao negociante apropriado com contexto completo sobre a atividade de pesquisa do cliente.
- A resolução de identidade do [!DNL Experience Platform] deve lidar com cenários em que um cliente interage com várias concessionárias, mantendo um perfil unificado e respeitando a visão de cada revendedor sobre seus próprios relacionamentos com os clientes.
