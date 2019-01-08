---
title: Technical Preview 1706
titleSuffix: Configuration Manager
description: Saiba mais sobre os recursos disponíveis na Visualização Técnica versão 1706 do System Center Configuration Manager.
ms.date: 09/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ca3b4714-2a16-495e-8a17-1d87991d5556
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 97d356ee4c9a763732b6e49ef6135a99dccf4c26
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416734"
---
# <a name="capabilities-in-technical-preview-1706-for-system-center-configuration-manager"></a>Funcionalidades na Visualização Técnica 1706 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis na Visualização Técnica do System Center Configuration Manager, versão 1706. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview. Antes de instalar esta versão da visualização técnica, veja [Visualização Técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de uma visualização técnica, como atualizar entre versões e como fornecer comentários sobre os recursos em uma visualização técnica.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conhecidos nesse Technical Preview:**

-   **Mover ponto de distribuição** - as opções no console para movimentação de um ponto de distribuição entre sites não podem ser usadas com esta versão devido ao limite da visualização técnica de um único site primário.

-   **Configurações de conformidade do dispositivo** - você pode enfrentar um comportamento oposto durante ao usar as duas novas configurações de conformidade do dispositivo:
    - **Bloquear a depuração de USB no dispositivo**
    - **Bloquear aplicativos de fontes desconhecidas**

        Por exemplo, se o administrador definir **Bloquear depuração de USB no dispositivo** como **true**, todos os dispositivos que não têm a depuração de USB habilitada serão marcados como não compatíveis.

**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improved-boundary-groups-for-software-update-points"></a>Grupos de limites aprimorados para os pontos de atualização de software
<!-- 1324591 --> Esta versão inclui aprimoramentos no funcionamento dos pontos de atualização de software com grupos de limites. O exemplo a seguir resume o novo comportamento de fallback:
- Agora, o fallback para pontos de atualização de software usa um tempo configurável para fallback para grupos de limites vizinhos, com um tempo mínimo de 120 minutos.

- Independentemente da configuração de fallback, um cliente tenta acessar o último ponto de atualização de software usado durante 120 minutos. Após não conseguir acessar o servidor durante 120 minutos, o cliente verifica seu pool de pontos de atualização de software disponíveis, para poder encontrar um novo.

  -   Todos os pontos de atualização de software no grupo de limites atual do cliente são adicionados imediatamente ao pool do cliente.

  -   Como um cliente tenta usar seu servidor original durante 120 minutos antes de procurar um novo, nenhum servidor adicional é contatado até que as duas horas passem.

  -   Se o fallback para um grupo vizinho estiver configurado para o mínimo de 120 minutos, os pontos de atualização de software do grupo de limites vizinho fará parte do pool de servidores disponíveis do cliente.

- Após não conseguir acessar o servidor original durante duas horas, o cliente muda para um ciclo mais curto a fim de entrar em contato com um novo ponto de atualização de software.

  Isso significa que, se um cliente não conseguir se conectar com um novo servidor, ele selecionará rapidamente o próximo servidor a partir do pool de servidores disponíveis e tentará contatá-lo.

  -   Esse ciclo continuará até que o cliente se conecte a um ponto de atualização de software que possa usar.
  -   Até que o cliente encontre um ponto de atualização de software, outros servidores serão adicionados ao pool de servidores disponíveis quando o tempo de fallback de cada grupo de limites vizinho acabar.

Para saber mais, confira [pontos de atualização de software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) no tópico Grupos de limites do Branch Atual.


## <a name="site-server-role-high-availability"></a>Alta disponibilidade da função de servidor do site
<!-- 1128774 --> A alta disponibilidade para a função de servidor do site é uma solução baseada no Configuration Manager para instalar um servidor do site primário no modo *Passivo*. O servidor do site no modo passivo existe além do servidor do site primário existente, que está no modo *Ativo*. Um servidor do site no modo passivo está disponível para uso imediato, quando for necessário.

Um servidor do site primário no modo passivo:
-   Usa o mesmo banco de dados do site que o servidor do site ativo.
-   Recebe uma cópia da biblioteca de conteúdo de servidores de site ativo, que é mantida em sincronia.
-   Não grava dados no banco de dados do site enquanto ele estiver no modo passivo.
-   Não oferece suporte à instalação ou remoção de funções de sistema de site opcionais, desde que esteja no modo passivo.

Para tornar o servidor do site de modo passivo seu servidor do site de modo ativo, promova-o manualmente. Isso muda o servidor do site ativo para servidor do site passivo. As funções de sistema de sites disponíveis no servidor de modo ativo original permanecem disponíveis, desde que o computador esteja acessível. Somente a função de servidor do site alterna entre o modo ativo e passivo.

Para instalar um servidor do site de modo passivo, use o **Assistente para Criar Servidor do Sistema de Sites** para configurar um novo servidor do site com um tipo de **Servidor do site primário**, e um modo de **Passivo**. Depois, o assistente executa a Configuração do Configuration Manager no servidor especificado para instalar o novo servidor do site no modo passivo. Após a conclusão da instalação, o servidor do site de modo ativo mantém o servidor do site de modo passivo e sua biblioteca de conteúdo em sincronia com as alterações ou configurações feitas no servidor do site ativo.

### <a name="prerequisites-and-limitations"></a>Pré-requisitos e limitações
-   Há suporte apenas para um único servidor do site de modo passivo em cada site primário.

-   O servidor do site de modo passivo pode ser local ou baseado em nuvem no Azure.

-   Os servidores do site de modo passivo e ativo devem estar no do mesmo domínio.

-   Os servidores do site de modo ativo e passivo devem usar o mesmo banco de dados de sites, que deve ser remoto com relação aos computadores de cada servidor do site.

    -   O SQL Server que hospeda o banco de dados pode usar uma instância padrão, instância nomeada, o cluster do SQL Server ou um Grupo de Disponibilidade AlwaysOn.

    -   O servidor do site de modo passivo é configurado para usar o mesmo banco de dados de sites que o servidor do site de modo ativo. No entanto, o servidor do site de modo passivo não usa esse banco de dados até sua promoção para o modo ativo.

-   O computador que executará o servidor do site de modo passivo:

    -   Deve atender aos [pré-requisitos para instalação de um site primário](https://docs.microsoft.com/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site).

    -   Instala usando arquivos de origem que correspondem à versão do servidor do site de modo ativo.

    -   Não pode ter uma função de sistema de site de qualquer site anterior à instalação do site de modo passivo.

-   Os computadores servidores do site de modo ativo e passivo podem executar diferentes sistemas operacionais ou versões de service pack, desde que ambos permaneçam com suporte de sua versão do Configuration Manager.

-   A promoção do servidor do site de modo passivo para o servidor de modo ativo é manual. Não há failover automático.

-   As funções do sistema de sites podem ser instaladas somente no servidor do site que está no modo ativo.

    -   Um servidor do site no modo ativo dá suporte a todas as funções de sistema de sites. Você não pode instalar funções do sistema de sites no servidor quando ele estiver no modo passivo.

    -   Funções de sistema de sites que usam um banco de dados (como o ponto de relatório) devem ter esse banco de dados em um servidor remoto com relação aos servidores do site de modo ativo e passivo.

    -   O SMS_Provider não é instalado no servidor do site no modo passivo. Como você precisa se conectar a um SMS_Provider para que o site promova manualmente o servidor do site de modo passivo para o modo ativo, recomendamos [instalar pelo menos uma instância adicional do provedor](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider) em um computador adicional.

**Problema conhecido**:   
Com esta versão, o **Status** para as seguintes condições é exibido no console como valores numéricos em vez de texto legível:
-   131071 – falha na instalação do servidor do site
-   720895 – falha na desinstalação da função de servidor do site
-   851967 – falha no failover

### <a name="add-a-site-server-in-passive-mode"></a>Adicionar um servidor do site no modo passivo
1.  No console, acesse **Administração** > **Configuração do Site** > **Sites** e inicie o [Assistente para Adicionar Funções do Sistema de Sites](/sccm/core/servers/deploy/configure/install-site-system-roles). Também é possível usar o **Assistente para Criar Servidor do Sistema de Sites**.

2.  Na página **Geral**, especifique o servidor que hospedará o servidor do site de modo passivo. O servidor especificado não pode hospedar outras funções do sistema de sites antes de instalar um servidor do site no modo passivo.

3.  Na página **Seleção de Função do Sistema**, selecione apenas **Servidor do site primário no modo passivo**.

4.  Para concluir o assistente, você deve fornecer as seguintes informações que serão usadas para executar a Configuração e instalação da função de servidor do site no servidor especificado:
    -   Escolha copiar os arquivos de instalação do servidor do site ativo para o novo servidor do site de modo passivo, ou especifique um caminho para um local com o conteúdo da pasta **CD.Latest** do servidor do site ativo.

    -   Especifique o mesmo servidor de banco de dados do site e o nome do banco de dados usados pelo servidor do site de modo ativo.

5.  Depois, o Configuration Manager instala o servidor do site no modo passivo no servidor especificado.

Para conferir o status de instalação detalhado, acesse **Administração** > **Configuração do Site** > **Sites**.
-   O status do servidor do site no modo passivo mostra **Instalando**.

-   Selecione o servidor e clique em **Mostrar Status** para abrir **Status de Instalação do Servidor do Site** para obter informações mais detalhadas.



### <a name="promote-the-passive-mode-site-server-to-active-mode"></a>Promover o servidor do site de modo passivo para o modo ativo
Quando você quiser alterar o servidor do site de modo passivo para o modo ativo, faça isso no painel **Nós** em **Administração** > **Configuração do Site** > **Sites**. Desde que você possa acessar uma instância do SMS_Provider, poderá acessar o site para fazer essa alteração.
1.  No painel **Nós** do console do Configuration Manager, selecione o servidor do site no modo passivo e, depois, na Faixa de opções, escolha **Promover para ativo**.

2.  O **Status** simples para o servidor que você está promovendo aparecerá no painel **Nós** como **Promovendo**.

3.  Após a conclusão da promoção, a coluna **Status** mostrará **OK** para novo servidor do site de modo *Ativo* e para o novo servidor do site do modo *Passivo*.

4.  Em **Administração** > **Configuração do Site** > **Sites**, o nome do servidor do site primário exibe agora o nome do novo servidor do site do modo *Ativo*.
Para obter o status detalhado, acesse **Monitoramento** > **Status do Servidor do Site**.
    -   A coluna **Modo** identifica qual servidor está *Ativo* ou *Passivo*.

    -   Ao promover um servidor do modo passivo para o modo ativo, selecione o servidor do site que você está promovendo para ativo e, depois, escolha **Mostrar Status** na faixa de opções. Isso abre a janela **Status de Promoção do Servidor do Site**, que exibe detalhes adicionais sobre o processo.

Quando um servidor do site no modo ativo mudar para o modo passivo, somente a função de sistema de sites ficará passiva. Todas as outras funções de sistema de sites instaladas nesse computador permanecerão ativas e acessíveis aos clientes.


### <a name="daily-monitoring"></a>Monitoramento diário
Quando você tiver um site primário no modo passivo, monitore-o diariamente para garantir sua sincronia com o servidor do site de modo ativo e pronta disponibilidade para uso. Para fazer isso, acesse **Monitoramento** > **Status do Servidor do Site**. Aqui você pode ver os servidores do site de modo passivo e ativo.

A guia **Resumo**:
-   A coluna **Modo** identifica qual servidor está Ativo ou Passivo.
-   A coluna **Status** lista **OK** quando o servidor de modo passivo estiver em sincronia com o servidor de modo ativo.
-   Para exibir detalhes adicionais sobre o estado de sincronização de conteúdo, clique em **Mostrar status** no Estado de Sincronização de Conteúdo. Isso abre a guia Biblioteca de Conteúdo, na qual você pode tentar corrigir problemas de sincronização de conteúdo.

A guia **Biblioteca de Conteúdo**:
-   Veja o **Estado** para conteúdo que sincroniza do servidor do site ativo para o servidor do site de modo passivo.
-   Você pode selecionar o conteúdo com um Estado de **Falha** e escolher **Sincronizar itens selecionados** na Faixa de Opções. Essa ação tenta ressincronizar esse conteúdo a partir da origem do conteúdo para o servidor do site de modo passivo. Durante a recuperação, o Estado aparece como **Em andamento**, e quando estiver sincronizado, é exibido como **Sucesso**.

### <a name="try-it-out"></a>Experimente!
Tente concluir as tarefas a seguir e, depois, envie-nos **Comentários** usando a guia **Início** da Faixa de Opções para nos contar foi:
-   Posso instalar um site primário no modo passivo.
-   Posso usar o console para promover o servidor do site de modo passivo e torná-lo o servidor do site de modo ativo, e confirmar a alteração do status dos dois servidores do site.


## <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Incluir relação de confiança para arquivos e pastas específicos em uma política de Proteção do Dispositivo
<!-- 1324676 --> Nesta versão, adicionamos mais recursos para o gerenciamento de política de [Proteção do dispositivo](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)

Agora, você tem a opção de adicionar a relação de confiança para arquivos específicos e pastas em uma política de Proteção do Dispositivo. Isso permite que você:

1.  Solucione problemas de comportamentos do instalador gerenciado
2.  Confie em aplicativos de linha de negócios que não podem ser implantados com o Configuration Manager
3.  Confie em aplicativos que estão incluídos em uma imagem de implantação de sistema operacional.

### <a name="try-it-out"></a>Experimente!

1.  Enquanto você estiver criando uma política de Proteção do Dispositivo, na guia Inclusões do Assistente para criação da política de Proteção do Dispositivo, clique em **Adicionar**.
2.  Na caixa de diálogo **Adicionar Arquivo ou Pasta Confiável**, especifique informações sobre o arquivo ou pasta na qual você deseja confiar. Você pode especificar um caminho de arquivo ou pasta local ou se conectar a um dispositivo remoto ao qual você tem permissão para se conectar, e especificar um caminho de arquivo ou pasta nesse dispositivo.
3.  Conclua o assistente.


## <a name="hide-task-sequence-progress"></a>Ocultar o progresso da sequência de tarefas
<!-- 1354291 --> Nesta versão, é possível controlar quando o andamento da sequência de tarefas é exibido aos usuários finais por meio de uma nova variável. Em sua sequência de tarefas, use a etapa **Definir Variável de Sequência de Tarefas** para definir o valor para a variável **TSDisableProgressUI** a fim de ocultar ou exibir o andamento da sequência de tarefas. Você pode usar a etapa Definir Variável de Sequência de Tarefas várias vezes em uma sequência de tarefas para alterar o valor da variável. Isso permite que você oculte ou exiba o andamento da sequência de tarefas em diferentes seções da sequência de tarefas.

#### <a name="to-hide-task-sequence-progress"></a>Para ocultar o progresso da sequência de tarefas
No editor de sequência de tarefas, use a etapa [Definir Variável de Sequência de Tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) para definir o valor da variável **TSDisableProgressUI** como **True** a fim de ocultar o andamento da sequência de tarefas.

#### <a name="to-display-task-sequence-progress"></a>Para exibir o andamento da sequência de tarefas
No editor de sequência de tarefas, use a etapa [Definir Variável de Sequência de Tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) para definir o valor da variável **TSDisableProgressUI** como **False** a fim de exibir o andamento da sequência de tarefas.

## <a name="specify-a-different-content-location-for-install-content-and-uninstall-content"></a>Especificar um local de conteúdo diferente para instalar e desinstalar o conteúdo
<!-- 1097546 --> Atualmente, no Configuration Manager, você especifica a localização de instalação que contém os arquivos de instalação de um aplicativo. Quando você especifica um local de instalação, ele também é usado como o local de desinstalação do conteúdo do aplicativo.
Com base em seus comentários, quando você quer desinstalar um aplicativo implantado, e o conteúdo do aplicativo não está no computador cliente, o cliente baixa todos os arquivos de instalação do aplicativo novamente antes do aplicativo ser desinstalado.
Para resolver esse problema, agora você pode especificar um local do conteúdo de instalação e um local do conteúdo de desinstalação opcional. Além disso, você pode optar por não especificar um local do conteúdo de desinstalação.

### <a name="try-it-out"></a>Experimente!

1. Nas propriedades do tipo de implantação de um aplicativo, clique na guia **Conteúdo**.
2. Configure o **Local do conteúdo de instalação** como normal.
3. Para **Desinstalar as configurações do conteúdo**, escolha uma das seguintes opções:
    - **Mesmo que o conteúdo de instalação** - O mesmo local de conteúdo será usado, não importa se você está instalando ou desinstalando o aplicativo.
    - **Nenhum conteúdo de desinstalação** - escolha esta opção se você não quiser fornecer um local de conteúdo de desinstalação para o aplicativo.
    - **Diferente do conteúdo de instalação** - escolha esta opção se você quiser especificar um local de conteúdo de desinstalação diferente do local de conteúdo de instalação.
5. Se você tiver selecionado **Diferente do conteúdo de instalação**, procure, ou insira, o local do conteúdo do aplicativo que será usado para desinstalar o aplicativo.
6. Clique em **OK** para fechar a caixa de diálogo Propriedades do tipo de implantação.


## <a name="accessibility-improvements"></a>Aprimoramentos na acessibilidade  
<!--1253000 --> Esta versão prévia apresenta vários aprimoramentos nos [recursos de acessibilidade](/sccm/core/understand/accessibility-features) no console do Configuration Manager. Elas incluem:     

**Novos atalhos de teclado para movimentar-se pelo console:**
-   CTRL + M - define o foco no painel principal (central).
-   CTRL + T - define o foco o nó superior no painel de navegação. Se o foco já estiver nesse painel, ele será definido para o último nó que você visitou.
-   CTRL + I - define o foco para a barra de trilha, abaixo da faixa de opções.
-   CTRL + L - define o foco para o campo **Pesquisa**, quando estiver disponível.
-   CTRL + D - define o foco para o painel de detalhes, quando estiver disponível.
-   ALT – altera o foco para dentro e fora da faixa de opções.

**Aprimoramentos gerais:**
-   Melhora a navegação no painel de navegação quando você digita as letras de um nome de nó.
-   A navegação por teclado no modo de exibição principal e na faixa de opções agora é circular.
-   Agora, a navegação por teclado no painel de detalhes é circular. Para retornar ao painel ou objeto anterior, use Ctrl + D, depois, Shift + TAB.
-   Depois de atualizar um modo de exibição do Workspace, o foco é definido para o painel principal desse workspace.
-   Correção de um problema para permitir que os leitores de tela anunciem os nomes dos itens de lista.
-   Adição de nomes acessíveis para vários controles na página, o que permite aos leitores de tela anunciarem informações importantes.


## <a name="changes-to-the-azure-services-wizard-to-support-upgrade-readiness"></a>Alterações no Assistente dos Serviços do Azure para oferecer suporte ao Upgrade Readiness
<!-- 1353331 --> Começando nesta versão, use o Assistente dos Serviços do Azure para configurar uma conexão do Configuration Manager com o [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics). O uso do assistente simplifica a configuração do conector usando um assistente comum para serviços relacionados do Azure.   

Embora o método para configurar a conexão tenha mudado, os pré-requisitos de conexão e do modo como você usa o Upgrade Readiness permanecem inalterados.   

### <a name="prerequisites-for-upgrade-readiness"></a>Pré-requisitos para o Upgrade Readiness
Os pré-requisitos para uma [conexão com o Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics#create-a-connection-to-upgrade-readiness) são os mesmos detalhados para o Branch Atual do Configuration Manager. Repetimos eles aqui para sua conveniência:  

**Pré-requisitos**
-   Para adicionar a conexão, seu ambiente do Configuration Manager deve configurar primeiro um [ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) em um [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation). Quando você adiciona a conexão ao seu ambiente, ele também instalará o Microsoft Monitoring Agent no computador que executa essa função de sistema de sites.
-   Registre o Configuration Manager como uma ferramenta de gerenciamento "Aplicativo Web e/ou API Web" e obtenha a [ID do cliente desse registro](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
-   Crie uma chave de cliente para a ferramenta de gerenciamento registrada no Azure Active Directory.
-   No Portal de Gerenciamento do Azure, forneça o aplicativo Web registrado com permissão para acessar o OMS, conforme descrito em [Fornecer ao Configuration Manager as permissões para OMS](https://azure.microsoft.com/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

> [!IMPORTANT]       
> Ao configurar a permissão para acessar o OMS, certifique-se de escolher a função **Colaborador** e atribua a ela permissões para o grupo de recursos do aplicativo registrado.

Após a configuração dos pré-requisitos, você estará pronto para usar o Assistente para criar a conexão.

### <a name="use-the-azure-services-wizard-to-configure-upgrade-readiness"></a>Use o Assistente dos Serviços do Azure para configurar o Upgrade Readiness
1.  No console, acesse **Administração** > **Visão geral** > **Serviços de Nuvem** > **Serviços do Azure** e, em seguida, escolha **Configurar Serviços do Azure**, na guia **Início** da faixa de opções, para iniciar o **Assistente de Serviços do Azure**.

2.  Na página de **Serviços do Azure**, selecione **Conector do Upgrade Readiness** e clique em **Próxima**.

3.  Na página **Aplicativo**, especifique seu **Ambiente do Azure** (a visualização técnica oferece suporte somente à nuvem pública). Depois, clique em **Importar** para abrir o a janela **Importar Aplicativos**.

4.  Na janela **Importar Aplicativos**, especifique os detalhes de um aplicativo Web que já existe em seu Azure AD.
    -   Forneça um nome amigável para o Nome de Locatário do Azure AD. Em seguida, especifique a ID do Locatário, o Nome do Aplicativo, a ID do Cliente, a chave secreta para o aplicativo Web do Azure e o URI do ID do Aplicativo.
    -   Clique em **Verificar** e, após o sucesso, clique em **OK** para continuar.

5.   Na página **Configuração**, especifique a assinatura, o grupo de recursos e o Workspace do Windows Analytics que você quer usar com esta conexão com o Upgrade Readiness.  

6.  Clique em **Avançar** para acessar a página **Resumo** e, em seguida, conclua o assistente para criar a conexão.


## <a name="new-client-settings-for-cloud-services"></a>Novas configurações de cliente para serviços de nuvem
<!-- 1319883 -->

Nesta versão, adicionamos duas novas configurações de cliente para o Configuration Manager. Você as encontrará na seção **Serviços de Nuvem**.  Essas configurações fornecem os seguintes recursos:

- Controle quais clientes do Configuration Manager podem acessar um gateway de gerenciamento de nuvem configurado.
- Registre automaticamente os clientes do Configuration Manager ingressados em um domínio do Windows 10 com o Azure Active Directory.

Essas novas configurações ajudam você a usar os recursos descritos em [Visualização Técnica 1705 do Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1705#new-capabilities-for-azure-ad-and-cloud-management).

### <a name="before-you-start"></a>Antes de começar

Você deve ter instalado e configurado o Azure AD Connect entre o Active Directory local e seu locatário do Azure AD.

Se você remover a conexão, o registro dos dispositivos não será cancelado, mas nenhum dispositivo novo será registrado.

### <a name="try-it-out"></a>Experimente!

1. Defina a seguinte seção de configurações de cliente (encontradas nos Serviços de Nuvem) usando as informações em [Como definir as configurações de cliente](/sccm/core/clients/deploy/configure-client-settings).
    -   **Registrar automaticamente os novos dispositivos ingressados em domínio do Windows 10 com o Azure Active Directory** – Defina como **Sim** (padrão) ou **Não**.
    -   **Habilitar clientes a usar um gateway de gerenciamento de nuvem** – Defina como **Sim** (padrão) ou **Não**.
2.  Implante as configurações do cliente na coleção necessária de dispositivos.

Para confirmar o ingresso do dispositivo ao Azure AD, execute o comando **dsregcmd.exe /status** em uma janela do prompt de comando. O campo **AzureAdjoined** nos resultados mostrarão **Sim** se o dispositivo tiver ingressado no Azure AD.

## <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Criar e executar scripts do PowerShell do console do Configuration Manager
<!-- 1236459 -->

No Configuration Manager, você pode implantar scripts em dispositivos de cliente usando pacotes e programas. Nesta visualização técnica, adicionamos uma nova funcionalidade que permite a execução das seguintes ações:

- Importar scripts do PowerShell no Configuration Manager
- Editar os scripts no console do Configuration Manager (apenas para scripts não assinados)
- Marcar scripts como aprovados ou negados, a fim de melhorar a segurança
- Execute scripts em coleções de computadores de cliente com Windows e em computadores com Windows gerenciados localmente. Você não implanta os scripts, em vez disso, eles são executados quase em tempo real nos dispositivos cliente.
- Examine os resultados retornados pelo script no console do Configuration Manager.


### <a name="prerequisites"></a>Pré-requisitos

Para usar scripts, você deve ser membro da função de segurança apropriada do Configuration Manager.

- **Para importar e criar scripts** - sua conta deve ter as permissões **Criar** para **Scripts SMS** na função de segurança **Administrador Completo**.
- **Para importar ou negar scripts** - sua conta deve ter as permissões **Aprovar** para **Scripts SMS** na função de segurança **Administrador Completo**.
- **Para executar scripts** - sua conta deve ter permissões de **Execução de Script** para **Coleções** na função de segurança **Gerenciador de Configurações de Conformidade**.

Para saber mais sobre as funções de segurança do Configuration Manager, confira [Conceitos básicos da administração baseada em funções para o System Center Configuration Manager](/sccm/core/understand/fundamentals-of-role-based-administration).

Por padrão, os usuários não podem aprovar um script que criaram. Como os scripts são poderosos, versáteis e podem ser implantados em vários dispositivos, apresentamos um novo conceito para a capacidade de separar as funções entre a pessoa que cria o script, e a pessoa que aprova o script. Isso proporciona um nível a mais de segurança contra a execução de um script sem supervisão. Você pode desativar essa aprovação secundária, para facilitar o teste, especialmente durante o lançamento da Visualização Técnica.

Para permitir que os usuários aprovem seus próprios scripts:

1. No console do Configuration Manager, clique em **Administração**.
2. No workspace **Administração**, expanda **Configuração do Site** e clique em **Sites**.
3. Na lista de sites, escolha seu site e, depois, na guia **Início**, no grupo **Sites**, clique em **Configurações de Hierarquia**.
4. Na guia **Geral** da caixa de diálogo **Propriedades das Configurações de Hierarquia**, desmarque a caixa de seleção **Não permitir que os autores de script aprovem seus próprios scripts**.


### <a name="try-it-out"></a>Experimente!

#### <a name="import-and-edit-a-script"></a>Importar e editar um script

1. No console do Configuration Manager, clique em **Biblioteca de Software**.
2. No workspace **Biblioteca de Software**, clique em **Scripts**.
3. Na guia **Início**, no grupo **Criar**, clique em **Criar Script**.
4. Na página **Script** do assistente **Criar Script**, configure o seguinte:
    - **Nome do Script** - insira um nome para o script. Embora você possa criar vários scripts com o mesmo nome, isso dificultará mais a localização do script necessário no console do Configuration Manager.
    - **Linguagem do script** - atualmente, apenas scripts do **PowerShell** têm suporte.
    - **Importar** - importe um script do PowerShell no console. O script é exibido no campo **Script**.
    - **Limpar** - remove o script atual do campo **Script**.
    - **Script** - exibe o script importado no momento. Edite o script neste campo conforme o necessário.
5. Conclua o assistente. O novo script é exibido na lista **Script** com um status de **Aguardando aprovação**. Antes de executar esse script em dispositivos cliente, você deve aprová-lo.


#### <a name="approve-or-deny-a-script"></a>Aprovar ou negar um script



Antes de poder executar um script, ele deve ser aprovado. Para aprovar um script:

1. No console do Configuration Manager, clique em **Biblioteca de Software**.
2. No workspace **Biblioteca de Software**, clique em **Scripts**.
3. Na lista **Script**, escolha o script que você quer aprovar ou negar e, na guia **Início**, no grupo **Script**, clique em **Aprovar/Negar**.
4. Na caixa de diálogo **Aprovar ou negar script**, **Aprove** ou **Negue** o script e, opcionalmente, insira um comentário sobre a sua decisão. Se você negar um script, ele não poderá ser executado em dispositivos cliente.
5. Conclua o assistente. Na lista **Script**, você verá a coluna **Estado de Aprovação** mudar dependendo da ação executada.

#### <a name="run-a-script"></a>Executar um script

Após a aprovação de um script, ele poderá ser executado em uma coleção que você escolher.

1. No console do Configuration Manager, clique em **Ativos e Conformidade**.
2. No workspace **Ativos e Conformidade**, clique em **Coleções de Dispositivos**.
3. Na lista **Coleções de Dispositivos**, clique na coleção de dispositivos na qual você deseja executar o script.
3. Na guia **Início**, no grupo **Todos os Sistemas**, clique em **Executar Script**.
4. Na página **Script** do assistente **Executar Script**, escolha um script na lista. Somente scripts aprovados são exibidos. Clique em **Avançar** e conclua o assistente.

#### <a name="monitor-a-script"></a>Monitorar um script

Depois de executar um script nos dispositivos cliente, use este procedimento para monitorar o sucesso da operação.

1. No console do Configuration Manager, clique em **Monitoramento**.
2. No workspace **Monitoramento**, clique em **Resultados do Script**.
3. Na lista **Resultados do Script**, veja os resultados de cada script executado em dispositivos cliente. Um código de saída do script **0** geralmente indica que o script foi executado com êxito.

## <a name="pxe-network-boot-support-for-ipv6"></a>Suporte de inicialização de rede PXE para IPv6
<!-- 1269793 --> Agora você pode habilitar o suporte à inicialização de rede do PXE para IPv6 para iniciar uma sequência de tarefas de implantação de sistema operacional. Quando você usa essa configuração, os pontos de distribuição habilitados para PXE oferecerá suporte para IPv4 e IPv6. Essa opção não exige WDS e interromperá o WDS, se ele estiver presente.

#### <a name="to-enable-pxe-boot-support-for-ipv6"></a>Para habilitar o suporte à inicialização de PXE para IPv6
Use o procedimento a seguir para habilitar a opção de suporte a IPv6 para PXE.

1. No console do Configuration Manager, acesse **Administração** > **Visão geral** > **Pontos de Distribuição** e clique em **Propriedades** para os pontos de distribuição habilitados para PXE.
2. Na guia **PXE**, selecione **Suporte a IPv6** para habilitar o suporte a IPv6 para PXE.

## <a name="manage-microsoft-surface-driver-updates"></a>Gerenciar atualizações de driver do Microsoft Surface
<!-- 1098490 --> Agora você pode usar o Configuration Manager para gerenciar atualizações de driver do Microsoft Surface.

### <a name="prerequisites"></a>Pré-requisitos
Todos os pontos de atualização de software devem executar o Windows Server 2016.

### <a name="try-it-out"></a>Experimente!
Tente concluir as tarefas a seguir e, depois, envie-nos **Comentários** usando a guia **Início** da Faixa de Opções para nos contar foi:
1. Habilite a sincronização para os drivers do Microsoft Surface. Use o procedimento em [Configurar classificação e produtos](/sccm/sum/get-started/configure-classifications-and-products) e selecione **Incluir drivers e atualizações de firmware do Microsoft Surface** na guia **Classificações** para habilitar os drivers do Surface.
2. [Sincronizar os drivers do Microsoft Surface](/sccm/sum/get-started/synchronize-software-updates.md).
3. [Implantar os drivers sincronizados do Microsoft Surface](/sccm/sum/deploy-use/deploy-software-updates)

## <a name="configure-windows-update-for-business-deferral-policies"></a>Configurar as políticas de adiamento do Windows Update for Business
<!-- 1290890 --> Agora você pode configurar as políticas de adiamento para as Atualizações de Recurso do Windows 10 ou Atualizações de Qualidade para dispositivos com Windows 10 gerenciados diretamente pelo Windows Update for Business. Você pode gerenciar as políticas de adiamento no novo nó **Políticas do Windows Update for Business** em **Biblioteca de Software** > **Manutenção do Windows 10**.

### <a name="prerequisites"></a>Pré-requisitos
Os dispositivos com Windows 10 gerenciados pelo Windows Update for Business devem ter conectividade com a Internet.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Para criar uma política de adiamento do Windows Update for Business
1. Em **Biblioteca de Software** > **Manutenção do Windows 10** > **Políticas do Windows Update for Business**
2. Na guia **Início**, no grupo **Criar**, selecione **Criar a Política do Windows Update for Business** para abrir o Assistente de criação de política do Windows Update for Business.
3. Na página **Geral**, forneça um nome e uma descrição para a política.
4. Na página **Políticas de Adiamento**, defina se deseja adiar ou pausar as Atualizações de Recurso.    
    Normalmente, as Atualizações de Recurso são recursos novos do Windows. Depois de definir a configuração **Nível de preparação do branch**, defina se, e por quanto tempo, você quer adiar o recebimento de Atualizações de Recurso após a disponibilização da Microsoft.
    - **Nível de preparação do branch**: defina o branch para o qual o dispositivo receberá atualizações do Windows (Branch Atual ou Branch Atual para Negócios).
    - **Período de adiamento (dias)**:  especifique o número de dias durante os quais as Atualizações de Recurso serão adiadas. Você pode adiar o recebimento dessas Atualizações de Recurso por um período de 180 dias a partir do lançamento.
    - **Pausar atualizações de recursos a partir de**: selecione se você quer pausar o recebimento de Atualizações de Recursos nos dispositivos durante um período de até 60 dias a contar do momento que você pausar as atualizações. Após o número máximo de dias, a funcionalidade de pausa expirará automaticamente, e o dispositivo verificará no Windows Update se há atualizações aplicáveis. Após essa verificação, você poderá pausar as atualizações novamente. Retome as Atualizações de Recurso desmarcando a caixa de seleção.   
5. Escolha se deseja adiar ou pausar as Atualizações de Qualidade.     
    Normalmente, as Atualizações de Qualidade são correções e aprimoramentos funcionalidades existentes do Windows, e geralmente são publicadas na primeira terça-feira de cada mês, embora possam ser liberadas a qualquer momento pela Microsoft. Você pode definir se, e por quanto tempo, deseja adiar o recebimento das Atualizações de Qualidade após sua disponibilização.
    - **Período de adiamento (dias)**: especifique o número de dias durante os quais as Atualizações de Recurso serão adiadas. Você pode adiar o recebimento dessas Atualizações de Recurso por um período de 180 dias a partir do lançamento.
    - **Pausar atualizações de qualidade a partir de**: selecione se você quer pausar o recebimento de Atualizações de Qualidade nos dispositivos durante um período de até 35 dias a contar do momento que você pausar as atualizações. Após o número máximo de dias, a funcionalidade de pausa expirará automaticamente, e o dispositivo verificará no Windows Update se há atualizações aplicáveis. Após essa verificação, você poderá pausar as atualizações novamente. Retome as Atualizações de Qualidade desmarcando a caixa de seleção.
6. Selecione **Instalar as atualizações de outros produtos da Microsoft** para habilitar a configuração da política de grupo que torna as configurações de adiamento aplicáveis ao Microsoft Update, bem como para o Windows Update.
7. Selecione **Incluir drivers com o Windows Update** para atualizar automaticamente os drivers de Windows Updates. Se você desmarcar essa configuração, as atualizações de driver não serão baixadas do Windows Update.
8. Conclua o assistente para criar a nova política de adiamento.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Para implantar uma política de adiamento do Windows Update for Business
1. Em **Biblioteca de Software** > **Manutenção do Windows 10** > **Políticas do Windows Update for Business**
2. Na guia **Início**, no grupo **Implantação**, selecione **Implantar a Política do Windows Update for Business**.
3. Defina as seguintes configurações:
    - **Política de configuração para implantação**: selecione a política do Windows Update para Empresas que você deseja implantar.
    - **Coleta**: clique em **Procurar** para selecionar a coleção de usuários na qual você deseja implantar a política.
    - **Corrigir regras não compatíveis quando houver suporte**: selecione para corrigir automaticamente quaisquer regras não compatíveis com o WMI (Instrumentação de Gerenciamento do Windows), o Registro, os scripts e todas as configurações de dispositivos móveis registrados pelo Configuration Manager.
    - **Permitir correção fora da janela de manutenção**: se uma janela de manutenção tiver sido configurada para a coleção na qual você está implantando a política, habilite esta opção para permitir que as configurações de conformidade corrijam o valor fora da janela de manutenção. Para obter mais informações sobre janelas de manutenção, consulte [Como usar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).
    - **Gerar um alerta**: configurará um alerta gerado se a conformidade da linha de base de configuração for menor que um percentual especificado por uma data e hora determinadas. Você também pode especificar se deseja que um alerta seja enviado para o System Center Operations Manager.
    - **Atraso aleatório (horas)**: especifica uma janela de atraso para evitar o processamento excessivo no Serviço de Registro de Dispositivo de Rede. O valor padrão é de 64 horas.
    - **Agendamento**: especifique o agendamento de avaliação de conformidade com base no qual o perfil implantado será avaliado em computadores cliente. O agendamento poderá ser simples ou personalizado. O perfil será avaliado por computadores cliente quando o usuário fizer logon.
4.  Conclua o assistente para implantar o perfil.



## <a name="support-for-entrust-certification-authorities"></a>Suporte para autoridades de certificação Entrust
<!-- 1350740 --> Agora, o Configuration Manager dá suporte a autoridades de certificação Entrust; isso permite a entrega de certificados PFX a dispositivos registrados no Microsoft Intune.

Você pode configurar o Entrust como a autoridade de certificação ao adicionar a função Ponto de Registro de Certificado no Configuration Manager. Ao adicionar um novo perfil de certificado que emite os certificados PFX, você pode selecionar uma autoridade de certificação Microsoft ou Entrust.

**Problema conhecido**: na Technical Preview 1706, os certificados PFX não são emitidos para autoridades de certificação da Microsoft. Isso não afeta os certificados PFX importados ou perfis SCEP.


## <a name="cisco-ipsec-support-for-ios-vpn-profiles"></a>Suporte do Cisco (IPsec) para perfis VPN do iOS
<!-- 1321367 -->

Você pode criar um perfil VPN do iOS com Cisco (IPsec) como o tipo de conexão. Para saber mais, confira [Criar perfis VPN](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).


## <a name="new-windows-configuration-item-settings"></a>Novas definições de item de configuração do Windows
<!-- 1354715 -->

Nesta versão, adicionamos as novas configurações a seguir, que você pode usar nos itens de configuração do Windows:

### <a name="password"></a>Senha

- **Criptografia de dispositivo**

### <a name="device"></a>Dispositivo

- **Modificação das configurações de região (somente desktop)**
- **Modificação das configurações de energia e suspensão**
- **Modificação das configurações de idioma**
- **Modificação do horário do sistema**
- **Modificação do nome do dispositivo**

### <a name="store"></a>Repositório

- **Atualização automática de aplicativos da store**
- **Usar somente armazenamento particular**
- **Inicialização de aplicativo proveniente do armazenamento**

### <a name="microsoft-edge"></a>Microsoft Edge

- **Bloquear o acesso a sinalizadores about:**
- **Substituição de prompt SmartScreen**
- **Substituição de prompt SmartScreen para arquivos**
- **Endereço IP do localhost WebRTC**
- **Mecanismo de pesquisa padrão**
- **URL de XML OpenSearch**
- **Home pages (somente desktop)**

Para saber mais sobre configurações de conformidade, veja [Assegurar a conformidade do dispositivo](/sccm/compliance/understand/ensure-device-compliance).


## <a name="new-device-compliance-policy-rules"></a>Novas regras de política de conformidade do dispositivo

* **Tipo de senha necessária**. Especifica se o usuário deve criar uma senha alfanumérica ou numérica. Para senhas alfanuméricas, especifique também o número mínimo de conjuntos de caracteres que a senha deverá conter. Os quatro conjuntos de caracteres são: letras minúsculas, maiúsculas, símbolos e números.

    **Com suporte em:**
    * Windows Phone 8+
    * Windows 8.1+
    * iOS 6+
<br></br>
* **Bloquear a depuração de USB no dispositivo**. Você não precisa definir essas configurações, pois a depuração de USB já está desabilitada em dispositivos com Android for Work.

    **Com suporte em:**
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
<br></br>
* **Bloquear aplicativos de fontes desconhecidas**. Exija que dispositivos impeçam a instalação de aplicativos de fontes desconhecidas. Você não precisa definir essa configuração, pois os dispositivos com Android for Work sempre restringem a instalação de fontes desconhecidas.

    **Com suporte em:**
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
<br></br>
* **Exigir verificação de ameaças em aplicativos**. Essa configuração especifica que o recurso Verificar aplicativos fique habilitado no dispositivo.

    **Com suporte em:**
    * Android 4.2 a 4.4
    * Samsung KNOX Standard 4.0+

Confira [criar e implantar uma política de conformidade do dispositivo](https://docs.microsoft.com/sccm/mdm/deploy-use/create-compliance-policy) para experimentar as novas regras de conformidade do dispositivo.

## <a name="new-mobile-application-management-policy-settings"></a>Novas configurações de política de gerenciamento de aplicativo móvel
A partir desta versão, você pode usar três novas configurações de política MAM (gerenciamento de aplicativo móvel):

- **Bloquear captura de tela (somente para dispositivos Android):** Especifica que as funcionalidades de captura de tela do dispositivo sejam bloqueadas durante o uso do aplicativo.

- **Desabilitar sincronização de contato:** impede que o aplicativo salve dados no aplicativo Contatos nativo do dispositivo.

- **Desabilitar impressão:** impede que o aplicativo imprima dados corporativos ou de estudante.

Veja [proteger aplicativos usando políticas de proteção de aplicativos no Configuration Manager](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies) para testar as novas configurações de política de proteção do aplicativo.

## <a name="android-and-ios-enrollment-restrictions"></a>Restrições de inscrição do Android e iOS
<!-- 1290826 --> Começando nessa versão, os administradores podem especificar que os usuários não podem inscrever dispositivos Android ou iOS pessoais no ambiente híbrido. Isso permite que você limite os dispositivos inscritos a dispositivos da empresa ou iOS previamente declarados inscritos somente com o Programa de registro do dispositivos.

### <a name="try-it-out"></a>Experimente
1. No console do Configuration Manager, no workspace **Administração**, acesse **Serviços de Nuvem** > **Assinatura do Microsoft Intune**.
2. Na guia **Início** do grupo **Assinatura**, escolha **Configurar Plataformas** e selecione **Android** ou **iOS**.
3. Selecione **Bloquear dispositivos de propriedade pessoal**.

## <a name="android-for-work-application-management-policy-for-copy-paste"></a>Política de gerenciamento de aplicativos do Android for Work para copiar e colar
Atualizamos as descrições de configuração de itens de configuração do Android for Work para **Permitir compartilhamento de dados entre o perfil de trabalho e pessoal**.

|Antes da Visualização Técnica 1706 | Nome da nova opção | Comportamento|
|-|-|-|
|Impeça compartilhamentos entre limites| Restrições de compartilhamento padrão| Trabalho para pessoal: padrão (espera-se o bloqueio em todas as versões) <br>Pessoal para trabalho: padrão (permitido no 6.x+, bloqueado no 5.x)|
|Sem restrições|   Aplicativos no perfil pessoal podem lidar com solicitações de compartilhamento do perfil de trabalho| Trabalho para pessoal: Permitido  <br>Pessoal para trabalho: Permitido|
|Aplicativos no perfil de trabalho podem lidar com solicitações de compartilhamento do perfil pessoal |Aplicativos no perfil de trabalho podem lidar com solicitações de compartilhamento do perfil pessoal |Trabalho para pessoal: Padrão<br>Pessoal para trabalho: Permitido<br>(Útil apenas na 5.x, em que pessoal para trabalho está bloqueado)|

Nenhuma dessas opções impede o comportamento de copiar e colar diretamente. Adicionamos uma configuração personalizada ao serviço e ao aplicativo Portal da Empresa no 1704 que pode ser configurada para impedir ações de copiar e colar. Isso pode ser definido por meio do URI personalizado.

-   OMA-URI:  ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
-   Tipo de valor: Booliano

A definição de DisallowCrossProfileCopyPaste como true impede o comportamento de copiar e colar entre perfis de trabalho e pessoal do Android for Work.

### <a name="try-it-out"></a>Experimente
1. No console do Configuration Manager, selecione **Ativos e Conformidade** > **Visão Geral** > **Configurações de Conformidade** > **Itens de Configuração**.
2. Escolha **Criar** para criar um novo item de configuração e especifique **Nome** e **Android for Work**.
3. Nos grupos de configuração do dispositivo para configuração, selecione **Perfil de Trabalho** e escolha **Próximo**.
4. Selecione o valor para **Permitir o compartilhamento de dados entre perfis pessoais e de trabalho** e conclua o assistente.

## <a name="device-health-attestation-assessment-for-compliance-policies-for-conditional-access"></a>Avaliação do Atestado de Integridade do Dispositivo para políticas de conformidade para acesso condicional
<!-- 1097546 --> Começando nesta versão, você pode usar o status do Atestado de Integridade do Dispositivo como uma regra de política de conformidade para acesso condicional aos recursos da empresa.

### <a name="try-it-out"></a>Experimente
Selecione uma regra de Atestado de Integridade do Dispositivo como parte de uma avaliação de política de conformidade.
