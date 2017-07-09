---
title: "Configurações com suporte para o LTSB | Microsoft Docs"
description: "Entenda quais sistemas operacionais e produtos dependentes funcionam com o Branch de Manutenção em Longo Prazo do System Center Configuration Manager."
ms.custom: na
ms.date: 5/10/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f0f818d4-7f45-402f-8758-dc88bc024953
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: b0ba955aa7f854c3fa2c06ccf9ccd8ed354758b0
ms.openlocfilehash: 31bddee83b2365cfa903077ffaa1d7116b194378
ms.contentlocale: pt-br
ms.lasthandoff: 06/12/2017


---
# <a name="supported-configurations-for-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Configurações com suporte para o Branch de Manutenção em Longo Prazo do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch de Manutenção em Longo Prazo)*

Use as informações neste tópico para entender quais sistemas operacionais e dependências de produto têm suporte pelo LTSB (Long-Term Servicing Branch) do Configuration Manager.
Caso não esteja indicado de outra forma aqui ou nos tópicos específicos do LTSB, as mesmas configurações e limitações que se aplicam à versão 1606 do Branch Atual se aplicam ao LTSB.  Quando ocorrerem conflitos, use as informações que se aplicam à edição que você está usando. Normalmente, o LTSB é mais limitado do que o Branch Atual.

## <a name="general-statement-of-support"></a>Declaração geral de suporte
Há suporte para os seguintes produtos e tecnologias por esse branch do Configuration Manager. No entanto, sua inclusão neste conteúdo não expressa uma extensão do suporte para qualquer produto ou versão além do ciclo de vida de suporte individual desses produtos. Os produtos além de seu ciclo de vida de suporte não têm suporte para uso com o Configuration Manager. Para obter mais informações, confira o site do [Ciclo de Vida do Suporte da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) e leia as [Perguntas frequentes sobre a Política de Ciclo de Vida do Suporte da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=31976).

Além disso, os produtos e versões do produto que não estão listados nos tópicos a seguir não têm suporte, a menos que eles tenham sido apresentados no [Enterprise Mobility + Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/) (Blog do Enterprise Mobility + Security).

**Limitações para suporte futuro:** o LTSB tem suporte limitado para futuros sistemas operacionais de servidor e cliente e dependências de produto. A lista de plataformas para o LTSB é fixa para a vida útil da versão:

**Windows:**
- Há suporte somente para atualizações de qualidade e segurança do Windows.
- Nenhum suporte é adicionado para CB (Branches Atuais), CBB (Branches Atuais para Negócios) ou LTSB do Windows 10.
-   Não há suporte para novas versões principais do Windows Server.

**SQL Server:**
- Somente atualizações de segurança e qualidade ou atualizações secundárias como service packs têm suporte para o SQL Server.
- Não há suporte para novas versões principais do SQL Server.  

## <a name="site-systems-and-servers"></a>Servidores e sistemas de sites
O LTSB dá suporte ao uso dos seguintes sistemas operacionais de computador Windows como sistemas de sites.  Cada sistema operacional tem os mesmos requisitos e limitações que a mesma entrada em [Supported operating systems for site system servers](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers) (Sistemas operacionais com suporte para servidores de sistema de sites).  Por exemplo, a instalação Server Core do Windows 2012 R2 deve ser uma versão x64, tem suporte apenas para hospedar um ponto de distribuição e não dá suporte para PXE ou Multicast.

**Sistemas operacionais com suporte:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows Server 2008 R2 com SP1 (x64): Standard, Enterprise, Datacenter
- Windows Server 2008 com SP2 (x86, x64): Standard, Enterprise e Datacenter *(consulte a observação 1)*
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Windows 7 com SP1 (x86, x64): Professional, Enterprise, Ultimate
- A instalação Server Core do Windows Server 2012
- A instalação Server Core do Windows Server 2012 R2    

*Observação 1*: não há suporte para esse sistema operacional para servidores do site ou funções do sistema de sites, com exceção do ponto de distribuição e do ponto de distribuição pull. Você pode continuar a usar esse sistema operacional como um ponto de distribuição até que a substituição desse suporte seja anunciada ou o período de suporte estendido do sistema operacional expire. Para obter mais informações, consulte [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095) (A instalação do CB e do LTSB do System Center Configuration Manager falha no Windows Server 2008).

## <a name="client-management"></a>Gerenciamento de cliente
As seções a seguir identificam os sistemas operacionais do cliente que você pode gerenciar com o LTSB. O LTSB não dá suporte à adição de novos sistemas operacionais como clientes com suporte.

### <a name="windows-computers"></a>Computadores com Windows
Você pode usar o LTSB para gerenciar os seguintes sistemas operacionais de computadores Windows com o software cliente do Configuration Manager que está incluído com o Configuration Manager. Para mais informações, confira [Como implantar clientes em computadores Windows no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).

**Sistemas operacionais com suporte:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter (Note 1)
- Windows Server 2012 (x64): Standard, Datacenter (Note 1)
- Windows Storage Server 2012 R2 (x64)
- Windows Storage Server 2012 (x64)
- Windows Server 2008 R2 com SP1 (x64): Standard, Enterprise, Datacenter (Observação 1)
- Windows Storage Server 2008 R2 (x86, x64): Workgroup, Standard, Enterprise
- Windows Server 2008 com SP2 (x86, x64): Standard, Enterprise, Datacenter (Observação 1)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Windows 7 com SP1 (x86, x64): Professional, Enterprise, Ultimate
- A instalação Server Core do Windows Server 2012 R2 (x64) (Observação 2)
- A instalação Server Core do Windows Server 2012 (x64) (Observação 2)
- A instalação Server Core do Windows Server 2008 R2 SP1 (x64)
- A instalação Server Core do Windows Server 2008 SP2 (x86, x64)

**(Observação 1)** Há suporte para versões do Datacenter, mas sem certificação para o Configuration Manager.  
**(Observação 2)** Para dar suporte à instalação por push do cliente, o computador que executa esta versão do sistema operacional deve executar o serviço de função de Servidor de Arquivos para a função de servidor de Serviços de Arquivo e Armazenamento. Para saber mais sobre como instalar recursos do Windows em um computador Server Core, confira [Instalar funções e recursos de servidor em um servidor Server Core](https://technet.microsoft.com/library/jj574158(v=ws.11).aspx) na biblioteca do TechNet do Windows Server 2012.

### <a name="windows-embedded"></a>Windows Embedded
Você pode usar o LTSB para gerenciar os seguintes dispositivos com Windows Embedded instalando o software cliente no dispositivo.  Para mais informações, consulte [Planejando a implantação de cliente em dispositivos do Windows Embedded no System Center Configuration Manager](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices).

**Requisitos e limitações:**  

-   Todos os recursos do cliente têm suporte nos sistemas Windows Embedded com suporte que não tenham filtros de gravação habilitados.  

-   Os clientes que usam um dos procedimentos a seguir têm suporte para todos os recursos, exceto o gerenciamento de energia:  

    -   EWF (Filtros de Gravação Avançados).    

    -   FBWF (Filtros de Gravação com Base em Arquivos) de RAM    

    -   UWF (Filtros de Gravação Unificados)  

-   Não há suporte para o catálogo de aplicativos em todos os dispositivos com Windows Embedded.  

-   Antes de monitorar malware detectado em dispositivos com Windows Embedded baseados no Windows XP, é necessário instalar o pacote de script WMI do Microsoft Windows no dispositivo incorporado. Use o Windows Embedded Target Designer para instalar este pacote. Os arquivos *WBEMDISP.DLL* e *WBEMDISP.TLB* devem existir e estar registrados na pasta %windir%\System32\WBEM no dispositivo inserido a fim de garantir que o malware detectado seja relatado.  

**Sistemas operacionais com suporte:**  
-   Windows 10 Enterprise 2016 LTSB (x86, x64)  
-   Windows 10 Enterprise 2015 LTSB (x86, x64)  
-   Windows Embedded 8.1 Industry (x86, x64)    
-   Windows Thin PC (x86, x64)    
-   Windows Embedded POSReady 7 (x86, x64)    
-   Windows Embedded Standard 7 com SP1 (x86, x64)    
-   Windows Embedded POSReady 2009 (x86)   
-   Windows Embedded Standard 2009 (x86)  

### <a name="windows-ce"></a>Windows CE  
 Você pode gerenciar dispositivos Windows CE com o cliente herdado do dispositivo móvel do Configuration Manager, que está incluído com o Configuration Manager.  

**Requisitos e limitações:**  

-   O cliente de dispositivo móvel exige 0,78 MB de espaço de armazenamento para instalar o cliente. Um dispositivo móvel pode exigir até 256 KB de espaço de armazenamento adicional para entrar.    

-   Os recursos para estes dispositivos móveis variam por plataforma e tipo de cliente. Para obter informações sobre o tipo de função de gerenciamento que o Configuration Manager dá suporte para o cliente herdado do dispositivo móvel, consulte [Escolher uma solução de gerenciamento de dispositivo para o System Center Configuration Manager](/sccm/core/plan-design/choose-a-device-management-solution).  

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

### <a name="mac-computers"></a>Computadores Mac  
 Você pode usar o LTSB para gerenciar computadores com Mac OS X com o cliente do Configuration Manager para Mac.

O pacote de instalação do cliente Mac não é fornecido com a mídia do Configuration Manager. É possível baixá-lo como parte do download dos “Clientes para sistemas operacionais adicionais” no [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

O suporte para sistemas operacionais Mac é limitado aos listados nesta seção. O suporte não inclui sistemas operacionais adicionais que podem ter suporte por uma atualização futura para pacotes de instalação de cliente Mac para o Branch Atual.

Para obter mais informações, consulte [Como implantar clientes em computadores Mac no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-macs).

**Versões com suporte:**  
-   Mac OS X 10.9 (Mavericks)  
-   Mac OS X 10.10 (Yosemite)  
-   Mac OS X 10.11 (El Capitan)  

## <a name="linux-and-unix-servers"></a>Servidores Linux e UNIX
Você pode usar o LTSB para gerenciar servidores Linux e UNIX com o cliente do Configuration Manager para Linux e UNIX.

Os pacotes de instalação do cliente para Linux e UNIX não são fornecidos com a mídia do Configuration Manager. É possível baixá-los como parte do download dos “Clientes para sistemas operacionais adicionais” no [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184). Além dos pacotes de instalação do cliente, o download do cliente inclui o script de instalação que gerencia a instalação do cliente em cada computador.

O suporte para sistemas operacionais Linux e UNIX é limitado aos listados nesta seção. O suporte não inclui sistemas operacionais adicionais que podem ter suporte por uma atualização futura para pacotes de cliente Linux e UNIX para o Branch Atual.

**Requisitos e limitações:**  

-   Para examinar as dependências de arquivo do sistema operacional do cliente para Linux e UNIX, confira [Prerequisites for Client Deployment to Linux and UNIX Servers](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers#bkmk_clientdeployprereqforlnu) (Pré-requisitos para implantação do cliente para servidores Linux e UNIX).  
-   Para obter uma visão geral das funcionalidades de gerenciamento com suporte para computadores que executam o Linux ou UNIX, consulte [Como implantar clientes para servidores UNIX e Linux no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).  
-   Para as versões com suporte do Linux e UNIX, a versão listada inclui todas as versões secundárias subsequentes. Por exemplo, quando o suporte for indicado para o CentOS versão 6, isso também incluirá qualquer versão secundária subsequente do CentOS 6, como o CentOS 6.3. Da mesma forma, quando o suporte for listado para um sistema de operacional que usa service packs, como o SUSE Linux Enterprise Server 11 SP1, o suporte incluirá os service packs subsequentes para essa versão do sistema operacional.
-   Para obter informações sobre pacotes de instalação do cliente e o Agente Universal, consulte [Como implantar clientes para servidores UNIX e Linux no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).


**Versões com suporte:**   
As versões a seguir têm suporte usando o arquivo .tar indicado.  
### <a name="aix"></a>AIX  

|Versão|Arquivo|  
|-|-|  
|Versão 5.3 (Power)|ccm-Aix53ppc.&lt;build\>.tar|  
|Versão 6.1 (Power)|ccm-Aix61ppc.&lt;build\>.tar|  
|Versão 7.1 (Power)|ccm-Aix71ppc.&lt;build\>.tar|  

### <a name="centos"></a>CentOS  

|Versão|Arquivo|  
|-|-|  
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="debian"></a>Debian  

|Versão|Arquivo|    
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

|Versão|Arquivo|  
|-|-|  
|Versão 11iv2 IA64|ccm-HpuxB.11.23i64.&lt;build\>.tar|  
|Versão 11iv2 PA-RISC|ccm-HpuxB.11.23PA.&lt;build\>.tar|  
|Versão 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  
|Versão 11iv3 PA-RISC|ccm-HpuxB.11.31PA.&lt;build\>.tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|Versão|Arquivo|    
|-|-|  
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Versão|Arquivo|  
|-|-|  
|Versão 4 x86|ccm-RHEL4x86.&lt;build\>.tar|  
|Versão 4 x64|ccm-RHEL4x64.&lt;build\>.tar|  
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="solaris"></a>Solaris  

|Versão|Arquivo|   
|-|-|  
|Versão 9 SPARC|ccm-Sol9sparc.&lt;build\>.tar|  
|Versão 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|Versão 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|Versão 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|Versão 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Versão|Arquivo|  
|-|-|  
|Versão 9 x86|ccm-SLES9x86.&lt;build\>.tar|  
|Versão 10 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 10 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 11 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 11 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 12 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="ubuntu"></a>Ubuntu  

|Versão|Arquivo|    
|-|-|  
|Versão 10.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 10.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 12.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 12.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 14.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 14.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="exchange-server-connector"></a>Conector do Exchange Server
 O LTSB dá suporte ao gerenciamento limitado de dispositivos que se conectam à instância do Exchange Server, sem instalar o software cliente. Para obter mais informações, consulte [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).

 **Requisitos e limitações:**  

-   O Configuration Manager oferece gerenciamento limitado para dispositivos móveis. O gerenciamento limitado está disponível ao usar o conector do Exchange Server para dispositivos habilitados para EAS (Exchange Active Sync) que se conectam a um servidor que executa o Exchange Server ou o Exchange Online.  

-   Para mais informações sobre para quais funções de gerenciamento o Configuration Manager dá suporte para dispositivos móveis que o conector do Exchange Server gerencia, confira [Escolher uma solução de gerenciamento de dispositivo para o System Center Configuration Manager](/sccm/core/plan-design/choose-a-device-management-solution).  

**Versões com suporte do Exchange Server:**  
-   Exchange Server 2010 SP1  
-   Exchange Server 2010 SP2  
-   Exchange Server 2013  

> [!NOTE]
> O LTSB não dá suporte para gerenciar dispositivos que se conectam por um serviço online, como o Exchange Online (Office 365).


## <a name="configuration-manager-console"></a>Console do Configuration Manager
O LTSB dá suporte aos seguintes sistemas operacionais para executar o console do Configuration Manager. Cada computador que hospeda o console deve ter o .NET Framework com a versão mínima 4.5.2, exceto para Windows 10, que exige no mínimo o .NET Framework 4.6.

**Sistemas operacionais com suporte:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows Server 2008 R2 com SP1 (x64): Standard, Enterprise, Datacenter
- Windows Server 2008 com SP2 (x86, x64): Standard, Enterprise, Datacenter
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Windows 7 com SP1 (x86, x64): Professional, Enterprise, Ultimate


## <a name="sql-server-versions-supported-for-the-site-database-and-reporting-point"></a>Versões do SQL Server com suporte para o ponto de relatório e banco de dados do site
O LTSB dá suporte às seguintes versões do SQL Server para hospedar o ponto de relatório e banco de dados do site. Para cada versão com suporte, os mesmos requisitos de configuração e limitação que aparecem em [Support for SQL Server versions](/sccm/core/plan-design/configs/support-for-sql-server-versions) (Suporte para versões do SQL Server) para o Branch Atual se aplicam ao LTSB.  Isso inclui o uso de um Cluster do SQL Server ou o grupo de disponibilidade do SQL Server AlwaysOn.  

**Versões com suporte:**

- SQL Server 2016: Standard, Enterprise
- SQL Server 2014 SP2: Standard, Enterprise
- SQL Server 2014 SP1: Standard, Enterprise
- SQL Server 2012 SP3: Standard, Enterprise
- SQL Server 2008 R2 SP3: Standard, Enterprise, Datacenter
- SQL Server 2016 Express
- SQL Server 2014 Express SP2
- SQL Server 2014 Express SP1
- SQL Server 2012 Express SP3

## <a name="support-for-active-directory-domains"></a>Suporte para domínios do Active Directory
Todos os sistemas de sites do LTSB devem ser membros de um domínio do Active Directory do Windows com suporte. O suporte para domínios do Active Directory tem os mesmos requisitos e limitações que aparecem no [Support for Active Directory domains](/sccm/core/plan-design/configs/support-for-active-directory-domains) (Suporte para domínios do Active Directory), mas é limitada para os seguintes níveis funcionais de domínio:

**Níveis com suporte:**
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

## <a name="additional-support-topics-that-apply-to-the-long-term-servicing-branch"></a>Tópicos de suporte adicionais que se aplicam ao Branch de Manutenção em Longo Prazo
As informações nos tópicos sobre o Branch Atual a seguir se aplicam ao LTSB:
- [Números de tamanho e escala](/sccm/core/plan-design/configs/size-and-scale-numbers)
- [Pré-requisitos de sites e do sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
- [Opções de alta disponibilidade](/sccm/protect/understand/high-availability-options)
- [Hardware recomendado](/sccm/core/plan-design/configs/recommended-hardware)
- [Suporte para redes e recursos do Windows](/sccm/core/plan-design/configs/support-for-windows-features-and-networks)
- [Suporte para ambientes de virtualização](/sccm/core/plan-design/configs/support-for-virtualization-environments)

