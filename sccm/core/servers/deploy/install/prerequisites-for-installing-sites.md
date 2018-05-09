---
title: Pré-requisitos para sites
titleSuffix: Configuration Manager
description: Saiba mais sobre os pré-requisitos para instalar os diferentes tipos de sites do System Center Configuration Manager.
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e45ec9aca5ee1a14f9058453497003814b2fdb0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="prerequisites-for-installing-system-center-configuration-manager-sites"></a>Pré-requisitos para instalar sites do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de começar a instalação do site, é uma boa ideia aprender sobre os pré-requisitos para instalar os diferentes tipos de sites do System Center Configuration Manager.

## <a name="primary-sites-and-the-central-administration-site"></a>Site de administração central e sites primários
Os pré-requisitos a seguir se aplicam à instalação de um site de administração central como o primeiro site de uma hierarquia, instalação de um site primário autônomo ou instalação de um site primário filho. Se você estiver instalando um site de administração central como parte de uma expansão da hierarquia, consulte [Expansão de um site primário autônomo](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand) neste tópico.

###  <a name="bkmk_PrereqPri"></a> Pré-requisitos para instalar um site primário ou um site de administração central  

-   A conta de usuário que instala o site deve ter os seguintes direitos:  

    -   **Administrador** no computador do servidor do site  
    -   **Administrador** em cada computador que hospedará o **banco de dados do site** ou uma instância do **Provedor de SMS** para o site  
    -   **Sysadmin** na instância do SQL Server que hospeda o banco de dados do site  

        > [!IMPORTANT]  
        >  Quando a Instalação for concluída, tanto a conta do usuário que executa a Instalação quanto a conta do computador do servidor do site devem manter os direitos de sysadmin no SQL Server. Não remova os direitos sysadmin dessas contas.  

-   Se você estiver instalando um site primário, precisará dos seguintes direitos adicionais:  
    -  **Administrador** em computadores adicionais nos quais você instalará o ponto de gerenciamento inicial e o ponto de distribuição, se não estiver no servidor do site  

-   Se você estiver instalando um novo site primário filho abaixo de um site de administração central, precisará dos seguintes direitos adicionais:  

    -   **Administrador** no computador que hospeda o site de administração central  

    -   Direitos de administração baseada em funções no Configuration Manager equivalentes à função de segurança de **Administrador de Infraestrutura** ou **Administrador Completo**  

-   É necessário usar a mídia de instalação correta (arquivos de origem) e executar a Instalação nesse local. Para obter informações sobre os arquivos de origem corretos a serem usados para instalar diferentes tipos de sites, consulte [Opções de instalação de diferentes tipos de sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options), no tópico [Preparar para instalar sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md).

-   O computador do servidor do site deve ter acesso aos arquivos de Instalação atualizados da Microsoft, de uma das seguintes maneiras:
    -  Antes de iniciar a instalação, será possível baixar e armazenar uma cópia desses arquivos em sua rede local usando o [Downloader de Instalação](../../../../core/servers/deploy/install/setup-downloader.md).
    -  Se uma cópia local desses arquivos não estiver disponível, o servidor do site deverá ter acesso à Internet para que ele possa baixar esses arquivos da Microsoft durante a instalação.

- Para expandir um site primário autônomo que tenha uma função do sistema de sites de ponto de conexão de serviço instalada, você deve desinstalar o ponto de conexão de serviço. Apenas uma instância dessa função é permitida em uma hierarquia, sendo permitida somente no site da camada superior da hierarquia. Você terá a oportunidade de reinstalar a função durante a instalação do site de administração central.
- O servidor do site e os computadores de banco de dados do site devem atender a todas as configurações de pré-requisito. Antes de iniciar a Instalação, será possível [executar manualmente o Verificador de Pré-requisitos](../../../../core/servers/deploy/install/prerequisite-checker.md) para identificar e corrigir problemas.  


### <a name="bkmk_expand"></a> Pré-requisitos para expandir um site primário autônomo
Um site primário autônomo deve atender aos seguinte pré-requisitos para que você possa expandi-lo para uma hierarquia com um site de administração central:

-   **É necessário instalar o novo site de administração central usando mídia de um CD. A última pasta (que contém os arquivos de origem) que corresponde à versão do site primário autônomo**

 Para garantir a correspondência de versões, use os arquivos de origem encontrados na [pasta CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder) no site primário autônomo.

 Para obter mais informações sobre os arquivos de origem corretos a serem usados para instalar diferentes sites, consulte [Opções de instalação de diferentes tipos de sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options), no tópico [Preparar para instalar sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md).


-   **O site primário autônomo não pode ser configurado para migrar dados de outra hierarquia do Configuration Manager**  

     É necessário interromper a migração ativa para o site primário autônomo de outras hierarquias do Configuration Manager e remover todas as configurações de migração. Isso inclui trabalhos de migração que não foram concluídos, coleta de dados e a configuração da hierarquia de origem ativa.  

     Isso é necessário porque as operações de migração são realizadas pelo site de camada superior da hierarquia e as configurações para migração não são transferidas ao site de administração central quando você expande um site primário autônomo.  

     Depois de expandir o site primário autônomo, se você reconfigurar a migração no site primário, o site de administração central executará as operações relacionadas à migração. Para obter mais informações sobre como configurar a migração, consulte [Configurar hierarquias de origem e sites de origem para migração para o System Center Configuration Manager](../../../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

-   **A conta de computador do computador que hospedará o novo site de administração central deve ser um membro do grupo de usuários Administradores no site primário autônomo**  

     Para expandir com êxito o site primário autônomo, a conta de computador do novo site de administração central deve ter direitos de **Administrador** no site primário autônomo. Isso é necessário somente durante a expansão do site. A conta poderá ser removida do grupo de usuários no site primário quando a expansão do site for concluída.  

-   **A conta de usuário que executa a Instalação do novo site de administração central deve ter direitos de administração baseada em função no site primário autônomo**  

     Para instalar um site de administração central como parte de uma expansão de site, a conta de usuário que executa a instalação do site de administração central deve ser definida em administração baseada em função no site primário autônomo como um **Administrador Completo** ou um **Administrador de Infraestrutura**.  

-   **Para expandir o site, será necessário desinstalar as seguintes funções do sistema de site do site primário autônomo:**  

    -   Ponto de sincronização do Asset Intelligence  
    -   Ponto do Endpoint Protection  
    -   Ponto de Conexão de Serviço  

   Essas funções do sistema de site têm suporte apenas no site de camada superior da hierarquia. Portanto, é necessário desinstalar essas funções do sistema de sites antes de expandir o site primário autônomo. Depois de expandir o site, você poderá reinstalar essas funções do sistema de site no site de administração central.  

    Todas as outras funções do sistema de site podem permanecer instaladas no site primário.  

-   **A porta para o SQL SSB (Server Service Broker) entre o site primário autônomo e o computador que instalará o site de administração central deve estar aberta**  

     Para replicar dados de maneira bem sucedida entre o site de administração central e um site primário, o Configuration Manager requer uma porta aberta entre os dois sites para o SSB usar. Ao instalar um site de administração central e expandir um site primário autônomo, a verificação de pré-requisitos não verifica se a porta especificada para o SSB está aberta no site primário.  

**Problemas conhecidos quando você configurou os serviços do Azure:**  
Quando você usar um dos seguintes serviços do Azure com o Configuration Manager e planejar expandir um site, depois de expandi-lo, será necessário remover e recriar a conexão para esse serviço.

Serviços:  
-       [OMS](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) (Operations Manager Suite)
-       [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics)
-       [Microsoft Store para Empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)

Siga as etapas a seguir para resolver esse problema:
 1.    No console do Configuration Manager, exclua o serviço do Azure do nó de serviços do Azure.
 2.    No Portal do Azure, exclua o locatário associado ao serviço do nó de locatários do Azure Active Directory.  Isso também exclui o aplicativo Web do Azure AD associado ao serviço.  
 3.   Reconfigure a conexão para o serviço do Azure para uso com o Configuration Manager.


## <a name="bkmk_secondary"></a> Sites secundários
A seguir encontram-se os pré-requisitos para instalar sites secundários:
-   O administrador que configura a instalação do site secundário no console do Configuration Manager deve ter direitos de administração baseada em funções equivalentes à função de segurança **Administrador de Infraestrutura** ou **Administrador Completo**.  
-   A conta de computador do site primário pai deve ser de **Administrador** no computador do servidor do site secundário.  
-   Quando o site secundário usa uma instância do SQL Server previamente instalada para hospedar o banco de dados do site secundário:  

    -   A **conta de computador** do site primário pai deve ter direitos **sysadmin** na instância do SQL Server no computador do servidor do site secundário.  

    -   A conta **Sistema Local** do computador do servidor do site secundário deve ter direitos **sysadmin** na instância do SQL Server no computador do servidor do site secundário.  

        > [!IMPORTANT]  
        >  Quando a Instalação terminar, ambas as contas devem manter os direitos sysadmin no SQL Server. Não remova os direitos sysadmin dessas contas.  

-   O computador do servidor do site secundário deve cumprir todas as configurações de pré-requisito, que inclui o SQL Server e as funções padrão do sistema de sites do ponto de gerenciamento e do ponto de distribuição.  
