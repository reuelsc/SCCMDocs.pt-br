---
title: Preparar o Windows 10 para o cogerenciamento
titleSuffix: Configuration Manager
description: Saiba como preparar dispositivos Windows 10 para o cogerenciamento.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/10/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: ac7f67a02602473a7635d8c70e4b1b1dc04363bc
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417040"
---
# <a name="prepare-windows-10-devices-for-co-management"></a>Preparar dispositivos Windows 10 para o cogerenciamento
Você pode habilitar o cogerenciamento em dispositivos Windows 10 que foram ingressados no AD e no Azure AD e registrados no Microsoft Intune e em um cliente no Configuration Manager. Para novos dispositivos Windows 10 e dispositivos que já estão registrados no Intune, instale o cliente do Configuration Manager antes que eles possam ser cogerenciados. Para dispositivos Windows 10 que já são clientes do Configuration Manager, você pode registrar os dispositivos no Intune e habilitar o cogerenciamento no console do Configuration Manager.

> [!IMPORTANT]
> Dispositivos móveis Windows 10 não são compatíveis com o cogerenciamento.



## <a name="prerequisites"></a>Pré-requisitos

Você deve ter os seguintes pré-requisitos em vigor antes de habilitar o cogerenciamento. Há pré-requisitos gerais e pré-requisitos diferentes para dispositivos com o cliente do Configuration Manager e dispositivos que não têm o cliente instalado.


### <a name="general-prerequisites"></a>Pré-requisitos gerais

Estes são os pré-requisitos gerais para habilitar o cogerenciamento:  

- Configuration Manager versão 1710 ou posterior  

    - Começando com o Configuration Manager versão 1806, você pode conectar várias instâncias do Configuration Manager a um único locatário do Intune. <!--1357944-->  

- [Site carregado com o Azure AD para gerenciamento de nuvem](/sccm/core/servers/deploy/configure/azure-services-wizard)  

- Licença do EMS ou do Intune para todos os usuários  

- [Registro automático do Azure AD](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) habilitado  

- Assinatura do Intune e a autoridade de MDM no Intune definida como **Intune**.  

    - Se você estiver usando [autoridade mista](/sccm/mdm/deploy-use/migrate-mixed-authority), primeiro conclua a migração para o Intune autônomo. Em seguida, defina a autoridade de MDM no Intune antes de configurar o cogerenciamento.<!--SCCMDocs issue #797-->


> [!NOTE]
> Se você tiver um ambiente de MDM híbrido (Intune integrado ao Configuration Manager), não será possível habilitar o cogerenciamento. No entanto, você pode iniciar a migração de usuários para o Intune autônomo e, em seguida, habilitar seus dispositivos Windows 10 associados para cogerenciamento. Para obter mais informações sobre como migrar para o Intune autônomo, consulte [Iniciar a migração do MDM híbrido para o Intune autônomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).


### <a name="prerequisite-azure-resource-manager-roles"></a>Funções de pré-requisito do Azure Resource Manager
<!--SCCMDocs issue #667--> Para obter mais informações sobre as funções do Azure, confira [Entender as diferentes funções](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).

|Ação|Função necessária|
|----|----|
|Configurar um Gateway de Gerenciamento de Nuvem|Gerenciador de assinatura do Azure|
|Configurar um ponto de distribuição na nuvem|Gerenciador de assinatura do Azure|
|Criar aplicativos do Azure Active Directory usando o console do Configuration Manager|Administrador Global do Azure Active Directory|
|Importando aplicativos cliente e aplicativos para servidores do Azure no console do Configuration Manager| Administrador do Configuration Manager, não há funções adicionais do Azure necessárias.|
|Configurar o cogerenciamento usando o assistente de cogerenciamento| Direitos de usuário do Azure Active Directory, além de ser um administrador do Configuration Manager com todos os direitos do escopo. 


### <a name="additional-prerequisites-for-devices-with-the-configuration-manager-client"></a>Pré-requisitos adicionais para dispositivos com o cliente do Configuration Manager

- Windows 10, versão 1709 ou posterior  

- [Ingressado no Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) (ingressado no AD e no Azure AD) ou ingressado somente no Azure AD (esse tipo é às vezes chamado de "ingressado no domínio da nuvem").


### <a name="additional-prerequisites-for-devices-without-the-configuration-manager-client"></a>Pré-requisitos adicionais para dispositivos sem o cliente do Configuration Manager

- Windows 10, versão 1709 ou posterior  

- [Gateway de Gerenciamento de Nuvem](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) no Configuration Manager (quando o Intune é usado para instalar o cliente do Configuration Manager)  


> [!IMPORTANT]
> Dispositivos móveis Windows 10 não são compatíveis com o cogerenciamento.



## <a name="command-line-to-install-configuration-manager-client"></a>Linha de comando para instalar o cliente do Configuration Manager

Crie um aplicativo no Intune para dispositivos Windows 10 que ainda não são clientes do Configuration Manager. Para fazer isso, execute estas etapas:

1. Navegue até portal.azure.com e, em seguida, abra a folha do Intune.
2. Clique em **Aplicativos Clientes** > **Aplicativos** > **Adicionar**. 
3. Em **Outros**, selecione **Aplicativo de linha de negócios**.
4. Carregue o arquivo de pacote do aplicativo Ccmsetup.msi. (Esse arquivo é encontrado na seguinte pasta no servidor do site: <*ConfigMgr installation directory*>\bin\i386.) 
5. Depois que o aplicativo for atualizado, configure as informações do aplicativo executando o seguinte argumento de linha de comando:

`ccmsetup.msi CCMSETUPCMD="/mp:<URL of cloud management gateway mutual auth endpoint> CCMHOSTNAME=<URL of cloud management gateway mutual auth endpoint> SMSSiteCode=<Sitecode> SMSMP=https://<FQDN of MP> AADTENANTID=<AAD tenant ID> AADCLIENTAPPID=<Server AppID for AAD Integration> AADRESOURCEURI=https://<Resource ID>"`

#### <a name="example-command-line-input"></a>exemplo de entrada de linha de comando
Se você tiver os seguintes valores:

- **URL do ponto de extremidade de autenticação mútua do Gateway de Gerenciamento de Nuvem**: `https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500`    

   >[!NOTE]    
   >Use o valor **MutualAuthPath** na exibição de SQL **vProxy_Roles** para o valor da **URL do ponto de extremidade de autenticação mútua do gateway de gerenciamento de nuvem**.  

- **FQDN do MP (ponto de gerenciamento)**: `mp1.contoso.com`    
- **Sitecode**: `PS1`    
- **ID de locatário do Azure AD**: `44b5bdda-67f5-4850-bdf4-a8ef611109e0`    
- **ID do aplicativo de cliente do Azure AD**: `51e781eb-aac6-4265-8030-4cd1ddaa9dd0`     
- **URI da ID de Recurso do AAD**: `ConfigMgrServer`    

  > [!NOTE]    
  > Use o valor **IdentifierUri** encontrado na exibição de SQL **vSMS_AAD_Application_Ex** para o valor do **URI da ID do recurso do AAD**.  

Então use a seguinte linha de comando:

`ccmsetup.msi CCMSETUPCMD="/mp:https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=PS1 SMSMP=https://mp1.contoso.com AADTENANTID=44b5bdda-67f5-4850-bdf4-a8ef611109e0 AADCLIENTAPPID=51e781eb-aac6-4265-8030-4cd1ddaa9dd0 AADRESOURCEURI=https://ConfigMgrServer"`


<!--1358215--> Da versão 1806 em diante, menos propriedades de linha de comando agora são necessárias.  

- As propriedades de linha de comando a seguir são necessárias em todos os cenários:  
    - CCMHOSTNAME  
    - SMSSITECODE  

- As propriedades a seguir são necessárias ao usar o Azure AD para autenticação de cliente em vez de certificados de autenticação de cliente baseados em PKI:  
    - AADCLIENTAPPID  
    - AADRESOURCEURI  

- A propriedade a seguir será necessária se o cliente for retornar para a Intranet:  
    - SMSMP  

O exemplo a seguir inclui todas as propriedades acima:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Para obter mais informações, consulte [Propriedades de instalação do cliente](/sccm/core/clients/deploy/about-client-installation-properties).


> [!TIP]
> Encontre os parâmetros de linha de comando para o seu site usando as seguintes etapas:     
> 
> 1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e escolha o nó **Cogerenciamento**.  
> 
> 2. Na faixa de opções, clique em **Configurar cogerenciamento** para abrir o Assistente para Integração de Cogerenciamento. (Se você já tiver configurado cogerenciamento, selecione **Propriedades**. Em seguida, vá para a etapa 4.)    
> 
> 3. Na página de Assinatura, selecione **Entrar**. Entre no seu locatário do Intune e, em seguida, clique em **Avançar**.    
> 
> 4. Na página Habilitação, selecione **Copiar** para copiar a linha de comando para a área de transferência. Em seguida, salve a linha de comando para usar o procedimento para criar o aplicativo.  
> 
> 5. Clique em **Cancelar** para sair do assistente.  

> [!IMPORTANT]    
> Se você personalizar a linha de comando para instalar o cliente do Configuration Manager, verifique se a linha de comando não excede 1024 caracteres. Quando a linha de comando for maior que 1.024 caracteres, a instalação do cliente falhará.



## <a name="new-windows-10-devices"></a>Novos dispositivos Windows 10

Para novos dispositivos Windows 10, você pode usar o serviço AutoPilot para definir a configuração inicial pelo usuário, que inclui ingressar o dispositivo no AD e no Azure AD, bem como registrar o dispositivo no Intune. Em seguida, crie um aplicativo no Intune para implantar o cliente do Configuration Manager.  

1. Habilite o AutoPilot para os novos dispositivos Windows 10. Para obter detalhes, consulte [Visão geral do Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).    

   > [!NOTE]   
   > A partir da versão 1802, use o Configuration Manager para coletar e relatar as informações do dispositivo exigidas pela Microsoft Store para Empresas e Educação. Esta informação inclui o número de série do dispositivo, o identificador de produto do Windows e um identificador de hardware. No console do Configuration Manager, workspace **Monitoramento**, expanda o nó **Geração de relatórios**, expanda **Relatórios** e selecione o nó **Hardware - Geral**. Execute o novo relatório, **Informações do dispositivo do Windows AutoPilot** e veja os resultados. No visualizador de relatórios, clique no ícone **Exportar** e selecione a opção **CSV (delimitado por vírgulas)**. Depois de salvar o arquivo, faça o upload dos dados para a Microsoft Store para Empresas e Educação. Para saber mais, confira [adicionar dispositivos na Microsoft Store para Empresas e Educação](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile).

2. Configure o registro automático no Azure AD para que seus dispositivos sejam registrados automaticamente no Intune. Para obter detalhes, consulte  [Registrar os dispositivos Windows no Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  

3. Crie um aplicativo no Intune com o pacote do cliente do Configuration Manager e implante o aplicativo nos dispositivos Windows 10 que você deseja cogerenciar. Use a [linha de comando para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) ao percorrer as etapas para [instalar clientes da Internet usando o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).   



## <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Dispositivos Windows 10 não registrados no Intune nem em um cliente do Configuration Manager

Para dispositivos Windows 10 que não estão registrados no Intune ou que têm o cliente do Configuration Manager, você pode usar o registro automático para registrar o dispositivo no Intune. Em seguida, crie um aplicativo no Intune para implantar o cliente do Configuration Manager.

1. Configure o registro automático no Azure AD para que seus dispositivos sejam registrados automaticamente no Intune. Para obter detalhes, consulte  [Registrar os dispositivos Windows no Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  

2. Crie um aplicativo no Intune com o pacote do cliente do Configuration Manager e implante o aplicativo nos dispositivos Windows 10 que você deseja cogerenciar. Use a [linha de comando para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) ao percorrer as etapas para [instalar clientes da Internet usando o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).



## <a name="windows-10-devices-enrolled-in-intune"></a>Dispositivos Windows 10 registrados no Intune

Para dispositivos Windows 10 que já estão registrados no Intune, crie um aplicativo no Intune para implantar o cliente do Configuration Manager. Use a [linha de comando para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) ao percorrer as etapas para [instalar clientes da Internet usando o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).  



## <a name="next-steps"></a>Próximas etapas

[Mudar as cargas de trabalho do Configuration Manager para o Intune](co-management-switch-workloads.md)
