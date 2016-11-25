---
title: Configurar controle remoto | System Center Configuration Manager
description: Configure o controle remoto no System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: aea35afe970e20bc2b22f9ae3f413a3c735caae1


---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>Configurando o controle remoto no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para poder usar o controle remoto no System Center Configuration Manager, você precisará executar as etapas de configuração a seguir.  

## <a name="how-to-enable-remote-control-and-configure-client-settings"></a>Como habilitar o controle remoto e definir configurações do cliente  
 Este procedimento descreve como definir as configurações padrão do cliente para o controle remoto e se aplica a todos os computadores em sua hierarquia. Se quiser que essas configurações se apliquem somente a alguns computadores, crie uma configuração personalizada do cliente de dispositivo e a atribua a uma coleção que contém os computadores nos quais deseja usar em uma sessão de controle remoto. Para obter mais informações sobre como criar configurações personalizadas de dispositivo, consulte [Como configurar as definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>Para habilitar o controle remoto e definir as configurações do cliente  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , clique em **Configurações do Cliente**.  

3.  Clique em **Configurações do Cliente Padrão**.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Na caixa de diálogo **Padrão**  , clique em **Ferramentas Remotas**.  

6.  Configure o controle remoto e defina as configurações de cliente de Assistência Remota e de Área de Trabalho Remota necessárias. Para obter uma lista de configurações do cliente de ferramentas remotas que podem ser definidas, veja a seção [Ferramentas Remotas](../../../../core/clients/deploy/about-client-settings.md#BKMK_RemoteToolsDeviceSettings) no tópico [Sobre as configurações de cliente no System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).  

    > [!NOTE]  
    >  Você pode alterar o nome da empresa que aparece na caixa de diálogo **Controle Remoto do ConfigMgr** configurando um valor para o **Nome da organização exibido no Centro de Software** nas configurações do cliente **Agente Computador** .  

    > [!IMPORTANT]  
    >  Para usar a Assistência Remota ou a Área de Trabalho Remota, ela deve estar instalada e configurada no computador que executa o console do Configuration Manager. Para obter mais informações sobre como instalar e configurar a Assistência Remota ou a Área de Trabalho Remota, veja a documentação do Windows.  

7.  Clique em **OK** para fechar a caixa de diálogo **Configurações Padrão** .  

 Os computadores cliente são definidos com essas configurações na próxima vez que baixarem a política do cliente. Para iniciar a recuperação de política para um cliente individual, veja [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Nov16_HO1-->


