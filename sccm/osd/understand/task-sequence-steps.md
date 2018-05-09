---
title: Etapas da sequência de tarefas
titleSuffix: Configuration Manager
description: Saiba mais sobre as etapas que você pode adicionar a uma sequência de tarefas do Configuration Manager.
ms.date: 03/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a678cbbd8500070e2d4056d6e424818e7000ef83
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="task-sequence-steps-in-system-center-configuration-manager"></a>Etapas da sequência de tarefas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As etapas de sequência de tarefas a seguir podem ser adicionadas à sequência de tarefas do Configuration Manager. Para obter informações sobre como editar uma sequência de tarefas, veja [Edit a task sequence](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

As configurações a seguir são comuns a todas as etapas da sequência de tarefas:

Na guia **Propriedades**:
 - **Nome**: o editor de sequência de tarefas requer que você especifique um nome curto para descrever essa etapa. Quando você adiciona uma nova etapa, o editor de sequência de tarefas define o nome para o Tipo por padrão. O tamanho do **Nome** não pode exceder 50 caracteres.
 - **Descrição**: opcionalmente, especifique informações mais detalhadas sobre essa etapa. O tamanho da **Descrição** não pode exceder 256 caracteres.
O restante deste artigo descreve as outras configurações na guia **Propriedades** para cada etapa da sequência de tarefas.

Na guia **Opções**:  
-   **Desabilitar esta etapa**: a sequência de tarefas ignora essa etapa quando ela é executada em um computador. O ícone para esta etapa é esmaecido no editor de sequência de tarefas. 
-   **Continuar em caso de erro**: a sequência de tarefas continua se um erro ocorre ao executar a etapa.  
-   **Adicionar Condição**: A sequência de tarefas avalia essas instruções condicionais para determinar se ela executa a etapa.   
As seções abaixo para etapas específicas de sequência de tarefas descrevem outras configurações possíveis na guia **Opções**.



##  <a name="BKMK_ApplyDataImage"></a> Aplicar Imagem de Dados   
 Use essa etapa para copiar a imagem de dados na partição de destino especificada.  

 Esta etapa é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão. Para mais informações sobre as variáveis de sequência de tarefas, confira [Variáveis de ação de sequência de tarefas](task-sequence-action-variables.md).  

No editor de sequência de tarefas, clique em **Adicionar**, selecione **Imagens** e selecione **Aplicar Imagem de Dados** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Pacote da imagem**  
 Clique em **Procurar** para especificar o **Pacote de Imagem** usado por essa sequência de tarefas. Selecione o pacote que você deseja instalar na caixa de diálogo **Selecionar um pacote** . As informações de propriedade associada para cada pacote de imagem existente são exibidas na parte inferior da caixa de diálogo **Selecionar um pacote** . Use a lista suspensa para selecionar a **imagem** você deseja instalar por meio do **Pacote de imagem**selecionado.  

> [!NOTE]  
>  Esta ação da sequência de tarefas trata a imagem como um arquivo de dados. Esta ação não faz nenhuma configuração para inicializar a imagem como um sistema operacional.  

 **Destino**  
 Configure uma das seguintes opções:

-   **Próxima partição disponível**: use a próxima partição sequencial que ainda não foi usada como destino por uma ação **Aplicar Sistema Operacional** ou **Aplicar Imagem de Dados** nessa sequência de tarefas.  

-   **Disco e partição específicos**: selecione o número do **Disco** (começando com 0) e o da **Partição** (começando com 1).  

-   **Letra da unidade lógica específica**: especifique a **Letra da Unidade** atribuída à partição pelo Windows PE. Essa letra de unidade pode ser diferente da letra de unidade atribuída pelo sistema operacional implantado recentemente.  

-   **Letra de unidade lógica armazenada em uma variável**: especifique a variável de sequência de tarefas que contém a letra da unidade atribuída à partição pelo Windows PE. Essa variável é normalmente definida na seção Avançado da caixa de diálogo **Propriedades da partição** para a ação da sequência de tarefa **Formatar e particionar o disco**.  

**Excluir todo o conteúdo da partição antes de aplicar a imagem**  
 Especifica que a sequência de tarefas exclui todos os arquivos na partição de destino antes de instalar a imagem. Não excluindo o conteúdo da partição, esta etapa pode ser usada para aplicar o conteúdo adicional a uma partição de destino anterior.  



##  <a name="BKMK_ApplyDriverPackage"></a> Aplicar pacote de driver  
 Use esta etapa para baixar todos os drivers no pacote de driver e instalá-los no sistema operacional Windows.

 A etapa da sequência de tarefas **Aplicar pacote de Driver** disponibiliza todos os drivers de dispositivo em um pacote de driver para uso pelo Windows. Adicione esta etapa entre as etapas **Aplicar sistema operacional** e **Instalação do Windows e do ConfigMgr** para disponibilizar os drivers de dispositivo no pacote de drivers para o Windows. Normalmente, a etapa **Aplicar pacote de Driver** é posicionada após a **Aplicação automática de drivers** . A etapa da sequência de tarefas **Aplicar pacote de Driver** também é útil em cenários de implantação de mídia autônoma.  

 Verifique se os drivers de dispositivo similares são colocados em um pacote de driver e distribua-os aos pontos de distribuição apropriados. Depois de eles serem distribuídos, os computadores cliente do Configuration Manager poderão instalá-los. Por exemplo, coloque todos os drivers de um fabricante em um pacote de driver. Em seguida, distribua o pacote para pontos de distribuição em que os computadores associados possam acessá-lo.

 A etapa **Aplicar Pacote de Driver** é útil para mídia autônoma. Esta etapa também é útil se você quer instalar um conjunto específico de drivers. Esses tipos de drivers incluem dispositivos que não serão detectados em uma varredura de plug-and-play, tal como impressoras de rede.  

 Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Apply Driver Package Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyDriverPackage).  

No editor de sequência de tarefas, clique em **Adicionar**, selecione **Drivers** e selecione **Aplicar Pacote de Driver** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Pacote de drivers**  
 Especifique o pacote de driver que contém os drivers de dispositivo necessários clicando em **Procurar** e iniciando a caixa de diálogo **Selecionar um pacote** . Especifique um pacote existente para disponibilizar. As propriedades do pacote associado são exibidas na parte inferior da caixa de diálogo.  

 **Selecione o driver de armazenamento em massa dentro do pacote que precisa ser instalado antes da instalação em sistemas operacionais anteriores ao Windows Vista**  
 Especifique os drivers de armazenamento em massa necessários para instalar um sistema operacional clássico.  

 **Driver**  
 Selecione o arquivo de driver de armazenamento em massa para instalar antes da instalação de um sistema operacional clássico. A lista suspensa é populada do pacote especificado.  

 **Modelo**  
 Especifique a inicialização crítica de dispositivo necessária para implantações de sistemas operacionais anteriores ao Windows Vista.  

 **Faça uma instalação autônoma de drivers não assinados nas versões do Windows em que isso é permitido**  
 Essa opção permite que o Windows instale drivers sem uma assinatura digital.  



##  <a name="BKMK_ApplyNetworkSettings"></a> Aplicar Configurações de Rede   
 Use essa etapa para especificar as informações de configuração de rede ou grupo de trabalho do computador de destino. A sequência de tarefas armazena esses valores no arquivo de resposta apropriado. A Instalação do Windows usa esse arquivo de resposta durante a ação **Instalação do Windows e ConfigMgr**.  

 Essa etapa de sequência de tarefas é executada em um sistema operacional padrão ou o Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Apply Network Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyNetworkSettings).  

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Configurações** e selecione **Aplicar Configurações de Rede** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Ingressar no grupo de trabalho**  
 Selecione esta opção para fazer o computador de destino ingressar no grupo de trabalho especificado. Insira o nome do grupo de trabalho na linha **Grupo de trabalho** . Esse valor pode ser substituído pelo valor capturado pela etapa da sequência de tarefas **Capturar as configurações de rede** .  

 **Ingressar em um domínio**  
 Selecione esta opção para fazer o computador de destino ingressar no domínio especificado. Especifique ou navegue para o domínio, como *fabricam.com*. Especifique ou procure um caminho LDAP (Lightweight Directory Access Protocol) para uma unidade organizacional. Por exemplo: *LDAP//OU=computers, DC=Fabricam.com, C=com*  

 **Conta**  
 Clique em **Definir** para especificar uma conta com as permissões necessárias para ingressar o computador no domínio. Na caixa de diálogo **Conta de Usuário do Windows**, é possível inserir o nome de usuário usando o seguinte formato: **Domínio\Usuário**.  

 **Adapter settings (Configurações do adaptador)**  
 Especifica configurações de rede para cada adaptador de rede no computador. Clique em **Novo** para abrir a caixa de diálogo **Configurações de rede** e especifique as configurações de rede. Se você também usar a etapa **Capturar Configurações de Rede**, a sequência de tarefas aplicará as configurações capturadas anteriormente ao adaptador de rede. A sequência de tarefas não aplica as configurações especificadas nesta etapa. Se a sequência de tarefas não captura as configurações de rede anteriormente, ela aplica as configurações especificadas na etapa **Aplicar Configurações de Rede**. A sequência de tarefas aplica essas configurações a adaptadores de rede na ordem de enumeração de dispositivos do Windows.  



##  <a name="BKMK_ApplyOperatingSystemImage"></a> Aplicar Imagem de Sistema Operacional  

> [!TIP]  
> Começando com o Windows 10, versão 1709, a mídia inclui várias edições. Quando você configura uma sequência de tarefas para usar uma imagem do sistema operacional ou um pacote de atualização do sistema operacional, é necessário selecionar uma [edição compatível](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).

 Use essa etapa para instalar um sistema operacional no computador de destino. Esta etapa executa ações, dependendo de ela usar ou não uma imagem do SO ou um pacote de atualização do SO.  

 A etapa **Aplicar imagem do sistema operacional** executa as seguintes ações ao usar uma imagem do SO:  

1.  Exclua todo o conteúdo no volume de destino, exceto os arquivos na pasta especificada pela variável &#95;SMSTSUserStatePath.

2.  Extração do conteúdo do arquivo .wim especificado para a partição de destino especificada.  

3.  Prepare o arquivo de resposta:  

    1.  Criação de um novo arquivo de resposta padrão da Instalação do Windows (sysprep.inf ou unattend.xml) para o sistema operacional que está sendo implantado.  

    2.  Mescle quaisquer valores do arquivo de resposta fornecido pelo usuário.  

4.  Cópia de carregadores de inicialização do Windows para a partição ativa.  

5.  Configuração do boot.ini ou do BCD (Banco de Dados de Configuração da Inicialização) para referenciar o sistema operacional recém-instalado.  

 A etapa **Aplicar imagem do sistema operacional** executa as seguintes ações ao usar um pacote de atualização do SO:  

1.  Exclua todo o conteúdo no volume de destino, exceto os arquivos na pasta especificada pela variável &#95;SMSTSUserStatePath.  

2.  Prepare o arquivo de resposta:  

    1.  Criação de um arquivo de resposta novo com valores padrão criados pelo Configuration Manager.  

    2.  Mescle quaisquer valores do arquivo de resposta fornecido pelo usuário.  

> [!NOTE]  
>  A etapa **Instalar o Windows e o ConfigMgr** inicia a Instalação do Windows. 

 Após a ação **Aplicar sistema operacional** ser executada, a variável OSDTargetSystemDrive é definida como a letra da unidade da partição que contém os arquivos do sistema operacional.  

 Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Apply Operating System Image Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyOperatingSystem).  

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Imagens** e selecione **Aplicar Imagem do Sistema Operacional** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Aplicar o sistema operacional de uma imagem capturada**  
 Instala uma imagem do sistema operacional que foi capturada anteriormente. Clique em **Procurar** para abrir a caixa de diálogo **Selecionar um pacote** e selecione o pacote de imagem existente que você deseja instalar. Se várias imagens forem associadas ao **pacote de imagem**especificado, use a lista suspensa para especificar a imagem associada que será usada para essa implantação. Você pode exibir informações básicas sobre cada imagem existente clicando na imagem.  

 **Apply operating system image from an original installation source (Aplicar a imagem do sistema operacional de uma fonte de instalação original)**  
 Instala um sistema operacional usando a instalação original. Clique em **Procurar** para abrir a caixa de diálogo **Selecionar um Pacote de Instalação do Sistema Operacional**. Em seguida, selecione o pacote de atualização do SO existente que você deseja usar. Você pode exibir informações básicas sobre cada origem de imagem existente clicando na origem da imagem. As propriedades da origem da imagem associada são exibidas no painel de resultados, na parte inferior da caixa de diálogo. Se houver várias edições associadas ao pacote especificado, use a lista suspensa para especificar a **Edição** associada a ser usada.  

 **Usar um arquivo de resposta autônomo ou Sysprep para uma instalação personalizada**  
 Use esta opção para fornecer um arquivo de resposta de instalação do Windows (**unattend.xml**, **unattend.txt**, ou **sysprep.inf**) dependendo do método de instalação e da versão do sistema operacional. O arquivo especificado pode incluir qualquer uma das opções de configuração padrão compatíveis com arquivos de resposta do Windows. Por exemplo, você pode usá-la para especificar a página inicial padrão do Internet Explorer. Especifique o pacote que contém o arquivo de resposta e o caminho associado ao arquivo no pacote.  

> [!NOTE]  
>  O arquivo de resposta da Instalação do Windows que você fornece pode conter de variáveis de sequência de tarefa integradas do formulário %*varname*%, em que *varname* é o nome da variável. A etapa **Instalação do Windows e ConfigMgr** substitui a cadeia de caracteres *%varname%* para os valores reais de variável. Essas variáveis de sequência de tarefas integradas não podem ser usadas em campos somente numérico em um arquivo de resposta unattend.xml.  

 Se você não fornecer um arquivo de resposta de Instalação do Windows, essa ação da sequência de tarefas gerará automaticamente um arquivo de resposta.  

 **Destino**  
 Configure uma das seguintes opções:  

-   **Próxima partição disponível**: use a próxima partição sequencial que ainda não foi usada como destino por uma ação **Aplicar Sistema Operacional** ou **Aplicar Imagem de Dados** nessa sequência de tarefas. 

-   **Disco e partição específicos**: selecione o número do **Disco** (começando com 0) e o da **Partição** (começando com 1).  

-   **Letra da unidade lógica específica**: especifique a **Letra da Unidade** atribuída à partição pelo Windows PE. Essa letra de unidade pode ser diferente da letra de unidade atribuída pelo sistema operacional implantado recentemente.  

-   **Letra de unidade lógica armazenada em uma variável**: especifique a variável de sequência de tarefas que contém a letra da unidade atribuída à partição pelo Windows PE. Essa variável é normalmente definida na seção Avançado da caixa de diálogo **Propriedades da partição** para a ação da sequência de tarefa **Formatar e particionar o disco**.  

### <a name="options"></a>Opções  
 Além das opções padrão, defina as seguintes configurações adicionais na guia **Opções** dessa etapa da sequência de tarefas:  

-   **Acessar o conteúdo diretamente do ponto de distribuição**  
     Configure a sequência de tarefas para acessar a imagem do sistema operacional diretamente do ponto de distribuição. Por exemplo, use essa opção ao implantar sistemas operacionais em dispositivos inseridos que têm a capacidade de armazenamento limitada. Ao selecionar essa opção, configure também as configurações de compartilhamento de pacote na guia **Acesso a Dados** das propriedades do pacote.  

    > [!NOTE]  
    >  Essa configuração substitui a opção de implantação que você configura na página **Pontos de Distribuição** do **Assistente de Implantação de Software**. Essa substituição é apenas para a imagem do sistema operacional que esta etapa especifica, não para todo o conteúdo da sequência de tarefas.  



##  <a name="BKMK_ApplyWindowsSettings"></a> Aplicar as Configurações do Windows  
 Use essa etapa para definir as configurações do Windows no computador de destino. A sequência de tarefas armazena esses valores no arquivo de resposta apropriado. A Instalação do Windows usa esse arquivo de resposta durante a ação **Instalação do Windows e ConfigMgr**.  

 Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Apply Windows Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyWindowsSettings).  

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Configurações** e selecione **Aplicar Configurações do Windows** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Nome de usuário**  
 Especifique o nome de usuário registrado que está associado com o computador de destino. Esse valor pode ser substituído pelo valor capturado pela etapa da sequência de tarefas **Capturar as configurações do Windows** .  

 **Nome da organização**  
 Especifique o nome de organização registrado que está associado com o computador de destino. Esse valor pode ser substituído pelo valor capturado pela etapa da sequência de tarefas **Capturar as configurações do Windows** .  

 **Chave do produto (Product Key)**  
 Especifique a chave do produto que é usada para a instalação do Windows no computador de destino.  

 **Licenciamento por servidor**  
 Especifique o modo de licenciamento do servidor. Você pode selecionar **Por servidor** ou **Por usuário** como o modo de licenciamento. Se você selecionar **Por servidor**, especifique também o número máximo de conexões permitidas por seu contrato de licença. Selecione **Não especificar** se o computador de destino não é um servidor ou se você não quiser especificar o modo de licenciamento.  

 **Máximo de conexões**  
 Especifique o número máximo de conexões que estão disponíveis para este computador conforme indicado no contrato de licença.  

 **Gerar aleatoriamente a senha do administrador local e desabilitar a conta em todas as plataformas com suporte (recomendado)**  
 Selecione esta opção para definir a senha de administrador local para uma cadeia de caracteres gerada aleatoriamente. Essa opção também desabilita a conta de administrador local em plataformas compatíveis com essa funcionalidade.  

 **Habilitar a conta e especificar a senha do administrador local**  
 Selecione esta opção para habilitar a conta de administrador local usando a senha especificada. Insira a senha na linha **Senha** e confirme a senha na linha **Confirmar senha** .  

 **Fuso Horário**  
 Especifique o fuso horário para o computador de destino. Esse valor pode ser substituído pelo valor capturado pela etapa da sequência de tarefas **Capturar as configurações do Windows** .  



##  <a name="BKMK_AutoApplyDrivers"></a> Drivers de Aplicação Automática  
 Use essa etapa para realizar a correspondência de drivers e instalá-los como parte da implantação do sistema operacional.  

 A etapa da sequência de tarefas **Aplicação automática de drivers** executa as seguintes ações:  

1.  Verifica o hardware e localiza as IDs de Plug-and-Play para todos os dispositivos presentes no sistema.  

2.  Envia a lista de dispositivos e das respectivas IDs de Plug-and-Play para o ponto de gerenciamento. O ponto de gerenciamento retorna uma lista de drivers compatíveis do catálogo de drivers para cada dispositivo de hardware. A lista inclui todos os drivers, independentemente do pacote de driver em que eles estão, incluindo drivers marcados com a categoria de driver especificada e drivers não desabilitados.  

3.  A sequência de tarefas seleciona o melhor driver para cada dispositivo de hardware. Esse driver é apropriado para o sistema operacional implantado e está em um ponto de distribuição acessível.  

4.  A sequência de tarefas baixa os drivers selecionados de um ponto de distribuição e prepara-os no sistema operacional de destino.  

    1.  Para instalações baseadas em imagem, a sequência de tarefas coloca os drivers no repositório de drivers do sistema operacional.  

    2.  Para instalações diretas, a sequência de tarefas configura a Instalação do Windows com o local dos drivers.  

5.  Durante a etapa **Instalar o Windows e o ConfigMgr** na sequência de tarefas, a Instalação do Windows encontra os drivers preparados por esta ação.  

> [!IMPORTANT]
>  A mídia autônoma não é capaz de usar a etapa **Aplicar Drivers Automaticamente**. A Instalação do Windows não tem nenhuma conexão com o site do Configuration Manager neste cenário.

Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Auto Apply Drivers Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_AutoApplyDrivers).  

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Drivers** e selecione **Aplicar Drivers Automaticamente** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Instalar apenas os drivers compatíveis que mais correspondam**  
 Especifica que a etapa de sequência de tarefas instala apenas o melhor driver correspondente a cada dispositivo de hardware detectado.  

 **Instalar todos os drivers compatíveis**  
 A sequência de tarefas instala todos os drivers compatíveis para cada dispositivo de hardware detectado. A Instalação do Windows escolhe então o melhor driver. Esta opção ocupa mais espaço em disco e largura de banda da rede. A sequência de tarefas baixa mais drivers, mas o Windows pode selecionar um driver melhor.  

 **Considerar os drivers de todas as categorias**  
 A sequência de tarefas pesquisa todas as categorias de driver disponíveis para os drivers de dispositivo apropriados.  

 **Limitar a correspondência de driver para considerar somente os drivers nas categorias selecionadas**  
 A sequência de tarefas pesquisa todas as categorias de driver especificadas para os drivers de dispositivo apropriados.  

 **Fazer instalação autônoma de drivers não assinados em versões do Windows, onde permitido**  
 Essa opção permite que o Windows instale drivers sem uma assinatura digital.   

  > [!IMPORTANT]  
  >  Essa opção não se aplica aos sistemas operacionais em que a política de assinatura de driver não pode ser configurada.  



##  <a name="BKMK_CaptureNetworkSettings"></a> Capturar configurações da rede  
 Use esta etapa para capturar as configurações de rede da Microsoft no computador que executa a sequência de tarefas. A sequência de tarefas salva essas configurações em variáveis de sequência de tarefas. Essas configurações substituem as configurações padrão definidas na etapa **Aplicar Configurações de Rede**.  

 Essa etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Capture Network Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureNetworkSettings).  

No editor de sequência de tarefas, clique em **Adicionar**, selecione **Configurações** e selecione **Capturar Configurações de Rede** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Migrar associação de domínio e grupo de trabalho**  
 Captura as informações de associação de domínio e grupo de trabalho do computador de destino.  

 **Migrar configuração do adaptador de rede**  
 Captura a configuração do adaptador de rede do computador de destino. As informações capturadas incluem as configurações de rede global, o número de adaptadores e as configurações de rede associadas a cada adaptador. Essas configurações incluem as configurações associadas com DNS, WINS, IP e filtros de porta.  



##  <a name="BKMK_CaptureOperatingSystemImage"></a> Capturar imagem do sistema operacional  
 Essa etapa captura uma ou mais imagens de um computador de referência. A sequência de tarefas cria um arquivo de imagem do Windows (.wim) no compartilhamento de rede especificado. Em seguida, use o assistente **Adicionar Pacote de Imagem de Sistema Operacional** para importar esta imagem para o Configuration Manager para que ele possa ser usado para implantações de sistema operacional baseadas em imagem.  

 O Configuration Manager captura cada volume (unidade) no computador de referência para uma imagem separada dentro do arquivo .wim. Se o computador de referência tiver vários volumes, o arquivo .wim resultante conterá uma imagem separada para cada volume. Apenas volumes formatados como NTFS ou FAT32 são capturados. Volumes com outros formatos e USB são ignorados.  

 O sistema operacional instalado no computador de referência deve ser uma versão do Windows compatível com o Configuration Manager. Use a ferramenta SysPrep para preparar o sistema operacional do computador de referência. O volume do sistema operacional instalado e o volume de inicialização devem ser o mesmo volume.  

 Especifique uma conta com permissões de gravação para o compartilhamento de rede selecionado.  

 Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Capture Operating System Image Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureOperatingSystemImage).  

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Imagens** e selecione **Capturar Imagem do Sistema Operacional** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Destino**  
 Nome do caminho do sistema de arquivos para o local que o Configuration Manager usa ao armazenar a imagem capturada do sistema operacional.  

 **Descrição**  
 Uma descrição opcional definida pelo usuário da imagem capturada do sistema operacional que é armazenada no arquivo .WIM.  

 **Versão**  
 Um número de versão opcional definido pelo usuário para atribuir a imagem capturada do sistema operacional. Esse valor pode ser qualquer combinação de letras e números e é armazenado no arquivo .WIM.  

 **Criado por**  
 O nome opcional do usuário que criou a imagem do sistema operacional e é armazenado no arquivo WIM.  

 **Capture operating system image account (Capturar conta de imagem do sistema operacional)**  
 Você deve inserir a conta do Windows que tenha permissões para a rede a compartilhar especificada. Clique em **Definir** para especificar o nome dessa conta do Windows.  



##  <a name="BKMK_CaptureUserState"></a> Capturar Estado do Usuário  
 Use esta etapa para usar a USMT (Ferramenta de Migração do Usuário) para capturar o estado do usuário e configurações do computador que executa a sequência de tarefas. Essa etapa de sequência de tarefas é usada em conjunto com a etapa da sequência de tarefas **Restaurar o estado do usuário** . Com o USMT 3.0.1 e posterior, essa opção sempre criptografa o armazenamento de estado do USMT usando uma chave de criptografia geradas e gerenciadas por Configuration Manager.  

 Para mais informações sobre como gerenciar o estado do usuário ao implantar sistemas operacionais, confira [Gerenciar o estado do usuário](../get-started/manage-user-state.md).  

 Se você deseja salvar e restaurar configurações de estado de usuário de um ponto de migração de estado, use a etapa **Capturar Estado do Usuário** com as etapas **Solicitar Repositório de Estado** e **Liberar Repositório de Estado**.  

 A etapa da sequência de tarefas **Capturar estado do usuário** fornece controle sobre um subconjunto limitado dos mais opções mais usadas do USMT. Opções de linha de comando adicionais podem ser especificadas usando a variável de sequência de tarefas OSDMigrateAdditionalCaptureOptions.  

 Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Capture User State Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureUserState).  

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Estado de Usuário** e selecione **Capturar Estado de Usuário** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Pacote da ferramenta de migração do usuário**  
 Especifique o pacote que contém a USMT (Ferramenta de Migração do Usuário). A sequência de tarefas usa esta versão da USMT para capturar o estado do usuário e as configurações. Este pacote não exige um programa. Especifique um pacote que contém a versão de 32 bits ou 64 bits do USMT. A arquitetura da USMT varia de acordo com a arquitetura do sistema operacional do qual a sequência de tarefas está realizando a captura de estado.  

 **Capture all user profiles with standard options (Capturar todos os perfis de usuário com opções padrão)**  
 Migre todas as informações de perfil do usuário. Esta é a opção padrão.  

 Se você selecionar essa opção, mas não selecionar **Restaurar perfis de usuário do computador local** na etapa **Restaurar Estado do Usuário**, a sequência de tarefas falhará. O Configuration Manager não pode migrar as novas contas sem atribuir senhas a elas. 

 Quando você usa a opção **Instalar um pacote de imagem existente** do assistente **Nova Sequência de Tarefas**, a sequência de tarefas resultante assume como padrão **Capturar todos os perfis de usuário com opções padrão**. Essa sequência de tarefas padrão não seleciona a opção de **Restaurar perfis de usuário do computador local**, em outras palavras, as contas de usuário de fora do domínio.  

 Selecione **Restaurar perfis de usuário do computador local** e forneça uma senha para a conta a ser migrada. Em uma sequência de tarefas criadas manualmente, essa configuração é encontrada na etapa Restaurar estado do usuário. Em uma sequência de tarefas criada pelo assistente **Nova sequência de tarefas** , essa configuração se encontra na página do assistente **Restaurar arquivos e configurações do usuário** .  

 Se você não tem nenhuma conta de usuário local, essa configuração não se aplica.  

 **Personalizar o modo como perfis de usuários são capturados**  
 Selecione esta opção para especificar uma migração de arquivo de perfil personalizado. Clique em **Arquivos** para selecionar os arquivos de configuração do USMT a serem usados com esta etapa. Especifique um arquivo .xml personalizado que contenha regras que definam os arquivos de estado do usuário para migrar.  

 **Clique aqui para selecionar os arquivos de configuração:**  
 Selecione esta opção para selecionar os arquivos de configuração do pacote da USMT que deseja usar para capturar os perfis de usuário. Clique no botão **Arquivos** para abrir a caixa de diálogo **Arquivos de configuração** . Para especificar um arquivo de configuração, insira o nome do arquivo na linha **Nome do arquivo** e clique no botão **Adicionar** .  

 **Habilitar log detalhado**  
 Habilite esta opção para gerar informações de arquivo de log mais detalhadas. Durante a captura de estado, a sequência de tarefas gera por padrão o ScanState.log na pasta de log de sequência de tarefas \windows\system32\ccm\logs.   

 **Skip files using encrypted file system (Ignorar arquivos usando o sistema de arquivos criptografados)**  
 Habilite esta opção para ignorar a captura de arquivos criptografados com o EFS (sistema de arquivos com criptografia). Esses arquivos incluem arquivos de perfil do usuário. Dependendo do sistema operacional e a versão do USMT, arquivos criptografados podem não ser lidos após a restauração. Para obter mais informações, consulte a documentação do USMT.  

 **Copiar usando o acesso ao sistema de arquivos**  
 Habilite esta opção especificar qualquer uma das seguintes configurações:  

-   **Continuar se não for possível capturar alguns arquivos**: habilite essa configuração para continuar o processo de migração mesmo que alguns arquivos não possam ser capturados. Se você desabilitar essa opção e um arquivo não puder ser capturado, a etapa da sequência de tarefas falhará. Essa opção é habilitada por padrão.  

-   **Capturar localmente usando links em vez de copiar arquivos**: habilite essa configuração para usar links físicos NTFS para capturar arquivos.  

     Para obter mais informações sobre como migrar dados usando links físicos, consulte [Repositório de migração de link físico](http://go.microsoft.com/fwlink/p/?LinkId=240222)  

-   **Capturar em modo offline (somente Windows PE)**: habilite essa configuração para capturar o estado de usuário no Windows PE em vez do sistema operacional completo.  
    
**Capture by using Volume Copy Shadow Services (VSS) (Capturar usando o VSS (Serviços de Cópias de Sombra de Volume))**  
 Essa opção permite capturar arquivos mesmo se eles estiverem bloqueados para edição por outro aplicativo.  



##  <a name="BKMK_CaptureWindowsSettings"></a> Capturar Configurações do Windows  
 Use esta etapa para capturar as configurações do Windows no computador que executa a sequência de tarefas. A sequência de tarefas salva essas configurações em variáveis de sequência de tarefas. Essas configurações capturadas substituem as configurações padrão definidas na etapa **Aplicar Configurações do Windows**.  

 Essa etapa de sequência de tarefas é executada em um sistema operacional padrão ou o Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Capture Windows Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureWindowsSettings).  

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Configurações** e selecione **Capturar Configurações do Windows** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Migrar nome do computador**  
 Capture o nome do computador NetBIOS do computador.  

 **Migrar nomes de usuário e de organização registrados**  
 Capture os nomes de usuário e de organização registrados do computador.  

 **Migrar fuso horário**  
 Capture a configuração de fuso horário no computador.  



##  <a name="BKMK_CheckReadiness"></a> Verificar Preparação  
 Use esta etapa para verificar se o computador de destino atende às condições de pré-requisitos de implantação especificadas.  

No editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e selecione **Verificar Preparação** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Assegurar o mínimo de memória (MB)**  
 Verifique se a quantidade de memória, em megabytes (MB), atende ou excede o valor especificado. A etapa habilita essa configuração por padrão.  

 **Assegurar o mínimo de velocidade do processador (MHz)**  
 Verifique se a velocidade do processador, em mega-hertz (MHz), atende ou excede o valor especificado. A etapa habilita essa configuração por padrão.  

 **Assegurar o mínimo de espaço livre em disco (MB)**  
 Verificar se a quantidade de espaço livre em disco, em megabytes (MB), atende ou excede o valor especificado.  

 **Assegurar que o SO atual a ser atualizado seja**  
 Verifique se o sistema operacional instalado no computador de destino atende o requisito especificado. A etapa define isso para **CLIENTE** por padrão.  

### <a name="options"></a>Opções
 > [!NOTE]  
 > Se você habilitar a configuração **Continuar em caso de erro** na guia **Opções** desta etapa, ele registra apenas os resultados da verificação de preparação. Se uma verificação falhar, a sequência de tarefas não será interrompida.



##  <a name="BKMK_ConnectToNetworkFolder"></a> Conectar à Pasta de Rede  
 Use essa etapa para criar uma conexão a uma pasta de rede compartilhada.  

 Essa etapa de sequência de tarefas é executada em um sistema operacional padrão ou o Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Connect to Network Folder Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ConnecttoNetworkFolder).  

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e selecione **Conectar-se à Pasta de Rede** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Caminho**  
 Clique em **Procurar** para especificar o caminho da pasta de rede. Use o formato *\\\server\share*.

 **Unidade**  
 Selecione a letra da unidade local para atribuir a esta conexão. 

 **Conta**  
 Clique em **Definir** para especificar a conta de usuário com permissões para se conectar a esta pasta de rede.



##  <a name="BKMK_DisableBitLocker"></a> Desabilitar BitLocker  
 Use esta etapa para desabilitar a criptografia BitLocker na unidade do sistema operacional atual ou em uma unidade específica. Essa ação deixa os protetores de chave visíveis em texto não criptografado no disco rígido, mas não descriptografa o conteúdo da unidade. Consequentemente, essa ação é concluída quase instantaneamente.  

> [!NOTE]  
>  A criptografia de unidade de disco BitLocker fornece criptografia de baixo nível do conteúdo de um volume de disco.  

 Se você tiver várias unidades criptografadas, você deve desabilitar o BitLocker nas unidades de dados antes de desativar o BitLocker na unidade do sistema operacional.  

 Esta etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE.  

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Discos** e selecione **Desabilitar BitLocker** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Unidade do sistema operacional atual**  
 Desabilita o BitLocker na unidade do sistema operacional atual.  

 **Unidade específica**  
 Desabilita o BitLocker em uma unidade específica. Use a lista suspensa para especificar a unidade em que o BitLocker será desabilitado.  



##  <a name="BKMK_DownloadPackageContent"></a> Baixar o conteúdo do pacote  
 Use essa etapa para baixar qualquer um dos seguintes tipos de pacote:  

-   Imagens do sistema operacional  

-   Pacotes de atualização de sistema operacional  

-   Pacotes de driver  

-   Pacotes  

-   Imagens de inicialização
    
Esta etapa funciona bem em uma sequência de tarefas para atualizar um sistema operacional nos seguintes cenários:  

-   Para usar uma sequência de tarefas de atualização única que pode funcionar com plataformas x86 e x64. Inclua duas etapas **Baixar Conteúdo do Pacote** no grupo **Preparar Upgrade**. Especificar as condições na guia **Opções** para detectar a arquitetura do cliente e baixar apenas o pacote de atualização do sistema operacional apropriado. Configure cada etapa **Baixar Conteúdo do Pacote** para usar a mesma variável. Use a variável para o caminho de mídia na etapa **Atualizar Sistema Operacional**.  

-   Para baixar um pacote de drivers aplicáveis dinamicamente, use duas etapas **Baixar Conteúdo do Pacote** com condições para detectar o tipo de hardware apropriado para cada pacote de drivers. Configure cada etapa **Baixar Conteúdo do Pacote** para usar a mesma variável. Use a variável para o valor **Conteúdo de teste** na seção Drivers da etapa **Atualizar sistema operacional**.  

> [!NOTE]    
> Quando você implanta uma sequência de tarefas que contém a etapa Baixar Conteúdo do Pacote, não selecione **Baixar todo o conteúdo localmente antes de iniciar a sequência de tarefas** ou **Acessar conteúdo diretamente de um ponto de distribuição** para **Opções de implantação** na página **Pontos de Distribuição** do Assistente de Implantação de Software.  

Esta etapa é executada em um sistema operacional padrão ou no Windows PE. No entanto, a opção para salvar o pacote no cache do cliente do Configuration Manager não tem suporte no WinPE.

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Software** e selecione **Baixar Conteúdo do Pacote** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 Ícone**Selecionar pacote**  
 Clique no ícone para selecionar o pacote que será baixado. Depois de selecionar um pacote, você pode clicar no ícone novamente para escolher outro pacote.  

 **Coloque no seguinte local**  
 Escolha esta opção para salvar o pacote em um dos seguintes locais:  

 -   **Diretório de trabalho da sequência de tarefas**  

 -   **Cache do cliente do Configuration Manager**: use esta opção para armazenar o conteúdo no cache do cliente. Isso permite que o cliente atue como uma origem do cache par para outros clientes de cache par. Para mais informações, confira [Prepare Windows PE peer cache to reduce WAN traffic](../get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md) (Preparar o cache par do Windows PE para reduzir o tráfego da WAN).  

 -    **Caminho personalizado**: com essa opção, o mecanismo de sequência de tarefas primeiro baixa o pacote para o diretório de trabalho da sequência de tarefas e depois o move para o caminho que você especificar. O mecanismo de sequência de tarefas agrega o caminho ao ID do pacote. 
   
**Salvar caminho como uma variável**  
 Você pode salvar o caminho como uma variável que pode ser usada em outra etapa da sequência de tarefas. O Configuration Manager adiciona um sufixo numérico ao nome da variável. Por exemplo, se você especificar uma variável %*mycontent*% como uma variável personalizada, ela será a raiz do local em que a sequência de tarefas armazenará todo o conteúdo referenciado. Esse conteúdo pode conter vários pacotes. Quando você fizer referência à variável, deverá adicionar um sufixo numérico a ela. Por exemplo, para o primeiro pacote, faça referência a %*mycontent01*%. Quando você fizer referência à variável em etapas subsequentes, tais como **Atualizar Sistema Operacional**, use %*mycontent02*% ou %*mycontent03*%, em que o número corresponde à ordem na qual a etapa **Baixar Conteúdo do Pacote** lista os pacotes.  

**Se o download do pacote falhar, continue baixando outros pacotes na lista**  
 Se a sequência de tarefas falhar ao baixar um pacote, ela começará a baixar o próximo pacote na lista.  



##  <a name="BKMK_EnableBitLocker"></a> Habilitar BitLocker  
Use esta etapa para habilitar a criptografia BitLocker em pelo menos duas partições no disco rígido. A primeira partição ativa contém o código de inicialização do Windows. Outra partição contém o sistema operacional. A partição de inicialização deve permanecer descriptografada.  

Use a etapa **Pré-provisionar o BitLocker** para habilitar o BitLocker em uma unidade no Windows PE. Para obter mais informações, consulte a seção [Pré-provisionar o BitLocker](#BKMK_PreProvisionBitLocker).  

> [!NOTE]  
>  A criptografia de unidade de disco BitLocker fornece criptografia de baixo nível do conteúdo de um volume de disco.  

A etapa **Habilitar BitLocker** só é executada em um sistema operacional padrão. Ela não é executada no Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Enable BitLocker Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

Quando você especificar **Somente TPM**, **TPM e chave de inicialização em USB** ou **TPM e PIN**, o TPM (Trusted Platform Module) deverá estar no seguinte estado antes de executar a etapa **Habilitar BitLocker**:  

-   Habilitada  
-   Ativado  
-   Propriedade permitida  
   
Esta etapa conclui qualquer inicialização restante do TPM. As etapas restantes não exigem a presença física ou reinicializações. As etapas de inicialização de TPM restantes são concluídas de modo transparente pela etapa **Habilitar BitLocker**, se necessário:  

-   Criar um par de chave de endosso  
-   Criar valor de autorização do proprietário e caução para o Active Directory, que devem ser estendidos para oferecer suporte a esse valor  
-   Apropriar-se  
-   Crie a chave de raiz de armazenamento ou redefina-a se existir, mas for incompatível  
   
Se você deseja que a sequência de tarefas aguarde a etapa **Habilitar BitLocker** para concluir o processo de criptografia de unidade, selecione a opção **Aguardar**. Se você não selecionar a opção **Aguardar**, o processo de criptografia de unidade ocorrerá em segundo plano. A sequência de tarefas continua imediatamente para a próxima etapa.  

O BitLocker pode ser usado para criptografar várias unidades em um sistema de computador (sistema operacional e unidades de dados). Para criptografar uma unidade de dados, primeiro criptografe a unidade do sistema operacional e conclua o processo de criptografia. Esse requisito existe porque a unidade do sistema operacional armazena os protetores de chave para as unidades de dados. Se você criptografar as unidades do sistema operacional e de dados na mesma sequência de tarefas, selecione a opção **Aguardar** na etapa **Habilitar BitLocker** para a unidade do sistema operacional.  

Se o disco rígido já estiver criptografado, mas o BitLocker estiver desabilitado, a etapa **Habilitar BitLocker** habilitará novamente o protetor de chave e será concluída rapidamente. Nova criptografia da unidade de disco rígida não é necessária neste caso.  

Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Enable BitLocker Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

No editor de sequência de tarefas, clique em **Adicionar**, selecione **Discos** e selecione **Habilitar BitLocker** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Escolher a unidade a ser criptografada**  
 Especifica a unidade para criptografar. Para criptografar a unidade do sistema operacional atual, selecione **Unidade do sistema operacional atual** e configure as seguintes opções para o gerenciamento de chaves:  

-   **Somente TPM**: selecione esta opção para usar somente o TPM (Trusted Platform Module).  

-   **Chave de inicialização somente em USB**: selecione esta opção para usar uma chave de inicialização armazenada em uma unidade flash USB. Quando você seleciona essa opção, o BitLocker bloqueia o processo normal de inicialização até que um dispositivo USB que contém uma chave de inicialização do BitLocker é anexado ao computador.  

-   **TPM e chave de inicialização em USB**: selecione esta opção para usar o TPM e uma chave de inicialização armazenada em uma unidade flash USB. Quando você seleciona essa opção, o BitLocker bloqueia o processo normal de inicialização até que um dispositivo USB que contém uma chave de inicialização do BitLocker é anexado ao computador.  

-   **TPM e PIN**: selecione esta opção para usar o TPM e um PIN (número de identificação pessoal). Quando você seleciona essa opção, o BitLocker bloqueia o processo normal de inicialização até que o usuário forneça o PIN.  
   
Para criptografar uma unidade de dados específicos e não do sistema operacional, selecione **Unidade específica**e selecione a unidade na lista.  

**Escolher onde criar a chave de recuperação**  
 Para especificar o local em que o BitLocker cria a senha de recuperação e fazer caução dela no Active Directory, selecione **No Active Directory**. Se você selecionar essa opção, estenda o Active Directory para o site. O BitLocker pode salvar as informações de recuperação associadas no Active Directory. Selecione **Não criar a chave de recuperação** para não criar uma senha. A criação de uma senha é uma prática recomendada.  

**Aguarde o BitLocker concluir o processo de criptografia de unidade em todas as unidades antes de continuar a execução da sequência de tarefas**  
 Selecione esta opção para permitir que a criptografia de unidade de disco BitLocker seja concluída antes de executar a próxima etapa na sequência de tarefas. Se você selecionar essa opção, todo o volume de disco será criptografado pelo BitLocker antes de o usuário fazer logon computador.  

O processo de criptografia pode levar horas para ser concluído quando um disco rígido grande está sendo criptografado. Não selecionar esta opção permite que a sequência de tarefas continue imediatamente.  



##  <a name="BKMK_FormatandPartitionDisk"></a> Formatar e Particionar Disco  
 Use esta etapa para formatar e particionar um disco especificado no computador de destino.  

> [!IMPORTANT]  
>  Todas as configurações que você especificar para esta etapa se aplicam a um único disco. Para formatar e particionar outro disco no computador de destino, você deve adicionar uma etapa **Formatar e Particionar Disco** adicional à sequência de tarefas.  

 Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Format and Partition Disk Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_FormatPartitionDisk).  

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Discos** e selecione **Formatar e Particionar Disco** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Número do Disco**  
 O número do disco físico a ser formatado. O número é baseado na ordem de enumeração de disco do Windows.  

 **Tipo de Disco**  
 O tipo de disco que é formatado. Há duas opções para selecionar na lista suspensa: 

-   Padrão (MBR) – Registro Mestre de Inicialização
-   GGT – Tabela de partição GUID  

> [!NOTE]  
>  Se você alterar o tipo de disco de **Padrão (MBR)** para **GPT** e o layout da partição contiver uma partição estendida, a sequência de tarefas removerá todas as partições estendidas e lógicas do layout. O editor de sequência de tarefas solicita que você confirme esta ação antes de alterar o tipo de disco.  
   
**Volume**  
 Informações específicas sobre a partição ou volume que a sequência de tarefas cria, incluindo os seguintes atributos:  

-   Name  
-   Espaço restante em disco  
   
Para criar uma nova partição, clique em **Novo** para abrir a caixa de diálogo **Propriedades da partição** . Especifique o tipo e o tamanho da partição, bem como se ela é uma partição de inicialização. Para modificar uma partição existente, clique na partição a ser modificada e no botão Propriedades. Para obter mais informações sobre como configurar partições de disco rígido, consulte os seguintes artigos:  

-   [Como configurar partições de disco rígido baseadas em UEFI/GGT](http://go.microsoft.com/fwlink/?LinkID=272104)  
-   [Como configurar partições de disco rígido baseado em BIOS/MBR](http://go.microsoft.com/fwlink/?LinkId=272105)  

Para excluir uma partição, selecione a partição a ser excluída e clique em **Excluir**.  



##  <a name="BKMK_InstallApplication"></a> Instalar Aplicativo  
Esta etapa instala os aplicativos especificados, ou então um conjunto de aplicativos definidos por uma lista dinâmica de variáveis de sequência de tarefas. Quando essa etapa é executada, a instalação do aplicativo começa imediatamente sem esperar que um intervalo de sondagem de política.  

Os aplicativos que são instalados devem atender aos seguintes critérios:  

-   O aplicativo deve ser um tipo de implantação do Windows Installer ou do Instalador de script. Não há suporte para tipos de implantação do pacote do aplicativo Windows (arquivo .appx).  

-   Ele deve executar sob a conta sistema local e não a conta de usuário.  

-   Ele não deve interagir com a área de trabalho. O programa deve ser executado silenciosamente ou em um modo autônomo.  

-   Ele não deve iniciar uma reinicialização por conta própria. O aplicativo deve solicitar uma reinicialização, usando o código de reinicialização padrão, um código de saída 3010. Este comportamento garante que a etapa de sequência de tarefas manipule corretamente a reinicialização. Se o aplicativo retornar um código de saída 3010, o mecanismo subjacente de sequência de tarefas executará a reinicialização. Após a reinicialização, a sequência de tarefas continua automaticamente.  

Quando a etapa **Instalar Aplicativo** é executada, o aplicativo verifica a aplicabilidade das regras de requisito e o método de detecção nos respectivos tipos de implantação. Com base nos resultados dessa verificação, o aplicativo instala o tipo de implantação aplicável. Se um tipo de implantação contém dependências, o tipo de implantação dependente é avaliado e instalado como parte da etapa de aplicativo de instalação. Dependências de aplicativos não têm suporte para mídia autônoma.  

> [!NOTE]  
>  Para instalar um aplicativo que substitui outro, os arquivos de conteúdo para o aplicativo substituído devem estar disponíveis. Caso contrário, essa etapa de sequência de tarefas falhará. Por exemplo, o Microsoft Visio 2010 é instalado em um cliente ou em uma imagem capturada. Quando a etapa **Instalar Aplicativo** instala o Microsoft Visio 2013, os arquivos de conteúdo para o Microsoft Visio 2010 (aplicativo substituído) devem estar disponíveis em um ponto de distribuição. Se o Microsoft Visio não é instalado em um cliente ou imagem capturada, a sequência de tarefas instala o Microsoft Visio 2013 sem verificar os arquivos de conteúdo do Microsoft Visio 2010.  

> [!NOTE]
> Se o cliente falha ao recuperar a lista de pontos de gerenciamento dos serviços de localização, use as variáveis internas SMSTSMPListRequestTimeoutEnabled e SMSTSMPListRequestTimeout para habilitar e especificar quantos milissegundos uma sequência de tarefas espera antes de tentar instalar novamente uma atualização de software ou de aplicativo. Para obter mais informações, consulte [Variáveis internas da sequência de tarefas](task-sequence-built-in-variables.md).

 Essa etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE.  

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Software** e selecione **Instalar Aplicativo** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Instalar os seguintes aplicativos**  
 A sequência de tarefas instala esses aplicativos na ordem especificada.  

 O Configuration Manager filtra qualquer aplicativo desabilitado ou aplicativos com as seguintes configurações:  

-   Somente quando um usuário tiver efetuado logon  
-   Executar com direitos de usuário  

Esses aplicativos não aparecem na caixa de diálogo **Selecione o aplicativo a ser instalado**.
  
**Instalar aplicativos de acordo com a lista de variáveis dinâmicas**  
A sequência de tarefas instala os aplicativos que usam este nome de variável de base. O nome de variável de base é para um conjunto de variáveis de sequência de tarefas definido para uma coleção ou computador. Essas variáveis especificam os aplicativos que a sequência de tarefas instala para essa coleção ou computador. Cada nome de variável consiste em seu nome de base comum e um sufixo numérico, começando com 01. O valor de cada variável deve conter o nome do aplicativo e nada mais.  

Para que a sequência de tarefas instale aplicativos usando uma lista de variáveis dinâmicas, habilite a seguinte configuração na guia **Geral** da caixa de diálogo **Propriedades** do aplicativo: **Permitir que este aplicativo seja instalado na ação de sequência de tarefas Instalar aplicativo em vez de implantar manualmente**  

> [!NOTE]  
>  Você não pode instalar aplicativos usando uma lista dinâmica de variável para implantações de mídia autônoma.  

Por exemplo, para instalar um único aplicativo usando uma variável de sequência de tarefas chamada AA01, especifique a seguinte variável:  

|Nome da variável|Valor da variável|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

Para instalar dois aplicativos, você deve especificar as seguintes variáveis:  

|Nome da variável|Valor da variável|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

As condições a seguir afetam os aplicativos instalados pela sequência de tarefas:  

-   Se o valor de uma variável contém todas as informações que não seja o nome do aplicativo. A sequência de tarefas não instala o aplicativo e prossegue.  

-   Se a sequência de tarefas não encontrar uma variável com o nome de base especificado e o sufixo "01", a sequência de tarefas não instalará nenhum aplicativo. 
    
> [!Important]  
> Esses valores diferenciam maiúsculas de minúsculas. Por exemplo, "instalar" é diferente de "Instalar". Caso precise alterar o valor, o Editor de Sequência de Tarefas não detecta alterações de maiúsculas e minúsculas. Você deve fazer outra edição em simultâneo; por exemplo, modificar a descrição da etapa.<!--509714-->   

   
**If an application fails, continue installing other applications in the list (Se um aplicativo falhar, continue a instalar outros aplicativos na lista)**  
 Essa configuração especifica que a etapa continuará quando a instalação de um aplicativo individual falhar. Se você especificar essa configuração, a sequência de tarefas continuará, independentemente de eventuais erros de instalação. Se você não especificar essa configuração e a instalação falhar, a etapa terminará imediatamente.  

### <a name="options"></a>Opções
 > [!NOTE] 
 > Quando você seleciona **Continuar em caso de erro** na guia **Opções** dessa etapa, a sequência de tarefas continua quando um aplicativo falha ao instalar. Quando você não habilitar essa opção, a sequência de tarefas falhará e não instalará os aplicativos restantes.  
 
Além das opções padrão, defina as seguintes configurações adicionais na guia **Opções** dessa etapa da sequência de tarefas:  

-   **Tente executar esta etapa novamente se o computador reiniciar inesperadamente**  
    Se uma das instalações do aplicativo reiniciar o computador inesperadamente, tente realizar essa etapa novamente. A etapa habilita essa configuração por padrão com duas novas tentativas. Você pode especificar de uma a cinco novas tentativas.  



##  <a name="BKMK_InstallPackage"></a> Instalar Pacote
Use essa etapa para instalar um pacote de software como parte da sequência de tarefas. Quando essa etapa é executada, a instalação começa imediatamente sem esperar que um intervalo de sondagem de política.  

O pacote deve atender aos seguintes critérios:  

-   Ele deve executar sob a conta sistema local e não uma conta de usuário.  

-   Ele não deve interagir com a área de trabalho. O programa deve ser executado silenciosamente ou em um modo autônomo.  

-   Ele não deve iniciar uma reinicialização por conta própria. O software deve solicitar uma reinicialização, usando o código de reinicialização padrão, um código de saída 3010. Este comportamento garante que a etapa de sequência de tarefas manipule adequadamente a reinicialização. Se o software retornar um código de saída 3010, o mecanismo subjacente de sequência de tarefas reiniciará o computador. Após a reinicialização, a sequência de tarefas continua automaticamente.  

Programas que usam a opção **Executar outro programa primeiro** para instalar um programa dependente não são suportados ao implantar um sistema operacional. Se você habilitar a opção de pacote **Executar outro programa primeiro** e o programa dependente já tiver executado no computador de destino, o programa dependente será executado e a sequência de tarefas continuará. No entanto, se o programa dependente ainda não tiver sido executado no computador de destino, a etapa de sequência de tarefas falhará.  

> [!NOTE]  
>  O site de administração central não tem as políticas de configuração de cliente necessárias para habilitar o agente de distribuição de software durante a sequência de tarefas. Quando você cria mídia autônoma para uma sequência de tarefas no site de administração central, e a sequência de tarefas inclui uma etapa **Instalar pacote** , o seguinte erro pode aparecer no arquivo CreateTsMedia.log:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>   
>  Para mídia autônoma que inclui uma etapa **Instalar Pacote**, crie a mídia autônoma em um site primário que tem o agente de distribuição de software habilitado. Como alternativa, adicione uma etapa **Executar Linha de Comando** após a etapa **Instalar o Windows e o ConfigMgr** e antes da primeira etapa **Instalar o Pacote**. A etapa **Executar Linha de Comando** executa como um comando WMIC para habilitar o agente de distribuição de software antes da primeira etapa **Instalar Pacote**. Use o seguinte comando na etapa **Executar Linha de Comando**:  
>   
>  **Linha de Comando**: `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
>   
>  Para mais informações sobre como criar mídia autônoma, confira [Create stand-alone media](../deploy-use/create-stand-alone-media.md) (Criar mídia autônoma).  

Essa etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE.  

No editor de sequência de tarefas, clique em **Adicionar**, selecione **Software** e selecione **Instalar Pacote** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Instalar um pacote de software único**  
 Essa configuração especifica um pacote de software do Configuration Manager. A etapa aguarda até a instalação ser concluída.  

 **Instalar pacotes de software de acordo com a lista de variáveis dinâmicas**  
 A sequência de tarefas instala os pacotes que usam este nome de variável de base. O nome de variável de base é para um conjunto de variáveis de sequência de tarefas definido para uma coleção ou computador. Essas variáveis especificam os pacotes que a sequência de tarefas instala para essa coleção ou computador. Cada nome de variável consiste em seu nome de base comum e um sufixo numérico, começando com 001. O valor de cada variável deve conter uma ID de pacote e o nome do software separados por dois-pontos.  

 Para que a sequência de tarefas instale o software usando uma lista de variáveis dinâmicas, habilite a seguinte configuração na guia **Avançado** das **Propriedades** do pacote: **Permitir que este programa seja instalado da sequência de tarefas de Pacote de Instalação sem ser implantado**  

> [!NOTE]  
>  Você não pode instalar pacotes de software usando uma lista dinâmica de variável para implantações de mídia autônoma.  

 Por exemplo, para instalar um único pacote de software usando uma variável de sequência de tarefas chamada AA001, especifique a seguinte variável:  

|Nome da variável|Valor da variável|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

 Para instalar três pacotes de software, você deve especificar as seguintes variáveis:  

|Nome da variável|Valor da variável|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|CEN00107:Install Silent|  
|AA003|CEN00031:Install|  

 As condições a seguir afetam os pacotes instalados pela sequência de tarefas:  

-   Se você não criar o valor de uma variável no formato correto ou não especificar um nome e uma ID do pacote válidos, a instalação do software falhará.  

-   Se a ID do pacote contiver caracteres minúsculos, a instalação do software falhará.  

-   Se a sequência de tarefas não encontrar uma variável com o nome de base especificado e o sufixo "001", a sequência de tarefas não instalará nenhum pacote. A sequência de tarefas continua.  
    
> [!Important]  
> Esses valores diferenciam maiúsculas de minúsculas. Por exemplo, "instalar" é diferente de "Instalar". Caso precise alterar o valor, o Editor de Sequência de Tarefas não detecta alterações de maiúsculas e minúsculas. Você deve fazer outra edição em simultâneo; por exemplo, modificar a descrição da etapa.<!--509714-->   

   
**Se a instalação de um pacote de software falhar, continue instalando os outros pacotes da lista**  
 Essa configuração especifica que a etapa continuará se a instalação de um pacote de software individual falhar. Se você especificar essa configuração, a sequência de tarefas continuará, independentemente de eventuais erros de instalação. Se você não especificar essa configuração e a instalação falhar, a etapa terminará imediatamente.  



##  <a name="BKMK_InstallSoftwareUpdates"></a> Instalar Atualizações de Software  
Use esta etapa para instalar as atualizações de software no computador de destino. O computador de destino não é avaliado para atualizações de software aplicáveis até que essa etapa de sequência de tarefas seja executada. Nesse momento, o computador de destino é avaliado para atualizações de software como qualquer outro cliente do Configuration Manager. Para que esta etapa instale atualizações de software, primeiro você deve implantar as atualizações em uma coleção da qual o computador de destino é um membro.  
>  [!IMPORTANT]
> Uma prática recomendada para um desempenho ideal é instalar a versão mais recente do Windows Update Agent. 
>* Para o Windows 7, consulte na [Base de Dados de Conhecimento o artigo 3161647](https://support.microsoft.com/kb/3161647).
>* Para o Windows 8, consulte na [Base de Dados de Conhecimento o artigo 3163023](https://support.microsoft.com/kb/3163023).

 Essa etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE. Para obter informações sobre variáveis de sequência de tarefas para esta ação da sequência de tarefas, veja [Install Software Updates Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_InstallSoftwareUpdates).

 > [!NOTE]
 > Se o cliente falha ao recuperar a lista de pontos de gerenciamento dos serviços de localização, use as variáveis internas SMSTSMPListRequestTimeoutEnabled e SMSTSMPListRequestTimeout para habilitar e especificar quantos milissegundos uma sequência de tarefas espera antes de tentar instalar novamente uma atualização de software ou de aplicativo. Para obter mais informações, consulte [Variáveis internas da sequência de tarefas](task-sequence-built-in-variables.md).

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Software** e selecione **Instalar Atualizações de Software** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Necessárias para instalação – somente atualizações de software obrigatórias**  
 Selecione esta opção para instalar todas as atualizações de software obrigatórias com prazos de instalação definidos pelo administrador.  

 **Disponíveis para instalação – todas as atualizações de software**  
 Selecione esta opção para instalar todas as atualizações de software disponíveis. Primeiro, você deve implantar essas atualizações em uma coleção da qual o computador é membro. Uma sequência de tarefas instala todas as atualizações de software disponíveis nos computadores de destino.  

 **Avaliar as atualizações de software dos resultados da varredura em cache**  
 Por padrão, a sequência de tarefas usa os resultados da varredura em cache do Windows Update Agent. Desmarque a caixa de seleção para instruir o Windows Update Agent a baixar o catálogo mais recente do ponto de atualização de software. Escolha essa opção ao usar uma sequência de tarefas para [capturar e criar uma imagem do sistema operacional](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md). Neste cenário é provável que ocorra um grande número de atualizações de software. Muitas dessas atualizações terão dependências, por exemplo, instalar X antes de Y aparece como aplicável. Ao desmarcar essa configuração e implantar a sequência de tarefas em muitos clientes, todos eles se conectam ao ponto de atualização de software ao mesmo tempo. Esse comportamento resulta em problemas de desempenho durante o processo e o download do catálogo. A prática recomendada é a configuração padrão para usar os resultados da verificação armazenados em cache. 

A variável de sequência de tarefas SMSTSSoftwareUpdateScanTimeout controla o tempo limite de verificação de atualizações de software durante essa etapa. O valor padrão é 30 minutos. Para obter mais informações, consulte [Variáveis internas da sequência de tarefas](task-sequence-built-in-variables.md).

### <a name="options"></a>Opções   
 Além das opções padrão, defina as seguintes configurações adicionais na guia **Opções** dessa etapa da sequência de tarefas:  

-   **Tente executar esta etapa novamente se o computador reiniciar inesperadamente**  
    Se uma das atualizações reiniciar o computador inesperadamente, tente realizar essa etapa novamente. A etapa habilita essa configuração por padrão com duas novas tentativas. Você pode especificar de uma a cinco novas tentativas.  

    > [!NOTE]
    > Configure a variável SMSTSWaitForSecondReboot para especificar por quantos segundos a sequência de tarefas fica em pausa depois que o computador é reiniciado nesse cenário. Para obter mais informações, consulte [Variáveis internas da sequência de tarefas](task-sequence-built-in-variables.md).



##  <a name="BKMK_JoinDomainorWorkgroup"></a> Ingressar no Domínio ou Grupo de Trabalho  
 Use essa etapa para adicionar o computador de destino a um grupo de trabalho ou domínio.  

 Essa etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE. Para obter informações sobre variáveis de sequência de tarefas para esta ação da sequência de tarefas, veja [Join Domain or Workgroup Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_JoinDomainWorkgroup).  

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e selecione **Ingressar no Domínio ou Grupo de Trabalho** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Ingressar no grupo de trabalho**  
 Selecione esta opção para fazer o computador de destino ingressar no grupo de trabalho especificado. Se o computador atualmente é um membro de um domínio, selecionar esta opção faz com que o computador seja reinicializado.  

 **Ingressar em um domínio**  
 Selecione esta opção para fazer o computador de destino ingressar no domínio especificado.  

 Opcionalmente, digite ou navegue para uma unidade organizacional (UO) no domínio especificado para ingressar o computador. Se o computador atualmente é um membro de algum outro domínio ou grupo de trabalho, essa opção causa a reinicialização do computador. Se o computador já é um membro de outra UO, a Instalação do Windows ignora esta configuração, já que o Active Directory Domain Services não permite alterar a unidade Organizacional por esse método.  

 **Insira a conta que tem permissão para ingressar no domínio**  
 Clique em **Definir** para inserir um nome de usuário e senha para uma conta com permissões para ingressar no domínio. Insira a conta no formato: *Domínio\conta*  



## <a name="BKMK_PrepareConfigMgrClientforCapture"></a> Preparar ConfigMgr Client for Capture  
Use esta etapa para remover ou configurar o cliente do Configuration Manager no computador de referência. Essa ação prepara o computador para captura como parte do processo de geração de imagens.

Começando no Configuration Manager versão 1610, a etapa **Preparar o Cliente do ConfigMgr** remove completamente o cliente do Configuration Manager, em vez de remover apenas informações importantes. Quando a sequência de tarefas implantar a imagem capturada do sistema operacional, ela instalará um novo cliente do Configuration Manager a cada vez.  

> [!Note]  
>  O mecanismo da sequência de tarefas só remove o cliente durante a sequência de tarefas **Compilar e capturar uma imagem do sistema operacional de referência**. O mecanismo de sequência de tarefas não remove o cliente durante outros métodos de captura, tais como mídia de captura ou uma sequência de tarefas personalizadas.

Antes do Configuration Manager versão 1610, esta etapa executa as seguintes tarefas:  

-   Remove a seção de propriedades de configuração de cliente do arquivo smscfg.ini no diretório do Windows. Essas propriedades incluem informações específicas do cliente incluindo o GUID do Configuration Manager e outros identificadores de cliente.  

-   Exclui todos os certificados do computador do SMS ou do Configuration Manager.  

-   Exclui o cache do cliente do Configuration Manager.  

-   Apaga a variável de site atribuída ao cliente do Configuration Manager.  

-   Exclui todas as políticas locais do Configuration Manager.  

-   Remove a chave raiz confiável para o cliente do Configuration Manager.  

Essa etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE.  

No editor de sequência de tarefas, clique em **Adicionar**, selecione **Imagens** e selecione **Preparar o Cliente do ConfigMgr para Captura** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Essa etapa não requer nenhuma configuração na guia **Propriedades**.



##  <a name="BKMK_PrepareWindowsforCapture"></a> Preparar Windows para Captura  
 Use essa etapa para especificar as opções do Sysprep ao capturar uma imagem do sistema operacional no computador de referência. Esta ação de sequência de tarefas executa o Sysprep e reinicia o computador na imagem de inicialização do Windows PE especificado para a sequência de tarefas. Essa ação falhará se o computador de referência estiver ingressado em um domínio.  

 Essa etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE. Para obter informações sobre variáveis de sequência de tarefas para esta ação da sequência de tarefas, veja [Prepare Windows for Capture Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_PrepareWindowsCapture).  

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Imagens** e selecione **Preparar o Windows para Captura** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Construir lista de drivers de armazenamento em massa automaticamente**  
 Selecione esta opção para fazer com que o Sysprep crie automaticamente uma lista de drivers de armazenamento em massa do computador de referência. Essa opção habilita a opção de criar drivers de armazenamento em massa no arquivo sysprep.inf no computador de referência. Para obter mais informações sobre essa configuração, consulte a documentação do Sysprep.  

 **Não redefinir sinalizador de ativação**  
 Selecione esta opção para impedir que o Sysprep redefina o sinalizador de ativação do produto.  



##  <a name="BKMK_PreProvisionBitLocker"></a> Pré-provisionar o BitLocker  
 Use esta etapa para habilitar o BitLocker em uma unidade durante a execução do Windows PE. Apenas o espaço em disco usado é criptografado e, portanto, os tempos de criptografia são muito mais rápidos. Aplique as opções de gerenciamento de chaves usando a etapa da sequência de tarefas do [Habilitar BitLocker](#BKMK_EnableBitLocker) depois que o sistema operacional for instalado. Esta etapa é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão.  

> [!IMPORTANT]  
>  Pré-provisionar o BitLocker requer no mínimo o Windows 7. O computador também deve conter um TPM (Trusted Platform Module) compatível e habilitado.  

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Discos** e selecione **Pré-provisionar BitLocker** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Aplicar BitLocker à unidade especificada**  
 Especificar a unidade para a qual você deseja habilitar o BitLocker. Apenas o espaço usado em disco está criptografado.  

 **Ignorar esta etapa para computadores que não têm um TPM ou quando o TPM não está habilitado**  
 Selecione esta opção para ignorar a criptografia de unidade em um computador que não tem um TPM compatível ou habilitado conforme necessário. Por exemplo, use esta opção ao implantar um sistema operacional em uma máquina virtual.  



##  <a name="BKMK_ReleaseStateStore"></a> Liberar Armazenamento de Estado  
 Use esta etapa para notificar o ponto de migração de estado de que a ação de captura ou restauração foi concluída. Use essa etapa junto com as etapas **Solicitar Repositório de Estado**, **Capturar Estado do Usuário** e **Restaurar Estado do Usuário**. Você pode usar estas etapas para migrar dados de estado do usuário usando um ponto de migração de estado e a USMT (Ferramenta de Migração do Usuário).  

 Para mais informações sobre como gerenciar o estado do usuário ao implantar sistemas operacionais, confira [Gerenciar o estado do usuário](../get-started/manage-user-state.md).  

 Se você usar a etapa **Solicitar Repositório de Estado** para solicitar acesso a um ponto de migração de estado para *capturar* o estado do usuário, essa etapa notificará o ponto de migração de estado de que o processo de captura foi concluído. O ponto de migração de estado marca então os dados de estado do usuário como disponíveis para restauração. O ponto de migração de estado define as permissões de controle de acesso a dados de estado do usuário, de modo que somente o computador realizando a restauração tem acesso somente leitura.  

 Se você usar a etapa **Solicitar Repositório de Estado** para solicitar acesso a um ponto de migração de estado para *restaurar* o estado do usuário, essa etapa notificará o ponto de migração de estado de que o processo de restauração foi concluído. O ponto de migração de estado ativa então as respectivas definições de retenção de dados configuradas.  

> [!IMPORTANT]  
>  Uma prática recomendada é definir a opção **Continuar em Caso de Erro** para todas as etapas entre as etapas **Solicitar Repositório de Estado** e **Liberar Repositório de Estado**. Cada etapa **Solicitar Repositório de Estado** deve ter uma etapa **Liberar Repositório de Estado** correspondente.  

 Essa etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE. Para obter informações sobre variáveis de sequência de tarefas para esta ação da sequência de tarefas, veja [Release State Store Sequence Action Variables](task-sequence-action-variables.md#BKMK_ReleaseStateStore).  

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Estado de Usuário** e selecione **Liberar Repositório de Estado** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Essa etapa não requer nenhuma configuração na guia **Propriedades**.



##  <a name="BKMK_RequestStateStore"></a> Solicitar Armazenamento de Estado  
 Use essa etapa para solicitar acesso a um ponto de migração de estado durante a captura ou a restauração de estado.  

 Para mais informações sobre como gerenciar o estado do usuário ao implantar sistemas operacionais, confira [Gerenciar o estado do usuário](../get-started/manage-user-state.md).  

 Use essa etapa junto com as etapas **Solicitar Repositório de Estado**, **Liberar Estado do Usuário** e **Restaurar Estado do Usuário**. Você pode usar estas etapas para migrar o estado do computador usando um ponto de migração de estado e a USMT (Ferramenta de Migração do Usuário).  

> [!NOTE]  
>  Ao criar um novo ponto de migração de estado, o armazenamento de estado do usuário permanece não disponível por até uma hora. Para agilizar a disponibilidade, ajuste quaisquer configurações de propriedade no ponto de migração do estado para disparar uma atualização de arquivo de controle do site.  

 Essa etapa de sequência de tarefas é executada em um sistema operacional padrão e no Windows PE para USMT offline. Para obter informações sobre as variáveis de sequência de tarefas para esta ação da sequência de tarefas, veja [Request State Store Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RequestState).  

No editor de sequência de tarefas, clique em **Adicionar**, selecione **Estado de Usuário** e selecione **Solicitar Repositório de Estado** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Capturar estado do computador**  
 Localize um ponto de migração de estado que atenda aos requisitos mínimos definidos nas configurações de ponto de migração de estado. Por exemplo, **Número máximo de clientes** e **Quantidade mínima de espaço livre em disco**. Essa opção não garante que exista espaço em disco disponível no momento da migração de estado. Esta opção solicita acesso ao ponto de migração de estado para capturar o estado do usuário e configurações de um computador.  

 Se o site do Configuration Manager tem vários pontos de migração de estado ativos, esta etapa encontra um ponto de migração de estado com espaço em disco disponível. A sequência de tarefas consulta o ponto de gerenciamento para obter uma lista de pontos de migração de estado e avalia cada um até encontrar um que atenda aos requisitos mínimos.  

 **Restaurar estado de outro computador**  
 Solicite acesso a um ponto de migração de estado para restaurar as configurações e o estado do usuário capturados anteriormente para um computador de destino.  

 Se há vários pontos de migração de estado, essa etapa localiza o ponto de migração de estado que tem o estado do computador de destino.  

 **Número de tentativas**  
 O número de vezes que essa etapa tenta localizar um ponto de migração de estado apropriado antes de falhar.  

 **Atraso na repetição (em segundos)**  
 A quantidade de tempo em segundos que a etapa de sequência de tarefas espera entre as novas tentativas.  

 **Se a conta de computador não conseguir se conectar a um armazenamento de estado, use a conta de acesso à rede.**  
 Se a sequência de tarefas não puder acessar o ponto de migração de estado usando a conta de computador, ela usará as credenciais de conta de acesso de rede para se conectar. Essa opção é menos segura porque outros computadores poderiam usar a conta de acesso de rede para acessar o estado armazenado. Essa opção poderá ser necessária se o computador de destino não estiver ingressado no domínio.  



##  <a name="BKMK_RestartComputer"></a> Reiniciar Computador  
 Use essa etapa para reiniciar o computador que executa a sequência de tarefas. Após a reinicialização, o computador continua automaticamente com a próxima etapa na sequência de tarefas.  

 Esta etapa pode ser executada em um sistema operacional padrão ou no Windows PE. Para mais informações sobre as variáveis de sequência de tarefas para esta ação da sequência de tarefas, confira [Restart computer task sequence action variables](task-sequence-action-variables.md#BKMK_RestartComputer) (Reiniciar as variáveis de ação da sequência de tarefas do computador).  

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e selecione **Reiniciar Computador** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **A imagem de inicialização atribuída a esta sequência de tarefas**  
 Selecione esta opção para o computador de destino usar a imagem de inicialização atribuída à sequência de tarefas. A sequência de tarefas usa a imagem de inicialização para executar as etapas subsequentes no Windows PE.  

 **Sistema operacional padrão instalado atualmente**  
 Selecione esta opção para o computador de destino ser reinicializado no sistema operacional instalado.  

 **Notificar usuário antes de reiniciar**  
 Selecione esta opção para exibir uma notificação ao usuário antes que computador de destino seja reiniciado. A etapa seleciona esta opção, por padrão.  

 **Mensagem de notificação**  
 Digite uma mensagem de notificação a ser exibida ao usuário antes da reinicialização do computador de destino.  

 **Tempo limite de exibição da mensagem**  
 Especifique a quantidade de tempo em segundos antes do computador de destino ser reiniciado. O padrão é 60 segundos.  



##  <a name="BKMK_RestoreUserState"></a> Restaurar Estado do Usuário  
 Use essa etapa para iniciar o USMT (Ferramenta de Migração do Usuário) para restaurar o estado do usuário e configurações para o computador de destino. Use essa etapa junto com a etapa **Capturar Estado do Usuário**.  

 Para mais informações sobre como gerenciar o estado do usuário ao implantar sistemas operacionais, confira [Gerenciar o estado do usuário](../get-started/manage-user-state.md).  

 Use essa etapa com as etapas **Solicitar Repositório de Estado** e **Liberar Repositório de Estado** para salvar ou restaurar as configurações de estado com um ponto de migração de estado. Com o USMT 3.0 e superior, essa opção sempre criptografa o armazenamento de estado do USMT usando uma chave de criptografia geradas e gerenciadas por Configuration Manager.  

 A etapa **Restaurar Estado do Usuário** fornece controle sobre um subconjunto limitado das opções da USMT mais usadas. Especifique opções de linha de comando adicionais com a variável de sequência de tarefas OSDMigrateAdditionalRestoreOptions.  

> [!IMPORTANT]  
>  Se você está usando essa etapa para uma finalidade não relacionada a um cenário de implantação de sistema operacional, adicione a etapa [Reiniciar Computador](#BKMK_RestartComputer) imediatamente após a etapa **Restaurar Estado do Usuário**.  

 Esta etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE. Para obter informações sobre as variáveis de sequência de tarefas para esta ação da sequência de tarefas, veja [Restore User State Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RestoreUserState).  

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Estado de Usuário** e selecione **Restaurar Estado de Usuário** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Pacote da ferramenta de migração do usuário**  
 Especifique o pacote que contém a versão da USMT a ser usada por esta etapa. Este pacote não exige um programa. Quando a etapa é executada, a sequência de tarefas usa a versão da USMT no pacote especificado. Especifique um pacote que contém a versão de 32 bits ou 64 bits do USMT. A arquitetura da USMT varia de acordo com a arquitetura do sistema operacional do qual a sequência de tarefas está restaurando o estado. 

 **Restaurar todos os perfis de usuários capturados com as opções padrão**  
 Restaura os perfis de usuário com as opções padrão. Para personalizar as opções a serem restauradas pela USMT, selecione **Personalizar captura de perfil do usuário**.  

 **Personalizar o modo como os perfis de usuário são restaurados**  
 Permite que você personalize os arquivos que você deseja restaurar o computador de destino. Clique em **Arquivos** para especificar os arquivos de configuração do pacote do USMT que deseja usar para restaurar os perfis de usuário. Para adicionar um arquivo de configuração, digite o nome do arquivo na caixa **Nome do arquivo** e clique em **Adicionar**. O painel de arquivos lista os arquivos de configuração usados pela USMT. O arquivo .xml que você especifica define qual arquivo de usuário é restaurado pela USMT.  

 **Restaurar perfis de usuário do computador local**  
 Restaura os perfis de usuário do computador local. Esses perfis não são para usuários do domínio. Você precisa atribuir novas senhas às contas de usuário local restauradas. A USMT não é capaz de migrar as senhas originais. Digite a senha nova na caixa **Senha** e confirme a senha em **Confirmar senha** .  

 **Continuar, se alguns arquivos não forem restaurados**  
 Continuará a restauração das configurações e estado do usuário, mesmo se a USMT não puder restaurar alguns arquivos. Essa etapa habilita esta opção por padrão. Se você desabilitar essa opção e a USMT encontrar erros durante a restauração de arquivos, essa etapa falhará imediatamente. A USMT não restaura todos os arquivos.   

 **Habilitar log detalhado**  
 Habilite esta opção para gerar informações de arquivo de log mais detalhadas. Durante a restauração de estado, a sequência de tarefas gera por padrão o Loadstate.log na pasta de log de sequência de tarefas \windows\system32\ccm\logs.  



##  <a name="BKMK_RunCommandLine"></a> Executar Linha de Comando  
 Use essa etapa para executar a linha de comando especificada.  

 Esta etapa pode ser executada em um sistema operacional padrão ou no Windows PE. Para obter informações sobre variáveis de sequência de tarefas para esta ação da sequência de tarefas, veja [Run Command Line Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RunCommand).  

 No editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e selecione **Executar Linha de Comando** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Linha de comando**  
 Especifica a linha de comando que é executada. Esse campo é obrigatório. A inclusão das extensões no nome de arquivo é uma prática recomendada, por exemplo, .vbs e .exe. Inclua todos os arquivos de configurações necessários, as opções de linha de comando ou opções.  

 Se o nome do arquivo não tiver uma extensão de nome de arquivo especificada, o Configuration Manager tentará usar .com, .exe, e.bat. Se o nome do arquivo tiver uma extensão que não é um executável, o Configuration Manager tentará aplicar uma associação local. Por exemplo, se a linha de comando for readme.gif, o Configuration Manager iniciará o aplicativo especificado no computador de destino para abrir arquivos .gif.  

 Exemplos:  

 `setup.exe /a`  

 `cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

> [!NOTE]  
>  Para executar com êxito, preceda as ações de linha de comando com o comando **cmd.exe /c**. Exemplos dessas ações incluem comandos de cópia, redirecionamento de saída e piping.  

 **Desabilitar o redirecionamento de sistema de arquivos de 64 bits**  
 Sistemas operacionais de 64 bits usam o redirecionador de sistema de arquivos WOW64 por padrão para executar linhas de comando. Esse comportamento é para encontrar corretamente versões de 32 bits das bibliotecas e dos executáveis do sistema operacional. Selecione esta opção para desabilitar o uso do redirecionador de sistema de arquivos WOW64. O Windows executa o comando usando versões de 64 bits nativas de bibliotecas e executáveis do sistema operacional. Esta opção não terá nenhum efeito ao executar em um sistema operacional de 32 bits.  

 **Iniciar em**  
 Especifica a pasta do executável do programa, até 127 caracteres. Essa pasta pode ser um caminho absoluto no computador de destino ou um caminho relativo à pasta do ponto de distribuição que contém os arquivos de instalação. Esse campo é opcional.  

 Exemplos:  

 **c:\officexp**  

 **i386**  

> [!NOTE]  
>  O botão **Procurar** procura arquivos e pastas no computador local. Qualquer coisa que você selecionar deverá existir no computador de destino no mesmo local e com os mesmos nomes de pasta e de arquivo.  

 **Pacote**  
 Quando você especificar arquivos ou programas na linha de comando que ainda não estão presentes no computador de destino, selecione essa opção para especificar o pacote do Configuration Manager que contém os arquivos apropriados. Este pacote não exige um programa. Esta opção não é necessária se os arquivos especificados existirem no computador de destino.  

 **Tempo limite**  
 Especifica um valor que representa quanto tempo o Configuration Manager permite para a execução da linha de comando. Esse valor pode ser de 1 a 999 minutos. O valor padrão é 15 minutos.  

 Essa opção é desabilitada por padrão.  

> [!IMPORTANT]  
>  Se você inserir um valor que não permita tempo suficiente para o comando especificado ser concluído com êxito, a etapa atual falhará. Toda a sequência de tarefas inteira poderá falhar dependendo de outras configurações de controle. Se o tempo limite expirar, o Configuration Manager encerrará o processo de linha de comando.  

 **Executar esta etapa usando a seguinte conta**  
 Especifica que a linha de comando é executada como uma conta de usuário do Windows diferente da conta sistema local.  

> [!NOTE]  
>  Para executar comandos ou scripts simples com outra conta depois de instalar o sistema operacional, você deve primeiro adicionar a conta ao computador. Além disso, você deve restaurar o perfil de conta de usuário do Windows para executar programas mais complexos, como um Windows Installer.  

 **Conta**  
 Especifica a conta de usuário do Windows usada por essa etapa para execução da linha de comando. A linha de comando é executada com as permissões da conta especificada. Clique em **Definir** para especificar o usuário local ou a conta de domínio.  

> [!IMPORTANT]  
>  Se esta etapa especifica uma conta de usuário e é executada no Windows PE, a ação falha. Você não pode ingressar o Windows PE em um domínio. O arquivo smsts.log registra essa falha.  



##  <a name="BKMK_RunPowerShellScript"></a> Executar Script do PowerShell  
 Use essa etapa para executar o script do PowerShell especificado.  

 Esta etapa pode ser executada em um sistema operacional padrão ou no Windows PE. Para executar esta etapa no Windows PE, o PowerShell deve ser habilitado na imagem de inicialização. Você pode habilitar o Windows PowerShell (WinPE-PowerShell) na guia **Componentes opcionais** nas propriedades da imagem de inicialização. Para mais informações sobre como modificar uma imagem de inicialização, confira [Manage boot images](../get-started/manage-boot-images.md) (Gerenciar imagens de inicialização).  

> [!NOTE]  
>  O PowerShell não é habilitado por padrão nos sistemas operacionais Windows Embedded.  

No editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e selecione **Executar Script do PowerShell** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Pacote**  
 Especifique o pacote do Configuration Manager que contém o script do PowerShell. Um pacote pode conter vários scripts do PowerShell.  

 **Nome do script**  
 Especifica o nome do script do PowerShell para executar. Esse campo é obrigatório.  

 **Parâmetros**  
 Especifica os parâmetros passados para o script do Windows PowerShell. Esses parâmetros são os mesmos que os parâmetros do script do Windows PowerShell na linha de comando.  

> [!IMPORTANT]  
>  Forneça parâmetros consumidos pelo script, não pela linha de comando do Windows PowerShell.  
>   
>  O exemplo a seguir contém parâmetros válidos:  
>   
>  `-MyParameter1 MyValue1 -MyParameter2 MyValue2`  
>   
>  O exemplo a seguir contém parâmetros inválidos. Os primeiros dois itens são parâmetros de linha de comando do Windows PowerShell (**-NoLogo** e **-ExecutionPolicy Unrestricted**). O script não consome esses parâmetros.  
>   
>  `-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`  

 **Política de execução do PowerShell**  
 Determinar quais scripts do Windows PowerShell (se houver) você permite que sejam executados no computador. Selecione uma das seguintes políticas de execução:  

-   **AllSigned**: executar somente scripts assinados por um fornecedor confiável  

-   **Undefined**: não definir nenhuma política de execução  

-   **Bypass**: carregar todos os arquivos de configuração e executar todos os scripts. Se você baixar um script não assinado da Internet, o Windows PowerShell não solicitará permissão antes de executar o script.  

> [!IMPORTANT]  
>  O PowerShell 1.0 não suporta as políticas de execução Indefinido e Ignorar.  



##  <a name="child-task-sequence"></a> Executar sequência de tarefas

Começando com o Configuration Manager versão 1710, você pode adicionar uma nova etapa que executa outra sequência de tarefas. Essa etapa cria um relacionamento pai-filho entre as sequências de tarefas. Com uma sequência de tarefas filho, é possível criar sequências de tarefas mais modulares e reutilizáveis.

Quando você adiciona uma sequência de tarefas filho a uma sequência de tarefas, considere as seguintes instruções:
 - As sequências de tarefas pai e filho efetivamente são combinadas em uma única política que o cliente executa.
 - O ambiente é global. Se a sequência de tarefas pai define uma variável e, em seguida, a sequência de tarefas filho altera essa variável, a variável retém o valor mais recente. Se a sequência de tarefas filho criar uma nova variável, a variável estará disponível para o restante da sequência de tarefas pai.
 - As mensagens de status são enviadas normalmente para uma operação de sequência de tarefas.
 - As sequências de tarefas gravam entradas no arquivo smsts.log, com novas entradas de log que deixam claro quando uma sequência de tarefas filho é iniciada.

No editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e selecione **Executar Sequência de Tarefas** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

**Selecionar sequência de tarefas para executar**  
 Clique em **Procurar** para selecionar a sequência de tarefas filho. A caixa de diálogo **Selecionar uma Sequência de Tarefas** não mostra a sequência de tarefas pai.



##  <a name="BKMK_SetDynamicVariables"></a> Definir Variáveis Dinâmicas  
 Use esta etapa para executar as seguintes ações:  

1.  Coletar informações do computador e do ambiente onde ele se encontra, e então definir variáveis de sequência de tarefas especificadas com as informações.  

2.  Avalia as regras estabelecidas e define as variáveis de sequência de tarefas com base nas variáveis e nos valores configurados para as regras que avaliam como verdadeiro.  

A sequência de tarefas define automaticamente as seguintes variáveis de sequência de tarefas somente leitura:  
 -   &#95;SMSTSMake  
 -   &#95;SMSTSModel  
 -   &#95;SMSTSMacAddresses  
 -   &#95;SMSTSIPAddresses  
 -   &#95;SMSTSSerialNumber  
 -   &#95;SMSTSAssetTag  
 -   &#95;SMSTSUUID  

Esta etapa pode ser executada em um sistema operacional padrão ou no Windows PE. Para mais informações sobre variáveis de sequência de tarefas, confira [Task sequence action variables](task-sequence-action-variables.md) (Variáveis de ação de sequência de tarefas).  

No editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e selecione **Definir Variáveis Dinâmicas** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

**Regras e variáveis dinâmicas**  
 Para definir uma variável dinâmica para uso na sequência de tarefas, adicione uma regra. Em seguida, defina um valor para cada variável especificada na regra. Além disso, adicione uma ou mais variáveis sem adicionar uma regra. Quando você adicionar uma regra, poderá escolher entre as seguintes categorias:  

 -   **Computador**: avaliar valores para a Marcação do ativo, UUID, número de série ou endereço MAC. Defina vários valores, conforme necessário. Se algum valor for true, a regra será avaliada como true. Por exemplo, a seguinte regra é avaliada como true se o número de série do dispositivo é 5892087 e o endereço MAC é 22-A4-5A-13-78-26.  

     `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

-   **Local**: avaliar valores para o gateway de rede padrão  

-   **Marca e Modelo**: avaliar valores para a marca e o modelo de um computador. A marca e o modelo devem ambas serem avaliadas como verdadeiro para a regra a ser avaliada como verdadeiro.   

    <!-- for future edits: an escape code must be used for the bolded asterisk character, but may be removed somewhere along the way. Instead of five asterisk, should be bold tags with &#42; in-between -->

    A partir do Configuration Manager versão 1610, você pode especificar um asterisco (**&#42;**) e um ponto de interrogação (**?**) como caracteres curinga, em que **&#42;** corresponde a vários caracteres e **?** corresponde a um único caractere. Por exemplo, a cadeia de caracteres "DELL*900?" corresponderá a DELL-ABC-9001 e DELL9009. 

    Especifique um asterisco (**&#42;**) e um ponto de interrogação (**?**) como caracteres curinga, em que **&#42;** corresponde a vários caracteres e **?** corresponde a um único caractere. Por exemplo, a cadeia de caracteres "DELL*900?" corresponde a DELL-ABC-9001 e DELL9009.

-   **Variável de Sequência de Tarefas**: adicionar uma variável, condição e valor da sequência de tarefas a ser avaliada. A regra avalia como verdadeiro quando o valor definido para a variável atende a condição especificada.  

    Especifique uma ou mais variáveis a serem definidas para uma regra que é avaliada como verdadeiro ou definir variáveis sem usar uma regra. Selecione uma variável existente ou crie uma variável personalizada.  

     -   **Variáveis de sequência de tarefas existentes**: selecione uma ou mais variáveis em uma lista de variáveis de sequência de tarefas existentes. Variáveis de matriz não estão disponíveis para selecionar.  

     -   **Variáveis personalizadas da sequência de tarefas**: defina uma variável personalizada da sequência de tarefas. Você também pode especificar uma variável de sequência de tarefas existente. Essa configuração é útil para especificar uma matriz de variáveis existente, como OSDAdapter, pois matrizes de variáveis não estão na lista de variáveis de sequência de tarefas existente.  

Depois de selecionar as variáveis de uma regra, você deve fornecer um valor para cada variável. A variável é definida como o valor especificado quando a regra for avaliada como verdadeiro. Para cada variável, você pode selecionar o **Valor secreto** para ocultar o valor da variável. Por padrão, algumas variáveis existentes ocultam valores, como a variável de sequência de tarefas OSDCaptureAccountPassword.  

> [!IMPORTANT]  
>  O Configuration Manager remove quaisquer valores de variável marcados como um **valor secreto** quando você importa uma sequência de tarefas com a etapa **Definir Variáveis Dinâmicas**. Reinsira o valor da variável dinâmica novamente depois de importar a sequência de tarefas.  



##  <a name="BKMK_SetTaskSequenceVariable"></a> Definir Variável de Sequência de Tarefas  
Use essa etapa para definir o valor de uma variável usada com a sequência de tarefas.  

Esta etapa pode ser executada em um sistema operacional padrão ou no Windows PE. Variáveis de sequência de tarefas são lidas por ações de sequência de tarefas e especificam o comportamento dessas ações. Para mais informações sobre variáveis de ação de sequência de tarefas específicas, confira [Variáveis de ação de sequência de tarefas](task-sequence-action-variables.md). Para mais informações sobre variáveis internas de sequência de tarefas específicas, confira [Variáveis internas de sequência de tarefas](/sccm/osd/understand/task-sequence-built-in-variables).

No editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e selecione **Definir Variável de Sequência de Tarefas** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Variável de sequência de tarefas**  
 Especifique o nome de uma variável interna ou de ação de sequência de tarefas ou especifique seu próprio nome de variável definido pelo usuário.  

 **Valor**  
 A sequência de tarefas define a variável para esse valor. Defina essa variável de sequência de tarefas para o valor de outra variável de sequência de tarefas com a sintaxe %varname%.  



##  <a name="BKMK_SetupWindowsandConfigMgr"></a> Instalar Windows e ConfigMgr  
 Use esta etapa para fazer a transição do Windows PE para o novo sistema operacional. Esta etapa da sequência de tarefas é necessária em qualquer implantação de sistema operacional. Ele instala o cliente do Configuration Manager no novo sistema operacional e prepara a sequência de tarefas para continuar a execução no novo sistema operacional.  

 Esta etapa é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão. Para obter mais informações sobre variáveis de sequência de tarefas para esta ação, consulte [Setup Windows and ConfigMgr task sequence action variables](task-sequence-action-variables.md#BKMK_SetupWindows) (Variáveis da ação da sequência de tarefas de Instalar Windows e ConfigMgr).  

 Esta etapa substitui as variáveis de diretório sysprep.inf ou unattend.xml, tais como %WINDIR% e %ProgramFiles%, pelo diretório de instalação do Windows PE, X:\Windows. A sequência de tarefas ignora variáveis especificadas usando essas variáveis de ambiente.  

 Use essa etapa de sequência de tarefas para executar as seguintes ações:  

1.  Etapas preliminares: Windows PE  

    1.  Substitua as variáveis de sequência de tarefas no arquivo unattend.xml.  

    2.  Baixe o pacote que contém o cliente do Configuration Manager. Adicione o pacote à imagem implantada.  

2.  Configurar o Windows  

    1.  Instalação baseada em imagem  

        1.  Desabilite o cliente do Configuration Manager na imagem, se ele existir. Em outras palavras, desabilite o Início Automático para o serviço de cliente do Configuration Manager.  

        2.  Atualiza o registro da imagem implantada para que o sistema operacional implantado comece com a mesma letra de unidade que o computador de referência.  

        3.  Reinicie para o sistema operacional implantado.  

        4.  Mini-instalação do Windows executada usando o arquivo de resposta sysprep.inf ou unattend.xml especificado com todas as interações do usuário final suprimidas. Se você usar a etapa **Aplicar Configurações de Rede** para ingressar em um domínio, essa informação estará no arquivo de resposta. A mini-instalação do Windows adiciona o computador ao domínio.  

    2.  Instalação baseada em Setup.exe.  Executa o Setup.exe que segue o processo de instalação típica do Windows:  

        1.  Copie o pacote de atualização do sistema operacional, especificado na etapa **Aplicar Sistema Operacional**, para a unidade de disco rígido.  

        2.  Reinicie para o sistema operacional recém-implantado.  

        3.  Mini-instalação do Windows executada usando o arquivo de resposta sysprep.inf ou unattend.xml especificado com todas as interfaces do usuário suprimidas. Se você usar a etapa **Aplicar Configurações de Rede** para ingressar em um domínio, essa informação estará no arquivo de resposta. A mini-instalação do Windows adiciona o computador ao domínio.  

3.  Instalar o cliente do Configuration Manager  

    1.  Após a conclusão da mini-instalação do Windows, a sequência de tarefas é retomada usando setupcomplete.cmd.  

    2.  Habilite ou desabilite a conta de administrador local, com base na opção selecionada na etapa **Aplicar configurações do Windows**.  

    3.  Instale o cliente do Configuration Manager usando o pacote baixado anteriormente e as propriedades de instalação especificadas nesta etapa. O cliente é instalado em "modo de provisionamento" para impedir o processamento de novas solicitações de política de até que a sequência de tarefas seja concluída.  

    4.  Aguarde até que o cliente esteja totalmente operacional.  

4.  A sequência de tarefas continua executando a próxima etapa.  

<!-- Engineering confirmed that the task sequence does nothing with respect to group policy processing.
> [!NOTE]  
>  The **Setup Windows and ConfigMgr** task sequence action is responsible for running Group Policy on the newly installed computer. The Group Policy is applied after the task sequence is finished.  
-->

No editor de sequência de tarefas, clique em **Adicionar**, selecione **Imagens** e selecione **Instalar o Windows e o ConfigMgr** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

 **Pacote do cliente**  
 Clique em **Procurar** e selecione o pacote de instalação de cliente do Configuration Manager a ser usado com essa etapa.  

 **Usar pacote de cliente de pré-produção quando disponível**  
 Se houver um pacote de cliente de pré-produção disponível e o computador fizer parte de uma coleção piloto, a sequência de tarefas usará esse pacote em vez do pacote do cliente de produção. O cliente de pré-produção é uma versão mais recente para testes no ambiente de produção. Clique em **Procurar** e selecione o pacote de instalação de cliente de pré-produção a ser usado com essa etapa.  

 **Propriedades de Instalação**  
 Atribuição de site e a configuração padrão são automaticamente especificadas pela ação de sequência de tarefas. Você pode usar esse campo para especificar as propriedades adicionais de instalação a serem usada ao instalar o cliente. Para inserir várias propriedades de instalação, separe-as com um espaço.  

 Você pode especificar as opções de linha de comando usadas durante a instalação do cliente. Por exemplo, você pode inserir **/skipprereq: silverlight.exe** para informar o CCMSetup.exe para não instalar o pré-requisito do Microsoft Silverlight. Para mais informações sobre as opções de linha de comando disponíveis para o CCMSetup.exe, confira [About client installation properties](../../core/clients/deploy/about-client-installation-properties.md) (Sobre as propriedades da instalação do cliente).  

### <a name="options"></a>Opções
> [!NOTE]
> Não habilite **Continuar em Caso de Erro** na guia **Opções**. Se houver um erro durante essa etapa, a sequência de tarefas falhará, independentemente de você habilitar essa configuração ou não.



##  <a name="BKMK_UpgradeOS"></a> Atualizar o sistema operacional  
 > [!TIP]  
 > Começando com o Windows 10, versão 1709, a mídia inclui várias edições. Quando você configura uma sequência de tarefas para usar uma imagem do sistema operacional ou um pacote de atualização do sistema operacional, é necessário selecionar uma [edição compatível](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).

 Use essa etapa para atualizar uma versão mais antiga do Windows para uma versão mais recente do Windows 10.  

 Essa etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE.  

No editor de sequência de tarefas, clique em **Adicionar**, selecione **Imagens** e selecione **Atualizar Sistema Operacional** para adicionar essa etapa. 

### <a name="properties"></a>Propriedades  
Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

**Atualizar pacote**  
 Selecione esta opção para especificar o pacote de atualização do sistema operacional Windows 10 a ser usado para a atualização.  

**Caminho de origem**  
 Especifica um caminho de rede ou local para a mídia do Windows 10 usada pela Instalação do Windows. Essa configuração corresponde à opção de linha de comando **/InstallFrom** da Instalação do Windows. Você também pode especificar uma variável, como %mycontentpath% ou %DPC01%. Quando você usa uma variável para o caminho de origem, ele deve ser especificado anteriormente na sequência de tarefas. Por exemplo, se você usar a etapa [Baixar o conteúdo do pacote](#BKMK_DownloadPackageContent) na sequência de tarefas, é possível especificar uma variável para o local do pacote de atualização do sistema operacional. Em seguida, você pode usar essa variável para o caminho de origem nesta etapa.  

**Edição**  
 Especifique a edição na mídia do sistema operacional a ser usada para a atualização.  

**Chave do produto (Product Key)**  
 Especificar a chave do produto (Product Key) a ser aplicada ao processo de atualização  

**Forneça o conteúdo do driver a seguir para a Instalação do Windows durante a atualização**  
 Adicione drivers ao computador de destino durante o processo de atualização. Essa configuração corresponde à opção de linha de comando **/InstallDriver** da Instalação do Windows. Os drivers devem ser compatíveis com o Windows 10. especifique uma das seguintes opções:  

-   **Pacote de driver**: clique em **Procurar** e selecione um pacote de driver existente na lista.  

-   **Conteúdo de teste**: selecione esta opção para especificar o local para o pacote de drivers. Você pode especificar uma pasta local, um caminho de rede ou uma variável de sequência de tarefas. Quando você usa uma variável para o caminho de origem, ele deve ser especificado anteriormente na sequência de tarefas. Por exemplo, usando a etapa [Download Package Content](task-sequence-steps.md#BKMK_DownloadPackageContent) .  

**Time-out (minutes) (Tempo limite (minutos))**  
 Especifica o número de minutos antes que o Configuration Manager falhe nesta etapa. Essa opção será útil se a Instalação do Windows parar o processamento, mas não encerrar.  

**Executar a verificação de compatibilidade da Instalação do Windows sem iniciar a atualização**  
 Execute a verificação de compatibilidade da Instalação do Windows sem iniciar o processo de atualização. Essa configuração corresponde à opção de linha de comando **/Compat ScanOnly** da Instalação do Windows. Você deve implantar a origem de instalação inteira ao usar essa opção. A instalação retorna um código de saída como resultado da verificação. A tabela a seguir fornece alguns dos códigos de saída mais comuns.  

|Código de saída|Detalhes|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Nenhum problema de compatibilidade (“êxito”).|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|Problemas de compatibilidade acionáveis.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|A opção de migração selecionada não está disponível. Por exemplo, uma atualização do Enterprise para Professional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Não qualificado para Windows 10.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|Não há espaço livre em disco suficiente.|  

Para obter mais informações sobre este parâmetro, veja [Opções de Linha de Comando da Instalação do Windows](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx)  

**Ignorar quaisquer mensagens de compatibilidade rejeitadas**  
 Especifica que a Configuração conclui a instalação, ignorando quaisquer mensagens de compatibilidade dispensáveis. Essa configuração corresponde à opção de linha de comando **/Compat IgnoreWarning** da Instalação do Windows.  

**Atualizar dinamicamente a Instalação do Windows com o Windows Update**  
 Habilite a instalação para executar operações de atualização dinâmica, tais como pesquisa, download e instalação de atualizações. Essa configuração corresponde à opção de linha de comando **/DynamicUpdate** da Instalação do Windows. Essa configuração não é compatível com as atualizações de software do Configuration Manager. Habilite esta opção quando você gerencia atualizações com o WSUS (Windows Server Update Services) autônomo ou o Windows Update para Empresas.  

**Substituir política e usar o Microsoft Update padrão** Substitua temporariamente a política local em tempo real para executar operações de Atualização Dinâmica e fazer com que o computador obtenha atualizações do Windows Update.
