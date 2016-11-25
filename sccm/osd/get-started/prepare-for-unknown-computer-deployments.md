---
title: "Preparar implantações de computador desconhecido | Configuration Manager"
description: "Saiba como implantar sistemas operacionais em computadores que não são gerenciados pelo Configuration Manager no seu ambiente do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9e447e34-0943-49ed-b6ba-3efebf3566c1
caps.latest.revision: 10
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1228dc7ebee2f17da9a7ade5641ef73e1891bba9


---
# <a name="prepare-for-unknown-computer-deployments-in-system-center-configuration-manager"></a>Preparar implantações de computador desconhecido no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as informações neste tópico para implantar sistemas operacionais em computadores desconhecidos no ambiente do System Center Configuration Manager. Um computador desconhecido é qualquer computador que não seja gerenciado pelo Configuration Manager. Isso significa que não há registro desses computadores no banco de dados do Configuration Manager. Computadores desconhecidos incluem:  

-   Um computador no qual o cliente do Configuration Manager não está instalado  

-   Um computador que não foi importado para o Configuration Manager  

-   Um computador que não foi descoberto pelo Configuration Manager  

 É possível implantar sistemas operacionais em computadores desconhecidos com os seguintes métodos de implantação:  

-   [Usar PXE para implantar o Windows na rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)  

-   [Usar a mídia inicializável para implantar um sistema operacional](../deploy-use/create-bootable-media.md)  

-   [Usar a mídia pré-configurada para implantar um sistema operacional](../deploy-use/create-prestaged-media.md)  

## <a name="unknown-computer-deployment-workflow"></a>Fluxo de trabalho de implantação em computador desconhecido  
 Veja a seguir o fluxo de trabalho básico para implantar um sistema operacional em um computador desconhecido:  

-   Selecione um objeto de computador desconhecido para usar na implantação. É possível implantar o sistema operacional em um dos objetos do computador desconhecido na coleção **Todos os Computadores Desconhecidos** ou adicionar os objetos na coleção **Todos os Computadores Desconhecidos** a outra coleção. O Configuration Manager fornece dois objetos de computador desconhecido na coleção **Todos os Computadores Desconhecidos**. Um objeto é para computadores x86 e o outro para computadores x64.  

    > [!NOTE]  
    >  O objeto **Computador x86 Desconhecido** é para computadores compatíveis somente com x86. O objeto **Computador x64 Desconhecido** é para computadores compatíveis com x86 e x64. Em outras palavras, esses objetos descrevem a arquitetura do computador de destino. Eles não descrevem o sistema operacional que você deseja implantar no computador de destino.  

-   Configure um ponto de distribuição habilitado para PXE ou crie a mídia para dar suporte a implantações em computador desconhecido.  

-   Implante uma sequência de tarefas para instalar o sistema operacional.  

## <a name="unknown-computer-installation-process"></a>Processo de instalação do computador desconhecido  
 Quando um computador é primeiramente iniciado do PXE ou da mídia, o Configuration Manager verifica se existe um registro desse computador no banco de dados do Configuration Manager. Se existe registro, o Configuration Manager verifica se há sequências de tarefas implantadas no registro. Se não existe registro, o Configuration Manager verifica se há sequências de tarefas implantadas em um objeto de computador desconhecido. Em ambos os casos, o Configuration Manager executa uma das ações a seguir:  

-   Se há uma sequência de tarefas disponível, o Configuration Manager solicita ao usuário que execute a sequência de tarefas.  

-   Se houver uma sequência de tarefas obrigatória, o Configuration Manager a executará automaticamente.  

-   Se não houver uma sequência de tarefas implantada no registro, o Configuration Manager gerará um erro indicando que não há sequências de tarefas implantadas no computador de destino.  

 Quando um computador desconhecido é iniciado, o Configuration Manager reconhece o computador como um computador não provisionado, e não como um computador desconhecido. Isso significa que o computador pode agora receber as sequências de tarefas que foram implantadas no objeto do computador desconhecido. A sequência de tarefas implantada instala uma imagem do sistema operacional que deve incluir o cliente do Configuration Manager.  

 Concluída a instalação do cliente do Configuration Manager, é criado um registro para o computador e o computador é listado na coleção apropriada do Configuration Manager. Se o computador falhar ao instalar a imagem do sistema operacional ou o cliente do Configuration Manager, será criado um registro “Desconhecido” para o computador e o computador aparecerá na coleção **Todos os Sistemas**.  

> [!NOTE]  
>  Durante a instalação da imagem do sistema operacional, a sequência de tarefas pode recuperar as variáveis da coleção, mas não as variáveis desse computador.  

##  <a name="a-namebkmkenablingunknowna-enabling-unknown-computer-support"></a><a name="BKMK_EnablingUnknown"></a> Habilitando o suporte a computador desconhecido  
 Use as opções a seguir para habilitar o suporte a computadores desconhecidos ao implantar um sistema operacional usando o PXE, a mídia inicializável e a mídia pré-configurada.  

-   **PXE**  

     Marque a caixa de seleção **Habilitar suporte a computadores desconhecidos** na guia **PXE** de um ponto de distribuição que está habilitado para PXE. Para obter mais informações, consulte [Configuring distribution points to accept PXE requests](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint) (Configurando pontos de distribuição para aceitar solicitações PXE).  

-   **Mídia inicializável**  

     Marque a caixa de seleção **Habilitar suporte a computadores desconhecidos** , na página **Segurança** do Assistente para Criar Mídia de Sequência de Tarefas. Para obter mais informações, consulte [Configuring distribution points to accept PXE requests](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint) (Configurando pontos de distribuição para aceitar solicitações PXE) e [Use PXE to deploy Windows over the network with System Center Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md) (Usar o PXE para implantar o Windows pela rede com o System Center Configuration Manager).  

-   **Mídia em pré-teste**  

     Marque a caixa de seleção **Habilitar suporte a computadores desconhecidos** , na página **Segurança** do Assistente para Criar Mídia de Sequência de Tarefas. Para obter mais informações, consulte [Create prestaged media with System Center Configuration Manager](../deploy-use/create-prestaged-media.md).  



<!--HONumber=Nov16_HO1-->


