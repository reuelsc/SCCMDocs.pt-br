---
title: "Atualizações no console | Microsoft Docs"
description: "O System Center Configuration Manager sincroniza com a nuvem da Microsoft para obter atualizações que você pode instalar no console."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
caps.latest.revision: 36
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 238ef5814c0c1b832c28d63c9f3879e21a6c439b
ms.openlocfilehash: 1b7063d45c6dc9b42e5002f684043a8e846416a2


---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>Instalações de atualizações para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager sincroniza com o serviço de nuvem da Microsoft para obter atualizações que você pode instalar do console do Configuration Manager.

## <a name="get-available-updates"></a>Obter atualizações disponíveis
Somente atualizações que se aplicam à sua infraestrutura e versão são baixadas e disponibilizadas na sua hierarquia. Essa sincronização pode ser automática ou manual, dependendo de como você configura o ponto de conexão de serviço de sua hierarquia:

-   No **modo online**, o ponto de conexão de serviço se conecta automaticamente ao serviço de nuvem da Microsoft e baixa as atualizações aplicáveis.  

     Por padrão, o Configuration Manager verifica se há novas atualizações a cada 24 horas. A partir da versão 1602 ou posterior, você também pode verificar imediatamente se há atualizações clicando em **Verificar Atualizações** no nó **Administração** > **Serviços de Nuvem** > **Atualizações e Manutenção** do console do Configuration Manager.  

-   No **modo offline**, o ponto de conexão de serviço não se conecta ao serviço de nuvem da Microsoft e você deve [Usar a Ferramenta de Conexão de Serviço para o System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md) manualmente para baixar e importar as atualizações disponíveis.  

> [!NOTE]  
>  Além das atualizações que você obtém ao realizar a sincronização com o serviço de nuvem da Microsoft, correções fora de banda instaladas usando a [Ferramenta de Registro de Atualização](http://technet.microsoft.com/library/mt691544.aspx) também são importadas para seu console, em que você pode selecioná-las para instalação.  

Após a sincronização das atualizações, você pode vê-las no console do Configuration Manager navegando até o nó **Administração** > **Serviços de Nuvem** > **Atualizações e Manutenção**:  

-   As atualizações que você não instalou são exibidas como **Disponíveis**.

-   As atualizações que você instalou são exibidas como **Instaladas**.  A partir da versão 1606, somente a atualização instalada mais recentemente é exibida e você pode clicar no botão **Histórico** na faixa de opções para exibir atualizações instaladas anteriormente.



Antes de configurar o ponto de conexão de serviço, entenda e planeje seus usos adicionais que podem afetar como você configurará essa função de sistema de sites:  

-   O ponto de conexão de serviço é usado para carregar informações de uso sobre seu site. Essas informações ajudam o serviço de nuvem da Microsoft a identificar as atualizações disponíveis para a versão atual de sua infraestrutura. Para obter mais informações, consulte [Dados de diagnóstico e de uso para o System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)  

-   O ponto de conexão de serviço é usado para gerenciar dispositivos com o Microsoft Intune e que usam o gerenciamento de dispositivo móvel local do Configuration Manager. Para obter mais informações, consulte [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md) (MDM [gerenciamento de dispositivo móvel] híbrido com o System Center Configuration Manager e o Microsoft Intune).  

Para entender melhor o que acontece quando as atualizações são baixadas, consulte:  

-   [Fluxograma — Baixar atualizações do System Center Configuration Manager](../../../core/servers/manage/download-updates-flowchart.md)

-   [Fluxograma — Replicação de atualização para o System Center Configuration Manager](../../../core/servers/manage/update-replication-flowchart.md)  

## <a name="permissions-to-view-and-manage-updates-and-features"></a>Permissões para exibir e gerenciar atualizações e recursos
Antes da instalação da atualização 1606, para exibir as atualizações no console, um usuário deve receber uma função de segurança que inclui a permissão para **Ler** no grupo de permissões **Site**, e o escopo de segurança **Tudo**. A partir da atualização 1606, uma nova classe de segurança de administração baseada em função chamada **Pacotes de atualização** foi introduzida. Ela concede acesso para exibir e gerenciar atualizações no console do Configuration Manager.    

**Sobre a classe de Pacotes de atualização:**  
Por padrão, os **Pacotes de atualização** (SMS_CM_Updatepackages) faz parte das seguintes funções de segurança internas com as permissões listadas:
 -  **Administrador Completo** com permissões para **Modificar** e **Ler** :
    -   Um usuário com essa função de segurança e acesso ao escopo de segurança **Tudo** pode exibir atualizações, instalar atualizações e habilitar recursos durante a instalação, além de habilitar recursos individuais após a atualização ter sido instalada anteriormente.
    - Um usuário com essa função de segurança e acesso ao escopo de segurança **Padrão** pode exibir atualizações, instalar atualizações, habilitar recursos durante a instalação e exibir recursos após uma atualização ter sido instalada, mas não habilitar os recursos após a atualização ter sido instalada anteriormente.

- **Analista somente leitura** com permissão para **Ler** :
  -  Um usuário com essa função de segurança e acesso ao escopo **Padrão** pode exibir atualizações, mas não as instalar, além de poder exibir recursos após uma atualização ter sido instalada, mas não as habilitar. Atualização para 1606 de 1511

**Resumo das permissões necessárias para atualizações e manutenção:**   
  - Use uma conta a que tenha sido atribuída uma função de segurança que inclua a classe **Atualizar pacotes** com permissões para **Modificar** e **Ler** .
  - Deve ser atribuído à conta o escopo **Padrão** .

**Para somente exibir atualizações**:
  - Use uma conta a que tenha sido atribuída uma função de segurança que inclua a classe **Atualizar pacotes** somente com permissão para **Ler** .
  - Deve ser atribuído à conta o escopo **Padrão** .

**Para habilitar recursos após as atualizações terem sido instaladas:**
  -   Use uma conta a que tenha sido atribuída uma função de segurança que inclua a classe **Atualizar pacotes** com permissões para **Modificar** e **Ler** .
  -  Deve ser atribuído à conta o escopo **Tudo** .






##  <a name="a-namebkmkbeforeinstalla-before-you-install-an-in-console-update"></a><a name="bkmk_beforeinstall"></a> Antes de instalar uma atualização no console  
 Confira as etapas a seguir antes de instalar atualizações de dentro do console do Configuration Manager:  

###  <a name="a-namebkmkstep1a-step-1-review-the-update-checklist"></a><a name="bkmk_step1"></a> Etapa 1: Analisar a lista de verificação de atualização  
Antes de instalar uma nova atualização de dentro do console do Configuration Manager, analise a lista de verificação de atualização aplicável para conhecer as ações a serem executadas antes de iniciar a atualização:  

-   Atualizar para a 1511 da [Atualização para o System Center Configuration Manager](../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)    

-   Atualizar para a 1602 da 1511: consulte  [Lista de verificação para instalar a atualização 1602](../../../core/servers/manage/checklist-for-installing-update-1602.md)

- Atualizar para a 1606 da 1511 ou da 1602: consulte [Lista de verificação para instalar a atualização 1606](../../../core/servers/manage/checklist-for-installing-update-1606.md)  

- Atualizar para a 1610 da 1511, 1602 ou da 1606: consulte [Lista de verificação para instalar a atualização 1610](../../../core/servers/manage/checklist-for-installing-update-1610.md)  

###  <a name="a-namebkmkstep2a-step-2-test-the-database-upgrade-before-installing-an-update"></a><a name="bkmk_step2"></a> Etapa 2: Testar a atualização do banco de dados antes de instalar uma atualização  
Antes de instalar uma nova atualização em sua hierarquia, como a atualização para a versão 1602, você deve testar a atualização de seu banco de dados do site. O nome da opção de linha de comando usada para testar a instalação de uma atualização para um backup de seu banco de dados do site é **testdbupgrade**.  

Diferente das versões anteriores do Configuration Manager, se a instalação de uma atualização falhar, não será necessário executar uma recuperação de site. Em vez disso, você poderá Repetir a instalação da atualização. Portanto, embora o teste de atualização do banco de dados seja menos fundamental do que em versões anteriores do produto, ainda é uma etapa recomendada.  

#### <a name="to-run-testdbupgrade-before-installing-an-update"></a>Para executar o testdbupgrade antes de instalar uma atualização  

1.  Obtenha um conjunto de arquivos de origem da pasta **CD.Latest** de um site que executa a versão para a qual você planeja atualizar. Isso pode exigir, primeiro, a instalação de um site em um ambiente de laboratório ou teste que executa essa versão do System Center Configuration Manager.  

     A pasta **CD.Latest** para um site contém os arquivos de origem dessa versão. Você deve usar esses arquivos de origem para executar o teste de atualização de seu banco de dados do site. Para obter mais informações, consulte [A pasta CD.Latest para o System Center Configuration Manager](../../../core/servers/manage/the-cd.latest-folder.md).  

     Por exemplo, se o seu site executar a versão 1501 e você quiser atualizar para a versão 1602, obtenha uma pasta CD.Latest de um site que já foi atualizado para a versão 1602. Normalmente, você pode instalar um site novo e temporário em um laboratório e atualizá-lo para a versão 1602 a fim de criar a pasta CD.Latest com os arquivos necessários.  

2.  Copie a pasta CD.Latest para um local no SQL Server que você usará para executar a atualização do banco de dados de teste. (Veja a próxima etapa).  

3.  Crie um backup do banco de dados do site do qual você deseja testar a atualização e restaure uma cópia desse banco de dados em uma instância do SQL Server que não hospeda um site do Configuration Manager. O SQL Server deve usar a mesma edição do SQL Server que seu banco de dados do site.  

4.  Após a restauração da cópia do banco de dados, execute a **Instalação** na pasta CD.Latest que você copiou de seu ambiente de laboratório ou teste. Ao executar a Instalação, use a opção de linha de comando **/TESTDBUPGRADE** . Se a instância do SQL Server que hospeda a cópia do banco de dados não for a instância padrão, será necessário fornecer também os argumentos da linha de comando para identificar a instância que hospeda a cópia do banco de dados do site.  

     Por exemplo, você planeja atualizar um banco de dados do site com o nome de banco de dados SMS_ABC. Você restaura uma cópia desse banco de dados do site para uma instância suportada do SQL Server com o nome de instância DBTest. Para testar uma atualização dessa cópia do banco de dados do site, use a linha de comando a seguir: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     Você pode encontrar Setup.exe no seguinte local na mídia de origem do System Center Configuration Manager: **SMSSETUP\BIN\X64**.  

5.  Na instância do SQL Server em que você executa o teste de atualização do banco de dados, monitore o arquivo ConfigMgrSetup.log na raiz da unidade do sistema para verificar o andamento e o êxito.  

     Se ocorrer falha na atualização do teste, resolva os problemas relacionados à falha de atualização do banco de dados do site, crie um novo backup do banco de dados do site e, em seguida, teste a atualização da nova cópia.  

     Depois que o processo for concluído com êxito, exclua a cópia do banco de dados.  

    > [!NOTE]  
    >  Não é possível restaurar a cópia do banco de dados do site, utilizada para a atualização de teste, para uso como um banco de dados do site em qualquer site.  

###  <a name="a-namebkmkstep3a-step-3-run-the-prerequisite-checker-before-installing-an-update"></a><a name="bkmk_step3"></a> Etapa 3: Executar o verificador de pré-requisitos antes de instalar uma atualização  
Antes de instalar uma atualização, considere a execução da verificação de pré-requisitos para essa atualização. Se você executar o pré-requisito antes de instalar uma atualização:  

-   Os arquivos de atualização serão replicados em outros sites antes de instalar a atualização  

-   A verificação de pré-requisitos será executada automaticamente outra vez quando você optar por instalar a atualização  

Posteriormente, quando você instalar uma atualização, terá a opção de configurá-la para ignorar os avisos de verificação de pré-requisitos.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Para executar o verificador de pré-requisitos antes de instalar uma atualização  

1.  Abra o console do Configuration Manager, vá até **Administração** > **Serviços de Nuvem** > **Atualizações e Manutenção**.  

2.  Clique com botão direito no pacote de atualizações para o qual você deseja executar a verificação de pré-requisitos.  

3.  Escolha **Executar verificação de pré-requisitos**.  Você pode ver o  

     Quando você executa a verificação de pré-requisitos, o conteúdo da atualização é replicado em sites filho.  Você pode ver o **distmgr.log** no servidor do site para confirmar a replicação bem-sucedida do conteúdo.  

4.  Para exibir os resultados da verificação, no console do Configuration Manager, acesse **Monitoramento** > **Status de Serviço e Atualizações** e procure o status do pré-requisito. Você também pode ver o arquivo ConfigMgrPrereq.log no servidor do site para obter mais detalhes.  



##  <a name="a-namebkmkinstalla-install-in-console-updates"></a><a name="bkmk_install"></a> Instalação de atualizações no console  
 Quando estiver pronto para instalar as atualizações de dentro do console do Configuration Manager, comece pelo site de nível superior de sua hierarquia. Esse site pode ser o site de administração central ou um site primário autônomo.  

 Recomendamos que você planeje a instalação da atualização fora do horário comercial normal de cada site, quando o processo de instalação da atualização e suas ações de reinstalação dos componentes do site e das funções do sistema de sites terão um efeito mínimo sobre as operações de seu negócio.  

-   Os sites primários filho iniciam automaticamente a atualização após a conclusão da instalação da atualização no site de administração central. Este é o processo padrão e recomendado. É possível usar os [Períodos de Serviço dos servidores de site](#bkmk_ServiceWindow) para controlar quando um site primário instala atualizações.  

-   É necessário atualizar manualmente os sites secundários de dentro do console do Configuration Manager após a conclusão da atualização do site pai primário. Não há suporte para atualização automática de servidores do site secundário.  

-   Quando usa um console do Configuration Manager após a atualização do site, você recebe uma solicitação para atualizar o console.  

-  Após o servidor do site concluir com êxito a instalação de uma atualização, ela atualiza automaticamente todas as funções de sistema de site aplicáveis.  A única limitação para isso se refere aos pontos de distribuição:
  - Devido a alterações introduzidas com a atualização 1606, ao instalar uma atualização de um site que já executa a versão 1606 ou posterior, os pontos de distribuição não ficam mais offline para serem atualizados ao mesmo tempo. Em vez disso, o servidor do site usa as configurações de distribuição de conteúdo do site para distribuir a atualização para um subconjunto de pontos de distribuição por vez. O resultado é que apenas alguns pontos de distribuição ficam offline para instalar a atualização. Isso permite que pontos de distribuição que ainda não começaram a ser atualizados ou que concluíram a atualização permaneçam online e forneçam conteúdo aos clientes.


###  <a name="a-namebkmkoverviewa-overview-of-in-console-update-installation"></a><a name="bkmk_overview"></a> Visão geral da instalação da atualização no console  
**1. Quando a instalação da atualização começa**  
Será apresentado a você um Assistente de atualizações que exibe uma lista das áreas de produtos para as quais a atualização se aplica.  

-   Na página **Geral** do assistente, você pode configurar **Avisos de pré-requisito**.  
      -   Os erros de pré-requisito sempre interrompem a instalação da atualização. Você deve resolver os erros antes de poder tentar novamente a instalação da atualização. Consulte [Repetir a instalação de uma atualização com falha](#bkmk_retry) para obter mais informações.  

    -   Avisos de pré-requisito também podem interromper a instalação da atualização. Você deve resolver esses avisos antes de tentar novamente a instalação da atualização.   Consulte [Repetir a instalação de uma atualização com falha](#bkmk_retry) para obter mais informações.  
    -   A seleção da opção **Ignorar os avisos de verificação de pré-requisitos e instalar essa atualização, independentemente dos requisitos ausentes**define uma condição para a instalação da atualização que ignora os avisos de pré-requisito e permite a continuação da instalação da atualização. Se você não selecionar essa opção, a instalação da atualização será interrompida quando um aviso for encontrado. A menos que você tenha executado anteriormente a verificação de pré-requisitos e resolvido os avisos de pré-requisito de um site, não recomendamos o uso dessa opção.  

      A partir da versão 1606, ons espaços de trabalho **Administração** e **Monitoramento** , o nó de Atualizações e Manutenção inclui um botão na Faixa de opções chamado **Ignorar os avisos de pré-requisito**. Esse botão fica disponível quando um pacote de atualização falha ao concluir a instalação devido a avisos de verificação de pré-requisitos.  Por exemplo, se você instalar uma atualização sem usar a opção de Ignorar avisos de pré-requisito (de dentro do Assistente de Atualizações), e a instalação da atualização for interrompida com um estado de aviso de pré-requisito, mas sem erros, você poderá selecionar **Ignorar avisos de pré-requisito** posteriormente na faixa de opções para disparar uma continuação automática da instalação da atualização que ignora os avisos de pré-requisito.  Quando essa opção é usada, a instalação da atualização continua automaticamente depois de alguns minutos.



-   Quando uma atualização for aplicável ao cliente do Configuration Manager, você verá a opção de testar a atualização do cliente com um conjunto limitado de clientes. Para obter mais informações, consulte [Como testar atualizações do cliente em uma coleção de pré-produção no System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

**2. Durante a instalação da atualização**  
Como parte da instalação da atualização, o Configuration Manager:  

-   Reinstale todos os componentes afetados, como as funções do sistema de sites ou o console do Configuration Manager  

-   Gerencia as atualizações para os clientes com base nas seleções feitas por você para o piloto do cliente e para [atualizações automáticas do cliente](https://technet.microsoft.com/library/mt627885.aspx)  

-   Não será necessário reiniciar os servidores do sistema de sites como parte da atualização (a menos que o .NET seja instalado como parte de um pré-requisito de funções do sistema de sites)  

> [!TIP]  
>  Quando as atualizações são instaladas, o Configuration Manager também atualiza a pasta CD.Latest, que é usada durante a recuperação de site.  

**3. Monitorar o andamento de atualizações durante a instalação**  
Use o seguinte para monitorar o progresso:  

-   No console do Configuration Manager, vá até o nó **Administração** > **Serviços de Nuvem** > **Atualizações e Manutenção**. Esse nó mostra o status da instalação para todos os pacotes de atualização.


-   No console do Configuration Manager, vá até o nó **Monitoramento** > **Visão Geral** > **Status de Serviço e Atualizações**. Esse nó mostra o status de instalação somente do pacote de atualização que está sendo instalado.  

    A partir da versão 1606, a instalação do pacote de atualização é dividida nas seguintes fases para facilitar o monitoramento. Para cada fase, agora há detalhes adicionais, incluindo qual arquivo de log exibir para obter mais informações:  
    -   **Baixar** (essa fase se aplica somente ao site de nível superior em que a função do sistema de sites do ponto de conexão de serviço está instalada)
    -   **Replicação**
    -   **Verificação de pré-requisitos**
    -   **Instalação**
    -   **Pós-instalação** (essa fase está disponível desde a versão 1610)

-   Você pode exibir o arquivo **CMUpdate.log** em **&lt;ConfigMgr_Installation_Directory>\Logs**  

**4. Quando a instalação da atualização é concluída**  
Após a conclusão da instalação da primeira atualização de site:  

-   Os sites primários filho instalarão automaticamente a atualização. Nenhuma ação do usuário é necessária.  

-   Será necessário atualizar manualmente os sites secundários de dentro do console do Configuration Manager.
> [!TIP]
> Embora a versão de um site secundário não seja exibida no console, você pode usar o SDK do Configuration Manager para confirmar uma versão de um site. Consulte [Classe WMI do Servidor SMS_Site](https://technet.microsoft.com/library/hh442832(CMSDK.16).aspx).


-   Até que todos os sites em sua hierarquia sejam atualizados para a nova versão, a hierarquia opera em um modo com versões mistas. Para obter mais informações, consulte [Interoperability between different versions of System Center Configuration Manager](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

**5.   Atualizar consoles do Configuration Manager**  
Após a atualização de um site de administração central ou site primário, cada console do Configuration Manager que se conecta a esse site também deve ser atualizado. Você receberá uma solicitação para atualizar um console:  

-   Quando você abrir o console  

-   Quando você navegar até um novo nó em um console aberto  

Recomendamos a instalação da atualização imediatamente, sem atraso.  

Após a conclusão da atualização do console, verifique se a versão do console e do site está correta. Acesse **Sobre o System Center Configuration Manager** no canto superior esquerdo do console em que é exibida a nova versão do site e do console.  

###  <a name="a-namebkmktoptiera-to-start-the-update-installation-at-the-top-tier-site"></a><a name="bkmk_toptier"></a> Para iniciar a instalação da atualização no site de nível superior  
No site de nível superior de sua hierarquia, no console do Configuration Manager, acesse **Administração** > **Serviços de Nuvem** > **Atualizações e Manutenção**, selecione uma atualização **Disponível** e clique em **Instalar Pacote de Atualização**.  

###  <a name="a-namebkmksecondarya-to-start-the-update-installation-at-a-secondary-site"></a><a name="bkmk_secondary"></a> Para iniciar a instalação da atualização em um site secundário  
Após a atualização do site primário pai de um site secundário, você poderá atualizar o site secundário de dentro do console do Configuration Manager.  Para fazer isso, use o **Assistente de Atualização de Site Secundário**.  

1.  No console do Configuration Manager, acesse **Administração** > **Configuração do Site** > **Sites**, selecione o site que deseja atualizar e, na guia Página Inicial, no grupo Site, clique em **Atualizar**.  

2.  Clique em **Sim** para iniciar a atualização do site secundário.  

Para monitorar a instalação da atualização em um site secundário, selecione o servidor do site secundário e, na guia Página Inicial, no grupo Site, clique em **Mostrar Status da Instalação**. Você também pode adicionar a coluna **Versão** à exibição da coluna para que você possa exibir a versão de cada site secundário.  

Após um site secundário ser atualizado com êxito, se o status no console não for atualizado ou sugerir uma falha na atualização, você poderá usar a opção **Tentar realizar a instalação novamente**. Essa opção não reinstala a atualização de um site secundário que instalou a instalação com êxito, mas força o console a atualizar o status.


##  <a name="a-namebkmkretrya-retry-installation-of-a-failed-update"></a><a name="bkmk_retry"></a> Repetir a instalação de uma atualização com falha  
Quando a instalação de uma atualização falha, revise os comentários no console para identificar as resoluções para erros e avisos.  Você também pode ver o arquivo ConfigMgrPrereq.log no servidor do site para obter mais detalhes. Antes de tentar novamente a instalação de uma atualização, você deve resolver os erros e os avisos.  

Quando estiver pronto para repetir a instalação de uma atualização, selecione a atualização com falha e selecione uma opção aplicável. O comportamento de repetição da instalação da atualização depende do nó do qual você inicia a repetição e da opção de repetição usada:  

1.  **Repita a instalação da hierarquia:**  
Você pode repetir a instalação de uma atualização para toda a hierarquia quando essa atualização estiver em um dos estados a seguir:  

    -   A verificação de pré-requisito foi aprovada com um ou mais avisos, e a opção de ignorar os avisos da verificação de pré-requisito não foi definida no Assistente de Atualização (O valor das atualizações para **Ignorar Aviso de Pré-requisito** no nó Atualizações e manutenção é **No**)   
    -   Falha dos pré-requisitos    
    -   Falha na instalação
    -   Falha na replicação do conteúdo para o site   

    Acesse **Administração** > **Serviços de Nuvem** > **Atualizações e Manutenção**, selecione a atualização e clique em uma das opções a seguir:  

    -   **Repetir** - quando você executa Repetir deste nó, da instalação da atualização começará novamente e ignorará automaticamente os avisos de pré-requisito. Ela também replicará novamente o conteúdo para a atualização se a replicação tiver falhado anteriormente.
    - **Ignorar avisos de pré-requisito** - a partir da versão 1606, se a instalação da atualização for interrompida devido a um aviso, você poderá clicar em Ignorar avisos de pré-requisito. Essa ação permite a continuação da instalação da atualização (após alguns minutos) e usa a opção para ignorar os avisos de pré-requisito.   

2.  **Repita a instalação para o site:**  
 Você pode repetir a instalação de uma atualização em um site específico quando essa atualização estiver em um dos estados a seguir:  

    -   A verificação de pré-requisito foi aprovada com um ou mais avisos, e a opção de ignorar os avisos da verificação de pré-requisito não foi definida no Assistente de Atualização (O valor das atualizações para **Ignorar Aviso de Pré-requisito** no nó Atualizações e manutenção é **No**)  
    -   Falha dos pré-requisitos    
    -   Falha na instalação    

    Acesse **Monitoramento** > **Visão geral** > **Status de Manutenção do Site**, selecione a atualização e clique em uma das opções a seguir:

       - **Repetir** - quando executa Repetir deste nó, você reinicia a instalação da atualização somente no site em questão. Diferente de quando Repetir é executado do nó Atualizações e Manutenção, essa repetição não ignora os avisos de pré-requisito.
       -    **Ignorar avisos de pré-requisito** - a partir da versão 1606, se a instalação da atualização for interrompida devido a um aviso, você poderá clicar em Ignorar avisos de pré-requisito. Essa ação permite a continuação da instalação da atualização (após alguns minutos) e usa a opção para ignorar os avisos de pré-requisito.

##  <a name="a-namebkmkaftera-after-a-site-installs-an-update"></a><a name="bkmk_after"></a> Após um site instalar uma atualização  
Use a lista de verificação a seguir para concluir tarefas comuns e configurações que são feitas após a atualização de um site:  

**Confirme se a replicação site a site está ativa:** no console do Configuration Manager, acesse os locais a seguir para exibir o status e confirmar que a replicação está ativa:  

-   **Monitoramento** > **Visão geral** > **Hierarquia do site**  

-   **Monitoramento** > **Visão geral** > **Replicação de banco de dados**  

Para obter mais informações, consulte [Monitorar a infraestrutura de hierarquia e de replicação no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) e [Sobre o Replication Link Analyzer](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA).  

 **Confirme se os servidores do site e os servidores do sistema de sites remoto foram reiniciados (se for necessário):** analise a infraestrutura de seu site e certifique-se de que os servidores de site e os servidores do sistema de sites aplicáveis (remotos do servidor do site) foram reinicializados com êxito.  Normalmente, isso é esperado apenas quando o Configuration Manager instala o .NET como pré-requisito para uma função de sistema de sites.  

 **Atualize consoles autônomos do Configuration Manager:** certifique-se de que todos os consoles remotos do Configuration Manager sejam atualizados para a mesma versão. Você receberá uma solicitação para atualizar o console quando:  

-   navegar até um novo nó no console  

-   Quando você abrir o console  

**Reconfigure as réplicas de banco de dados para os pontos de gerenciamento nos sites primários:** se você utilizar réplicas de banco de dados para pontos de gerenciamento em sites primários, será necessário desinstalar as réplicas de banco de dados antes de atualizar o site. Depois de atualizar um site primário, reconfigure a réplica de banco de dados para pontos de gerenciamento. Para obter mais informações, consulte [Réplicas de banco de dados para pontos de gerenciamento no System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Reconfigure quaisquer tarefas de manutenção de banco de dados desabilitadas antes da atualização:** se você tiver desabilitado as [Tarefas de manutenção de banco de dados para o System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) em um site antes da atualização, reconfigure-as no site usando as mesmas configurações que estavam em vigor antes da atualização.  

**Atualizar clientes:** para obter informações sobre como atualizar clientes existentes e como instalar novos clientes, consulte [Como atualizar clientes para computadores Windows no System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)  

**Configurações adicionais:** revise as alterações feitas antes de iniciar a atualização e restaure essas configurações em seus sites e hierarquia.  

##  <a name="a-namebkmkoptionsa-enable-optional-features-from-updates"></a><a name="bkmk_options"></a> Habilitar recursos opcionais de atualizações  
Ao instalar uma atualização que inclui um ou mais recursos opcionais, você terá a oportunidade de habilitar esses recursos em sua hierarquia.  Você pode fazer isso no momento da instalação da atualização ou retornar ao console posteriormente e habilitar os recursos opcionais.

Para exibir os recursos disponíveis e seus status, no console, navegue até **Administração** > **Serviços de Nuvem** > **Atualizações e Manutenção** > **Recursos**.

Quando um recurso não é opcional, ele é instalado automaticamente e não aparece no nó **Recursos** .  

##  <a name="a-namebkmkprereleasea-use-pre-release-features-from-updates"></a><a name="bkmk_prerelease"></a> Usar recursos de pré-lançamento de atualizações
A partir do 1606, você deverá dar consentimento para usar Recursos de pré-lançamento no System Center Configuration Manager antes de selecionar e habilitar seu uso.  

Os recursos de pré-lançamento foram incluídos no produto para testes iniciais em um ambiente de produção, mas não devem ser considerados prontos para produção.

Para dar consentimento, no console, navegue até **Administração** > **Configuração do Site** > **Sites**e selecione **Configurações da Hierarquia**. Na guia **Geral** , selecione **Consentir com o uso de recursos de pré-lançamento**.
 -  Dar o consentimento é uma ação única por hierarquia não pode ser desfeita  
 -  Até que dê o consentimento, você não pode habilitar novos recursos de pré-lançamento incluídos com a atualização 1606 e versões de atualização posteriores

 > [!NOTE]
 > Se você tiver habilitado o recursos de pré-lançamento da Atualização 1602 antes de instalar a Atualização 1606, esses recursos permanecerão habilitados para uso após a instalação da 1606, mesmo que você não tenha consentido com o uso dos recursos de pré-lançamento.

Quando sua hierarquia executa a versão 1606 ou posterior e você instala uma atualização que inclui recursos de pré-lançamento, esses recursos são visíveis no Assistente de Atualizações e Manutenção com os recursos regulares incluídos na atualização:
  - **Se você tiver consentido:** você poderá habilitar os recursos de pré-lançamento no Assistente de Atualizações e Manutenção quando estiver instalando a atualização. Para fazer isso, selecione os recursos de pré-lançamento como faria com qualquer outro recurso.     

    Você também pode esperar para habilitar um recurso de pré-lançamento mais tarde do nó **Administração** > **Serviços de Nuvem** > **Atualizações e Manutenção** > **Recursos** do console. Para fazer isso, no nó Recursos, selecione o recurso e clique em **Ativar**. (Essa opção fica esmaecida e indisponível até você dê consentimento.)  
  -   **Se você não tiver consentido:** ao instalar uma atualização, os recursos de pré-lançamento ficarão visíveis no Assistente de Atualizações e Manutenção, mas ficarão esmaecidos e não poderão ser habilitados. Após a instalação da atualização, você pode exibir esses recursos no nó Recursos, mas não habilitá-las até que você tenha dado o consentimento nas Configurações da Hierarquia.

 > [!TIP]
 > Quando você estiver instalando a atualização 1606, os recursos de pré-lançamento incluídos com a atualização 1606 não ficam visíveis no Assistente de Atualizações e Manutenção e não podem ser habilitados no momento em questão. Após a instalação da atualização 1606, você pode exibir os recursos de pré-lançamento incluídos no nó Recursos.

Se você tiver dado consentimento em um site primário autônomo e, depois, expandir a hierarquia instalando um novo site de administração central, você deverá dar consentimento novamente no site de administração central.

**Os seguintes recursos de pré-lançamento estão disponíveis:**

 |Recurso                    |Adicionado como pré-lançamento |Adicionado como recurso completo |  
|----------------------------|---------------------|------------------------|
| Cache de Pares para distribuição de conteúdo para clientes |  [Versão 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Gateway de gerenciamento de nuvem |  [Versão 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Painel Fontes de Dados do Cliente |  [Versão 1610](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Conector do OMS (Microsoft Operations Management Suite)  | [Versão 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Realização de serviços em uma coleção com reconhecimento de cluster (realização de serviços em um grupo de servidores)| [Versão 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|Acesso condicional para PCs gerenciados pelo System Center Configuration Manager | [Versão 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)                        |




##  <a name="a-namebkmkservicewindowa-service-windows-for-site-servers"></a><a name="bkmk_ServiceWindow"></a> Janelas de manutenção para servidores de site  
Em um servidor do site, você pode configurar períodos de serviço para controlar quando atualizações de infraestrutura do Configuration Manager podem ser aplicadas ao servidor do site.  Cada servidor do site dá suporte a vários períodos, com o período permitido para instalação de atualizações de infraestrutura determinado por uma combinação de todos os períodos configurados para esse servidor do site específico.  

**Para configurar um período de serviço:**  

1.  No console do Configuration Manager, abra **Administração** > **Configuração de Site** > **Sites** e selecione o servidor do site para o qual deseja configurar um período de serviço.  

2.  Em seguida, edite as **Propriedades** dos servidores do site e selecione a guia **Período de Serviço** , na qual você pode definir um ou mais períodos de serviço para o servidor do site.  

##  <a name="a-namebkmkfaqa-why-dont-i-see-certain-updates-in-my-console"></a><a name="bkmk_faq"></a> Por que eu não vejo determinadas atualizações em meu console?  
 Se você não conseguir encontrar uma atualização específica, ou quaisquer atualizações em seu console, após uma sincronização bem-sucedida com o serviço de nuvem da Microsoft, o motivo pode ser o seguinte:  

-   A atualização exige uma configuração que sua infraestrutura não usa, ou a versão atual de seu produto não atende a um pré-requisito para receber a atualização.  

     Se você acredita que tem as configurações necessárias ou atende a outros pré-requisitos para uma atualização que não está presente, confirme se o seu ponto de conexão de serviço está no modo online e use a opção **Verificar Atualizações** no nó Atualizações e Manutenção para forçar uma verificação.  Se você estiver no modo offline, use a ferramenta de conexão de serviço para sincronizar-se manualmente com o serviço de nuvem.  

-   Sua conta não tem as permissões corretas de administração baseada em funções para exibir as atualizações no console do Configuration Manager.

    Consulte [Permissões para gerenciar atualizações](../../../core/servers/manage/install-in-console-updates.md#permissions-to-view-and-manage-updates-and-features) neste tópico para obter informações sobre permissões necessárias para exibir as atualizações e habilitar recursos do console.



<!--HONumber=Dec16_HO3-->


