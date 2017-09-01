---
title: "Pré-requisitos do site | Microsoft Docs"
description: Saiba como configurar um computador Windows com um servidor de sistema de sites do System Center Configuration Manager.
ms.custom: na
ms.date: 8/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 09749a3045ca6eebf1363b6e53cd8607b5f32578
ms.sourcegitcommit: 974fbc4408028c8be28911e5cd646efcf47c7f15
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
---
# <a name="site-and-site-system-prerequisites-for-system-center-configuration-manager"></a>Pré-requisitos de site e do sistema de sites para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


 Computadores baseados em Windows exigem configurações específicas para dar suporte ao uso como servidores do sistema de sites do System Center Configuration Manager.  

 
 Para alguns produtos, como o WSUS (Windows Server Update Services) para o ponto de atualização de software, você precisa consultar essa documentação de produtos para identificar os pré-requisitos adicionais e as limitações de uso do produto. Somente as configurações que se aplicam diretamente ao uso com o Configuration Manager estão incluídas aqui.   

> [!NOTE]  
>  Em janeiro de 2016, o suporte expirou para o .NET Framework 4.0, 4.5 e 4.5.1. Para obter mais informações, consulte [Perguntas frequentes sobre a política do ciclo de vida de suporte do Microsoft .NET Framework](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update) em support.microsoft.com.  

## <a name="bkmk_generalprerewq"></a> Requisitos e limitações gerais do servidor do site
**O seguinte se aplica a todos os servidores do sistema de sites:**

-   Cada servidor do sistema de sites deve usar um sistema operacional de 64 bits. A única exceção é a função do sistema de sites do ponto de distribuição, que pode ser instalada em alguns sistemas operacionais de 32 bits.  

-   Não há suporte para os sistemas de sites em instalações do Server Core de qualquer sistema operacional. Uma exceção a isso é que as instalações do Server Core têm suporte para a função do sistema de sites do ponto de distribuição, sem o suporte a multicast ou PXE.  

-   Depois que um servidor de sistema de sites é instalado, não há suporte para alterar:  

    -   O nome de domínio do domínio em que o computador do sistema de sites está localizado (também chamado de uma **renomeação de domínio**).  

    -   A associação de domínio do computador.  

    -   O nome do computador.  

  Se precisar alterar qualquer uma dessas, primeiro remova a função do sistema de sites do computador e reinstale a função após a conclusão da alteração. Se isso afetar o computador do servidor do site, será necessário desinstalar o site e reinstalá-lo depois que a alteração for concluída.  

-   Não há suporte para as funções do sistema de sites em uma instância de um cluster do Windows Server. A única exceção é o servidor de banco de dados do site.  

-   Não há suporte para alterar as configurações de tipo de inicialização ou de “Fazer logon como” de qualquer serviço do Configuration Manager. Se você fizer isso, poderá impedir que serviços essenciais funcionem corretamente.  

##  <a name="bkmk_2012Prereq"></a> Pré-requisitos para o Windows Server 2012 e sistemas operacionais posteriores  
###  <a name="bkmk_2012sspreq"></a> Servidor do site: site primário e site de administração central  
  **Funções e recursos do Windows Server:**  

-   .NET Framework 3.5 SP1 (ou posterior)  

-   .NET Framework 4.5.2  

-   Compactação Diferencial Remota  

**Windows ADK:**  

-   Antes de instalar ou atualizar um site de administração central ou site primário, você deve instalar a versão do ADK (Kit de Avaliação e Implantação) do Windows exigida pela versão do Configuration Manager que você está instalando ou atualizando. Confira [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk) no Suporte para Windows 10 como um tópico de cliente.  

-   Para mais informações sobre esse requisito, consulte [Requisitos de infraestrutura para implantação do sistema operacional](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

**Pacotes Redistribuíveis do Visual C++:**  

-   O Configuration Manager instala o Pacote Redistribuível do Microsoft Visual C++ 2013 em cada computador que instala um servidor do site.  

-   Os sites de administração central e os sites primários exigem as versões x86 e x64 do arquivo dos Pacotes Redistribuíveis aplicáveis.  

###  <a name="bkmk_2012secpreq"></a> Servidor do site: site secundário  
**Funções e recursos do Windows Server:**  

-   .NET Framework 3.5 SP1 (ou posterior)  

-   .NET Framework 4.5.2  

-   Compactação Diferencial Remota  

**Pacotes Redistribuíveis do Visual C++:**  

-   O Configuration Manager instala o Pacote Redistribuível do Microsoft Visual C++ 2013 em cada computador que instala um servidor do site.  

-   Os sites secundários exigem somente a versão x64.  

**Funções padrão do sistema de sites:**  

-   Por padrão, um site secundário instala um **ponto de gerenciamento** e um **ponto de distribuição**.  

-   Certifique-se de que o servidor de site secundário atenda aos pré-requisitos para estas funções do sistema de sites.  

###  <a name="bkmk_2012dbpreq"></a> Servidor de banco de dados  
**Serviço Registro Remoto:**  

-   Durante a instalação do site do Configuration Manager, você deve habilitar o serviço Registro remoto no computador que hospedará o banco de dados do site.  

**SQL Server:**  

-   Antes de instalar um site de administração central ou site primário, você deve instalar uma versão com suporte do SQL Server a fim de hospedar o banco de dados do site.  

-   Antes de instalar um site secundário, você pode instalar uma versão com suporte do SQL Server.  

-   Se você optar por fazer o Configuration Manager instalar o SQL Server Express como parte de uma instalação do site secundário, verifique se o computador atende aos requisitos para execução do SQL Server Express.  

###  <a name="bkmk_2012smsprovpreq"></a> Servidor do Provedor de SMS  
**Windows ADK:**  

-   O computador no qual você instala uma instância do Provedor de SMS deve ter a versão exigida do Windows ADK exigida pela versão do Configuration Manager que você está instalando ou atualizando. Confira [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk) no Suporte para Windows 10 como um tópico de cliente.

-   Para mais informações sobre esse requisito, consulte [Requisitos de infraestrutura para implantação do sistema operacional](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

###  <a name="bkmk_2012acwspreq"></a> Ponto de sites da Web do Catálogo de Aplicativos  
**Funções e recursos do Windows Server:**  

-   .NET Framework 3.5 SP1 (ou posterior)  

-   .NET Framework 4.5.2:  

    -   ASP.NET 4.5  

**Configuração do IIS:**  

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

###  <a name="bkmk_2012ACwsitepreq"></a> Ponto de serviços Web do Catálogo de Aplicativos  
**Funções e recursos do Windows Server:**  

-   .NET Framework 3.5 SP1 (ou posterior)  

-   .NET Framework 4.5.2:  

    -   ASP.NET 4.5:  

        -   Ativação HTTP (e opções selecionadas automaticamente)  

**Configuração do IIS:**  

-   Recursos HTTP comuns:  

    -   Documento padrão  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  

-   Desenvolvimento de aplicativos:  

    -   ASP.NET 3.5 (e opções selecionadas automaticamente)  

    -   Extensibilidade 3.5 do .NET  

    -   ASP.NET 4.5 (e opções selecionadas automaticamente)  

    -   Extensibilidade 4.5 do .NET  

**Memória do computador:**  

-   O computador que hospeda esta função do sistema de sites deve ter, no mínimo, 5% da memória livre disponível dos computadores para habilitar a função do sistema de sites para processar solicitações.  

-   Quando esta função do sistema de sites estiver colocalizada com outra função do sistema de sites que tenha este mesmo requisito, esse requisito de memória do computador não será aumentado, mas permanecerá em, no mínimo, 5%.  

###  <a name="bkmk_2012AIpreq"></a> Ponto de sincronização do Asset Intelligence  
**Funções e recursos do Windows Server:**  

-   .NET Framework 4.5.2  

###  <a name="bkmk_2012crppreq"></a> Ponto de registro de certificado  
**Funções e recursos do Windows Server:**  

-   .NET Framework 4.5.2:  

    -   Ativação HTTP  

**Configuração do IIS:**  

-   Desenvolvimento de aplicativos:  

    -   ASP.NET 3.5 (e opções selecionadas automaticamente)  

    -   ASP.NET 4.5 (e opções selecionadas automaticamente)  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  

    -   Compatibilidade de WMI do IIS 6  

###  <a name="bkmk_2012dppreq"></a> Ponto de distribuição  
**Funções e recursos do Windows Server:**  

-   Compactação Diferencial Remota  

**Configuração do IIS:**  

-   Desenvolvimento de aplicativos:  

    -   Extensões ISAPI  

-   Segurança:  

    -   Autenticação do Windows  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  

    -   Compatibilidade de WMI do IIS 6  

**PowerShell:**  

-   No Windows Server 2012 ou posterior, o PowerShell 3.0 ou 4.0 é exigido antes da instalação do ponto de distribuição.  

**Pacotes Redistribuíveis do Visual C++:**  

-   O Configuration Manager instala o Pacote Redistribuível do Microsoft Visual C++ 2013 em cada computador que hospeda um ponto de distribuição.  

-   A versão instalada depende da plataforma do computador (x86 ou x64).  

**Microsoft Azure:**  

-   Você pode usar um serviço de nuvem no Microsoft Azure para hospedar um ponto de distribuição.  

**Para dar suporte a PXE ou multicast:**  

-   Instale e configure a função de WDS (Serviços de Implantação do Windows) do Windows Server.  

    > [!NOTE]  
    >  O WDS é instalado e configurado automaticamente quando você configura um ponto de distribuição, a fim de dar suporte a PXE ou multicast em um servidor que executa o Windows Server 2012 ou posterior.  

> [!NOTE]  
> A função do sistema de sites do ponto de distribuição não exige o BITS (Serviço de Transferência Inteligente em Segundo Plano). Quando o BITS estiver configurado no computador do ponto de distribuição, o BITS no computador do ponto de distribuição não será usado para facilitar o download de conteúdo por clientes que usam o BITS.  

###  <a name="bkmk_2012EPPpreq"></a> Ponto do Endpoint Protection  
**Funções e recursos do Windows Server:**  

-   .NET Framework 3.5 SP1 (ou posterior)  

###  <a name="bkmk_2012Enrollpreq"></a> Ponto de registro  
**Funções e recursos do Windows Server:**  

-   .NET Framework 3.5 (ou posterior)  

-   .NET Framework 4.5.2:  

     Quando essa função do sistema de sites é instalada, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor em um estado de reinicialização pendente. Quando uma reinicialização fica pendente para o .NET Framework, os aplicativos .NET podem falhar até que o servidor seja reinicializado e a instalação seja concluída.  

    -   Ativação HTTP (e opções selecionadas automaticamente)  

    -   ASP.NET 4.5  


**Configuração do IIS:**  

-   Recursos HTTP comuns:  

    -   Documento padrão  

-   Desenvolvimento de aplicativos:  

    -   ASP.NET 3.5 (e opções selecionadas automaticamente)  

    -   Extensibilidade 3.5 do .NET  

    -   ASP.NET 4.5 (e opções selecionadas automaticamente)  

    -   Extensibilidade 4.5 do .NET  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  

**Memória do computador:**  

-   O computador que hospeda esta função do sistema de sites deve ter, no mínimo, 5% da memória livre disponível dos computadores para habilitar a função do sistema de sites para processar solicitações.  

-   Quando esta função do sistema de sites estiver colocalizada com outra função do sistema de sites que tenha este mesmo requisito, esse requisito de memória do computador não será aumentado, mas permanecerá em, no mínimo, 5%.  

###  <a name="bkmk_2012EnrollProxpreq"></a> Ponto proxy do registro  
**Funções e recursos do Windows Server:**  

-   .NET Framework 3.5 (ou posterior)  

-   .NET Framework 4.5.2  

     Quando essa função do sistema de sites é instalada, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor em um estado de reinicialização pendente. Quando uma reinicialização fica pendente para o .NET Framework, os aplicativos .NET podem falhar até que o servidor seja reinicializado e a instalação seja concluída.  

**Configuração do IIS:**  

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

**Memória do computador:**  

-   O computador que hospeda esta função do sistema de sites deve ter, no mínimo, 5% da memória livre disponível dos computadores para habilitar a função do sistema de sites para processar solicitações.  

-   Quando esta função do sistema de sites estiver colocalizada com outra função do sistema de sites que tenha este mesmo requisito, esse requisito de memória do computador não será aumentado, mas permanecerá em, no mínimo, 5%.  

###  <a name="bkmk_2012FSPpreq"></a> Ponto de status de fallback  
A configuração padrão do IIS é necessária com as seguintes adições:  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  

###  <a name="bkmk_2012MPpreq"></a> Ponto de gerenciamento  
**Funções e recursos do Windows Server:**  

-   .NET Framework 4.5.2  

-   Extensões de Servidor BITS (e opções selecionadas automaticamente) ou BITS (Serviço de Transferência Inteligente em Segundo Plano) (e opções selecionadas automaticamente)  

**Configuração do IIS:**  

-   Desenvolvimento de aplicativos:  

    -   Extensões ISAPI  

-   Segurança:  

    -   Autenticação do Windows  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  

    -   Compatibilidade de WMI do IIS 6  

###  <a name="bkmk_2012RSpoint"></a> Ponto do Reporting Services  
**Funções e recursos do Windows Server:**  

-   .NET Framework 4.5.2  

**SQL Server Reporting Services:**  

-   Você deve instalar e configurar pelo menos uma instância do SQL Server para dar suporte ao SQL Server Reporting Services antes da instalação do ponto do Reporting Services.  

-   A instância usada para o SQL Server Reporting Services pode ser a mesma instância usada para o banco de dados do site.  

-   Além disso, a instância que você usar pode ser compartilhada com outros produtos do System Center, contanto que os outros produtos do System Center não tenham restrições para compartilhar a instância do SQL Server.  

###  <a name="bkmk_SCPpreq"></a> Ponto de conexão de serviço  
**Funções e recursos do Windows Server:**  

-   .NET Framework 4.5.2  

     Quando essa função do sistema de sites é instalada, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor em um estado de reinicialização pendente. Quando uma reinicialização fica pendente para o .NET Framework, os aplicativos .NET podem falhar até que o servidor seja reinicializado e a instalação seja concluída.  

**Pacotes Redistribuíveis do Visual C++:**  

-   O Configuration Manager instala o Pacote Redistribuível do Microsoft Visual C++ 2013 em cada computador que hospeda um ponto de distribuição.  

-   A função do sistema de sites exige a versão x64.  

###  <a name="bkmk_2012SUPpreq"></a> Ponto de atualização de software  
**Funções e recursos do Windows Server:**  

-   .NET Framework 3.5 SP1 (ou posterior)  

-   .NET Framework 4.5.2  

A configuração padrão do IIS é necessária.

**Windows Server Update Services:**  

-   Você deve instalar a função do Windows Server, Windows Server Update Services, em um computador antes de instalar um ponto de atualização de software.  

-   Para obter mais informações, consulte [Planejar atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

### <a name="state-migration-point"></a>Ponto de migração de estado  
A configuração padrão do IIS é necessária.  

##  <a name="bkmk_2008"></a> Pré-requisitos para o Windows Server 2008 R2 e Windows Server 2008  
Agora, o Windows Server 2008 e o Windows Server 2008 R2 estão em suporte estendido e não mais em suporte maintstream, conforme detalhado pelo [Ciclo de Vida do Suporte da Microsoft](https://support.microsoft.com/lifecycle). Para obter mais informações sobre o suporte futuro para esses sistemas operacionais como servidores do sistema de sites com o Configuration Manager, consulte [Recursos removidos e preteridos do System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

**O seguinte se aplica a todos os requisitos do .NET Framework:**  

-   Instale a versão completa do .NET Framework antes de instalar as funções do sistema de sites. Por exemplo, confira o [Microsoft .NET Framework 4 (Instalador autônomo)](http://go.microsoft.com/fwlink/p/?LinkId=193048). O .NET Framework 4 Client Profile é insuficiente para esse requisito.  

**O seguinte se aplica a todos os requisitos de ativação do WCF (Windows Communication Foundation):**  

-   Você pode configurar a ativação do WCF como parte do recurso do Windows, .NET Framework, no servidor do sistema de sites. Por exemplo, no Windows Server 2008 R2, execute o **Assistente para Adicionar Recursos** para instalar recursos adicionais no servidor. Na página **Selecionar Recursos**, expanda **Recursos do NET Framework 3.5.1**, expanda **Ativação do WCF** e marque as caixas de seleção de **Ativação HTTP** e **Ativação não HTTP** para habilitar essas opções.  

###  <a name="bkmk_2008sspreq"></a> Servidor do site: site primário e site de administração central  
**.NET Framework:**  

-   .NET Framework 3.5 SP1 (ou posterior)  

-   .NET Framework 4.5.2  

**Recurso do Windows:**  

-   Compactação Diferencial Remota  

**Windows ADK:**  

-   Antes de instalar ou atualizar um site de administração central ou site primário, você deve instalar a versão do Windows ADK exigida pela versão do Configuration Manager que você está instalando ou atualizando.  Confira [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk) no Suporte para Windows 10 como um tópico de cliente.  

-   Para mais informações sobre esse requisito, consulte [Requisitos de infraestrutura para implantação do sistema operacional](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

**Pacotes Redistribuíveis do Visual C++:**  

-   O Configuration Manager instala o Pacote Redistribuível do Microsoft Visual C++ 2013 em cada computador que instala um servidor do site.  

-   Os sites de administração central e os sites primários exigem as versões x86 e x64 do arquivo dos Pacotes Redistribuíveis aplicáveis.  

###  <a name="bkmk_2008secpreq"></a> Servidor do site: site secundário  
**.NET Framework:**  

-   .NET Framework 3.5 SP1 (ou posterior)  

-   .NET Framework 4.5.2  

**Pacotes Redistribuíveis do Visual C++:**  

-   O Configuration Manager instala o Pacote Redistribuível do Microsoft Visual C++ 2013 em cada computador que instala um servidor do site.  

-   Os sites secundários exigem somente a versão x64.  

**Funções padrão do sistema de sites:**  

-   Por padrão, um site secundário instala um **ponto de gerenciamento** e um **ponto de distribuição**.  

-   Certifique-se de que o servidor de site secundário atenda aos pré-requisitos para estas funções do sistema de sites.  

###  <a name="bkmk_2008dbpreq"></a> Servidor de banco de dados  
**Serviço Registro Remoto:**  

-   Durante a instalação do site do Configuration Manager, você deve habilitar o serviço Registro remoto no computador que hospedará o banco de dados do site.  

**SQL Server:**  

-   Antes de instalar um site de administração central ou site primário, você deve instalar uma versão com suporte do SQL Server a fim de hospedar o banco de dados do site.  

-   Antes de instalar um site secundário, você pode instalar uma versão com suporte do SQL Server.  

-   Se você optar por fazer o Configuration Manager instalar o SQL Server Express como parte de uma instalação do site secundário, verifique se o computador atende aos requisitos para execução do SQL Server Express.  

###  <a name="bkmk_2008smsprovpreq"></a> Servidor do Provedor de SMS  
**Windows ADK:**  

-   O computador no qual você instala uma instância do Provedor de SMS deve ter a versão exigida do Windows ADK exigida pela versão do Configuration Manager que você está instalando ou atualizando. Confira [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk) no Suporte para Windows 10 como um tópico de cliente.  

-   Para mais informações sobre esse requisito, consulte [Requisitos de infraestrutura para implantação do sistema operacional](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

###  <a name="bkmk_2008acwspreq"></a> Ponto de sites da Web do Catálogo de Aplicativos  
**.NET Framework:**  

-   .NET Framework 4.5.2  

**Configuração do IIS:**

A configuração padrão do IIS é necessária com as seguintes adições:  

-   Recursos HTTP comuns:  

    -   Conteúdo Estático  

    -   Documento padrão  

-   Desenvolvimento de aplicativos:  

    -   ASP.NET (e opções selecionadas automaticamente)  

         Em alguns cenários, como quando o IIS é instalado ou reconfigurado após a instalação do .NET Framework versão 4.5.2, você deve habilitar explicitamente o ASP.NET versão 4.5. Por exemplo, em um computador 64 bits que executa o .NET Framework versão 4.0.30319, execute o seguinte comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

-   Segurança:  

    -   Autenticação do Windows  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  

###  <a name="bkmk_2008ACwsitepreq"></a> Ponto de serviços Web do Catálogo de Aplicativos  
**.NET Framework:**  

-   .NET Framework 3.5 SP1 (ou posterior)  

-   .NET Framework 4.5.2  

**Ativação do WCF (Windows Communication Foundation):**  

-   Ativação HTTP  

-   Ativação não HTTP  

**Configuração do IIS:**

A configuração padrão do IIS é necessária com as seguintes adições:  

-   Desenvolvimento de aplicativos:  

    -   ASP.NET (e opções selecionadas automaticamente)  

         Em alguns cenários, como quando o IIS é instalado ou reconfigurado após a instalação do .NET Framework versão 4.5.2, você deve habilitar explicitamente o ASP.NET versão 4.5. Por exemplo, em um computador 64 bits que executa o .NET Framework versão 4.0.30319, execute o seguinte comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  

**Memória do computador:**  

-   O computador que hospeda esta função do sistema de sites deve ter, no mínimo, 5% da memória livre disponível dos computadores para habilitar a função do sistema de sites para processar solicitações.  

-   Quando esta função do sistema de sites estiver colocalizada com outra função do sistema de sites que tenha este mesmo requisito, esse requisito de memória do computador não será aumentado, mas permanecerá em, no mínimo, 5%.  

###  <a name="bkmk_2008AIpreq"></a> Ponto de sincronização do Asset Intelligence  
**.NET Framework:**  

-   .NET Framework 4.5.2  

###  <a name="bkmk_2008crppreq"></a> Ponto de registro de certificado  
**.NET Framework:**  

-   .NET Framework 4.5.2  

-   Ativação HTTP  

**Configuração do IIS:**

A configuração padrão do IIS é necessária com as seguintes adições:  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  

    -   Compatibilidade de WMI do IIS 6  

###  <a name="bkmk_2008dppreq"></a> Ponto de distribuição  
**Configuração do IIS:**

É possível usar a configuração padrão do IIS ou uma configuração personalizada. Para usar uma configuração personalizada do IIS, você deve habilitar as seguintes opções para o IIS:  

-   Desenvolvimento de aplicativos:  

    -   Extensões ISAPI  

-   Segurança:  

    -   Autenticação do Windows  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  

    -   Compatibilidade de WMI do IIS 6  

Ao usar uma configuração personalizada do IIS, é possível remover opções que não são necessárias, como as seguintes:  

-   Recursos HTTP comuns:  

    -   Redirecionamento de HTTP  

-   Scripts de gerenciamento e ferramentas do IIS  

**Recurso do Windows:**  

-   Compactação Diferencial Remota  

**Pacotes Redistribuíveis do Visual C++:**  

-   O Configuration Manager instala o Pacote Redistribuível do Microsoft Visual C++ 2013 em cada computador que hospeda um ponto de distribuição.  

-   A versão instalada depende da plataforma do computador (x86 ou x64).  

**Microsoft Azure:**  

-   Você pode usar um serviço de nuvem no Azure para hospedar um ponto de distribuição.  

**Para dar suporte a PXE ou multicast:**  

-   Instale e configure a função de WDS (Serviços de Implantação do Windows) do Windows Server.  

    > [!NOTE]  
    >  O WDS é instalado e configurado automaticamente quando você configura um ponto de distribuição, a fim de dar suporte a PXE ou multicast em um servidor que executa o Windows Server 2012 ou posterior.  

> [!NOTE]  
> A função do sistema de sites do ponto de distribuição não exige o BITS (Serviço de Transferência Inteligente em Segundo Plano). Quando o BITS estiver configurado no computador do ponto de distribuição, o BITS no computador do ponto de distribuição não será usado para facilitar o download de conteúdo por clientes que usam o BITS.  


###  <a name="bkmk_2008EPPpreq"></a> Ponto do Endpoint Protection  
**.NET Framework:**  

-   .NET Framework 3.5 SP1 (ou posterior)  

###  <a name="bkmk_2008Enrollpreq"></a> Ponto de registro  
**.NET Framework:**  

-   .NET Framework 4.5.2  

     Quando essa função do sistema de sites for instalada, se o servidor ainda não tiver uma versão com suporte do .NET Framework instalada, o Configuration Manager instalará automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor em um estado de reinicialização pendente. Quando uma reinicialização fica pendente para o .NET Framework, os aplicativos .NET podem falhar até que o servidor seja reinicializado e a instalação seja concluída.  

**Ativação do WCF (Windows Communication Foundation):**  

-   Ativação HTTP  

-   Ativação não HTTP  

**Configuração do IIS:**

A configuração padrão do IIS é necessária com as seguintes adições:  

-   Desenvolvimento de aplicativos:  

    -   ASP.NET (e opções selecionadas automaticamente)  

         Em alguns cenários, como quando o IIS é instalado ou reconfigurado após a instalação do .NET Framework versão 4.5.2, você deve habilitar explicitamente o ASP.NET versão 4.5. Por exemplo, em um computador 64 bits que executa o .NET Framework versão 4.0.30319, execute o seguinte comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

**Memória do computador:**  

-   O computador que hospeda esta função do sistema de sites deve ter, no mínimo, 5% da memória livre disponível dos computadores para habilitar a função do sistema de sites para processar solicitações.  

-   Quando esta função do sistema de sites estiver colocalizada com outra função do sistema de sites que tenha este mesmo requisito, esse requisito de memória do computador não será aumentado, mas permanecerá em, no mínimo, 5%.  

###  <a name="bkmk_2008EnrollProxpreq"></a> Ponto proxy do registro  
**.NET Framework:**  

-   .NET Framework 4.5.2  

     Quando essa função do sistema de sites for instalada, se o servidor ainda não tiver uma versão com suporte do .NET Framework instalada, o Configuration Manager instalará automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor em um estado de reinicialização pendente. Quando uma reinicialização fica pendente para o .NET Framework, os aplicativos .NET podem falhar até que o servidor seja reinicializado e a instalação seja concluída.  

**Ativação do WCF (Windows Communication Foundation):**  

-   Ativação HTTP  

-   Ativação não HTTP  

**Configuração do IIS:**

A configuração padrão do IIS é necessária com as seguintes adições:  

-   Desenvolvimento de aplicativos:  

    -   ASP.NET (e opções selecionadas automaticamente)  

         Em alguns cenários, como quando o IIS é instalado ou reconfigurado após a instalação do .NET Framework versão 4.5.2, você deve habilitar explicitamente o ASP.NET versão 4.5. Por exemplo, em um computador 64 bits que executa o .NET Framework versão 4.0.30319, execute o seguinte comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

**Memória do computador:**  

-   O computador que hospeda esta função do sistema de sites deve ter, no mínimo, 5% da memória livre disponível dos computadores para habilitar a função do sistema de sites para processar solicitações.  

-   Quando esta função do sistema de sites estiver colocalizada com outra função do sistema de sites que tenha este mesmo requisito, esse requisito de memória do computador não será aumentado, mas permanecerá em, no mínimo, 5%.  

###  <a name="bkmk_2008FSPpreq"></a> Ponto de status de fallback  
**Configuração do IIS:**

A configuração padrão do IIS é necessária com as seguintes adições:  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  

###  <a name="bkmk_2008MPpreq"></a> Ponto de gerenciamento  
**.NET Framework:**  

-   .NET Framework 4.5.2  

**Configuração do IIS:**

É possível usar a configuração padrão do IIS ou uma configuração personalizada. Cada ponto de gerenciamento habilitado para dar suporte a dispositivos móveis exige uma configuração do IIS adicional para o ASP.NET (e suas opções selecionadas automaticamente).

Em alguns cenários, como quando o IIS é instalado ou reconfigurado após a instalação do .NET Framework versão 4.5.2, você deve habilitar explicitamente o ASP.NET versão 4.5. Por exemplo, em um computador 64 bits que executa o .NET Framework versão 4.0.30319, execute o seguinte comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  


Para usar uma configuração personalizada do IIS, você deve habilitar as seguintes opções para o IIS:  

-   Desenvolvimento de aplicativos:  

    -   Extensões ISAPI  

-   Segurança:  

    -   Autenticação do Windows  

-   Compatibilidade do Gerenciamento do IIS 6:  

    -   Compatibilidade de Metabase do IIS 6  

    -   Compatibilidade de WMI do IIS 6  


Ao usar uma configuração personalizada do IIS, é possível remover opções que não são necessárias, como as seguintes:  

-   Recursos HTTP comuns:  

    -   Redirecionamento de HTTP  

-   Scripts de gerenciamento e ferramentas do IIS  

**Recurso do Windows:**  

-   Extensões de Servidor BITS (e opções selecionadas automaticamente) ou BITS (Serviço de Transferência Inteligente em Segundo Plano) (e opções selecionadas automaticamente)  

###  <a name="bkmk_2008RSpoint"></a> Ponto do Reporting Services  
**.NET Framework:**  

-   .NET Framework 4.5.2  

**SQL Server Reporting Services:**  

-   Você deve instalar e configurar pelo menos uma instância do SQL Server para dar suporte ao SQL Server Reporting Services antes da instalação do ponto do Reporting Services.  

-   A instância usada para o SQL Server Reporting Services pode ser a mesma instância usada para o banco de dados do site.  

-   Além disso, a instância que você usar pode ser compartilhada com outros produtos do System Center, contanto que os outros produtos do System Center não tenham restrições para compartilhar a instância do SQL Server.  

###  <a name="bkmk_2008SCPpreq"></a> Ponto de conexão de serviço  
**.NET Framework:**  

-   .NET Framework 4.5.2  

     Quando essa função do sistema de sites for instalada, se o servidor ainda não tiver uma versão com suporte do .NET Framework instalada, o Configuration Manager instalará automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor em um estado de reinicialização pendente. Quando uma reinicialização fica pendente para o .NET Framework, os aplicativos .NET podem falhar até que o servidor seja reinicializado e a instalação seja concluída.  

**Pacotes Redistribuíveis do Visual C++:**  

-   O Configuration Manager instala o Pacote Redistribuível do Microsoft Visual C++ 2013 em cada computador que hospeda um ponto de distribuição.  

-   A função do sistema de sites exige a versão x64.  

###  <a name="bkmk_2008SUPpreq"></a> Ponto de atualização de software  
**.NET Framework:**  

-   .NET Framework 3.5 SP1 (ou posterior)  

-   .NET Framework 4.5.2  

**Configuração do IIS:**

A configuração padrão do IIS é necessária.  

**Windows Server Update Services:**  

-   Você deve instalar a função do Windows Server, Windows Server Update Services, em um computador antes de instalar um ponto de atualização de software.  

-   Para obter mais informações, consulte [Planejar atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).

###  <a name="bkmk_2008SMPpreq"></a> Ponto de migração de estado  
**Configuração do IIS:**

A configuração padrão do IIS é necessária.  
