---
title: Recursos no Technical Preview 1511
titleSuffix: Configuration Manager
description: Saiba mais sobre os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1511.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 69473706-21b3-498b-a67e-670fdc988f0d
author: aczechowski
robots: noindex,nofollow
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 8a805d6b7075d61b0e7669200670ac8434eccdf5
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336554"
---
# <a name="capabilities-in-technical-preview-1511-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1511 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1511. Esta versão é uma instalação de linha de base para o technical preview que você pode usar para instalar um novo site de technical preview ou para atualizar de uma versão anterior do technical preview.   Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview), para se familiarizar com os requisitos e limitações gerais de uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.  

Veja a seguir os novos recursos que você pode experimentar nesta versão.  

##  <a name="BKMK_WUfB"></a> Integração com o Windows Update for Business no Windows 10  
 Agora, o Configuration Manager tem a capacidade de diferenciar um computador com Windows 10 conectado diretamente via WUfB (Windows Update for Business) em relação àqueles conectados ao WSUS para obtenção de atualizações do Windows 10.  Para computadores conectados via WUfB, as atualizações e os upgrades podem ser gerenciados no ritmo definido por um usuário administrativo por meio das Políticas de Grupo ou das políticas de MDM, e essas atualizações e/ou esses upgrades podem ser instalados diretamente do WUfB.    
Para computadores conectados via WUfB, o Configuration Manager não poderá relatar o status de conformidade (incluindo Atualizações do Windows ou Atualizações de Definição). Além disso, o Configuration Manager não poderá implantar atualizações da Microsoft ou atualizações de terceiros nesses computadores.  

 **Pré-requisitos deste cenário:**  

-   Windows 10 Desktop Pro ou Windows 10 Enterprise Edition versão 1511 ou posterior  

-   Computadores a ser gerenciados por meio do [Windows Update para Empresas](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx).  

### <a name="try-it-out"></a>Experimente!  
 Tente concluir a seguinte tarefa e depois use as informações de comentários perto da parte superior deste tópico para nos contar como ela funcionou:  

1.  Desabilite o Windows Update Agent para que ele não examine o WSUS, se tiver sido habilitado anteriormente.   
    A chave do Registro **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\useWSUSServer** pode ser definida para indicar se o computador está verificando em relação ao WSUS ou ao Windows Update.  Quando o valor for 2, ele não verificará com relação ao WSUS.  

2.  Anote o novo atributo **UseWUServer**, no nó **Windows Update** do Gerenciador de Recursos do Configuration Manager.  

3.  Crie uma coleção com base no atributo **UseWUServer** para todos os computadores que estão conectados por meio do WUfB para atualizações.  

4.  Crie uma configuração de agente cliente para desabilitar o fluxo de trabalho de atualização de software e implante a configuração na coleção de computadores que estão conectados diretamente ao WUfB.  

5.  Os computadores gerenciados via WUfB exibirão **Desconhecido** no status de conformidade e não serão contados como parte do percentual de conformidade geral.  

##  <a name="BKMK_Office365ProPlus"></a> Gerenciamento da atualização do cliente do Office 365 ProPlus por meio do System Center Configuration Manager  
 Agora, o Configuration Manager tem a capacidade de gerenciar atualizações de clientes de desktop do Office 365 usando o fluxo de trabalho do Gerenciamento de Atualizações de Software do Configuration Manager.    
Quando a Microsoft publica uma nova atualização de clientes de desktop do Office 365 para WSUS (Windows Server Updates Services), o Configuration Manager poderá sincronizar a atualização com seu catálogo se a atualização do Office 365 estiver configurada como parte da sincronização do catálogo.  O servidor do site do Configuration Manager baixará as atualizações de clientes do Office 365 e distribuirá o pacote para pontos de distribuição do Configuration Manager.  Em seguida, o cliente do Configuration Manager informará os clientes de desktop do Office 365 sobre onde é possível obter as atualizações e quando iniciar o processo de instalação de atualização.  

**Pré-requisitos deste cenário:**  

### <a name="try-it-out"></a>Experimente!  
 Tente concluir a seguinte tarefa e depois use as informações de comentários perto da parte superior deste tópico para nos contar como ela funcionou:  

1.  É possível sincronizar as atualizações do Office 365 para o servidor do site do Configuration Manager e vê-las no console do Configuration Manager.  

2.  Você pode aprovar e implantar atualizações do Office 365 com êxito.  

3.  Você pode baixar e implantar atualizações do Office 365 com êxito.  

4.  Você pode verificar a conformidade com as atualizações do Office 365 usando o monitoramento ou os relatórios no console.  

 Para obter as etapas detalhadas, veja [Gerenciar atualizações do cliente Office 365 com o System Center Configuration Manager Technical Preview](https://technet.microsoft.com/library/mt628083.aspx).  

##  <a name="BKMK_AlwasyOn"></a> Suporte para o SQL Server AlwaysOn para bancos de dados altamente disponíveis  
 O Configuration Manager agora dá suporte ao uso de grupos de disponibilidade AlwaysOn do SQL Server para hospedar o banco de dados do site.  Quando você instala um novo site, é possível direcionar a instalação para usar o grupo de disponibilidade em vez de uma instância normal do SQL Server.  

> [!NOTE]  
>  A configuração bem-sucedida e o uso de grupos de disponibilidade exigem que você esteja familiarizado com a configuração de grupos de disponibilidade do SQL Server e se baseiam na documentação e nos procedimentos fornecidos na biblioteca de documentação do SQL Server.  

O processo de alto nível para configurar e usar os grupos de disponibilidade inclui:  

1.  Configurar o grupo de disponibilidade no SQL Server.  

2.  Instale um novo site do Configuration Manager e, durante a Instalação, direcione o site para usar o grupo de disponibilidade especificando o Ponto de extremidade dos grupos.  

**Pré-requisitos deste cenário:**  

-   Requer uma versão do SQL Server com suporte pelo Configuration Manager Technical Preview  

-   É necessário criar e configurar o Grupo de Disponibilidade do SQL Server antes de instalar o Configuration Manager  

-   O grupo de disponibilidade deve ter uma réplica primária e pode ter até duas réplicas secundárias síncronas  

-   O grupo de disponibilidade deve ter pelo menos um Ponto de Extremidade  

-   Você deve ter um local de rede que pode ser acessado por cada SQL Server no Grupo de Disponibilidade. Este local é usado pela Instalação durante a configuração do Grupo de Disponibilidade e pode ser removido após a conclusão da Instalação.  

**Problemas conhecidos desta versão:**  

-   Não é possível adicionar com êxito um novo membro de réplica a um Grupo de Disponibilidade que já esteja sendo usado como um banco de dados do site. Em vez disso, você deve reinstalar o site depois de adicionar o novo membro de réplica.  

-   Para este cenário, talvez seja necessário instalar o **cliente nativo do SQL Server 2012** ([do SQL Server 2012 Feature Pack](http://www.microsoft.com/download/details.aspx?id=29065)) no servidor do ponto de gerenciamento. Isso evita erros de conexão SQL (que são registrados no **mp_getauth.log** no servidor de ponto de gerenciamento).  

### <a name="try-it-out"></a>Experimente!  
Tente concluir as seguintes tarefas e depois use as informações de comentários perto da parte superior deste tópico para nos contar como elas funcionaram:  

-   Posso instalar um site primário que usa um servidor de banco de dados configurado para Grupos de Disponibilidade SQL AlwaysOn  

-   Consegui causar o failover dos meus Grupos de Disponibilidade SQL AlwaysOn para uma nova réplica no grupo e o site primário ainda está operacional  

### <a name="configuring-sql-server-alwayson-for-configuration-manager"></a>Configurando o SQL Server AlwaysOn para o Configuration Manager  
 Use os procedimentos a seguir para primeiro criar e configurar o grupo de disponibilidade e depois instale um novo site do Configuration Manager que usa o grupo de disponibilidade.  

#### <a name="to-create-a-sql-server-alwayson-availability-group"></a>Para criar um grupo de disponibilidade AlwaysOn do SQL Server  
O processo usado para [criar um grupo de disponibilidade do SQL Server](https://technet.microsoft.com/library/ff878265\(v=sql.120\).aspx) é documentado na biblioteca de documentação do SQL Server.  Ao criar o grupo de disponibilidade, garanta que os seguintes requisitos para uso com o Configuration Manager sejam atendidos:  

-   Um máximo de três membros:  

    -   Uma réplica primária e até duas réplicas secundárias  

    -   As réplicas secundárias devem ser síncronas.  

        > [!TIP]  
        >  Recomendamos que as réplicas secundárias sejam configuradas para ser somente leitura. Isso permite que você use uma réplica secundária para funções como relatórios, ao mesmo tempo que mantém o desempenho da réplica primária para as operações do site.  

-   Pelo menos um ponto de extremidade. O nome virtual deste ponto de extremidade será usado ao instalar o site do Configuration Manager.  

    > [!TIP]  
    >  Embora o grupo possa conter vários Pontos de extremidade, o Configuration Manager pode usar apenas um.  

#### <a name="to-install-a-configuration-manager-site-that-uses-the-availability-group"></a>Para instalar um site do Configuration Manager que usa o grupo de disponibilidade  
Para instalar um site que usa um grupo de disponibilidade do SQL Server:  

1.  Substitua o seguinte quando for solicitado pela Instalação do Configuration Manager:  

    -   **Nome do SQL Server:** insira o nome virtual do Ponto de extremidade configurado ao criar o grupo de disponibilidade. O nome virtual deve ser um nome DNS completo, como **&lt;endpointServer\>.fabrikam.com**.  

    -   **Instância**: este valor deve permanecer em branco. Não há nenhuma instância nesta configuração.  

    -   **Banco de dados**: insira o nome do banco de dados que você criou na réplica primária do grupo de disponibilidade.  

2.  Em seguida, você deve fornecer um local de rede que pode ser acessado por cada SQL Server no grupo:  

    -   A conta de computador e a conta de serviço de cada SQL Server exigem o acesso de controle total a este local.  

    -   Este local é usado somente durante a instalação e pode não ser compartilhado ou ser excluído após a conclusão da Instalação e a instalação do site.  

3.  Depois de fornecer essas informações, conclua a instalação com o processo e as configurações normais.  

##  <a name="BKMK_ClusterServerUpdates"></a> Atender a um cluster de servidores  
Agora você pode criar uma coleção que contém os servidores em um cluster e definir as configurações de cluster a serem usadas ao implantar atualizações no cluster. É possível controlar o percentual de servidores que estão online em um determinado momento, bem como configurar scripts pré e pós-implantação do PowerShell para executar ações personalizadas.  

**Problemas conhecidos desta versão:**  

-   Relatórios não estão disponíveis para verificar o status da implantação de atualizações de software para servidores de cluster.  

-   A opção de sequência de manutenção na página **Configurações de Cluster** está desabilitada e não está disponível nesta versão.  

### <a name="try-it-out"></a>Experimente!  
Tente concluir a seguinte tarefa e depois use as informações de comentários perto da parte superior deste tópico para nos contar como ela funcionou:  

-   Posso criar uma coleção que representa um cluster de servidores. Para este teste, é possível configurar suas regras de associação de coleta para ter dois computadores nesta coleção.  

-   Posso especificar que somente 50% dos servidores no cluster podem estar offline em qualquer ponto da instalação de cluster. Use os scripts de exemplo no procedimento para especificar os scripts de pré e pós-implantação.  

-   Implante uma atualização nesta coleção. Examine os arquivos start.txt e end.txt em C:\temp e verifique as horas de início e término da implantação nos servidores no cluster. Examine o arquivo UpdatesDeployment.log para obter mais informações.  

#### <a name="to-create-a-collection-for-a-server-cluster"></a>Para criar uma coleção para um cluster de servidores  

1.  [Crie uma coleção de dispositivos](https://technet.microsoft.com/library/gg712295.aspx) que contém os servidores no cluster.  

2.  No espaço de trabalho **Ativos e Conformidade**, clique em **Coleções de Dispositivos**, clique com o botão direito do mouse na coleção que contém os servidores no cluster e clique em **Propriedades**.  

3.  Na guia **Geral**, selecione **Todos os dispositivos fazem parte do mesmo cluster de servidores** e clique em **Configurações**.  

4.  Na página **Configurações de Cluster**, selecione o percentual de servidores que podem ser colocados offline ao mesmo tempo para que as atualizações de software sejam instaladas. Um único servidor de cluster pode ficar offline por vez, independentemente do percentual que você fornecer. O Configuration Manager será arredondado para baixo ao selecionar a quantidade de servidores que terão manutenção ao mesmo tempo. Por exemplo, se você escolher 51% e houver quatro servidores no cluster, dois servidores serão colocados offline ao mesmo tempo.  

5.  Especifique se deseja usar um script de pré-implantação (drenagem de nó) ou pós-implantação (retomada de nó).  

    > [!TIP]  
    >  Veja abaixo exemplos que você pode usar em testes de scripts de pré-implantação e pós-implantação que gravam a hora atual em um arquivo de texto:  
    >   
    >  **Pré-implantação**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Pós-implantação**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-cluster"></a>Para implantar atualizações de software no cluster de servidores  

1.  [Implante atualizações de software](https://technet.microsoft.com/library/gg712304.aspx) na coleção de clusters de servidores.  

2.  [Monitore a implantação de atualização de software](https://technet.microsoft.com/library/gg712304.aspx).  
