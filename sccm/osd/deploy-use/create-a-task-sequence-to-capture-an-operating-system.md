---
title: Criar uma sequência de tarefas para capturar um sistema operacional
titleSuffix: Configuration Manager
description: Uma sequência de tarefas de montagem e captura cria um computador de referência que pode incluir drivers específicos e atualizações de software juntamente com o sistema operacional.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 25e4ac68-0e78-4bbe-b8fc-3898b372c4e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a1ef2883bfeb61df55ff045b76e9bc45a11b4da2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-task-sequence-to-capture-an-operating-system-in-system-center-configuration-manager"></a>Criar uma sequência de tarefas para capturar um sistema operacional no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Quando você usa uma sequência de tarefas para implantar um sistema operacional em um computador no System Center Configuration Manager, o computador instala a imagem do sistema operacional que você especificar na sequência de tarefas. Para personalizar a imagem do sistema operacional para que ela inclua drivers específicos, aplicativos, atualizações de software, etc., você pode usar uma sequência de tarefas de criação e captura para criar um computador de referência e, em seguida, capturar a imagem do sistema operacional do computador de referência. Se você já tiver um computador de referência disponível para capturar, você pode criar uma sequência de tarefas personalizadas para capturar o sistema operacional. Use as seções a seguir para capturar um sistema operacional personalizado.  

##  <a name="BKMK_BuildCaptureTS"></a> Use uma sequência de tarefas para criar e capturar um computador de referência  
 A sequência de tarefas de montagem e captura particiona e formata o computador de referência, instala o sistema operacional, bem como o cliente do Configuration Manager, aplicativos e atualizações de software e, em seguida, captura o sistema operacional do computador de referência. Os pacotes associados à sequência de tarefas, como aplicativos, devem estar disponíveis nos pontos de distribuição antes de criar a compilação e capturar a sequência de tarefas.  

###  <a name="BKMK_CreatePackages"></a> Preparando-se para as implantações de sistema operacional  
 Há muitos cenários para implantar um sistema operacional em computadores em seu ambiente. Na maioria dos casos, você vai criar uma sequência de tarefas e selecionar **instalar um pacote de imagem existente** no assistente Criar Sequência de Tarefas para instalar o sistema operacional, migrar as configurações do usuário, aplicar atualizações de software e instalar aplicativos. Antes de criar uma sequência de tarefas para instalar um sistema operacional, o seguinte deve estar disponível:  

-   **Necessária**  

    -   A [imagem de inicialização](../get-started/manage-boot-images.md) deve estar disponível no console do Configuration Manager.  

    -   Uma [imagem do sistema operacional](../get-started/manage-operating-system-images.md) deve estar disponível no console do Configuration Manager.  

-   **Necessário (se usado)**  

    -   Os [pacotes de driver](../get-started/manage-drivers.md) que contêm os drivers do Windows necessários para dar suporte ao hardware no computador de referência devem estar disponíveis no console do Configuration Manager. Para obter mais informações sobre as etapas de sequência de tarefas para gerenciar drivers, veja [Usar sequências de tarefas para instalar drivers de dispositivo](../get-started/manage-drivers.md#BKMK_TSDrivers).  

    -   As [atualizações de software](../../sum/get-started/synchronize-software-updates.md) devem estar sincronizadas no console do Configuration Manager.  

    -   Os [aplicativos](../../apps/deploy-use/create-applications.md) devem ser adicionados ao console do Configuration Manager.  

###  <a name="BKMK_CreateBuildCaptureTS"></a> Criar uma sequência de tarefas de montagem e captura  
 Use o procedimento a seguir para usar uma sequência de tarefas para criar um computador de referência e capturar o sistema operacional.  

#### <a name="to-create-a-task-sequence-that-builds-and-captures-an-operating-system-image"></a>Para criar uma sequência de tarefas que monta e captura uma imagem de sistema operacional  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Sequência de Tarefas** para iniciar o Assistente para Criar Sequência de Tarefas.  

4.  Na página **Criar uma Nova Sequência de Tarefas** , selecione **Montar e capturar uma imagem do sistema operacional de referência**.  

5.  Na página **Informações da Sequência de Tarefas** , especifique as seguintes configurações e clique em **Próximo**.  

    -   **Nome da sequência de tarefas**: especifique um nome que identifique a sequência de tarefas.  

    -   **Descrição**: especifique uma descrição da tarefa executada pela sequência de tarefas, como, por exemplo, uma descrição do sistema operacional que é criada pela sequência de tarefas.  

    -   **Imagem de inicialização**: especifique a imagem de inicialização que instala a imagem da sistema operacional.  

        > [!IMPORTANT]  
        >  A arquitetura da imagem de inicialização deve ser compatível com a arquitetura de hardware do computador de destino.  

6.  Na página **Instalar Windows** , especifique as seguintes configurações e clique em **Próximo**.  

    -   **Pacote de imagens**: especifique o pacote de imagens do sistema operacional, que contém os arquivos necessários para instalar o sistema operacional.  

    -   **Índice de imagem**: especifique o sistema operacional para instalar. Se a imagem do sistema operacional tiver várias versões, selecione a versão que você deseja instalar.  

    -   **Chave do produto**: especifique a chave do produto do sistema operacional Windows a instalar. Você pode especificar as chaves de licença de volume codificadas e as chaves do produto padrão. Se você usar uma chave de produto sem codificação, cada grupo de 5 caracteres deverá ser separado por um traço (-). Por exemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **Modo de licenciamento do servidor**: especifique se a licença do servidor é **Por estação**, **Por servidor**ou se nenhuma licença está especificada. Se a licença do servidor for **Por servidor**, especifique também o número máximo de conexões de servidor.  

    -   Especifique como lidar com a conta de administrador usada quando o sistema operacional é implantado.  

        -   **Gerar aleatoriamente a senha do administrador local e desabilitar a conta em todas as plataformas com suporte**: especifique se deseja que o Configuration Manager crie uma senha aleatória para a conta de administrador local e desabilite a conta quando o sistema operacional for implantado.  

        -   **Ativar a conta e especificar a senha do administrador local**: especifique se a mesma senha deve ser usada para a conta do administrador local em todos os computadores nos quais o sistema operacional será implantado.  

7.  Na página **Configurar a Rede** , especifique as seguintes configurações e clique em **Próximo**.  

    -   **Ingressar no grupo de trabalho**: especifique se deseja adicionar o computador de destino a um grupo de trabalho quando o sistema operacional é implantado.  

    -   **Ingressar em um domínio**: especifique se deseja adicionar o computador de destino a um domínio quando o sistema operacional for implantado. Em **Domínio**, especifique o nome do domínio.  

        > [!IMPORTANT]  
        >  Você pode localizar os domínios na floresta local, mas, para tanto, é necessário especificar o nome de domínio para uma floresta remota.  

         Você também pode especificar uma UO (unidade organizacional). Essa configuração opcional especifica o nome diferenciado do LDAP X.500 da UO na qual a conta do computador será criada, se ela ainda não existir.  

    -   **Conta**: especifique o nome de usuário e senha para a conta que tenha permissões para ingressar no domínio especificado. Por exemplo: *domain\user* ou *%variable%*.  

        > [!IMPORTANT]  
        >  Você deve inserir as credenciais de domínio adequadas se planeja migrar as configurações de domínio ou as configurações do grupo de trabalho.  

8.  Na página **Instalar o Configuration Manager**, especifique o pacote do cliente do Configuration Manager que contém os arquivos de origem para instalar o cliente do Configuration Manager, acrescente propriedades adicionais necessárias para instalar o cliente e clique em **Próximo**.  

     Para obter mais informações sobre as propriedades que podem ser usadas para instalar um cliente, consulte [Sobre as propriedades de instalação do cliente](../../core/clients/deploy/about-client-installation-properties.md).  

9. Na página **Incluir Atualizações** , especifique se deseja instalar as atualizações de software necessárias, todas as atualizações ou nenhuma e clique em **Próximo**. Se optar pela instalação das atualizações de software, o Configuration Manager instalará somente aquelas que fizerem parte das coleções das quais o computador de destino é membro.  

10. Na página **Instalar Aplicativos** , especifique os aplicativos a instalar no computador de destino e clique em **Próximo**. Se você especificar vários aplicativos, será possível também definir a continuação da sequência de tarefas em caso de falha na instalação de algum aplicativo.  

11. Na página **Preparação do Sistema** , especifique as seguintes configurações e clique em **Próximo**.  

    -   **Pacote**: especifique o pacote do Configuration Manager que contém a versão apropriada do Sysprep a usar para capturar as configurações do computador de referência.  

         Se a versão do sistema operacional em execução for o Windows Vista ou posterior, o Sysprep será instalado automaticamente no computador e não haverá necessidade de especificar um pacote.  

12. Na página **Propriedades da Imagem** , especifique as seguintes configurações para a imagem do sistema operacional e clique em **Próximo**.  

    -   **Criado por**: especifique o nome do usuário que criou a imagem do sistema operacional.  

    -   **Versão**: especifique um número de versão definido pelo usuário que está associado à imagem do sistema operacional.  

    -   **Descrição**: especifique uma descrição definida pelo usuário da imagem de computador do sistema operacional.  

13. Na página **Capturar Imagem** , especifique as seguintes configurações e clique em **Próximo**.  

    -   **Caminho**: especifique uma pasta de rede compartilhada em que o arquivo de saída .WIM será armazenado. Esse arquivo contém a imagem do sistema operacional baseada nas configurações especificadas neste assistente. Se você especificar uma pasta que já contém um arquivo .WIM, o arquivo existente será substituído.  

    -   **Conta**: especifique a conta do Windows que tem permissões para o compartilhamento de rede em que a imagem está armazenada.  

14. Conclua o assistente.  

15. Para adicionar etapas adicionais à sequência de tarefas, selecione a sequência de tarefas criada e clique em **Editar**. Para obter informações sobre como editar uma sequência de tarefas, veja [Editar uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

 Implante a sequência de tarefas em um computador de referência em uma das seguintes maneiras:  

-   Se o computador de referência for um cliente do Configuration Manager, você poderá implantar a sequência de tarefas de montagem e captura na coleção que contém o computador de referência. Para obter informações sobre como implantar a imagem do sistema operacional, veja [Criar uma sequência de tarefas para instalar um sistema operacional](create-a-task-sequence-to-install-an-operating-system.md).  

    > [!NOTE]  
    >  Se a sequência de tarefas tiver uma etapa da sequência de tarefas de particionamento de disco, não selecione a opção **Baixar Programa** quando implantar a sequência de tarefas.  

-   Se o computador de referência não for um cliente do Configuration Manager ou se você desejar executar manualmente a sequência de tarefas no computador referência, execute o **Assistente para Criar Mídia de Sequência de Tarefas** para criar uma mídia inicializável. Para obter informações sobre como criar a mídia inicializável, consulte [Criar mídia inicializável](create-bootable-media.md).  

##  <a name="BKMK_CaptureExistingRefComputer"></a> Capturar uma imagem de sistema operacional de um computador de referência existente  
 Quando você tiver um computador de referência pronto para capturar, você pode criar uma sequência de tarefas que captura o sistema operacional do computador de referência. Você usará a etapa da sequência de tarefas **Capturar imagem do sistema operacional** para capturar imagens de um ou mais computadores de referência e armazená-las em um arquivo de imagem (.wim) no compartilhamento de rede especificado. O computador de referência é iniciado no Windows PE usando uma imagem de inicialização, cada disco rígido no computador de referência é capturado como uma imagem separada no arquivo. wim. Se o computador de referência tiver várias unidades, o arquivo .wim resultante conterá uma imagem separada para cada volume. Apenas volumes formatados como NTFS ou FAT32 são capturados. Volumes com outros formatos e USB são ignorados.  

 Use o procedimento a seguir para capturar uma imagem do sistema operacional de um computador de referência existente.  

#### <a name="to-capture-an-operating-system-from-an-existing-reference-computer"></a>Para capturar um sistema operacional de um computador de referência existente  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Sequência de Tarefas** para iniciar o Assistente para Criar Sequência de Tarefas.  

4.  Na página **Criar uma nova sequência de tarefas** , selecione **Criar uma nova sequência de tarefas personalizada**.  

5.  Na página **Informações da Sequência de Tarefas** , especifique um nome e uma descrição para a sequência de tarefas.  

6.  Especifique uma imagem de inicialização para a sequência de tarefas. Esta imagem de inicialização é usada para iniciar o computador de referência com o Windows PE.  Para obter mais informações, consulte [Gerenciar imagens de inicialização](../get-started/manage-boot-images.md).  

7.  Conclua o assistente.  

8.  Em **Sequências de Tarefas**, selecione a sequência de tarefas personalizada e, em seguida, na guia **Início** no grupo **Sequência de Tarefas** , clique em **Editar** para abrir o editor de sequência de tarefas.  

9. Use esta etapa apenas se o cliente Configuration Manager estiver instalado no computador de referência.  

     Clique em **Adicionar**, depois em **Imagens** e, em seguida, clique em [Preparar o Cliente do ConfigMgr para Captura](../understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture). Esta etapa usa o cliente do Configuration Manager no computador de referência e o prepara para a captura como parte do processo de geração de imagens.  

    > [!Note]  
    >  A sequência de tarefas não dá suporte para desinstalar o cliente do Configuration Manager.

10. Clique em **Adicionar**, depois em **Imagens** e, em seguida, clique em [Preparar o Windows para Captura](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture). Esta ação de sequência de tarefas executa o Sysprep e reinicia o computador na imagem de inicialização do Windows PE especificado para a sequência de tarefas. O computador de referência não deve estar associado a um domínio para essa ação ser concluída com êxito.  

11. Clique em **Adicionar**, depois em **Imagens** e, em seguida, clique em [Capturar Imagem do Sistema Operacional](../understand/task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  Essa etapa só será executada no Windows PE para capturar os discos rígidos no computador de referência. Defina as seguintes configurações para a etapa de sequência de tarefas.  

    -   **Nome** e **Descrição**: se desejar, você pode alterar o nome da etapa de sequência de tarefas e fornecer uma descrição.  

    -   **Destino**: especifique uma pasta de rede compartilhada em que o arquivo de saída .WIM será armazenado. Esse arquivo contém a imagem do sistema operacional baseada nas configurações especificadas neste assistente. Se você especificar uma pasta que já contém um arquivo .WIM, o arquivo existente será substituído.  

    -   **Descrição**, **Versão**e **Criado por**: você também pode fornecer detalhes sobre a imagem que vai capturar.  

    -   **Capturar conta de imagem de sistema operacional**: especifique a conta do Windows que tem permissão para o compartilhamento de rede especificado. Clique em **Definir** para especificar o nome dessa conta do Windows.  

     Clique em **OK** para fechar do editor de sequência de tarefas.  

 Implante a sequência de tarefas em um computador de referência em uma das seguintes maneiras:  

-   Se o computador de referência for um cliente do Configuration Manager, você poderá implantar a sequência de tarefas na coleção que contém o computador de referência. Para obter informações sobre como implantar a imagem do sistema operacional, veja [Criar uma sequência de tarefas para instalar um sistema operacional](create-a-task-sequence-to-install-an-operating-system.md).  

-   Se o computador de referência não for um cliente do Configuration Manager ou se você desejar executar manualmente a sequência de tarefas no computador referência, execute o **Assistente para Criar Mídia de Sequência de Tarefas** para criar uma mídia inicializável. Para obter informações sobre como criar a mídia inicializável, consulte [Criar mídia inicializável](create-bootable-media.md).  

##  <a name="BKMK_BuildandCaptureTSExample"></a> Sequências de tarefas para compilar e capturar uma imagem do sistema operacional  
 Use a tabela a seguir como um guia conforme você cria uma sequência de tarefas que compila e captura uma imagem do sistema operacional. A tabela ajudará você a decidir a sequência geral de etapas da sequência de tarefas e como organizar e estruturar essas etapas de sequência de tarefas em grupos lógicos. A sequência de tarefas que você criar pode variar por meio desta amostra e pode conter mais ou menos grupos e etapas da sequência de tarefas.  

> [!IMPORTANT]  
>  Sempre use o assistente Criar sequência de tarefas para criar esse tipo de sequência de tarefas.  

 Quando você usa a opção **Nova Sequência de Tarefas** para criar essa nova sequência de tarefas, alguns nomes desta etapa serão diferentes do que seriam se você adicionasse essas etapas de sequência de tarefas manualmente a uma sequência de tarefas existente. A tabela a seguir exibe as diferenças de nomenclatura:  

|Novo nome de etapa de sequência de tarefas do assistente Sequência de tarefas|Nome da etapa equivalente do Editor de sequência de tarefas|  
|------------------------------------------------------|-----------------------------------------------|  
|Reiniciar no Windows PE|Reinicialize no Windows PE ou o disco rígido|  
|Particionar Disco 0|Formatar e Particionar Disco|  
|Aplicar Drivers de Dispositivo|Drivers de Aplicação Automática|  
|Instalar atualizações|Instalar Atualizações de Software|  
|Ingressar em grupo de trabalho|Ingressar no Domínio ou Grupo de Trabalho|  
|Preparar cliente ConfigMgr|Prepare ConfigMgr Client for Capture|  
|Preparar o sistema operacional|Prepare Windows for Capture|  
|Capturar o computador de referência|Capturar imagem do sistema operacional|  

|Grupo/etapa de sequência de tarefas|Referência|  
|-------------------------------|---------------|  
|Criar o computador de referência - **(novo grupo de sequências de tarefas)**|Criar um grupo de sequências de tarefas. Um grupo de sequências de tarefas mantém as etapas de sequência de tarefas semelhantes juntas para melhor organização e controle de erro.<br /><br /> Esse grupo contém as ações necessárias para criar um computador de referência.|  
|Reiniciar no Windows PE|Use esta etapa para especificar as opções de reinicialização do computador de destino. Esta etapa exibirá uma mensagem para o usuário que o computador será reiniciado para que a instalação possa continuar.<br /><br /> Esta etapa usa a variável de sequência de tarefas **_SMSTSInWinPE** de somente leitura. Se o valor associado for igual a **falso** a etapa de sequência de tarefas continuará.|  
|Particionar disco 0|Use esta etapa para especificar as ações necessárias para formatar o disco rígido no computador de destino. O número de disco padrão é **0**.<br /><br /> Esta etapa usa a variável de sequência de tarefas **_SMSTSClientCache** de somente leitura. Esta etapa será executada se o cache do cliente do Configuration Manager não existir.|  
|Aplicar Sistema Operacional|Use essa etapa de sequência de tarefas para instalar uma imagem especificada de sistema operacional no computador de destino. Essa etapa se aplica a todas as imagens de volume contidas no arquivo WIM para o volume de disco sequencial correspondente no computador de destino após o primeiro excluir todos os arquivos no volume (com exceção de arquivos de controle específicos do Configuration Manager).|  
|Aplicar as Configurações do Windows|Use essa etapa de sequência de tarefas para ajustar as informações de definição das configurações do Windows no computador de destino.|  
|Aplicar Configurações de Rede|Use esta etapa para especificar as informações de configuração de rede ou grupo de trabalho do computador de destino.|  
|Aplicar Drivers de Dispositivo|Use esta etapa para corresponder e instalar unidades como parte da implantação do sistema operacional. Você pode permitir que a Instalação do Windows pesquise todas as categorias de driver existentes selecionando a opção **Considerar drivers de todas as categorias** ou limitar quais categorias de driver de Instalação do Windows pesquisarão ao selecionar a opção **Limitar a correspondência de driver para considerar somente os drivers em categorias selecionadas**.<br /><br /> Esta etapa usa somente leitura **_SMSTSMediaType** variável de sequência de tarefas. Se o valor associado não for igual a **FullMedia** , essa etapa será executada.|  
|Instalar Windows e ConfigMgr|Use essa etapa de sequência de tarefas para instalar o software cliente do Configuration Manager. O Configuration Manager instala e registra o GUID do cliente do Configuration Manager. Você pode atribuir os parâmetros necessários para a instalação na janela **Propriedades de instalação** .|  
|Instalar atualizações|Use esta etapa de sequência de tarefas para especificar como as atualizações de software serão instaladas no computador de destino. O computador de destino não é avaliado para atualizações de software aplicáveis até que essa etapa de sequência de tarefas seja executada. Nesse momento, o computador de destino é avaliado para atualizações de software semelhantes a qualquer outro cliente gerenciado do Configuration Manager.<br /><br /> Esta etapa usa a variável de sequência de tarefas **_SMSTSMediaType** somente leitura. Se o valor associado não for igual a **FullMedia** , essa etapa será executada.|  
|Capture o computador de referência - **(novo grupo de sequências de tarefas)**|Crie outro grupo de sequências de tarefas. Esse grupo contém as etapas necessárias para preparar e capturar um computador de referência.|  
|Ingressar em grupo de trabalho|Use esta etapa de sequência de tarefas para especificar as informações necessárias para o computador de destino ingressar em um grupo de trabalho.|  
|Prepare ConfigMgr Client for Capture|Use esta etapa para levar o cliente do Configuration Manager no computador de referência e prepará-lo para a captura como parte do processo de geração de imagens|  
|Preparar o sistema operacional|Use esta etapa para especificar as opções do Sysprep para usar ao capturar configurações do Windows no computador de referência. Esta etapa de sequência de tarefas executa o Sysprep e reinicia o computador na imagem de inicialização do Windows PE especificado para a sequência de tarefas.|  
|Capturar imagem do sistema operacional|Use essa etapa para inserir um compartilhamento de rede existente específico e um arquivo .WIM para usar ao salvar a imagem. Esse local é usado como o lugar de origem do pacote ao adicionar um pacote de imagem de sistema operacional usando o assistente **Adicionar de Pacote de Imagem de Sistema Operacional**.|  

 Depois de capturar uma imagem de um computador de referência, não capture outra imagem do sistema operacional do computador de referência, pois as entradas do Registro são criadas durante a configuração inicial. Crie um novo computador de referência sempre que capturar a imagem do sistema operacional. Se você planeja usar o mesmo computador de referência para criar imagens futuras do sistema operacional, primeiramente, desinstale o cliente do Configuration Manager e depois instale-o novamente.  

## <a name="next-steps"></a>Próximas etapas  
[Métodos para implantar sistemas operacionais corporativos](methods-to-deploy-enterprise-operating-systems.md)
