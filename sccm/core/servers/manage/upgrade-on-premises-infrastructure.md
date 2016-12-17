---
title: Atualizar a infraestrutura local | System Center Configuration Manager
description: Saiba como atualizar a infraestrutura, como o SQL Server e o sistema operacional do site dos sistemas de sites.
ms.custom: na
ms.date: 10/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c8115fba0722fc902e60ce201d8a9914036c1245
ms.openlocfilehash: 1239bf81991bb233a9640606bb47f598a70d5e50


---
# <a name="upgrade-on-premises-infrastructure-that-supports-system-center-configuration-manager"></a>Atualizar infraestrutura local que dá suporte ao System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as informações a seguir para ajudá-lo a atualizar sua infraestrutura que executa o System Center Configuration Manager.  

##  <a name="a-namebkmksupconfigupgradesitesrva-upgrade-site-operating-system-of-site-systems"></a><a name="BKMK_SupConfigUpgradeSiteSrv"></a> Atualizar sistema operacional do site dos sistemas de sites  
 O Configuration Manager dá suporte à atualização in-loco do sistema operacional dos servidores que hospedam um servidor do site e dos servidores remotos que hospedam qualquer função do sistema de site, nas seguintes situações:  

-   Atualização in-loco para um service pack superior do Windows Server, se o nível do service pack do Windows resultante tiver suporte do Configuration Manager.  
-   Atualização in-loco de:
    - Windows Server 2012 R2 para Windows Server 2016 ([Ver detalhes adicionais](#upgrade-windows-server-2012-r2-to-2016))
    - Windows Server 2012 para Windows Server 2012 R2 ([Ver detalhes adicionais](#upgrade-windows-server-2012-to-windows-server-2012-r2))
    - Quando você usa o Configuration Manager versão 1602 ou posterior, também há suporte para atualizar o Windows Server 2008 R2 para o Windows Server 2012 R2 ([Ver detalhes adicionais](#upgrade-windows-server-2008-r2-to-windows-server-2012-r2))

    > [!WARNING]  
    >  Antes de atualizar para o Windows Server 2012 R2, **você deve desinstalar o WSUS 3.2** do servidor.  
    >   
    >  Para obter informações sobre esta etapa crítica, confira a seção Funcionalidade nova e alterada em [Visão geral do Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx) na documentação do Windows Server.  

Para atualizar um servidor, use os procedimentos de atualização fornecidos pelo sistema operacional para o qual você está atualizando.  Veja o seguinte:
  -  [Opções de atualização para o Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) na documentação do Windows Server.  
  - [Opções de atualização e conversão para o Windows Server 2016](https://technet.microsoft.com/windows-server-docs/get-started/supported-upgrade-paths) na documentação do Windows Server.

### <a name="upgrade-windows-server-2012-r2-to-2016"></a>Atualizar o Windows Server 2012 R2 para o 2016  
Este cenário de atualização do sistema operacional tem as seguintes condições:

**Antes da atualização:**  
-   Remova o cliente do SCEP (System Center Endpoint Protection). O Windows Server 2016 tem o Windows Defender interno, que substitui o cliente do SCEP. A presença do cliente do SCEP pode impedir a atualização para o Windows Server 2016.

**Após a atualização:**
-   Certifique-se de que o Windows Defender esteja habilitado, configurado para o início automático e em execução.
-   Certifique-se de que os seguintes serviços do Configuration Manager estejam em execução:
  -     SMS_EXECUTIVE
  -     SMS_SITE_COMPONENT_MANAGER


-   Verifique se os serviços de **Ativação de Processos do Windows** e **WWW/W3svc** estão habilitados, configurados para o início automático e em execução para as seguintes funções de sistema de site (esses serviços são desabilitados durante a atualização):
  -     Servidor do site
  -     Ponto de gerenciamento
  -     Ponto de serviços Web do Catálogo de Aplicativos
  -     Ponto de sites da Web do Catálogo de Aplicativos


-   Certifique-se de que cada servidor que hospeda uma função de sistema de sites continue atendendo a todos os [pré-requisitos das funções de sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) que são executadas no servidor. Por exemplo, talvez seja necessário reinstalar o BITS, o WSUS ou definir configurações específicas para o IIS.

  Após restaurar os pré-requisitos ausentes, reinicie o servidor mais uma vez para garantir que os serviços estejam iniciados e operacionais.

**Problema conhecido para consoles remotos do Configuration Manager:**  
Após atualizar o servidor do site ou um servidor que hospeda uma instância de SMS_Provider para o Windows Server 2016, talvez os usuários administrativos não possam conectar um console do Configuration Manager ao site. Para contornar esse problema, você precisa restaurar manualmente as permissões para o grupo de Administradores de SMS no WMI. As permissões devem ser definidas no servidor do site e, em cada servidor remoto que hospeda uma instância do provedor de SMS:

1. Nos servidores aplicáveis, abra o MMC (Console de Gerenciamento Microsoft) e adicione o snap-in para **Controle WMI** e selecione **Computador local**.
2. No MMC, abra as **Propriedades** de **Controle WMI (Local)** e selecione a guia **Segurança**.
3. Expanda a árvore abaixo da Raiz, selecione o nó **SMS** e clique em **Segurança**.  Verifique se o grupo **Administradores de SMS** tem as seguintes permissões:
  -     Habilitar conta
  -     Habilitação remota
4. Em seguida, na guia **Segurança**, abaixo do nó SMS, selecione o nó **site_<sitecode>** e clique em **Segurança**. Verifique se o grupo **Administradores de SMS** tem as seguintes permissões:
  -   Executar métodos
  -   Gravação do provedor
  -   Habilitar conta
  -   Habilitação remota
5. Salve as permissões para restaurar o acesso do console do Configuration Manager.

### <a name="windows-server-2012-to-windows-server-2012-r2"></a>Windows Server 2012 para Windows Server 2012 R2

**Antes da atualização:**
-  Diferente dos outros cenários com suporte, este cenário não requer considerações adicionais antes da atualização.

**Após a atualização:**
  - Certifique-se de que o Serviço de Implantação do Windows esteja iniciado e em execução para as seguintes funções de sistema de site (o serviço é interrompido durante a atualização):
    - Servidor do site
    - Ponto de gerenciamento
    - Ponto de serviços Web do Catálogo de Aplicativos
    - Ponto de sites da Web do Catálogo de Aplicativos


  -     Verifique se os serviços de **Ativação de Processos do Windows** e **WWW/W3svc** estão habilitados, configurados para o início automático e em execução para as seguintes funções de sistema de site (esses serviços são desabilitados durante a atualização):
    -   Servidor do site
    -   Ponto de gerenciamento
    -   Ponto de serviços Web do Catálogo de Aplicativos
    -   Ponto de sites da Web do Catálogo de Aplicativos


  -     Certifique-se de que cada servidor que hospeda uma função de sistema de sites continue atendendo a todos os [pré-requisitos das funções de sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) que são executadas no servidor. Por exemplo, talvez seja necessário reinstalar o BITS, o WSUS ou definir configurações específicas para o IIS.

  Após restaurar os pré-requisitos ausentes, reinicie o servidor mais uma vez para garantir que os serviços estejam iniciados e operacionais.

### <a name="upgrade-windows-server-2008-r2-to-windows-server-2012-r2"></a>Atualizar o Windows Server 2008 R2 para o Windows Server 2012 R2
Este cenário de atualização do sistema operacional tem as seguintes condições:  

**Antes da atualização:**
-   Desinstale o WSUS 3.2.  
    Antes de atualizar o sistema operacional de um servidor para o Windows Server 2012 R2, você precisa desinstalar o WSUS 3.2 do servidor. Para obter informações sobre esta etapa crítica, confira a seção "Funcionalidade nova e alterada" em "Visão geral do Windows Server Update Services" na documentação do Windows Server.

**Após a atualização:**
  - Certifique-se de que o Serviço de Implantação do Windows esteja iniciado e em execução para as seguintes funções de sistema de site (o serviço é interrompido durante a atualização):
    - Servidor do site
    - Ponto de gerenciamento
    - Ponto de serviços Web do Catálogo de Aplicativos
    - Ponto de sites da Web do Catálogo de Aplicativos


  -     Verifique se os serviços de **Ativação de Processos do Windows** e **WWW/W3svc** estão habilitados, configurados para o início automático e em execução para as seguintes funções de sistema de site (esses serviços são desabilitados durante a atualização):
    -   Servidor do site
    -   Ponto de gerenciamento
    -   Ponto de serviços Web do Catálogo de Aplicativos
    -   Ponto de sites da Web do Catálogo de Aplicativos


  -     Certifique-se de que cada servidor que hospeda uma função de sistema de sites continue atendendo a todos os [pré-requisitos das funções de sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) que são executadas no servidor. Por exemplo, talvez seja necessário reinstalar o BITS, o WSUS ou definir configurações específicas para o IIS.

  Após restaurar os pré-requisitos ausentes, reinicie o servidor mais uma vez para garantir que os serviços estejam iniciados e operacionais.


### <a name="unsupported-upgrade-scenarios"></a>Cenários de atualização sem suporte
Os seguintes cenários de atualização do Windows Server são consultados com frequência, mas não têm suporte do Configuration Manager:  

-   Windows Server 2008 para Windows Server 2012 ou posterior  
-   Windows Server 2008 R2 para Windows Server 2012



##  <a name="a-namebkmksupconfigupgradeclienta-upgrade-the-operating-system-of-configuration-manager-clients"></a><a name="BKMK_SupConfigUpgradeClient"></a> Atualizar o sistema operacional de clientes do Configuration Manager  
 O Configuration Manager dá suporte a uma atualização in-loco do sistema operacional para clientes do Configuration Manager nas seguintes situações:  

-   Atualização in-loco para um service pack superior do Windows, se o nível do service pack resultante tiver suporte do Configuration Manager.  

-   Atualização in-loco do Windows de uma versão com suporte para Windows 10. Para obter mais informações, consulte [Atualizar o Windows para a versão mais recente com o System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   Atualizações de serviços de compilação a compilação do Windows 10.  Consulte [Gerenciar o Windows como um serviço usando o System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md) para obter mais informações.  

##  <a name="a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server"></a><a name="BKMK_SupConfigUpgradeDBSrv"></a> Atualizar o SQL Server no servidor de banco de dados do site  
  O Configuration Manager dá suporte a uma atualização in-loco do SQL Server de uma versão com suporte do SQL no servidor de banco de dados do site. Veja a seguir os detalhes sobre os cenários de atualização do SQL Server com suporte do Configuration Manager e os requisitos para cada cenário.

 Para obter informações sobre quais versões do SQL Server têm suporte do Configuration Manager, consulte [Suporte para versões do SQL Server para o System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

 **Atualizar a versão do service pack do SQL Server:**    
 O Configuration Manager dará suporte à atualização in-loco do SQL Server para um service pack superior se o nível do service pack resultante do SQL Server tiver suporte do Configuration Manager.

 Quando você tem vários sites do Configuration Manager em uma hierarquia, cada site pode executar uma versão diferente do service pack do SQL Server, e não há limitação quanto à ordem em que os sites são atualizados para a versão do service pack do SQL Server que é usada para o banco de dados do site.

 **Atualizar para uma nova versão do SQL Server:**   
 O Configuration Manager dá suporte à atualização in-loco do SQL Server para as seguintes versões:

 - SQL Server 2012  
 - SQL Server 2014  
 - SQL Server 2016  

Ao atualizar a versão do SQL Server que hospeda o banco de dados do site, é necessário atualizar a versão do SQL Server que é usada nos sites na seguinte ordem:

 1. Atualize o SQL Server no site de administração central primeiro.
 2. Atualize os sites secundários antes de atualizar o site primário pai de um site secundário.
 3. Atualize os sites primários pai por último. Isso inclui os sites primários filho que relatam para um site de administração central e os sites primários autônomos que são o site de nível superior de uma hierarquia.



**Para obter mais informações sobre o SQL Server, consulte a documentação sobre o SQL Server no TechNet:**  
-   [Atualização para o SQL Server 2014](http://technet.microsoft.com/library/ms143393\(v=sql.120))  
-   [Atualização para o SQL Server 2012](http://technet.microsoft.com/library/ms143393\(v=sql.110))
-   [Atualização para o SQL Server 2016](https://technet.microsoft.com/library/bb677622(v=sql.130))



### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Para atualizar o SQL Server no servidor de banco de dados do site  

1.  Pare todos os serviços do Configuration Manager no site.  
2.  Atualize o SQL Server para uma versão com suporte.  
3.  Reinicie os serviços do Configuration Manager.  

> [!NOTE]  
>  Ao alterar a edição do SQL Server em uso no site de administração central de uma Standard Edition para uma Datacenter ou Enterprise Edition, a partição do banco de dados que limita o número de clientes com suporte da hierarquia não é alterada.



<!--HONumber=Nov16_HO1-->


