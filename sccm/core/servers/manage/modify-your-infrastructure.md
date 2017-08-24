---
title: Modificar a infraestrutura | Microsoft Docs
description: "Saiba como fazer alterações ou executar ações que afetam a infraestrutura do Configuration Manager que você implantou."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
caps.latest.revision: "19"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: a5228c4984347be4b115bfa5563791fa2fb7319c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="modify-your-system-center-configuration-manager-infrastructure"></a>Modificar a infraestrutura do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Depois de instalar um ou mais sites, talvez você precise modificar configurações ou tomar medidas que afetem a infraestrutura implantada.  


##  <a name="BKMK_ManageSMSprovider"></a> Gerenciar o Provedor de SMS  
 O Provedor de SMS (um arquivo de biblioteca de vínculo dinâmico: smsprov.dll) fornece o ponto de contato administrativo para um ou mais consoles do Configuration Manager. Ao instalar vários Provedores de SMS, você pode fornecer redundância para pontos de contato para administrar o site e a hierarquia.  

 Em cada site do Configuration Manager, você pode executar novamente a Instalação para:  

-   Adicionar outra instância do Provedor de SMS (cada instância adicional do Provedor de SMS deve estar em um computador separado)  

-   Remover uma instância do Provedor de SMS (para remover o último Provedor de SMS de um site, é necessário desinstalar o site)  

 É possível monitorar a instalação ou a remoção do Provedor de SMS exibindo o **ConfigMgrSetup.log** na pasta raiz do servidor de site em que você executa a Instalação.  

 Antes de modificar o Provedor de SMS em um site, familiarize-se com as informações em [Planejar o Provedor de SMS para o System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

#### <a name="to-manage-the-sms-provider-configuration-for-a-site"></a>Para gerenciar a configuração do Provedor de SMS para um site  

1.  Execute a **Instalação do Configuration Manager** na **&lt;pasta de instalação do site do Configuration Manager\>\BIN\X64\setup.exe**.  

2.  Na página **Introdução** , selecione **Realizar a manutenção do site ou redefinir este site**e clique em **Próximo**.  

3.  Na página **Manutenção do Site** , selecione **Modificar configuração do Provedor de SMS**e clique em **Próximo**.  

4.  Na página **Gerenciar Provedores de SMS** , selecione uma das opções a seguir e conclua o assistente usando uma dessas opções:  

    -   Para adicionar um Provedor de SMS adicional nesse site:  

         Selecione **Adicionar um novo Provedor de SMS**, especifique o FQDN para um computador que irá hospedar, mas que atualmente não hospeda, um Provedor de SMS e clique em **Próximo**.  

    -   Para remover um Provedor de SMS de um servidor:  

         Selecione **Desinstalar o Provedor de SMS especificado**, selecione o nome do computador do qual deseja remover o Provedor de SMS, clique em **Próximo**e confirme a ação.  

        > [!TIP]  
        >  Para mover o Provedor de SMS entre dois computadores, é necessário instalar o Provedor de SMS no novo computador e removê-lo do local original. Não há opção dedicada para mover o Provedor de SMS entre computadores em um único processo.  

 Após a conclusão do Assistente de Instalação, a configuração do Provedor de SMS é concluída. Na guia **Geral** , na caixa de diálogo **Propriedades** do site, você pode verificar os computadores que têm um Provedor de SMS instalados para um site.  

##  <a name="bkmk_Console"></a> Gerenciar o console do Configuration Manager  
 Estas são as tarefas que você pode realizar para gerenciar o console do Configuration Manager:  

-   **Modificar o idioma exibido no console do Gerenciador de Configurações** – para modificar os idiomas instalados, consulte [Gerenciar idiomas do console do Configuration Manager](#BKMK_ManageConsoleLanguages) neste tópico.  

-   **Instalar consoles adicionais** – para instalar consoles adicionais, consulte [Instalar consoles do System Center Configuration Manager](/sccm/core/servers/deploy/install/install-consoles).  

-   **Configurar DCOM** – para configurar permissões DCOM para habilitar consoles remotos do servidor do site a se conectarem, consulte [Configurar permissões DCOM para consoles remotos do Configuration Manager](#BKMK_ConfigDCOMforRemoteConsole) neste tópico.  

-   **Modificar permissões para limitar o que os usuários administrativos podem ver no console** – para modificar permissões administrativas, que limitam o que os usuários podem ver e fazer no console, consulte [Modificar o escopo administrativo de um usuário administrativo](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_ModAdminUser).     

###  <a name="BKMK_ManageConsoleLanguages"></a> Gerenciar o idioma do console do Configuration Manager  
 Durante a instalação do servidor do site, os arquivos de instalação do console do Configuration Manager e os pacotes de idiomas com suporte do site são copiados para a subpasta **&lt;ConfigMgrInstallationPath\>\Tools\ConsoleSetup** no servidor do site.  

-   Quando você inicia a instalação do console do Configuration Manager dessa pasta no servidor do site, o console do Configuration Manager e os arquivos do pacote de idiomas com suporte são copiados para o computador  

-   Quando um pacote de idiomas está disponível para a configuração do idioma atual no computador, o console do Configuration Manager é aberto nesse idioma  

-   Se o pacote de idiomas associado não estiver disponível para o console do Configuration Manager, o console será aberto em inglês  

Por exemplo, considere um cenário em que você instala o console do Configuration Manager de um servidor do site que dá suporte a inglês, alemão e francês. Se você abrir o console do Configuration Manager em um computador cujo idioma configurado é o francês, o console será aberto em francês. Se você abrir o console do Configuration Manager em um computador cujo idioma configurado é o japonês, o console será aberto em inglês, pois o pacote do idioma japonês não está disponível.  

 Se que o console do Configuration Manager é aberto, ele determina as configurações de idioma definidas para o computador, verifica se um pacote de idiomas associado está disponível para o console do Configuration Manager e abre o console usando o pacote de idiomas apropriado. Quando desejar abrir o console do Configuration Manager em inglês independentemente das configurações de idioma definidas no computador, você precisará remover manualmente ou renomear os arquivos de pacote de idiomas no computador.  

 Use os procedimentos a seguir para iniciar o console do Configuration Manager em inglês independentemente da configuração de localidade definida no computador.  

##### <a name="to-install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>Para instalar uma versão apenas em inglês do console do Configuration Manager em computadores  

1.  No Windows Explorer, navegue até **&lt;ConfigMgrInstallationPath\>\Tools\ConsoleSetup\LanguagePack**  

2.  Renomeie os arquivos **.msp** e **.mst** . Por exemplo, você pode alterar **&lt;nome do arquivo\>.MSP** para **&lt;nome do arquivo\>.MSP.disabled**.  

3.  Instale o console do Configuration Manager no computador.  

    > [!IMPORTANT]  
    >  Quando novos idiomas do servidor forem configurados para o servidor do site, os arquivos .msp e .mst serão copiados novamente para a pasta **LanguagePack**, e você deverá repetir esse procedimento para instalar novos consoles do Configuration Manager somente em inglês.  

##### <a name="to-temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>Para desabilitar temporariamente um idioma do console em uma instalação existente do console do Configuration Manager  

1.  No computador que está executando o console do Configuration Manager, feche o console do Configuration Manager.  

2.  No Windows Explorer, navegue até &lt;*ConsoleInstallationPath*>\Bin\ no computador do console do Configuration Manager.  

3.  Renomeie a pasta do idioma apropriado para o idioma configurado no computador. Por exemplo, se as configurações de idioma do computador estiverem definidas como alemão, você poderá renomear a pasta **de** para **de.disabled**.  

4.  Para abrir o console do Configuration Manager no idioma configurado para o computador, renomeie a pasta para o nome original. Por exemplo, renomeie **de.disabled** para **de**.  

##  <a name="BKMK_ConfigDCOMforRemoteConsole"></a> Configurar permissões DCOM para consoles remotos do Configuration Manager  
 A conta de usuário que executa o console do Configuration Manager requer permissão para acessar o banco de dados do site usando o Provedor de SMS. No entanto, usuários administrativos que usam um console remoto do Configuration Manager também precisam de permissões DCOM de **Ativação Remota** em:  

-   o computador do servidor do site  

-   Cada computador que hospeda uma instância do Provedor de SMS  

 O grupo de segurança chamado **Administradores de SMS** concede acesso ao Provedor de SMS de um computador e também pode ser usado para conceder as permissões DCOM necessárias. Esse grupo é local para o computador quando o Provedor de SMS é executado em um servidor membro e é um grupo de domínio local quando o Provedor de SMS é executado em um controlador de domínio.  

> [!IMPORTANT]  
>  O console do Configuration Manager usa a WMI (Instrumentação de Gerenciamento do Windows) para se conectar ao Provedor de SMS, e a WMI usa o DCOM internamente. Portanto, o Configuration Manager vai requerer permissões para ativar um servidor DCOM no computador do Provedor de SMS se o console do Configuration Manager estiver sendo executado em um computador que não seja o do Provedor de SMS. Por padrão, a Ativação Remota é concedida somente aos membros do grupo Administradores internos. Se você permitir que o grupo Administradores de SMS tenha permissão de Ativação Remota, um membro desse grupo poderá tentar ataques DCOM contra o computador do Provedor de SMS. Essa configuração também aumenta a superfície sujeita a ataques do computador. Para atenuar essa ameaça, monitore atentamente os membros do grupo Administradores de SMS.  

 Use o procedimento a seguir para configurar cada site de administração central, servidor de site primário e cada computador em que o Provedor de SMS está instalado para conceder acesso remoto do console do Configuration Manager a usuários administrativos.  

#### <a name="to-configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>Para configurar permissões DCOM para conexões remotas do console do Gerenciador de Configurações  

1.  Abra  os  **Serviços de Componentes** executando **Dcomcnfg.exe**.  

2.  Em **Serviços de Componentes**, clique em **Raiz do console** >  **Serviços de Componentes** > **Computadores**e clique em **Meu Computador**. No menu **Ação** , clique em **Propriedades**.  

3.  Na caixa de diálogo **Propriedades do Meu Computador** , na guia **Segurança COM** , seção **Permissões de Inicialização e Ativação** , clique em **Editar Limites**.  

4.  Na caixa de diálogo **Permissões de Inicialização e Ativação** , clique em **Adicionar**.  

5.  Na caixa de diálogo **Selecionar Usuário, Computadores, Contas de Serviço ou Grupos** , na caixa **Digite os nomes de objetos a serem selecionados (exemplos)** , digite **SMS Admins**e clique em **OK**.  

    > [!NOTE]  
    >  Talvez seja necessário alterar a configuração de **Deste Local** para localizar o grupo Administradores de SMS. Esse grupo é local para o computador quando o Provedor de SMS é executado em um servidor membro e é um grupo de domínio local quando o Provedor de SMS é executado em um controlador de domínio.  

6.  Na seção **Permissões para Administradores de SMS** , para permitir a ativação remota, marque a caixa de seleção **Ativação Remota** .  

7.  Clique em **OK** , clique em **OK** novamente e feche **Gerenciamento de Computador**. Agora, seu computador está configurado para permitir o acesso remoto do console do Configuration Manager a membros do grupo de Administradores de SMS.  

 Repita esse procedimento em cada computador do Provedor de SMS que der suporte a consoles remotos do Configuration Manager.  

##  <a name="bkmk_dbconfig"></a> Modificar a configuração do banco de dados do site  
 Depois de instalar um site, você pode modificar a configuração do banco de dados e o servidor do banco de dados do site executando a Instalação em um servidor de site de administração central ou no servidor do site primário. Você poderá mover o banco de dados do site para uma nova instância do SQL Server no mesmo computador ou para um computador diferente que execute uma versão do SQL Server com suporte. Não há suporte para essas alterações e outras relacionadas em relação à configuração do banco de dados em sites secundários.  

 Para obter mais informações sobre os limites de suporte, veja [Política de suporte para alterações manuais do banco de dados em um ambiente do Configuration Manager](https://support.microsoft.com/kb/3106512).  

> [!NOTE]  
>  Quando você modifica a configuração do banco de dados de um site, o Configuration Manager reinicia ou reinstala serviços do Configuration Manager no servidor do site e em servidores do sistema de sites remotos que se comunicam com o banco de dados.  

**Para modificar a configuração do banco de dados**, é necessário executar a Instalação no servidor do site e selecionar a opção **Realizar a manutenção do site ou redefinir este site**. Em seguida, selecione a opção **Modificar configuração do SQL Server** . Você pode alterar as seguintes configurações do banco de dados do site:  

-   O servidor baseado no Windows que hospeda o banco de dados.  

-   A instância do SQL Server em uso em um servidor que hospeda o banco de dados do SQL Server.  

-   Nome do banco de dados.  

-   Porta do SQL Server em uso pelo Configuration Manager  

-   Porta do Service Broker do SQL Server em uso pelo Configuration Manager  

**Ao mover o banco de dados do site, você deverá configurar o seguinte:**  

-   **Configurar o acesso:** ao mover o banco de dados do site para um novo computador, adicione a conta de computador do servidor do site ao grupo **Local de Administradores** no computador que executa o SQL Server. Se usar um cluster do SQL Server para o banco de dados do site, você deverá adicionar a conta de computador ao grupo **Local de administradores** de cada computador do nó de cluster do Windows Server.  

-   **Habilitar a integração CLR (Common Language Runtime):**  quando você move o banco de dados para uma nova instância do SQL Server, ou para um novo computador SQL Server, é necessário habilitar a integração CLR (Common Language Runtime). Para habilitar o CLR, use o **SQL Server Management Studio** para se conectar à instância do SQL Server que hospeda o banco de dados do site e execute o seguinte procedimento armazenado como uma consulta: **sp_configure ‘clr enabled’,1; reconfigure**.  
-  **Verificar se o novo SQL Server tem acesso ao local de backup:** ao usar um UNC para armazenar o backup do banco de dados do site, depois de mover o banco de dados para um novo servidor, incluindo uma movimentação para um Grupo de Disponibilidade AlwaysOn do SQL Server ou um cluster do SQL Server, garanta que a conta de computador do novo SQL Server tem permissões de **gravação** no local do UNC.  


> [!IMPORTANT]  
>  Antes de mover um banco de dados que possui uma ou mais réplicas de banco de dados para pontos de gerenciamento, primeiro remova as réplicas do banco de dados. Depois de concluir a movimentação do banco de dados, você poderá reconfigurar suas réplicas. Para obter mais informações, consulte [Database replicas for management points for System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

##  <a name="bkmk_SPN"></a> Gerenciar o SPN para o servidor de banco de dados do site  
Você pode escolher a conta que executa os serviços do SQL para o banco de dados do site:  

-   Quando os serviços são executados com a conta de sistema de computadores, o SPN é registrado automaticamente para você.  

-   Quando os serviços são executados com uma conta de usuário local do domínio, é necessário registrar manualmente o SPN para garantir que os clientes SQL e outros sistemas de sites podem realizar a autenticação Kerberos. Sem a autenticação Kerberos, a comunicação com o banco de dados poderá falhar.  

A documentação do SQL Server pode ajudar você a [registrar manualmente o SPN](https://technet.microsoft.com/library/ms191153\(v=sql.120\).aspx)e fornecer informações adicionais sobre conexões SPNs e Kerberos.  

> [!IMPORTANT]  
>  -   Ao criar um SPN para um SQL Server clusterizado, você deverá especificar o nome virtual do cluster do SQL Server como o nome do computador do SQL Server.  
> -   O comando usado para registrar um SPN para uma instância nomeada do SQL Server é o mesmo usado para registrar um SPN para uma instância padrão, com exceção de que o número da porta deve coincidir com a porta usada pela instância nomeada.  

Você pode registrar um SPN para a conta de serviço do SQL Server do servidor de banco de dados do site usando a ferramenta **Setspn** . É necessário executar a ferramenta Setspn em um computador que reside no domínio do SQL Server, que deverá usar as credenciais de administrador de domínio para a execução.  

 Use os procedimentos a seguir como exemplos de como gerenciar o SPN para a conta de serviço do SQL Server que usa a ferramenta Setspn no Windows Server 2008 R2. Para obter orientações específicas sobre o Setspn, consulte [Setspn Overview (Visão geral do Setspn)](http://go.microsoft.com/fwlink/p/?LinkId=226343), ou documentação semelhante específica para o seu sistema operacional.  

> [!NOTE]  
>  Os procedimentos a seguir fazem referência à ferramenta de linha de comando Setspn. A ferramenta de linha de comando Setspn está incluída quando você instala as ferramentas de suporte do Windows Server 2003 do CD do produto ou do [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=100114). Para obter mais informações sobre como instalar as ferramentas de suporte do Windows do CD do produto, consulte [Instalar Ferramentas de Suporte do Windows](http://go.microsoft.com/fwlink/p/?LinkId=62270).  

#### <a name="to-manually-create-a-domain-user-service-principal-name-spn-for-the-sql-server-service-account"></a>Para criar manualmente um SPN de usuário de domínio para a conta de serviço do SQL Server  

1.  No menu **Iniciar** , clique em **Executar**e insira **cmd** na caixa de diálogo Executar.  

2.  Na linha de comando, navegue até o diretório de instalação das ferramentas de suporte do Windows Server. Por padrão, essas ferramentas estão localizadas no diretório **C:\Arquivos de Programas\Ferramentas de Suporte** .  

3.  Insira um comando válido para criar o SPN. Para criar o SPN, você pode usar o nome NetBIOS ou o FQDN (nome de domínio totalmente qualificado) do computador que executa o SQL Server. No entanto, é necessário criar um SPN para o nome NetBIOS e para o FQDN.  

    > [!IMPORTANT]  
    >  Ao criar um SPN para um SQL Server clusterizado, você deverá especificar o nome virtual do cluster do SQL Server como o nome do computador do SQL Server.  

    -   Para criar um SPN para o nome NetBIOS do computador do SQL Server, digite o seguinte comando: **setspn -A MSSQLSvc/&lt;nome do computador do SQL Server\>:1433 &lt;Domínio\Conta>**  

    -   Para criar um SPN para o FQDN do computador do SQL Server, digite o seguinte comando: **setspn -A MSSQLSvc/&lt;FQDN do SQL Server\>:1433 &lt;Domínio\Conta>**  

    > [!NOTE]  
    >  O comando usado para registrar um SPN para uma instância nomeada do SQL Server é o mesmo usado para registrar um SPN para uma instância padrão, com exceção de que o número da porta deve coincidir com a porta usada pela instância nomeada.  

#### <a name="to-verify-the-domain-user-spn-is-registered-correctly-by-using-the-setspn-command"></a>Para verificar se o usuário de domínio SPN está registrado corretamente usando o comando Setspn  

1.  No menu **Iniciar** , clique em **Executar**e insira **cmd** na caixa de diálogo **Executar** .  

2.  No prompt de comando, digite o seguinte comando: **setspn -L &lt;domínio\Conta de Serviço do SQL>**.  

3.  Verifique o **ServicePrincipalName** registrado para garantir que tenha sido criado um SPN válido para o SQL Server.  

#### <a name="to-verify-the-domain-user-spn-is-registered-correctly-when-using-the-adsiedit-mmc-console"></a>Para verificar se o usuário de domínio SPN está registrado corretamente ao usar o console do ADSIEdit MMC  

1.  No menu **Iniciar** , clique em **Executar**e insira **adsiedit.msc** para iniciar o console do ADSIEdit MMC.  

2.  Se necessário, conecte-se ao domínio do servidor do site.  

3.  No painel do console, expanda o domínio do servidor do site, expanda **DC=&lt;nome diferenciado do servidor\>**, expanda **CN=Users**, clique com o botão direito do mouse em **CN=&lt;Usuário da Conta de Serviço\>** e clique em **Propriedades**.  

4.  Na caixa de diálogo **CN=&lt;Usuário da Conta de Serviço\> Propriedades**, examine o valor de **servicePrincipalName** para garantir que um SPN válido tenha sido criado e associado ao computador correto do SQL Server.  

#### <a name="to-change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>Para alterar a conta de serviço do SQL Server do sistema local para uma conta de usuário de domínio  

1.  Crie ou selecione uma conta de usuário de domínio ou do sistema local que você deseja usar como a conta de serviço do SQL Server.  

2.  Abra o **SQL Server Configuration Manager**.  

3.  Clique em **Serviços do SQL Server** e clique duas vezes em **SQL Server&lt;NOME DA INSTÂNCIA\>**.  

4.  Na guia **Logon** , selecione **Esta conta**e insira o nome de usuário e a senha para a conta de usuário do domínio criado na etapa 1, ou clique em **Procurar** para localizar a conta de usuário nos Serviços de Domínio Active Directory, e clique em **Aplicar**.  

5.  Clique em **Sim** na caixa de diálogo **Confirmar Alteração de Conta** para confirmar a alteração da conta de serviço e reiniciar o serviço SQL Server.  

6.  Clique em **OK** depois de alterada com êxito a conta de serviço.  

##  <a name="bkmk_reset"></a> Executar uma redefinição de site  
 Quando uma redefinição de site é executada em um site de administração central ou site primário, o site:  

-   Reaplica as permissões de registro e arquivo do Configuration Manager padrão  

-   Reinstala todos os componentes do site e todas as funções do sistema de sites no site  

Sites secundários não oferecem suporte a redefinições de site.  

Redefinições de site podem ser executadas manualmente, quando você opta por realizá-las, mas também pode ser executadas automaticamente após você modificar a configuração do site.  

Por exemplo, se tiver ocorrido uma alteração nas contas usadas por componentes do Configuration Manager, considere uma redefinição de site manual para garantir que os componentes do site sejam atualizados para usar os detalhes da nova conta. No entanto, se você modificar os idiomas do cliente ou do servidor de um site, o Configuration Manager executará automaticamente uma redefinição de site, pois ela é necessária para que o site possa usar essa alteração.  

> [!NOTE]  
>  Redefinições de site não redefinem permissões de acesso para objetos que não são do Configuration Manager.  

Quando é executada uma redefinição de site:  

1.  A instalação para e reinicia os componentes de serviço e thread do **SMS_SITE_COMPONENT_MANAGER** do serviço **SMS_EXECUTIVE** .  

2.  A instalação remove e depois recria a pasta de compartilhamento do sistema de sites e o componente **SMS Executive** no computador local e em computadores remotos do sistema de site.  

3.  A instalação reinicia o serviço **SMS_SITE_COMPONENT_MANAGER** , esse serviço instala o **SMS_EXECUTIVE** e os serviços do **SMS_SQL_MONITOR** .  

Além disso, redefinições de site restauram os seguintes objetos:  

-   As chaves de Registro do **SMS** ou **NAL** , e todas as subchaves padrão nestas chaves.  

-   A árvore de diretório de arquivos do Configuration Manager e arquivos padrão ou subdiretórios nessa árvore.  

**Pré-requisitos para executar uma redefinição de site**  

A conta que você usa para executar uma redefinição de site deve ter as seguintes permissões:  

-   A conta que você usa para executar uma redefinição de site deve ter as seguintes permissões:  

    -   **Site de administração central**: a conta que você usa para executar uma redefinição desse site deve ser de administrador local no servidor do site de administração central e deve ter privilégios equivalentes à função de segurança de administração baseada em função de **Administrador Completo** .  

    -   **Site primário**: a conta que você usa para executar uma redefinição desse site deve ser de administrador local no servidor do site primário e deve ter privilégios equivalentes à função de segurança de administração baseada em função de **Administrador Completo** . Se o site primário estiver em uma hierarquia com um site de administração central, essa conta também deverá ser de administrador local no servidor do site de administração central.  

**Limitações de uma redefinição de site**
  - A partir da versão 1602, você não pode usar uma redefinição de site para alterar os pacotes de idiomas do Cliente ou do Servidor instalados nos sites enquanto a hierarquia estiver configurada para dar suporte para [testar atualizações do cliente em uma coleção de pré-produção](/sccm/core/clients/manage/upgrade/test-client-upgrades).

#### <a name="to-perform-a-site-reset"></a>Para executar uma redefinição de site  

1.  Execute a **Instalação do Configuration Manager** na **&lt;pasta de instalação do site do Configuration Manager\>\BIN\X64\setup.exe**.  

    > [!TIP]  
    >  Você também pode executar uma redefinição de site iniciando a Instalação do Configuration Manager no menu **Iniciar** do computador do servidor de sites ou da mídia de origem do Configuration Manager.  

2.  Na página **Introdução** , selecione **Realizar a manutenção do site ou redefinir este site**e clique em **Próximo**.  

3.  Na página **Manutenção do Site** , selecione **Redefinir o site sem alterações na configuração**e clique em **Próximo**.  

4.  Clique em **Sim** para iniciar a redefinição de site.  

Terminada a redefinição de site, clique em **Fechar** para concluir o procedimento.  

##  <a name="bkmk_sitelang"></a> Gerenciar pacotes de idiomas em um site  
Depois de instalar um site, você pode alterar os pacotes de idiomas de cliente e servidor que estão em uso:  

**Pacotes de idiomas do servidor:**  

-   **Aplica-se a:**  

     Instalações do console do Configuration Manager  

     Novas instalações de funções de sistema de sites aplicáveis  

-   **Detalhes:**  

     Após atualizar os pacotes de idiomas de servidor em um site, você pode adicionar suporte aos pacotes de idiomas nos consoles do Configuration Manager.  

     Para adicionar suporte a um pacote de idioma de servidor em um console do Configuration Manager, instale o console do Configuration Manager por meio da pasta **ConsoleSetup** em um servidor de site que inclui o pacote de idioma que você deseja usar. Se o console do Configuration Manager já estiver instalado, desinstale-o primeiro para que a nova instalação possa identificar a lista atual de pacotes de idiomas com suporte.  

**Pacotes de idiomas do cliente:**  

-   **Aplica-se a:**  

     Alterações nos pacotes de idiomas de cliente atualizam os arquivos de origem da instalação do cliente, de modo que novas atualizações e instalações do cliente acrescentam suporte à lista atualizada de idiomas do cliente.  

-   **Detalhes:**  

     Após atualizar os pacotes de idiomas de cliente em um site, instale cada cliente que usará os pacotes utilizando os arquivos de origem que incluem os pacotes de idiomas de cliente.  

Para obter informações sobre os idiomas de cliente e servidor que têm suporte do Configuration Manager, consulte [Pacotes de idiomas no System Center Configuration Manager](../../../core/servers/deploy/install/language-packs.md)  

#### <a name="to-modify-the-language-packs-that-are-supported-at-a-site"></a>Para modificar os pacotes de idiomas com suporte em um site  

1.  No servidor do site, execute a Instalação do Configuration Manager da **&lt;Pasta de instalação do site do Configuration Manager\>\BIN\X64\setup.exe.**  

2.  Na página **Introdução** , selecione **Realizar a manutenção do site ou redefinir este site**e clique em **Próximo**.  

3.  Na página **Manutenção do Site** , selecione **Modificar configuração de idioma**e clique em **Próximo**.  

4.  Na página **Downloads de Pré-requisitos** , selecione **Baixar arquivos necessários** , para adquirir atualizações de pacotes de idiomas, ou selecione **Usar arquivos baixados anteriormente** para usar arquivos baixados anteriormente que incluem os pacotes de idiomas que você deseja adicionar ao site. Clique em **Próximo** para validar os arquivos e continuar.  

5.  Na página **Seleção do Idioma do Servidor** , marque a caixa de seleção para os idiomas de servidor aos quais esse site oferece suporte e clique em **Avançar**.  

6.  Na página **Seleção do Idioma do Cliente** , marque a caixa de seleção para os idiomas de cliente aos quais esse site oferece suporte e clique em **Avançar**.  

7.  Clique em **Próximo**, para modificar o suporte a idiomas no site.  

    > [!NOTE]  
    >  O Configuration Manager inicia uma redefinição de site que também reinstala todas as funções do sistema de sites no site.  

8.  Clique em **Fechar** para concluir esse procedimento.  

##  <a name="BKMK_ModDBAlert"></a> Modificar o limite de alerta do servidor de banco de dados  
 Por padrão, o Configuration Manager gera alertas quando há pouco espaço livre em disco em um servidor de banco de dados do site. Os padrões são definidos para gerar um alerta quando houver 10 GB ou menos de espaço livre em disco, e um alerta crítico quando houver 5 GB ou menos de espaço livre em disco. Você pode modificar esses valores ou desabilitar os alertas para cada site.  

 Para alterar essas configurações:  

1.  No espaço de trabalho **Administração** , expanda **Configuração do Site**e clique em **Sites**.  

2.  Selecione o site que você deseja configurar e abra as **Propriedades** do site.  

3.  Na caixa de diálogo **Propriedades** do site, selecione a guia **Alerta** e edite as configurações.  

4.  Clique em **OK** para fechar a caixa de diálogo de propriedades do site.  
