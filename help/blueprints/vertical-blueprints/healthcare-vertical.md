---
source-git-commit: f7104d114a2644a494003bc78eb20768904f652c
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 1%

---
﻿---
title: Saúde
description: Saiba mais sobre o Healthcare Shield, um complemento Adobe Experience Platform para aplicativos baseados em plataforma, como Real-Time CDP, Customer Journey Analytics e Adobe Journey Optimizer. O complemento torna esses aplicativos qualificados para os requisitos de HIPAA e PHI.
solution: Experience Platform
---
# Escudo da Saúde

O Healthcare Shield é um complemento do Adobe Experience Platform para aplicativos baseados em Adobe Experience Platform, como Real-Time CDP, Customer Journey Analytics e Adobe Journey Optimizer, projetado para preparar esses aplicativos para a HIPAA para atender aos requisitos de processamento e uso de PHI (Protected Health Information, informações de saúde protegidas).

## Perguntas frequentes sobre o Healthcare Shield

As perguntas frequentes a seguir fornecem respostas a perguntas comuns sobre o Healthcare Shield.

### O que é o HIPAA?

HIPAA é a Health Insurance Portability and Accountability Act (HIPAA), um regulamento norte-americano que estabelece proteções importantes para limitar o uso e a divulgação de informações de saúde protegidas (PHI) quando criadas, recebidas, mantidas ou transmitidas por uma entidade coberta pela HIPAA ou por parceiros de negócios (como clientes de Adobe) a um parceiro comercial (parceiros de tecnologia como o Adobe).

O Adobe está preparado para HIPAA como um parceiro comercial em relação às soluções específicas de Adobe prontas para HIPAA e conformidade com as regras de Segurança, Privacidade e Notificação de Violação do HIPAA.

### O que é um Contrato de Associação de Negócios (BAA) e por que ele é importante?

Quando uma Entidade Coberta ou um Business Associate (um cliente de Adobe) usa os serviços de um Business Associate (como o Adobe) para criar, receber, manter ou transmitir determinados tipos de dados do consumidor que sejam Dados Protegidos de Saúde (PHI) ou ePHI (versão eletrônica de PHI), a Entidade Coberta e o Business Associate são solicitados a assinar um Business Associate Agreement (BAA).

O BAA requer, por contrato, o Adobe, já que o Business Associate deve proteger adequadamente a PHI, cumprindo os requisitos das Regras de Privacidade, Segurança e Notificação de Violação do HIPAA.

Com o complemento Healthcare Shield para Real-Time CDP, o Adobe agora pode executar um BAA com clientes que licenciam esse recurso junto com o Adobe Real-Time CDP B2C e os fluxos de consumidores do Adobe Real-Time CDP B2P Edition.

### Por que o Healthcare Shield for Real-Time CDP (e os futuros aplicativos baseados em plataforma) está disponível somente nos EUA?

Como a HIPAA é uma lei norte-americana, estamos limitando a disponibilidade do Healthcare Shield para os EUA e para empresas sujeitas à HIPAA. A Adobe pretende expandir a cobertura para outras jurisdições, já que estamos dentro dos requisitos locais e estamos confiantes de que podemos alcançá-las.

### O que é o Healthcare Shield for Real-Time CDP?

O Healthcare Shield for Real-Time CDP destina-se aos clientes que são uma entidade coberta ou um Business Associate e pretendem utilizar a PHI na Real-Time CDP para a assimilação de dados, criação de públicos-alvo e ativação entre canais, bem como exigir que o Adobe execute um BAA. O Healthcare Shield é necessário para entidades cobertas com HIPAA e casos de uso necessários para a CDP em tempo real.

### Por que as perspectivas de saúde da Real-Time CDP devem comprar o Healthcare Shield?

Como complemento do Real-Time CDP, o Healthcare Shield atualiza o aplicativo para um status &quot;preparado para HIPAA&quot;. Isso significa que o aplicativo tem as salvaguardas para alavancar a PHI de acordo com os requisitos da HIPAA. Além disso, com o Healthcare Shield, o Adobe está disposto e capaz de autorizar o cliente a trazer certos tipos de dados pessoais confidenciais permitidos para o aplicativo pronto para HIPAA. O Adobe assinará os Business Associate Agreements (BAAs) com os clientes que licenciam o Healthcare Shield para um aplicativo compatível baseado na plataforma.

### Que tipos de dados estão autorizados para o Real-Time CDP com o Healthcare Shield (e quais não estão)?

Com o Healthcare Shield, as marcas podem trazer o seguinte PHI para aplicativos baseados em plataforma, como o Real-Time CDP (&quot;Dados pessoais confidenciais permitidos&quot;): Informações financeiras, médicas ou sanitárias de uma pessoa. Mas estamos excluindo especificamente dados que podem ser usados para identificar abuso de substâncias, saúde mental, registros genéticos de saúde ou registros de saúde de um menor, número de conta completo, números completos de cartão de crédito, identificadores governamentais (como SSN) e informações pessoais de crianças protegidas por qualquer lei de proteção infantil (como informações pessoais definidas pela lei americana Children&#39;s Online Privacy Act (&quot;COPPA&quot;)).

### Com o Healthcare Shield, os clientes da Real-Time CDP podem usar qualquer tipo de PHI para criar públicos-alvo e ativá-los?

Mesmo quando um cliente pode trazer dados pessoais confidenciais permitidos para aplicativos nativos da plataforma, ele precisa entender que é o único responsável por manter-se em conformidade com todas as regulamentações aplicáveis e obter permissões, consentimentos, autorizações e autorizações apropriadas dos consumidores para usar os dados de acordo com as maneiras desejadas.

### Quais são as nuances de assimilar e ativar dados do cliente com aplicativos Adobe que não estejam prontos para HIPAA?

Um Healthcare Shield licenciado pelo cliente não pode usar, assimilar, coletar, compartilhar ou integrar dados pessoais confidenciais permitidos a qualquer aplicativo e serviço de Adobe não preparado para HIPAA. Por exemplo, um cliente não deve ativar segmentos que contêm PHI em aplicativos como Audience Manager, Adobe Target e Adobe Analytics. Os clientes que licenciam o Healthcare Shield podem assimilar dados pessoais confidenciais ou PHI autorizado em aplicativos de Adobe prontos para HIPAA, independentemente de a fonte de dados ser considerada pronta ou não para HIPAA.

### Quais são as nuances de assimilar e ativar dados do cliente com aplicativos não-Adobe não preparados para HIPAA?

Um cliente que licencie o Healthcare Shield deve usar um bom senso para determinar onde ele ativa segmentos que contêm PHI fora dos aplicativos de Adobe. O Adobe não controla e não é responsável por provedores de terceiros e os dados enviados por um cliente a um provedor de terceiros podem não oferecer suporte ao processamento de dados de acordo com os rótulos de uso de dados do Adobe no schema de clientes. Além disso, o Adobe não pode fornecer assistência jurídica para nossos clientes.

## Principais casos de uso do Health Care

![](Aspose.Words.749b0c49-3370-4549-9a4d-bf21df8fbfb8.001.png)

|**Casos de uso padrão da RTCDP B2C Edition**|**Descrição**| | :- | :- | |Coleta de dados de fluxo|<p>- Modelos de dados normalizados e flexíveis utilizáveis em Adobe e não-Adobe</p><p>- Esquemas de dados baseados em pessoas e contas projetados para marketing B2C</p><p>- O Tag Management e o encaminhamento de eventos coletam e distribuem dados no nível do evento em tempo real.</p><p>- Perfis otimizados que aceleram o tempo de entrega da experiência</p>| |Gerenciamento de perfil confiável|<p>- Perfis unificados que contêm dados de atributo do consumidor, comportamento e preferência</p><p>- O quadro de governança de dados é flexível, transparente e aplicado a perfis unificados com criação de políticas e aplicação automática para evitar o uso indevido de dados. </p>| |Ativação em tempo real|<p>- Segmentação de arrastar e soltar projetada para profissionais de marketing B2C</p><p>- Resolução de identidade de pessoa e nível de conta e enriquecimento de perfil para ativação entre canais</p><p>- Experiências consistentes do cliente por meio da orquestração de público-alvo e ativação em tempo real entre canais e ambientes (Adobe e não-Adobe)</p>| |Aquisição do cliente|<p>- Insights sobre a conversão de usuários não autenticados em usuários reconhecidos/autenticados</p><p>- Incentivar os usuários não registrados a se registrarem como membros.</p><p>- Aumentar e/ou recuperar assinaturas</p><p>- Analise os perfis do cliente para entender a propensão (por exemplo, . comparar segmentos de alto valor com segmentos de baixo desempenho e otimizar para aquisição) </p>| |Envolvimento do cliente|<p>- Ofertas do Target com base no comportamento do consumidor, recenticidade e ação de frequência para ofertas (online e offline)</p><p>- Unifique as propriedades digitais para uma experiência conectada (por exemplo, incentive downloads de aplicativos móveis e use a ativação de segmentos em canais para conectar experiências)</p>| |Personalização em escala|<p>- Avaliar segmentos na borda para a mesma página em tempo real e a próxima personalização da página</p><p>- Aumente o engajamento fornecendo experiências exclusivas e direcionadas para visitantes que abandonam uma sessão entre jornadas (por exemplo, abandonem o carrinho, repetem visitantes que não conseguem converter).</p><p>- Unifique e conecte comportamentos offline e online para otimizar e engajar usuários</p>| |Venda cruzada/venda adicional|<p>- Manter os clientes enquanto expandem e mantém os relacionamentos existentes com os usuários</p><p>- Impulsionar novos fluxos de receita com unidade de negócios/marca/oferta para o valor vitalício do cliente</p><p>- Obtenha informações sobre a AOV em produtos e SKUs (por exemplo, pacotes frequentes, sensibilidade a preços)</p>| |Retenção/Fidelidade do Cliente|<p>- Reativar consumidores para gerar fidelidade e evitar churn do cliente</p><p>- Preparar recomendações personalizadas de produtos para clientes de alto valor com base em preferências e propensão</p><p>- Criar um cadastro padrão para engajamento e ofertas especiais para consumidores fiéis</p><p>- Vincular preferências online e offline para otimizar ofertas entre canais</p>| |Colaboração de dados|<p>- Crie handshakes em uma interface do usuário para criar workflows de colaboração de dados.</p><p>- (Aproveite as sobreposições de dados primários em todos os setores para informar as decisões e campanhas estratégicas de negócios.</p><p>- Analisar silos de dados e entender a jornada holística do cliente</p><p>- Respeitar preferências e consentimento por caso de uso</p>| |Eficiência e otimização de mídia/marketing|<p>- Ganhe eficiência organizacional centralizando e mantendo os canais de ativação e dados do cliente em um sistema de registro</p><p>- Suporte a campanhas de supressão para gastos/eficiências de mídia eficazes</p><p>- Alinhar-se às políticas de TI por meio de controle e aplicação de políticas</p><p>- Forneça acesso aos dados conforme necessário, em tempo real, para oferecer suporte a campanhas oportunas</p>|

## **3- Recursos técnicos relevantes**
![](Aspose.Words.749b0c49-3370-4549-9a4d-bf21df8fbfb8.001.png)

**Diferenças**:

|**Pronto para uso**|**Escudo da Saúde**| | :- | :- | :- | |Criptografia|Criptografia de dados no AEP [documentação oficial](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/encryption.html?lang=en)|<p>Criptografia de dados no AEP [documentação oficial](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/encryption.html?lang=en)</p><p>+</p><p>Chaves gerenciadas pelo cliente </p>| |Higiene dos dados|<p>**Fundamento**: Ferramenta de autoatendimento para permitir que os clientes gerenciem o ciclo de vida dos dados. Isso inclui exclusão de dados do cliente, campo</p><p>atualizações de nível e definição da expiração de dados em conjuntos de dados para remover dados expirados.</p><p>Limite de **10.000 solicitações de exclusão** por mês </p><p>Limite de 2 TTLs do conjunto de dados</p>|<p>**Premium**: Estenda a capacidade/limite diário da funcionalidade de Higiene de Dados para preparar conjuntos de dados maiores em menos tempo.</p><p>Limite de **2.000.000 solicitações de exclusão** por mês como parte do HealthCare</p><p>Limite de 20 TTLs do conjunto de dados</p>| |Consentimento|<p>**Fundamento**: Consentimento e preferências granulares adicionando manualmente o consentimento e os atributos relacionados à preferência à segmentação do público-alvo.</p><p></p>|<p>**Premium**: Crie e imponha automaticamente políticas sobre como os dados do cliente devem ser usados com base no consentimento e nas preferências.</p><p></p>|

### **Governança:**
- **Higiene de dados**
   - [**Visão geral da higiene dos dados**](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-hygiene/overview.html?lang=en)
   - [**Higiene dos dados no Adobe Experience Platform**](https://experienceleague.adobe.com/docs/experience-platform/hygiene/home.html?lang=en)
- **Aplicação de políticas**
   - [**Visão geral da governança de dados**](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=en)
   - [**Visão geral das políticas de uso de dados**](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=en)
   - [**Governança, privacidade e segurança no Adobe Experience Platform**](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/overview.html?lang=en#consent)

### **Privacidade:**
- **Consentimento**
   - [**Aplicação automática da política**](https://experienceleague.adobe.com/docs/experience-platform/data-governance/enforcement/auto-enforcement.html?lang=en#consent-policy-evaluation)

### **Segurança:**
- **Controles de acesso**
   - [**Visão geral do controle de acesso baseado em atributos**](https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/overview.html)
- **Auditorias de atividade do usuário**
   - [**Logs de auditoria**](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html)
- **Criptografia avançada**
   - [**Visão geral da segurança no Adobe Experience Platform**](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf)
   - [**Criptografar valores**](https://experienceleague.adobe.com/docs/experience-platform/tags/api/guides/encrypting-values.html?lang=en)
   - [**Criptografia de dados no Adobe Experience Platform**](https://experienceleague.adobe.com/docs/experience-platform/catalog/data-protection.html)
   - [**Funções de mapeamento de preparação de dados - Hash**](https://experienceleague.adobe.com/docs/experience-platform/data-prep/functions.html?lang=en#hashing)
- [**Adobe Real-time Customer Data Platform e o Healthcare Shield | Adobe Experience Cloud**](https://experienceleague.adobe.com/docs/customer-data-management-voices-events/events/healthcare-shield.html?lang=en)

Cumprir a promessa de experiência, com acesso a menos dados. Se você for um anunciante, editor ou agência, este webinário ajudará a desbloquear a variável

- [**Visão geral dos logs de auditoria | Adobe Experience Platform**](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html "https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html")

Saiba como os logs de auditoria permitem ver quem realizou quais ações na Adobe Experience Platform.

- [**Visão geral da higiene de dados | Adobe Experience Platform**](https://experienceleague.adobe.com/docs/experience-platform/hygiene/home.html?lang=en)

A Higiene de dados do Adobe Experience Platform permite gerenciar o ciclo de vida de seus dados ao atualizar ou limpar registros desatualizados ou imprecisos.

- [**Aplicação Automática de Política | Adobe Experience Platform**](https://experienceleague.adobe.com/docs/experience-platform/data-governance/enforcement/auto-enforcement.html?lang=en)

Este documento aborda como as políticas de uso de dados são aplicadas automaticamente ao ativar segmentos para destinos no Experience Platform.

- [**Visão geral do controle de acesso baseado em atributos | Adobe Experience Platform**](https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/overview.html "https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/overview.html")

Este documento fornece informações sobre o controle de acesso baseado em atributos no Adobe Experience Platform
## **4- Produtos e serviços HIPAA e Adobe**
O Adobe continua inovando e adaptando-se para atender às necessidades de nossos clientes no setor de saúde para atender às necessidades específicas de privacidade e segurança. 

Aqui estão os [detalhes](https://www.adobe.com/trust/compliance/hipaa-ready.html).
## **5 - Diagrama da arquitetura de alto nível**
Produtos prontos para HIPAA (e não):

![](Aspose.Words.749b0c49-3370-4549-9a4d-bf21df8fbfb8.001.png)

[https://lucid.app/lucidchart/8a795213-3bfa-43f3-a542-f0de56123afd/edit?invitationId=inv_d3183739-8c07-4ca2-bfd1-16d819b911a6&amp;page=0_0#](https://lucid.app/lucidchart/8a795213-3bfa-43f3-a542-f0de56123afd/edit?invitationId=inv_d3183739-8c07-4ca2-bfd1-16d819b911a6&amp;page=0_0)

![](Aspose.Words.749b0c49-3370-4549-9a4d-bf21df8fbfb8.001.png)
## **6- Abordagem:**
### **Etapas de implementação:**
![](Aspose.Words.749b0c49-3370-4549-9a4d-bf21df8fbfb8.001.png)

Aspectos a serem considerados em cada etapa:

![](Aspose.Words.749b0c49-3370-4549-9a4d-bf21df8fbfb8.001.png)

Esta seção descreve algumas práticas recomendadas a serem seguidas e é dividida em três fases:
### **Fase de entrevista:**
O processo de entrevista com as partes interessadas é fundamental para compreender os seguintes aspectos:

- Objetivo: Tipo de casos de uso - Conversão, Prospecção, Envolvimento etc.
- Desempenho: Quaisquer expectativas de meta de nível de serviço
- Fontes de dados: Web/Analytics, Offline/Online, CRM, Fidelidade etc.
- Volume de dados
- Requisitos de SLT/SLA
- Identidades - Número de identidades, tratamento de dados autenticado vs anônimo
- Formato dos dados: JSON, CSV etc.
- Qualidade dos dados, necessidade de transformações de dados
- Qualquer plano para Correspondência de segmentos (Compartilhamento) com parceiros 
- Qualquer público externo a ser importado
- Criptografia: Padrão vs. Chave gerenciada pelo cliente
- Combinação de dados: é considerada uma e-PHI
- Coleta de dados de consentimento - SDK do OneTrust, Consent
- Necessidades de destino: Requisitos de controle de frequência e latência e acesso
- Controle de acesso
- Requisitos de limpeza de dados
- Requisitos da atualização de dados
- Necessidades de alertas
- Acesso à API

### **Fase de projeto:**
Com base no processo de entrevista, a fase de design abordará o seguinte. Escusado será dizer que a documentação de design precisa ser revisada e desconectada. O documento de design pode abranger os seguintes aspectos:

- Valor dos dados:
   - Volume - Quantidade de dados assimilados
   - Timespan - Duração de tempo em que os dados assimilados devem residir
   - Fidelidade - riqueza do perfil
- Considere as medidas de proteção da AEP junto com os requisitos de SLT/SLA 
- Uso de licença
- Necessidades de isolamento de dados - várias sandboxes em uma ou várias organizações
- Filtragem de dados
- Requisitos de higiene dos dados (quantidade de dados e frequência)
- Processo e metodologia para atender aos requisitos de exclusão/atualização de dados 
- Necessidades de transformação de dados - upstream, preparação de dados, serviço de query
- Entender e determinar identidades primárias e outras
- [Design do esquema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en)
- Determine o número de conjuntos de dados, perfis e não perfis
- Design da Política de Mesclagem
- Gerenciamento de dados de consentimento
- Governança: Funções, rótulos, políticas, ações de marketing e controle de acesso
- [Enriquecimento de perfil](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)
- Requisitos de design de segmentação para Edge/Streaming/Batch
- Destinos e planos de ativação esperados. Considere a HIPAA pronta somente para as necessidades de destino
- Planos para o Analytics
- Alertas
- Adicionar requisitos de acesso à API

### **Fase de implementação:**
Depois que o documento de design for revisado e desconectado, a fase de implementação poderá começar a abordar as seguintes áreas:

- Número de sandboxes necessárias: Dev/Test/Prod
- Controle de acesso a sandboxes
- Metodologia de implantação
- Necessidades e frequência de TTL (Higiene de Dados)
- Esquema XDM e controle de acesso
- Execução do consentimento
- Governança: Funções, rótulos, políticas e ações de marketing 
- Segmentação
- Conjuntos de dados e controle de acesso
- Configuração da Higiene de dados
- Configuração de destinos e controle de acesso
- Configurar alertas
- Implementar requisitos de acesso da API
- Teste de ponta a ponta com dados de modelo

