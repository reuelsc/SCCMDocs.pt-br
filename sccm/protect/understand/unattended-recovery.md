---
title: "Recuperação autônoma | Microsoft Docs"
description: Use um script para recuperar seus sites no System Center Configuration Manager.
ms.custom: na
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b5a1a1d165a6888bc26e809666d2331ff3c24d68
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="unattended-site-recovery-for-configuration-manager"></a>Recuperação autônoma de sites para o Configuration Manager   

*Aplica-se a: System Center Configuration Manager (Branch Atual)* Para executar uma [recuperação autônoma](/sccm/protect/understand/recover-sites#site-recovery-procedures) de um site de administração central ou de um site primário do Configuration Manager, é possível criar um script de instalação autônoma e usar a Instalação com a opção de comando **/script**. O script fornece o mesmo tipo de informação que o Assistente de Instalação solicita, porém não há configurações padrão. Todos os valores devem ser especificados para as chaves de instalação que se aplicam ao tipo de recuperação usado.

 Para usar a opção de linha de comando de instalação /script, é necessário criar um arquivo de inicialização e especificar o nome do arquivo de inicialização após a opção de linha de comando de instalação /script. O nome do arquivo não é importante, contanto que tenha a extensão de nome de arquivo **.ini**. Para fazer referência ao arquivo de inicialização de instalação na linha de comando, é necessário fornecer o caminho completo do arquivo. Por exemplo, se o arquivo de inicialização de instalação for nomeado como *setup.ini* e armazenado na *pasta C:\setup*, sua linha de comando será:

 **setup /script c:\setup\setup.ini**.

> [!IMPORTANT]  
>  É necessário ter direitos de administrador para executar a Instalação. Ao executar a Instalação com o script autônomo, inicie o prompt de comando em um contexto de administrador usando **Executar como administrador**.

 O script contém nomes de seção, nomes de chave e valores. Os nomes de chave da seção requeridos variam de acordo com o tipo de recuperação do script. A ordem das chaves dentro das seções, bem como a ordem das seções dentro do arquivo, não é importante. As chaves não diferenciam maiúsculas de minúsculas. Ao fornecer valores para chaves, o nome da chave deve ser seguido por um de sinal de igualdade (=) e o valor da chave.

 Use as seções a seguir como auxílio para criar seu script para a recuperação autônoma do site. As tabelas listam as chaves de script de instalação disponíveis, seus valores correspondentes, se são necessárias, em que tipo de instalação são usadas e uma descrição breve da chave.

## <a name="recover-a-central-administration-site-unattended"></a>Recuperar um site de administração central de forma autônoma
 Use as informações a seguir para configurar um arquivo de script de Instalação autônoma para recuperação em um site de administração central.

 **Identificação**

-   **Nome da chave:** Action

    -   **Obrigatória:** Sim
    -   **Valores:** RecoverCCAR
    -   **Detalhes:** recupera um site de administração central


-   **Nome da chave:** CDLatest

    -   **Obrigatório:** Sim – somente ao usar a mídia da pasta CD.Latest.
    -   **Valores:** 1 qualquer valor diferente de 1 é considerado como não usando o CD.Latest.
    -   **Detalhes:** seu script deve incluir essa chave e o valor ao executar a instalação de uma mídia em uma pasta CD.Latest com a finalidade de instalar um site primário ou de administração central ou recuperar um site de administração central ou primário. Esse valor informa à instalação que a forma de mídia CD.Latest está sendo usada.

**RecoveryOptions**   
-   **Nome da chave:** ServerRecoveryOptions   

    -   **Obrigatória:** Sim
    -   **Valores:** 1, 2 ou 4  
         1 = Servidor do site de recuperação e SQL Server.   
         2 = Recuperar apenas o servidor do site.  
         4 = Recuperar apenas o SQL Server.
    -   **Detalhes:** especifica se a Instalação recuperará o servidor do site, o SQL Server ou ambos. As chaves associadas são necessárias quando o seguinte valor é definido para a configuração de ServerRecoveryOptions:  
        -   **Valor = 1** Você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.

             A chave **BackupLocation** é necessária quando o valor **10** é configurado para a chave **DatabaseRecoveryOptions** , que restaura o banco de dados do site por meio do backup.

        -   **Valor = 2** Você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.

        -   **Valor = 4** A chave **BackupLocation** é necessária quando o valor **10** é configurado para a chave **DatabaseRecoveryOptions** , que restaura o banco de dados do site por meio do backup.

-   **Nome da chave:** DatabaseRecoveryOptions

    -   **Obrigatória:** Talvez
    -   **Valores:** 10, 20, 40, 80  
         10 = Restaurar, por meio do backup, o banco de dados do site.  
         20 = Usar um banco de dados do site recuperado manualmente usando outro método.   
         40 = Criar um novo banco de dados para o site. Use essa opção quando não houver backup do banco de dados do site disponível. Os dados globais e do site são recuperados por meio da replicação de outros sites.  
         80 = Ignorar recuperação do banco de dados.
    -   **Detalhes:** especifica como a Instalação recuperará o banco de dados do site no SQL Server. Essa chave é necessária quando a configuração **ServerRecoveryOptions** tem o valor **1** ou **4**.


-   **Nome da chave:** ReferenceSite  

    -   **Obrigatória:** Talvez
    -   **Valores:** &lt;FQDNDoSiteDeReferência\>
    -   **Detalhes:** especificará o site primário de referência que o site de administração central usa para recuperar dados globais se o backup do banco de dados for mais antigo que o período de retenção do controle de alterações ou quando o site for recuperado sem backup.

         Quando um site de referência não é especificado e o backup é mais antigo que o período de retenção do controle de alterações, todos os sites primários são reinicializados com os dados restaurados por meio do site de administração central.

         Quando o site de referência não é especificado e o backup está dentro do período de retenção do controle de alterações, somente as alterações ocorridas desde o backup são replicadas dos sites primários. Quando houver alterações conflitantes de sites primários diferentes, o site de administração central usará a primeira alteração que receber.

         Essa chave é necessária quando a configuração **DatabaseRecoveryOptions** tem o valor **40**.

-   **Nome da chave:** SiteServerBackupLocation

    -   **Obrigatória:** Não
    -   **Valores:** &lt;CaminhoParaConjuntoDeBackupDoServidorDeSite\>
    -   **Detalhes:** especifica o caminho para o conjunto de backups do servidor de site. Essa chave é opcional quando a configuração **ServerRecoveryOptions** tem o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.


-   **Nome da chave:** BackupLocation

    -   **Obrigatória:** Talvez
    -   **Valores:** &lt;CaminhoParaConjuntoDeBackupDoBancoDeDadosDoSite\>
    -   **Detalhes:** especifica o caminho para o conjunto de backup do banco de dados do site. A chave **BackupLocation** é necessária quando o valor **1** ou **4** é configurado para a chave **ServerRecoveryOptions** , e o valor **10** é configurado para a chave **DatabaseRecoveryOptions** .


**Opções**

-   **Nome da chave:** ProductID
    -   **Obrigatória:** Sim
    -   **Valores:**   
         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
          Avaliação
    -   **Detalhes:** a chave do produto (Product Key) de instalação do Configuration Manager, incluindo os traços. Inserir **Eval** pode instalar a versão de avaliação do Configuration Manager.  


-   **Nome da chave:** SiteCode

    -   **Obrigatória:** Sim
    -   **Valores:** &lt;Código do site\>
    -   **Detalhes:** três caracteres alfanuméricos que identificam exclusivamente o site na hierarquia. É necessário especificar o código do site que foi usado pelo site antes da falha.


-   **Nome da chave:** SiteName

    -   **Obrigatória:** Sim
    -   **Valores:** SiteName
    -   **Detalhes:** descrição desse site.


-   **Nome da chave:** SMSInstallDir

    -   **Obrigatória:** Sim
    -   **Valores:** &lt;*ConfigMgrInstallationPath*>
    -   **Detalhes:** especifica a pasta de instalação dos arquivos de programa do Configuration Manager.
        > [!NOTE]   
        >  Você pode especificar o caminho novo ou o original para usar na instalação do Configuration Manager.

-   **Nome da chave:** SDKServer

    -   **Obrigatória:** Sim
    -   **Valores:** &lt;*FQDN do Provedor de SMS*>
    -   **Detalhes:** especifica o FQDN para o servidor que hospedará o Provedor de SMS. Você deve especificar o servidor que hospedou o Provedor de SMS antes da falha.

         Você pode configurar outros Provedores de SMS para o site após a instalação inicial.

-   **Nome da chave:** PrerequisiteComp

    -   **Obrigatória:** Sim
    -   **Valores:** 0 ou 1  
         0 = baixar   
         1 = já baixado
    -   **Detalhes:** especifica se os arquivos de pré-requisito da Instalação já foram baixados. Por exemplo, se você usar o valor 0, a Instalação baixará os arquivos.  


-   **Nome da chave:** PrerequisitePath

    -   **Obrigatória:** Sim
    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>
    -   **Detalhes:** especifica o caminho para os arquivos de pré-requisito da Instalação. Dependendo do valor do **PrerequisiteComp** , a Instalação usará esse caminho para armazenar arquivos baixados ou para localizar arquivos baixados anteriormente.

-   **Nome da chave:** AdminConsole

    -   **Obrigatória:** Talvez
    -   **Valores:** 0 ou 1 0 = não instalar   
         1 = instalar
    -   **Detalhes:** especifica se deseja instalar o console do Configuration Manager. Essa chave é necessária quando a configuração de **ServerRecoveryOptions** tem o valor **4**.


-   **Nome da chave:** JoinCEIP

    -   **Obrigatória:** Sim
    -   **Valores:** 0 ou 1  
         0 = não ingressar  
         1 = ingressar
    -   **Detalhes:** especifica se deve ingressar no Programa de Aperfeiçoamento da Experiência do Usuário.

**SQLConfigOptions**

-   **Nome da chave:** SQLServerName

    -   **Obrigatória:** Sim
    -   **Valores:** *&lt;NomeDoServidorSQL\>*
    -   **Detalhes:** o nome do servidor ou o nome da instância clusterizada executando o SQL Server que hospedará o banco de dados do site. Você deverá especificar o mesmo servidor que hospedou o banco de dados do site antes da falha.


-   **Nome da chave:** DatabaseName

    -   **Obrigatória:** Sim
    -   **Valores:** *&lt;SiteDatabaseName\>* ou *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*
    -   **Detalhes:** especifica o nome do banco de dados do SQL Server a ser criado ou usado para instalar o banco de dados do site de administração central. Você deverá especificar o mesmo nome do banco de dados usado antes da falha.

        > [!IMPORTANT]  
        >  Você deverá especificar o nome da instância e o nome do banco de dados do site se você não usar a instância padrão.

-   **Nome da chave:** SQLSSBPort

    -   **Obrigatória:** Não
    -   **Valores:** &lt;*SSBPortNumber*>
    -   **Detalhes:** especifica a porta do SQL Server Service Broker (SSB) usada pelo SQL Server. Normalmente, o SSB está configurado para usar a porta TCP 4022, mas há suporte para outras portas. Você deve especificar a mesma porta do SSB que foi usada antes da falha.

## <a name="recover-a-primary-site-unattended"></a>Recuperar um site primário autônomo
 Use as informações a seguir para configurar um arquivo de script de Instalação autônoma para recuperação em um site de administração central.

 **Identificação**

-   **Nome da chave:** Action

    -   **Obrigatória:** Sim
    -   **Valores:** RecoverPrimarySite
    -   **Detalhes:** recupera um site primário


-   **Nome da chave:** CDLatest

    -   **Obrigatório:** Sim – somente ao usar a mídia da pasta CD.Latest.
    -   **Valores:** 1 qualquer valor diferente de 1 é considerado como não usando o CD.Latest.
    -   **Detalhes:** seu script deve incluir essa chave e o valor ao executar a instalação de uma mídia em uma pasta CD.Latest com a finalidade de instalar um site primário ou de administração central ou recuperar um site de administração central ou primário. Esse valor informa à instalação que a forma de mídia CD.Latest está sendo usada.

**RecoveryOptions**

-   **Nome da chave:** ServerRecoveryOptions

    -   **Obrigatória:** Sim
    -   **Valores:** 1, 2 ou 4    
         1 = Servidor do site de recuperação e SQL Server.   
         2 = Recuperar apenas o servidor do site.  
         4 = Recuperar apenas o SQL Server.
    -   **Detalhes:** especifica se a Instalação recuperará o servidor do site, o SQL Server ou ambos. As chaves associadas são necessárias quando o seguinte valor é definido para a configuração de ServerRecoveryOptions:

        -   **Valor = 1** Você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.

             A chave **BackupLocation** é necessária quando o valor **10** é configurado para a chave **DatabaseRecoveryOptions** , que restaura o banco de dados do site por meio do backup.

        -   **Valor = 2** Você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.

        -   **Valor = 4** A chave **BackupLocation** é necessária quando o valor **10** é configurado para a chave **DatabaseRecoveryOptions** , que restaura o banco de dados do site por meio do backup.

-   **Nome da chave:** DatabaseRecoveryOptions

    -   **Obrigatória:** Talvez
    -   **Valores:** 10, 20, 40, 80  
         10 = Restaurar, por meio do backup, o banco de dados do site.  
         20 = Usar um banco de dados do site recuperado manualmente usando outro método.     
         40 = Criar um novo banco de dados para o site. Use essa opção quando não houver backup do banco de dados do site disponível. Os dados globais e do site são recuperados por meio da replicação de outros sites.  
         80 = Ignorar recuperação do banco de dados.
    -   **Detalhes:** especifica como a Instalação recuperará o banco de dados do site no SQL Server. Essa chave é necessária quando a configuração **ServerRecoveryOptions** tem o valor **1** ou **4**.


-   **Nome da chave:** SiteServerBackupLocation

    -   **Obrigatória:** Não
    -   **Valores:** &lt;CaminhoParaConjuntoDeBackupDoServidorDeSite\>
    -   **Detalhes:** especifica o caminho para o conjunto de backups do servidor de site. Essa chave é opcional quando a configuração **ServerRecoveryOptions** tem o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.     


-   **Nome da chave:** BackupLocation

    -   **Obrigatória:** Talvez
    -   **Valores:** &lt;CaminhoParaConjuntoDeBackupDoBancoDeDadosDoSite\>
    -   **Detalhes:** especifica o caminho para o conjunto de backup do banco de dados do site. A chave **BackupLocation** é necessária quando o valor **1** ou **4** é configurado para a chave **ServerRecoveryOptions** , e o valor **10** é configurado para a chave **DatabaseRecoveryOptions** .

**Opções**

-   **Nome da chave:** ProductID

    -   **Obrigatória:** Sim
    -   **Valores:**     
         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         Avaliação     
    -   **Detalhes:** a chave do produto (Product Key) de instalação do Configuration Manager, incluindo os traços. Inserir **Eval** pode instalar a versão de avaliação do Configuration Manager.  


-   **Nome da chave:** SiteCode

    -   **Obrigatória:** Sim
    -   **Valores:** &lt;Código do site\>
    -   **Detalhes:** três caracteres alfanuméricos que identificam exclusivamente o site na hierarquia. É necessário especificar o código do site que foi usado pelo site antes da falha.


-   **Nome da chave:** SiteName

    -   **Obrigatória:** Sim
    -   **Valores:** SiteName
    -   **Detalhes:** descrição desse site.


-   **Nome da chave:** SMSInstallDir

    -   **Obrigatória:** Sim
    -   **Valores:** &lt;*ConfigMgrInstallationPath*>
    -   **Detalhes:** especifica a pasta de instalação dos arquivos de programa do Configuration Manager.

        > [!NOTE]   
        >  Você pode especificar o caminho novo ou o original para usar na instalação do Configuration Manager.

-   **Nome da chave:** SDKServer

    -   **Obrigatória:** Sim
    -   **Valores:** &lt;*FQDN do Provedor de SMS*>
    -   **Detalhes:** especifica o FQDN para o servidor que hospedará o Provedor de SMS. Você deve especificar o servidor que hospedou o Provedor de SMS antes da falha.

         Você pode configurar outros Provedores de SMS para o site após a instalação inicial.

-   **Nome da chave:** PrerequisiteComp

    -   **Obrigatória:** Sim
    -   **Valores:** 0 ou 1    
         0 = baixar   
         1 = já baixado   
    -   **Detalhes:** especifica se os arquivos de pré-requisito da Instalação já foram baixados. Por exemplo, se você usar o valor 0, a Instalação baixará os arquivos.


-   **Nome da chave:** PrerequisitePath

    -   **Obrigatória:** Sim
    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>
    -   **Detalhes:** especifica o caminho para os arquivos de pré-requisito da Instalação. Dependendo do valor do **PrerequisiteComp** , a Instalação usará esse caminho para armazenar arquivos baixados ou para localizar arquivos baixados anteriormente.


-   **Nome da chave:** AdminConsole

    -   **Obrigatória:** Talvez
    -   **Valores:** 0 ou 1  
         0 = não instalar   
         1 = instalar  
    -   **Detalhes:** especifica se deseja instalar o console do Configuration Manager. Essa chave é necessária quando a configuração de **ServerRecoveryOptions** tem o valor **4**.

-   **Nome da chave:** JoinCEIP

    -   **Obrigatória:** Sim
    -   **Valores:** 0 ou 1    
         0 = não ingressar  
         1 = ingressar
    -   **Detalhes:** especifica se deve ingressar no Programa de Aperfeiçoamento da Experiência do Usuário.


**SQLConfigOptions**

-   **Nome da chave:** SQLServerName

    -   **Obrigatória:** Sim
    -   **Valores:** *&lt;NomeDoServidorSQL\>*
    -   **Detalhes:** o nome do servidor ou o nome da instância clusterizada executando o SQL Server que hospedará o banco de dados do site. Você deverá especificar o mesmo servidor que hospedou o banco de dados do site antes da falha.


-   **Nome da chave:** DatabaseName

    -   **Obrigatória:** Sim
    -   **Valores:** *&lt;SiteDatabaseName\>* ou *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*
    -   **Detalhes:** especifica o nome do banco de dados do SQL Server a ser criado ou usado para instalar o banco de dados do site de administração central. Você deverá especificar o mesmo nome do banco de dados usado antes da falha.

        > [!IMPORTANT]    
        >  Você deverá especificar o nome da instância e o nome do banco de dados do site se você não usar a instância padrão.

-   **Nome da chave:** SQLSSBPort

    -   **Obrigatória:** Não
    -   **Valores:** &lt;*SSBPortNumber*>
    -   **Detalhes:** especifica a porta do SQL Server Service Broker (SSB) usada pelo SQL Server. Normalmente, o SSB está configurado para usar a porta TCP 4022, mas há suporte para outras portas. Você deve especificar a mesma porta do SSB que foi usada antes da falha.

**ExpansionOption de hierarquia**

-   **Nome da chave:** CCARSiteServer

    -   **Obrigatória:** Talvez
    -   **Valores:** &lt;*SiteCodeForCentralAdministrationSite*>
    -   **Detalhes:** especifica o site de administração central ao qual o site primário será anexado quando ingressar na hierarquia do Configuration Manager. Essa configuração é necessária se o site primário foi anexado ao site de administração central antes da falha. É necessário especificar o código do site usado para o site de administração central antes da falha.

-   **Nome da chave:** CASRetryInterval

    -   **Obrigatória:** Não
    -   **Valores:** &lt;*Interval*>
    -   **Detalhes:** especifica o intervalo de repetição (em minutos) para tentar uma conexão ao site de administração central depois de a conexão falhar. Por exemplo, se a conexão com o site de administração central falhar, o site primário aguardará o número de minutos especificado para CASRetryInterval e tentará novamente se conectar.


-   **Nome da chave:** WaitForCASTimeout

    -   **Obrigatória:** Não
    -   **Valores:** &lt;*Timeout*>
    -   **Detalhes:** especifica o valor máximo do tempo limite (em minutos) para o site primário se conectar ao site de administração central. Por exemplo, se o site primário falhar ao conectar-se ao site de administração central, o site primário tentará novamente a conexão ao site de administração central baseado no CASRetryInterval até chegar ao período do WaitForCASTimeout. Você pode especificar um valor de 0 a 100.
