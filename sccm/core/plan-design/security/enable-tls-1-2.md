---
title: Como habilitar o TLS 1.2
titleSuffix: Configuration Manager
description: Informações sobre como habilitar o TLS 1.2 para o Configuration Manager.
ms.date: 06/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3d97ee2e68f9f4606ad46c8566467fad459ffa9
ms.sourcegitcommit: 725e1bf7d3250c2b7b7be9da01135517428be7a1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822080"
---
# <a name="how-to-enable-tls-12"></a>Como habilitar o TLS 1.2

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo descreve como habilitar o TLS 1.2 para o Configuration Manager, incluindo para os componentes individuais. Os requisitos de atualização de recursos comumente usados e a solução de alguns problemas comuns também são descritos neste artigo.

O Configuration Manager conta com vários componentes para ter uma comunicação segura. O protocolo usado para determinada conexão depende dos recursos de todos os componentes necessários. Se um componente estiver desatualizado, a comunicação poderá usar um protocolo mais antigo e menos seguro.

Para habilitar o Configuration Manager corretamente para dar suporte ao TLS 1.2, você deve primeiro habilitar o TLS 1.2 para todos os componentes necessários. Os componentes necessários dependem do seu ambiente e dos recursos do Configuration Manager usados.

Inicie esse processo com os clientes, especialmente os que têm versões anteriores do Windows. Antes de habilitar o TLS 1.2 em servidores do Configuration Manager, verifique se todos os clientes oferecem suporte ao TLS 1.2. Caso contrário, os clientes não conseguirão se comunicar com os servidores e poderão ficar órfãos.


## <a name="tasks-for-features-and-scenarios"></a>Tarefas para cenários e recursos

Para habilitar o TLS 1.2 para os componentes dos quais o Configuration Manager depende para ter uma comunicação segura, você deve:

- [Habilitar o protocolo TLS 1.2 como um provedor de segurança](#enable-tls-12-protocol-as-a-security-provider)
- [Atualizar o .NET Framework para dar suporte ao TLS 1.2](#update-net-framework-to-support-tls-12)
- [Atualizar o SQL Server e os componentes cliente](#update-sql-server-and-client-components)
- [Atualizar o Windows e WinHTTP no Windows 8.0, Windows Server 2012 R2 e versões anteriores](#update-windows-and-winhttp)
- [Atualizar WSUS (Windows Server Update Services)](#update-windows-server-update-services-wsus)

Esta seção descreve as dependências para cenários e recursos específicos do Configuration Manager. Para determinar as próximas etapas, localize os itens que se aplicam ao seu ambiente.

|Cenário ou recurso|Tarefas de atualização|
|--- |--- |
|Servidores de site (central, principal ou secundário)| - [Atualizar o .NET Framework](#update-net-framework-to-support-tls-12)<br/> – Verificar as configurações de criptografia forte|
|Servidor de banco de dados do site|[Atualizar o SQL Server e seus componentes cliente](#update-sql-server-and-client-components)|
|Servidores do site secundário|[Atualizar o SQL Server e seus componentes cliente](#update-sql-server-and-client-components) para uma versão compatível do SQL Express|
|Funções do sistema de site| - [Atualizar o .NET Framework](#update-net-framework-to-support-tls-12) e verificar as configurações de criptografia forte <br/> - [Atualizar o SQL Server e seus componentes cliente](#update-sql-server-and-client-components) em funções que precisam dele, incluindo o [SQL Server Native Client](#sql-server-native-client)|
|Ponto do Reporting Services|- [Atualize o .NET Framework](#update-net-framework-to-support-tls-12) no servidor do site, nos servidores do SQL Reporting Services e em todos os computadores que tenham o console<br/> – Reiniciar o serviço SMS_Executive conforme necessário|
|Ponto de atualização de software|[Atualizar o WSUS](#update-windows-server-update-services-wsus)|
|Console do Configuration Manager| - [Atualizar o .NET Framework](#update-net-framework-to-support-tls-12)<br/> – Verificar as configurações de criptografia forte|
|Cliente do Configuration Manager com funções do sistema de sites HTTPS|[Atualizar o Windows para ser compatível com TLS 1.2 em comunicações cliente-servidor por meio de WinHTTP](#update-windows-and-winhttp)|
|Centro de software| - [Atualizar o .NET Framework](#update-net-framework-to-support-tls-12)<br/> – Verificar as configurações de criptografia forte|
|Clientes do Windows 7| *Antes* de habilitar o TLS 1.2 em quaisquer componentes de servidor, [atualize o Windows para oferecer suporte ao TLS 1.2 para comunicações cliente-servidor usando o WinHTTP](#update-windows-and-winhttp). Se você habilitar o TLS 1.2 em componentes de servidor pela primeira vez, poderá fazer com que versões anteriores de clientes fiquem órfãs.|


## <a name="enable-tls-12-protocol-as-a-security-provider"></a>Habilitar o protocolo TLS 1.2 como um provedor de segurança

Verifique a configuração de subchaves do registro de `\SecurityProviders\SCHANNEL\Protocols`, conforme mostrado nas [melhores práticas de protocolo TLS com o .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).

> [!NOTE]
> O TLS 1.2 fica habilitado por padrão. Portanto, não é necessário fazer nenhuma alteração nessas chaves para habilitá-lo. Você pode fazer alterações nos protocolos para desabilitar o TLS 1.0 e o TLS 1.1 depois que tiver seguido o restante das diretrizes deste artigo e verificado que o ambiente funciona com a habilitação apenas do TLS 1.2.


## <a name="update-net-framework-to-support-tls-12"></a>Atualizar o .NET Framework para dar suporte ao TLS 1.2

### <a name="determine-net-version"></a>Determinar a versão do .NET

Primeiro, determine o número de versão do .NET. Para saber mais, confira [Como determinar quais versões e níveis de service pack do Microsoft .NET Framework estão instalados](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso).

### <a name="install-net-updates"></a>Instalar atualizações do .NET

Algumas versões do .NET Framework podem exigir atualizações para permitir uma criptografia forte. Use estas diretrizes:

- O .NET Framework 4.6.2 e versões posteriores são compatíveis com TLS 1.1 e TLS 1.2. Confirme as configurações do registro, mas nenhuma outra alteração será necessária.

- Atualizar o .NET Framework 4.6 e versões anteriores para dar suporte a TLS 1.1 e TLS 1.2. Para saber mais, confira [Versões e dependências do .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).

- Se você estiver usando o .NET Framework 4.5.1 ou 4.5.2 no Windows 8.1 ou Windows Server 2012, os detalhes e atualizações relevantes também estarão disponíveis no [Centro de Download](https://www.microsoft.com/download/details.aspx?id=42883).

### <a name="configure-for-strong-cryptography"></a>Verificar a criptografia forte

Configure o .NET Framework para dar suporte a uma criptografia forte. Defina a configuração do registro `SchUseStrongCrypto` para `DWORD:00000001`. Esse valor desabilita a codificação de fluxo RC4 e requer uma reinicialização. Para saber mais sobre essa configuração, confira o [Comunicado de Segurança da Microsoft 296038](https://docs.microsoft.com/security-updates/SecurityAdvisories/2015/2960358).

Defina as chaves de registro a seguir em todos os computadores que se comunicam pela rede que têm um sistema habilitado para TLS 1.2. Por exemplo, os clientes do Configuration Manager ou qualquer função do sistema de sites remotos que não esteja instalada no servidor do site.

Para aplicativos de 32 bits executados em sistemas de 32 bits ou aplicativos de 64 bits executados em sistemas de 64 bits, atualize o seguinte valor de subchave:

```Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

Para aplicativos de 32 bits executados em sistemas de 64 bits, atualize o seguinte valor de subchave:

```Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

> [!Note]  
> A configuração `SchUseStrongCrypto` permite que o .NET use o TLS 1.1 e TLS 1.2. A configuração `SystemDefaultTlsVersions` permite que o .NET use a configuração do sistema operacional. Para saber mais, confira [Práticas recomendadas do TLS com o .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls).


## <a name="update-sql-server-and-client-components"></a>Atualizar o SQL Server e os componentes cliente

O Microsoft SQL Server 2016 e versões posteriores são compatíveis com TLS 1.1 e TLS 1.2. As versões anteriores e bibliotecas dependentes podem exigir atualizações. Para saber mais, confira [KB 3135244: Suporte ao TLS 1.2 para o Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

Os servidores do site secundário precisam usar pelo menos o SQL Server 2016 Express com Service Pack 2 (13.2.50.26) ou posterior.

### <a name="sql-server-native-client"></a>SQL Server Native Client

> [!NOTE]
> O [KB 3135244](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) também descreve os requisitos para componentes cliente do SQL Server.

Certifique-se de também atualizar o SQL Server Native Client para, pelo menos, a versão SQL 2012 SP4 (11.*.7001.0). A partir da versão 1810, esse requisito é uma [verificação de pré-requisitos (aviso)](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#sql-server-native-client).

O Configuration Manager usa o SQL Server Native Client nas seguintes funções de sistema de sites:

- Servidor de banco de dados do site
- Servidor do site: site de administração central, site primário ou site secundário
- Ponto de gerenciamento
- Ponto de gerenciamento de dispositivo
- Ponto de migração de estado
- Provedor de SMS
- Ponto de atualização de software
- Ponto de distribuição habilitado para multicast
- Ponto de serviço de atualização do Asset Intelligence
- Ponto do Reporting Services
- Serviço Web do catálogo de aplicativos
- Ponto de registro
- Ponto do Endpoint Protection
- Ponto de Conexão de Serviço
- Ponto de registro de certificado
- Ponto de serviço de data warehouse


## <a name="update-windows-and-winhttp"></a>Atualizar Windows e WinHTTP

O Windows 8.1, Windows Server 2012 R2, Windows 10, Windows Server 2016 e versões posteriores do Windows oferecem suporte nativo ao TLS 1.2 para comunicações cliente-servidor através do WinHTTP.

As versões anteriores do Windows, como o Windows 7 ou o Windows Server 2012, não habilitam o TLS 1.1 ou 1.2 por padrão para comunicações cliente-servidor por meio de HTTPS. Para essas versões anteriores do Windows, instale a [Atualização 3140245](https://support.microsoft.com/help/3140245) para habilitar o TLS 1.1 e TLS 1.2 como os protocolos de segurança padrão no WinHTTP no Windows. Em seguida, configure os valor de registro a seguir:

> [!IMPORTANT]
> Habilite essas configurações em todos os clientes *antes* de habilitar o TLS 1.2 em servidores do Configuration Manager. Caso contrário, você pode, sem querer, deixá-los órfãos.

Verifique se o valor da configuração do registro `DefaultSecureProtocols`, por exemplo:

```Registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```

Se você alterar esse valor, reinicie o computador.

> [!Note]  
> O exemplo acima mostra o valor de `0xAA0` para a configuração `DefaultSecureProtocols` do WinHTTP. [KB 3140245: A atualização para habilitar o TLS 1.1 e o TLS 1.2 como protocolos seguros padrão no WinHTTP no Windows](https://support.microsoft.com/help/3140245) lista o valor hexadecimal de cada protocolo. Por padrão, no Windows, esse valor é `0x0A0` para habilitar o SSL 3.0 e TLS 1.0 para WinHTTP. O exemplo acima mantém esses padrões e também habilita o TLS 1.1 e TLS 1.2 para WinHTTP. Essa configuração garante que a alteração não interromperá outros aplicativos que ainda possam depender do SSL 3.0 ou TLS 1.0. Você pode usar o valor de `0xA00` para habilitar somente o TLS 1.1 e o TLS 1.2. O Configuration Manager oferece suporte ao protocolo mais seguro que o Windows negocia entre os dois dispositivos.
>
> Se você quiser desabilitar completamente o SSL 3.0 e o TLS 1.0, use a configuração de protocolo SChannel desabilitada no Windows. Para saber mais, confira [Como restringir o uso de certos algoritmos de criptografia e protocolos no Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).


## <a name="update-windows-server-update-services-wsus"></a>Atualizar o WSUS (Windows Server Update Services)

Para dar suporte ao TLS 1.2 em comunicações cliente-servidor no WSUS no Windows Server 2012 e Windows Server 2012 R2, instale a atualização a seguir no servidor do WSUS:

- Para o servidor WSUS que esteja executando o Windows Server 2012, instale a [atualização 4022721](https://support.microsoft.com/help/4022721) ou uma atualização posterior.
- Para o servidor WSUS que esteja executando o Windows Server 2012 R2, instale a [atualização 4022720](https://support.microsoft.com/help/4022720) ou uma atualização posterior.


## <a name="known-issues"></a>Problemas conhecidos

Esta seção fornece conselhos para problemas comuns que ocorrem ao habilitar o suporte a TLS 1.2.

### <a name="unsupported-platforms"></a>Plataformas sem suporte

As plataformas de cliente a seguir têm suporte do Configuration Manager, mas não têm suporte em um ambiente TLS 1.2:

- Windows Server 2008
- Windows CE
- Apple OS X
- Dispositivos Windows 10 gerenciados com o MDM local

### <a name="reports-dont-show-in-the-console"></a>Os relatórios não são exibidos no console

Se os relatórios não forem exibidos no console do Configuration Manager, atualize o computador no qual você está executando o console. É preciso [atualizar o .NET Framework](#update-net-framework-to-support-tls-12) e habilitar a criptografia forte.

### <a name="fips-security-policy-enabled"></a>Política de segurança FIPS habilitada

Se você habilitar a configuração da política de segurança FIPS para o cliente ou para um servidor, a negociação de Canal seguro (Schannel) poderá fazer com que o TLS 1.0 seja utilizado. Esse comportamento ocorrerá mesmo se você desabilitar o protocolo no registro.

Para investigar, habilite o log de eventos do Canal seguro e, em seguida, examine os eventos do Schannel no log do sistema. Para saber mais, confira [Como restringir o uso de certos algoritmos de criptografia e protocolos no Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

### <a name="sql-server-communication-failure"></a>Falha de comunicação do SQL Server

Se a comunicação do SQL Server falhar e retornar um erro **SslSecurityError**, verifique as seguintes configurações:

- [Atualize o .NET Framework](#update-net-framework-to-support-tls-12) e habilite a criptografia forte em cada computador
- [Atualize o SQL Server](#update-sql-server-and-client-components) no servidor host
- [Atualize os componentes do cliente SQL](#update-sql-server-and-client-components) em todos os sistemas que se comunicam com o SQL. Por exemplo, os servidores do site, o provedor SMS e servidores de função do site.

### <a name="configuration-manager-client-communication-failures"></a>Falhas de comunicação do cliente do Configuration Manager

Se o cliente do Configuration Manager não se comunicar com as funções de site, verifique se o [Windows foi atualizado](#update-windows-and-winhttp) para dar suporte ao TLS 1.2 em comunicações cliente-servidor usando o WinHTTP. As funções comuns do site incluem pontos de distribuição, pontos de gerenciamento e pontos de migração de estado.

### <a name="reporting-services-point-fails-and-returns-an-expected-error"></a>O ponto do Reporting Services falha e retorna um erro esperado

Se o ponto do Reporting Services não configurar relatórios, verifique em **SRSRP.log** se há a seguinte entrada de erro:

`The underlying connection was closed:`
`An expected error occurred on a receive.`

Para resolver esse problema, siga estas etapas:

1. [Atualize o .NET Framework](#update-net-framework-to-support-tls-12) e habilite a criptografia forte em todos os computadores relevantes.

1. Depois de instalar todas as atualizações, reinicie o serviço SMS_Executive.

### <a name="application-catalog-doesnt-initialize"></a>O catálogo de aplicativos não é inicializado

> [!Important]  
> O catálogo de aplicativos foi preterido. Para saber mais, consulte [Recursos removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).

Se o catálogo de aplicativos não for inicializado, verifique no arquivo **ServicePortalWebSite.svclog** se há a seguinte entrada de erro:

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

Para resolver esse problema, siga estas etapas:

1. [Atualize o .NET Framework](#update-net-framework-to-support-tls-12) e habilite a criptografia forte em todos os computadores relevantes.

1. Na pasta `%WinDir%\System32\InetSrv` do servidor de catálogo de aplicativos, crie um arquivo **W2SP.exe.config** com o seguinte conteúdo:

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <runtime>
      <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
      </runtime>
    </configuration>
    ```

    > [!NOTE]
    > Esse arquivo é o arquivo padrão criado se o aplicativo fosse compilado usando o .NET Framework 4.6.3.

1. Use a segurança do transporte HTTPS para funções de Catálogo de Aplicativos.

    > [!Important]
    > Quando você usa a segurança de mensagem HTTP para funções de Catálogo de Aplicativos, o WCF é codificado para usar somente SSL 3.0 e TLS 1.0. Isso impede o uso do TLS 1.2.

1. Se alguma alteração tiver sido feita, reinicie o computador.

### <a name="software-center-or-browser-doesnt-communicate-with-the-application-catalog"></a>O Centro de Software ou o navegador não se comunica com o catálogo de aplicativos

> [!Important]  
> O catálogo de aplicativos foi preterido. Para saber mais, consulte [Recursos removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).

Remover a função do catálogo de aplicativos é o melhor método para fazer com que o Centro de Software funcione com aplicativos disponíveis para o usuário em um site habilitado para TLS 1.2. Em seguida, deixe o Centro de Software se comunicar diretamente com um ponto de gerenciamento. Para saber mais, confira [Remover o catálogo de aplicativos](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat).

Se precisar resolver falhas de comunicação entre o catálogo de aplicativos e o Centro de Software ou o navegador, verifique as seguintes condições:

- [Atualize o .NET Framework](#update-net-framework-to-support-tls-12) e habilite a criptografia forte em cada computador.

- Depois de fazer as alterações, reinicie todos os computadores afetados.

<!-- - Configure the browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default. removing, Silverlight experience is out of support-->

### <a name="service-connection-point-upload-failures"></a>Falhas de carregamento do ponto de conexão de serviço

Se o ponto de conexão de serviço não carregar dados para o SCCMConnectedService, [atualize o .NET Framework](#update-net-framework-to-support-tls-12) e habilite a criptografia forte em cada computador. Reinicie os computadores depois que as alterações forem feitas.

### <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>O console do Configuration Manager exibe a caixa de diálogo de integração do Intune

Se a caixa de diálogo de integração do Intune for exibida quando o console tentar se conectar ao portal do Intune, [atualize o .NET Framework](#update-net-framework-to-support-tls-12) e habilite a criptografia forte em cada computador. Reinicie os computadores depois que as alterações forem feitas.

### <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>O console do Configuration Manager exibe falha ao entrar no Azure

Quando você tenta criar aplicativos no Azure Active Directory (Azure AD), se a caixa de diálogo de integração dos Serviços do Azure falhar imediatamente após você escolher **Fazer login**, [atualize o .NET Framework](#update-net-framework-to-support-tls-12) e ative a criptografia forte. Reinicie os computadores depois que as alterações forem feitas.

### <a name="configuration-manager-cloud-services-and-tls-12"></a>Serviços de nuvem do Configuration Manager e o TLS 1.2

A partir da versão 1802, as máquinas virtuais do Azure usadas pelo gateway de gerenciamento de nuvem e pontos de distribuição de nuvem oferecem suporte ao TLS 1.2. Os clientes compatíveis com a versão 1802 ou posterior usam automaticamente o TLS 1.2.

O **SMSAdminui.log** pode conter um erro semelhante ao exemplo a seguir:

```
Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationException
Service returned error. Check InnerException for more details
at Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationContext.GetAADAuthResultObject
...
Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException
Service returned error. Check InnerException for more details
at Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext.RunAsyncTask
...
System.Net.WebException
The underlying connection was closed: An unexpected error occurred on a receive.
at System.Net.HttpWebRequest.GetResponse
```

No Log de Eventos do Sistema, a EventID 36874 do SChannel pode ser registrada com a seguinte descrição: `An TLS 1.2 connection request was received from a remote client application, but none of the cipher suites supported by the client application are supported by the server. The TLS connection request has failed.`
<!--SCCMDocs issue #1608-->


## <a name="see-also"></a>Consulte também

- [Práticas recomendadas do protocolo TLS com o .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)

- [KB 3135244: Suporte do TLS 1.2 para Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)

- [Referência técnica de controles de criptografia](cryptographic-controls-technical-reference.md)
