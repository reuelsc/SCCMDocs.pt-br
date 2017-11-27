---
title: Alterar sua autoridade de MDM
titleSuffix: Configuration Manager
description: "Saiba como alterar a autoridade do MDM do Configuration Manager (híbrido) para o Intune autônomo"
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/17/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: c61a44cce443a7ff210a626d114068691541aaae
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="change-your-mdm-authority"></a>Alterar sua autoridade de MDM
A partir do Configuration Manager versão 1610, você pode alterar sua autoridade MDM sem precisar entrar em contato com o Suporte da Microsoft e sem a necessidade de cancelar o registro e registrar novamente os dispositivos gerenciados existentes. Este artigo fornece as etapas para alterar um locatário existente do Microsoft Intune configurado pelo console do Configuration Manager (híbrido) para o Intune autônomo. Quando você concluir as etapas neste artigo, os dispositivos passarão a ser gerenciados pelo Microsoft Intune no [Portal do Azure](https://portal.azure.com). 

> [!Note]    
> Se você quiser alterar para o Configuration Manager (híbrido) um locatário existente do Microsoft Intune, com a autoridade de MDM definida para o Intune, consulte [Alterar a autoridade de MDM](https://docs.microsoft.com/intune-classic/deploy-use/change-mdm-authority).

> [!Important]    
> Este artigo é indicado para alterar a sua autoridade de MDM quando você ainda não migrou usuários. Para alterar a autoridade de MDM depois de ter [migrado um subconjunto de usuários](migrate-hybridmdm-to-intunesa.md), confira [Alterar a autoridade de MDM](migrate-change-mdm-authority.md).

## <a name="key-considerations"></a>Principais considerações
Depois de alterar para a nova autoridade de MDM, provavelmente haverá um tempo de transição (até oito horas) antes de o dispositivo fazer o check-in e sincronizar com o serviço. Você deve definir as configurações na nova autoridade de MDM (Intune autônomo) para garantir que os dispositivos registrados continuarão a ser gerenciados e protegidos após a alteração. Observe as seguintes considerações:
- Os dispositivos devem se conectar ao serviço após a alteração para que as configurações da nova autoridade de MDM (Intune autônomo) substituam as configurações existentes no dispositivo.
- Depois de alterar a autoridade de MDM, algumas das configurações básicas (como perfis) da autoridade de MDM anterior (híbrido) permanecem no dispositivo por até sete dias. É recomendável configurar aplicativos e configurações (políticas, perfis, aplicativos etc.) na nova autoridade de MDM assim que possível. Além disso, implante as configurações nos grupos de usuários que contêm usuários com dispositivos registrados existentes. Quando um dispositivo se conecta ao serviço após a alteração na autoridade de MDM, ele recebe novas configurações da nova autoridade de MDM. As políticas de destino recentes substituirão as políticas existentes no dispositivo.
- Depois que você alterar para a nova autoridade de MDM, poderá levar até uma semana para que os dados de conformidade no [Portal do Azure](https://portal.azure.com) sejam relatados com precisão. No entanto, os estados de conformidade no Azure Active Directory e no dispositivo serão precisos, então o dispositivo ainda estará protegido.
- Os dispositivos que não têm usuários associados (normalmente quando você tem o Programa de registro de dispositivos iOS ou cenários de registro em massa) não são migrados para a nova autoridade de MDM. Para esses dispositivos, você precisa chamar o suporte para obter assistência para movê-los para a nova autoridade de MDM.

## <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>Preparar para alterar a autoridade de MDM para o Intune autônomo
Examine as informações a seguir para se preparar para a alteração para a autoridade de MDM:
- Você deve ter o Configuration Manager versão 1610 ou superior para que a opção que altera a autoridade de MDM esteja disponível.
- Pode levar até oito horas para um dispositivo se conectar ao serviço depois que você alterar para a nova autoridade de MDM.
- Verifique se todos os usuários que estão sendo gerenciados pelo híbrido têm uma licença do Intune/EMS atribuída a eles antes da alteração na autoridade de MDM. Ter essa licença garante que o usuário e seus dispositivos serão gerenciados pelo Intune autônomo após a alteração na autoridade de MDM. Para saber mais, veja [Atribuir licenças do Intune a suas contas de usuário](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Verifique se a conta de usuário administrador tem uma licença do Intune/EMS atribuída e confirme que a conta de usuário do administrador pode entrar no Intune antes da alteração para a autoridade de MDM. A autoridade de MDM deverá exibir **Definir para o Configuration Manager** (locatário híbrido) no Intune no [Portal do Azure](https://portal.azure.com) antes da alteração na autoridade de MDM.
- Não deve haver nenhum impacto perceptível para os usuários finais durante a alteração na autoridade de MDM. 

## <a name="change-the-mdm-authority-to-intune-standalone"></a>Alterar a autoridade de MDM para o Intune autônomo
O processo para alterar a autoridade de MDM para o Intune autônomo inclui as seguintes etapas de alto nível:  
- No console do Configuration Manager, use a opção **Alterar a autoridade de MDM para o Microsoft Intune** para remover a assinatura existente do Microsoft Intune.
- No Intune no [Portal do Azure](https://portal.azure.com), configure e implante as novas configurações e os aplicativos da nova autoridade de MDM (Intune).
- Da próxima vez que o dispositivo se conectar ao serviço, ele sincronizará e receberá as novas configurações da nova autoridade de MDM.

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>Para alterar a autoridade de MDM para o Intune autônomo
1. No console do Configuration Manager, vá para **Administração** &gt; **Visão Geral** &gt; **Serviços de Nuvem** &gt; **Assinatura do Microsoft Intune** e exclua sua assinatura do Intune.
2. Selecione **Alterar a autoridade de MDM para o Microsoft Intune** e, em seguida, clique em **Avançar**.
   ![Baixar a solicitação de certificado APNs](./media/mdm-change-delete-subscription.png)
3. Entre no locatário do Intune que você usou originalmente quando definiu a autoridade de MDM no Configuration Manager.
4. Clique em **Próximo** e conclua o assistente.
5. A autoridade MDM agora está definida para **Microsoft Intune**. A assinatura do Intune não deve ser exibida no nó de assinaturas do Microsoft Intune do console do Configuration Manager. 
6. Para verificar se a autoridade de MDM está definida, execute as seguintes etapas: a. Entre no [Portal do Azure](https://portal.azure.com) usando o mesmo locatário do Intune que você usou anteriormente. 
    b. Escolha **Mais Serviços** > **Monitoramento + Gerenciamento** > **Intune** > **Registro de dispositivos**. A autoridade de MDM é exibida na seção superior direita da folha **Visão geral**. 

## <a name="next-steps"></a>Próximas etapas
Depois de a alteração na autoridade de MDM ser concluída, examine as seguintes etapas:
- Quando o serviço Intune detectar que a autoridade de MDM de um locatário foi alterada, ele enviará uma mensagem de notificação solicitando que todos os dispositivos registrados façam check-in e sejam sincronizados com o serviço (isso ocorre fora do check-in agendado regularmente). Portanto, depois que a autoridade de MDM para o locatário tiver sido alterada de híbrida para o Intune autônomo, todos os dispositivos que estiverem ligados e online se conectarão ao serviço, receberão a nova autoridade de MDM e serão gerenciados pelo Intune autônomo no futuro. Não haverá interrupção para o gerenciamento e a proteção desses dispositivos.
- Os dispositivos que estiverem desativados ou offline durante (ou logo após) a alteração na autoridade de MDM se conectarão e sincronizarão com o serviço na nova autoridade de MDM quando estiverem ligados e online.  
- Os usuários podem alterar rapidamente para a nova autoridade de MDM iniciando manualmente um check-in do dispositivo para o serviço. Os usuários podem fazer isso facilmente pelo aplicativo Portal da Empresa e iniciando uma verificação de conformidade do dispositivo.
- Após a alteração da autoridade de MDM, para verificar se tudo está funcionando corretamente depois que os dispositivos fizerem check-in e forem sincronizados com o serviço, procure os dispositivos no [Portal do Azure](https://portal.azure.com). Os dispositivos que antes eram gerenciados pelo Configuration Manager (híbrido) agora serão exibidos como dispositivos gerenciados no Intune.    
- Há um período provisório em que um dispositivo está offline durante a alteração na autoridade de MDM e quando esse dispositivo faz check-in no serviço. Para ajudar a garantir que o dispositivo permaneça protegido e funcionando durante esse intervalo, os seguintes itens permanecerão no dispositivo por até sete dias (ou até que o dispositivo se conecte com a nova autoridade de MDM e receba as novas configurações que substituirão as existentes):
    - Perfil de email
    - Perfil da VPN
    - Perfil de certificado
    - Perfil de Wi-Fi
    - Perfis de configuração
- Verifique se as novas configurações que se destinam a substituir as configurações existentes têm o mesmo nome que as anteriores para garantir que as configurações antigas sejam substituídas. Caso contrário, os dispositivos podem acabar com políticas e perfis redundantes.    

  > [!TIP]   
  > Como prática recomendada, você deve criar todos os parâmetros de gerenciamento e as configurações, além das implantações, logo após a alteração para a autoridade de MDM ser concluída. Isso ajuda a garantir que os dispositivos estejam protegidos e sejam gerenciados ativamente durante esse intervalo.   
-  Depois de alterar a autoridade MDM, execute as etapas a seguir para validar que os novos dispositivos sejam registrados com êxito para a nova autoridade:   
    - Registrar um novo dispositivo
    - Verifique se o dispositivo recém-registrado aparece no [Portal do Azure](https://portal.azure.com).
    - Execute uma ação no dispositivo, como Bloqueio Remoto, por meio do [Portal do Azure](https://portal.azure.com). Se a ação for bem-sucedida, isso significará que o dispositivo está sendo gerenciado pela nova autoridade de MDM.
- Se você tiver problemas com dispositivos específicos, poderá cancelar o registro e registrar novamente os dispositivos para que eles se conectem à nova autoridade e sejam gerenciados o mais rápido possível.