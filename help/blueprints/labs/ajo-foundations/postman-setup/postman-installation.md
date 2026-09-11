---
title: Instalação do Postman
description: Instale o Postman e familiarize-se com suas coleções, ambientes e interface do espaço de trabalho antes de fazer chamadas de API em laboratórios posteriores.
doc-type: article
solution: Experience Platform
exl-id: c277edb5-f758-4955-bcd7-b15a9b9ab949
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---


# Instalação do Postman

## Objetivo

Ao final desse laboratório, você poderá instalar o Postman, configurar um espaço de trabalho e um ambiente básicos para fazer chamadas de api subsequentes necessárias a futuros laboratórios.

>[!IMPORTANT]
>
>A Postman é necessária para vários laboratórios neste curso.  Mesmo que já tenha instalado o Postman, será necessário concluir este laboratório para garantir que você tenha os Arquivos de ambiente e a Coleção de API instalados e configurados corretamente.



## Instalar o Postman

Navegue até o site do Postman e baixe o aplicativo Postman ou utilize a Versão Web —> [https://www.postman.com/download/](https://www.postman.com/download/)

![Página de download do Postman no site da Postman](assets/postman-installation-postman-download.png)

## Criar um espaço de trabalho do Postman (opcional)

Se você for *novo(a) no Postman* e essa for sua primeira instalação, não será necessário criar um novo espaço de trabalho. Na primeira inicialização, escolha continuar sem fazer logon e use o cliente leve que não requer um espaço de trabalho.

Se você *já estiver familiarizado com o Postman* e o tiver instalado, é provável que você já tenha entrado e tenha vários espaços de trabalho. Se esse for o caso, recomendamos que você crie um novo espaço de trabalho para *esta inicialização*. As instruções podem ser encontradas no [site do Postman.](https://learning.postman.com/docs/collaborating-in-postman/using-workspaces/create-workspaces/)

## Interface do Postman

Abra o Postman e familiarize-se rapidamente com algumas áreas do aplicativo. Para trabalhar com o Experience Platform, precisamos nos concentrar em apenas algumas áreas principais do aplicativo.

![Visão geral da interface do Postman com barra lateral, cabeçalho e área de trabalho principal rotulada](assets/postman-installation-interface-overview.png "Interface do Postman")

## Barra lateral

A barra lateral é o que permite navegar rapidamente pelos diferentes elementos do Postman. Durante os laboratórios, você só usará os dois itens abaixo:

**Coleções** - grupos de solicitações salvas que podem ser importadas de um local externo ou criadas por você mesmo.

**Ambientes** - um conjunto de variáveis que você pode referenciar em suas solicitações do Postman. No Experience Platform, você pode considerar os ambientes do Postman como sinônimos de sandboxes da Adobe em uma organização IMS. Usaremos a função do Ambiente no Postman



## Cabeçalho

Espaços de trabalho - permitem organizar o trabalho em vários agrupamentos (ou seja, projetos, equipes etc.)



## Área de trabalho principal

A área de trabalho principal é onde você realizará a maioria do seu trabalho ao trabalhar no Postman. Todas as solicitações de API são expostas em uma guia específica na área de trabalho principal.

**Barra lateral direita** - fornece acesso adicional a ferramentas com base na guia atual selecionada. Exemplos são a documentação da solicitação, os comentários e os trechos de código, para citar alguns recursos.

**Seletor de ambiente** - permite alternar rapidamente entre ambientes diferentes para acessar variáveis pré-configuradas ao trabalhar com APIs. Ao trabalhar com o Experience Platform, você aproveitará isso ao trabalhar com uma sandbox da AEP específica na organização IMS atribuída.



## Rodapé

Na parte inferior do aplicativo Postman, você encontrará um conjunto de funções que permitem visualizar rapidamente os logs das chamadas feitas, o acesso rápido para localizar e substituir e várias outras funções.



## Recapitulação

Agora você deve ter o Postman instalado e compreender algumas noções básicas da interface do usuário
