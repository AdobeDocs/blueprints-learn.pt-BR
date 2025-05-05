---
title: Ativação de conta B2B para destinos Advertising e destinos de arquivos
description: Use o engajamento baseado em conta para criar públicos-alvo e direcioná-los por meio de destinos.
solution: Real-Time Customer Data Platform
source-git-commit: 074edca2f061459935d5f8b5e59e8cbd69b0fe4f
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 5%

---

# Ativação da conta B2B para destinos de anúncios e destinos de arquivos

O contrato baseado em conta permite que os profissionais de marketing B2B criem públicos-alvo de contas (ou seja, listas de empresas) e direcionem essas empresas por meio de destinos como o LinkedIn, que aceita listas de empresas como entrada ou exportação para destinos de armazenamento em nuvem para direcionamento e alcance de vendas.

## Casos de uso

Usando o engajamento baseado em conta, os profissionais de marketing podem desbloquear três casos de uso importantes:

* **Preencha as lacunas do grupo de compras:** um profissional de marketing pode anunciar em contas em que ainda não tem contatos para as funções de CMO ou CIO. Primeiro, é possível criar um público-alvo de contas sem um contato com o título &quot;CMO&quot; ou &quot;CIO&quot; e depois ativar o público-alvo no LinkedIn. No destino, a LinkedIn pode lançar uma campanha direcionada a esse público-alvo e a pessoas específicas com títulos de trabalho de &quot;CMO&quot; ou &quot;CIO&quot; para alcançar esses novos contatos e destacar os benefícios de suas ofertas.
* **Venda adicional ou venda cruzada para outras divisões de uma empresa que seja um cliente existente:** um profissional de marketing pode criar um público-alvo de conta que comprou o produto X entre 3 e 9 meses atrás, mas ainda não possui o produto Y. Eles podem então ativar o, destacando os benefícios do produto Y para esse público-alvo.
* **Empresas de destino que estão usando produtos concorrentes:** um profissional de marketing pode vender para contas a fim de substituir os produtos de um concorrente, mesmo sem contatos nessas contas. Eles podem criar um público-alvo de contas com base nos dados dos parceiros, mostrando a propriedade ou o uso do produto de um concorrente e, em seguida, ativar por meio do LinkedIn para fornecer contatos nas contas de destino para expansão.

## Aplicativos

* Edição B2B da Real-time Customer Data Platform

## Padrões de integração

* Fontes de dados B2B (Marketo, Salesforce etc.) -> Real-time Customer Data Platform B2B Edition -> Destinos.
* Várias fontes de dados B2B podem ser usadas para mapear dados de conta, lead, oportunidade e pessoas para a B2B Edition do Real-time Customer Data Platform.

## Arquitetura

![Arquitetura de referência para o Blueprint do Audience Activation da conta B2B](assets/b2b-blueprint-account-audience-activation.png)

## Destinos de público da conta

* (Empresas) Públicos-alvo correspondentes do LinkedIn
* Destinos do Cloud Storage
   * Azure Data Lake
   * Zona de aterrissagem de dados
   * SFTP
   * Azure Blob
   * AWS S3

## Medidas de proteção

* Limite de 50 segmentos de conta por sandbox.
* Avaliação da segmentação em lote.
   * Avaliado automaticamente a cada 24 horas após a conclusão da execução do público-alvo em lote e dos trabalhos de exportação de perfil.
   * Não há suporte para edge, streaming ou avaliação ad-hoc.
* Os atributos da conta estão disponíveis para exportação.
* Eventos de pessoas.
   * Até 30 dias de retrospectiva de evento, sem ordem de predicados de evento.
   * AND / OR são compatíveis (portanto, você pode dizer &quot;A e B precisam acontecer&quot;,  mas você não pode dizer &quot;A deve acontecer 3 dias antes de B&quot;).
* Para destinos de armazenamento na nuvem, o agendamento de exportação oferece suporte à opção &quot;Após avaliação de segmento&quot;.
* [Proteções de perfil B2B e segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails).

## Etapas de implementação para o Real-time Customer Data Platform B2B Edition, criação e ativação de público-alvo da conta

* Para obter as etapas de implementação do Real-time Customer Data Platform B2B Edition, consulte a [Introdução ao Real-time Customer Data Platform B2B Edition](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial) documentação.
* Para conhecer as etapas de criação de público-alvo da conta, consulte a documentação de [Públicos-alvo da conta](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/account-audiences).
* Para ver as etapas do Audience Activation de conta, consulte a documentação [Ativar públicos-alvo de conta](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/ui/activate/activate-account-audiences).
   * Mapeamento necessário para [(Empresas) LinkedIn Matched Audiences destination](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/ui/activate/activate-account-audiences#required-mappings).

## Considerações de implantação

Os públicos-alvo correspondentes do linkedIn têm alguns requisitos, incluindo o tamanho mínimo de público-alvo de 300 membros correspondentes. Se o público-alvo da conta ativado para o destino do público-alvo correspondente vinculado da empresa não atender ao requisito, a definição do público-alvo precisará ser modificada para aumentar o tamanho do público-alvo para iniciar uma campanha do LinkedIn.

## Documentação relacionada

* [Edição B2B da Real-time Customer Data Platform](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview)
* [Criar e ativar o vídeo tutorial de público-alvo da conta](https://experienceleague.adobe.com/pt-br/docs/platform-learn/tutorials/audiences/create-audiences-with-b2b-data)
* [Criar públicos-alvo da conta](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/ui/account-audiences)
* [Ativar públicos-alvo da conta](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/ui/activate/activate-account-audiences)
* [Adobe Experience Platform - Conector de Destino do LinkedIn](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/catalog/social/linkedin)
