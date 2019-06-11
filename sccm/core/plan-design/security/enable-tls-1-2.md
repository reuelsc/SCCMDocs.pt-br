---
title: Como habilitar o TLS 1.2
titleSuffix: Configuration Manager
description: Informações sobre como habilitar o TLS 1.2 para o Microsoft Configuration Manager.
ms.date: 05/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3641c3a9adce23f24a80135d996da03e12e78907
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66355603"
---
# <a name="how-to-enable-tls-12-for-configuration-manager"></a>Como habilitar o TLS 1.2 para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo descreve como habilitar o TLS 1.2 para o Configuration Manager, incluindo para os componentes individuais. Os requisitos de atualização de recursos comumente usados e a solução de alguns problemas comuns também são descritos neste artigo.

O Configuration Manager conta com vários componentes para ter uma comunicação segura. O protocolo usado para determinada conexão depende dos recursos de todos os componentes necessários. Se um componente estiver desatualizado, a comunicação poderá usar um protocolo mais antigo e menos seguro.

Para habilitar o Configuration Manager a fim de dar suporte a TLS 1.2 corretamente, você deve habilitar o TLS 1.2 para todos os componentes necessários. Os componentes necessários dependem do seu ambiente e dos recursos do Configuration Manager utilizados.


## <a name="to-enable-tls-12"></a>Para habilitar o TLS 1.2

Para habilitar o TLS 1.2, primeiro habilite o TLS 1.2 como um provedor de segurança para cada computador que está executando o Configuration Manager ou interagindo com ele. Em seguida, habilite o TLS 1.2 para os componentes dos quais o Configuration Manager depende para ter uma comunicação segura.

### <a name="enable-the-tls-12-protocol-as-a-security-provider"></a>Habilitar o protocolo TLS 1.2 como um provedor de segurança

Verifique a configuração de subchaves de registro de "\SecurityProviders\SCHANNEL\Protocols", conforme mostrado nas [melhores práticas de protocolo TLS com o .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry?).

> [!NOTE]
> O TLS 1.2 fica habilitado por padrão. Portanto, não é necessário fazer nenhuma alteração nessas chaves para habilitá-lo. Você pode fazer alterações nos protocolos para desabilitar o TLS 1.0 e o TLS 1.1 depois que tiver seguido o restante das diretrizes deste artigo e verificado que o ambiente funciona com a habilitação apenas do TLS 1.2.

### <a name="enable-tls-12-for-dependent-components"></a>Habilitar o TLS 1.2 para componentes dependentes
Para habilitar o TLS 1.2 para os componentes dependentes dos quais o Configuration Manager depende para ter uma comunicação segura, você precisa:

- [Atualizar o .NET Framework para dar suporte ao TLS 1.2](#update-net-framework-to-support-tls-12)
- [Atualizar o SQL Server e os componentes cliente](#update-sql-server-and-client-components)
- [Atualizar o Windows e WinHTTP no Windows 8.0, Windows Server 2012 R2 e versões anteriores](#update-windows-and-winhttp)
- [Atualizar WSUS (Windows Server Update Services)](#update-windows-server-update-services)

#### <a name="update-net-framework-to-support-tls-12"></a>Atualizar o .NET Framework para dar suporte ao TLS 1.2
Para atualizar o .NET Framework para dar suporte a TLS 1.2, primeiro determine o número de versão do .NET. Para obter ajuda, consulte [Como determinar quais versões e níveis de service pack do Microsoft .NET Framework estão instalados](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso).

Versões anteriores do .NET Framework podem exigir atualizações ou alterações de registro para permitir uma criptografia forte. Use estas diretrizes:

- O .NET Framework 4.6.2 é compatível com TLS 1.1 e TLS 1.2.  Não são necessárias alterações adicionais.
- O NET Framework 4.6 e versões anteriores [devem ser atualizadas](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies) para dar suporte a TLS 1.1 e TLS 1.2.

Se você estiver usando o .NET Framework 4.5.1 ou 4.5.2 no Windows 8.1, Windows RT 8.1 ou Windows Server 2012, detalhes e atualizações relevantes também estarão disponíveis no [Centro de Download](https://www.microsoft.com/download/details.aspx?id=42883).
-  O .NET Framework deve ser configurado para dar suporte a uma criptografia forte. Defina a configuração do registro `SchUseStrongCrypto` para `DWORD:00000001`. Isso desabilita a codificação de fluxo RC4 e requer uma reinicialização. Para saber mais sobre essa configuração, consulte o [Microsoft Security Advisory 296038](https://docs.microsoft.com/security-updates/SecurityAdvisories/2015/2960358).

Para aplicativos de 32 bits executados em sistemas de 32 bits ou aplicativos de 64 bits executados em sistemas de 64 bits, atualize o seguinte valor de subchave:

```
[HKEY_LOCAL_MACHINE\SOFTWARE\
   Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto" = (DWORD): 00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\
   Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto"=dword:00000001
```
Para aplicativos de 32 bits executados em sistemas de 64 bits, atualize o seguinte valor de subchave:

```
[HKEY_LOCAL_MACHINE\SOFTWARE\
   Wow6432Node\Microsoft\.NETFramework\\v2.0.50727]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto" = (DWORD): 00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\
   WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto"=dword:00000001
```
#### <a name="update-sql-server-and-client-components"></a>Atualizar o SQL Server e os componentes cliente

O Microsoft SQL Server 2016 é compatível com TLS 1.1 e TLS 1.2.
As versões anteriores e bibliotecas dependentes podem exigir atualizações. Para saber mais, confira [KB 3135244: Suporte ao TLS 1.2 para o Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

> [!NOTE]
> O KB 3135244 também descreve os requisitos para componentes cliente do SQL Server. Atualize cada componente usado em seu ambiente.

#### <a name="update-windows-and-winhttp"></a>Atualizar Windows e WinHTTP

O Windows 10, o Windows 8.1, o Windows Server 2016 e o Windows Server 2012 R2 são originalmente compatíveis com TLS 1.2 para comunicações cliente-servidor sobre WinHTTP pronto para uso.

O Windows 8.0, Windows Server 2012 e versões anteriores do Windows não têm o TLS 1.1 ou 1.2 habilitado por padrão para comunicações cliente-servidor por meio de HTTPS. Para essas versões anteriores do Windows, você deve instalar a [Atualização 3140245](https://support.microsoft.com/help/3140245) para habilitar o TLS 1.1 e TLS 1.2 como os protocolos de segurança padrão no WinHTTP no Windows e definir valores de registro a seguir.

> [!IMPORTANT]
> Isso deve ser executado primeiro em todos os clientes de nível inferior, **antes** da habilitação do TLS 1.2, ou você pode torná-los órfãos inadvertidamente.

Verifique se a configuração do registro do `DefaultSecureProtocols` é `0xAA0`, como segue:

```
HKEY_LOCAL_MACHINE\SOFTWARE\
   \Microsoft\Windows\CurrentVersion\
      Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\
   Wow6432Node\Microsoft\Windows\CurrentVersion\
      Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```
> [!NOTE]
> Essa alteração exige uma reinicialização.

#### <a name="update-windows-server-update-services"></a>Atualizar Windows Server Update Services

Para ter suporte a TLS 1.2 em comunicações cliente-servidor no WSUS no Windows Server 2012 e Windows Server 2012 R2, você deve aplicar a atualização a seguir no servidor do WSUS:
- Para o servidor WSUS que esteja executando o Windows Server 2012, aplique a [atualização 4022721](https://support.microsoft.com/help/4022721) ou uma atualização posterior.
- Para servidor do WSUS que esteja executando o Windows Server 2012 R2, aplique a [atualização 4022720](https://support.microsoft.com/help/4022720) ou uma atualização posterior.

## <a name="tasks-required-for-configuration-manager-features-and-scenarios"></a>Tarefas obrigatórias para cenários e recursos do Configuration Manager
Esta seção descreve as dependências para cenários e recursos específicos do Configuration Manager. Para determinar as próximas etapas, localize os itens que se aplicam ao seu ambiente e, em seguida, verifique as dependências usando as etapas fornecidas anteriormente em [Habilitar o TLS 1.2 para componentes dependentes](#enable-tls-12-for-dependent-components).

|Cenário ou recurso|Tarefas de atualização|
|--- |--- |
|Servidores de site (central, principal ou secundário)|[Atualizar o .NET Framework](#update-net-framework-to-support-tls-12) e verificar as configurações de criptografia forte.|
|Provedor de SMS|[Atualizar o SQL Server e seus componentes cliente](#update-sql-server-and-client-components) conforme apropriado para cada provedor de SMS.|
|Funções do sistema de site|[Atualizar o .NET Framework](#update-net-framework-to-support-tls-12) e verificar as configurações de criptografia forte. [Atualizar o SQL Server e seus componentes cliente](#update-sql-server-and-client-components).|
|Catálogo de aplicativos de ponto de conexão de serviço|[Atualizar o .NET Framework](#update-net-framework-to-support-tls-12) e verificar as configurações de criptografia forte.|
|Ponto de relatório SRS|[Atualizar o .NET Framework](#update-net-framework-to-support-tls-12) no servidor do site e nos servidores SRS. Reinicie o serviço SMS_Executive conforme necessário.|
|Console do Configuration Manager|[Atualizar o .NET Framework](#update-net-framework-to-support-tls-12) e verificar as configurações de criptografia forte.|
|Cliente do SCCM com funções do sistema de sites HTTPS|[Atualizar o Windows para ser compatível com TLS 1.2 em comunicações cliente-servidor por meio de WinHTTP](#update-windows-and-winhttp).|
|Centro de software|[Atualizar o .NET Framework](#update-net-framework-to-support-tls-12) e verificar as configurações de criptografia forte.|
|Ponto de atualização de software|[Atualizar o WSUS](#update-windows-server-update-services).|
|Pontos de gerenciamento|Atualizar para o cliente nativo do SQL Server mais recente a fim de habilitar o Configuration Manager para se comunicar com os componentes mais recentes do SQL Server habilitado para TLS 1.2. Consulte a tabela "Downloads de componentes cliente" em [Suporte ao TLS 1.2 para o Microsoft SQL Server](https://support.microsoft.com/help/3135244).|

## <a name="known-issues"></a>Problemas conhecidos

Esta seção fornece conselhos para problemas comuns que ocorrem ao habilitar o suporte a TLS 1.2.

### <a name="fips-security-policy-enabled"></a>Política de segurança FIPS habilitada

Se a configuração de política de segurança FIPS estiver habilitada para o cliente ou para um servidor, a negociação de Canal seguro (Schannel) poderá fazer com que o TLS 1.0 seja utilizado mesmo se o protocolo estiver desabilitado usando o registro.

Para investigar, habilite o log de eventos do Canal seguro e, em seguida, examine os eventos do Schannel no log do sistema. Para saber informações relacionadas, confira [Como restringir o uso de certos algoritmos de criptografia e protocolos no Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

### <a name="sql-server-communication-failure"></a>Falha de comunicação do SQL Server

Se a comunicação do SQL Server falhar e retornar um erro **SslSecurityError**, verifique se:
- O .NET Framework está atualizado e tem criptografia forte habilitada em cada computador.
- O SQL Server está atualizado no servidor host.
- Os componentes cliente do SQL estão atualizados nos servidores de site, no provedor de SMS, nos servidores de função de site e em todos os outros sistemas que se comunicam com o SQL server.

### <a name="configuration-manager-client-communication-failures"></a>Falhas de comunicação do cliente do Configuration Manager

Se o cliente do Configuration Manager não se comunicar com os pontos de extremidade de função de site, como pontos de distribuição, pontos de gerenciamento e pontos de migração de estado, verifique se o Windows foi atualizado para dar suporte ao TLS 1.2 em comunicação cliente-servidor por meio do WinHTTP.

### <a name="srs-reporting-point-fails-and-returns-an-expected-error"></a>O Ponto de Relatório SRS falha e retorna um erro esperado

Se o ponto de relatório SRS não configurar relatórios, verifique em *SRSRP.log* se há a seguinte entrada de erro:

`The underlying connection was closed:`
`An expected error occurred on a receive.`

Para resolver esse problema, siga estas etapas:

1. Verifique se o .NET Framework está atualizado e tem criptografia forte habilitada em todos os computadores relevantes.
1. Verifique se o serviço SMS_Executive foi reiniciado depois da instalação de todas as atualizações.

### <a name="application-catalog-doesnt-initialize"></a>O catálogo de aplicativos não é inicializado

Se o catálogo de aplicativos não for inicializado, verifique no arquivo *ServicePortalWebSite.svclog* se há a seguinte entrada de erro:

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

Para resolver esse problema, siga estas etapas:
1. Verifique se o .NET Framework está atualizado e tem criptografia forte habilitada em todos os computadores relevantes.
1. Na pasta C:\Windows\System32\InetSrv do servidor de catálogo de aplicativos, crie um arquivo *W2SP.exe.config* executando o seguinte script: 

   ```xml
   <?xml version="1.0" encoding="utf-8" ?>
   <configuration>
     <runtime>
     <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
     </runtime>
   </configuration>
   ```
   > [!NOTE]
   > Isso é o arquivo padrão que seria criado se o aplicativo fosse compilado usando o .NET Framework 4.6.3.
1. Use segurança do transporte HTTPS para funções de Catálogo de Aplicativos.

   > [!NOTE]
   > Quando você usa a segurança de mensagem HTTP para funções de Catálogo de Aplicativos, o WCF é codificado para usar somente SSL 3.0 e TLS 1.0. Isso impede o uso do TLS 1.2.
1. Se alguma alteração for feita, reinicie o computador.


### <a name="software-center-or-browser-doesnt-communicate-with-application-catalog"></a>O Centro de Software ou o navegador não se comunica com o Catálogo de Aplicativos

Para resolver falhas de comunicação entre o Catálogo de Aplicativos e o Centro de Software ou o navegador, verifique as seguintes condições:

- O .NET Framework está atualizado e tem criptografia forte habilitada em cada computador.
- O navegador está configurado para suporte ao TLS 1. Antes do Windows 10, essa opção ficava desabilitada por padrão.
- Todos os computadores foram reiniciados depois que as alterações foram feitas.

   > [!NOTE]
   > Para fazer com que o Centro de Software funcione com o servidor imposto pelo TLS 1.2 para aplicativos disponíveis ao usuário, recomendamos que você remova as funções de catálogo de aplicativos e permita que o Centro de Software se comunique com o ponto de gerenciamento. Para saber mais, confira [Remover o catálogo de aplicativos](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat).

### <a name="service-connection-point-upload-failures"></a>Falhas de upload do ponto de conexão de serviço

Se o ponto de conexão de serviço não carregar dados para o SCCMConnectedService, verifique se o .NET Framework está atualizado e tem criptografia forte habilitada em cada computador. Lembre-se de reiniciar os computadores depois que as alterações forem feitas.

### <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>O console do Configuration Manager exibe a caixa de diálogo de integração do Intune

Se a caixa de diálogo de integração do Intune for exibida quando o console tentar se conectar ao portal do Intune, verifique se o .NET Framework está atualizado e tem criptografia forte habilitada em cada computador.  Lembre-se de reiniciar os computadores depois que as alterações forem feitas.

### <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>O console do Configuration Manager exibe falha ao entrar no Azure

Se a caixa de diálogo de integração dos serviços do Azure falhar imediatamente depois que você selecionar **Entrar** ao tentar criar aplicativos do Azure AD, verifique se o .NET Framework está atualizado e se a criptografia forte está habilitada. Uma reinicialização é necessária para que essas alterações entrem em vigor.

## <a name="see-also"></a>Consulte também

[Referência técnica de controles de criptografia](cryptographic-controls-technical-reference.md)
