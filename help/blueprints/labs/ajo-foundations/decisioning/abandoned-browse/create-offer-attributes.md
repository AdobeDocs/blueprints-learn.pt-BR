---
hold: true
title: Criar atributos de oferta
description: Adicione atributos personalizados do dispositivo, como marca, modelo e camada ao esquema XDM da oferta padrão para uso na classificação e nas regras de qualificação.
doc-type: article
solution: Experience Platform
exl-id: 00326a7c-8139-46f5-85bd-5ea1f63f29cf
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 0%

---


# Criar atributos de oferta

## Objetivo

Nesta seção, você adicionará campos XDM personalizados ao esquema XDM de oferta padrão. Esses campos personalizados podem ser usados em critérios de classificação, classificação e qualificação. Eles também podem ser dados retornados para o dispositivo solicitante.

## Criar objeto pai de dispositivo personalizado

1. Expanda o item de menu **Decisão** no painel esquerdo, se necessário, e clique em **Catálogos.**
2. Por padrão, a página &quot;Ofertas&quot; é exibida. Clique no botão **Editar esquema** no canto superior direito.

![Botão Editar esquema na página Catálogo de ofertas](assets/create-offer-attributes-edit-schema-button.png)

>[!TIP]
>
>A página resultante é o editor de esquema XDM padrão. Assim como o XDM é usado para definir a estrutura de dados dos conjuntos de dados, o XDM é usado aqui para definir os atributos de uma oferta.

>[!NOTE]
>
>O esquema &quot;Itens de oferta personalizados - Experience Decisioning&quot; é um esquema padrão gerado pelo sistema que se aplica a todas as ofertas. No entanto, é possível adicionar itens a esse esquema para atender a necessidades de negócios exclusivas, que é o que você fará nesta seção.
>
>Além disso, percorrer a página de ofertas é um atalho para acessar esse esquema. Você também pode acessá-lo por meio do menu Esquema no painel esquerdo.

&#x200B;3. Clique no ícone **+** à direita do nível raiz do esquema e, usando o menu &quot;Propriedades do Campo&quot; agora visível no painel direito, preencha os seguintes campos com os valores fornecidos:
   - Nome do campo: **dispositivo**
   - Nome de exibição: **Dispositivo**
   - Lista suspensa de tipos: **Objeto**
   - Atribuir ao Grupo de Campos (digite este valor em): **Detalhes da Oferta**

>[!NOTE]
>
>O Grupo de campos Atribuir a parece ser uma lista suspensa, mas também aceita entrada de texto direta; portanto, insira o texto &#39;Detalhes da oferta&#39;. Ao digitá-lo, você vê um item &quot;Detalhes da oferta (Novo)&quot; também aparecer. Qualquer novo atributo deve ser atribuído a um grupo de campos, portanto, nesta etapa, você está criando um novo grupo de campos chamado Detalhes da oferta.

&#x200B;4. Verifique se todas as propriedades foram preenchidas como a captura de tela abaixo:

![Propriedades de campo do novo objeto Dispositivo preenchidas](assets/create-offer-attributes-device-object-field-properties.png)

&#x200B;5. Depois de verificar que todos os campos estão corretos, clique no botão azul **Aplicar**, na parte inferior do menu &#39;Propriedades do campo&#39; (painel direito), para ver as alterações aplicadas ao esquema:

![Grupo de campos de dispositivo aplicado ao esquema de oferta](assets/create-offer-attributes-device-object-applied.png)

>[!TIP]
>
>Assim como o XDM normal, os atributos personalizados são agrupados em um namespace específico para a organização IMS, ou seja, a ID de locatário imsorg ou &quot;dep&quot; neste caso. Você também vê que o novo grupo de campos &quot;Detalhes da oferta&quot; agora está listado no painel &quot;Composição&quot;, à esquerda do esquema.

>[!WARNING]
>
>Observe que essas alterações NÃO são salvas. Eles são apenas &#39;Aplicados&#39;. Se você saísse da página sem salvar, perderia seu trabalho. Conclua as etapas desta seção antes de sair.

## Criar atributos personalizados do dispositivo

Agora que o objeto XDM do dispositivo foi criado, você pode continuar criando campos específicos do dispositivo.

1. Clique no ícone **+** à direita do novo objeto **dispositivo** que você acabou de criar e, usando o menu &#39;Propriedades de Campo&#39; no painel direito, preencha os seguintes campos com os valores fornecidos:
   - Nome do campo: **make**
   - Nome de exibição: **Marca**
   - Lista suspensa de tipos: **Cadeia de caracteres**
   - Atribuir ao Grupo de Campos: **Detalhes da Oferta** (já deve estar selecionado)
   - Depois de verificar que todos os campos estão corretos, clique no botão azul **Aplicar** para ver as alterações aplicadas ao esquema
2. Repita as etapas anteriores para adicionar dois atributos adicionais para **Modelo** e **Camada**. Use o mesmo padrão de nomenclatura, tipo e grupo de campos. Quando terminar, o esquema deverá ter esta aparência:

![Esquema de oferta mostrando os campos Marca, Modelo e Camada preenchidos](assets/create-offer-attributes-make-model-tier-fields.png)

&#x200B;3. Com todos os novos campos/atributos XDM criados, clique em **Salvar** no canto superior direito e você receberá uma mensagem verde &quot;Esquema salvo com êxito&quot; na parte inferior da tela. Agora você concluiu as etapas desta seção.

>[!WARNING]
>
>O schema que você acabou de atualizar se aplica a TODAS as ofertas, incluindo todas as ofertas futuras. Tenha muito cuidado ao adicionar atributos a este esquema. No nosso caso de uso de exemplo de uma empresa de telecomunicações que vende telefones celulares, a marca, o modelo e os atributos de nível do dispositivo provavelmente serão amplamente usados para muitas ofertas e para os próximos anos, portanto, faz sentido adicioná-los. Ao pensar sobre quais atributos são necessários para uma oferta, evite adicionar atributos exclusivos a uma campanha específica. Em meses ou anos, esse esquema pode ficar sobrecarregado e causar problemas ao criar ofertas. Você verá como isso se aplica na seção onde você criará ofertas.

## Recapitulação

Você atualizou com sucesso o esquema de ofertas padrão com campos personalizados reutilizáveis que serão aproveitados em partes posteriores do laboratório ao criar e avaliar ofertas.
