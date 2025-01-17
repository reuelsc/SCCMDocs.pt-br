---
title: Clientes e dispositivos com suporte
titleSuffix: Configuration Manager
description: Saiba a quais versões de sistema operacional o Configuration Manager oferece suporte para clientes e dispositivos.
ms.date: 10/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c6b47c99199458c902f1f56ccc3d5007dfd126eb
ms.sourcegitcommit: 86968fc2f129e404ff8e08f91a05fa17b5c47527
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2019
ms.locfileid: "67251536"
---
# <a name="supported-os-versions-for-clients-and-devices-for-configuration-manager"></a>Versões de sistema operacional compatíveis com clientes e dispositivos para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 O Configuration Manager oferece suporte à instalação de um software cliente em computadores Windows, Mac, Linux e UNIX.  

#### <a name="requirements-and-limitations-for-all-clients"></a>Requisitos e limitações para todos os clientes  

-   Não há suporte para alterar as configurações de tipo de inicialização ou de **Fazer logon como** de qualquer serviço do Configuration Manager. Essa alteração pode impedir o funcionamento correto dos serviços essenciais.    

-   Não há suporte para a instalação ou execução do cliente do Configuration Manager para Linux ou UNIX ou do cliente para Mac em computadores com uma conta diferente da raiz. Isso pode impedir o funcionamento correto dos serviços essenciais.  



##  <a name="windows-computers"></a>Computadores com Windows  

 Para gerenciar as seguintes versões do sistema operacional do Windows, use o cliente incluído no Configuration Manager. Para saber mais, confira [Como implantar clientes em computadores Windows](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).  


### <a name="supported-client-os-versions"></a>Versões de sistema operacional do cliente com suporte

-   **Windows 10**  

    Para obter mais informações, consulte [Suporte para o Windows 10](/sccm/core/plan-design/configs/support-for-windows-10).  

-   **Windows 8.1** (x86, x64): Professional, Enterprise    

-   **Windows 7 com SP1** (x86, x64): Professional, Enterprise e Ultimate    


### <a name="supported-server-os-versions"></a>Versões de sistema operacional de servidor com suporte

-  **Windows Server 2019**: Standard, Datacenter <sup>[Observação 1](#bkmk_note1)</sup>  
    (a partir do Configuration Manager versão 1806.)

-  **Windows Server 2016**: Standard, Datacenter <sup>[Observação 1](#bkmk_note1)</sup>  

-   **Windows Storage Server 2016**: Workgroup, Standard  

-   **Windows Server 2012 R2** (x64): Standard, Datacenter <sup>[Observação 1](#bkmk_note1)</sup>    

-   **Windows Storage Server 2012 R2** (x64)    

-   **Windows Server 2012** (x64): Standard, Datacenter <sup>[Observação 1](#bkmk_note1)</sup>    

-   **Windows Storage Server 2012** (x64)    

-   **Windows Server 2008 R2 com SP1** (x64): Standard, Enterprise, Datacenter <sup>[Observação 1](#bkmk_note1)</sup>    

-   **Windows Storage Server 2008 R2** (x86, x64): Workgroup, Standard, Enterprise    

-   **Windows Server 2008 com SP2** (x86, x64): Standard, Enterprise, Datacenter <sup>[Observação 1](#bkmk_note1)</sup>    


#### <a name="server-core"></a>Server Core
As seguintes versões referem especificamente à instalação do Server Core do sistema operacional. <sup>[Observação 3](#bkmk_note3)</sup>  

As versões de canal semestral do Windows Server são as instalações do Server Core, por exemplo, Windows Server, versão 1809. Como um cliente do Configuration Manager, elas são compatíveis da mesma forma que a versão associada de canal semestral do Windows 10. Para obter mais informações, consulte [Suporte para o Windows 10](/sccm/core/plan-design/configs/support-for-windows-10).


-   **Windows Server 2019** (x64) <sup>[Observação 2](#bkmk_note2)</sup>  

-   **Windows Server 2016** (x64) <sup>[Observação 2](#bkmk_note2)</sup>   

-   **Windows Server 2012 R2** (x64) <sup>[Observação 2](#bkmk_note2)</sup>     

-   **Windows Server 2012** (x64) <sup>[Observação 2](#bkmk_note2)</sup>     

-   **Windows Server 2008 R2** sem service pack ou com SP1 (x64)     

-   **Windows Server 2008 SP2** (x86, x64)   

#### <a name="bkmk_note1"></a> Observação 1
 O Configuration Manager testa e oferece suporte às edições do Windows Server Datacenter, mas não é certificado oficialmente para o Windows Server. O suporte de hotfixes do Configuration Manager não é oferecido para problemas específicos do Windows Server Datacenter Edition. Para obter mais informações sobre o programa de certificação do Windows Server, consulte [Catálogo do Windows Server](https://www.windowsservercatalog.com/). 

#### <a name="bkmk_note2"></a> Observação 2
 Para oferecer suporte à [instalação do cliente por push](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation), adicione o serviço Servidor de Arquivos da função de servidor Serviços de Arquivo e Armazenamento. Para obter informações sobre como instalar recursos do Windows em um Server Core, consulte [Instalar funções, serviços de função e recursos, usando os cmdlets do Windows PowerShell](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#install-roles-role-services-and-features-by-using-windows-powershell-cmdlets).  

#### <a name="bkmk_note3"></a> Observação 3
 O novo aplicativo do Centro de Software não conta com suporte em qualquer versão do Windows Server Core.<!--SCCMDocs issue 683-->



##  <a name="windows-embedded-computers"></a>Computadores Windows Embedded  

 Gerencie dispositivos com Windows Embedded instalando o cliente do Configuration Manager no dispositivo. Para saber mais, confira [Planejar a implantação no cliente para dispositivos Windows Embedded](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices).  


### <a name="requirements-and-limitations"></a>Requisitos e limitações

-   Todos os recursos do cliente têm suporte nos sistemas Windows Embedded que não tenham filtros de gravação habilitados.  

-   Os clientes que usam um dos procedimentos a seguir têm suporte para todos os recursos, exceto o gerenciamento de energia:  

    -   EWF (Filtros de Gravação Avançados).    

    -   FBWF (Filtros de Gravação com Base em Arquivos) de RAM    

    -   UWF (Filtros de Gravação Unificados)  

-   Não há suporte para o Catálogo de Aplicativos em todos os dispositivos com Windows Embedded.  


### <a name="supported-os-versions"></a>Versões compatíveis do sistema operacional  

-   **Windows 10 Enterprise** (x86, x64)  

-   **Windows 10 IoT Enterprise** (x86, x64)  
    Esta versão inclui o canal de manutenção de longo prazo (LTSC). Para saber mais, confira [Visão geral do Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

-   **Windows Embedded 8.1 Industry** (x86, x64)    

-   **Windows Embedded 8 Standard** (x86, x64)    

-   **Windows Thin PC** (x86, x64)    

-   **Windows Embedded POSReady 7** (x86, x64)    

-   **Windows Embedded Standard 7 com SP1** (x86, x64)    



## <a name="windows-ce-computers"></a>Computadores Windows CE

 Gerencie dispositivos Windows CE com o cliente herdado de dispositivo móvel do Configuration Manager, que está incluso no Configuration Manager.  


### <a name="requirements-and-limitations"></a>Requisitos e limitações  

-   O cliente de dispositivo móvel requer 0,78 MB de espaço de armazenamento para a instalação. A entrada pode exigir até 256 KB de espaço de armazenamento adicional.    

-   Os recursos para estes dispositivos móveis variam por plataforma e tipo de cliente. Para saber mais sobre quais funções de gerenciamento são compatíveis, consulte [Escolher uma solução de gerenciamento de dispositivo](/sccm/core/plan-design/choose-a-device-management-solution).  


### <a name="supported-os-versions"></a>Versões compatíveis do sistema operacional  

-   Windows CE 7.0 (processadores ARM e x86)  

#### <a name="supported-languages-include"></a>Os idiomas compatíveis incluem

-   Chinês (simplificado e tradicional)    

-   Inglês (EUA)    

-   Francês (França)    

-   Alemão    

-   Italiano    

-   Japonês  

-   Coreano  

-   Português (Brasil)  

-   Russo  

-   Espanhol (Espanha)  



## <a name="mac-computers"></a>Computadores Mac  

 Gerencie computadores macOS com o cliente do Configuration Manager para Mac.  

 O pacote de instalação do cliente Mac não é fornecido com a mídia do Configuration Manager. Baixe os **Clientes para Sistemas Operacionais Adicionais** no [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

 Para saber mais, confira [Como implantar clientes em Macs](/sccm/core/clients/deploy/deploy-clients-to-macs).  


### <a name="supported-versions"></a>Versões com suporte

-   **Mac OS X 10.6** (Snow Leopard)

-   **Mac OS X 10.7** (Lion)

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra)

-   **Mac OS X 10.13** (macOS High Sierra)

- **macOS Mojave (10.14)** 


##  <a name="linux-and-unix-servers"></a>Servidores Linux e UNIX  

> [!Important]  
> A partir de 22 de março de 2018, os clientes Linux e UNIX para o Configuration Manager foram preteridos. Para saber mais, confira [Comunicado de reprovação do suporte aos clientes Linux e Unix](/sccm/core/plan-design/changes/whats-new-in-version-1802#deprecation-announcement-for-linux-and-unix-client-support).  

 Gerencie servidores Linux e UNIX com o cliente do Configuration Manager para Linux e UNIX.  

 Os pacotes de instalação do cliente para Linux e UNIX não são fornecidos com a mídia do Configuration Manager. Baixe os **Clientes para Sistemas Operacionais Adicionais** no [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184). Além dos pacotes de instalação do cliente, o download do cliente inclui o script que gerencia a instalação do cliente em cada computador.  


### <a name="requirements-and-limitations"></a>Requisitos e limitações

-   Para examinar as dependências de arquivo do sistema operacional do cliente em Linux e UNIX, consulte [Pré-requisitos para implantação de cliente em servidores Linux e UNIX](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers#BKMK_ClientDeployPrereqforLnU).  

-   Para obter uma visão geral das funcionalidades de gerenciamento compatíveis com Linux ou UNIX, consulte [Como implantar clientes para servidores UNIX e Linux](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).  

-   Para as versões com suporte do Linux e UNIX, a versão listada inclui todas as versões secundárias subsequentes. Por exemplo, o CentOS versão 6 inclui o CentOS 6.3. Da mesma forma, o suporte para um sistema de operacional que usa service packs (como o SUSE Linux Enterprise Server 11 SP1) inclui os service packs subsequentes para essa versão do sistema operacional.  

-   Para saber mais sobre pacotes de instalação no cliente e o Agente Universal, consulte [Como implantar clientes em servidores UNIX e Linux](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).  


### <a name="supported-versions"></a>Versões com suporte

As versões a seguir têm suporte usando o arquivo .tar indicado.  

#### <a name="aix"></a>AIX  

|Version|Arquivo TAR|  
|-|-|  
|Versão 6.1 (Power)|ccm-Aix61ppc.&lt;build\>.tar|  
|Versão 7.1 (Power)|ccm-Aix71ppc.&lt;build\>.tar|  

#### <a name="centos"></a>CentOS  

|Version|Arquivo TAR|  
|-|-|  
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="debian"></a>Debian  

|Version|Arquivo TAR|  
|-|-|  
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 8 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 8 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="hp-ux"></a>HP-UX  

|Version|Arquivo TAR|  
|-|-|  
|Versão 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  

#### <a name="oracle-linux"></a>Oracle Linux  

|Version|Arquivo TAR|  
|-|-|  
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Version|Arquivo TAR|  
|-|-|  
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="solaris"></a>Solaris  

|Version|Arquivo TAR|  
|-|-|  
|Versão 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|Versão 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|Versão 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|Versão 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

#### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Version|Arquivo TAR|  
|-|-|  
|Versão 10 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 10 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 11 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 11 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 12 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="ubuntu"></a>Ubuntu  

|Version|Arquivo TAR|  
|-|-|  
|Versão 10.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 10.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 12.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 12.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 14.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 14.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 16.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 16.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  



##  <a name="bkmk_OnpremOS"></a> Gerenciamento de dispositivo móvel local  

 O Configuration Manager tem recursos internos para gerenciar dispositivos locais sem instalar o software cliente. Para saber mais, confira [Gerenciar dispositivos móveis com a infraestrutura local](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).  


### <a name="requirements-and-limitations"></a>Requisitos e limitações

-   Configure o **Ponto de conexão de serviço** no site de camada superior de sua hierarquia.  


### <a name="supported-operating-systems"></a>Sistemas operacionais com suporte

- **Windows 10 Pro** (x86, x64)  

- **Windows 10 Pro Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    Esta versão inclui o canal de manutenção de longo prazo (LTSC). Para saber mais, confira [Visão geral do Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows 10 Mobile**  

- **Windows 10 Mobile Enterprise**  

- **Windows 10 IoT Mobile Enterprise**  

- **Windows 10 Team para o Surface Hub**  



##  <a name="bkmk_ExSrvConOS"></a> Conector do Exchange Server  

O Configuration Manager dá suporte ao gerenciamento limitado de dispositivos que se conectam ao Exchange Server, sem instalar o cliente do Configuration Manager. Para saber mais, confira [Gerenciar dispositivos móveis com o Configuration Manager e o Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  


### <a name="supported-versions-of-exchange-server"></a>Versões compatíveis do Exchange Server

- **Exchange Online (Office 365)** : Essa versão inclui o Business Productivity Online Standard Suite  

- **Exchange Server 2016** (começando com a versão 1802)  

- **Exchange Server 2013**  

- **Exchange Server 2010 SP1** ou **Exchange Server 2010 SP2** 
