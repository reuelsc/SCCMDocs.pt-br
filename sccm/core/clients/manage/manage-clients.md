---
title: Gerenciar clientes | System Center Configuration Manager
description: Saiba como gerenciar clientes no System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
caps.latest.revision: 17
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: 67a814330123a1615a0663872bf4af64e5b81a84


---
# <a name="how-to-manage-clients-in-system-center-configuration-manager"></a>Como gerenciar clientes no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Quando um cliente do System Center Configuration Manager for instalado e atribuído com êxito a um site do Configuration Manager, você verá o dispositivo no espaço de trabalho **Ativos e Conformidade** no nó **Dispositivos** e em uma ou mais coleções no nó **Coleções de Dispositivos**. Quando você seleciona o dispositivo ou a coleção que contém o dispositivo, você pode selecionar várias operações de gerenciamento. No entanto, também há outras maneiras de gerenciar o cliente, as quais podem envolver outros espaços de trabalho no console ou tarefas que não usam o console do Configuration Manager.  

 Use este tópico para ter uma visão geral das tarefas que podem gerenciar um cliente do Configuration Manager no espaço de trabalho **Ativos e Conformidade**, bem como informações mais detalhadas sobre tarefas adicionais que ajudam a gerenciar o cliente do Configuration Manager. Para obter informações sobre como configurar o cliente, consulte [Como definir as configurações do cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md)  

> [!NOTE]  
>  Um cliente do Configuration Manager pode estar instalado e não ser exibido no console do Configuration Manager. Esse cenário poderá acontecer se o cliente ainda não tiver sido atribuído a um site com êxito, ou se o console tiver que ser atualizado ou uma associação de coleção atualizada.  
>   
>  Além disso, um dispositivo também pode ser exibido no console quando o cliente do Configuration Manager não estiver instalado. Esse cenário poderá acontecer se o dispositivo for descoberto, mas o cliente do Configuration Manager não estiver instalado e atribuído. Os dispositivos móveis que são gerenciados usando o conector do Exchange Server não instalam o cliente do Configuration Manager. Além disso, os dispositivos registrados pelo Microsoft Intune não instalam o cliente do Configuration Manager.  
>   
>  Use a coluna **Cliente** no console do Configuration Manager para determinar se o cliente do Configuration Manager está instalado, para que você possa gerenciá-lo do console do Configuration Manager.  

##  <a name="a-namebkmkmanagingclientsdevicesnodea-manage-clients-from-the-devices-node"></a><a name="BKMK_ManagingClients_DevicesNode"></a> Gerenciar clientes no nó Dispositivos  
 Use o procedimento e a tabela a seguir para gerenciar um ou mais dispositivos no nó **Dispositivos** no espaço de trabalho **Ativos e Conformidade** .  

> [!IMPORTANT]  
>  Dependendo do tipo de dispositivo, algumas dessas opções poderão não estar disponíveis.  

#### <a name="to-manage-clients-from-the-devices-node"></a>Para gerenciar clientes no nó Dispositivos  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Dispositivos**.  

3.  Selecione um ou mais dispositivos e depois selecione uma das tarefas de gerenciamento de cliente a seguir na faixa de opções ou clique com o botão direito do mouse no dispositivo:  

    -   **Gerenciar informações de afinidade do dispositivo do usuário**  

         Permite configurar as associações entre usuários e dispositivos, o que permite implantar o software para usuários de forma eficiente.  

         Consulte [Vincular usuários e dispositivos com a afinidade de dispositivo de usuário no System Center Configuration Manager](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)  

    -   **Adicionar o dispositivo a uma coleção nova ou existente**  

         Use essas ações relacionadas a coleções para adicionar rapidamente o dispositivo selecionado a uma coleção usando uma regra direta.  

         [Operações e manutenção de coleções no System Center Configuration Manager](../../../core/clients/manage/collections/operations-and-maintenance-for-collections.md)  

    -   **Instalar e reinstalar o cliente usando o Assistente de Push de Cliente**  

         O assistente Push de Cliente proporciona uma maneira eficiente de instalar e reinstalar o cliente do Configuration Manager para repará-lo ou reconfigurá-lo em computadores que executam o Windows com as opções de configuração de site e com as propriedades adicionais de client.msi especificadas para a instalação do cliente por push.  

        > [!TIP]  
        >  Há várias maneiras diferentes de instalar (e reinstalar) o cliente do Configuration Manager. Embora o Assistente de Push de Cliente ofereça um método de instalação de cliente conveniente, pois é possível executá-lo do console, esse método de instalação de cliente possui muitas dependências e não é adequado para todos os ambientes. Se você não conseguir instalar o cliente com êxito usando o push de cliente, existem muitos outros métodos de instalação que você pode usar. Para obter mais informações sobre as dependências, consulte [Pré-requisitos para a implantação de clientes em computadores com Windows no System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md). Para obter mais informações sobre outros métodos de instalação de cliente, consulte [Métodos de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md).  

         Consulte [Como instalar clientes do Configuration Manager usando push de cliente](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

    -   **Transferir Site**  

         Transfira um ou mais clientes, incluindo dispositivos móveis gerenciados, para outro site primário na hierarquia. Os clientes podem ser reatribuídos individualmente ou podem ser selecionados várias vezes e reatribuídos em massa a um novo site.  

    -   **Administrar o cliente remotamente**  

         Você pode executar o Gerenciador de Recursos para ver as informações de inventário de hardware e de software de um cliente do Windows e administrá-lo remotamente usando o Controle Remoto, a Assistência Remota ou a Área de Trabalho Remota.  

         Consulte [Como usar o Gerenciador de Recursos para exibir o inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) e [Como usar o Gerenciador de Recursos para exibir o inventário de software no System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

         Consulte [Como administrar remotamente um computador cliente com Windows usando o System Center Configuration Manager](../../../core/clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

    -   **Aprovar um cliente**  

         Quando o cliente se comunica com o sistema de site usando HTTP e um certificado autoassinado, é necessário aprovar esses clientes para identificá-los como computadores confiáveis. Por padrão, a configuração do site aprova automaticamente clientes da mesma floresta e de florestas confiáveis do Active Directory, para que você não precise aprovar cada cliente manualmente. No entanto, é necessário aprovar manualmente computadores do grupo de trabalho confiáveis e outros computadores nos quais você confia, mas não estão aprovados.  

        > [!WARNING]  
        >  Embora algumas funções de gerenciamento possam funcionar para clientes não aprovados, não há suporte para esse cenário no Configuration Manager.  

         Não é necessário aprovar clientes que sempre se comunicam com sistemas de site usando HTTPS em vez de HTTP ou clientes que usam um certificado PKI ao se comunicarem com sistemas de site usando HTTP. Esses clientes estabelecem uma relação de confiança com o Configuration Manager usando os certificados PKI.  

    -   **Bloquear ou desbloquear um cliente**  

         Bloqueie um cliente no qual você não confia mais, para que ele não receba a política de cliente e para impedir que sistemas de sites do Configuration Manager se comuniquem com ele.  

        > [!WARNING]  
        >  Bloquear um cliente impede apenas a comunicação dele com os sistemas de sites do Configuration Manager, e não a comunicação dele com outros dispositivos. Além disso, quando o cliente se comunica com sistemas de site usando HTTP em vez de HTTPS, há algumas limitações de segurança.  

         Caso mude de ideia posteriormente, você poderá desbloquear um cliente bloqueado. No entanto, se você desbloquear um computador baseado em Intel AMT que estava provisionado para AMT ao ser bloqueado, será necessário executar etapas adicionais para poder gerenciar esse computador novamente fora da banda.  

         Consulte [Determinar o bloqueio de clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/determine-whether-to-block-clients.md).  

    -   **Limpar implantação PXE necessária**  

         Use esta opção para reimplantar as implantações PXE necessárias para o computador selecionado.  

         Consulte [Use o PXE para implantar o Windows pela rede com o System Center Configuration Manager](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   **Gerenciar as propriedades do cliente**  

         Você pode exibir os dados de descoberta e as implantações direcionadas ao cliente. Você também pode configurar variáveis que as sequências de tarefa usam para implantar um sistema operacional no dispositivo.  

    -   **Excluir o cliente**  

        > [!WARNING]  
        >  Não exclua um cliente se você quiser desinstalar o cliente do Configuration Manager ou removê-lo de uma coleção.  

         A ação **Excluir** exclui manualmente o registro do cliente do banco de dados do Configuration Manager e, geralmente, essa ação deve ser executada apenas em cenários de solução de problemas. Se você excluir o registro do cliente e o cliente do Configuration Manager ainda estiver instalado e se comunicando com o Configuration Manager, a Descoberta de Pulsação recriará esse registro e ele reaparecerá no console do Configuration Manager, embora o histórico do cliente e suas associações anteriores sejam perdidas.  

        > [!NOTE]  
        >  Quando você exclui um cliente de dispositivo móvel registrado pelo Configuration Manager, essa ação também revoga o certificado PKI enviado ao dispositivo móvel e o certificado é rejeitado pelo ponto de gerenciamento, mesmo que o IIS não verifique a CRL. Certificados de clientes herdados de dispositivos móveis não são revogados quando esses clientes são excluídos.  

         Para desinstalar o cliente, consulte [Desinstalar o cliente do Configuration Manager](#BKMK_UninstalClient).  

         Para atribuir o cliente a um novo site primário, consulte [Como atribuir clientes a um site no System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

         Para remover o cliente de uma coleção, reconfigure as propriedades da coleção. Consulte [Como gerenciar coleções no System Center Configuration Manager](../../../core/clients/manage/collections/manage-collections.md).  

    -   **Apagar um dispositivo móvel**  

         Você pode apagar os dispositivos móveis que oferecem suporte ao comando de apagamento.  

         Essa ação removerá permanentemente todos os dados do dispositivo móvel, os quais incluem dados e configurações pessoais. Geralmente, essa ação restaura os padrões de fábrica do dispositivo móvel. Apague um dispositivo móvel quando ele não for mais confiável; por exemplo, em caso de perda ou roubo.  

        > [!TIP]  
        >  Consulte a documentação do fabricante para obter mais informações sobre como o dispositivo móvel processa um comando de apagamento remoto.  

         Quando uma solicitação de apagamento é enviada, há geralmente um atraso até que o dispositivo móvel receba o comando de apagamento:  

        -   Se o dispositivo móvel for registrado pelo Configuration Manager ou pelo Microsoft Intune, o cliente receberá o comando de apagamento na próxima vez em que baixar a política do cliente.  

        -   Se o dispositivo móvel for gerenciado pelo conector do Exchange Server, ele receberá o comando de apagamento na próxima vez que fizer a sincronização com o Exchange.  

         Você pode usar a coluna **Apagar Status** para monitorar quando o dispositivo móvel receberá o comando de apagamento. Até que o dispositivo móvel envie um confirmação de apagamento ao Configuration Manager, você poderá cancelar o comando de apagamento.  

    -   **Desativar um dispositivo móvel**  

         Há suporte para a opção **Desativar** somente em dispositivos móveis registrados pelo Intune ou pelo Gerenciamento de Dispositivo Móvel local.  

         Para obter mais informações, veja [Ajude a proteger seus dados com apagamento remoto, bloqueio remoto ou redefinição de senha usando o System Center Configuration Manager](../../../mdm/deploy-use/wipe-lock-reset-devices.md).  

    -   **Alterar a propriedade de um dispositivo**  

         Você poderá alterar a propriedade dos dispositivos para **Empresa** ou **Pessoal** se um dispositivo não estiver associado ao domínio e não tiver o cliente do Configuration Manager instalado.  

         É possível usar esse valor nos requisitos de aplicativo para controlar as implantações, e você também pode usar essa configuração para controlar quanto inventário é coletado dos dispositivos dos usuários.  

        Para ver o valor da propriedade na lista de dispositivos, talvez você precise adicionar a coluna para o modo de exibição clicando com o botão direito do mouse em qualquer título de coluna e escolhendo **Proprietário do Dispositivo**.

         Para obter mais informações, consulte [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../mdm/plan-design/hybrid-mobile-device-management.md) (MDM [gerenciamento de dispositivo móvel] híbrido com o System Center Configuration Manager e o Microsoft Intune).  

##  <a name="a-namebkmkmanagingclientsdevicecollectionsnodea-manage-clients-from-the-device-collections-node"></a><a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> Gerenciar clientes no nó Coleções de Dispositivos  
 Use o procedimento e a tabela a seguir para gerenciar dispositivos de uma coleção no nó **Coleções de Dispositivos** , no espaço de trabalho **Ativos e Conformidade** .  

 Muitas das tarefas de gerenciamento de cliente que você pode realizar ao selecionar um único ou vários dispositivos no nó **Dispositivos** também podem ser realizadas no nível da coleção. Isso tem a vantagem de aplicar automaticamente a tarefa de gerenciamento a todos os dispositivos qualificados da coleção. Embora esse possa ser um método conveniente para gerenciar vários clientes ao mesmo tempo, ele também pode gerar muitos pacotes de rede e aumentar o uso da CPU no servidor do site.  

 Existem também algumas tarefas de gerenciamento de cliente que só podem ser realizadas no nível da coleção, as quais estão listadas na tabela a seguir.  

 Para poder realizar tarefas de gerenciamento de cliente no nível da coleção, considere a quantidade de dispositivos existentes na coleção, se eles estão conectados por conexões de rede de baixa largura de banda e quanto tempo a tarefa levará para ser concluída em todos os dispositivos. Quando você executa uma tarefa de gerenciamento de cliente, não é possível interrompê-la no console.  

#### <a name="to-manage-clients-from-the-device-collections-node"></a>Para gerenciar clientes no nó Coleções de Dispositivos  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Coleções de Dispositivos**.  

3.  Selecione uma coleção e depois uma das tarefas de gerenciamento de cliente a seguir na faixa de opções ou clique com o botão direito do mouse na coleção:  

    -   **Verifique a existência de malwares nos computadores e baixe arquivos de definição de antimalware.**  

         Consulte [Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

    -   **Implante o software, as linhas de base de configuração e as sequências de tarefas.**  

         Para obter mais informações sobre implantação de software e linhas de base de configuração, consulte:  

        -   [Implantar atualizações de software no System Center Configuration Manager](../../../sum/deploy-use/deploy-software-updates.md)  

        -   [Planejar e definir configurações de conformidade no System Center Configuration Manager](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

    -   **Definir configurações de gerenciamento de energia.**  

         Consulte [Como criar e aplicar planos de energia no System Center Configuration Manager](../../../core/clients/manage/power/create-and-apply-power-plans.md). Planos de energia podem ser usados somente em computadores que executam o Windows.  

    -   **Notifique os computadores para que baixem a política assim que possível.**  

         Use a notificação de cliente para informar aos clientes selecionados do Windows a necessidade de baixar a política de computador assim que possível, fora do intervalo de sondagem configurado da política do cliente.  

         As tarefas de notificação de cliente são exibidas no nó **Operações Cliente** , no espaço de trabalho **Monitoramento** .  

##  <a name="a-namebkmkclientcachea-configure-the-client-cache-for-configuration-manager-clients"></a><a name="BKMK_ClientCache"></a> Configurar o cache de cliente para clientes do Configuration Manager  
 É possível configurar o local e a quantidade de espaço em disco que os clientes do Windows Configuration Manager usam para armazenar arquivos temporários quando instalam aplicativos e programas. As atualizações de software também usam cache de cliente, mas não são restritas pelo tamanho do cache configurado e sempre tentam baixar no cache. É possível definir as configurações do cache de cliente quando você instala o cliente do Configuration Manager manualmente, quando usa a instalação do cliente por push ou após o cliente ser instalado.

Na versão 1606 do Configuration Manager, você pode especificar o tamanho da pasta de cache usando as configurações do cliente no console do Configuration Manager.   

 O local padrão para o cache de cliente do Configuration Manager é %*windir*%\ccmcache e espaço em disco padrão é 5120 MB.  

> [!IMPORTANT]  
>  Não criptografe a pasta usada para o cache do cliente. O Configuration Manager não pode baixar o conteúdo em uma pasta criptografada.  

### <a name="about-client-cache"></a>Sobre o cache do cliente  

O cliente do Configuration Manager baixa o conteúdo do software necessário logo após receber a implantação, mas aguarda para executá-lo até o horário agendado para a implantação. No horário agendado, o cliente do Configuration Manager verifica se o conteúdo está disponível no cache. Se o conteúdo está no cache e é a versão correta, o cliente sempre usa seu conteúdo armazenado em cache. No entanto, quando a versão necessária do conteúdo foi alterada e o conteúdo foi excluído para ceder espaço a outro pacote, o conteúdo é baixado no cache novamente.  

Se o cliente tentar baixar conteúdo de um programa ou aplicativo que seja maior que o tamanho do cache, a implantação falhará devido ao tamanho do cache insuficiente e o Configuration Manager gerará a ID de mensagem de status 10050. Se o tamanho do cache for aumentado mais tarde, o comportamento de repetição de download será diferente para um programa necessário e um aplicativo necessário:  

-   Para um programa necessário: O cliente não tenta automaticamente baixar o conteúdo novamente. Você deve reimplantar o pacote e o programa no cliente.  
-   Para um aplicativo necessário: Como a implantação do aplicativo é baseada em estado, o cliente automaticamente tentará baixar o conteúdo novamente da próxima vez que baixar sua política de cliente.  

Se o cliente tenta baixar um pacote menor em tamanho do que o cache mas este já está completamente cheio, todas as implantações necessárias continuam tentando fazê-lo até que o espaço do cache esteja disponível, até que o download chegue ao tempo limite ou até que o limite de repetição chegue à falha de espaço no cache. Se o tamanho do cache for aumentado posteriormente, o cliente do Configuration Manager tentará baixar o pacote novamente durante o próximo intervalo de repetição. O cliente tenta baixar o conteúdo a cada quatro horas por 18 vezes.  

O conteúdo armazenado em cache não é excluído automaticamente e permanece no cache por no mínimo um dia após o cliente usar esse conteúdo. Se você configura as propriedades do pacote com a opção para persistir o conteúdo no cache do cliente, o cliente não exclui automaticamente o conteúdo do pacote do cache. Se o espaço do cache do cliente é usado por pacotes que foram baixados nas últimas 24 horas e o cliente precisa baixar novos pacotes, você pode aumentar o tamanho do cache do cliente ou escolher a opção de excluir para remover o conteúdo do cache persistente.  

 Use os procedimentos a seguir para configurar o cache do cliente durante a instalação manual do cliente ou após a sua instalação.  

### <a name="to-configure-the-client-cache-when-you-install-clients-by-using-manual-client-installation"></a>Para configurar o cache do cliente para a instalação manual do cliente  

Execute o comando CCMSetup.exe por meio do local de origem da instalação e especifique as seguintes propriedades que precisar, separadas por espaço:  

   -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Para a versão 1606, use as configurações de tamanho de cache disponíveis em **Configurações do Cliente** no console do Configuration Manager em vez de SMSCACHESIZE. Para obter mais informações, consulte [Configurações do Cache do Cliente](../../../core/clients/deploy/about-client-settings.md#Client-Cache-Settings).

Para obter mais informações sobre como usar essas propriedades de linha de comando para CCMSetup.exe, consulte [Sobre as propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="to-configure-the-client-cache-folder-when-you-install-clients-by-using-client-push-installation"></a>Para configurar o cache do cliente para a instalação do cliente por push  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Configuração do Site**e clique em **Sites**.  

3.  Na lista **Sites** , selecione o site para o qual deseja configurar a instalação automática do cliente por push em todo o site.  

4.  Na guia **Início** , no grupo **Configurações** , clique em **Configurações de Instalação de Cliente**e clique na guia **Propriedades da Instalação**.  

5.  Na guia **Propriedades da Instalação** , especifique as seguintes propriedades que precisar e separe-as usando espaços:  

    -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Para a versão 1606, use as configurações de tamanho de cache disponíveis em **Configurações do Cliente** no console do Configuration Manager em vez de SMSCACHESIZE. Para obter mais informações, consulte [Configurações do Cache do Cliente](../../../core/clients/deploy/about-client-settings.md#Client-Cache-Settings).

       Para obter mais informações sobre como usar essas propriedades de linha de comando para CCMSetup.exe, consulte [Sobre as propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

6.  Clique em **OK** para salvar as propriedades que você especificou.  

### <a name="to-configure-the-client-cache-folder-on-the-client-computer"></a>Para configurar a pasta de cache do cliente no computador do cliente  

1.  No computador cliente, navegue até o **Configuration Manager** no Painel de Controle e clique duas vezes para abrir as propriedades.  

2.  Clique na guia **Cache** .  

3.  Especifique o espaço em disco a reservar para o cache do cliente.  

4.  Para alterar o local da pasta cache do cliente , clique em **Alterar Local**e especifique o novo local. O local padrão é *%windir%*\ccmcache.  

5.  Para excluir os arquivos armazenados atualmente na pasta cache do cliente, clique em **Excluir Arquivos**.  

6.  Clique em **OK** para fechar as **Propriedades do Configuration Manager**.  

### <a name="to-configure-client-cache-size-in-client-settings"></a>Para configurar o tamanho do cache do cliente nas Configurações do Cliente

A partir da versão 1606, você pode ajustar o tamanho da pasta de cache do cliente sem precisar reinstalar o cliente. Para fazer isso, configure o tamanho do cache do cliente no console do Configuration Manager usando as Configurações do Cliente.  

1. No console do Configuration Manager, vá até **Administração** > **Configurações do Cliente**.

2. Clique duas vezes em **Configurações do Cliente Padrão**.
  Você também pode criar configurações personalizadas para aplicar o tamanho do cache de forma mais seletiva. Para obter mais informações sobre configurações do cliente padrão e personalizadas, consulte [Como definir as configurações do cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

 3. Clique em **Configurações de Cache do Cliente** e escolha **Sim** para **Configurar o tamanho do cache do cliente**.

 4. Ajuste o tamanho máximo do cache usando **MB** ou **percentual das configurações de disco**. O cache é ajustado para o tamanho que for menor.

 5. Clique em **OK**.

    O cliente do Configuration Manager configurará o tamanho do cache com essas configurações quando a próxima política de cliente for baixada.

##  <a name="a-namebkmkuninstalclienta-uninstall-the-configuration-manager-client"></a><a name="BKMK_UninstalClient"></a> Desinstalar o cliente do Configuration Manager  
 É possível desinstalar o software cliente do Windows Configuration Manager de um computador usando o **CCMSetup.exe** com a propriedade **/Uninstall**. Execute o CCMSetup.exe em um computador individual por meio do prompt de comando ou implante um pacote ou programa para desinstalar o cliente para a coleção de computadores.  

> [!WARNING]  
>  Não é possível desinstalar o cliente do Configuration Manager usando um dispositivo móvel. Se precisar remover o cliente do Configuration Manager de um dispositivo móvel, você precisará apagar o dispositivo, o que excluirá todos os dados no dispositivo móvel.  

 Use o procedimento a seguir para desinstalar o cliente do Configuration Manager de computadores.  

#### <a name="to-uninstall-the-configuration-manager-client-from-the-command-prompt"></a>Para desinstalar o cliente do Configuration Manager do prompt de comando  

1.  Abra um prompt de comando do Windows e altere a pasta para o local em que o CCMSetup.exe está localizado.  

2.  Digite **Ccmsetup.exe /uninstall**e pressione **Enter**.  

> [!NOTE]  
>  O processo de desinstalação é silencioso e não exibe nenhum resultado na tela. Para verificar se a desinstalação do cliente foi bem-sucedida, examine o arquivo de log **CCMSetup.log** na pasta *%windir%\ ccmsetup* no computador cliente.  

##  <a name="a-namebkmkconflictingrecordsa-manage-conflicting-records-for-configuration-manager-clients"></a><a name="BKMK_ConflictingRecords"></a> Gerenciar registros conflitantes de clientes do Configuration Manager  
 O Configuration Manager usa a ID de hardware para tentar identificar clientes que possam ser duplicatas e alertar você quando houver registros conflitantes. Por exemplo, se você reinstalar um computador, a ID de hardware será a mesma, mas o GUID usado pelo Configuration Manager poderá ser alterado.  

 Quando o Configuration Manager pode solucionar um conflito usando a autenticação do Windows da conta de computador, ou um certificado PKI de origem confiável, o conflito será solucionado automaticamente para você. No entanto, quando o Configuration Manager não pode resolver o conflito, ele usa uma configuração de hierarquia que mescla automaticamente os registros quando detecta IDs de hardware duplicadas (a configuração padrão) ou permite que você decida quando mesclar, bloquear ou criar novos registros de clientes. Se você decidir gerenciar manualmente registros duplicados, será necessário solucionar manualmente os registros conflitantes usando o console do Configuration Manager.  

#### <a name="to-change-the-hierarchy-setting-for-managing-conflicting-records"></a>Para alterar a configuração de hierarquia para gerenciar registros conflitantes  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Configuração do Site**e clique em **Sites**.  

3.  No grupo **Sites** , clique em **Configurações da Hierarquia**e na guia **Aprovação de Cliente e Registros de Conflitos** .  

4.  Clique em **Resolver automaticamente registros em conflito** para mesclar automaticamente os registros conflitantes ou clique em **Resolver manualmente registros em conflito**e em **OK**.  

    > [!NOTE]  
    >  Quando o Configuration Manager pode resolver o conflito usando a conta de computador ou um certificado PKI, essa configuração é ignorada e o conflito é resolvido automaticamente.  

#### <a name="to-manually-resolve-conflicting-records"></a>Para resolver manualmente registros conflitantes  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Status do Sistema**e clique em **Registros Conflitantes**.  

3.  No painel de resultados, selecione um ou mais registros conflitantes e clique em **Registro Conflitante**.  

4.  Na caixa de diálogo **Registro Conflitante** , selecione uma das seguintes opções e clique em **OK**:  

    -   **Mesclar** para combinar o registro recém-detectado com o registro de cliente existente, criando um registro unificado.  

    -   **Novo** para criar um novo registro para o registro conflitante de cliente.  

    -   **Bloquear** para criar um novo registro para o registro conflitante de cliente, mas o marca como bloqueado.  

##  <a name="a-namebkmkpolicyretrievala-initiate-policy-retrieval-for-a-configuration-manager-client"></a><a name="BKMK_PolicyRetrieval"></a> Iniciar a recuperação de política para um cliente do Configuration Manager  
 Um cliente do Windows Configuration Manager baixa sua política de cliente segundo um cronograma que você define como uma configuração do cliente. No entanto, pode haver situações em que você quer iniciar a recuperação da política ad hoc do cliente, por exemplo, em um cenário de solução de problemas ou em testes.  

 Use os procedimentos a seguir para iniciar a recuperação da política ad hoc do cliente fora de seu intervalo de sondagem agendado usando a guia **Ações** no cliente do Configuration Manager ou executando um script no computador. Você deve estar conectado ao computador cliente com direitos administrativos para executar esses procedimentos.  

> [!NOTE]  
>  Você pode usar a notificação de cliente para iniciar a recuperação da política do cliente fora de seu intervalo de sondagem agendado.  
>   
>  Você pode gerenciar os clientes que executam Linux e UNIX. Para obter informações sobre a recuperação da política para clientes que executam Linux e UNIX, consulte a seção [Computer policy for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_PolicyforLnU).  

#### <a name="to-initiate-client-policy-retrieval-by-using-client-notification"></a>Para iniciar a recuperação da política do cliente por meio de notificação de cliente  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Coleções de Dispositivos**.  

3.  Selecione a coleção de dispositivos que contém os computadores para os quais deseja baixar a política e na guia **Início** , no grupo **Coleções** , clique em **Notificação de Cliente** e em **Baixar Política de Computador**.  

    > [!NOTE]  
    >  É possível também usar a notificação de cliente para iniciar a recuperação de política para um ou mais dos dispositivos selecionados que são exibidos em um nó da coleção temporária no nó **Dispositivos** .  

#### <a name="to-manually-initiate-client-policy-retrieval-by-using-the-actions-tab-on-the-configuration-manager-client"></a>Para iniciar manualmente a recuperação da política do cliente usando a guia Ações no cliente do Configuration Manager  

1.  Selecione **Configuration Manager** no Painel de Controle do computador.  

2.  Clique na guia **Ações** .  

3.  Clique em **Ciclo de Recuperação e Avaliação de Diretiva de Computador** para iniciar a política do computador e clique em **Executar Agora**.  

4.  Clique em **OK** para confirmar o prompt.  

5.  Repita as etapas 3 e 4 para quaisquer outras ações necessárias, como **Ciclo de Recuperação e Avaliação de Diretiva de Usuário** para as configurações do cliente do usuário.  

6.  Clique em **OK** para fechar as **Propriedades do Configuration Manager**.  

#### <a name="to-manually-initiate-client-policy-retrieval-by-using-a-script"></a>Para iniciar manualmente a recuperação da política do cliente usando um script  

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

    -   Abra um prompt de comando e digite: **cscript &lt;caminho\nomearquivo.vbs>**.  

5.  Clique em **OK** na caixa de diálogo **Windows Script Host** .  



<!--HONumber=Nov16_HO1-->


