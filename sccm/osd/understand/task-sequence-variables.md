---
title: Referência da variável de sequência de tarefas
titleSuffix: Configuration Manager
description: Saiba mais sobre as variáveis para controlar e personalizar uma sequência de tarefas do Configuration Manager.
ms.date: 05/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 62f15230-d3a6-4afc-abd4-1e07e7ba6c97
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3e1ad62c8b8b0f780670e7baf7ebf11de7f6b483
ms.sourcegitcommit: 60d45a5df135b84146f6cfea2bac7fd4921d0469
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67194580"
---
# <a name="task-sequence-variables"></a>Variáveis de sequência de tarefas

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo é uma referência para todas as variáveis disponíveis em ordem alfabética. Use a função **Localizar** do navegador (normalmente **CTRL** + **F**) para encontrar uma variável específica. Há informações sobre a variável ser específica para uma etapa em particular. O artigo sobre [etapas da sequência de tarefas](/sccm/osd/understand/task-sequence-steps) inclui a lista de variáveis específicas de cada etapa.

Para saber mais, confira [Uso de variáveis de sequência de tarefas](/sccm/osd/understand/using-task-sequence-variables).

## <a name="bkmk_tsvar"></a> Referência da variável de sequência de tarefas

### <a name="OSDDetectedWinDir"></a> _OSDDetectedWinDir

A sequência de tarefas verifica unidades de disco rígido do computador em busca de uma instalação de sistema operacional anterior quando o Windows PE é iniciado. O local da pasta do Windows é armazenado nessa variável. Você pode configurar sua sequência de tarefas para recuperar esse valor do ambiente e usá-lo a fim de especificar o mesmo local da pasta do Windows a ser usado para a nova instalação do sistema operacional.

### <a name="OSDDetectedWinDrive"></a> _OSDDetectedWinDrive

A sequência de tarefas verifica unidades de disco rígido do computador em busca de uma instalação de sistema operacional anterior quando o Windows PE é iniciado. O local do disco rígido onde o sistema operacional é instalado é armazenado nessa variável. Você pode configurar sua sequência de tarefas para recuperar esse valor do ambiente e usá-lo a fim de especificar o mesmo local de disco rígido a ser usado para o novo sistema operacional.

### <a name="OSDMigrateUsmtPackageID"></a> _OSDMigrateUsmtPackageID

*Aplica-se à etapa [Capturar Estado do Usuário](task-sequence-steps.md#BKMK_CaptureUserState).*

(entrada)

Especifica a ID do pacote do Configuration Manager que contém os arquivos do USMT. Esta variável é obrigatória.

### <a name="OSDMigrateUsmtRestorePackageID"></a> _OSDMigrateUsmtRestorePackageID

*Aplica-se à etapa [Restaurar Estado do Usuário](task-sequence-steps.md#BKMK_RestoreUserState).*

(entrada)

Especifica a ID do pacote do Configuration Manager que contém os arquivos do USMT. Esta variável é obrigatória.

### <a name="SMSTSAdvertID"></a> _SMSTSAdvertID

Armazena a ID exclusiva da atual implantação de sequência de tarefas em execução Ele usa o mesmo formato que uma ID de implantação de distribuição de software do Configuration Manager. Se a sequência de tarefas estiver sendo executada por meio de uma mídia autônoma, esta variável não será definida.

#### <a name="example"></a>Exemplo

`ABC20001`

### <a name="SMSTSAssetTag"></a> _SMSTSAssetTag

*Aplica-se à etapa [Definir Variáveis Dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Especifica a marca de ativo do computador.

### <a name="SMSTSBootImageID"></a> _SMSTSBootImageID

Se a sequência de tarefas em execução no momento fizer referência a um pacote de imagem de inicialização, essa variável armazenará a ID do pacote da imagem de inicialização. Se a sequência de tarefas não fizer referência a um pacote de imagem de inicialização, essa variável não será definida.

#### <a name="example"></a>Exemplo

`ABC00001`  

### <a name="SMSTSBootUEFI"></a> _SMSTSBootUEFI

A sequência de tarefas define a variável ao detectar um computador no modo UEFI.

### <a name="SMSTSClientCache"></a> _SMSTSClientCache

<!-- SCCMDocs issue 1400 -->
A sequência de tarefas define essa variável quando armazena em cache o conteúdo na unidade local. A variável contém o caminho para o cache. Se essa variável não existir, não haverá cache.

### <a name="SMSTSClientGUID"></a> _SMSTSClientGUID

Armazena o valor da GUID do cliente do Configuration Manager. Se a sequência de tarefas estiver sendo executada por uma mídia autônoma, esta variável não será definida.

#### <a name="example"></a>Exemplo

`0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c`

### <a name="SMSTSCurrentActionName"></a> _SMSTSCurrentActionName

Especifica o nome da etapa de sequência de tarefas em execução no momento. Essa variável é definida antes que o gerenciador de sequência de tarefas seja executado a cada etapa individual.

#### <a name="example"></a>Exemplo

`run command line`

### <a name="SMSTSDefaultGateways"></a> _SMSTSDefaultGateways

*Aplica-se à etapa [Definir Variáveis Dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Especifica os gateways padrão usados pelo computador.

### <a name="SMSTSDownloadOnDemand"></a> _SMSTSDownloadOnDemand

Se a sequência de tarefas atual estiver em execução no modo de download sob demanda, essa variável será `true`. O modo de download sob demanda significa que o gerenciador de sequência de tarefas baixa o conteúdo localmente apenas quando ele precisar acessar o conteúdo.

### <a name="SMSTSInWinPE"></a> _SMSTSInWinPE

Quando a etapa da sequência de tarefas atual estiver em execução no Windows PE, essa variável será `true`. Teste essa variável de sequência de tarefas para determinar o ambiente do sistema operacional atual.

### <a name="SMSTSIPAddresses"></a> _SMSTSIPAddresses

*Aplica-se à etapa [Definir Variáveis Dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Especifica os endereços IP usados pelo computador.

### <a name="SMSTSLastActionName"></a> _SMSTSLastActionName

*Da versão 1810 em diante*  

Armazena o nome da última ação executada. Esta variável está relacionada a **_SMSTSLastActionRetCode**. A sequência de tarefas registra esses valores no arquivo smsts.log. Essa variável é útil ao solucionar problemas de uma sequência de tarefas. Quando uma etapa falha, um script personalizado pode incluir o nome da etapa junto com o código de retorno.

### <a name="SMSTSLastActionRetCode"></a> _SMSTSLastActionRetCode

Armazena o código de retorno da última ação executada. Essa variável pode ser usada como uma condição para determinar se a próxima etapa é executada.

#### <a name="example"></a>Exemplo

`0`

### <a name="SMSTSLastActionSucceeded"></a> _SMSTSLastActionSucceeded

- Se a etapa anterior for bem-sucedida, essa variável será `true`.  

- Se a etapa anterior falhar, será `false`.  

- Se a sequência de tarefas ignorar a ação anterior porque a etapa foi desabilitada ou a condição associada foi avaliada como **false**, essa variável não será redefinida. Ela ainda mantém o valor para a ação anterior.  

### <a name="SMSTSLaunchMode"></a> _SMSTSLaunchMode

Especifica que a sequência de tarefas começou por um dos seguintes métodos:  

- **SMS**: o cliente do Configuration Manager, como quando um usuário o inicia pelo Centro de Software
- **UFD**: mídia USB herdada
- **UFD+FORMAT**: mídia USB mais recente
- **CD**: um CD inicializável
- **DVD**: um DVD inicializável
- **PXE**: inicialização de rede com PXE
- **HD**: mídia em pré-teste em um disco rígido

### <a name="SMSTSLogPath"></a> _SMSTSLogPath

Armazena o caminho completo do diretório de log. Use esse valor para determinar onde as etapas de sequência de tarefas registram suas ações. Esse valor não é definido quando não houver um disco rígido disponível.

### <a name="SMSTSMacAddresses"></a> _SMSTSMacAddresses

*Aplica-se à etapa [Definir Variáveis Dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Especifica os endereços MAC usados pelo computador.

### <a name="SMSTSMachineName"></a> _SMSTSMachineName

Armazena e especifica o nome do computador. Armazena o nome do computador que a sequência de tarefas usa para registrar todas as mensagens de status. Para alterar o nome do computador no novo sistema operacional, use a variável [OSDComputerName](#OSDComputerName-input).

### <a name="SMSTSMake"></a> _SMSTSMake

*Aplica-se à etapa [Definir Variáveis Dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Especifica a marca do computador.

### <a name="SMSTSMDataPath"></a> _SMSTSMDataPath

Especifica o caminho definido pela variável [SMSTSLocalDataDrive](#SMSTSLocalDataDrive). Ao definir SMSTSLocalDataDrive antes do início da sequência de tarefas, como ao definir uma variável de coleta, o Configuration Manager define a variável _SMSTSMDataPath após o início da sequência de tarefas.

### <a name="SMSTSMediaType"></a> _SMSTSMediaType

Especifica o tipo de mídia usada para iniciar a instalação. Exemplos de tipos de mídia são mídia de inicialização, mídia cheia, PXE e mídia pré-configurada.

### <a name="SMSTSModel"></a> _SMSTSModel

*Aplica-se à etapa [Definir Variáveis Dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Especifica o modelo do computador.

### <a name="SMSTSMP"></a> _SMSTSMP

Armazena a URL ou endereço IP de um ponto de gerenciamento do Configuration Manager.

### <a name="SMSTSMPPort"></a> _SMSTSMPPort

Armazena o número da porta de um ponto de gerenciamento do Configuration Manager.

### <a name="SMSTSOrgName"></a> _SMSTSOrgName

Armazena o nome do título de identidade visual que a sequência de tarefas exibe na caixa de diálogo de progresso.

### <a name="SMSTSOSUpgradeActionReturnCode"></a> _SMSTSOSUpgradeActionReturnCode

*Aplica-se à etapa [Atualizar Sistema Operacional](task-sequence-steps.md#BKMK_UpgradeOS).*

Armazena o valor do código de saída que a Instalação do Windows retorna para indicar êxito ou falha. Essa variável é útil com a opção de linha de comando `/Compat`.

#### <a name="example"></a>Exemplo

Após a conclusão de uma varredura somente compat, execute ações nas etapas posteriores dependendo do código de saída de falha ou de êxito. Em caso de êxito, inicie o upgrade. Ou defina um marcador no ambiente para coletar com o inventário de hardware. Por exemplo, adicione um arquivo ou defina uma chave de registro. Use esse marcador para criar uma coleção de computadores que estão prontos para upgrade ou que exigem uma ação antes do upgrade.

### <a name="SMSTSPackageID"></a> _SMSTSPackageID

Armazena a ID da atual sequência de tarefas em execução Esta ID usa o mesmo formato que uma ID de pacote do Configuration Manager.

#### <a name="example"></a>Exemplo

`HJT00001`

### <a name="SMSTSPackageName"></a> _SMSTSPackageName

Armazena o nome da sequência de tarefas atual em execução. Um administrador do Configuration Manager especifica esse nome ao criar a sequência de tarefas.

#### <a name="example"></a>Exemplo

`Deploy Windows 10 task sequence`

### <a name="SMSTSRunFromDP"></a> _SMSTSRunFromDP

Definido como `true` se a sequência de tarefas atual estiver em execução no modo Executar do Ponto de Distribuição. Esse modo significa que o gerenciador da sequência de tarefas obtém o pacote necessário para compartilhamentos de ponto de distribuição.

### <a name="SMSTSSerialNumber"></a> _SMSTSSerialNumber

*Aplica-se à etapa [Definir Variáveis Dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Especifica o número de série do computador.

### <a name="SMSTSSetupRollback"></a> _SMSTSSetupRollback

Especifica se a instalação do Windows executou uma operação de reversão durante uma atualização in-loco. Os valores da variável podem ser `true` ou `false`.

### <a name="SMSTSSiteCode"></a> _SMSTSSiteCode

Especifica o código do site do Configuration Manager.

#### <a name="example"></a>Exemplo

`ABC`

### <a name="SMSTSTimezone"></a> _SMSTSTimezone

Essa variável armazena as informações de fuso horário no seguinte formato:

```
Bias,StandardBias,DaylightBias,StandardDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,DaylightDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,StandardName,DaylightName
```

#### <a name="example"></a>Exemplo

Para o fuso horário **Hora padrão da Costa Leste (EUA e Canadá)** :

```
300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0,Eastern Standard Time,Eastern Daylight Time
```

### <a name="SMSTSType"></a> _SMSTSType

Especifica o tipo da sequência de tarefas em execução atual. Pode ter um dos seguintes valores:  

- **1**: indica uma sequência de tarefas genérica
- **2**: uma sequência de tarefas de implantação de sistema operacional

### <a name="SMSTSUseCRL"></a> _SMSTSUseCRL

Quando a sequência de tarefas usa HTTPS para se comunicar com o ponto de gerenciamento, essa variável especifica se ela usa a CRL (lista de certificados revogados).

### <a name="SMSTSUserStarted"></a> _SMSTSUserStarted

Especifica se uma sequência de tarefas foi iniciada por um usuário. Essa variável é definida somente se a sequência de tarefas é iniciada por meio do Centro de Software. Por exemplo, se [_SMSTSLaunchMode](#SMSTSLaunchMode) está definido como `SMS`.

Esta variável pode ter os seguintes valores:  

- `true`: especifica que a sequência de tarefas é iniciada manualmente por um usuário no Centro de Software.  

- `false`: especifica que a sequência de tarefas é iniciada automaticamente pelo agendamento do Configuration Manager.

### <a name="SMSTSUseSSL"></a> _SMSTSUseSSL

Especifica se a sequência de tarefas usa SSL para se comunicar com o ponto de gerenciamento do Configuration Manager. Se você configurar os sistemas de site como HTTPS, o valor será definido como `true`.

### <a name="SMSTSUUID"></a> _SMSTSUUID

*Aplica-se à etapa [Definir Variáveis Dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Especifica o UUID do computador.

### <a name="SMSTSWTG"></a> _SMSTSWTG

Especifica se o computador está executando como um dispositivo Windows To Go.

### <a name="TSAppInstallStatus"></a> _TSAppInstallStatus

A sequência de tarefas define esta variável de acordo com o status de instalação do aplicativo durante a etapa [Instalar Aplicativo](task-sequence-steps.md#BKMK_InstallApplication). Ela define um dos seguintes valores:  

- **Indefinido**: a etapa Instalar Aplicativo não foi executada.  

- **Erro**: pelo menos um aplicativo falhou devido a um erro durante a etapa Instalar Aplicativo.  

- **Aviso**: nenhum erro ocorreu durante a etapa Instalar Aplicativo. Um ou mais aplicativos, ou uma dependência necessária, não foram instalados porque um requisito não foi atendido.  

- **Êxito**: não há nenhum erro ou aviso detectado durante a etapa Instalar Aplicativo.  

### <a name="OSDAdapter"></a> OSDAdapter

*Aplica-se à etapa [Aplicar Configurações de Rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(entrada)

Esta variável de sequência de tarefas é uma variável de *matriz*. Cada elemento na matriz representa as configurações para um único adaptador de rede no computador. Acesse as configurações para cada adaptador combinando o nome de variável de matriz com o índice do adaptador de rede baseado em zero e o nome da propriedade.

Se esta etapa configurar vários adaptadores de rede, ela definirá as propriedades para o *segundo* adaptador de rede usando o índice **1** no nome da variável. Por exemplo: OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList e OSDAdapter1DNSDomain.

Use os seguintes nomes de variáveis para definir as propriedades do *primeiro* adaptador de rede para a etapa a ser configurada:

#### <a name="osdadapter0enabledhcp"></a>OSDAdapter0EnableDHCP

Essa configuração é necessária. Os possíveis valores são `True` ou `False`. Por exemplo:

`true`: habilitar o protocolo Dynamic Host Configuration Protocol (DHCP) para o adaptador

#### <a name="osdadapter0ipaddresslist"></a>OSDAdapter0IPAddressList

Lista delimitada por vírgulas dos endereços IP do adaptador. Essa propriedade será ignorada, a menos que **EnableDHCP** seja definido como `false`. Essa configuração é necessária.

#### <a name="osdadapter0subnetmask"></a>OSDAdapter0SubnetMask

Lista delimitada por vírgulas das máscaras de sub-rede. Essa propriedade será ignorada, a menos que **EnableDHCP** seja definido como `false`. Essa configuração é necessária.

#### <a name="osdadapter0gateways"></a>OSDAdapter0Gateways

Lista delimitada por vírgulas dos endereços IP de gateway. Essa propriedade será ignorada, a menos que **EnableDHCP** seja definido como `false`. Essa configuração é necessária.

#### <a name="osdadapter0dnsdomain"></a>OSDAdapter0DNSDomain

Domínio DNS (Sistema de Nomes de Domínio) do adaptador.

#### <a name="osdadapter0dnsserverlist"></a>OSDAdapter0DNSServerList

Lista delimitada por vírgulas dos servidores DNS do adaptador. Essa configuração é necessária.

#### <a name="osdadapter0enablednsregistration"></a>OSDAdapter0EnableDNSRegistration

Definido como `true` para registrar o endereço IP para o adaptador no DNS.

#### <a name="osdadapter0enablefulldnsregistration"></a>OSDAdapter0EnableFullDNSRegistration

Definido como `true` para registrar o endereço IP do adaptador no DNS com o nome de DNS completo do computador.

#### <a name="osdadapter0enableipprotocolfiltering"></a>OSDAdapter0EnableIPProtocolFiltering

Definido como `true` para habilitar a filtragem de protocolo IP no adaptador.

#### <a name="osdadapter0ipprotocolfilterlist"></a>OSDAdapter0IPProtocolFilterList

Lista delimitada por vírgulas de protocolos que podem ser executados com IP. Essa propriedade será ignorada se **EnableIPProtocolFiltering** estiver definido como `false`.

#### <a name="osdadapter0enabletcpfiltering"></a>OSDAdapter0EnableTCPFiltering

Definido como `true` para habilitar a filtragem de porta TCP para o adaptador.

#### <a name="osdadapter0tcpfilterportlist"></a>OSDAdapter0TCPFilterPortList

Lista delimitada por vírgulas de portas que receberão permissões de acesso para TCP. Essa propriedade será ignorada se **EnableTCPFiltering** estiver definido como `false`.

#### <a name="osdadapter0tcpipnetbiosoptions"></a>OSDAdapter0TcpipNetbiosOptions

Opções de NetBIOS por TCP/IP. Os valores possíveis são:  

- `0`: usar as configurações de NetBIOS do servidor DHCP  
- `1`: habilitar o NetBIOS por TCP/IP  
- `2`: desabilitar o NetBIOS por TCP/IP  

#### <a name="osdadapter0enablewins"></a>OSDAdapter0EnableWINS

Definido como `true` para usar o WINS para resolução de nome.

#### <a name="osdadapter0winsserverlist"></a>OSDAdapter0WINSServerList

Lista delimitada por vírgulas dos endereços IP do servidor WINS. Essa propriedade será ignorada, a menos que **EnableWINS** esteja definido como `true`.

#### <a name="osdadapter0macaddress"></a>OSDAdapter0MacAddress

Endereço MAC usado para fazer a correspondência das configurações com o adaptador de rede físico.

#### <a name="osdadapter0name"></a>OSDAdapter0Name

O nome da conexão de rede como aparece no programa do painel de controle das conexões de rede. O nome tem entre 0 e 255 caracteres de comprimento.

#### <a name="osdadapter0index"></a>OSDAdapter0Index

Índice das configurações do adaptador de rede na matriz de configurações.

#### <a name="example"></a>Exemplo

- **OSDAdapterCount** = `1`  
- **OSDAdapter0EnableDHCP** = `FALSE`  
- **OSDAdapter0IPAddressList** = `192.168.0.40`  
- **OSDAdapter0SubnetMask** = `255.255.255.0`  
- **OSDAdapter0Gateways** = `192.168.0.1`  
- **OSDAdapter0DNSSuffix** = `contoso.com`  

### <a name="OSDAdapterCount"></a> OSDAdapterCount

*Aplica-se à etapa [Aplicar Configurações de Rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(entrada)

Especifica o número de adaptadores de rede instalados no computador de destino. Ao definir o valor de **OSDAdapterCount**, defina também todas as opções de configuração de cada adaptador.

Por exemplo, se você definir o valor de **OSDAdapter0TCPIPNetbiosOptions** do primeiro adaptador, é preciso configurar todos os valores do adaptador.

Se você não especificar esse valor, a sequência de tarefas ignorará todos os valores de **OSDAdapter**.

### <a name="OSDApplyDriverBootCriticalContentUniqueID"></a> OSDApplyDriverBootCriticalContentUniqueID

*Aplica-se à etapa [Aplicar Pacote de Driver](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(entrada)

Especifica a ID de conteúdo do driver do dispositivo de armazenamento em massa a ser instalada do pacote de drivers. Se esta variável não for especificada, nenhum driver de armazenamento em massa será instalado.

### <a name="OSDApplyDriverBootCriticalHardwareComponent"></a> OSDApplyDriverBootCriticalHardwareComponent

*Aplica-se à etapa [Aplicar Pacote de Driver](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(entrada)

Especifica se um driver de dispositivo de armazenamento em massa estiver instalado, essa variável deverá ser **scsi**.

Se [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) estiver definido, essa variável será obrigatória.

### <a name="OSDApplyDriverBootCriticalID"></a> OSDApplyDriverBootCriticalID

*Aplica-se à etapa [Aplicar Pacote de Driver](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(entrada)

Especifica a ID crítica de inicialização do driver do dispositivo de armazenamento em massa a ser instalada. Esta ID é listada na seção **scsi** do arquivo txtsetup.oem do driver de dispositivo.

Se [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) estiver definido, essa variável será obrigatória.

### <a name="OSDApplyDriverBootCriticalINFFile"></a> OSDApplyDriverBootCriticalINFFile

*Aplica-se à etapa [Aplicar Pacote de Driver](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(entrada)

Especifica o arquivo INF do driver de armazenamento em massa a ser instalado.

Se [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) estiver definido, essa variável será obrigatória.

### <a name="OSDAutoApplyDriverBestMatch"></a> OSDAutoApplyDriverBestMatch

*Aplica-se à etapa [Aplicar Drivers Automaticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

(entrada)

Se houver vários drivers de dispositivo no catálogo de drivers que são compatíveis com um dispositivo de hardware, essa variável determinará a ação da etapa.

#### <a name="valid-values"></a>Valores válidos

- `true` (padrão): instala somente o melhor driver de dispositivo  

- `false`: instala todos os drivers de dispositivo compatíveis e o Windows escolhe o melhor driver a usar  

### <a name="OSDAutoApplyDriverCategoryList"></a> OSDAutoApplyDriverCategoryList

*Aplica-se à etapa [Aplicar Drivers Automaticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

(entrada)

Uma lista delimitada por vírgulas de IDs exclusivas de categorias do catálogo de drivers. A etapa **Aplicação Automática de Driver** considera apenas os drivers em pelo menos uma das categorias especificadas. Esse valor é opcional e não está definido por padrão. Obtenha as IDs de categoria disponíveis enumerando a lista de objetos **SMS_CategoryInstance** no site.

### <a name="OSDBitLockerRecoveryPassword"></a> OSDBitLockerRecoveryPassword

*Aplica-se à etapa [Habilitar BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).*

(entrada)

Ao invés de gerar uma senha aleatória de recuperação, a etapa **Habilitar BitLocker** usa o valor especificado como a senha de recuperação. O valor deve ser uma senha de recuperação do BitLocker numérica e válida.

### <a name="OSDBitLockerStartupKey"></a> OSDBitLockerStartupKey

*Aplica-se à etapa [Habilitar BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).*

(entrada)

Em vez de gerar uma chave de inicialização aleatória para a opção de gerenciamento de chaves **Chave de Inicialização somente em USB**, a etapa **Habilitar BitLocker** usa o TPM (Trusted Platform Module) como a chave de inicialização. O valor deve ser uma chave de inicialização do BitLocker válida, codificada em Base64 e de 256 bits.

### <a name="OSDCaptureAccount"></a> OSDCaptureAccount

*Aplica-se à etapa [Capturar Imagem do SO](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(entrada)

Especifica um nome de conta do Windows que tem permissão para armazenar a imagem capturada em um compartilhamento de rede ([OSDCaptureDestination](#OSDCaptureDestination)). Especifique também a [OSDCaptureAccountPassword](#OSDCaptureAccountPassword).

Para saber mais sobre a conta de imagem do sistema operacional de captura, consulte [Contas](/sccm/core/plan-design/hierarchy/accounts#capture-os-image-account).

### <a name="OSDCaptureAccountPassword"></a> OSDCaptureAccountPassword

*Aplica-se à etapa [Capturar Imagem do SO](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(entrada)

Especifica a senha da conta do Windows ([OSDCaptureAccount](#OSDCaptureAccount)) usada para armazenar a imagem capturada em um compartilhamento de rede ([OSDCaptureDestination](#OSDCaptureDestination)).

### <a name="OSDCaptureDestination"></a> OSDCaptureDestination

*Aplica-se à etapa [Capturar Imagem do SO](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(entrada)

Especifica o local em que a sequência de tarefas salva a imagem capturada do sistema operacional. O comprimento máximo do nome do diretório é de 255 caracteres. Se o compartilhamento de rede requer autenticação, especifique as variáveis [OSDCaptureAccount](#OSDCaptureAccount) e [OSDCaptureAccountPassword](#OSDCaptureAccountPassword).

### <a name="OSDComputerName-input"></a> OSDComputerName (entrada)

*Aplica-se à etapa [Aplicar Configurações do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Especifica o nome do computador de destino.

#### <a name="example"></a>Exemplo

`%_SMSTSMachineName%` (padrão)

### <a name="OSDComputerName-output"></a> OSDComputerName (saída)

*Aplica-se à etapa [Capturar Configurações do Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

Defina como o nome NetBIOS do computador. O valor será definido somente se a variável [OSDMigrateComputerName](#OSDMigrateComputerName) for definida como `true`.

### <a name="OSDConfigFileName"></a> OSDConfigFileName

*Aplica-se à etapa [Aplicar Imagem do SO](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).*

(entrada)

Especifica o nome do arquivo de resposta da implantação do sistema operacional que está associado ao pacote de imagem de implantação do sistema operacional.  

### <a name="OSDDataImageIndex"></a> OSDDataImageIndex

*Aplica-se à etapa [Aplicar Imagem de Dados](task-sequence-steps.md#BKMK_ApplyDataImage).*

(entrada)

Especifica o valor de índice da imagem aplicada ao computador de destino.

### <a name="OSDDiskIndex"></a> OSDDiskIndex

*Aplica-se à etapa [Formatar e Particionar Disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(entrada)

Especifica o número de discos físicos a ser particionados.

### <a name="OSDDNSDomain"></a> OSDDNSDomain

*Aplica-se à etapa [Aplicar Configurações de Rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(entrada)

Especifica o servidor DNS primário usado pelo computador de destino.

### <a name="OSDDNSSuffixSearchOrder"></a> OSDDNSSuffixSearchOrder

*Aplica-se à etapa [Aplicar Configurações de Rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(entrada)

Especifica a ordem de pesquisa DNS para o computador de destino.

### <a name="OSDDomainName"></a> OSDDomainName

*Aplica-se à etapa [Aplicar Configurações de Rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(entrada)

Especifica o nome de um domínio do Active Directory ingressado pelo computador de destino. O valor especificado deve ser um nome de domínio válido dos Serviços de Domínio do Active Directory.

### <a name="OSDDomainOUName"></a> OSDDomainOUName

*Aplica-se à etapa [Aplicar Configurações de Rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(entrada)

Especifica o nome de formato RFC 1779 da UO (unidade organizacional) ingressada pelo computador de destino. Se especificado, o valor deve conter o caminho completo.

#### <a name="example"></a>Exemplo

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`

### <a name="OSDDoNotLogCommand"></a> OSDDoNotLogCommand

<!--1358493-->
*A partir da versão 1806*  
*Aplica-se à etapa [Instalar Pacote](/sccm/osd/understand/task-sequence-steps#BKMK_InstallPackage).*

*A partir da versão 1902*  
*Aplica-se à etapa [Executar Linha de Comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine).*

(entrada)

Para impedir que os dados potencialmente confidenciais sejam exibidos ou registrados, defina a variável como `TRUE`. Essa variável mascara o nome do programa em **smsts.log** durante uma etapa **Instalar Pacote**.

A partir da versão 1902, quando você define essa variável como `TRUE`, ela também oculta a linha de comando da etapa **Executar Linha de Comando** no arquivo de log.<!--3654172-->

### <a name="OSDEnableTCPIPFiltering"></a> OSDEnableTCPIPFiltering

*Aplica-se à etapa [Aplicar Configurações de Rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(entrada)

Especifica se a filtragem de TCP/IP está habilitada.

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false` (padrão)  

### <a name="OSDGPTBootDisk"></a> OSDGPTBootDisk

*Aplica-se à etapa [Formatar e Particionar Disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(entrada)

Especifica se uma partição EFI deve ser criada em um disco rígido GPT. Computadores baseados em EFI usam essa partição como o disco de inicialização.

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false` (padrão)

### <a name="OSDImageCreator"></a> OSDImageCreator

*Aplica-se à etapa [Capturar Imagem do SO](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(entrada)

Um nome opcional do usuário que criou a imagem. Este nome é armazenado no arquivo WIM. O comprimento máximo do nome de usuário é de 255 caracteres.

### <a name="OSDImageDescription"></a> OSDImageDescription

*Aplica-se à etapa [Capturar Imagem do SO](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(entrada)

Uma descrição opcional da imagem capturada do sistema operacional definida pelo usuário. Essa descrição é armazenada no arquivo WIM. O comprimento máximo da descrição é de 255 caracteres.

### <a name="OSDImageIndex"></a> OSDImageIndex

*Aplica-se à etapa [Aplicar Imagem do SO](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).*

(entrada)

Especifica o valor de índice da imagem do arquivo WIM aplicado ao computador de destino.

### <a name="OSDImageVersion"></a> OSDImageVersion

*Aplica-se à etapa [Capturar Imagem do SO](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(entrada)

Um número de versão opcional definido pelo usuário para atribuir à imagem capturada do sistema operacional. Esse número de versão é armazenado no arquivo WIM. Esse valor pode ser qualquer combinação de caracteres alfanuméricos com um comprimento máximo de 32 caracteres.

### <a name="OSDInstallDriversAdditionalOptions"></a> OSDInstallDriversAdditionalOptions

<!--516679/2840016-->
*A partir da versão 1806*  
*Aplica-se à etapa [Aplicar Pacote de Driver](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyDriverPackage).*

(entrada)

Especifica mais opções para adicionar à linha de comando do DISM ao aplicar um pacote de driver. A sequência de tarefas não verifica as opções de linha de comando.

Para usar essa variável, habilite a configuração **Instalar o pacote de driver pelo DISM em execução com opção de recurso** na etapa **Aplicar Pacote de Driver**.

Para saber mais, confira [Opções de linha de comando do DISM do Windows 10](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options).

### <a name="OSDJoinAccount"></a> OSDJoinAccount

*Aplica-se às seguintes etapas:*  

- [Aplicar Configurações de Rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Ingressar no Domínio ou Grupo de Trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(entrada)

Especifica a conta de usuário do domínio usada para adicionar o computador de destino ao domínio. Essa variável é necessária ao ingressar em um domínio.

Para saber mais sobre a conta de entrada no domínio da sequência de tarefas, confira [Contas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-domain-join-account).

### <a name="OSDJoinDomainName"></a> OSDJoinDomainName

*Aplica-se à etapa [Ingressar no Domínio ou Grupo de Trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(entrada)

Especifica o nome de um domínio do Active Directory ingressado pelo computador de destino. O tamanho do nome de domínio precisa ter entre 1 e 255 caracteres.

### <a name="OSDJoinDomainOUName"></a> OSDJoinDomainOUName

*Aplica-se à etapa [Ingressar no Domínio ou Grupo de Trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(entrada)

Especifica o nome de formato RFC 1779 da UO (unidade organizacional) ingressada pelo computador de destino. Se especificado, o valor deve conter o caminho completo. O tamanho do nome da UO precisa ter entre 0 e 32.767 caracteres. Esse valor não será definido se a variável [OSDJoinType](#OSDJoinType) for definida como `1` (ingressar no grupo de trabalho).

#### <a name="example"></a>Exemplo

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`  

### <a name="OSDJoinPassword"></a> OSDJoinPassword

*Aplica-se às seguintes etapas:*  

- [Aplicar Configurações de Rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Ingressar no Domínio ou Grupo de Trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(entrada)

Especifica a senha de [OSDJoinAccount](#OSDJoinAccount) usada pelo computador de destino para ingressar no domínio do Active Directory. Se o ambiente da sequência de tarefas não incluir essa variável, a Instalação do Windows tentará usar uma senha em branco. Se a variável [OSDJoinType](#OSDJoinType) for definida como `0` (ingressar no domínio), esse valor será obrigatório.

### <a name="OSDJoinSkipReboot"></a> OSDJoinSkipReboot

*Aplica-se à etapa [Ingressar no Domínio ou Grupo de Trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(entrada)

Especifica se é necessário ignorar a reinicialização depois que o computador de destino ingressar no domínio ou no grupo de trabalho.

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false`  

### <a name="OSDJoinType"></a> OSDJoinType

*Aplica-se à etapa [Ingressar no Domínio ou Grupo de Trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(entrada)

Especifica se o computador de destino ingressa em um domínio ou grupo de trabalho do Windows.

#### <a name="valid-values"></a>Valores válidos

- `0`: ingressar o computador de destino em um domínio do Windows  
- `1`: ingressar o computador de destino em um grupo de trabalho  

### <a name="OSDJoinWorkgroupName"></a> OSDJoinWorkgroupName

*Aplica-se à etapa [Ingressar no Domínio ou Grupo de Trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(entrada)

Especifica o nome de um grupo de trabalho ingressado pelo computador de destino. O comprimento do nome do grupo de trabalho deve estar entre 1 e 32 caracteres.

### <a name="OSDKeepActivation"></a> OSDKeepActivation

*Aplica-se à etapa [Preparar o Windows para Captura](task-sequence-steps.md#BKMK_PrepareWindowsforCapture).*

(entrada)

Especifica se o sysprep redefine o sinalizador de ativação do produto.

#### <a name="valid-values"></a>Valores válidos

- `true`
- `false` (padrão)

### <a name="OSDLocalAdminPassword"></a> OSDLocalAdminPassword

*Aplica-se à etapa [Aplicar Configurações do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(entrada)

Especifica a senha da conta do administrador local. Se você habilitar a opção **Gerar a senha de administrador local aleatoriamente e desabilitar a conta em todas as plataformas compatíveis**, esta etapa ignorará esta variável. O valor especificado deve estar entre 1 e 255 caracteres.

### <a name="OSDLogPowerShellParameters"></a> OSDLogPowerShellParameters

<!--3556028-->
*A partir da versão 1902*  
*Aplicável à etapa [Executar Script do PowerShell](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript).*

(entrada)

Para evitar que dados potencialmente sensíveis sejam registrados, a etapa **Executar Script do PowerShell** não registra parâmetros de script no arquivo **smsts.log**. Para incluir os parâmetros de script no log de sequência de tarefas, defina essa variável como **TRUE**.

### <a name="OSDMigrateAdapterSettings"></a> OSDMigrateAdapterSettings

*Aplica-se à etapa [Capturar Configurações de Rede](task-sequence-steps.md#BKMK_CaptureNetworkSettings).*

(entrada)

Especifica se a sequência de tarefas captura as informações do adaptador de rede. Essas informações incluem definições de configuração de TCP/IP, DNS e WINS.

#### <a name="valid-values"></a>Valores válidos

- `true` (padrão)
- `false`

### <a name="OSDMigrateAdditionalCaptureOptions"></a> OSDMigrateAdditionalCaptureOptions

*Aplica-se à etapa [Capturar Estado do Usuário](task-sequence-steps.md#BKMK_CaptureUserState).*

(entrada)

Especifique opções de linha de comando adicionais para a USMT (Ferramenta de Migração do Usuário) que a sequência de tarefas usa para capturar o estado do usuário. A etapa não expõe estas configurações no editor da sequência de tarefas. Especifique essas opções como uma cadeia de caracteres, que acrescenta a sequência de tarefas à linha de comando da USMT gerada automaticamente para ScanState.

As opções da USMT especificadas com essa variável da sequência de tarefas não são validadas quanto à precisão antes da execução da sequência de tarefas.

Para saber mais sobre as opções disponíveis, consulte [Sintaxe do ScanState](https://docs.microsoft.com/windows/deployment/usmt/usmt-scanstate-syntax).

### <a name="OSDMigrateAdditionalRestoreOptions"></a> OSDMigrateAdditionalRestoreOptions

*Aplica-se à etapa [Restaurar Estado do Usuário](task-sequence-steps.md#BKMK_RestoreUserState).*

(entrada)

Especifica opções adicionais da linha de comando da USMT (Ferramenta de Migração do Usuário) para migração, que a sequência de tarefas usa ao restaurar o estado de usuário. Especifique as opções adicionais como uma cadeia de caracteres, que acrescenta a sequência de tarefas à linha de comando da USMT gerada automaticamente para LoadState.

As opções da USMT especificadas com essa variável da sequência de tarefas não são validadas quanto à precisão antes da execução da sequência de tarefas.

Para saber mais sobre as opções disponíveis, consulte [Sintaxe do LoadState](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax).

### <a name="OSDMigrateComputerName"></a> OSDMigrateComputerName

*Aplica-se à etapa [Capturar Configurações do Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

(entrada)

Especifica se o nome do computador é migrado.

#### <a name="valid-values"></a>Valores válidos

- `true` (padrão). A variável [OSDComputerName (saída)](#OSDComputerName-output) será definida como o nome NetBIOS do computador.  
- `false`  

### <a name="OSDMigrateConfigFiles"></a> OSDMigrateConfigFiles

*Aplica-se à etapa [Capturar Estado do Usuário](task-sequence-steps.md#BKMK_CaptureUserState).*

(entrada)

Especifica os arquivos de configuração usados para controlar a captura de perfis de usuário. Essa variável será usada apenas se [OSDMigrateMode](#OSDMigrateMode) estiver definido como `Advanced`. Esse valor de lista delimitado por vírgulas é definido para executar a migração personalizada de perfil do usuário.

#### <a name="example"></a>Exemplo

`miguser.xml,migsys.xml,migapps.xml`  

### <a name="OSDMigrateContinueOnLockedFiles"></a> OSDMigrateContinueOnLockedFiles

*Aplica-se à etapa [Capturar Estado do Usuário](task-sequence-steps.md#BKMK_CaptureUserState).*

(entrada)

Se a USMT não puder capturar alguns arquivos, essa variável permitirá que a captura de estado do usuário prossiga.

#### <a name="valid-values"></a>Valores válidos

- `true` (padrão)  
- `false`  

### <a name="OSDMigrateContinueOnRestore"></a> OSDMigrateContinueOnRestore

*Aplica-se à etapa [Restaurar Estado do Usuário](task-sequence-steps.md#BKMK_RestoreUserState).*

(entrada)

Continue o processo, mesmo se a USMT não puder restaurar alguns arquivos.

#### <a name="valid-values"></a>Valores válidos

- `true` (padrão)  
- `false`  

### <a name="OSDMigrateEnableVerboseLogging"></a> OSDMigrateEnableVerboseLogging

*Aplica-se às seguintes etapas:*  

- [Capturar Estado do Usuário](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Restaurar Estado do Usuário](task-sequence-steps.md#BKMK_RestoreUserState)  

(entrada)

Habilita o log detalhado para USMT. A etapa requer esse valor.

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false` (padrão)  

### <a name="OSDMigrateLocalAccounts"></a> OSDMigrateLocalAccounts

*Aplica-se à etapa [Restaurar Estado do Usuário](task-sequence-steps.md#BKMK_RestoreUserState).*

(entrada)

Especifica se a conta do computador local é restaurada.

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false` (padrão)  

### <a name="OSDMigrateLocalAccountPassword"></a> OSDMigrateLocalAccountPassword

*Aplica-se à etapa [Restaurar Estado do Usuário](task-sequence-steps.md#BKMK_RestoreUserState).*

(entrada)

Se a variável [OSDMigrateLocalAccounts](#OSDMigrateLocalAccounts) for `true`, essa variável precisará conter a senha atribuída a *todas* as contas locais migradas. A USMT atribui a mesma senha a todas as contas locais migradas. Considere esta senha como temporária e altere-a posteriormente usando algum outro método.

### <a name="OSDMigrateMode"></a> OSDMigrateMode

*Aplica-se à etapa [Capturar Estado do Usuário](task-sequence-steps.md#BKMK_CaptureUserState).*

(entrada)

Permite que você personalize os arquivos que a USMT captura.

#### <a name="valid-values"></a>Valores válidos

- `Simple`: a sequência de tarefas usará somente os arquivos padrão de configuração da USMT  

- `Advanced`: a variável [OSDMigrateConfigFiles](#OSDMigrateConfigFiles) da sequência de tarefas especificará os arquivos de configuração que a USMT usa  

### <a name="OSDMigrateNetworkMembership"></a> OSDMigrateNetworkMembership

*Aplica-se à etapa [Capturar Configurações de Rede](task-sequence-steps.md#BKMK_CaptureNetworkSettings).*

(entrada)

Especifica se a sequência de tarefas migra as informações de associação de grupo de trabalho ou domínio.

#### <a name="valid-values"></a>Valores válidos

- `true` (padrão)
- `false`

### <a name="OSDMigrateRegistrationInfo"></a> OSDMigrateRegistrationInfo

*Aplica-se à etapa [Capturar Configurações do Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

(entrada)

Especifica se a etapa migra as informações do usuário e da organização.

#### <a name="valid-values"></a>Valores válidos

- `true` (padrão). A variável [OSDRegisteredOrgName (saída)](#OSDRegisteredOrgName-output) será definida como o nome da organização registrada do computador.  
- `false`  

### <a name="OSDMigrateSkipEncryptedFiles"></a> OSDMigrateSkipEncryptedFiles

*Aplica-se à etapa [Capturar Estado do Usuário](task-sequence-steps.md#BKMK_CaptureUserState).*

(entrada)

Especifica se os arquivos criptografados serão capturados.

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false` (padrão)  

### <a name="OSDMigrateTimeZone"></a> OSDMigrateTimeZone

*Aplica-se à etapa [Capturar Configurações do Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

(entrada)

Especifica se o fuso horário do computador é migrado.

#### <a name="valid-values"></a>Valores válidos

- `true` (padrão). A variável [OSDTimeZone (saída)](#OSDTimeZone-output) será definida como o fuso horário do computador.  
- `false`  

### <a name="OSDNetworkJoinType"></a> OSDNetworkJoinType

*Aplica-se à etapa [Aplicar Configurações de Rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(entrada)

Especifica se o computador de destino ingressa em um domínio do Active Directory ou um grupo de trabalho.

#### <a name="value-values"></a>Valores do valor

- `0`: ingressar em um domínio do Active Directory  
- `1`: ingressar em um grupo de trabalho

### <a name="OSDPartitions"></a> OSDPartitions

*Aplica-se à etapa [Formatar e Particionar Disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(entrada)

Esta variável da sequência de tarefas é uma variável de matriz das configurações de partição. Cada elemento na matriz representa as configurações para uma única partição no disco rígido. Acesse as configurações definidas para cada partição combinando o nome de variável de matriz com o número de partição de disco baseado em zero e o nome da propriedade.

Use os seguintes nomes de variáveis para definir as propriedades para a *primeira* partição que esta etapa cria no disco rígido:

#### <a name="osdpartitions0type"></a>OSDPartitions0Type

Especifica o tipo de partição. Esta propriedade é necessária. Os valores válidos são `Primary`, `Extended`, `Logical` e `Hidden`.

#### <a name="osdpartitions0filesystem"></a>OSDPartitions0FileSystem

Especifica o tipo de sistema de arquivos a ser usado ao formatar a partição. Esta propriedade é opcional. Se você não especificar um sistema de arquivos, a etapa não formatará a partição. Os valores válidos são `FAT32` e `NTFS`.

#### <a name="osdpartitions0bootable"></a>OSDPartitions0Bootable

Especifica se a partição é inicializável. Esta propriedade é necessária. Se esse valor for definido como `TRUE` para discos MBR, essa etapa marcará esta partição como ativa.

#### <a name="osdpartitions0quickformat"></a>OSDPartitions0QuickFormat

Especifica o tipo de formato usado. Esta propriedade é necessária. Se esse valor for definido como `TRUE`, a etapa executará uma formatação rápida. Caso contrário, a etapa executa uma formatação completa.

#### <a name="osdpartitions0volumename"></a>OSDPartitions0VolumeName

Especifica o nome atribuído ao volume quando ele é formatado. Esta propriedade é opcional.

#### <a name="osdpartitions0size"></a>OSDPartitions0Size

Especifica o tamanho da partição. Esta propriedade é opcional. Se esta propriedade não for especificada, a partição será criada usando todo o espaço livre restante. As unidades são especificadas pela variável **OSDPartitions0SizeUnits** .

#### <a name="osdpartitions0sizeunits"></a>OSDPartitions0SizeUnits

A etapa usa essas unidades para interpretar a variável **OSDPartitions0Size**. Esta propriedade é opcional. Os valores válidos são `MB` (padrão), `GB` e `Percent`.

#### <a name="osdpartitions0volumelettervariable"></a>OSDPartitions0VolumeLetterVariable

Quando essa etapa cria partições, sempre usa a próxima letra de unidade disponível no Windows PE. Use essa propriedade opcional para especificar o nome de outra variável de sequência de tarefas. A etapa usa essa variável para salvar a nova letra da unidade para referência futura.

Se você definir várias partições com esta etapa da sequência de tarefas, as propriedades da *segunda* partição serão definidas usando o índice **1** no nome da variável. Por exemplo: **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat** e **OSDPartitions1VolumeName**.

### <a name="OSDPartitionStyle"></a> OSDPartitionStyle

*Aplica-se à etapa [Formatar e Particionar Disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(entrada)

Especifica o estilo de partição a ser usado ao particionar o disco.

#### <a name="valid-values"></a>Valores válidos

- `GPT`: use o estilo Tabela de partição GUID
- `MBR`: Use o estilo de partição do registro mestre de inicialização

### <a name="OSDProductKey"></a> OSDProductKey

*Aplica-se à etapa [Aplicar Configurações do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(entrada)

Especifica a chave do produto (Product Key) do Windows. O valor especificado deve estar entre 1 e 255 caracteres.

### <a name="OSDRandomAdminPassword"></a> OSDRandomAdminPassword

*Aplica-se à etapa [Aplicar Configurações do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(entrada)

Especifica uma senha gerada aleatoriamente para a conta de administrador local no novo sistema operacional.

#### <a name="valid-values"></a>Valores válidos

- `true` (padrão): a Instalação do Windows desabilita a conta de administrador local no computador de destino  

- `false`: a Instalação do Windows habilita a conta de administrador local no computador de destino e define a senha da conta para o valor de [OSDLocalAdminPassword](#OSDLocalAdminPassword)  

### <a name="OSDRegisteredOrgName-input"></a> OSDRegisteredOrgName (entrada)

*Aplica-se à etapa [Aplicar Configurações do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Especifica o nome da organização padrão registrada no novo sistema operacional. O valor especificado deve estar entre 1 e 255 caracteres.

### <a name="OSDRegisteredOrgName-output"></a> OSDRegisteredOrgName (saída)

*Aplica-se à etapa [Capturar Configurações do Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

Defina como o nome da organização registrada do computador. O valor será definido somente se a variável [OSDMigrateRegistrationInfo](#OSDMigrateRegistrationInfo) for definida como `true`.

### <a name="OSDRegisteredUserName"></a> OSDRegisteredUserName

*Aplica-se à etapa [Aplicar Configurações do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(entrada)

Especifica o nome de usuário padrão registrado no novo sistema operacional. O valor especificado deve estar entre 1 e 255 caracteres.

### <a name="OSDServerLicenseConnectionLimit"></a> OSDServerLicenseConnectionLimit

*Aplica-se à etapa [Aplicar Configurações do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(entrada)

Especifica o número máximo de conexões permitidas. O número especificado deve estar no intervalo entre 5 e 9.999 conexões.

### <a name="OSDServerLicenseMode"></a> OSDServerLicenseMode

*Aplica-se à etapa [Aplicar Configurações do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(entrada)

Especifica o modo de licença do Windows Server usado.

#### <a name="valid-values"></a>Valores válidos

- `PerSeat`
- `PerServer`

### <a name="OSDSetupAdditionalUpgradeOptions"></a> OSDSetupAdditionalUpgradeOptions

*Aplica-se à etapa [Atualizar Sistema Operacional](task-sequence-steps.md#BKMK_UpgradeOS).*

(entrada)

Especifica as demais opções da linha de comando que são adicionadas à Instalação do Windows durante um upgrade do Windows 10. A sequência de tarefas não verifica as opções de linha de comando.

Para obter mais informações, veja [Opções de Linha de Comando da Instalação do Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

### <a name="OSDStateFallbackToNAA"></a> OSDStateFallbackToNAA

*Aplica-se à etapa [Solicitar Armazenamento de Estado](task-sequence-steps.md#BKMK_RequestStateStore).*

(entrada)

Quando a conta do computador não consegue se conectar ao ponto de migração de estado, essa variável especifica se a sequência de tarefas voltará a usar a conta de acesso de rede (NAA).

Para saber mais sobre a conta de acesso à rede, consulte [Contas](/sccm/core/plan-design/hierarchy/accounts#network-access-account).

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false` (padrão)  

### <a name="OSDStateSMPRetryCount"></a> OSDStateSMPRetryCount

*Aplica-se à etapa [Solicitar Armazenamento de Estado](task-sequence-steps.md#BKMK_RequestStateStore).*

(entrada)

Especifica o número de vezes que a etapa da sequência de tarefas tentará localizar um ponto de migração de estado antes da etapa falhar. A contagem especificada deve estar entre 0 e 600.

### <a name="OSDStateSMPRetryTime"></a> OSDStateSMPRetryTime

*Aplica-se à etapa [Solicitar Armazenamento de Estado](task-sequence-steps.md#BKMK_RequestStateStore).*

(entrada)

Especifica o número de segundos durante os quais a etapa da sequência de tarefas aguarda entre as novas tentativas. O número de segundos pode ter, no máximo, 30 caracteres.

### <a name="OSDStateStorePath"></a> OSDStateStorePath

*Aplica-se às seguintes etapas:*  

- [Capturar Estado do Usuário](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Liberar Armazenamento de Estado](task-sequence-steps.md#BKMK_ReleaseStateStore)  
- [Solicitar Armazenamento de Estado](task-sequence-steps.md#BKMK_RequestStateStore)  
- [Restaurar Estado do Usuário](task-sequence-steps.md#BKMK_RestoreUserState)  

(entrada)

O compartilhamento de rede ou o nome de caminho local da pasta em que a sequência de tarefas salva ou restaura o estado do usuário. Sem valor padrão.

### <a name="OSDTargetSystemDrive"></a> OSDTargetSystemDrive

*Aplica-se à etapa [Aplicar Imagem do SO](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).*

(saída)

Especifica a letra da unidade da partição que contém os arquivos do sistema operacional após aplicar a imagem.

### <a name="OSDTargetSystemRoot-input"></a> OSDTargetSystemRoot (entrada)

*Aplica-se à etapa [Capturar Imagem do SO](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

Especifica o caminho no diretório do Windows para o SO instalado no computador de referência. A sequência de tarefas o verifica como um sistema operacional compatível para captura pelo Configuration Manager.

### <a name="OSDTargetSystemRoot-output"></a> OSDTargetSystemRoot (saída)

*Aplica-se à etapa [Preparar o Windows para Captura](task-sequence-steps.md#BKMK_PrepareWindowsforCapture).*

Especifica o caminho no diretório do Windows para o SO instalado no computador de referência. A sequência de tarefas o verifica como um sistema operacional compatível para captura pelo Configuration Manager.

### <a name="OSDTimeZone-input"></a> OSDTimeZone (entrada)

*Aplica-se à etapa [Aplicar Configurações do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Especifica a configuração de fuso horário padrão usada no novo sistema operacional.

### <a name="OSDTimeZone-output"></a> OSDTimeZone (saída)

*Aplica-se à etapa [Capturar Configurações do Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

Defina como o fuso horário do computador. O valor será definido somente se a variável [OSDMigrateTimeZone](#OSDMigrateTimeZone) for definida como `true`.

### <a name="OSDWipeDestinationPartition"></a> OSDWipeDestinationPartition

*Aplica-se à etapa [Aplicar Imagem de Dados](task-sequence-steps.md#BKMK_ApplyDataImage).*

(entrada)

Especifica se é necessário excluir os arquivos localizados na partição de destino.

#### <a name="valid-values"></a>Valores válidos

- `true` (padrão)
- `false`

### <a name="OSDWorkgroupName"></a> OSDWorkgroupName

*Aplica-se à etapa [Aplicar Configurações de Rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(entrada)

Especifica o nome do grupo de trabalho ingressado pelo computador de destino.

Especifique essa variável ou a variável [OSDDomainName](#OSDDomainName). O nome do grupo de trabalho pode ter, no máximo, 32 caracteres.

### <a name="SMSClientInstallProperties"></a> SMSClientInstallProperties

*Aplica-se à etapa [Configurar Windows e ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).*

(entrada)

Especifica as propriedades de instalação do cliente que a sequência de tarefas usa ao instalar o cliente do Configuration Manager.

Para obter mais informações, veja [Sobre os parâmetros e as propriedades de instalação de cliente](/sccm/core/clients/deploy/about-client-installation-properties).

### <a name="SMSConnectNetworkFolderAccount"></a> SMSConnectNetworkFolderAccount

*Aplica-se à etapa [Conectar à Pasta de Rede](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(entrada)

Especifica a conta de usuário usada para conectar o compartilhamento de rede em [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath). Especifique a senha da conta com o valor [SMSConnectNetworkFolderPassword](#SMSConnectNetworkFolderPassword).

Para saber mais sobre a conta de conexão da pasta de rede da sequência de tarefas, confira [Contas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-network-folder-connection-account).

### <a name="SMSConnectNetworkFolderDriveLetter"></a> SMSConnectNetworkFolderDriveLetter

*Aplica-se à etapa [Conectar à Pasta de Rede](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(entrada)

Especifica a letra da unidade da rede à qual se conectar. Esse valor é opcional. Se não for especificado, a conexão de rede não será mapeada para uma letra de unidade. Se especificado, este valor deve estar no intervalo de D a Z. Não use X, é a letra da unidade usada pelo Windows PE durante a fase Windows PE.

#### <a name="examples"></a>Exemplos

- `D:`  
- `E:`  

### <a name="SMSConnectNetworkFolderPassword"></a> SMSConnectNetworkFolderPassword

*Aplica-se à etapa [Conectar à Pasta de Rede](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(entrada)

Especifica a senha de [SMSConnectNetworkFolderAccount](#SMSConnectNetworkFolderAccount) usada para conectar o compartilhamento de rede em [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath).

### <a name="SMSConnectNetworkFolderPath"></a> SMSConnectNetworkFolderPath

*Aplica-se à etapa [Conectar à Pasta de Rede](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(entrada)

Especifica o caminho de rede para a conexão. Se precisar mapear esse caminho para uma letra de unidade, use o valor [SMSConnectNetworkFolderDriveLetter](#SMSConnectNetworkFolderDriveLetter).

#### <a name="example"></a>Exemplo

`\\server\share`

### <a name="SMSInstallUpdateTarget"></a> SMSInstallUpdateTarget

*Aplica-se à etapa [Instalar Atualizações de Software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).*

(entrada)

Especifica se é necessário instalar todas as atualizações ou apenas as atualizações obrigatórias.

#### <a name="valid-values"></a>Valores válidos

- `All`  
- `Mandatory`  

### <a name="SMSRebootMessage"></a> SMSRebootMessage

*Aplica-se à etapa [Reiniciar Computador](task-sequence-steps.md#BKMK_RestartComputer).*

(entrada)

Especifica a mensagem a ser exibida para os usuários antes de reiniciar o computador de destino. Se essa variável não for definida, o texto da mensagem padrão será exibido. A mensagem especificada não pode exceder 512 caracteres.

#### <a name="example"></a>Exemplo

`Save your work before the computer restarts.`  

### <a name="SMSRebootTimeout"></a> SMSRebootTimeout

*Aplica-se à etapa [Reiniciar Computador](task-sequence-steps.md#BKMK_RestartComputer).*

(entrada)

Especifica o número de segundos que o aviso é exibido para o usuário antes da reinicialização do computador.

#### <a name="examples"></a>Exemplos

- `0` (padrão): não exibir uma mensagem de reinicialização  
- `60`: exibe o aviso por um minuto  

### <a name="SMSTSAssignmentsDownloadInterval"></a> SMSTSAssignmentsDownloadInterval

O número de segundos para aguardar antes que o cliente tente baixar a política desde a última tentativa que não retornou nenhuma política. Por padrão, o cliente aguarda **0** segundos antes de tentar novamente.

Você pode definir essa variável usando um comando prestart da mídia ou PXE.

### <a name="SMSTSAssignmentsDownloadRetry"></a> SMSTSAssignmentsDownloadRetry

O número de vezes que um cliente tentará baixar a política depois que nenhuma política foi encontrada na primeira tentativa. Por padrão, o cliente tenta novamente **0** vezes.

Você pode definir essa variável usando um comando prestart da mídia ou PXE.

### <a name="SMSTSAssignUsersMode"></a> SMSTSAssignUsersMode

Especifica como uma sequência de tarefas associa os usuários ao computador de destino. Defina a variável para um dos seguintes valores:  

- **Auto**: quando a sequência de tarefas implanta o sistema operacional no computador de destino, ela cria uma relação entre os usuários especificados e o computador de destino.  

- **Pendente**: a sequência de tarefas cria uma relação entre os usuários especificados e o computador de destino. Um administrador precisa aprovar a relação para configurá-la.  

- **Desabilitado**: a sequência de tarefas não associa os usuários ao computador de destino ao implantar o sistema operacional.

### <a name="SMSTSDisableStatusRetry"></a> SMSTSDisableStatusRetry

<!--512358-->
Em cenários desconectados, o mecanismo de sequência de tarefas tenta repetidamente enviar mensagens de status ao ponto de gerenciamento. Esse comportamento neste cenário causa atrasos no processamento da sequência de tarefas.

A partir da versão 1802, defina essa variável como `true` e o mecanismo de sequência de tarefas não tentará enviar mensagens de status após a primeira falha de envio. Essa primeira tentativa inclui várias novas tentativas.

Quando a sequência de tarefas for reiniciada, o valor dessa variável persistirá. No entanto, a sequência de tarefas tenta enviar uma mensagem de status inicial. Essa primeira tentativa inclui várias novas tentativas. Se for bem-sucedida, a sequência de tarefas continuará a enviar o status, independentemente do valor dessa variável. Se o status falhar ao enviar, a sequência de tarefas usará o valor dessa variável.

> [!NOTE]  
> O [Relatório de status da sequência de tarefas](/sccm/core/servers/manage/list-of-reports#task-sequence---deployment-status) depende dessas mensagens de status para exibir o progresso, o histórico e os detalhes de cada etapa.

### <a name="SMSTSDisableWow64Redirection"></a> SMSTSDisableWow64Redirection

*Aplica-se à etapa [Executar Linha de Comando](task-sequence-steps.md#BKMK_RunCommandLine).*

(entrada)

Por padrão em um sistema operacional de 64 bits, a sequência de tarefas localiza e executa o programa na linha de comando usando o redirecionador de sistema de arquivos do WOW64. Esse comportamento permite ao comando localizar versões de 32 bits de programas e DLLs do sistema operacional. A definição dessa variável como `true` desabilita o uso do redirecionador de sistema de arquivos WOW64. O comando localiza versões nativas de 64 bits de programas e DLLs do sistema operacional. Essa variável não tem nenhum efeito em um sistema operacional de 32 bits.

### <a name="SMSTSDownloadAbortCode"></a> SMSTSDownloadAbortCode

Essa variável contém o valor do código "anular" para a ferramenta de download de programas externa. Esse programa é especificado na variável [SMSTSDownloadProgram](#SMSTSDownloadProgram). Se o programa retornar um código de erro igual ao valor da variável SMSTSDownloadAbortCode, o download do conteúdo falhará e nenhum outro método de download será tentado.

### <a name="SMSTSDownloadProgram"></a> SMSTSDownloadProgram

Use essa variável para especificar um provedor de conteúdo alternativo (ACP). Um ACP é um programa de download usado para baixar o conteúdo. A sequência de tarefas usa o ACP ao invés do programa de download padrão do Configuration Manager. Como parte do processo de download do conteúdo, a sequência de tarefas verifica essa variável. Se especificada, a sequência de tarefas executa o programa para baixar o conteúdo.

### <a name="SMSTSDownloadRetryCount"></a> SMSTSDownloadRetryCount

O número de vezes que o Configuration Manager tenta baixar o conteúdo de um ponto de distribuição. Por padrão, o cliente tenta novamente **2** vezes.

### <a name="SMSTSDownloadRetryDelay"></a> SMSTSDownloadRetryDelay

O número de segundos que o Configuration Manager aguarda antes de tentar baixar conteúdo novamente de um ponto de distribuição. Por padrão, o cliente aguarda **15** segundos antes de tentar novamente.

### <a name="SMSTSDriverRequestConnectTimeOut"></a> SMSTSDriverRequestConnectTimeOut

*Aplica-se à etapa [Aplicar Drivers Automaticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

Ao solicitar o catálogo de drivers, essa variável é o número de segundos que a sequência de tarefas aguarda pela conexão do servidor HTTP. Se a conexão demorar mais do que a configuração de tempo limite, a sequência de tarefas cancelará a solicitação. Por padrão, o tempo limite é definido como **60** segundos.

### <a name="SMSTSDriverRequestReceiveTimeOut"></a> SMSTSDriverRequestReceiveTimeOut

*Aplica-se à etapa [Aplicar Drivers Automaticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

Ao solicitar o catálogo de drivers, essa variável é o número de segundos que a sequência de tarefas aguarda uma resposta. Se a conexão demorar mais do que a configuração de tempo limite, a sequência de tarefas cancelará a solicitação. Por padrão, o tempo limite é definido como **480** segundos.

### <a name="SMSTSDriverRequestResolveTimeOut"></a> SMSTSDriverRequestResolveTimeOut

*Aplica-se à etapa [Aplicar Drivers Automaticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

Ao solicitar o catálogo de drivers, essa variável é o número de segundos que a sequência de tarefas aguarda uma resolução de nome HTTP. Se a conexão demorar mais do que a configuração de tempo limite, a sequência de tarefas cancelará a solicitação. Por padrão, o tempo limite é definido como **60** segundos.

### <a name="SMSTSDriverRequestSendTimeOut"></a> SMSTSDriverRequestSendTimeOut

*Aplica-se à etapa [Aplicar Drivers Automaticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

Ao enviar uma solicitação para o catálogo de drivers, essa variável é o número de segundos que a sequência de tarefas aguarda para enviar a resposta. Se a solicitação demorar mais do que a configuração de tempo limite, a sequência de tarefas cancelará a solicitação. Por padrão, o tempo limite é definido como **60** segundos.

### <a name="SMSTSErrorDialogTimeout"></a> SMSTSErrorDialogTimeout

Quando ocorre um erro em uma sequência de tarefas, ele exibe uma caixa de diálogo com o erro. A sequência de tarefas a descarta automaticamente após o número de segundos especificado por essa variável. Por padrão, este valor é **900** segundos (15 minutos).

### <a name="SMSTSLanguageFolder"></a> SMSTSLanguageFolder

Use essa variável para alterar o idioma de exibição de uma imagem de inicialização neutra de idioma.

### <a name="SMSTSLocalDataDrive"></a> SMSTSLocalDataDrive

Especifica onde a sequência de tarefas armazena os arquivos temporários no computador de destino enquanto está em execução.

Defina essa variável antes do início da sequência de tarefas configurando uma variável de coleta. Depois de iniciada a sequência de tarefas, o Configuration Manager define a variável [_SMSTSMDataPath](#SMSTSMDataPath).

### <a name="SMSTSMP"></a> SMSTSMP

Use esta variável para especificar a URL ou endereço IP de um ponto de gerenciamento do Configuration Manager.

### <a name="SMSTSMPListRequestTimeoutEnabled"></a> SMSTSMPListRequestTimeoutEnabled

*Aplica-se às seguintes etapas:*  

- [Instalar Aplicativo](task-sequence-steps.md#BKMK_InstallApplication)  
- [Instalar Atualizações de Software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(entrada)

Se o cliente não estiver na Intranet, use essa variável para permitir que solicitações repetidas de MPList atualizem o cliente. Por padrão, essa variável é definida como `True`.

Quando os clientes estão na Internet, defina essa variável como `False` para evitar atrasos desnecessários.

### <a name="SMSTSMPListRequestTimeout"></a> SMSTSMPListRequestTimeout

*Aplica-se às seguintes etapas:*  

- [Instalar Aplicativo](task-sequence-steps.md#BKMK_InstallApplication)  
- [Instalar Atualizações de Software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(entrada)

Se a sequência de tarefas falhar na recuperação da lista de ponto de gerenciamento (MPList) dos serviços de localização, essa variável especifica quantos milissegundos aguardará antes de tentar a etapa novamente. Por padrão, a sequência de tarefas espera `60000` milissegundos (60 segundos) antes de tentar novamente. E tenta novamente até três vezes.

### <a name="SMSTSPeerDownload"></a> SMSTSPeerDownload

Use essa variável para habilitar o cliente a usar o cache de sistemas pares do Windows PE. Definir essa variável como `true` habilita essa funcionalidade.

### <a name="SMSTSPeerRequestPort"></a> SMSTSPeerRequestPort

Uma porta de rede personalizada que usa o cache par do Windows PE para a difusão inicial. A porta padrão definida nas configurações do cliente é a **8004**.

### <a name="SMSTSPersistContent"></a> SMSTSPersistContent

Use essa variável para manter temporariamente o conteúdo no cache da sequência de tarefas. Essa variável é diferente da [SMSTSPreserveContent](#SMSTSPreserveContent), que mantém conteúdo no cache do cliente do Configuration Manager após a conclusão da sequência de tarefas. SMSTSPersistContent usa o cache de sequência de tarefas, SMSTSPreserveContent usa o cache de cliente do Configuration Manager.

### <a name="SMSTSPostAction"></a> SMSTSPostAction

Especifica um comando que é executado após a sequência de tarefas. Por exemplo, especifique um script que permite filtros de gravação em dispositivos inseridos depois que a sequência de tarefas implanta um sistema operacional no dispositivo.

### <a name="SMSTSPreferredAdvertID"></a> SMSTSPreferredAdvertID

Força a sequência de tarefas a executar uma implantação direcionada específica no computador de destino. Defina essa variável por meio de um comando prestart de mídia ou PXE. Se essa variável for definida, a sequência de tarefas substitui todas as implantações necessárias.

### <a name="SMSTSPreserveContent"></a> SMSTSPreserveContent

Essa variável sinaliza o conteúdo na sequência de tarefas a ser mantido no cache do cliente do Configuration Manager após a implantação. Essa variável é diferente de [SMSTSPersistContent](#SMSTSPersistContent), que mantém o conteúdo apenas durante a sequência de tarefas. SMSTSPersistContent usa o cache de sequência de tarefas, SMSTSPreserveContent usa o cache de cliente do Configuration Manager. Defina SMSTSPreserveContent como `true` para habilitar essa funcionalidade.

### <a name="SMSTSRebootDelay"></a> SMSTSRebootDelay

Especifica o número de segundos a esperar antes do computador ser reiniciado. Se esta variável for zero (0), o gerenciador de sequência de tarefas não exibirá uma caixa de diálogo de notificação antes da reinicialização.

#### <a name="example"></a>Exemplo

- `0`: não exibir uma notificação  

- `60`: exibir uma notificação por um minuto  

### <a name="SMSTSRebootMessage"></a> SMSTSRebootMessage

Especifica a mensagem a ser exibida na caixa de diálogo de notificação de reinicialização. Se essa variável não for definida, será exibida uma mensagem padrão.

#### <a name="example"></a>Exemplo

`The task sequence is restarting this computer`

### <a name="SMSTSRebootRequested"></a> SMSTSRebootRequested

Indica que uma reinicialização será solicitada após a etapa da sequência de tarefas atual ser concluída. Se for necessária uma reinicialização, defina essa variável como `true` e o Gerenciador de sequência de tarefas reiniciará o computador após essa etapa de sequência de tarefas. Se a etapa de sequência de tarefas exigir uma reinicialização para concluir a ação, defina essa variável. Depois que o computador é reiniciado, a sequência de tarefas continua sendo executada na próxima etapa da sequência de tarefas.

### <a name="SMSTSRetryRequested"></a> SMSTSRetryRequested

Solicita uma nova tentativa após a etapa atual ser concluída. Se essa variável de sequência de tarefas for definida, a variável [SMSTSRebootRequested](#SMSTSRebootRequested) também deve ser definida como `true`. Depois que o computador for reiniciado, o gerenciador da sequência de tarefas executará novamente a mesma etapa da sequência de tarefas.

### <a name="SMSTSRunCommandLineUserName"></a> SMSTSRunCommandLineUserName

*Aplica-se à etapa [Executar Linha de Comando](task-sequence-steps.md#BKMK_RunCommandLine).*

(entrada)

Especifica a conta pela qual a linha de comando é executada. O valor é uma cadeia de caracteres do formato nomeusuário ou domínio\nomeusuário. Especifique a senha da conta com a variável [SMSTSRunCommandLinePassword](#SMSTSRunCommandLinePassword).

Para saber mais sobre a conta de execução da sequência de tarefas, confira [Contas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-run-as-account).

### <a name="SMSTSRunCommandLinePassword"></a> SMSTSRunCommandLinePassword

*Aplica-se à etapa [Executar Linha de Comando](task-sequence-steps.md#BKMK_RunCommandLine).*

(entrada)

Define a senha para a conta especificada pela variável [SMSTSRunCommandLineUserName](#SMSTSRunCommandLineUserName).

### <a name="SMSTSSoftwareUpdateScanTimeout"></a> SMSTSSoftwareUpdateScanTimeout

*Aplica-se à etapa [Instalar Atualizações de Software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).*

(entrada)

Controle o tempo limite para a verificação de atualizações de software durante essa etapa. Por exemplo, aumente o valor se você espera ter várias atualizações durante a verificação. O valor padrão é `1800` segundos (30 minutos). O valor da variável é definido em segundos.

> [!NOTE]  
> Começando pela versão 1802, o valor padrão é `3600` segundos (60 minutos).  

### <a name="SMSTSUDAUsers"></a> SMSTSUDAUsers

Especifica os usuários primários do computador de destino usando o seguinte formato: `<DomainName>\<UserName>`. Separe vários usuários com vírgulas (`,`). Para mais informações, consulte [Associar usuários a um computador de destino](/sccm/osd/get-started/associate-users-with-a-destination-computer).

#### <a name="example"></a>Exemplo

`contoso\jqpublic, contoso\megb, contoso\janedoh`

### <a name="SMSTSWaitForSecondReboot"></a> SMSTSWaitForSecondReboot

*Aplica-se à etapa [Instalar Atualizações de Software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).*

(entrada)

Essa variável opcional da sequência de tarefas controla o comportamento do cliente quando uma instalação de atualização de software exige duas reinicializações. Defina essa variável antes desta etapa para evitar a falha da sequência de tarefas devido à segunda reinicialização depois da instalação de atualização de software.

Defina o valor de SMSTSWaitForSecondReboot para especificar por quantos segundos a sequência de tarefas fica em pausa depois que o computador é reiniciado. Permita que haja tempo suficiente em caso de uma segunda reinicialização.

Por exemplo, se você definir SMSTSWaitForSecondReboot como `600`, a sequência de tarefas pausa por 10 minutos após uma reinicialização antes da execução das etapas adicionais. Essa variável é útil quando uma única etapa de sequência de tarefas Instalar Atualizações de Software instala centenas de atualizações de software.

### <a name="TSDisableProgressUI"></a> TSDisableProgressUI

<!-- 1354291 -->
Use essa variável para controlar quando a sequência de tarefas exibe o progresso para os usuários finais. Para ocultar ou exibir o andamento em momentos diferentes, defina essa variável várias vezes em uma sequência de tarefas.  

- `true`: ocultar o progresso da sequência de tarefas  

- `false`: exibir o andamento da sequência de tarefas  

### <a name="TSErrorOnWarning"></a> TSErrorOnWarning

*Aplica-se à etapa [Instalar Aplicativo](task-sequence-steps.md#BKMK_InstallApplication).*

(entrada)

Especifique se o mecanismo de sequência de tarefas considera um aviso detectado como um erro durante essa etapa. A sequência de tarefas define a variável [_TSAppInstallStatus](#TSAppInstallStatus) como `Warning` quando um ou mais aplicativos, ou uma dependência necessária, não foram instalados porque não cumpriram um requisito. Ao definir essa variável como `True` e a sequência de tarefas definir **_TSAppInstallStatus** como `Warning`, o resultado é um erro. Um valor `False` é o comportamento padrão.

### <a name="WorkingDirectory"></a> WorkingDirectory

*Aplica-se à etapa [Executar Linha de Comando](task-sequence-steps.md#BKMK_RunCommandLine).*

(entrada)

Especifica o diretório inicial para uma ação de linha de comando. O nome do diretório especificado não pode exceder 255 caracteres.

#### <a name="examples"></a>Exemplos

- `C:\`  
- `%SystemRoot%`  


## <a name="deprecated-variables"></a>Variáveis preteridas

As seguintes variáveis foram preteridas:

- **OSDAllowUnsignedDriver**: não é usada ao implantar o Windows Vista e sistemas operacionais posteriores
- **OSDBuildStorageDriverList**: aplica-se somente ao Windows XP e ao Windows Server 2003
- **OSDDiskpartBiosCompatibilityMode**: só é necessária ao implantar o Windows XP ou o Windows Server 2003
- **OSDInstallEditionIndex**: não é necessária após o Windows Vista
- **OSDPreserveDriveLetter**: para saber mais, confira [OSDPreserveDriveLetter](#osdpreservedriveletter)

### <a name="osdpreservedriveletter"></a>OSDPreserveDriveLetter

> [!Important]
> Esta variável de sequência de tarefas foi preterida.
>
> Durante uma implantação de sistema operacional, por padrão, a Instalação do Windows determina a melhor letra de unidade a usar (geralmente C:).

*Comportamento anterior*: ao aplicar uma imagem, a variável OSDPreverveDriveLetter determina se a sequência de tarefas usa a letra da unidade capturada no arquivo da imagem (WIM). Defina o valor desta variável como `false` para usar o local especificado para a configuração **Destino** na etapa da sequência de tarefas **Aplicar Sistema Operacional**. Para saber mais, confira [Aplicar imagem do sistema operacional](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).


## <a name="see-also"></a>Consulte também

- [Etapas da sequência de tarefas](/sccm/osd/understand/task-sequence-steps)
- [Uso de variáveis de sequência de tarefas](/sccm/osd/understand/using-task-sequence-variables)
- [Considerações sobre o planejamento para automatizar tarefas](/sccm/osd/plan-design/planning-considerations-for-automating-tasks)
