---
title: Atualizar para o Configuration Manager
description: Conheça as etapas para executar uma atualização in-loco com êxito de um site e hierarquia que executa o System Center 2012 Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 86e41e932995abc47b6229ce3405f810d75b992b
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159290"
---
# <a name="upgrade-to-configuration-manager"></a>Atualizar para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Faça a atualização in-loco para o Branch Atual do Configuration Manager de um site e uma hierarquia que executa o System Center 2012 Configuration Manager. Antes de atualizar do System Center 2012 Configuration Manager, é necessário preparar os sites. Essa preparação exige que você remova configurações específicas que podem impedir a atualização bem-sucedida. Em seguida, siga a sequência de atualização quando houver mais de um único site envolvido.  

> [!TIP]  
> Ao gerenciar a infraestrutura do site e da hierarquia do Configuration Manager, os termos *upgrade*, *update* e *install* são usados para descrever três conceitos separados. Para saber como cada termo é usado, consulte [About upgrade, update, and install](/sccm/core/understand/upgrade-update-install) (Sobre upgrade, atualização e instalação).



## <a name="bkmk_path"></a> Caminhos de atualização in-loco  

As opções a seguir são os caminhos de atualização in-loco com suporte no momento:


### <a name="upgrade-to-version-1902"></a>Atualizar para a versão 1902

Quando você tiver a mídia de linha de base da versão 1902, poderá atualizar os seguintes itens para uma versão totalmente licenciada do System Center Configuration Manager, versão 1902:   
- Uma instalação de avaliação do System Center Configuration Manager, versão 1902
- System Center 2012 Configuration Manager com Service Pack 1
- System Center 2012 Configuration Manager com Service Pack 2
- System Center 2012 R2 Configuration Manager
- System Center 2012 R2 Configuration Manager com Service Pack 1

### <a name="upgrade-to-version-1802"></a>Atualizar para a versão 1802
Quando você tiver a mídia de linha de base da versão 1802, atualize o seguinte para uma versão totalmente licenciada do System Center Configuration Manager versão 1802:   
- Uma instalação de avaliação do System Center Configuration Manager versão 1802
- System Center 2012 Configuration Manager com Service Pack 1
- System Center 2012 Configuration Manager com Service Pack 2
- System Center 2012 R2 Configuration Manager
- System Center 2012 R2 Configuration Manager com Service Pack 1

### <a name="upgrade-to-version-1606"></a>Atualizar para a versão 1606
Em 15 de dezembro de 2016, a mídia de linha de base para a versão 1606 foi relançada para adicionar suporte a cenários adicionais de atualização. Essa versão dá suporte para a atualização das seguintes atualizações para uma versão totalmente licenciada do System Center Configuration Manager, versão 1606:  
- Uma instalação de avaliação do System Center Configuration Manager versão 1606
- Uma instalação de versão Release Candidate do System Center Configuration Manager  
- System Center 2012 Configuration Manager com Service Pack 1  
- System Center 2012 Configuration Manager com Service Pack 2  
- System Center 2012 R2 Configuration Manager sem service pack
- System Center 2012 R2 Configuration Manager com Service Pack 1  

Se usar a mídia de linha de base versão 1606 baixada antes de 15 de dezembro de 2016, você poderá atualizar apenas os seguintes itens para uma versão totalmente licenciada do System Center Configuration Manager versão 1606:
- Uma instalação de avaliação do System Center Configuration Manager versão 1606
- System Center 2012 Configuration Manager com Service Pack 2
- System Center 2012 R2 Configuration Manager com Service Pack 1

Confira mais informações sobre o uso da versão 1606 em [Peguntas frequentes sobre os Branches e o licenciamento do Configuration Manager](/sccm/core/understand/product-and-licensing-faq).

> [!TIP]  
>  Ao atualizar de uma versão do System Center 2012 Configuration Manager para o Branch Atual, talvez você possa simplificar o processo de atualização. Para obter mais informações, consulte:  
>   
> - [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#bkmk_Baselines)  
> - [A pasta CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder)  


### <a name="unsupported-paths"></a>Caminhos sem suporte

Não há suporte para os seguintes caminhos:

- Não há suporte para atualização de um Technical Preview Branch para uma instalação totalmente licenciada. Uma versão Technical Preview só poderá ser atualizada para uma versão posterior da Technical Preview.  

- Não há suporte para a migração de uma versão Technical Preview para uma versão totalmente licenciada.  



##  <a name="bkmk_checklist"></a> Listas de verificação de atualização  

As listas de verificação a seguir podem ajudá-lo a planejar uma atualização bem-sucedida para o Configuration Manager.  


### <a name="before-you-upgrade"></a>Antes de atualizar  

Leia estas etapas antes de fazer a atualização para o Configuration Manager.


#### <a name="review-your-system-center-2012-configuration-manager-environment"></a>Revisar o ambiente do System Center 2012 Configuration Manager
Resolva os problemas conforme os detalhes constantes no artigo do Suporte da Microsoft a seguir: [os clientes do Configuration Manager são reinstalados a cada cinco horas por causa de uma tarefa recorrente de repetição, o que pode causar uma atualização acidental do cliente](https://support.microsoft.com/help/4018655).

#### <a name="make-sure-your-environment-meets-the-supported-configurations"></a>Verificar se o ambiente atende às configurações com suporte

- Examine a versão do sistema operacional do servidor em uso para hospedar as funções do sistema de sites:  

    - Alguns sistemas operacionais mais antigos que têm suporte no System Center 2012 Configuration Manager não têm suporte no Branch Atual do Configuration Manager. Antes de atualizar, remova as funções do sistema de site nessas versões do sistema operacional. Para obter mais informações, confira [Sistemas operacionais com suporte para servidores do sistema de sites](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).   

    - O verificador de pré-requisitos do Configuration Manager não verifica os pré-requisitos das funções do sistema de sites no servidor do site ou em sistemas de sites remotos  

- Examine os pré-requisitos necessários para cada computador que hospeda uma função do sistema de sites. Por exemplo, para implantar um sistema operacional, o Configuration Manager usa o Windows ADK (Kit de Avaliação e Implantação do Windows 10). Antes de executar a instalação, você deve baixar e instalar o Windows 10 ADK no servidor do site e em cada computador que executa uma instância do Provedor de SMS.  

Confira mais informações a respeito das plataformas com suporte e as configurações de pré-requisito em [Configurações com suporte](/sccm/core/plan-design/configs/supported-configurations).  

Confira mais informações sobre o uso do Windows ADK com o Configuration Manager em [Requisitos de infraestrutura para implantação do sistema operacional](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

#### <a name="review-the-site-and-hierarchy-status-and-verify-that-there-are-no-unresolved-issues"></a>Examinar o status do site e da hierarquia e verificar se há problemas que não foram resolvidos
Antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, do servidor de banco de dados do site e das funções do sistema de site que estão instalados em computadores remotos. Uma atualização de site pode falhar em razão de problemas operacionais existentes.  

#### <a name="install-all-applicable-critical-updates-for-operating-systems-on-computers-that-host-the-site-the-site-database-server-and-remote-site-system-roles"></a>Instalar todas as atualizações críticas aplicáveis dos sistemas operacionais nos computadores que hospedam o site, o servidor do banco de dados do site e as funções do sistema de sites remoto
Antes de atualizar um site, instale todas as atualizações críticas para cada sistema de site aplicável. Se uma atualização instalada precisar de uma reinicialização, reinicie os computadores aplicáveis antes de iniciar a atualização do service pack.  

#### <a name="uninstall-the-site-system-roles-not-supported-by-configuration-manager"></a>Desinstalar as funções do sistema de sites sem suporte pelo Configuration Manager
As seguintes funções do sistema de site não são mais usadas no Configuration Manager. Desinstale-as antes de atualizar do System Center 2012 Configuration Manager:  

- Ponto de Gerenciamento Fora de Banda  

- Ponto do Validador da Integridade do Sistema  

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Desabilite réplicas de banco de dados para pontos de gerenciamento em sites primários
O Configuration Manager não pode atualizar um site primário que tenha uma réplica de banco de dados para pontos de gerenciamento. Desabilite a replicação de banco de dados antes de você:  

- Criar um backup do banco de dados do site para testar a atualização do banco de dados  

- Atualizar o site de produção para o System Center Configuration Manager  

Para obter mais informações, consulte os seguintes artigos:  

- System Center 2012 Configuration Manager: [Configurar as réplicas de banco de dados para pontos de gerenciamento](/sccm/core/servers/deploy/configure/database-replicas-for-management-points#BKMK_DBReplica_Config)  

- Configuration Manager, Branch Atual: [Réplicas de banco de dados para pontos de gerenciamento](/sccm/core/servers/deploy/configure/database-replicas-for-management-points)  

#### <a name="reconfigure-software-update-points-that-use-nlb"></a>Reconfigurar os pontos de atualização de software que usam NLB
O Configuration Manager não pode atualizar um site que usa um cluster NLB (Balanceamento de Carga de Rede) para hospedar pontos de atualização de software.  

Se você usar clusters NLB para pontos de atualização de software, use o PowerShell para remover do cluster NLB. (A partir do System Center 2012 Configuration Manager SP1, não há nenhuma opção no console do Configuration Manager para configurar um cluster NLB)  

#### <a name="disable-all-site-maintenance-tasks-at-each-site-for-the-duration-of-that-sites-upgrade"></a>Desabilitar todas as tarefas de manutenção do site, em cada site, durante a atualização do site
Antes de atualizar para o Configuration Manager, desabilite todas as tarefas de manutenção de site que possam ser executadas durante o período em que o processo de atualização estiver ativo. Isso inclui, entre outras, as seguintes tarefas:  

- Servidor do Site de Backup  
- Excluir Operações Antigas do Cliente  
- Excluir Dados Antigos de Descoberta  

Se uma tarefa de manutenção de banco de dados do site for executada durante o processo de atualização, a atualização do site poderá falhar.  

Para desabilitar uma tarefa, registre o agendamento da tarefa para que você possa restaurar sua configuração depois de concluir a atualização do site. 

Confira mais informações sobre as tarefas de manutenção de site nos seguintes artigos:  

- System Center 2012 Configuration Manager: [Planejando as operações de site](/sccm/core/plan-design/hierarchy/plan-for-the-site-database)  

- Configuration Manager, Branch Atual: [Referência para tarefas de manutenção](/sccm/core/servers/manage/reference-for-maintenance-tasks)  

#### <a name="run-setup-prerequisite-checker"></a>Executar o verificador de pré-requisitos de instalação
Antes de atualizar um site, execute o **Verificador de Pré-requisitos** independentemente da Instalação, para validar que seu site atende aos pré-requisitos. Posteriormente, ao atualizar o site, o Verificador de pré-requisitos será executado novamente.  

Se você usar a mídia de linha de base para a versão 1606, de outubro de 2016, a verificação de pré-requisitos independente avaliará o site quanto à atualização para o Branch Atual e para o LTSB (Branch de Manutenção em Longo Prazo) do Configuration Manager. Como o LTSB não oferece suporte a alguns recursos, você poderá ver entradas no *ConfigMgrPrereq.log* semelhantes aos seguintes exemplos:
- `INFO: The site is a LTSB edition.`
- `Unsupported site system role 'Asset Intelligence synchronization point' for the LTSB edition;    Error;    Configuration Manager has detected that the 'Asset Intelligence synchronization point' is installed. Asset Intelligence is not supported on the LTSB edition. You must uninstall the Asset Intelligence synchronization point site system role before you can continue.`

Se você planeja atualizar para o Branch Atual, os erros da edição LTSB poderão ser ignorados com segurança. Eles se aplicam apenas se você planeja atualizar para o LTSB.

Posteriormente, quando você executar a Instalação do Configuration Manager para fazer a atualização, a verificação de pré-requisitos será executada novamente. Ela avaliará seu site com base no Branch do Configuration Manager que você optou instalar (Branch Atual ou LTSB). Se optar por atualizar para o Branch Atual, a inicialização não executará a verificação de recursos que não têm suporte no LTSB.

Confira mais informações em [Verificador de pré-requisitos](/sccm/core/servers/deploy/install/prerequisite-checker) e a [Lista de verificações de pré-requisitos](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).  

#### <a name="download-prerequisite-files-and-redistributable-files-for-configuration-manager"></a>Baixar os arquivos de pré-requisito e os arquivos redistribuíveis do Configuration Manager
Use a **Ferramenta de download de instalação** para baixar os arquivos redistribuíveis que são pré-requisitos, os pacotes de idiomas e as atualizações de produto mais recentes do Configuration Manager.  

Para obter informações, consulte [Ferramenta de download de instalação](/sccm/core/servers/deploy/install/setup-downloader).  

#### <a name="plan-to-manage-server-and-client-languages"></a>Planejar para gerenciar idiomas do servidor e do cliente
Quando você atualiza um site, a atualização do site instala somente as versões de pacote de idiomas que você seleciona durante a atualização.  

- A instalação examina a configuração de idioma atual de seu site. Ela identifica os pacotes de idiomas disponíveis na pasta em que você armazena os arquivos de pré-requisitos baixados anteriormente.  

- Você pode confirmar a seleção do servidor atual e os pacotes de idiomas do cliente ou alterar as seleções para adicionar ou remover suporte a idiomas.  

- Somente os pacotes de idiomas que estiverem disponíveis quando você executar a Instalação poderão ser selecionados.  

> [!NOTE]  
> Não é possível usar os pacotes de idiomas do System Center 2012 Configuration Manager para habilitar idiomas para um site do Branch Atual do Configuration Manager.  

Confira mais informações sobre pacotes de idiomas em [Pacotes de idioma](/sccm/core/servers/deploy/install/language-packs).  

#### <a name="review-considerations-for-site-upgrades"></a>Examinar a lista de considerações para atualizações do site
Quando você atualiza um site, alguns recursos e configurações são redefinidos para uma configuração padrão. Para ajudá-lo a se preparar para essas alterações e outras relacionadas, confira [Considerações para atualização](#bkmk_considerations).  

#### <a name="create-a-backup-of-the-site-database-at-the-central-administration-site-and-primary-sites"></a>Criar um backup do banco de dados do site no site de administração central e nos sites primários
Antes de atualizar um site, faça o backup do banco de dados do site para ter certeza de que tenha feito um backup bem-sucedido para ser usado em uma recuperação de desastre.  

Para obter mais informações, veja [Backup e recuperação](/sccm/core/servers/manage/backup-and-recovery).  

#### <a name="back-up-a-customized-configurationmof-file"></a>Fazer backup do arquivo Configuration.mof personalizado
Se você usar o arquivo Configuration.mof personalizado para definir as classes de dados a serem usadas com o inventário de hardware, crie um backup desse arquivo. Após a atualização, restaure esse arquivo em seu site. Para obter informações, confira [Como estender o inventário de hardware](/sccm/core/clients/manage/inventory/extend-hardware-inventory).  

#### <a name="test-the-database-upgrade-process-on-a-copy-of-the-most-recent-site-database-backup"></a>Testar o processo de atualização do banco de dados em uma cópia do backup mais recente do banco de dados do site
Antes de atualizar um site de administração central do Configuration Manager ou site primário, teste o processo de atualização do banco de dados do site em uma cópia do banco de dados do site.  

- Teste o processo de atualização do banco de dados do site. Quando você atualiza um site, o banco de dados do site pode ser modificado.  

- Embora o teste da atualização do banco de dados não seja obrigatório, ele pode identificar problemas na atualização antes que seu banco de dados de produção seja afetado  

- Uma atualização do banco de dados do site com falha pode deixar o banco de dados do site inoperante e pode requerer uma recuperação de site para restaurar a funcionalidade  

- Embora o banco de dados do site seja compartilhado entre sites em uma hierarquia, planeje testar o banco de dados em cada site aplicável antes de atualizar esse site  

- Se você usar réplicas de banco de dados para pontos de gerenciamento em um site primário, desabilite a replicação antes de criar o backup do banco de dados do site  

O Configuration Manager não oferece suporte ao backup de sites secundários nem ao teste de atualização de um banco de dados do site secundário.  

Não há suporte para executar um teste da atualização do banco de dados no banco de dados do site de produção. Isso atualiza o banco de dados do site e pode deixar o site inoperante.  

Para obter mais informações, consulte [Testar a atualização de banco de dados do site](#bkmk_test).  

#### <a name="restart-the-site-server-and-each-computer-that-hosts-a-site-system-role"></a>Reiniciar o servidor do site e cada computador que hospeda uma função do sistema de sites
Faça isso para garantir que não haja nenhuma ação pendente de uma instalação recente de atualizações ou pré-requisitos.  

#### <a name="upgrade-sites"></a>Atualizar sites
Iniciando no site de nível superior na hierarquia, execute o Setup.exe na mídia de origem do Configuration Manager.  

Depois que o site de nível superior concluir a atualização, você poderá iniciar a atualização de cada site filho. Conclua a atualização de cada site antes de começar a atualizar o próximo site.  

Até que todos os sites na sua hierarquia sejam atualizados para o Configuration Manager, a hierarquia opera em um modo com versões mistas.  

Para obter informações sobre como executar a atualização, consulte [Atualizar sites](#bkmk_upgrade).  


### <a name="after-you-upgrade"></a>Após a atualização  

Examine estas etapas antes de realizar a atualização para o Configuration Manager.

#### <a name="upgrade-stand-alone-configuration-manager-consoles"></a>Atualizar os consoles autônomos do Configuration Manager
Por padrão, quando você atualiza um site de administração central ou um site primário, a instalação também atualiza o console do Configuration Manager que está instalado no servidor do site. Atualize manualmente cada console que está instalado em um computador que não seja o servidor do site.  

> [!TIP]  
> Feche cada console aberto antes de iniciar a atualização.  

Para saber mais, veja [Instalar consoles do Configuration Manager](/sccm/core/servers/deploy/install/install-consoles).  

#### <a name="reconfigure-database-replicas-for-management-points-at-primary-sites"></a>Reconfigurar as réplicas de banco de dados para pontos de gerenciamento em sites primários
Se você usar réplicas de banco de dados para pontos de gerenciamento em sites primários, desinstale as réplicas de banco de dados antes de atualizar o site. Depois de atualizar um site primário, reconfigure a réplica de banco de dados para pontos de gerenciamento.   

Para obter mais informações, consulte [Réplicas de banco de dados para pontos de gerenciamento](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).  

#### <a name="reconfigure-any-database-maintenance-tasks-you-disabled-before-the-upgrade"></a>Reconfigurar todas as tarefas de manutenção de banco de dados desabilitadas antes da atualização
Se você tiver desabilitado as [tarefas de manutenção](/sccm/core/servers/manage/reference-for-maintenance-tasks) do banco de dados no site antes da atualização, reconfigure tais tarefas no site usando as mesmas configurações que estavam em vigor antes da atualização.  

#### <a name="upgrade-clients"></a>Atualizar clientes
Depois que todos os sites estiverem atualizados para o Configuration Manager, planeje a atualização dos clientes.  

Quando você atualiza um cliente, o software cliente atual é desinstalado e a nova versão do software cliente é instalada. Para atualizar clientes, você pode usar qualquer método ao qual o Configuration Manager dá suporte.  

> [!TIP]  
> Quando você atualiza o site de nível superior de uma hierarquia, o pacote de instalação do cliente em cada ponto de distribuição na hierarquia também é atualizado. Quando você atualiza um site primário, o pacote de atualização de cliente disponível nesse site primário é atualizado.  

Para obter mais informações, consulte [Como atualizar clientes em computadores Windows](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers).  



## <a name="bkmk_considerations"></a> Considerações para atualização  


### <a name="automatic-actions"></a>Ações automáticas

Ao atualizar para o Configuration Manager, as ações a seguir ocorrerão automaticamente:  

- O site é reiniciado. Essa ação inclui a reinstalação de todas as funções do sistema de site.  

- Se o site for de nível superior em uma hierarquia, ele atualizará o pacote de instalação do cliente em cada ponto de distribuição na hierarquia. O site também atualiza as imagens de inicialização padrão para usar a nova versão do Windows PE que está incluída no Kit de Avaliação e Implantação do Windows 10. No entanto, a atualização não atualizará a mídia existente para uso com a implantação da imagem.  

- Se for um site primário, ele atualizará o pacote de atualização do cliente para esse site.  


### <a name="manual-actions-after-an-upgrade"></a>Ações manuais após a atualização

Depois de atualizar o site, certifique-se de executar as ações a seguir:  

- Verifique se os clientes atribuídos a cada site primário atualizam e instalam a nova versão do cliente  

- Atualize todos os consoles do Configuration Manager que se conectam ao site e que são executados em computadores remotos do servidor do site  

- Nos sites primários nos quais você usa réplicas de banco de dados para pontos de gerenciamento, reconfigurar as réplicas de banco de dados  

- Depois que o site for atualizado, atualize manualmente as mídias físicas, como arquivos ISO, para CDs, DVDs ou pen drives. Isso também inclui as mídias em pré-teste oferecidas a fornecedores de hardware. A atualização do site atualiza as imagens de inicialização padrão; ela não é capaz de atualizar esses arquivos de mídia ou dispositivos usados externamente com o Configuration Manager.  

- Planeje a atualização das imagens de inicialização personalizadas quando você não necessitar da versão antiga do Windows PE.  


### <a name="actions-that-affect-configurations-and-settings"></a>Ações que afetam as configurações e as definições**   

Quando um site é atualizado para o Configuration Manager, algumas definições e configurações não permanecem depois da atualização. Algumas configurações são definidas com um novo padrão. A lista a seguir inclui algumas configurações que não são mantidas ou que são alteradas:  

- **Centro de Software**  
    Os itens do Centro de Software a seguir são redefinidos para seus valores padrão:  

    - **Informações de trabalho** é redefinido para horário comercial das **5h** às **22h** , de segunda-feira a sexta-feira.  

    - O valor para **Manutenção do computador** é definido para **Suspender atividades do Centro de Software quando meu computador estiver no modo de apresentação**.  
    
    - O valor para **Controle remoto** é definido para o valor nas configurações do cliente atribuídas ao computador.  

- **Agendamentos de resumo da atualização de software**: Os agendamentos personalizados de resumo para atualizações de software ou grupos de atualização de software são redefinidos para o valor padrão de 1 hora. Concluída a atualização, redefina os valores personalizados de resumo para a frequência necessária.  



## <a name="bkmk_test"></a> Testar a atualização de banco de dados do site  

As informações a seguir se aplicarão somente quando você estiver atualizando uma versão anterior, como o System Center 2012 Configuration Manager, para o Branch Atual do Configuration Manager.

Para atualizar um site, teste uma cópia do banco de dados do site para a atualização.  

Para testar o banco de dados quanto a uma atualização, primeiro restaure a cópia do banco de dados do site para uma instância do SQL Server que não hospede um site do Configuration Manager. A versão do SQL Server que você usa para hospedar a cópia do banco de dados deve ter suporte no Configuration Manager.  

Após restaurar o banco de dados do site, no computador do SQL Server, execute a Instalação do Configuration Manager na pasta de mídia de origem do Configuration Manager. Use a opção de linha de comando `/TESTDBUPGRADE`.  

Para obter mais informações, consulte os seguintes artigos:

- [Fazer backup de um site do Configuration Manager](/sccm/core/servers/manage/backup-and-recovery)  

- [Opções de linha de comando para a Instalação](/sccm/core/servers/deploy/install/command-line-options-for-setup#bkmk_setup)  

- [Suporte para versões do SQL Server](/sccm/core/plan-design/configs/support-for-sql-server-versions)  

> [!TIP]  
> Se você integrar o Microsoft Intune com o Configuration Manager:  
>   
>  Quando você executa uma atualização de banco de dados de teste na cópia do banco de dados do site que tem 5 dias ou mais, você poderá receber uma das seguintes mensagens:  
>   
> - AVISO: a atualização forçará uma sincronização completa com a nuvem.  
> - ERRO: a atualização de banco de dados forçará uma sincronização completa com a nuvem.  
>   
> Ambos podem ser ignorados durante o teste da atualização do banco de dados. Eles não indicam falha ou problema na atualização de teste. Em vez disso, eles indicam que, durante a atualização em si, dados do grupo de replicação de banco de dados de **Nuvem** podem ser sincronizados com Microsoft Intune.  


### <a name="test-a-site-database-for-upgrade"></a>Testar o banco de dados de um site para atualização  

Use o procedimento a seguir em cada site de administração central e no site primário os quais planeja atualizar:  

1. Faça uma cópia do banco de dados do site. Em seguida, restaure essa cópia em uma instância do SQL Server que use a mesma edição que seu banco de dados do site e que não hospede um site do Configuration Manager. Por exemplo, se o banco de dados do site for executado em uma instância do Enterprise Edition do SQL Server, verifique se você restaurou o banco de dados para uma instância do SQL Server que também executa o Enterprise Edition do SQL Server.  

2. Após restaurar a cópia do banco de dados, execute a Instalação da mídia de origem para o Branch Atual do Configuration Manager. Ao executar a Instalação, use a opção de linha de comando `/TESTDBUPGRADE`. Se a instância do SQL Server que hospeda a cópia do banco de dados não for a instância padrão, forneça também os argumentos da linha de comando para identificar a instância que hospeda a cópia do banco de dados do site.  

    Por exemplo, você planeja atualizar um banco de dados do site com o nome de banco de dados SMS_ABC. Você restaura uma cópia desse banco de dados do site para uma instância suportada do SQL Server com o nome de instância DBTest. Para testar uma atualização dessa cópia do banco de dados do site, use a linha de comando a seguir: `Setup.exe /TESTDBUPGRADE DBtest\CM_ABC`  

    O setup.exe está no seguinte local na mídia de origem do Configuration Manager: `SMSSETUP\BIN\X64`  

3. Na instância do SQL Server em que você executa o teste de atualização do banco de dados, monitore o arquivo ConfigMgrSetup.log na raiz da unidade do sistema para verificar o andamento e o êxito:  

    - Se o teste de atualização falhar, solucione os problemas relacionados à falha de atualização do banco de dados do site. Em seguida, crie um novo backup do banco de dados do site e teste a atualização da nova cópia do banco de dados.  

    - Depois que o processo for concluído com êxito, exclua a cópia do banco de dados.  

        > [!NOTE]  
        > Não há suporte para a restauração da cópia do banco de dados do site, utilizada para a atualização de teste, para uso como um banco de dados do site em qualquer site.  

Depois de atualizar com sucesso a cópia do banco de dados do site, continue a atualização do site do Configuration Manager e o respectivo banco de dados do site.  



## <a name="bkmk_upgrade"></a> Atualizar sites  

Estará tudo pronto para atualizar o site do Configuration Manager depois de concluir as seguintes tarefas:
- Faça a atualização prévia das configurações de seu site
- Teste a atualização do banco de dados do site em uma cópia do banco de dados
- Baixe os arquivos de pré-requisitos e os pacotes de idiomas para a versão que planeja instalar

Ao atualizar um site de uma hierarquia, você atualiza primeiro o site de nível superior da hierarquia. Esse site de nível superior é um site de administração central ou um site primário autônomo. Após a conclusão da atualização do site de administração central, é possível atualizar os sites primários filhos na ordem que desejar. Após atualizar um site primário, você pode atualizar os sites secundários filho desse site ou atualizar os sites primários adicionais antes de atualizar sites secundários.  

Para atualizar o site de administração central ou o site primário, execute a Instalação na mídia de origem do Configuration Manager. Não execute a Instalação para atualizar sites secundários. Em vez disso, use o console do Configuration Manager para atualizar um site secundário após concluir a atualização do seu site primário pai.  

Antes de atualizar um site, feche o console do Configuration Manager no servidor do site até que a atualização do site esteja concluída. Além disso, feche cada console do Configuration Manager executado em outros computadores que não sejam o do servidor do site. Você pode reconectar o console após a conclusão da atualização do site. No entanto, até que você faça a atualização do console do Configuration Manager para a sua nova versão, esse console não poderá exibir alguns objetos e algumas informações que estão disponíveis na nova versão do Configuration Manager.  


### <a name="upgrade-a-central-administration-site-or-primary-site"></a>Atualizar o site de administração central ou o site primário  

1. Verifique se o usuário que executa a Instalação tem os seguintes direitos de segurança:  

    - Direitos de **Administrador** local no servidor do site  

    - Se o servidor de banco de dados do site for remoto do servidor do site, ele deve ter direitos de **Administrador** local nele.  

2. No servidor do site, abra o seguinte programa: `<ConfigMgSourceMedia>\SMSSETUP\BIN\X64\Setup.exe`. Essa ação abre o Assistente de Instalação do Configuration Manager.  

3. Leia as informações disponíveis na página **Antes de começar** e, em seguida, selecione **Próximo**.  

4. Na página **Guia de Introdução**, selecione **Atualizar este site do Configuration Manager** e, em seguida, selecione **Próximo**.  

5. Na página **Chave do Produto (Product Key)** :  

    Se você tiver anteriormente instalado a avaliação do Configuration Manager, poderá selecionar **Instalar a edição licenciada deste produto**. Em seguida, insira a chave do seu produto para a instalação completa do Configuration Manager. Essa ação converte o site para a versão completa.  

    Você também pode especificar a **Data de vencimento do Software Assurance** do seu contrato de licença como um lembrete conveniente para essa data. Se não inserir esse valor durante a instalação, você poderá especificá-lo posteriormente no console do Configuration Manager.  

    > [!NOTE]  
    > A Microsoft não valida a data de validade que você inseriu e não usará essa data para a validação da licença. Você pode usá-la como um lembrete da data de vencimento. O Configuration Manager verifica periodicamente se há novas atualizações de software oferecidas online, e o status da licença do Software Assurance deve estar atualizado para que você esteja qualificado a usar essas atualizações adicionais.    

    Para obter mais informações, veja [Licenciamento e branches](/sccm/core/understand/learn-more-editions).

6. Na página **Termos de Licença de Software Microsoft**, leia e aceite os termos de licença e clique em **Avançar**.  

7. Na página **Licenças de Pré-requisito**, leia e aceite os termos de licença do software de pré-requisitos e clique em **Próximo**. A Instalação baixa e instala automaticamente o software nos clientes ou sistemas do site quando necessário. Antes de continuar para a próxima página, concorde com todos os termos.  

8. Na página **Downloads de Pré-requisitos**, especifique se a instalação deve baixar o conteúdo mais recentes da Internet ou usar os arquivos baixados anteriormente. Esse conteúdo inclui os arquivos de pré-requisitos redistribuíveis, pacotes de idiomas e as atualizações mais recentes do produto. Se você tiver baixado os arquivos usando o Downloader de Instalação, selecione **Usar arquivos baixados anteriormente** e especifique a pasta de download. Para obter mais informações, consulte [Downloader de Instalação](/sccm/core/servers/deploy/install/setup-downloader).  

    > [!NOTE]  
    > Ao usar arquivos baixados anteriormente, verifique se o caminho para a pasta de download contém a versão mais recente dos arquivos.  

9. Na página **Seleção do Idioma do Servidor** , exiba a lista de idiomas atualmente instalados para o site. Selecione os idiomas adicionais que estão disponíveis nesse site para o console do Configuration Manager e para os relatórios. É possível também eliminar os idiomas para os quais você não deseja mais que esse site ofereça suporte. Por padrão, o idioma inglês está selecionado e não pode ser removido.  

    > [!IMPORTANT]  
    > As versões do Configuration Manager não podem usar pacotes de idiomas de uma versão anterior a ela. Para habilitar o suporte a idiomas no site do Configuration Manager que você atualizou, deve usar a versão do pacote de idiomas da nova versão. Por exemplo, durante a atualização do System Center 2012 Configuration Manager para o Branch Atual do Configuration Manager, se a versão do Branch Atual de um pacote de idiomas não estiver disponível com os arquivos de pré-requisitos baixados, não será possível instalar o suporte para esse idioma.  

10. Na página **Seleção do Idioma do Cliente** , exiba a lista de idiomas atualmente instalados para o site. Selecione os idiomas adicionais disponíveis nesse site para os computadores cliente ou limpe os idiomas para os quais não deseja mais oferecer suporte nesse site. Especifique se deseja habilitar todos os idiomas do cliente para clientes de dispositivos móveis e, em seguida, clique em **Próximo**. Por padrão, o idioma inglês está selecionado e não pode ser removido.  

11. Na página **Resumo das Configurações**, examine a configuração. Quando terminar, selecione **Próximo** para iniciar o Verificador de Pré-requisitos a fim de verificar a preparação do servidor para a atualização do site.  

12. Na página **Verificação de Instalação de Pré-requisitos**, se não houver nenhum problema listado, selecione **Próximo** para atualizar o site e as funções do sistema do site. 

    Se o Verificador de Pré-requisitos encontrar um problema, selecione os itens da lista para ver os detalhes sobre como solucioná-lo. Solucione todos os itens da lista que contém status de **Erro** antes de continuar com a Instalação. Após resolver o problema, clique em **Executar Verificação** para reiniciar a verificação de pré-requisito. Você também pode abrir o arquivo ConfigMgrPrereq.log na raiz da unidade do sistema para verificar os resultados do Verificador de Pré-requisitos. O arquivo de log pode conter informações adicionais que não são exibidas na interface do usuário. Para obter uma lista das regras e descrições dos pré-requisitos de instalação, consulte [Prerequisite Checker](/sccm/core/servers/deploy/install/list-of-prerequisite-checks) (Verificador de pré-requisitos).

Na página **Atualizar** , a Instalação exibe o status do andamento geral. Quando a instalação do servidor do site principal e do sistema de site for concluída, feche o assistente. A configuração do site continuará em segundo plano.  


### <a name="upgrade-a-secondary-site"></a>Atualizar um site secundário  

1. Verifique se o usuário administrativo que executa a Instalação tem os seguintes direitos de segurança:  

    - Direitos de **Administrador** local no computador do site secundário  

    - Função de segurança de **Administrador de Infraestrutura** ou de **Administrador Completo** no site primário pai  

    - Direitos de Administrador do sistema (**SA**) no banco de dados do site secundário  

2. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**.  

3. Selecione o site secundário que deseja atualizar. Na guia **Início** da faixa de opções, no grupo **Site**, selecione **Atualizar**.  

4. Selecione **Sim** para confirmar a decisão e para iniciar a atualização do site secundário.  

A atualização do site secundário é executada em segundo plano. Após a conclusão da atualização, confirme o status no console do Configuration Manager. Selecione o servidor do site secundário e, em seguida, na guia **Início** da faixa de opções, no grupo **Site**, selecione **Mostrar Status da Instalação**.  



## <a name="BKMK_PostUpgrade"></a> Tarefas pós-atualização  

Após atualizar o site, talvez seja necessário concluir tarefas adicionais para finalizar a atualização ou reconfigurar o site. Essas tarefas podem incluir os seguintes itens: 
- Atualizar os clientes do Configuration Manager
- Atualizar os consoles do Configuration Manager
- Habilitar novamente as réplicas do banco de dados para pontos de gerenciamento
- Restaurar as configurações de funcionalidade do Configuration Manager que você usa e que não permaneceram após a atualização  

