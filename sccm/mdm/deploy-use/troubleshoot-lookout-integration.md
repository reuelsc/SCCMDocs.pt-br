---
title: "Solucionar problemas da integração ao Lookout | System Center Configuration Manager"
description: "Este tópico descreve a solução de problemas que geralmente ocorrem com a Integração do Lookout."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e36b98c7-d0f4-4dd6-bac3-6a6c4b4bf841
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 399e8b9e2e2dd4621abb6ffca765ce2a69d86b9e
ms.lasthandoff: 03/06/2017


---
# <a name="troubleshoot-lookout-integration-with-intune"></a>Solucionar problemas da integração do Lookout ao Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

## <a name="troubleshoot-login-errors"></a>Solução de problemas de erros de logon
### <a name="403-errors"></a>Erros&403;
Você verá um erro 403 quando você fizer logon no [console do Lookout MTP](https://aad.lookout.com): **você não está autorizado a acessar o serviço** Isso pode acontecer quando o nome de usuário especificado não é um membro do grupo do Azure AD (Active Directory) configurado para acessar o Lookout MTP.

O Lookout MTP está configurado para permitir que apenas os usuários de um grupo do Azure AD configurado tenham acesso. Se você não tiver certeza de qual grupo está configurado com acesso ao Lookout MTP, contate o suporte do Lookout.

Você pode contatar o suporte do Lookout usando os métodos a seguir:

* Email: enterprisesupport@lookout.com
* Faça logon no [Console do MTP](http://aad.lookout.com) e navegue até o módulo **Suporte**.
* Acesse: https://enterprise.support.lookout.com/hc/en-us/requests e faça uma solicitação de suporte.

### <a name="unable-to-sign-in"></a>Não é possível entrar
Você pode ver o seguinte erro quando o usuário administrador global do Azure AD não aceitar a configuração inicial do Lookout.

![captura de tela da tela de logon do Lookout mostrando erro de conexão](media/lookout-consent-not-accepted-error.png)

Para resolver esse problema, o usuário administrador global deve fazer logon em https://aad.lookout.com/les?action=consent e aceitar a solicitação para iniciar a instalação. Informações mais detalhadas podem ser encontradas no tópico [Configurar sua assinatura com o Lookout MTP](set-up-your-subscription-with-lookout.md)

## <a name="troubleshoot-device-status-issues"></a>Solucionar problemas de status do dispositivo

### <a name="device-not-showing-up-in-the-lookout-mtp-console-device-list"></a>O dispositivo não está aparecendo na lista de dispositivos do console do Lookout MTP

Isso pode acontecer em qualquer um dos seguintes cenários:
* Quando o usuário ao qual este dispositivo pertence não está no **Grupo de Registro** especificado no **Console do Lookout MTP**.  Do módulo **Sistema**, acesse a guia **Conector do Intune** e veja as configurações do **Gerenciamento de Registro**.  Você deverá ver um ou mais grupos do Azure AD configurados para o registro.  Verifique se o usuário ao qual o dispositivo ausente pertence faz parte de um dos grupos especificados do Azure AD.  Depois que um novo usuário for adicionado ao grupo de registro, demorará para o intervalo de sondagem configurado (o padrão é&5; minutos) ver o dispositivo no módulo **Dispositivos** do Console do Lookout MTP.

* Se o dispositivo não tiver suporte no Lookout MTP.  Os dispositivos que não têm suporte serão exibidos na seção **Dispositivos Gerenciados** das configurações do conector no Console do Lookout MTP.

### <a name="device-continues-to-be-reported-as-pending"></a>O dispositivo continuará a ser relatado como **pendente**

Um dispositivo exibido como **Pendente** significa que o usuário final não abriu o aplicativo Lookout for Work e tocou no botão **Ativar**. Para obter mais detalhes sobre a ativação do dispositivo com o aplicativo Lookout for Work, leia o tópico a seguir:

[Será solicitada a instalação do aplicativo Lookout for Work em seu dispositivo Android ](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

### <a name="in-the-lookout-mtp-console-a-device-is-showing-as-active-but-does-not-have-a-device-id"></a>No console do Lookout MTP, um dispositivo está sendo exibido como ativo, mas não tem uma ID de dispositivo.
Isso significa que o usuário ao qual este dispositivo pertence não está no grupo de registro especificado no Console do Lookout MTP.   Um dispositivo pode ficar nesse estado se o usuário ao qual o dispositivo pertence foi removido do grupo de registro ou se o grupo de registro ao qual o usuário pertence foi removido.

No módulo **Sistema** do console do Lookout MTP, acesse a guia **Conector do Intune** e examine as configurações do **Registro**.  Você deverá ver um ou mais grupos do Azure AD configurados para o registro.  Verifique se o usuário ao qual o dispositivo pertence faz parte de um dos grupos especificados do Azure AD.

Enquanto um dispositivo estiver nesse estado, o Lookout continuará a notificar o usuário de quaisquer ameaças detectadas, mas não enviará nenhuma informação de ameaça ao Intune.

### <a name="device-shows-disconnected-state"></a>O dispositivo exibe o estado desconectado

Desconectado significa que o Lookout MTP não recebeu sinal do dispositivo durante um intervalo de tempo pré-configurado (o padrão é 30 dias com um mínimo de sete dias). Isso significa que o aplicativo Portal da Empresa ou o aplicativo Lookout for Work não está instalado no dispositivo ou foi desinstalado. A reinstalação dos aplicativos deve solucionar esse problema. Quando o usuário abrir o Lookout for Work e ativar o aplicativo, o dispositivo será ressincronizado com o Lookout MTP e com o Intune.

### <a name="forcing-a-resync-on-the-device"></a>Forçando uma ressincronização do dispositivo
No módulo **Dispositivos** do console do Lookout MTP, o administrador pode selecionar o dispositivo e optar por excluí-lo.   Na próxima vez que o proprietário do dispositivo abrir o aplicativo Lookout for Work e tocar em **Ativar**, o estado do dispositivo fará uma ressincronização completa.

### <a name="the-owner-of-the-device-is-no-longer-using-this-device"></a>O proprietário do dispositivo não está mais usando este dispositivo
Você deve apagar o dispositivo e pedir ao novo usuário para se registrar conforme descrito [neste tópico](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/wipe-lock-reset-devices#full-wipe).


Você também pode ir ao módulo **Dispositivos** do Console do Lookout MTP e escolher **Excluir**.

Desde que o novo usuário esteja em um dos grupos de registro especificados no console do Lookout MTP, o dispositivo será exibido depois que o Azure AD associar o dispositivo ao novo usuário.

## <a name="compliance-remediation-workflows"></a>Fluxos de trabalho de correção de conformidade
[Será solicitada a instalação do Lookout for Work em seu dispositivo Android]( http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

[Você precisa resolver uma ameaça que o Lookout for Work encontrou em seu dispositivo Android ](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)

