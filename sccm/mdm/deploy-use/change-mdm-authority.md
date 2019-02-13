---
title: Alterar sua autoridade de MDM
titleSuffix: Configuration Manager
description: Saiba como alterar a autoridade do MDM do Configuration Manager (híbrido) para o Intune autônomo
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/14/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.collection: M365-identity-device-management
ms.openlocfilehash: c0420113feaaf9c9485b8d1e3d488b07878c61b5
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131958"
---
# <a name="change-your-mdm-authority"></a>Alterar sua autoridade de MDM

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode alterar sua autoridade de MDM sem precisar contatar o Suporte da Microsoft nem cancelar o registro dos dispositivos gerenciados existentes e registrá-los novamente. Este artigo fornece as etapas para alterar um locatário existente do Microsoft Intune configurado pelo console do Configuration Manager (híbrido) para o Intune autônomo. Quando você concluir as etapas neste artigo, os dispositivos serão gerenciados pelo Microsoft Intune no [Portal do Azure](https://portal.azure.com). 

Este artigo é indicado para alterar a sua autoridade de MDM quando você ainda não migrou usuários. Para alterar a autoridade do MDM depois de ter [migrado um subconjunto de usuários](migrate-hybridmdm-to-intunesa.md), consulte [Alterar a autoridade do MDM](migrate-change-mdm-authority.md).

> [!Important]  
> A partir de 13 de agosto de 2018, o gerenciamento de dispositivos móveis híbrido é um [recurso preterido](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para saber mais, confira [O que é o MDM híbrido](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="key-considerations"></a>Principais considerações

Depois que você alterar a autoridade de MDM, haverá um tempo de transição de até oito horas. Esse é o tempo necessário para que o dispositivo faça check-in e seja sincronizado com o serviço. Para garantir que os dispositivos registrados continuem a ser gerenciados e protegidos após a alteração, defina as configurações diretamente no Intune. Observe as seguintes considerações:

- Os dispositivos devem se conectar ao serviço após a alteração para que as configurações da nova autoridade de MDM (Intune autônomo) substituam as configurações existentes no dispositivo.  

- Depois de alterar a autoridade de MDM, algumas das configurações básicas (como perfis) da autoridade de MDM anterior (híbrido) permanecem no dispositivo por até sete dias. É recomendável configurar aplicativos e configurações (políticas, perfis, aplicativos etc.) na nova autoridade de MDM assim que possível. Além disso, implante as configurações nos grupos de usuários que contêm usuários com dispositivos registrados existentes. Quando um dispositivo se conecta ao serviço após a alteração na autoridade de MDM, ele recebe novas configurações da nova autoridade de MDM. As políticas de destino recentes substituirão as políticas existentes no dispositivo.  

- Depois que você alterar para a nova autoridade de MDM, poderá levar até uma semana para que os dados de conformidade no [Portal do Azure](https://portal.azure.com) sejam relatados com precisão. No entanto, os estados de conformidade no Azure Active Directory e no dispositivo são precisos. O dispositivo ainda está protegido.  

- Os dispositivos que não têm usuários associados não são migrados para a nova autoridade de MDM. Esse comportamento geralmente ocorre quando você tem o Programa de registro de dispositivos iOS ou cenários de registro em massa. No caso desses dispositivos, contate o suporte para obter assistência para passá-los à nova autoridade de MDM.  



## <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>Preparar para alterar a autoridade de MDM para o Intune autônomo

Examine as informações a seguir para se preparar para a alteração para a autoridade de MDM:

- Pode levar até oito horas para um dispositivo se conectar ao serviço depois que você alterar para a nova autoridade de MDM.  

- Verifique se todos os usuários que estão sendo gerenciados pelo híbrido têm uma licença do Intune/EMS atribuída a eles antes da alteração na autoridade de MDM. Esta licença garante que o usuário e seus dispositivos sejam gerenciados pelo Intune autônomo após a alteração da autoridade de MDM. Para saber mais, veja [Atribuir licenças do Intune a suas contas de usuário](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).  

- Verifique se a conta de usuário administrador tem uma licença do EMS/Intune atribuída. Confirme se a conta de usuário administrador pode entrar no Intune antes da alteração da autoridade de MDM. A autoridade de MDM deverá exibir **Definir para o Configuration Manager** (locatário híbrido) no Intune no [Portal do Azure](https://portal.azure.com) antes da alteração na autoridade de MDM.  

- Não deve haver nenhum impacto perceptível para os usuários finais durante a alteração na autoridade de MDM. 



## <a name="change-the-mdm-authority-to-intune-standalone"></a>Alterar a autoridade de MDM para o Intune autônomo

O processo para alterar a autoridade de MDM para o Intune autônomo inclui as seguintes etapas de alto nível:  

- No console do Configuration Manager, use a opção **Alterar a autoridade de MDM para o Microsoft Intune** para remover a assinatura existente do Microsoft Intune.  

- No Intune no [Portal do Azure](https://portal.azure.com), configure e implante as novas configurações e os aplicativos da nova autoridade de MDM (Intune).  

- Da próxima vez que o dispositivo se conectar ao serviço, ele sincronizará e receberá as novas configurações da nova autoridade de MDM.  

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>Para alterar a autoridade de MDM para o Intune autônomo
1. No console do Configuration Manager, acesse o workspace **Administração**. Expanda **Serviços de Nuvem** e selecione o nó **Assinatura do Microsoft Intune**. Exclua sua assinatura existente do Intune.  

2. Selecione **Alterar a autoridade de MDM para o Microsoft Intune** e, em seguida, clique em **Avançar**.  

   ![Assistente para Remover Assinatura do Microsoft Intune, página de introdução](./media/mdm-change-delete-subscription.png)

3. Entre no locatário do Intune que você usou originalmente quando definiu a autoridade de MDM no Configuration Manager.  

4. Clique em **Próximo** e conclua o assistente.  

5. A autoridade MDM agora está definida para **Microsoft Intune**. A Assinatura do Intune não é exibida no nó Assinaturas do Microsoft Intune do console do Configuration Manager.  

6. Para verificar se a autoridade de MDM está definida, execute as seguintes etapas:  

    1. Entre no [Portal do Azure](https://portal.azure.com) usando o mesmo locatário do Intune que você usou anteriormente.  

    2. Escolha **Todos os Serviços** > **Intune** > **Registro de dispositivo**. A autoridade de MDM é exibida na seção superior direita de **Visão Geral**.  



## <a name="next-steps"></a>Próximas etapas

Depois de a alteração na autoridade de MDM ser concluída, examine as seguintes etapas:  

- Quando o serviço Intune detecta que a autoridade de MDM de um locatário foi alterada, ele envia uma mensagem de notificação a todos os dispositivos registrados para que eles façam check-in e sejam sincronizados com o serviço. Esse comportamento está fora do check-in agendado regularmente. Portanto, depois que você alterar a autoridade de MDM do locatário de híbrida para o Intune autônomo, todos os dispositivos que estiverem ligados e online se conectarão ao serviço, receberão a nova autoridade de MDM e serão gerenciados pelo Intune autônomo. Não há interrupção no gerenciamento e na proteção desses dispositivos.  

- Os dispositivos que estiverem desativados ou offline durante (ou logo após) a alteração na autoridade de MDM se conectarão e sincronizarão com o serviço na nova autoridade de MDM quando estiverem ligados e online.   

- Os usuários podem alterar rapidamente para a nova autoridade de MDM iniciando manualmente um check-in do dispositivo para o serviço. Os usuários podem executar essa ação facilmente usando o aplicativo Portal da Empresa e iniciando uma verificação de conformidade do dispositivo.  

- Após a alteração da autoridade de MDM, para verificar se tudo está funcionando corretamente depois que os dispositivos fizerem check-in e forem sincronizados com o serviço, procure os dispositivos no [Portal do Azure](https://portal.azure.com). Os dispositivos que antes eram gerenciados pelo Configuration Manager (híbridos) agora são exibidos como dispositivos gerenciados no Intune.    

- Há um período provisório em que um dispositivo está offline durante a alteração na autoridade de MDM e quando esse dispositivo faz check-in no serviço. Para ajudar a garantir que o dispositivo permaneça protegido e funcionando durante esse intervalo, os seguintes perfis permanecerão no dispositivo por até sete dias (ou até que o dispositivo se conecte com a nova autoridade de MDM e receba novas configurações que substituirão as existentes):  
    - Perfil de email
    - Perfil da VPN
    - Perfil de certificado
    - Perfil de Wi-Fi
    - Perfis de configuração  

- Para substituir as configurações antigas, verifique se as novas configurações que devem substituir as configurações existentes têm o mesmo nome que as anteriores. Caso contrário, os dispositivos podem acabar com políticas e perfis redundantes.    

  > [!TIP]   
  > Crie todos os parâmetros de gerenciamento e as configurações, além das implantações, logo após a alteração para a autoridade de MDM ser concluída. Essa ação ajuda a proteger e gerenciar ativamente os dispositivos durante o período intermediário.   

-  Depois de alterar a autoridade MDM, execute as etapas a seguir para validar que os novos dispositivos sejam registrados com êxito para a nova autoridade:   

    - Registrar um novo dispositivo  

    - Verifique se o dispositivo recém-registrado aparece no [Portal do Azure](https://portal.azure.com).  

    - Execute uma ação no dispositivo, como Bloqueio Remoto, por meio do [Portal do Azure](https://portal.azure.com). Se a ação for bem-sucedida, isso significa que o dispositivo está sendo gerenciado pela nova autoridade de MDM.  
    
- Se você tiver problemas com dispositivos específicos, cancele o registro dos dispositivos e registre-os novamente. Essa ação conecta os dispositivos à nova autoridade e faz com que eles sejam gerenciados o mais rápido possível.  

- Se você habilitar o [Android for Work](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client) como um locatário híbrido e, em seguida, migrar o locatário para o Intune autônomo, a configuração do Android for Work nas restrições de registro poderá ser exibida como bloqueada em vez de permitir. Defina-a manualmente como **Permitir** para habilitar novamente o registro do Android for Work.<!--512117-->  

- Depois de alterar a autoridade de MDM, o token Apple VPP e os [aplicativos iOS associados a ele adquiridos por volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps) não são removidos automaticamente. Para limpar essas informações, siga as etapas em [Excluir um token do Apple VPP](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps#delete-an-apple-vpp-token). Depois que a operação for concluída, o site removerá o token. Ele também remove do nó da App Store Licenciada os metadados do aplicativo para esse token.<!--SCCMDocs issue 579-->  

    Em raras ocorrências, você verá um erro de que o site não pôde excluir o objeto de gerenciamento.  

    - Se o token não estiver visível, ignore o erro  

    - Se o token ainda estiver listado, tente excluí-lo novamente  

