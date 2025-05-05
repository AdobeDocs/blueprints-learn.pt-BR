---
title: Blueprint da ativação de público-alvo e perfil B2B
description: Ofereça experiências do cliente centradas em perfil e públicos-alvo baseados em contas com a Real-time Customer Data Platform.
solution: Real-Time Customer Data Platform
kt: 9311
exl-id: 5215d077-b0a9-4417-ae9b-f4961d4a73fa
source-git-commit: 3dfdb1a237995e7f17e280e24f8865e992d9eb5f
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 52%

---

# Blueprint da ativação de público-alvo e perfil B2B

Use as informações de conta, oportunidade e lead vinculadas a um cliente individual para criar perfis B2B acionáveis com o intuito de melhorar a personalização e o direcionamento nos canais.

## Casos de uso

* Crie públicos-alvo de pessoas para direcionamento e personalização nos canais em relação a dados B2B, incluindo contas, oportunidades e leads.
* Ative públicos-alvo para quaisquer destinos da Experience Platform para direcionamento e personalização.
* Crie públicos-alvo de contas (por exemplo, listas de empresas) e direcione essas empresas por meio de destinos como o LinkedIn, que aceitam listas de empresas como entrada ou exportação para destinos de armazenamento na nuvem para direcionamento e alcance de vendas.

## Aplicativos

* Edição B2B da Real-time Customer Data Platform

## Padrões de integração

* Fontes de dados B2B (Marketo, Salesforce etc.) -> Real-time Customer Data Platform B2B Edition -> Destinos
* Várias fontes de dados B2B podem ser usadas para mapear dados de conta, lead, oportunidade e pessoas para a B2B Edition do Real-time Customer Data Platform.

## Arquitetura

![Arquitetura de referência para o Blueprint de Ativação B2B](assets/b2b-activation.png)

## Medidas de proteção

* Observe que as medidas de proteção e de implantação relacionadas ao Marketo Engage só são relevantes quando o Marketo Engage é usado como fonte e/ou destino.

* Para obter detalhes adicionais e medidas de proteção para modelo de dados, tamanho e segmentação, consulte o [documento de medidas de proteção de implantação](../experience-platform/deployment/guardrails.md)


### Suporte a várias instâncias e organizações IMS:

A seguir, são descritos os padrões suportados de instâncias de mapeamento da Experience Platform e do Marketo Engage.

#### Marketo como fonte de dados para a Experience Platform:

* Há suporte para várias instâncias do Marketo Engage para uma instância da Experience Platform.
* Não há suporte para uma instância do Marketo Engage para muitas instâncias da Experience Platform.
* Há suporte para uma instância do Marketo Engage para uma instância da Experience Platform e várias sandboxes.

#### Marketo como destino da Experience Platform:

* Há suporte para a Experience Platform para muitas instâncias do Marketo Engage
* Há suporte para muitas instâncias da Experience Platform para uma instância do Marketo Engage

#### Proteção de perfil e segmentação da Experience Platform:

* Consulte as medidas de proteção de perfil e segmentação para a Experience Platform – [Medidas de proteção de perfil e segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=pt-BR)
* Segmentos B2B que incluem contas, leads, oportunidades usam relacionamentos de várias entidades que resultam na avaliação do segmento se transformando em lote. A segmentação de transmissão é compatível com segmentos que sejam limitados a pessoas e eventos.
* Inclua um segmento b2b em lote como entrada para um segmento de streaming ou borda para suportar casos de uso de segmentos b2b de streaming. A associação do segmento em lote é baseada no resultado mais recente da avaliação diária da segmentação em lote.

#### Experience Platform – conector de origem do Marketo Engage:

* O preenchimento retroativo histórico pode levar até 7 dias para ser concluído, dependendo do volume de dados.
* As atualizações de dados e alterações contínuas do Marketo são enviadas para o Experience Platform por meio da API de transmissão, que pode estar latente por cerca de 10 minutos para o perfil e pode levar até 60 minutos para o data lake, dependendo do volume.

#### Experience Platform – conector de destino do Marketo:

* O compartilhamento do segmento de transmissão do Real-time Customer Data Platform para o Marketo Engage pode levar até 15 minutos. Os perfis de preenchimento retroativo que já existiam no segmento antes da ativação pela primeira vez podem levar até 24 horas.
* A segmentação em lote é compartilhada uma vez por dia com base na programação de segmentação da Experience Platform. Segmentos B2B que usam relacionamentos com várias entidades, por exemplo, segmentos que usam dados nos objetos de conta e oportunidade, são sempre executados em modo de lote.

#### Proteção do Marketo Engage:

* Os contatos e leads devem ser assimilados e definidos diretamente no Marketo Engage para que o público-alvo da Real-time Customer Data Platform corresponda a um contato e lead do Marketo Engage.
* O destino RTCDP do Marketo pode, opcionalmente, criar novos leads no Marketo para clientes que estão em um segmento, mas não existem no Marketo.

#### Proteção de destino

* Consulte a documentação de destino para obter orientações específicas sobre os destinos. [Proteção de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=pt-BR)


## Etapas de implementação

Para obter orientações sobre como implementar e configurar a Edição B2B da Real-time Customer Data Platform, consulte a Edição B2B da Documentação da Real-time Customer Data Platform. [Edição B2B da Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/b2b-overview.html?lang=pt-BR)

Existem dois padrões de implementação possíveis. A capacidade de assimilar perfis e dados B2B do Marketo Engage ou a capacidade de assimilar dados B2B de outras fontes de dados da CRM.

## Considerações de implantação

Orientações sobre as principais considerações e configurações do blueprint.

* Integração do CRM com e sem o Marketo:
Se a implementação usar o Marketo Engage como uma origem e o Marketo Engage estiver conectado ao CRM, os dados do CRM fluirão automaticamente pela mesma conexão, removendo a necessidade de conectar o CRM diretamente à plataforma, a menos que haja objetos de dados adicionais do CRM que não sejam transmitidos pela Marketo. Use o conector de origem da Experience Platform se as tabelas adicionais precisarem ser assimiladas. Se a implementação não estiver usando o Marketo Engage como uma origem, conecte a origem do CRM diretamente à plataforma usando o conector do Experience Platform de origem do CRM.
* O conector de destino Marketo Engage para a Platform, que envia públicos-alvo para o Marketo Engage para ativação, compartilha membros do público-alvo com base em endereços de email e ECIDs correspondentes. Ele tem a opção de criar um novo lead se o contato ainda não existir. Ao criar um novo lead, até 50 atributos de perfil (atributos não matriz ou mapa) no Real-time Customer Data Platform podem ser mapeados para campos Pessoa no Marketo.

## Documentação relacionada

* [Edição B2B da Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/b2b-overview.html?lang=pt-BR)
* [Introdução ao Real-time Customer Data Platform B2B Edition](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial)
* [Medidas de proteção para o Real-time Customer Data Platform B2B Edition](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails)
* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR)
* [Marketo Engage](https://experienceleague.adobe.com/docs/marketo/using/home.html?lang=pt-BR)
* [Adobe Experience Platform – Conector de origem do Marketo](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo.html?lang=pt-BR)
* [Adobe Experience Platform – Conector de destino do Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=pt-BR)
