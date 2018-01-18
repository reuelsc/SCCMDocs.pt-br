---
title: Preparar dispositivos Windows 10 para o cogerenciamento
description: Saiba como preparar dispositivos Windows 10 para o cogerenciamento.
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/20/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: 
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: d605dd4770be6878b08f4ac61da6ab27e3b6d61f
ms.sourcegitcommit: ac9268e31440ffe91b133c2ba8405d885248d404
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="prepare-windows-10-devices-for-co-management"></a>Preparar dispositivos Windows 10 para o cogerenciamento
Você pode habilitar o cogerenciamento em dispositivos Windows 10 que foram ingressados no AD e no Azure AD e registrados no Intune e em um cliente no Configuration Manager. Para novos dispositivos Windows 10 e dispositivos que já estão registrados no Intune, instale o cliente do Configuration Manager antes que eles possam ser cogerenciados. Para dispositivos Windows 10 que já são clientes do Configuration Manager, você pode registrar os dispositivos no Intune e habilitar o cogerenciamento no console do Configuration Manager.

## <a name="command-line-to-install-configuration-manager-client"></a>Linha de comando para instalar o cliente do Configuration Manager
Você deve criar um aplicativo no Intune para dispositivos Windows 10 que ainda não são clientes do Configuration Manager. Ao criar o aplicativo nas próximas seções, use a seguinte linha de comando:

ccmsetup.msi CCMSETUPCMD="/mp:&#60;*URL do ponto de extremidade de autenticação mútua do gateway de gerenciamento de nuvem*&#62;/ CCMHOSTNAME=&#60;*URL do ponto de extremidade de autenticação mútua do gateway de gerenciamento de nuvem*&#62; SMSSiteCode=&#60;*Código do site*&#62; SMSMP=https:&#47;/&#60;*FQDN do MP*&#62; AADTENANTID=&#60;*ID do locatário do AAD*&#62; AADTENANTNAME=&#60;*Nome do locatário*&#62; AADCLIENTAPPID=&#60;*AppID do servidor para integração com o AAD*&#62; AADRESOURCEURI=https:&#47;/&#60;*ID do recurso*&#62;”

Por exemplo, se você tiver os valores a seguir:

- **URL do ponto de extremidade de autenticação mútua do gateway de gerenciamento de nuvem**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >Use o valor **MutualAuthPath** na exibição de SQL **vProxy_Roles** para o valor da **URL do ponto de extremidade de autenticação mútua do gateway de gerenciamento de nuvem**.

- **FQDN do MP (ponto de gerenciamento)**: sccmmp.corp.contoso.com    
- **Código do site**: PS1    
- **ID do locatário do Azure AD**: 72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Nome do locatário do Azure AD**: contoso    
- **ID do aplicativo cliente do Azure AD**: bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- **URI da ID do recurso do AAD**: ConfigMgrServer    

  > [!Note]    
  > Use o valor **IdentifierUri** encontrado na exibição de SQL **vSMS_AAD_Application_Ex** para o valor do **URI da ID do recurso do AAD**.

Você usaria a seguinte linha de comando:

ccmsetup.msi CCMSETUPCMD="/mp:https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=PS1 SMSMP=https:/&#47;sccmmp.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI=https:/&#47;ConfigMgrServer”

> [!Tip]
> Você pode encontrar os parâmetros de linha de comando para o seu site usando as seguintes etapas:     
> 1. No console do Configuration Manager, acesse **Administração** > **Visão Geral** > **Serviços de Nuvem** > **Cogerenciamento**.  
> 2. Na guia Início, no grupo Gerenciar, escolha **Configurar o cogerenciamento** para abrir o Assistente para Integração de Cogerenciamento.    
> 3. Na página Assinatura, clique em **Entrar**, entre no seu locatário do Intune e, em seguida, clique em **Avançar**.    
> 4. Na página Habilitação, clique em **Copiar** na seção **Dispositivos registrados no Intune** para copiar a linha de comando para a área de transferência e, em seguida, salve a linha de comando, que será usada no procedimento para criar o aplicativo.  
> 5. Clique em **Cancelar** para sair do assistente.

> [!Important]    
> Se você personalizar a linha de comando para instalar o cliente do Configuration Manager, verifique se a linha de comando não excede 1.024 caracteres. Quando a linha de comando for maior que 1.024 caracteres, a instalação do cliente falhará.


## <a name="new-windows-10-devices"></a>Novos dispositivos Windows 10
Para novos dispositivos Windows 10, você pode usar o serviço AutoPilot para definir a configuração inicial pelo usuário, que inclui ingressar o dispositivo no AD e no Azure AD, bem como registrar o dispositivo no Intune. Em seguida, crie um aplicativo no Intune para implantar o cliente do Configuration Manager.  
1. Habilite o AutoPilot para os novos dispositivos Windows 10. Para obter detalhes, consulte [Visão geral do Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).  
2. Configure o registro automático no Azure AD para que seus dispositivos sejam registrados automaticamente no Intune. Para obter detalhes, consulte  [Registrar os dispositivos Windows no Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).
3. Crie um aplicativo no Intune com o pacote do cliente do Configuration Manager e implante o aplicativo nos dispositivos Windows 10 que você deseja cogerenciar. Use a [linha de comando para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) ao percorrer as etapas para [instalar clientes da Internet usando o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).   

## <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Dispositivos Windows 10 não registrados no Intune nem em um cliente do Configuration Manager
Para dispositivos Windows 10 que não estão registrados no Intune e não têm o cliente do Configuration Manager, você pode usar o registro automático para registrar o dispositivo no Intune. Em seguida, crie um aplicativo no Intune para implantar o cliente do Configuration Manager.
1. Configure o registro automático no Azure AD para que seus dispositivos sejam registrados automaticamente no Intune. Para obter detalhes, consulte  [Registrar os dispositivos Windows no Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  
2. Crie um aplicativo no Intune com o pacote do cliente do Configuration Manager e implante o aplicativo nos dispositivos Windows 10 que você deseja cogerenciar. Use a [linha de comando para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) ao percorrer as etapas para [instalar clientes da Internet usando o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).

## <a name="windows-10-devices-enrolled-in-intune"></a>Dispositivos Windows 10 registrados no Intune
Para dispositivos Windows 10 que já estão registrados no Intune, crie um aplicativo no Intune para implantar o cliente do Configuration Manager. Use a [linha de comando para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) ao percorrer as etapas para [instalar clientes da Internet usando o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

## <a name="next-steps"></a>Próximas etapas
[Mudar as cargas de trabalho do Configuration Manager para o Intune](co-management-switch-workloads.md)