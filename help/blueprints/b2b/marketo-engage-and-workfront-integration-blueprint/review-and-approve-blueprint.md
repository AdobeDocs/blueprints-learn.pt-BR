---
title: Revisar e aprovar blueprint
description: Revisar e aprovar o blueprint - blueprint de integração do Marketo Engage e do Workfront
source-git-commit: 4c63a1e552c893a2b2ae753bd3eaccab5c673448
workflow-type: tm+mt
source-wordcount: '1262'
ht-degree: 0%

---

# Revisar e aprovar blueprint {#review-and-approve-blueprint}

Garantir que os ativos e as campanhas de marketing atendam às expectativas e aos padrões de uma empresa vai além de fornecer o conteúdo e as mensagens certos ao público certo. As empresas também têm a responsabilidade de manter políticas internas, normas do setor e até mesmo pré-requisitos legais ao iniciar novas iniciativas de marketing. Incorporando etapas de análise e aprovação ao processo de desenvolvimento de campanha, as equipes de marketing podem garantir que o conteúdo e as mensagens sejam precisos e estejam em conformidade com os padrões do setor, especialmente em setores como financeiro, saúde e farmacêutico.

Com o Workfront e o Marketo Engage, as equipes de marketing têm a oportunidade de ter um sistema de marketing totalmente conectado, com mensagens precisas e em conformidade.

## Desbloqueie revisões e aprovações avançadas para o Marketo Engage com Workfront {#unlock-proofing-and-advanced-approvals}

Quando pensamos em criar campanhas de marketing, devemos considerar que vários sistemas oferecem suporte às diferentes etapas envolvidas, incluindo: planejamento, criação, revisão, feedback, aprovação e execução. Com o Workfront e o Marketo Engage, as equipes têm todas as ferramentas necessárias para conduzi-las ao longo do processo completo de planejamento e lançamento de uma nova campanha de marketing. Além disso, as equipes podem simplificar ainda mais seu processo de análise e aprovação para aumentar a velocidade do desenvolvimento da campanha, garantindo ao mesmo tempo que a precisão e a conformidade sejam mantidas no mais alto padrão.

### Revisar e aprovar casos de uso desbloqueados com o Marketo Engage e o Workfront {#review-and-approve-use-cases-unlocked-with-marketo-engage-and-workfront}

* Elimine feedbacks diferentes e aumente a colaboração em um local centralizado utilizando os recursos de anotação e comentários do Workfront em ativos do Marketo Engage.

* Centralize suas aprovações acionando-as no Marketo Engage a partir dos workflows de aprovação do Workfront.

* Ofereça suporte e simplifique fluxos de trabalho complexos de aprovação de ativos de marketing utilizando os recursos avançados de aprovação da Workfront com ativos do Marketo Engage.

* Democratizar o acesso de rascunhos de marketing puxando programaticamente os ativos do Marketo no Workfront para serem revisados por várias partes interessadas.

* Controle alterações e crie uma trilha de papel centralizando todo o trabalho de revisão e prova de ativos Marketo Engage no Workfront.

## Planejando o fluxo de trabalho de prova e aprovação {#planning-your-proof-and-approval-workflow}

Antes de configurar a integração de prova e aprovação entre o Marketo Engage e o Workfront, considere os seguintes aspectos:

* Quais ativos precisarão ser revisados e aprovados?
* Quem precisará ser o aprovador?
* Será necessário ter vários aprovadores antes que um ativo de marketing possa ser ativado?
* Em que ponto do processo de desenvolvimento da campanha os ativos de marketing serão montados e prontos para serem revisados?

Responder a essas perguntas ajudará você a obter uma linha de base para a aparência do seu fluxo de aprovação e como começar a pensar em configurar sua instância do Workfront.

## Criação de um fluxo de trabalho de prova e aprovação entre o Marketo Engage e o Workfront {#building-a-proof-and-approval-workflow}

Para simplificar o processo de prova e aprovação entre o Workfront e o Marketo Engage, é possível integrar as duas soluções usando o Workfront Fusion. O Workfront Fusion fornece uma interface de fluxo de trabalho para acionar ações e transmitir informações entre as instâncias do Workfront e do Marketo Engage.

Para fazer isso, considere as etapas abaixo como parte do processo para obter uma experiência integrada de revisão e aprovação.

1. Configure seu projeto do Workfront com uma tarefa Pronto para revisão.
1. Acione o email do Marketo Engage para sincronizar com o Workfront com uma alteração de status de tarefa.
1. Converta seu arquivo de email Marketo Engage em prova revisável no Workfront.
1. Use a prova do Workfront para colaborar por meio de comentários e anotações.
1. Aprove o Workfront Proof para acionar a aprovação de ativos no Marketo Engage e marque a tarefa como concluída.

### Configurar um projeto do Workfront com uma tarefa Pronto para revisão {#configure-a-workfront-project-with-a-ready-for-review-task}

Uso [modelos de projeto](https://experienceleague.adobe.com/docs/workfront/using/manage-work/projects/create-and-manage-project-templates/project-template-overview.html){target="_blank"} para capturar a maioria dos processos, informações e configurações repetíveis associados aos projetos em sua organização. Você pode definir tarefas, colocar tópicos em fila, criar formulários personalizados e anexar documentos ao seu modelo.

No modelo de projeto no Workfront, inclua tarefas para revisar ativos que fazem parte da campanha de marketing. Além disso, você pode adicionar um processo de aprovação para lidar com aprovações únicas ou aprovações de vários níveis mais complexas.

Se quiser iniciar uma nova campanha de email, você deve ter um modelo de projeto que inclua uma tarefa para revisar o email, bem como um processo de aprovação para garantir que o email seja aprovado pela parte interessada correta antes que possa ser enviado.

![tela tarefas](assets/review-and-approve-blueprint-1.png){zoom=&quot;yes&quot;}

### Acione o email do Marketo Engage para sincronizar com o Workfront com a alteração de status da tarefa {#trigger-your-marketo-engage-email-to-sync-to-workfront}

Como parte do processo de revisão, você poderá sincronizar emails com seu projeto do Workfront depois que estiverem prontos para análise pela sua equipe de marketing. Para fazer isso, recomendamos configurar uma tarefa Ready to Review com um [status da tarefa](https://experienceleague.adobe.com/docs/workfront/using/manage-work/projects/update-work-on-a-project/update-task-status.html){target="_blank"} que significa quando o email está pronto para ser revisado. Em nosso exemplo, adicionamos uma opção Revisar status do Marketo Email na tarefa, que pode ser selecionada quando o rascunho de email estiver pronto para ser revisado pelas partes interessadas.

Com esse status em vigor no projeto do Workfront, você pode configurar o cenário do Workfront Fusion para acompanhar a tarefa Pronto para revisão e atualizar para &quot;Revisar email do Marketo&quot;. Depois de atualizado, o cenário pode recuperar o email de Marketo Engage como um arquivo de HTML, compactá-lo e salvar uma cópia dele nos documentos de projeto do Workfront a serem revisados.

![tela pronto para revisão](assets/review-and-approve-blueprint-2.png){zoom=&quot;yes&quot;}

### Converter seu email Marketo Engage em prova revisável no Workfront {#convert-your-marketo-engage-email-to-reviewable-proof-in-workfront}

Quando a tarefa Pronto para revisão é movida para o status &quot;Revisar email do Marketo&quot; e o email do Marketo Engage é salvo no Workfront, você pode configurar o cenário do Workfront Fusion para converter o email em uma Prova do Workfront.

### Use provas do Workfront para colaborar por meio de comentários e anotações {#use-workfront-proofing-to-collaborate}

[Prova do Workfront](https://experienceleague.adobe.com/docs/workfront/using/review-and-approve-work/proofing/proofing-overview/proofing-basics.html){target="_blank"} Os recursos do permitem que sua equipe de marketing pegue um novo ativo, como uma imagem ou um email, e colabore por meio de comentários e anotações. Quando uma prova estiver pronta para ser ativada, os tomadores de decisão poderão aprovar o ativo a partir da ferramenta de prova.

![converter tela de email](assets/review-and-approve-blueprint-3.png){zoom=&quot;yes&quot;}

### Aprovar prova o Workfront Proof e acionar a aprovação de ativos no Marketo Engage, marcar a tarefa como concluída {#approve-workfront-proof-and-trigger-asset-approval-in-marketo-engage}

O Workfront Fusion pode detectar quando o email foi aprovado pelas partes interessadas e enviar uma solicitação ao Marketo Engage para aprovar o email dentro do Marketo.

Com o email revisado/aprovado pelos membros da equipe certa, o email está pronto para entrar no Marketo Engage!

## Modelos de Cenário do Fusion {#fusion-scenario-templates}

Para ajudar a simplificar o desenvolvimento de workflows de revisão e aprovação em sua própria instância do Workfront e do Marketo Engage, criamos Modelos do Fusion que ajudarão você a começar a integração. Você pode utilizar esses modelos pesquisando &quot;Marketo&quot; na seção Modelos públicos do Fusion e baixando-os para sua instância.

### Revisar um email Prova de seu rascunho de email do Marketo Engage no Workfront {#review-an-email-proof-of-your-marketo-engage-email-draft-in-workfront}

O cenário de fusão abaixo o conduzirá durante a primeira metade do fluxo de revisão e aprovação, no qual o rascunho de email pode ser extraído do Marketo Engage e salvo no Workfront como uma prova. Depois de salvo como uma prova nos documentos do projeto do Workfront, ele pode ser revisado pelas partes interessadas de marketing, comentado e anotado como parte do processo de revisão.

![fluxo de análise e aprovação do cenário de fusão](assets/review-and-approve-blueprint-4.png){zoom=&quot;yes&quot;}

### Aprovar um email no Workfront que aciona a aprovação do ativo no Marketo Engage {#approve-an-email-in-workfront-that-triggers-approval}

O cenário de fusão abaixo pode ser usado para detectar quando uma Prova no Workfront foi aprovada e rotear essa aprovação para o Marketo Engage para atualizar o rascunho de email para que esteja ativo e pronto para ser usado em um programa Marketo Engage.

![aprovação de prova de cenário de fusão](assets/review-and-approve-blueprint-5.png){zoom=&quot;yes&quot;}

Juntos, esses dois cenários podem ser usados para criar um caminho bidirecional para transferir ativos de marketing do Marketo Engage para os workflows robustos de revisão e aprovação da Workfront, e enviar as aprovações de volta para o Marketo Engage do Workfront.
