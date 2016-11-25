---
title: "Pré-requisitos para atualizações de software | Configuration Manager"
description: "Saiba mais sobre os pré-requisitos para atualizações de software no System Center Configuration Manager."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fe56129c09b8936ba59181add86acb239111fea7


---

# <a name="prerequisites-for-software-updates-in-system-center-configuration-manager"></a>Pré-requisitos para atualizações de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico lista os pré-requisitos para atualizações de software no System Center Configuration Manager. Para cada um deles, as dependências externas e internas são listadas em tabelas separadas.  

## <a name="software-update-dependencies-external-to-configuration-manager"></a>Dependências de atualizações de software externas ao Configuration Manager  
 As seções a seguir listam as dependências externas para atualizações de software.  

### <a name="internet-information-services-iis"></a>Serviços de Informações da Internet (IIS)  
 O IIS (Serviços de Informações da Internet) deve estar nos servidores de sistema de sites para executar o ponto de atualização de software, o ponto de gerenciamento e o ponto de distribuição. Para mais informações, consulte [Pré-requisitos para funções de sistema de sites](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  
 O WSUS é necessário para sincronização de atualizações de software e para o exame de avaliação de conformidade de atualizações de software nos clientes. O servidor WSUS deve ser instalado antes de se criar a função de sistema de site do ponto de atualização de software. Há suporte para as seguintes versões do WSUS em um ponto de atualização de software:  

-   WSUS 4 (função no Windows Server 2012 e Windows Server 2012 R2)  

-   WSUS 3.2 (função no Windows Server 2008 R2)  

 Quando você possui diversos pontos de atualização de software em um site, verifique se todos estão executando a mesma versão do WSUS.  

> [!WARNING]  
>  A classificação de atualizações de software **Atualizações** conta com suporte apenas a partir do WSUS 4.0. Antes de sincronizar essa nova classificação e poder avaliar computadores com Windows 10 em um plano de manutenção do Windows 10, é essencial que você instale o [hotfix 3095113](https://support.microsoft.com/kb/3095113) para o WSUS nos pontos de atualização de software e servidores do site. Esse hotfix permite que o WSUS em um servidor baseado no Windows Server 2012 ou no Windows Server 2012 R2 sincronize e distribua atualizações de recurso para o Windows 10. Para obter mais informações, consulte [Gerenciar o Windows como um serviço](../../osd/deploy-use/manage-windows-as-a-service.md).  
>   
>  Se você sincronizar atualizações de software com a classificação **Atualizações** antes de instalar o [hotfix 3095113](https://support.microsoft.com/kb/3095113), consulte [Recover from synchronizing the Atualizações category before you install KB 3095113](#BKMK_RecoverUpgrades).  

### <a name="wsus-administration-console"></a>Console de Administração do WSUS  
 O Console de Administração do WSUS é necessário no servidor de site do Configuration Manager quando o ponto de atualização de software está em um servidor de sistema de sites remoto e o WSUS ainda não está instalado no servidor de site.  

> [!IMPORTANT]  
>  A versão do WSUS no servidor de site deve ser a mesma versão do WSUS em execução nos pontos de atualização de software.  

> [!IMPORTANT]  
>  Não use o Console de Administração do WSUS para definir as configurações do WSUS. O Configuration Manager se conecta ao WSUS que é executado no ponto de atualização de software e define as configurações apropriadas.  

### <a name="windows-update-agent-wua"></a>Windows Update Agent (WUA)  
 O cliente WUA é necessário para habilitar a conexão de clientes ao servidor WSUS e recuperar a lista de atualizações de software que deve ser verificada quanto à conformidade.  

 Quando você instala o Configuration Manager, a última versão do WUA é baixada. Depois, quando o cliente do Configuration Manager é instalado, o WUA é atualizado, se necessário. No entanto, se a instalação falhar, você deverá usar um método diferente para atualizar o WUA.  

## <a name="software-update-dependencies-internal-to-configuration-manager"></a>Dependências de atualizações de software internas ao Configuration Manager  
 As seções a seguir listam as dependências internas para atualizações de software no Configuration Manager.  

### <a name="management-points"></a>Pontos de gerenciamento  
 Os pontos de gerenciamento transferem informações entre os computadores cliente e o site do Configuration Manager. Eles são necessários para atualizações de software.  

### <a name="software-update-point"></a>Ponto de atualização de software  
 Você deve instalar um ponto de atualização de software no servidor WSUS para poder implantar atualizações de software no Configuration Manager. Para mais informações, consulte [Instalar e configurar um ponto de atualização de software](../get-started/install-a-software-update-point.md).

### <a name="distribution-points"></a>Pontos de distribuição  
 Pontos de distribuição são necessários para armazenar o conteúdo de atualizações de software. Para obter mais informações sobre como instalar pontos de distribuição e gerenciar conteúdo, consulte [Gerenciar conteúdo e infraestrutura de conteúdo](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="client-settings-for-software-updates"></a>Configurações do cliente para atualizações de software  
 Por padrão, as atualizações de software estão habilitadas para clientes. Entretanto, existem outras configurações disponíveis que controlam como e quando os clientes avaliam a conformidade das atualizações de software e como elas são instaladas.  

 Para obter mais informações, consulte:  

-   [Configurações do cliente para atualizações de software](../get-started/manage-settings-for-software-updates.md#a-namebkmkclientsettingsa-client-settings-for-software-updates).  

-   Tópico [Configurações do cliente para atualizações de software](../../core/clients/deploy/about-client-settings.md#a-namebkmksoftwareupdatesdevicesettinga-software-updates).  

### <a name="reporting-services-point"></a>Ponto do Reporting Services  
 A função do sistema de site do ponto do Reporting Services pode exibir relatórios de atualizações de software. Essa função é opcional, mas recomendada. Para obter mais informações sobre como criar um ponto do Reporting Services, consulte [Configurando relatórios](../../core/servers/manage/configuring-reporting.md).  

##  <a name="a-namebkmkrecoverupgradesa-recover-from-synchronizing-the-upgrades-category-before-you-install-kb-3095113"></a><a name="BKMK_RecoverUpgrades"></a> Recuperar-se da sincronização da categoria Atualizações antes de instalar o KB 3095113  
 Você deve instalar o [hotfix 3095113](https://support.microsoft.com/kb/3095113) para o WSUS nos pontos de atualização de software e servidores do site antes de sincronizar a classificação **Atualizações** . Se o hotfix não estiver instalado quando a classificação **Atualizações** for habilitada, o WSUS verá a atualização de recurso do build 1511 do Windows 10 mesmo que não possa baixar e implantar corretamente os pacotes associados. Se você sincronizar todas as atualizações sem primeiro ter instalado o [hotfix 3095113](https://support.microsoft.com/kb/3095113), o SUSDB (banco de dados do WSUS) será populado com dados inúteis que deverão ser apagados para que as atualizações possam ser implantadas corretamente.  Use o procedimento a seguir para se recuperar desse problema.  

#### <a name="to-recover-from-synchronizing-the-upgrades-classification-before-you-install-kb-3095113"></a>Para se recuperar da sincronização da classificação Atualizações antes de instalar o KB 3095113  

1.  Exclua as atualizações de software com a classificação Atualizações. Você pode usar um script do PowerShell semelhante ao exemplo a seguir:  

    ```  
    $Server = Get-WSUSServer  
    $Config = $Server.GetConfiguration()  
    $Update10563 = “df4e45a3-946d-4467-b3fd-8621174bb666”  
    $UpdateGUID = New-Object Guid($Update10563)  
    $Server.DeleteUpdate($UpdateGUID)  
    ```  

    > [!IMPORTANT]  
    >  Você deve executar o script em todos os pontos de atualização de software na hierarquia do Configuration Manager antes de ir para a próxima etapa.  

     Para excluir em massa atualizações de software com a classificação Atualizações, modifique o script do PowerShell para ler vários GUIDs de um arquivo txt.  

2.  Desmarque a classificação **Atualizações** nas propriedades do componente do Ponto de Atualização de Software (para obter os detalhes, consulte [Configurar classificações e produtos](../get-started/configure-classifications-and-products.md)) e inicie a sincronização de atualizações de software (para obter detalhes, consulte [Sincronizar atualizações de software](../get-started/synchronize-software-updates.md).  

3.  Instale o [hotfix 3095113](https://support.microsoft.com/kb/3095113) para o WSUS nos pontos de atualização de software e servidores do site.  

4.  Marque a classificação **Atualizações** nas propriedades do componente do Ponto de Atualização de Software (para obter os detalhes, consulte [Configurar classificações e produtos](../get-started/configure-classifications-and-products.md)) e inicie a sincronização de atualizações de software (para obter detalhes, consulte [Sincronizar atualizações de software](../get-started/synchronize-software-updates.md).  

## <a name="next-steps"></a>Próximas etapas
[Preparar-se para o gerenciamento de atualização de software](../get-started/prepare-for-software-updates-management.md)



<!--HONumber=Nov16_HO1-->


