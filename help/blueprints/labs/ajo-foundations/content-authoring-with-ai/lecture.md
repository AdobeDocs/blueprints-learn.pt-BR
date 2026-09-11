---
hold: true
title: Palestra
description: Explore o modelo de anatomia de conteúdo em quatro camadas, os padrões de integração de conteúdo do AJO e do AEM e a governança de conteúdo assistida por IA para personalização em escala.
doc-type: article
solution: Experience Platform
exl-id: 1ac39a70-51f8-426e-97cf-1ff08450d326
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---


# Palestra

## Objetivos de aprendizagem

- Explicar por que o conteúdo, não dados ou jornadas, é a principal restrição nos programas de personalização em escala
- Descrever o modelo de anatomia de conteúdo em quatro camadas: ativos, fragmentos, modelos e mensagens
- Diferenciar entre fragmentos do AJO e fragmentos de conteúdo do AEM, incluindo como cada um lida com a propagação
- Mapear os estágios do ciclo de vida do conteúdo para criar, armazenar, gerenciar, controlar, ativar e medir
- Compare os três padrões de integração de conteúdo: AJO independente, AJO + AEM Assets e AJO + GenStudio for Performance Marketing
- Identifique os sinais de arquitetura que indicam quando escalar de um padrão para o próximo
- Descreva as três camadas do recurso de IA na pilha do Adobe: Assistente de conteúdo, Modelos personalizados da Firefly e o Serviço de marca unificada
- Explicar o princípio da supervisão humana no loop em fluxos de trabalho de conteúdo assistido por IA
- Diferenciar personalização verdadeira da inserção de nome ou multiplicação de ativos

## Vídeo

Neste vídeo, você aprenderá o modelo de anatomia de conteúdo em quatro camadas, os três padrões de integração de conteúdo do AJO e como os recursos de IA se encaixam em um sistema de conteúdo governado.

>[!VIDEO](https://video.tv.adobe.com/v/3491063/?quality=12&learn=on)

## Principais pontos

O Personalization em escala depende de três pilares: conteúdo, dados e jornadas. A maioria das empresas investe pesadamente em orquestração de dados e jornadas, mas trata o conteúdo como uma reflexão posterior, que é exatamente o motivo pelo qual o conteúdo é onde os programas de personalização quebram primeiro. Para um arquiteto do AJO, entender como estruturar o conteúdo como um sistema governado, em vez de uma pilha de ativos únicos, é o que separa uma implementação escalável de uma que entra em colapso sob sua própria subutilização de modelo.

**Nesta lição você abordou:**

- A tese: a personalização não falha por causa dos dados, falha porque o conteúdo não é arquitetado como um sistema
- A anatomia do conteúdo de quatro camadas: Assets (mídia atômica no DAM), Fragmentos (blocos visuais ou de expressão reutilizáveis), Modelos (zonas bloqueadas versus editáveis) e Mensagens (a saída final montada e pronta para canal)
- O ciclo de vida do conteúdo: criar, armazenar, gerenciar, administrar, ativar, medir — e como as falhas ocorrem da esquerda para a direita quando um estágio é ignorado
- Padrão 1, AJO independente: melhor para mercado único, canal único, em 50 variantes, quando a velocidade é a restrição principal; usa o AEM Assets Essentials como um DAM agrupado básico
- Os fragmentos do AJO são armazenados no AJO, copiados em modelos como duplicatas, sem atualizações automáticas e um limite de 30 fragmentos/1 nível de aninhamento
- Padrão 2, AJO + AEM: melhor para vários mercados, mais de 50 variantes, quando a governança é a principal restrição; AEM se torna o sistema de registro, AJO o sistema de ativação
- Os fragmentos de conteúdo do AEM são mencionados (não copiados) pelo AJO, portanto, as atualizações se propagam instantaneamente em cada modelo de referência, jornada e campanha
- Três cenários que interrompem silenciosamente a propagação do fragmento: herança interrompida (fragmento desbloqueado), novos atributos de personalização adicionados a um fragmento publicado e restrições de rótulo do Controle de acesso em nível de objeto (OLAC)
- Padrão 3, AJO + GenStudio for Performance Marketing: melhor para escala de produção e geração de variantes de alto volume; requer a governança do Padrão 2 como um pré-requisito obrigatório
- Os quatro pilares que mantêm a geração de IA na marca: Serviço de marca unificada, Content Credentials, curadoria em loop humano e integração do AJO
- A matriz de decisão de arquitetura e o modelo de maturidade de conteúdo da Supply chain (níveis de 1 ad-hoc a 5 autônomos) para diagnosticar onde um cliente está hoje
- A personalização verdadeira é a variação inteligente em um único modelo governado, não campos de mesclagem de nome ou campanhas separadas por segmento
