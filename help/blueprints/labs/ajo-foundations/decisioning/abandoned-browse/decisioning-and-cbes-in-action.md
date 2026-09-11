---
hold: true
title: Decisão e CBEs em ação
description: Use o Postman para enviar eventos de experiência para perfis de teste e validar se a qualificação, a classificação e o limite de frequência retornam as ofertas corretas.
doc-type: article
solution: Experience Platform
exl-id: 540e50c9-bf39-49a4-ae63-c1d7b94f6b8c
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '2147'
ht-degree: 0%

---


# Decisão e CBEs em ação

## Objetivo

Agora que a Jornada está ativa, você pode começar a enviar eventos de experiência e ver as ofertas retornadas. Como as IDs de ano de nascimento e plano de telefone de perfis individuais afetam qual oferta é retornada, precisamos enviar Eventos de experiência para perfis pré-configurados com anos de nascimento e IDs de plano específicos.

## Perfis e configuração do Postman

Os três perfis que você usará já estão na sandbox e estão descritos nesta tabela:

| Nome | Sobrenome | Ano de nascimento | ID do plano | customerID | ECID | Email |
| ---------- | ------------ | ---------- | ------- | ---------- | -------------------------------------- | --------------- |
| Bob | Básico | 1974 | 1 | 287415903 | 34566216966446312560595171785271630085 | bob\@dep.com |
| Peter | Profissional | 1981 | 2 | 105946728 | 22344522145769262754334953788432801285 | peter\@dep.com |
| Ursula | Ultimate | 2002 | 3 | 730682145 | 35615467908312308343036144243711275069 | ursula\@dep.com |

Localizar esses perfis no AEP

1. Se necessário, expanda o item **Cliente** no painel esquerdo e clique em **Perfis**
1. Clique na guia **Procurar** e, entre todos os perfis que já foram criados para você ou que você criou como parte dos laboratórios anteriores, você verá estes três perfis.

Encontre os eventos de experiência correspondentes para cada perfil na coleção do Postman

1. Se necessário, abra o Postman
1. Verifique se as variáveis de ambiente **EDGE\_REGION** e **DATASTREAM\_CONFIG** ainda estão definidas. Se precisarem ser definidos novamente, analise as etapas no laboratório &quot;Importar ambiente e coleção&quot;.
1. Expanda a pasta **Laboratório de decisão**. Você vê dois eventos de experiência para cada perfil:

![Pasta do Laboratório do Postman Decisioning mostrando dois Eventos de Experiência por perfil](assets/decisioning-and-cbes-in-action-postman-collection-folder.png)

## Envio em eventos de experiência

&#x200B;> [!IMPORTANT]
>
>Não ignore a explicação do texto de abertura desta seção!

Com tempo e recursos ilimitados, teríamos que criar e implantar uma biblioteca de tags com o AEP Web SDK em um site real. Isso demonstraria como recuperar e relatar ofertas. No entanto, dada a amplitude e a profundidade do conteúdo coberto nesses laboratórios, optamos por pré-criar os Eventos de experiência necessários para entrar na Jornada, recuperar ofertas e relatar essas ofertas em uma coleção do Postman, em vez de exigir que você marque um site. Quando usada corretamente, esta coleção imita como um site com tags apropriadas (ou qualquer canal digital) usaria o canal de delivery do CBE em uma Jornada.

A abordagem recomendada para implantações do AEP Web SDK é usar uma abordagem de duas chamadas por página. Nesse padrão, o Web SDK envia uma chamada de &quot;busca&quot; na parte superior da página para a Edge que solicita todas as personalizações necessárias para o usuário. Essas personalizações são retornadas pela Edge e, em seguida, renderizadas pela Web SDK. Uma segunda chamada na parte inferior da página, normalmente chamada de Coleta de dados, é enviada para a Edge e relata o que foi mostrado ao usuário final, juntamente com outros dados para o Analytics, o CJA e outras soluções. Quando se trata de recuperar apresentações da Edge, lembre-se de um simples mnemônico: FAR, que significa Buscar, Aplicar e Relatar. Todas as apresentações devem ser buscadas, aplicadas ou renderizadas (mostradas ao usuário final) e, em seguida, relatadas. É importante que essas ofertas sejam relatadas como vistas para que as regras de limite de frequência funcionem.

As atividades do Adobe Target e o Canal da Web da AJO podem ter suas respostas buscadas e aplicadas automaticamente pelo AEP Web SDK. Seus relatórios também podem ser enviados com a chamada de Coleta de dados na parte inferior da página. No entanto, os CBEs são diferentes. O AEP Web SDK pode buscar as apresentações, mas cabe ao cliente aplicar (renderizar) o que for retornado e usar o AEP Web SDK para relatar o que foi mostrado. Um CBE normalmente não usa as chamadas de coleta de dados para relatar o que foi mostrado, portanto, elas devem ser passadas manualmente.

Na coleção do Postman, você verá que cada perfil tem duas chamadas de evento de experiência

Um Evento de experiência de busca no início da página

Um evento de experiência de coleta de dados no final da página

O Evento de experiência do início da página inclui o parâmetro &quot;jsonOfferContainer&quot; na solicitação, que é o &quot;Local na página&quot; configurado para o CBE. Além disso, essa chamada usa a funcionalidade de script do Postman para obter a resposta da Edge e, em seguida, enviar imediatamente uma segunda chamada para o Edge relatando que a oferta foi mostrada ao usuário final. Não há aplicação real ou renderização da oferta porque não há nenhum site para este laboratório. Mas, da perspectiva do AJO, a oferta foi retornada e relatada como vista.

A chamada de coleta de dados do final da página é meramente para gerar uma visualização de página para a página de visão geral do iPhone 17. Lembre-se de que o segmento para entrar na própria Jornada requer três visualizações dessa página. Depois que o Evento de experiência for enviado em 3 vezes, esse usuário informará a Jornada e somente o Evento de experiência de busca do início da página será necessário para obter a oferta e relatar que ela foi vista.

Comece com o perfil do Bob.

1. Clique na solicitação **Bob - Coleção de dados final da página**.
2. Clique na guia **Body** e observe os parâmetros que estão sendo transmitidos, como o namespace customerID no IdentityMap, que indica que ele está autenticado, bem como o parâmetro &#39;web.webPageDetails.name&#39; que é transmitido no nome de página de &#39;phones\:apple\:iphone 17\:overview&#39;.

![Bob - corpo da solicitação de Coleta de Dados Final da Página no Postman](assets/decisioning-and-cbes-in-action-bob-page-bottom-request.png)

&#x200B;3. Clique em **Enviar** no canto superior direito para enviar uma exibição de página. Você recebe uma resposta semelhante a esta

![Resposta recebida após o envio do evento Bob&#39;s Page Bottom Data Collection](assets/decisioning-and-cbes-in-action-bob-data-collection-response.png)

&#x200B;4. Depois de receber uma resposta adequada, clique em **Enviar** novamente para reenviar o mesmo evento de fim de página pela segunda vez. Aguarde alguns segundos e envie uma chamada da 3ª Coleção de dados para o perfil Bob. Você enviou um total de 3 chamadas de fim de página.

Nesse ponto, o sistema está processando essas ocorrências e adicionando Bob ao segmento de transmissão &quot;dep: Interested in iPhone 17&quot;. Feito isso, Bob é colocado na Jornada. Uma vez na Jornada, leva apenas alguns minutos para a entrada de Bob na Jornada e no segmento ser projetada para a loja de perfis da Edge para Bob.

&#x200B;5. Retorne à interface do usuário do AJO e clique em **Perfis** no painel esquerdo, seguido pela guia **Procurar**.
&#x200B;6. Procure o perfil de Bob usando o namespace **customerID** com o valor de **287415903**.

![Procurando o perfil de Bob usando o namespace customerID](assets/decisioning-and-cbes-in-action-search-bob-profile.png)

&#x200B;7. Clique em **Exibir** para abrir o perfil do Bob (a cor do perfil do Bob pode ser diferente da mostrada na captura de tela).

![Página de perfil do Bob aberta no AJO](assets/decisioning-and-cbes-in-action-bob-profile-opened.png)

&#x200B;8. Quando o perfil de Bob for aberto, clique na guia **Associação de público-alvo** e você verá que Bob agora é um membro do segmento &quot;dep: Interessado no iPhone 17&quot;, pelo menos da perspectiva do AEP Hub.
&#x200B;9. Clique em **Atributos** e selecione o botão de opção **Edge** para alternar para o modo de exibição do Edge.

![Guia Atributos com o botão de opção Edge para alternar a exibição de perfil](assets/decisioning-and-cbes-in-action-edge-view-toggle.png)

>[!WARNING]
>
>Há um erro na interface do usuário infeliz que requer que você clique na guia Atributos para alternar o botão de opção para Edge.



&#x200B;10. Clique novamente em **Associação de público-alvo** e, se você tiver feito essas etapas com rapidez suficiente, verá que a Edge está selecionada e mostrará que Bob não tem associação de público-alvo

![A exibição do Edge do perfil de Bob ainda não mostra nenhuma associação de público-alvo](assets/decisioning-and-cbes-in-action-edge-audience-membership-empty.png)

&#x200B;11. Em uma nova guia do navegador, navegue até a Jornada criada e clique nela. Você pode ver que um perfil entrou na Jornada e agora está no nó CBE.

![Tela de Jornada mostrando o perfil de Bob inserido e no nó CBE](assets/decisioning-and-cbes-in-action-bob-enters-journey.png)

Neste ponto, Bob entrou na Jornada e a projeção do Edge está montando uma projeção que atualiza o perfil de Bob na Edge.

&#x200B;12. Volte para o Postman e clique na segunda das chamadas de evento de experiência do Bob, **Bob - Busca no Topo da Página.**
&#x200B;13. Clique em **Enviar**. O que deveria acontecer?
    - Se o perfil do Edge de Bob ainda não tiver sido atualizado, você receberá uma resposta muito semelhante ao que recebeu da chamada de Coleta de dados. Se esse for o caso, aguarde mais um ou dois minutos e tente enviar a chamada de Bob&#39;s Page Top Fetch novamente.
    - Se o perfil do Edge de Bob foi atualizado, você receberá uma resposta com o JSON que foi configurado anteriormente, juntamente com informações adicionais usadas para os relatórios. Mas, antes de seguir em frente, que oferta do iPhone 17 Bob deve ser oferecido?

      Bob nasceu em 1974, que é maior que 1966, então ele teria se qualificado para o critério de fórmula de 2º ranking, e suas pontuações de prioridade de oferta Generic, Base e Pro teriam sido multiplicadas por 100, dando a essas ofertas pontuações de 100, 200 e 300, respectivamente. No entanto, Bob Basic tem um ID de plano 1, portanto, ele não está qualificado para as ofertas de nível Ultra ou Pro graças à regra de Decisão. Portanto, a oferta de camada Base, que tem uma pontuação de 200, seria exibida. Você pode ver isso na resposta (provavelmente será necessário rolar a tela para baixo):

![Resposta do Postman mostrando a oferta da camada Base retornada para Bob](assets/decisioning-and-cbes-in-action-bob-base-offer-response.png)

&#x200B;14. Lembre-se de que essa solicitação do Postman envia automaticamente uma notificação de exibição para essa oferta. Portanto, o AJO já gravou pelo menos uma impressão para essa oferta. Clique em **Enviar** novamente para enviar uma segunda impressão. Verifique se a oferta base foi retornada novamente.
&#x200B;15. Lembre-se de que um limite de frequência de 3 impressões se aplica aos modelos de nível Base, Pro e Ultra. Clique em **Enviar** pela terceira vez para obter uma terceira resposta com a camada Base e gravar outra impressão.
&#x200B;16. Clique em **Enviar** uma quarta vez e o que deve acontecer? O limite de frequência para a oferta da camada Base é atingido e você recebe a oferta Genérica na resposta:

![Resposta do Postman mostrando a oferta Genérica retornada após o limite de frequência ser atingido](assets/decisioning-and-cbes-in-action-bob-generic-offer-after-cap.png)

&#x200B;17. Clique em **Enviar** novamente e você verá a oferta da camada Genérica. Você pode clicar em Enviar mais 100 vezes e receber a mesma oferta de volta até o dia seguinte, quando o limite de frequência for redefinido.

>[!WARNING]
>
>Lembre-se de que no AJO, o dia é reiniciado à meia-noite GMT. Se você enviasse outra chamada de busca após a meia-noite GMT, veria a oferta da camada base retornar.

&#x200B;18. Retorne à interface do usuário do Journey Orchestration e clique na Jornada **Abandonar navegação do iPhone 17** que você criou. Como a Jornada é publicada e publicada em tempo real, você começa a ver as estatísticas. Você pode ver que 1 perfil entrou na Jornada e está atualmente no nó CBE.

![Relatórios de Jornada mostrando um perfil atualmente no nó CBE](assets/decisioning-and-cbes-in-action-bob-enters-journey.png)

>[!NOTE]
>
>Nesse ponto, você pode estar se perguntando por que o perfil não está no nó de espera. Depois de atingir o nó CBE e projetar as atualizações para o perfil do Edge de Bob, ele deve estar no nó de espera? A resposta curta é que poderia ser, mas... também se pode argumentar que, como o CBE está sendo ativamente retornado, é aí que Bob está nessa Jornada. Mas, depois de 3 dias, a Jornada mostrará que o perfil concluiu a Jornada sem nunca estar realmente no nó de espera.

## Enviar eventos de experiência para outros perfis

Agora que você viu a Jornada funcionando para o perfil do Bob, há dois outros perfis a serem testados.

1. Retorne à Postman e localize os eventos de Experiência para Peter e Ursula.
2. Execute o evento &quot;Coleta de dados no final da página&quot; 3 vezes para cada perfil, lembrando de 1 a 3 segundos entre cada solicitação de coleta de Enviar/Dados.
3. Aguarde alguns minutos para que os três perfis se qualifiquem para o segmento de transmissão, insira a Jornada e projete o CBE nos perfis do Edge.
4. Envie a chamada de Busca superior da página quantas vezes forem necessárias para verificar se as regras de decisão e as fórmulas de Classificação estão funcionando como esperado.

**Perfis de decisão: comportamento esperado**

| Nome | Sobrenome | 1ª oferta | 2ª oferta | 3ª oferta | 4ª oferta |
| ---------- | ------------ | --------- | --------- | --------- | --------- |
| Bob | Básico | Base | Genérico | Genérico | Genérico |
| Peter | Profissional | Pro | Base | Genérico | Genérico |
| Ursula | Ultimate | Ultra | Pro | Base | Genérico |

&#x200B;5. Quando terminar, retorne à Jornada. Você vê que todos os três perfis entraram na Jornada e estão no nó CBE.

>[!NOTE]
>
>Se você aguardasse 3 dias e reenviasse o Início da busca de página, descobriria que nenhuma oferta foi retornada e que todos os três perfis concluíram a Jornada

## Recapitulação

Nesta página final do laboratório, você foi para a fase de execução, onde testou sua configuração de decisão usando eventos de experiência e um canal de experiência baseada em código (CBE). Você usou o Postman para enviar eventos de experiência simulados para o Adobe Journey Optimizer para que:

- Os perfis entraram na jornada criada porque atendiam aos critérios do segmento de streaming.
- O canal CBE foi chamado com eventos de busca para obter decisões de oferta com base nos dados do perfil (ano de nascimento, plano de telefone etc.).
- As ofertas eram retornadas e contadas em relação aos limites de frequência conforme configurados, mostrando como regras e lógicas de classificação diferentes afetavam qual oferta era entregue.
- Você verificou que o limite de frequência e a qualificação funcionavam conforme esperado ao enviar repetidamente chamadas de busca de oferta.

Você executou chamadas de decisão reais e validou se suas regras de qualificação, fórmulas de classificação e configuração de oferta se comportam corretamente quando os perfis interagem com o mecanismo de decisão.
