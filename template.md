---
title:
- TÍTULO DO ARTIGO em 35 caracteres ou menos
titleSuffix: Configuration Manager
description: ''
ms.date: mm/dd/yyyy
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid:
- GET ONE FROM guidgenerator.com
author:
- GITHUB USERNAME
ms.author:
- ALIAS
manager:
- ALIAS
ms.openlocfilehash: bb0a23b8870d31136967b1bc594580bcc2cd0cd9
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351932"
---
# <a name="metadata-and-markdown-template"></a>Modelo de metadados e Markdown

Esse modelo do docs.ms contém exemplos de sintaxe de markdown, bem como uma orientação sobre como configurar os metadados. Ele está disponível no diretório raiz de cada repositório EM Piloto (por exemplo, ~/Azure-RMSDocs-pr/template.md) e deve ser lido como um arquivo markdown, embora você possa consultar [a versão publicada](https://stage.docs.microsoft.com/en-us/rights-management/template) para ver como os exemplos de markdown são processados.

Ao criar um arquivo markdown, você deve copiar o modelo para um novo arquivo, preencher os metadados conforme especificado abaixo, definir o título H1 acima para o título do artigo e excluir o conteúdo.


## <a name="metadata"></a>Metadados

O bloco de metadados completo está acima, dividido em campos obrigatórios e opcionais; consulte a [referência de metadados de OPS](https://ppe.msdn.microsoft.com/en-us/ce-csi-docs/ops/ops-onboarding/managing-content/content-meta-data) para obter mais detalhes. Algumas observações importantes:

- Você **deve** ter um espaço entre os dois-pontos (:), e o valor para um elemento de metadados.
- Se um elemento de metadados opcional não tiver um valor, comente o elemento com um # (não deixe em branco ou use "na"); se você estiver adicionando um valor a um elemento que foi comentado, remova o #.
- Dois pontos em um valor (por exemplo, um título) quebram o analisador de metadados. Em seu lugar, use a codificação HTML &#58; (por exemplo, "title: Azure Rights Management&#58; noções básicas | Azure RMS").
- **título**: este título aparecerá nos resultados do mecanismo de pesquisa. O título deve terminar com uma barra vertical (|) seguida pelo nome do serviço (por exemplo, veja acima). O título não precisa (e provavelmente não deve) ser idêntico ao título em seu título H1. Ele deve ter aproximadamente 65 caracteres (incluindo | NOME DO SERVIÇO)
- **author**, **manager**, **reviewer**: O campo author deve conter o **Nome de usuário do Github** do autor, não seu alias.  Por outro lado, os campos "manager" e "reviewer", devem conter aliases. ms.reviewer especifica o nome do PM associado ao artigo ou serviço.
- **ms.assetid**: esse é o GUID do artigo de CAPS. Ao criar um novo arquivo markdown, obtenha um GUID em [https://www.guidgenerator.com](https://www.guidgenerator.com).
- **ms.prod**, **ms.service**, **ms.technology**, **ms.devlang**, **ms.topic**, **ms.tgt_pltfrm**: os valores possíveis para esses elementos podem ser encontrados [aqui](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default).

## <a name="basic-markdown-and-gfm"></a>Markdown Básico e GFM

Todo markdown básico e do tipo Github têm suporte. Para saber mais sobre eles, confira:

- [Sintaxe de markdown de linha de base](https://daringfireball.net/projects/markdown/syntax)
- [Documentação de GFM (markdown do tipo Github)](https://guides.github.com/features/mastering-markdown)

## <a name="headings"></a>Títulos

Veja acima os exemplos de títulos de primeiro e segundo nível.

**Deve** haver apenas um título de primeiro nível em seu tópico, que será exibido como o título da página.  

Títulos de segundo nível gerarão o Sumário na página que aparece na seção "Neste artigo" embaixo do título da página.

### <a name="third-level-heading"></a>Título de terceiro nível
#### <a name="fourth-level-heading"></a>Título de quarto nível
##### <a name="fifth-level-heading"></a>Título de quinto nível
###### <a name="sixth-level-heading"></a>Título de sexto nível

## <a name="text-styling"></a>Estilo do texto

*Itálico*

**Negrito**

~~Tachado~~



## <a name="links"></a>Links

Para vincular a um arquivo markdown no mesmo repositório, use [links relativos](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2).

- Exemplo: [O que é o Azure Rights Management](./understand-explore/what-is-azure-rights-management.md)

Para vincular a um título no mesmo arquivo markdown, exiba a origem do artigo publicado, localize a id do cabeçalho (por exemplo, `id="blockquote"`, e vincule usando #+id (por exemplo, `#blockquote`).

- Exemplo: [Blockquotes](#blockquote)

Para vincular a um título em um arquivo markdown no mesmo repositório, use link relativo+vinculação por hashtag.

- Exemplo: [visão geral técnica do processo de inscrição](./understand-explore/rms-for-individuals-user-signup.md#technical-overview-of-the-sign-up-process)

Para vincular a um arquivo externo, use a URL completa como o link.

- Exemplo: [Github](http://www.github.com)

Se aparecer uma URL em um arquivo markdown, ela será transformada em um link clicável.

- Exemplo: http://www.github.com

## <a name="lists"></a>Listas

### <a name="ordered-lists"></a>Listas ordenadas

1. Esta
1. é
1. uma
1. lista
1. Lista  


#### <a name="ordered-list-with-an-embedded-list"></a>Lista ordenada com uma lista inserida

1. Esta
1. é
1. uma
1. lista
    1. inserida
    1. Professor Black
1. Senhorita Scarlett
1. lista


### <a name="unordered-lists"></a>Listas Não Ordenadas

- Esta
- é
- a
- lista
- lista


##### <a name="unordered-list-with-an-embedded-lists"></a>Lista não ordenada com uma lista incorporada

- Esta
- lista
- lista
    - Dona Violeta
    - Sr. Marinho
- contém  
- outras
    1. Coronel Mostarda
    1. Dona Branca
- listas


## <a name="horizontal-rule"></a>Régua horizontal

---

## <a name="tables"></a>Tabelas

| Tabelas        | São           | Legais  |
| ------------- |:-------------:| -----:|
| a col. 3 está      | alinhada à direita | $1600 |
| a col. 2 está      | centralizada      |   $12 |
| a coluna 1 assume o padrão de | alinhada à esquerda     |    $1 |


## <a name="code"></a>Código

### <a name="codeblock"></a>Codeblock (bloco de código)

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### <a name="in-line-code"></a>In-line code (código embutido)

Este é um exemplo de `in-line code`.

## <a name="blockquotes"></a>Blockquotes (citações em bloco)

> A seca já durava dez milhões de anos, e o reino dos terríveis lagartos havia terminado muito antes disso. Aqui no Equador, no continente que um dia seria conhecido como África, a batalha pela existência atingiu um novo clímax de ferocidade, e o vencedor ainda não era conhecido. Nessa terra estéril e deserta, apenas os pequenos ou velozes ou selvagens poderiam prosperar, ou até mesmo ter esperança de sobreviver.

## <a name="images"></a>Imagens

### <a name="static-image"></a>Imagem estática

![este é o texto alt](./media/AzRMS_elements.png)

### <a name="linked-image"></a>Imagem vinculada

[![texto alt para imagem vinculada](./media/AzRMS_elements.png)](https://azure.microsoft.com)

### <a name="animated-gif"></a>Gif animado

![gif animado](./media/hololens.gif)

## <a name="alerts"></a>Alertas

### <a name="note"></a>Observação

> [!NOTE]
> Isto é uma OBSERVAÇÃO

### <a name="warning"></a>Aviso

> [!WARNING]
> Isto é um AVISO

### <a name="tip"></a>Dica

> [!TIP]
> Isto é uma DICA

### <a name="important"></a>Importante

> [!IMPORTANT]
> Isto é IMPORTANTE

## <a name="videos"></a>Vídeos

### <a name="channel-9"></a>Channel 9

<iframe src="http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>


### <a name="youtube"></a>Youtube

<iframe width="420" height="315" src="https://www.youtube.com/embed/R6_eWWfNB54" frameborder="0" allowfullscreen></iframe>

## <a name="docsms-extentions"></a>extensões do docs.ms

### <a name="button"></a>Botão

> [!div class="button"]
[links de botão](/rights-management)

### <a name="selector"></a>Seletor

> [!div class="op_single_selector"]
- [foo](/rights-management/template.md)
- [bar](/rights-management/scratch.md)

### <a name="step-by-step"></a>Passo a passo

>[!div class="step-by-step"]
[Anterior](https://www.example.com)
[Próximo](https://www.example.com)
