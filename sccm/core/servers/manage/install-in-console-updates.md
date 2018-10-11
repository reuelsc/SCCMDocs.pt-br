---
title: Atualização no console
titleSuffix: Configuration Manager
description: Instalar as atualizações do Configuration Manager por meio da nuvem da Microsoft
ms.date: 08/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 503255c571288fa0da0b0b81f3a76fc2b38bbb19
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893916"
---
# <a name="install-in-console-updates-for-configuration-manager"></a>Instalar atualizações no console para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Configuration Manager é sincronizado com o serviço de nuvem da Microsoft para obter atualizações. Em seguida, instale essas atualizações de dentro do console do Configuration Manager.



## <a name="get-available-updates"></a>Obter atualizações disponíveis

O site baixa apenas as atualizações que se aplicam à sua infraestrutura e versão. Essa sincronização pode ser automática ou manual, dependendo de como você configura o ponto de conexão de serviço de sua hierarquia:

-   No **modo online**, o ponto de conexão de serviço se conecta automaticamente ao serviço de nuvem da Microsoft e baixa as atualizações aplicáveis.  

     Por padrão, o Configuration Manager verifica se há novas atualizações a cada 24 horas. Verifique manualmente se há atualizações no console do Configuration Manager. Vá para o espaço de trabalho **Administração**, selecione o nó **Atualizações e Manutenção** e clique em **Verificar se há Atualizações** na faixa de opções.  

-   No **modo offline**, o ponto de conexão de serviço não se conecta ao serviço de nuvem da Microsoft. Para baixar e, em seguida, importar as atualizações disponíveis, [use a Ferramenta de Conexão de serviço](/sccm/core/servers/manage/use-the-service-connection-tool).  

> [!NOTE]  
> Se necessário, você pode importar correções fora da banda para o seu console. Para fazer isso, use a [ferramenta de registro de atualização](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes). Essas correções fora de banda complementam as atualizações que você obtém quando sincroniza com o serviço de nuvem da Microsoft.  


Após a sincronização das atualizações, exiba-as no console do Configuration Manager. Vá para o espaço de trabalho **Administração** e selecione o nó **Atualizações e Manutenção**.  

-   As atualizações que você não instalou são exibidas como **Disponíveis**.  

-   As atualizações que você instalou são exibidas como **Instaladas**. Apenas a atualização instalada mais recentemente é mostrada. Clique no botão **Histórico** na faixa de opções para exibir as atualizações instaladas anteriormente.  


Antes de configurar o ponto de conexão de serviço, entenda e planeje seus usos adicionais. Os seguintes usos podem afetar como você configura essa função de sistema de site:  

-   O site usa o ponto de conexão de serviço para carregar informações de uso sobre seu site. Essas informações ajudam o serviço de nuvem da Microsoft a identificar as atualizações disponíveis para a versão atual de sua infraestrutura. Para obter mais informações, consulte [Dados de diagnóstico e de uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  

-   O site usa o ponto de conexão de serviço para gerenciar dispositivos com o Microsoft Intune e que usam o gerenciamento de dispositivo móvel local do Configuration Manager. Para obter mais informações, veja [MDM (gerenciamento de dispositivo móvel) híbrido](/sccm/mdm/understand/hybrid-mobile-device-management).  

Para entender melhor o que acontece quando as atualizações são baixadas, veja os fluxogramas a seguir:  

-   [Fluxograma — baixar atualizações](/sccm/core/servers/manage/download-updates-flowchart)  

-   [Fluxograma — atualizar replicação](/sccm/core/servers/manage/update-replication-flowchart)  



## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Atribuir permissões para exibir e gerenciar atualizações e recursos

Para exibir as atualizações no console, um usuário deve ter uma função de segurança de administração baseada em função que inclua a classe de segurança **Pacotes de atualização**. Essa classe concede acesso para exibir e gerenciar as atualizações no console do Configuration Manager.    


#### <a name="about-the-update-packages-class"></a>Sobre a classe Pacotes de atualização   
Por padrão, a classe **Pacotes de atualização** (SMS_CM_Updatepackages) faz parte das seguintes funções de segurança internas com as permissões listadas:  

-  **Administrador Completo** com permissões para **Modificar** e **Ler** :  

    -   Um usuário com essa função de segurança e acesso ao escopo de segurança **Tudo** pode exibir e instalar atualizações. O usuário também pode habilitar recursos durante a instalação e habilitar recursos individuais após o site ser atualizado.  

    - Um usuário com essa função de segurança e acesso ao escopo de segurança **Padrão** pode exibir e instalar atualizações. O usuário também pode habilitar recursos durante a instalação e exibir recursos individuais após o site ser atualizado. Porém, esse usuário não pode habilitar os recursos após as atualizações do site.  

- **Analista somente leitura** com permissão para **Ler** :  

  -  Um usuário com essa função de segurança e acesso ao escopo **Padrão** pode exibir atualizações, mas não instalá-las. Esse usuário também pode exibir os recursos após o site ser atualizado, mas não pode habilitá-los.  


#### <a name="permissions-required-for-updates-and-servicing"></a>Permissões necessárias para atualizações e manutenção   
- Use uma conta à qual você atribua uma função de segurança que inclua a classe **Atualizar pacotes** com as permissões **Modificar** e **Ler**.  

- Atribuir a conta ao escopo **Padrão**.  

#### <a name="permissions-to-only-view-updates"></a>Permissões para somente exibir atualizações   
- Use uma conta à qual você atribua uma função de segurança incluindo a classe **Atualizar pacotes** somente com a permissão de **Leitura**.  

- Atribuir a conta ao escopo **Padrão**.  

#### <a name="permissions-required-to-enable-features-after-the-site-updates"></a>Permissões necessárias para habilitar recursos após a atualização do site   
-  Use uma conta à qual você atribua uma função de segurança que inclua a classe **Atualizar pacotes** com as permissões **Modificar** e **Ler**.  

-  Atribua a conta ao escopo **Todos**.  



##  <a name="bkmk_beforeinstall"></a> Antes de instalar uma atualização no console  

Examine as etapas a seguir antes de instalar atualizações de dentro do console do Configuration Manager.  


###  <a name="bkmk_step1"></a> Etapa 1: Analisar a lista de verificação de atualização  

Examine a lista de verificação de atualização aplicável de ações a serem executadas antes de iniciar a atualização:

- [Lista de verificação para instalar a atualização 1806](/sccm/core/servers/manage/checklist-for-installing-update-1806)  

- [Lista de verificação para instalar a atualização 1802](/sccm/core/servers/manage/checklist-for-installing-update-1802)

- [Lista de verificação para instalar a atualização 1710](/sccm/core/servers/manage/checklist-for-installing-update-1710)  


###  <a name="bkmk_step2"></a> Etapa 2: executar o verificador de pré-requisitos antes de instalar uma atualização  

Antes de instalar uma atualização, considere a execução da verificação de pré-requisitos para essa atualização. Se você executar o pré-requisito antes de instalar uma atualização:  

-   O site replica arquivos de atualização para outros sites antes de instalar a atualização.  

-   Quando você escolhe instalar a atualização, a verificação de pré-requisitos é executada automaticamente outra vez.  

> [!NOTE]   
> Quando você inicia uma verificação de pré-requisitos e, em seguida, exibe o status, a fase **Instalação** parece estar ativa. No entanto, o site não está realmente instalando a atualização. Para executar a verificação de pré-requisitos, o processo de atualização extrai o pacote da biblioteca de conteúdo. Ele então coloca o pacote em uma pasta de preparo em que ele possa acessar as verificações de pré-requisitos atuais. Quando você instala uma atualização, esse mesmo processo é executado. Esse comportamento é o motivo pelo qual a fase de instalação é exibida como **Em andamento**. Apenas a etapa *Extrair pacote de atualização* é mostrada na categoria de Instalação.  

Posteriormente, quando você instalar a atualização, poderá configurá-la para ignorar os avisos de verificação de pré-requisitos.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Para executar o verificador de pré-requisitos antes de instalar uma atualização  

1.  No console do Configuration Manager, vá até o espaço de trabalho **Administração** e selecione o nó **Atualizações e Manutenção**.   

2.  Selecione o pacote de atualização para o qual você deseja executar a verificação de pré-requisitos.  

3.  Clique em **Executar verificação de pré-requisitos** na faixa de opções.  

     Quando você executa a verificação de pré-requisitos, o conteúdo da atualização é replicado em sites filho. Exiba **distmgr.log** no servidor do site para confirmar que o conteúdo foi replicado com sucesso.  

4.  Para exibir os resultados da verificação de pré-requisitos:  

    1. No console do Configuration Manager, acesse o espaço de trabalho **Monitoramento**.  

    2. Selecione o nó **Status de Atualizações e Manutenção** nó e procure o status do pré-requisito.  

    3. Para obter mais informações, veja **ConfigMgrPrereq.log** no servidor do site.  



##  <a name="bkmk_install"></a> Instalação de atualizações no console  

Quando estiver pronto para instalar as atualizações de dentro do console do Configuration Manager, comece pelo site de nível superior da sua hierarquia. Esse site é o site de administração central ou um site primário autônomo.  

Instale a atualização fora do horário comercial normal para cada site para minimizar o efeito nas operações comerciais. A instalação da atualização pode incluir ações como reinstalar os componentes do site e funções do sistema de sites.  

-   Os sites primários filho automaticamente iniciam a atualização após a conclusão da instalação da atualização no site de administração central. Esse processo ocorre por padrão e é recomendado. Para controlar quando um site primário instala atualizações, use [janelas de Manutenção para servidores de site](/sccm/core/servers/manage/service-windows).  

-   Após a atualização do site pai primário ser concluída, atualize manualmente os sites secundários de dentro do console do Configuration Manager. Não há suporte para a atualização automática de servidores do site secundário.  

-   Quando você usa um console do Configuration Manager após a atualização do site, é solicitado a atualizar o console.  

-  Após o servidor do site concluir com êxito a instalação de uma atualização, ela atualiza automaticamente todas as funções de sistema de site aplicáveis. No entanto, nem todos os pontos de distribuição são reinstalados e ficam offline para atualização ao mesmo tempo. Em vez disso, o servidor do site usa as configurações de distribuição de conteúdo do site para distribuir a atualização para um subconjunto de pontos de distribuição por vez. O resultado é que apenas alguns pontos de distribuição ficam offline para instalar a atualização. Os pontos de distribuição que não começaram a ser atualizados ou que concluíram a atualização permanecem online e aptos a fornecer conteúdo aos clientes.


###  <a name="bkmk_overview"></a> Visão geral da instalação da atualização no console  

#### <a name="1-when-the-update-installation-starts"></a>1. Quando a instalação da atualização começa  
Será apresentado a você um Assistente de Atualizações que exibe uma lista das áreas de produtos para às quais a atualização se aplica.  

-   Na página **Geral** do assistente, você poderá configurar **Avisos de pré-requisito**, se necessário:  

    -   Os erros de pré-requisito sempre interrompem a instalação da atualização. Corrija os erros antes de poder tentar novamente a instalação da atualização. Para saber mais, veja [Repetir a instalação de uma atualização com falha](#bkmk_retry).  

    -   Avisos de pré-requisito também podem interromper a instalação da atualização. Corrija esses avisos antes de tentar novamente a instalação da atualização. Para saber mais, veja [Repetir a instalação de uma atualização com falha](#bkmk_retry).  

    -   **Ignorar os avisos de verificação de pré-requisitos e instalar esta atualização, independentemente dos requisitos ausentes**: defina uma condição para que a instalação da atualização ignore os avisos de pré-requisitos. Essa opção permite que a instalação da atualização continue. Se você não selecionar essa opção, a instalação de atualização será interrompida quando o processo de encontrar um aviso. A menos que você tenha executado anteriormente a verificação de pré-requisitos e corrigido os avisos de pré-requisito para um site, não use essa opção.  

      Nos espaços de trabalho **Administração** e **Monitoramento**, o nó Atualizações e Manutenção inclui um botão na faixa de opções chamado **Ignorar avisos de pré-requisito**. Esse botão fica disponível quando um pacote de atualização falha ao concluir a instalação devido a avisos de verificação de pré-requisitos. Por exemplo, você instala uma atualização sem usar a opção para ignorar os avisos de pré-requisitos (de dentro do Assistente de atualizações). A instalação da atualização é interrompida com um estado de aviso de pré-requisito, mas sem erros. Mais tarde, você clica em **Ignorar avisos de pré-requisito** na faixa de opções. Essa ação dispara uma continuação automática daquela instalação da atualização, que ignora os avisos de pré-requisito. Quando você usa essa opção, a instalação da atualização continua automaticamente depois de alguns minutos.  


-   Quando uma atualização é aplicável ao cliente do Configuration Manager, escolha testar a atualização do cliente com um conjunto limitado de clientes. Para obter mais informações, consulte [Como testar atualizações do cliente em uma coleção de pré-produção](/sccm/core/clients/manage/upgrade/test-client-upgrades).  


#### <a name="2-during-the-update-installation"></a>2. Durante a instalação da atualização  
Como parte da instalação da atualização, o Configuration Manager executa as seguintes ações:  

-   Reinstale todos os componentes afetados, como as funções do sistema de sites ou o console do Configuration Manager.  

-   Gerencia as atualizações para os clientes com base nas seleções feitas por você para o piloto do cliente e para [atualizações automáticas do cliente](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade).  

-   Servidores do sistema de sites geralmente não precisam reiniciar como parte da atualização. Se uma função usar o .NET e o pacote atualizar esse componente de pré-requisito, o sistema de sites poderá ser reiniciado.  

> [!TIP]  
>  Quando você instala atualizações do Configuration Manager, o site também atualiza a pasta CD.Latest. Para obter mais informações, veja [A pasta CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder).  


#### <a name="3-monitor-the-progress-of-updates-as-they-install"></a>3. Monitorar o andamento de atualizações durante a instalação  
Siga estas etapas para monitorar o progresso:  

-   No console do Configuration Manager, vá até o espaço de trabalho **Administração** e selecione o nó **Atualizações e Manutenção**. Esse nó mostra o status da instalação para todos os pacotes de atualização.  

-   No console do Configuration Manager, vá até o espaço de trabalho **Monitoramento** e selecione o nó **Status de Atualizações e Manutenção**. Esse nó mostra o status de instalação somente do pacote de atualização que o site está instalando.  

    A instalação da atualização é dividida em várias fases para facilitar o monitoramento. Para cada uma das seguintes fases, detalhes adicionais no status de instalação incluem qual arquivo de log exibir para obter mais informações:  

    -   **Download**: essa fase se aplica somente ao site de nível superior com o ponto de conexão de serviço.   

    -   **Replicação**   

    -   **Verificação de pré-requisitos**   

    -   **Instalação**    

    -   **Pós-instalação**: para obter mais informações, veja [tarefas pós-instalação](#post-installation-tasks).  

-   Exiba o arquivo **cmupdate.log** no `<ConfigMgr_Installation_Directory>\Logs` no servidor do site.  


#### <a name="4-when-the-update-installation-completes"></a>4. Quando a instalação da atualização é concluída  
Após a conclusão da instalação da primeira atualização de site:  

-   Os sites primários filho instalam automaticamente a atualização. Nenhuma ação do usuário é necessária.  

-   Atualize manualmente sites secundários de dentro do console do Configuration Manager. Para obter mais informações, veja [Iniciar a instalação da atualização em um site secundário](#bkmk_secondary).  

-   Até que todos os sites em sua hierarquia sejam atualizados para a nova versão, a hierarquia opera em um modo com versões mistas. Para obter mais informações, veja [Interoperabilidade entre versões diferentes](/sccm/core/plan-design/hierarchy/interoperability-between-different-versions).  


#### <a name="5-update-configuration-manager-consoles"></a>5. Atualizar consoles do Configuration Manager  
Após a atualização de um site de administração central ou atualizações de site primário, cada console do Configuration Manager que se conecte ao site também deverá ser atualizado. Você foi solicitado a atualizar um console:  

-   Quando você abrir o console  

-   Quando você acessa um novo nó em um console aberto  

Atualize o console imediatamente após a atualização do site.  

Depois que o console tiver sido atualizado, verifique se as versões do console e do site estão corretas. Vá para **Sobre o System Center Configuration Manager** no canto superior esquerdo do console.  

 > [!Note]  
 > Iniciando na versão 1802, a versão do console agora é ligeiramente diferente da versão do site. A versão secundária do console agora corresponde à versão de lançamento do Configuration Manager. Por exemplo, no Configuration Manager versão 1802, a versão inicial é 5.0.8634.1000 e a versão inicial do console é 5.**1802**.1082.1700. Os números de build (1082) e de revisão (1700) podem ser alterados com hotfixes futuros para a versão 1802.



###  <a name="bkmk_toptier"></a> Para iniciar a instalação da atualização no site de nível superior  

No site de nível superior da sua hierarquia, no console do Configuration Manager, vá para o espaço de trabalho **Administração** e selecione o nó **Atualizações e manutenção**. Selecione uma atualização com o estado **Disponível** e, em seguida, clique em **Instalar Pacote de Atualização** na faixa de opções.  


###  <a name="bkmk_secondary"></a> Para iniciar a instalação da atualização em um site secundário  

Após a atualização do site primário pai de um site secundário, atualize o site secundário do de dentro do console do Configuration Manager. Para fazer isso, use o **Assistente de Atualização de Site Secundário**.  

1.  No console do Configuration Manager, acesse o espaço de trabalho **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**. Selecione o site secundário que você deseja atualizar e, em seguida, clique em **Atualizar** na faixa de opções.  

2.  Clique em **Sim** para iniciar a atualização do site secundário.  

Para monitorar a instalação da atualização em um site secundário, selecione o site secundário e clique em **Mostrar Status da Instalação** na faixa de opções. Adicione também a coluna **Versão** ao nó Sites de modo que possa exibir a versão de cada site secundário.  

Em alguns casos, o status no console não será atualizado ou sugerirá que a atualização falhou. Depois que um site secundário for atualizado com êxito, use a opção **Repetir instalação**. Essa opção não reinstala a atualização para um site secundário que instalou a atualização com êxito, mas força o console a atualizar o status.


### <a name="post-installation-tasks"></a>Tarefas pós-instalação

Quando um site instala uma atualização, há várias tarefas que não podem ser iniciadas até a atualização concluir a instalação no servidor do site. Essa lista inclui as tarefas de pós-instalação essenciais para operações de site e hierarquia. Por serem essenciais, são monitoradas ativamente. Tarefas adicionais que não são monitoradas diretamente incluem a reinstalação de funções do sistema de sites. Para exibir o status das tarefas pós-instalação críticas, selecione a tarefa **Pós-Instalação** enquanto monitora a instalação da atualização para um site.

Nem todas as tarefas são concluídas imediatamente. Algumas tarefas não são iniciadas até que cada site conclua a instalação da atualização. Algumas novas funcionalidades que você pode estar aguardando podem ser atrasadas até que essas tarefas sejam concluídas. A ativação de novos recursos não é iniciada até que todos os sites concluam a instalação da atualização e, portanto, os novos recursos podem não estar visíveis por algum tempo.

As tarefas de pós-instalação incluem:

-   **Instalação do serviço SMS_EXECUTIVE**
  -   Serviços fundamentais que são executados no servidor do site.
  -   A reinstalação desse serviço deve ser concluída rapidamente.


-   **Instalação do componente SMS_DATABASE_NOTIFICATION_MONITOR**
  -   A thread essencial de componente do site do serviço SMS_EXECUTIVE.
  -   A reinstalação desse serviço deve ser concluída rapidamente.


-   **Instalação do componente SMS_HIERARCHY_MANAGER**
  -   Componente de site fundamental que é executado no servidor do site.
  -   Responsável por reinstalar funções em servidores do sistema de sites. O status para a reinstalação da função do sistema de sites individual não é exibido.
  -   A reinstalação desse serviço deve ser concluída rapidamente.


-   **Instalação do componente SMS_REPLICATION_CONFIGURATION_MONITOR**
  -   Componente de site fundamental que é executado no servidor do site.
  -   A reinstalação desse serviço deve ser concluída rapidamente.


-   **Instalação do componente SMS_POLICY_PROVIDER**
  -   Componente de site fundamental que é executado apenas em sites primários.
  -   A reinstalação desse serviço deve ser concluída rapidamente.


-   **Monitoramento de inicialização de replicação**   
  -   Essa tarefa é exibida apenas no site de administração central e em sites primários filho.
  -   Dependente do SMS_REPLICATION_CONFIGURATION_MONITOR.
  -   Deve ser concluído rapidamente.


-   **Atualizando o Pacote de Pré-produção do Cliente do Configuration Manager**    
  -   Essa tarefa é exibida até mesmo quando a pré-produção do cliente (também chamada de piloto do cliente) não está habilitada para uso.
  -   Não é iniciado até que todos os sites na hierarquia concluam a instalação da atualização.


-   **Atualização da pasta do Cliente no Servidor do Site**
  -   Essa tarefa não é exibida se o cliente é usado em pré-produção.  
  -   Deve ser concluído rapidamente.


-   **Atualização do Pacote do Cliente do Configuration Manager**
  -   Essa tarefa não é exibida se o cliente é usado em pré-produção.  
  -   Termina somente depois que todos os sites instalam a atualização.  


-   **Ativação de recursos**
  -   Essa tarefa é exibida apenas no site de nível superior da hierarquia.
  -   Não é iniciado até que todos os sites na hierarquia concluam a instalação da atualização.
  -   Os recursos individuais não são exibidos.



##  <a name="bkmk_retry"></a> Repetir a instalação de uma atualização com falha  

Quando a instalação de uma atualização falha, revise os comentários no console para identificar as resoluções para erros e avisos. Para obter mais detalhes, exiba **ConfigMgrPrereq.log** no servidor do site. Antes de tentar novamente a instalação de uma atualização, você deve corrigir os erros e os avisos.  

> [!TIP]  
> Se uma atualização tiver problemas de download ou replicação, use a [ferramenta de redefinição de atualização](/sccm/core/servers/manage/update-reset-tool).  

Quando estiver pronto para repetir a instalação de uma atualização, selecione a atualização com falha e escolha uma opção aplicável. O comportamento de repetição da instalação da atualização depende do nó em que você inicia a repetição e da opção de repetição usada.  

#### <a name="retry-installation-for-the-hierarchy"></a>Repita a instalação para a hierarquia
Repita a instalação de uma atualização para toda a hierarquia quando essa atualização estiver em um dos estados a seguir:  

  -   Verificações de pré-requisitos aprovadas com um ou mais avisos e a opção de ignorar os avisos de verificação de pré-requisitos não foram definidas no Assistente de Atualização. (O valor da atualização para **Ignorar Aviso de Pré-Requisito** no nó **Atualizações e Manutenção** é **Não**.)   

  -   Falha dos pré-requisitos    

  -   Falha na instalação  

  -   Falha na replicação do conteúdo para o site   

Vá para o espaço de trabalho **Administração** e selecione o nó **Atualizações e Manutenção**. Selecione a atualização e, em seguida, escolha uma das seguintes opções:  

  -   **Repetir** – quando você executar **Repetir** de **Atualizações e Manutenção**, a instalação da atualização começará novamente e ignorará automaticamente os avisos de pré-requisito. Se a replicação de conteúdo tiver falhado anteriormente, o conteúdo para a atualização será replicado novamente.  

  - **Ignorar avisos de pré-requisitos**: se a instalação da atualização for interrompida devido a um aviso, você poderá escolher **Ignorar avisos de pré-requisitos**. Essa ação permite que a instalação da atualização continue (após alguns minutos) e usa a opção para ignorar os avisos de pré-requisito.   

#### <a name="retry-installation-for-the-site"></a>Repita a instalação para o site  
Repita a instalação de uma atualização em um site específico quando essa atualização estiver em um dos estados a seguir:  

  -   Verificações de pré-requisitos aprovadas com um ou mais avisos e a opção de ignorar os avisos de verificação de pré-requisitos não foram definidas no Assistente de Atualização. (O valor da atualização para **Ignorar Aviso de Pré-Requisitos** no nó Atualizações e Manutenção é **Não**.)  

  -   Falha dos pré-requisitos    

  -   Falha na instalação    

Vá para o espaço de trabalho **Monitoramento** e selecione o nó **Status de Manutenção do Site**. Selecione a atualização e, em seguida, clique em uma das seguintes opções:  

  - **Repetir**: quando você **Repete** do **Status de Manutenção do Site**, você reinicia a instalação da atualização somente nesse site. Diferentemente de quando **Repetir** é executado do nó **Atualizações e Manutenção**, essa repetição não ignora os avisos de pré-requisito.  

  - **Ignorar avisos de pré-requisitos**: se a instalação da atualização for interrompida devido a um aviso, você poderá clicar em **Ignorar avisos de pré-requisitos**. Essa ação permite que a instalação da atualização continue (após alguns minutos) e usa a opção para ignorar os avisos de pré-requisito.  



##  <a name="bkmk_after"></a> Após um site instalar uma atualização  

Depois que o site for atualizado, examine a lista de verificação pós-atualização para a versão aplicável:  

- [Lista de verificação pós-atualização da versão 1806](/sccm/core/servers/manage/checklist-for-installing-update-1806#post-update-checklist)  

- [Lista de verificação pós-atualização da versão 1802](/sccm/core/servers/manage/checklist-for-installing-update-1802#post-update-checklist)  

- [Lista de verificação pós-atualização da versão 1710](/sccm/core/servers/manage/checklist-for-installing-update-1710#post-update-checklist)  



##  <a name="bkmk_options"></a> Habilitar recursos opcionais de atualizações  

Quando uma atualização inclui um ou mais recursos opcionais, você tem a oportunidade de habilitar esses recursos em sua hierarquia. Habilite recursos quando a atualização for instalada ou retorne ao console posteriormente para habilitar os recursos opcionais.

Para exibir recursos disponíveis e seus status, no console, vá para o espaço de trabalho **Administração**, expanda **Atualizações e manutenção** e selecione o nó **Recursos**.

Quando um recurso não é opcional, ele é instalado automaticamente. Ele não aparece no nó **Recursos**.  

> [!Important]  
> Em uma hierarquia de vários sites, habilite recursos opcionais ou pré-lançamento apenas do site de administração central. Esse comportamento garante que não haja nenhum conflito na hierarquia. <!--507197-->
 

Ao habilitar um novo recurso ou recurso de pré-lançamento, o gerenciador de hierarquia (HMAN) do Configuration Manager deve processar a alteração antes de o recurso ser disponibilizado. O processamento da alteração costuma ser imediato. Dependendo do ciclo de processamento do HMAN, ele poderá levar até 30 minutos para ser concluído. Depois que a alteração for processada, reinicie o console antes de usar o recurso.

#### <a name="list-of-optional-features"></a>Lista de recursos opcionais
Os recursos a seguir são opcionais na versão mais recente do Configuration Manager:<!--505213-->  

<!--Note to include in target articles

> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  

-->

- [Alta disponibilidade do servidor do site](/sccm/core/servers/deploy/configure/site-server-high-availability)<!--1128774-->
- [Atualizações de software de terceiros](/sccm/sum/deploy-use/third-party-software-updates)<!--1357605,1352101,1358714-->
- [Aprovar pedidos de aplicativos para usuários por dispositivo](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings) <!--1357015-->  
- [Suporte para o Cisco AnyConnect 4.0.07x e posterior para iOS](/sccm/mdm/deploy-use/create-vpn-profiles)<!--1357393-->
- [Avaliação do Atestado de Integridade do Dispositivo para políticas de conformidade para acesso condicional](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--1235616-->
- [Criar e executar scripts](/sccm/apps/deploy-use/create-deploy-scripts) <!--1236459-->
- [Executar etapa da sequência de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence) <!--1261338-->
- [Pré-cache do conteúdo de sequência de tarefas](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) <!--1021244-->
- [Atualizações de driver do Surface](/sccm/sum/get-started/configure-classifications-and-products) <!--1098490-->
- [Gateway de Gerenciamento de Nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) <!--1101764-->
- [Ponto de serviço do Data Warehouse](/sccm/core/servers/manage/data-warehouse) <!--1277922-->
- [Cache de pares do cliente](/sccm/core/plan-design/hierarchy/client-peer-cache) <!--1101436-->
- [Criação de PFX](/sccm/protect/deploy-use/introduction-to-certificate-profiles) <!--1321368-->
- [Conector do Azure Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics) <!--1258052-->
- [Política do Windows Defender Exploit Guard](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) <!--1355468-->
- [VPN para Windows 10](/sccm/protect/deploy-use/vpn-profiles) <!--1283610-->
- O [Passport for Work](/sccm/protect/deploy-use/windows-hello-for-business-settings) (também conhecido como *Windows Hello para Empresas*) <!--1245704-->
- [Acesso condicional para PCs gerenciados](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)  <!--1191496-->


> [!Tip]  
> Para obter mais informações sobre os recursos que exigem autorização para habilitar, veja [Recursos de pré-lançamento](/sccm/core/servers/manage/pre-release-features).  
> 
> Para obter mais informações sobre os recursos que estão disponíveis somente no branch de Technical Preview, veja [Technical Preview](/sccm/core/get-started/technical-preview).



##  <a name="bkmk_prerelease"></a> Usar recursos de pré-lançamento de atualizações

O branch atual inclui recursos pré-lançamento para testes iniciais em um ambiente de produção. Para obter mais informações, veja [recursos de pré-lançamento](/sccm/core/servers/manage/pre-release-features).



## <a name="bkmk_faq"></a> Perguntas frequentes

###  <a name="why-dont-i-see-certain-updates-in-my-console"></a>Por que eu não vejo determinadas atualizações em meu console?  

Se você não conseguir encontrar uma atualização específica no console após uma sincronização bem-sucedida com o serviço de nuvem da Microsoft, esse comportamento poderá ocorrer devido a um dos seguintes motivos:  

-   A atualização exige uma configuração que sua infraestrutura não usa, ou a versão atual de seu produto não atende a um pré-requisito para receber a atualização.  

     Se você acreditar que tem as configurações necessárias e os pré-requisitos para uma atualização ausente, confirme se o ponto de conexão de serviço está no modo online. Em seguida, use a opção **Verificar se Há Atualizações** no nó **Atualizações e Manutenção** para forçar uma verificação. Se o ponto de conexão de serviço estiver no modo offline, use a ferramenta de conexão de serviço para sincronizar-se manualmente com o serviço de nuvem.  

-   Sua conta não tem as permissões corretas de administração baseada em funções para exibir as atualizações no console do Configuration Manager. Para obter mais informações, veja [permissões para gerenciar atualizações](#assign-permissions-to-view-and-manage-updates-and-features).  

