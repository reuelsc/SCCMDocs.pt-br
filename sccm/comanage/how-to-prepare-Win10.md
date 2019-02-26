---
title: Gerenciar dispositivos baseados na internet em conjunto
titleSuffix: Configuration Manager
description: Saiba como preparar os dispositivos baseados na internet do Windows 10 para cogerenciamento.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.collection: M365-identity-device-management
ms.openlocfilehash: fbe26eee8b01c581776b1c134e1fe59cf4293e1a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754519"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>Como preparar os dispositivos baseados na internet para o cogerenciamento

Este artigo se concentra no segundo caminho para o cogerenciamento para novos dispositivos baseados na internet. Esse cenário é quando você tem novos dispositivos Windows 10 que ingressem no Azure AD e registrados automaticamente para o Intune. Instalar o cliente do Configuration Manager para atingir um estado de cogerenciamento.  



## <a name="windows-autopilot"></a>Windows Autopilot

Para novos dispositivos Windows 10, você pode usar o serviço Autopilot para definir a experiência de caixa (OOBE). Esse processo inclui ingressar o dispositivo no Azure AD e o registro do dispositivo no Intune.  

Para obter mais informações, consulte [visão geral do Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot).    

Para configurar seus dispositivos para ser registrados automaticamente no Intune quando tentarem entrar no Azure AD, consulte [dispositivos Windows registrar para o Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  


### <a name="gather-information-from-configuration-manager"></a>Coletar informações do Configuration Manager

A partir da versão 1802, use o Configuration Manager para coletar e relatar as informações do dispositivo exigidas pela Microsoft Store para Empresas e Educação. Esta informação inclui o número de série do dispositivo, o identificador de produto do Windows e um identificador de hardware. Ele é usado para registrar o dispositivo em que a Microsoft Store para dar suporte ao Windows Autopilot. 

1. No console do Configuration Manager, vá para o **monitoramento** espaço de trabalho, expanda o **Reporting** nó, expanda **relatórios**e selecione o **Hardware - Geral** nó.  

2. Executar o relatório **informações de dispositivo do Windows Autopilot**e exibir os resultados.  

3. No Visualizador de relatórios, selecione a **exportar** ícone e escolha o **CSV (delimitado por vírgula)** opção.  

4. Depois de salvar o arquivo, faça o upload dos dados para a Microsoft Store para Empresas e Educação.  

Para obter mais informações, consulte [adicionar dispositivos na Microsoft Store para empresas e educação](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile).


### <a name="autopilot-for-existing-devices"></a>AutoPilot para dispositivos existentes
<!--1358333-->

[Windows Autopilot para dispositivos existentes](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) está disponível o Windows 10, versão 1809 ou posterior. Esse recurso permite que você recriar a imagem e provisionar um dispositivo com Windows 7 para [modo controlada pelo usuário do Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) usando uma sequência de tarefas do Configuration Manager única e nativo. 



## <a name="install-the-configuration-manager-client"></a>Instalar o cliente do Configuration Manager

Para dispositivos baseados na internet no segundo caminho, você precisa criar um aplicativo no Intune. Implante esse aplicativo nos dispositivos Windows 10 que já não são clientes do Configuration Manager. 

### <a name="get-the-command-line-from-configuration-manager"></a>Obter a linha de comando do Configuration Manager

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e escolha o nó **Cogerenciamento**.  

2. Selecione o objeto de cogerenciamento e, em seguida, escolha **propriedades** na faixa de opções.  

3. Sobre o **habilitação** guia, copie a linha de comando. Cole-o no bloco de notas para salvar para o próximo processo.  

A linha de comando a seguir está um exemplo: `CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC"`

<!--1358215--> Da versão 1806 em diante, menos propriedades de linha de comando agora são necessárias.  

- As propriedades de linha de comando a seguir são necessárias em todos os cenários:  
    - CCMHOSTNAME  
    - SMSSITECODE  

- As propriedades a seguir são necessárias ao usar o Azure AD para autenticação de cliente em vez de certificados de autenticação de cliente baseados em PKI:  
    - AADCLIENTAPPID  
    - AADRESOURCEURI  

- Se o cliente passa de volta à intranet, a propriedade a seguir é necessária:  
    - SMSMP  

- Se usando seu próprio certificado SSL de PKI e sua CRL não é publicado na internet, o seguinte parâmetro é necessário:  
    - /noCRLCheck  
    
     Para obter mais informações, consulte [planejando CRLs](/sccm/core/plan-design/security/plan-for-security#-plan-for-the-site-server-signing-certificate-self-signed)  

O exemplo a seguir inclui todas essas propriedades:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Para obter mais informações, consulte [Propriedades de instalação do cliente](/sccm/core/clients/deploy/about-client-installation-properties).


### <a name="create-the-app-in-intune"></a>Criar o aplicativo no Intune

1. Vá para o [portal do Azure](https://portal.azure.com)e, em seguida, abra a página do Intune.  

2. Selecione **aplicativos de cliente** > **aplicativos** > **adicionar**.  

3. Em **Outros**, selecione **Aplicativo de linha de negócios**.  

4. Carregar o **CCMSetup** arquivo de pacote do aplicativo. Encontrar esse arquivo na seguinte pasta no Gerenciador de configuração do servidor do site: `<ConfigMgr installation directory>\bin\i386`.  

5. Depois que o aplicativo for atualizado, configure as informações do aplicativo com a linha de comando que você copiou do Configuration Manager.  

> [!IMPORTANT]    
> Se você personalizar essa linha de comando, verifique se que ele não tem mais de 1024 caracteres. Quando o comprimento da linha de comando é maior que 1024 caracteres, a instalação do cliente falhará.


