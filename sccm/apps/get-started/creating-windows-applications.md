---
title: Criar aplicativos do Windows
titleSuffix: Configuration Manager
description: Saiba mais informações sobre como criar e implantar aplicativos do Windows no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 38732081ce27fde764f7d47a565ce1211cef1f54
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383542"
---
# <a name="create-windows-applications-in-configuration-manager"></a>Criar aplicativos do Windows no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Além dos outros requisitos e procedimentos do Configuration Manager para [criar um aplicativo](/sccm/apps/deploy-use/create-applications), também leve em conta as considerações a seguir ao criar e implantar aplicativos para dispositivos Windows.  



## <a name="bkmk_general"></a> Considerações gerais  

O Configuration Manager dá suporte à implantação do pacote do aplicativo (.appx) e do lote de aplicativo (.appxbundle) do Windows para dispositivos Windows 8.1 e Windows 10.

Começando na versão 1806, o Configuration Manager também dá suporte aos novos formatos de pacote do aplicativo (.msix) e de lote de aplicativo (.msixbundle) do Windows 10. Os builds mais recentes do [Windows Insider Preview](https://insider.windows.com/) dão suporte a esses novos formatos no momento.<!--1357427-->  

- Para obter uma visão geral do MSIX, confira [Visão detalhada do MSIX](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/).  

- Para saber como criar um novo aplicativo MSIX, confira [Suporte a MSIX introduzido no Insider Build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).  

Ao criar um aplicativo no console do Configuration Manager, selecione o **Tipo** de arquivo de instalação do aplicativo como **Pacote do aplicativo do Windows (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)**. Para mais informações, consulte [Criar aplicativos](/sccm/apps/deploy-use/create-applications). 

> [!Note]  
> Para aproveitar os novos recursos do Configuration Manager, primeiro atualize os clientes para a versão mais recente. Embora a nova funcionalidade seja exibida no console do Configuration Manager quando você atualiza o site e o console, o cenário completo só funcionará quando a versão do cliente também for a mais recente.<!--SCCMDocs issue 646-->  



## <a name="bkmk_provision"></a> Provisionar pacotes do aplicativo do Windows para todos os usuários em um dispositivo
<!--1358310--> Começando na versão 1806, é possível provisionar um aplicativo com um pacote do aplicativo do Windows para todos os usuários no dispositivo. Um exemplo comum desse cenário é o provisionamento de um aplicativo da Microsoft Store para Empresas e Educação, como o Minecraft: Education Edition, para todos os dispositivos usados pelos alunos em uma escola. Anteriormente, o Configuration Manager somente permitia a instalação desses aplicativos por usuário. Depois de entrar em um novo dispositivo, o aluno precisava esperar para acessar um aplicativo. Agora, quando o aplicativo é provisionado no dispositivo para todos os usuários, eles podem começar a produzir mais rapidamente.

> [!Important]  
> Tenha cuidado com a instalação, o provisionamento e atualização de versões diferentes do mesmo pacote do aplicativo do Windows em um dispositivo, pois isso pode causar resultados inesperados. Esse comportamento pode ocorrer ao usar o Configuration Manager para provisionar o aplicativo, mas, em seguida, permitir que os usuários atualizem o aplicativo da Microsoft Store. Para obter mais informações, confira as diretrizes da próxima etapa ao [Gerenciar aplicativos da Microsoft Store para Empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#next-steps).  

Ao provisionar um aplicativo licenciado offline, o Configuration Manager não permite que o Windows o atualize automaticamente da Microsoft Store.  

O Configuration Manager dá suporte ao provisionamento de aplicativo nas seguintes versões do Windows:<!--SCCMDocs-pr issue 2762-->
- Ação de instalação: Windows 10, versão 1607 e posteriores
- Ação de desinstalação: Windows 10, versão 1703 e posteriores

Para configurar um tipo de implantação de aplicativo do Windows para esse recurso, habilite a opção para **Provisionar este aplicativo para todos os usuários no dispositivo**. Para mais informações, consulte [Criar aplicativos](/sccm/apps/deploy-use/create-applications).


> [!Note]  
> Se você precisar desinstalar um aplicativo provisionado de dispositivos nos quais os usuários já entraram, será necessário criar duas implantações de desinstalação. Direcione a primeira implantação de desinstalação a uma coleção de dispositivos que contenha os dispositivos. Direcione a segunda implantação de desinstalação a uma coleção de usuários que contenha os usuários que já entraram nos dispositivos com o aplicativo provisionado. Quando você desinstala um aplicativo provisionado em um dispositivo, no momento, o Windows não desinstala esse aplicativo dos usuários também. 



## <a name="bkmk_uwp"></a> Suporte para aplicativos UWP (Plataforma Universal do Windows)  

Os dispositivos Windows 10 não exigem uma chave de sideload para instalar aplicativos de linha de negócios. Para habilitar o sideload no Windows, no entanto, a chave do Registro `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps` precisa ter o valor **1**.  

Se você não configurar essa chave do Registro, o Configuration Manager definirá esse valor automaticamente como **1** na primeira vez que você implantar um aplicativo no dispositivo. Se você definir esse valor como **0**, o Configuration Manager não poderá alterar o valor automaticamente e a implantação do aplicativo de linha de negócios falhará.  

Assine digitalmente os aplicativos UWP de linha de negócios. Use um certificado de autenticação de código confiável em cada dispositivo no qual você implantar o aplicativo. Use certificados de PKI da sua organização ou compre um certificado de um provedor terceiro cujo certificado raiz público já seja confiável para o Windows.  

Para assinar os pacotes de aplicativos móveis, use a tabela a seguir para determinar o tipo de certificado de autenticação de código a ser usado:

| Pacote  | Symantec  | Não Symantec  |
|---------|---------|---------|
| Pacotes **.appx** universais em dispositivos Windows 10 Mobile | Sim | Sim |
| Pacotes **.xap** | Sim | Não | 
| Pacotes **.appx** criados para Windows Phone 8.1 para serem instalados em dispositivos Windows 10 Mobile | Sim | Não | 



## <a name="bkmk_mdm-msi"></a> Implantar aplicativos do Windows Installer em dispositivos Windows 10 registrados no MDM  

O tipo de implantação do **Windows Installer por meio do MDM (\*.msi)** permite criar e implantar aplicativos baseados no Windows Installer em dispositivos registrados no MDM que executam o Windows 10.  

Ao usar esse tipo de implantação, considere os seguintes pontos:    

-   Carregue somente um único arquivo com a extensão MSI.  

-   O Configuration Manager usa o código do produto e a versão do produto do arquivo para detecção do aplicativo.  

-   O Windows usa o comportamento de reinicialização padrão do aplicativo. O Configuration Manager não controla o comportamento de reinicialização do aplicativo.  

-   Os pacotes de MSI por usuário são instalados para um único usuário.  

-   Os pacotes de MSI por computador são instalados para todos os usuários do dispositivo.  

-   O Configuration Manager dá suporte à atualizações do aplicativo. O código do produto MSI de cada versão precisa ser o mesmo.  
