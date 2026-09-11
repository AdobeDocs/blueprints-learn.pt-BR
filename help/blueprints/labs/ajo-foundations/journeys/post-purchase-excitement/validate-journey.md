---
title: Validar jornada
description: Verifique a execução da jornada por meio de contagens de entrada e saída, relatórios de delivery de email e dados de serviço de consulta para eventos de etapa.
doc-type: article
solution: Experience Platform
exl-id: 2e6e73e5-6bd8-4dde-ba06-29b67f927131
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---


# Validar jornada

## Objetivo de aprendizado

Verifique se a jornada foi acionada e executada conforme esperado.  Verifique se os relatórios mostram as métricas atualizadas conforme esperado.

## Verificando sua jornada

1. Vá para a Jornada Pedido enviado, abra-a se a tiver fechado
2. Você vê pelo menos 2 perfis inseridos

   ![Contagem de Entradas de Perfil mostrada para a jornada](assets/validate-journey-profile-entered-count.png)

3. Clique em **Exibir relatório** -> **Últimas 24 horas** na parte superior direita.
4. Por padrão, você está na guia **Jornada** (no painel esquerdo)
   - Você verá algumas entradas e saídas (a contagem dependerá de quantos eventos você enviou, qualquer teste, erros etc.)

![relatório da guia Jornada mostrando entradas e saídas](assets/validate-journey-journey-tab-enters-exits.png)

Se tudo tiver sido limpo (role para baixo para verificar):

**estatísticas da Jornada**

3 Perfis inseridos (Henry, Você e o teste que fizemos)

Você pode clicar no botão de alternância na parte superior para **excluir eventos de teste**, se desejar, e você verá esses números serem alterados

3 Perfis encerrados (Henry, você e o teste que fizemos)

**Ações executadas e erros**

6 ações (3 emails, 3 GetShippingDetails)

**Motivos de erro de ações**

0 erros (espero)

**Eventos**

3 eventos (orderShipped)

3 eventos externos

5. Clique na guia **Email** (no painel esquerdo)
   - **Email - Desempenho de Envio**
     - Você vê alguns valores para **Entregue** e **Enviado** (a contagem dependerá de quantos eventos você enviou, erros etc.)
     - Esperamos que você não tenha erros (a menos que tenha encontrado alguns problemas anteriormente)
   - **Email - Estatísticas**
     - Email - 3 direcionados, enviados, entregues

   ![Guia Email mostrando desempenho e estatísticas de envio](assets/validate-journey-email-tab-sending-performance.png)

6. Verifique sua **caixa de entrada de email** e veja se recebeu o email (ele é semelhante a este abaixo)
   - *,* seu pedido enviou ETA: *10/17/2026* Número de Rastreamento: *051009364*

   >[!NOTE]
   >
   >Verifique se há Campanhas do AJO na sua pasta de spam [ajo-campaigns@email.dep-labs.com](mailto:ajo-campaigns@email.dep-labs.com)

   >[!NOTE]
   >
   >**Por que o nome está ausente?**
   >
   >Alteramos o nó Email para examinar o Contexto do evento para o endereço de email.  Mas o nome na personalização é extraído de \{\{profile.person.name.firstName\}\}.
   >
   >Quando você procura seu perfil para seu email, você tem um nome?



7. *Após 30-60 minutos*, você pode até mesmo verificar seu conjunto de dados no data lake com o seguinte: **Consultas** -> **Criar Consulta** -> **Copiar/Colar SQL** -> **Executar**

>[!NOTE]
>
>O evento de envio do pedido foi transmitido, portanto, embora ele atualize o perfil rapidamente, leva um tempo para que o data lake seja atualizado.

```sql
SELECT * FROM dep_orders
WHERE timestamp >= CURRENT_DATE
LIMIT 10
```

![Resultados do serviço de consulta para o conjunto de dados dep_orders](assets/validate-journey-query-service-dataset-results.png)

## Bônus (verificar eventos de etapa)

>[!NOTE]
>
>Eventos de etapa registram sempre que um perfil inicia uma jornada e cada etapa na jornada. Observação: pode levar alguns minutos para registrar esses eventos no conjunto de dados.



1. No Serviço de consulta, é possível visualizar o que o conjunto de dados de eventos da etapa está capturando executando este SQL. Copie o SQL abaixo e cole em uma query.

```sql
select timestamp,
  identityMap,
  _experience.journeyOrchestration.stepevents.journeyVersionName,
  _experience.journeyOrchestration.stepevents.NodeName,
  _experience.journeyOrchestration.stepevents.*
  from journey_step_events
limit 50
```

Os resultados têm mais de 100 colunas e dão uma ideia de quais registros de Eventos de etapa.

>[!NOTE]
>
>Curioso sobre o que cada campo significa, verifique o Dicionário de Esquemas do AJO e altere a lista suspensa para o esquema de Eventos de etapa do Jornada: [https://experienceleague.adobe.com/tools/ajo-schemas/schema-dictionary.html?lang=en](https://experienceleague.adobe.com/tools/ajo-schemas/schema-dictionary.html?lang=en)



## Recapitulação

A instância do jornada aparece nos relatórios ou logs do jornada e a ação configurada é executada
