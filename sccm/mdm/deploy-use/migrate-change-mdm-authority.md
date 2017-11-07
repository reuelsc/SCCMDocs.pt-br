---
title: Alterar a autoridade de MDM para o Intune
titleSuffix: Configuration Manager
description: "Saiba como alterar a autoridade de MDM do Configuration Manager (híbrido) para Intune autônomo."
keywords: 
author: dougeby
manager: angrobe
ms.date: 09/14/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: be503ec9-5324-4f7c-bcf5-77204328e99c
ms.openlocfilehash: 746bf7d7ef7dd411c47840731edfe664510e5a77
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="change-your-mdm-authority-to-intune-standalone"></a>Alterar a autoridade de MDM para o Intune autônomo

*Aplica-se a: System Center Configuration Manager (Branch Atual)*    

Você pode alterar um locatário existente configurado do Microsoft Intune do console do Configuration Manager (MDM híbrido) para o Intune autônomo. Alterar a autoridade de MDM no nível de locatário para o Intune é a fase final do processo de [migrar usuários e dispositivos do MDM híbrido para o Intune autônomo](migrate-hybridmdm-to-intunesa.md) na configuração somente em nuvem.    

> [!Important]    
> Para alterar a autoridade de MDM sem antes migrar os usuários do MDM híbrido para o Intune, confira [Alterar sua autoridade de MDM](change-mdm-authority.md).

As etapas deste tópico alternam a autoridade de MDM do locatário para Intune e migram todos os dispositivos que ainda não foram migrados para o Intune autônomo. Este tópico fornece informações sobre como alterar um locatário existente configurado do Microsoft Intune do console do Configuration Manager (híbrido) para Intune autônomo e supõe que você já tenha concluído as seguintes etapas:
- Usou a [ferramenta Importação de Dados do Intune](migrate-import-data.md) para importar objetos do Configuration Manager para o Intune. 
- [Preparou o Intune para migração do usuário](migrate-prepare-intune.md) a fim de garantir que os usuários e respectivos dispositivos continuem sendo gerenciados depois que forem migrados.
- [Alterou a autoridade de MDM para usuários específicos (autoridade de MDM mista)](migrate-mixed-authority.md) de modo a iniciar o gerenciamento de dispositivos de usuários no portal do Azure.


## <a name="users-and-devices-that-have-not-been-migrated"></a>Usuários e dispositivos que não foram migrados
Você já migrou muitos usuários e testou a funcionalidade do Intune para garantir que tudo funcione conforme o esperado. Sendo assim, as políticas, os perfis, os aplicativos, etc., foram configurados no Intune e você testou completamente os objetos nos dispositivos. Não deve haver exigência por novas configurações para suas políticas no nível de locatário após a alteração na autoridade de MDM. No entanto, em relação aos usuários e dispositivos que não foram migrados anteriormente, leia as seguintes informações quanto ao que esperar após a alteração na autoridade de MDM:    
- Provavelmente haverá um tempo de transição (até oito horas) para que o dispositivo faça check-in e sincronize com o serviço.
- Os dispositivos devem se conectar com o serviço após a alteração para que as configurações da nova autoridade de MDM (Intune autônomo) substituam as configurações existentes no dispositivo.
- Algumas das configurações básicas (como perfis) da autoridade de MDM anterior (híbrido) permanecem no dispositivo por até sete dias. 
- Os dispositivos que não têm usuários associados (normalmente quando você tem o Programa de registro de dispositivos iOS ou cenários de registro em massa) não são migrados para a nova autoridade de MDM. Para esses dispositivos, você precisa chamar o suporte para obter assistência para movê-los para a nova autoridade de MDM.

## <a name="prerequisites"></a>Pré-requisitos
Examine as informações a seguir para se preparar para a alteração para a autoridade de MDM:
- Você deve ter o Configuration Manager versão 1610 ou superior para que a opção que altera a autoridade de MDM esteja disponível.
- Verifique se todos os usuários que estão sendo gerenciados pelo MDM híbrido têm uma licença do Intune/EMS atribuída a eles antes da alteração na autoridade de MDM. Ter essa licença garante que o usuário e seus dispositivos serão gerenciados pelo Intune autônomo após a alteração na autoridade de MDM. Para saber mais, veja [Atribuir licenças do Intune a suas contas de usuário](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Verifique se a conta de usuário administrador tem uma licença do EMS/Intune atribuída.

### <a name="change-the-mdm-authority-to-intune"></a>Alterar a autoridade de MDM para o Intune
Use o procedimento a seguir para alterar a autoridade de MDM no nível de locatário para Intune.

1.  No console do Configuration Manager, vá para **Administração** &gt; **Visão Geral** &gt; **Serviços de Nuvem** &gt; **Assinatura do Microsoft Intune** e exclua sua assinatura do Intune.
2.  Selecione **Alterar a autoridade de MDM para o Microsoft Intune** e, em seguida, clique em **Avançar**.

    ![Caixa de diálogo Remover assinatura do Microsoft Intune](media/mdm-change-delete-subscription.png)
3.  Entre no locatário do Intune que você usou originalmente quando definiu a autoridade de MDM no Configuration Manager.
4.  Clique em **Próximo** e conclua o assistente.
5.  A autoridade de MDM agora está redefinida. A Assinatura do Intune não é mais exibida no nó Assinaturas do Microsoft Intune do console do Configuration Manager.
6.  Faça logon no [Intune no portal do Azure](https://portal.azure.com/#blade/Microsoft_Intune_DeviceSettings/ExtensionLandingBlade/overview) usando o mesmo locatário do Intune utilizado antes.    

  > [!Important]    
  > Não use o console clássico do Intune. Você deve fazer logon no Intune no portal do Azure.
7.  Confirme que a autoridade de MDM foi alterada para **Microsoft Intune**. 

## <a name="next-steps"></a>Próximas etapas
Após a conclusão da alteração da autoridade de MDM, revise as seguintes informações:
- Não deve haver nenhum impacto perceptível para os usuários finais durante a alteração na autoridade de MDM. 
- Não é necessário reconfigurar as políticas no nível de locatário. 
- Você pode editar as políticas no nível de locatário usando o Intune no portal do Azure após a alteração na autoridade de MDM.
-  Depois de alterar a autoridade MDM, execute as etapas a seguir para validar que os novos dispositivos sejam registrados com êxito para a nova autoridade:   
    - Registrar um novo dispositivo
    - Verifique se o dispositivo registrado recentemente é mostrado no Intune.
    - Execute uma ação, como bloqueio remoto, do console de administração para o dispositivo. Se a ação for bem-sucedida, isso significará que o dispositivo está sendo gerenciado pela nova autoridade de MDM.
- Se você tiver problemas com dispositivos específicos, poderá cancelar o registro e registrar novamente os dispositivos para que eles se conectem à nova autoridade e sejam gerenciados o mais rápido possível.
- Em relação aos usuários e dispositivos que não foram migrados anteriormente:
    - Verifique se os dispositivos agora estão sendo exibidos na folha **Dispositivos** como dispositivos gerenciados. Esses dispositivos devem fazer check-in e sincronizar com o serviço após a alteração na autoridade de MDM para que possam ser exibidos. 
    - Quando o serviço Intune detectar que a autoridade de MDM de um locatário foi alterada, ele enviará uma mensagem de notificação para todos os dispositivos registrados de modo a fazer check-in e sincronizar com o serviço (fora do check-in agendado regularmente). Portanto, depois que a autoridade de MDM para o locatário tiver sido alterada de híbrida para o Intune autônomo, todos os dispositivos que estiverem ligados e online se conectarão ao serviço, receberão a nova autoridade de MDM e serão gerenciados pelo Intune autônomo deste ponto em diante. Não haverá interrupção para o gerenciamento e a proteção desses dispositivos.
    - Os dispositivos que estiverem desativados ou offline durante (ou logo após) a alteração na autoridade de MDM se conectarão e sincronizarão com o serviço na nova autoridade de MDM quando estiverem ligados e online.  
    - Os usuários podem alterar rapidamente para a nova autoridade de MDM iniciando manualmente um check-in do dispositivo para o serviço. Os usuários podem fazer check-in facilmente usando o aplicativo Portal da Empresa e iniciando uma verificação de conformidade do dispositivo.
    - Há um período provisório em que um dispositivo está offline durante a alteração na autoridade de MDM e quando esse dispositivo faz check-in no serviço. Para ajudar a garantir que o dispositivo permaneça protegido e funcionando durante esse intervalo, os seguintes perfis permanecerão no dispositivo por até sete dias (ou até que o dispositivo se conecte com a nova autoridade de MDM e receba novas configurações que substituirão as existentes):
        - Perfil de email
        - Perfil da VPN
        - Perfil de certificado
        - Perfil de Wi-Fi
        - Perfis de configuração
    - Contate o suporte para obter ajuda com a alteração da autoridade de MDM em dispositivos que não estão associados a um usuário. 
