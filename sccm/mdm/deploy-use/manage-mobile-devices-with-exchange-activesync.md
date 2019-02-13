---
title: 'Gerenciar dispositivos móveis '
titleSuffix: Configuration Manager
description: Gerencie dispositivos móveis usando o conector do Exchange Server no System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a157e8696a9b4b24acb722be037185351f94ccdc
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127874"
---
# <a name="manage-mobile-devices-with-system-center-configuration-manager-and-exchange"></a>Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o conector do Exchange Server no System Center Configuration Manager quando desejar gerenciar dispositivos móveis que se conectam ao Exchange Server (local ou online) usando o protocolo Microsoft Exchange ActiveSync e quando não for possível registrá-los com o Configuration Manager. É possível configurar os recursos de gerenciamento de dispositivo móvel do Exchange, como apagamento remoto de dados no dispositivo e controle de configurações para vários servidores Exchange, no console do Configuration Manager.  

 ![configmgr&#45;with&#45;exchange](../../mdm/deploy-use/media/configmgr-with-exchange.png "configmgr-with-exchange")  

 Quando você gerencia dispositivos móveis usando o conector do Exchange Server, o cliente do Configuration Manager não é instalado nesses dispositivos. Portanto, algumas funções de gerenciamento são limitadas. Por exemplo, você não pode instalar softwares nesses dispositivos nem usar itens de configuração para defini-los. Para obter mais informações sobre quais recursos de gerenciamento você pode usar com o Configuration Manager para dispositivos móveis, consulte [Escolher uma solução de gerenciamento de dispositivo para o System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md).  

> [!IMPORTANT]  
>  Antes de instalar o conector do Exchange Server, verifique se o Configuration Manager dá suporte à versão do Microsoft Exchange que você está usando. Para obter mais informações, consulte “conector do Exchange Server” em [Supported operating systems for sites and clients for System Center Configuration Manager (Sistemas operacionais com suporte para sites e clientes do System Center Configuration Manager)](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  

 Ao usar o conector do Exchange Server, os dispositivos móveis podem ser gerenciados pelas configurações definidas no Configuration Manager em vez de gerenciados pelas políticas de caixa de correio padrão do Exchange ActiveSync. Defina as configurações que você deseja usar nas configurações de grupo a seguir: **Gerais**, **senha**, **gerenciamento de Email**, **segurança**, e **aplicativo**. Por exemplo, na configuração de grupo **Senha** , você pode definir se os dispositivos móveis exigem uma senha, o tamanho mínimo da senha, a sua complexidade e se é permitido recuperá-la.  

 Ao definir pelo menos uma configuração no grupo, o Configuration Manager gerencia todas as configurações no grupo para dispositivos móveis. Se você não definir uma configuração em um grupo, o Exchange continuará a gerenciar os dispositivos móveis com base nessas configurações. As políticas de caixa de correio do Exchange ActiveSync que são configuradas no Exchange Server e atribuídas a usuários ainda serão aplicadas.  

 Você também pode configurar o conector do Exchange Server para gerenciar as regras de acesso do Exchange, bem como permitir, bloquear ou colocar em quarentena dispositivos móveis. É possível apagar remotamente dispositivos móveis usando o console do Configuration Manager e os usuários podem apagar remotamente seus dispositivos móveis usando o Catálogo de Aplicativos.  

 O dispositivo móvel do usuário aparece automaticamente no Catálogo de Aplicativos quando é gerenciado pelo conector do Exchange Server e o Exchange Server é local. Ao configurar o conector do Exchange Server para o Microsoft Exchange Online, é necessário configurar manualmente a afinidade de dispositivo de usuário para que o dispositivo móvel do usuário apareça no Catálogo de Aplicativos. Para obter mais informações sobre como configurar manualmente a afinidade de dispositivo de usuário, consulte [Vincular usuários e dispositivos com a afinidade de dispositivo de usuário no System Center Configuration Manager](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

> [!TIP]  
>  Se você gerenciar um dispositivo móvel usando o conector do Exchange Server e esse dispositivo for transferido para outro usuário, exclua o dispositivo do console do Configuration Manager antes que o novo proprietário configure sua conta do Exchange no dispositivo móvel transferido.  

## <a name="required-security-permissions"></a>Permissões de segurança necessárias  
 Você deve ter as seguintes permissões de segurança para configurar o conector do Exchange Server:  

- Para adicionar, modificar e excluir o conector do Exchange Server: permissão **Modificar** para o objeto **Site**.  

- Para definir as configurações de dispositivo móvel: **ModifyConnectorPolicy** permissão para o **Site** objeto.  

  A função de segurança **Administrador Completo** inclui as permissões necessárias para configurar o conector do Exchange Server.  

  Você deve ter as seguintes permissões de segurança para gerenciar dispositivos móveis:  

- Para apagar um dispositivo móvel: **Excluir recurso** do objeto **Coleção**.  

- Para cancelar um comando de apagamento: **Modificar recurso** para o objeto **Coleção**.  

- Para permitir e bloquear dispositivos móveis: **Modificar recurso** para o objeto **Coleção**.  

  A função de segurança **Administrador de Operações** inclui as permissões necessárias para gerenciar dispositivos móveis usando o conector do Exchange Server.  

  Para obter mais informações sobre como configurar permissões de segurança, consulte [Configurar a administração baseada em funções do System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

## <a name="installing-and-configuring-an-exchange-server-connector"></a>Instalando e configurando um conector do Exchange Server  
 Use o procedimento a seguir para instalar e configurar um conector do Exchange Server para gerenciar dispositivos móveis. O Configuration Manager dá suporte apenas a um conector em uma organização do Exchange. Concluídas essas etapas, é possível monitorar os dispositivos móveis encontrados e gerenciados pelo conector visualizando as coleções que exibem os dispositivos móveis e usando os relatórios pertinentes a eles.  

> [!NOTE]  
>  O Configuration Manager gera nomes para os dispositivos móveis que ele encontra por meio do formato *UserName*_*DeviceType*. Se um usuário tiver mais de um dispositivo móvel do mesmo tipo, o Configuration Manager exibirá o mesmo nome para esses dispositivos móveis no console e nos relatórios.  

#### <a name="to-install-and-configure-an-exchange-server-connector"></a>Para instalar e configurar um conector do Exchange Server  

1.  Decida qual conta se conectará ao servidor de Acesso para Cliente do Exchange para gerenciar os dispositivos móveis. A conta pode ser a do computador do servidor do site ou uma conta de usuário do Windows. Em seguida, configure essa conta para executar os seguintes cmdlets do Exchange Server:  

    -   **Clear-ActiveSyncDevice**  

    -   **Get-ActiveSyncDevice**  

    -   **Get-ActiveSyncDeviceAccessRule**  

    -   **Get-ActiveSyncDeviceStatistics**  

    -   **Get-ActiveSyncMailboxPolicy**  

    -   **Get-ActiveSyncOrganizationSettings**  

    -   **Get-ExchangeServer**  
    
    -   **Get-Mailbox**
    
    -   **Get-Recipient**  

    -   **Set-ADServerSettings**  

    -   **Set-ActiveSyncDeviceAccessRule**  

    -   **Set-ActiveSyncMailboxPolicy**  

    -   **Set-CASMailbox**  

    -   **New-ActiveSyncDeviceAccessRule**  

    -   **New-ActiveSyncMailboxPolicy**  

    -   **Remove-ActiveSyncDevice**  
    
    -   **Get-CasMailbox**  
    
    -   **Get-usuário**  
    
    -   **Set-ActiveSyncOrganizationSettings**  

    > [!NOTE]  
    >  As seguintes funções de gerenciamento do Exchange Server incluem esses cmdlets: Gerenciamento de destinatários, gerenciamento de organização somente para exibição e gerenciamento de servidor. Para obter mais informações sobre grupos de funções de gerenciamento do Microsoft Exchange Server 2010, consulte [Entendendo os Grupos de Função de Gerenciamento](http://go.microsoft.com/fwlink/p/?LinkId=212914).  

    > [!TIP]  
    >  Se você tentar instalar ou o usar o conector do Exchange Server sem os cmdlets necessários, verá um erro registrado com a mensagem `Invoking cmdlet <cmdlet> failed` no arquivo EasDisc.log, no computador do servidor do site.  

2.  No console do Configuration Manager, clique em **Administração**.  

3.  No workspace **Administração**, expanda **Configuração da Hierarquia**e clique em **Conectores do Exchange Server**.  

4.  Na guia **Início** , no grupo **Criar** , clique em **Adicionar Exchange Server**.  

5.  Conclua o Assistente para Adicionar Exchange Server:  

    -   Se você usar uma instância local do Exchange Server e especificar um Servidor de Acesso para Cliente, poderá especificar um único servidor ou uma matriz de Servidor de Acesso para Cliente para cada site do Active Directory. Se o servidor ou a matriz estiver offline, o Configuration Manager tentará descobrir um Servidor de Acesso para Cliente para usá-lo. Se isso não for possível, o Configuration Manager voltará a usar um servidor de caixa de correio para estabelecer uma conexão com um Servidor de Acesso para Cliente. As tentativas são registradas como avisos no arquivo EasDisc.log, no computador do servidor do site. Por exemplo, procure `Failed to open runspace for site <site_name>`.  

    -   Para a conta de conector do Exchange Server, especifique a conta que você configurou na etapa 1.  

    -   Se você também registrar os dispositivos móveis usando o Configuration Manager, habilite a opção **Gerenciamento de Dispositivos Móveis Externos** para garantir que esses dispositivos continuem recebendo emails do Exchange após serem registrados pelo Configuration Manager.  

    -   Na página **Conta** do assistente, é possível configurar a conta usada para enviar notificações por email para clientes bloqueados pelo acesso condicional do Configuration Manager. A conta especificada deve ter uma caixa de correio válida no Exchange Server.  

         Para obter mais informações, consulte [Gerenciar estado do usuário no System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md).  

6.  É possível verificar a instalação do conector do Exchange Server usando mensagens de status e analisando os arquivos de log:  

    -   Para confirmar se o Gerenciador de Componentes do Site instalou com sucesso o conector do Exchange Server, procure a ID de status **1015** do componente **SMS_EXCHANGE_CONNECTOR** . Se o Configuration Manager não puder instalar o conector com êxito (por exemplo, porque o computador do Servidor de Acesso para Cliente especificado está offline), o Configuration Manager tentará instalar novamente a cada 60 minutos até que a instalação seja concluída com êxito ou até que você remova o conector do Exchange Server.  

    -   No computador do servidor do site, procure o arquivo SiteComp.log e, no arquivo de log, procure `Component SMS_EXCHANGE_CONNECTOR flagged for installation`. Uma instalação bem-sucedida é registrada com o seguinte texto: `STATMSG: ID=1015`.  
