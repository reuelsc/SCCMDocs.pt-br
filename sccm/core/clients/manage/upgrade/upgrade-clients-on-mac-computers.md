---
title: 'Atualizar clientes do macOS '
titleSuffix: Configuration Manager
description: Atualize clientes em computadores Mac no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fb0ef52bc3359e1b31b2e2237a87e58bf671bcb7
ms.sourcegitcommit: 4b8afbd08ecf8fd54950eeb630caf191d3aa4767
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36260829"
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-system-center-configuration-manager"></a>Como atualizar clientes em computadores Mac no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Siga as etapas de alto nível descritas abaixo para atualizar o cliente para computadores Mac usando um aplicativo do System Center Configuration Manager. Como alternativa, você também pode baixar o arquivo de instalação do cliente Mac, copiá-lo para um local de rede compartilhada ou uma pasta local no computador Mac e, em seguida, orientar os usuários a executar a instalação manualmente.  

> [!NOTE]  
>  Antes de executar estas etapas, verifique se seu computador Mac atende aos pré-requisitos. Consulte [Sistemas operacionais com suporte para computadores Mac](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).  

## <a name="step-1-download-the-latest-mac-client-installation-file-from-the-microsoft-download-center"></a>Etapa 1: Baixe o arquivo de instalação mais recente do cliente do Mac do Centro de Download da Microsoft  
 O cliente Mac do Configuration Manager não é fornecido na mídia de instalação do Configuration Manager e deve ser baixado do Centro de Download da Microsoft. Os arquivos de instalação do cliente Mac estão contidos em um arquivo do Windows Installer chamado ConfigmgrMacClient.msi.  

 Você pode baixar o arquivo do [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=525184).  

## <a name="step-2-run-the-downloaded-installation-file-to-create-the-mac-client-installation-file"></a>Etapa 2: Executar o arquivo de instalação baixado para criar o arquivo de instalação do cliente Mac  
 Em um computador com Windows, execute o **ConfigmgrMacClient.msi** baixado para descompactar o arquivo de instalação do cliente Mac, chamado **Macclient.dmg**. Esse arquivo pode ser encontrado, por padrão, na pasta **C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client** no computador Windows depois que você descompactar os arquivos.  

## <a name="step-3-extract-the-client-installation-files"></a>Etapa 3: Extrair os arquivos de instalação do cliente  
 Copie o arquivo Macclient.dmg para um compartilhamento de rede ou uma pasta local em um computador Mac. Em seguida, de um computador Mac, monte e abra o arquivo Macclient.dmg e copie os arquivos para uma pasta no computador Mac.  

## <a name="step-4-create-a-cmmac-file-that-can-be-used-to-create-an-application"></a>Etapa 4: Criar um arquivo .cmmac que pode ser usado para criar um aplicativo  

1.  Use a ferramenta **CMAppUtil** (localizada na pasta **Ferramentas** dos arquivos de instalação do cliente Mac) para criar um arquivo .cmmac por meio do pacote de instalação do cliente. Esse arquivo será usado para criar o aplicativo do Configuration Manager.  

2.  Copie o novo arquivo **CMClient.pkg.cmmac** para um local disponível no computador que está executando o console do Configuration Manager.  

 Para mais informações, consulte [Procedimentos complementares para criar e implantar aplicativos para computadores Mac](/sccm/apps/get-started/creating-mac-computer-applications#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers).  

## <a name="step-5-create-and-deploy-an-application-containing-the-mac-client-files"></a>**Etapa 5:** Crie e implante um aplicativo contendo os arquivos do cliente Mac  

1.  No console do Configuration Manager, crie um aplicativo por meio do arquivo **CMClient.pkg.cmmac** que contém os arquivos de instalação do cliente.  

2.  Implante esse aplicativo em computadores Mac na sua hierarquia.  

 Para mais informações, consulte [Criando aplicativos de computador Mac com o System Center Configuration Manager](../../../../apps/get-started/creating-mac-computer-applications.md).  

## <a name="step-6-users-install-the-latest-client"></a>Etapa 6: Os usuários instalam o cliente mais recente  
 Usuários de clientes Mac receberão um aviso de que uma atualização para o cliente do Configuration Manager está disponível e deve ser instalada. Depois de instalar o cliente, os usuários deverão reiniciar o computador Mac.  

 Depois que o computador for reiniciado, o Assistente de Registro de Computador será executado automaticamente para solicitar um novo certificado de usuário. O assistente de Registro do Computador será executado automaticamente somente na primeira vez da instalação de cliente do SCCM. E ele não será executado novamente se você tentar atualizar o cliente com um novo instalador mais tarde, pois ele já tem um certificado de usuário válido. 

 Se você não usar o registro do Configuration Manager, mas instalar o certificado do cliente independentemente do Configuration Manager, veja [Configurar o cliente atualizado para usar um certificado existente](#BKMK_UpgradingClient_MachineEnrollment).  

##  <a name="BKMK_UpgradingClient_MachineEnrollment"></a> Configure the upgraded client to use an existing certificate  
 Execute o procedimento a seguir para evitar que o Assistente de Registro de Computador seja executado e configure o cliente atualizado para usar um certificado de cliente existente.  

-   No console do Configuration Manager, crie um item de configuração do tipo **Mac OS X**.  

-   Adicione uma definição a esse item de configuração com o tipo de configuração **Script**.  

-   Adicione o seguinte script à configuração:  

    ```  
    #!/bin/sh  
    echo "Starting script\n"  
    echo "Changing directory to MAC Client\n"  
    cd /Users/Administrator/Desktop/'MAC Client'/  
    echo "Import root cert\n"  
    /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
    echo "Using openssl to convert pfx to a crt\n"  
    /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
    echo "Adding trust to root cert\n"  
    /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
    echo "Import client cert\n"  
    /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
    echo "Executing ccmclient with MP\n"  
    sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
    echo "Editing Plist file\n"  
    sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
    echo "Changing directory to CCM\n"  
    cd /Library/'Application Support'/Microsoft/CCM/  
    echo "Making connection to the server\n"  
    sudo open ./CCMClient  
    echo "Ending Script\n"  
    exit  

    ```  

-   Adicione o item de configuração à linha de base de configuração e implante-a em todos os computadores Mac que instalam um certificado independentemente do Configuration Manager.  

 Para obter mais informações sobre como criar e implantar itens de configuração para computadores Mac, consulte [Como criar itens de configuração para dispositivos Mac OS X gerenciados com o cliente do System Center Configuration Manager](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md) e [Como implantar linhas de base de configuração no System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md).  
