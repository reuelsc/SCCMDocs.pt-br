---
title: Clientes e dispositivos com suporte | System Center Configuration Manager
description: "Saiba a quais sistemas operacionais o System Center Configuration Manager oferece dá suporte para clientes e dispositivos."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
caps.latest.revision: 5
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 862291f52d5a1bb34fb5483806972fcf70f158a8

---
# <a name="supported-operating-systems-for-clients-and-devices-for-system-center-configuration-manager"></a>Sistemas operacionais com suporte para clientes e dispositivos para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*




 O System Center Configuration Manager oferece suporte à instalação de um software cliente em vários computadores com Windows, Mac e Linux e UNIX.  

 **Requisitos e limitações para todos os clientes:**  

-   Não há suporte para alterar as configurações de tipo de inicialização ou de Fazer logon como de qualquer serviço do Configuration Manager. Isso pode impedir o funcionamento correto dos serviços essenciais.    

-   Não há suporte para a instalação ou execução do cliente do Configuration Manager para Linux ou UNIX, ou o cliente para Mac, em computadores com uma conta diferente da raiz. Isso pode impedir o funcionamento correto dos serviços essenciais.  

##  <a name="a-namebkmkwinclientosa-windows-computers"></a><a name="bkmk_WinClientos"></a> Computadores Windows  
 É possível gerenciar computadores Windows com o cliente do Configuration Manager, incluído com o Configuration Manager. Para mais informações, confira [How to deploy clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md) (Como implantar clientes em computadores Windows no System Center Configuration Manager).  

**Sistemas operacionais com suporte:**  

-  **Windows Server 2016** – Standard, Datacenter <sup>1</sup>
  - Há suporte para o Windows Server 2016 a partir da versão 1606 do Configuration Manager com o pacote cumulativo de atualizações do hotfix de KB3186654 (ou a versão de linha de base do 1606 lançada em outubro de 2016).  


-   **Windows Server 2012 R2** (x64) – Standard, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2012 R2** (x64)    

-   **Windows Server 2012** (x64) – Standard, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2012** (x64)    

-   **Windows Server 2008 R2 com SP1** (x64) – Standard, Enterprise, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2008 R2** (x86, x64) – Workgroup, Standard, Enterprise    

-   **Windows Server 2008 com SP2** (x86, x64) – Standard, Enterprise, Datacenter <sup>1</sup>    

-   **Windows 10 Enterprise LTSB** (x86, x64) <sup>3</sup>    

-   **Windows 10** (x86, x64) – Pro, Enterprise    

-   **Windows 8.1** (x86, x64) – Professional, Enterprise    

-   **Windows 8** (x86, x64) – Professional, Enterprise    

-   **Windows 7 com SP1** (x86, x64) – Professional, Enterprise, Ultimate    

-   **A instalação Server Core do Windows Server 2012 R2** (x64) <sup>2</sup>    

-   **A instalação Server Core do Windows Server 2012** (x64) <sup>2</sup>    

-   **A instalação Server Core do Windows Server 2008 R2**  
    **(sem nenhum service pack ou com o SP1)** (x64)    

-   **A instalação Server Core do Windows Server 2008 SP2** (x86, x64)  

 <sup>1</sup> Há suporte para versões do Datacenter, mas sem certificação para o Configuration Manager. O suporte de hotfix não é oferecido para problemas específicos do Windows Server Datacenter Edition.  

 <sup>2</sup> Para dar suporte à instalação do cliente por push, o computador que executa esta versão do sistema operacional deve executar o serviço de função do Servidor de Arquivos para a função de servidor dos Serviços de Arquivo e Armazenamento. Para saber mais sobre como instalar recursos do Windows em um computador Server Core, confira [Instalar funções e recursos de servidor em um servidor Server Core](http://go.microsoft.com/fwlink/p/?LinkId=299359) na biblioteca do TechNet do Windows Server 2012.  

 <sup>3</sup> O uso deste sistema operacional exige a versão 1602 ou posterior.  

##  <a name="a-namebkmkembeddedosa-windows-embedded"></a><a name="bkmk_EmbeddedOS"></a> Windows Embedded  
 É possível gerenciar dispositivos com Windows Embedded instalando o software cliente do Configuration Manager no dispositivo.  Para mais informações, consulte [Planejando a implantação de cliente em dispositivos do Windows Embedded no System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

**Requisitos e limitações:**  

-   Todos os recursos do cliente têm suporte nos sistemas Windows Embedded com suporte que não tenham filtros de gravação habilitados.  

-   Os clientes que usam um dos procedimentos a seguir têm suporte para todos os recursos que esperam o gerenciamento de energia:  

    -   EWF (Filtros de Gravação Avançados).    

    -   FBWF (Filtros de Gravação com Base em Arquivos) de RAM    

    -   UWF (Filtros de Gravação Unificados)  

-   Não há suporte para o catálogo de aplicativos em todos os dispositivos com Windows Embedded.  

-   Antes de monitorar malware detectado em dispositivos com Windows Embedded baseados no Windows XP, é necessário instalar o pacote de script WMI do Microsoft Windows no dispositivo incorporado. Use o Windows Embedded Target Designer para instalar este pacote. Os arquivos **WBEMDISP.DLL** e **WBEMDISP.TLB** devem existir e estar registrados na pasta **%windir%\System32\WBEM** no dispositivo inserido a fim de garantir que o malware detectado seja relatado.  

**Sistemas operacionais com suporte:**  

-   **Windows 10 Enterprise** (x86, x64)  

-   **Windows 10 IoT Enterprise** (x86, x64)  

-   **Windows Embedded 8.1 Industry** (x86, x64)    

-   **Windows Embedded 8 Industry** (x86, x64)    

-   **Windows Embedded 8 Standard** (x86, x64)    

-   **Windows Embedded 8 Pro** (x86, x64)    

-   **Windows Thin PC** (x86, x64)    

-   **Windows Embedded POSReady 7** (x86, x64)    

-   **Windows Embedded Standard 7 com SP1** (x86, x64)    

-   **WEPOS 1.1 com SP3** (x86)    

-   **Windows Embedded POSReady 2009** (x86)    

-   **Windows Fundamentals for Legacy PCs (WinFLP)** (x86)    

-   **Windows XP Embedded SP3** (x86)    

-   **Windows Embedded Standard 2009** (x86)  

## <a name="windows-ce"></a>Windows CE  
 Você pode gerenciar dispositivos Windows CE com o cliente herdado do dispositivo móvel do Configuration Manager, que está incluído com o Configuration Manager.  

**Requisitos e limitações**  

-   O cliente de dispositivo móvel exige 0,78 MB de espaço de armazenamento para instalar o cliente. O registro em log no dispositivo móvel pode exigir até 256 KB de espaço adicional de armazenamento.    

-   Os recursos para estes dispositivos móveis variam por plataforma e tipo de cliente. Para obter informações sobre a quais funções de gerenciamento o Configuration Manager dá suporte para o cliente herdado do dispositivo móvel, consulte [Escolher uma solução de gerenciamento de dispositivo para o System Center Configuration Manager](../../../core/plan-design/choose-a-device-management-solution.md).  

**Sistemas operacionais com suporte:**  

-   Windows CE 7.0 (processadores ARM e x86)  

**Os idiomas com suporte incluem:**  

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
 É possível gerenciar computadores com Mac OS X com o cliente do Configuration Manager para Mac.  

 O pacote de instalação do cliente Mac não é fornecido com a mídia do Configuration Manager. É possível baixá-lo como parte do download dos Clientes para sistemas operacionais adicionais no [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

**Requisitos e limitações:**  

 É necessário usar o cliente do Configuration Manager para Mac (versão 5.0.8333.1 ou posterior), que deve ser baixado separadamente. Ao contrário do cliente do Windows, o cliente do Mac não está incluído no software do Configuration Manager quando você o instala. Para baixar o cliente do Mac, acesse [Microsoft System Center Configuration Manager – Clientes para sistemas operacionais adicionais](http://go.microsoft.com/fwlink/?LinkID=525184).  

 Para obter mais informações, consulte [Como implantar clientes em computadores Mac no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-macs.md).  

**Versões com suporte:**  

-   **Mac OS X 10.9** (Mavericks)  

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

##  <a name="a-namebkmklinuxosa-linux-and-unix-servers"></a><a name="bkmk_LinuxOS"></a> Servidores Linux e UNIX  
 É possível gerenciar servidores Linux e UNIX com o cliente do Configuration Manager para Linux e UNIX.  

 Os pacotes de instalação do cliente para Linux e UNIX não são fornecidos com a mídia do Configuration Manager. É possível baixá-los como parte do download dos Clientes para sistemas operacionais adicionais no [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184). Além dos pacotes de instalação do cliente, o download do cliente inclui o script de instalação que gerencia a instalação do cliente em cada computador.  

**Requisitos e limitações:**  

-   Para examinar as dependências de arquivo do sistema operacional do cliente para Linux e UNIX, confira [Prerequisites for Client Deployment to Linux and UNIX Servers](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU) (Pré-requisitos para implantação do cliente para servidores Linux e UNIX).  

-   Para obter uma visão geral das funcionalidades de gerenciamento com suporte para computadores que executam o Linux ou UNIX, consulte [Como implantar clientes para servidores UNIX e Linux no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

-   Para as versões com suporte do Linux e UNIX, a versão listada inclui todas as versões secundárias subsequentes. Por exemplo, quando o suporte for indicado para o CentOS versão 6, isso também incluirá qualquer versão secundária subsequente do CentOS 6, como o CentOS 6.3. Da mesma forma, quando o suporte for listado para um sistema de operacional que usa service packs, como o SUSE Linux Enterprise Server 11 SP1, o suporte incluirá os service packs subsequentes para essa versão do sistema operacional.  

-   Para obter informações sobre pacotes de instalação do cliente e o Agente Universal, consulte [Como implantar clientes para servidores UNIX e Linux no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

**Versões com suporte:** as versões a seguir têm suporte usando o arquivo .tar indicado.  

### <a name="aix"></a>AIX  

|||  
|-|-|  
|Versão 5.3 (Power)|ccm-Aix53ppc.&lt;build\>.tar|  
|Versão 6.1 (Power)|ccm-Aix61ppc.&lt;build\>.tar|  
|Versão 7.1 (Power)|ccm-Aix71ppc.&lt;build\>.tar|  

### <a name="centos"></a>CentOS  

|||  
|-|-|  
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="debian"></a>Debian  

|||  
|-|-|  
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 8 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 8 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="hp-ux"></a>HP-UX  

|||  
|-|-|  
|Versão 11iv2 IA64|ccm-HpuxB.11.23i64.&lt;build\>.tar|  
|Versão 11iv2 PA-RISC|ccm-HpuxB.11.23PA.&lt;build\>.tar|  
|Versão 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  
|Versão 11iv3 PA-RISC|ccm-HpuxB.11.31PA.&lt;build\>.tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|||  
|-|-|  
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|||  
|-|-|  
|Versão 4 x86|ccm-RHEL4x86.&lt;build\>.tar|  
|Versão 4 x64|ccm-RHEL4x64.&lt;build\>.tar|  
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="solaris"></a>Solaris  

|||  
|-|-|  
|Versão 9 SPARC|ccm-Sol9sparc.&lt;build\>.tar|  
|Versão 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|Versão 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|Versão 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|Versão 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|||  
|-|-|  
|Versão 9 x86|ccm-SLES9x86.&lt;build\>.tar|  
|Versão 10 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 10 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 11 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 11 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 12 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="ubuntu"></a>Ubuntu  

|||  
|-|-|  
|Versão 10.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 10.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 12.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 12.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 14.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 14.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  

##  <a name="a-namebkmkintuneosa-mobile-devices-enrolled-by-microsoft-intune"></a><a name="bkmk_IntuneOS"></a> Dispositivos móveis registrados pelo Microsoft Intune  
 Para obter detalhes sobre os computadores e dispositivos que é possível gerenciar ao integrar Microsoft Intune ao Configuration Manager, consulte os dois tópicos a seguir na biblioteca de documentação do Microsoft Intune:  

-   [Funcionalidades de gerenciamento de dispositivos móveis do Microsoft Intune](https://docs.microsoft.com/intune/get-started/choose-how-to-manage-devices)  
-   [Recursos de gerenciamento de PC do Windows no Microsoft Intune](https://docs.microsoft.com/intune/get-started/windows-pc-management-capabilities-in-microsoft-intune)  

##  <a name="a-namebkmkonpremosa-on-premises-mobile-device-management"></a><a name="bkmk_OnpremOS"></a> Gerenciamento de dispositivo móvel local  
 O Configuration Manager tem recursos internos para gerenciar dispositivos locais sem instalar o software cliente.  Para obter mais informações, consulte [Gerenciar dispositivos móveis com infraestrutura local no System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

 **Requisitos e limitações:**  

-   É necessário configurar o **Ponto de conexão de serviço** no site de camada superior de sua hierarquia  

 **Sistemas operacionais com suporte:**  

-   **Windows 10 Pro** (x86, x64)  

-   **Windows 10 Pro Enterprise** (x86, x64)  

-   **Windows 10 IoT Enterprise** (x86, x64)

-   **Windows 10 Mobile**  

-   **Windows 10 Mobile Enterprise**  

-  **Windows 10 IoT Mobile Enterprise**

##  <a name="a-namebkmkexsrvconosa-exchange-server-connector"></a><a name="bkmk_ExSrvConOS"></a> Conector do Exchange Server  
 O Configuration Manager oferece suporte ao gerenciamento limitado de dispositivos que se conectam ao Exchange Server, sem instalar o software cliente.  Para obter mais informações, consulte [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

 **Requisitos e limitações:**  

-   O Configuration Manager oferece gerenciamento limitado para dispositivos móveis ao usar o conector do Exchange Server para dispositivos compatíveis com EAS (Exchange Active Sync) que se conectam a um servidor que executa o Exchange Server ou o Exchange Online.  

-   Para saber mais sobre a quais funções de gerenciamento o Configuration Manager dá suporte para dispositivos móveis gerenciados pelo conector do Exchange Server, consulte Determinar como gerenciar dispositivos móveis no Configuration Manager.  

**Versões com suporte do Exchange Server:**  

-   **Exchange Server 2010 SP1**  

-   **Exchange Server 2010 SP2**  

-   **Exchange Server 2013**  

-   **Exchange Online (Office 365)** – inclui o Business Productivity Online Standard Suite  



<!--HONumber=Nov16_HO1-->


