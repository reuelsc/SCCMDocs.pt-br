---
title: "Pré-requisitos de sites | Microsoft Docs"
description: "Saiba mais sobre os diferentes pré-requisitos necessários para instalar os diferentes tipos de sites do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: d39c8acca79c97c3979020c284616038b897d7cf

---
# <a name="prerequisites-for-installing-system-center-configuration-manager-sites"></a>Pré-requisitos para instalar sites do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


As seções a seguir fornecem detalhes sobre os diferentes pré-requisitos necessários para instalar os diferentes tipos de sites do System Center Configuration Manager.



## <a name="primary-sites-and-the-central-administration-site"></a>Site de administração central e sites primários
Os pré-requisitos a seguir se aplicam à instalação de um site de administração central como o primeiro site de uma hierarquia, um site primário autônomo ou um site primário filho. Se você estiver instalando um site de administração central como parte de um cenário de expansão da hierarquia, consulte [Expanding a stand-alone primary site (Expandindo um site primário autônomo)](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand
) neste tópico.

####  <a name="a-namebkmkprereqpria-prerequisites-to-install-a-primary-site-or-central-administration-site"></a><a name="bkmk_PrereqPri"></a> Pré-requisitos para instalar um site primário ou um site de administração central  

-   O usuário que instalará o site deve ter as seguintes permissões:  

    -   **Administrador Local** no computador do servidor do site  

    -   **Administrador Local** em cada computador que hospedará o **banco de dados do site** ou uma instância do **SMS_Provider** para o site  

    -   **Sysadmin** na instância do SQL Server que hospeda o banco de dados do site  

        > [!IMPORTANT]  
        >  Após a conclusão da instalação, tanto a conta do usuário que executa a instalação quanto a conta do computador do servidor de site devem manter os direitos de sysadmin no SQL Server. Não há suporte para a remoção dos direitos sysadmin dessas contas.  

-   Ao instalar um site primário, são necessárias as permissões adicionais a seguir:  
    -  **Administrador Local** em computadores adicionais nos quais você instalará o ponto de gerenciamento inicial e o ponto de distribuição, se não estiver no servidor do site.  

-   Ao instalar um novo site primário filho abaixo do site de administração central, serão necessárias as permissões adicionais a seguir:  

    -   **Administrador Local** no computador que hospeda o site de administração central  

    -   Permissões de administração baseada em funções no Configuration Manager equivalentes à função de segurança de **Administrador de Infraestrutura** ou **Administrador Completo**.  

-   É necessário usar a mídia de instalação correta (arquivos de origem) e executar a Instalação nesse local. Para obter informações sobre os arquivos de origem corretos a serem usados para instalar diferentes sites, consulte [Opções para instalar os diferentes tipos de sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options), no tópico [Prepare to install sites (Preparar para instalar sites)](../../../../core/servers/deploy/install/prepare-to-install-sites.md).

-   O computador do servidor do site deve ter acesso aos arquivos de Instalação atualizados da Microsoft:
    -  Antes de iniciar a instalação, será possível baixar e armazenar uma cópia desses arquivos em sua rede local usando o [Downloader de Instalação](../../../../core/servers/deploy/install/setup-downloader.md)
    -  Se uma cópia local desses arquivos não estiver disponível, o servidor do site deverá ter acesso à Internet para que ele possa baixar esses arquivos da Microsoft durante a instalação

  - Para expandir um site primário autônomo que tenha uma função do sistema de sites de Ponto de Conexão de Serviço instalada, você deve desinstalar o Ponto de Conexão de Serviço. Apenas uma instância dessa função é permitida em uma hierarquia, sendo permitida somente no site da camada superior da hierarquia. Você terá a oportunidade de reinstalar a função durante a instalação do site de administração central.
  - O servidor do site e os computadores de banco de dados do site devem atender a todas as configurações de pré-requisito. Antes de iniciar a instalação, será possível [executar manualmente o Verificador de Pré-requisitos](../../../../core/servers/deploy/install/prerequisite-checker.md) para identificar e corrigir problemas.  


## <a name="a-namebkmkexpanda-expanding-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> Expansão de um site primário autônomo
Um site primário autônomo deve atender aos seguinte pré-requisitos para que você possa expandi-lo para uma hierarquia com um site de administração central:


-   **Será necessário instalar a mídia de instalação do novo site de administração central (arquivos de origem) que corresponde à versão do site primário autônomo:**  
     Para garantir a correspondência de versões, instale o novo site usando os arquivos de origem encontrados na [pasta CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) no site primário autônomo.

     Para obter mais informações sobre os arquivos de origem corretos a serem usados para instalar diferentes sites, consulte [Opções para instalar os diferentes tipos de sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options), no tópico [Prepare to install sites (Preparar para instalar sites)](../../../../core/servers/deploy/install/prepare-to-install-sites.md).


-   **O site primário autônomo não pode ser configurado para migrar dados de outra hierarquia do Configuration Manager:**  

     É necessário interromper a migração ativa para o site primário autônomo, de outras hierarquias do Configuration Manager e remover todas as configurações de migração. Isso inclui trabalhos de migração que não foram concluídos, Coleta de Dados e a configuração da hierarquia de origem ativa.  

     Isso é necessário porque as operações de migração são realizadas pelo site de camada superior da hierarquia e as configurações para migração não são transferidas ao site de administração central quando você expande um site primário autônomo.  

     Depois de expandir o site primário autônomo, se você reconfigurar a migração no site primário, ela será o site de administração central que realiza as operações relacionadas à migração. Para obter mais informações sobre como configurar a migração, consulte [Configurando hierarquias de origem e sites de origem para migração para o System Center Configuration Manager](../../../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

-   **A conta de computador do computador que hospedará o novo site de administração central deve ser um membro do grupo de Administradores no site primário autônomo:**  

     Para expandir com êxito o site primário autônomo, a conta de computador do novo site de administração central deve ser um membro do grupo de **Administradores** dos sites primários autônomos. Isso é necessário somente durante a expansão do site, e a conta pode ser removida do grupo no site primário após a conclusão da expansão do site.  

-   **A conta de usuário que executa a instalação do novo site de administração central deve ter permissões de administração baseada em função no site primário autônomo:**  

     Para instalar um site de administração central como parte de um cenário de expansão de site, a conta de usuário que executa a instalação do site de administração central deve ser definida em administração baseada em função no site primário autônomo como um **Administrador Completo** ou um **Administrador de Infraestrutura**.  

-   **Para expandir o site, será necessário desinstalar as seguintes funções do sistema de site do site primário autônomo:**  

    -   Ponto de sincronização do Asset Intelligence  

    -   Ponto do Endpoint Protection  

    -   Ponto de Conexão de Serviço  

     Essas funções do sistema de site têm suporte apenas no site de camada superior da hierarquia. Portanto, é necessário desinstalar essas funções do sistema de sites antes de expandir o site primário autônomo. Depois de expandir o site, você poderá reinstalar essas funções do sistema de site no site de administração central.  

    Todas as outras funções do sistema de site podem permanecer instaladas no site primário.  

-   **A porta para o SQL Server Service Broker deve estar aberta entre o site primário autônomo e o computador que instalará o site de administração central:**  

     Para replicar dados de maneira bem sucedida entre o site de administração central e um site primário, o Configuration Manager requer que uma porta que será usada pelo SQL Server Service seja aberta entre os dois sites. Ao instalar uma administração central e expandir um site primário autônomo, a verificação de pré-requisitos não estabelece que a porta que você determinou para o SQL Server Service Broker seja aberta no site primário.  


## <a name="a-namebkmksecondarya-secondary-sites"></a><a name="bkmk_secondary"></a> Sites secundários
A seguir encontram-se os pré-requisitos para instalar sites secundários:
-   O usuário administrativo que configura a instalação do site secundário no console do Configuration Manager deve ter direitos de administração baseada em funções equivalentes à função de segurança **Administrador de Infraestrutura** ou **Administrador Completo**.  

-   A conta de computador do site primário pai deve ser de **Administrador Local** no computador do servidor do site secundário.  

-   Quando o site secundário usa uma instância do SQL Server previamente instalada para hospedar o banco de dados do site secundário:  

    -   A **conta de computador** do site primário pai deve ter direitos **sysadmin** na instância do SQL Server no computador do servidor do site secundário.  

    -   A conta **Sistema Local** do computador do servidor do site secundário deve ter direitos **sysadmin** na instância do SQL Server no computador do servidor do site secundário.  

        > [!IMPORTANT]  
        >  Após a conclusão da instalação, ambas as contas devem manter os direitos sysadmin no SQL Server. Não há suporte para a remoção dos direitos sysadmin dessas contas.  

-   O computador do servidor do site secundário deve cumprir todas as configurações de pré-requisito, que inclui o SQL Server e as funções padrão do sistema de sites do ponto de gerenciamento e do ponto de distribuição.  



<!--HONumber=Dec16_HO3-->


