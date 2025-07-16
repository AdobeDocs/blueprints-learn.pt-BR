---
title: Jornadas B2B usando o blueprint de dados do Marketo
description: Blueprint para implantação rápida do Journey Optimizer B2B edition usando dados do Marketo Engage.
solution: Journey Optimizer B2B Edition
source-git-commit: 29ac41aa5d1d33b63c094ef56b03af73b88f96af
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 3%

---

# Jornadas B2B usando o blueprint de dados do Marketo

Este guia abrangente descreve o processo de integração do Marketo Engage com o Adobe Journey Optimizer B2B edition. Ele aborda a configuração de esquema personalizado, a assimilação de perfis e contas e a orquestração de jornadas personalizadas para grupos de compra. Usando dados do Marketo Engage, esse blueprint garante direcionamento e engajamento precisos em vários canais, gerando demanda mais qualificada e aprimorando as experiências do cliente.

## Casos de uso

* **Criar e Gerenciar Grupos de Compras**: use a IA gerativa para reunir e gerenciar grupos de compras nas contas de destino, garantindo uma cobertura abrangente das principais partes interessadas
* **Automatizar Atribuição de Membros**: atribua membros automaticamente a funções de grupos de compras com base em critérios definidos, como consumo de conteúdo e dados de CRM
* **Jornadas personalizadas**: crie e visualize jornadas de várias etapas personalizadas para cada grupo de compras e membro com base em sua função, conta, interesse no produto e estágio do ciclo de vida
* **Automação em tempo real**: automatize a progressão de contas e grupos de compras por meio de jornadas com acionadores de engajamento em tempo real e pontuação de qualificação
* **Cross-Channel Engagement**: envolva grupos de compra em vários canais, incluindo email, SMS, anúncios, bate-papo, eventos e webinários, para simplificar a geração de demanda e a qualificação
* **Insights orientados por IA**: use insights orientados por IA para otimizar a entrega de conteúdo e as estratégias de envolvimento para compradores individuais e grupos de compras inteiros
* **Ativação de Dados Unificados**: ative as listas de contas unificadas da Adobe Real-Time Customer Data Platform para fornecer os dados mais recentes e completos para a criação e o gerenciamento de grupos de compras
* **Collaboration aprimorado**: coordene os esforços de marketing e vendas para criar oportunidades de vendas mais precisas e acelerar a criação de pipelines

## Aplicativos

* Journey Optimizer edição B2B
* Edição B2B da Real-time Customer Data Platform
* Marketo Engage

## Padrões de integração

| Integração | Descrição |
| :-- | :--- |
| [Conector do Marketo Engage](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) | O Adobe Experience Platform facilita a assimilação de dados do Marketo, fornecendo recursos para estruturar, rotular e aprimorar os dados usando seus serviços. |
| [Journey Optimizer B2B edition - Ação do Marketo Engage](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/account-journeys/journey-nodes/action-nodes#marketo-engage-actions) | Sincronize o Account-Based Marketing no Journey Optimizer B2B edition com esforços baseados em clientes potenciais no Marketo Engage usando ações baseadas em pessoas para gerenciar associações de lista, partições de pessoas e campanhas de solicitação. |
| [Journey Optimizer B2B edition - Ativos da Marketo Engage](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/content-management/assets/marketo-engage-dam/marketo-engage-design-studio) | O Marketo Engage Design Studio é a fonte de ativos padrão do Journey Optimizer B2B edition, permitindo um fácil gerenciamento de ativos para jornadas de conta. |

## Arquitetura

![Arquitetura de solução para AJO B2B somente com dados do Marketo](./assets/ajo-b2b-marketo-only.png){zoomable="yes"}

## Medidas de proteção

* Limite de 50 segmentos de conta por sandbox.
* Avaliação da segmentação em lote.
   * Avaliado automaticamente a cada 24 horas após a conclusão da execução do público-alvo em lote e dos trabalhos de exportação de perfil.
   * Não há suporte para edge, streaming ou avaliação ad-hoc.
* Os atributos da conta estão disponíveis para exportação.
* Eventos de pessoas.
   * Até 30 dias de retrospectiva de evento, sem ordem de predicados de evento.
   * AND / OR é compatível (portanto, você pode dizer &quot;A e B precisam acontecer&quot;,  mas você não pode dizer &quot;A deve acontecer 3 dias antes de B&quot;).
* Máximo de 5 milhões de contas em todas as jornadas de conta
* Um máximo de 40 milhões de pessoas em todas as jornadas da conta
* Máximo de 1.000 pessoas por conta em um grupo de compra e jornada
* [Medidas de proteção de perfil e de segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/guardrails)

## Etapas de implementação

* Instale esquemas B2B e namespaces usando uma das opções abaixo
   * Usando a [coleção do Postman](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility)
   * Usando [modelos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/ui-tutorials/templates) na interface do usuário da plataforma
* Criar um dicionário de dados que define o mapeamento entre os campos do Marketo e o esquema XDM da Experience Platform
   * Use os [Metadados do objeto Marketo](https://experienceleague.adobe.com/pt-br/docs/marketo/using/product-docs/administration/field-management/export-all-object-metadata) como ponto de partida
   * [Personalize o esquema XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/ui/fields/overview) para incluir seus campos personalizados
   * Revise os [campos XDM](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/accounts/field-mapping) padrão compatíveis com o Journey Optimizer B2B edition. Se precisar de campos adicionais, abra um tíquete de suporte para configurá-los
      * **workEmail.address** é necessário no conjunto de dados Pessoa
      * **accountName** é necessário no conjunto de dados Conta
   * Adicione uma nova coluna de campo XDM à planilha de metadados do Marketo exportada para registrar o mapeamento pretendido
* Configurar o [conector de origem do Marketo Engage](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
   * Use o dicionário de dados definido acima para definir o [Mapeamento de importação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-prep/ui/mapping#import-mapping) para o conector de origem
   * A recomendação é não habilitar o perfil antes de considerar as [Considerações de implementação](#implementation-considerations)
   * Recomendação para assimilar Pessoas, Empresas, Oportunidades e Atividades no mínimo, pois esses objetos são os mais úteis ao criar públicos da Conta
* Implementar [Regras de Vinculação do Gráfico de Identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/identity-graph-linking-rules/overview) para Pessoas:
   * Defina como os registros de Pessoa são vinculados usando namespaces de identidade (por exemplo, email, b2b_person).
   * Configure namespaces de identidade e regras de identificação na AEP.
   * Validar o vínculo usando dados de Pessoa de amostra e ferramentas de visualização.
* Habilitar os conjuntos de dados de Pessoa, Empresas, Oportunidades e Atividades para [perfil](https://experienceleague.adobe.com/pt-br/docs/experience-platform/catalog/datasets/user-guide#enable-profile)
* Defina seu primeiro [Público-alvo da conta](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/accounts/account-audience-overview)
* Defina [grupos de compras](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/accounts/buying-groups/buying-groups-overview) ou uma [jornada de conta](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/account-journeys/journey-overview) usando o Público-alvo da conta
   * O trabalho do grupo de compras é executado diariamente, processando novas contas qualificadas como Público-alvo da conta ou pessoas recentemente associadas
   * A manutenção do grupo de compras é executada todas as sextas-feiras à meia-noite da TC, portanto, a remoção de membros ou a adição de membros recém-qualificados ocorre somente às sextas-feiras

## Configuração recomendada

Para simplificar a implementação e garantir a compatibilidade com o Adobe Journey Optimizer B2B edition, a seguinte configuração é recomendada:

* **Usar os campos de identidade padrão:**
   * O _email_ e a _b2b_person_ devem ser retidos como campos de identidade no esquema de Pessoa para oferecer suporte à identificação de identidade e à ativação de público-alvo.
* **Usar os mapeamentos padrão para o Marketo Source Connector:**
   * Aproveite os mapeamentos de campo prontos para uso fornecidos pela Adobe para simplificar a assimilação de dados e reduzir a sobrecarga de configuração.
* **Usar mapeamentos padrão para AJO B2B:**
   * Adote os [mapeamentos de campo padrão](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/accounts/field-mapping) do Journey Optimizer B2B edition para garantir a compatibilidade com a lógica de grupo de compra e a orquestração de jornadas.
* **Bloquear atualizações de campo em todos os campos, exceto email:**
   * No Marketo Engage, configure o gerenciamento de campos para [bloquear atualizações](https://experienceleague.adobe.com/pt-br/docs/marketo/using/product-docs/administration/field-management/block-updates-to-a-field) do Adobe Experience Platform para todos os campos, exceto _email_. Isso ajuda a manter a integridade dos dados e, ao mesmo tempo, permite a resolução de identidades.
* **Implementar regras de vinculação de identidade usando o email como um namespace de identidade exclusivo**
   * Configure [regras de vinculação de gráficos de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/identity-graph-linking-rules/overview) no Adobe Experience Platform para usar _email_ explicitamente como um namespace de identidade exclusivo. Essas regras garantem que os perfis sejam compilados com precisão nas fontes de dados em que o _email_ está presente, permitindo uma resolução de identidade robusta. Seguindo as práticas recomendadas do Adobe, defina regras de vinculação que priorizam o email como um identificador estável e globalmente exclusivo para manter um gráfico de identidade consistente e compatível com a privacidade.
Essa configuração fornece um equilíbrio entre a facilidade de implantação e o controle de dados, garantindo uma base confiável para a orquestração de jornadas B2B.

## Considerações de implantação

Ao implementar o Adobe Journey Optimizer B2B edition, é crucial entender os recursos de identificação fornecidos pela Real-time Customer Data Platform. Essa plataforma realiza a identificação de identidades nos níveis de pessoa e conta, garantindo uma visualização unificada dos dados do cliente.

### Pontos principais

* **Identificação de identidade**: a plataforma compila identidades usando identificadores padrão, como Marketo ID, CRM ID e email. Isso ajuda a criar um perfil abrangente mesclando dados de diferentes fontes.
* **Riscos potenciais**: usar o email como um identificador para compilação pode levar ao colapso não intencional da identidade. Isso significa que indivíduos diferentes que compartilham o mesmo endereço de email podem ser mesclados incorretamente em um único perfil. Esse colapso de identidade pode afetar negativamente a precisão dos dados do CRM e comprometer sua integridade.
* **Estratégia de mesclagem**: a CDP B2B emprega uma estratégia de mesclagem baseada em tempo, na qual é usada a lastUpdatedDate mais recente para um determinado atributo de perfil. Essa estratégia garante que os dados mais recentes sejam refletidos no perfil.
* **Considerações para email**: é essencial avaliar totalmente o uso do email como um identificador para mesclar fragmentos de perfil. Embora possa ser benéfico, o risco de colapso da identidade deve ser cuidadosamente considerado em relação às vantagens. Uma desvantagem é que, sem o email como um identificador, a associação de público externo criada pelo AJO B2B não se integra ao perfil existente.
* **Integração de pessoas do Marketo**: o AJO B2B usa a pessoa do Marketo com a ID de cliente potencial mais baixa quando vários registros do Marketo são mesclados em um único perfil.

Tendo esses pontos em mente, você pode tomar decisões informadas sobre como configurar a identificação de identidade no Adobe Journey Optimizer B2B edition, garantindo perfis de clientes precisos e confiáveis.

### Avaliação dos resultados da compilação de identidades

O Serviço de consulta pode ser usado para ver o impacto da identificação em um conjunto de dados que não tenha perfil ativado. A consulta a seguir pode ser usada para fazer a avaliação

#### Número de registros assimilados

Esta consulta retorna o número total de registros assimilados no conjunto de dados do perfil de pessoa

```sql
select
    count(distinct b2b.personKey.sourceKey)
from
    marketo_person_ajo_b2b
```

#### Emails duplicados

Esta consulta retorna o número de registros de pessoas que serão mesclados como parte da compilação de identidade da plataforma

```sql
select
    SUM(personCount)
from
    (
        select
            emailAddress,
            count(*) as personCount
        from
            (
                select
                    MAX(workemail.address) as emailAddress
                from
                    marketo_person_ajo_b2b
                where
                    workemail.address IS NOT NULL
                group by
                    b2b.personKey.sourceKey
            )
        group by
            emailAddress
        having
            count(*) > 1
    )
```

#### Endereços de email com registros duplicados

Essa consulta retorna os emails com os registros mais duplicados no conjunto de dados.  Essa lista pode ser usada para verificar alguns desses registros para entender melhor como a vinculação de identidades pode afetar o Marketo e o CRM.  Consulte a [visão geral do Serviço de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/home) para obter mais detalhes sobre como funciona a vinculação de identidades.

```sql
select
    *
from
    (
        select
            emailAddress,
            MAX(personId) as personId,
            count(*) as personCount
        from
            (
                select
                    b2b.personKey.sourceKey,
                    MAX(workemail.address) as emailAddress,
                    MAX(b2b.personKey.sourceId) as personId
                from
                    marketo_person_ajo_b2b
                where
                    workemail.address IS NOT NULL
                group by
                    b2b.personKey.sourceKey
            )
        group by
            emailAddress
        having
            count(*) > 1
    )
order by
    personCount desc
```

### Opções

#### Remover email como identidade

Após a análise, se você determinar que o email não é um campo válido para ser usado como um campo de identidade, o esquema Pessoa poderá ser modificado para [remover email como um campo de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/ui/fields/identity)

#### Bloquear atualizações do Adobe Experience Platform

Se manter o email como um campo de identidade for melhor para seus casos de uso, há a opção de [bloquear atualizações de campo](https://experienceleague.adobe.com/pt-br/docs/marketo/using/product-docs/administration/field-management/block-updates-to-a-field) provenientes do AJO B2B e permitir que o AJO B2B seja executado principalmente em dados do Marketo.

## Documentação relacionada

* [Edição B2B da Real-time Customer Data Platform](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview)
* [Introdução ao Real-time Customer Data Platform B2B edition](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial)
* [Medidas de proteção do Real-time Customer Data Platform B2B edition](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails)
* [Adobe Experience Platform](https://experienceleague.adobe.com/pt-br/docs/experience-platform)
* [Serviço de identidade da Adobe Experience Platform](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/home)
* [Marketo Engage](https://experienceleague.adobe.com/pt-br/docs/marketo/using/home)
* [Adobe Experience Platform – Conector de origem do Marketo](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
* [Documentação do Adobe Journey Optimizer B2B edition](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/guide-overview)
