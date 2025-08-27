---
title: '[!DNL Journey Optimizer] - Blueprint do Jornada'
description: Execute mensagens e experiências acionadas usando a Adobe Experience Platform como um hub central para dados de transmissão, perfis de clientes e segmentação.
solution: Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: 0a3ebcbc6029df46bd988cb8f15ecf838f80c3c9
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 15%

---

# [!DNL Journey Optimizer] Blueprints

O Adobe [!DNL Journey Optimizer] é um aplicativo nativo em nuvem criado na Adobe Experience Platform que permite a orquestração agendada e em tempo real de jornadas de clientes em vários canais. Ele é compatível com acionadores orientados por eventos, segmentação de público e serviços de decisão para fornecer experiências personalizadas por email, SMS, push, Web e mensagens no aplicativo. Ele se integra a sistemas de entrada e saída, permitindo o gerenciamento unificado do estado do público-alvo e o engajamento contextual em todo o ciclo de vida do cliente.

Este blueprint descreve os recursos técnicos do aplicativo e fornece um aprofundamento sobre os vários componentes de arquitetura que compõem o [!DNL Journey Optimizer].

<br>

## Casos de uso

>[!BEGINTABS]
>[!TAB Jornada Casos De Uso (Controlado Por Eventos, Em Tempo Real)]

- **Recuperação de abandono:** acione mensagens personalizadas quando um usuário abandonar um carrinho, formulário ou sessão, por email, push ou no aplicativo.
- **Inscrição de novo usuário:** envolva novos usuários imediatamente após eles se registrarem com novas preferências de conta, promoções relevantes ou benefícios
- **Mensagens Transacionais:** envia confirmações, alertas ou atualizações em tempo real (por exemplo, pedido enviado, redefinição de senha) usando disparadores de eventos.
- **Direcionamento contextual:** comunique-se com os usuários no momento com base em seus sinais e localização para ajudar a orientar e direcionar sua experiência
- **Venda adicional/venda cruzada contextual:** forneça ofertas personalizadas com base em atributos de perfil em tempo real e interações recentes.

>[!TAB Casos De Uso Da Orquestração De Campanha (Agendados, Iniciados Por Marca)]

- **Campanhas promocionais**: inicie campanhas multicanais em várias etapas para lançamentos de produtos, ofertas sazonais ou eventos de vendas.
- **Lifecycle Marketing**: automatize campanhas recorrentes, como mensagens de aniversário, lembretes de renovação ou marcos de fidelidade.
- **Envios de funil com base no público-alvo**: segmente e envie públicos-alvo para campanhas estruturadas com base na lógica de negócios ou nos atributos de CRM.
- **Newsletter e Distribuição de Conteúdo**: agende e entregue conteúdo personalizado para públicos-alvo direcionados por email e dispositivos móveis.
- **Campanhas de reengajamento**: identifique usuários dormentes e reintroduza-os em fluxos de engajamento com base em limites de inatividade.

>[!ENDTABS]

<br>

## Arquitetura

<img src="images/ajo-architecture.svg" alt="Blueprint do Adobe Journey Optimizer da arquitetura de referência" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Cenários do blueprint

| Cenário | Descrição |
| :-- | :-- |
| [Jornadas](journey-optimizer-journeys.md) | As Jornadas do AJO no Adobe Journey Optimizer são experiências do cliente automatizadas e personalizadas acionadas por eventos em tempo real ou segmentos de público-alvo, permitindo que os profissionais de marketing entreguem mensagens relevantes em canais como email, SMS e notificações por push. |
| [Orquestração de Campanha](journey-optimizer-campaigns.md) | O AJO Campaign Orchestration permite que os profissionais de marketing projetem e executem campanhas personalizadas entre canais usando dados em tempo real e insights do público-alvo. Ele é compatível com direcionamento dinâmico, entrega de mensagens e lógica de jornada para otimizar a participação do cliente em canais de email, SMS, push e personalizados. | |

<br>

## Padrões de integração

| Integração | Descrição | Considerações técnicas |
| :-- | :-- | :-- |
| [Mensagens de terceiros](3rd-party-messaging.md) | Demonstra como o Adobe [!DNL Journey Optimizer] pode ser integrado a plataformas de mensagens de terceiros para orquestrar e fornecer comunicações personalizadas com o cliente. | <ul><li>O sistema de terceiros deve oferecer suporte à **autenticação de token de portador**</li><li>**Não há suporte para IPs estáticos** devido à arquitetura de vários locatários.</li><li>Esteja ciente dos **limites de taxa da API** em sistemas de terceiros; os clientes podem precisar comprar capacidade adicional para gerenciar o tráfego originado do **Adobe Journey Optimizer**.</li><li>Não há suporte para o **Gerenciamento de Decisão** em cargas de mensagem ou na lógica de entrega.</li></ul> |
| [[!DNL Journey Optimizer] com Adobe Campaign v8](../campaign-v8/ajo-and-campaign-v8.md) | Demonstra como o Adobe [!DNL Journey Optimizer] pode se integrar aos recursos de mensagens transacionais do Adobe Campaign v8 para executar a entrega final de mensagens. | <ul><li>Não há limitação de mensagens. Máximo de 4.000 mensagens a cada 5 minutos.</li><li>Oferece suporte somente a jornadas iniciadas por evento</li><li>A Gestão de decisões não é compatível com mensagens enviadas pelo Campaign</li></ul> |

<br>

## Pré-requisitos

Adobe [!DNL Experience Platform]:

- Esquemas e conjuntos de dados devem ser configurados no sistema antes que você possa configurar as fontes de dados do [!DNL Journey Optimizer]
- Para esquemas baseados em classe de Evento de experiência XDM, adicione o grupo de campos &#39;Orchestration eventID&#39; quando quiser que um evento acionado que não seja um evento baseado em regras
- Para esquemas baseados em classe de Perfil individual XDM, adicione o grupo de campos &quot;Detalhes do teste do perfil&quot; para poder carregar perfis de teste para uso com [!DNL Journey Optimizer]

<br>

Email:

- Deve ter um subdomínio pronto para ser usado no envio de mensagens
- O subdomínio pode ser totalmente delegado à Adobe (recomendado) ou podem ser usados CNAMEs para indicar servidores DNS específicos da Adobe (personalizado)
- É necessário registro TXT do Google para cada subdomínio, para garantir um boa capacidade de entrega

<br>

Push para dispositivo móvel:

- O cliente deve ter um desenvolvedor de publicações de conteúdo para dispositivos móveis disponível para criar o aplicativo
- SDK móvel da Adobe Experience Platform

<br>

## Medidas de proteção

[[!DNL Journey Optimizer] Link de Produto de Medidas de Proteção](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails.html)

[Medidas de Proteção e Orientação de Latência de Ponta a Ponta](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

## Documentação relacionada

- [[!DNL Experience Platform] documentação](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
- [[!DNL Experience Platform] Documentação de tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)
- [[!DNL Experience Platform Mobile SDK] documentação](https://experienceleague.adobe.com/docs/mobile.html)
- [[!DNL Journey Optimizer] documentação](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html)
- [[!DNL Journey Optimizer] descrição do produto](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html)