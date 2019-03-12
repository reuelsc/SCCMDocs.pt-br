---
title: Gerenciar drivers
titleSuffix: Configuration Manager
description: Use o catálogo de drivers do Configuration Manager para importar drivers de dispositivo, drivers de grupo em pacotes e distribuir esses pacotes aos pontos de distribuição.
ms.date: 03/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: be3cc24721674e9da276e7a65af03a5b4a266eed
ms.sourcegitcommit: 33a006204f7f5f9b9acd1f3e84c4bc207362d00a
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 03/04/2019
ms.locfileid: "57305687"
---
# <a name="manage-drivers-in-configuration-manager"></a>Gerenciar drivers no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Configuration Manager fornece um catálogo de drivers que pode ser usado para gerenciar os drivers de dispositivos do Windows no ambiente do Configuration Manager. Use o catálogo de drivers para importar drivers de dispositivo no Configuration Manager, para agrupá-los em pacotes e para distribuir esses pacotes em pontos de distribuição. Os drivers de dispositivo podem ser acessados quando você instala o SO integral no computador de destino e quando usa o Windows PE em uma imagem de inicialização. Os drivers de dispositivo do Windows consistem em um arquivo INF (arquivo de informações) de instalação e arquivos adicionais necessários para dar suporte ao dispositivo. Quando você implanta um SO, o Configuration Manager obtém as informações de hardware e plataforma para o dispositivo por meio de seu arquivo INF. 



## <a name="BKMK_DriverCategories"></a> Categorias de driver

Quando você importa drivers de dispositivo, é possível atribuir os drivers de dispositivo a uma categoria. Categorias de driver de dispositivo ajudam a agrupar drivers de dispositivo de uso similar no catálogo de driver. Por exemplo, atribua todos os drivers de dispositivo do adaptador de rede a uma categoria específica. Em seguida, ao criar uma sequência de tarefas que inclua a etapa [Auto Apply Drivers](/sccm/osd/understand/task-sequence-steps#BKMK_AutoApplyDrivers), especifique uma categoria específica de drivers de dispositivo. O Configuration Manager faz a varredura do hardware e seleciona os drivers aplicáveis dessa categoria a serem preparados no sistema para uso da Instalação do Windows.  



## <a name="BKMK_ManagingDriverPackages"></a> Pacotes de driver

Agrupe drivers de dispositivo semelhantes em pacotes para ajudar a simplificar as implantações de SO. Por exemplo, crie um pacote de driver para cada fabricante de computador na rede. É possível criar um pacote de driver ao importar drivers no catálogo de drivers diretamente no nó **Pacotes de Driver**. Depois de criar um pacote de driver, distribua-o para pontos de distribuição. Em seguida, os computadores clientes do Configuration Manager podem instalar os drivers conforme necessário. 

Considere os seguintes pontos:  

- Quando você cria um pacote de driver, o local de origem do pacote deve apontar para um compartilhamento de rede vazio, não usado por outro pacote de driver. O Provedor de SMS deve ter as permissões de **Controle Total** para esse local.  

- Quando você adiciona drivers de dispositivo em um pacote de driver, o Configuration Manager os copia para o local de origem do pacote de driver. Você pode adicionar a um pacote de driver apenas os drivers de dispositivo que você importou e que estão habilitados no catálogo de drivers.  

- Você pode copiar um subconjunto dos drivers de dispositivo de um pacote de driver existente. Primeiro, crie um novo pacote de driver. Em seguida, adicione o subconjunto de drivers de dispositivo ao novo pacote e distribua o novo pacote para um ponto de distribuição.  

- Ao usar sequências de tarefas para instalar drivers, crie pacotes de driver que contêm menos de 500 drivers de dispositivo.


### <a name="BKMK_CreatingDriverPackages"></a> Criar um pacote de driver  

> [!IMPORTANT]  
> Para criar um pacote de driver, é necessário ter uma pasta de rede vazia, que não seja usada por outro pacote de driver. Na maioria dos casos, crie uma nova pasta antes de iniciar este procedimento.  

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**. Expanda **Sistemas Operacionais** e, em seguida, selecione o nó **Pacotes de Driver**.  

2. Na guia **Início** da faixa de opções, no grupo **Criar**, selecione **Adicionar Pacote de Driver**.  

3. Especifique um **Nome** descritivo para o pacote de driver.  

4. Insira um **Comentário** opcional para o pacote de driver. Use a descrição para fornecer informações sobre o conteúdo ou a finalidade do pacote de driver.  

5. Na caixa **Caminho** , especifique uma pasta de origem para o pacote de driver. Cada pacote de driver deve usar uma pasta exclusiva. Esse caminho é necessário como um local de rede.  

   > [!IMPORTANT]  
   > A conta do servidor do site deve ter permissões de **Controle Total** para a pasta de origem especificada.  

O novo pacote de driver não contém drivers. A próxima etapa adiciona drivers ao pacote.  

Se o nó **Pacotes de Driver** contiver diversos pacotes, você poderá adicionar pastas ao nó para separar os pacotes em grupos lógicos.  


### <a name="BKMK_PackageActions"></a> Ações adicionais para pacotes de driver  

Você pode executar ações adicionais para gerenciar pacotes de driver ao selecionar um ou mais pacotes de driver do nó **Pacotes de Driver**. 


#### <a name="create-prestage-content-file"></a>Criar Arquivo de Conteúdo de Pré-Teste
Cria arquivos que você pode usar para importar conteúdo e seus metadados associados manualmente. Usar o conteúdo de pré-teste quando a largura de banda de rede for baixa entre o servidor do site e os pontos de distribuição em que o pacote de driver está armazenado.

#### <a name="delete"></a>Excluir
Remove o pacote de driver a partir do **Pacotes de Driver** .

#### <a name="distribute-content"></a>Distribuir Conteúdo
Distribui o pacote de driver aos pontos de distribuição, grupos do ponto de distribuição e aos grupos do ponto de distribuição associados a coleções.

#### <a name="manage-access-accounts"></a>Gerenciar Contas de Acesso
Adiciona, modifica ou remove contas de acesso do pacote de driver.

Para saber mais sobre contas de acesso de pacote, consulte [Contas usadas no Configuration Manager](/sccm/core/plan-design/hierarchy/accounts).

#### <a name="move"></a>Mover
Move pacote de driver para outra pasta do nó **Pacotes de Driver** .

#### <a name="update-distribution-points"></a>Atualizar Pontos de Distribuição
Atualiza o pacote de driver de dispositivo em todos os pontos de distribuição onde o pacote é armazenado. Essa ação copia somente o conteúdo alterado desde a última vez que ele foi distribuído.

#### <a name="properties"></a>Propriedades
Abre a caixa de diálogo **Propriedades**. Revise e altere o conteúdo e as propriedades do driver. Por exemplo, altere o nome e a descrição do driver, habilite-o ou desabilite-o e especifique em quais plataformas ele pode ser executado. 

<!--3607716, fka 1358270--> A partir da versão 1810, os pacotes de driver têm campos de metadados para **Fabricante** e **Modelo**. Use esses campos para marcar pacotes de driver com informações para auxiliar na manutenção geral do sistema ou para identificar drivers antigos e duplicados que podem ser excluídos. Na guia **Geral**, selecione um valor existente nas listas suspensas ou insira uma cadeia de caracteres para criar uma nova entrada. 

No nó **Pacotes de Driver**, esses campos são exibidos na lista como as colunas **Fabricante do Driver** e **Modelo do Driver**. Eles também podem ser usados como critérios de pesquisa. 



## <a name="BKMK_DeviceDrivers"></a> Drivers de dispositivo

É possível instalar drivers em computadores de destino sem incluí-los na imagem do SO que está sendo implantada. O Configuration Manager fornece um catálogo de drivers que contém referências a todos os drivers importados para o Configuration Manager. O catálogo de drivers está localizado no workspace **Biblioteca de Software** e consiste em dois nós: **Drivers** e **Pacotes de driver**. O nó **Drivers** lista todos os drivers que você importou no catálogo de drivers.  


### <a name="BKMK_ImportDrivers"></a> Importar drivers de dispositivo para o catálogo de drivers  

Antes de você poder usar um driver ao implantar um SO, importe-o para o catálogo de drivers. Para gerenciá-los melhor, importe apenas os drivers que você planeja instalar como parte de suas implantações de SO. Armazene várias versões de drivers no catálogo de drivers, de modo a facilitar a atualização dos drivers existentes, quando os requisitos de dispositivo de hardware mudarem em sua rede.  

Como parte do processo de importação do driver de dispositivo, o Configuration Manager lê as seguintes propriedades sobre o driver:
- Provider
- Class
- Version
- Assinatura
- Hardware com suporte
- Informações de plataforma com suporte

Por padrão, o driver é nomeado após o primeiro dispositivo de hardware que ele suporta. Você pode renomear o driver de dispositivo posteriormente. A lista de plataformas com suporte baseia-se nas informações do arquivo INF do driver. Como a precisão dessas informações pode variar, verifique manualmente se há suporte para o driver depois de importá-lo no catálogo.  

Depois de importar drivers de dispositivo para o catálogo, adicione-os a pacotes de driver ou a pacotes de imagens de inicialização.  

> [!IMPORTANT]  
> Não é possível importar drivers de dispositivo diretamente para uma subpasta do nó **Drivers**. Para importar um driver de dispositivo para uma subpasta, importe primeiro o dispositivo para o nó **Drivers** e mova o driver para a subpasta.  


#### <a name="process-to-import-windows-device-drivers-into-the-driver-catalog"></a>Importar drivers de dispositivo do Windows para o catálogo de drivers  

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**. Expanda **Sistemas Operacionais** e selecione o nó **Drivers**.  

2. Na guia **Início** na faixa de opções, no grupo **Criar**, selecione **Importar Driver** para iniciar o **Assistente de Importação de Novo Driver**.  

3. Na página **Localizar Driver**, especifique as seguintes opções:  

    - **Importe todos os drivers no seguinte caminho de rede (UNC)**: Para importar todos os drivers de dispositivo em uma pasta específica, especifique seu caminho de rede. Por exemplo: `\\servername\share\folder`.  

        > [!NOTE]  
        > Se houver muitas subpastas e muitos arquivos INF de driver, esse processo pode levar tempo.  

    - **Importe um driver específico**: Para importar um determinado driver de uma pasta, especifique o caminho de rede para o arquivo INF do driver de dispositivo do Windows.  

    - **Especifique a opção para drivers duplicados**: Selecione como deseja que o Configuration Manager gerencie as categorias de driver quando você importar um driver de dispositivo duplicado  
        - **Importar o driver e acrescentar uma nova categoria às categorias existentes**  
        - **Importar o driver e manter as categorias existentes**  
        - **Importar o driver e substituir as categorias existentes**  
        - **Não importar o driver**  

    > [!IMPORTANT]  
    > Ao importar drivers, o servidor do site deve ter permissão de **Leitura** para a pasta; caso contrário, a importação falhará.  

4. Na página **Detalhes do Driver**, especifique as seguintes opções:  

    - **Ocultar drivers que não estão em uma classe de armazenamento ou de rede (para imagens de inicialização)**: Use essa configuração para exibir somente drivers de armazenamento e de rede. Essa opção oculta outros drivers que, geralmente, não são necessários para as imagens de inicialização, como drivers de vídeo ou de modem.  

    - **Ocultar drivers que não são assinados digitalmente**: A Microsoft recomenda somente o uso de drivers assinados digitalmente  

    - Na lista de drivers, selecione os drivers que deseja importar para o catálogo de drivers.  

    - **Habilitar estes drivers e permitir que os computadores os instalem**: Selecione essa configuração para permitir que computadores instalem os drivers de dispositivo. Essa opção é habilitada por padrão.  

        > [!IMPORTANT]  
        > Se um driver de dispositivo estiver causando um problema ou você desejar suspender a instalação de um driver de dispositivo, desative-o durante a importação. Você também pode desabilitar os drivers depois de importá-los.  

    - Para atribuir os drivers de dispositivo a uma categoria administrativa para fins de filtragem, como "Desktops" ou "Notebooks", selecione **Categorias**. Em seguida, escolha uma categoria existente ou crie uma nova categoria. Use categorias para controlar quais drivers de dispositivo são aplicados pela etapa da sequência de tarefas de [Drivers de Aplicação Automática](/sccm/osd/understand/task-sequence-steps#BKMK_AutoApplyDrivers).  

5. Na página **Adicionar Driver aos Pacotes**, escolha se deseja adicionar os drivers a um pacote.  

    - Selecione os pacotes de driver usados para distribuir os drivers de dispositivo.  

        Se necessário, selecione **Novo Pacote** para criar um novo pacote de driver. Ao criar um novo pacote de driver, forneça um compartilhamento de rede que não esteja sendo usado por outros pacotes de driver.  

    - Se o pacote já foi distribuído para os pontos de distribuição, selecione **Sim** na caixa de diálogo para atualizar as imagens de inicialização nos pontos de distribuição. Não é possível usar drivers de dispositivo até que eles sejam distribuídos aos pontos de distribuição. Se você selecionar **Não**, execute a ação **Atualizar Ponto de Distribuição** antes de usar a imagem de inicialização. Se o pacote de driver nunca foi distribuído, você deve usar a ação **Distribuir Conteúdo** no nó **Pacotes de Driver**.  

6. Na página **Adicionar Driver às Imagens de Inicialização**, escolha se deseja adicionar os drivers de dispositivo às imagens de inicialização existentes.  

    > [!NOTE]  
    > Adicione somente drivers de armazenamento e de rede às imagens de inicialização.  

    - Selecione **Sim** na caixa de diálogo para atualizar as imagens de inicialização nos pontos de distribuição. Não é possível usar drivers de dispositivo até que eles sejam distribuídos aos pontos de distribuição. Se você selecionar **Não**, execute a ação **Atualizar Ponto de Distribuição** antes de usar a imagem de inicialização. Se o pacote de driver nunca foi distribuído, você deve usar a ação **Distribuir Conteúdo** no nó **Pacotes de Driver**.  

    - O Configuration Manager avisará se a arquitetura de um ou mais drivers não corresponder à arquitetura das imagens de inicialização selecionadas. Se elas não corresponderem, selecione **OK**. Volte para a página **Detalhes do Driver** e desmarque os drivers que não correspondem à arquitetura da imagem de inicialização selecionada. Por exemplo, se você selecionar uma imagem de inicialização em base em x64 e x86, todos os drivers devem dar suporte a ambas as arquiteturas. Se você selecionar uma imagem de inicialização com base em x64, todos os drivers devem dar suporte à arquitetura x64.  

        > [!NOTE]  
        > - A arquitetura é baseada na arquitetura relatada no INF do fabricante.  
        > - Se um driver relatar que dá suporte a ambas as arquiteturas, você poderá importá-lo para qualquer uma das duas imagens de inicialização.  

    - O Configuration Manager avisa se você adicionar drivers de dispositivo que não sejam drivers de rede ou de armazenamento a uma imagem de inicialização. Na maioria dos casos, eles não são necessários para a imagem de inicialização. Selecione **Sim** para adicionar os drivers à imagem de inicialização ou **Não** para voltar e modificar sua seleção de driver.  

    - O Configuration Manager avisará se um ou mais dos drivers selecionados não estiverem assinados digitalmente de maneira correta. Selecione **Sim** para continuar e selecione **Não** para voltar e fazer alterações em sua seleção de driver.  

7. Conclua o assistente.  


### <a name="BKMK_ModifyDriverPackage"></a> Gerenciar drivers de dispositivo em um pacote de driver  

Use os procedimentos a seguir para modificar pacotes de driver e imagens de inicialização. Para adicionar ou remover um driver, primeiro localize-o no nó **Drivers**. Em seguida, edite os pacotes ou as imagens de inicialização com os quais o driver selecionado está associado.  

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**. Expanda **Sistemas Operacionais** e selecione o nó **Drivers**.  

2. Selecione os drivers de dispositivo que você deseja adicionar ao pacote de driver.  

3. Na guia **Início** da faixa de opções, no grupo **Driver**, selecione **Editar** e, em seguida, escolha **Pacotes de Driver**.  

4. Para adicionar um driver de dispositivo, marque a caixa de seleção dos pacotes de driver aos quais deseja adicionar os drivers de dispositivo. Para remover um driver de dispositivo, desmarque a caixa de seleção dos pacotes de driver dos quais deseja remover o driver de dispositivo.  

    Se você estiver adicionando drivers de dispositivo associados a pacotes de drivers, poderá criar opcionalmente um novo pacote. Selecione **Novo Pacote**, que abre a caixa de diálogo **Novo Pacote de Driver**.  

5. Se o pacote já foi distribuído para os pontos de distribuição, selecione **Sim** na caixa de diálogo para atualizar as imagens de inicialização nos pontos de distribuição. Não é possível usar drivers de dispositivo até que eles sejam distribuídos aos pontos de distribuição. Se você selecionar **Não**, execute a ação **Atualizar Ponto de Distribuição** antes de usar a imagem de inicialização. Se o pacote de driver nunca foi distribuído, você deve usar a ação **Distribuir Conteúdo** no nó **Pacotes de Driver**. Antes que os drivers estejam disponíveis, é necessário atualizar o pacote de driver nos pontos de distribuição.  

    Selecione **OK** quando terminar.  


### <a name="BKMK_ManageDriversBootImage"></a> Gerenciar drivers de dispositivo em uma imagem de inicialização  

Você pode adicionar às imagens de inicialização, drivers de dispositivo do Windows que foram importados para o catálogo. Ao adicionar drivers de dispositivo a uma imagem de inicialização, use as seguintes diretrizes:  

- Adicione somente drivers de armazenamento e de rede às imagens de inicialização. Outros tipos de drivers geralmente não são necessários no Windows PE. Drivers não obrigatórios aumentam desnecessariamente o tamanho das imagens de inicialização.  

- Adicione apenas drivers de dispositivo para o Windows 10 a uma imagem de inicialização. A versão necessária do Windows PE é baseada no Windows 10.  

- Verifique se está usando o driver de dispositivo correto para a arquitetura da imagem de inicialização. Não adicione um driver de dispositivo x86 a uma imagem de inicialização x64.  

#### <a name="process-to-modify-the-device-drivers-associated-with-a-boot-image"></a>Modificar drivers de dispositivo associados a uma imagem de inicialização  

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**. Expanda **Sistemas Operacionais** e selecione o nó **Drivers**.  

2. Selecione os drivers de dispositivo que você deseja adicionar ao pacote de driver.  

3. Na guia **Início** da faixa de opções, no grupo **Driver**, selecione **Editar** e, em seguida, escolha **Imagens de Inicialização**.  

4. Para adicionar um driver de dispositivo, marque a caixa de seleção da imagem de inicialização à qual deseja adicionar os drivers de dispositivo. Para remover um driver de dispositivo, desmarque a caixa de seleção da imagem de inicialização da qual deseja remover o driver de dispositivo.  

5. Caso não deseje atualizar os pontos de distribuição onde a imagem de inicialização está armazenada, desmarque a caixa de seleção **Atualizar pontos de distribuição ao terminar**. Por padrão, os pontos de distribuição são atualizados quando a imagem de inicialização é atualizada.  

    - Selecione **Sim** na caixa de diálogo para atualizar as imagens de inicialização nos pontos de distribuição. Não é possível usar drivers de dispositivo até que eles sejam distribuídos aos pontos de distribuição. Se você selecionar **Não**, execute a ação **Atualizar Ponto de Distribuição** antes de usar a imagem de inicialização. Se o pacote de driver nunca foi distribuído, você deve usar a ação **Distribuir Conteúdo** no nó **Pacotes de Driver**.  

    - O Configuration Manager avisará se a arquitetura de um ou mais drivers não corresponder à arquitetura das imagens de inicialização selecionadas. Se elas não corresponderem, selecione **OK**. Volte para a página **Detalhes do Driver** e desmarque os drivers que não correspondem à arquitetura da imagem de inicialização selecionada. Por exemplo, se você selecionar uma imagem de inicialização em base em x64 e x86, todos os drivers devem dar suporte a ambas as arquiteturas. Se você selecionar uma imagem de inicialização com base em x64, todos os drivers devem dar suporte à arquitetura x64.  

        > [!NOTE]
        > - A arquitetura é baseada na arquitetura relatada no INF do fabricante.  
        > - Se um driver relatar que dá suporte a ambas as arquiteturas, você poderá importá-lo para qualquer uma das duas imagens de inicialização.  

    - O Configuration Manager avisa se você adicionar drivers de dispositivo que não sejam drivers de rede ou de armazenamento a uma imagem de inicialização. Na maioria dos casos, eles não são necessários para a imagem de inicialização. Selecione **Sim** para adicionar os drivers à imagem de inicialização ou **Não** para voltar e modificar sua seleção de driver.  

    - O Configuration Manager avisará se um ou mais dos drivers selecionados não estiverem assinados digitalmente de maneira correta. Selecione **Sim** para continuar ou selecione **Não** para voltar e fazer alterações em sua seleção de driver.  


### <a name="BKMK_DriverActions"></a> Ações adicionais para drivers de dispositivo  

Você pode executar ações adicionais para gerenciar drivers quando selecioná-los no nó **Drivers**.  

#### <a name="categorize"></a>Categorizar
Limpa, gerencia ou define uma categoria administrativa para os drivers selecionados.

#### <a name="delete"></a>Excluir
Remove o driver do nó **Drivers** e também remove o driver dos pontos de distribuição associados.

#### <a name="disable"></a>Desabilitar
Proíbe a instalação do driver. Essa ação desabilita temporariamente o driver. A sequência de tarefas não pode instalar um driver desabilitado ao implantar um sistema operacional. 

> [!Note]  
> Essa ação apenas impede que os drivers sejam instalados usando a etapa da sequência de tarefas **Driver de Aplicação Automática**.

#### <a name="enable"></a>Habilitar
Permite que computadores cliente e sequências de tarefas do Configuration Manager instalem o driver de dispositivo durante a implantação do SO.

#### <a name="move"></a>Mover
Move o driver de dispositivo para outra pasta do nó **Drivers** .

#### <a name="properties"></a>Propriedades
Abre a caixa de diálogo **Propriedades**. Revise e altere as propriedades do driver. Por exemplo, altere seu nome e descrição, habilite ou desabilite-o e especifique em quais plataformas ele pode ser executado.



## <a name="BKMK_TSDrivers"></a> Usar sequências de tarefas para instalar drivers  

Use sequências de tarefas para automatizar a forma como o SO é implantado. Cada etapa da sequência de tarefas pode executar uma ação específica, como instalar um driver. Ao implantar um SO, você pode usar as duas etapas de sequência de tarefas a seguir para instalar os drivers de dispositivo:  

- [Drivers de Aplicação Automática](/sccm/osd/understand/task-sequence-steps#BKMK_AutoApplyDrivers): Esta etapa permite que você combine automaticamente e instale drivers de dispositivo como parte de uma implantação de sistema operacional. Você pode configurar a etapa da sequência de tarefas para instalar apenas o melhor driver correspondente a cada dispositivo de hardware detectado. Como alternativa, especifique que a etapa instala todos os drivers compatíveis para cada dispositivo de hardware detectado e, em seguida, deixe a Instalação do Windows escolher o melhor driver. Você também pode especificar uma categoria de driver para limitar os drivers disponíveis para essa etapa.  

- [Aplicar pacote de driver](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyDriverPackage): Esta etapa permite disponibilizar para a instalação do Windows todos os drivers de dispositivo de um pacote de driver específico. Nos pacotes de driver especificados, a instalação do Windows busca drivers de dispositivo que são necessários. Ao criar a mídia autônoma, é necessário usar esta etapa para instalar drivers de dispositivo.  

Ao usar essas etapas de sequência de tarefas, você também pode especificar como os drivers são instalados no computador onde o SO está sendo implantado. Para obter mais informações, consulte [Gerenciar sequências de tarefas para automatizar tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks).  



## <a name="BKMK_DriverReports"></a> Relatórios de driver  

Na categoria de relatórios **Gerenciamento de driver** , vários relatórios podem ser usados para determinar informações gerais sobre os drivers de dispositivo no catálogo de driver. Para obter mais informações sobre relatórios, consulte [Relatórios](/sccm/core/servers/manage/reporting).

