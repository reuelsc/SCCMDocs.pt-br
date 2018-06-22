---
title: Recuperação autônoma
titleSuffix: Configuration Manager
description: Use um script para recuperar seus sites no System Center Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 043a99b85614186cef910e6cf04cfa1cdd5e62c5
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32352111"
---
# <a name="unattended-site-recovery-for-configuration-manager"></a>Recuperação autônoma de sites para o Configuration Manager   

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Para executar uma [recuperação autônoma](/sccm/protect/understand/recover-sites#site-recovery-procedures) de um site de administração central ou de um site primário do Configuration Manager, crie um script de instalação autônoma e, em seguida, use a instalação com a opção de comando **/script**. O script fornece o mesmo tipo de informação solicitado pelo assistente de instalação, porém não há configurações padrão. Todos os valores devem ser especificados para as chaves de instalação que se aplicam ao tipo de recuperação usado.

 Para usar a opção de linha de comando de instalação /script, crie um arquivo de inicialização. Especifique esse nome de arquivo após a opção /script. O nome do arquivo não é importante, contanto que tenha a extensão de nome de arquivo **.ini**. Para fazer referência ao arquivo de inicialização de instalação na linha de comando, é necessário fornecer o caminho completo do arquivo. Por exemplo, se o arquivo de inicialização de instalação for nomeado como *setup.ini* e armazenado na *pasta C:\setup*, sua linha de comando será:

 `setup /script c:\setup\setup.ini`

> [!IMPORTANT]  
>  Você precisa ter direitos de Administrador para executar a instalação. Ao executar a instalação com o script autônomo, inicie o prompt de comando em um contexto de Administrador usando **Executar como administrador**.

 O script contém nomes de seção, nomes de chave e valores. Os nomes de chave da seção requeridos variam de acordo com o tipo de recuperação do script. A ordem das chaves dentro das seções, bem como a ordem das seções dentro do arquivo, não é importante. As chaves não diferenciam maiúsculas de minúsculas. Ao fornecer valores para chaves, o nome da chave deve ser seguido por um de sinal de igualdade (=) e o valor da chave.

 Use as seções a seguir como auxílio para criar seu script para a recuperação autônoma do site. As tabelas listam as chaves de script de instalação disponíveis, seus valores correspondentes, se são necessárias, em que tipo de instalação são usadas e uma descrição breve da chave.

## <a name="recover-a-central-administration-site-unattended"></a>Recuperar um site de administração central de forma autônoma
 Use as informações a seguir para configurar um arquivo de script de instalação autônoma para recuperar um site de administração central.

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
    -   **Detalhes:** especifica se a instalação recupera o servidor do site, o SQL Server ou ambos. As chaves associadas são necessárias quando o seguinte valor é definido para a configuração de ServerRecoveryOptions:  
        -   **Valor = 1** Você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.

             A chave **BackupLocation** é necessária quando o valor **10** é configurado para a chave **DatabaseRecoveryOptions** , que restaura o banco de dados do site por meio do backup.

        -   **Valor = 2** Você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.

        -   **Valor = 4** A chave **BackupLocation** é necessária quando o valor **10** é configurado para a chave **DatabaseRecoveryOptions** , que restaura o banco de dados do site por meio do backup.

-   **Nome da chave:** DatabaseRecoveryOptions

    -   **Obrigatória:** Talvez
    -   **Valores:**   
         - **10** = Restaurar o banco de dados do site por meio do backup.  
         - **20** = Usar um banco de dados do site recuperado manualmente usando outro método.   
         - **40** = Criar um novo banco de dados para o site. Use essa opção quando não houver backup do banco de dados do site disponível. Os dados globais e do site são recuperados por meio da replicação de outros sites.  
         - **80** = Ignorar a recuperação do banco de dados.
    -   **Detalhes:** especifica como a instalação recupera o banco de dados do site no SQL Server. Essa chave é necessária quando a configuração **ServerRecoveryOptions** tem o valor **1** ou **4**.


-   **Nome da chave:** ReferenceSite  

    -   **Obrigatória:** Talvez
    -   **Valores:** &lt;FQDNDoSiteDeReferência\>
    -   **Detalhes:** especifica o site primário de referência. Se o backup do banco de dados é mais antigo que o período de retenção do controle de alterações ou se o site é recuperado sem um backup, o site de administração central usa o site de referência para recuperar os dados globais.

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
         - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         - Avaliação
    -   **Detalhes:** a chave do produto (Product Key) de instalação do Configuration Manager, incluindo os traços. Inserir **Eval** pode instalar a versão de avaliação do Configuration Manager.  


-   **Nome da chave:** SiteCode

    -   **Obrigatória:** Sim
    -   **Valores:** &lt;Código do site\>
    -   **Detalhes:** três caracteres alfanuméricos que identificam exclusivamente o site na hierarquia. Especifique o código do site usado pelo site antes da falha.


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
    -   **Detalhes:** especifica o FQDN para o servidor que hospeda o Provedor de SMS. Especifique o servidor que hospedou o Provedor de SMS antes da falha.

         Você pode configurar outros Provedores de SMS para o site após a instalação inicial.

-   **Nome da chave:** PrerequisiteComp

    -   **Obrigatória:** Sim
    -   **Valores:** 0 ou 1  
         0 = baixar   
         1 = já baixado
    -   **Detalhes:** especifica se os arquivos de pré-requisito da instalação já foram baixados. Por exemplo, se você usar o valor 0, a instalação baixará os arquivos.  


-   **Nome da chave:** PrerequisitePath

    -   **Obrigatória:** Sim
    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>
    -   **Detalhes:** especifica o caminho para os arquivos de pré-requisito da instalação. Dependendo do valor de **PrerequisiteComp**, a instalação usará esse caminho para armazenar os arquivos baixados ou para localizar os arquivos baixados anteriormente.

-   **Nome da chave:** AdminConsole

    -   **Obrigatória:** Talvez
    -   **Valores:** 0 ou 1 0 = não instalar   
         1 = instalar
    -   **Detalhes:** especifica se deseja instalar o console do Configuration Manager. Essa chave é necessária quando a configuração de **ServerRecoveryOptions** tem o valor **4**.


-   **Nome da chave:** JoinCEIP   
    > [!Note]  
    > A partir do Configuration Manager versão 1802, o recurso Programa de Aperfeiçoamento da Experiência do Usuário é removido do produto.

    -   **Obrigatória:** Sim
    -   **Valores:** 0 ou 1  
         0 = não ingressar  
         1 = ingressar
    -   **Detalhes:** especifica se deve ingressar no Programa de Aperfeiçoamento da Experiência do Usuário.

**SQLConfigOptions**

-   **Nome da chave:** SQLServerName

    -   **Obrigatória:** Sim
    -   **Valores:** *&lt;NomeDoServidorSQL\>*
    -   **Detalhes:** o nome do servidor ou o nome da instância clusterizada que executa o SQL Server que hospeda o banco de dados do site. Especifique o mesmo servidor que hospedou o banco de dados do site antes da falha.


-   **Nome da chave:** DatabaseName

    -   **Obrigatória:** Sim
    -   **Valores:** *&lt;SiteDatabaseName\>* ou *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*
    -   **Detalhes:** especifica o nome do banco de dados do SQL Server a ser criado ou usado para instalar o banco de dados do site de administração central. Especifique o mesmo nome do banco de dados usado antes da falha.

        > [!IMPORTANT]  
        >  Se você não usar a instância padrão, precisará especificar o nome da instância e o nome do banco de dados do site.

-   **Nome da chave:** SQLSSBPort

    -   **Obrigatória:** Não
    -   **Valores:** &lt;*SSBPortNumber*>
    -   **Detalhes:** especifica a porta do SQL Server Service Broker (SSB) usada pelo SQL Server. Normalmente, o SSB está configurado para usar a porta TCP 4022, mas há suporte para outras portas. Especifique a mesma porta SSB usada antes da falha.

## <a name="recover-a-primary-site-unattended"></a>Recuperar um site primário autônomo
 Use as informações a seguir para configurar um arquivo de script de instalação autônoma para recuperar um site de administração central.

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
    -   **Detalhes:** especifica se a instalação recupera o servidor do site, o SQL Server ou ambos. As chaves associadas são necessárias quando o seguinte valor é definido para a configuração de ServerRecoveryOptions:

        -   **Valor = 1** Você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.

             A chave **BackupLocation** é necessária quando o valor **10** é configurado para a chave **DatabaseRecoveryOptions** , que restaura o banco de dados do site por meio do backup.

        -   **Valor = 2** Você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.

        -   **Valor = 4** A chave **BackupLocation** é necessária quando o valor **10** é configurado para a chave **DatabaseRecoveryOptions** , que restaura o banco de dados do site por meio do backup.

-   **Nome da chave:** DatabaseRecoveryOptions

    -   **Obrigatória:** Talvez
    -   **Valores:**   
         - **10** = Restaurar o banco de dados do site por meio do backup.  
         - **20** = Usar um banco de dados do site recuperado manualmente usando outro método.     
         - **40** = Criar um novo banco de dados para o site. Use essa opção quando não houver backup do banco de dados do site disponível. Os dados globais e do site são recuperados por meio da replicação de outros sites.  
         - **80** = Ignorar a recuperação do banco de dados.
    -   **Detalhes:** especifica como a instalação recupera o banco de dados do site no SQL Server. Essa chave é necessária quando a configuração **ServerRecoveryOptions** tem o valor **1** ou **4**.


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
         - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         - Avaliação     
    -   **Detalhes:** a chave do produto (Product Key) de instalação do Configuration Manager, incluindo os traços. Inserir **Eval** pode instalar a versão de avaliação do Configuration Manager.  


-   **Nome da chave:** SiteCode

    -   **Obrigatória:** Sim
    -   **Valores:** &lt;Código do site\>
    -   **Detalhes:** três caracteres alfanuméricos que identificam exclusivamente o site na hierarquia. Especifique o código do site usado pelo site antes da falha.


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
    -   **Detalhes:** especifica o FQDN para o servidor que hospeda o Provedor de SMS. Especifique o servidor que hospedou o Provedor de SMS antes da falha.

         Você pode configurar outros Provedores de SMS para o site após a instalação inicial.

-   **Nome da chave:** PrerequisiteComp

    -   **Obrigatória:** Sim
    -   **Valores:** 0 ou 1    
         0 = baixar   
         1 = já baixado   
    -   **Detalhes:** especifica se os arquivos de pré-requisito da instalação já foram baixados. Por exemplo, se você usar o valor 0, a instalação baixará os arquivos.


-   **Nome da chave:** PrerequisitePath

    -   **Obrigatória:** Sim
    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>
    -   **Detalhes:** especifica o caminho para os arquivos de pré-requisito da instalação. Dependendo do valor de **PrerequisiteComp**, a instalação usará esse caminho para armazenar os arquivos baixados ou para localizar os arquivos baixados anteriormente.


-   **Nome da chave:** AdminConsole

    -   **Obrigatória:** Talvez
    -   **Valores:** 0 ou 1  
         0 = não instalar   
         1 = instalar  
    -   **Detalhes:** especifica se deseja instalar o console do Configuration Manager. Essa chave é necessária quando a configuração de **ServerRecoveryOptions** tem o valor **4**.

-   **Nome da chave:** JoinCEIP  
    > [!Note]  
    > A partir do Configuration Manager versão 1802, o recurso Programa de Aperfeiçoamento da Experiência do Usuário é removido do produto.

    -   **Obrigatória:** Sim
    -   **Valores:** 0 ou 1    
         0 = não ingressar  
         1 = ingressar
    -   **Detalhes:** especifica se deve ingressar no Programa de Aperfeiçoamento da Experiência do Usuário.


**SQLConfigOptions**

-   **Nome da chave:** SQLServerName

    -   **Obrigatória:** Sim
    -   **Valores:** *&lt;NomeDoServidorSQL\>*
    -   **Detalhes:** o nome do servidor ou o nome da instância clusterizada que executa o SQL Server que hospeda o banco de dados do site. Especifique o mesmo servidor que hospedou o banco de dados do site antes da falha.


-   **Nome da chave:** DatabaseName

    -   **Obrigatória:** Sim
    -   **Valores:** *&lt;SiteDatabaseName\>* ou *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*
    -   **Detalhes:** especifica o nome do banco de dados do SQL Server a ser criado ou usado para instalar o banco de dados do site de administração central. Especifique o mesmo nome do banco de dados usado antes da falha.

        > [!IMPORTANT]    
        >  Se você não usar a instância padrão, precisará especificar o nome da instância e o nome do banco de dados do site.

-   **Nome da chave:** SQLSSBPort

    -   **Obrigatória:** Não
    -   **Valores:** &lt;*SSBPortNumber*>
    -   **Detalhes:** especifica a porta do SQL Server Service Broker (SSB) usada pelo SQL Server. Normalmente, o SSB está configurado para usar a porta TCP 4022, mas há suporte para outras portas. Especifique a mesma porta SSB usada antes da falha.

**ExpansionOption de hierarquia**

-   **Nome da chave:** CCARSiteServer

    -   **Obrigatória:** Talvez
    -   **Valores:** &lt;*SiteCodeForCentralAdministrationSite*>
    -   **Detalhes:** especifica o site de administração central ao qual o site primário é anexado quando ele ingressa na hierarquia do Configuration Manager. Essa configuração é necessária se o site primário foi anexado ao site de administração central antes da falha. Especifique o código do site usado para o site de administração central antes da falha.

-   **Nome da chave:** CASRetryInterval

    -   **Obrigatória:** Não
    -   **Valores:** &lt;*Intervalo*>
    -   **Detalhes:** especifica o intervalo de repetição (em minutos) para tentar uma conexão ao site de administração central depois de a conexão falhar. Por exemplo, se a conexão com o site de administração central falha, o site primário aguarda o número de minutos especificados para CASRetryInterval e, em seguida, tenta a conexão novamente.


-   **Nome da chave:** WaitForCASTimeout

    -   **Obrigatória:** Não
    -   **Valores:** &lt;*Timeout*>
    -   **Detalhes:** especifica o valor máximo do tempo limite (em minutos) para o site primário se conectar ao site de administração central. Por exemplo, se o site primário falhar ao conectar-se ao site de administração central, o site primário tentará novamente a conexão ao site de administração central baseado no CASRetryInterval até chegar ao período do WaitForCASTimeout. Você pode especificar um valor de 0 a 100.
