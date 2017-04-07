---
title: "Configurar o gerenciamento de dispositivo híbrido do Android com o System Center Configuration Manager e o Microsoft Intune | Microsoft Docs"
description: "Preparar para gerenciar dispositivos móveis Android com o Configuration Manager e o Intune."
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
caps.latest.revision: 9
caps.handback.revision: 0
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 199096db7a23fb14db98b95e75246ed254848ab7
ms.openlocfilehash: f6b949247435a2fede680cd8e146e5d7cf3989d9
ms.lasthandoff: 03/27/2017


---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar o gerenciamento de dispositivo híbrido do Android com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico ajuda o administrador de TI a habilitar o registro híbrido de dispositivos Android e Android for Work. Os dispositivos podem ser gerenciados com o Configuration Manager usando uma Assinatura do Microsoft Intune configurada. Os usuários podem fazer o download do aplicativo Android do portal da empresa no Google Play, que permite que eles registrem dispositivos Android (incluindo Samsung KNOX Standard) e Android for Work. Como administrador do Configuration Manager, você pode gerenciar as configurações de conformidade, apagar ou excluir dispositivos Android, implantar aplicativos e coletar inventários de software e hardware. Se o aplicativo do Android do portal da empresa não estiver instalado nos dispositivos Android, você não terá todos os recursos de gerenciamento, como inventário e configurações de conformidade, mas ainda poderá implantar aplicativos nos dispositivos Android.  

## <a name="enable-android-enrollment"></a>Habilitar o registro do Android  
As etapas a seguir permitem que o Configuration Manager gerencie dispositivos Android sem um perfil de trabalho (ou seja, o registro "Android clássico").

1.  **Pré-requisitos** – Antes de configurar o registro para qualquer plataforma, conclua os pré-requisitos e os procedimentos em [Configurar MDM híbrido](setup-hybrid-mdm.md).  
2.  No console do Configuration Manager, no espaço de trabalho **Administração**, selecione **Visão Geral** > **Serviços de Nuvem** > **Assinaturas do Microsoft Intune** e selecione sua assinatura do Intune.  
3.  Na guia **Início** do grupo **Assinatura**, selecione **Configurar Plataformas** > **Android**.  

4.  Na caixa de diálogo **Propriedades da Assinatura do Microsoft Intune** , selecione a guia **Android** e clique para marcar a caixa de seleção **Habilitar registro do Android** .  

 Depois da configuração, você precisará permitir que os usuários saibam como registrar seus dispositivos. Consulte [O que dizer aos usuários sobre o registro de seus dispositivos](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Essas informações se aplicam a dispositivos móveis gerenciados pelo Microsoft Intune e pelo Configuration Manager.

## <a name="enable-android-for-work-enrollment"></a>Habilitar o registro do Android for Work
As etapas a seguir permitem que o Configuration Manager gerencie dispositivos Android sem um perfil de trabalho (ou seja, o registro "Android clássico").

 1. Crie uma conta do Google em https://accounts.google.com/SignUp para usar como a conta de administrador do Android for Work ou entre com a conta que será associada a todas as tarefas de gerenciamento do Android for Work para esse locatário do Intune. Essa pode ser uma conta do Google compartilhada entre os administradores que gerenciam dispositivos Android. Essa é a conta do Google que sua organização usa para gerenciar e publicar aplicativos no console do Play for Work. Você usará essa conta para aprovar os aplicativos na loja do Play for Work, portanto, mantenha o controle do nome da conta e senha.
 2. Habilite o registro do Android associando a conta do Google ao locatário do Intune gerenciado no Configuration Manager:
   1. No console do Configuration Manager, no espaço de trabalho **Administração**, selecione **Visão Geral** > **Serviços de Nuvem** > **Assinaturas do Microsoft Intune** e selecione sua assinatura do Intune.
   2. Na guia **Início** do grupo **Assinatura**, selecione **Configurar Plataformas** > **Android for Work**.
   3. Na caixa de diálogo, selecione **Configurar Android for Work no console do Intune**. O console do Intune é aberto no navegador da Web.
   4. Use suas credenciais de administrador do Intune para fazer logon no portal do Intune.
   5. Selecione **Configurar** para abrir o site do Android for Work da Google Play.
   6. Na página de entrada do Google, insira as credenciais da conta do Google da etapa 1 e forneça as informações da sua empresa.
 3. Quando você retornar ao portal do Intune, o Android for Work estará habilitado e haverá três opções de registro para dispositivos do Android for Work:
   - **Gerenciar todos os dispositivos como Android** – (desabilitada) todos os dispositivos Android, incluindo dispositivos que dão suporte ao Android for Work, serão registrados como dispositivos Android convencionais
   - **Gerenciar dispositivos com suporte como Android for Work** – (habilitada) todos os dispositivos que dão suporte ao Android for Work são registrados como dispositivos Android for Work. Qualquer dispositivo Android que não tem suporte para Android for Work é registrado como um dispositivo Android convencional.
   - **Gerenciar dispositivos com suporte como Android for Work somente para os usuários nestes grupos** – (habilitado apenas para alguns grupos) permite direcionar o gerenciamento do Android for Work a um conjunto de usuários limitado. Somente os membros dos grupos selecionados que registram um dispositivo que dá suporte ao Android for Work são registrados como dispositivos Android for Work. Todos os outros são registrados como dispositivos Android.

> [!NOTE]
> Um problema conhecido impede que a opção **Gerenciar dispositivos com suporte para os usuários somente desses grupos como Android para o trabalho** funcione conforme o esperado. Os dispositivos dos usuários nos grupos Azure AD especificados se registrarão como Android, em vez de Android para o trabalho. Para habilitar o Android para o trabalho, você deve usar a opção **Gerenciar todos os dispositivos com suporte como Android para o trabalho**.


Depois da configuração, você precisará permitir que os usuários saibam como registrar seus dispositivos. Consulte [O que dizer aos usuários sobre o registro de seus dispositivos](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Essas informações se aplicam a dispositivos móveis gerenciados pelo Microsoft Intune e pelo Configuration Manager.

Você verá o nome da conta e o nome de organização no portal do Intune quando a associação for concluída. Nesse ponto, você pode fechar ambos os navegadores.

### <a name="enroll-an-android-for-work-device"></a>Registrar um dispositivo Android for Work
 A maneira como os usuários finais registram dispositivos do Android for Work é semelhante ao registro do Android. Os usuários podem baixar e executar o aplicativo de Portal da Empresa para Android em seus dispositivos móveis. O aplicativo solicitará que eles criem um perfil de trabalho como parte do processo de registro.  Depois de criar o perfil de trabalho, os usuários devem mudar para a versão gerenciada do Portal da Empresa. O Portal da Empresa gerenciado é marcado com uma pequena pasta laranja no canto inferior direito.

### <a name="manage-android-for-work-devices"></a>Gerenciar dispositivos Android for Work
Se tiver habilitado o registro do Android for Work, você poderá executar as seguintes tarefas de gerenciamento para dispositivos do Android for Work:
- [Aprovar aplicativos](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [Criar itens de configuração](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Gerenciar configurações de conformidade](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Gerenciar perfis de email](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [Apagar seletivamente o perfil de trabalho](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)

> [!div class="button"]
[< Etapa anterior](create-service-connection-point.md)  [Próxima etapa >](set-up-additional-management.md)

