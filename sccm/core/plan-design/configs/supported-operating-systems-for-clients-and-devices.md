---
title: Clientes e dispositivos com suporte
titleSuffix: Configuration Manager
description: Saiba a quais versões de sistema operacional o Configuration Manager oferece suporte para clientes e dispositivos.
ms.date: 08/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8abe612272dd8a48a23ffdcb945aa7b6766afdb9
ms.sourcegitcommit: 7eebd112a9862bf98359c1914bb0c86affc5dbc0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/22/2018
ms.locfileid: "42586395"
---
# <a name="supported-os-versions-for-clients-and-devices-for-configuration-manager"></a>Versões de sistema operacional compatíveis com clientes e dispositivos para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 O Configuration Manager oferece suporte à instalação de um software cliente em computadores Windows, Mac, Linux e UNIX.  

#### <a name="requirements-and-limitations-for-all-clients"></a>Requisitos e limitações para todos os clientes  

-   Não há suporte para alterar as configurações de tipo de inicialização ou de **Fazer logon como** de qualquer serviço do Configuration Manager. Essa alteração pode impedir o funcionamento correto dos serviços essenciais.    

-   Não há suporte para a instalação ou execução do cliente do Configuration Manager para Linux ou UNIX ou do cliente para Mac em computadores com uma conta diferente da raiz. Isso pode impedir o funcionamento correto dos serviços essenciais.  



##  <a name="windows-computers"></a>Computadores com Windows  

 Use o cliente incluído no Configuration Manager para gerenciar as seguintes versões do sistema operacional do Windows. Para saber mais, confira [Como implantar clientes em computadores Windows](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).  


### <a name="supported-os-versions"></a>Versões compatíveis do sistema operacional  

-  **Windows Server 2016**: Standard, Datacenter <sup>[Observação 1](#bkmk_note1)</sup>  

-   **Windows Storage Server 2016**: Workgroup, Standard  

-   **Windows Server 2012 R2** (x64): Standard, Datacenter <sup>[Observação 1](#bkmk_note1)</sup>    

-   **Windows Storage Server 2012 R2** (x64)    

-   **Windows Server 2012** (x64): Standard, Datacenter <sup>[Observação 1](#bkmk_note1)</sup>    

-   **Windows Storage Server 2012** (x64)    

-   **Windows Server 2008 R2 com SP1** (x64): Standard, Enterprise, Datacenter <sup>[Observação 1](#bkmk_note1)</sup>    

-   **Windows Storage Server 2008 R2** (x86, x64): Workgroup, Standard, Enterprise    

-   **Windows Server 2008 com SP2** (x86, x64): Standard, Enterprise, Datacenter <sup>[Observação 1](#bkmk_note1)</sup>    

-   **Windows 10**  

    Para saber mais sobre as diferentes versões do Windows 10 que são compatíveis com as diferentes versões do Configuration Manager, consulte [Suporte para versões do Windows 10](/sccm/core/plan-design/configs/support-for-windows-10).  

-   **Windows 8.1** (x86, x64): Professional, Enterprise    

-   **Windows 7 com SP1** (x86, x64): Professional, Enterprise e Ultimate    

-   **A instalação Server Core do Windows Server, versão 1709** (x64) <sup>[Observação 2](#bkmk_note2)</sup> <sup>[Observação 3](#bkmk_note3)</sup>  
    Esta versão do sistema operacional é compatível a partir da versão 1710 do Configuration Manager.  

-   **A instalação Server Core do Windows Server 2016** (x64) <sup>[Observação 2](#bkmk_note2)</sup> <sup>[Observação 3](#bkmk_note3)</sup>  

-   **A instalação Server Core do Windows Server 2012 R2** (x64) <sup>[Observação 2](#bkmk_note2)</sup> <sup>[Observação 3](#bkmk_note3)</sup>    

-   **A instalação Server Core do Windows Server 2012** (x64) <sup>[Observação 2](#bkmk_note2)</sup> <sup>[Observação 3](#bkmk_note3)</sup>    

-   **A instalação Server Core do Windows Server 2008 R2** sem service pack ou com SP1 (x64) <sup>[Observação 3](#bkmk_note3)</sup>    

-   **A instalação Server Core do Windows Server 2008 SP2** (x86, x64) <sup>[Observação 3](#bkmk_note3)</sup>  

#### <a name="bkmk_note1"></a> Observação 1
 Há suporte para versões Datacenter, mas sem certificação para o Configuration Manager. O suporte de hotfix não é oferecido para problemas específicos do Windows Server Datacenter Edition.  

#### <a name="bkmk_note2"></a> Observação 2
 Para oferecer suporte à instalação do cliente por push, o computador que executa esta versão do sistema operacional deve executar o serviço de função do Servidor de Arquivos para a função de servidor dos Serviços de Arquivo e Armazenamento. Para saber mais sobre como instalar recursos do Windows em um computador Server Core, consulte [Instalar funções, serviços de função e recursos usando os cmdlets do Windows PowerShell](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#BKMK_installwps).  

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

-   Antes de monitorar malware detectado em dispositivos Windows Embedded baseados no Windows XP, é necessário instalar o pacote de script WMI do Microsoft Windows no dispositivo. Use o Windows Embedded Target Designer para instalar este pacote. Os arquivos **WBEMDISP.DLL** e **WBEMDISP.TLB** devem existir e estar registrados na pasta **%windir%\System32\WBEM** no dispositivo inserido a fim de garantir que o malware detectado seja relatado.  


### <a name="supported-os-versions"></a>Versões compatíveis do sistema operacional  

-   **Windows 10 Enterprise** (x86, x64)  

-   **Windows 10 IoT Enterprise** (x86, x64)  
    Esta versão inclui o canal de manutenção de longo prazo (LTSC). Para saber mais, confira [Visão geral do Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

-   **Windows Embedded 8.1 Industry** (x86, x64)    

-   **Windows Embedded 8 Standard** (x86, x64)    

-   **Windows Thin PC** (x86, x64)    

-   **Windows Embedded POSReady 7** (x86, x64)    

-   **Windows Embedded Standard 7 com SP1** (x86, x64)    


### <a name="unsupported-os-versions"></a>Versões incompatíveis do sistema operacional

As seguintes versões de sistema operacional são baseadas no Windows XP Embedded. A partir da versão 1702, não há suporte para essas versões de sistema operacional incorporadas. Para saber mais, confira [Sistemas operacionais cliente preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems).  

-   **WEPOS 1.1 com SP3** (x86)    

-   **Windows Embedded POSReady 2009** (x86)    

-   **Windows Fundamentals for Legacy PCs (WinFLP)** (x86)    

-   **Windows XP Embedded SP3** (x86)    

-   **Windows Embedded Standard 2009** (x86)  



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



##  <a name="mobile-devices-enrolled-by-microsoft-intune"></a>Dispositivos móveis registrados pelo Microsoft Intune  

 Para saber mais sobre os computadores e dispositivos que você pode gerenciar ao integrar o Microsoft Intune ao Configuration Manager, consulte os artigos a seguir na biblioteca de documentação do Microsoft Intune:  

-   [Funcionalidades de gerenciamento de dispositivos móveis do Microsoft Intune](https://docs.microsoft.com/intune/get-started/choose-how-to-manage-devices)  
-   [Recursos de gerenciamento de PC do Windows no Microsoft Intune](https://docs.microsoft.com/intune/get-started/windows-pc-management-capabilities-in-microsoft-intune)  



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

-   **Exchange Server 2010 SP1**  

-   **Exchange Server 2010 SP2**  

-   **Exchange Server 2013**  

-   **Exchange Online (Office 365)**: essa versão inclui o Business Productivity Online Standard Suite  
