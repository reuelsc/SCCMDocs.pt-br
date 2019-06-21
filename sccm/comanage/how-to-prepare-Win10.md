---
title: Cogerenciar dispositivos baseados na Internet
titleSuffix: Configuration Manager
description: Saiba como preparar dispositivos Windows 10 baseados na Internet para o cogerenciamento.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/05/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5600743af8acc0da121454aef2d90167c3ded5fa
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67286617"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>Como preparar dispositivos baseados na Internet para o cogerenciamento

Este artigo enfoca o segundo caminho para o cogerenciamento, para novos dispositivos baseados na Internet. Este cenário ocorre quando você tem novos dispositivos Windows 10 que ingressam no Azure AD e se registram automaticamente no Intune. Instale o cliente do Configuration Manager para atingir um estado de cogerenciamento.  



## <a name="windows-autopilot"></a>Windows Autopilot

Para novos dispositivos Windows 10, você pode usar o serviço AutoPilot para definir a configuração inicial pelo usuário. Esse processo inclui ingressar o dispositivo no AD e no Azure AD, bem como registrar o dispositivo no Intune.  

Para saber mais, confira [Visão geral do Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot).    

Para configurar seus dispositivos para serem registrados automaticamente no Intune ao ingressar no Azure AD, confira  [Registrar dispositivos Windows no Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  


### <a name="gather-information-from-configuration-manager"></a>Coletar informações do Configuration Manager

A partir da versão 1802, use o Configuration Manager para coletar e relatar as informações do dispositivo exigidas pela Microsoft Store para Empresas e Educação. Esta informação inclui o número de série do dispositivo, o identificador de produto do Windows e um identificador de hardware. Ele é usado para registrar o dispositivo na Microsoft Store para dar suporte ao Windows Autopilot. 

1. No console do Configuration Manager, acesse o workspace **Monitoramento**, expanda o nó **Geração de relatórios**, expanda **Relatórios** e selecione o nó **Hardware - Geral**.  

2. Execute o relatório, **Informações do dispositivo do Windows AutoPilot** e veja os resultados.  

3. No visualizador de relatórios, selecione o ícone **Exportar** e escolha a opção **CSV (delimitado por vírgulas)** .  

4. Depois de salvar o arquivo, faça o upload dos dados para a Microsoft Store para Empresas e Educação.  

Para saber mais, confira [Adicionar dispositivos na Microsoft Store para Empresas e Educação](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile).


### <a name="autopilot-for-existing-devices"></a>Autopilot para dispositivos existentes
<!--1358333-->

O [Windows Autopilot para dispositivos existentes](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) está disponível no Windows 10, versão 1809 ou posterior. Esse recurso permite refazer a imagem e provisionar um dispositivo Windows 7 para o [modo orientado pelo usuário do Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) usando uma única sequência de tarefas nativa do Configuration Manager. 

Para saber mais, confira [Sequência de tarefas do Windows Autopilot para dispositivos existentes](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices).



## <a name="install-the-configuration-manager-client"></a>Instalar o cliente do Configuration Manager

Para dispositivos baseados na Internet no segundo caminho, é preciso criar um aplicativo no Intune. Implante esse aplicativo em dispositivos Windows 10 que ainda não são clientes do Configuration Manager. 

### <a name="get-the-command-line-from-configuration-manager"></a>Obter a linha de comando do Configuration Manager

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e escolha o nó **Cogerenciamento**.  

2. Selecione o objeto de cogerenciamento e, em seguida, escolha **Propriedades** na faixa de opções.  

3. Na guia **Habilitação**, copie a linha de comando. Cole-a no bloco de notas para salvar para o próximo processo.  

A linha de comando a seguir é um exemplo: `CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC"`

<!--1358215-->
A partir da versão 1806, são necessárias menos propriedades de linha de comando.  

- As propriedades de linha de comando a seguir são necessárias em todos os cenários:  
    - CCMHOSTNAME  
    - SMSSITECODE  

- As propriedades a seguir são necessárias ao usar o Azure AD para autenticação de cliente em vez de certificados de autenticação de cliente baseados em PKI:  
    - AADCLIENTAPPID  
    - AADRESOURCEURI  

- Se o cliente voltar para a Intranet, a seguinte propriedade será necessária:  
    - SMSMP  

- Se você usar seu próprio certificado SSL PKI e sua CRL não for publicada na Internet, será necessário o seguinte parâmetro:  
    - /noCRLCheck  
    
     Para saber mais, confira [Planejamento de CRLs](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForCRLs)  

Começando na versão 1810, o site publica informações adicionais do Microsoft Azure AD no Gateway de Gerenciamento de Nuvem. Um cliente associado ao Azure AD obtém essas informações do CMG durante o processo ccmsetup, usando o mesmo locatário ao qual ele está associado. Esse comportamento simplifica ainda mais o registro de dispositivos para o cogerenciamento em um ambiente com mais de um locatário do Azure AD. Agora as duas únicas propriedades necessárias do ccmsetup são **CCMHOSTNAME** e **SMSSiteCode**.<!--3607731-->

> [!Note]
> Se você já estiver implantando o cliente do Configuration Manager no Intune, atualize o aplicativo do Intune com uma nova linha de comando e a nova MSI. <!-- SCCMDocs-pr issue 3084 -->

O exemplo a seguir inclui todas essas propriedades:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Para obter mais informações, consulte [Propriedades de instalação do cliente](/sccm/core/clients/deploy/about-client-installation-properties).


### <a name="create-the-app-in-intune"></a>Criar o aplicativo no Intune

1. Vá para o [portal do Azure](https://portal.azure.com) e, em seguida, abra a página do Intune.  

2. Selecione **Aplicativos Clientes** > **Aplicativos** > **Adicionar**.  

3. Em **Outros**, selecione **Aplicativo de linha de negócios**.  

4. Carregue o arquivo de pacote do aplicativo **ccmsetup.msi**. Encontre esse arquivo na seguinte pasta no servidor do site do Configuration Manager: `<ConfigMgr installation directory>\bin\i386`.  

    > [!Tip]  
    > Ao atualizar o site, não deixe de atualizar também esse aplicativo no Intune.  

5. Depois que o aplicativo for atualizado, configure as informações dele com a linha de comando que você copiou do Configuration Manager.  

> [!IMPORTANT]    
> Se você personalizar essa linha de comando, garanta que não tenha mais de 1.024 caracteres. Quando a extensão da linha de comando for maior que 1.024 caracteres, a instalação do cliente falhará.


