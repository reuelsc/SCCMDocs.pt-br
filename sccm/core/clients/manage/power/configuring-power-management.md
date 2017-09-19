---
title: Configurando o gerenciamento de energia | Microsoft Docs
description: Configure o gerenciamento de energia no System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
caps.latest.revision: "5"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 7d2125464103cf0c040592c9f7ddbc25ae022758
ms.sourcegitcommit: f6a428a8db7145affa388f59e0ad880bdfcf17b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2017
---
# <a name="configuring-power-management-in-system-center-configuration-manager"></a>Configurando o gerenciamento de energia no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para poder usar o gerenciamento de energia no System Center Configuration Manager, você precisará executar as etapas de configuração a seguir.  

## <a name="enable-and-configure-power-management-client-settings"></a>Habilitar e definir as configurações do cliente de gerenciamento de energia  
 Este procedimento define as configurações de cliente padrão para o gerenciamento de energia e se aplica a todos os computadores em sua hierarquia. Se quiser que essas configurações se apliquem somente a alguns computadores, crie uma configuração personalizada do cliente de dispositivo e a atribua a uma coleção que contém os computadores nos quais deseja usar o gerenciamento de energia. Para obter mais informações sobre como criar configurações personalizadas de dispositivo, consulte [Como configurar as definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

#### <a name="to-enable-power-management-and-configure-client-settings"></a>Para habilitar o gerenciamento de energia e definir as configurações do cliente  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , clique em **Configurações do Cliente**.  

3.  Clique em **Configurações do Cliente Padrão**.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Na caixa de diálogo **Configurações Padrão do Cliente** , clique em **Gerenciamento de Energia**.  

6.  Defina o seguinte valor para as configurações do cliente de gerenciamento de energia:  

    -   **Permitir o gerenciamento de energia de dispositivos** – Na lista suspensa, selecione **True** para habilitar o gerenciamento de energia.  

7.  Defina as configurações do cliente necessárias. Para obter uma lista de configurações do cliente de gerenciamento de energia que podem ser definidas, veja a seção [Gerenciamento de Energia](../../../../core/clients/deploy/about-client-settings.md#power-management) no tópico [Sobre as configurações de cliente no System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).  

8.  Clique em **OK** para fechar a caixa de diálogo **Configurações do Cliente Padrão** .  

 Os computadores cliente serão definidos com essas configurações durante o próximo download da política do cliente. Para iniciar a recuperação de política para um cliente individual, veja [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

## <a name="exclude-computers-from-power-management"></a>Excluir computadores do gerenciamento de energia  
 Você pode impedir que as coleções de computadores recebam as configurações de gerenciamento de energia. Se um computador for membro de qualquer coleção que seja excluída das configurações de gerenciamento de energia, esse computador não aplicará as configurações de gerenciamento de energia mesmo que seja membro de outra coleção que aplica as configurações de gerenciamento de energia.  

 Talvez você queira excluir computadores do gerenciamento de energia por qualquer um dos seguintes motivos:  

-   Você tem um requisito de negócios para que computadores sejam ligados em todos os momentos.  

-   Você criou uma coleção de controle de computadores nos quais você não deseja aplicar as configurações de gerenciamento de energia.  

-   Alguns de seus computadores não são capazes de aplicar as configurações de gerenciamento de energia.  

-   Você deseja excluir os computadores que executam o Windows Server do gerenciamento de energia.  

> [!NOTE]  
>  Se a opção **Permitir que os usuários excluam seu dispositivo do gerenciamento de energia** estiver definida nas configurações do cliente, os usuários poderão excluir seus próprios computadores do gerenciamento de energia usando o Centro de Software.  

 Para descobrir os computadores que foram excluídos do gerenciamento de energia, execute o relatório **Computadores Excluídos**. Para obter mais informações sobre esse relatório, consulte [Computadores Excluídos](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Excluded) no tópico [Como monitorar e planejar o gerenciamento de energia no System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

> [!IMPORTANT]  
>  As configurações de energia aplicadas aos computadores com o Windows XP ou Windows Server 2003 não são revertidas para seus valores originais, mesmo que você exclua o computador do gerenciamento de energia. Em versões posteriores do Windows, a exclusão de um computador do gerenciamento de energia faz com que todas as configurações de energia sejam revertidas para seus valores originais. Não é possível reverter as configurações de energia individuais para seus valores originais.  

#### <a name="to-exclude-a-collection-of-computers-from-power-management"></a>Para excluir uma coleção de computadores do gerenciamento de energia  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Coleções de Dispositivos**.  

3.  Na lista **Coleções de Dispositivos** , selecione a coleção que deseja excluir do gerenciamento de energia e, na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Na guia **Gerenciamento de Energia** da caixa de diálogo *Propriedades\>***<nome da coleção**, selecione **Nunca aplicar configurações de gerenciamento de energia aos computadores desta coleção**.  

5.  Clique em **OK** para fechar a caixa de diálogo *Propriedades\>***<Nome da Coleção** e salvar as configurações.  
