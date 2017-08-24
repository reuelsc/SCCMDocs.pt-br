---
title: Gerenciar clientes | Microsoft Docs
description: Saiba como gerenciar clientes no System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
caps.latest.revision: "17"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 3a86924b2e5db3ac16eeda78b95ae6747ffd656f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-manage-clients-in-system-center-configuration-manager"></a>Como gerenciar clientes no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Quando um cliente do System Center Configuration Manager for instalado e atribuído com êxito a um site do Configuration Manager, você verá o dispositivo no espaço de trabalho **Ativos e Conformidade** no nó **Dispositivos** e em uma ou mais coleções no nó **Coleções de Dispositivos**. Quando você seleciona o dispositivo ou uma coleção, pode executar operações de gerenciamento. No entanto, também há outras maneiras de gerenciar o cliente, as quais podem envolver outros espaços de trabalho no console ou tarefas que não usam o console do Configuration Manager.  

> [!NOTE]  
>  Um cliente do Configuration Manager pode estar instalado e não ser exibido no console do Configuration Manager. Isso poderá acontecer se o cliente ainda não tiver sido atribuído a um site com êxito ou se o console precisar ser atualizado ou uma associação de coleção atualizada.  
>   
>  Além disso, um dispositivo também pode ser exibido no console quando o cliente do Configuration Manager não estiver instalado. Isso poderá acontecer se o dispositivo for descoberto, mas o cliente do Configuration Manager não estiver instalado e atribuído. Os dispositivos móveis que são gerenciados usando o conector do Exchange Server e os dispositivos que são registrados pelo Microsoft Intune, não instalam o cliente do Configuration Manager.  
>   
>  Use a coluna **Cliente** no console do Configuration Manager para determinar se o cliente do Configuration Manager está instalado, para que você possa gerenciá-lo do console do Configuration Manager.  

##  <a name="BKMK_ManagingClients_DevicesNode"></a> Gerenciar clientes no nó Dispositivos  

Observe que, dependendo do tipo de dispositivo, algumas dessas opções poderão não estar disponíveis.  

1.  No console do Configuration Manager, escolha **Ativos e Conformidade** >  **Dispositivos**.  

3.  Selecione um ou mais dispositivos e depois selecione uma das tarefas de gerenciamento de cliente na faixa de opções ou clique com o botão direito do mouse no dispositivo:  

    -   **Gerenciar informações de afinidade do dispositivo do usuário**  

         Configure as associações entre usuários e dispositivos para que você possa implantar o software para os usuários de forma eficiente.  

         Consulte [Vincular usuários e dispositivos com a afinidade de dispositivo de usuário no System Center Configuration Manager](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)  

    -   **Adicionar o dispositivo a uma coleção nova ou existente**  

         Adicione o dispositivo a uma coleção com uma regra direta.  
         
    -   **Instalar e reinstalar o cliente usando o Assistente de Push de Cliente**  

         Instale e reinstale o cliente do Configuration Manager para repará-lo ou reconfigurá-lo em computadores que executam o Windows. Inclui opções de configuração do site e as propriedades de client.msi definidas para instalação do cliente por push.  

        > [!TIP]  
        >  Há várias maneiras diferentes de instalar (e reinstalar) o cliente do Configuration Manager. Embora o Assistente de Push de Cliente ofereça um método de instalação de cliente conveniente, pois é possível executá-lo do console, esse método tem muitas dependências e não é adequado para todos os ambientes. Para obter mais informações sobre as dependências, consulte [Pré-requisitos para a implantação de clientes em computadores com Windows no System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md). Para obter mais informações sobre outros métodos de instalação de cliente, consulte [Métodos de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md).  

         Consulte [Como instalar clientes do Configuration Manager usando push de cliente](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

    -   **Transferir Site**  

         Transfira um ou mais clientes, incluindo dispositivos móveis gerenciados, para outro site primário na hierarquia. Os clientes podem ser reatribuídos individualmente ou podem ser selecionados várias vezes e reatribuídos em massa a um novo site.  

    -   **Administrar o cliente remotamente**  

         Você pode executar o Gerenciador de Recursos para ver as informações de inventário de hardware e de software de um cliente do Windows e administrá-lo remotamente usando o Controle Remoto, a Assistência Remota ou a Área de Trabalho Remota.  

         Consulte [Como usar o Gerenciador de Recursos para exibir o inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) e [Como usar o Gerenciador de Recursos para exibir o inventário de software no System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

         Consulte [Como administrar remotamente um computador cliente com Windows usando o System Center Configuration Manager](../../../core/clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

    -   **Aprovar um cliente**  

         Quando o cliente se comunica com o sistema de sites usando HTTP e um certificado autoassinado, é necessário aprovar esses clientes para identificá-los como computadores confiáveis. Por padrão, a configuração do site aprova automaticamente clientes da mesma floresta e de florestas confiáveis do Active Directory, para que você não precise aprovar cada cliente manualmente. No entanto, é necessário aprovar manualmente computadores do grupo de trabalho confiáveis e outros computadores nos quais você confia, mas não estão aprovados.  

        > [!WARNING]  
        >  Embora algumas funções de gerenciamento possam funcionar para clientes não aprovados, não há suporte para esse cenário no Configuration Manager.  

         Não é necessário aprovar clientes que sempre se comunicam com sistemas de sites usando HTTPS ou clientes que usam um certificado PKI ao se comunicarem com sistemas de sites usando HTTP. Esses clientes estabelecem uma relação de confiança usando os certificados PKI.  

    -   **Bloquear ou desbloquear um cliente**  

         Bloqueie um cliente no qual você não confia mais, para que ele não receba a política de cliente e para impedir que sistemas de sites do Configuration Manager se comuniquem com ele.  

        > [!WARNING]  
        >  Bloquear um cliente impede apenas a comunicação dele com os sistemas de sites do Configuration Manager, e não a comunicação dele com outros dispositivos. Além disso, quando o cliente se comunica com sistemas de site usando HTTP em vez de HTTPS, há algumas limitações de segurança.  

         Você pode desbloquear um cliente bloqueado. No entanto, se você desbloquear um computador baseado em Intel AMT que estava provisionado para AMT ao ser bloqueado, será necessário executar etapas adicionais para poder gerenciar esse computador novamente fora da banda.  

         Consulte [Determinar o bloqueio de clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/determine-whether-to-block-clients.md).  

    -   **Limpar implantação PXE necessária**  

         Reimplante as implantações PXE necessárias para o computador.  

         Consulte [Use o PXE para implantar o Windows pela rede com o System Center Configuration Manager](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   **Gerenciar as propriedades do cliente**  

         Exiba os dados de descoberta e as implantações direcionadas ao cliente. Você também pode configurar variáveis que as sequências de tarefa usam para implantar um sistema operacional no dispositivo.  

    -   **Excluir o cliente**  

        > [!WARNING]  
        >  Não exclua um cliente se você quiser desinstalar o cliente do Configuration Manager ou removê-lo de uma coleção.  

         A ação **Excluir** exclui manualmente o registro do cliente do banco de dados do Configuration Manager e, geralmente, você não deve usar essa ação exceto em cenários de solução de problemas. Se você excluir o registro do cliente e o cliente ainda estiver instalado e se comunicando com o Configuration Manager, a Descoberta de Pulsação recriará esse registro e ele reaparecerá no console do Configuration Manager, embora o histórico do cliente e suas associações anteriores sejam perdidas.  

        > [!NOTE]  
        >  Quando você exclui um cliente de dispositivo móvel registrado pelo Configuration Manager, essa ação também revoga o certificado PKI enviado ao dispositivo móvel e o certificado é rejeitado pelo ponto de gerenciamento, mesmo que o IIS não verifique a CRL. Certificados de clientes herdados de dispositivos móveis não são revogados quando esses clientes são excluídos.  

         Para desinstalar o cliente, consulte [Desinstalar o cliente do Configuration Manager](#BKMK_UninstalClient).  

         Para atribuir o cliente a um novo site primário, consulte [Como atribuir clientes a um site no System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

         Para remover o cliente de uma coleção, reconfigure as propriedades da coleção. Consulte [Como gerenciar coleções no System Center Configuration Manager](../../../core/clients/manage/collections/manage-collections.md).  

    -   **Apagar um dispositivo móvel**  

         Você pode apagar os dispositivos móveis que oferecem suporte ao comando de apagamento.  

         Essa ação remove permanentemente todos os dados do dispositivo móvel, que incluem dados e configurações pessoais. Geralmente, essa ação restaura os padrões de fábrica do dispositivo móvel. Apague um dispositivo móvel quando ele não for mais confiável, por exemplo, se ele for perdido ou roubado.  

        > [!TIP]  
        >  Consulte a documentação do fabricante para obter mais informações sobre como o dispositivo móvel processa um comando de apagamento remoto.  

         Geralmente há um atraso até que o dispositivo móvel receba o comando de apagamento:  

        -   Se o dispositivo móvel for registrado pelo Configuration Manager ou pelo Microsoft Intune, o cliente receberá o comando quando baixar a política do cliente.  

        -   Se o dispositivo móvel for gerenciado pelo conector do Exchange Server, ele receberá o comando quando fizer a sincronização com o Exchange.  

         Você pode usar a coluna **Apagar Status** para monitorar quando o dispositivo receberá o comando de apagamento. Até que o dispositivo envie um confirmação de apagamento ao Configuration Manager, você poderá cancelar o comando de apagamento.  

    -   **Desativar um dispositivo móvel**  

         Há suporte para a opção **Desativar** somente em dispositivos móveis registrados pelo Intune ou pelo Gerenciamento de Dispositivo Móvel local.  

         Para obter mais informações, veja [Ajude a proteger seus dados com apagamento remoto, bloqueio remoto ou redefinição de senha usando o System Center Configuration Manager](../../../mdm/deploy-use/wipe-lock-reset-devices.md).  

    -   **Alterar a propriedade de um dispositivo**  

         Você poderá alterar a propriedade dos dispositivos para **Empresa** ou **Pessoal** se um dispositivo não estiver associado ao domínio e não tiver o cliente do Configuration Manager instalado.  

         É possível usar esse valor nos requisitos de aplicativo para controlar as implantações e para controlar quanto inventário é coletado dos dispositivos dos usuários.  

        Talvez seja necessário adicionar a coluna **Proprietário do Dispositivo** à exibição clicando com o botão direito do mouse em qualquer título de coluna e selecionando-a.

         Para obter mais informações, consulte [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md) (MDM [gerenciamento de dispositivo móvel] híbrido com o System Center Configuration Manager e o Microsoft Intune).  

##  <a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> Gerenciar clientes no nó Coleções de Dispositivos  
  Muitas das tarefas que você pode executar em um único dispositivo ou em vários dispositivos no nó **Dispositivos** podem ser realizadas em coleções. Isso aplica automaticamente a operação a todos os dispositivos qualificados da coleção. Observe que isso gera muitos pacotes de rede e aumenta o uso da CPU no servidor do site.  

  Para poder realizar tarefas de gerenciamento de cliente no nível da coleção, considere a quantidade de dispositivos existentes na coleção, se eles estão conectados por conexões de rede de baixa largura de banda e quanto tempo a tarefa levará para ser concluída em todos os dispositivos. Uma vez iniciada, você não pode interromper a tarefa do console.  

#### <a name="to-manage-clients-from-the-device-collections-node"></a>Para gerenciar clientes no nó Coleções de Dispositivos  

1.  No console do Configuration Manager, escolha **Ativos e Conformidade** > **Coleções de Dispositivos**.  

3.  Selecione uma coleção e depois uma das tarefas de gerenciamento de cliente a seguir na faixa de opções ou clique com o botão direito do mouse na coleção. Essas tarefas de gerenciamento do cliente podem ser executadas *somente* no nível da coleção.  

    -   **Verifique a existência de malwares nos computadores e baixe arquivos de definição de antimalware.**  

         Consulte [Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

    -   **Implante o software, as linhas de base de configuração e as sequências de tarefas.**  

         Consulte:  

        -   [Implantar atualizações de software no System Center Configuration Manager](../../../sum/deploy-use/deploy-software-updates.md)  

        -   [Planejar e definir configurações de conformidade no System Center Configuration Manager](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

    -   **Definir configurações de gerenciamento de energia.**  

         Consulte [Como criar e aplicar planos de energia no System Center Configuration Manager](../../../core/clients/manage/power/create-and-apply-power-plans.md). Planos de energia podem ser usados somente em computadores que executam o Windows.  

    -   **Notifique os computadores para que baixem a política assim que possível.**  

         Use a notificação de cliente para informar aos clientes do Windows selecionados para baixar a política de computador assim que possível, fora do intervalo de sondagem da política do cliente.  

         As tarefas de notificação de cliente são exibidas no nó **Operações Cliente** , no espaço de trabalho **Monitoramento** .  

##  <a name="BKMK_ClientCache"></a> Configurar o cache de cliente para clientes do Configuration Manager  
O cache do cliente armazena arquivos temporários para quando os clientes instalam aplicativos e programas. As atualizações de software também usam cache de cliente, mas não são restritas pelo tamanho do cache configurado e sempre tentam baixar no cache. É possível definir as configurações do cache de cliente, como tamanho e local, quando você instala o cliente do Configuration Manager manualmente, quando usa a instalação do cliente por push ou após o cliente ser instalado.

A partir da versão 1606 do Configuration Manager, você pode especificar o tamanho da pasta de cache usando as configurações do cliente no console do Configuration Manager.   

 O local padrão para o cache de cliente do Configuration Manager é %*windir*%\ccmcache e espaço em disco padrão é 5120 MB.  

> [!IMPORTANT]  
>  Não criptografe a pasta usada para o cache do cliente. O Configuration Manager não pode baixar o conteúdo em uma pasta criptografada.  

### <a name="about-client-cache"></a>Sobre o cache do cliente  

O cliente do Configuration Manager baixa o conteúdo do software necessário logo após receber a implantação, mas aguarda para executá-lo até o horário agendado para a implantação. No horário agendado, o cliente do Configuration Manager verifica se o conteúdo está disponível no cache. Se o conteúdo estiver no cache e for a versão correta, o cliente usará seu conteúdo armazenado em cache. Quando a versão necessária do conteúdo foi alterada ou se o conteúdo foi excluído para ceder espaço a outro pacote, o conteúdo será baixado no cache novamente.  

Se o cliente tentar baixar conteúdo de um programa ou aplicativo que seja maior que o tamanho do cache, a implantação falhará devido ao tamanho do cache insuficiente e o Configuration Manager gerará a ID de mensagem de status 10050. Se o tamanho do cache for aumentado posteriormente, o resultado será:  

-   Para um programa necessário: O cliente não tenta automaticamente baixar o conteúdo novamente. Você deve reimplantar o pacote e o programa no cliente.  
-   Para um aplicativo necessário: o cliente automaticamente tentará baixar o conteúdo novamente quando baixar sua política de cliente.  

Se o cliente tenta baixar um pacote menor em tamanho do que o cache, mas o cache já estiver cheio, todas as implantações necessárias continuam tentando fazê-lo até que o espaço do cache esteja disponível, até que o download atinja o tempo limite ou até que o limite de repetição chegue para a falha de espaço no cache. Se o tamanho do cache for aumentado posteriormente, o cliente do Configuration Manager tentará baixar o pacote novamente durante o próximo intervalo de repetição. O cliente tenta baixar o conteúdo a cada quatro horas por 18 vezes.  

O conteúdo armazenado em cache não é excluído automaticamente e permanece no cache por no mínimo um dia após o cliente usar esse conteúdo. Se você configura as propriedades do pacote com a opção para persistir o conteúdo no cache do cliente, o cliente não exclui automaticamente o conteúdo do pacote do cache. Se o espaço do cache do cliente é usado por pacotes que foram baixados nas últimas 24 horas e o cliente precisa baixar novos pacotes, você pode aumentar o tamanho do cache do cliente ou escolher a opção de excluir para remover o conteúdo do cache persistente.  

 Use os procedimentos a seguir para configurar o cache do cliente durante a instalação manual do cliente ou após a sua instalação.  

### <a name="to-configure-the-client-cache-when-you-install-clients-by-using-manual-client-installation"></a>Para configurar o cache do cliente para a instalação manual do cliente  

Execute o comando CCMSetup.exe por meio do local de origem da instalação e especifique as seguintes propriedades que precisar, separadas por espaço:  

   -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Para a versão 1606, use as configurações de tamanho de cache disponíveis em **Configurações do Cliente** no console do Configuration Manager em vez de SMSCACHESIZE. Para obter mais informações, consulte [Configurações do Cache do Cliente](../../../core/clients/deploy/about-client-settings.md#client-cache-settings).

Para obter mais informações sobre como usar essas propriedades de linha de comando para CCMSetup.exe, consulte [Sobre as propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="to-configure-the-client-cache-folder-when-you-install-clients-by-using-client-push-installation"></a>Para configurar o cache do cliente para a instalação do cliente por push  

1.  No console do Configuration Manager, escolha **Administração** > **Configuração de Site** > **Sites**.  

3.  Selecione o site apropriado e, na guia **Início**, no grupo **Configurações**, escolha **Configurações de Instalação do Site** > **guia Propriedades da Instalação**.  

5.  Especifique as propriedades a seguir, separadas por espaços:  

    -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Para a versão 1606, use as configurações de tamanho de cache disponíveis em **Configurações do Cliente** no console do Configuration Manager em vez de SMSCACHESIZE. Para obter mais informações, consulte [Configurações do Cache do Cliente](../../../core/clients/deploy/about-client-settings.md#client-cache-settings).

       Para obter mais informações sobre como usar essas propriedades de linha de comando para CCMSetup.exe, consulte [Sobre as propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="to-configure-the-client-cache-folder-on-the-client-computer"></a>Para configurar a pasta de cache do cliente no computador do cliente  

1.  No computador cliente, navegue até o **Configuration Manager** no Painel de Controle e clique duas vezes para abrir as propriedades.  

2.  Na guia **Cache**, defina as propriedades de espaço e local. O local padrão é *%windir%*\ccmcache.  

5.  Para excluir os arquivos na pasta de cache, escolha **Excluir Arquivos**.  

    > [!NOTE]
    > 
    > O cache é uma pasta regular do Windows, portanto você pode automatizar a exclusão do conteúdo da pasta usando um script, um utilitário ou com o cmdlet do PowerShell `Remove-Item`. 


### <a name="to-configure-client-cache-size-in-client-settings"></a>Para configurar o tamanho do cache do cliente nas Configurações do Cliente

A partir da versão 1606, você pode ajustar o tamanho da pasta de cache do cliente sem precisar reinstalar o cliente. Para fazer isso, configure o tamanho do cache do cliente no console do Configuration Manager usando as Configurações do Cliente.  

1. No console do Configuration Manager, vá até **Administração** > **Configurações do Cliente**.

2. Clique duas vezes em **Configurações do Cliente Padrão**.
  Você também pode criar configurações personalizadas para aplicar o tamanho do cache de forma mais seletiva. Para obter mais informações sobre configurações do cliente padrão e personalizadas, consulte [Como definir as configurações do cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

 3. Escolha **Configurações de Cache do Cliente** e escolha **Sim** para **Configurar o tamanho do cache do cliente** e use **MB** ou as **configurações de percentual do disco**. O cache é ajustado para o tamanho que for menor.

     O cliente do Configuration Manager configurará o tamanho do cache com essas configurações quando a próxima política de cliente for baixada.

##  <a name="BKMK_UninstalClient"></a> Desinstalar o cliente do Configuration Manager  
 É possível desinstalar o software cliente do Windows Configuration Manager de um computador usando o **CCMSetup.exe** com a propriedade **/Uninstall**. Execute o CCMSetup.exe em um computador individual por meio do prompt de comando ou implante um pacote ou programa para desinstalar o cliente para a coleção de computadores.  

> [!WARNING]  
>  Não é possível desinstalar o cliente do Configuration Manager usando um dispositivo móvel. Se precisar remover o cliente do Configuration Manager de um dispositivo móvel, você precisará apagar o dispositivo, o que excluirá todos os dados no dispositivo móvel.  

#### <a name="to-uninstall-the-configuration-manager-client-from-the-command-prompt"></a>Para desinstalar o cliente do Configuration Manager do prompt de comando  

1.  Abra um prompt de comando do Windows e altere a pasta para o local em que o CCMSetup.exe está localizado.  

2.  Digite **Ccmsetup.exe /uninstall**e pressione **Enter**.  

> [!NOTE]  
>  O processo de desinstalação não exibe nenhum resultado na tela. Para verificar se a desinstalação do cliente foi bem-sucedida, examine o arquivo de log **CCMSetup.log** na pasta *%windir%\ ccmsetup* no computador cliente.  

##  <a name="BKMK_ConflictingRecords"></a> Gerenciar registros conflitantes de clientes do Configuration Manager  
 O Configuration Manager usa a ID de hardware para tentar identificar clientes que possam ser duplicatas e alertar você quando houver registros conflitantes. Por exemplo, se você reinstalar um computador, a ID de hardware será a mesma, mas o GUID usado pelo Configuration Manager poderá ser alterado.  

 Quando o Configuration Manager pode solucionar um conflito usando a autenticação do Windows da conta de computador ou um certificado PKI de origem confiável, o conflito é solucionado automaticamente. No entanto, quando o Configuration Manager não pode resolver o conflito, ele usa uma configuração de hierarquia que mescla automaticamente os registros quando detecta IDs de hardware duplicadas (a configuração padrão) ou permite que você decida quando mesclar, bloquear ou criar novos registros de clientes. Se você decidir gerenciar manualmente registros duplicados, será necessário solucionar manualmente os registros conflitantes usando o console do Configuration Manager.  


#### <a name="to-change-the-hierarchy-setting-for-managing-conflicting-records"></a>Para alterar a configuração de hierarquia para gerenciar registros conflitantes  

1.  No console do Configuration Manager, escolha **Administração** > **Configuração de Site** > **Sites** > **Configurações da Hierarquia**
2.  Na guia **Aprovação de Cliente e Registros de Conflitos**, escolha **Resolver automaticamente registros em conflito** ou **Resolver manualmente registros em conflito**.  

#### <a name="to-manually-resolve-conflicting-records"></a>Para resolver manualmente registros conflitantes  

1.  No console do Configuration Manager, escolha **Monitoramento** > **Status do Sistema** > **Registros Conflitantes**.  

3.  Selecione um ou mais registros conflitantes e escolha **Registro Conflitante**.  

4.  Selecione uma das seguintes opções:  

    -   **Mesclar** para combinar o registro recém-detectado com o registro de cliente existente.  

    -   **Novo** para criar um novo registro para o registro conflitante de cliente.  

    -   **Bloquear** para criar um novo registro para o registro conflitante de cliente, mas o marca como bloqueado.  

## <a name="manage-duplicate-hardware-identifiers"></a>Gerenciar identificadores de hardware duplicados
Começando do Configuration Manager versão 1610, é possível fornecer uma lista de IDs de hardware que será ignorada pelo Configuration Manager, para fins de registro de cliente e de inicialização PXE. Há dois problemas comuns que esse procedimento ajuda a resolver.

1. Muitos novos dispositivos, como o Surface Pro 3, não incluem uma porta Ethernet integrada. Um adaptador USB para Ethernet é geralmente usado para estabelecer uma conexão com fio para a implantação do sistema operacional. No entanto, eles costumam ser adaptadores compartilhados devido ao custo e à usabilidade geral. Como o endereço MAC do adaptador é usado para identificar o dispositivo, reutilizar o adaptador se torna problemático sem ações de administrador adicionais entre cada implantação. A partir da versão 1610, você pode excluir o endereço MAC desse adaptador para que ele possa ser reutilizado nesse cenário.
2. Embora o esperado é que a ID do SMBIOS seja um identificador de hardware exclusivo, alguns dispositivos de hardware de especialidade são criados com IDs duplicadas. Embora não seja tão comum quanto o cenário do adaptador USB para Ethernet acima, a lista de IDs de hardware pode ser usada para tratar desse problema também.

#### <a name="to-add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Para adicionar identificadores de hardware a serem ignorados pelo Configuration Manager  
1. No console do Configuration Manager, vá para **Administração** > **Visão Geral** > **Configuração de Site** > **Sites**.
2. Na guia **Início**, no grupo **Sites**, escolha **Configurações da Hierarquia**.
3. Na guia **Aprovação de Cliente e Registros de Conflitos**, escolha **Adicionar** na seção **Identificadores de Hardware Duplicados** para adicionar novos identificadores de hardware.

##  <a name="BKMK_PolicyRetrieval"></a> Iniciar a recuperação de política para um cliente do Configuration Manager  
 Um cliente do Windows Configuration Manager baixa sua política de cliente segundo um cronograma que você define como uma configuração do cliente. No entanto, pode haver situações em que você quer iniciar a recuperação da política ad hoc do cliente, por exemplo, para solução de problemas ou teste.  

Você pode iniciar a política de recuperação usando:


- [Notificação de cliente](#initiate-client-policy-retrieval-using-client-notification) 
- [A guia **Ações** no cliente](#manually-initiate-client-policy-retrieval-on-the-actions-tab-of-the-configuration-manager-client)
- [Um script](#manually-initiate-client-policy-retrieval-by-script)

> [!NOTE]  
>   
>  Para obter informações sobre a recuperação da política para clientes que executam Linux e UNIX, consulte a seção [Computer policy for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_PolicyforLnU).  

#### <a name="initiate-client-policy-retrieval-using-client-notification"></a>Iniciar a recuperação da política do cliente usando a notificação de cliente  

1.  No console do Configuration Manager, escolha **Ativos e Conformidade** > **Coleções de Dispositivos**.  

3.  Selecione a coleção de dispositivos que contém os computadores que você deseja baixar a política. Na guia **Início**, no grupo **Coleções**, escolha **Notificação de Cliente** > **Baixar Política do Computador**.  

    > [!NOTE]  
    >  É possível também usar a notificação de cliente para iniciar a recuperação de política para um ou mais dos dispositivos selecionados que são exibidos em um nó da coleção temporária no nó **Dispositivos** .  

#### <a name="manually-initiate-client-policy-retrieval-on-the-actions-tab-of-the-configuration-manager-client"></a>Iniciar manualmente a recuperação da política do cliente na guia Ações do cliente do Configuration Manager  

1.  Selecione **Configuration Manager** no Painel de Controle do computador.  

2.  Na guia **Ações**, escolha **Ciclo de Recuperação e Avaliação de Política de Computador** para iniciar a política do computador e escolha **Executar Agora**.  

4.  Escolha **OK** para confirmar o prompt.  

5.  Repita as etapas 3 e 4 para quaisquer outras ações necessárias, como **Ciclo de Recuperação e Avaliação de Diretiva de Usuário** para as configurações do cliente do usuário.  

#### <a name="manually-initiate-client-policy-retrieval-by-script"></a>Iniciar manualmente a recuperação da política do cliente por script  

1.  Abra um editor de texto, como o Bloco de Notas.  

2.  Copie e insira o seguinte no arquivo:  

    ```  
    on error resume next  

    dim oCPAppletMgr 'Control Applet manager object.  
    dim oClientAction 'Individual client action.  
    dim oClientActions 'A collection of client actions.  

    'Get the Control Panel manager object.  
    set  oCPAppletMgr=CreateObject("CPApplet.CPAppletMgr")  
    if err.number <> 0 then  
        Wscript.echo "Couldn't create control panel application manager"  
        WScript.Quit  
    end if  

    'Get a collection of actions.  
    set oClientActions=oCPAppletMgr.GetClientActions  
    if err.number<>0 then  
        wscript.echo "Couldn't get the client actions"  
        set oCPAppletMgr=nothing  
        WScript.Quit  
    end if  

    'Display each client action name and perform it.  
    For Each oClientAction In oClientActions  

        if oClientAction.Name = "Request & Evaluate Machine Policy" then  
            wscript.echo "Performing action " + oClientAction.Name   
            oClientAction.PerformAction  
        end if  
    next  

    set oClientActions=nothing  
    set oCPAppletMgr=nothing  
    ```  

3.  Salve o arquivo com uma extensão .vbs.  

4.  No computador cliente, execute o arquivo usando um dos seguintes métodos:  

    -   Navegue até o arquivo usando o Windows Explorer e clique duas vezes no arquivo de script.  

    -   Abra um prompt de comando e digite: **cscript &lt;caminho\nomearquivo.vbs>**.  

5.  Escolha **OK** na caixa de diálogo **Windows Script Host**.  
