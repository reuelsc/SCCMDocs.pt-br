---
title: "Visualização Técnica 1705 | Microsoft Docs"
description: "Saiba mais sobre os recursos disponíveis na Visualização Técnica versão 1705 do System Center Configuration Manager."
ms.custom: na
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 00684289-d21a-45f8-b1e3-c5c787d73096
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: f4c46bfab9b40b29654f4e883817a5508ab25b74
ms.openlocfilehash: 1a38d25fbc26bd1f45c6fa2a0e931536af2d8b2f
ms.contentlocale: pt-br
ms.lasthandoff: 06/28/2017

---
# <a name="capabilities-in-technical-preview-1705-for-system-center-configuration-manager"></a>Funcionalidades na Visualização Técnica 1705 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis na Visualização Técnica do System Center Configuration Manager, versão 1705. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview. Antes de instalar esta versão da visualização técnica, veja [Visualização Técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de uma visualização técnica, como atualizar entre versões e como fornecer comentários sobre os recursos em uma visualização técnica.    

**Problemas conhecidos nesse Technical Preview:**
-   **O conector do Operations Manager Suite não é atualizado**. Quando você atualiza de uma versão anterior da Visualização Técnica que tinha o conector do OMS configurado, esse conector não é atualizado e não está mais disponível no console. Após a atualização, você deve [usar o Assistente dos Serviços do Azure](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) e restabelecer a conexão com seu espaço de trabalho do OMS.
-   **Os drivers do Surface não são sincronizados com êxito**. Embora o suporte para drivers do Surface estejam listados em **Novidades** no console do Configuration Manager para a visualização técnica, esse recurso ainda não funciona conforme o esperado.
-   **Não foi possível criar políticas de adiamento do Windows Update for Business**. Embora a capacidade de configurar as políticas de adiamento do Windows Update for Business esteja listada em **Novidades** no console do Configuration Manager para a visualização técnica, o assistente não abre e não é possível configurar as políticas.


<!--  Known Issues Template
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="update-reset-tool"></a>Ferramenta de redefinição de atualização  
Você pode usar a Ferramenta de Redefinição de Atualização do Configuration Manager, **CMUpdateReset.exe**, para corrigir problemas quando as atualizações no console tiverem problemas ao baixar ou replicar. Essa ferramenta está incluída na versão 1705 da Visualização Técnica. Você pode localizá-lo no servidor do seu site da visualização técnica depois de instalar a visualização na pasta ***\cd.latest\SMSSETUP\TOOLS***.

Você pode usar essa ferramenta com as versões 1606 ou posteriores da Visualização Técnica. Esse suporte a versões anteriores é fornecido para que a ferramenta possa ser usada com vários cenários de atualização da visualização técnica e sem ter de esperar até a próxima visualização técnica ficar disponível.

Você pode usar essa ferramenta quando uma atualização no console ainda não estiver instalada e estiver em um estado de falha. Um estado de falha pode significar que o download da atualização permanece em andamento, mas está preso e demora muito tempo, talvez horas além de suas expectativas históricas para pacotes de atualização de tamanho semelhante. Também pode ter havido uma falha ao replicar a atualização para os sites primários filhos.  

Quando você executa a ferramenta, ela é executada em relação à atualização que você especificar. Por padrão, a ferramenta não exclui com sucesso atualizações baixadas ou instaladas.  

### <a name="prerequisites"></a>Pré-requisitos
A conta usada para executar a ferramenta requer as seguintes permissões:
-   Permissões de **leitura** e **gravação** para o banco de dados do site de administração central e cada site primário em sua hierarquia. Para definir essas permissões, você poderá adicionar a conta de usuário como membro das [funções de banco de dados fixas](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) **db_datawriter** e **db_datareader** no banco de dados do Configuration Manager de cada site. A ferramenta não consegue interagir com os sites secundários.
-   **Administrador local** no site de nível superior da sua hierarquia.
-   **Administrador local** no computador que hospeda o ponto de conexão de serviço.

Você precisará da interface gráfica do usuário do pacote de atualização que você deseja redefinir. Para obter a interface gráfica do usuário:
-   No console, acesse **Administração** > **Atualizações e Manutenção** e, em seguida, no painel de exibição, clique com o botão direito no título de uma das colunas (como **Estado**), em seguida, selecione **Interface gráfica do usuário do Pacote**. Isso adiciona essa coluna à exibição e a coluna mostra a interface gráfica do usuário do pacote de atualização.

> [!TIP]  
> Para copiar a interface gráfica do usuário, selecione a linha para o pacote de atualização que deseja redefinir e, em seguida, use CTRL+C para copiar essa linha. Se você colar a seleção copiada em um editor de texto, poderá copiar somente a interface gráfica do usuário para usar como um parâmetro de linha de comando quando você executar a ferramenta.

### <a name="run-the-tool"></a>Executar a ferramenta    
A ferramenta deve ser executada no site de nível superior da hierarquia.

Quando você executa a ferramenta, usa parâmetros de linha de comando para especificar o SQL Server no site de nível superior da hierarquia, o nome do banco de dados do site e a interface gráfica do usuário do pacote de atualização que você deseja redefinir. A ferramenta em seguida identifica os servidores adicionais necessários para acessar, com base no status das atualizações.   

Se o pacote de atualização estiver em um estado de *pós-download*, a ferramenta não limpará o pacote. Como opção, você pode forçar a remoção de uma atualização que baixou com êxito usando o parâmetro force delete (confira os parâmetros de linha de comando posteriormente neste tópico).

Depois que a ferramenta é executada:
-   Se um pacote foi excluído, reinicie o serviço SMS_Executive de sites de nível superior e, em seguida, verifique se há atualizações para baixar o pacote novamente.
-   Se um pacote não tiver sido excluído, você não precisará realizar nenhuma ação, porque a atualização será reinicializada e reiniciará a instalação ou replicação.

**Parâmetros da linha de comando:**  

| Parâmetro        |Descrição                 |  
|------------------|----------------------------|  
|**-S &lt;Nome de domínio totalmente qualificado do SQL Server do seu site de nível superior>** | *Necessária* <br> Você deve especificar o nome de domínio totalmente qualificado do SQL Server que hospeda o banco de dados do site para o site de nível superior da sua hierarquia.    |  
| **-D &lt;Nome do banco de dados>**                        | *Necessária* <br> Você deve especificar o nome do banco de dados de sites de nível superior.  |  
| **-P &lt;Interface gráfica do usuário do pacote>**                         | *Necessária* <br> Você deve especificar a interface gráfica do usuário para o pacote de atualização que você deseja redefinir.   |  
| **-I &lt;Nome da instância do SQL Server>**             | *Opcional* <br> Use isso para identificar a instância do SQL Server que hospeda o banco de dados do site. |
| **-FDELETE**                              | *Opcional* <br> Use isto para forçar a exclusão de um pacote de atualização baixado com êxito. |  
 **Exemplos:**  
 Em um cenário típico, você deve redefinir uma atualização que apresenta problemas de download. O nome de domínio totalmente qualificado do seu SQL Server é *server1.fabrikam.com*, o banco de site é *CM_XYZ* e a interface gráfica do usuário do pacote é *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Execute: ***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

 Em um cenário mais complexo, você deve forçar a exclusão do pacote de atualização problemático. O nome de domínio totalmente qualificado do seu SQL Server é *server1.fabrikam.com*, o banco de site é *CM_XYZ* e a interface gráfica do usuário do pacote é *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Execute: ***CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

### <a name="test-the-tool-with-the-technical-preview"></a>Teste a ferramenta com a Visualização Técnica  
Você pode usar essa ferramenta com as versões 1606 ou posteriores da Visualização Técnica. Esse suporte a versões anteriores é fornecido para que a ferramenta possa ser usada com um número maior de cenários de atualização da visualização técnica, sem ter de esperar até a próxima versão de visualização técnica estar disponível.

Execute a ferramenta em um pacote de atualização para uma versão de visualização técnica anterior a essa atualização concluir sua verificação de pré-requisitos. Um estado de verificação de pré-requisitos concluído é identificado por um dos seguintes status para o pacote em **Administração** > **Atualizações e Manutenção**:  
-   **Verificação de pré-requisitos aprovada**
-   **Verificação de pré-requisitos aprovada com aviso**
-   **Verificação de pré-requisitos reprovada**


## <a name="high-dpi-console-support"></a>Suporte de console com alto DPI

Com esta versão, devem ser corrigidos os problemas com o modo como o console do Configuration Manager pode ser expandido e exibe diferentes partes da interface do usuário quando é exibido em dispositivos de DPI alto (como um livro do Surface).


## <a name="peer-cache-improvements"></a>Aprimoramentos de cache de pares
A partir dessa visualização técnica, o cache par [não usa mais a conta de acesso de rede](/sccm/core/plan-design/hierarchy/client-peer-cache) para autenticar solicitações de download dos pares.


## <a name="improvements-for-sql-server-always-on-availability-groups"></a>Aprimoramentos para Grupos de Disponibilidade AlwaysOn do SQL Server  
Com esta versão, agora você pode usar réplicas de confirmação assíncrona nos grupos de disponibilidade AlwaysOn do SQL Server usados com o Configuration Manager.  Isso significa que você pode adicionar mais réplicas a seus grupos de disponibilidade para usar como backups fora do local (remotos) e, em seguida, usá-los em um cenário de recuperação de desastres.  

-   O Configuration Manager dá suporte ao uso de réplica de confirmação assíncrona para recuperar sua réplica síncrona.  Confira [Opções de recuperação do banco de dados do site](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) no tópico Backup e recuperação para obter informações sobre como fazer isso.

-   Esta versão não dá suporte a failover para usar a réplica de confirmação assíncrona como seu banco de dados do site.
> [!CAUTION]  
> Como o Configuration Manager não valida o estado da réplica de confirmação assíncrona para confirmar que é atual, e [por design essa réplica pode estar fora de sincronia](https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes), o uso de uma réplica de confirmação assíncrona como o banco de dados do site pode colocar em risco a integridade do site e dos dados.  

-   Você pode usar o mesmo número e tipo de réplicas em um grupo de disponibilidade como compatível com a versão do SQL Server que você usa.   (O suporte anterior foi limitado a duas réplicas de confirmação síncronas).

### <a name="configure-an-asynchronous-commit-replica"></a>Configurar uma réplica de confirmação assíncrona
Para adicionar uma réplica assíncrona a um [grupo de disponibilidade que você usa com o Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database), você não precisa executar os scripts de configuração necessários para configurar uma réplica síncrona. (Isso ocorre porque não há suporte para usar essa réplica assíncrona como o banco de dados do site). Veja [a documentação do SQL Server](https://msdn.microsoft.com/library/hh213247(v=sql.120).aspx(d=robot)) para obter informações sobre como adicionar réplicas secundárias a grupos de disponibilidade.

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Usar a réplica assíncrona para recuperar o site
Antes de usar uma réplica assíncrona para recuperar o banco de dados do site, você deverá parar o site primário ativo para impedir gravações adicionais no banco de dados do site. Depois de parar o site, você poderá usar uma réplica assíncrona em vez de usar um [banco de dados recuperado manualmente](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption).

Para parar o site, você poderá usar a [ferramenta de manutenção de hierarquia](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe) para interromper os principais serviços no servidor do site. Use a linha de comando: **Preinst.exe /stopsite**   

Parar o site é equivalente a interromper o serviço do Gerenciador de Componentes de Site (sitecomp) seguido pelo serviço SMS_Executive, no servidor do site.

> [!TIP]  
> Se você usar uma réplica primária passiva (introduzida nesta Visualização Técnica como [Alta disponibilidade da função de servidor do site](#site-server-role-high-availability)), não precisará interromper a réplica passiva. Somente o site primário ativo deve ser interrompido.



## <a name="improved-user-notifications-for-office-365-updates"></a>Notificações de usuário aprimoradas para atualizações do Office 365
Melhorias foram feitas para aproveitar a experiência de usuário do Office com Clique para Executar quando um cliente instala uma atualização do Office 365. Isso inclui notificações pop-up e no aplicativo, e uma experiência de contagem regressiva. Antes desta versão, quando uma atualização do Office 365 era enviada para um cliente, os aplicativos do Office que estavam abertos eram fechados automaticamente sem aviso. Após essa atualização, os aplicativos do Office não serão mais fechados inesperadamente.

### <a name="prerequisites"></a>Pré-requisitos
Esta atualização aplica-se a clientes do Office 365 ProPlus.

### <a name="known-issues"></a>Problemas conhecidos
Quando um cliente avalia uma atribuição de atualização do Office 365 pela primeira vez e a atualização tem um prazo agendado no passado, agendado imediatamente ou programado dentro de 30 minutos, a experiência de usuário do Office 365 pode ser divergente. Por exemplo, o cliente pode receber uma caixa de diálogo de contagem regressiva de 30 minutos para a atualização, mas a imposição real poderia iniciar antes do final da contagem regressiva. Para evitar esse comportamento, considere o seguinte:
- Implante a atualização do Office 365 com um prazo final agendado para mais de 60 minutos depois da hora atual.
- Configure uma janela de manutenção durante o horário não comercial na coleção ou configure um período de cortesia de imposição na implantação.

### <a name="try-it-out"></a>Experimente!
Tente concluir as tarefas a seguir e, depois, envie-nos **Comentários** usando a guia **Início** da Faixa de Opções para nos contar foi:
- Implante em um cliente uma atualização do Office 365 com um prazo final definido para um horário de pelo menos 60 minutos depois da hora atual. Observe o novo comportamento no cliente.


## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Configurar e implantar políticas de Proteção de Aplicativos do Windows Defender

O [Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) é um novo recurso do Windows que ajuda a proteger os usuários através da abertura de sites não confiáveis em um contêiner isolado seguro que não esteja acessível por outras partes do sistema operacional. Nesse visualização técnica, adicionamos suporte para configurar esse recurso usando as configurações de conformidade do Configuration Manager que você configura e, em seguida, implanta em uma coleção.
Este recurso será lançado na versão prévia para a versão de 64 bits da atualização do criador do Windows 10 (codinome: RS2). Para testar esse recurso agora, você deverá estar usando uma versão prévia desta atualização.


### <a name="before-you-start"></a>Antes de começar

Para criar e implantar as políticas do Windows Defender Application Guard, os dispositivos do Windows 10 nos quais você implantará a política deverão ser configurados com uma política de isolamento de rede. Para obter mais detalhes, veja a postagem no blog mencionado posteriormente.
Esse recurso só funciona com versões atuais do Windows 10 Insider. Para testá-lo, os clientes deverão estar executando uma versão recente do Windows 10 Insider.

### <a name="try-it-out"></a>Experimente!

Verifique se você leu a postagem no blog para entender as noções básicas sobre o Windows Defender Application Guard.

Para criar uma política e procurar as configurações disponíveis:

1.  No console do Configuration Manager, escolha **Ativos e Conformidade**.
2.  No espaço de trabalho **Ativos e Conformidade**, escolha **Visão Geral** > **Endpoint Protection** > **Windows Defender Application Guard**.
3.  Na guia **Início**, no grupo **Criar**, clique em **Criar Política do Windows Defender Application Guard**.
4.  Usando a postagem no blog como referência, você pode procurar e definir as configurações disponíveis para experimentar o recurso.
5.  Quando tiver terminado, conclua o assistente e implante a política para um ou mais dispositivos Windows 10.

### <a name="further-reading"></a>Leitura adicional

Para saber mais sobre o Windows Defender Application Guard, veja [esta postagem no blog]( https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97).
Além disso, para saber mais sobre o modo autônomo do Windows Defender Application Guard, veja [esta postagem no blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).




## <a name="new-capabilities-for-azure-ad-and-cloud-management"></a>Novos recursos do Azure AD e gerenciamento de nuvem

Nesta versão, você pode configurar os serviços de nuvem para usar o Azure AD para dar suporte ao cenário a seguir:

- Instalar manualmente o cliente do Configuration Manager pela Internet e que ele seja atribuído a um site do Configuration Manager.
- Usar o Intune para implantar o cliente do Configuration Manager em dispositivos na Internet.

### <a name="advantages"></a>Vantagens

Usar os serviços de nuvem e o Azure AD elimina a necessidade de usar certificados de autenticação de cliente.

Você pode descobrir os usuários do Azure AD em seu site para usar nas coleções e outras operações do Configuration Manager.

### <a name="before-you-start"></a>Antes de começar

- Você deve ter um locatário do Azure AD.
- Seus dispositivos devem executar o Windows 10 e ser unidos ao Azure AD.  Os clientes também podem ser ingressados ao domínio além de ingressados ao Azure AD).
- Além de [pré-requisitos existentes](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) para a função do sistema de site do ponto de gerenciamento, você deverá garantir que o **ASP.NET 4.5** (e as outras opções que estiverem automaticamente selecionadas com esse) esteja habilitado no computador que hospeda esta função do sistema de site.
- Para usar o Microsoft Intune para implantar o cliente do Configuration Manager:
    - Você deve ter um locatário do Intune em funcionamento (o Configuration Manager e o Intune não precisam estar conectados).
    - No Intune, você criou e implantou um aplicativo que contém o cliente do Configuration Manager. Para obter detalhes sobre como fazer isso, veja Como instalar clientes em dispositivos do Windows gerenciados por MDM.
- Para usar o Configuration Manager para implantar o cliente:
    - Pelo menos um ponto de gerenciamento deve ser configurado para o modo HTTPS.
    - Você deve configurar um Gateway de Gerenciamento de Nuvem.


### <a name="set-up-the-cloud-management-gateway"></a>Configurar o Gateway de Gerenciamento de Nuvem

Configure o Gateway de Gerenciamento de Nuvem para permitir que clientes acessem seu site do Configuration Manager pela Internet sem o uso de certificados.

Você encontrará ajuda sobre como fazer isso nos tópicos a seguir:

- [Planejar o gateway de gerenciamento de nuvem no Configuration Manager](/sccm/core/clients/manage/plan-cloud-management-gateway).
- [Configurar o gateway de gerenciamento de nuvem para o Configuration Manager](/sccm/core/clients/manage/setup-cloud-management-gateway).
- [Monitorar o gateway de gerenciamento de nuvem no Configuration Manager](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway).

### <a name="set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Configurar o aplicativo dos Serviços do Azure em serviços de nuvem do Configuration Manager

Isso conecta o site do Configuration Manager ao Azure AD e é um pré-requisito para todas as outras operações nesta seção. Para fazer isso:

1.  No espaço de trabalho **Administração** do console do Configuration Manager, expanda **Serviços de Nuvem** e clique em **Serviços do Azure**.
2.  Na guia **Página Inicial**, no grupo **Serviços do Azure**, clique em **Configurar os Serviços do Azure**.
3.  Na página **Serviços do Azure** do Assistente de Serviços do Azure, selecione **Gerenciamento de Nuvem** para permitir que os clientes sejam autenticados com a hierarquia usando o Azure AD.
4.  Na página **Geral** do assistente, especifique um nome e uma descrição para o serviço do Azure.
5.  Na página **Aplicativo** do assistente, selecione o seu ambiente do Azure na lista e clique em **Procurar** para selecionar os aplicativos de cliente e servidor que serão usados para configurar o serviço do Azure:
    - Na janela do **aplicativo de servidor**, selecione o aplicativo de servidor que você deseja usar e depois clique em **OK**. Aplicativos de servidor são os aplicativos Web do Azure que contêm as configurações da sua conta do Azure, incluindo sua ID de locatário, ID de cliente e uma chave secreta para clientes. Se você não tiver um aplicativo de servidor disponível, use um dos seguintes:
        - **Criar**: Para criar um novo aplicativo de servidor, clique em **Criar**. Forneça um nome amigável para o aplicativo e o locatário. Em seguida, depois que você entrar no Azure, o Configuration Manager cria o aplicativo Web do Azure para você, incluindo a ID do cliente e a chave secreta para uso com o aplicativo Web. Posteriormente, você pode exibi-las no portal do Azure.
        - **Importar**: Para usar um aplicativo Web que já existe em sua assinatura do Azure, clique em **Importar**. Forneça um nome amigável para o aplicativo e o locatário e especifique a ID de locatário, ID do cliente e a chave secreta para o aplicativo Web do Azure que você deseja que o Configuration Manager use. Depois que você verificar as informações, clique em **OK** para continuar. Esta opção não está disponível atualmente nessa versão prévia.
    - Repita o mesmo processo para o aplicativo cliente.

  Você precisa conceder a permissão de aplicativo *Ler dados do diretório* quando você usar a Importação de Aplicativo, para definir as permissões corretas no portal. Se você usar a criação de aplicativos, as permissões serão criadas automaticamente com o aplicativo, mas você ainda precisará dar consentimento para o aplicativo no portal do Azure.
6.  Na página **Descoberta** do assistente, opcionalmente escolha **Ativar a Descoberta de Usuário do Azure Active Directory** e, em seguida, clique em **Configurações**.
Na caixa de diálogo **Configurações de Descoberta de Usuário do Azure AD**, configure um agendamento para quando ocorrer a descoberta. Você também pode habilitar a descoberta delta que verifica apenas as contas novas ou alteradas no Azure AD.
7.  Conclua o assistente.

Neste ponto, você se conectou a seu site do Configuration Manager para o Azure AD.


### <a name="install-the-cm-client-from-the-internet"></a>Instalar o cliente CM pela Internet

Antes de começar, verifique se os arquivos de origem de instalação do cliente estão armazenados localmente no dispositivo para o qual você deseja instalar o cliente.
Em seguida, use as instruções em [Como implantar clientes em computadores com Windows no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually) usando a seguinte linha de comando de instalação (substitua os valores de exemplo pelos seus próprios valores):

**ccmsetup.exe /NoCrlCheck /Source:C:\CLIENT  CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode=HEC AADTENANTID=780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME=contoso  AADCLIENTAPPID=<GUID> AADRESOURCEURI=https://contososerver**

- **/NoCrlCheck**: se o gateway de gerenciamento de nuvem ou ponto de gerenciamento usar um certificado do servidor não público, o cliente poderá não ser capaz de alcançar o local da CRL.
- **/Source**: Pasta local: local dos arquivos de instalação do cliente.
- **CCMHOSTNAME**: o nome do seu ponto de gerenciamento da Internet. Você pode encontrá-lo executando **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** de um prompt de comando em um cliente gerenciado.
- **SMSMP**: o nome do seu ponto de gerenciamento de pesquisa – pode ser em sua intranet.
- **SMSSiteCode**: o código do site do Configuration Manager.
- **AADTENANTID**, **AADTENANTNAME**: a ID e o nome do locatário do Azure AD vinculado ao Configuration Manager. Você pode localizar isso executando dsregcmd.exe /status em um prompt de comando em um dispositivo unido do Azure AD.
- **AADCLIENTAPPID**: a ID do aplicativo cliente do Azure AD. Para obter ajuda sobre como localizar isso, veja [Usar o portal para criar um aplicativo e uma entidade de serviço do Azure Active Directory que pode acessar recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key).
- **AADResourceUri**: o URI do identificador do aplicativo de servidor integrado do Azure AD.

## <a name="use-azure-services-wizard-to-configure-a-connection-to-oms"></a>Use o Assistente para Serviços do Azure para configurar uma conexão para OMS
A partir da versão de visualização técnica 1705, use o **Assistente de Serviços do Azure** para configurar sua conexão do Configuration Manager para o serviço de nuvem do Operations Management Suite (OMS). O assistente substitui os fluxos de trabalho anteriores para configurar essa conexão.

-   O assistente é usado para configurar os serviços de nuvem para o Configuration Manager, como o OMS, o Windows Store for Business (WSfB) e o Azure Active Directory (Azure AD).  

-   O Configuration Manager conecta-se ao OMS para recursos como [Log Analytics](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) ou [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics).

### <a name="prerequisites-for-the-oms-connector"></a>Pré-requisitos para o Conector do OMS
Os pré-requisitos para configurar uma conexão para o OMS são os mesmos dos [documentados para a versão Branch Atual 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#prerequisites). Essa informação é repetida aqui:  

-   Fornecendo a permissão do Configuration Manager para o OMS.

-   O conector do OMS deve ser instalado no computador que hospeda um [ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) no [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

-   Você deve instalar um Agente de Monitoramento da Microsoft para o OMS instalado no ponto de conexão de serviço junto com o conector do OMS. O agente e o conector do OMS devem ser configurados para usar o mesmo **espaço de trabalho do OMS**. Para instalar o agente, veja [Baixar e instalar o agente](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) na documentação do OMS.
-   Depois de instalar o conector e o agente, você deverá configurar o OMS para usar dados do Configuration Manager. Para fazer isso, no Portal do OMS, veja [Importar as coleções do Configuration Manager](/azure/log-analytics/log-analytics-sccm#import-collections).

### <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>Use o Assistente para Serviços do Azure para configurar a conexão para OMS

1.  No console, acesse **Administração** > **Visão geral** > **Serviços de Nuvem** > **Serviços do Azure** e, em seguida, escolha **Configurar Serviços do Azure**, na guia **Início** da faixa de opções, para iniciar o **Assistente de Serviços do Azure**.

2.  Na página **Serviços do Azure**, selecione o serviço de nuvem do Operation Management Suite. Forneça um nome amigável para o **Nome do serviço do Azure** e uma descrição opcional e clique **Próxima**.

3.  Na página **Aplicativo**, especifique seu Ambiente do Azure (a visualização técnica oferece suporte somente à nuvem pública). Em seguida, clique em **Procurar** para abrir a janela do Aplicativo do Servidor.

4.  Selecione um aplicativo Web:

    -   **Importar**: Para usar um aplicativo Web que já existe em sua assinatura do Azure, clique em **Importar**. Forneça um nome amigável para o aplicativo e o locatário e especifique a ID de locatário, ID do cliente e a chave secreta para o aplicativo Web do Azure que você deseja que o Configuration Manager use. Depois que você **verificar** as informações, clique em **OK** para continuar.   

    > [!NOTE]   
    > Quando você configura o OMS com essa visualização, o OMS oferece suporte somente à função *import* função para um aplicativo Web. Não há suporte para a criação de um novo aplicativo Web. Da mesma forma, não é possível reutilizar um aplicativo existente para o OMS.

5.  Se você concluiu todos os outros procedimentos com êxito, as informações na tela **Configuração de Conexão de OMS** aparecerão automaticamente nesta página. As informações para as configurações de conexão devem aparecer para sua **Assinatura do Azure**, **Grupo de recursos do Azure** e **Espaço de trabalho do Operations Management Suite**.

6.  O assistente conecta-se ao serviço do OMS usando as informações que você inseriu. Selecione as coleções de dispositivos que você deseja sincronizar com o OMS e, em seguida, clique em **Adicionar**.

7.  Verifique suas configurações de conexão na tela **Resumo** e, em seguida, selecione **Avançar**. A tela **Andamento** mostra o status da conexão e, em seguida, clique em **Concluir**.

8.  Após concluir o assistente, o console do Configuration Manager mostra que você configurou o **Operations Management Suite** como um **Tipo de Serviço de Nuvem**.

