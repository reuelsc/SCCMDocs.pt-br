---
title: Use uma sequência de tarefas para gerenciar discos rígidos virtuais
titleSuffix: Configuration Manager
description: Crie e modifique um VHD, adicione aplicativos e atualizações de software e publique o VHD e no System Center VMM (Virtual Machine Manager) do Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 0212b023-804a-4f84-b880-7a59cdb49c67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49de1e2f94d1016f3c0139ccf534b85a718bf7e0
ms.sourcegitcommit: 3dfe3f4401651afa9dc65d14a8944ae4e4198b3e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48862491"
---
# <a name="use-a-task-sequence-to-manage-virtual-hard-disks-in-system-center-configuration-manager"></a>Use uma sequência de tarefas para gerenciar discos rígidos virtuais no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


   > [!NOTE] 
   >  O suporte para esse recurso foi preterido na versão 1710. Para obter mais informações, confira [Recursos removidos e preteridos do Configuration Manager](https://docs.microsoft.com/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).

No System Center Configuration Manager, é possível gerenciar VHDs (discos rígidos virtuais) e integrar os VHDs que você criou no seu datacenter do console do Configuration Manager. Especificamente, é possível criar e modificar um VHD, adicionar aplicativos e atualizações de software ao VHD e publicar o VHD no System Center VMM (Virtual Machine Manager) por meio do console do Configuration Manager.  

 Use as seções a seguir para gerenciar os VHDs no Configuration Manager.

## <a name="prerequisites"></a>Pré-requisitos  
 Antes de começar, verifique os seguintes pré-requisitos:  

-   O computador de onde você gerencia os VHDs deve executar um dos seguintes sistemas operacionais:  

    -   Windows 8.1 x64  

    -   Windows 8 x64  

    -   Windows Server 2008 R2  

    -   Windows Server 2012  

    -   Windows Server 2012 R2  

-   A virtualização deve ser habilitada no BIOS e o Hyper-V deve estar instalado no computador do qual você executa o console do Configuration Manager para gerenciar os VHDs. Como prática recomendada, instale as ferramentas de gerenciamento do Hyper-V para ajudar a testar e a solucionar problemas nos seus discos rígidos virtuais. Por exemplo, para monitorar o arquivo smsts.log para acompanhar o progresso da sequência de tarefas no Hyper-V, você deve ter as ferramentas de gerenciamento do Hyper-V instaladas. Para obter mais informações sobre os requisitos do Hyper-V, consulte [Pré-requisitos de instalação do Hyper-V](http://technet.microsoft.com/library/cc731898.aspx).  

    > [!IMPORTANT]  
    >  O processo para criar um VHD consome tempo do processador e memória. Logo, é recomendável que você gerencie os VHDs de um console do Configuration Manager que não esteja instalado no servidor do site.  

-   O servidor do site deve ter permissão de acesso para **Gravar** na pasta que conterá o arquivo do VHD ao gerenciar VHDs de um computador remoto ao servidor do site.  

-   Verifique se há espaço livre suficiente em disco no computador de onde você gerencia os VHDs. Os requisitos de espaço no disco rígido do VHD variam dependendo do sistema operacional e dos aplicativos que você instalou.  

-   Verifique se há memória suficiente no computador de onde você gerencia os VHDs. Durante o processo para criar o VHD, a máquina virtual é configurada para consumir 2 GB de memória.  

-   Instale o console do System Center Virtual Machine Manager (VMM) no computador de onde você carrega o VHD para o VMM. Você pode instalar o console do VMM em um computador separado de onde gerencia seus VHDs, o que significa que não precisa ter o Hyper-V instalado para importar o VHD no VMM.  

    > [!NOTE]  
    >  Se você instalar o console do VMM enquanto o console do Configuration Manager estiver aberto, será preciso reiniciar o console do Configuration Manager assim que a instalação do console do VMM for concluída. Do contrário, o Configuration Manager não se conectará com êxito ao servidor de gerenciamento do VMM para carregar um VHD.  

##  <a name="BKMK_CreateVHDSteps"></a> Etapas para criar um VHD  
 Para criar um VHD, é necessário criar uma sequência de tarefas que contenha as etapas para criar o VHD e usar a sequência de tarefas no Assistente para Criar Disco Rígido Virtual para criar o VHD. As seções a seguir fornecem as etapas para criar o VHD.  

###  <a name="BKMK_CreateTS"></a> Criar uma sequência de tarefas para o VHD  
 Você deve criar uma sequência de tarefas que contenha as etapas para criar o VHD. No Assistente para Criar Sequência de Tarefas, há a opção **Instalar um pacote da imagem existente em um disco rígido virtual** que cria as etapas a serem usadas para criar o VHD. Por exemplo, o assistente adiciona as seguintes etapas necessárias: Reiniciar no Windows PE, Formatar e particionar o Disco, Aplicar Sistema Operacional e Desligar Computador. Você não pode criar o VHD enquanto está no sistema operacional completo. Além disso, o Configuration Manager deve esperar até que a máquina virtual seja desligada antes de completar o pacote. Por padrão, o assistente espera 5 minutos antes de desligar a máquina virtual. Depois de criar a sequência de tarefas, você pode adicionar outras etapas, se necessário.  

> [!IMPORTANT]  
>  O procedimento a seguir cria a sequência de tarefas usando a opção **Instalar um pacote da imagem existente em um disco rígido virtual** , que inclui automaticamente as etapas necessárias para criar com êxito o VHD. Se você escolher usar uma sequência de tarefas existente ou criar uma manualmente, certifique-se de ter adicionado a etapa Desligar Computador no final da sequência. Sem essa etapa, a máquina virtual temporária não é excluída e o processo de criação do VHD não é concluído. No entanto, o assistente é concluído e relata com êxito.  

 Use o procedimento a seguir para criar a sequência de tarefas para criar o VHD:  

#### <a name="to-create-the-task-sequence-to-create-the-vhd"></a>Para criar a sequência de tarefas para criar o VHD  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Sequência de Tarefas** para iniciar o Assistente para Criar Sequência de Tarefas.  

4.  Na página **Criar uma Nova Sequência de Tarefas** , clique em **Instalar um pacote de imagem existente em um disco rígido virtual**e em **Avançar**.  

5.  Na página **Informações da Sequência de Tarefas** , especifique as seguintes configurações e clique em **Próximo**.  

    -   **Nome da sequência de tarefas**: especifique um nome que identifique a sequência de tarefas.  

    -   **Descrição**: especifique uma descrição da sequência de tarefas.  

    -   **Imagem de inicialização**: especifique a imagem de inicialização que instala o sistema operacional no computador de destino. Para obter mais informações, consulte [Gerenciar imagens de inicialização](../get-started/manage-boot-images.md).  

6.  Na página **Instalar Windows** , especifique as seguintes configurações e clique em **Próximo**.  

    -   **Pacote de imagem**: especifique o pacote que contém a imagem do sistema operacional para instalação.  

    -   **Imagem**: se o pacote de imagens do sistema operacional contém várias imagens, especifique o índice da imagem do sistema operacional para instalação.  

    -   **Chave do produto**: especifique a chave do produto do sistema operacional Windows a instalar. Você pode especificar as chaves de licença de volume codificadas e as chaves do produto padrão. Se você usar uma chave de produto sem codificação, cada grupo de 5 caracteres deverá ser separado por um traço (-). Por exemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **Modo de licenciamento do servidor**: especifique se a licença do servidor é **Por estação**, **Por servidor**ou se nenhuma licença está especificada. Se a licença do servidor for **Por servidor**, especifique também o número máximo de conexões de servidor.  

    -   Especifique como lidar com a conta de administrador usada quando a imagem de sistema operacional é implantada.  

        -   **Gerar aleatoriamente a senha do administrador local e desabilitar a conta em todas as plataformas com suporte (recomendado)**: use essa configuração para que o assistente crie aleatoriamente uma senha para a conta de administrador local e desabilite a conta quando a imagem do sistema operacional for implantada.  

        -   **Ativar a conta e especificar a senha do administrador local**: use essa configuração para usar uma senha específica para a conta de administrador local em todos os computadores nos quais a imagem do sistema operacional será implantada.  

7.  Na página **Configurar a Rede** , especifique as seguintes configurações e clique em **Próximo**.  

    -   **Ingressar no grupo de trabalho**: especifique se deseja adicionar o computador de destino a um grupo de trabalho.  

    -   **Ingressar em um domínio**: especifique se deseja adicionar o computador de destino a um domínio. Em **Domínio**, especifique o nome do domínio.  

        > [!IMPORTANT]  
        >  Você pode localizar os domínios na floresta local, mas, para tanto, é necessário especificar o nome de domínio para uma floresta remota.  

         Você também pode especificar uma UO (unidade organizacional). Essa configuração opcional especifica o nome diferenciado do LDAP X.500 da UO na qual a conta do computador será criada, se ela ainda não existir.  

    -   **Conta**: especifique o nome de usuário e senha para a conta que tenha permissões para ingressar no domínio especificado. Por exemplo: *domain\user* ou *%variable%*.  

8.  Na página **Instalar o Configuration Manager**, especifique o pacote do cliente do Configuration Manager para instalar no computador de destino e clique em **Próximo**.  

9. Na página **Instalar Aplicativos** , especifique os aplicativos a instalar no computador de destino e clique em **Próximo**. Se você especificar vários aplicativos, será possível também definir a continuação da sequência de tarefas em caso de falha na instalação de algum aplicativo.  

10. Conclua o assistente.  

###  <a name="BKMK_CreateVHD"></a> Criar um VHD  
 Criada a sequência de tarefas para o VHD, use o Assistente para Criar Disco Rígido Virtual para criar o VHD.  

> [!IMPORTANT]  
>  Antes de executar este procedimento, verifique se os pré-requisitos relacionados no início do tópico foram atendidos.  

 Use o procedimento a seguir para criar um VHD.  

#### <a name="to-create-a-vhd"></a>Para criar um VHD  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Discos Rígidos Virtuais**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Disco Rígido Virtual** para iniciar o Assistente para Criar Disco Rígido Virtual.  

    > [!NOTE]  
    >  O Hyper-V deve estar instalado no computador que está executando o console do Configuration Manager do qual você gerencia os VHDs ou a opção **Criar Disco Rígido Virtual** não será habilitada. Para obter mais informações sobre os requisitos do Hyper-V, consulte [Pré-requisitos de instalação do Hyper-V](http://technet.microsoft.com/library/cc731898.aspx).  

    > [!TIP]  
    >  Para organizar os seus VHDs, crie uma pasta ou selecione uma já existente no nó **Discos Rígidos Virtuais** e clique em **Criar Disco Rígido Virtual** a partir da pasta.  

4.  Na página **Geral** , especifique as seguintes configurações e clique em **Próximo**.  

    -   **Nome**: especifique um nome exclusivo para o VHD.  

    -   **Versão**: especifique um número de versão para o VHD. Esta é uma configuração opcional.  

    -   **Comentário**: especifique uma descrição para o VHD.  

    -   **Caminho**: especifique o caminho e o nome do arquivo do qual o assistente criará o arquivo VHD.  

         Você deve inserir um caminho de rede válido no formato UNC. Por exemplo: **\\\nomedoservidor\\<nomedocompartilhamento\>\\<nomedoarquivo\>.vhd**.  

        > [!WARNING]  
        >  O Configuration Manager deve ter permissão de acesso para **Gravar** no caminho especificado para criar o VHD. Quando o Configuration Manager não consegue acessar o caminho, ele registra o erro associado no arquivo distmgr.log do servidor do site.  

5.  Na página **Sequência de Tarefas** , especifique a sequência de tarefas que você especificou na seção anterior e clique em **Avançar**.  

6.  Na página **Pontos de Distribuição** , selecione um ou mais pontos de distribuição que possuem o conteúdo exigido pela sequência de tarefas e clique em **Próximo**.  

7.  Na página **Personalização** , clique em **Próximo**. O processo para criar o VHD ignora todas as configurações que você especificar nesta página.  

8.  Verifique as configurações e clique em **Avançar**. O assistente cria o VHD.  

    > [!TIP]  
    >  O tempo para concluir o processo para criar o VHD pode variar. Enquanto o assistente trabalha nesse processo, você pode monitorar os arquivos de log a seguir para acompanhar o progresso. Por padrão, os logs estão localizados no computador que está executando o console do Configuration Manager em %*ProgramFiles(x86)*%\Microsoft Configuration Manager\AdminConsole\AdminUILog.  
    >   
    >  -   **CreateTSMedia.log**: o assistente grava informações nesse log enquanto cria a mídia de sequência de tarefas. Examine esse arquivo de log para acompanhar o progresso do assistente quando ele cria a mídia independente.  
    > -   **DeployToVHD.log**: o assistente grava informações nesse log ao longo do processo de criação do VHD. Examine esse arquivo de log para acompanhar o progresso do assistente por todas as etapas após ele ter criado a mídia independente.  
    >   
    >  Além disso, quando a instalação do sistema operacional começar, você poderá abrir o Hyper-V Manager (se tiver instalado as ferramentas de gerenciamento do Hyper-V no computador) e conectar à máquina virtual temporária criada pelo assistente para ver a sequência de tarefas sendo executada. É possível monitorar, a partir da máquina virtual, o arquivo smsts.log para acompanhar o progresso da sequência de tarefas. Caso ocorra algum problema ao completar a etapa de sequência de tarefas, você pode usar esse arquivo de log para ajudá-lo a solucionar o problema. O arquivo smsts.log fica em x: \windows\temp\smstslog\smsts.log antes da formatação do disco rígido e em c:\\\_SMSTaskSequence\Logs\Smstslog\ depois da formatação. Depois da conclusão das etapas de sequência de tarefas, a máquina virtual é desligada após 5 minutos (por padrão) e excluída.  

 Após o Configuration Manager criar o VHD, ele estará localizado no nó **Discos Rígidos Virtuais** no console do Configuration Manager, no nó **Implantação de Sistema Operacional** no espaço de trabalho **Biblioteca de Software**.  

> [!NOTE]  
>  O Configuration Manager recupera o tamanho do VHD ao se conectar ao local de origem do VHD. Se o Configuration Manager não conseguir acessar o arquivo VHD, **0** será exibido na coluna **Tamanho (KB)** para o VHD.  

##  <a name="BKMK_ModifyVHDSteps"></a> Etapas para modificar um VHD existente  
 Para modificar um VHD, é necessário criar uma sequência de tarefas com as etapas necessárias. Em seguida, selecione a sequência de tarefas no Assistente para Modificar Disco Rígido Virtual. O assistente conecta o VHD à máquina virtual, executa a sequência de tarefas no VHD e atualiza o arquivo VHD. As seções a seguir fornecem as etapas para modificar o VHD.  

###  <a name="BKMK_ModifyTS"></a> Criar uma sequência de tarefas para modificar o VHD  
 Para modificar um VHD existente, você precisa primeiro criar uma sequência de tarefas. Escolha apenas as etapas necessárias para modificar a sequência de tarefas. Por exemplo, se você deseja adicionar um aplicativo ao VHD, crie uma sequência de tarefas personalizada e, feito isso, adicione apenas a etapa Instalar Aplicativo.  

 Use o procedimento a seguir para criar a sequência de tarefas para modificar o VHD.  

#### <a name="to-create-a-custom-task-sequence-to-modify-the-vhd"></a>Para criar uma sequência de tarefas personalizada para modificar o VHD  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Sequência de Tarefas** para iniciar o Assistente para Criar Sequência de Tarefas.  

4.  Na página **Criar uma Nova Sequência de Tarefas** , selecione **Criar uma Nova Sequência de Tarefas Personalizada**e clique em **Próximo**.  

5.  Na página **Informações da Sequência de Tarefas** , especifique as seguintes configurações e clique em **Próximo**.  

    -   **Nome da sequência de tarefas**: especifique um nome que identifique a sequência de tarefas.  

    -   **Descrição**: especifique uma descrição da sequência de tarefas.  

    -   **Imagem de inicialização**: especifique a imagem de inicialização que instala o sistema operacional no computador de destino. Para obter mais informações, consulte [Gerenciar imagens de inicialização](../get-started/manage-boot-images.md).  

6.  Conclua o assistente.  

 Use o procedimento a seguir para adicionar etapas de sequência de tarefas para a sequência de tarefas personalizada.  

#### <a name="to-add-task-sequence-steps-to-the-custom-task-sequence"></a>Para adicionar etapas de sequência de tarefas para a sequência de tarefas personalizada  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**, clique em **Sequências de Tarefas**e selecione a sequência de tarefas personalizada que você criou no procedimento anterior.  

3.  Na guia **Início** , no grupo **Sequência de Tarefas** , clique em **Editar** para iniciar o editor de sequência de tarefas.  

4.  Adicione as etapas da sequência de tarefas a usar para modificar o VHD.  

5.  Clique em **OK** para sair do editor de sequência de tarefas.  

###  <a name="BKMK_ModifyVHD"></a> Modificar um VHD  
 Criada a sequência de tarefas para o VHD, use o Assistente para Modificar Disco Rígido Virtual para modificar o VHD.  

 Use o procedimento a seguir para modificar um VHD.  

#### <a name="to-modify-a-vhd"></a>Para modificar um VHD  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**, clique em **Discos Rígidos Virtuais**e selecione o VHD a modificar.  

3.  Na guia **Início** , no grupo **Disco Rígido Virtual** , clique em **Modificar Disco Rígido Virtual** para iniciar o Assistente para Modificar Disco Rígido Virtual.  

    > [!NOTE]  
    >  O Hyper-V deve estar instalado no computador que está executando o console do Configuration Manager de onde você gerencia os VHDs ou a opção **Modificar Disco Rígido Virtual** não será habilitada. Para obter mais informações sobre os requisitos do Hyper-V, consulte [Pré-requisitos de instalação do Hyper-V](http://technet.microsoft.com/library/cc731898.aspx).  

4.  Na página **Geral** , confirme as seguintes configurações e clique em **Próximo**.  

    -   **Nome**: especifica o nome exclusivo para o VHD.  

    -   **Versão**: especifica o número de versão para o VHD. Esta é uma configuração opcional.  

    -   **Comentário**: especifica a descrição para o VHD.  

    -   **Caminho**: especifica o caminho e o nome do arquivo para onde está localizado o arquivo VHD. Não é possível modificar essa configuração.  

        > [!WARNING]  
        >  O Configuration Manager deve ter permissão de acesso para **Gravar** no caminho especificado para criar o VHD. Quando o Configuration Manager não consegue acessar o caminho, ele registra o erro associado no arquivo distmgr.log do servidor do site.  

5.  Na página **Sequência de Tarefas** , especifique a sequência de tarefas personalizada que você criou na seção anterior e clique em **Próximo**.  

6.  Na página **Pontos de Distribuição** , selecione um ou mais pontos de distribuição que possuem o conteúdo exigido pela sequência de tarefas e clique em **Próximo**.  

7.  Na página **Personalização** , clique em **Próximo**. O processo para modificar o VHD ignora todas as configurações que você especificar nesta página.  

8.  Verifique as configurações e clique em **Avançar**. O assistente cria o VHD modificado.  

    > [!TIP]  
    >  O tempo para concluir o processo para modificar o VHD pode variar. Enquanto o assistente trabalha nesse processo, você pode monitorar os arquivos de log a seguir para acompanhar o progresso. Por padrão, os logs estão localizados no computador que está executando o console do Configuration Manager em %*ProgramFiles(x86)*%\Microsoft Configuration Manager\AdminConsole\AdminUILog.  
    >   
    >  -   **CreateTSMedia.log**: o assistente grava informações nesse log enquanto cria a mídia de sequência de tarefas. Examine esse arquivo de log para acompanhar o progresso do assistente quando ele cria a mídia independente.  
    > -   **DeployToVHD.log**: o assistente grava informações nesse log ao longo do processo de modificação do VHD. Examine esse arquivo de log para acompanhar o progresso do assistente por todas as etapas após ele ter criado a mídia independente.  
    >   
    >  Além disso, você poderá abrir o Hyper-V Manager (se tiver instalado as ferramentas de gerenciamento do Hyper-V no computador) e conectar-se à máquina virtual temporária criada pelo assistente para ver a sequência de tarefas em execução. É possível monitorar, a partir da máquina virtual, o arquivo smsts.log para acompanhar o progresso da sequência de tarefas. Caso ocorra algum problema ao completar a etapa de sequência de tarefas, você pode usar esse arquivo de log para ajudá-lo a solucionar o problema. O arquivo smsts.log fica em x: \windows\temp\smstslog\smsts.log antes da formatação do disco rígido e em c:\\\_SMSTaskSequence\Logs\Smstslog\ depois da formatação. Depois da conclusão das etapas de sequência de tarefas, a máquina virtual é desligada após 5 minutos (por padrão) e excluída.  

##  <a name="BKMK_ApplyUpdates"></a> Aplicar atualizações de software a um VHD  
 Periodicamente, são lançadas novas atualizações de software que se aplicam ao sistema operacional em seu VHD. Você pode aplicar as atualizações de software aplicáveis a um VHD em um agendamento especificado. No agendamento especificado, o Configuration Manager aplica as atualizações de software selecionadas para o VHD.  

 As informações sobre o VHD são armazenadas no banco de dados do site, incluindo as atualizações de software que foram aplicadas no momento da criação do VHD. As atualizações de software que foram aplicadas ao VHD desde que ele foi inicialmente criado também são armazenadas no banco de dados do site. Quando você inicia o assistente para aplicar as atualizações de software ao VHD, o assistente recupera uma lista de atualizações de software aplicáveis que ainda não foram aplicadas ao VHD para que você as selecione.  

 É possível selecionar a configuração **Continuar se houver erro** para que o Configuration Manager continue aplicando as atualizações de software em caso de erro durante a aplicação de uma ou mais atualizações que você selecionou.  

> [!NOTE]  
>  As atualizações de software são copiadas da biblioteca de conteúdo no servidor do site.  

 Use o procedimento a seguir para aplicar atualizações de software ao VHD.  

#### <a name="to-apply-software-updates-to-a-vhd"></a>Para aplicar atualizações de software a um VHD  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Discos Rígidos Virtuais**.  

3.  Selecione o VHD para aplicar atualizações de software.  

4.  Na guia **Início** , no grupo **Disco Rígido Virtual** , clique em **Agendar Atualizações** para iniciar o assistente.  

5.  Na página **Escolher Atualizações** , selecione as atualizações de software a serem aplicadas ao VHD e clique em **Avançar**.  

6.  Na página **Definir Agendamento** , especifique as seguintes configurações e clique em **Próximo**.  

    1.  **Agendamento**: especifique o agendamento para quando as atualizações de software são aplicadas ao VHD.  

    2.  **Continuar se houver erro**: selecione essa opção para continuar a aplicar as atualizações de software à imagem em caso de erro.  

7.  Na página **Resumo** , verifique as seguintes informações e clique em **Próximo**.  

8.  Na página **Conclusão** , verifique se as atualizações de software foram aplicadas com êxito à imagem do sistema operacional.  

##  <a name="BKMK_ImportToVMM"></a> Importar o VHD para o System Center Virtual Machine Manager  
 O System Center VMM é uma solução de gerenciamento para o datacenter virtualizado, que permite configurar e gerenciar o host de virtualização, o serviço de rede e os recursos de armazenamento para criar e implantar máquinas virtuais e serviços para nuvens privadas que você criou. Depois de criar um VHD no Configuration Manager, é possível importar e gerenciar o VHD usando o VMM.  

> [!TIP]  
>  Antes de carregar um VHD para o VMM, verifique se o console do VMM está devidamente conectado ao servidor de gerenciamento do VMM.  

 Use o procedimento a seguir para importar um VHD para o VMM.  

#### <a name="to-import-a-vhd-to-vmm"></a>Para importar um VHD para o VMM  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Discos Rígidos Virtuais**.  

3.  Na guia **Início** , no grupo **Disco Rígido Virtual** , clique em **Carregar no Gerenciador de Máquina Virtual** para iniciar o Assistente para Carregar no Gerenciador de Máquina Virtual.  

4.  Na página **Geral** , defina as seguintes configurações e clique em **Avançar**.  

    -   **Nome do servidor do VMM**: especifique o FQDN do computador em que está instalado o servidor de gerenciamento do VMM. O assistente se conecta ao servidor de gerenciamento do VMM para baixar os compartilhamentos da biblioteca para o servidor.  

    -   **Compartilhamento de biblioteca do VMM**: especifique o compartilhamento de biblioteca do VMM da lista suspensa.  

    -   **Usar transferência descriptografada**: selecione essa configuração para transferir o arquivo do VHD para o servidor de gerenciamento do VMM sem o uso de criptografia.  

5.  Na página de Resumo, verifique as configurações e conclua o assistente. O tempo que ele leva para carregar o VHD pode variar dependendo do tamanho do arquivo do VHD e da largura de banda de rede para o servidor de gerenciamento do VMM.  
