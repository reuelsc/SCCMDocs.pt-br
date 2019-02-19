---
title: Pré-requisitos para atualizações de software
titleSuffix: Configuration Manager
description: Saiba mais sobre os pré-requisitos para atualizações de software no System Center Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 02/02/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.collection: M365-identity-device-management
ms.openlocfilehash: 395c22b3fb7652a1da4652d1bf259bffb601c109
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133554"
---
# <a name="prerequisites-for-software-updates-in-system-center-configuration-manager"></a>Pré-requisitos para atualizações de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo lista os pré-requisitos para atualizações de software no System Center Configuration Manager. Para cada um deles, as dependências externas e internas são listadas em tabelas separadas.  

## <a name="software-update-dependencies-that-are-external-to-configuration-manager"></a>Dependências de atualizações de software externas ao Configuration Manager  
 As seções a seguir listam as dependências externas para atualizações de software.  

### <a name="internet-information-services"></a>Serviços de informações da Internet  
 O IIS (Serviços de Informações da Internet) deve ser instalado nos servidores de sistema de sites para executar o ponto de atualização de software, o ponto de gerenciamento e o ponto de distribuição. Para mais informações, consulte [Pré-requisitos para funções de sistema de sites](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### <a name="windows-server-update-services"></a>Windows Server Update Services  
 O WSUS (Windows Server Update Services) é necessário para sincronização de atualizações de software e para o exame de aplicabilidade de atualizações de software nos clientes. O servidor WSUS precisa ser instalado antes de se criar a função do ponto de atualização de software. Há suporte para as seguintes versões do WSUS em um ponto de atualização de software:  

-   WSUS 10.0.14393 (função no Windows Server 2016)
-   WSUS 10.0.17763 (função no Windows Server 2019) (exige o Configuration Manager 1810 ou posterior)
-   WSUS 6.2 e 6.3 (função no Windows Server 2012 e Windows Server 2012 R2)

>[!NOTE]
>-   Começando com a versão 1702, o Windows Server 2008 R2 não é compatível com a função de ponto de atualização de software. Para obter mais informações, confira [Sistemas operacionais com suporte para servidores do sistema de sites](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers#bkmk_2008r2sp1).  

Quando você tiver diversos pontos de atualização de software em um site, verifique se todos estão executando a mesma versão do WSUS.  

> [!WARNING]  
>  A classificação de atualizações de software **Upgrades** só é compatível a partir do WSUS 4.0. Antes de sincronizar essa nova classificação e poder avaliar computadores com Windows 10 em um plano de manutenção do Windows 10, é essencial que você instale o [hotfix 3095113](https://support.microsoft.com/kb/3095113) para o WSUS nos pontos de atualização de software e servidores do site. Com esse hotfix, o WSUS em um servidor baseado no Windows Server 2012 ou no Windows Server 2012 R2 pode sincronizar e distribuir upgrades de recurso para o Windows 10. Para obter mais informações, consulte [Gerenciar o Windows como um serviço](../../osd/deploy-use/manage-windows-as-a-service.md).  
>   
>  Se você sincronizar atualizações de software com a classificação **Atualizações** antes de instalar o [hotfix 3095113](https://support.microsoft.com/kb/3095113), consulte [Para se recuperar da sincronização da classificação Atualizações antes de instalar o KB 3095113](#BKMK_RecoverUpgrades).  

### <a name="wsus-administration-console"></a>Console de Administração do WSUS  
 O Console de Administração do WSUS é necessário no servidor de site do Configuration Manager quando o ponto de atualização de software está em um servidor de sistema de sites remoto e o WSUS ainda não está instalado no servidor de site.  

> [!IMPORTANT]  
> A versão do WSUS no servidor de site deve ser a mesma versão do WSUS em execução nos pontos de atualização de software.
>
> Não use o Console de Administração do WSUS para definir as configurações do WSUS. O Configuration Manager se conecta à instância do WSUS executada no ponto de atualização de software e define as configurações apropriadas.  



### <a name="windows-update-agent"></a>Windows Update Agent  
 O cliente do WUA (Windows Update Agent) é exigido em clientes para que eles possam se conectar ao servidor do WSUS. O WUA recupera a lista de atualizações de software que devem ser verificados quanto à conformidade.  

 Quando você instala o Configuration Manager, a última versão do WUA é baixada. Depois, quando você instala o cliente do Configuration Manager, o WUA é atualizado, se necessário. No entanto, se a instalação falhar, será necessário usar um método diferente para fazer upgrade do WUA.  

## <a name="software-update-dependencies-that-are-internal-to-configuration-manager"></a>Dependências de atualizações de software internas ao Configuration Manager  
 As seções a seguir listam as dependências internas para atualizações de software no Configuration Manager.  

### <a name="management-points"></a>Pontos de gerenciamento  
 Os pontos de gerenciamento transferem informações entre os computadores cliente e o site do Configuration Manager. Os pontos de gerenciamento são necessários para atualizações de software.  

### <a name="software-update-points"></a>Pontos de atualização de software  
 Você deve instalar um ponto de atualização de software no servidor WSUS para poder implantar atualizações de software no Configuration Manager. Para mais informações, consulte [Instalar e configurar um ponto de atualização de software](../get-started/install-a-software-update-point.md).

### <a name="distribution-points"></a>Pontos de distribuição  
 Pontos de distribuição são necessários para armazenar o conteúdo de atualizações de software. Para obter mais informações sobre como instalar pontos de distribuição e gerenciar conteúdo, consulte [Gerenciar conteúdo e infraestrutura de conteúdo](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="client-settings-for-software-updates"></a>Configurações do cliente para atualizações de software  
 Por padrão, as atualizações de software estão habilitadas para clientes. Entretanto, existem outras configurações disponíveis que controlam como e quando os clientes avaliam a conformidade das atualizações de software e como elas são instaladas.  

 Para obter mais informações, consulte os seguintes artigos:  

-   [Configurações do cliente para atualizações de software](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

-   [Configurações do cliente de atualizações de software](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-points"></a>Pontos do Reporting Services  
 A função do sistema de site do ponto do Reporting Services pode exibir relatórios de atualizações de software. Essa função é opcional, mas recomendada. Para obter mais informações sobre como criar um ponto do Reporting Services, consulte [Configurando relatórios](../../core/servers/manage/configuring-reporting.md).  

##  <a name="BKMK_RecoverUpgrades"></a> Recuperar-se da sincronização da categoria Atualizações antes de instalar o KB 3095113  
 Você deve instalar o [hotfix 3095113](https://support.microsoft.com/kb/3095113) para o WSUS nos pontos de atualização de software e servidores do site antes de sincronizar a classificação **Atualizações** . Se o hotfix não estiver instalado quando a classificação **Atualizações** for habilitada, o WSUS verá o upgrade de recurso do Windows 10 build 1511 mesmo se não puder baixar e implantar corretamente os pacotes associados. 
 
 Se você sincronizar os upgrades antes de instalar o [hotfix 3095113](https://support.microsoft.com/kb/3095113), o SUSDB (banco de dados do WSUS) será populado por dados inúteis. Esses dados precisam ser apagados antes de que os upgrades possam ser implantados corretamente. Use o procedimento a seguir para se recuperar desse problema.  

#### <a name="to-recover-from-synchronizing-the-upgrades-classification-before-you-install-kb-3095113"></a>Para se recuperar da sincronização da classificação Atualizações antes de instalar o KB 3095113  

1.  Exclua atualizações de software com a classificação **Upgrades**. É possível usar um script do PowerShell semelhante ao exemplo a seguir:  

    ```  
    $Server = Get-WSUSServer  
    $Config = $Server.GetConfiguration()  
    $Update10563 = “df4e45a3-946d-4467-b3fd-8621174bb666”  
    $UpdateGUID = New-Object Guid($Update10563)  
    $Server.DeleteUpdate($UpdateGUID)  
    ```  

    > [!IMPORTANT]  
    >  Você deve executar o script em todos os pontos de atualização de software na hierarquia do Configuration Manager antes de ir para a próxima etapa.  

     Para excluir em massa atualizações de software com a classificação **Upgrades**, modifique o script do PowerShell para ler vários GUIDs de um arquivo de texto.  

2.  Desmarque a classificação **Upgrades** nas propriedades de componente do Ponto de Atualização de Software. (Para obter mais informações, consulte [Configure classifications and products](../get-started/configure-classifications-and-products.md) (Configurar classificações e produtos).) Em seguida, inicie a sincronização de atualizações de software. (Para obter mais informações, consulte [Synchronize software updates](../get-started/synchronize-software-updates.md) (Sincronizar atualizações de software).)  

3.  Instale o [hotfix 3095113](https://support.microsoft.com/kb/3095113) para o WSUS nos pontos de atualização de software e servidores do site.  

4.  Selecione a classificação **Upgrades** nas propriedades de componente do Ponto de Atualização de Software. (Para obter mais informações, consulte [Configure classifications and products](../get-started/configure-classifications-and-products.md) (Configurar classificações e produtos).) Em seguida, inicie a sincronização de atualizações de software. (Para obter mais informações, consulte [Synchronize software updates](../get-started/synchronize-software-updates.md) (Sincronizar atualizações de software).)  

## <a name="next-steps"></a>Próximas etapas
[Preparar-se para o gerenciamento de atualização de software](../get-started/prepare-for-software-updates-management.md)
