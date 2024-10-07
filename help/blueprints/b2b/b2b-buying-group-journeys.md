---
title: Blueprint de marketing baseado em grupo e de gerenciamento de Jornadas
description: Saiba como idealizar, projetar e criar uma jornada que qualifique clientes potenciais para um grupo de compra no Adobe Journey Optimizer B2B edition.
solution: Journey Optimizer B2B Edition
source-git-commit: b514d7a639d4d624875552c892ae266fdfe089f3
workflow-type: tm+mt
source-wordcount: '2118'
ht-degree: 0%

---

# Comprar o blueprint de marketing baseado em grupo e de gerenciamento de Jornadas

Atualmente, as equipes de marketing enfrentam muitos desafios para fornecer oportunidades qualificadas às vendas. Um desses desafios é trabalhar com as pessoas certas na organização e geralmente é evidente em esforço e precisão. Com _pontuação de lead_, o grupo é muito restrito e as equipes podem perder as pessoas certas. Com a _pontuação de conta_, é necessário mais esforço para identificar a pessoa certa com uma visão tão ampla de uma conta.

É neste desafio que o conceito de **_grupo de compras_** é apresentado. Um grupo de compra permite que os profissionais de marketing encontrem o grupo certo de pessoas na conta e trabalhem com esses indivíduos através da lente da qualificação dos leads e da identificação de sua função no grupo.

## Como os grupos de compras são usados para qualificar clientes potenciais e contas

Criar e se esforçar para concluir um grupo de compras aumenta a eficácia da atividade de marketing na qualificação de leads para oportunidades de vendas. Os grupos de compra dependem dos leads correspondentes para modelos de função que estão vinculados à intenção da Solução.

Um exemplo de grupo de compras pode ser o _Grupo de Compras de Sementes da Acme Corp_, que tem um interesse de solução de _Sementes Orientadas por IA_.

Os grupos de compra representam um grupo de pessoas na empresa que estão interessadas em uma solução por meio de um propósito de solução. E um grupo de compras pode ser identificado para mais de um interesse de solução e os indivíduos aparecem em mais de um grupo de compras.

Como resultado das capacidades B2B aprimoradas fornecidas pelo Journey Optimizer B2B edition, agora é possível enfrentar esses desafios:

* Falta de campanhas de marketing de _customer-first_.
* Conversão inconsistente do lead qualificado de marketing (MQL) para o lead qualificado de vendas (SQL), exigindo o alinhamento das iniciativas com as vendas para desenvolver o MQL
* Falta de um mecanismo que possa ser vendido para identificar e direcionar contas _competidas_.
* Risco de concentração na receita e no pipeline.

Os seguintes KPIs estão bem alinhados à medição do sucesso de casos de uso:

* **Percepção**: os clientes-alvo estão vendo seus anúncios e eles os direcionam para o seu site em uma taxa maior do que antes?
* **Compromisso**: os clientes-alvo estão acessando seu site e se envolvendo com conteúdo?
* **Tempo**: quanto tempo a equipe de vendas leva para localizar e adicionar contatos de várias ferramentas à oportunidade?
* **Custo**: quanto dinheiro cada lead custa em cada plataforma?

## Marketing baseado em conta

Um caso de uso comum, e o foco neste blueprint, é uma iniciativa de marketing baseada em conta. Este caso de uso explora o ponto em que seu grupo de compras criado é preenchido com um cliente potencial quando ele está associado a uma função e interesse de solução.

Ao conduzir um indivíduo por meio da jornada, você coleta mais informações sobre o cliente potencial (Fluxo de trabalho do grupo de compra), por meio de formulários, Sincronização de CRM e ativação do LinkedIn.

Quando um cliente potencial demonstra claramente o interesse pela solução, isso indica um evento comercial definido por uma perspectiva comercial. Neste ponto, a empresa está confiante de que este cliente potencial está realmente interessado em um produto. No Journey Optimizer B2B edition, o cliente potencial está associado a um grupo de compras para essa solução em um modelo de funções (como influenciadores, tomadores de decisão, campeões e patrocinadores).

Como o diagrama a seguir ilustra, você pode coletar detalhes em formulários ou por meio da ativação do LinkedIn e qualificar um propósito de solução quando ocorrer a interação com um bot de chat.

![jornada do grupo de compras](./assets/buying-group-journey-diagram.svg){zoomable="yes"}

Quando a porcentagem de conclusão do grupo de compra for alta o suficiente, você compartilhará o grupo com a equipe de vendas por meio do SQL ou de uma SOL para converter os clientes potenciais na conta em uma venda concluída.

## Solução focada em conta

O foco da gestão de clientes potenciais B2B está nas contas e em seus clientes potenciais. A camada técnica é configurada para suportar os dados que representam essas características, que é um requisito para a segmentação de conta e o gerenciamento de jornadas bem-sucedidos.

### Requisitos

A solução focada em conta requer os seguintes aplicativos e serviços:

* Adobe Journey Optimizer B2B edition
* Adobe Real-time Customer Data Platform (RTCDP) B2B edition
* Adobe Marketo Engage

>[!NOTE]
>
>O licenciamento do Journey Optimizer B2B edition deve incluir os seguintes itens:
><ul><li>Instância do Journey Optimizer B2B edition conectada ao Experience Platform B2B</li><li>Instância de Marketo Engage que está sincronizada com RTCDP</li></ul>
&gt;<br/>
&gt;Para clientes de Marketo Engage existentes, a conexão com a instância existente é a abordagem recomendada.
&gt;<br/><br/>
&gt;Há extensões adicionais disponíveis para a solução melhorar a riqueza do perfil:
&gt;<ul><li>Fontes adicionais para RTCDP para enriquecer o perfil</li><li>Destino RTCDP para Marketo Engage</li></ul>

A implementação desta solução também requer uma compreensão clara do conceito de _Conta_ e _Grupo de compras_, e como eles amplificam e aceleram sua qualificação de vendas potenciais. Com essa compreensão, você também deve identificar a pontuação desejada da integridade do grupo de compras.

### Arquitetura

![Arquitetura de solução para compra de marketing baseado em grupos e gerenciamento de jornadas](./assets/ajo-b2b-architecture.png){zoomable="yes"}

### Esquema de dados

Com qualquer implementação da automação de marketing orientada por dados, o design de esquemas é crucial para o sucesso da implementação. Antes de projetar seu esquema, revise os [namespaces B2B e esquemas](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo-namespaces) e compreenda o utilitário de geração automática que está disponível para gerar um novo esquema em um novo cenário de implementação.

Os esquemas são enriquecidos especificamente com elementos de dados B2B para oferecer suporte à relação avançada em perfis e incluir a perspectiva da conta por meio do `sourceKey` para vincular eventos e perfis ao esquema da conta. Os esquemas são uma representação dos requisitos organizacionais e dos dados coletados e analisados. Para atender a essas necessidades, os esquemas B2B são flexíveis e são uma extensão dos elementos B2B necessários.

Ao projetar o schema de dados para sua organização, é uma prática recomendada representar e rotular as principais entidades em seu ERD com as entidades de alto nível. (Consulte o primeiro diagrama na [documentação do esquema B2B da RTCDP](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/relationship-b2b)). Esse processo é muito útil para entender os elementos de dados necessários que você precisa definir em cada esquema.

Nesse estágio, os Eventos de experiência ainda não podem influenciar jornadas. Além dos esquemas de Evento de experiência, é recomendável adicionar propriedades à conta que representam decisões importantes com base nas atividades do usuário. Essas propriedades são usadas para elementos de caminho dividido no designer de jornadas.

>[!NOTE]
>
>Atualmente, a única relação com suporte pelo Journey Optimizer B2B edition é a relação direta através do atributo `personComponents[0].sourceAccountKey.sourceKey` na entidade `Person`. A expansão futura está planejada para acomodar o objeto de relação conta-pessoa no esquema B2b.

### conector de origem do Marketo Engage

Para enriquecer os elementos de dados da conta, você pode usar o Marketo Engage e seus dados B2B para enriquecer a visualização de conta do RTCDP e do Journey Optimizer B2B edition. A configuração do Conector Marketo Engage Source e o mapeamento de dados de Marketo Engage para atributos de esquema RTCDP permitem que os dados fluam do Marketo Engage para o RTCDP e, se designados, para o perfil.

Para obter informações detalhadas sobre a configuração do conector e o mapeamento de campo necessário para o esquema, consulte a [documentação do conector Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo).

### Medidas de proteção

As medidas de proteção do Journey Optimizer B2B edition estão detalhadas na [página Descrição do produto](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer-b2b.html).

Medidas de proteção relacionadas à implementação

* Todas as medidas de proteção do Público-alvo B2B estão descritas no [blueprint do Público-alvo B2B e da Ativação de perfil](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails) e foram transpostas diretamente para o sucesso do Journey Optimizer B2B edition.
* Se a ativação for necessária por meio de canais Marketo Engage na jornada da conta ou quando a Sincronização do CRM for usada para enriquecer a conta, as [medidas de proteção relacionadas a Marketo Engage](https://helpx.adobe.com/legal/product-descriptions/adobe-marketo-engage---product-description.html#performance-guardrails) serão relevantes.

Revise a [documentação das Medidas de Proteção da Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/guardrails/overview) para obter detalhes adicionais sobre as Medidas de Proteção da RTCDP.

### Provisão

* Todas as instâncias devem estar na mesma organização IMS.
* Somente uma instância do Journey Optimizer B2B edition pode ser vinculada a uma sandbox Experience Platform.
* É altamente recomendável implementar o [Marketo Source Connector para Real-time Customer Data Platform](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo).

## Implementação

As etapas a seguir fornecem orientação para habilitar grupos de compra em sua instância do Journey Optimizer B2B edition, incluindo a ativação de público-alvo para suportar a expansão de sua base de contas com foco nos modelos de função de grupo de compra ausentes.

### Etapas de pré-requisito

1. Defina o esquema XDM que representará sua visualização de negócios de Contas e Clientes potenciais.

   Como primeira etapa, você define e cria um esquema de experiência projetado para atender às necessidades do caso de uso B2B e abranger as fontes de dados, tanto em lote quanto em tempo real. Esse design deve representar a maneira como a empresa está pensando nas entidades de conta e pessoa e nos casos de uso que você deseja suportar. Para que o esquema seja um esquema B2B, o esquema deve seguir as estruturas disponíveis na [documentação do Esquema B2B RTCDP](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/relationship-b2b).

   Uma prática útil é pegar os nomes das entidades do diagrama e identificá-las no esquema rotulando-as da mesma maneira. Observe que alguns esquemas exigem chaves específicas, como `sourceKey`, para funcionar no B2B da RTCDP. A curto prazo, a relação _Muitos para Muitos_ entre conta e pessoa por meio do Relacionamento Conta-Pessoa não é compatível com o Journey Optimizer B2B. Use os scripts do acelerador para o melhor ponto de partida:

   * Use o [script de criação de esquema B2B RTCDP](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility) para gerar o esquema inicial
   * Adicione campos específicos do caso de uso aos esquemas gerados para concluir o esquema de acordo com a necessidade da organização.

   Nesse estágio, você tem a conexão entre o Marketo Engage e a RTCDP, e a estrutura do esquema para aceitar os dados da conta e da pessoa para preencher os conjuntos de dados dos Segmentos da conta está definida. A próxima etapa é conectar a RTCDP com o Marketo Engage e o Journey Optimizer B2B edition.

1. Configure o conector Marketo Engage, incluindo o mapeamento de Marketo Engage para a estrutura XDM.

   Com a estrutura XDM e os campos em vigor, prossiga para conectar o Marketo Engage à RTCDP usando o conector, que alimenta os conjuntos de dados com dados do Marketo Engage e do Journey Optimizer B2B. Comece organizando o mapeamento dos campos das classes Marketo Engage para RTCDP. Use as informações na [documentação do conector](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo#field-mapping-from-marketo-engage-to-xdm) para identificar os campos que você deseja incluir da implementação do Marketo Engage.

### Configuração do grupo de compra

1. Crie públicos-alvo de conta no Journey Optimizer B2B edition ou RTCDP.

   Ative a opção Scheduling all audiences na página Customer → Audiences → Browse para ativar os públicos-alvo da conta. (Nos casos em que isso não funciona, é necessário criar um segmento de Perfil do cliente para permitir a criação de Públicos-alvo de conta.)

   Para criar um segmento, siga as etapas da [documentação de públicos-alvo da conta](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-audiences/account-audience-overview). O uso do Construtor de segmentos com os campos de dados que você identificou como chave para o Público-alvo da conta seria a atividade principal na definição do Público-alvo.

   Nesse estágio, você sabe que os leads da conta para o foco por meio da RTCDP e para o uso dos blocos de construção do grupo de compras.

1. Defina o modelo de funções.

   Em cada grupo de compras, identifique as funções que representam a função que os indivíduos desempenham no grupo que você deseja endereçar. Por exemplo, você pode usar o _tomador de decisão_, _influenciador_ e _campeão_. Defina também o peso e as condições dessa função no grupo de compras.

   A [documentação dos modelos de funções](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-role-templates) descreve esse processo e como definir condições especiais.

1. Defina o interesse da solução.

   Um interesse de solução é uma maneira de indicar o foco dos grupos de compra para suas atividades e estratégia de marketing.

   Para definir um interesse de solução, siga as etapas da [documentação sobre interesses de solução](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/solution-interests). Lembre-se de que você o usa para corresponder o grupo de compras a uma iniciativa de vendas na organização.

1. Configurar o grupo de compras.

   Com os blocos de construção do grupo de compras prontos, configure o grupo de compras para o interesse da solução e o público-alvo da conta com um público-alvo para concluir o modelo de funções com os membros certos da conta. Com essa configuração, atribua um interesse de solução ao modelo de funções identificado e atribua a cada função um peso no sucesso de vendas desse produto específico.

   Para criar o grupo de compras, siga as etapas da [documentação sobre grupos de compras](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-create).

   Neste estágio, você está pronto para [criar uma jornada](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-overview#get-started-with-a-journey) e começar a trabalhar com o Público da Conta para criar o grupo de compras e qualificá-lo para os interesses da solução.

### Ativação de público

Aumente a integridade do grupo de compras por meio da ativação de público-alvo.

1. Defina um Público-alvo da conta correspondente do anúncio do LinkedIn.

   Além das atividades de preenchimento de email e formulário, o Journey Optimizer B2B edition oferece um recurso de anúncio do LinkedIn para aumentar a abrangência de sua conta e apoiar o esforço para concluir um grupo de compras por meio da expansão da extensão de leads de conta e do aumento do alcance de suas atividades de marketing.

   Para usar a mídia paga da LinkedIn para se comunicar com contas em que os grupos de compra não estão suficientemente concluídos ou envolvidos, expanda ou interaja com o Público-alvo da conta, use o [recurso Públicos-alvo correspondentes da conta da LinkedIn](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-audiences/linkedin-account-matched-audiences) para gerar públicos-alvo de anúncio da LinkedIn por meio de Públicos-alvo correspondentes da conta.

1. Ativar o público-alvo para grupos de compra.

>[!TIP]
>
>Algumas dicas para campanhas bem-sucedidas:
>
>* Uma campanha deve ter filtros de função para ajustar grupos de compra com funções ausentes para aumentar o ROI.
>* Para capturar clientes potenciais, direcione clientes potenciais para preencher formulários (formulários LinkedIn ou Marketo Engage) e redirecione os erros de formulário.
