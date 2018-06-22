---
title: Variáveis de ação da sequência de tarefas
titleSuffix: Configuration Manager
description: Use variáveis de ação de sequência, como variáveis de configuração de rede, para definir configurações para uma única etapa em uma sequência de tarefas do Configuration Manager.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e2269031-0977-4f01-a274-420e00630575
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f66203e335524fa922ec1b6ab3dd4dc5fb917b0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32352576"
---
# <a name="task-sequence-action-variables-in-system-center-configuration-manager"></a>Variáveis de ação da sequência de tarefas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Variáveis de ação de sequência de tarefas especificam configurações que são usadas por uma única etapa em uma sequência de tarefas do System Center Configuration Manager. Por padrão, a etapa da sequência de tarefas inicializa suas configurações antes de ser executada. Essas configurações estão disponíveis apenas enquanto a etapa de sequência de tarefas associada está em execução. Em outras palavras, a sequência de tarefas adiciona o valor da variável de ação para o ambiente da sequência de tarefas antes da execução da etapa da sequência de tarefas. A sequência de tarefas remove o valor do ambiente após a etapa ser executada.  

## <a name="action-variable-example"></a>Exemplo de variável de ação  
 Por exemplo, você pode especificar um diretório de início para uma ação de linha de comando usando a etapa **Executar Linha de Comando** da sequência de tarefas. Esta etapa inclui uma propriedade **Iniciar em** , cujo valor padrão é armazenado no ambiente da sequência de tarefas como a variável **WorkingDirectory** . A variável de ambiente **WorkingDirectory** é inicializada antes da ação da sequência de tarefas **Executar Linha de Comando** . Durante a etapa **Executar Linha de Comando** , o valor **WorkingDirectory** pode ser acessado por meio da propriedade **Start In** . Depois que a etapa for concluída, a sequência de tarefas remove o valor da variável **WorkingDirectory** do ambiente. Se a sequência contiver outra etapa da sequência de tarefas **Executar Linha de Comando**, a sequência de tarefas inicializará uma nova variável **WorkingDirectory** e a definirá como o valor inicial para a etapa atual.  

 O valor *padrão* de uma variável de ação de sequência de tarefas está presente quando a etapa de sequência de tarefas é executada. Se você definir um valor *novo*, ele estará disponível para várias etapas na sequência de tarefas. Se você usar um dos métodos de criação da variável de sequência de tarefas para substituir o valor de uma variável interna, o novo valor permanecerá no ambiente e substituirá o valor padrão para as outras etapas na sequência de tarefas. Por exemplo, se uma etapa **Definir Variável de Sequência de Tarefas** for adicionada como a primeira etapa da sequência de tarefas e se ela definir a variável de ambiente **WorkingDirectory** como **C:\\**, as etapas **Executar Linha de Comando** na sequência de tarefas usarão o novo valor de diretório inicial.  

## <a name="action-variables-for-task-sequence-actions"></a>Variáveis de ação para ações de sequência de tarefas  
 As variáveis de sequência de tarefas do Configuration Manager são agrupadas segundo a ação da sequência de tarefas associada. Use os links a seguir para coletar informações sobre as variáveis de ação associadas a uma ação específica. As variáveis de sequência de tarefas controlam como é operada a ação de sequência da tarefas. A ação de sequência de tarefas lê e usa as variáveis que você marca como variáveis de entrada. Como alternativa, você pode usar a etapa [Definir Variável de Sequência de Tarefas](task-sequence-steps.md#BKMK_SetTaskSequenceVariable) ou o objeto TSEnvironment COM para definir as variáveis no tempo de execução. Somente a ação da sequência de tarefas marca variáveis como variáveis de saída. Ações que ocorrem posteriormente na sequência de tarefas leem essas variáveis de saída.  

> [!NOTE]  
>  Nem todas as ações da sequência de tarefas são associadas a um conjunto de variáveis de sequência de tarefas. Por exemplo, embora existam variáveis associadas à ação Habilitar BitLocker, não há variáveis associadas à ação Desabilitar BitLocker.  



###  <a name="BKMK_ApplyDataImage"></a> Aplicar Imagem de Dados   
 Para obter mais informações, consulte [Aplicar Imagem de Dados](task-sequence-steps.md#BKMK_ApplyDataImage). 

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDDataImageIndex<br /><br /> (entrada)|Especifica o valor de índice da imagem aplicado ao computador de destino.|  
|OSDWipeDestinationPartition<br /><br /> (entrada)|Especifica se é necessário excluir os arquivos localizados na partição de destino.<br /><br /> Valores válidos:<br /><br /> **true** (padrão)<br /><br /> **false**|  



###  <a name="BKMK_ApplyDriverPackage"></a> Aplicar pacote de driver   
Para obter mais informações, consulte [Aplicar Pacote de Drivers](task-sequence-steps.md#BKMK_ApplyDriverPackage).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDApplyDriverBootCriticalContentUniqueID<br /><br /> (entrada)|Especifica a ID de conteúdo do driver do dispositivo de armazenamento em massa a ser instalada do pacote de drivers. Se esta variável não for especificada, nenhum driver de armazenamento em massa será instalado.|  
|OSDApplyDriverBootCriticalINFFile<br /><br /> (entrada)|Especifica o arquivo INF do driver de armazenamento em massa a ser instalado.<br /><br /> <br /><br /> Esta variável de sequência de tarefas é obrigatória se OSDApplyDriverBootCriticalContentUniqueID estiver definido.|  
|OSDApplyDriverBootCriticalHardwareComponent<br /><br /> (entrada)|Especifica se um driver de dispositivo de armazenamento em massa estiver instalado, essa variável deverá ser **scsi**.<br /><br /> Esta variável de sequência de tarefas é obrigatória se OSDApplyDriverBootCriticalContentUniqueID estiver definido.|  
|OSDApplyDriverBootCriticalID<br /><br /> (entrada)|Especifica a ID crítica de inicialização do driver do dispositivo de armazenamento em massa a ser instalada. Esta ID é listada na seção **scsi** do arquivo txtsetup.oem do driver de dispositivo.<br /><br /> Esta variável de sequência de tarefas é obrigatória se OSDApplyDriverBootCriticalContentUniqueID estiver definido.|  
|OSDAllowUnsignedDriver<br /><br /> (entrada)|Especifica se é necessário configurar o Windows para permitir a instalação de drivers de dispositivo não assinados. Essa variável de sequência de tarefas não é usada ao implantar o Windows Vista e o sistema operacional posterior.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (padrão)|  



###  <a name="BKMK_ApplyNetworkSettings"></a> Aplicar Configurações de Rede   
 Para obter mais informações, consulte [Aplicar Configurações de Rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDAdapter<br /><br /> (entrada)|Esta variável de sequência de tarefas é uma variável de matriz. Cada elemento na matriz representa as configurações para um único adaptador de rede no computador. Acesse as configurações para cada adaptador combinando o nome de variável de matriz com o índice do adaptador de rede baseado em zero e o nome da propriedade.<br /><br />Se esta etapa configurar vários adaptadores de rede, ela definirá as propriedades para o segundo adaptador de rede usando o índice no nome da variável. Por exemplo, OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList, OSDAdapter1DNSDomain, OSDAdapter1WINSServerList e OSDAdapter1EnableWINS.<br /><br />Por exemplo, use os seguintes nomes de variáveis para definir as propriedades do primeiro adaptador de rede para esta etapa da sequência de tarefas a ser configurada:<br /><br /> <ul><li>**OSDAdapter0EnableDHCP**: **true** habilita o protocolo DHCP para o adaptador.<br />    Essa configuração é necessária. Os valores possíveis são: **True** ou **False**.</li><li>**OSDAdapter0IPAddressList**: lista delimitada por vírgula de endereços IP do adaptador. Essa propriedade será ignorada, a menos que **EnableDHCP** seja definido como **false**.<br />    Essa configuração é necessária.</li><li>**OSDAdapter0SubnetMask**: lista delimitada por vírgula de máscaras de sub-rede. Essa propriedade será ignorada, a menos que **EnableDHCP** seja definido como **false**.<br />    Essa configuração é necessária.</li><li>**OSDAdapter0Gateways**: lista delimitada por vírgula de endereços IP de gateway. Essa propriedade será ignorada, a menos que **EnableDHCP** seja definido como **false**.<br />    Essa configuração é necessária.</li><li>**OSDAdapter0DNSDomain**:domínio DNS (Sistema de Nomes de Domínio) do adaptador.</li><li>**OSDAdapter0DNSServerList**: lista delimitada por vírgula de servidores DNS do adaptador.<br />    Essa configuração é necessária.</li><li>**OSDAdapter0EnableDNSRegistration**: **true** para registrar o endereço IP do adaptador no DNS.</li><li>**OSDAdapter0EnableFullDNSRegistration**: **true** para registrar o endereço IP do adaptador no DNS com o nome DNS completo do computador.</li><li>**OSDAdapter0EnableIPProtocolFiltering**: **true** para habilitar a filtragem de protocolo IP no adaptador.</li><li>**OSDAdapter0IPProtocolFilterList**: lista delimitada por vírgula de protocolos que podem ser executados com IP. Essa propriedade será ignorada se **EnableIPProtocolFiltering** estiver definido como **false**.</li><li>**OSDAdapter0EnableTCPFiltering**: **true** para habilitar a filtragem de porta TCP do adaptador.</li><li>**OSDAdapter0TCPFilterPortList**: lista delimitada por vírgula de portas que receberão permissões de acesso para TCP. Essa propriedade será ignorada se **EnableTCPFiltering** estiver definido como **false**.</li><li>**OSDAdapter0TcpipNetbiosOptions**: opções de NetBIOS em TCP/IP. Os valores possíveis são:<br /><br /> <ul><li>**0**: usar as configurações de NetBIOS do servidor DHCP.</li><li>**1**: habilitar o NetBIOS por TCP/IP.</li><li>**2**: desabilitar o NetBIOS por TCP/IP.</li></ul></li><li>**OSDAdapter0EnableWINS**: **true** para usar o WINS para a resolução de nomes.</li><li>**OSDAdapter0WINSServerList**: lista delimitada por vírgula de endereços IP do servidor WINS. Essa propriedade será ignorada, a menos que **EnableWINS ativa** esteja definido como **true**.</li><li>**OSDAdapter0MacAddress**: endereço MAC usado para fazer a correspondência das configurações com o adaptador de rede física.</li><li>**OSDAdapter0Name**: nome da conexão de rede como ele aparece no programa do painel de controle das conexões de rede. O comprimento do nome está entre 0 e 255 caracteres.</li><li>**OSDAdapter0Index**: índice das configurações do adaptador de rede na matriz de configurações.<br /><br />     OSDAdapterCount=1<br />    OSDAdapter0EnableDHCP=FALSE<br />    OSDAdapter0IPAddressList=192.168.0.40<br />    OSDAdapter0SubnetMask=255.255.255.0<br />    OSDAdapter0Gateways=192.168.0.1<br />    OSDAdapter0DNSSuffix=contoso.com</li></ul>|  
|OSDAdapterCount<br /><br /> (entrada)|Especifica o número de adaptadores de rede instalados no computador de destino. Quando o valor **OSDAdapterCount** estiver definido, todas as opções de configuração para cada adaptador deverão ser definidas. Por exemplo, se você definir o valor de **OSDAdapterTCPIPNetbiosOptions** como um adaptador específico, todos os valores desse adaptador também precisarão ser configurados.<br /><br />Se esse valor não for especificado, todos os valores **OSDAdapter** serão ignorados.|  
|OSDDNSDomain<br /><br /> (entrada)|Especifica o servidor DNS primário que é usado pelo computador de destino.|  
|OSDDomainName<br /><br /> (entrada)|Especifica o nome do domínio do Windows ingressado pelo computador de destino. O valor especificado deve ser um nome de domínio válido dos Serviços de Domínio do Active Directory.|  
|OSDDomainOUName<br /><br /> (entrada)|Especifica o nome de formato RFC 1779 da UO (unidade organizacional) ingressada pelo computador de destino. Se especificado, o valor deve conter o caminho completo.<br /><br /> Exemplo:<br /><br /> **LDAP://OU=MinhaUo,DC=MeuDomínio,DC=MinhaEmpresa,DC=com**|  
|OSDEnableTCPIPFiltering<br /><br /> (entrada)|Especifica se a filtragem de TCP/IP está habilitada.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (padrão)|  
|OSDJoinAccount<br /><br /> (entrada)|Especifica a conta de rede que é usada para adicionar o computador de destino a um domínio do Windows.|  
|OSDJoinPassword<br /><br /> (entrada)|Especifica a senha de rede usada para adicionar o computador de destino a um domínio do Windows.|  
|OSDNetworkJoinType<br /><br /> (entrada)|Especifica se o computador de destino ingressa em um domínio ou grupo de trabalho do Windows.<br /><br /> **0** indica que o computador de destino ingressa em um domínio do Windows. **1** especifica que o computador ingressa em um grupo de trabalho.<br /><br /> Valores válidos:<br /><br /> **0**<br /><br /> **1**|  
|OSDDNSSuffixSearchOrder<br /><br /> (entrada)|Especifica a ordem de pesquisa DNS para o computador de destino.|  
|OSDWorkgroupName<br /><br /> (entrada)|Especifica o nome do grupo de trabalho ingressado pelo computador de destino.<br /><br /> Especifique esse valor ou o valor de **OSDDomainName**. O nome do grupo de trabalho pode ter, no máximo, 32 caracteres.<br /><br /> Exemplo:<br /><br /> **Accounting**|  



###  <a name="BKMK_ApplyOperatingSystem"></a> Aplicar Imagem de Sistema Operacional   
 Para obter mais informações, consulte [Apply Operating System Image](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDConfigFileName<br /><br /> (entrada)|Especifica o nome do arquivo de resposta da implantação de sistema operacional associado ao pacote de implantação de sistema operacional.|  
|OSDImageIndex<br /><br /> (entrada)|Especifica o valor de índice da imagem do arquivo WIM aplicado ao computador de destino.|  
|OSDInstallEditionIndex<br /><br /> (entrada)|Especifica a versão do Windows Vista ou do sistema operacional mais recente instalada. Se nenhuma versão for especificada, a Instalação do Windows determinará a versão que será instalada usando a chave do produto (Product Key) referenciada.<br /><br /> Use apenas um valor de 0 (zero) se as seguintes condições forem verdadeiras:<br /><br /> – Você está instalando um sistema operacional anterior ao Windows Vista<br />– Você está instalando uma edição de licença por volume do Windows Vista ou posterior, e nenhuma chave do produto (Product Key) foi especificada.<br /><br /> Valores válidos:<br /><br /> **0** (padrão)|  
|OSDTargetSystemDrive (saída)|Especifica a letra da unidade da partição que contém os arquivos do sistema operacional.|  



###  <a name="BKMK_ApplyWindowsSettings"></a> Aplicar as Configurações do Windows   
 Para mais informações, consulte [Aplicar as Configurações do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDComputerName<br /><br /> (entrada)|Especifica o nome do computador de destino.<br /><br /> Exemplo:<br /><br /> **%_SMSTSMachineName%** (padrão)|  
|OSDProductKey<br /><br /> (entrada)|Especifica a chave do produto (Product Key) do Windows. O valor especificado deve estar entre 1 e 255 caracteres.|  
|OSDRegisteredUserName<br /><br /> (entrada)|Especifica o nome de usuário registrado padrão no novo sistema operacional. O valor especificado deve estar entre 1 e 255 caracteres.|  
|OSDRegisteredOrgName<br /><br /> (entrada)|Especifica o nome da organização registrada padrão no novo sistema operacional. O valor especificado deve estar entre 1 e 255 caracteres.|  
|OSDTimeZone<br /><br /> (entrada)|Especifica a configuração de fuso horário padrão usada no novo sistema operacional.|  
|OSDServerLicenseMode<br /><br /> (entrada)|Especifica o modo de licença do Windows Server que é usado.<br /><br /> Valores válidos:<br /><br /> **PerSeat**<br /><br /> **PerServer**|  
|OSDServerLicenseConnectionLimit<br /><br /> (entrada)|Especifica o número máximo de conexões permitidas. O número especificado deve estar no intervalo entre 5 e 9.999 conexões.|  
|OSDRandomAdminPassword<br /><br /> (entrada)|Especifica uma senha gerada aleatoriamente para a conta de administrador no novo sistema operacional. Se definido como **true**, a Instalação do Windows desabilita a conta de administrador local no computador de destino. Se definido como **false**, a Instalação do Windows habilita a conta de administrador local no computador de destino e define a senha da conta para o valor de **OSDLocalAdminPassword**.<br /><br /> Valores válidos:<br /><br /> **true** (padrão)<br /><br /> **false**|  
|OSDLocalAdminPassword<br /><br /> (entrada)|Especifica a senha do administrador local. Se você habilitar **Gerar a senha de administrador local aleatoriamente e desabilitar a conta em todas as plataformas compatíveis**, esta etapa ignorará esta variável. O valor especificado deve estar entre 1 e 255 caracteres.|  



###  <a name="BKMK_AutoApplyDrivers"></a> Drivers de Aplicação Automática   
 Para mais informações, consulte [Aplicar Drivers Automaticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDAutoApplyDriverCategoryList<br /><br /> (entrada)|Uma lista delimitada por vírgulas de IDs exclusivas de categorias do catálogo de drivers. A etapa **Aplicação Automática de Driver** considera apenas os drivers em pelo menos uma das categorias especificadas. Esse valor é opcional e não é definido por padrão. Obtenha as IDs de categoria disponíveis enumerando a lista de objetos **SMS_CategoryInstance** no site.|  
|OSDAllowUnsignedDriver<br /><br /> (entrada)|Especifica se o Windows está configurado para permitir que drivers de dispositivo não assinados sejam instalados. Essa variável de sequência de tarefas não é usada ao implantar o Windows Vista e sistemas operacionais posteriores.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (padrão)|  
|OSDAutoApplyDriverBestMatch<br /><br /> (entrada)|Se houver vários drivers de dispositivo no catálogo de drivers que são compatíveis com um dispositivo de hardware, essa variável determinará a ação da etapa. Se definido como **true**, a etapa instala somente o melhor driver de dispositivo. Se **false**, a etapa instala todos os drivers de dispositivo compatível e o Windows escolhe o melhor driver a ser usado.<br /><br /> Valores válidos:<br /><br /> **true** (padrão)<br /><br /> **false**|  
|SMSTSDriverRequestConnectTimeOut|Ao solicitar o catálogo de drivers, essa variável é o número de segundos que a sequência de tarefas aguarda pela conexão do servidor HTTP. Se a conexão demorar mais do que a configuração de tempo limite, a sequência de tarefas cancelará a solicitação. Por padrão, o tempo limite é definido como **60** segundos.|  
|SMSTSDriverRequestReceiveTimeOut|Ao solicitar o catálogo de drivers, essa variável é o número de segundos que a sequência de tarefas aguarda uma resposta. Se a conexão demorar mais do que a configuração de tempo limite, a sequência de tarefas cancelará a solicitação. Por padrão, o tempo limite é definido como **480** segundos.|
|SMSTSDriverRequestResolveTimeOut|Ao solicitar o catálogo de drivers, essa variável é o número de segundos que a sequência de tarefas aguarda uma resolução de nome HTTP. Se a conexão demorar mais do que a configuração de tempo limite, a sequência de tarefas cancelará a solicitação. Por padrão, o tempo limite é definido como **60** segundos.|
|SMSTSDriverRequestSendTimeOut|Ao enviar uma solicitação para o catálogo de drivers, essa variável é o número de segundos que a sequência de tarefas aguarda para enviar a resposta. Se a solicitação demorar mais do que a configuração de tempo limite, a sequência de tarefas cancelará a solicitação. Por padrão, o tempo limite é definido como **60** segundos.|



###  <a name="BKMK_CaptureNetworkSettings"></a> Capturar configurações da rede   
 Para obter mais informações, consulte [Capturar Configurações de Rede](task-sequence-steps.md#BKMK_CaptureNetworkSettings).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDMigrateAdapterSettings<br /><br /> (entrada)|Especifica se as informações de configurações do adaptador de rede (TCP/IP, DNS e WINS) são capturadas.<br /><br /> Exemplos:<br /><br /> **true** (padrão)<br /><br /> **false**|  
|OSDMigrateNetworkMembership<br /><br /> (entrada)|Especifica se as informações de associação de grupo de trabalho ou de domínio são migradas como parte da implantação de sistema operacional.<br /><br /> Exemplos:<br /><br /> **true** (padrão)<br /><br /> **false**|  



###  <a name="BKMK_CaptureOperatingSystemImage"></a> Capturar imagem do sistema operacional   
 Para obter mais informações, consulte [Capturar Imagem do Sistema Operacional](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDCaptureAccount<br /><br /> (entrada)|Especifica um nome de conta do Windows que tem permissões para armazenar a imagem capturada em um compartilhamento de rede.|  
|OSDCaptureAccountPassword<br /><br /> (entrada)|Especifica a senha da conta do Windows usada para armazenar a imagem capturada em um compartilhamento de rede.|  
|OSDCaptureDestination<br /><br /> (entrada)|Especifica o local em que a imagem capturada do sistema operacional é salva. O comprimento máximo do nome do diretório é de 255 caracteres.|  
|OSDImageCreator<br /><br /> (entrada)|Um nome opcional do usuário que criou a imagem. Este nome é armazenado no arquivo WIM. O comprimento máximo do nome de usuário é de 255 caracteres.|  
|OSDImageDescription<br /><br /> (entrada)|Uma descrição opcional definida pelo usuário da imagem capturada do sistema operacional. Essa descrição é armazenada no arquivo WIM. O comprimento máximo da descrição é de 255 caracteres.|  
|OSDImageVersion<br /><br /> (entrada)|Um número de versão opcional definido pelo usuário para atribuir a imagem capturada do sistema operacional. Esse número de versão é armazenado no arquivo WIM. Esse valor pode ser qualquer combinação de letras com um comprimento máximo de 32 caracteres.|  
|OSDTargetSystemRoot<br /><br /> (entrada)|Especifica o caminho para o diretório do Windows do sistema operacional instalado no computador de referência. Este sistema operacional é confirmado como um sistema operacional com suporte para captura pelo Configuration Manager.|  



###  <a name="BKMK_CaptureUserState"></a> Capturar Estado do Usuário   
 Para obter mais informações, consulte [Capturar Estado do Usuário](task-sequence-steps.md#BKMK_CaptureUserState).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrada)|O UNC ou nome de caminho local da pasta em que o estado de usuário foi salvo. Nenhum padrão.|  
|OSDMigrateAdditionalCaptureOptions<br /><br /> (entrada)|Opções de linha de comando da USMT (Ferramenta de Migração do Usuário) que a sequência de tarefas usa para capturar o estado do usuário. A etapa não expõe estas configurações no editor de sequência de tarefas. Especifique essas opções como uma cadeia de caracteres, que acrescenta a sequência de tarefas à linha de comando USMT gerada automaticamente.<br /><br />As opções do USMT especificadas com essa variável de sequência de tarefas não são validadas quanto à precisão antes da execução da sequência de tarefas.|  
|OSDMigrateMode<br /><br /> (entrada)|Permite que você personalize os arquivos que são capturados pelo USMT. Se essa variável for definida como **Simple**, a sequência de tarefas usará somente os arquivos padrão de configuração do USMT. Se for definida como **Advanced**, a variável de sequência de tarefas OSDMigrateConfigFiles especificará os arquivos de configuração que o USMT usa.<br /><br /> Valores válidos:<br /><br /> **Simple**<br /><br /> **Advanced**|  
|OSDMigrateConfigFiles<br /><br /> (entrada)|Especifica os arquivos de configuração usados para controlar a captura de perfis de usuário. Essa variável será usada apenas se OSDMigrateMode estiver definido como Avançado. Esse valor de lista delimitado por vírgulas é definido para executar a migração personalizada de perfil do usuário.<br /><br /> Exemplo: miguser.xml, migsys.xml, migapps.xml|  
|OSDMigrateContinueOnLockedFiles<br /><br /> (entrada)|Se a USMT não puder capturar alguns arquivos, essa variável permitirá que a captura de estado do usuário prossiga.<br /><br /> Valores válidos:<br /><br /> **true** (padrão)<br /><br /> **false**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (entrada)|Habilita o log detalhado para USMT.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (padrão)|  
|OSDMigrateSkipEncryptedFiles<br /><br /> (entrada)|Especifica se os arquivos criptografados serão capturados.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (padrão)|  
|_OSDMigrateUsmtPackageID<br /><br /> (entrada)|Especifica a ID do pacote do Configuration Manager que contém os arquivos do USMT. Esta variável é obrigatória.|  



###  <a name="BKMK_CaptureWindowsSettings"></a> Capturar Configurações do Windows   
 Para obter mais informações, consulte [Capturar Configurações do Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDMigrateComputerName<br /><br /> (entrada)|Especifica se o nome do computador é migrado.<br /><br /> Valores válidos:<br /><br /> **true** (padrão)<br /><br /> **false**<br /><br /> Se o valor for **true**, a variável OSDComputerName será definida como o nome NetBIOS do computador.|  
|OSDComputerName<br /><br /> (saída)|Defina como o nome NetBIOS do computador. O valor será definido somente se a variável OSDMigrateComputerName for definida como **true**.|  
|OSDMigrateRegistrationInfo<br /><br /> (entrada)|Especifica se a etapa migra as informações do usuário e da organização.<br /><br /> Valores válidos:<br /><br /> **true** (padrão)<br /><br /> **false**<br /><br /> Se o valor for **true**, a variável OSDRegisteredOrgName será definida como o nome da organização registrada do computador.|  
|OSDRegisteredOrgName<br /><br /> (saída)|Defina como o nome da organização registrada do computador. O valor será definido somente se a variável OSDMigrateRegistrationInfo for definida como **true**.|  
|OSDMigrateTimeZone<br /><br /> (entrada)|Especifica se o fuso horário do computador é migrado.<br /><br /> Valores válidos:<br /><br /> **true** (padrão)<br /><br /> **false**<br /><br /> Se o valor for **true**, a variável OSDTimeZone será definida como o fuso horário do computador.|  
|OSDTimeZone<br /><br /> (saída)|Defina como o fuso horário do computador. O valor será definido somente se a variável OSDMigrateTimeZone for definida como **true**.|  



###  <a name="BKMK_ConnecttoNetworkFolder"></a> Conectar à Pasta de Rede   
 Para obter mais informações, consulte [Conectar à Pasta de Rede](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|SMSConnectNetworkFolderAccount<br /><br /> (entrada)|Especifica a conta de administrador usada para se conectar ao compartilhamento de rede.|  
|SMSConnectNetworkFolderDriveLetter<br /><br /> (entrada)|Especifica a letra da unidade da rede à qual se conectar. Esse valor é opcional; se não for especificado, a conexão de rede não será mapeada para uma letra da unidade. Se esse valor for especificado, o valor deverá estar no intervalo de D: a Z:. Além disso, não use X, pois essa é a letra da unidade usada pelo Windows PE durante a fase do Windows PE.<br /><br /> Exemplos:<br /><br /> **D:**<br /><br /> **E:**|  
|SMSConnectNetworkFolderPassword<br /><br /> (entrada)|Especifica a senha de rede usada para se conectar ao compartilhamento de rede.|  
|SMSConnectNetworkFolderPath<br /><br /> (entrada)|Especifica o caminho de rede para a conexão.<br /><br /> Exemplo:<br /><br /> **\\\servername\sharename**|  



###  <a name="BKMK_EnableBitLocker"></a> Habilitar BitLocker   
 Para mais informações, consulte [Habilitar BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDBitLockerRecoveryPassword<br /><br /> (entrada)|Em vez de gerar uma senha aleatória de recuperação, a ação da sequência de tarefas **Habilitar BitLocker** usa o valor especificado como a senha de recuperação. O valor deve ser uma senha de recuperação do BitLocker numérica e válida.|  
|OSDBitLockerStartupKey<br /><br /> (entrada)|Em vez de gerar uma chave de inicialização aleatória para a opção de gerenciamento de chaves **Chave de Inicialização somente em USB**, a etapa **Habilitar BitLocker** usa o TPM (Trusted Platform Module) como a chave de inicialização. O valor deve ser uma chave de inicialização do BitLocker válida, codificada em Base64 e de 256 bits.|  



###  <a name="BKMK_FormatPartitionDisk"></a> Formatar e Particionar Disco   
 Para mais informações, consulte [Formatar e Particionar Disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDDiskIndex<br /><br /> (entrada)|Especifica o número de discos físicos a ser particionados.|  
|OSDDiskpartBiosCompatibilityMode<br /><br /> (entrada)|Ao particionar o disco rígido para compatibilidade com certos tipos de BIOS, essa variável especifica se as otimizações de alinhamento de cache devem ser desabilitadas. Isso é necessário durante a implantação dos sistemas operacionais Windows XP ou Windows Server 2003. Para obter mais informações, veja o [artigo 931760](http://go.microsoft.com/fwlink/?LinkId=134081) e o [artigo 931761](http://go.microsoft.com/fwlink/?LinkId=134082) na Base de Dados de Conhecimento Microsoft.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (padrão)| 
|OSDGPTBootDisk<br /><br /> (entrada)|Especifica se uma partição EFI deve ser criada em um disco rígido GPT. Computadores baseados em EFI usam essa partição como o disco de inicialização.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (padrão)|  
|OSDPartitions<br /><br /> (entrada)|Especifica uma matriz de configurações de partição; veja o tópico sobre o SDK para acessar variáveis de matriz no ambiente da sequência de tarefas.<br /><br /> Esta variável de sequência de tarefas é uma variável de matriz. Cada elemento na matriz representa as configurações para uma única partição no disco rígido. Acesse as configurações definidas para cada partição combinando o nome de variável de matriz com o número de partição de disco baseado em zero e o nome da propriedade.<br /><br /> Por exemplo, use os seguintes nomes de variáveis para definir as propriedades para a primeira partição que esta etapa cria no disco rígido:<br /><br /> - **OSDPartitions0Type**: especifica o tipo de partição. Esta propriedade é necessária. Os valores válidos são **Primary**, **Extended**, **Logical** e **Hidden**.<br />-   **OSDPartitions0FileSystem**: especifica o tipo de sistema de arquivos a ser usado ao formatar a partição. Esta propriedade é opcional. Se você não especificar um sistema de arquivos, a etapa não formatará a partição. Os valores válidos são **FAT32** e **NTFS**.<br />-   **OSDPartitions0Bootable**: especifica se a partição é inicializável. Esta propriedade é necessária. Se esse valor for definido como **TRUE** para discos MBR, essa etapa marcará esta partição como ativa.<br />-   **OSDPartitions0QuickFormat**: especifica o tipo de formato usado. Esta propriedade é necessária. Se esse valor for definido como **TRUE**, a etapa executará uma formatação rápida. Caso contrário, a etapa executa uma formatação completa.<br />-   **OSDPartitions0VolumeName**: especifica o nome atribuído ao volume quando ele é formatado. Esta propriedade é opcional.<br />-   **OSDPartitions0Size**: especifica o tamanho da partição. As unidades são especificadas pela variável **OSDPartitions0SizeUnits** . Esta propriedade é opcional. Se esta propriedade não for especificada, a partição será criada usando todo o espaço livre restante.<br />-   **OSDPartitions0SizeUnits**: a etapa usa essas unidades para interpretar a variável **OSDPartitions0Size**. Esta propriedade é opcional. Os valores válidos são **MB** (padrão), **GB** e **Percent**.<br />-   **OSDPartitions0VolumeLetterVariable**: quando essa etapa cria partições, ela sempre usa a próxima letra da unidade disponível no Windows PE. Use essa propriedade opcional para especificar o nome de outra variável de sequência de tarefas. A etapa usa essa variável para salvar a nova letra da unidade para referência futura.<br /><br />Se você definir várias partições com esta ação da sequência de tarefas, as propriedades da segunda partição serão definidas usando o índice no nome da variável. Por exemplo: **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat** e **OSDPartitions1VolumeName**.|  
|OSDPartitionStyle<br /><br /> (entrada)|Especifica o estilo de partição a ser usado ao particionar o disco. **MBR** indica o estilo de partição do registro mestre de inicialização, e **GPT** indica o estilo de Tabela de Partição GUID.<br /><br /> Valores válidos:<br /><br /> **GPT**<br /><br /> **MBR**|  



###  <a name="BKMK_InstallApplication"></a> Instalar Aplicativo   
 Para obter mais informações, consulte [Instalar Aplicativo](task-sequence-steps.md#BKMK_InstallApplication).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação<br /><br /> (entrada)|Descrição|  
|----------------------------------------|-----------------|  
| TSErrorOnWarning |Especifique se o mecanismo de sequência de tarefas considera um aviso detectado como um erro durante essa etapa. A sequência de tarefas define a variável _TSAppInstallStatus de acordo com o **Aviso** quando um ou mais aplicativos, ou uma dependência necessária, não foram instalados porque eles não cumpriram um requisito. Quando você define essa variável como **True** e a sequência de tarefas define _TSAppInstallStatus como Aviso, o resultado é um erro. Um valor de **False** é o comportamento padrão.| 
|SMSTSMPListRequestTimeoutEnabled|Use essa variável para permitir que solicitações MPList repetidas atualizem o cliente se ele não estiver na intranet. <br />Por padrão, essa variável é definida como **True**. Quando os clientes estão na internet, defina essa variável como **False** para evitar atrasos desnecessários. Essa variável é aplicável somente às etapas da sequência de tarefas Instalar Aplicativo e Instalar Atualizações de Software.|  
|SMSTSMPListRequestTimeout|Especifique quantos milissegundos uma sequência de tarefas espera antes de tentar instalar novamente um aplicativo após uma falha ao recuperar a lista de ponto de gerenciamento dos serviços de localização. Por padrão, a sequência de tarefas espera **60000** milissegundos (60 segundos) antes de tentar executar novamente a etapa, tentando novamente até três vezes.|  



###  <a name="BKMK_InstallSoftwareUpdates"></a> Instalar Atualizações de Software   
Para obter mais informações, consulte [Instalar Atualizações de Software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação<br /><br /> (entrada)|Descrição|  
|----------------------------------------|-----------------|  
|SMSInstallUpdateTarget<br /><br /> (entrada)|Especifica se é necessário instalar todas as atualizações ou apenas as atualizações obrigatórias.<br /><br /> Valores válidos:<br /><br /> **Todos**<br /><br /> **Mandatory**|  
|SMSTSSoftwareUpdateScanTimeout| Controle o tempo limite para a verificação de atualizações de software durante essa etapa. Por exemplo, aumente o valor se você espera ter várias atualizações durante a verificação. O valor padrão é **1800** segundos (30 minutos). O valor da variável é definido em segundos. |
|SMSTSWaitForSecondReboot|Essa variável opcional da sequência de tarefas controla o comportamento do cliente quando uma instalação de atualização de software exige duas reinicializações. Defina essa variável antes desta etapa para evitar a falha da sequência de tarefas devido à segunda reinicialização depois da instalação de atualização de software.<br /><br /> Defina o valor de SMSTSWaitForSecondReboot para especificar por quantos segundos a sequência de tarefas fica em pausa depois que o computador é reiniciado. Permita que haja tempo suficiente em caso de uma segunda reinicialização. <br />Por exemplo, se você definir SMSTSWaitForSecondReboot para 600, a sequência de tarefas será pausada por 10 minutos após uma reinicialização antes da execução das etapas adicionais. Essa variável é útil quando uma única etapa de sequência de tarefas Instalar Atualizações de Software instala centenas de atualizações de software.| 
|SMSTSMPListRequestTimeoutEnabled|Use essa variável para permitir que solicitações MPList repetidas atualizem o cliente se ele não estiver na intranet. <br />Por padrão, essa variável é definida como **True**. Quando os clientes estão na internet, defina essa variável como **False** para evitar atrasos desnecessários. Essa variável é aplicável somente às etapas da sequência de tarefas Instalar Aplicativo e Instalar Atualizações de Software.|  
|SMSTSMPListRequestTimeout|Especifique quantos milissegundos uma sequência de tarefas espera antes de tentar instalar novamente uma atualização de software após uma falha ao recuperar a lista de ponto de gerenciamento dos serviços de localização. Por padrão, a sequência de tarefas espera **60000** milissegundos (60 segundos) antes de tentar executar novamente a etapa, tentando novamente até três vezes.|  



###  <a name="BKMK_JoinDomainWorkgroup"></a> Ingressar no Domínio ou Grupo de Trabalho   
 Para obter mais informações, consulte [Ingressar no Domínio ou Grupo de Trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDJoinAccount<br /><br /> (entrada)|Especifica a conta usada pelo computador de destino para ingressar no domínio do Active Directory. Essa variável é necessária ao ingressar em um domínio.|  
|OSDJoinDomainName<br /><br /> (entrada)|Especifica o nome de um domínio do Active Directory ingressado pelo computador de destino. O tamanho do nome de domínio precisa ter entre 1 e 255 caracteres.|  
|OSDJoinDomainOUName<br /><br /> (entrada)|Especifica o nome de formato RFC 1779 da UO (unidade organizacional) ingressada pelo computador de destino. Se especificado, o valor deve conter o caminho completo. O tamanho do nome da UO precisa ter entre 0 e 32.767 caracteres. Esse valor não será definido se a variável **OSDJoinType** for definida como **1** (ingressar no grupo de trabalho).<br /><br /> Exemplo:<br /><br /> **LDAP://OU=MinhaUo,DC=MeuDomínio,DC=MinhaEmpresa,DC=com**|  
|OSDJoinPassword<br /><br /> (entrada)|Especifica a senha de rede usada pelo computador de destino para ingressar no domínio do Active Directory. Se o ambiente da sequência de tarefas não incluir essa variável, a Instalação do Windows tentará usar uma senha em branco. Se a variável **OSDJoinType** for definida como **0** (ingressar no domínio), esse valor será obrigatório.|  
|OSDJoinSkipReboot<br /><br /> (entrada)|Especifica se é necessário ignorar a reinicialização depois que o computador de destino ingressar no domínio ou no grupo de trabalho.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false**|  
|OSDJoinType<br /><br /> (entrada)|Especifica se o computador de destino ingressa em um domínio ou grupo de trabalho do Windows. Para ingressar o computador de destino em um domínio do Windows, especifique **0**. Para ingressar o computador de destino em um grupo de trabalho, especifique **1**.<br /><br /> Valores válidos:<br /><br /> **0**<br /><br /> **1**|  
|OSDJoinWorkgroupName<br /><br /> (entrada)|Especifica o nome de um grupo de trabalho ingressado pelo computador de destino. O comprimento do nome do grupo de trabalho deve estar entre 1 e 32 caracteres.<br /><br /> Exemplo:<br /><br /> **Accounting**|  



###  <a name="BKMK_PrepareWindowsCapture"></a> Preparar Windows para Captura   
 Para obter mais informações, consulte [Preparar o Windows para Captura](task-sequence-steps.md#BKMK_PrepareWindowsforCapture).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDBuildStorageDriverList<br /><br /> (entrada)|Especifica se o Sysprep compila uma lista de drivers de dispositivo de armazenamento em massa. Essa configuração se aplica somente ao Windows XP e Windows Server 2003. Essa variável popula a seção [SysprepMassStorage] de sysprep.inf com informações sobre todos os drivers de armazenamento em massa que são compatíveis com a imagem a ser capturada.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (padrão)|  
|OSDKeepActivation<br /><br /> (entrada)|Especifica se o sysprep redefine o sinalizador de ativação do produto.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (padrão)|  
|OSDTargetSystemRoot<br /><br /> (saída)|Especifica o caminho para o diretório do Windows do sistema operacional instalado no computador de referência. Este sistema operacional é confirmado como um sistema operacional com suporte para captura pelo Configuration Manager.|  



###  <a name="BKMK_ReleaseStateStore"></a> Liberar Armazenamento de Estado   
 Para mais informações, consulte as [Notas de Versão da Store](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrada)|O UNC ou nome de caminho local d local do qual o estado de usuário foi restaurado. Esse valor é usado pelas ações da sequência de tarefas **Capturar Estado de Usuário** e **Restaurar Estado de Usuário** .|  



###  <a name="BKMK_RequestState"></a> Solicitar Armazenamento de Estado   
  Para mais informações, consulte as [Notas de Versão da Store](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDStateFallbackToNAA<br /><br /> (entrada)|Quando a conta do computador não consegue se conectar ao ponto de migração de estado, essa variável especifica se a sequência de tarefas voltará a usar a conta de acesso de rede (NAA).<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (padrão)|  
|OSDStateSMPRetryCount<br /><br /> (entrada)|Especifica o número de vezes que a etapa da sequência de tarefas tentará localizar um ponto de migração de estado antes da etapa falhar. A contagem especificada deve estar entre 0 e 600.|  
|OSDStateSMPRetryTime<br /><br /> (entrada)|Especifica o número de segundos durante os quais a etapa da sequência de tarefas aguarda entre as novas tentativas. O número de segundos pode ter, no máximo, 30 caracteres.|  
|OSDStateStorePath<br /><br /> (saída)|O caminho UNC para a pasta no ponto de migração de estado em que o estado de usuário foi armazenado.|  



###  <a name="BKMK_RestartComputer"></a> Reiniciar Computador   
 Para mais informações, consulte [Reiniciar Computer](task-sequence-steps.md#BKMK_RestartComputer).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|SMSRebootMessage<br /><br /> (entrada)|Especifica a mensagem a ser exibida para os usuários antes de reiniciar o computador de destino. Se essa variável não for definida, o texto da mensagem padrão será exibido. A mensagem especificada não deve exceder 512 caracteres.<br /><br /> Exemplo:<br /><br /> **Salve seu trabalho antes da reinicialização do computador.**|  
|SMSRebootTimeout<br /><br /> (entrada)|Especifica o número de segundos que o aviso é exibido para o usuário antes da reinicialização do computador. Especifique zero segundo para indicar que nenhuma mensagem de reinicialização é exibida.<br /><br /> Exemplos:<br /><br /> **0** (padrão)<br /><br />  **60**|  



###  <a name="BKMK_RestoreUserState"></a> Restaurar Estado do Usuário   
  Para obter mais informações, consulte [Restaurar Estado do Usuário](task-sequence-steps.md#BKMK_RestoreUserState).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrada)|O UNC ou nome de caminho local da pasta do qual o estado de usuário foi restaurado.|  
|OSDMigrateContinueOnRestore<br /><br /> (entrada)|Continue o processo, mesmo se a USMT não puder restaurar alguns arquivos.<br /><br /> Valores válidos:<br /><br /> **true** (padrão)<br /><br /> **false**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (entrada)|Habilita o log detalhado para a ferramenta USMT. Esse valor é exigido pela ação.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (padrão)|  
|OSDMigrateLocalAccounts<br /><br /> (entrada)|Especifica se a conta do computador local é restaurada.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (padrão)|  
|OSDMigrateLocalAccountPassword<br /><br /> (entrada)|Se a variável **OSDMigrateLocalAccounts** for “true”, essa variável precisará conter a senha atribuída a todas as contas locais migradas. A USMT atribui a mesma senha a todas as contas locais migradas. Considere esta senha como temporária e altere-a posteriormente usando algum outro método.|  
|OSDMigrateAdditionalRestoreOptions<br /><br /> (entrada)|Especifica as demais opções de migração da linha de comando da USMT (Ferramenta de Migração do Usuário) que são usadas ao restaurar o estado de usuário. As opções adicionais são especificadas na forma de uma cadeia de caracteres que é anexada à linha de comando USMT gerada automaticamente. As opções do USMT especificadas com essa variável de sequência de tarefas não são validadas quanto à precisão antes da execução da sequência de tarefas.|  
|_OSDMigrateUsmtRestorePackageID<br /><br /> (entrada)|Especifica a ID do pacote do Configuration Manager que contém os arquivos do USMT. Esta variável é obrigatória.|  



###  <a name="BKMK_RunCommand"></a> Executar Linha de Comando   
  Para obter mais informações, consulte [Executar Linha de Comando](task-sequence-steps.md#BKMK_RunCommandLine).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|SMSTSDisableWow64Redirection<br /><br /> (entrada)|Por padrão em um sistema operacional de 64 bits, a sequência de tarefas localiza e executa o programa na linha de comando usando o redirecionador de sistema de arquivos do WOW64. Esse comportamento permite ao comando localizar versões nativas de 32 bits de programas e DLLs do sistema operacional. A definição dessa variável como **true** desabilita o uso do redirecionador de sistema de arquivos WOW64. O comando localiza versões nativas de 64 bits de programas do sistema operacional e DLLs. Essa variável não tem nenhum efeito em um sistema operacional de 32 bits.|  
|WorkingDirectory<br /><br /> (entrada)|Especifica o diretório inicial para uma ação de linha de comando. O nome do diretório especificado não deve exceder 255 caracteres.<br /><br /> Exemplos:<br /><br /> -   **C:\\**<br />-   **%SystemRoot%**|  
|SMSTSRunCommandLineUserName<br /><br /> (entrada)|Especifica a conta pela qual a linha de comando é executada. O valor é uma cadeia de caracteres do formato nomeusuário ou domínio\nomeusuário.|  
|SMSTSRunCommandLinePassword<br /><br /> (entrada)|Especifica a senha para a conta especificada pela variável SMSTSRunCommandLineUserName.|  



### <a name="set-dynamic-variables"></a>Definir Variáveis Dinâmicas  
Para obter mais informações, consulte [Definir Variáveis Dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação<br /><br /> (entrada)|Descrição|  
|----------------------------------------|-----------------|  
|_SMSTSMake|Especifica a marca do computador.|  
|_SMSTSModel|Especifica o modelo do computador.|  
|_SMSTSMacAddresses|Especifica os endereços MAC usados pelo computador.|  
|_SMSTSIPAddresses|Especifica os endereços IP usados pelo computador.|  
|_SMSTSSerialNumber|Especifica o número de série do computador.|  
|_SMSTSAssetTag|Especifica a marca de ativo do computador.|  
|_SMSTSUUID|Especifica o UUID do computador.|  
|_SMSTSDefaultGateways|Especifica os gateways padrão usados pelo computador.|  



###  <a name="BKMK_SetupWindows"></a> Instalar Windows e ConfigMgr   
  Para mais informações, consulte [Configurar Windows e ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação<br /><br /> (entrada)|Descrição|  
|----------------------------------------|-----------------|  
|SMSClientInstallProperties<br /><br /> (entrada)|Especifica as propriedades de instalação do cliente que são usadas durante a instalação do cliente do Configuration Manager.|  



### <a name="upgrade-operating-system"></a>Atualizar o sistema operacional  
 Para obter mais informações, consulte [Fazer Upgrade no Sistema Operacional](task-sequence-steps.md#BKMK_UpgradeOS).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação<br /><br /> (entrada)|Descrição|  
|----------------------------------------|-----------------|  
|OSDSetupAdditionalUpgradeOptions<br /><br /> (entrada)|Especifica as demais opções da linha de comando que são adicionadas à Instalação do Windows durante um upgrade do Windows 10. A sequência de tarefas não verifica as opções de linha de comando.<br /><br /> Para obter mais informações, veja [Opções de Linha de Comando da Instalação do Windows](/windows-hardware/manufacture/desktop/windows-setup-command-line-options).|  
