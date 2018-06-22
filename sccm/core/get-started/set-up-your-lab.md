---
title: Configurar seu laboratório
titleSuffix: Configuration Manager
description: Configure um laboratório para avaliar o Configuration Manager com a simulação de atividades reais.
ms.date: 09/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b1970688-0cd2-404f-a17f-9e2aa4a78758
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a1799dcffa55de80c0c700a56301d7d71f3b4a48
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32341960"
---
# <a name="set-up-your-system-center-configuration-manager-lab"></a>Configurar seu laboratório do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Ao seguir as orientações descritas neste tópico, você poderá configurar um laboratório para avaliar o Configuration Manager com atividades reais simuladas.  

##  <a name="BKMK_LabCore"></a> Principais componentes  
 Configurar seu ambiente para o System Center Configuration Manager requer alguns componentes principais para dar suporte à instalação do Configuration Manager.    

-   **O ambiente de laboratório usa o Windows Server 2012 R2**, em que vamos instalar o System Center Configuration Manager.  

     Você pode baixar uma versão de avaliação do Windows Server 2012 R2 no [Centro de Avaliação do TechNet](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012).  

     Considere modificar ou desabilitar a Configuração de Segurança Reforçada do Internet Explorer para acessar com mais facilidade alguns dos downloads mencionados ao longo destes exercícios. Leia [Internet Explorer: configuração de segurança avançada](https://technet.microsoft.com/en-us/library/dd883248\(v=ws.10\).aspx) para obter mais informações.  

-   **O ambiente de laboratório usa o SQL Server 2012 SP2** como o banco de dados do site.  

     É possível baixar uma versão de avaliação do SQL Server 2012 no [Centro de Download da Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=29066).  

     O SQL Server tem [versões com suporte do SQL Server](../../core/plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions) que devem ser usadas com o System Center Configuration Manager.  

    -   O Configuration Manager requer uma versão de 64 bits do SQL Server para hospedar o banco de dados do site.  

    -   **SQL_Latin1_General_CP1_CI_AS** como a classe **Agrupamento de SQL** .  

    -   **A autenticação do Windows**, [em vez da autenticação do SQL](https://technet.microsoft.com/library/ms144284.aspx), é necessária.  

    -   Uma **instância do SQL Server** dedicada é necessária.  

    -   Não limite a **memória endereçável de sistema** para o SQL Server.  

    -   Configure a **conta de serviço do SQL Server** para ser executado usando uma conta de usuário de domínio com direitos limitados.  

    -   É necessário instalar o **SQL Server Reporting Services**.  

    -   **Comunicações entre sites** usam o SQL Server Service Broker na porta padrão TCP 4022.  

    -   **Comunicações intrasite** entre o mecanismo de banco de dados do SQL Server e as funções de sistema de sites do Configuration Manager selecionadas usam a porta padrão TCP 1433.  

-   **O controlador de domínio usa o Windows Server 2008 R2** com o Active Directory Domain Services instalado. O controlador de domínio também funciona como o host para os servidores DHCP e DNS para uso com um nome de domínio totalmente qualificado.  

     Para obter mais informações, consulte esta [Visão geral do Active Directory Domain Services](https://technet.microsoft.com/en-us/library/hh831484).  

-   **O Hyper-V é usado com algumas máquinas virtuais** para verificar se as etapas de gerenciamento executadas nestes exercícios estão funcionando conforme o esperado. Um mínimo de três máquinas virtuais é recomendado, com o Windows 7 (ou posterior) instalado.  

     Para obter mais informações, consulte [Visão geral do Hyper-V](https://technet.microsoft.com/en-us/library/hh831531.aspx).  

-   **Serão necessárias permissões de administrador** para todos esses componentes. O  

    -   O Configuration Manager requer um administrador com permissões locais no ambiente do Windows Server  

    -   O Active Directory requer um administrador com permissões para modificar o esquema  

    -   As máquinas virtuais exigem permissões locais nas próprias máquinas  

Embora não seja necessário para este laboratório, você pode examinar [Configurações com suporte para o System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md) para obter informações adicionais sobre os requisitos para a implementação do System Center Configuration Manager. Consulte a documentação para ver as versões de software diferentes daquelas mencionadas aqui.  

Depois de instalar todos esses componentes, existem outras etapas necessárias para configurar o ambiente do Windows para o Configuration Manager:  

##  <a name="BKMK_LabADPrep"></a> Preparar o conteúdo do Active Directory para o laboratório  
 Para este laboratório, você criará um grupo de segurança e adicionará um usuário de domínio a ele.  

-   Grupo de segurança: **Evaluation**  

    -   Escopo do grupo: **Universal**  

    -   Tipo de grupo: **Security**  

-   Usuário de domínio: **ConfigUser**  

     Em circunstâncias normais, você não concederia acesso universal a todos os usuários em seu ambiente. Você está fazendo isso com esse usuário para simplificar a ativação de seu laboratório online.  

As próximas etapas necessárias para habilitar clientes do Configuration Manager a consultar o Active Directory Domain Services a fim de localizar os recursos do site são listadas nos próximos procedimentos.  

##  <a name="BKMK_CreateSysMgmtLab"></a> Criar o contêiner do System Management  
 O Configuration Manager não criará automaticamente o contêiner necessário do System Management no Active Directory Domain Services quando o esquema é estendido. Portanto, você vai criá-lo para o laboratório. Essa etapa exigirá a [instalação do Editor ADSI.](https://technet.microsoft.com/en-us/library/cc773354\(WS.10\).aspx#BKMK_InstallingADSIEdit)  

 Verifique se você está conectado com uma conta que tem a permissão **Criar Todos os Objetos Filho** no Contêiner **Sistema** dos Serviços de Domínio do Active Directory.  

#### <a name="to-create-the-system-management-container"></a>Para criar o contêiner do System Management:  

1.  Execute o **Editor ADSI**e conecte-se ao domínio em que o servidor do site reside.  

2.  Expanda o **Domínio&lt;nome de domínio totalmente qualificado do computador\>**, expanda o **<nome diferenciado\>**, clique com o botão direito do mouse em **CN=System**, clique em **Novo** e em **Objeto**.  

3.  Na caixa de diálogo **Criar Objeto** , selecione **Contêiner**e clique em **Próximo**.  

4.  Na caixa **Valor** , digite **System Management**e clique em **Avançar**.  

5.  Clique em **Concluir** para concluir o procedimento.  

##  <a name="BKMK_SetSecPermLab"></a> Definir permissões de segurança para o contêiner do Gerenciamento do Sistema  
 Conceda à conta de computador do servidor do site as permissões necessárias para publicar informações do site no contêiner. Você usará o Editor ADSI para essa tarefa também.  

> [!IMPORTANT]  
>  Confirme se você está conectado ao domínio do servidor do site antes de começar o procedimento a seguir.  

#### <a name="to-set-security-permissions-for-the-system-management-container"></a>Para definir permissões de segurança para o contêiner do System Management:  

1.  No painel do console, expanda o **domínio do servidor do site**, expanda **DC=&lt;nome diferenciado do servidor\>** e depois expanda **CN=System**. Clique com o botão direito do mouse em **CN=System Management**e clique em **Propriedades**.  

2.  Na caixa de diálogo **CN=System Management Properties** , clique na guia **Segurança** e em **Adicionar** para adicionar a conta de computador do servidor do site. Conceda à conta permissões de **Controle Total** .  

3.  Clique em **Avançado**, selecione a conta de computador do servidor de site e clique em **Editar**.  

4.  Na lista **Aplicar em** , selecione **Este objeto e todos os descendentes**.  

5.  Clique em **OK** para fechar o console do **Editor ADSI** e concluir o procedimento.  

     Para obter informações adicionais sobre esse procedimento, consulte [Estender o esquema do Active Directory para o System Center Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md)  

##  <a name="BKMK_ExtADSchLab"></a> Estender o esquema do Active Directory usando extadsch.exe  
 Você estenderá o esquema do Active Directory para este laboratório, pois isso permite usar todos os recursos e funcionalidades do Configuration Manager com o mínimo de sobrecarga administrativa. A extensão do esquema do Active Directory é uma configuração aplicada a toda a floresta que só pode feita uma vez por floresta. A extensão do esquema modifica permanentemente o conjunto de classes e de atributos em sua configuração base do Active Directory. Essa ação é irreversível. A extensão do esquema permite que o Configuration Manager acesse os componentes que possibilitarão a ele funcionar com mais eficiência em seu ambiente de laboratório.  

> [!IMPORTANT]  
>  Certifique-se de que você está conectado no controlador de domínio mestre de esquema com uma conta que seja membro do grupo de segurança **Administradores de Esquema** . A tentativa de usar credenciais alternativas falhará.  

#### <a name="to-extend-the-active-directory-schema-using-extadschexe"></a>Para estender o esquema do Active Directory usando o extadsch.exe:  

1.  Crie um backup do estado do sistema do controlador de domínio do mestre de esquema. Para obter mais informações sobre como fazer backup do controlador de domínio mestre, veja [Backup do Windows Server](https://technet.microsoft.com/en-us/library/cc770757.aspx)  

2.  Navegue até **\SMSSETUP\BIN\X64** na mídia de instalação.  

3.  Execute **extadsch.exe**.  

4.  Verifique se a extensão do esquema foi realizada com êxito verificando o **extadsch.log** localizado na pasta raiz da unidade do sistema.  

     Para obter informações adicionais sobre esse procedimento, consulte [Estender o esquema do Active Directory para o System Center Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md).  

##  <a name="BKMK_OtherTasksLab"></a> Outras tarefas necessárias  
 Você também precisará concluir as seguintes tarefas antes da instalação.  

 **Criar uma pasta para armazenar todos os downloads**  

 Haverá vários downloads necessários para os componentes da mídia de instalação ao longo deste exercício. Antes de iniciar qualquer procedimento de instalação, determine um local que não exigirá que você mova esses arquivos até que você deseje desativar o laboratório. É recomendado ter uma única pasta com subpastas separadas para armazenar esses downloads.  

 **Instalar o .NET e ativar o Windows Communication Foundation**  

 Você precisará instalar duas versões do .NET Framework: primeiro, .NET 3.5.1 e, em seguida, .NET 4.5.2+. Você também precisará ativar o WCF (Windows Communication Foundation). O WCF foi projetado para oferecer uma abordagem gerenciável para a computação distribuída, uma ampla interoperabilidade e o suporte direto para a orientação de serviços, além de simplificar o desenvolvimento de aplicativos conectados por meio de um modelo de programação orientado a serviços. Leia [O que é o Windows Communication Foundation?](https://technet.microsoft.com/en-us/subscriptions/ms731082\(v=vs.90\).aspx) para obter mais informações sobre o WCF.  

#### <a name="to-install-net-and-activate-windows-communication-foundation"></a>Para instalar o .NET e ativar o Windows Communication Foundation:  

1.  Abra **Server Manager**e navegue até **Gerenciar**. Clique em **Adicionar Funções e Recursos** para abrir o **Assistente para Adicionar Funções e Recursos.**  

2.  Examine as informações fornecidas no painel **Antes de Começar** e clique em **Avançar**.  

3.  Selecione **Instalação baseada em função ou em recurso**e clique em **Avançar**.  

4.  Selecione o servidor no **Pool de Servidores**e clique em **Avançar**.  

5.  Examine o painel **Funções de Servidor** e clique em **Avançar**.  

6.  Adicione os seguintes **Recursos** selecionando-os na lista:  

    -   **Recursos do .NET Framework 3.5**  

        -   **.NET Framework 3.5 (inclui .NET 2.0 e 3.0)**  

    -   **Recursos do .NET Framework 4.5**  

        -   **.NET Framework 4.5**  

        -   **ASP.NET 4,5**  

        -   **Serviços do WCF**  

            -   **Ativação HTTP**  

            -   **Compartilhamento de porta TCP**  

7.  Examine as telas **Função de Servidor Web (IIS)** e **Serviços de Função** e clique em **Avançar**.  

8.  Examine a tela **Confirmação** e clique em **Avançar**.  

9. Clique em **Instalar** e verifique se a instalação foi concluída corretamente no painel **Notificações** do **Gerenciador de Servidores**.  

10. Após a instalação básica do .NET, navegue até o [Centro de Download da Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=42643) para obter o instalador da Web para o .NET Framework 4.5.2. Clique no botão **Baixar** e **Execute** o instalador. Ele detectará automaticamente e instalará os componentes necessários no idioma selecionado.  

Para obter mais informações, veja os seguintes artigos para saber por que essas versões do .NET Framework são necessárias:  

-   [Versões e dependências do .NET Framework](https://technet.microsoft.com/en-us/library/bb822049.aspx)  

-   [Tutorial passo a passo da compatibilidade do aplicativo do .NET Framework 4 RTM](https://technet.microsoft.com/en-us/library/dd889541.aspx)  

-   [Como: atualizar um aplicativo Web ASP.NET para o ASP.NET 4](https://technet.microsoft.com/en-us/library/dd483478\(VS.100\).aspx)  

-   [Perguntas frequentes sobre a Política de ciclo de vida de suporte do Microsoft .NET Framework](https://support.microsoft.com/en-us/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update)  

-   [Tudo sobre o CLR – Em processo e lado a lado](https://msdn.microsoft.com/en-us/magazine/ee819091.aspx)  

**Habilitar BITS, IIS e RDC**  

O [BITS (Serviço de Transferência Inteligente em Segundo Plano)](https://technet.microsoft.com/en-us/library/dn282296.aspx) é usado para aplicativos que precisam transferir arquivos de forma assíncrona entre um cliente e um servidor. Com a medição do fluxo das transferências em primeiro e segundo planos, o BITS preserva a capacidade de resposta de outros aplicativos de rede. Ele continuará automaticamente retomando as transferências de arquivos se uma sessão de transferência for interrompida.  

Você instalará o BITS para este laboratório, pois este servidor do site também será usado como um ponto de gerenciamento.  

O IIS (Serviços de Informações da Internet) é um servidor Web flexível e escalonável que pode ser usado para hospedar qualquer coisa na Web. Ele é usado pelo Configuration Manager para diversas funções do sistema de sites. Para obter informações adicionais sobre o IIS, consulte [Sites para servidores de sistema de sites no System Center Configuration Manager](../../core/plan-design/network/websites-for-site-system-servers.md).  

[RDC (Compactação Diferencial Remota)](https://technet.microsoft.com/en-us/library/cc754372.aspx) é um conjunto de APIs que os aplicativos podem usar para determinar se quaisquer alterações foram feitas em um conjunto de arquivos. O RDC permite que o aplicativo replique somente as partes alteradas de um arquivo, reduzindo ao mínimo o tráfego de rede.  

#### <a name="to-enable-bits-iis-and-rdc-site-server-roles"></a>Para habilitar as funções do servidor do site do BITS, IIS e RDC:  

1.  No servidor do site, abra **Server Manager**. Navegue até **Gerenciar**. Clique em **Adicionar Funções e Recursos** para abrir o **Assistente para Adicionar Funções e Recursos**.  

2.  Examine as informações fornecidas no painel **Antes de Começar** e clique em **Avançar**.  

3.  Selecione **Instalação baseada em função ou em recurso**e clique em **Avançar**.  

4.  Selecione o servidor no **Pool de Servidores**e clique em **Avançar**.  

5.  Adicione as seguintes **Funções de Servidor** selecionando-as na lista:  

    -   **Web Server (IIS)**  

        -   **Recursos comuns de HTTP**  

            -   **Documento padrão**  

            -   **Pesquisa no Diretório**  

            -   **Erros HTTP**  

            -   **Conteúdo Estático**  

            -   **Redirecionamento de HTTP**  

        -   **Integridade e diagnóstico**  

            -   **Log HTTP**  

            -   **Ferramentas de log**  

            -   **Monitor de Solicitações**  

            -   **Rastreamento**  

    -   **Desempenho**  

        -   **Compactação de Conteúdo Estático**  

        -   **Compactação de conteúdo dinâmico**  

    -   **Security**  

        -   **Filtragem de Solicitações**  

        -   **Autenticação básica**  

        -   **Autenticação de mapeamento de certificado de cliente**  

        -   **Restrições de IP e domínio**  

        -   **Autorização de URL**  

        -   **Autorização do Windows**  

    -   **Desenvolvimento de aplicativos**  

        -   **Extensibilidade 3.5 do .NET**  

        -   **Extensibilidade 4.5 do .NET**  

        -   **ASP**  

        -   **ASP.NET 3.5**  

        -   **ASP.NET 4,5**  

        -   **Extensões ISAPI**  

        -   **Filtros ISAPI**  

        -   **Inclusões do lado do servidor**  

    -   **Servidor FTP**  

        -   **Serviço de FTP**  

    -   **Ferramentas de gerenciamento**  

        -   **Console de gerenciamento do IIS**  

        -   **Compatibilidade de gerenciamento do IIS 6**  

            -   **Compatibilidade de Metabase do IIS 6**  

            -   **Console de gerenciamento do IIS 6**  

            -   **Ferramentas de script do IIS 6**  

            -   **Compatibilidade de WMI do IIS 6**  

        -   **Scripts e ferramentas de gerenciamento do IIS 6**  

        -   **Management Service**  

6.  Adicione os seguintes **Recursos** selecionando-os na lista:  

    -   **BITS (Serviço de Transferência Inteligente em Segundo Plano)**  

          -   **Extensão de servidor IIS**  

    -   **Ferramentas Administrativas do Servidor Remoto**  

          -   **Ferramentas de administração do recurso**  

          -   **Ferramentas de extensões de servidor BITS**  

7.  Clique em **Instalar** e verifique se a instalação foi concluída corretamente no painel **Notificações** do **Gerenciador de Servidores**.  

Por padrão, o IIS bloqueia o acesso de diversos tipos de extensões de arquivo e locais por comunicação HTTP ou HTTPS. Para permitir que esses arquivos sejam distribuídos para sistemas cliente, você precisará configurar a filtragem de solicitação para o IIS em seu ponto de distribuição. Para obter mais informações, consulte [Filtragem de Solicitações do IIS para pontos de distribuição](../../core/plan-design/network/prepare-windows-servers.md#BKMK_IISFiltering).  

#### <a name="to-configure-iis-filtering-on-distribution-points"></a>Para configurar a filtragem do IIS nos pontos de distribuição:  

1.  Abra **IIS Manager** e selecione o nome de seu servidor na barra lateral. Isso o levará para a tela **Início** .  

2.  Verifique se a **Exibição de Recursos** está selecionada na parte inferior da tela **Início** . Navegue até **IIS** e abra **Solicitar Filtragem**.  

3.  No painel **Ações** , clique em **Permitir Extensão de Nome de Arquivo...**  

4.  Digite **.msi** na caixa de diálogo e clique em **OK**.  

##  <a name="BKMK_InstallCMLab"></a> Instalando o Configuration Manager  
Você vai [Determinar quando usar um site primário](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChoosePriimary) para gerenciar os clientes diretamente. Isso permitirá que seu ambiente de laboratório dê suporte ao gerenciamento de [Escala de sistema de sites](/sccm/core/plan-design/configs/size-and-scale-numbers) para dispositivos potenciais.  
Durante esse processo, você também instalará o console do Configuration Manager, que será usado para gerenciar a transferência dos dispositivos de avaliação.  

Antes de começar a instalação, inicie o [Verificador de Pré-requisitos](/sccm/core/servers/deploy/install/prerequisite-checker) no servidor usando o Windows Server 2012 para confirmar se todas as configurações foram habilitadas corretamente.  

#### <a name="to-download-and-install-configuration-manager"></a>Para baixar e instalar o Configuration Manager:  

1.  Navegue até a página [Avaliações do System Center](https://www.microsoft.com/evalcenter/evaluate-system-center-2012-configuration-manager-and-endpoint-protection) para baixar a versão de avaliação mais recente do System Center Configuration Manager.  

2.  Descompacte a mídia de download em seu local predefinido.  

3.  Siga o procedimento de instalação listado em [Instalar um site usando o Assistente de Instalação do System Center Configuration Manager](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites). Nesse procedimento, você digitará o seguinte:  

    |Etapa no procedimento de instalação do site|Seleção|  
    |-----------------------------------------|---------------|  
    |Etapa 4: A página da **Chave do Produto (Product Key)**|Selecione **Avaliação**.|  
    |Etapa 7:  **Downloads de pré-requisito**|Selecione **Baixar arquivos necessários** e especifique o local predefinido.|  
    |Etapa 10: **Configurações do site e da instalação**|-   **Código do site:LAB**<br />-   **Nome do site:Evaluation**<br />-   **Pasta de instalação:** especifique seu local predefinido.|  
    |Etapa 11: **Instalação do site primário**|Selecione **Instalar o site primário como um site autônomo**e clique em **Avançar**.|  
    |Etapa 12: **Instalação do banco de dados**|-   **Nome do SQL Server (FQDN):** insira seu FQDN aqui.<br />-   **Nome da instância:** deixe em branco, pois você usará a instância padrão do SQL instalada anteriormente.<br />-   **Porta do Service Broker:** deixe como a porta padrão 4022.|  
    |Etapa 13: **Instalação do banco de dados**|Mantenha essas configurações como padrão.|  
    |Etapa 14: **Provedor de SMS**|Mantenha essas configurações como padrão.|  
    |Etapa 15: **Configurações de comunicação do cliente**|Confirme se a opção **Todas as funções do sistema de sites aceitam somente a comunicação HTTPS de clientes** não está marcada|  
    |Etapa 16: **Funções do sistema de sites**|Insira o FQDN e confirme se a seleção de **Todas as funções do sistema de site aceitam apenas a comunicação HTTPS de clientes** ainda está desmarcada.|  

##  <a name="BKMK_EnablePubLab"></a> Habilitar a publicação do site do Configuration Manager  
Cada site do Configuration Manager publica suas próprias informações específicas do site no contêiner do System Management em sua partição de domínio no esquema do Active Directory. Canais bidirecionais para comunicação entre o Active Directory e o Configuration Manager devem ser abertos para manipular este tráfego. Você habilitará também a Descoberta de floresta para determinar a certos componentes de infraestrutura de rede e do Active Directory.  

#### <a name="to-configure-active-directory-forests-for-publishing"></a>Para configurar florestas do Active Directory para publicação:  

1.  No canto inferior esquerdo do console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Configuração da Hierarquia**e clique em **Métodos de Descoberta**.  

3.  Selecione **Descoberta de Florestas do Active Directory** e clique em **Propriedades**.  

4.  Na caixa de diálogo **Propriedades** , selecione **Habilitar Descoberta de Florestas do Active Directory**. Depois que isso for ativado, selecione **Criar automaticamente limites de site do Active Directory quando forem descobertos**. Será exibida uma caixa de diálogo que informa: **Deseja executar a descoberta completa assim que possível?** Clique em **Sim**.  

5.  No grupo **Método de Descoberta** na parte superior da tela, clique em **Executar Descoberta de Floresta Agora**e navegue até as **Florestas do Active Directory** na barra lateral. Sua floresta do Active Directory deve ser mostrada na lista de florestas descobertas.  

6.  Vá para a parte superior da tela, para a guia **Geral** .  

7.  No espaço de trabalho **Administração** , expanda **Configuração da Hierarquia**e clique em **Florestas do Active Directory**.  

#### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-your-active-directory-forest"></a>Para habilitar um site do Configuration Manager a publicar informações em sua floresta do Active Directory:  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  Você vai configurar uma nova floresta que ainda não foi descoberta.  

3.  No espaço de trabalho de **Administração** , clique em **Florestas do Active Directory**.  

4.  Na guia **Publicação** das propriedades do site, selecione a floresta conectada e clique em **OK** para salvar a configuração.
