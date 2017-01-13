---
title: "Pré-requisitos de migração | Microsoft Docs"
description: "Entenda as versões compatíveis do Configuration Manager, os idiomas com suporte do site de origem e as configurações necessárias para migração."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec976930-7467-4d3c-b33c-991bf408a74a
caps.latest.revision: 10
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6cbb790df47c9a87514b0233e2d0c12dd6f23ee9
ms.openlocfilehash: 70e2531076abedc1381b6e3bccf15b5afe27b465


---
# <a name="prerequisites-for-migration-in-system-center-configuration-manager"></a>Pré-requisitos para a migração no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para migrar de uma hierarquia de origem com suporte, é necessário ter acesso a cada site de origem aplicável do Configuration Manager e às permissões no site de destino do System Center Configuration Manager para configurar e executar as operações de migração.  

 Use as informações das seções a seguir para ajudá-lo a entender as versões do Configuration Manager que têm suporte para migração, além das configurações necessárias.  

-   [Versões do Configuration Manager com suporte para migração](#BKMK_SupportedMigrationVersions)  

-   [Idiomas do site de origem com suporte para migração](#BKMK_SorceSiteLanguage)  

-   [Configurações necessárias para a migração](#BKMK_Required_Configurations)  

##  <a name="a-namebkmksupportedmigrationversionsa-versions-of-configuration-manager-that-are-supported-for-migration"></a><a name="BKMK_SupportedMigrationVersions"></a> Versões do Configuration Manager com suporte para migração  
 Você pode migrar dados de uma hierarquia de origem que executa qualquer uma das seguintes versões do Configuration Manager:  

-   Configuration Manager 2007 SP2 (para fins de migração, o Configuration Manager 2007 R2 ou R3 no site de origem não são considerados. Contanto que o site de origem execute o SP2, os sites com o complemento R2 ou R3 instalado contam com suporte para migração para o System Center Configuration Manager)  

-   System Center 2012 Configuration Manager SP2 ou System Center 2012 R2 Configuration Manager SP1  

    > [!TIP]  
    >  Além de migração, você pode usar uma atualização in-loco de sites que executam o System Center 2012 Configuration Manager para o System Center Configuration Manager.  

-   Uma hierarquia do System Center Configuration Manager da mesma versão ou de versão inferior do System Center Configuration Manager  

##  <a name="a-namebkmksorcesitelanguagea-source-site-languages-that-are-supported-for-migration"></a><a name="BKMK_SorceSiteLanguage"></a> Idiomas do site de origem com suporte para migração  
 Ao migrar dados entre as hierarquias do Configuration Manager, eles são armazenados na hierarquia de destino em formato de idioma neutro para o System Center Configuration Manager. Devido ao fato de o Configuration Manager 2007 não armazenar os dados em um formato de idioma neutro, o processo de migração deve converter os objetos nesse formato durante a migração do Configuration Manager 2007. Portanto, somente os sites de origem do Configuration Manager 2007 instalados com os seguintes idiomas têm suporte para migração:  

-   Inglês  

-   Francês  

-   Alemão  

-   Japonês  

-   Coreano  

-   Russo  

-   Chinês simplificado  

-   Chinês tradicional  

Quando você migra dados de uma hierarquia do System Center 2012 Configuration Manager ou do System Center Configuration Manager, não há limitações de idioma do site de origem. Os objetos do banco de dados do site de origem já estão em um formato de idioma neutro.  

##  <a name="a-namebkmkrequiredconfigurationsa-required-configurations-for-migration"></a><a name="BKMK_Required_Configurations"></a> Configurações necessárias para a migração  
Veja a seguir as configurações necessárias para o uso da migração e de suas operações.  

-   **Para configurar, executar e monitorar a migração no console do Configuration Manager:**  

     No site de destino, sua conta deve ser atribuída à função de segurança de administração baseada em funções do **Administrador de Infraestrutura**. Essa função de segurança concede permissões para gerenciamento de todas as operações de migração, que incluem criação de trabalhos de migração, limpeza, monitoramento e a ação de compartilhar e atualizar os pontos de distribuição.  

-   **Coleta de dados:**  

     Para habilitar o site de destino para coletar dados, é necessário configurar as duas contas de acesso ao site de origem demonstradas a seguir para uso em todo site de origem:  

    -   **Conta do Site de Origem:** essa conta é usada para acessar o Provedor de SMS do site de origem.  

        -   Para sites de origem do Configuration Manager 2007 SP2, essa conta necessita de permissão de **Leitura** para todos os objetos do site de origem.  

        -   Para um site de origem do System Center 2012 Configuration Manager ou do System Center Configuration Manager, essa conta exige permissão de **Leitura** para todos os objetos do site de origem. Você concede essa permissão à conta usando a administração baseada em funções. Para obter informações sobre como usar a administração baseada em funções, consulte [Fundamentals of role-based administration for System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

    -   **Conta do Banco de Dados do Site de Origem:** essa conta é usada para acessar o banco de dados do SQL Server do site de origem e exige as permissões **Connect**, **Execute**e **Select** para o banco de dados do site de origem.  

    Você pode configurar essas contas definindo uma nova hierarquia de origem, uma coleta de dados para um site de origem adicional, ou reconfigurando as credenciais para um site de origem. Essas contas podem usar uma conta de usuário do domínio ou então você pode especificar a conta de computador do site de nível superior da hierarquia de destino.  

    > [!IMPORTANT]  
    >  Se você usar a conta de computador do Configuration Manager para as contas de acesso, verifique se a conta é membro do grupo de segurança **Distributed COM – Usuários** no domínio no qual o site de origem reside.  

    Ao coletar dados, os seguintes protocolos e portas de rede são usados:  

    -   NetBIOS/SMB – 445 (TCP)  

    -   RPC (WMI) - 135 (TCP)  

    -   SQL Server - portas TCP usadas pelos bancos de dados de sites de origem e de destino.  

-   **Migrar atualizações de software:**  

     Para poder migrar as atualizações de software, é necessário configurar a hierarquia de destino com um ponto de atualização de software. Para obter mais informações, consulte [Planejando a migração de atualização de Software](../../core/migration/planning-for-the-migration-of-objects.md#Plan_migrate_Software_updates).  

-   **Compartilhar pontos de distribuição:**  

     Para compartilhar com êxito pontos de distribuição do site de origem, pelo menos um site primário ou o site de administração central na hierarquia de destino deve usar os mesmos números de porta para as solicitações do cliente que os do site de origem. Para obter informações sobre portas de solicitação de cliente, consulte [Como configurar portas de comunicação do cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-communication-ports.md)  

     Para todo site de origem, são compartilhados somente os pontos de distribuição instalados nos servidores do sistema de site configurados com um FQDN.  

     Além disso, para compartilhar um ponto de distribuição de um site de origem do System Center 2012 Configuration Manager ou do System Center Configuration Manager, a **Conta de Site de Origem** (que acessa o Provedor de SMS para o servidor do site de origem) deve ter permissões **Modificar** para o objeto **Site** no site de origem. Você pode conceder essa permissão para a conta usando a administração baseada em funções. Para obter informações sobre como usar a administração baseada em funções, consulte [Fundamentals of role-based administration for System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  


-   **Atualizar ou reatribuir pontos de distribuição:**  

     A **Conta de Acesso do Site de Origem** configurada para coletar dados do Provedor de SMS do site de origem deve possuir as seguintes permissões:  

    -   Para atualizar um ponto de distribuição do Configuration Manager 2007, a conta necessita das permissões de **Leitura**, **Executar** e **Excluir** para a classe do **Site** no servidor do site do Configuration Manager 2007 para remover com êxito o ponto de distribuição do site de origem do Configuration Manager 2007  

    -   Para reatribuir um ponto de distribuição do System Center 2012 Configuration Manager ou do System Center Configuration Manager, a conta deve ter uma permissão **Modificar** para o objeto **Site** no site de origem. Você pode conceder essa permissão para a conta usando a administração baseada em funções. Para obter informações sobre como usar a administração baseada em funções, consulte [Fundamentals of role-based administration for System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

     Para atualizar ou reatribuir com sucesso um ponto de distribuição a uma nova hierarquia, as portas configuradas para solicitações de cliente no site que gerencia o ponto de distribuição na hierarquia de origem deve ser igual às portas que estão configuradas para solicitações de cliente no site de destino que irá gerenciar o ponto de distribuição. Para obter informações sobre portas de solicitação de cliente, consulte [Como configurar portas de comunicação do cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-communication-ports.md).  



<!--HONumber=Dec16_HO3-->


