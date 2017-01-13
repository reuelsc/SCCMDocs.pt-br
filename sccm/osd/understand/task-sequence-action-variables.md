---
title: "Variáveis de ação de sequência de tarefas | Microsoft Docs"
description: "Use variáveis de ação de sequência, como variáveis de configuração de rede, para definir configurações para uma única etapa em uma sequência de tarefas do Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2269031-0977-4f01-a274-420e00630575
caps.latest.revision: 10
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: 6049ec2369e0a97b21ce6523ba8448335385ab9a


---
# <a name="task-sequence-action-variables-in-system-center-configuration-manager"></a>Variáveis de ação da sequência de tarefas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Variáveis de ação de sequência de tarefas especificam configurações que são usadas por uma única etapa em uma sequência de tarefas do System Center Configuration Manager. Por padrão, as configurações usadas por uma etapa da sequência de tarefas são inicializadas antes que a etapa é executada e estão disponíveis apenas durante a execução da etapa de sequência de tarefas associada. Em outras palavras, a configuração da variável de sequência de tarefas é adicionada ao ambiente da sequência de tarefas antes que a etapa da sequência de tarefas seja executada, e o valor é removido do ambiente da sequência de tarefas depois que a etapa da sequência de tarefas é executada.  

## <a name="action-variable-example"></a>Exemplo de variável de ação  
 Por exemplo, você pode especificar um diretório de início para uma ação de linha de comando usando a etapa **Executar Linha de Comando** da sequência de tarefas. Esta etapa inclui uma propriedade **Iniciar em** , cujo valor padrão é armazenado no ambiente da sequência de tarefas como a variável **WorkingDirectory** . A variável de ambiente **WorkingDirectory** é inicializada antes da ação da sequência de tarefas **Executar Linha de Comando** . Durante a etapa **Executar Linha de Comando** , o valor **WorkingDirectory** pode ser acessado por meio da propriedade **Start In** . Depois que a etapa da sequência de tarefas for concluída, o valor da variável **WorkingDirectory** será removido do ambiente da sequência de tarefas. Se a sequência contiver outra etapa da sequência de tarefas **Executar Linha de Comando** , a nova variável **WorkingDirectory** será inicializada e definida como o valor inicial para essa etapa da sequência de tarefas.  

 Enquanto o valor padrão de uma configuração de ação da sequência de tarefas está presente durante a execução da etapa da sequência de tarefas, qualquer novo valor definido pode ser usado por várias etapas na sequência. Se você usar um dos métodos de criação da variável de sequência de tarefas para substituir o valor de uma variável interna, o novo valor permanecerá no ambiente e substituirá o valor padrão para as outras etapas na sequência de tarefas. No exemplo anterior, se uma etapa **Definir Variável de Sequência de Tarefas** for adicionada como a primeira etapa da sequência de tarefas e se ela definir a variável de ambiente **WorkingDirectory** para o valor **C:\\**, as etapas **Executar Linha de Comando** na sequência de tarefas usarão o novo valor de diretório inicial.  

## <a name="action-variables-for-task-sequence-actions"></a>Variáveis de ação para ações de sequência de tarefas  
 As variáveis de sequência de tarefas do Configuration Manager são agrupadas segundo a ação da sequência de tarefas associada. Use os links a seguir para coletar informações sobre as variáveis de ação associadas a uma ação específica. As variáveis de sequência de tarefas controlam como é operada a ação de sequência da tarefas. A ação de sequência de tarefas lê e usa as variáveis que você marca como variáveis de entrada. Como alternativa, você pode usar a ação Definir Variável de Sequência de Tarefas ou o objeto TSEnvironment COM para definir as variáveis no tempo de execução. Somente a ação de sequência de tarefas marca variáveis como variáveis de saída, que são lidas pelas ações que ocorrem posteriormente na sequência de tarefas.  

> [!NOTE]  
>  Nem todas as ações da sequência de tarefas são associadas a um conjunto de variáveis de sequência de tarefas. Por exemplo, embora existam variáveis associadas à ação Habilitar BitLocker, não há variáveis associadas à ação Desabilitar BitLocker.  

###  <a name="a-namebkmkapplydataimagea-apply-data-image-task-sequence-action-variables"></a><a name="BKMK_ApplyDataImage"></a> Aplicar variáveis de ação da sequência de tarefas da imagem de dados  
 As variáveis dessa ação especificam qual imagem de um arquivo WIM é aplicada ao computador de destino e se os arquivos na partição de destino são excluídos ou não. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Etapa da sequência de tarefas Aplicar Imagem de Dados](task-sequence-steps.md#BKMK_ApplyDataImage).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDDataImageIndex<br /><br /> (entrada)|Especifica o valor de índice da imagem aplicado ao computador de destino.|  
|OSDWipeDestinationPartition<br /><br /> (entrada)|Especifica se é necessário excluir os arquivos localizados na partição de destino.<br /><br /> Valores válidos:<br /><br /> **"true"** (padrão)<br /><br /> **"false"**|  

###  <a name="a-namebkmkapplydriverpackagea-apply-driver-package-task-sequence-action-variables"></a><a name="BKMK_ApplyDriverPackage"></a> Aplicar variáveis de ação da sequência de tarefas do pacote de driver  
 As variáveis dessa ação especificam informações sobre a instalação de drivers de armazenamento em massa e se é necessário instalar drivers não assinados. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Aplicar Pacote de Driver](task-sequence-steps.md#BKMK_ApplyDriverPackage).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDApplyDriverBootCriticalContentUniqueID<br /><br /> (entrada)|Especifica a ID de conteúdo do driver do dispositivo de armazenamento em massa a ser instalada do pacote de drivers. Se isso não for especificado, nenhum driver de armazenamento em massa será instalado.|  
|OSDApplyDriverBootCriticalINFFile<br /><br /> (entrada)|Especifica o arquivo INF do driver de armazenamento em massa a ser instalado.<br /><br /> <br /><br /> Esta variável de sequência de tarefas é obrigatória se OSDApplyDriverBootCriticalContentUniqueID estiver definido.|  
|OSDApplyDriverBootCriticalHardwareComponent<br /><br /> (entrada)|Especifica se um driver de dispositivo de armazenamento em massa está instalado; deve ser **scsi**.<br /><br /> <br /><br /> Esta variável de sequência de tarefas é obrigatória se OSDApplyDriverBootCriticalContentUniqueID estiver definido.|  
|OSDApplyDriverBootCriticalID<br /><br /> (entrada)|Especifica a ID crítica de inicialização do driver do dispositivo de armazenamento em massa a ser instalada. Esta ID é listada na seção “**scsi**” do arquivo txtsetup.oem do driver de dispositivo.<br /><br /> <br /><br /> Esta variável de sequência de tarefas é obrigatória se OSDApplyDriverBootCriticalContentUniqueID estiver definido.|  
|OSDAllowUnsignedDriver<br /><br /> (entrada)|Especifica se é necessário configurar o Windows para permitir a instalação de drivers de dispositivo não assinados. Essa variável de sequência de tarefas não é usada ao implantar o Windows Vista e o sistema operacional posterior.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (padrão)|  

###  <a name="a-namebkmkapplynetworksettingsa-apply-network-settings-task-sequence-action-variables"></a><a name="BKMK_ApplyNetworkSettings"></a> Aplicar variáveis de ação da sequência de tarefas das configurações de rede  
 As variáveis dessa ação especificam as configurações de rede para o computador de destino, como configurações de adaptadores de rede do computador, configurações de domínio e configurações de grupo de trabalho. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Etapa Aplicar Configurações de Rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDAdapter<br /><br /> (entrada)|Esta variável de sequência de tarefas é uma variável de matriz. Cada elemento na matriz representa as configurações para um único adaptador de rede no computador. As configurações definidas para cada adaptador são acessadas pela combinação do nome de variável de matriz com o índice do adaptador de rede baseado em zero e o nome da propriedade.<br /><br /> <br /><br /> Se vários adaptadores de rede precisarem ser configurados com esta ação da sequência de tarefas, as propriedades do segundo adaptador de rede serão definidas usando seu índice no nome da variável; por exemplo, OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList, OSDAdapter1DNSDomain, OSDAdapter1WINSServerList, OSDAdapter1EnableWINS e assim por diante.<br /><br /> <br /><br /> Por exemplo, os seguintes nomes de variáveis podem ser usados para definir as propriedades para o primeiro adaptador de rede que será configurado por esta ação da sequência de tarefas:<br /><br /> <ul><li>**OSDAdapter0EnableDHCP** – true para habilitar o protocolo DHCP para o adaptador.<br />    Essa configuração é necessária. Os valores possíveis são: True ou False.</li><li>**OSDAdapter0IPAddressList** – lista delimitada por vírgula de endereços IP do adaptador. Essa propriedade será ignorada, a menos que **EnableDHCP** seja definido como **false**.<br />    Essa configuração é necessária.</li><li>**OSDAdapter0SubnetMask** – lista delimitada por vírgula de máscaras de sub-rede. Essa propriedade será ignorada, a menos que **EnableDHCP** seja definido como **false**.<br />    Essa configuração é necessária.</li><li>**OSDAdapter0Gateways** – lista delimitada por vírgula de endereços IP de gateway. Essa propriedade será ignorada, a menos que **EnableDHCP** seja definido como **false**.<br />    Essa configuração é necessária.</li><li>**OSDAdapter0DNSDomain** -Domínio DNS (Sistema de Nomes de Domínio) do adaptador.</li><li>**OSDAdapter0DNSServerList** – lista delimitada por vírgula de servidores DNS do adaptador.<br />    Essa configuração é necessária.</li><li>**OSDAdapter0EnableDNSRegistration** - **true** para registrar o endereço IP do adaptador no DNS.</li><li>**OSDAdapter0EnableFullDNSRegistration** - **true** para registrar o endereço IP do adaptador no DNS com o nome DNS completo do computador.</li><li>**OSDAdapter0EnableIPProtocolFiltering** - **true** para habilitar a filtragem de protocolo IP no adaptador.</li><li>**OSDAdapter0IPProtocolFilterList** – lista delimitada por vírgula de protocolos que podem ser executados com IP. Essa propriedade será ignorada se **EnableIPProtocolFiltering** estiver definido como **false**.</li><li>**OSDAdapter0EnableTCPFiltering** - **true** para habilitar a filtragem de porta TCP do adaptador.</li><li>**OSDAdapter0TCPFilterPortList** – lista delimitada por vírgula de portas que receberão permissões de acesso para TCP. Essa propriedade será ignorada se **EnableTCPFiltering** estiver definido como **false**.</li><li>**OSDAdapter0TcpipNetbiosOptions** – opções de NetBIOS em TCP/IP. Os valores possíveis são:<br /><br /> <ul><li>0 Use as configurações de NetBIOS do servidor DHCP.</li><li>1 Habilitar NetBIOS por TCP/IP.</li><li>2 Desabilitar NetBIOS por TCP/IP.</li></ul></li><li>**OSDAdapter0EnableWINS** - **true** para usar o WINS para a resolução de nomes.</li><li>**OSDAdapter0WINSServerList** – Lista delimitada por vírgula de endereços IP do servidor WINS. Essa propriedade será ignorada, a menos que **EnableWINS ativa** esteja definido como **true**.</li><li>**OSDAdapter0MacAddress** – endereço MAC (Media access controller) usado para fazer a correspondência das configurações com o adaptador de rede física.</li><li>**OSDAdapter0Name** – nome da conexão de rede como ele aparece no programa do painel de controle das conexões de rede. O comprimento do nome está entre 0 e 255 caracteres.</li><li>**OSDAdapter0Index** – índice das configurações do adaptador de rede na matriz de configurações.<br /><br />     OSDAdapterCount=1<br />    OSDAdapter0EnableDHCP=FALSE<br />    OSDAdapter0IPAddressList=192.168.0.40<br />    OSDAdapter0SubnetMask=255.255.255.0<br />    OSDAdapter0Gateways=192.168.0.1<br />    OSDAdapter0DNSSuffix=contoso.com</li></ul>|  
|OSDAdapterCount<br /><br /> (entrada)|Especifica o número de adaptadores de rede instalados no computador de destino. Quando o valor **OSDAdapterCount** estiver definido, todas as opções de configuração para cada adaptador deverão ser definidas. Por exemplo, se você definir o valor de **OSDAdapterTCPIPNetbiosOptions** como um adaptador específico, todos os valores desse adaptador também precisarão ser configurados.<br /><br /> <br /><br /> Se esse valor não for especificado, todos os valores **OSDAdapter** serão ignorados.|  
|OSDDNSDomain<br /><br /> (entrada)|Especifica o servidor DNS primário que é usado pelo computador de destino.|  
|OSDDomainName<br /><br /> (entrada)|Especifica o nome do domínio do Windows ingressado pelo computador de destino. O valor especificado deve ser um nome de domínio válido dos Serviços de Domínio do Active Directory.|  
|OSDDomainOUName<br /><br /> (entrada)|Especifica o nome de formato RFC 1779 da UO (unidade organizacional) ingressada pelo computador de destino. Se especificado, o valor deve conter o caminho completo.<br /><br /> Exemplo:<br /><br /> **LDAP://OU=MinhaUo,DC=MeuDomínio,DC=MinhaEmpresa,DC=com**|  
|OSDEnableTCPIPFiltering<br /><br /> (entrada)|Especifica se a filtragem de TCP/IP está habilitada.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (padrão)|  
|OSDJoinAccount<br /><br /> (entrada)|Especifica a conta de rede que é usada para adicionar o computador de destino a um domínio do Windows.|  
|OSDJoinPassword<br /><br /> (entrada)|Especifica a senha de rede usada para adicionar o computador de destino a um domínio do Windows.|  
|OSDNetworkJoinType<br /><br /> (entrada)|Especifica se o computador de destino ingressa em um domínio ou grupo de trabalho do Windows.<br /><br /> **“0”** indica que o computador de destino ingressa em um domínio do Windows. **“1”** especifica que o computador ingressa em um grupo de trabalho.<br /><br /> Valores válidos:<br /><br /> **“0”**<br /><br /> **“1”**|  
|OSDDNSSuffixSearchOrder<br /><br /> (entrada)|Especifica a ordem de pesquisa DNS para o computador de destino.|  
|OSDWorkgroupName<br /><br /> (entrada)|Especifica o nome do grupo de trabalho ingressado pelo computador de destino.<br /><br /> É necessário especificar esse valor ou o valor **OSDDomainName** . O nome do grupo de trabalho pode ter, no máximo, 32 caracteres.<br /><br /> Exemplo:<br /><br /> **"Accounting"**|  

###  <a name="a-namebkmkapplyoperatingsystema-apply-operating-system-image-task-sequence-action-variables"></a><a name="BKMK_ApplyOperatingSystem"></a> Aplicar variáveis de ação da sequência de tarefas da imagem do sistema operacional  
 As variáveis dessa ação especificam as configurações para o sistema operacional que você deseja instalar no computador de destino. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Aplicar Imagem de Sistema Operacional](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDConfigFileName<br /><br /> (entrada)|Especifica o nome do arquivo de resposta da implantação de sistema operacional associado ao pacote de implantação de sistema operacional.|  
|OSDImageIndex<br /><br /> (entrada)|Especifica o valor de índice da imagem do arquivo WIM aplicado ao computador de destino.|  
|OSDInstallEditionIndex<br /><br /> (entrada)|Especifica a versão do Windows Vista ou do sistema operacional mais recente instalada. Se nenhuma versão for especificada, a instalação do Windows determinará a versão que será instalada usando a chave do produto (Product Key) referenciada.<br /><br /> Use apenas um valor de 0 (zero) se as seguintes condições forem verdadeiras:<br /><br /> – Você está instalando um sistema operacional anterior ao Windows Vista<br />– Você está instalando uma edição de licença por volume do Windows Vista ou posterior, e nenhuma chave do produto (Product Key) foi especificada.<br /><br /> Valores válidos:<br /><br /> **"0"** (padrão)|  
|OSDTargetSystemDrive (saída)|Especifica a letra da unidade da partição que contém os arquivos do sistema operacional.|  

###  <a name="a-namebkmkapplywindowssettingsa-apply-windows-settings-task-sequence-action-variables"></a><a name="BKMK_ApplyWindowsSettings"></a> Aplicar variáveis de ação da sequência de tarefas das configurações do Windows  
 As variáveis dessa ação especificam as configurações do Windows para o computador de destino, como o nome do computador, a chave do produto (Product Key) do Windows, o usuário registrado e a organização e a senha de administrador local. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Aplicar Configurações do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDComputerName<br /><br /> (entrada)|Especifica o nome do computador de destino.<br /><br /> Exemplo:<br /><br /> **"%_SMSTSMachineName%"** (padrão)|  
|OSDProductKey<br /><br /> (entrada)|Especifica a chave do produto (Product Key) do Windows. O valor especificado deve estar entre 1 e 255 caracteres.|  
|OSDRegisteredUserName<br /><br /> (entrada)|Especifica o nome de usuário registrado padrão no novo sistema operacional. O valor especificado deve estar entre 1 e 255 caracteres.|  
|OSDRegisteredOrgName<br /><br /> (entrada)|Especifica o nome da organização registrada padrão no novo sistema operacional. O valor especificado deve estar entre 1 e 255 caracteres.|  
|OSDTimeZone<br /><br /> (entrada)|Especifica a configuração de fuso horário padrão usada no novo sistema operacional.|  
|OSDServerLicenseMode<br /><br /> (entrada)|Especifica o modo de licença do Windows Server que é usado.<br /><br /> Valores válidos:<br /><br /> **"PerSeat"**<br /><br /> **"PerServer"**|  
|OSDServerLicenseConnectionLimit<br /><br /> (entrada)|Especifica o número máximo de conexões permitidas. O número especificado deve estar no intervalo entre 5 e 9.999 conexões.|  
|OSDRandomAdminPassword<br /><br /> (entrada)|Especifica uma senha gerada aleatoriamente para a conta de administrador no novo sistema operacional. Se definido como **true**, a conta de administrador local será desabilitada no computador de destino. Se definido como **false**, a conta de administrador local será habilitada no computador de destino e a senha da conta de administrador local receberá o valor da variável **OSDLocalAdminPassword**.<br /><br /> Valores válidos:<br /><br /> **"true"** (padrão)<br /><br /> **"false"**|  
|OSDLocalAdminPassword<br /><br /> (entrada)|Especifica a senha do administrador local. Esse valor será ignorado se a opção **Gerar aleatoriamente a senha de administrador local e desabilitar a conta em todas as plataformas com suporte** for habilitada. O valor especificado deve estar entre 1 e 255 caracteres.|  

###  <a name="a-namebkmkautoapplydriversa-auto-apply-drivers-task-sequence-action-variables"></a><a name="BKMK_AutoApplyDrivers"></a> Aplicar automaticamente variáveis de ação da sequência de tarefas de drivers  
 As variáveis dessa ação especificam quais drivers do Windows são instalados no computador de destino e se os drivers não assinados são instalados. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Drivers de Aplicação Automática](task-sequence-steps.md#BKMK_AutoApplyDrivers).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDAutoApplyDriverCategoryList<br /><br /> (entrada)|Uma lista delimitada por vírgulas de IDs exclusivas de categorias do catálogo de drivers. Se especificada, a ação da sequência de tarefas **Aplicar Driver Automaticamente** considerará apenas os drivers que estão em, pelo menos, uma dessas categorias ao instalar os drivers. Esse valor é opcional e não é definido por padrão. As IDs de categoria disponíveis podem ser obtidas pela enumeração da lista de objetos **SMS_CategoryInstance** no site.|  
|OSDAllowUnsignedDriver<br /><br /> (entrada)|Especifica se o Windows está configurado para permitir que drivers de dispositivo não assinados sejam instalados. Essa variável de sequência de tarefas não é usada ao implantar o Windows Vista e sistemas operacionais posteriores.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (padrão)|  
|OSDAutoApplyDriverBestMatch<br /><br /> (entrada)|Especifica o que a ação de sequência de tarefas faz se houver vários drivers de dispositivo no catálogo de drivers que são compatíveis com um dispositivo de hardware. Se definido como **true**, somente o melhor driver de dispositivo será instalado.  Se for definido como **false**, serão instalados todos os drivers de dispositivo compatíveis, e o sistema operacional escolherá o melhor driver a ser usado.<br /><br /> Valores válidos:<br /><br /> **"true"** (padrão)<br /><br /> **"false"**|  

###  <a name="a-namebkmkcapturenetworksettingsa-capture-network-settings-task-sequence-action-variables"></a><a name="BKMK_CaptureNetworkSettings"></a> Capturar variáveis de ação da sequência de tarefas de configurações de rede  
 As variáveis dessa ação especificam se as informações de configuração das definições do adaptador de rede (TCP/IP, DNS e WINS) são capturadas e se as informações de associação de grupo de trabalho ou domínio são migradas como parte da implantação de sistema operacional. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Capturar Configurações da Rede](task-sequence-steps.md#BKMK_CaptureNetworkSettings).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDMigrateAdapterSettings<br /><br /> (entrada)|Especifica se as informações de configurações do adaptador de rede (TCP/IP, DNS e WINS) são capturadas.<br /><br /> Exemplos:<br /><br /> **"true"** (padrão)<br /><br /> **"false"**|  
|OSDMigrateNetworkMembership<br /><br /> (entrada)|Especifica se as informações de associação de grupo de trabalho ou de domínio são migradas como parte da implantação de sistema operacional.<br /><br /> Exemplos:<br /><br /> **"true"** (padrão)<br /><br /> **"false"**|  

###  <a name="a-namebkmkcaptureoperatingsystemimagea-capture-operating-system-image-task-sequence-action-variables"></a><a name="BKMK_CaptureOperatingSystemImage"></a> Capturar variáveis de ação da sequência de tarefas da imagem do sistema operacional  
 As variáveis dessa ação especificam informações sobre a imagem de sistema operacional que está sendo capturada, como o local em que a imagem está armazenada, quem criou a imagem e uma descrição dela. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Capturar Imagem do Sistema Operacional](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  

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

###  <a name="a-namebkmkcaptureuserstatea-capture-user-state-task-sequence-action-variables"></a><a name="BKMK_CaptureUserState"></a> Capturar variáveis de ação da sequência de tarefas de estado de usuário  
 As variáveis dessa ação especificam as informações usadas pela USMT (Ferramenta de Migração do Usuário), como a pasta em que o estado de usuário foi salvo, opções de linha de comando para a USMT e os arquivos de configuração usados para controlar a captura dos perfis de usuário.  Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Capturar Estado do Usuário](task-sequence-steps.md#BKMK_CaptureUserState).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrada)|O UNC ou nome de caminho local da pasta em que o estado de usuário foi salvo. Nenhum padrão.|  
|OSDMigrateAdditionalCaptureOptions<br /><br /> (entrada)|Especifica as opções de migração de linha de comando da USMT (Ferramenta de Migração do Usuário) que são usadas ao capturar o estado de usuário, mas que não são expostas na interface do usuário do Configuration Manager. As opções adicionais são especificadas na forma de uma cadeia de caracteres que é anexada à linha de comando USMT gerada automaticamente.<br /><br /> <br /><br /> As opções do USMT especificadas com essa variável de sequência de tarefas não são validadas quanto à precisão antes da execução da sequência de tarefas.|  
|OSDMigrateMode<br /><br /> (entrada)|Permite que você personalize os arquivos que são capturados pelo USMT. Se essa variável for definida como "Simple", somente os arquivos padrão de configuração do USMT serão usados. Se for definida como "Advanced", a variável de sequência de tarefas OSDMigrateConfigFiles especificará os arquivos de configuração usados pelo USMT.<br /><br /> Valores válidos:<br /><br /> **"Simple"**<br /><br /> **"Advanced"**|  
|OSDMigrateConfigFiles<br /><br /> (entrada)|Especifica os arquivos de configuração usados para controlar a captura de perfis de usuário. Essa variável será usada apenas se OSDMigrateMode estiver definido como “Advanced”. Esse valor de lista delimitado por vírgulas é definido para executar a migração personalizada de perfil do usuário.<br /><br /> Exemplo: miguser.xml, migsys.xml, migapps.xml|  
|OSDMigrateContinueOnLockedFiles<br /><br /> (entrada)|Permite a continuação da captura de estado do usuário se não for possível capturar alguns arquivos.<br /><br /> Valores válidos:<br /><br /> **"true"** (padrão)<br /><br /> **"false"**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (entrada)|Habilita o log detalhado do USMT.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (padrão)|  
|OSDMigrateSkipEncryptedFiles<br /><br /> (entrada)|Especifica se os arquivos criptografados serão capturados.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (padrão)|  
|_OSDMigrateUsmtPackageID<br /><br /> (entrada)|Especifica a ID do pacote do Configuration Manager que conterá os arquivos do USMT. Esta variável é obrigatória.|  

###  <a name="a-namebkmkcapturewindowssettingsa-capture-windows-settings-task-sequence-action-variables"></a><a name="BKMK_CaptureWindowsSettings"></a> Capturar variáveis de ação da sequência de tarefas de configurações do Windows  
 As variáveis dessa ação especificam se configurações específicas do Windows são migradas para o computador de destino, como o nome do computador, o nome da organização do registro e informações de fuso horário. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Capturar Configurações do Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDMigrateComputerName<br /><br /> (entrada)|Especifica se o nome do computador é migrado.<br /><br /> Valores válidos:<br /><br /> **"true"** (padrão)<br /><br /> **"false"**<br /><br /> Se o valor for "true", a variável OSDComputerName será definida como o nome NetBIOS do computador.|  
|OSDComputerName<br /><br /> (saída)|Defina como o nome NetBIOS do computador. O valor será definido somente se a variável OSDMigrateComputerName for definida como “true”.|  
|OSDMigrateRegistrationInfo<br /><br /> (entrada)|Especifica se o usuário do computador e as informações organizacionais são migradas.<br /><br /> Valores válidos:<br /><br /> **"true"** (padrão)<br /><br /> **"false"**<br /><br /> Se o valor for "true", a variável OSDRegisteredOrgName será definida como o nome da organização registrada do computador.|  
|OSDRegisteredOrgName<br /><br /> (saída)|Defina como o nome da organização registrada do computador. O valor será definido somente se a variável OSDMigrateRegistrationInfo for definida como “true”.|  
|OSDMigrateTimeZone<br /><br /> (entrada)|Especifica se o fuso horário do computador é migrado.<br /><br /> Valores válidos:<br /><br /> **"true"** (padrão)<br /><br /> **"false"**<br /><br /> Se o valor for "true", a variável OSDTimeZone será definida como o fuso horário do computador.|  
|OSDTimeZone<br /><br /> (saída)|Defina como o fuso horário do computador. O valor será definido somente se a variável OSDMigrateTimeZone for definida como “true”.|  

###  <a name="a-namebkmkconnecttonetworkfoldera-connect-to-network-folder-task-sequence-action-variables"></a><a name="BKMK_ConnecttoNetworkFolder"></a> Conectar a variáveis de ação da sequência de tarefas da pasta de rede  
 As variáveis desta ação especificam informações sobre uma pasta em uma rede, como a conta usada e a senha para se conectar à pasta de rede, a letra da unidade da pasta e o caminho para a pasta. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Conectar à Pasta de Rede](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|SMSConnectNetworkFolderAccount<br /><br /> (entrada)|Especifica a conta de administrador usada para se conectar ao compartilhamento de rede.|  
|SMSConnectNetworkFolderDriveLetter<br /><br /> (entrada)|Especifica a letra da unidade da rede à qual se conectar. Esse valor é opcional; se não for especificado, a conexão de rede não será mapeada para uma letra da unidade. Se esse valor for especificado, o valor deverá estar no intervalo de D: a Z:.  Além disso, não use X, pois essa é a letra da unidade usada pelo Windows PE durante a fase do Windows PE.<br /><br /> Exemplos:<br /><br /> **"D:"**<br /><br /> **"E:"**|  
|SMSConnectNetworkFolderPassword<br /><br /> (entrada)|Especifica a senha de rede usada para se conectar ao compartilhamento de rede.|  
|SMSConnectNetworkFolderPath<br /><br /> (entrada)|Especifica o caminho de rede para a conexão.<br /><br /> Exemplo:<br /><br /> **"\\\servername\sharename"**|  

###  <a name="a-namebkmkconvertdiska-convert-disk-to-dynamic-task-sequence-action-variables"></a><a name="BKMK_ConvertDisk"></a> Converter disco em variáveis dinâmicas de ação da sequência de tarefas  
 A variável dessa ação especifica o número do disco físico para converter de disco básico em dinâmico. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Converter Disco em Dinâmico](task-sequence-steps.md#BKMK_ConvertDisktoDynamic).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDConvertDiskIndex<br /><br /> (entrada)|Especifica o número de discos físicos que são convertidos.|  

###  <a name="a-namebkmkenablebitlockera-enable-bitlocker-task-sequence-action-variables"></a><a name="BKMK_EnableBitLocker"></a> Habilitar variáveis de ação da sequência de tarefas do BitLocker  
 As variáveis dessa ação especificam as opções de senha de recuperação e chave de inicialização usadas para habilitar o BitLocker no computador de destino. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Habilitar BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDBitLockerRecoveryPassword<br /><br /> (entrada)|Em vez de gerar uma senha aleatória de recuperação, a ação da sequência de tarefas **Habilitar BitLocker** usa o valor especificado como a senha de recuperação. O valor deve ser uma senha de recuperação do BitLocker numérica e válida.|  
|OSDBitLockerStartupKey<br /><br /> (entrada)|Em vez de gerar uma chave de inicialização aleatória para a opção de gerenciamento de chaves **Chave de Inicialização somente em USB**, a ação da sequência de tarefas **Habilitar BitLocker** usa o TPM (Trusted Platform Module) como a chave de inicialização. O valor deve ser uma chave de inicialização do BitLocker válida, codificada em Base64 e de 256 bits.|  

###  <a name="a-namebkmkformatpartitiondiska-format-and-partition-disk-task-sequence-action-variables"></a><a name="BKMK_FormatPartitionDisk"></a> Variáveis de ação da sequência de tarefas de formato e disco de partição  
 As variáveis dessa ação especificam informações para formatar e particionar um disco físico, como o número do disco e uma matriz de configurações de partição. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Formatar e Particionar Disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDDiskIndex<br /><br /> (entrada)|Especifica o número de discos físicos a ser particionados.|  
|OSDDiskpartBiosCompatibilityMode<br /><br /> (entrada)|Especifica se é necessário desabilitar as otimizações de alinhamento de cache ao particionar o disco rígido para compatibilidade com certos tipos de BIOS. Isso pode ser necessário durante a implantação de sistemas operacionais Windows XP ou Windows Server 2003. Para obter mais informações, veja o [artigo 931760](http://go.microsoft.com/fwlink/?LinkId=134081) e o [artigo 931761](http://go.microsoft.com/fwlink/?LinkId=134082) na Base de Dados de Conhecimento Microsoft.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (padrão)|  
|OSDGPTBootDisk<br /><br /> (entrada)|Especifica se é necessário criar uma partição EFI em um disco rígido GPT para que ele possa ser usado como o disco de inicialização em computadores baseados em EFI.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (padrão)|  
|OSDPartitions<br /><br /> (entrada)|Especifica uma matriz de configurações de partição; veja o tópico sobre o SDK para acessar variáveis de matriz no ambiente da sequência de tarefas.<br /><br /> Esta variável de sequência de tarefas é uma variável de matriz. Cada elemento na matriz representa as configurações para uma única partição no disco rígido. As configurações definidas para cada partição podem ser acessadas pela combinação do nome de variável de matriz com o número de partição de disco baseado em zero e o nome da propriedade.<br /><br /> Por exemplo, os seguintes nomes de variáveis podem ser usados para definir as propriedades para a primeira partição que será criada por esta ação da sequência de tarefas:<br /><br /> - **OSDPartitions0Type** – especifica o tipo de partição. Esta é uma propriedade obrigatória. Os valores válidos são "**Primary**", "**Extended**", "**Logical**" e "**Hidden**".<br />-   **OSDPartitions0FileSystem** -Especifica o tipo de sistema de arquivos a ser usado ao formatar a partição. Essa é uma propriedade opcional; se nenhum sistema de arquivos for especificado, a partição não será formatada. Os valores válidos são “**FAT32**”e “**NTFS**”.<br />-   **OSDPartitions0Bootable** -Especifica se a partição será inicializável. Esta é uma propriedade obrigatória. Se esse valor for definido como "**TRUE**" para discos MBR, isso se tornará a partição ativa.<br />-   **OSDPartitions0QuickFormat** -Especifica o tipo de formato usado. Esta é uma propriedade obrigatória. Se esse valor for definido como "**TRUE**", uma formatação rápida será executada; caso contrário, será executada uma formatação completa.<br />-   **OSDPartitions0VolumeName** -Especifica o nome atribuído ao volume quando ele é formatado. Esta é uma propriedade opcional.<br />-   **OSDPartitions0Size** - Especifica o tamanho da partição. As unidades são especificadas pela variável **OSDPartitions0SizeUnits** . Esta é uma propriedade opcional. Se esta propriedade não for especificada, a partição será criada usando todo o espaço livre restante.<br />-   **OSDPartitions0SizeUnits** -Especifica as unidades que serão usadas ao interpretar a variável de sequência de tarefas **OSDPartitions0Size** . Esta é uma propriedade opcional. Os valores válidos são “**MB**” (padrão), “**GB**” e “**%**”.<br />-   **OSDPartitions0VolumeLetterVariable** - As partições sempre usarão a próxima letra da unidade disponível no Windows PE quando forem criadas. Use essa propriedade opcional para especificar o nome de outra variável de sequência de tarefas, que será usado para salvar a nova letra da unidade para referência futura.<br /><br /> <br /><br /> Se várias partições precisarem ser definidas com esta ação da sequência de tarefas, as propriedades da segunda partição poderão ser definidas usando seu índice no nome da variável; por exemplo, **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat**, **OSDPartitions1VolumeName** e assim por diante.|  
|OSDPartitionStyle<br /><br /> (entrada)|Especifica o estilo de partição a ser usado ao particionar o disco. "**MBR**" indica o estilo de partição do registro mestre de inicialização, e "**GPT**" indica o estilo de tabela de partição GUID.<br /><br /> Valores válidos:<br /><br /> **"GPT"**<br /><br /> **"MBR"**|  

###  <a name="a-namebkmkinstallsoftwareupdatesa-install-software-updates-task-sequence-action-variables"></a><a name="BKMK_InstallSoftwareUpdates"></a> Instalar variáveis de ação da sequência de tarefas das Atualizações de Software  
 A variável dessa ação especifica se é necessário instalar todas as atualizações ou apenas as atualizações obrigatórias. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Instalar Atualizações de Software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação<br /><br /> (entrada)|Descrição|  
|----------------------------------------|-----------------|  
|SMSInstallUpdateTarget<br /><br /> (entrada)|Especifica se é necessário instalar todas as atualizações ou apenas as atualizações obrigatórias.<br /><br /> Valores válidos:<br /><br /> **"All"**<br /><br /> **"Mandatory"**|  

###  <a name="a-namebkmkjoindomainworkgroupa-join-domain-or-workgroup-task-sequence-action-variables"></a><a name="BKMK_JoinDomainWorkgroup"></a> Ingressar variáveis de ação da sequência de tarefas no domínio ou no grupo de trabalho  
 As variáveis dessa ação especificam as informações necessárias para ingressar o computador de destino em um domínio ou grupo de trabalho do Windows. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Ingressar no Domínio ou Grupo de Trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDJoinAccount<br /><br /> (entrada)|Especifica a conta usada pelo computador de destino para ingressar no domínio do Windows. Essa variável é necessária ao ingressar em um domínio.|  
|OSDJoinDomainName<br /><br /> (entrada)|Especifica o nome de um domínio do Windows ingressado pelo computador de destino. O comprimento do nome de domínio do Windows deve estar entre 1 e 255 caracteres.|  
|OSDJoinDomainOUName<br /><br /> (entrada)|Especifica o nome de formato RFC 1779 da UO (unidade organizacional) ingressada pelo computador de destino. Se especificado, o valor deve conter o caminho completo. O comprimento do nome de UO do domínio do Windows deve estar entre 0 e 32.767 caracteres. Esse valor não será definido se a variável **OSDJoinType** for definida como “1” (ingressar no grupo de trabalho).<br /><br /> Exemplo:<br /><br /> **LDAP://OU=MinhaUo,DC=MeuDomínio,DC=MinhaEmpresa,DC=com**|  
|OSDJoinPassword<br /><br /> (entrada)|Especifica a senha de rede usada pelo computador de destino para ingressar no domínio do Windows. Se a variável não for especificada, uma senha em branco será usada. Esse valor será necessário se a variável **OSDJoinType** for definida como “**0**” (ingressar no domínio).|  
|OSDJoinSkipReboot<br /><br /> (entrada)|Especifica se é necessário ignorar a reinicialização depois que o computador de destino ingressar no domínio ou no grupo de trabalho.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"**|  
|OSDJoinType<br /><br /> (entrada)|Especifica se o computador de destino ingressa em um domínio ou grupo de trabalho do Windows. Para ingressar o computador de destino em um domínio do Windows, especifique “**0**”. Para ingressar o computador de destino em um grupo de trabalho, especifique “**1**”.<br /><br /> Valores válidos:<br /><br /> **“0”**<br /><br /> **“1”**|  
|OSDJoinWorkgroupName<br /><br /> (entrada)|Especifica o nome de um grupo de trabalho ingressado pelo computador de destino. O comprimento do nome do grupo de trabalho deve estar entre 1 e 32 caracteres.<br /><br /> Exemplo:<br /><br /> **"Accounting"**|  

###  <a name="a-namebkmkpreparewindowscapturea-prepare-windows-for-capture-task-sequence-action-variables"></a><a name="BKMK_PrepareWindowsCapture"></a> Preparar o Windows para a captura de variáveis de ação da sequência de tarefas  
 As variáveis dessa ação especificam as informações usadas para capturar o sistema operacional Windows do computador de destino. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Preparar o ConfigMgr para Captura](task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDBuildStorageDriverList<br /><br /> (entrada)|Especifica se o sysprep compila uma lista de drivers de dispositivo de armazenamento em massa. Essa configuração se aplica somente ao Windows XP e Windows Server 2003. Ela populará a seção [SysprepMassStorage] de sysprep.inf com informações sobre todos os drivers de armazenamento em massa que são compatíveis com a imagem a ser capturada.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (padrão)|  
|OSDKeepActivation<br /><br /> (entrada)|Especifica se o sysprep redefine o sinalizador de ativação do produto.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (padrão)|  
|OSDTargetSystemRoot<br /><br /> (saída)|Especifica o caminho para o diretório do Windows do sistema operacional instalado no computador de referência. Este sistema operacional é confirmado como um sistema operacional com suporte para captura pelo Configuration Manager.|  

###  <a name="a-namebkmkreleasestatestorea-release-state-store-sequence-action-variables"></a><a name="BKMK_ReleaseStateStore"></a> Variáveis de ação da sequência de armazenamento de estado de versão  
 As variáveis dessa ação especificam as informações usadas para liberar o estado de usuário armazenado. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Liberar Armazenamento de Estado](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrada)|O UNC ou nome de caminho local d local do qual o estado de usuário foi restaurado. Esse valor é usado pelas ações da sequência de tarefas **Capturar Estado de Usuário** e **Restaurar Estado de Usuário** .|  

###  <a name="a-namebkmkrequeststatea-request-state-store-task-sequence-action-variables"></a><a name="BKMK_RequestState"></a> Variáveis de ação da sequência de tarefas de armazenamento de estado de solicitação  
 As variáveis dessa ação especificam as informações usadas para solicitar o estado de usuário armazenado, como a pasta no ponto de migração de estado em que os dados de usuário são armazenados. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Liberar Armazenamento de Estado](../../osd/understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDStateFallbackToNAA<br /><br /> (entrada)|Especifica se a Conta de Acesso à Rede é usada como um fallback quando a conta de computador não puder se conectar ao ponto de migração de estado.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (padrão)|  
|OSDStateSMPRetryCount<br /><br /> (entrada)|Especifica o número de vezes que a etapa da sequência de tarefas tentará localizar um ponto de migração de estado antes da etapa falhar. A contagem especificada deve estar entre 0 e 600.|  
|OSDStateSMPRetryTime<br /><br /> (entrada)|Especifica o número de segundos durante os quais a etapa da sequência de tarefas aguarda entre as novas tentativas. O número de segundos pode ter, no máximo, 30 caracteres.|  
|OSDStateStorePath<br /><br /> (saída)|O caminho UNC para a pasta no ponto de migração de estado em que o estado de usuário foi armazenado.|  

###  <a name="a-namebkmkrestartcomputera-restart-computer-task-sequence-action-variables"></a><a name="BKMK_RestartComputer"></a> Reiniciar variáveis de ação da sequência de tarefas do computador  
 As variáveis dessa ação especificam as informações usadas para reiniciar o computador de destino. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Reiniciar Computador](task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|SMSRebootMessage<br /><br /> (entrada)|Especifica a mensagem a ser exibida para os usuários antes de reiniciar o computador de destino. Se essa variável não for definida, o texto da mensagem padrão será exibido. A mensagem especificada não deve exceder 512 caracteres.<br /><br /> Exemplo:<br /><br /> – “Este computador será reiniciado. Salve seu trabalho.”|  
|SMSRebootTimeout<br /><br /> (entrada)|Especifica o número de segundos que o aviso é exibido para o usuário antes da reinicialização do computador. Especifique zero segundo para indicar que nenhuma mensagem de reinicialização é exibida.<br /><br /> Exemplos:<br /><br /> **"0"** (padrão)<br /><br /> **"5"**<br /><br /> **"10"**|  

###  <a name="a-namebkmkrestoreuserstatea-restore-user-state-task-sequence-action-variables"></a><a name="BKMK_RestoreUserState"></a> Restaurar variáveis de ação da sequência de tarefas de estado de usuário  
 As variáveis dessa ação especificam as informações usadas para restaurar o estado de usuário do computador de destino, como o nome do caminho da pasta do qual o estado de usuário é restaurado e se a conta de computador local é restaurada. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Restaurar Estado do Usuário](task-sequence-steps.md#BKMK_RestoreUserState).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrada)|O UNC ou nome de caminho local da pasta do qual o estado de usuário foi restaurado.|  
|OSDMigrateContinueOnRestore<br /><br /> (entrada)|Especifica que a restauração de estado de usuário continuará mesmo que alguns arquivos não possam ser restaurados.<br /><br /> Valores válidos:<br /><br /> **"true"** (padrão)<br /><br /> **"false"**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (entrada)|Habilita o log detalhado para a ferramenta USMT. Esse valor é exigido pela ação; ele deve ser definido como “true” ou “false”.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (padrão)|  
|OSDMigrateLocalAccounts<br /><br /> (entrada)|Especifica se a conta do computador local é restaurada.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (padrão)|  
|OSDMigrateLocalAccountPassword<br /><br /> (entrada)|Se a variável **OSDMigrateLocalAccounts** for "true", essa variável deverá conter a senha que é atribuída a todas as contas locais que são migradas. Como a mesma senha é atribuída a todas as contas locais migradas, ela é considerada uma senha temporária que será alterada posteriormente por algum método diferente da implantação de sistema operacional do Configuration Manager.|  
|OSDMigrateAdditionalRestoreOptions<br /><br /> (entrada)|Especifica as demais opções de migração da linha de comando da USMT (Ferramenta de Migração do Usuário) que são usadas ao restaurar o estado de usuário. As opções adicionais são especificadas na forma de uma cadeia de caracteres que é anexada à linha de comando USMT gerada automaticamente. As opções do USMT especificadas com essa variável de sequência de tarefas não são validadas quanto à precisão antes da execução da sequência de tarefas.|  
|_OSDMigrateUsmtRestorePackageID<br /><br /> (entrada)|Especifica a ID do pacote do Configuration Manager que contém os arquivos do USMT. Esta variável é obrigatória.|  

###  <a name="a-namebkmkruncommanda-run-command-line-task-sequence-action-variables"></a><a name="BKMK_RunCommand"></a> Executar variáveis de ação da sequência de tarefas da linha de comando  
 As variáveis dessa ação especificam as informações usadas para executar um comando da linha de comando, como o diretório de trabalho em que o comando é executado. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Executar Linha de Comando](task-sequence-steps.md#BKMK_RunCommandLine).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação|Descrição|  
|--------------------------|-----------------|  
|SMSTSDisableWow64Redirection<br /><br /> (entrada)|Por padrão, quando executado em um sistema operacional de 64 bits, o programa na linha de comando é localizado e executado usando o redirecionador do sistema de arquivos do WOW64, para que as versões de 32 bits dos programas e DLLs do sistema operacional sejam encontradas. Configurar esta variável como “true” desabilita o uso do redirecionador do sistema de arquivos do WOW64 para que as versões nativas de 64 bits de DLLs e programas do sistema operacional possam ser encontradas. Essa variável não tem nenhum efeito em um sistema operacional de 32 bits.|  
|WorkingDirectory<br /><br /> (entrada)|Especifica o diretório inicial para uma ação de linha de comando. O nome do diretório especificado não deve exceder 255 caracteres.<br /><br /> Exemplos:<br /><br /> -   **"C:\\"**<br />-   **"%SystemRoot%"**|  
|SMSTSRunCommandLineUserName<br /><br /> (entrada)|Especifica a conta pela qual a linha de comando é executada. O valor é uma cadeia de caracteres do formato nomeusuário ou domínio\nomeusuário.|  
|SMSTSRunCommandLinePassword<br /><br /> (entrada)|Especifica a senha para a conta especificada pela variável SMSTSRunCommandLineUserName.|  

### <a name="set-dynamic-variables"></a>Definir Variáveis Dinâmicas  
 As variáveis para esta ação são definidas automaticamente ao adicionar a etapa Definir Variáveis Dinâmicas da sequência de tarefas. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Definir Variáveis Dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables).  

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

###  <a name="a-namebkmksetupwindowsa-setup-windows-and-configmgr-task-sequence-action-variables"></a><a name="BKMK_SetupWindows"></a> Configurar variáveis de ação da sequência de tarefas do Windows e ConfigMgr  
 A variável dessa ação especifica as propriedades de instalação do cliente que são usadas durante a instalação do cliente do Configuration Manager. Para obter mais informações sobre a etapa da sequência de tarefas associada a essas variáveis, consulte [Instalar Windows e ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação<br /><br /> (entrada)|Descrição|  
|----------------------------------------|-----------------|  
|SMSClientInstallProperties<br /><br /> (entrada)|Especifica as propriedades de instalação do cliente que são usadas durante a instalação do cliente do Configuration Manager.|  

### <a name="upgrade-operating-system"></a>Atualizar o sistema operacional  
 A variável dessa ação especifica as opções de linha de comando adicionais que não estão disponíveis no console do Configuration Manager e que serão adicionadas à Instalação para uma atualização do Windows 10. Para obter mais informações sobre a etapa da sequência de tarefas associada a essa variável, consulte [Atualizar sistema operacional](task-sequence-steps.md#BKMK_UpgradeOS).  

#### <a name="details"></a>Detalhes  

|Nome de variável de ação<br /><br /> (entrada)|Descrição|  
|----------------------------------------|-----------------|  
|OSDSetupAdditionalUpgradeOptions<br /><br /> (entrada)|Especifica as demais opções da linha de comando que são adicionadas à Instalação durante uma atualização do Windows 10. As opções de linha de comando não são verificadas. Portanto, verifique se a opção que você inseriu está correta.<br /><br /> Para obter mais informações, veja [Opções de Linha de Comando da Instalação do Windows](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx).|  



<!--HONumber=Dec16_HO3-->


