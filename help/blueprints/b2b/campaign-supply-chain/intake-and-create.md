---
description: Entrada e criação - Otimize a cadeia de fornecimento de campanha com a Marketo e a Workfront
title: Tomar e criar
exl-id: 09679521-727c-4676-8e91-23d0b7fd54a2
source-git-commit: 2baa77bfe61abc1e4cf2aa9dbfe344f1b1e280ce
workflow-type: tm+mt
source-wordcount: '1325'
ht-degree: 0%

---

# Tomar e criar {#intake-and-create}

O número de solicitações de marketing que entram em uma equipe de operações de marketing para lançar novas campanhas pode transformar uma equipe de alto funcionamento em uma porta giratória de tarefas repetitivas, causando estagnação e esgotamento da inovação.

Ao estabelecer um processo para enviar solicitações de campanha e automatizar a criação de campanhas de marketing normalmente solicitadas, você pode: aumente a velocidade de suas campanhas, reduza erros, encaminhe solicitações para o membro certo das operações de marketing, equilibre e aprimore a utilização de recursos e concentre mais suas operações de marketing em tarefas mais estratégicas.

Com o Workfront e o Marketo Engage, uma conexão sistema a sistema permite detalhes de um [Formulário de solicitação do Workfront](https://experienceleague.adobe.com/docs/workfront/using/administration-and-setup/customize/custom-forms/create-or-edit-a-custom-form.html){target=&quot;_blank&quot;} para criar um Programa Marketo Engage, preencha as variáveis principais, como: linhas de assunto, cópia de email, imagens, datas, horas, informações do evento e muito mais.

Para obter essa integração, você usará o Workfront Fusion, uma camada de automação de trabalho que permite automatizar workflows entre o Workfront e outros sistemas.

O fluxo de trabalho abaixo mostra uma solicitação de webinar feita por um gerente de campanha usando um formulário de solicitação do Workfront. Os detalhes enviados na solicitação acionam um programa e email a serem criados no Marketo Engage para o webinário. Além disso, os detalhes são obtidos do formulário de solicitação para preencher o conteúdo do email.

![](assets/intake-and-create-1.png)

>[!TIP]
>
>Para saber mais sobre os diferentes tipos de objetos no Workfront usados para organizar a campanha de marketing e como ela é mapeada para um programa do Marketo Engage, verifique o [Visão geral do Marketo e Workfront](/help/blueprints/optimize-campaign-supply-chain-with-marketo-and-workfront/overview.md){target=&quot;_blank&quot;}.

## Prepare seu processo de desenvolvimento de campanha para automação {#prepare-your-campaign-development-process-for-automation}

Por trás de cada excelente automação de fluxo de trabalho está um processo definido que garante que as equipes e as partes interessadas obtenham o máximo valor da automação.

**Que tipos de solicitações de marketing você receberá?**

Pense em quais tipos de táticas de marketing você executará, como emails, criação, webinars primários e eventos. Você também executa webinars de terceiros ou anúncios de exibição? Cada uma dessas solicitações deve ser considerada, pois pode ser necessário campos de entrada específicos no formulário de solicitação e mapeará para diferentes modelos de programa no Marketo Engage que serão clonados.

Você também precisará entender se está executando campanhas em várias regiões. Se esse for o caso, você deverá contabilizar um Projeto no Workfront, criando vários programas no Marketo Engage, e cada programa representa suporte a idiomas diferentes.

É importante saber antecipadamente quais tipos de solicitações de marketing você espera receber para garantir que as solicitações possam ser facilitadas de maneira automatizada.

**Que informações devem ser capturadas na solicitação da campanha?**

Pense nas informações principais que precisarão ser capturadas no formulário de solicitação para cada uma das diferentes táticas executadas. Abaixo estão alguns exemplos de informações que podem ser capturadas em um formulário do Workfront para ajudar a automatizar o desenvolvimento da campanha.

<table> 
  <tr> 
   <td><b>Tático de marketing</b></td>
   <td><b>Informações para capturar</b></td>
  </tr>
  <tr> 
   <td>Explosão de email</td>
   <td>・ Assunto do email<br />
・ Data programada<br />
・ Cópia por e-mail<br />
・ Chamada à ação<br />
・ Imagens - Os URLs do AEM Assets podem ser referenciados diretamente para uso no Marketo<br />
・ Critérios de qualificação de público-alvo</td>
  </tr>
  <tr>
   <td>Webinar/Evento</td>
   <td>・ Nome do evento<br />
・ Data do evento<br />
・ Tempo do evento<br />
・ Cidade do Evento<br />
・ Descrição do evento<br />
・ Página de registro do webinar - PageURL OnDemand<br />
・ Nomes de alto-falante<br />
・ Títulos de alto-falante<br />
・ Imagens do alto-falante<br />
・ Emails necessários (Convite, Confirmação, Lembrete, Acompanhamento)<br />
・ Imagem(ões) de cabeçalho de email<br />
・ Critérios de qualificação de público-alvo</td>
  </tr>
  <tr>
   <td>Enfermeiro</td>
   <td>・ Número de emails<br />
・ Cópia por e-mail<br />
・ Cabeçalhos de email<br />
・ Chamada à ação<br />
・ Critérios de qualificação de público-alvo</td>
  </tr>
  </tbody>
</table>

>[!NOTE]
>
>Atualmente, a criação programática de públicos-alvo por meio da automação é limitada no Marketo Engage, pois os tokens não são compatíveis com as listas inteligentes. Isso significa que os públicos-alvo precisarão ser criados no Marketo Engage por um usuário ou, se você tiver um público-alvo predeterminado com o qual se comunica continuamente, poderá incluir uma lista inteligente configurada como parte do modelo de programa que é clonado durante o processo de automação.

### Estabeleça seu centro de excelência {#establish-your-center-of-excellence}

Se quiser automatizar a criação de programas, você precisará de um centro de excelência em Marketo Engage. Um centro de excelência inclui programas e ativos templatizados para ajudar a agilizar e padronizar o processo de desenvolvimento da campanha. Por exemplo, você pode ter um template de programa para suas diferentes necessidades de campanha: email, criação, evento presencial e webinário. Além disso, você pode ter vários modelos de programa de email que você usa para diferentes regiões ou diferentes tipos de anúncios de email.

Criar seu centro de excelência com modelos de programa no Marketo Engage é um dos primeiros passos para ter uma abordagem mais programática para a execução da campanha e atuará como uma base para automatizar as solicitações de campanha.

Depois de ter um conjunto de modelos de programa reutilizáveis, você pode dimensionar seus esforços usando a automação descrita neste blueprint para direcionar mais velocidade ao desenvolvimento de sua campanha.

Para saber mais sobre como criar seu próprio centro de excelência, consulte o [Comunidade Marketo](https://nation.marketo.com/t5/product-blogs/marketo-master-class-center-of-excellence-with-chelsea-kiko/ba-p/243221){target=&quot;_blank&quot;} para práticas recomendadas.

### Usar tokens para preencher conteúdo {#use-tokens-to-populate-content}

Com o Marketo Engage, os tokens podem ser usados para preencher o conteúdo nos ativos da campanha. Por exemplo, após clonar um template de email do seu centro de excelência, o Workfront Fusion pode obter detalhes da solicitação de campanha no Workfront e transmiti-los para os Meus tokens no programa Marketo Engage. Os valores de token podem então ser herdados diretamente no email para criar o email.

![](assets/intake-and-create-2.png)

### Preencher imagens do AEM Assets {#populate-images-from-aem-assets}

Você pode ainda automatizar o desenvolvimento de emails e páginas de aterrissagem utilizando tokens de Marketo Engage em combinação com links para ativos no AEM Assets. Os solicitantes do Campaign podem enviar links de imagem publicados do AEM Assets como parte do processo de solicitação. O Workfront Fusion pode então pegar esses links e incorporá-los ao HTML de um email usando Marketo Engage tokens.

Lembre-se, você precisará criar seus Programas e Modelos de Programa no Marketo Engage para utilizar Meus Tokens para que o Fusion possa atualizar os valores dos token com as informações enviadas no Workfront.

>[!NOTE]
>
>A AEM Assets não é necessária para suportar esse workflow, mas pode permitir um processo mais simplificado para gerenciar ativos da campanha na cadeia de suprimento de desenvolvimento da campanha.

### Montar uma biblioteca de pesquisa para todos os tipos de solicitação de programa {#assemble-a-lookup-library-for-all-program-request-types}

Ao automatizar a criação de novos programas do Marketo Engage a partir de solicitações do Workfront, é importante incluir uma etapa na automação do Workfront Fusion que possa obter informações da solicitação do Workfront e pesquisar os modelos de programa corretos que devem ser clonados no Marketo Engage.

Para fazer isso, você pode importar um conjunto de dados no Workfront Fusion que inclui uma lista de todos os diferentes modelos de programas no seu Marketo Engage center de excelência.

Algumas informações básicas a serem incluídas na Biblioteca de pesquisa do modelo de programa são:

<table> 
  <tr> 
   <td><b>Coluna</b></td>
   <td><b>Descrição</b></td>
  </tr>
  <tr> 
   <td>Tipo de campanha</td>
   <td>Pode ser email, webinário, criação, evento, webinar de terceiros, importação de lista etc. O Tipo de campanha atuará como uma descrição legível para o que está sendo solicitado.</td>
  </tr>
  <tr> 
   <td>Tipo de solicitação Workfront</td>
   <td>Esse é o tipo de solicitação selecionado no formulário do Workfront, que pode ser o mesmo tipo de campanha, como email, webinar, criação ou evento. Isso é usado para mapear a entrada selecionada no formulário Workfront para um Modelo de programa no Marketo.</td>
  </tr>
  <tr> 
   <td>ID de formulário do Workfront</td>
   <td>A ID exclusiva do formulário de solicitação de Workfront usado para validar a solicitação de gravação está sendo mapeada para o Modelo de programa do Marketo Engage.</td>
  </tr>
  <tr> 
   <td>ID do programa Marketo</td>
   <td>Esta é a ID do modelo de programa no Marketo Engage que mapeia para a solicitação que está sendo feita. Com essas informações prontamente disponíveis no Workfront Fusion permitirá que o Fusion faça a solicitação ao Marketo Engage e saiba exatamente qual programa clonar.</td>
  </tr>
  </tbody>
</table>

## Fluxo de assimilação e criação de automação {#intake-and-create-automation-flow}

Este é um exemplo de como a lógica do fluxo de trabalho pode ser montada em Fusion usando o pré-construído [Workfront](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/fusion-apps-and-modules/workfront-modules.html){target=&quot;_blank&quot;} e [Marketo Engage](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/fusion-apps-and-modules/marketo-modules.html)Módulos {target=&quot;_blank&quot;} que permitem fornecer automação mais rapidamente.

![](assets/intake-and-create-3.png)

## Recursos {#resources}

* [Módulos Adobe Marketo Engage](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/fusion-apps-and-modules/marketo-modules.html){target=&quot;_blank&quot;}

* [Módulos Adobe Workfront](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/fusion-apps-and-modules/workfront-modules.html){target=&quot;_blank&quot;}

* [Visão geral do Marketo e Workfront](/help/blueprints/optimize-campaign-supply-chain-with-marketo-and-workfront/overview.md){target=&quot;_blank&quot;}
