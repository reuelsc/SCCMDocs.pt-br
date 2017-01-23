---
title: Servidores de sistema de sites com suporte | Microsoft Docs
description: "Saiba quais versões do Windows você pode usar para hospedar um site ou função de sistema de sites do System Center Configuration Manager."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
caps.latest.revision: 44
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bebbeebba76ab5cf0c517fcb00b7b6a516a08e3e
ms.openlocfilehash: 12fe730d924979eec2ef55ea80a1fa90b7b47464


---
# <a name="supported-operating-systems-for-system-center-configuration-manager-site-system-servers"></a>Sistemas operacionais com suporte para servidores do sistema de sites do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Este artigo detalha as versões do Windows você pode usar para hospedar um site ou função de sistema de sites do System Center Configuration Manager.


Use as informações neste tópico com as informações nos seguintes artigos:
-   [Hardware recomendado para o Configuration Manager](../../../core/plan-design/configs/recommended-hardware.md)
-   [Pré-requisitos de site e sistema de sites para o Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Números de tamanho e escala para o Configuration Manager](../../../core/plan-design/configs/size-and-scale-numbers.md)



## <a name="windows-server-2016-standard-and-datacenter"></a>Windows Server 2016: Standard e Datacenter
Há suporte para o Windows Server 2016 a partir do Configuration Manager versão 1606, com o pacote cumulativo de atualizações do hotfix do KB3186654 (ou a versão de linha de base do 1606, liberada em outubro de 2016).

**Servidores do site:**  

-   Site de administração central  

-   Site primário  

-   Site secundário  

**Servidores de sistema de sites:**  

-   Ponto de serviços Web do Catálogo de Aplicativos  

-   Ponto de sites da Web do catálogo de aplicativos  

-   Ponto de sincronização do Asset Intelligence  

-   Ponto de registro de certificado  

-   Ponto de distribuição  

     Os pontos de distribuição dão suporte a várias configurações diferentes que têm diferentes requisitos. Em alguns casos, essas configurações dão suporte à instalação não apenas em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções disponíveis para pontos de distribuição, consulte [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Gerenciar o conteúdo e a infraestrutura de conteúdo do System Center Configuration Manager).  

-   Ponto do Endpoint Protection  

-   Ponto de registro  

-   Ponto proxy do registro  

-   Ponto de status de fallback  

-   Ponto de gerenciamento

-   Ponto do Reporting Services  

-   Ponto de conexão de serviço  

-   Servidor de banco de dados do site  

     Não há suporte para servidores de banco de dados de sites em um RODC (controlador de domínio somente leitura). Para obter mais informações, consulte [Você pode encontrar problemas ao instalar o SQL Server em um controlador de domínio](http://go.microsoft.com/fwlink/p/?LinkId=264856) na Base de Dados de Conhecimento Microsoft. Além disso, os servidores do site secundário não têm suporte em qualquer controlador de domínio.  

-   SMS_Provider  

-   Ponto de atualização de software  

-   Ponto de migração de estado

## <a name="windows-server-2012-r2-x64-standard-and-datacenter"></a>Windows Server 2012 R2 (x64): Standard e Datacenter  
**Servidores do site:**  

-   Site de administração central  

-   Site primário  

-   Site secundário  

**Servidores de sistema de sites:**  

-   Ponto de serviços Web do Catálogo de Aplicativos  

-   Ponto de sites da Web do catálogo de aplicativos  

-   Ponto de sincronização do Asset Intelligence  

-   Ponto de registro de certificado  

-   Ponto de distribuição  

     Os pontos de distribuição dão suporte a várias configurações diferentes que têm diferentes requisitos. Em alguns casos, essas configurações dão suporte à instalação não apenas em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções disponíveis para pontos de distribuição, consulte [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Gerenciar o conteúdo e a infraestrutura de conteúdo do System Center Configuration Manager).  

-   Ponto do Endpoint Protection  

-   Ponto de registro  

-   Ponto proxy do registro  

-   Ponto de status de fallback  

-   Ponto de gerenciamento

-   Ponto do Reporting Services  

-   Ponto de conexão de serviço  

-   Servidor de banco de dados do site  

     Não há suporte para servidores de banco de dados de sites em um RODC (controlador de domínio somente leitura). Para obter mais informações, consulte [Você pode encontrar problemas ao instalar o SQL Server em um controlador de domínio](http://go.microsoft.com/fwlink/p/?LinkId=264856) na Base de Dados de Conhecimento Microsoft. Além disso, os servidores do site secundário não têm suporte em qualquer controlador de domínio.  

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

-   Ponto de sites da Web do catálogo de aplicativos  

-   Ponto de sincronização do Asset Intelligence  

-   Ponto de registro de certificado  

-   Ponto de distribuição  

     Os pontos de distribuição dão suporte a várias configurações diferentes que têm diferentes requisitos. Em alguns casos, essas configurações dão suporte à instalação não apenas em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções disponíveis para pontos de distribuição, consulte [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Gerenciar o conteúdo e a infraestrutura de conteúdo do System Center Configuration Manager).  

-   Ponto do Endpoint Protection  

-   Ponto de registro  

-   Ponto proxy do registro  

-   Ponto de status de fallback  

-   Ponto de gerenciamento

-   Ponto do Reporting Services  

-   Ponto de conexão de serviço  

-   Servidor de banco de dados do site  

     Não há suporte para servidores de banco de dados de sites em um RODC (controlador de domínio somente leitura). Para obter mais informações, consulte [Você pode encontrar problemas ao instalar o SQL Server em um controlador de domínio](http://go.microsoft.com/fwlink/p/?LinkId=264856) na Base de Dados de Conhecimento Microsoft. Além disso, os servidores do site secundário não têm suporte em qualquer controlador de domínio.  

-   SMS_Provider  

-   Ponto de atualização de software  

-   Ponto de migração de estado  

## <a name="windows-server-2008-r2-with-sp1-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 R2 com SP1 (x64): Standard, Enterprise e Datacenter  
 Agora o Windows Server 2008 R2 está com suporte estendido e não mais com suporte base, conforme detalhado na [Política de Ciclo de Vida da Microsoft](https://support.microsoft.com/lifecycle). Para obter mais informações sobre o suporte futuro para esses sistemas operacionais como servidores do sistema de sites com o Configuration Manager, consulte [Recursos removidos e preteridos do System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

**Servidores do site:**  

-   Site de administração central  

-   Site primário  

-   Site secundário  

**Servidores de sistema de sites:**  

-   Ponto de serviços Web do Catálogo de Aplicativos  

-   Ponto de sites da Web do catálogo de aplicativos  

-   Ponto de sincronização do Asset Intelligence  

-   Ponto de registro de certificado  

-   Ponto de distribuição  

     Os pontos de distribuição dão suporte a várias configurações diferentes que têm diferentes requisitos. Em alguns casos, essas configurações dão suporte à instalação não apenas em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções disponíveis para pontos de distribuição, consulte [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Gerenciar o conteúdo e a infraestrutura de conteúdo do System Center Configuration Manager).  

-   Ponto do Endpoint Protection  

-   Ponto de registro  

-   Ponto proxy do registro  

-   Ponto de status de fallback  

-   Ponto de gerenciamento

-   Ponto do Reporting Services  

-   Ponto de conexão de serviço  

-   Servidor de banco de dados do site  

     Não há suporte para servidores de banco de dados de sites em um RODC (controlador de domínio somente leitura). Para obter mais informações, consulte [Você pode encontrar problemas ao instalar o SQL Server em um controlador de domínio](http://go.microsoft.com/fwlink/p/?LinkId=264856) na Base de Dados de Conhecimento Microsoft. Além disso, os servidores do site secundário não têm suporte em qualquer controlador de domínio.  

-   SMS_Provider  

-   Ponto de atualização de software  

-   Ponto de migração de estado  

## <a name="windows-server-2008-with-sp2-x86-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 com SP2 (x86, x64): Standard, Enterprise e Datacenter  
 Agora o Windows Server 2008 está com suporte estendido e não mais com suporte base, conforme detalhado na [Política de Ciclo de Vida da Microsoft](https://support.microsoft.com/lifecycle). Para obter mais informações sobre o suporte futuro para esses sistemas operacionais como servidores do sistema de sites com o Configuration Manager, consulte [Recursos removidos e preteridos do System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

**Servidores do site:**  

-   Site de administração central  

-   Site primário  

-   Site secundário  

**Servidores de sistema de sites:**  

-   Ponto de serviços Web do Catálogo de Aplicativos  

-   Ponto de sites da Web do catálogo de aplicativos  

-   Ponto de sincronização do Asset Intelligence  

-   Ponto de registro de certificado  

-   Ponto de distribuição  

    -   Os pontos de distribuição neste sistema operacional não dão suporte a Multicast.  

    -   Há suporte para PXE para os pontos de distribuição neste sistema operacional, mas não para a inicialização de rede de computadores cliente no modo EFI. Há suporte para computadores cliente com BIOS ou inicialização EFI no modo herdado.  

    -   Os pontos de distribuição dão suporte a várias configurações diferentes que têm diferentes requisitos. Em alguns casos, essas configurações dão suporte à instalação não apenas em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções disponíveis para pontos de distribuição, consulte [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Gerenciar o conteúdo e a infraestrutura de conteúdo do System Center Configuration Manager).  

-   Ponto do Endpoint Protection  

-   Ponto de registro  

-   Ponto proxy do registro  

-   Ponto de status de fallback  

-   Ponto de gerenciamento

-   Ponto do Reporting Services  

-   Ponto de conexão de serviço  

-   Servidor de banco de dados do site  

     Não há suporte para servidores de banco de dados de sites em um RODC (controlador de domínio somente leitura). Para obter mais informações, consulte [Você pode encontrar problemas ao instalar o SQL Server em um controlador de domínio](http://go.microsoft.com/fwlink/p/?LinkId=264856) na Base de Dados de Conhecimento Microsoft. Além disso, os servidores do site secundário não têm suporte em qualquer controlador de domínio.  

-   SMS_Provider  

-   Ponto de atualização de software  

-   Ponto de migração de estado  

## <a name="windows-10-x86-x64-pro-and-enterprise"></a>Windows 10 (x86, x64): Pro e Enterprise  
**Servidores de sistema de sites:**  

-   Ponto de distribuição  

    -   Não há suporte do PXE para pontos de distribuição neste sistema operacional.  

    -   Os pontos de distribuição nesta versão de sistema operacional não dão suporte a Multicast.  

    -   Os pontos de distribuição dão suporte a várias configurações diferentes que têm diferentes requisitos. Em alguns casos, essas configurações dão suporte à instalação não apenas em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções disponíveis para pontos de distribuição, consulte [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Gerenciar o conteúdo e a infraestrutura de conteúdo do System Center Configuration Manager).  

## <a name="windows-81-x86-x64-professional-and-enterprise"></a>Windows 8.1 (x86, x64): Professional e Enterprise  
**Servidores de sistema de sites:**  

-   Ponto de distribuição  

    -   Não há suporte do PXE para pontos de distribuição neste sistema operacional.  

    -   Os pontos de distribuição nesta versão de sistema operacional não dão suporte a Multicast.  

    -   Os pontos de distribuição dão suporte a várias configurações diferentes que têm diferentes requisitos. Em alguns casos, essas configurações dão suporte à instalação não apenas em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções disponíveis para pontos de distribuição, consulte [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Gerenciar o conteúdo e a infraestrutura de conteúdo do System Center Configuration Manager).  

## <a name="windows-8-x86-x64-professional-and-enterprise"></a>Windows 8 (x86, x64): Professional e Enterprise
**Servidores de sistema de sites:**  

-   Ponto de distribuição  

    -   Não há suporte do PXE para pontos de distribuição neste sistema operacional.  

    -   Os pontos de distribuição nesta versão de sistema operacional não dão suporte a Multicast.  

    -   Os pontos de distribuição dão suporte a várias configurações diferentes que têm diferentes requisitos. Em alguns casos, essas configurações dão suporte à instalação não apenas em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções disponíveis para pontos de distribuição, consulte [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Gerenciar o conteúdo e a infraestrutura de conteúdo do System Center Configuration Manager).  

## <a name="windows-7-with-sp1-x86-x64-professional-enterprise-and-ultimate"></a>Windows 7 com SP1 (x86, x64): Professional, Enterprise e Ultimate  
**Servidores de sistema de sites:**  

-   Ponto de distribuição  

    -   Não há suporte do PXE para pontos de distribuição neste sistema operacional.  

    -   Os pontos de distribuição nesta versão de sistema operacional não dão suporte a Multicast.  

    -   Os pontos de distribuição dão suporte a várias configurações diferentes que têm diferentes requisitos. Em alguns casos, essas configurações dão suporte à instalação não apenas em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções disponíveis para pontos de distribuição, consulte [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Gerenciar o conteúdo e a infraestrutura de conteúdo do System Center Configuration Manager).  

## <a name="the-server-core-installation-of-windows-server-2012"></a>A instalação Server Core do Windows Server 2012  
 Além dos sistemas operacionais anteriores listados, há suporte para a instalação Server Core do Windows Server 2012 para uso como um ponto de distribuição com as seguintes limitações:  

-   Há suporte apenas para a versão de 64 bits.  

-   Os pontos de distribuição nesse sistema operacional não dão suporte a PXE nem a Multicast.

## <a name="the-server-core-installation-of-windows-server-2012-r2"></a>A instalação Server Core do Windows Server 2012 R2  
 Além dos sistemas operacionais anteriores listados, há suporte para a instalação Server Core do Windows Server 2012 R2 para uso como um ponto de distribuição com as seguintes limitações:  

-   Há suporte apenas para a versão de x64 bits.

-   Os pontos de distribuição nesse sistema operacional não dão suporte a PXE nem a Multicast.  



<!--HONumber=Jan17_HO1-->


