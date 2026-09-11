---
hold: true
title: Ler um público-alvo
description: Saiba como usar a atividade Ler público-alvo com um Dimension de direcionamento de perfil em uma campanha orquestrada e testar como os perfis sem correspondência são descartados ao reconciliar dados relacionais.
doc-type: article
solution: Experience Platform
exl-id: f825efe9-4349-4195-a017-c956c15df946
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '1268'
ht-degree: 0%

---


# Ler um público-alvo

## Objetivo

No próximo conjunto de etapas, você criará uma campanha para ler um público-alvo do AEP e usá-lo junto com o Dimension do Profile Target criado anteriormente. Use a atividade Split para dividir os dados com base em uma condição. Por fim, teste a campanha para entender como esses públicos-alvo funcionam quando usados com o esquema relacional.

## Público-alvo de leitura

Este laboratório aborda o uso da atividade Read audience em conjunto com o esquema Relacional para enriquecimento.

O Orchestrated Campaign usa o schema relacional para todas as atividades. Ao usar a atividade Read audience, que lê o público-alvo do AEP, uma Entidade correspondente (Target Dimension) deve ser configurada para reconciliar o público-alvo com o Dimension do Campaign Target.

## Criar uma campanha

1. No painel lateral esquerdo, clique em **Campanhas**

![Navegação no painel esquerdo para Campanhas](assets/read-an-audience-navigate-to-campaigns.png)

&#x200B;2. Clique em **Criar campanha**

![Botão Criar campanha](assets/read-an-audience-create-campaign-button.png)

&#x200B;3. Selecione a **Orquestração - Marketing** e clique em **Confirmar**

![Orquestração - Seleção do tipo de campanha de marketing](assets/read-an-audience-select-orchestration-marketing.png)

&#x200B;4. Forneça os detalhes da campanha da seguinte maneira e clique no **botão Salvar**
   - Nome: **OC-RSL-ReadAudience-Test**
   - Descrição: **Teste de público-alvo de leitura RSL**

![Formulário de configurações da campanha com campos de nome e descrição](assets/read-an-audience-campaign-settings-form.png)

&#x200B;5. Aguardar a mensagem de confirmação

![Mensagem de confirmação após salvar as configurações da campanha](assets/read-an-audience-campaign-settings-confirmation.png)



## Adicionar atividade Ler público

1. Clique no(a) **+** dentro da tela para abrir o menu de opções e selecione **Ler público** nas **Atividades de direcionamento**

![Menu de atividades de direcionamento com a opção Ler público selecionada](assets/read-an-audience-add-read-audience-activity.png)

&#x200B;2. No painel de detalhes **Ler público-alvo**, clique no ícone Pesquisar para **Público-alvo**

![Ler o painel de detalhes do público-alvo com o ícone Pesquisa de público-alvo](assets/read-an-audience-search-audience-icon.png)

&#x200B;3. Selecione o público-alvo **dep: Membros Básicos do Plano** com Contagem de Perfis de **9** e clique em **Adicionar público-alvo**

![dep: público-alvo de Membros do Plano Básico selecionado com Contagem de Perfil de 9](assets/read-an-audience-select-basic-plan-members-audience.png)

&#x200B;4. Clique no menu suspenso da **Entidade** e selecione o `dep-rel: Customer Account - customer_id` Dimension de Destino da Campanha

![Menu suspenso Entidade com a Dimension de Destino de Conta de Cliente selecionada](assets/read-an-audience-select-entity-target-dimension.png)

>[!NOTE]
>
>Outros atributos também podem ser extraídos do Perfil do AEP para uso na tela usando o botão **Adicionar atributo**. Mas para esse laboratório, atributos extras não são necessários, então essa etapa é ignorada.



## Testar a campanha

1. As configurações para a atividade **Ler Público** estão preenchidas. Clique em **Iniciar** para executar a campanha no **Modo de teste**

![Botão Iniciar para executar a campanha no modo de Teste](assets/read-an-audience-start-test-mode.png)

>[!NOTE]
>
>Isso leva alguns minutos para ser executado.
>
>O modo de teste permite que a execução da campanha verifique e monitore seu comportamento junto com os resultados de cada atividade. As atividades são executadas sequencialmente até o final da tela.



&#x200B;2. A execução do teste é iniciada e os resultados são exibidos quando concluídos. Clique no nó **Resultado** e, em seguida, Visualize os resultados para ver os resultados da execução

![Nó de resultados com a opção Visualizar resultados](assets/read-an-audience-preview-test-results.png)

&#x200B;3. Observe que **2** (de 9) perfis do **Público-alvo de leitura** não têm uma **Dimensão de destino** correspondente do esquema relacional (isto é, eles existem no repositório de perfis, mas não no repositório relacional). E como a Campanha Orquestrada funciona no esquema Relacional, os `customer_id` (**2**) sem correspondência do **Público-alvo de leitura** são descartados e apenas os *correspondentes*, **7** neste caso, podem ser usados em atividades subsequentes que usam os **dados relacionais** na campanha

![Visualizar resultados mostrando perfis sem um Dimension de Destino correspondente](assets/read-an-audience-missing-target-dimension.png)

>[!NOTE]
>
>As etapas a seguir usam os dados relacionais para confirmar a instrução acima de `customer_id` sem correspondência sendo descartada.

&#x200B;4. Clique em **Parar** para parar o **Modo de teste** da campanha

![Botão Parar para encerrar o modo de Teste da campanha](assets/read-an-audience-stop-test-mode.png)

&#x200B;5. Clique em **+** no final do fluxo e adicione **Split** das **Atividades de direcionamento**

![Menu de atividades de direcionamento com a opção Dividir selecionada](assets/read-an-audience-add-split-activity.png)

&#x200B;6. No painel de detalhes da atividade **Split**, expanda a primeira divisão chamada **Subset**

![Dividir o painel de detalhes da atividade com o segmento Subconjunto expandido](assets/read-an-audience-expand-subset-split.png)

&#x200B;7. Renomeie-o para &quot;**No Repositório**&quot; e clique em **Criar filtro** para definir a condição de filtro

![Segmento renomeado como Em Repositório com a opção de filtro Criar](assets/read-an-audience-rename-in-store-segment.png)

&#x200B;8. No painel **Criar filtro** r, clique em **Adicionar condição**

![Criar painel de filtros com o botão Adicionar condição](assets/read-an-audience-add-condition-button.png)

&#x200B;9. Como nenhum outro atributo foi extraído do Perfil do AEP, o único atributo de Perfil do AEP disponível aqui é `Customer ID`. No entanto, as colunas do armazenamento relacional correspondente à dimensão de Destino correspondente estão disponíveis para configurar a condição de filtro. Expanda a **Dimensão de Direcionamento** clicando em **>**

![Dimensão de direcionamento expandida para mostrar colunas de repositório relacional](assets/read-an-audience-expand-targeting-dimension.png)

&#x200B;10. Selecione `Source` na lista e clique em **Confirmar**

![Atributo Source selecionado das colunas da Targeting dimension](assets/read-an-audience-select-source-attribute.png)

&#x200B;11. Os valores distintos da coluna Source estão disponíveis na lista suspensa. Para a **Condição personalizada**, selecione **&quot;Na Loja&quot;** na lista suspensa e clique em **Confirmar** para sair

![Condição personalizada definida como Na Loja](assets/read-an-audience-set-in-store-condition.png)

&#x200B;12. De volta ao painel de detalhes da atividade **Split**, as configurações da primeira Split são concluídas. Clique em **Adicionar segmento** à segunda divisão

![Botão Adicionar segmento no painel de detalhes da atividade de Divisão](assets/read-an-audience-add-segment-button.png)

Um novo segmento com o nome **Result** foi criado

![Novo segmento chamado Resultado](assets/read-an-audience-new-result-segment.png)

&#x200B;13. Renomeie &quot;**Result**&quot; para &quot;**Not In Store**&quot; e clique em **Criar filtro** para definir a condição de filtro

![Segmento renomeado para Fora do Repositório com a opção de filtro](assets/read-an-audience-rename-not-in-store-segment.png)

&#x200B;14. No painel **Criar filtro**, clique em **Adicionar condição**. Siga a mesma abordagem acima, expanda a **Dimensão de direcionamento** clicando em **>**, selecione `Source` na lista e clique em **Confirmar**

![Dimensão de direcionamento expandida para mostrar colunas de repositório relacional](assets/read-an-audience-expand-targeting-dimension.png)

![Atributo Source selecionado das colunas da Targeting dimension](assets/read-an-audience-select-source-attribute.png)

&#x200B;15. Para a **Condição personalizada**, selecione **&quot;Na Loja&quot;** na lista suspensa e, para o operador, selecione &quot;**não é igual a**&quot;. Clique em **Confirmar** para sair

![Condição personalizada definida como diferente de No Repositório](assets/read-an-audience-set-not-in-store-condition.png)

&#x200B;16. De volta ao painel de detalhes da atividade **Split**, as configurações das duas Divisões estão concluídas. Clique em **Iniciar** para executar a campanha no **Modo de teste**

![Botão Iniciar para executar a campanha no modo Teste após configurar a Divisão](assets/read-an-audience-start-test-mode-second-run.png)

&#x200B;17. A execução do teste começa e os resultados são exibidos após a conclusão. Como apenas **7** dimensão de Destino correspondente foi encontrada no esquema Relacional, a mesma contagem também é observada após as operações Split (**7** e **0**)

![Resultados de atividade dividida mostrando contagens de 7 e 0](assets/read-an-audience-verify-split-counts.png)

&#x200B;18. Clique em cada caixa de resultados e **Visualizar resultados** para exibir os resultados

![Opção Visualizar resultados para cada caixa de resultado de Divisão](assets/read-an-audience-preview-split-results.png)

&#x200B;19. Clique em **Parar** para parar o **Modo de teste** da campanha

![Botão Parar para finalizar a execução final do modo de Teste](assets/read-an-audience-stop-test-mode-final.png)

>[!NOTE]
>
>Enquanto o público de Leitura mostrava **9** perfis. Como criamos um filtro no Source e o campo Source existe no armazenamento relacional, tivemos que ingressar do armazenamento de perfil ao armazenamento relacional para verificá-lo. Quando foi unido ao esquema Relacional, por meio do Dimension do Target do Campaign, somente um total de **7** perfis correspondeu. Estas **7** IDs do cliente correspondentes estão disponíveis para uso nas atividades a seguir que tentam usar dados relacionais. Todas as **7** IDs do cliente tiveram `Source` definido como **&quot;Na Loja&quot;**, o que foi evidente pelos fluxos de Divisão.
>
>Portanto, manter a consistência dos dados é essencial ao usar os perfis do AEP juntamente com seus equivalentes relacionais para enriquecimento.

>[!TIP]
>
>Parabéns, isso conclui o laboratório sobre o uso da atividade Ler público com esquema relacional.

## Recapitulação

Agora você viu como é fácil criar uma campanha e executar uma atividade Ler público junto com o Dimension do Direcionamento de perfil para aproveitar o esquema relacional. Você usou a atividade Split para dividir o público com base em uma condição. Por fim, o modo de teste ajudou a entender que é importante ter a consistência de dados entre o Perfil e o esquema Relacional.

Você pode ler mais [aqui](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/campaigns/orchestrated-campaigns/design-campaigns/read-audience), se estiver interessado.
