---
title: "Atualizações no console | Microsoft Docs"
description: "O System Center Configuration Manager sincroniza com a nuvem da Microsoft para obter atualizações que você pode instalar no console."
ms.custom: na
ms.date: 09/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
caps.latest.revision: "36"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 5302b5712e33c753d0193a32498bc02a2241428c
ms.sourcegitcommit: 474e6ddbaaeac4ba17d8172321e08deeb0140d0a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/19/2017
---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>Instalações de atualizações para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager sincroniza com o serviço de nuvem da Microsoft para obter atualizações. Em seguida, você pode instalar essas atualizações do console do Configuration Manager.

## <a name="get-available-updates"></a>Obter atualizações disponíveis
Somente atualizações que se aplicam à sua infraestrutura e versão são baixadas e disponibilizadas na sua hierarquia. Essa sincronização pode ser automática ou manual, dependendo de como você configura o ponto de conexão de serviço de sua hierarquia:

-   No **modo online**, o ponto de conexão de serviço se conecta automaticamente ao serviço de nuvem da Microsoft e baixa as atualizações aplicáveis.  

     Por padrão, o Configuration Manager verifica se há novas atualizações a cada 24 horas. Você também pode verificar imediatamente se há atualizações escolhendo **Verificar Atualizações** no nó **Administração** > **Atualizações e Manutenção** do console do Configuration Manager. (Antes da versão 1702, este nó ficava em **Administração** > **Serviços de Nuvem**.)

-   No **modo offline**, o ponto de conexão de serviço não se conecta ao serviço de nuvem da Microsoft. Para baixar e importar as atualizações disponíveis, [use a Ferramenta de Conexão de Serviço para o System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

> [!NOTE]  
>   Você pode importar correções fora da banda para o console. Para fazer isso, use a [Ferramenta de registro de atualização](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes). Essas correções fora de banda complementam as atualizações que você obtém quando sincroniza com o serviço Microsoft Cloud.


Após a sincronização das atualizações, você pode exibi-las no console do Configuration Manager indo até o nó **Administração** > **Atualizações e Manutenção**:  

-   As atualizações que você não instalou são exibidas como **Disponíveis**.

-   As atualizações que você instalou são exibidas como **Instaladas**.  Apenas a atualização instalada mais recentemente é mostrada. Você pode escolher o botão **Histórico** na faixa de opções para exibir as atualizações instaladas anteriormente.



Antes de configurar o ponto de conexão de serviço, entenda e planeje seus usos adicionais. Os seguintes usos podem afetar como você configura essa função de sistema de site:  

-   O ponto de conexão de serviço é usado para carregar informações de uso sobre seu site. Essas informações ajudam o serviço de nuvem da Microsoft a identificar as atualizações disponíveis para a versão atual de sua infraestrutura. Para obter mais informações, consulte [Dados de diagnóstico e de uso para o System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

-   O ponto de conexão de serviço é usado para gerenciar dispositivos com o Microsoft Intune e que usam o gerenciamento de dispositivo móvel local do Configuration Manager. Para obter mais informações, consulte [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md) (MDM [gerenciamento de dispositivo móvel] híbrido com o System Center Configuration Manager e o Microsoft Intune).  

Para entender melhor o que acontece quando as atualizações são baixadas, consulte:  

-   [Fluxograma — Baixar atualizações do System Center Configuration Manager](../../../core/servers/manage/download-updates-flowchart.md)

-   [Fluxograma — Replicação de atualização para o System Center Configuration Manager](../../../core/servers/manage/update-replication-flowchart.md)  

## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Atribuir permissões para exibir e gerenciar atualizações e recursos
Para exibir as atualizações no console, um usuário deve ter uma função de segurança de administração baseada em função que inclua a classe de segurança **Pacotes de atualização**. Essa classe concede acesso para exibir e gerenciar as atualizações no console do Configuration Manager.    

**Sobre a classe de Pacotes de atualização:**  
Por padrão, os **Pacotes de atualização** (SMS_CM_Updatepackages) faz parte das seguintes funções de segurança internas com as permissões listadas:
 -  **Administrador Completo** com permissões para **Modificar** e **Ler** :
    -   Um usuário com essa função de segurança e acesso ao escopo de segurança **Tudo** pode exibir e instalar atualizações. O usuário também pode habilitar recursos durante a instalação e habilitar recursos individuais após a atualização ser instalada.
    - Um usuário com essa função de segurança e acesso ao escopo de segurança **Padrão** pode exibir e instalar atualizações. O usuário também pode habilitar recursos durante a instalação e exibir recursos após uma atualização ser instalada. Mas esse usuário não pode habilitar os recursos depois que a atualização está instalada.

- **Analista somente leitura** com permissão para **Ler** :
  -  Um usuário com essa função de segurança e acesso ao escopo **Padrão** pode exibir atualizações, mas não instalá-las. Esse usuário também pode exibir recursos após uma atualização ter sido instalada, mas não pode habilitá-las.

**Permissões necessárias para atualizações e manutenção:**   
  - Use uma conta a que tenha sido atribuída uma função de segurança que inclua a classe **Atualizar pacotes** com permissões para **Modificar** e **Ler** .
  - Deve ser atribuído à conta o escopo **Padrão** .

**Permissões para apenas exibir atualizações**:
  - Use uma conta a que tenha sido atribuída uma função de segurança que inclua a classe **Atualizar pacotes** somente com permissão para **Ler** .
  - Deve ser atribuído à conta o escopo **Padrão** .

**Permissões necessárias para habilitar recursos após as atualizações terem sido instaladas:**
  -  Use uma conta a que tenha sido atribuída uma função de segurança que inclua a classe **Atualizar pacotes** com permissões para **Modificar** e **Ler** .
  -  Deve ser atribuído à conta o escopo **Tudo** .



##  <a name="bkmk_beforeinstall"></a> Antes de instalar uma atualização no console  
 Examine as etapas a seguir antes de instalar atualizações de dentro do console do Configuration Manager.  

###  <a name="bkmk_step1"></a> Etapa 1: Analisar a lista de verificação de atualização  
Examine a lista de verificação de atualização aplicável de ações a serem executadas antes de iniciar a atualização:

- Atualizar para 1606: veja [Lista de verificação para instalar a atualização 1606](../../../core/servers/manage/checklist-for-installing-update-1606.md).  

- Atualizar para a 1610 da 1606: veja [Lista de verificação para instalar a atualização 1610](../../../core/servers/manage/checklist-for-installing-update-1610.md).  

- Atualizar para a 1702 da 1606 ou da 1610: consulte [Lista de verificação para instalar a atualização 1702](../../../core/servers/manage/checklist-for-installing-update-1702.md).

<!-- Removed as update guidance 6/6/2017. The Test DB Upgrade details are no longer recommended nor required. They live on in a new topic for customers who still want to use them. -->

###  <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a>Etapa 2: Executar o verificador de pré-requisitos antes de instalar uma atualização  
Antes de instalar uma atualização, considere a execução da verificação de pré-requisitos para essa atualização. Se você executar o pré-requisito antes de instalar uma atualização:  

-   Os arquivos de atualização serão replicados em outros sites antes de instalar a atualização.  

-   A verificação de pré-requisitos será executada automaticamente outra vez quando você optar por instalar a atualização.  

> [!NOTE]   
> Quando você iniciar uma verificação de pré-requisitos e exibir o status, a fase **Instalação** parecerá estar ativa. No entanto, a atualização não está de fato sendo instalada. Para executar a verificação de pré-requisitos, o processo de atualização extrai o pacote da biblioteca de conteúdo e o coloca em uma pasta de preparo onde as verificações de pré-requisitos atuais podem ser acessadas.  Este mesmo processo é executado quando você instala uma atualização. Por esse motivo, a Instalação é mostrada como 'Em andamento'. Apenas a etapa *Extrair pacote de atualização* é mostrada na categoria de Instalação.  

Posteriormente, quando você instalar a atualização, poderá configurá-la para ignorar os avisos de verificação de pré-requisitos.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Para executar o verificador de pré-requisitos antes de instalar uma atualização  

1.  Abra o console do Configuration Manager, vá até **Administração** > **Atualizações e Manutenção**.   

2.  Clique com botão direito no pacote de atualizações para o qual você deseja executar a verificação de pré-requisitos.  

3.  Escolha **Executar verificação de pré-requisitos**.  

     Quando você executa a verificação de pré-requisitos, o conteúdo da atualização é replicado em sites filho.  Você pode exibir o distmgr.log no servidor do site para confirmar a replicação bem-sucedida do conteúdo.  

4.  Para exibir os resultados da verificação, no console do Configuration Manager, acesse **Monitoramento** > **Status de Serviço e Atualizações** e procure o status do pré-requisito. Você também pode ver o arquivo ConfigMgrPrereq.log no servidor do site para obter mais detalhes.  



##  <a name="bkmk_install"></a> Instalação de atualizações no console  
 Quando estiver pronto para instalar as atualizações de dentro do console do Configuration Manager, comece pelo site de nível superior de sua hierarquia. Esse site pode ser o site de administração central ou um site primário autônomo.  

 Recomendamos que você instale a atualização fora do horário comercial normal de cada site para minimizar o efeito nas operações comerciais. Isso ocorre porque a instalação da atualização pode incluir ações como reinstalar os componentes do site e funções de sistema de site.  

-   Os sites primários filho iniciam automaticamente a atualização após a conclusão da instalação da atualização no site de administração central. Este é o processo padrão e recomendado. É possível usar os [Service windows for site servers](/sccm/core/servers/manage/service-windows) (Períodos de serviço para servidores do site). para controlar quando um site primário instala atualizações.  

-   Atualize manualmente os sites secundários de dentro do console do Configuration Manager após a conclusão da atualização do site pai primário. Não há suporte para atualização automática de servidores do site secundário.  

-   Quando usa um console do Configuration Manager após a atualização do site, você recebe uma solicitação para atualizar o console.  

-  Após o servidor do site concluir com êxito a instalação de uma atualização, ela atualiza automaticamente todas as funções de sistema de site aplicáveis.  A única limitação refere-se aos pontos de distribuição. Ao instalar uma atualização, todos os pontos de distribuição não são reinstalados e, ao mesmo tempo, ficam offline para atualização. Em vez disso, o servidor do site usa as configurações de distribuição de conteúdo do site para distribuir a atualização para um subconjunto de pontos de distribuição por vez. O resultado é que apenas alguns pontos de distribuição ficam offline para instalar a atualização. Os pontos de distribuição que não começaram a ser atualizados ou que concluíram a atualização permaneçam online e forneçam conteúdo aos clientes.


###  <a name="bkmk_overview"></a> Visão geral da instalação da atualização no console  
**1. Quando a instalação da atualização começa**  
Será apresentado a você um Assistente de atualizações que exibe uma lista das áreas de produtos para as quais a atualização se aplica.  

-   Na página **Geral** do assistente, você pode configurar **Avisos de pré-requisito**.  
      -   Os erros de pré-requisito sempre interrompem a instalação da atualização. Corrija os erros antes de poder tentar novamente a instalação da atualização. Consulte [Repetir a instalação de uma atualização com falha](#bkmk_retry) para obter mais informações.  

    -   Avisos de pré-requisito também podem interromper a instalação da atualização. Corrija esses avisos antes de tentar novamente a instalação da atualização. Para saber mais, veja [Repetir a instalação de uma atualização com falha](#bkmk_retry).  
    -   A opção **Ignorar os avisos de verificação de pré-requisitos e instalar essa atualização, independentemente dos requisitos ausentes** define uma condição para a instalação da atualização que ignora os avisos de pré-requisito. Isso permite que a instalação da atualização continue. Se você não selecionar essa opção, a instalação da atualização será interrompida quando um aviso for encontrado. A menos que você tenha executado anteriormente a verificação de pré-requisitos e corrigido os avisos de pré-requisito de um site, não recomendamos o uso dessa opção.  

      Nos espaços de trabalho **Administração** e **Monitoramento**, o nó Atualizações e Manutenção inclui um botão na Faixa de opções chamado **Ignorar avisos de pré-requisito**. Esse botão fica disponível quando um pacote de atualização falha ao concluir a instalação devido a avisos de verificação de pré-requisitos. Por exemplo, você instala uma atualização sem usar a opção para ignorar os avisos de pré-requisitos (de dentro do Assistente de atualizações). A instalação da atualização é interrompida com um estado de aviso de pré-requisito, mas sem erros. Mais tarde você pode escolher **Ignorar avisos de pré-requisito** na faixa de opções para disparar uma continuação automática dessa instalação de atualização que, em seguida, ignora os avisos de pré-requisito. Quando você usa essa opção, a instalação da atualização continua automaticamente depois de alguns minutos.



-   Quando uma atualização for aplicável ao cliente do Configuration Manager, você verá a opção de testar a atualização do cliente com um conjunto limitado de clientes. Para obter mais informações, consulte [Como testar atualizações do cliente em uma coleção de pré-produção no System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

**2. Durante a instalação da atualização**  
Como parte da instalação da atualização, o Configuration Manager:  

-   Reinstale todos os componentes afetados, como as funções do sistema de sites ou o console do Configuration Manager.  

-   Gerencia as atualizações para os clientes com base nas seleções feitas por você para o piloto do cliente e para [atualizações automáticas do cliente](https://technet.microsoft.com/library/mt627885.aspx).  

-   Não reiniciará os servidores do sistema de sites como parte da atualização a menos que o .NET seja instalado como parte de um pré-requisito de funções do sistema de sites.  

> [!TIP]  
>  Quando as atualizações são instaladas, o Configuration Manager também atualiza a pasta CD.Latest. Essa pasta é usada durante uma recuperação de site.  

**3. Monitorar o andamento de atualizações durante a instalação**  
Use o seguinte para monitorar o progresso:  

-   Abra o console do Configuration Manager: nó **Administração** > **Atualizações e Manutenção**. Esse nó mostra o status da instalação para todos os pacotes de atualização.


-   No console do Configuration Manager, vá até o nó **Monitoramento** > **Visão Geral** > **Status de Serviço e Atualizações**. Esse nó mostra o status de instalação somente do pacote de atualização que está sendo instalado no momento.  

    A instalação do pacote de atualização é dividida nas seguintes fases para facilitar o monitoramento. Para cada fase, os detalhes adicionais incluem qual arquivo de log exibir para obter mais informações:  
    -   **Download** (essa fase se aplica somente ao site de nível superior em que o sistema de sites do ponto de conexão de serviço está instalada.)   

    -   **Replicação**   

    -   **Verificação de pré-requisitos**   

    -   **Instalação**    

    -   **Pós-instalação** (as [tarefas de pós-instalação](#post-installation-tasks) estão disponíveis desde a versão 1610).  

-   Você pode exibir o arquivo **CMUpdate.log** em **&lt;ConfigMgr_Installation_Directory>\Logs**  

**4. Quando a instalação da atualização é concluída**  
Após a conclusão da instalação da primeira atualização de site:  

-   Os sites primários filho instalam automaticamente a atualização. Nenhuma ação do usuário é necessária.  

-   Será necessário atualizar manualmente os sites secundários de dentro do console do Configuration Manager.
> [!TIP]
> Embora a versão de um site secundário não seja exibida no console, você poderá usar o SDK do Configuration Manager para confirmar uma versão de um site. Consulte [Classe WMI do Servidor SMS_Site](https://technet.microsoft.com/library/hh442832(CMSDK.16).aspx).


-   Até que todos os sites em sua hierarquia sejam atualizados para a nova versão, a hierarquia opera em um modo com versões mistas. Para obter mais informações, consulte [Interoperability between different versions of System Center Configuration Manager](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

**5.   Atualizar consoles do Configuration Manager**  
Após a atualização de um site de administração central ou site primário, cada console do Configuration Manager que se conecta a esse site também deve ser atualizado. Você receberá uma solicitação para atualizar um console:  

-   Quando você abrir o console.  

-   Quando você navegar até um novo nó em um console aberto.  

Recomendamos a instalação da atualização imediatamente.  

Após a conclusão da atualização do console, verifique se a versão do console e do site está correta. Vá para **Sobre o System Center Configuration Manager** no canto superior esquerdo do console.  

###  <a name="bkmk_toptier"></a> Para iniciar a instalação da atualização no site de nível superior  
No site de nível superior de sua hierarquia, no console do Configuration Manager, acesse **Administração** > **Atualizações e Manutenção**, selecione uma atualização **Disponível** e clique em **Instalar Pacote de Atualização**.  

###  <a name="bkmk_secondary"></a> Para iniciar a instalação da atualização em um site secundário  
Após a atualização do site primário pai de um site secundário, você poderá atualizar o site secundário de dentro do console do Configuration Manager.  Para fazer isso, use o **Assistente de Atualização de Site Secundário**.  

1.  No console do Configuration Manager, acesse **Administração** > **Configuração do Site** > **Sites**, selecione o site que deseja atualizar e, na guia Página Inicial, no grupo **Site**, escolha **Atualizar**.  

2.  Clique em **Sim** para iniciar a atualização do site secundário.  

Para monitorar a instalação da atualização em um site secundário, selecione o servidor do site secundário. Em seguida, na guia **Início**, no grupo **Site**, escolha **Mostrar Status da Instalação**. Você também pode adicionar a coluna **Versão** à exibição da coluna para que você possa exibir a versão de cada site secundário.  

Após um site secundário ser atualizado com êxito, se o status no console não for atualizado ou sugerir uma falha na atualização, use a opção **Tentar realizar a instalação novamente**. Essa opção não reinstala a atualização de um site secundário que instalou a instalação com êxito, mas força o console a atualizar o status.

### <a name="post-installation-tasks"></a>Tarefas de pós-instalação
A partir da versão 1610, você pode exibir informações sobre tarefas de pós-instalação.

Quando um site instala uma atualização, há várias tarefas que não podem ser iniciadas até a atualização concluir a instalação no servidor do site. Veja a seguir uma lista de tarefas de pós-instalação que são essenciais para operações do site e de hierarquia. Como elas são essenciais, são monitoradas ativamente. As tarefas adicionais que não são diretamente monitoradas incluem a reinstalação de funções do sistema de site. Para exibir o status de tarefas de pós-instalação críticas, selecione a tarefa **Pós-instalação** enquanto monitora a instalação da atualização para um site.

Nem todas as tarefas são concluídas imediatamente. Algumas tarefas não serão iniciados até a conclusão da instalação da atualização de cada site. Portanto, algumas novas funcionalidades que você possa estar aguardando poderão ser atrasadas até que essas tarefas sejam concluídas. Por exemplo, como ativar novos recursos não é iniciado até que todos os sites concluam a instalação da atualização, novos recursos poderão não estar visíveis por algum tempo.

As tarefas de pós-instalação incluem:

-   **Instalação do serviço SMS_EXECUTIVE**
  -   Serviços fundamentais que são executados no servidor do site.
  -   A reinstalação desse serviço deve ser concluída rapidamente.


-   **Instalação do componente SMS_DATABASE_NOTIFICATION_MONITOR**
  -   A thread essencial de componente do site do serviço SMS_EXECUTIVE.
  -   A reinstalação desse serviço deve ser concluída rapidamente.


-   **Instalação do componente SMS_HIERARCHY_MANAGER**
  -   Componente de site fundamental que é executado no servidor do site.
  -   Responsável por reinstalar as funções do sistema de site nos servidores do sistema de site.  Não é exibido o status para a reinstalação de função do sistema de sites individuais.
  -   A reinstalação desse serviço deve ser concluída rapidamente.


-   **Instalação do componente SMS_REPLICATION_CONFIGURATION_MONITOR**
  -   Componente de site fundamental que é executado no servidor do site.
  -   A reinstalação desse serviço deve ser concluída rapidamente.


-   **Instalação do componente SMS_POLICY_PROVIDER**
  -   Componente de site fundamental que é executado apenas em sites primários.
  -   A reinstalação desse serviço deve ser concluída rapidamente.


-   **Monitoramento de inicialização de replicação**   
  -   Isso é exibido apenas no site de administração central e em sites primários filho.
  -   Dependente do SMS_REPLICATION_CONFIGURATION_MONITOR.
  -   Deve ser concluído rapidamente.


-   **Atualizando o Pacote de Pré-produção do Cliente do Configuration Manager**    
  -   Isso é exibido até mesmo quando a pré-produção do cliente (também chamada de piloto do cliente) não está habilitada para uso.
  -   Não é iniciado até que todos os sites na hierarquia concluam a instalação da atualização.


-   **Atualização da pasta do Cliente no Servidor do Site**
  -   Isso não será exibido se você usar o cliente em pré-produção.  
  -   Deve ser concluído rapidamente.


-   **Atualização do Pacote do Cliente do Configuration Manager**
  -   Isso não será exibido se você usar o cliente em pré-produção.  
  -   Termina somente depois que todos os sites instalam a atualização.  


-   **Ativação de recursos**
  -   Isso é exibido apenas no site de nível superior da hierarquia.
  -   Não é iniciado até que todos os sites na hierarquia concluam a instalação da atualização.
  -   Os recursos individuais não são exibidos.


##  <a name="bkmk_retry"></a> Repetir a instalação de uma atualização com falha  
Quando a instalação de uma atualização falhar, examine os comentários no console para identificar as resoluções para erros e avisos. Você também pode ver o arquivo ConfigMgrPrereq.log no servidor do site para obter mais detalhes. Antes de tentar novamente a instalação de uma atualização, você deve corrigir os erros e os avisos.  

> [!TIP]  
> Se uma atualização tiver problemas de download ou replicação, você poderá usar a [ferramenta de redefinição de atualização](/sccm/core/servers/manage/update-reset-tool). Essa ferramenta está disponível em sites que executam a versão 1706 ou posterior.

Quando estiver pronto para repetir a instalação de uma atualização, selecione a atualização com falha e escolha uma opção aplicável. O comportamento de repetição da instalação da atualização depende do nó em que você inicia a repetição e da opção de repetição usada.  

1.  **Repita a instalação da hierarquia:**  
Você pode repetir a instalação de uma atualização para toda a hierarquia quando essa atualização estiver em um dos estados a seguir:  

    -   Verificação de pré-requisitos aprovada com um ou mais avisos e a opção de ignorar os avisos de verificação de pré-requisitos não foi definida no Assistente de Atualização. (O valor da atualização para **Ignorar aviso de pré-requisito** no nó **Atualizações e manutenção** é **Não**.)   
    -   Falha dos pré-requisitos    
    -   Falha na instalação
    -   Falha na replicação do conteúdo para o site   

    Acesse **Administração** > **Atualizações e Manutenção**, selecione a atualização e selecione uma das opções a seguir:  

    -   **Repetir** – quando você executar **Repetir** deste nó, a instalação da atualização começará novamente e ignorará automaticamente os avisos de pré-requisito. O conteúdo para a atualização também replicará novamente se a replicação tiver falhado anteriormente.
    - **Ignorar avisos de pré-requisito** – a partir da versão 1606, se a instalação da atualização for interrompida devido a um aviso, você poderá escolher **Ignorar avisos de pré-requisito**. Essa ação permite a continuação da instalação da atualização (após alguns minutos) e usa a opção para ignorar os avisos de pré-requisito.   

2.  **Repita a instalação para o site:**  
 Você pode repetir a instalação de uma atualização em um site específico quando essa atualização estiver em um dos estados a seguir:  

    -   Verificação de pré-requisitos aprovada com um ou mais avisos e opção de ignorar os avisos de verificação de pré-requisitos não foi definida no Assistente de Atualização. (O valor das atualizações para **Ignorar aviso de pré-requisito** no nó Atualizações e manutenção é **Não**).  
    -   Falha dos pré-requisitos    
    -   Falha na instalação    

    Acesse **Monitoramento** > **Visão geral** > **Status de Manutenção do Site**, selecione a atualização e clique em uma das opções a seguir:

       - **Repetir** – quando executa **Repetir** deste nó, você reinicia a instalação da atualização somente no site em questão. Diferente de quando **Repetir** é executado do nó **Atualizações e Manutenção**, essa repetição não ignora os avisos de pré-requisito.
       -    **Ignorar avisos de pré-requisito** – a partir da versão 1606, se a instalação da atualização for interrompida devido a um aviso, você poderá clicar em **Ignorar avisos de pré-requisito**. Essa ação permite a continuação da instalação da atualização (após alguns minutos) e usa a opção para ignorar os avisos de pré-requisito.

##  <a name="bkmk_after"></a> Após um site instalar uma atualização  
Use a lista de verificação a seguir para concluir tarefas comuns e configurações que são feitas após um site ser atualizado.   

**Confirme se a replicação site a site está ativa:** no console do Configuration Manager, acesse os locais a seguir para exibir o status e confirmar que a replicação está ativa:  

-   **Monitoramento** > **Visão geral** > **Hierarquia do site**  

-   **Monitoramento** > **Visão geral** > **Replicação de banco de dados**  

Para obter mais informações, consulte [Monitorar a infraestrutura de hierarquia e de replicação no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) e [Sobre o Replication Link Analyzer](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA).  

 **Confirme se os servidores do site e os servidores do sistema de sites remoto foram reiniciados (se for necessário):** examine a infraestrutura de seu site e certifique-se de que os servidores de site e os servidores do sistema de sites aplicáveis foram reinicializados com êxito. Normalmente, os servidores de site são reiniciados apenas quando o Configuration Manager instala o .NET como pré-requisito para uma função de sistema de sites.  

 **Atualize consoles autônomos do Configuration Manager:** certifique-se de que todos os consoles remotos do Configuration Manager sejam atualizados para a mesma versão. Você receberá uma solicitação para atualizar o console quando:  

-   Vá para um novo nó no console.  

-   Abra o console.

**Reconfigure as réplicas de banco de dados para os pontos de gerenciamento nos sites primários:** se você utilizar réplicas de banco de dados para pontos de gerenciamento em sites primários, será necessário desinstalar as réplicas de banco de dados antes de atualizar o site. Depois de atualizar um site primário, reconfigure a réplica de banco de dados para pontos de gerenciamento. Para obter mais informações, consulte [Réplicas de banco de dados para pontos de gerenciamento no System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Reconfigure quaisquer tarefas de manutenção de banco de dados desabilitadas antes da atualização:** se você tiver desabilitado as [tarefas de manutenção](../../../core/servers/manage/maintenance-tasks.md) de banco de dados antes de instalar a atualização, reconfigure-as no site. Use as mesmas configurações que estavam em vigor antes da atualização.  

**Clientes de atualização:** para saber mais, veja [Como atualizar clientes para computadores Windows no System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

**Configurações adicionais:** examine as alterações feitas antes de iniciar a atualização e restaure essas configurações em seus sites e hierarquia.  

##  <a name="bkmk_options"></a> Habilitar recursos opcionais de atualizações  
Quando uma atualização inclui um ou mais recursos opcionais, você tem a oportunidade de habilitar esses recursos em sua hierarquia.  Você pode habilitar recursos quando a atualização é instalada ou pode retornar ao console posteriormente e habilitar os recursos opcionais.

Para exibir os recursos disponíveis e seus status, no console, navegue até **Administração** > **Atualizações e Manutenção** > **Recursos**.

Quando um recurso não é opcional, ele é instalado automaticamente e não aparece no nó **Recursos**.  


Ao habilitar um novo recurso ou recurso de pré-lançamento, o gerenciador de hierarquia (HMAN) do Configuration Manager deve processar a alteração antes de o recurso ser disponibilizado. O processamento da alteração costuma ser imediato, mas pode levar até 30 minutos para ser concluído, dependendo do ciclo de processamento do HMAN. Após o processamento da alteração, é necessário reiniciar o console antes de exibir a nova interface do usuário relacionada a esse recurso.


##  <a name="bkmk_prerelease"></a> Usar recursos de pré-lançamento de atualizações
Os recursos de pré-lançamento estão incluídos na Ramificação atual para testes iniciais em um ambiente de produção. Você pode usar esses recursos em seu ambiente de produção, mas eles não são considerados prontos para produção. Saiba mais sobre os [recursos de pré-lançamento](/sccm/core/servers/manage/pre-release-features), inclusive como habilitá-los em seu ambientes.             


## <a name="known-issues"></a>Problemas conhecidos

###  <a name="bkmk_faq"></a> Por que eu não vejo determinadas atualizações em meu console?  
 Se você não conseguir encontrar uma atualização específica em seu console após uma sincronização bem-sucedida com o serviço de nuvem da Microsoft, o motivo pode ser o seguinte:  

-   A atualização exige uma configuração que sua infraestrutura não usa, ou a versão atual de seu produto não atende a um pré-requisito para receber a atualização.  

     Se você achar que tem as configurações necessárias e os pré-requisitos para uma atualização ausente, confirme se o ponto de conexão de serviço está no modo online. Em seguida, use a opção **Verificar se Há Atualizações** no nó **Atualizações e Manutenção** para forçar uma verificação.  Se você estiver no modo offline, use a ferramenta de conexão de serviço para sincronizar-se manualmente com o serviço de nuvem.  

-   Sua conta não tem as permissões corretas de administração baseada em funções para exibir as atualizações no console do Configuration Manager.

    Consulte [Permissões para gerenciar atualizações](../../../core/servers/manage/install-in-console-updates.md#assign-permissions-to-view-and-manage-updates-and-features) neste tópico para obter informações sobre permissões necessárias para exibir as atualizações e habilitar recursos do console.

### <a name="why-do-i-see-two-updates-for-version-1610"></a>Por que vejo duas atualizações para a versão 1610?
Ao exibir atualizações no console, você poderá ver duas atualizações para instalar a versão 1610. Essas atualizações têm datas diferentes. Ambos serão exibidos quando uma das seguintes condições for verdadeira:   
-   Você instalou uma versão anterior (como 1606) após a versão 1610 ter ficado disponível

-   Sua hierarquia executa a versão 1511 ou 1602 e não foi possível baixar a versão 1606

Há duas versões de atualização 1610, porque esta atualização foi lançada novamente após algumas pequenas alterações a alguns binários do arquivo. Essas alterações não afetam a funcionalidade do Configuration Manager ou a atualização.

Quando as atualizações ficarem disponíveis no seu console, recomendamos que você instale a atualização com a data mais recente. No entanto, como as duas atualizações fornecem os mesmos recursos, quando você já tiver instalado um deles não precisa fazer mais nada.
-   Se você instalou a atualização mais antiga, não precisa instalar a atualização mais recente. No entanto, se você instalar a atualização mais recente depois de instalar a primeira atualização, os binários em questão serão atualizados. Não ocorre nenhuma alteração adicional e nenhuma ação adicional de sua parte será necessária.

-   Se você instalou a atualização mais recente e, em seguida, instalou a atualização mais antiga, nenhuma ação adicional é necessária. Isso ocorre porque os binários mais recentes que você já instalou não serão substituídos pelos binários da atualização original.
