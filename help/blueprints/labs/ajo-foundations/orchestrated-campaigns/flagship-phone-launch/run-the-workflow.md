---
title: Executar o fluxo de trabalho
description: Saiba como executar um fluxo de trabalho do Orchestrated Campaign no modo de teste e solucionar problemas do motivo pelo qual alguns registros são descartados de um envio de SMS devido à falta de junções de dimensões de destino.
doc-type: article
solution: Experience Platform
exl-id: c3b35b27-92ae-44ca-a5fb-3f76990f9db4
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%
---

# Executar o fluxo de trabalho

## Objetivo

Nas próximas etapas, você aprenderá a testar seu fluxo de trabalho e, mais importante, sua atividade de SMS usando o modo de teste.



## Verificar fluxo de trabalho

1. Quando você termina, o fluxo de trabalho final é semelhante ao seguinte. Verifique se tudo está bem. Você verá:

   ![Tela final de fluxo de trabalho pronta para teste](assets/run-the-workflow-final-workflow-canvas.png)

2. Se você ainda não interrompeu o fluxo de trabalho, clique no botão **Parar** na parte superior direita.

   ![Botão Parar na parte superior direita do fluxo de trabalho](assets/run-the-workflow-click-stop-button.png)

   >[!NOTE]
   >
   >Opcionalmente, tente clicar no botão Reiniciar, mas é provável que você veja um erro, pois adicionou atividades após a criação do fluxo de trabalho e seu cache não é mais válido.



3. Clique no botão **Iniciar** para executar e testar o fluxo de trabalho de ponta a ponta

   ![Botão Iniciar para executar o teste de fluxo de trabalho](assets/run-the-workflow-click-start-button.png)



4. Revise o resultado que entra na atividade de SMS clicando em **Resultado** (há dois Resultados, portanto, use o esquerdo como mostrado abaixo) e, em seguida, no painel esquerdo clicando no botão **Visualizar resultados**.

   ![Transição de Resultado Deixada selecionada antes da atividade de SMS](assets/run-the-workflow-select-result-transition.png)

   ![Botão Visualizar resultados no painel direito](assets/run-the-workflow-click-preview-results.png)



5. Você vê **33 registros** e o targeting dimension corresponde à ID do cliente (a chave de junção para o perfil)

![33 registros com targeting dimension correspondente à ID do cliente](assets/run-the-workflow-33-records-customer-id.png)



## Testar a atividade de SMS

1. Feche a janela anterior, clique na **atividade de SMS** e clique no botão **Executar teste** no painel direito

   ![Botão Executar teste na atividade de SMS](assets/run-the-workflow-click-run-test-sms.png)



2. Quase imediatamente, um novo botão aparece rotulado **Exibir relatório**.  Clique no botão **Exibir relatório** para iniciar na tela do relatório.

   ![Botão Exibir relatório para o teste de atividade de SMS](assets/run-the-workflow-click-view-report.png)

   >[!NOTE]
   >
   >Essa tela não é preenchida inicialmente, pois leva algum tempo para executar a execução de teste. Talvez seja necessário atualizar algumas vezes antes de ver os resultados.



3. Ao obter resultados, você verá que 100% foram direcionados!

   ![Resultados de envio de teste de SMS mostrando 100% de direcionamento](assets/run-the-workflow-100-percent-targeted.png)

   *Aguarde, um minuto... o resultado recebido foi de 33 registros, então para onde foram os 4?*



4. Volte para a tela do fluxo de trabalho e clique na transição **Resultado** que entra na atividade de SMS e clique em **Visualizar resultados** no painel direito.

   ![Revendo os resultados da transição após o teste de SMS](assets/run-the-workflow-recheck-transition-results.png)



5. Na tela Preview results, role até o final da tabela e observe que **4 registros** têm uma **Targeting dimension em branco**.

![4 registros com uma targeting dimension em branco na parte inferior da tabela](assets/run-the-workflow-4-records-missing-dimension.png)



## Explicação

Aqui está o que aconteceu.

- Você tinha 33 linhas de clientes para as quais queria enviar uma mensagem SMS
- Depois que a atividade 4 de dimensão de alteração dessas linhas de cliente não tinha nenhuma conta de cliente associada
- A associação ao Perfil de cliente em tempo real exige uma ID do cliente e, como não há nenhuma nesses 4 registros, não há como pesquisar um perfil ou criar um novo imediatamente

Resultado —> Campanhas orquestradas descartam esses 4 registros na execução da mensagem

>[!NOTE]
>
>Há um aprimoramento chegando para ajudar a resolver esse problema de duas maneiras:
>
>1. Verifique se um log de exclusão foi criado para registros que não têm um targeting dimension no envio
>2. Atualize a atividade Change dimension para fazer uma associação interna e uma externa, o que descartaria esses 4 registros antecipadamente

>[!SUCCESS]
>
>Parabéns! Agora você está oficialmente certificado para lançar suas próprias Campanhas Orquestradas e transmitir mensagens para o mundo, de maneira responsável. Agora você pode comercializar com confiança!



## Publicação do workflow

Você não fará isso no laboratório, mas pelo contexto, veja o que acontece no momento da publicação:

1. O agendador entra em ação se a campanha tiver um agendamento definido
1. As atividades Salvar público-alvo criam o shell de público-alvo no Portal de público-alvo e os perfis qualificados começam a assimilar
1. A execução da mensagem começa para a primeira atividade de mensagem no workflow
   - Pesquisas de perfil ocorrem em relação ao instantâneo de Perfil
     - Os perfis correspondentes respeitam o consentimento encontrado no perfil
     - Os perfis não correspondentes são criados em tempo real
   - Os logs de entrega são criados no `AJO Message Feedback Event Dataset`
