---
title: Configurar o gerenciamento de dispositivo híbrido para Android com o Microsoft Intune
titleSuffix: Configuration Manager
description: Preparar para gerenciar dispositivos móveis Android com o Configuration Manager e o Intune.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f833a28a22e4b3ffd2c8fc237effec94e26e69e8
ms.sourcegitcommit: 10b3a571e2a822bbd7b58a25840ee1e6f703a7a2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34814249"
---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar o gerenciamento de dispositivo híbrido do Android com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo ajuda você a habilitar o registro híbrido de dispositivos Android e Android for Work. Em seguida, você pode usar o Configuration Manager para gerenciar os dispositivos por meio de uma assinatura do Microsoft Intune configurada. Os usuários podem baixar o aplicativo Android do portal da empresa no Google Play, que permite registrar dispositivos Android (incluindo Samsung KNOX Standard) e Android for Work.

Com o Configuration Manager, você pode gerenciar as configurações de conformidade, apagar ou excluir dispositivos Android, implantar aplicativos e coletar inventários de hardware e software. Sem o aplicativo Portal da Empresa para Android instalado no dispositivo, você não terá os recursos de gerenciamento, como inventário e configurações de conformidade, mas ainda poderá implantar aplicativos em dispositivos Android.  



## <a name="enable-android-enrollment"></a>Habilitar o registro do Android  
As etapas a seguir permitem que o Configuration Manager gerencie dispositivos Android sem um perfil de trabalho, ou seja, o registro "Android clássico".

1. Antes de configurar o registro para qualquer plataforma, conclua os pré-requisitos e procedimentos em [Configurar MDM híbrido](setup-hybrid-mdm.md).  
2. No console do Configuration Manager, no espaço de trabalho **Administração**, escolha **Visão Geral** > **Serviços de Nuvem** > **Assinatura do Microsoft Intune** e escolha sua assinatura do Intune.  
3. Na guia **Início** do grupo **Assinatura**, escolha **Configurar Plataformas** > **Android**.  
4. Na caixa de diálogo **Propriedades da Assinatura do Microsoft Intune**, escolha a guia **Android** e clique para marcar a caixa de seleção **Habilitar registro do Android**. Escolha **Bloquear dispositivos de propriedade pessoal** para limitar o registro a [dispositivos pré-declarados](predeclare-devices-with-hardware-id.md).

 Após a configuração, será necessário permitir que os usuários saibam como registrar seus dispositivos. Consulte [O que dizer aos usuários sobre o registro de seus dispositivos](/intune/end-user-educate). Essas informações se aplicam a dispositivos móveis gerenciados pelo Microsoft Intune e pelo Configuration Manager.



## <a name="enable-android-for-work-enrollment"></a>Habilitar o registro do Android for Work
As etapas a seguir permitem que o Configuration Manager gerencie dispositivos Android com um perfil de trabalho.

1. [Crie uma conta do Google](https://accounts.google.com/SignUp) a ser usada como a conta do administrador do Android for Work. Também é possível entrar com a conta associada a todas as tarefas de gerenciamento do Android for Work nesse locatário do Intune. Essa conta pode ser do Google compartilhada entre os administradores que gerenciam dispositivos Android. Essa é a conta do Google que sua organização usa para gerenciar e publicar aplicativos no console do Play for Work. Você usará essa conta para aprovar os aplicativos na loja do Play for Work, portanto, mantenha o controle do nome da conta e senha.
2. Habilite o registro do Android associando a conta do Google ao locatário do Intune gerenciado no Configuration Manager:
   1. No console do Configuration Manager, no espaço de trabalho **Administração**, escolha **Visão Geral** > **Serviços de Nuvem** > **Assinaturas do Microsoft Intune** e escolha sua assinatura do Intune.
   2. Na guia **Início** do grupo **Assinatura**, escolha **Configurar Plataformas** > **Android for Work**.
   3. Na caixa de diálogo, escolha **Configurar Android for Work no console do Intune**. O console do Intune é aberto no navegador da Web.
   4. Use suas credenciais de administrador do Intune para entrar no Intune pelo portal do Azure.
   5. Clique em **Google Play Gerenciado**. 
       1. Selecione **Concordo** para conceder à Microsoft a permissão de [enviar informações do usuário e do dispositivo para o Google](/intune/data-intune-sends-to-google).
       2. Selecione **Iniciar Google para conectar-se agora** para abrir o site do Android for Work do Google Play. O site é aberto em uma nova guia no seu navegador.
       3. Na página de entrada do Google, insira a conta do Google da etapa 1.
       4. Forneça o nome da sua empresa em **Nome da organização**. Para **Provedor de EMM (Gerenciamento de Mobilidade Empresarial)**, o "Microsoft Intune" deverá ser exibido. 
       5. Aceite o contrato do Android for Work e, em seguida, escolha **Confirmar**. Sua solicitação será processada.

   6. Na página de entrada do Google, insira as credenciais da conta do Google da etapa 1 e forneça as informações da sua empresa.
3. Quando você voltar para o Intune no portal do Azure, acesse a folha de registro do **Android for Work** e clique em **Perfis de trabalho**. Agora o Android for Work está habilitado. Você tem duas opções de registro para os dispositivos do Android for Work:
   - **Gerenciar todos os dispositivos como Android** (desabilitado). Todos os dispositivos Android, incluindo dispositivos que oferecem suporte ao Android for Work, serão registrados como dispositivos Android convencionais.
   - **Gerenciar dispositivos com suporte como Android for Work** (habilitado). Todos os dispositivos que oferecem suporte ao Android for Work serão registrados como dispositivos Android for Work. Todo dispositivo Android que não é compatível com o Android for Work é registrado como um dispositivo Android convencional.

> [!NOTE]
> Um problema conhecido impede que a opção **Gerenciar dispositivos com suporte para os usuários somente desses grupos como Android para o trabalho** funcione conforme o esperado. Os dispositivos dos usuários nos grupos do Azure AD especificados são inscritos como Android, em vez de Android for Work. Para habilitar o Android for Work, é necessário usar a opção **Gerenciar dispositivos com suporte como Android for Work**.


Depois que você concluir sua configuração, informe aos usuários como eles devem registrar seus dispositivos. Consulte [O que dizer aos usuários sobre o registro de seus dispositivos](/intune/end-user-educate). Essas informações se aplicam a dispositivos móveis gerenciados pelo Microsoft Intune e pelo Configuration Manager.

Quando a associação for concluída, você verá o nome da conta e o nome de organização no Intune no portal do Azure. No momento, você pode fechar os dois navegadores.

### <a name="enroll-an-android-for-work-device"></a>Registrar um dispositivo Android for Work
A maneira como os usuários registram dispositivos Android for Work é semelhante ao registro do Android. Os usuários podem baixar e executar o aplicativo de Portal da Empresa para Android em seus dispositivos móveis. O aplicativo solicitará que eles criem um perfil de trabalho como parte do processo de registro. Após a criação do perfil de trabalho, os usuários devem mudar para a versão gerenciada do Portal da Empresa. O Portal da Empresa gerenciado é marcado com uma pequena pasta laranja no canto inferior direito.

### <a name="manage-android-for-work-devices"></a>Gerenciar dispositivos Android for Work
Após habilitar o registro do Android for Work, será possível executar as seguintes tarefas de gerenciamento para dispositivos Android for Work:
- [Aprovar aplicativos](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [Criar itens de configuração](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Gerenciar configurações de conformidade](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Gerenciar perfis de email](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [Apagar seletivamente o perfil de trabalho](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)

> [!div class="button"]
[< Etapa anterior](create-service-connection-point.md)  [Próxima etapa >](set-up-additional-management.md)
