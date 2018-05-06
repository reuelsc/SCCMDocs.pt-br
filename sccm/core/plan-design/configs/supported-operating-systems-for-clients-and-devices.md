---
title: Clientes e dispositivos com suporte
titleSuffix: Configuration Manager
description: Saiba a quais sistemas operacionais o System Center Configuration Manager oferece dá suporte para clientes e dispositivos.
ms.custom: na
ms.date: 04/17/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
caps.latest.revision: 5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d6befce522bcfef293f36def39405e9555cd3510
ms.sourcegitcommit: e23350fe65ff99228274e465b24b5e163769f38f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/20/2018
---
# <a name="supported-operating-systems-for-clients-and-devices-for-system-center-configuration-manager"></a>Sistemas operacionais com suporte para clientes e dispositivos para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


 O Configuration Manager dá suporte à instalação de um software cliente em vários computadores Windows, Mac, Linux e UNIX.  

 **Requisitos e limitações para todos os clientes:**  

-   A alteração das configurações do tipo de inicialização ou **Fazer logon como** para qualquer serviço do Configuration Manager não tem suporte e pode impedir que serviços essenciais funcionem corretamente.    

-   Não há suporte para a instalação ou execução do cliente do Configuration Manager para Linux ou UNIX ou do cliente para Mac em computadores com uma conta diferente da raiz. Isso pode impedir o funcionamento correto dos serviços essenciais.  

##  <a name="windows-computers"></a>Computadores com Windows  
 Você pode usar o cliente do Configuration Manager que está incluído no Configuration Manager para gerenciar os seguintes sistemas operacionais do Windows. Para mais informações, confira [Como implantar clientes em computadores Windows no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

**Sistemas operacionais com suporte:**  


-  **Windows Server 2016**: Standard, Datacenter <sup>1</sup>
  - O sistema operacional é compatível desde o Configuration Manager versão 1606, com o pacote cumulativo de atualizações do hotfix do KB3186654 (ou a versão de linha de base 1606, lançada em outubro de 2016).  

-   **Windows Storage Server 2016**  

-   **Windows Server 2012 R2** (x64): Standard, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2012 R2** (x64)    

-   **Windows Server 2012** (x64): Standard, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2012** (x64)    

-   **Windows Server 2008 R2 com SP1** (x64): Standard, Enterprise, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2008 R2** (x86, x64): Workgroup, Standard, Enterprise    

-   **Windows Server 2008 com SP2** (x86, x64): Standard, Enterprise, Datacenter <sup>1</sup>    

-   **Windows 10** Confira [Suporte para versões do Windows 10](/sccm/core/plan-design/configs/support-for-windows-10) para obter detalhes sobre as diferentes versões do Windows 10 para as quais as diferentes versões do Configuration Manager dão suporte.

-   **Windows 8.1** (x86, x64): Professional, Enterprise    

<!---   **Windows 8** (x86, x64): Professional, Enterprise  -removed Jan 12,2018 sms505863-->

-   **Windows 7 com SP1** (x86, x64): Professional, Enterprise e Ultimate    

-   **A instalação Server Core do Windows Server, versão 1709** (x64) <sup>2</sup>
  - Este sistema operacional é compatível a partir da versão 1710.

-   **A instalação Server Core do Windows Server 2016** (x64) <sup>2</sup>
  - Este sistema operacional é compatível a partir da versão 1606, com o pacote cumulativo de atualizações do hotfix do KB3186654 (ou a versão de linha de base 1606, lançada em outubro de 2016).


-   **A instalação Server Core do Windows Server 2012 R2** (x64) <sup>2</sup>    

-   **A instalação Server Core do Windows Server 2012** (x64) <sup>2</sup>    

-   **A instalação Server Core do Windows Server 2008 R2**  
    **(sem nenhum service pack ou com o SP1)** (x64)    

-   **A instalação Server Core do Windows Server 2008 SP2** (x86, x64)  

 <sup>1</sup> Há suporte para versões do Datacenter, mas sem certificação para o Configuration Manager. O suporte de hotfix não é oferecido para problemas específicos do Windows Server Datacenter Edition.  

 <sup>2</sup> Para dar suporte à instalação do cliente por push, o computador que executa esta versão do sistema operacional deve executar o serviço de função do Servidor de Arquivos para a função de servidor dos Serviços de Arquivo e Armazenamento. Para saber mais sobre como instalar recursos do Windows em um computador Server Core, confira [Instalar funções e recursos de servidor em um servidor Server Core](http://go.microsoft.com/fwlink/p/?LinkId=299359) na biblioteca do TechNet do Windows Server 2012.  


##  <a name="windows-embedded-computers"></a>Computadores Windows Embedded  
 É possível gerenciar dispositivos com Windows Embedded instalando o software cliente do Configuration Manager no dispositivo.  Para mais informações, consulte [Planejando a implantação de cliente em dispositivos do Windows Embedded no System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

**Requisitos e limitações:**  

-   Todos os recursos do cliente têm suporte nos sistemas Windows Embedded que não tenham filtros de gravação habilitados.  

-   Os clientes que usam um dos procedimentos a seguir têm suporte para todos os recursos, exceto o gerenciamento de energia:  

    -   EWF (Filtros de Gravação Avançados).    

    -   FBWF (Filtros de Gravação com Base em Arquivos) de RAM    

    -   UWF (Filtros de Gravação Unificados)  

-   Não há suporte para o catálogo de aplicativos em todos os dispositivos com Windows Embedded.  

-   Antes de monitorar malware detectado em dispositivos Windows Embedded baseados no Windows XP, é necessário instalar o pacote de script WMI do Microsoft Windows no dispositivo. Use o Windows Embedded Target Designer para instalar este pacote.
Os arquivos **WBEMDISP.DLL** e **WBEMDISP.TLB** devem existir e estar registrados na pasta **%windir%\System32\WBEM** no dispositivo inserido a fim de garantir que o malware detectado seja relatado.  

**Sistemas operacionais com suporte:**  

-   **Windows 10 Enterprise** (x86, x64)  

-   **Windows 10 IoT Enterprise** (x86, x64)  

-   **Windows Embedded 8.1 Industry** (x86, x64)    

   <!----   **Windows Embedded 8 Industry** (x86, x64)  -removed Jan 12,2018 sms505863-->

-   **Windows Embedded 8 Standard** (x86, x64)    

<!---   **Windows Embedded 8 Pro** (x86, x64)    -removed Jan 12,2018 sms505863-->

-   **Windows Thin PC** (x86, x64)    

-   **Windows Embedded POSReady 7** (x86, x64)    

-   **Windows Embedded Standard 7 com SP1** (x86, x64)    

Os seguintes sistemas operacionais têm base no Windows XP Embedded e só têm suporte com o Configuration Manager versão 1610 e anterior. [A partir da versão 1702, esses sistemas operacionais inseridos não terão mais suporte](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems).  

-   **WEPOS 1.1 com SP3** (x86)    

-   **Windows Embedded POSReady 2009** (x86)    

-   **Windows Fundamentals for Legacy PCs (WinFLP)** (x86)    

-   **Windows XP Embedded SP3** (x86)    

-   **Windows Embedded Standard 2009** (x86)  

## <a name="windows-ce-computers"></a>Computadores Windows CE
 Você pode gerenciar dispositivos Windows CE com o cliente herdado do dispositivo móvel do Configuration Manager, que está incluído com o Configuration Manager.  

**Requisitos e limitações**  

-   O cliente de dispositivo móvel requer 0,78 MB de espaço de armazenamento para a instalação. A entrada pode exigir até 256 KB de espaço de armazenamento adicional.    

-   Os recursos para estes dispositivos móveis variam por plataforma e tipo de cliente. Para obter informações sobre quais funções de gerenciamento têm suporte, confira [Escolher uma solução de gerenciamento de dispositivo para o System Center Configuration Manager](../../../core/plan-design/choose-a-device-management-solution.md).  

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

 O pacote de instalação do cliente Mac não é fornecido com a mídia do Configuration Manager. Baixe os **Clientes para Sistemas Operacionais Adicionais** no [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

 Para obter mais informações, consulte [Como implantar clientes em computadores Mac no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-macs.md).  

**Versões com suporte:**  

-   **Mac OS X 10.6** (Snow Leopard)

-   **Mac OS X 10.7** (Lion)

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra)

-   **Mac OS X 10.13** (macOS High Sierra)

##  <a name="linux-and-unix-servers"></a>Servidores Linux e UNIX  
 É possível gerenciar servidores Linux e UNIX com o cliente do Configuration Manager para Linux e UNIX.  

 Os pacotes de instalação do cliente para Linux e UNIX não são fornecidos com a mídia do Configuration Manager. Baixe os **Clientes para Sistemas Operacionais Adicionais** no [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184). Além dos pacotes de instalação do cliente, o download do cliente inclui o script que gerencia a instalação do cliente em cada computador.  

**Requisitos e limitações:**  

-   Para examinar as dependências de arquivo do sistema operacional do cliente para Linux e UNIX, confira [Prerequisites for Client Deployment to Linux and UNIX Servers](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU) (Pré-requisitos para implantação do cliente para servidores Linux e UNIX).  

-   Para obter uma visão geral das funcionalidades de gerenciamento com suporte para Linux ou UNIX, consulte [Como implantar clientes para servidores UNIX e Linux no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

-   Para as versões com suporte do Linux e UNIX, a versão listada inclui todas as versões secundárias subsequentes. Por exemplo, o CentOS versão 6 inclui o CentOS 6.3. Da mesma forma, o suporte para um sistema de operacional que usa service packs (como o SUSE Linux Enterprise Server 11 SP1) inclui os service packs subsequentes para essa versão do sistema operacional.  

-   Para obter informações sobre pacotes de instalação do cliente e o Agente Universal, consulte [Como implantar clientes para servidores UNIX e Linux no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

**Versões com suporte:** as versões a seguir têm suporte usando o arquivo .tar indicado.  

### <a name="aix"></a>AIX  

|||  
|-|-|  
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
|Versão 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  

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
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="solaris"></a>Solaris  

|||  
|-|-|  
|Versão 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|Versão 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|Versão 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|Versão 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|||  
|-|-|  
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
|Versão 16.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 16.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  


##  <a name="mobile-devices-enrolled-by-microsoft-intune"></a>Dispositivos móveis registrados pelo Microsoft Intune  
 Para obter detalhes sobre os computadores e dispositivos que você pode gerenciar ao integrar o Microsoft Intune ao Configuration Manager, consulte os dois tópicos a seguir na biblioteca de documentação do Microsoft Intune:  

-   [Funcionalidades de gerenciamento de dispositivos móveis do Microsoft Intune](https://docs.microsoft.com/intune/get-started/choose-how-to-manage-devices)  
-   [Recursos de gerenciamento de PC do Windows no Microsoft Intune](https://docs.microsoft.com/intune/get-started/windows-pc-management-capabilities-in-microsoft-intune)  

##  <a name="bkmk_OnpremOS"></a> Gerenciamento de dispositivo móvel local  
 O Configuration Manager tem recursos internos para gerenciar dispositivos locais sem instalar o software cliente.  Para obter mais informações, consulte [Gerenciar dispositivos móveis com infraestrutura local no System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

 **Requisitos e limitações:**  

-   É necessário configurar o **Ponto de conexão de serviço** no site de camada superior de sua hierarquia.  

**Sistemas operacionais com suporte:**  

- **Windows 10 Pro** (x86, x64)  

- **Windows 10 Pro Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)

- **Windows 10 Mobile**  

- **Windows 10 Mobile Enterprise**  

- **Windows 10 IoT Mobile Enterprise**

- **Windows 10 Team para o Surface Hub**

##  <a name="bkmk_ExSrvConOS"></a> Conector do Exchange Server  
O Configuration Manager dá suporte ao gerenciamento limitado de dispositivos que se conectam ao Exchange Server, sem instalar o cliente do Configuration Manager. Para obter mais informações, consulte [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

 **Requisitos e limitações:**  

-   O Configuration Manager oferece gerenciamento limitado para dispositivos móveis ao usar dispositivos com o conector do Exchange Server para o Exchange Active Sync que se conecta a um servidor que executa o Exchange Server ou o Exchange Online.  

-   Para saber mais sobre a quais funções de gerenciamento o Configuration Manager dá suporte para dispositivos móveis gerenciados pelo conector do Exchange Server, consulte Determinar como gerenciar dispositivos móveis no Configuration Manager.  

**Versões com suporte do Exchange Server:**  

-   **Exchange Server 2010 SP1**  

-   **Exchange Server 2010 SP2**  

-   **Exchange Server 2013**  

-   **Exchange Online (Office 365)**: inclui o Business Productivity Online Standard Suite  
