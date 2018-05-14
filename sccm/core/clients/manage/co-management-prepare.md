---
title: Preparar o Windows 10 para o cogerenciamento
titleSuffix: Configuration Manager
description: Saiba como preparar dispositivos Windows 10 para o cogerenciamento.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/28/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 8c025d7c7a1dc452cb96f937801656bc4d0cadab
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="prepare-windows-10-devices-for-co-management"></a>Preparar dispositivos Windows 10 para o cogerenciamento
Você pode habilitar o cogerenciamento em dispositivos Windows 10 que foram ingressados no AD e no Azure AD e registrados no Microsoft Intune e em um cliente no Configuration Manager. Para novos dispositivos Windows 10 e dispositivos que já estão registrados no Intune, instale o cliente do Configuration Manager antes que eles possam ser cogerenciados. Para dispositivos Windows 10 que já são clientes do Configuration Manager, você pode registrar os dispositivos no Intune e habilitar o cogerenciamento no console do Configuration Manager.

> [!IMPORTANT]
> Dispositivos móveis Windows 10 não são compatíveis com o cogerenciamento.


## <a name="prerequisites"></a>Pré-requisitos
Você deve ter os seguintes pré-requisitos em vigor antes de habilitar o cogerenciamento. Há pré-requisitos gerais e pré-requisitos diferentes para dispositivos com o cliente do Configuration Manager e para dispositivos que não têm o cliente instalado.
### <a name="general-prerequisites"></a>Pré-requisitos gerais
Estes são os pré-requisitos gerais para habilitar o cogerenciamento:  

- Configuration Manager versão 1710 ou posterior
- [Site carregado com o Azure AD para gerenciamento de nuvem](/sccm/core/servers/deploy/configure/azure-services-wizard)
- Licença do EMS ou do Intune para todos os usuários
- [Registro automático do Azure AD](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) habilitado
- Assinatura do Intune &#40;autoridade do MDM no Intune definida para **Intune**&#41;


   > [!Note]  
   > Se você tiver um ambiente de MDM híbrido (Intune integrado ao Configuration Manager), não será possível habilitar o cogerenciamento. No entanto, você pode iniciar a migração de usuários para o Intune autônomo e, em seguida, habilitar seus dispositivos Windows 10 associados para cogerenciamento. Para obter mais informações sobre como migrar para o Intune autônomo, consulte [Iniciar a migração do MDM híbrido para o Intune autônomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).

### <a name="additional-prerequisites-for-devices-with-the-configuration-manager-client"></a>Pré-requisitos adicionais para dispositivos com o cliente do Configuration Manager
- Windows 10, versão 1709 ou posterior
- [Azure AD híbrido ingressado](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (ingressado no AD e ao Azure AD)

### <a name="additional-prerequisites-for-devices-without-the-configuration-manager-client"></a>Pré-requisitos adicionais para dispositivos sem o cliente do Configuration Manager
- Windows 10, versão 1709 ou posterior
- [Gateway de Gerenciamento de Nuvem](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) no Configuration Manager (quando o Intune é usado para instalar o cliente do Configuration Manager)

> [!IMPORTANT]
> Dispositivos móveis Windows 10 não são compatíveis com o cogerenciamento.


## <a name="command-line-to-install-configuration-manager-client"></a>Linha de comando para instalar o cliente do Configuration Manager
Crie um aplicativo no Intune para dispositivos Windows 10 que ainda não são clientes do Configuration Manager. Ao criar o aplicativo nas próximas seções, use a seguinte linha de comando:

`ccmsetup.msi CCMSETUPCMD="/mp:<URL of cloud management gateway mutual auth endpoint> CCMHOSTNAME=<URL of cloud management gateway mutual auth endpoint> SMSSiteCode=<Sitecode> SMSMP=https://<FQDN of MP> AADTENANTID=<AAD tenant ID> AADCLIENTAPPID=<Server AppID for AAD Integration> AADRESOURCEURI=https://<Resource ID>"`

Por exemplo, se você tiver os valores a seguir:

- **URL do ponto de extremidade de autenticação mútua do gateway de gerenciamento de nuvem**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500    

   >[!Note]    
   >Use o valor **MutualAuthPath** na exibição de SQL **vProxy_Roles** para o valor da **URL do ponto de extremidade de autenticação mútua do gateway de gerenciamento de nuvem**.

- **FQDN do MP (ponto de gerenciamento)**: mp1.contoso.com    
- **Código do site**: PS1    
- **ID do locatário do Azure AD**: 60a413f4-c606-4744-8adb-9476ae3XXXXX    
- **ID do aplicativo cliente do Azure AD**: 9fb9315f-4c42-405f-8664-ae63283XXXXX     
- **URI da ID do recurso do AAD**: ConfigMgrServer    

  > [!Note]    
  > Use o valor **IdentifierUri** encontrado na exibição de SQL **vSMS_AAD_Application_Ex** para o valor do **URI da ID do recurso do AAD**.

Você usaria a seguinte linha de comando:

`ccmsetup.msi CCMSETUPCMD="/mp:https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=PS1 SMSMP=https://mp1.contoso.com AADTENANTID=60a413f4-c606-4744-8adb-9476ae3XXXXX AADCLIENTAPPID=9fb9315f-4c42-405f-8664-ae63283XXXXX AADRESOURCEURI=https://ConfigMgrServer"`

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

   > [!NOTE]   
   > A partir da versão 1802, use o Configuration Manager para coletar e relatar as informações do dispositivo exigidas pela Microsoft Store para Empresas e Educação. Esta informação inclui o número de série do dispositivo, o identificador de produto do Windows e um identificador de hardware. No console do Configuration Manager, espaço de trabalho **Monitoramento**, expanda o nó **Geração de relatórios**, expanda **Relatórios** e selecione o nó **Hardware - Geral**. Execute o novo relatório, **Informações do dispositivo do Windows AutoPilot** e veja os resultados. No visualizador de relatórios, clique no ícone **Exportar** e selecione a opção **CSV (delimitado por vírgulas)**. Depois de salvar o arquivo, faça o upload dos dados para a Microsoft Store para Empresas e Educação. Para saber mais, confira [adicionar dispositivos na Microsoft Store para Empresas e Educação](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile).

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