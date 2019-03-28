---
title: Alta disponibilidade do servidor do site
titleSuffix: Configuration Manager
description: Como configurar a alta disponibilidade para o servidor de site do Configuration Manager com a adição de um servidor do site no modo passivo.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6dcef836-c0d1-40af-ad30-cd8d864b09a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: be3b70d91155b379881332ddb7c8d405d0d92e84
ms.sourcegitcommit: d8d142044586a53709b4478ad945f714737c8d6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58523853"
---
# <a name="site-server-high-availability-in-configuration-manager"></a>Alta disponibilidade do servidor do site no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

<!--1128774-->

Historicamente, você poderia adicionar redundância à maioria das funções no Configuration Manager com várias instâncias dessas funções em seu ambiente. Exceto para o próprio servidor do site. A partir da versão 1806 do Configuration Manager, a alta disponibilidade da função de servidor do site é uma solução baseada no Configuration Manager de instalação de um servidor de site adicional no modo  *passivo*. A versão 1810 adiciona suporte à hierarquia, portanto, os sites de administração central e os sites primários filhos também podem ter um servidor de site adicional no modo passivo. O servidor do site no modo passivo pode ser local ou baseado em nuvem no Azure.

Esse recurso traz os seguintes benefícios 
- Redundância e alta disponibilidade para a função de servidor do site  
- Alteração mais fácil do hardware ou sistema operacional do servidor do site  
- Transferência mais fácil do servidor do seu site para o Azure IaaS  

O servidor do site no modo passivo é usado além do servidor do site existente que está no modo *ativo*. Um servidor do site no modo passivo está disponível para uso imediato quando for necessário. Inclua este servidor do site adicional como parte de seu design geral para tornar o serviço do Configuration Manager [altamente disponível](/sccm/core/servers/deploy/configure/high-availability-options).  

Um servidor do site em modo passivo:
- Usa o mesmo banco de dados do site que o seu servidor do site no modo ativo.
- Não grava dados no banco de dados do site quando ele está em modo passivo.
- Usa a mesma biblioteca de conteúdo que seu servidor do site no modo ativo.

Para fazer o servidor do site no modo passivo ficar ativo, você *promove*-o manualmente. Essa ação alterna o servidor do site no modo ativo para que seja o servidor do site no modo passivo. As funções de sistema de sites disponíveis no servidor de modo ativo original permanecem disponíveis, desde que o computador esteja acessível. Somente a função de servidor do site é alternada entre os modos ativo e passivo.

O Microsoft Core Services Engineering e Operations usou esse recurso para migrar seu site de administração central para o Microsoft Azure. Para obter mais informações, confira o [artigo do Microsoft IT Showcase](https://www.microsoft.com/itshowcase/Article/Content/1065/Migrating-System-Center-Configuration-Manager-onpremises-infrastructure-to-Microsoft-Azure).



## <a name="prerequisites"></a>Pré-requisitos

- A biblioteca de conteúdo do site deve estar em um compartilhamento de rede remota. Ambos os servidores do site precisam de permissões de Controle Total para o compartilhamento e seu conteúdo. Para obter mais informações, confira [Gerenciar biblioteca de conteúdo](/sccm/core/plan-design/hierarchy/the-content-library#bkmk_remote).<!--1357525-->  

    - A conta de computador do servidor do site precisa de permissões de **Controle total** para o caminho de rede para o qual você está transferindo a biblioteca de conteúdo. Essa permissão se aplica ao compartilhamento e ao sistema de arquivos. Nenhum dos componentes são instalados no sistema remoto.

    - O servidor do site não pode ter a função de ponto de distribuição. O ponto de distribuição também usa a biblioteca de conteúdo, e essa função não dá suporte para biblioteca de conteúdo remota. Depois de mover a biblioteca de conteúdo, você não pode mais adicionar a função de ponto de distribuição ao servidor do site.  

- O servidor do site no modo passivo pode ser local ou baseado em nuvem no Azure.  
    > [!Note]  
    > Um servidor do site baseado em nuvem em modo passivo usa a IaaS (infraestrutura como serviço) do Azure. Para obter mais informações, consulte os seguintes artigos:  
    > - [Máquinas virtuais do Azure (para infraestrutura baseada em nuvem)](/sccm/core/understand/use-cloud-services#azure-virtual-machines-for-cloud-based-infrastructure)
    > - [Perguntas frequentes sobre o Configuration Manager no Azure](/sccm/core/understand/configuration-manager-on-azure)  

- Ambos os servidores do site devem ser associados ao mesmo Domínio do Active Directory.  

- Na versão 1806, o site deve ser um site primário autônomo.  

    - A partir da versão 1810, o Configuration Manager oferece suporte a servidores de site no modo passivo em uma hierarquia. O site de administração central e os sites primários filhos podem ter um servidor de site adicional no modo passivo.<!-- 3607755 -->  

- Ambos os servidores do site devem usar o mesmo banco de dados do site.  

    - Na versão 1806, o banco de dados deve ser remoto a partir de cada servidor do site. Da versão 1810 em diante, o processo de instalação do Configuration Manager não bloqueia mais a instalação da função de servidor de site em um computador com a função do Windows para clustering de failover. O Always On do SQL requer essa função; portanto, anteriormente não era possível colocar o banco de dados do site no servidor do site. Com essa alteração, é possível criar um site altamente disponível com menos servidores usando o Always On do SQL e um servidor do site no modo passivo.<!-- SCCMDocs issue 1074 -->  

    - O SQL Server que hospeda o banco de dados do site pode usar uma instância padrão, uma instância nomeada, o [cluster do SQL Server](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database) ou um [Grupo de disponibilidade Always On do SQL Server](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).  

    - Os dois servidores de sites precisam das funções de segurança **sysadmin** e **securityadmin** na instância do SQL Server que hospeda o banco de dados do site. O servidor do site original já deve ter essas funções, portanto, adicione-as ao novo servidor do site. Por exemplo, o script SQL a seguir adiciona essas funções ao novo servidor de site **VM2** no domínio Contoso:  

        ```SQL
        USE [master]
        GO
        CREATE LOGIN [contoso\vm2$] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
        GO
        ALTER SERVER ROLE [sysadmin] ADD MEMBER [contoso\vm2$]
        GO
        ALTER SERVER ROLE [securityadmin] ADD MEMBER [contoso\vm2$]
        GO        
        ```
    - Ambos os servidores do site precisam acessar o banco de dados do site na instância do SQL Server. O servidor do site original já deve ter esse acesso, portanto, adicione-o ao novo servidor do site. Por exemplo, o script SQL a seguir adiciona um logon ao banco de dados **CM_ABC** ao novo servidor de site **VM2** no domínio Contoso:  

        ```SQL
        USE [CM_ABC]
        GO
        CREATE USER [contoso\vm2$] FOR LOGIN [contoso\vm2$] WITH DEFAULT_SCHEMA=[dbo]
        GO
        ```

    - O servidor do site no modo passivo é configurado para usar o mesmo banco de dados do site que o servidor do site no modo ativo. O servidor do site no modo passivo apenas lê do banco de dados. Ele não grava no banco de dados até depois de ser promovido para o modo ativo.  

- O servidor do site em modo passivo:  

    - É necessário atender aos pré-requisitos para instalação de um site primário. Por exemplo, .NET Framework, compactação diferencial remota e Windows ADK. Para ver a lista completa, confira [Pré-requisitos de site e sistema sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).<!-- SCCMDocs issue 765 -->  

    - É necessário ter uma conta de computador no grupo de Administradores local no servidor do site no modo ativo.<!--516036-->

    - É necessário fazer a instalação usando arquivos de origem que correspondam à versão do servidor do site no modo ativo.  

    - Não é possível ter uma função do sistema de sites de qualquer site instalado antes da instalação do servidor do site na função de modo passivo.  

- Ambos os servidores do site podem executar diferentes versões do service pack ou sistema operacional, desde que ambas sejam [compatíveis com o Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  

- Não hospede a função de ponto de conexão de serviço em um servidor de site configurado para alta disponibilidade. Se estiver atualmente no servidor do site original, será necessário removê-lo e instalá-lo em outro servidor do sistema de sites. Para obter mais informações, consulte [Sobre o ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point).  

- Permissões para a [conta de instalação do sistema do site](/sccm/core/plan-design/hierarchy/accounts#site-system-installation-account)  

    - Por padrão, muitos clientes usam a conta de computador do servidor do site para instalar novos sistemas de site. O requisito então exige a adição da conta do computador do servidor do site ao grupo de **Administradores** local no sistema de sites remoto. Se o seu ambiente usar essa configuração, adicione a conta de computador do novo servidor do site a esse grupo local em todos os sistemas de site remoto. Por exemplo, todos os pontos de distribuição remotos.  

    - Recomendamos usar uma conta de serviço para instalar o sistema de sites para aumentar a segurança da configuração. A configuração mais segura é a de uso de uma conta de serviço local. Se o seu ambiente usa essa configuração, nenhuma alteração é necessária.  



## <a name="limitations"></a>Limitações

- Há suporte apenas para um único servidor do site no modo passivo em cada site.  

- Na versão 1806, não há suporte para um servidor do site no modo passivo em uma hierarquia. Uma hierarquia que inclui um site de administração central e um site primário filho. Crie apenas um servidor do site no modo passivo em um site primário autônomo.<!--1358224-->  

    - A partir da versão 1810, o Configuration Manager oferece suporte a servidores de site no modo passivo em uma hierarquia. O site de administração central e os sites primários filhos podem ter um servidor de site adicional no modo passivo.<!-- 3607755 -->  

- Não há suporte para um servidor do site no modo passivo em um site secundário.<!--SCCMDocs issue 680-->  

    > [!Note]  
    > Ainda há suporte para sites secundários em um site primário com servidores de site altamente disponíveis.

- A promoção do servidor do site no modo passivo para o modo ativo é manual. Não há failover automático.  

- Funções do sistema do site não podem ser instaladas no novo servidor antes de adicionar o servidor do site no modo passivo.  

    > [!Note]  
    > Depois que ele instala o servidor do site no modo passivo, você pode adicionar mais funções conforme necessário. Por exemplo, o Provedor de SMS ou um ponto de gerenciamento em um site primário.  

- Para funções como o ponto de relatório que usam um banco de dados, hospede o banco de dados em um servidor remoto de ambos os servidores do site.  

- Quando você adiciona o servidor do site na função de modo passivo, este também não instala a função Provedor de SMS. Instale pelo menos uma instância adicional do provedor em outro servidor para alta disponibilidade. Se o design incluir essa função no servidor do site, instale-o no novo servidor do site depois de adicioná-lo à função de modo passivo. Para obter mais informações, veja [Planejar para o provedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).  

- O console do Configuration Manager não é instalado automaticamente no servidor do site no modo passivo.  



## <a name="add-a-site-server-in-passive-mode"></a>Adicionar um servidor do site no modo passivo

Para obter mais informações sobre o processo geral de adição de funções, veja [Instalar funções do sistema de site](/sccm/core/servers/deploy/configure/install-site-system-roles).

1. No console do Configuration Manager, vá para o workspace **Administração**, expanda **Configuração do Site**, selecione o nó **Sites** e clique em **Criar Servidor do Sistema de Sites** na faixa de opções.   

2. Na página **Geral** do Assistente para Criar Servidor do Sistema de Sites, especifique o servidor para hospedar o servidor do site no modo passivo. O servidor especificado não pode hospedar nenhuma função do sistema de sites antes de instalar um servidor do site no modo passivo.  

3. Na página **Seleção de Função do Sistema**, selecione apenas **Servidor do site no modo passivo**.  

    > [!Note]  
    > O assistente executa as seguintes verificações inicias de pré-requisitos nesta página:  
    > - O servidor selecionado não é um servidor do site secundário
    > - O servidor selecionado ainda não é um servidor do site no modo passivo
    > - A biblioteca de conteúdo do site está em um local remoto  
    >  
    > Se essas verificações iniciais de pré-requisitos falharem, você não poderá continuar além dessa página do assistente.  

4. Na página **Servidor do Site no Modo Passivo**, forneça as seguintes informações que são usadas para executar a instalação e instalar a função de servidor do site no servidor especificado:

     - Selecione uma das seguintes opções:  

         - **Copiar os arquivos de origem de instalação na rede do servidor do site em modo ativo**: esta opção cria um pacote compactado e o envia para o novo servidor do site.  

         - **Usar os arquivos de origem no seguinte local no servidor do site em modo passivo**: por exemplo, um caminho local para o qual você já copiou os arquivos de origem. Verifique se que este conteúdo é da mesma versão que o servidor do site no modo ativo.  

         - (*Recomendado*) **Use os arquivos de origem no seguinte local de rede**: especifique o caminho diretamente para os conteúdos da pasta **CD.Latest** do servidor do site no modo ativo. Por exemplo, `\\Server\SMS_ABC\CD.Latest` em que "*Server*" é o nome do servidor do site no modo ativo, e "*ABC*" é o código do site.  

     - Especifique o caminho local no qual instalar o Configuration Manager no novo servidor do site. Por exemplo: `C:\Program Files\Configuration Manager`  

5. Conclua o assistente. Depois, o Configuration Manager instala o servidor do site no modo passivo no servidor especificado.

Para obter o status de instalação detalhado, no console, vá para o workspace **Monitoramento** e selecione o nó **Status do Servidor do Site**. O estado do servidor do site no modo passivo é exibido como **Instalando**. Para obter informações mais detalhadas, selecione o servidor e clique em **Mostrar Status**. Essa ação abre a janela de Status de Instalação do Servidor do Site. Quando o processo for concluído, o estado será exibido como **OK** para ambos os servidores.   

Para obter mais informações sobre o processo de instalação, veja [Fluxograma – configurar um servidor do site no modo passivo](/sccm/core/servers/deploy/configure/passive-site-server-flowchart).

Depois de adicionar um servidor do site no modo passivo, veja ambos os servidores do site na guia **Nós** no nó **Sites** do console. 

Todos os componentes do servidor do site do Configuration Manager estão em espera no servidor do site no modo passivo. Os serviços do Windows ainda estão em execução.



## <a name="site-server-promotion"></a>Promoção do servidor do site  

Da mesma forma que backup e recuperação, planeje e pratique seu processo para mudar os servidores do site. Considere os seguintes pontos em seu plano de promoção:  

- Pratique uma promoção planejada, em que ambos os servidores do site estão online. Também pratique um failover não planejado forçando a desconexão ou o desligamento do servidor do site no modo ativo.  

- Determine seus processos operacionais durante o failover e o que comunicar com outros administradores do Configuration Manager.  

- Antes de uma promoção planejada:  

    - Verifique o status geral do site e componentes do site. Verifique se tudo está íntegro conforme o normal para o seu ambiente.  

    - Verifique o status do conteúdo de todos os pacotes que estão ativamente replicando entre sites.  

    - Verifique o status do site secundário e a replicação do site. 

    - Não inicie nenhum novo trabalho de distribuição de conteúdo ou manutenção em servidores de sites filhos ou secundários. 

        > [!Note]  
        > Se a replicação de arquivo ou banco de dados entre sites estiver em andamento durante o failover, o novo servidor do site poderá não receber o conteúdo replicado. Se isso acontecer, redistribua o conteúdo de software depois que o novo servidor do site estiver ativo.<!--515436--> Para replicação de banco de dados, talvez seja necessário reinicializar um site secundário após o failover.<!-- SCCMDocs issue 808 -->


### <a name="process-to-promote-the-site-server-in-passive-mode-to-active-mode"></a>Processo para promover o servidor do site do modo passivo para o modo ativo

Esta seção descreve como alterar o servidor do site do modo passivo para o modo ativo. Para acessar o site e fazer essa alteração, você precisa ser capaz de acessar uma instância do Provedor de SMS. Para obter mais informações, veja [Usar vários provedores de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#BKMK_MultiSMSProv).  

> [!Important]  
> Por padrão, somente o servidor do site original tem a função de Provedor de SMS. Se esse servidor estiver offline, você não poderá se conectar ao site como provedor, pois nenhum provedor estará disponível. Quando você adiciona o servidor do site no modo passivo, o Provedor de SMS não é adicionado automaticamente. Adicione pelo menos uma função de Provedor de SMS adicional ao seu site para um serviço altamente disponível.  

> [!Tip]  
> O console do Configuration Manager solicita a lista de Provedores de SMS disponíveis da WMI no servidor do site. Quando você instala vários provedores de SMS em um site, o site atribui aleatoriamente cada nova solicitação de conexão para usar um provedor de SMS instalado. Não é possível especificar o local do Provedor de SMS a ser usado com uma sessão de conexão específica. Se o seu console não conseguir se conectar ao site porque o servidor do site atual está offline, especifique o outro servidor do site na janela Conexão do Site.  

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**. Selecione o site e, em seguida, mude para a guia **Nós**. Selecione o servidor do site no modo passivo e, em seguida, clique em **Promover para ativo** na faixa de opções. Clique em **Sim** para confirmar e continuar.   
  
2. Atualize o nó do console. A coluna **Status** para o servidor que você está promovendo exibe a guia **Nós** como **Promovendo**.  

3. Após a conclusão da promoção, a coluna **Status** mostrará **OK** para o novo servidor do site no modo ativo e para o novo servidor do site no modo passivo. A coluna **Nome do Servidor** para o site agora exibe o nome do novo servidor do site no modo ativo.

Para o status detalhado, vá para o workspace **Monitoramento** e selecione o nó **Status do Servidor do Site**. A coluna **Modo** identifica qual servidor está *Ativo* ou *Passivo*. Ao promover um servidor do modo passivo para o modo ativo, selecione o servidor do site que você está promovendo para ativo e depois escolha **Mostrar Status** na faixa de opções. Essa ação abre a janela Status de Promoção do Servidor do Site, que exibe detalhes adicionais sobre o processo.

Quando um servidor do site no modo ativo mudar para o modo passivo, somente a função de sistema de sites ficará passiva. Todas as outras funções de sistema de sites instaladas nesse computador permanecerão ativas e acessíveis aos clientes.

Para obter mais informações sobre o processo de promoção *planejado*, veja [Fluxograma – promover o servidor do site (planejado)](/sccm/core/servers/deploy/configure/promote-site-server-flowchart).


### <a name="unplanned-failover"></a>Failover não planejado

Se o servidor do site atual no modo ativo estiver offline, o servidor do site para promoção tentará contatar o servidor do site atual no modo ativo por 30 minutos. Se o servidor offline voltar antes dessa hora, ele será notificado com êxito e a alteração continuará normalmente. Caso contrário, o servidor do site para promoção forçará a atualização da configuração do site para que ele esteja ativo. Se o servidor offline voltar após esse período, ele primeiro verificará o estado atual no banco de dados do site. Em seguida, ele continua rebaixando a si mesmo para o servidor do site no modo passivo.

Durante esse período de espera 30 minutos, o site não tem nenhum servidor do site no modo ativo. Os clientes ainda se comunicar com funções voltadas para o cliente, como pontos de gerenciamento, pontos de atualização de software e pontos de distribuição. Os usuários podem instalar software que já esteja implantado. Nenhuma administração de site é possível nesse período. Para obter mais informações, veja [Impactos de falha do site](/sccm/core/servers/manage/site-failure-impacts).  

Se o servidor offline estiver danificado de modo que não possa retornar, exclua esse servidor do site do console. Em seguida, crie um novo servidor do site no modo passivo para restaurar um serviço altamente disponível. 

Para obter mais informações sobre o processo de failover *não planejado*, veja o [Fluxograma – promover o servidor do site (não planejado)](/sccm/core/servers/deploy/configure/promote-site-server-unplanned-flowchart).


### <a name="additional-tasks-after-site-server-promotion"></a>Tarefas adicionais após a promoção do servidor do site  

Depois de alternar entre os servidores do site, não será necessário realizar a maioria das outras tarefas durante a [recuperação de um site](/sccm/core/servers/manage/recover-sites#post-recovery-tasks). Por exemplo, você não precisa redefinir senhas nem reconectar a sua assinatura do Microsoft Intune.

As etapas a seguir podem ser necessárias em seu ambiente:  

- Se você importar certificados PKI para pontos de distribuição, reimporte o certificado para os servidores afetados. Para obter mais informações, veja [Gerar novamente os certificados para pontos de distribuição](/sccm/core/servers/manage/recover-sites#regenerate-the-certificates-for-distribution-points).  

- Se você integrar o Configuration Manager ao Microsoft Store para Empresas, reconfigure aquela conexão. Para obter mais informações, veja [Gerenciar aplicativos da Microsoft Store para Empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).  



## <a name="daily-monitoring"></a>Monitoramento diário

Quando você tiver um servidor do site no modo passivo, monitore-o diariamente. Verifique se seu Status permanece OK e está pronto para uso. No console do Configuration Manager, vá até o workspace **Monitoramento** e selecione o nó **Status do Servidor do Site**. Exiba os servidores do site e seu status atual. Também exiba o status no workspace **Administração**. Expanda **Configuração do Site** e selecione o nó **Sites**. Selecione o site e, em seguida, mude para a guia **Nós**. 
