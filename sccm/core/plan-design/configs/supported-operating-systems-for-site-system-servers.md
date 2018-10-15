---
title: Servidores de sistema de site com suporte
titleSuffix: Configuration Manager
description: Saiba quais versões do Windows podem ser usadas para hospedar um site ou função de sistema de site do Configuration Manager.
ms.date: 10/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3fd8e815ab57730ad2186a7e75cd51f21012383a
ms.sourcegitcommit: 265d38d55ca0db043e3a7131a56f123e1d98aa5b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/03/2018
ms.locfileid: "48236167"
---
# <a name="supported-operating-systems-for-configuration-manager-site-system-servers"></a>Sistemas operacionais compatíveis com servidores do sistema de site do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Este artigo detalha as versões do Windows que você pode usar para hospedar um site ou função de sistema de sites do Configuration Manager.


Use as informações neste artigo com as informações nos seguintes artigos:
-   [Hardware recomendado para o Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware)
-   [Pré-requisitos de site e sistema de sites para o Configuration Manager](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
-   [Números de tamanho e escala para o Configuration Manager](/sccm/core/plan-design/configs/size-and-scale-numbers)



## <a name="bkmk_2016"></a> Windows Server 2016: Standard e Datacenter

Com o Pacote Cumulativo de Atualizações 1 para o Configuration Manager versão 1606 ([KB3186654](https://support.microsoft.com/help/3186654)), há suporte para esta versão do sistema operacional nas seguintes funções:

#### <a name="site-servers"></a>Servidores do site

-   Site de administração central  
-   Site primário  
-   Site secundário  

#### <a name="site-system-servers"></a>Servidores de sistema de sites

-   Ponto de serviços Web do Catálogo de Aplicativos  
-   Ponto de sites da Web do Catálogo de Aplicativos  
-   Ponto de sincronização do Asset Intelligence  
-   Ponto de registro de certificado  
-   Ponto de conexão do gateway de gerenciamento de nuvem  
-   Ponto de serviço de data warehouse  
-   Ponto de distribuição <sup>[Observação 1](#bkmk_note1)</sup>  
-   Ponto do Endpoint Protection  
-   Ponto de registro  
-   Ponto proxy do registro  
-   Ponto de status de fallback  
-   Ponto de gerenciamento
-   Ponto do Reporting Services  
-   Ponto de Conexão de Serviço  
-   Servidor de banco de dados do site <sup>[Observação 2](#bkmk_note2)</sup>  
-   SMS_Provider  
-   Ponto de atualização de software  
-   Ponto de migração de estado



## <a name="bkmk_stor2016"></a> Windows Storage Server 2016

#### <a name="site-system-server"></a>Servidor do sistema de site

-   Ponto de distribuição <sup>[Observação 1](#bkmk_note1)</sup>  



## <a name="bkmk_2012r2"></a> Windows Server 2012 R2 (x64): Standard e Datacenter  

#### <a name="site-servers"></a>Servidores do site

-   Site de administração central  
-   Site primário  
-   Site secundário  

#### <a name="site-system-servers"></a>Servidores de sistema de sites

-   Ponto de serviços Web do Catálogo de Aplicativos  
-   Ponto de sites da Web do Catálogo de Aplicativos  
-   Ponto de sincronização do Asset Intelligence  
-   Ponto de registro de certificado  
-   Ponto de conexão do gateway de gerenciamento de nuvem  
-   Ponto de serviço de data warehouse  
-   Ponto de distribuição <sup>[Observação 1](#bkmk_note1)</sup>  
-   Ponto do Endpoint Protection  
-   Ponto de registro  
-   Ponto proxy do registro  
-   Ponto de status de fallback  
-   Ponto de gerenciamento
-   Ponto do Reporting Services  
-   Ponto de Conexão de Serviço  
-   Servidor de banco de dados do site <sup>[Observação 2](#bkmk_note2)</sup>  
-   SMS_Provider  
-   Ponto de atualização de software  
-   Ponto de migração de estado  



## <a name="bkmk_2012"></a> Windows Server 2012 (x64): Standard e Datacenter  

#### <a name="site-servers"></a>Servidores do site

-   Site de administração central  
-   Site primário  
-   Site secundário  

#### <a name="site-system-servers"></a>Servidores de sistema de sites

-   Ponto de serviços Web do Catálogo de Aplicativos  
-   Ponto de sites da Web do Catálogo de Aplicativos  
-   Ponto de sincronização do Asset Intelligence  
-   Ponto de registro de certificado  
-   Ponto de conexão do gateway de gerenciamento de nuvem  
-   Ponto de serviço de data warehouse  
-   Ponto de distribuição <sup>[Observação 1](#bkmk_note1)</sup>  
-   Ponto do Endpoint Protection  
-   Ponto de registro  
-   Ponto proxy do registro  
-   Ponto de status de fallback  
-   Ponto de gerenciamento
-   Ponto do Reporting Services  
-   Ponto de Conexão de Serviço  
-   Servidor de banco de dados do site <sup>[Observação 2](#bkmk_note2)</sup>  
-   SMS_Provider  
-   Ponto de atualização de software  
-   Ponto de migração de estado  



## <a name="bkmk_2008r2sp1"></a> Windows Server 2008 R2 com SP1 (x64): Standard, Enterprise e Datacenter  

Agora, o Windows Server 2008 R2 está com suporte estendido e não mais com suporte base, conforme detalhado na [Ciclo de Vida do Suporte da Microsoft](https://support.microsoft.com/lifecycle). Para obter mais informações sobre o suporte futuro para esses sistemas operacionais como servidores do sistema de sites com o Configuration Manager, consulte [Sistemas operacionais de servidor preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

Os servidores do site ou a maioria das funções do sistema de sites não são compatíveis com esse sistema operacional. Ele ainda é compatível com a função do sistema de sites do ponto de distribuição, incluindo pontos de distribuição pull e para PXE e multicast.

#### <a name="site-system-servers"></a>Servidores de sistema de sites
-   Ponto de distribuição <sup>[Observação 1](#bkmk_note1)</sup>  

    - Os pontos de distribuição neste sistema operacional são compatíveis com PXE e multicast.  



## <a name="bkmk_2008sp2"></a> Windows Server 2008 com SP2 (x86, x64): Standard, Enterprise e Datacenter  

Agora, o Windows Server 2008 está com suporte estendido e não mais com suporte base, conforme detalhado no [Ciclo de Vida do Suporte da Microsoft](https://support.microsoft.com/lifecycle). Para obter mais informações sobre o suporte futuro para esses sistemas operacionais como servidores do sistema de sites com o Configuration Manager, consulte [Sistemas operacionais de servidor preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

Esse sistema operacional não é compatível com servidores do site ou funções do sistema de sites, exceto pelo ponto de distribuição e ponto de distribuição pull. Continue usando esse sistema operacional como um ponto de distribuição até que a reprovação desse suporte seja comunicada ou o período de suporte estendido desse sistema operacional expire. Para obter mais informações, consulte [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095) (A instalação do CB e do LTSB do System Center Configuration Manager falha no Windows Server 2008).

#### <a name="site-system-servers"></a>Servidores de sistema de sites
-   Ponto de distribuição <sup>[Observação 1](#bkmk_note1)</sup>  

    -   Os pontos de distribuição neste sistema operacional são compatíveis com PXE e multicast.  

    -   Os pontos de distribuição deste sistema operacional não são compatíveis com a inicialização de rede de computadores cliente no modo EFI. Há suporte para computadores cliente com BIOS ou inicialização EFI no modo herdado.  



## <a name="bkmk_win10"></a> Windows 10 (x86, x64): Pro e Enterprise  

#### <a name="site-system-servers"></a>Servidores de sistema de sites

-   Ponto de distribuição <sup>[Observação 1](#bkmk_note1)</sup>  

    -   Os pontos de distribuição deste sistema operacional não são compatíveis com PXE com os Serviços de Implantação do Windows padrão. A partir da versão 1806, o PXE pode ser habilitado em um ponto de distribuição deste sistema operacional com a opção de **Habilitar um respondente PXE sem os Serviços de Implantação do Windows**. Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

    -   Os pontos de distribuição desta versão de sistema operacional não dão suporte a multicast.  



## <a name="bkmk_win81"></a> Windows 8.1 (x86, x64): Professional e Enterprise  

#### <a name="site-system-servers"></a>Servidores de sistema de sites

-   Ponto de distribuição <sup>[Observação 1](#bkmk_note1)</sup>  

    -   Os pontos de distribuição deste sistema operacional não são compatíveis com PXE com os Serviços de Implantação do Windows padrão. A partir da versão 1806, o PXE pode ser habilitado em um ponto de distribuição deste sistema operacional com a opção de **Habilitar um respondente PXE sem os Serviços de Implantação do Windows**. Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

    -   Os pontos de distribuição desta versão de sistema operacional não dão suporte a multicast.  



## <a name="bkmk_win7sp1"></a> Windows 7 com SP1 (x86, x64): Professional, Enterprise e Ultimate  

#### <a name="site-system-servers"></a>Servidores de sistema de sites

-   Ponto de distribuição <sup>[Observação 1](#bkmk_note1)</sup>  

    -   Os pontos de distribuição deste sistema operacional não são compatíveis com PXE com os Serviços de Implantação do Windows padrão. A partir da versão 1806, o PXE pode ser habilitado em um ponto de distribuição deste sistema operacional com a opção de **Habilitar um respondente PXE sem os Serviços de Implantação do Windows**. Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

    -   Os pontos de distribuição desta versão de sistema operacional não dão suporte a multicast.  



## <a name="bkmk_core1803"></a> A instalação Server Core do Windows Server, versão 1803
<!--503702-->A partir do Configuration Manager 1802,[o Windows Server, versão 1803](https://docs.microsoft.com/windows-server/get-started/get-started-with-1803) tem suporte para uso como um ponto de distribuição com as seguintes limitações:  

  -   Há suporte apenas para a versão de x64 bits.  

  -   Os pontos de distribuição deste sistema operacional não dão suporte a PXE ou multicast com os Serviços de Implantação do Windows padrão. A partir da versão 1806, o PXE pode ser habilitado em um ponto de distribuição deste sistema operacional com a opção de **Habilitar um respondente PXE sem os Serviços de Implantação do Windows**. Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="bkmk_core1709"></a> A instalação Server Core do Windows Server, versão 1709

A partir do Configuration Manager 1710, [o Windows Server, versão 1709](https://docs.microsoft.com/windows-server/get-started/get-started-with-1709) tem suporte para uso como um ponto de distribuição com as seguintes limitações:  

  -   Há suporte apenas para a versão de x64 bits.  

  -   Os pontos de distribuição deste sistema operacional não dão suporte a PXE ou multicast com os Serviços de Implantação do Windows padrão. A partir da versão 1806, o PXE pode ser habilitado em um ponto de distribuição deste sistema operacional com a opção de **Habilitar um respondente PXE sem os Serviços de Implantação do Windows**. Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="bkmk_core2016"></a> A instalação Server Core do Windows Server 2016

Com o Pacote Cumulativo de Atualizações 1 para o Configuration Manager versão 1606 ([KB3186654](https://support.microsoft.com/help/3186654)), há suporte para esta versão de sistema operacional para uso como um ponto de distribuição com as seguintes limitações:  

  -   Há suporte apenas para a versão de x64 bits.  

  -   Os pontos de distribuição deste sistema operacional não dão suporte a PXE ou multicast com os Serviços de Implantação do Windows padrão. A partir da versão 1806, o PXE pode ser habilitado em um ponto de distribuição deste sistema operacional com a opção de **Habilitar um respondente PXE sem os Serviços de Implantação do Windows**. Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="bkmk_core2012r2"></a> A instalação Server Core do Windows Server 2012 R2  

Há suporte para a instalação do Server Core do Windows Server 2012 R2 para uso como um ponto de distribuição com as seguintes limitações:  

-   Há suporte apenas para a versão de x64 bits.

-   Os pontos de distribuição deste sistema operacional não dão suporte a PXE ou multicast com os Serviços de Implantação do Windows padrão. A partir da versão 1806, o PXE pode ser habilitado em um ponto de distribuição deste sistema operacional com a opção de **Habilitar um respondente PXE sem os Serviços de Implantação do Windows**. Para saber mais, confira [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="bkmk_core2012"></a> A instalação Server Core do Windows Server 2012  

Há suporte para a instalação do Server Core do Windows Server 2012 para uso como um ponto de distribuição com as seguintes limitações:  

-   Há suporte apenas para a versão de 64 bits.  

-   Os pontos de distribuição deste sistema operacional não dão suporte a PXE ou multicast com os Serviços de Implantação do Windows padrão. A partir da versão 1806, o PXE pode ser habilitado em um ponto de distribuição deste sistema operacional com a opção de **Habilitar um respondente PXE sem os Serviços de Implantação do Windows**. Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).



## <a name="general-notes"></a>Observações gerais

#### <a name="bkmk_note1"></a> Observação 1: pontos de distribuição
Os pontos de distribuição dão suporte a várias configurações diferentes que têm diferentes requisitos. Em alguns casos, essas configurações dão suporte à instalação não apenas em servidores, mas em sistemas operacionais cliente. Para mais informações, confira [Manage content and content infrastructure](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure) (Gerenciar o conteúdo e a infraestrutura de conteúdo).  

#### <a name="bkmk_note2"></a> Observação 2: servidores de banco de dados do site
Os servidores de banco de dados do site não são compatíveis com um RODC (controlador de domínio somente leitura). Para obter mais informações, confira o artigo do Suporte da Microsoft: [Você pode encontrar problemas ao instalar o SQL Server em um controlador de domínio](https://support.microsoft.com/help/2032911). 

Além disso, os servidores do site secundário não são compatíveis com qualquer controlador de domínio.  
