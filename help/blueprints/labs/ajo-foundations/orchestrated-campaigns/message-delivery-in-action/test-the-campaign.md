---
hold: true
title: Testar a campanha
description: Saiba como executar uma Campanha orquestrada no modo de teste e interpretar por que um canal de email baseado em perfil do AEP produz erros de entrega que um canal baseado em relação evita.
doc-type: article
solution: Experience Platform
exl-id: e77ae8ab-f18f-4683-8fdd-ba4f4629d96c
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 0%

---


# Testar a campanha

## Objetivo

No próximo conjunto de etapas, você executará a campanha no modo de teste para confirmar as funções da campanha, conforme esperado, antes de publicá-la. Nesse caso, o modo de teste não envia emails, mas ajuda a verificar todo o fluxo e identificar problemas antecipadamente.

## Iniciar o fluxo de trabalho

1. Após configurar os dois fluxos de email, a Campanha é semelhante à seguinte. Clique no botão **Iniciar** para executar a campanha no **Modo de teste**

![Clique em Iniciar para executar a campanha no modo de Teste](assets/test-the-campaign-click-start-test-mode.png)

>[!NOTE]
>
>Conforme mencionado no laboratório anterior, o modo Test permite validar a execução da campanha e os resultados das várias atividades. Cada atividade é executada sequencialmente até que o fim do fluxo seja atingido.



&#x200B;2. A execução do teste de todas as atividades da campanha é iniciada, verifique os resultados

![Execução de teste de atividades de campanha em andamento](assets/test-the-campaign-verify-execution-results.png)



## Relatório de email #1

1. Para testar a entrega de email, clique na atividade **Enviar email usando o atributo de perfil** e, no painel direito, clique em **Executar teste**

![Executar teste para email usando a atividade de atributo de perfil](assets/test-the-campaign-run-test-profile-attribute.png)

&#x200B;2. Aguarde a mensagem de confirmação e clique em **Exibir relatório** para ver os detalhes do teste de email

![Clique em Exibir relatório para ver os detalhes do teste de email](assets/test-the-campaign-view-report-1.png)

&#x200B;3. A página Email report é apresentada com as estatísticas da campanha e o status da execução. O teste de Email é uma verificação da atividade para garantir que não haja erros e não envie emails. Normalmente, leva aproximadamente \~**5** minutos para ser concluído.

![Página do relatório de email com estatísticas do Campaign](assets/test-the-campaign-campaign-statistics-1.png)

>[!NOTE]
>
>Talvez seja necessário atualizar a página algumas vezes para ver o resultado final do teste.



&#x200B;4. Quando o teste de Email estiver concluído, os resultados serão apresentados. Há alguma porcentagem de erros; clique em **Exibir mais** para saber o motivo.

![Taxa de erros com Exibir mais links](assets/test-the-campaign-error-rate-view-more.png)

&#x200B;5. Os estados de motivo `Email address not found in profile`

![Motivo: endereço de email não encontrado no perfil](assets/test-the-campaign-email-not-found-reason.png)

>[!NOTE]
>
>Como o **Endereço de entrega** configurado para a atividade Email, o **Email usando o atributo Perfil**, foi configurado para usar o atributo Perfil `personalEmail.address`, ele criou uma dependência no **Perfil do AEP**.
>
>Das **38** IDs de clientes qualificados do esquema relacional, o sistema encontrou apenas **7** Perfis correspondentes do AEP. Para os **31** restantes, os Perfis do AEP não existiam, o que resultou na mensagem de erro `Email address not found in profile`.
>
>É importante lembrar que os dados no datalake e no armazenamento relacional são mantidos **consistentes** ao usar os atributos do Perfil do AEP em campanhas orquestradas.



## Relatório de email #2

1. Repita o mesmo processo para a atividade **Email usando Dimension de Destino**

![Executar teste para Email usando atividade do Dimension do Target](assets/test-the-campaign-run-test-target-dimension.png)

&#x200B;2. Aguarde a mensagem de confirmação e clique em **Exibir relatório** para ver os detalhes do teste de email

![Clique em Exibir relatório para ver os detalhes do teste de email](assets/test-the-campaign-view-report-2.png)

&#x200B;3. Quando o teste de Email estiver concluído, os resultados serão apresentados. Nesse caso, não haverá erros

![Estatísticas de campanha sem erros](assets/test-the-campaign-campaign-statistics-2.png)

>[!NOTE]
>
>Como o **Endereço de entrega** da atividade de email **Email usando Dimension de Destino** foi configurado para usar o `dep_rel_customer_account.email`, do esquema Relacional, não havia dependência nos Perfis AEP ou em seus atributos.
>
>Descobriu-se que todas as **38** IDs de clientes qualificadas tinham emails correspondentes no repositório Relacional e podiam ser direcionadas com êxito sem erros.



## Interromper o fluxo de trabalho

Clique no botão **Parar** para parar o **Modo de teste** da campanha

>[!TIP]
>
>Ambas as configurações de canal de email foram testadas na mesma campanha, e foram observadas diferenças entre o uso de um atributo de perfil do AEP e o uso do Target Dimension na configuração do canal de email.
>
>Parabéns, isso conclui o laboratório de Entrega de mensagens.

## Recapitulação

Agora você viu como testar a campanha criada para entender o fluxo e o comportamento. Aqui, as nuances de usar as diferentes configurações para a configuração do canal de email eram bem compreendidas durante a execução do fluxo de teste.

Você pode ler mais sobre o modo de teste de campanha [aqui](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/orchestrated-campaigns/launch/start-monitor-campaigns), se estiver interessado.
