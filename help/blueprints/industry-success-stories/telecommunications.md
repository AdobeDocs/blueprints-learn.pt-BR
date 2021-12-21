---
title: Setor de telecomunicações - Journey Optimizer para envio de mensagens por disparo
description: Forneça aos clientes ofertas personalizadas em tempo real, além de uma integração eficiente do cliente para fidelidade de longo prazo.
solution: Experience Platform, Journey Optimizer
kt: 9486
source-git-commit: c393d73d2fa7acd4e5c2d99c098503b023b6115d
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 12%

---


# Desafio comercial do setor de telecomunicações

Antes de implementar este Blueprint, as campanhas de email &quot;adicionar uma nova linha&quot; da empresa de telecomunicações dependiam se o usuário tinha se convertido e somente verificado isso após um período de espera de 7 dias. Assim que estes critérios forem atendidos, quaisquer pontos de contato adicionais foram iniciados.

Esta limitação teve de ser resolvida a fim de dar início a um acompanhamento mais atempado dos utilizadores que pretendiam adicionar uma linha antes do atual período de espera de 7 dias.

## Abordagem Adobe

* Os dados do Adobe Analytics para identificar usuários que não foram convertidos para adicionar uma nova linha são incluídos como uma fonte de dados para uso pelo Adobe Journey Optimizer.
* O Adobe Journey Optimizer usa uma regra para o momento em que o cliente recebe uma mensagem personalizada de &quot;abandono&quot;, projetada para incentivar um cliente a converter, adicionando uma nova linha à conta.


## Valor comercial fornecido

| Metas | Táticas | Valor desbloqueado |
|---|---|---|
| **Aumente as taxas de conversão da campanha **<br></br>**Aumentar as receitas das contas anuais**</ul> | <ul><li>Crie um novo segmento em tempo quase real para usuários que demonstraram interesse em adicionar uma linha, mas ainda não foram convertidos.</li><li>Impulsione o acompanhamento de clientes não convertidos com um segundo ponto de contato para não conversores interessados. </li><li>Use uma estratégia de teste para medir o desempenho da jornada e otimizar para conversão por email.</li></ul> | <ul><li><strong>Experiências relevantes e de alta qualidade:</strong> Com a orquestração de jornadas em vigor, os clientes passam por mensagens mais relevantes, o que reduz o churn da lista de emails.</li><li><strong>Escala de Journey Orchestration:</strong>Uma jornada personalizada e mais oportuna pode ser criada para gerar um aumento nas conversões e na receita total.</li></ul> |

## Blueprint principal: Público-alvo e ativação com aplicativos Experience Cloud

### Descrição

<ul><li>Execute mensagens acionadas e por streaming usando a Adobe Experience Platform como hub central para transmissão de dados, perfis e segmentação de clientes, com o Journey Orchestration para transmitir a orquestração de jornadas e entrega de mensagens</li></ul>

### Aplicativos da Experience Cloud

<ul><li>Adobe Journey Optimizer</li></ul>

### Arquitetura do Blueprint

<a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer.html?lang=pt-BR"><img alt="a imagem em miniatura de uma empresa de Telecomunicações oferece ofertas personalizadas em tempo real, além de integração eficiente do cliente para fidelidade de longo prazo." src="https://experienceleague.adobe.com/docs/blueprints-learn/assets/journey-optimizer.png?lang=en"/></a>





