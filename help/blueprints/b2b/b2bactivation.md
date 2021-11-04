---
title: Ativação B2B
description: Forneça públicos-alvo baseados em conta e experiências de clientes centradas em perfis com o Real-time Customer Data Platform ​.
solution: Experience Platform, Real-time Customer Data Platform
kt: 9311
exl-id: null
source-git-commit: d811d82418d477372caa9e5b0b67af197275d459
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 5%

---

# Público-alvo B2B e ativação de perfil

Use informações de conta, oportunidade e cliente potencial vinculadas a um cliente individual para criar perfis b2b acionáveis para melhorar a personalização e o direcionamento entre canais.

## Casos de uso

* Crie públicos-alvo de pessoas para segmentação e personalização em canais em relação a dados B2B, incluindo contas, oportunidades e leads.
* Ative públicos-alvo para quaisquer destinos de Experience Platform para direcionamento e personalização.

## Aplicativos

* Plataforma de dados do cliente em tempo real Edição B2B

## Padrões de integração

* Fontes de dados B2B (Marketo, Salesforce etc.) -> Real-time Customer Data Platform B2B Edition -> Destinos Várias fontes de dados B2B podem ser usadas para mapear dados de conta, lead, oportunidade e pessoas para a B2B Edition do Real-time Customer Data Platform.

## Arquitetura

<img src="assets/b2b-activation.svg" alt="Arquitetura de referência para o B2B Ativation Blueprint" style="border:1px solid #4a4a4a" />
<br>

## Medidas de proteção

Observe que as medidas de proteção e de implementação relacionadas com o Marketo Engage só são relevantes quando o Marketo Engage é usado como fonte e/ou destino.

### Suporte a várias instâncias e organizações IMS:

A seguir, são descritos os padrões suportados de instâncias de Experience Platform e Marketo Engage de mapeamento.

#### Marketo como fonte de dados para o Experience Platform:

* Há suporte para várias instâncias de Marketo Engage para uma instância de Experience Platform.
* Várias instâncias de Marketo Engage para muitas instâncias de Experience Platform não são compatíveis.
* Não há suporte para uma instância Marketo Engage para muitas instâncias do Experience Platform.
* Há suporte para uma instância Marketo Engage para uma instância Experience Platform e várias sandboxes.

#### Marketo como destino do Experience Platform:

* Experience Platform para muitas instâncias do Marketo Engage é suportado
* Há suporte para muitas instâncias de Experience Platform para uma instância de Marketo Engage.

#### Proteção de perfil e segmentação do Experience Platform:

* Consulte as grades de proteção de perfil e segmentação para o Experience Platform - [Diretrizes de perfil e segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)
* Segmentos B2B que incluem contas, leads, oportunidades usam relacionamentos de várias entidades que resultam na avaliação do segmento se tornar lote. A segmentação de transmissão é compatível com segmentos que são limitados a pessoas e eventos.

#### Experience Platform - Marketo Engage Source Connector:

* O preenchimento retroativo histórico pode levar até 7 dias para ser concluído, dependendo do volume de dados.
* As atualizações e alterações de dados constantes do Marketo são enviadas para o Experience Platform por meio da API de transmissão que pode estar latente até cerca de 5 minutos para o perfil e em torno de 15 minutos para o lago de dados, dependendo do volume.

#### Experience Platform - Conector de destino Marketo:

* O compartilhamento de segmentos de transmissão do Real-time Customer Data Platform para o Marketo Engage pode levar até 5 minutos.
* A segmentação em lote é compartilhada uma vez por dia com base no agendamento de segmentação do Experience Platform. Segmentos B2B que incluem contas, leads, oportunidades usam relacionamentos de várias entidades que resultam no segmento se tornar lote.

#### Marketo Engage Guardrails:

* Os contatos e leads devem ser assimilados e definidos diretamente no Marketo Engage para que o público-alvo da Real-time Customer Data Platform corresponda a um contato e um cliente potencial do Marketo Engage.

#### Medidas de proteção de destino

* Consulte a documentação de destino para obter orientações específicas sobre os destinos. [Diretrizes de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)


## Etapas de implementação

Para obter orientações sobre como implementar e configurar a edição B2B da Real-time Customer Data Platform, consulte a Edição B2B da Documentação da Real-time Customer Data Platform. [Edição B2B do Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/b2b-overview.html?lang=en)

Existem dois padrões de implementação possíveis. A capacidade de assimilar dados B2B e perfis do Marketo Engage ou a capacidade de assimilar dados B2B de outras fontes de dados CRM.

## Considerações de implementação

Orientação sobre as principais considerações e configurações do blueprint.

* Integração CRM com e sem Marketo: Se a implementação for usar o Marketo Engage como fonte e o Marketo Engage estiver conectado ao CRM, use o conector de origem do Marketo no Experience Platform para assimilar os dados do CRM no Experience Platform. Use o conector de origem do Experience Platform se forem necessárias tabelas adicionais. Se a implementação não estiver usando o Marketo Engage como uma fonte, conecte a fonte do CRM diretamente à AEP usando o conector do Experience Platform de origem do CRM.
* Não é recomendado iniciar e alimentar o cliente com chumbo da edição B2B do Real-time Customer Data Platform por si só. Para este caso de uso, recomenda-se o uso de uma ferramenta de amamentação de chumbo (como o Marketo Engage).
* O conector de destino do Marketo Engage para AEP, que envia públicos para o Marketo Engage para ativação, envia somente endereços de email e ECIDs. Ele não cria um novo lead se o contato ainda não existir, portanto, é necessário assimilar o perfil e dados do lead no Marketo Engage.

## Documentação relacionada

* [Edição B2B do Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/b2b-overview.html?lang=en)
* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Marketo Engage](https://experienceleague.adobe.com/docs/marketo/using/home.html?lang=en)
* [Adobe Experience Platform - Conector de origem Marketo](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo.html?lang=pt-BR)
* [Adobe Experience Platform - Conector de destino do Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en)