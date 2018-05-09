---
title: Planejar a implantação do cliente em computadores Mac
titleSuffix: Configuration Manager
description: Planeje a implantação de cliente em computadores Mac no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8d15ae3f-de42-461f-a907-c43873da22d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05268780bd6dc3b86052b694f360065f8f70d6e6
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="planning-for-client-deployment-to-mac-computers-in-system-center-configuration-manager"></a>Planejando a implantação de cliente em computadores Mac no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode instalar o cliente do Configuration Manager em computadores Mac que executam o sistema operacional Mac OS X e usam os seguintes recursos de gerenciamento:  

-   **Inventário de hardware**  

     Você pode usar o inventário de hardware do Configuration Manager para coletar informações sobre o hardware e os aplicativos instalados em computadores Mac. Essas informações podem ser exibidas no Gerenciador de Recursos no console do Configuration Manager e usadas para criar coleções, consultas e relatórios. Para mais informações, consulte [Como usar o Gerenciador de Recursos para exibir o inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

     O Configuration Manager coleta as seguintes informações de hardware de computadores Mac:  

    -   Processador  

    -   Sistema de computador  

    -   Unidade de disco  

    -   Partição de disco  

    -   Adaptador de rede  

    -   Sistema operacional  

    -   Serviço  

    -   Processar  

    -   Software instalado  

    -   Produto do sistema de computador  

    -   Controlador USB  

    -   Dispositivo USB  

    -   Unidade de CD-ROM  

    -   Controlador de vídeo  

    -   Monitor de mesa  

    -   Bateria portátil  

    -   Memória física  

    -   Impressora  

    > [!IMPORTANT]  
    >  Você não pode estender as informações do hardware que são coletadas de computadores Mac durante o inventário de hardware.  

-   **Configurações de conformidade**  

     Você pode usar as configurações de conformidade do Configuration Manager para exibir a conformidade e corrigir configurações de preferência do Mac OS X (.plist). Por exemplo, você pode impor configurações para a home page no navegador da Web Safari ou verificar se o firewall da Apple está habilitado. Você também pode usar scripts de shell para monitorar e corrigir as configurações no MAC OS X.  

-   **Gerenciamento de aplicativo**  

     O Configuration Manager pode implantar o software em computadores Mac. Você pode implantar os seguintes formatos de software em computadores Mac:  

    -   Imagem de disco da Apple (.DMG)  

    -   Arquivo do pacote meta (.mpkg)  

    -   Pacote do Mac OS X Installer (.PKG)  

    -   Aplicativo do Mac OS X (.APP)  

 Ao instalar o cliente do Configuration Manager em computadores Mac, você não pode usar os recursos de gerenciamento a seguir com suporte pelo cliente do Configuration Manager em computadores Windows:  

-   Instalação do cliente por push  

-   Implantação de sistema operacional  

-   Atualizações de software  

    > [!NOTE]  
    >  Você pode usar o gerenciamento de aplicativos do Configuration Manager para implantar atualizações de software necessárias do Mac OS X em computadores Mac. Além disso, você pode usar as configurações de conformidade para verificar se os computadores têm as atualizações de software necessárias.  

-   Janelas de manutenção  

-   Controle remoto  

-   Gerenciamento de Energia  

-   Correção e verificação de cliente do status do cliente  

 Para obter mais informações sobre como instalar e configurar o cliente do Configuration Manager no Mac, consulte [Como implantar clientes em Macs no System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md).
