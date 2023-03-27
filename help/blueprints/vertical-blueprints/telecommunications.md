---
title: Setor de telecomunicações – Journey Optimizer para envio de mensagens acionadas
description: Forneça aos clientes ofertas personalizadas em tempo real, além de uma integração eficiente do cliente para fidelidade de longo prazo.
solution: Journey Optimizer
kt: 9486
exl-id: fa4a6569-3972-4b97-91f1-7ca8ffd3c5b3
source-git-commit: 1a0ce987fc615080bb78fb8ecf60c96e362a95c0
workflow-type: ht
source-wordcount: '333'
ht-degree: 100%

---

# Desafio das empresas do setor de telecomunicações

Antes de implantar este blueprint, as campanhas de email “Adicione uma nova linha” da empresa de telecomunicações dependiam se o usuário tinha se convertido e somente verificado após um período de espera de 7 dias. Assim que estes critérios eram atendidos, quaisquer pontos de contato adicionais eram iniciados.

Esta limitação teve de ser resolvida a fim de dar início a um acompanhamento mais pontual dos usuários que pretendiam adicionar uma linha antes do atual período de espera de 7 dias.

## Abordagem da Adobe

* Os dados do Adobe Analytics para identificar usuários que não foram convertidos para adicionar uma nova linha são incluídos como uma fonte de dados para uso pelo Adobe Journey Optimizer.
* O Adobe Journey Optimizer usa uma regra para o momento em que o cliente recebe uma mensagem personalizada de “abandono” projetada para incentivar a conversão de um cliente, adicionando uma nova linha à conta.


## Valor comercial fornecido

| Metas | Táticas | Valor desbloqueado |
|---|---|---|
| **Aumente as taxas de conversão da campanha **<br></br>** Aumente as receitas de contas anuais**</ul> | <ul><li>Crie um novo segmento em tempo quase real para usuários que demonstraram interesse em adicionar uma linha, mas ainda não foram convertidos.</li><li>Impulsione o acompanhamento de clientes não convertidos com um segundo ponto de contato para clientes interessados que não foram convertidos. </li><li>Use uma estratégia de teste para medir o desempenho da jornada e otimizar a conversão por email.</li></ul> | <ul><li><strong>Experiências relevantes e de alta qualidade:</strong> Com a orquestração de jornadas em vigor, os clientes recebem mensagens mais relevantes, o que reduz o churn da lista de emails.</li><li><strong>Escala de Journey Orchestration:</strong> Uma jornada personalizada e mais oportuna pode ser criada para gerar um aumento nas conversões e na receita total.</li></ul> |

## Blueprint principal: público-alvo e ativação com aplicativos da Experience Cloud

### Descrição

<ul><li>Execute mensagens acionadas e por streaming usando a Adobe Experience Platform como hub central para transmissão de dados, perfis e segmentação de clientes, com o Journey Orchestration para transmitir a orquestração de jornadas e entrega de mensagens</li></ul>

### Aplicativos da Experience Cloud

<ul><li>Adobe Journey Optimizer</li></ul>

### Arquitetura do Blueprint

<a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer.html?lang=pt-BR"><img alt="imagem de uma empresa de telecomunicações que oferece ofertas personalizadas em tempo real, além de integração eficiente do cliente para fidelidade de longo prazo." src="https://experienceleague.adobe.com/docs/blueprints-learn/assets/ajo-architecture.svg"/></a>
