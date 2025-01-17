---
title: Instalar o Updates Publisher
titleSuffix: Configuration Manager
description: Instalar o System Center Updates Publisher em seu ambiente
ms.date: 02/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: ab5cda93-b67c-4aa5-904d-7b63ce790aa0
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: eb07b154c1da9c7b93f2d8e0f06b825eb52fd561
ms.sourcegitcommit: 417e3834a42b415a8e129327dd3c15cc0c7ec5a2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2019
ms.locfileid: "65443188"
---
# <a name="install-updates-publisher"></a>Instalar o Updates Publisher

*Aplica-se ao: System Center Updates Publisher*

As informações neste artigo podem ajudar você a baixar, instalar e configurar o Updates Publisher para uso com o seu ambiente do System Center Configuration Manager.

## <a name="prerequisites-and-limitations"></a>Pré-requisitos e limitações
O System Center Updates Publisher só pode ser usado com o System Center Configuration Manager. Ele não é destinado para uso com hierarquias autônomas do WSUS.

As seções a seguir detalham os requisitos de instalação e uso do Updates Publisher, e as limitações ou problemas conhecidos de seu uso.  

### <a name="operating-systems"></a>Sistemas operacionais
Instale e execute o Updates Publisher em uma edição de 64 bits dos sistemas operacionais a seguir. Não há requisitos mínimos de service pack ou pacote cumulativo de atualizações.

-   Windows Server 2016 (Standard, Datacenter)
-   Windows Server 2012 R2 (Standard, Datacenter)
-   Windows 10 (Pro, Education, Pro Education, Enterprise)
-   Windows 8.1 (Professional, Enterprise)

### <a name="prerequisites"></a>Pré-requisitos
Os itens a seguir são necessários no computador que executa o Updates Publisher.

-   **Sistema operacional de 64 bits**: o computador no qual você instala o Updates Publisher deve executar um sistema operacional de 64 bits.
-   **WSUS 4.0 ou posterior**:
    -   No Windows Server, instale o Console de Administração padrão para atender a esse requisito.
    -   Para Windows 10 e Windows 8.1, instale [RSAT (Ferramentas de Administração de Servidor Remoto) para sistemas operacionais Windows](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems). Isso instala o suporte necessário para usar o Updates Publisher (*cmdlets do PowerShell e API*, e *Console de Gerenciamento de Interface do Usuário*).
-   **Permissões**:
    -   Instalação: administrador local
    -   A maioria das operações: usuário local
    -   Publicação, ou operações que envolvem o WSUS: membro do grupo de administradores de WSUS no servidor do WSUS.

### <a name="supported-languages"></a>Idiomas com suporte
O Updates Publisher está disponível somente em inglês, mas pode gerenciar atualizações para outros idiomas. O suporte ao idioma depende da tarefa, como publicação, criação ou edição das atualizações.

Ao exportar ou publicar atualizações, o Updates Publisher exibe o título e a descrição da atualização de software com base na localidade do computador em que o Updates Publisher está instalado.

Por exemplo, crie uma atualização de software que tem um título em inglês e espanhol.

-   Se você criar a atualização em um computador cuja localidade é inglês, por padrão, você verá o título e a descrição em inglês.
-   Se, em seguida, você exportar ou publicar essa atualização em um computador cuja localidade é o espanhol, você verá o título e a descrição em espanhol nesse computador.

### <a name="publishing"></a>Publicando
Quando você publica atualizações de software, pode especificar o idioma do arquivo binário de atualização de software. Você também pode especificar que a localidade do binário é neutra. Os idiomas a seguir têm suporte:

-   Árabe
-   Chinês (RAE de Hong Kong)
-   Chinês (tradicional)
-   Chinês (simplificado)
-   Tcheco
-   Dinamarquês
-   Holandês
-   Inglês
-   Finlandês
-   Francês
-   Alemão
-   Grego
-   Hebraico
-   Húngaro
-   Italiano
-   Japonês
-   Coreano
-   Norueguês
-   Polonês
-   Português
-   Português (Brasil)
-   Russo
-   Espanhol
-   Sueco
-   Turco

### <a name="software-update-titles-and-descriptions"></a>Descrições e títulos de atualização de software
Os idiomas a seguir têm suporte para títulos e descrições de atualização de software.

-   Chinês (tradicional)
-   Chinês (simplificado)
-   Inglês
-   Francês
-   Alemão
-   Italiano
-   Japonês
-   Coreano
-   Português (Brasil)
-   Russo
-   Espanhol

## <a name="install-updates-publisher"></a>Instalar o Updates Publisher
Obtenha o **UpdatesPubliser.msi** para a instalação do System Center Updates Publisher no [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=55543).

Para instalar o Updates Publisher, execute **UpdatesPublisher.msi** em um computador que atenda aos *pré-requisitos*. O instalador cria a seguinte pasta para conter os arquivos necessários para executar o Updates Publisher: %PROGRAMFILES%\Microsoft\UpdatesPublisher*.

Como essa pasta contém todos os arquivos necessários para usar o Updates Publisher, você pode copiar a pasta e seu conteúdo para um novo local ou outro computador, e usar o Updates Publisher nesse local. No entanto, o novo local ou computador deve atender aos pré-requisitos para execução do Updates Publisher.

Após a conclusão da instalação, execute **UpdatesPublisher.exe** na pasta *UpdatesPublisher* para iniciar o Updates Publisher.

## <a name="next-steps"></a>Próximas etapas
 Depois de instalar o Updates Publisher, recomendamos que você [configure as opções](updates-publisher-options.md) para o Updates Publisher. Você deve configurar algumas opções antes de poder usar alguns recursos do Updates Publisher.

 No entanto, se você quiser usar os padrões e não planejar implantar atualizações em um servidor de atualização ou em dispositivos gerenciados, acesse diretamente [Gerenciar catálogos de atualização de software](updates-publisher-catalogs.md) ou [Criar atualizações de software](create-updates-with-updates-publisher.md) e crie seus próprios catálogos de atualização.
