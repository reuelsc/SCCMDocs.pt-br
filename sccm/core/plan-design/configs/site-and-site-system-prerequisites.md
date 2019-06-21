---
title: Pré-requisitos do site
titleSuffix: Configuration Manager
description: Saiba como configurar um computador Windows como um servidor do sistema de sites do Configuration Manager.
ms.date: 03/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: daee7a247fd12637736caa9c341798950a66c786
ms.sourcegitcommit: 86968fc2f129e404ff8e08f91a05fa17b5c47527
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2019
ms.locfileid: "67251845"
---
# <a name="site-and-site-system-prerequisites-for-configuration-manager"></a>Pré-requisitos do site e do sistema de sites para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os computadores baseados no Windows exigem configurações específicas para que possam ser usados como servidores do sistema de sites do Configuration Manager. 

Este artigo concentra-se principalmente no [Windows Server 2012 e posteriores](#bkmk_2012Prereq). O [Windows Server 2008 R2 e o Windows Server 2008](#bkmk_2008) são compatíveis com a função do sistema de sites de ponto de distribuição. Para obter mais informações, confira [Sistemas operacionais com suporte para servidores do sistema de sites](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers). 

Para alguns produtos, como o WSUS (Windows Server Update Services) para o ponto de atualização de software, você precisa consultar essa documentação de produtos para identificar os pré-requisitos adicionais e as limitações de uso. Somente as configurações que se aplicam diretamente ao uso com o Configuration Manager estão incluídas aqui.   

> [!NOTE]  
>  Em janeiro de 2016, o suporte expirou para o .NET Framework 4.0, 4.5 e 4.5.1. Para obter mais informações, consulte [Perguntas frequentes sobre a política do ciclo de vida de suporte do .NET Framework](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update).  



## <a name="bkmk_generalprerewq"></a> Requisitos e limitações gerais

Os seguintes requisitos aplicam-se a todos os servidores do sistema de sites:

- Cada servidor do sistema de sites precisa usar um sistema operacional de 64 bits. A única exceção é a função do sistema de sites do ponto de distribuição, que pode ser instalada em alguns sistemas operacionais de 32 bits.  

- Não há suporte para os sistemas de sites em instalações Server Core de nenhum sistema operacional. Uma exceção é que as instalações Server Core são compatíveis com a função do sistema de sites de ponto de distribuição. Para obter mais informações, confira [Sistemas operacionais com suporte para servidores de sistema de sites do Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  

- Depois que um servidor de sistema de sites é instalado, não há suporte para alterar:  

    - O nome de domínio do domínio em que o computador do sistema de sites está localizado (também chamado de uma **renomeação de domínio**).  

    - A associação de domínio do computador.  

    - O nome do computador.  

  Se você precisar alterar um desses itens, primeiro remova a função do sistema de sites do computador. Reinstale a função depois que a alteração for concluída. Para as alterações que afetam o servidor do site, primeiro desinstale o site. Reinstale o site depois que a alteração for concluída.  

- Não há suporte para funções do sistema de sites em uma instância de um cluster do Windows Server. A única exceção é o servidor de banco de dados do site. Para obter mais informações, confira [Usar um cluster do SQL Server para o banco de dados do site do Configuration Manager](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database).  

    Da versão 1810 em diante, o processo de instalação do Configuration Manager não bloqueia mais a instalação da função de servidor de site em um computador com a função do Windows para clustering de failover. O Always On do SQL requer essa função; portanto, anteriormente não era possível colocar o banco de dados do site no servidor do site. Com essa alteração, é possível criar um site altamente disponível com menos servidores usando o Always On do SQL e um servidor do site no modo passivo. Para obter mais informações, confira [Opções de alta disponibilidade](/sccm/core/servers/deploy/configure/high-availability-options). <!--3607761, fka 1359132-->  

- Não há suporte para alterar as configurações de tipo de inicialização ou de “Fazer logon como” de qualquer serviço do Configuration Manager. Se você fizer isso, poderá impedir que serviços essenciais funcionem corretamente.  


###  <a name="bkmk_2012Prereq"></a> Pré-requisitos para o Windows Server 2012 e sistemas operacionais posteriores  

Confira as seções principais deste artigo para obter os pré-requisitos específicos para servidores e funções do sistema de sites no Windows Server 2012 e em versões posteriores:

- [Servidores do site de administração central e do site primário](#bkmk_2012sspreq)
- [Servidor do site secundário](#bkmk_2012secpreq)
- [Servidor de banco de dados](#bkmk_2012dbpreq)
- [Servidor do provedor de SMS](#bkmk_2012smsprovpreq)
- [Ponto de site da Web do catálogo de aplicativos](#bkmk_2012acwspreq)
- [Ponto de serviços Web do catálogo de aplicativos](#bkmk_2012ACwsitepreq)
- [Ponto de sincronização do Asset Intelligence](#bkmk_2012AIpreq)
- [Ponto de registro de certificado](#bkmk_2012crppreq)
- [Ponto de distribuição](#bkmk_2012dppreq)
- [Ponto do Endpoint Protection](#bkmk_2012EPPpreq)
- [Ponto de registro](#bkmk_2012Enrollpreq)
- [Ponto proxy do registro](#bkmk_2012EnrollProxpreq)
- [Ponto de status de fallback](#bkmk_2012FSPpreq)
- [Ponto de gerenciamento](#bkmk_2012MPpreq)
- [Ponto do Reporting Services](#bkmk_2012RSpoint)
- [Ponto de conexão de serviço](#bkmk_SCPpreq)
- [Ponto de atualização de software](#bkmk_2012SUPpreq)
- [Ponto de migração de estado](#bkmk_2012SMPpreq)

##  <a name="bkmk_2012sspreq"></a> Servidores do site de administração central e do site primário 

#### <a name="windows-server-roles-and-features"></a>Recursos e funções do Windows Server  

- .NET Framework 3.5 SP1 (ou posterior)  

- .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2  

    - Para obter mais informações sobre as versões do .NET Framework, confira [Versões e dependências do .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).

- Compactação Diferencial Remota  

#### <a name="windows-adk"></a>Windows ADK  

- Antes de instalar ou atualizar um site de administração central ou um site primário, instale a versão do ADK (Kit de Avaliação e Implantação) do Windows exigida pela versão do Configuration Manager que você está instalando ou atualizando. Para obter mais informações, confira [ADK do Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).  

- Para mais informações sobre esse requisito, consulte [Requisitos de infraestrutura para implantação do sistema operacional](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

#### <a name="visual-c-redistributable"></a>Pacotes Redistribuíveis do Visual C++  

- O Configuration Manager instala o Pacote Redistribuível do Microsoft Visual C++ 2013 em cada computador que instala um servidor do site.  

- Os sites de administração central e os sites primários exigem as versões x86 e x64 do arquivo de pacotes redistribuíveis aplicáveis.  



##  <a name="bkmk_2012secpreq"></a> Servidor do site secundário   

#### <a name="windows-server-roles-and-features"></a>Recursos e funções do Windows Server  

- .NET Framework 3.5 SP1 (ou posterior)  

- .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2  

    - Para obter mais informações sobre as versões do .NET Framework, confira [Versões e dependências do .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).  

- Compactação Diferencial Remota  

#### <a name="visual-c-redistributable"></a>Pacotes Redistribuíveis do Visual C++  

- O Configuration Manager instala o Pacote Redistribuível do Microsoft Visual C++ 2013 em cada computador que instala um servidor do site.  

- Os sites secundários exigem somente a versão x64.  

#### <a name="default-site-system-roles"></a>Funções do sistema de sites padrão  

- Por padrão, um site secundário instala um **ponto de gerenciamento** e um **ponto de distribuição**.  

- Certifique-se de que o servidor de site secundário atenda aos pré-requisitos para estas funções do sistema de sites.  



##  <a name="bkmk_2012dbpreq"></a> Servidor de banco de dados  

#### <a name="remote-registry-service"></a>Serviço de Registro remoto  

- Durante a instalação do site do Configuration Manager, habilite o serviço **Registro Remoto** no computador que hospeda o banco de dados do site.  

#### <a name="sql-server"></a>SQL Server  

- Antes de instalar um site de administração central ou um site primário, instale uma versão com suporte do SQL Server para hospedar o banco de dados do site. Para obter mais informações, confira [Versões do SQL Server com suporte](/sccm/core/plan-design/configs/support-for-sql-server-versions).  

- Antes de instalar um site secundário, você pode instalar uma versão com suporte do SQL Server.  

- Se você optar por fazer o Configuration Manager instalar o SQL Server Express como parte de uma instalação do site secundário, verifique se o computador atende aos requisitos para execução do SQL Server Express.  



##  <a name="bkmk_2012smsprovpreq"></a> Servidor do Provedor de SMS  

#### <a name="windows-adk"></a>Windows ADK  

- O computador no qual você instala uma instância do Provedor de SMS deve ter a versão exigida do Windows ADK exigida pela versão do Configuration Manager que você está instalando ou atualizando. Para obter mais informações, confira [ADK do Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).  

- Para mais informações sobre esse requisito, consulte [Requisitos de infraestrutura para implantação do sistema operacional](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

#### <a name="windows-server-roles-and-features"></a>Recursos e funções do Windows Server  

- Se você está utilizando o [serviço de administração](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_admin-service), o servidor host da função de provedor de SMS requer o .NET versão 4.5.2 ou posterior  <!-- SCCMDocs issue #1203 -->

- Web Server (IIS)

##  <a name="bkmk_2012acwspreq"></a> Ponto de sites da Web do Catálogo de Aplicativos  

#### <a name="windows-server-roles-and-features"></a>Recursos e funções do Windows Server  

- .NET Framework 3.5 SP1 (ou posterior)  

- .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2  

    - ASP.NET 4.5  

    - Para obter mais informações sobre as versões do .NET Framework, confira [Versões e dependências do .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).  


#### <a name="iis-configuration"></a>Configuração do IIS  

-   Recursos HTTP comuns:  

    -   Documento padrão  

    -   Conteúdo Estático  

-   Desenvolvimento de aplicativos:  

    -   ASP.NET 3.5 (e opções selecionadas automaticamente)  

    -   ASP.NET 4.5 (e opções selecionadas automaticamente)  

    -   Extensibilidade 3.5 do .NET  

    -   Extensibilidade 4.5 do .NET  

-   Segurança:  

    -   Autenticação do Windows  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  



##  <a name="bkmk_2012ACwsitepreq"></a> Ponto de serviços Web do Catálogo de Aplicativos  

#### <a name="windows-server-roles-and-features"></a>Recursos e funções do Windows Server  

-   .NET Framework 3.5 SP1 (ou posterior)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2:  

    -   ASP.NET 4.5:  

        -   Ativação HTTP (e opções selecionadas automaticamente)  

#### <a name="iis-configuration"></a>Configuração do IIS  

-   Recursos HTTP comuns:  

    -   Documento padrão  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  

-   Desenvolvimento de aplicativos:  

    -   ASP.NET 3.5 (e opções selecionadas automaticamente)  

    -   Extensibilidade 3.5 do .NET  

    -   ASP.NET 4.5 (e opções selecionadas automaticamente)  

    -   Extensibilidade 4.5 do .NET  

#### <a name="computer-memory"></a>Memória do computador  

-   O computador que hospeda esta função do sistema de sites deve ter, no mínimo, 5% da memória livre disponível dos computadores para habilitar a função do sistema de sites para processar solicitações.  

-   Quando essa função do sistema de sites estiver localizada no mesmo local que outra função do sistema de sites que tenha esse mesmo requisito, esse requisito de memória do computador não será aumentado, mas permanecerá no mínimo de 5%.  



##  <a name="bkmk_2012AIpreq"></a> Ponto de sincronização do Asset Intelligence  

#### <a name="windows-server-roles-and-features"></a>Recursos e funções do Windows Server  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 



##  <a name="bkmk_2012crppreq"></a> Ponto de registro de certificado  

#### <a name="windows-server-roles-and-features"></a>Recursos e funções do Windows Server  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2:  

    -   Ativação HTTP  

#### <a name="iis-configuration"></a>Configuração do IIS  

-   Desenvolvimento de aplicativos:  

    -   ASP.NET 3.5 (e opções selecionadas automaticamente)  

    -   ASP.NET 4.5 (e opções selecionadas automaticamente)  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  

    -   Compatibilidade de WMI do IIS 6  



##  <a name="bkmk_2012dppreq"></a> Ponto de distribuição  

#### <a name="windows-server-roles-and-features"></a>Recursos e funções do Windows Server  

-   Compactação Diferencial Remota  

#### <a name="iis-configuration"></a>Configuração do IIS  

-   Desenvolvimento de aplicativos:  

    -   Extensões ISAPI  

-   Segurança:  

    -   Autenticação do Windows  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  

    -   Compatibilidade de WMI do IIS 6  

#### <a name="powershell"></a>PowerShell  

-   No Windows Server 2012 ou posterior, o PowerShell 3.0 ou 4.0 é exigido antes da instalação do ponto de distribuição.  

#### <a name="visual-c-redistributable"></a>Pacotes Redistribuíveis do Visual C++  

-   O Configuration Manager instala o Pacote Redistribuível do Microsoft Visual C++ 2013 em cada computador que hospeda um ponto de distribuição.  

-   A versão instalada depende da plataforma do computador (x86 ou x64).  

#### <a name="microsoft-azure"></a>Microsoft Azure  

-   Você pode usar um serviço de nuvem no Microsoft Azure para hospedar um ponto de distribuição.  

#### <a name="to-support-pxe-or-multicast"></a>Para dar suporte a PXE ou multicast  

-   Instale e configure a função de WDS (Serviços de Implantação do Windows) do Windows Server.  

    > [!NOTE]  
    >  O WDS é instalado e configurado automaticamente quando você configura um ponto de distribuição, a fim de dar suporte a PXE ou multicast em um servidor que executa o Windows Server 2012 ou posterior.  

-   Começando na versão 1806, é possível habilitar um respondente PXE em um ponto de distribuição sem o serviço de Implantação do Windows.  

Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> Quando o ponto de distribuição transfere conteúdo, ele usa o **BITS** (Serviço de Transferência Inteligente em Segundo Plano) interno do Windows. A função de ponto de distribuição não exige a instalação do recurso Extensão do Servidor IIS do BITS, pois o cliente não carrega informações nele.  



##  <a name="bkmk_2012EPPpreq"></a> Ponto do Endpoint Protection  

#### <a name="windows-server-roles-and-features"></a>Recursos e funções do Windows Server  

-   .NET Framework 3.5 SP1 (ou posterior)  

-   Recursos do Windows Defender (Windows Server 2016 ou posterior)  



##  <a name="bkmk_2012Enrollpreq"></a> Ponto de registro  

#### <a name="windows-server-roles-and-features"></a>Recursos e funções do Windows Server  

- .NET Framework 3.5 (ou posterior)  

- .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2:  

     Quando essa função do sistema de sites é instalada, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor em um estado de reinicialização pendente. Se uma reinicialização fica pendente para o .NET Framework, os aplicativos .NET podem falhar até que o servidor seja reinicializado e a instalação seja concluída.  

    - Ativação HTTP (e opções selecionadas automaticamente)  

    - ASP.NET 4.5  

    - Serviços do WCF (Windows Communication Foundation)<!-- SCCMDocs issue #1168 -->  

#### <a name="iis-configuration"></a>Configuração do IIS  

-   Recursos HTTP comuns:  

    -   Documento padrão  

-   Desenvolvimento de aplicativos:  

    -   ASP.NET 3.5 (e opções selecionadas automaticamente)  

    -   Extensibilidade 3.5 do .NET  

    -   ASP.NET 4.5 (e opções selecionadas automaticamente)  

    -   Extensibilidade 4.5 do .NET  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  

#### <a name="computer-memory"></a>Memória do computador  

-   O computador que hospeda esta função do sistema de sites deve ter, no mínimo, 5% da memória livre disponível dos computadores para habilitar a função do sistema de sites para processar solicitações.  

-   Quando essa função do sistema de sites estiver localizada no mesmo local que outra função do sistema de sites que tenha esse mesmo requisito, esse requisito de memória do computador não será aumentado, mas permanecerá no mínimo de 5%.  



##  <a name="bkmk_2012EnrollProxpreq"></a> Ponto proxy do registro  

#### <a name="windows-server-roles-and-features"></a>Recursos e funções do Windows Server  

-   .NET Framework 3.5 (ou posterior)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 

     Quando essa função do sistema de sites é instalada, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor em um estado de reinicialização pendente. Se uma reinicialização fica pendente para o .NET Framework, os aplicativos .NET podem falhar até que o servidor seja reinicializado e a instalação seja concluída.  

#### <a name="iis-configuration"></a>Configuração do IIS  

-   Recursos HTTP comuns:  

    -   Documento padrão  

    -   Conteúdo Estático  

-   Desenvolvimento de aplicativos:  

    -   ASP.NET 3.5 (e opções selecionadas automaticamente)  

    -   ASP.NET 4.5 (e opções selecionadas automaticamente)  

    -   Extensibilidade 3.5 do .NET  

    -   Extensibilidade 4.5 do .NET  

-   Segurança:  

    -   Autenticação do Windows  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  

#### <a name="computer-memory"></a>Memória do computador  

-   O computador que hospeda esta função do sistema de sites deve ter, no mínimo, 5% da memória livre disponível dos computadores para habilitar a função do sistema de sites para processar solicitações.  

-   Quando essa função do sistema de sites estiver localizada no mesmo local que outra função do sistema de sites que tenha esse mesmo requisito, esse requisito de memória do computador não será aumentado, mas permanecerá no mínimo de 5%.  



##  <a name="bkmk_2012FSPpreq"></a> Ponto de status de fallback 

#### <a name="windows-server-roles-and-features"></a>Recursos e funções do Windows Server 

-   Extensões de Servidor BITS (e opções selecionadas automaticamente) ou BITS (Serviço de Transferência Inteligente em Segundo Plano) (e opções selecionadas automaticamente) 

#### <a name="iis-configuration"></a>Configuração do IIS 

A configuração padrão do IIS é necessária com as seguintes adições:  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  



##  <a name="bkmk_2012MPpreq"></a> Ponto de gerenciamento  

#### <a name="windows-server-roles-and-features"></a>Recursos e funções do Windows Server  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 

-   Extensões de Servidor BITS (e opções selecionadas automaticamente) ou BITS (Serviço de Transferência Inteligente em Segundo Plano) (e opções selecionadas automaticamente)  

#### <a name="iis-configuration"></a>Configuração do IIS  

-   Desenvolvimento de aplicativos:  

    -   Extensões ISAPI  

-   Segurança:  

    -   Autenticação do Windows  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  

    -   Compatibilidade de WMI do IIS 6  



##  <a name="bkmk_2012RSpoint"></a> Ponto do Reporting Services  

#### <a name="windows-server-roles-and-features"></a>Recursos e funções do Windows Server  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 

#### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services  

-   Instale e configure pelo menos uma instância do SQL Server para dar suporte ao SQL Server Reporting Services antes da instalação do ponto de relatório.  

-   A instância usada para o SQL Server Reporting Services pode ser a mesma instância usada para o banco de dados do site.  

-   Além disso, a instância que você usar pode ser compartilhada com outros produtos do System Center, contanto que os outros produtos do System Center não tenham restrições para compartilhar a instância do SQL Server.  



##  <a name="bkmk_SCPpreq"></a> Ponto de conexão de serviço  

#### <a name="windows-server-roles-and-features"></a>Recursos e funções do Windows Server  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 

     Quando essa função do sistema de sites é instalada, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor em um estado de reinicialização pendente. Se uma reinicialização fica pendente para o .NET Framework, os aplicativos .NET podem falhar até que o servidor seja reinicializado e a instalação seja concluída.  

#### <a name="visual-c-redistributable"></a>Pacotes Redistribuíveis do Visual C++  

-   O Configuration Manager instala o Pacote Redistribuível do Microsoft Visual C++ 2013 em cada computador que hospeda um ponto de distribuição.  

-   A função do sistema de sites exige a versão x64.  



##  <a name="bkmk_2012SUPpreq"></a> Ponto de atualização de software  

#### <a name="windows-server-roles-and-features"></a>Recursos e funções do Windows Server  

-   .NET Framework 3.5 SP1 (ou posterior)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 

A configuração padrão do IIS é necessária.

#### <a name="windows-server-update-services"></a>Windows Server Update Services  

-   Instale a função de servidor Windows Server Update Services no computador antes de instalar um ponto de atualização de software.  

-   Para obter mais informações, confira [Planejar atualizações de software](/sccm/sum/plan-design/plan-for-software-updates).  

> [!NOTE]  
> Ao usar um Ponto de Atualização de Software em um servidor que não seja o servidor do site, instale primeiro o Console de Administração do WSUS no servidor do site.   

##  <a name="bkmk_2012SMPpreq"></a> Ponto de migração de estado  
<!--SCCMDocs issue 645-->
#### <a name="windows-server-roles-and-features"></a>Recursos e funções do Windows Server  

-   .NET Framework 3.5 (ou posterior)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2:  

     Quando essa função do sistema de sites é instalada, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor em um estado de reinicialização pendente. Se uma reinicialização fica pendente para o .NET Framework, os aplicativos .NET podem falhar até que o servidor seja reinicializado e a instalação seja concluída.  

    -   Ativação HTTP (e opções selecionadas automaticamente)  

    -   ASP.NET 4.5  

#### <a name="iis-configuration"></a>Configuração do IIS  

-   Recursos HTTP comuns:  

    -   Documento padrão  

-   Desenvolvimento de aplicativos:  

    -   ASP.NET 3.5 (e opções selecionadas automaticamente)  

    -   Extensibilidade 3.5 do .NET  

    -   ASP.NET 4.5 (e opções selecionadas automaticamente)  

    -   Extensibilidade 4.5 do .NET  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  



##  <a name="bkmk_2008"></a> Pré-requisitos para o Windows Server 2008 R2 e Windows Server 2008  

Agora, o Windows Server 2008 e o Windows Server 2008 R2 estão em suporte estendido e não mais em suporte maintstream, conforme detalhado pelo [Ciclo de Vida do Suporte da Microsoft](https://support.microsoft.com/lifecycle). Para obter mais informações sobre o suporte futuro para esses sistemas operacionais, como servidores do sistema de sites com o Configuration Manager, consulte [Sistemas operacionais de servidor removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#server-os).  

Não há suporte para essas versões de sistema operacional para servidores do site nem para a maioria das funções do sistema de sites. Elas ainda são compatíveis com a função do sistema de sites de ponto de distribuição, incluindo pontos de distribuição por pull, PXE e multicast.


###  <a name="bkmk_2008dppreq"></a> Ponto de distribuição  

#### <a name="iis-configuration"></a>Configuração do IIS

É possível usar a configuração padrão do IIS ou uma configuração personalizada. Para usar uma configuração personalizada do IIS, você deve habilitar as seguintes opções para o IIS:  

-   Desenvolvimento de aplicativos:  

    -   Extensões ISAPI  

-   Segurança:  

    -   Autenticação do Windows  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  

    -   Compatibilidade de WMI do IIS 6  

Ao usar uma configuração personalizada do IIS, é possível remover opções que não são necessárias, como os itens a seguir:  

-   Recursos HTTP comuns:  

    -   Redirecionamento de HTTP  

-   Scripts de gerenciamento e ferramentas do IIS  

#### <a name="windows-feature"></a>Recurso do Windows  

-   Compactação Diferencial Remota  

#### <a name="visual-c-redistributable"></a>Pacotes Redistribuíveis do Visual C++  

-   O Configuration Manager instala o Pacote Redistribuível do Microsoft Visual C++ 2013 em cada computador que hospeda um ponto de distribuição.  

-   A versão instalada depende da plataforma do computador (x86 ou x64).  

#### <a name="microsoft-azure"></a>Microsoft Azure  

-   Você pode usar um serviço de nuvem no Azure para hospedar um ponto de distribuição.  

#### <a name="to-support-pxe-or-multicast"></a>Para dar suporte a PXE ou multicast  

-   Instale e configure a função de WDS (Serviços de Implantação do Windows) do Windows Server.  

    > [!NOTE]  
    >  O WDS é instalado e configurado automaticamente quando você configura um ponto de distribuição, a fim de dar suporte a PXE ou multicast em um servidor que executa o Windows Server 2012 ou posterior.  

-   Começando na versão 1806, é possível habilitar um respondente PXE em um ponto de distribuição sem o serviço de Implantação do Windows.  

Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> Quando o ponto de distribuição transferir conteúdo, transferirá usando o BITS **Serviço de Transferência Inteligente em Segundo Plano** integrado ao sistema operacional Windows. A função do ponto de distribuição não exige a instalação do recurso BITS IIS Server Extension, pois o cliente não carrega informações nele.   

