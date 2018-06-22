---
title: Atualização para o System Center Configuration Manager
description: Conheça as etapas para executar uma atualização in-loco com êxito de um site e hierarquia que executa o System Center 2012 Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1cea0a54bc4c4c2d69f979bb09d83d7f5fac7706
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342708"
---
# <a name="upgrade-to-system-center-configuration-manager"></a>Atualização para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode executar uma atualização in-loco para atualizar para o System Center Configuration Manager de um site e uma hierarquia que executa o System Center 2012 Configuration Manager.  

 Antes de atualizar do System Center 2012 Configuration Manager, você deve preparar sites, o que exige que você remova configurações específicas que podem impedir uma atualização bem-sucedida, e então seguir a sequência de atualização quando houver mais de um único site envolvido.  

 > [!TIP]
 > Ao gerenciar a infraestrutura do site e da hierarquia do System Center Configuration Manager, os termos *upgrade*, *atualização* e *instalação* são usados para descrever três conceitos separados. Para saber como cada termo é usado, consulte [About upgrade, update, and install](/sccm/core/understand/upgrade-update-install) (Sobre upgrade, atualização e instalação).

##  <a name="bkmk_path"></a> Caminhos de atualização in-loco  

**Atualizar para a versão 1802**   
Quando você tiver a mídia de linha de base da versão 1802, atualize o seguinte para uma versão totalmente licenciada do System Center Configuration Manager versão 1802:   
-     Uma instalação de avaliação do System Center Configuration Manager versão 1802
-     System Center 2012 Configuration Manager com Service Pack 1
-     System Center 2012 Configuration Manager com Service Pack 2
-     System Center 2012 R2 Configuration Manager
-     System Center 2012 R2 Configuration Manager com Service Pack 1

**Atualizar para a versão 1702**   
Quando tiver a mídia de linha de base versão 1702, você poderá atualizar o seguinte para uma versão totalmente licenciada do System Center Configuration Manager versão 1702:   
-     Uma instalação de avaliação do System Center Configuration Manager versão 1702
-     System Center 2012 Configuration Manager com Service Pack 1
-     System Center 2012 Configuration Manager com Service Pack 2
-     System Center 2012 R2 Configuration Manager
-     System Center 2012 R2 Configuration Manager com Service Pack 1

**Atualizar para a versão 1606**  
Em 15 de dezembro de 2016, a mídia de linha de base para a versão 1606 foi relançada para adicionar suporte a cenários adicionais de atualização. Essa nova versão dá suporte para a atualização do seguinte para uma versão totalmente licenciada do System Center Configuration Manager versão 1606:  
-   Uma instalação de avaliação do System Center Configuration Manager versão 1606
-   Uma instalação de versão Release Candidate do System Center Configuration Manager  
-   System Center 2012 Configuration Manager com Service Pack 1  
-   System Center 2012 Configuration Manager com Service Pack 2  
-   System Center 2012 R2 Configuration Manager sem service pack
-   System Center 2012 R2 Configuration Manager com Service Pack 1  

Se usar a mídia de linha de base versão 1606 baixada antes de 15 de dezembro de 2016, você poderá atualizar apenas o seguinte para uma versão totalmente licenciada do System Center Configuration Manager versão 1606:
-   Uma instalação de avaliação do System Center Configuration Manager versão 1606
-   System Center 2012 Configuration Manager com Service Pack 2
-   System Center 2012 R2 Configuration Manager com Service Pack 1

<!-- Version 1511 has now dropped out of support
**Upgrade to version 1511**  
When you have version 1511 baseline media, you can upgrade the following to a fully licensed  version of System Center Configuration Manager version 1511:  
-   An evaluation install of System Center Configuration Manager version 1511
-   A release candidate install of System Center Configuration Manager  
-   System Center 2012 Configuration Manager with Service Pack 1  
-   System Center 2012 Configuration Manager with Service Pack 2  
-   System Center 2012 R2 Configuration Manager  
-   System Center 2012 R2 Configuration Manager with Service Pack 1  
-->


> [!TIP]  
>  Ao atualizar de uma versão do System Center 2012 Configuration Manager para o Branch Atual, talvez você possa simplificar o processo de atualização. Para obter mais informações, consulte:  
>   
>  -   A seção [Versões de linha de base e atualização](../../../../core/servers/manage/updates.md#bkmk_Baselines) em [Atualizações para o System Center Configuration Manager](../../../../core/servers/manage/updates.md)  
>  -   [A pasta CD.Latest para o System Center Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md)  

 **Não há suporte para o seguinte:**  
-   Não há suporte para atualizar uma versão de Technical Preview do System Center Configuration Manager para uma instalação totalmente licenciada.  Uma versão Technical Preview só pode ser atualizada para uma versão posterior da Technical Preview.  

-   Não há suporte para a migração de um Technical Preview para uma versão totalmente licenciada.  

##  <a name="bkmk_checklist"></a> Listas de verificação de atualização  
 As listas de verificação a seguir podem ajudá-lo a planejar uma atualização bem-sucedida do System Center Configuration Manager.  

### <a name="before-you-upgrade"></a>Antes de atualizar  

**Revise seu ambiente do System Center 2012 Configuration Manager** e resolver problemas, conforme detalhado no KB4018655: [os clientes do Configuration Manager reinstalam a cada cinco horas por causa de uma tarefa recorrente de repetição e pode causar uma atualização acidental do cliente](https://support.microsoft.com/help/4018655).

**Verifique se o ambiente computacional atende às configurações com suporte** necessárias para atualizar para o System Center Configuration Manager:  

Examine os sistemas operacionais de servidor em uso para hospedar funções de sistema de sites:  

-   Alguns sistemas operacionais mais antigos com suporte pelo System Center 2012 Configuration Manager não têm suporte pelo System Center Configuration Manager, e as funções de sistema de sites nesses sistemas operacionais devem ser realocadas ou removidas antes da atualização. Examine a documentação [Sistemas operacionais com suporte para servidores de sistema de sites](../../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).   
-   O Verificador de Pré-requisitos do Configuration Manager não verifica os pré-requisitos para funções do sistema de sites no servidor do site ou em sistemas de sites remotos  

Examine os pré-requisitos necessários em cada computador que hospeda uma função do sistema de sites:  

-   Por exemplo, para implantar um sistema operacional, o System Center Configuration Manager usa o Windows ADK (Kit de Avaliação e Implantação do Windows 10). Antes de executar a instalação, você deve baixar e instalar o Windows 10 ADK no servidor do site e em cada computador que executa uma instância do Provedor de SMS.  

Para obter informações gerais sobre as plataformas com suporte e as configurações de pré-requisito, consulte [Supported configurations for System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md).  

Para obter informações sobre o uso do Windows ADK com o Configuration Manager, consulte [Infrastructure requirements for operating system deployment in System Center Configuration Manager](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md) (Requisitos de infraestrutura para implantação de sistema operacional no System Center Configuration Manager).  

**Examinar o status do site e da hierarquia e verificar se não existem problemas não resolvidos:**  
Antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, do servidor de banco de dados do site e das funções do sistema de site que estão instalados em computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.  

**Instalar todas as atualizações críticas aplicáveis para sistemas operacionais em computadores que hospedam o site, o servidor de banco de dados do site e as funções do sistema de site remoto:**  
Antes de atualizar um site, instale todas as atualizações críticas para cada sistema de site aplicável. Se uma atualização instalada precisar de uma reinicialização, reinicie os computadores aplicáveis antes de iniciar a atualização do service pack.  

Para obter mais informações, consulte [Windows Update](http://go.microsoft.com/fwlink/p/?LinkId=105851).  

**Desinstalar as funções do sistema de sites sem suporte pelo System Center Configuration Manager:**  
As seguintes funções de sistema de sites não são mais usadas no System Center Configuration Manager e devem ser desinstaladas antes da atualização do System Center 2012 Configuration Manager:  

-   Ponto de Gerenciamento Fora de Banda  
-   Ponto do Validador da Integridade do Sistema  

**Desabilitar réplicas de banco de dados para pontos de gerenciamento em sites primários:**  
O Configuration Manager não pode atualizar com êxito um site primário que tenha uma réplica de banco de dados habilitada para pontos de gerenciamento. Desabilite a replicação de banco de dados antes de você:  

-   Criar um backup do banco de dados do site para testar a atualização do banco de dados  
-   Atualizar o site de produção para o System Center Configuration Manager  

Para obter mais informações, consulte:  
-   System Center 2012 Configuration Manager: [Configurar réplicas de banco de dados para os pontos de gerenciamento](https://technet.microsoft.com/library/hh846234.aspx)  
-   System Center Configuration Manager: [Database replicas for management points for System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md) (Réplicas de banco de dados para pontos de gerenciamento para o System Center Configuration Manager)  

**Reconfigure os pontos de atualização de software que usam NLBs:**  
O Configuration Manager não pode atualizar um site que usa um cluster NLB (Balanceamento de Carga de Rede) para hospedar pontos de atualização de software.  

Se você usar clusters NLB para pontos de atualização de software, use o PowerShell para remover do cluster NLB. (A partir do System Center 2012 Configuration Manager SP1, não há nenhuma opção no console do Configuration Manager para configurar um cluster NLB)  

**Desabilitar todas as tarefas de manutenção do site em cada site durante a atualização do site:**  
Antes de atualizar para o System Center Configuration Manager, desabilite todas as tarefas de manutenção que possam ser executadas nesse site durante o período em que o processo de atualização ficar ativo. Isso inclui, mas não está limitado ao seguinte:  

-   Servidor do Site de Backup  
-   Excluir Operações Antigas do Cliente  
-   Excluir Dados Antigos de Descoberta  

Quando uma tarefa de manutenção de banco de dados do site é executada durante o processo de atualização, a atualização do site pode falhar.  

Para desabilitar uma tarefa, registre o agendamento da tarefa para que você possa restaurar sua configuração depois de concluir a atualização do site.  

Para obter mais informações sobre tarefas de manutenção de site, veja:  

-   System Center 2012 Configuration Manager: [Planejando operações do site no Configuration Manager](https://technet.microsoft.com/library/gg712686.aspx)  
-   System Center Configuration Manager: [Reference for maintenance tasks for System Center Configuration Manager](../../../../core/servers/manage/reference-for-maintenance-tasks.md) (Referência para tarefas de manutenção do System Center Configuration Manager)  

**Executar o Verificador de Pré-requisitos de Instalação**:  
Antes de atualizar um site, você pode executar o **Verificador de Pré-requisitos** independentemente da Instalação para validar que seu site atende aos pré-requisitos. Posteriormente, ao atualizar o site, o Verificador de pré-requisitos será executado novamente.  

Se você usar a mídia de linha de base para a versão 1606 de outubro de 2016, a verificação de pré-requisitos independente avaliará o site quanto à atualização para o Branch Atual e para o LTSB (Branch de Manutenção em Longo Prazo) do System Center Configuration Manager. Como não há suporte para alguns recursos de LTSB, você poderá ver entradas em *ConfigMgrPrereq.log* semelhantes ao seguinte:
 - INFORMAÇÕES: o site é uma edição LTSB.
 - Função do sistema de sites 'Ponto de sincronização do Asset Intelligence' sem suporte para a edição LTSB;    Erro;    O Configuration Manager detectou que o 'ponto de sincronização do Asset Intelligence' está instalado. Não há suporte para o Asset Intelligence na edição LTSB. Você deve desinstalar a função de sistema de sites de ponto de sincronização do Asset Intelligence antes de continuar.

Se você planeja atualizar para o Branch Atual, os erros para a edição LTSB poderão ser ignorados com segurança. Eles se aplicam apenas se você planeja atualizar para o LTSB.

Posteriormente, ao executar a instalação do Configuration Manager para fazer a atualização, a verificação de pré-requisitos executará novamente e avaliará seu site com base no branch do System Center Configuration Manager que você escolheu instalar (Branch Atual ou LTSB). Se optar por atualizar para o Branch Atual, a verificação de recursos que não têm suporte do LTSB não será executada.

Para obter mais informações, consulte o [Verificador de pré-requisitos](/sccm/core/servers/deploy/install/prerequisite-checker) e a [Lista de verificações de pré-requisitos para o System Center Configuration Manager](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).  

**Baixar arquivos de pré-requisitos e arquivos redistribuíveis para o System Center Configuration Manager:**    
Use o **Downloader de Instalação** para baixar arquivos de pré-requisitos redistribuíveis, pacotes de idiomas e as atualizações mais recentes de produtos para o System Center Configuration Manager.  

Para obter informações, consulte [Ferramenta de download de instalação](/sccm/core/servers/deploy/install/setup-downloader).  

**Planejar para gerenciar idiomas do servidor e do cliente**:  
Quando você atualiza um site, a atualização do site instala somente as versões de pacote de idiomas que você seleciona durante a atualização.  

-   A instalação examina a configuração do idioma atual do seu site e identifica os pacotes de idiomas disponíveis na pasta em que você armazena arquivos de pré-requisitos baixados anteriormente.  
-   Você pode confirmar a seleção do servidor atual e os pacotes de idiomas do cliente ou alterar as seleções para adicionar ou remover suporte para idiomas.  
-   Somente os pacotes de idiomas que estão disponíveis quando você executa a instalação (que você obtém com os arquivos de pré-requisito baixados) podem ser selecionados.  

> [!NOTE]  
>  Você não pode usar os pacotes de idiomas do System Center 2012 Configuration Manager para habilitar idiomas para um site do System Center Configuration Manager.  

Para obter mais informações sobre pacotes de idiomas, consulte [Pacotes de idiomas no System Center Configuration Manager](../../../../core/servers/deploy/install/language-packs.md).  

**Examinar a lista de considerações para atualizações do site**:  
Quando você atualiza um site, alguns recursos e configurações são redefinidos para uma configuração padrão. Para ajudá-lo a se preparar para essas alterações e outras relacionadas, examine as informações em  [Considerações para atualização](#bkmk_considerations).  

**Criar um backup do banco de dados do site no site de administração central e em sites primários:**  
Antes de atualizar um site, faça backup do banco de dados do site para assegurar que você fez um backup com êxito a ser usado para recuperação de desastre.  

Consulte [Backup e recuperação para o System Center Configuration Manager](../../../../protect/understand/backup-and-recovery.md).  

**Fazer backup de um arquivo Configuration.mof personalizado**:  
Se você usar um arquivo Configuration.mof personalizado para definir as classes de dados usadas com o inventário de hardware, crie um backup desse arquivo antes de atualizar o site. Em seguida, após a atualização, restaure esse arquivo em seu site. Para obter mais informações sobre o uso desse arquivo, consulte [Como estender o inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

**Testar o processo de atualização de banco de dados em uma cópia do backup mais recente do banco de dados do site:**  
Antes de atualizar um site de administração central do Configuration Manager ou site primário, teste o processo de atualização do banco de dados do site em uma cópia do banco de dados do site.  

-   Você deve testar o processo de atualização de banco de dados do site, pois quando você atualiza um site, o banco de dados do site pode ser modificado  
-   Embora o teste de atualização de banco de dados não seja necessário, ele pode identificar problemas na atualização antes que seu banco de dados de produção seja afetado  
-   Uma atualização do banco de dados do site com falha pode deixar o banco de dados do site inoperante e pode requerer uma recuperação de site para restaurar a funcionalidade  
-   Embora o banco de dados do site seja compartilhado entre sites em uma hierarquia, planeje testar o banco de dados em cada site aplicável antes de atualizar esse site  
-   Se você usar réplicas de banco de dados para pontos de gerenciamento em um site primário, desabilite a replicação antes de criar o backup do banco de dados do site  

O Configuration Manager não dá suporte ao backup de sites secundários nem ao teste de atualização de um banco de dados do site secundário.  

Não há suporte para executar um teste da atualização do banco de dados no banco de dados do site de produção. Isso atualiza o banco de dados do site e pode deixar o site inoperante.  

Para obter mais informações, consulte [Testar a atualização de banco de dados do site](#bkmk_test).  

**Reiniciar o servidor do site e cada computador que hospeda uma função de sistema de sites**:  
Isso é feito para assegurar que não haja nenhuma ação pendente de uma instalação recente de atualizações ou de pré-requisitos e, além disso, é um processo interno específico da empresa.  

**Atualizar sites**:  
Iniciando no site de nível superior na hierarquia, execute Setup.exe da mídia de origem do System Center Configuration Manager.  

Depois que o site de nível superior concluir a atualização, você poderá iniciar a atualização de cada site filho. Conclua a atualização de cada site antes de começar a atualizar o próximo site  

Até que todos os sites na sua hierarquia sejam atualizados para System Center Configuration Manager, a hierarquia opera em um modo com versões mistas.  

Para obter informações sobre como executar a atualização, consulte [Atualizar sites](#bkmk_upgrade).  

### <a name="after-you-upgrade"></a>Após a atualização  
**Atualizar consoles do Configuration Manager autônomos**:  
Por padrão, quando você atualiza um site de administração central ou um site primário, a instalação também atualiza o console do Configuration Manager que está instalado no servidor do site. No entanto, você deve atualizar manualmente cada console instalado em um computador que não seja o do servidor do site.  

> [!TIP]  
>  Feche cada console aberto antes de iniciar a atualização.  

Para obter mais informações, veja [Instalar consoles do System Center Configuration Manager](../../../../core/servers/deploy/install/install-consoles.md).  

**Reconfigurar réplicas de banco de dados para pontos de gerenciamento em sites primários:**  
Ao utilizar réplicas de banco de dados para pontos de gerenciamento em sites primários, você deverá desinstalar as réplicas antes de atualizar o site. Depois de atualizar um site primário, reconfigure a réplica de banco de dados para pontos de gerenciamento.   
Para obter mais informações, veja  [Database replicas for management points for System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Reconfigurar as tarefas de manutenção de banco de dados desabilitadas antes da atualização:**  
Se você tiver desabilitado tarefas de manutenção do banco de dados ([Referência de tarefas de manutenção para o System Center Configuration Manager](../../../../core/servers/manage/reference-for-maintenance-tasks.md)) em um site antes da atualização, reconfigure-as no site usando as mesmas configurações que estavam em vigor antes da atualização.  

**Atualizar clientes**:  
Depois de todos os sites de atualização para o System Center Configuration Manager, planeje a atualização de clientes.  

Quando você atualiza um cliente, o software cliente atual é desinstalado e a nova versão do software cliente é instalada. Para atualizar clientes, você pode usar qualquer método ao qual o Configuration Manager dá suporte.  

> [!TIP]  
>  Quando você atualiza o site de nível superior de uma hierarquia, o pacote de instalação do cliente em cada ponto de distribuição na hierarquia também é atualizado. Quando você atualiza um site primário, o pacote de atualização de cliente disponível nesse site primário é atualizado.  

Para obter informações sobre como atualizar clientes existentes e como instalar novos clientes, consulte [Como atualizar clientes para computadores Windows no System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

##  <a name="bkmk_considerations"></a> Considerações para atualização  
**Ações automáticas**:  
Ao atualizar para o System Center Configuration Manager, as ações a seguir ocorrerão automaticamente:  

-   O site executa uma redefinição, que inclui a reinstalação de todas as funções do sistema de site.  
-   Se o site for de nível superior em uma hierarquia, ele atualizará o pacote de instalação do cliente em cada ponto de distribuição na hierarquia. O site também atualiza as imagens de inicialização padrão para usar a nova versão do Windows PE incluída no Kit de Avaliação e Implantação do Windows 10. No entanto, a atualização não atualizará a mídia existente para uso com a implantação da imagem.  
-   Se for um site primário, ele atualizará o pacote de atualização do cliente para esse site.  

**Ações manuais do usuário administrativo após uma atualização**   
Depois de atualizar um site, verifique se as ações a seguir são executadas:  

-   Verificar se os clientes atribuídos a cada site primário estão atualizados e instalar o software cliente da nova versão  
-   Atualize todos os consoles do Configuration Manager que se conectam ao site e que são executados em computadores remotos do servidor do site  
-   Nos sites primários nos quais você usa réplicas de banco de dados para pontos de gerenciamento, reconfigurar as réplicas de banco de dados  
-   Depois que o site for atualizado, você deve atualizar manualmente a mídia física como arquivos ISO para CDs e DVDs ou unidades flash USB, ou então a mídia pré-configurada usada para implantações do Windows To Go ou oferecida a fornecedores de hardware. Embora a atualização do site atualize as imagens de inicialização padrão, ela não é capaz de atualizar esses arquivos de mídia ou dispositivos usados como externos para Configuration Manager  
-   Planeje atualizar imagens de inicialização não padrão quando não necessitar da versão original (antiga) do Windows PE.  

**Ações que afetam as configurações e definições**   
Quando um site é atualizado para o System Center Configuration Manager, algumas definições e configurações não permanecem após a atualização ou são definidas com uma nova configuração padrão. A tabela a seguir inclui configurações que não permanecem, ou são alteradas, e fornece detalhes para ajudá-lo a planejá-las durante uma atualização de site:  

-   **Centro de Software:**  
    Os itens do Centro de Software a seguir são redefinidos para seus valores padrão:  
    -   **Informações de trabalho** é redefinido para horário comercial das **5h** às **22h** , de segunda-feira a sexta-feira.  
    -   O valor para **Manutenção do computador** é definido para **Suspender atividades do Centro de Software quando meu computador estiver no modo de apresentação**.  
    -   O valor para **Controle remoto** é definido para o valor nas configurações do cliente atribuídas ao computador.  
-   **Agendamentos de resumo de atualização de software:**  
     Os agendamentos personalizados de resumo para atualizações de software ou grupos de atualização de software são redefinidos para o valor padrão de 1 hora. Concluída a atualização, redefina os valores personalizados de resumo para a frequência necessária.  

##  <a name="bkmk_test"></a> Testar a atualização de banco de dados do site  
As informações a seguir se aplicarão somente quando você estiver atualizando uma versão anterior como o System Center 2012 Configuration Manager para o System Center Configuration Manager.

Para atualizar um site, teste uma cópia do banco de dados do site para a atualização.  

Para testar o banco de dados para uma atualização, primeiro restaure uma cópia do banco de dados do site para uma instância do SQL Server que não hospede um site do Configuration Manager. A versão do SQL Server usada para hospedar a cópia do banco de dados deve ser uma versão do SQL Server com suporte pelo Configuration Manager, que é a origem da cópia do banco de dados.  

Em seguida, após restaurar o banco de dados do site, no computador do SQL Server, execute a Instalação do Configuration Manager da pasta de mídia de origem do System Center Configuration Manager com a opção de linha de comando **/TESTDBUPGRADE**.  

-   Para obter informações sobre como criar e restaurar um backup de um banco de dados do site, consulte [Opções de linha de comando para instalação](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  
-   Para obter informações sobre a opção de linha de comando **/TESTDBUPGRADE**, veja a tabela em [Opções de linha de comando para instalação](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  
-   Para obter informações sobre as versões do SQL Server com suporte, consulte o tópico [Suporte para versões do SQL Server para o System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

> [!TIP]  
>  Se você integrar o Microsoft Intune com o Configuration Manager:  
>   
>  Quando você executa uma atualização de banco de dados de teste na cópia do banco de dados do site que tem 5 dias ou mais, você poderá receber uma das seguintes mensagens:  
>   
>  -   AVISO: a atualização forçará a sincronização completa com a nuvem.  
>  -   ERRO: a atualização do banco de dados forçará uma sincronização completa com a nuvem.  
>   
> Ambos podem ser ignorados durante o teste de uma atualização de banco de dados, pois não indicam uma falha ou problema com a atualização de teste. Em vez disso, eles indicam que, durante a atualização em si, dados do grupo de replicação de banco de dados de **Nuvem** podem ser sincronizados com Microsoft Intune.  

Use o procedimento a seguir em cada site de administração central e no site primário que planeja atualizar.  

#### <a name="to-test-a-site-database-for-upgrade"></a>Para testar um banco de dados do site para atualização  

1.  Faça uma cópia do banco de dados do site e, em seguida, restaure essa cópia para uma instância do SQL Server que use a mesma edição do seu banco de dados do site e que não hospede um site do Configuration Manager. Por exemplo, se o banco de dados do site for executado em uma instância do Enterprise Edition do SQL Server, verifique se você restaurou o banco de dados para uma instância do SQL Server que também executa o Enterprise Edition do SQL Server.  

2.  Após restaurar a cópia do banco de dados, execute a Instalação da mídia de origem para o System Center Configuration Manager. Ao executar a Instalação, use a opção de linha de comando **/TESTDBUPGRADE** . Se a instância do SQL Server que hospeda a cópia do banco de dados não for a instância padrão, será necessário fornecer também os argumentos da linha de comando para identificar a instância que hospeda a cópia do banco de dados do site.  

     Por exemplo, você planeja atualizar um banco de dados do site com o nome de banco de dados SMS_ABC. Você restaura uma cópia desse banco de dados do site para uma instância suportada do SQL Server com o nome de instância DBTest. Para testar uma atualização dessa cópia do banco de dados do site, use a linha de comando a seguir: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     Você pode encontrar Setup.exe no seguinte local na mídia de origem do System Center Configuration Manager: **SMSSETUP\BIN\X64**.  

3.  Na instância do SQL Server em que você executa o teste de atualização do banco de dados, monitore o arquivo ConfigMgrSetup.log na raiz da unidade do sistema para verificar o andamento e o êxito:  

    -   Se ocorrer falha na atualização do teste, resolva os problemas relacionados à falha de atualização do banco de dados do site, crie um novo backup do banco de dados do site e, em seguida, teste a atualização da nova cópia.  
    -   Depois que o processo for concluído com êxito, exclua a cópia do banco de dados.  

        > [!NOTE]  
        >  Não é possível restaurar a cópia do banco de dados do site, utilizada para a atualização de teste, para uso como um banco de dados do site em qualquer site.  

Após atualizar com êxito uma cópia do banco de dados do site, prossiga com a atualização do site do Configuration Manager e do seu banco de dados.  

##  <a name="bkmk_upgrade"></a> Atualizar sites  
Após concluir as configurações de pré-atualização do seu site, teste a atualização do banco de dados do site em uma cópia deste e baixe os arquivos de pré-requisito e os pacotes de idioma da versão do service pack que planeja instalar, você estará pronto para atualizar o seu site do Configuration Manager.  

Ao atualizar um site de uma hierarquia, você atualiza primeiro o site de nível superior da hierarquia. Esse site de nível superior é um site de administração central ou um site primário autônomo. Após a conclusão da atualização de um site de administração central, você pode atualizar sites primários filhos na ordem que desejar. Após atualizar um site primário, você pode atualizar os sites secundários filho desse site ou atualizar os sites primários adicionais antes de atualizar sites secundários.  

Para atualizar um site de administração central ou um site primário, execute a Instalação da mídia de origem do System Center Configuration Manager. No entanto, não execute a Instalação para atualizar sites secundários. Em vez disso, use o console do Configuration Manager para atualizar um site secundário após concluir a atualização do seu site primário pai.  

Para atualizar um site, feche o console do Configuration Manager que está instalado no seu servidor até que a atualização deste seja concluída. Além disso, feche cada console do Configuration Manager executado em outros computadores que não sejam o do servidor do site. Você pode reconectar o console após a conclusão da atualização do site. No entanto, até que você faça a atualização de um console do Configuration Manager para a nova versão do Configuration Manager, esse console não poderá exibir alguns objetos e informações disponíveis na nova versão do Configuration Manager.  

Use os procedimentos a seguir para atualizar um relatório dos sites do Configuration Manager:  

#### <a name="to-upgrade-a-central-administration-site-or-primary-site"></a>Para atualizar um site de administração central ou site primário  

1.  Verifique se o usuário que executa a Instalação tem os seguintes direitos de segurança:  

    -   Direitos do Administrador Local no computador servidor do site.  
    -   Direitos do Administrador Local no servidor de banco de dados do site remoto para o site, se for remoto.    </br></br>

2.  No computador do servidor do site, abra o Windows Explorer e navegue até **&lt;ConfigMgSourceMedia\>\SMSSETUP\BIN\X64**.  

3.  Clique duas vezes no **Setup.exe**. O Assistente de Instalação do Configuration Manager é aberto.  

4.  Na página **Antes de Começar** , clique em **Avançar**.  

5.  Na página **Guia de Introdução** , selecione **Atualizar este site do Configuration Manager**e, em seguida, clique em **Próximo**.  

6.  Na página **Chave do Produto** , clique em **Próximo**.  

     Se você já tiver instalado o Configuration Manager Evaluation, selecione **Instalar a edição licenciada deste produto** e, em seguida, insira a chave do produto (Product Key) para que a instalação completa do Configuration Manager converta o site para a versão completa.  

     Começando com a versão de outubro de 2016 da mídia de linha de base da versão 1606 do System Center Configuration Manager, você pode especificar a data de validade do contrato do Software Assurance. Você também tem a opção de especificar a **Data de vencimento do Software Assurance** do seu contrato de licença como um lembrete conveniente dessa data. Se não inserir essa informação durante a instalação, você poderá especificá-la posteriormente no console do Configuration Manager.

     >  [!NOTE]   
     >  A Microsoft não valida a data de validade inserida e não usará essa data para validação da licença.  No entanto, você pode usá-la como um lembrete da data de vencimento. Isso é útil porque o Configuration Manager verifica periodicamente se há novas atualizações de software oferecidas online. O status de licença do Software Assurance deve estar atualizado para que você esteja qualificado para usar essas atualizações adicionais.    

     Para mais informações, consulte [Licenciamento e branches do System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

7.  Na página **Termos de Licença para Software Microsoft** , leia e aceite os termos de licença e clique em **Próximo**.  

8.  Na página **Licenças de Pré-requisito** , leia e aceite os termos de licença do software de pré-requisitos e clique em **Próximo**. A Instalação baixa e instala automaticamente o software nos clientes ou sistemas do site, quando necessário. Marque todas as caixas de seleção para avançar para a próxima página.  

9. Na página **Downloads de Pré-requisitos** , especifique se a Instalação baixa os arquivos de pré-requisitos redistribuíveis mais recentes, os pacotes de idioma e as atualizações de produto mais recentes da Internet, ou utilize os arquivos baixados anteriormente e, em seguida, clique em **Próximo**. Se você tiver baixado os arquivos usando o Downloader de Instalação, selecione **Usar arquivos baixados anteriormente** e especifique a pasta de download. Para obter mais informações, consulte [Downloader de Instalação](/sccm/core/servers/deploy/install/setup-downloader).

    > [!NOTE]  
    >  Ao usar arquivos baixados anteriormente, verifique se o caminho para a pasta de download contém a versão mais recente dos arquivos.  

10. Na página **Seleção do Idioma do Servidor** , exiba a lista de idiomas atualmente instalados para o site. Selecione os idiomas adicionais disponíveis nesse site para o console do Configuration Manager e para relatórios, ou limpe os idiomas para os quais não deseja mais dar suporte nesse site, em seguida, clique em **Próximo**. Por padrão, o idioma inglês é selecionado e não pode ser removido.  

    > [!IMPORTANT]  
    >  Cada versão do Configuration Manager não pode usar pacotes de idiomas de uma versão anterior do Configuration Manager. Para habilitar o suporte a idiomas no site do Configuration Manager que você atualizou, deve usar a versão do pacote de idiomas da nova versão. Por exemplo, durante a atualização do System Center 2012 Configuration Manager para o System Center Configuration Manager, se a versão do System Center Configuration Manager de um pacote de idiomas não estiver disponível com os arquivos de pré-requisitos baixados, o suporte para esse idioma não poderá ser instalado.  

11. Na página **Seleção do Idioma do Cliente** , exiba a lista de idiomas atualmente instalados para o site. Selecione os idiomas adicionais disponíveis nesse site para os computadores cliente ou limpe os idiomas para os quais não deseja mais oferecer suporte nesse site. Especifique se deseja habilitar todos os idiomas do cliente para clientes de dispositivos móveis e, em seguida, clique em **Próximo**. Por padrão, o idioma inglês é selecionado e não pode ser removido.  

    > [!IMPORTANT]  
    >  Cada versão do Configuration Manager não pode usar pacotes de idiomas de uma versão anterior do Configuration Manager. Para habilitar o suporte a idiomas no site do Configuration Manager que você atualizou, deve usar a versão do pacote de idiomas da nova versão. Por exemplo, durante a atualização do System Center 2012 Configuration Manager para o System Center Configuration Manager, se a versão do System Center Configuration Manager de um pacote de idiomas não estiver disponível com os arquivos de pré-requisitos baixados, o suporte para esse idioma não poderá ser instalado.  

12. Na página **Resumo das Configurações** , clique em **Próximo** para iniciar o Verificador de Pré-requisitos e verificar a preparação do servidor para a atualização do site.  

13. Na página **Verificação de Instalação de Pré-requisitos** , se não houver problemas listados, clique em **Próximo** para atualizar o site e as funções do sistema do site. Se o Verificador de Pré-requisitos encontrar um problema, clique em um item da lista para ver os detalhes sobre como solucioná-lo. Solucione todos os itens da lista que contém status de **Erro** antes de continuar com a Instalação. Após resolver o problema, clique em **Executar Verificação** para reiniciar a verificação de pré-requisito. Você também pode abrir o arquivo ConfigMgrPrereq.log na raiz da unidade do sistema para verificar os resultados do Verificador de Pré-requisitos. O arquivo de log pode conter informações adicionais que não são exibidas na interface do usuário. Para obter uma lista das regras e descrições dos pré-requisitos de instalação, consulte [Prerequisite Checker](/sccm/core/servers/deploy/install/list-of-prerequisite-checks) (Verificador de pré-requisitos).  

Na página **Atualizar** , a Instalação exibe o status do andamento geral. Quando a instalação do servidor do site principal e do sistema de site for concluída, feche o assistente. A configuração do site continuará em segundo plano.  

#### <a name="to-upgrade-a-secondary-site"></a>Para atualizar um site secundário  

1.  Verifique se o usuário administrativo que executa a Instalação tem os seguintes direitos de segurança:  

    -   Direitos do Administrador Local no computador do site secundário  
    -   Função de segurança de Administrador de Infraestrutura ou de Administrador Completo no site primário pai  
    -   Direitos do administrador do sistema no banco de dados do site secundário  
    </br>
2.  No console do Configuration Manager, clique em **Administração**.  

3.  No espaço de trabalho **Administração** , expanda **Configuração do Site**e clique em **Sites**.  

4.  Selecione o site secundário que deseja atualizar e, em seguida, na guia **Início** , no grupo **Site** , clique em **Atualizar**.  

5.  Clique em **Sim** para confirmar a decisão e para iniciar a atualização do site secundário.  

A atualização do site secundário é feita em segundo plano. Após a conclusão da atualização, confirme o status no console do Configuration Manager. Para confirmar o status, selecione o servidor do site secundário e, em seguida, na guia **Início** , no grupo **Site** , clique em **Mostrar Status da Instalação**.  

##  <a name="BKMK_PostUpgrade"></a> Executar tarefas pós-atualização  
Após atualizar um site para um novo service pack, talvez seja necessário concluir tarefas adicionais para finalizar a atualização ou reconfigurar o site. Essas tarefas podem incluir a atualização de clientes do Configuration Manager ou consoles do Configuration Manager, a reabilitação de réplicas de banco de dados para pontos de gerenciamento ou a restauração de configurações para a funcionalidade do Configuration Manager usada e que não persiste após a atualização do service pack.  

**Problemas conhecidos para sites secundários:**  
- **Ao atualizar para a versão 1511:** para garantir que os clientes em sites secundários possam localizar o ponto de gerenciamento do site secundário (ponto de gerenciamento proxy), adicione manualmente o ponto de gerenciamento aos grupos de limites que também incluem os pontos de distribuição no site secundário.  

- **Ao atualizar para a versão 1606 ou posterior:** os pontos de gerenciamento proxy são adicionados automaticamente aos grupos de limites que incluem pontos de distribuição no site secundário.
