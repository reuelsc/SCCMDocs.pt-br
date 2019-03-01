---
title: Alterar a autoridade de MDM para o Intune
titleSuffix: Configuration Manager
description: Saiba como alterar a autoridade de MDM do Configuration Manager (híbrido) para Intune autônomo.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 02/27/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: be503ec9-5324-4f7c-bcf5-77204328e99c
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9d6a909be4b1817b9a251046d666839e2e351443
ms.sourcegitcommit: 0bf253085adeca0d9ea62d76497eb5ebf5ce89da
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2019
ms.locfileid: "57012421"
---
# <a name="change-your-mdm-authority-to-intune-standalone"></a>Alterar a autoridade de MDM para o Intune autônomo

*Aplica-se a: System Center Configuration Manager (Branch Atual)*    

Você pode alterar um locatário existente configurado do Microsoft Intune do console do Configuration Manager (MDM híbrido) para o Intune autônomo. Alterar a autoridade de MDM no nível de locatário para o Intune é a fase final do processo de [migrar usuários e dispositivos do MDM híbrido para o Intune autônomo](migrate-hybridmdm-to-intunesa.md) na configuração somente em nuvem.    

> [!Important]    
> Para alterar a autoridade de MDM sem antes migrar os usuários do MDM híbrido para o Intune, confira [Alterar sua autoridade de MDM](change-mdm-authority.md).

Este artigo fornece informações sobre como alterar um locatário existente do Microsoft Intune configurado no console do Configuration Manager (híbrido) para o Intune autônomo. Ele pressupõe que você já concluiu as etapas a seguir:
- Usou a [ferramenta Importação de Dados do Intune](migrate-import-data.md) para importar objetos do Configuration Manager para o Intune. 
- [Preparar o Intune para migração do usuário](migrate-prepare-intune.md) a fim de garantir que os usuários e respectivos dispositivos continuem sendo gerenciados depois da migração.
- [Alterou a autoridade de MDM para usuários específicos (autoridade de MDM mista)](migrate-mixed-authority.md) de modo a iniciar o gerenciamento de dispositivos de usuários no portal do Azure.


## <a name="users-and-devices-that-havent-been-migrated"></a>Os usuários e dispositivos que ainda não foram migrados
Você já migrou muitos usuários e testou a funcionalidade do Intune para garantir que as coisas estão funcionando conforme o esperado. Você configurou políticas, perfis e aplicativos no Intune e você testou completamente os objetos nos dispositivos. Não deve haver exigência por novas configurações para suas políticas no nível de locatário após a alteração na autoridade de MDM. No entanto, para usuários e dispositivos que você ainda não migrados anteriormente, examine as seguintes informações sobre o que esperar após a alteração na autoridade de MDM:    

- Provavelmente haverá um tempo de transição de até oito horas antes do dispositivo fizer check-in e sincronize com o serviço.  

- Os dispositivos devem se conectar com o serviço após a alteração para que as configurações da nova autoridade de MDM (Intune autônomo) substituam as configurações existentes no dispositivo.  

- Algumas das configurações básicas (como perfis) da autoridade de MDM anterior (híbrido) permanecem no dispositivo por até sete dias.  

- Os dispositivos que não têm usuários associados não são migrados para a nova autoridade de MDM. Normalmente, esses dispositivos são com cenários para o programa de registro de dispositivo iOS ou registro em massa. Para esses dispositivos, você precisa chamar o suporte para obter assistência para movê-los para a nova autoridade de MDM.



## <a name="prerequisites"></a>Pré-requisitos
Examine as informações a seguir para se preparar para a alteração para a autoridade de MDM:
- Você deve ter o Configuration Manager versão 1610 ou superior para que a opção que altera a autoridade de MDM esteja disponível.
- Certifique-se de atribuir uma licença do Intune/EMS para todos os usuários atualmente gerenciados pelo MDM híbrido. A licença garante que o usuário e seus dispositivos são gerenciados pelo Intune autônomo após a alteração na autoridade de MDM. Para saber mais, veja [Atribuir licenças do Intune a suas contas de usuário](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Verifique se a conta de usuário administrador tem uma licença do EMS/Intune atribuída.

## <a name="change-the-mdm-authority-to-intune"></a>Alterar a autoridade de MDM para o Intune
Use o procedimento a seguir para alterar a autoridade de MDM no nível de locatário para Intune.

1. No console do Configuration Manager, vá para o **Administration** espaço de trabalho, expanda **serviços de nuvem**e selecione o **assinatura do Microsoft Intune** nó. Exclua sua assinatura existente do Intune.  

2. Selecione **alterar a autoridade de MDM para o Microsoft Intune**e, em seguida, selecione **próxima**.

    ![Caixa de diálogo Remover assinatura do Microsoft Intune](media/mdm-change-delete-subscription.png)  

3. Entre no locatário do Intune que você usou originalmente quando definiu a autoridade de MDM no Configuration Manager. Selecione **próxima** e conclua o assistente.

    A autoridade de MDM agora está redefinida. A Assinatura do Intune não é mais exibida no nó Assinaturas do Microsoft Intune do console do Configuration Manager.  

4. Entrar para o [portal do Intune](https://aka.ms/IntunePortal).

5. Selecione **registro de dispositivo**.  

6. Na visão geral de registro do dispositivo, consulte a **autoridade de MDM** propriedade.

   > [!Important]    
   > Não use o console clássico do Intune. Entrar no Intune no portal do Azure.  

7. Confirme que a autoridade de MDM foi alterada para **Microsoft Intune**. 



## <a name="after-migration"></a>Após a migração

Após a conclusão da alteração da autoridade de MDM, revise as seguintes informações:

- Não deve haver nenhum impacto perceptível para os usuários finais durante a alteração na autoridade de MDM.  

- Você não precisará reconfigurar as políticas de nível de locatário.  

- Se você precisar editar as políticas no nível do locatário, faça essa ação do Intune no portal do Azure.  

- Se você tiver problemas com dispositivos específicos, cancele o registro dos dispositivos e registre-os novamente. Essa ação lhes conectado para a nova autoridade e gerenciado mais rápido possível.


#### <a name="validate-new-device-enrollment"></a>Validar o novo registro de dispositivo
Depois de alterar a autoridade de MDM, use as etapas a seguir para validar que os novos dispositivos sejam registrados com êxito para a nova autoridade:   
1. Registrar um novo dispositivo
2. Verifique se que o dispositivo registrado recentemente aparece no Intune
3. Inicie uma ação de dispositivo do portal do Intune, como [bloqueio remoto](https://docs.microsoft.com/intune/device-remote-lock). Se for bem-sucedida, o dispositivo com êxito é gerenciado pela nova autoridade de MDM.


#### <a name="for-users-and-devices-that-you-havent-previously-migrated"></a>Para usuários e dispositivos que você ainda não migrados anteriormente

- Verificar se os dispositivos agora são exibidos na **dispositivos** página como dispositivos gerenciados. Antes que eles são exibidos, esses dispositivos devem fazer check-in e sincronizar com o serviço após a alteração na autoridade de MDM. 

- Quando o serviço Intune detectar que a autoridade MDM de um locatário foi alterada, ele envia uma mensagem de notificação para todos os dispositivos registrados. Ele instrui dispositivos para fazer check-in e sincronizar com o serviço. Essa notificação ocorre fora do check-in agendado regularmente. Depois de alterar a autoridade de MDM para o locatário de híbrida para o Intune autônomo, todos os dispositivos online se conectar com o serviço. Eles receberão a nova autoridade MDM e, em seguida, são gerenciados pelo Intune autônomo de agora em diante. Não há nenhuma interrupção para o gerenciamento e a proteção desses dispositivos.

- Para dispositivos que estiverem offline durante ou logo após a alteração na autoridade de MDM, eles se conectem e sincronizar com o serviço sob a nova autoridade MDM quando eles são ligados e online.  

- Você pode alterar rapidamente para a nova autoridade MDM iniciando manualmente um check-in do dispositivo para o serviço. Use o aplicativo de Portal da empresa para iniciar uma verificação de conformidade do dispositivo.

- Há um período provisório, quando um dispositivo estiver offline durante a alteração na autoridade de MDM e que o dispositivo faz check-in do serviço. Para garantir que o dispositivo permaneça protegido e funcional durante esse período provisório, os seguintes perfis permanecerão no dispositivo por até sete dias. Eles também podem permanecer até que o dispositivo se conecta com a nova autoridade MDM e receba novas configurações que substituirão as existentes:
    - Perfil de email
    - Perfil da VPN
    - Perfil de certificado
    - Perfil de Wi-Fi
    - Perfis de configuração

- Para dispositivos que não estão associados um usuário, contate o suporte para ajudar a alterar a autoridade de MDM. 

#### <a name="bkmk-ki-dep"></a> Registros de dispositivo DEP da Apple
<!--ICM 105091970--> Depois de concluir a migração do MDM híbrido, você pode observar o dispositivo DEP da Apple registros permanecem no console do Configuration Manager. Depois que você alterar a autoridade de MDM para o Intune, você não pode remover esses dispositivos do Configuration Manager. 

Há duas soluções alternativas:

- Se você vir esse comportamento antes de alterar a autoridade de MDM, em seguida, exclua os registros DEP do Configuration Manager.  

- Se você já tiver migrado e ainda estiver usando o Configuration Manager, use o seguinte comando SQL no banco de dados do site para remover os registros:  

    ```SQL
    Delete from MDMCorpOwnedDevices where DeviceType=8 and DiscoverySources=4
    ```



## <a name="next-steps"></a>Próximas etapas

Agora que a migração for concluída, gerencie dispositivos móveis com o Intune. Para obter mais informações, consulte [o que há de novo no Microsoft Intune](https://docs.microsoft.com/intune/whats-new).

