---
title: Configurar o controle remoto | Microsoft Docs
description: Configure o controle remoto no System Center Configuration Manager.
ms.custom: na
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 88828e68bc4aff216e83807ea8288c7d42c60cbd
ms.openlocfilehash: cbfa9dc6cb37518c0a561700272cc882b0041350


---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>Configurando o controle remoto no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Este procedimento descreve como definir as configurações padrão do cliente para o controle remoto e se aplica a todos os computadores em sua hierarquia. Se quiser que essas configurações se apliquem somente a alguns computadores, crie uma configuração personalizada do cliente de dispositivo e a atribua a uma coleção que contém os computadores nos quais deseja usar em uma sessão de controle remoto. Para obter mais informações, consulte [Como definir as configurações do cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md). 

Para usar a Assistência Remota ou a Área de Trabalho Remota, ela deve estar instalada e configurada no computador que executa o console do Configuration Manager. Para obter mais informações sobre como instalar e configurar a Assistência Remota ou a Área de Trabalho Remota, veja a documentação do Windows.  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>Para habilitar o controle remoto e definir as configurações do cliente  

1.  No console do Configuration Manager, escolha **Administração** > **Configurações do Cliente** > **Configurações do Cliente Padrão**.  

4.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

5.  Na caixa de diálogo **Padrão**, escolha **Ferramentas Remotas**.  

6.  Configure o controle remoto e defina as configurações de cliente da Assistência Remota e da Área de Trabalho Remota. Para obter uma lista de configurações do cliente de ferramentas remotas que podem ser definidas, consulte [Ferramentas remotas](../../../../core/clients/deploy/about-client-settings.md#remote-tools).  

    Você pode alterar o nome da empresa que aparece na caixa de diálogo **Controle Remoto do ConfigMgr** configurando um valor para o **Nome da organização exibido no Centro de Software** nas configurações do cliente **Agente Computador** .  

 Os computadores cliente são definidos com essas configurações na próxima vez que baixarem a política do cliente. Para iniciar a recuperação de política para um cliente individual, veja [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Dec16_HO1-->


