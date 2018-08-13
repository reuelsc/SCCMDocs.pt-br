---
title: Servidores de sistema de site com suporte
titleSuffix: Configuration Manager
description: Saiba quais versões do Windows podem ser usadas para hospedar um site ou função de sistema de site do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cccd695c51aa5628b18f8341f50849a73b0d9a2c
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384904"
---
# <a name="supported-operating-systems-for-configuration-manager-site-system-servers"></a>Sistemas operacionais compatíveis com servidores do sistema de site do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Este artigo detalha as versões do Windows que você pode usar para hospedar um site ou função de sistema de sites do Configuration Manager.


Use as informações neste artigo com as informações nos seguintes artigos:
-   [Hardware recomendado para o Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware)
-   [Pré-requisitos de site e sistema de sites para o Configuration Manager](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
-   [Números de tamanho e escala para o Configuration Manager](/sccm/core/plan-design/configs/size-and-scale-numbers)



## <a name="windows-server-2016-standard-and-datacenter"></a>Windows Server 2016: Standard e Datacenter
Com o pacote cumulativo de atualizações do hotfix da KB3186654, há suporte para as seguintes funções nesse sistema operacional:

**Servidores do site:**  

-   Site de administração central  

-   Site primário  

-   Site secundário  

**Servidores de sistema de sites:**  

-   Ponto de serviços Web do Catálogo de Aplicativos  

-   Ponto de sites da Web do Catálogo de Aplicativos  

-   Ponto de sincronização do Asset Intelligence  

-   Ponto de registro de certificado  

-   Ponto de distribuição  

     Os pontos de distribuição dão suporte a várias configurações diferentes que têm diferentes requisitos. Em alguns casos, essas configurações dão suporte à instalação não apenas em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções disponíveis para pontos de distribuição, consulte [Gerenciar o conteúdo e a infraestrutura de conteúdo](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

-   Ponto do Endpoint Protection  

-   Ponto de registro  

-   Ponto proxy do registro  

-   Ponto de status de fallback  

-   Ponto de gerenciamento

-   Ponto do Reporting Services  

-   Ponto de Conexão de Serviço  

-   Servidor de banco de dados do site  

     Os servidores de banco de dados do site não são compatíveis com um RODC (controlador de domínio somente leitura). Para obter mais informações, consulte [Você pode encontrar problemas ao instalar o SQL Server em um controlador de domínio](https://support.microsoft.com/help/2032911) na Base de Dados de Conhecimento Microsoft. Além disso, os servidores do site secundário não são compatíveis com qualquer controlador de domínio.  

-   SMS_Provider  

-   Ponto de atualização de software  

-   Ponto de migração de estado



## <a name="windows-storage-server-2016"></a>Windows Storage Server 2016

**Servidor do sistema de site**  

-   Ponto de distribuição  



## <a name="windows-server-2012-r2-x64-standard-and-datacenter"></a>Windows Server 2012 R2 (x64): Standard e Datacenter  

**Servidores do site:**  

-   Site de administração central  

-   Site primário  

-   Site secundário  

**Servidores de sistema de sites:**  

-   Ponto de serviços Web do Catálogo de Aplicativos  

-   Ponto de sites da Web do Catálogo de Aplicativos  

-   Ponto de sincronização do Asset Intelligence  

-   Ponto de registro de certificado  

-   Ponto de distribuição  

     Os pontos de distribuição dão suporte a várias configurações diferentes que têm diferentes requisitos. Em alguns casos, essas configurações dão suporte à instalação não apenas em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções disponíveis para pontos de distribuição, consulte [Gerenciar o conteúdo e a infraestrutura de conteúdo](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

-   Ponto do Endpoint Protection  

-   Ponto de registro  

-   Ponto proxy do registro  

-   Ponto de status de fallback  

-   Ponto de gerenciamento

-   Ponto do Reporting Services  

-   Ponto de Conexão de Serviço  

-   Servidor de banco de dados do site  

     Os servidores de banco de dados do site não são compatíveis com um RODC (controlador de domínio somente leitura). Para obter mais informações, consulte [Você pode encontrar problemas ao instalar o SQL Server em um controlador de domínio](https://support.microsoft.com/help/2032911) na Base de Dados de Conhecimento Microsoft. Além disso, os servidores do site secundário não são compatíveis com qualquer controlador de domínio.  

-   SMS_Provider  

-   Ponto de atualização de software  

-   Ponto de migração de estado  



## <a name="windows-server-2012-x64-standard-and-datacenter"></a>Windows Server 2012 (x64): Standard e Datacenter  

**Servidores do site:**  

-   Site de administração central  

-   Site primário  

-   Site secundário  

**Servidores de sistema de sites:**  

-   Ponto de serviços Web do Catálogo de Aplicativos  

-   Ponto de sites da Web do Catálogo de Aplicativos  

-   Ponto de sincronização do Asset Intelligence  

-   Ponto de registro de certificado  

-   Ponto de distribuição  

     Os pontos de distribuição dão suporte a várias configurações diferentes que têm diferentes requisitos. Em alguns casos, essas configurações dão suporte à instalação não apenas em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções disponíveis para pontos de distribuição, consulte [Gerenciar o conteúdo e a infraestrutura de conteúdo](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

-   Ponto do Endpoint Protection  

-   Ponto de registro  

-   Ponto proxy do registro  

-   Ponto de status de fallback  

-   Ponto de gerenciamento

-   Ponto do Reporting Services  

-   Ponto de Conexão de Serviço  

-   Servidor de banco de dados do site  

     Os servidores de banco de dados do site não são compatíveis com um RODC (controlador de domínio somente leitura). Para obter mais informações, consulte [Você pode encontrar problemas ao instalar o SQL Server em um controlador de domínio](https://support.microsoft.com/help/2032911) na Base de Dados de Conhecimento Microsoft. Além disso, os servidores do site secundário não são compatíveis com qualquer controlador de domínio.  

-   SMS_Provider  

-   Ponto de atualização de software  

-   Ponto de migração de estado  



## <a name="windows-server-2008-r2-with-sp1-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 R2 com SP1 (x64): Standard, Enterprise e Datacenter  

Agora, o Windows Server 2008 R2 está com suporte estendido e não mais com suporte base, conforme detalhado na [Ciclo de Vida do Suporte da Microsoft](https://support.microsoft.com/lifecycle). Para obter mais informações sobre o suporte futuro para esses sistemas operacionais como servidores do sistema de sites com o Configuration Manager, consulte [Sistemas operacionais de servidor preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

Os servidores do site ou a maioria das funções do sistema de sites não são compatíveis com esse sistema operacional. Ele ainda é compatível com a função do sistema de sites do ponto de distribuição, incluindo pontos de distribuição pull e para PXE e multicast.

**Servidores de sistema de sites:**  
-   Ponto de distribuição  

    -   Os pontos de distribuição deste sistema operacional são compatíveis com PXE e Multicast.  

    -   Os pontos de distribuição dão suporte a várias configurações diferentes que têm diferentes requisitos. Em alguns casos, essas configurações dão suporte à instalação não apenas em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções disponíveis para pontos de distribuição, consulte [Gerenciar o conteúdo e a infraestrutura de conteúdo](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  



## <a name="windows-server-2008-with-sp2-x86-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 com SP2 (x86, x64): Standard, Enterprise e Datacenter  

Agora, o Windows Server 2008 está com suporte estendido e não mais com suporte base, conforme detalhado no [Ciclo de Vida do Suporte da Microsoft](https://support.microsoft.com/lifecycle). Para obter mais informações sobre o suporte futuro para esses sistemas operacionais como servidores do sistema de sites com o Configuration Manager, consulte [Sistemas operacionais de servidor preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

Esse sistema operacional não é compatível com servidores do site ou funções do sistema de sites, exceto pelo ponto de distribuição e ponto de distribuição pull. Continue usando esse sistema operacional como um ponto de distribuição até que a reprovação desse suporte seja comunicada ou o período de suporte estendido desse sistema operacional expire. Para obter mais informações, consulte [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095) (A instalação do CB e do LTSB do System Center Configuration Manager falha no Windows Server 2008).

**Servidores de sistema de sites:**  
-   Ponto de distribuição  

    -   Os pontos de distribuição deste sistema operacional são compatíveis com PXE e Multicast.  

    -   Os pontos de distribuição deste sistema operacional não são compatíveis com a inicialização de rede de computadores cliente no modo EFI. Há suporte para computadores cliente com BIOS ou inicialização EFI no modo herdado.  

    -   Os pontos de distribuição dão suporte a várias configurações diferentes que têm diferentes requisitos. Em alguns casos, essas configurações dão suporte à instalação não apenas em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções disponíveis para pontos de distribuição, consulte [Gerenciar o conteúdo e a infraestrutura de conteúdo](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  



## <a name="windows-10-x86-x64-pro-and-enterprise"></a>Windows 10 (x86, x64): Pro e Enterprise  

**Servidores de sistema de sites:**  

-   Ponto de distribuição  

    -   Os pontos de distribuição deste sistema operacional não são compatíveis com PXE com os Serviços de Implantação do Windows padrão. A partir da versão 1806, o PXE pode ser habilitado em um ponto de distribuição deste sistema operacional com a opção de **Habilitar um respondente PXE sem os Serviços de Implantação do Windows**. Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

    -   Os pontos de distribuição desta versão de sistema operacional não são compatíveis com o Multicast.  

    -   Os pontos de distribuição dão suporte a várias configurações diferentes que têm diferentes requisitos. Em alguns casos, essas configurações dão suporte à instalação não apenas em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções disponíveis para pontos de distribuição, consulte [Gerenciar o conteúdo e a infraestrutura de conteúdo](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  



## <a name="windows-81-x86-x64-professional-and-enterprise"></a>Windows 8.1 (x86, x64): Professional e Enterprise  

**Servidores de sistema de sites:**  

-   Ponto de distribuição  

    -   Os pontos de distribuição deste sistema operacional não são compatíveis com PXE com os Serviços de Implantação do Windows padrão. A partir da versão 1806, o PXE pode ser habilitado em um ponto de distribuição deste sistema operacional com a opção de **Habilitar um respondente PXE sem os Serviços de Implantação do Windows**. Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

    -   Os pontos de distribuição desta versão de sistema operacional não são compatíveis com o Multicast.  

    -   Os pontos de distribuição dão suporte a várias configurações diferentes que têm diferentes requisitos. Em alguns casos, essas configurações dão suporte à instalação não apenas em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções disponíveis para pontos de distribuição, consulte [Gerenciar o conteúdo e a infraestrutura de conteúdo](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  



## <a name="windows-7-with-sp1-x86-x64-professional-enterprise-and-ultimate"></a>Windows 7 com SP1 (x86, x64): Professional, Enterprise e Ultimate  

**Servidores de sistema de sites:**  

-   Ponto de distribuição  

    -   Os pontos de distribuição deste sistema operacional não são compatíveis com PXE com os Serviços de Implantação do Windows padrão. A partir da versão 1806, o PXE pode ser habilitado em um ponto de distribuição deste sistema operacional com a opção de **Habilitar um respondente PXE sem os Serviços de Implantação do Windows**. Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

    -   Os pontos de distribuição desta versão de sistema operacional não são compatíveis com o Multicast.  

    -   Os pontos de distribuição dão suporte a várias configurações diferentes que têm diferentes requisitos. Em alguns casos, essas configurações dão suporte à instalação não apenas em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções disponíveis para pontos de distribuição, consulte [Gerenciar o conteúdo e a infraestrutura de conteúdo](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  



## <a name="the-server-core-installation-of-windows-server-version-1803"></a>A instalação server core do Windows Server, versão 1803
<!--503702-->A partir do Configuration Manager 1802,[o Windows Server, versão 1803](https://docs.microsoft.com/windows-server/get-started/get-started-with-1803) tem suporte para uso como um ponto de distribuição com as seguintes limitações:  

  -   Há suporte apenas para a versão de x64 bits.  

  -   Os pontos de distribuição deste sistema operacional não são compatíveis com PXE ou Multicast com os Serviços de Implantação do Windows padrão. A partir da versão 1806, o PXE pode ser habilitado em um ponto de distribuição deste sistema operacional com a opção de **Habilitar um respondente PXE sem os Serviços de Implantação do Windows**. Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="the-server-core-installation-of-windows-server-version-1709"></a>A instalação server core do Windows Server, versão 1709

A partir do Configuration Manager 1710, [o Windows Server, versão 1709](https://docs.microsoft.com/windows-server/get-started/get-started-with-1709) tem suporte para uso como um ponto de distribuição com as seguintes limitações:  

  -   Há suporte apenas para a versão de x64 bits.  

  -   Os pontos de distribuição deste sistema operacional não são compatíveis com PXE ou Multicast com os Serviços de Implantação do Windows padrão. A partir da versão 1806, o PXE pode ser habilitado em um ponto de distribuição deste sistema operacional com a opção de **Habilitar um respondente PXE sem os Serviços de Implantação do Windows**. Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="the-server-core-installation-of-windows-server-2016"></a>A instalação Server Core do Windows Server 2016

Com o pacote cumulativo de atualizações do hotfix da KB3186654, esse sistema operacional pode ser usado como um ponto de distribuição com as seguintes limitações:  

  -   Há suporte apenas para a versão de x64 bits.  

  -   Os pontos de distribuição deste sistema operacional não são compatíveis com PXE ou Multicast com os Serviços de Implantação do Windows padrão. A partir da versão 1806, o PXE pode ser habilitado em um ponto de distribuição deste sistema operacional com a opção de **Habilitar um respondente PXE sem os Serviços de Implantação do Windows**. Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="the-server-core-installation-of-windows-server-2012-r2"></a>A instalação Server Core do Windows Server 2012 R2  

Há suporte para a instalação do Server Core do Windows Server 2012 R2 para uso como um ponto de distribuição com as seguintes limitações:  

-   Há suporte apenas para a versão de x64 bits.

-   Os pontos de distribuição deste sistema operacional não são compatíveis com PXE ou Multicast com os Serviços de Implantação do Windows padrão. A partir da versão 1806, o PXE pode ser habilitado em um ponto de distribuição deste sistema operacional com a opção de **Habilitar um respondente PXE sem os Serviços de Implantação do Windows**. Para saber mais, confira [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="the-server-core-installation-of-windows-server-2012"></a>A instalação Server Core do Windows Server 2012  

Há suporte para a instalação do Server Core do Windows Server 2012 para uso como um ponto de distribuição com as seguintes limitações:  

-   Há suporte apenas para a versão de 64 bits.  

-   Os pontos de distribuição deste sistema operacional não são compatíveis com PXE ou Multicast com os Serviços de Implantação do Windows padrão. A partir da versão 1806, o PXE pode ser habilitado em um ponto de distribuição deste sistema operacional com a opção de **Habilitar um respondente PXE sem os Serviços de Implantação do Windows**. Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).
