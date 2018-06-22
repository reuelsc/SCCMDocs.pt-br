---
title: 'Gerenciar drivers '
titleSuffix: Configuration Manager
description: Use o catálogo de drivers do Configuration Manager para importar drivers de dispositivo, drivers de grupo em pacotes e distribuir esses pacotes aos pontos de distribuição.
ms.date: 01/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4eb97430bd5d7ae5cc50044f8049f41cb9b4cf08
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351523"
---
# <a name="manage-drivers-in-system-center-configuration-manager"></a>Gerenciar drivers no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager fornece um catálogo de drivers que pode ser usado para gerenciar os drivers de dispositivos do Windows no ambiente do Configuration Manager. É possível usar o catálogo de drivers para importar drivers de dispositivo no Configuration Manager, para agrupá-los em pacotes e para distribuir esses pacotes em pontos de distribuição, dos quais é possível acessá-los ao implantar um sistema operacional. Drivers de dispositivo podem ser acessados quando você instala o sistema operacional integral no computador de destino e quando instala o Windows PE usando uma imagem de inicialização. Os drivers de dispositivo do Windows consistem em um arquivo INF (arquivo de informações) de instalação e arquivos adicionais necessários para dar suporte ao dispositivo. Quando um sistema operacional é implantado, o Configuration Manager obtém as informações de hardware e plataforma para o dispositivo por meio de seu arquivo INF. Use o seguinte para gerenciar drivers em seu ambiente do Configuration Manager.

##  <a name="BKMK_DriverCategories"></a> Categorias de driver de dispositivo  
 Quando você importa drivers de dispositivo, é possível atribuir os drivers de dispositivo a uma categoria. Categorias de driver de dispositivo ajudam a agrupar drivers de dispositivo de uso similar no catálogo de driver. Por exemplo, você pode atribuir todos os drivers de dispositivo do adaptador de rede a uma categoria específica. Em seguida, ao criar uma sequência de tarefas que inclua a etapa [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) , é possível especificar uma categoria específica de drivers de dispositivo. O Configuration Manager faz a varredura do hardware e seleciona os drivers aplicáveis dessa categoria a serem preparados no sistema para uso da Instalação do Windows.  

##  <a name="BKMK_ManagingDriverPackages"></a> Pacotes de driver  
 É possível agrupar drivers de dispositivo semelhantes em pacotes para ajudar a simplificar as implantações de sistema operacional. Por exemplo, você pode decidir criar um pacote de driver para cada fabricante de computador na rede. É possível criar um pacote de driver durante a importação de drivers no catálogo de drivers diretamente no nó **Pacotes de Driver** . Depois de criado, o pacote de driver deverá ser distribuído para pontos de distribuição, de onde os computadores cliente do Configuration Manager podem instalar os drivers conforme forem necessários. Considere o seguinte:  

-   Quando você cria um pacote de driver, o local de origem do pacote deve apontar para um compartilhamento de rede vazio, não usado por outro pacote de driver, e o Provedor de SMS deve ter as permissões de Leitura e Gravação para esse local.  

-   Quando você adiciona drivers de dispositivo em um pacote de driver, o Configuration Manager copia o driver de dispositivo para o local de origem do pacote de driver. Você pode adicionar a um pacote de driver apenas drivers de dispositivo que foram importados e que estão habilitados no catálogo de driver.  

-   Para copiar um subconjunto dos drivers de dispositivo de um pacote de driver existente, crie um novo pacote de driver, adicione o subconjunto de drivers de dispositivo ao novo pacote e distribua o novo pacote em um ponto de distribuição.  

 Use as seções a seguir para criar e gerenciar pacotes de driver.  

###  <a name="CreatingDriverPackages"></a> Criar um pacote de driver  
 Use o procedimento a seguir para criar um novo pacote de driver.  

> [!IMPORTANT]  
>  Para criar um pacote de driver, é necessário ter uma pasta de rede vazia, que não seja usada por outro pacote de driver. Na maioria dos casos, é necessário criar uma nova pasta antes de iniciar este procedimento.  

> [!NOTE]  
>  Ao usar sequências de tarefas para instalar drivers, crie pacotes de driver que contêm menos de 500 drivers de dispositivo.  

 Use o procedimento a seguir para criar um pacote de driver.  

#### <a name="to-create-a-driver-package"></a>Para criar um pacote de driver  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Pacotes de Driver**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Pacote de Driver**.  

4.  Na caixa **Nome** , especifique um nome descritivo para o pacote de driver.  

5.  Na caixa **Comentário** , insira uma descrição opcional para o pacote de driver. Verifique se a descrição fornece informações sobre o conteúdo ou a finalidade do pacote de driver.  

6.  Na caixa **Caminho** , especifique uma pasta de origem para o pacote de driver. Digite o caminho para a pasta de origem no formato UNC (convenção de nomenclatura universal). Cada pacote de driver deve usar uma pasta exclusiva.  

    > [!IMPORTANT]  
    >  A conta do servidor do site deve ter permissões de **Leitura** e **Gravação** para a pasta de origem especificada.  

 O novo pacote de driver não contém drivers. A próxima etapa é adicionar drivers ao pacote.  

 Se o nó **Pacotes de Driver** contiver diversos pacotes, você poderá adicionar pastas ao nó para separar os pacotes em grupos lógicos.  

###  <a name="BKMK_PackageActions"></a> Ações adicionais para pacotes de driver  
 Você pode executar ações adicionais para gerenciar pacotes de driver ao selecionar um ou mais pacotes de driver do nó **Pacotes de Driver** . Essas ações incluem:  

|Ação|Descrição|  
|------------|-----------------|  
|**Criar Arquivo de Conteúdo de Pré-Teste**|Cria arquivos que possam ser usados para importar conteúdo e seus metadados associados manualmente. Usar o conteúdo de pré-teste quando a largura de banda de rede for baixa entre o servidor do site e os pontos de distribuição em que o pacote de driver está armazenado.|  
|**Excluir**|Remove o pacote de driver a partir do **Pacotes de Driver** .|  
|**Distribuir Conteúdo**|Distribui o pacote de driver aos pontos de distribuição, grupos do ponto de distribuição e aos grupos do ponto de distribuição associados a coleções.|  
|**Gerenciar Contas de Acesso**|Adiciona, modifica ou remove contas de acesso do pacote de driver.<br /><br /> Para obter mais informações sobre contas de acesso de pacote, consulte [Contas usadas no Configuration Manager](../../core/plan-design/hierarchy/accounts.md).|  
|**Moverr**|Move pacote de driver para outra pasta do nó **Pacotes de Driver** .|  
|**Atualizar Pontos de Distribuição**|Atualiza o pacote de driver de dispositivo em todos os pontos de distribuição onde o pacote é armazenado. Essa ação copia somente o conteúdo alterado desde a última vez que ele foi distribuído.|  
|**Propriedades**|Abre a caixa de diálogo **Propriedades** , onde é possível verificar e alterar as propriedades e o conteúdo do driver de dispositivo. Por exemplo, é possível alterar o nome e a descrição do driver de dispositivo, habilitá-lo e especificar as plataformas em que o driver de dispositivo pode ser executado.|  

##  <a name="BKMK_DeviceDrivers"></a> Drivers de dispositivo  
 É possível instalar drivers de dispositivo em computadores de destino sem incluí-los na imagem do sistema operacional que está sendo implantada. O Configuration Manager fornece um catálogo de drivers que contém referências a todos os drivers de dispositivos importados para o Configuration Manager. O catálogo de drivers está localizado no espaço de trabalho **Biblioteca de Software** e consiste em dois nós: **Drivers** e **Pacotes de Driver**. O nó **Drivers** lista todos os drivers que você importou no catálogo de drivers. Use esse nó para descobrir os detalhes sobre cada driver importado, modificar os drivers em um pacote de driver ou em uma imagem de inicialização, habilitar ou desabilitar um driver e assim por diante.  

###  <a name="BKMK_ImportDrivers"></a> Importar drivers de dispositivo para o catálogo de drivers  
 Você deve importar drivers de dispositivo no catálogo de drivers para poder usá-los quando implantar um sistema operacional. Para melhor gerenciar seus drivers de dispositivos, importe somente aqueles drivers de dispositivos que pretende instalar como parte da implantação de seu sistema operacional. No entanto, você também pode armazenar várias versões de drivers de dispositivo no catálogo de drivers, de modo a facilitar a atualização dos drivers de dispositivo existentes, quando os requisitos de dispositivo de hardware mudarem em sua rede.  

 Como parte do processo de importação do driver de dispositivo, o Configuration Manager lê as informações do provedor, da classe, da versão, da assinatura, do hardware e da plataforma com suporte associadas ao dispositivo. Por padrão, o driver é nomeado após o primeiro dispositivo de hardware que ele suporta; no entanto, é possível renomeá-lo posteriormente. A lista de plataformas com suporte baseia-se nas informações do arquivo INF do driver. Como a precisão dessas informações pode variar, verifique manualmente se há suporte para o driver de dispositivo após ele ser importado para o catálogo de drivers.  

 Depois de importar drivers de dispositivo para o catálogo, é possível adicioná-los aos pacotes de driver ou aos pacotes de imagens de inicialização.  

> [!IMPORTANT]  
>  Não é possível importar drivers de dispositivo diretamente para uma subpasta do nó **Drivers** . Para importar um driver de dispositivo para uma subpasta, importe primeiro o dispositivo para o nó **Drivers** e mova o driver para a subpasta.  

 Use o procedimento a seguir para importar drivers de dispositivo do Windows.  

#### <a name="to-import-windows-device-drivers-into-the-driver-catalog"></a>Para importar drivers de dispositivo do Windows para o catálogo de drivers  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Drivers**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Importar Driver** para iniciar o **Assistente de Importação de Novo Driver**.  

4.  Na página **Localizar Driver** , especifique as seguintes opções e clique em **Próximo**:  

    -   **Importe todos os drivers no seguinte caminho de rede (UNC)**: Para importar todos os drivers de dispositivo contidos em uma determinada pasta, especifique o caminho de rede para a pasta do driver de dispositivo. Por exemplo:  **\\\servername\folder**.  

        > [!NOTE]  
        >  O processo para importar todos os drivers poderá levar algum tempo se houver muitas pastas e muitos arquivos de driver (.inf).  

    -   **Importar um driver específico**: para importar um determinado driver de uma pasta, especifique o caminho de rede (UNC) para o arquivo .INF do driver de dispositivo do Windows ou o arquivo Txtsetup.oem de armazenamento em massa do driver.  

    -   **Especificar a opção para drivers duplicados**: selecione como você deseja que o Configuration Manager gerencie as categorias de driver quando um driver de dispositivo duplicado for importado.  

    > [!IMPORTANT]  
    >  Ao importar drivers, o servidor do site deve ter permissão de **Leitura** para a pasta; caso contrário, a importação falhará.  

5.  Na página **Detalhes do Driver** , especifique as seguintes opções e clique em **Próximo**:  

    -   **Ocultar drivers que não estão em uma classe de armazen. ou de rede (para imagens de inic.)**: use esta configuração para exibir somente os drivers de armazenamento e de rede e para ocultar outros drivers que geralmente não são necessários para as imagens de inicialização, como um driver de vídeo ou de modem.  

    -   **Ocultar drivers que não são assinados digitalmente**: use esta configuração para ocultar drivers que não são assinados digitalmente.  

    -   Na lista de drivers, selecione os drivers que deseja importar para o catálogo de drivers.  

    -   **Habilitar estes drivers e permitir que os computadores os instalem**: selecione esta configuração para permitir que computadores instalem os drivers de dispositivo. Por padrão, essa caixa de seleção é marcada.  

        > [!IMPORTANT]  
        >  Se um driver de dispositivo estiver causando um problema ou se você desejar suspender a instalação de um driver de dispositivo, você poderá desabilitar o driver de dispositivo desmarcando a caixa **Habilitar estes drivers e permitir que os computadores os instalem** . Você também pode desabilitar drivers após eles serem importados.  

    -   Para atribuir os drivers de dispositivo a uma categoria administrativa para fins de filtragem, como as "Desktops" ou "Notebooks", clique em **Categorias** e selecione uma categoria existente ou crie uma nova. Você também pode usar a atribuição de categoria para configurar os drivers de dispositivo que serão aplicados à implantação pela etapa da sequência de tarefas [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) .  

6.  Na página **Adicionar Driver aos Pacotes** , escolha se deseja adicionar os drivers a um pacote e clique em **Avançar**. Considere o seguinte para adicionar os drivers a um pacote:  

    -   Selecione os pacotes de driver usados para distribuir os drivers de dispositivo.  

         Opcionalmente, clique em **Novo Pacote** para criar um novo pacote de driver. Ao criar um novo pacote de driver, é necessário fornecer um compartilhamento de rede que não esteja sendo usado por outros pacotes de driver.  

    -   Se o pacote já foi distribuído para os pontos de distribuição, clique em **Sim** na caixa de diálogo para atualizar as imagens de inicialização nos pontos de distribuição. Não é possível usar drivers de dispositivo até que eles sejam distribuídos aos pontos de distribuição. Se você clicar em **Não**, será necessário executar a ação **Atualizar Ponto de Distribuição** antes que a imagem de inicialização contenha os drivers atualizados. Se o pacote de driver nunca foi distribuído, você deve clicar em **Distribuir Conteúdo** no nó **Pacotes de Driver** .  

7.  Na página **Adicionar Driver às Imagens de Inicialização** , escolha se deseja adicionar os drivers de dispositivo às imagens de inicialização existentes e clique em **Avançar**. Se você selecionar uma imagem de inicialização, considere o seguinte:  

    > [!NOTE]  
    >  Como melhor prática, adicione somente drivers de dispositivo de rede e de armazenamento em massa às imagens de inicialização para cenários de implantação de sistema operacional.  

    -   Clique em **Sim** na caixa de diálogo para atualizar as imagens de inicialização nos pontos de distribuição. Não é possível usar drivers de dispositivo até que eles sejam distribuídos aos pontos de distribuição. Se você clicar em **Não**, será necessário executar a ação **Atualizar Ponto de Distribuição** antes que a imagem de inicialização contenha os drivers atualizados. Se o pacote de driver nunca foi distribuído, você deve clicar em **Distribuir Conteúdo** no nó **Pacotes de Driver** .  

    -   O Configuration Manager avisará se a arquitetura de um ou mais drivers não corresponder à arquitetura das imagens de inicialização selecionadas. Se elas não corresponderem, clique em **OK** e volte para a página **Detalhes do Driver** para desmarcar os drivers que não correspondem à arquitetura da imagem de inicialização selecionada. Por exemplo, se você selecionar uma imagem de inicialização em base em x64 e x86, todos os drivers devem dar suporte a ambas as arquiteturas. Se você selecionar uma imagem de inicialização com base em x64, todos os drivers devem dar suporte à arquitetura x64.  

        > [!NOTE]  
        >  -   A arquitetura é baseada na arquitetura relatada no .INF do fabricante.  
        > -   Se um driver relatar que dá suporte a ambas as arquiteturas, você poderá importá-lo para qualquer uma das duas imagens de inicialização.  

    -   O Configuration Manager avisará se você adicionar drivers de dispositivo que não são drivers de rede ou de armazenamento a uma imagem de inicialização, pois, na maioria dos casos, eles não são necessários para a imagem de inicialização. Clique em **Sim** para adicionar os drivers à imagem de inicialização ou em **Não** para voltar e modificar sua seleção de driver.  

    -   O Configuration Manager avisará se um ou mais dos drivers selecionados não estiverem assinados digitalmente de maneira correta. Clique em **Sim** para continuar e clique em **Não** para voltar e fazer alterações em sua seleção de driver.  

8.  Conclua o assistente.  

###  <a name="BKMK_ModifyDriverPackage"></a> Gerenciar drivers de dispositivo em um pacote de driver  
 Use os procedimentos a seguir para modificar pacotes de driver e imagens de inicialização. Para adicionar ou remover drivers de dispositivo, localize os drivers no nó **Drivers** e edite os pacotes ou as imagens de inicialização aos quais os drivers selecionados estão associados.  

#### <a name="to-modify-the-device-drivers-in-a-driver-package"></a>Para modificar os drivers de dispositivo em um pacote de driver  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Drivers**.  

3.  No nó **Drivers** , selecione os drivers de dispositivo que deseja adicionar ao pacote de driver.  

4.  Na guia **Início** , no grupo **Driver** , clique em **Editar**e em **Pacotes de Driver**.  

5.  Para adicionar um driver de dispositivo, marque a caixa de seleção dos pacotes de driver aos quais deseja adicionar os drivers de dispositivo. Para remover um driver de dispositivo, desmarque a caixa de seleção dos pacotes de driver dos quais deseja remover o driver de dispositivo.  

     Se estiver adicionado drivers de dispositivo associados a pacotes de driver, você poderá opcionalmente criar um novo pacote, clicando em **Novo Pacote**, o que abrirá a caixa de diálogo **Novo Pacote de Driver** .  

6.  Se o pacote já foi distribuído para os pontos de distribuição, clique em **Sim** na caixa de diálogo para atualizar as imagens de inicialização nos pontos de distribuição. Não é possível usar drivers de dispositivo até que eles sejam distribuídos aos pontos de distribuição. Se você clicar em **Não**, será necessário executar a ação **Atualizar Ponto de Distribuição** antes que a imagem de inicialização contenha os drivers atualizados. Se o pacote de driver nunca foi distribuído, você deve clicar em **Distribuir Conteúdo** no nó **Pacotes de Driver** . Antes que os drivers estejam disponíveis, é necessário atualizar o pacote de driver nos pontos de distribuição.  

     Clique em **OK**.  

###  <a name="BKMK_ManageDriversBootImage"></a> Gerenciar drivers de dispositivo em uma imagem de inicialização  
 É possível adicionar, a imagens de inicialização, drivers de dispositivo do Windows que foram importados no catálogo de driver. Ao adicionar drivers de dispositivo a uma imagem de inicialização, use as seguintes diretrizes:  

-   Adicione somente drivers de dispositivo de armazenamento em massa e adaptador de rede a imagens de inicialização, pois outros tipos de drivers geralmente não são necessários. Drivers não obrigatórios aumentam o tamanho das imagens de inicialização desnecessariamente.  

-   Adicione somente drivers de dispositivo para o Windows 10 a uma imagem de inicialização, pois a versão necessária do Windows PE baseia-se no Windows 10.  

-   Verifique se está usando o driver de dispositivo correto para a arquitetura da imagem de inicialização.  Não adicione um driver de dispositivo x86 a uma imagem de inicialização x64.  

 Use o procedimento a seguir para adicionar ou remover drivers de dispositivo em uma imagem de inicialização.  

#### <a name="to-modify-the--device-drivers-associated-with-a-boot-image"></a>Para modificar drivers de dispositivo associados a uma imagem de inicialização  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Drivers**.  

3.  No nó **Drivers** , selecione os drivers de dispositivo que deseja adicionar ao pacote de driver.  

4.  Na guia **Início** , no grupo **Driver** , clique em **Editar**e em **Imagens de Inicialização**.  

5.  Para adicionar um driver de dispositivo, marque a caixa de seleção da imagem de inicialização à qual deseja adicionar os drivers de dispositivo. Para remover um driver de dispositivo, desmarque a caixa de seleção da imagem de inicialização da qual deseja remover o driver de dispositivo.  

6.  Caso não deseje atualizar os pontos de distribuição onde a imagem de inicialização está armazenada, desmarque a caixa de seleção **Atualizar pontos de distribuição ao terminar** . Por padrão, os pontos de distribuição são atualizados quando a imagem de inicialização é atualizada.  

     Clique em **OK** e considere o seguinte:  

    -   Clique em **Sim** na caixa de diálogo para atualizar as imagens de inicialização nos pontos de distribuição. Não é possível usar drivers de dispositivo até que eles sejam distribuídos aos pontos de distribuição. Se você clicar em **Não**, será necessário executar a ação **Atualizar Ponto de Distribuição** antes que a imagem de inicialização contenha os drivers atualizados. Se o pacote de driver nunca foi distribuído, você deve clicar em **Distribuir Conteúdo** no nó **Pacotes de Driver** .  

    -   O Configuration Manager avisará se a arquitetura de um ou mais drivers não corresponder à arquitetura das imagens de inicialização selecionadas. Se elas não corresponderem, clique em **OK** e volte para a página **Detalhes do Driver** para desmarcar os drivers que não correspondem à arquitetura da imagem de inicialização selecionada. Por exemplo, se você selecionar uma imagem de inicialização em base em x64 e x86, todos os drivers devem dar suporte a ambas as arquiteturas. Se você selecionar uma imagem de inicialização com base em x64, todos os drivers devem dar suporte à arquitetura x64.  

        > [!NOTE]  
        >  -   A arquitetura é baseada na arquitetura relatada no .INF do fabricante.  
        > -   Se um driver relatar que dá suporte a ambas as arquiteturas, você poderá importá-lo para qualquer uma das duas imagens de inicialização.  

    -   O Configuration Manager avisará se você adicionar drivers de dispositivo que não são drivers de rede ou de armazenamento a uma imagem de inicialização, pois, na maioria dos casos, eles não são necessários para a imagem de inicialização. Clique em **Sim** para adicionar os drivers à imagem de inicialização ou em **Não** para voltar e modificar sua seleção de driver.  

    -   O Configuration Manager avisará se um ou mais dos drivers selecionados não estiverem assinados digitalmente de maneira correta. Clique em **Sim** para continuar e clique em **Não** para voltar e fazer alterações em sua seleção de driver.  

7.  Clique em **OK**.  

###  <a name="BKMK_DriverActions"></a> Ações adicionais para drivers de dispositivo  
 Você pode executar ações adicionais para gerenciar drivers de dispositivo ao selecionar um ou mais drivers de dispositivo do nó **Drivers** . Essas ações incluem:  

|Ação|Descrição|  
|------------|-----------------|  
|**Categorizar**|Limpa, gerencia ou define uma categoria administrativa para os drivers de dispositivo selecionados.|  
|**Excluir**|Removes o driver de dispositivo do nó **Drivers** e também remove o driver dos pontos de distribuição associados.|  
|**Desabilitar**|Proíbe o driver de dispositivo de ser instalado. É possível desabilitar drivers de dispositivo temporariamente para que os computadores cliente e as sequências de tarefas do Configuration Manager não possam instalá-los durante a implantação de sistemas operacionais. **Observação:**  a ação Desabilitar apenas impede os drivers de serem instalados usando a etapa da sequência de tarefas Driver de Aplicação Automática.|  
|**Habilitar**|Permite que computadores cliente e sequências de tarefas do Configuration Manager instalem o driver de dispositivo durante a implantação do sistema operacional.|  
|**Moverr**|Move o driver de dispositivo para outra pasta do nó **Drivers** .|  
|**Propriedades**|Abre a caixa de diálogo **Propriedades** , onde é possível verificar e alterar as propriedades do driver de dispositivo. Por exemplo, é possível alterar o nome e a descrição do driver de dispositivo, ativá-lo e especificar as plataformas em que o driver de dispositivo pode ser executado.|  

##  <a name="BKMK_TSDrivers"></a> Usar sequências de tarefas para instalar drivers de dispositivo  
 Use sequências de tarefas para automatizar a forma como o sistema operacional é implantado. Cada etapa na sequência de tarefas pode executar uma ação específica, como instalar um driver de dispositivo. Ao implantar sistemas operacionais, você pode usar as duas etapas de sequência de tarefas a seguir para instalar os drivers de dispositivo:  

-   [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers): essa etapa permite que você combine automaticamente e instale drivers de dispositivo como parte de uma implantação de sistema operacional. Você pode configurar a etapa de sequência de tarefas para instalar somente o driver mais compatível com cada dispositivo de hardware detectado ou especificar que a etapa de sequência de tarefas instale todos os drivers compatíveis com cada dispositivo de hardware detectado, e então deixar que a Instalação do Windows escolha o melhor driver. Além disso, pode especificar uma categoria de drivers de dispositivo para limitar os drivers disponíveis para essa etapa.  

-   [Apply Driver Package](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage): essa etapa permite disponibilizar para a Instalação do Windows todos os drivers de dispositivo de um pacote de driver específico. Nos pacotes de driver especificados, a instalação do Windows busca drivers de dispositivo que são necessários. Ao criar a mídia autônoma, é necessário usar esta etapa para instalar drivers de dispositivo.  

 Ao usar essas etapas de sequência de tarefas, você também pode especificar como os drivers de dispositivo são instalados no computador onde o sistema operacional está sendo implantado. Para obter mais informações, consulte [Gerenciar sequências de tarefas para automatizar tarefas](../deploy-use/manage-task-sequences-to-automate-tasks.md).  

##  <a name="BKMK_InstallingDeviceDiriversTS"></a> Usar sequências de tarefas para instalar drivers de dispositivo em computadores  
 Use o procedimento a seguir para instalar drivers de dispositivo como parte da implantação de sistema operacional.  

#### <a name="use-a-task-sequence-to-install-device-drivers"></a>Usar uma sequência de tarefas para instalar drivers de dispositivo  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  No nó **Sequências de Tarefas** , selecione a sequência de tarefas que você deseja modificar para instalar o driver de dispositivo e clique em **Editar**.  

4.  Mova para o local em que deseja adicionar as etapas do **Driver** , clique em **Adicionar**e selecione **Drivers**.  

5.  Adicione a etapa **Drivers de aplicação automática** se deseja que a sequência de tarefas instale todos os drivers de dispositivo ou categorias específicas que estão especificadas. Especifique as opções da etapa na guia **Propriedades** e quaisquer condições da etapa na guia **Opções** .  

     Adicione a etapa **Aplicar pacote de driver** se desejar que a sequência de tarefas instale somente aqueles drivers de dispositivos do pacote especificado. Especifique as opções da etapa na guia **Propriedades** e quaisquer condições da etapa na guia **Opções** .  

    > [!IMPORTANT]  
    >  Também é possível selecionar **Desabilitar esta etapa** na guia **Opções** para desabilitar a etapa a fim de solucionar problemas na sequência de tarefas.  

6.  Clique em **OK** para salvar a sequência de tarefas.  

 Para obter mais informações sobre como criar uma sequência de tarefas para instalar um sistema operacional, consulte [Create a task sequence to install an operating system (Criar uma sequência de tarefas para instalar um sistema operacional)](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md).  

##  <a name="BKMK_DriverReports"></a> Relatórios de gerenciamento de drivers  
 Na categoria de relatórios **Gerenciamento de driver** , vários relatórios podem ser usados para determinar informações gerais sobre os drivers de dispositivo no catálogo de driver. Para obter mais informações sobre relatórios, consulte [Relatórios](../../core/servers/manage/reporting.md).
