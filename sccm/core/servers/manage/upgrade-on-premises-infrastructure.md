---
title: Atualizar infraestrutura local
titleSuffix: Configuration Manager
description: Saiba como atualizar a infraestrutura, como o SQL Server e o sistema operacional dos sistemas de sites.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7ff6d885ca635e15c62eddcdfa06abdc1a09cdf8
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456593"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-configuration-manager"></a>Atualizar infraestrutura local que dá suporte ao Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as informações descritas neste artigo para ajudá-lo a fazer upgrade da infraestrutura de servidor que executa o Configuration Manager.  

- Se você quiser *atualizar* de uma versão anterior para o Configuration Manager, branch atual, veja [Atualizar para o Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).  

- Se desejar *atualizar* a infraestrutura do Configuration Manager, Branch Atual, para uma nova versão, veja [Atualizações para o Configuration Manager](/sccm/core/servers/manage/updates).  



## <a name="BKMK_SupConfigUpgradeSiteSrv"></a> Atualizar o sistema operacional dos sistemas de sites  

O Configuration Manager dá suporte para a atualização in-loco do servidor do sistema operacional que hospeda um servidor do site e qualquer função do sistema de site nas seguintes situações:  

- Se o Configuration Manager ainda for compatível com o nível de service pack do Windows resultante, ele será compatível com atualização in-loco para um service pack posterior do Windows Server.  

- Atualização in-loco de:  

    - Windows Server 2016 para Windows Server 2019   

    - Windows Server 2012 R2 para Windows Server 2019   

    - Windows Server 2012 R2 para Windows Server 2016   

    - Windows Server 2012 para Windows Server 2016   

    - Windows Server 2012 para Windows Server 2012 R2   

    - Windows Server 2008 R2 para Windows Server 2012 R2   

Para atualizar um servidor, use os procedimentos de atualização fornecidos pelo sistema operacional para o qual você está atualizando. Confira os seguintes artigos:  

- [Centro de Atualização do Windows Server](http://aka.ms/upgradecenter)  

- [Opções de atualização e conversão para o Windows Server 2016](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths)  

- [Opções de Atualização para o Windows Server 2012 R2](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416\(v=ws.11))   


### <a name="bkmk_2016-2019"></a> Atualizar para o Windows Server 2016 ou 2019

Use as etapas nesta seção para qualquer um dos seguintes cenários de atualização:  

- Atualizar o Windows Server 2012 R2 ou o Windows Server 2016 para o Windows Server de 2019  

- Atualizar o Windows Server 2012 ou o Windows Server 2012 R2 para o Windows Server 2016  


#### <a name="before-upgrade"></a>Antes da atualização  
- (Windows Server 2012 ou Windows Server 2012 R2): remova o cliente do SCEP (System Center Endpoint Protection). O Windows Server agora tem o Windows Defender interno, que substitui o cliente do SCEP. A presença do cliente do SCEP pode impedir uma atualização para o Windows Server.  

- Remova a função WSUS do servidor se estiver instalada. Você pode manter o SUSDB e reconectá-lo uma vez que o WSUS for reinstalado.  

#### <a name="after-upgrade"></a>Após a atualização   
- Verifique se o Windows Defender está habilitado, configurado para o início automático e em execução.  

- Verifique se os seguintes serviços do Configuration Manager estão em execução:  

    - SMS_EXECUTIVE  

    - SMS_SITE_COMPONENT_MANAGER  

- Verifique se a **Ativação de Processos do Windows** e os serviços **WWW/W3svc** estão habilitados e configurados para início automático. O processo de atualização desabilita esses serviços, portanto, verifique se eles estão em execução para as seguintes funções de sistema de sites:  

    - Servidor do site  

    - Ponto de gerenciamento  

    - Ponto de serviços Web do Catálogo de Aplicativos  

    - Ponto de sites da Web do Catálogo de Aplicativos  

- Verifique se cada servidor que hospeda uma função de sistema de sites continua a atender a todos os [pré-requisitos](/sccm/core/plan-design/configs/site-and-site-system-prerequisites). Por exemplo, talvez seja necessário reinstalar o BITS, o WSUS ou definir configurações específicas para o IIS.  

- Após restaurar os pré-requisitos ausentes, inicie o servidor mais uma vez para verificar se os serviços iniciaram e estão operacionais.  

- Se você estiver atualizando o servidor do site primário, [execute uma redefinição de site](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_reset).  

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>Problema conhecido para consoles remotos do Configuration Manager   
Depois de atualizar o servidor do site ou uma instância do provedor de SMS, você não pode se conectar com o console do Configuration Manager. Para contornar esse problema, restaure manualmente as permissões para o grupo de **Administradores de SMS** no WMI. As permissões devem ser definidas no servidor do site e, em cada servidor remoto que hospeda uma instância do provedor de SMS:

1. Nos servidores aplicáveis, abra o MMC (Console de Gerenciamento Microsoft) e adicione o snap-in para **Controle WMI** e depois selecione **Computador local**.  

2. No MMC, abra as **Propriedades** de **Controle WMI (Local)** e selecione a guia **Segurança**.  

3. Expanda a árvore abaixo da Raiz, selecione o nó **SMS** e clique em **Segurança**.  Verifique se o grupo **Administradores de SMS** tem as seguintes permissões:  

    - Habilitar conta  

    - Habilitação remota  

4. Na guia **Segurança**, abaixo do nó **SMS**, selecione o nó **site_&lt;sitecode**> e escolha **Segurança**. Verifique se o grupo **Administradores de SMS** tem as seguintes permissões:  

    - Executar métodos  

    - Gravação do provedor  

    - Habilitar conta  

    - Habilitação remota  

5. Salve as permissões para restaurar o acesso do console do Configuration Manager.  


### <a name="bkmk_2012r2"></a> Atualizar para o Windows Server 2012 R2

Ao atualizar do Windows Server 2008 R2 ou do Windows Server 2012 para Windows Server 2012 R2, as seguintes condições se aplicam:

#### <a name="before-upgrade"></a>Antes da atualização  
- No Windows Server 2012: remova a função do WSUS do servidor se ela estiver instalada. Você pode manter o SUSDB e reconectá-lo uma vez que o WSUS for reinstalado.  

- No Windows Server 2008 R2: antes de atualizar para o Windows Server 2012 R2, é necessário desinstalar o WSUS 3.2 do servidor. Você pode manter o SUSDB e reconectá-lo uma vez que o WSUS for reinstalado. Para obter mais informações, veja [Visão geral do Windows Server Update Services](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345\(v=ws.11)#new-and-changed-functionality).  

#### <a name="after-upgrade"></a>Após a atualização  
- O processo de atualização desabilita os Serviços de Implantação do Windows. Verifique se esse serviço foi iniciado e está em execução para as seguintes funções de sistema de sites:  

    - Servidor do site  

    - Ponto de gerenciamento  

    - Ponto de serviços Web do Catálogo de Aplicativos  

    - Ponto de sites da Web do Catálogo de Aplicativos  

- Verifique se a **Ativação de Processos do Windows** e os serviços **WWW/W3svc** estão habilitados e configurados para início automático. O processo de atualização desabilita esses serviços, portanto, verifique se eles estão em execução para as seguintes funções de sistema de sites:  

    - Servidor do site  

    - Ponto de gerenciamento  

    - Ponto de serviços Web do Catálogo de Aplicativos  

    - Ponto de sites da Web do Catálogo de Aplicativos  

- Verifique se cada servidor que hospeda uma função de sistema de sites continua a atender a todos os [pré-requisitos](/sccm/core/plan-design/configs/site-and-site-system-prerequisites). Por exemplo, talvez seja necessário reinstalar o BITS, o WSUS ou definir configurações específicas para o IIS.  

    Após restaurar os pré-requisitos ausentes, inicie o servidor mais uma vez para verificar se os serviços iniciaram e estão operacionais.  


### <a name="unsupported-upgrade-scenarios"></a>Cenários de atualização sem suporte

Os seguintes cenários de atualização do Windows Server são consultados com frequência, mas não têm suporte do Configuration Manager:  

- Windows Server 2008 para Windows Server 2012 ou posterior  

- Windows Server 2008 R2 para Windows Server 2012  



##  <a name="BKMK_SupConfigUpgradeClient"></a> Atualizar o sistema operacional de clientes  

O Configuration Manager dá suporte a uma atualização in-loco do sistema operacional para clientes do Configuration Manager nas seguintes situações:  

- Se o Configuration Manager for compatível com o nível de service pack resultante, ele será compatível com atualização in-loco para um service pack posterior do Windows.  

- Atualização in-loco do Windows de uma versão com suporte para Windows 10. Para obter mais informações, confira [Atualizar o Windows para a versão mais recente](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version).  

- Atualizações de serviços de compilação a compilação do Windows 10. Para obter mais informações, consulte [Gerenciar o Windows como um serviço](/sccm/osd/deploy-use/manage-windows-as-a-service).  



##  <a name="BKMK_SupConfigUpgradeDBSrv"></a> Atualizar o SQL Server  

O Configuration Manager é compatível com uma atualização in-loco do SQL Server no servidor de banco de dados do site. 

Para obter informações sobre as versões do SQL Server compatíveis com o Configuration Manager, veja [Suporte para versões do SQL Server](/sccm/core/plan-design/configs/support-for-sql-server-versions).  


### <a name="upgrade-the-service-pack-version-of-sql-server"></a>Atualizar a versão do service pack do SQL Server    

Se o Configuration Manager ainda for compatível com o nível de service pack do SQL Server resultante, ele será compatível com a atualização in-loco do SQL Server para um service pack mais recente.

Quando você tiver mais de um site do Configuration Manager em uma hierarquia, cada site poderá executar uma versão diferente do service pack do SQL Server. Não há limitação à ordem na qual os sites atualizam a versão do service pack do SQL Server.


### <a name="upgrade-to-a-new-version-of-sql-server"></a>Atualizar para uma nova versão do SQL Server   

O Configuration Manager dá suporte à atualização in-loco do SQL Server para as seguintes versões:

- SQL Server 2017  

- SQL Server 2016  

- SQL Server 2014  

Ao atualizar a versão do SQL Server que hospeda o banco de dados do site, é necessário atualizar a versão do SQL Server que é usada nos sites na seguinte ordem:

1. Atualize o SQL Server no site de administração central primeiro  

2. Atualize os sites secundários antes de atualizar o site primário pai de um site secundário  

3. Atualize os sites primários pai por último. Esses sites incluem os sites primários filho que relatam para um site de administração central e os sites primários autônomos que são o site de nível superior de uma hierarquia.  


### <a name="sql-server-cardinality-estimation-level"></a>Nível de estimativa de cardinalidade do SQL Server   

Ao atualizar o banco de dados do site de uma versão anterior do SQL Server, o banco de dados manterá seu nível de estimativa de cardinalidade do SQL existente se ele estiver no mínimo permitido para a instância do SQL Server. Atualizar o SQL Server com um banco de dados em um nível de compatibilidade menor do que o nível permitido automaticamente define o banco de dados para o nível de compatibilidade mais baixo permitido pelo SQL Server.

A tabela a seguir identifica os níveis de compatibilidade recomendados para bancos de dados do site do Configuration Manager:

|Versão do SQL Server | Níveis de compatibilidade com suporte | Nível recomendado |
|----------------|--------------------|--------|
| SQL Server 2017 | 140, 130, 120, 110  | 140 |
| SQL Server 2016 | 130, 120, 110  | 130 |
| SQL Server 2014 | 120, 110      | 110 |

Para identificar o nível de compatibilidade estimativa de cardinalidade do SQL Server em uso para seu banco de dados do site, execute a seguinte consulta SQL no servidor de banco de dados do site:  
```SQL
SELECT name, compatibility_level FROM sys.databases
```

Para obter mais informações sobre níveis de compatibilidade CE do SQL e como configurá-los, consulte [Nível de compatibilidade de ALTER DATABASE (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017).


Para obter mais informações sobre a atualização do SQL Server, veja os seguintes artigos do SQL Server:  

- [Atualizar para o SQL Server 2017](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)  

- [Atualização para o SQL Server 2016](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2016)  

- [Atualização para o SQL Server 2014](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2014)  



### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Para atualizar o SQL Server no servidor de banco de dados do site  

1. Pare todos os serviços do Configuration Manager no site  

2. Atualize o SQL Server para uma versão com suporte  

3. Reinicie os serviços do Configuration Manager  

> [!NOTE]  
> Quando você altera a edição do SQL Server em uso no site de administração central de Standard para Datacenter ou Enterprise, a partição de banco de dados não muda. Essa partição de banco de dados limita o número de clientes com suporte da hierarquia.  
