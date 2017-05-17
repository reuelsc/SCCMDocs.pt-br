---
title: "A biblioteca de conteúdo | Microsoft Docs"
description: "Saiba mais sobre a biblioteca de conteúdo que o System Center Configuration Manager usa para reduzir o tamanho geral do conteúdo distribuído."
ms.custom: na
ms.date: 2/14/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: d31fecdb71b498864df2bce7403a4290ea9700ae
ms.openlocfilehash: 0fa9f431c00476d71b2b08f92f914d76636d1a27
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017

---
# <a name="the-content-library-in-system-center-configuration-manager"></a>A biblioteca de conteúdo no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A biblioteca de conteúdo é um single instance store de conteúdo que o System Center Configuration Manager usa para reduzir o tamanho geral do corpo de conteúdo combinado que você distribui. A biblioteca de conteúdo armazena todos os arquivos de conteúdo para atualizações de software, aplicativos, implantações de sistema operacional, entre outros.

 - Uma cópia da biblioteca de conteúdo é automaticamente criada e mantida em cada **servidor do site** e em cada **ponto de distribuição**.

 - Antes de o Configuration Manager baixar arquivos de conteúdo para o servidor do site ou copiar os arquivos para pontos de distribuição, ele verifica se cada arquivo de conteúdo já está na biblioteca de conteúdo.
 - Se o arquivo de conteúdo estiver disponível, o Configuration Manager não o copiará. Em vez disso, ele associará o arquivo de conteúdo existente ao aplicativo ou pacote.

Em computadores em que você instala um ponto de distribuição, é possível configurar:

- Uma ou mais unidades de disco nas quais você deseja criar a biblioteca de conteúdo.
- Uma prioridade para cada unidade que você usa.

Quando o Configuration Manager copia os arquivos de conteúdo, ele os copia para a unidade com a prioridade mais alta até que essa unidade contenha menos de uma quantidade mínima de espaço livre especificado.
- Você pode definir as configurações da unidade durante a instalação do ponto de distribuição.
- Você não pode definir as configurações da unidade nas propriedades do ponto de distribuição após a conclusão da instalação.


Para obter mais informações sobre como definir as configurações de unidade dos pontos de distribuição, consulte [Gerenciar conteúdo e infraestrutura de conteúdo do System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


>  [!IMPORTANT]  
>  Para mover a biblioteca de conteúdo para um local diferente em um ponto de distribuição após a instalação, use a **ferramenta de Transferência da Biblioteca de Conteúdo** no kit de ferramentas do System Center 2012 R2 Configuration Manager. Você pode baixar o kit de ferramentas do [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkId=279566).  

## <a name="about-the-content-library-on-the-central-administration-site"></a>Sobre a biblioteca de conteúdo no site de administração central  
 Por padrão, o Configuration Manager cria uma biblioteca de conteúdo no site de administração central quando o site é instalado. A biblioteca de conteúdo é colocada na unidade do servidor do site com mais espaço livre em disco. Como não é possível instalar um ponto de distribuição no site de administração central, você não pode priorizar as unidades para uso pela biblioteca de conteúdo. Semelhante à biblioteca de conteúdo em outros servidores de site e em pontos de distribuição, quando a unidade que contém a biblioteca de conteúdo fica sem espaço em disco disponível, a biblioteca de conteúdo passa automaticamente para a próxima unidade disponível.  

 O Configuration Manager usa a biblioteca de conteúdo no site de administração central nos seguintes cenários:  

-   Quando você cria conteúdo no site de administração central.  

-   Quando você migra conteúdo de outro site do Configuration Manager e atribui o site de administração central como o site que gerencia esse conteúdo.  

> [!NOTE]  
>  Quando você cria conteúdo em um site primário e o distribui a um site primário diferente ou site secundário abaixo de um site primário diferente, o site de administração central armazena temporariamente esse conteúdo na caixa de entrada do agendador no site de administração central, mas não adiciona o conteúdo à biblioteca de conteúdo.  

 Use as opções a seguir para gerenciar a biblioteca de conteúdo no site de administração central:  

-   Para impedir que a biblioteca de conteúdo seja instalada em uma unidade específica, crie um arquivo vazio chamado **no_sms_on_drive.sms** e copie-o para a pasta raiz da unidade antes de criar a biblioteca de conteúdo.  

-   Depois da criação da biblioteca de conteúdo, use a **Ferramenta de Transferência da Biblioteca de Conteúdo** do kit de ferramentas do System Center 2012 R2 Configuration Manager para gerenciar o local da biblioteca de conteúdo. Você pode baixar o kit de ferramentas do [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkId=279566).  

