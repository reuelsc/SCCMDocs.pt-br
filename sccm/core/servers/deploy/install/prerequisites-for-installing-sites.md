---
title: Pré-requisitos para sites
titleSuffix: Configuration Manager
description: Saiba mais sobre os pré-requisitos para instalar os diferentes tipos de sites do Configuration Manager.
ms.date: 04/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 76ab690024509d63293a7b9b94721644023702a9
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159348"
---
# <a name="prerequisites-for-installing-configuration-manager-sites"></a>Pré-requisitos para instalar sites do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de começar a instalação do site, conheça os pré-requisitos para instalar os diferentes tipos de sites do Configuration Manager.



## <a name="primary-sites-and-the-central-administration-site"></a>Site de administração central e sites primários

Os pré-requisitos a seguir aplicam-se à instalação de um dos seguintes tipos:
- Um site de administração central como o primeiro site de uma hierarquia
- Um site primário autônomo
- Um site primário filho

Se você estiver instalando um site de administração central como parte de uma expansão da hierarquia, veja [Expansão de um site primário autônomo](#bkmk_expand).


###  <a name="bkmk_PrereqPri"></a> Pré-requisitos para instalar um site primário ou um site de administração central  

- As funções e os recursos do Windows Server e os componentes do Windows a seguir devem ser instalados:  
    - .NET Framework 3.5 SP1 (ou posterior)
    - .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2
    - Compactação Diferencial Remota
    - Windows ADK
    - Pacotes Redistribuíveis do Visual C++  
    
    Para obter mais informações, confira [Pré-requisitos do sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012sspreq)  

- A conta de usuário que instala o site deve ter os seguintes direitos:  

    - **Administrador** nos seguintes servidores:  
        - O servidor do site  
        - Cada servidor que hospeda o **banco de dados do site**  
        - Cada instância das **provedor de SMS** para o site  

    - **Sysadmin** na instância do SQL Server que hospeda o banco de dados do site  

        > [!IMPORTANT]  
        >  Quando a instalação do Configuration Manager for concluída, tanto a conta do usuário que executa a Instalação quanto a conta do computador do servidor do site devem manter os direitos sysadmin no SQL Server. Não remova os direitos sysadmin dessas contas.  

- Se você estiver instalando um site primário, precisará dos seguintes direitos adicionais:  

    - **Administrador** em servidores adicionais nos quais você instalará o ponto de gerenciamento inicial e o ponto de distribuição, se não estiver no servidor do site  

- Se você estiver instalando um novo site primário filho abaixo de um site de administração central, precisará dos seguintes direitos adicionais:  

    - **Administrador** no servidor que hospeda o site de administração central  

    - Direitos de administração baseada em funções no Configuration Manager equivalentes à função de segurança de **Administrador de Infraestrutura** ou **Administrador Completo**  

- Use os arquivos de origem de instalação corretos e execute a instalação nesse local. Para obter informações sobre os arquivos de origem corretos a serem usados para instalar diferentes tipos de sites, veja [Opções de instalação de diferentes tipos de sites](/sccm/core/servers/deploy/install/prepare-to-install-sites#bkmk_options).  

- O servidor do site deve ter acesso aos arquivos de Instalação atualizados da Microsoft, de uma das seguintes maneiras:  

    - Antes de iniciar a instalação, baixe e armazene uma cópia desses arquivos em sua rede local. Para obter mais informações, consulte [Downloader de Instalação](/sccm/core/servers/deploy/install/setup-downloader).  

    - Se uma cópia local desses arquivos não estiver disponível, o servidor do site deverá ter acesso à Internet. Ele baixa esses arquivos da Microsoft durante a instalação.  

- O servidor do site e os servidores de banco de dados do site devem atender a todas as configurações de pré-requisito. Antes de iniciar a instalação do Configuration Manager, [execute manualmente o Verificador de Pré-requisitos](/sccm/core/servers/deploy/install/prerequisite-checker) para identificar e corrigir problemas.  


### <a name="bkmk_expand"></a> Pré-requisitos para expandir um site primário autônomo

Um site primário autônomo deve atender aos seguinte pré-requisitos para que você possa expandi-lo para uma hierarquia com um site de administração central:

#### <a name="source-file-version-matches-site-version"></a>A versão do arquivo de origem corresponde à versão do site
Instale o novo site de administração central usando mídia de uma pasta CD.Latest que corresponde à versão do site primário autônomo. Para garantir a correspondência de versões, use os arquivos de origem encontrados na [pasta CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder) no site primário autônomo. 

Para saber mais sobre os arquivos de origem corretos a serem usados para instalar diferentes sites, veja [Opções de instalação de diferentes tipos de sites](/sccm/core/servers/deploy/install/prepare-to-install-sites#bkmk_options).  

#### <a name="stop-active-migration-from-another-hierarchy"></a>Interromper a migração ativa de outra hierarquia
Não é possível configurar o site primário autônomo para migrar dados de outra hierarquia do Configuration Manager. Interrompa a migração ativa para o site primário autônomo de outras hierarquias do Configuration Manager e remover todas as configurações de migração. Essas configurações incluem: 
- Trabalhos de migração que não tenham sido concluídos  
- Coleta de dados  
- A configuração da hierarquia de origem ativa  

Essa configuração é necessária porque o Configuration Manager migra dados do site de nível superior da hierarquia. Quando você expande um site primário autônomo, as configurações para migração não são transferidas para o site de administração central.  

Depois de expandir o site primário autônomo, se você reconfigurar a migração no site primário, o site de administração central executará as operações de migração. 

Para saber mais sobre como configurar a migração, veja [Configurar hierarquias de origem e sites de origem para migração](/sccm/core/migration/configuring-source-hierarchies-and-source-sites-for-migration).  

#### <a name="computer-account-as-administrator"></a>Conta de computador como administrador
A conta de computador do servidor que hospedará o novo site de administração central deve ser um membro do grupo de **Administradores** no servidor de site primário autônomo. 

Para expandir com êxito o site primário autônomo, a conta de computador do novo site de administração central deve ter direitos de **Administrador** no site primário autônomo. Isso é necessário somente durante a expansão do site. Quando a expansão do site for concluída, você poderá remover a conta do grupo de usuários no site primário.  

#### <a name="installation-account-permissions"></a>Permissões da conta de instalação
A conta de usuário que executa a instalação do Configuration Manager do novo site de administração central deve ter direitos de administração baseada em função no site primário autônomo.

Para instalar um site de administração central como parte de uma expansão de site, a conta de usuário que executa a instalação do site de administração central deve ser definida em administração baseada em função no site primário autônomo como um **Administrador Completo** ou um **Administrador de Infraestrutura**.  

#### <a name="top-level-site-roles"></a>Funções do site de nível superior
Antes de expandir o site, desinstale as seguintes funções do sistema de site do site primário autônomo:

- Ponto de sincronização do Asset Intelligence  
- Ponto do Endpoint Protection  
- Ponto de Conexão de Serviço  

O Configuration Manager só dá suporte a essas funções no site de nível superior da hierarquia. Desinstale essas funções do sistema de sites antes de expandir o site primário autônomo. Depois de expandir o site, reinstale essas funções do sistema de site no site de administração central.  

Todas as outras funções do sistema de site podem permanecer instaladas no site primário.  

#### <a name="open-the-sql-server-service-broker-port"></a>Abra a porta do SQL Server Service Broker
A porta da rede deve estar aberta para o SQL SSB (Server Service Broker) entre o site primário autônomo e o servidor para o site de administração central.  

Para replicar dados de maneira bem sucedida entre o site de administração central e um site primário, o Configuration Manager requer uma porta aberta entre os dois sites para o SSB usar. Quando você instala um site de administração central e expande um site primário autônomo, a verificação de pré-requisitos não verifica se a porta especificada para o SSB está aberta no site primário.  

#### <a name="known-issues-with-azure-services"></a>Problemas conhecidos com os serviços do Azure
Quando você usar um dos seguintes serviços do Azure com o Configuration Manager, depois de expandi-lo, remova e recrie a conexão para esse serviço.

- [Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics)  
- [Upgrade Readiness](/sccm/core/clients/manage/upgrade-readiness)  
- [Microsoft Store para Empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)  

Siga as etapas a seguir para resolver esse problema:
 1. No console do Configuration Manager, exclua o serviço do Azure do nó de **serviços do Azure**.  

 2. No Portal do Azure, exclua o locatário associado ao serviço do nó de locatários do Azure Active Directory. Essa ação também exclui o aplicativo Web do Azure AD associado ao serviço.  

 3. Reconfigure a conexão para o serviço do Azure para uso com o Configuration Manager.  



## <a name="bkmk_secondary"></a> Sites secundários

A seguir encontram-se os pré-requisitos para instalar sites secundários:  

- As seguintes funções e recursos do Windows Server e componentes do Windows devem ser instalados:  
    - .NET Framework 3.5 SP1 (ou posterior)
    - .NET Framework 4.5.2,4.6.1,4.6.2,4.7,4.7.1 ou 4.7.2
    - Compactação Diferencial Remota
    - Pacotes Redistribuíveis do Visual C++  
    
    Para obter mais informações, confira [Pré-requisitos do sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012secpreq)  

- O administrador que configura a instalação do site secundário no console do Configuration Manager deve ter direitos de administração baseada em funções equivalentes à função de segurança **Administrador de Infraestrutura** ou **Administrador Completo**.  

- A conta de computador do site primário pai deve ser de **Administrador** no servidor do site secundário.  

- Quando o site secundário usa uma instância do SQL Server previamente instalada para hospedar o banco de dados do site secundário:  

    - A conta de computador do site primário pai deve ter direitos **sysadmin** na instância do SQL Server no servidor do site secundário.  

    - A conta **Sistema Local** do computador do servidor do site secundário deve ter direitos **sysadmin** na instância do SQL Server no servidor do site secundário.  

        > [!IMPORTANT]  
        >  Quando a instalação do Configuration Manager terminar, ambas as contas devem manter os direitos de sysadmin no SQL Server. Não remova os direitos sysadmin dessas contas.  

- O servidor do site secundário deve atender a todas as configurações de pré-requisito. Essas configurações incluem o SQL Server e as funções do sistema de site padrão do ponto de gerenciamento e do ponto de distribuição.  
