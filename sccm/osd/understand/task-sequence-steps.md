---
title: Etapas da sequência de tarefas
titleSuffix: Configuration Manager
description: Saiba mais sobre as etapas que você pode adicionar a uma sequência de tarefas do Configuration Manager.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3e0b70a2b024555bd67f63b3a31a6408b07c273b
ms.sourcegitcommit: be8c0182db9ef55a948269fcbad7c0f34fd871eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42756070"
---
# <a name="task-sequence-steps-in-configuration-manager"></a>Etapas de sequência de tarefas no Configuration Manager

 *Aplica-se a: System Center Configuration Manager (Branch Atual)*

 As etapas de sequência de tarefas a seguir podem ser adicionadas à sequência de tarefas do Configuration Manager. Para obter informações sobre como editar uma sequência de tarefas, veja [Edit a task sequence](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_ModifyTaskSequence).  

 As configurações a seguir são comuns a todas as etapas da sequência de tarefas:

#### <a name="properties-tab"></a>Guia Propriedades
 - **Nome**: o editor de sequência de tarefas requer que você especifique um nome curto para descrever essa etapa. Quando você adiciona uma nova etapa, o editor de sequência de tarefas define o nome para o Tipo por padrão. O tamanho do **Nome** não pode exceder 50 caracteres.  

 - **Descrição**: opcionalmente, especifique informações mais detalhadas sobre essa etapa. O tamanho da **Descrição** não pode exceder 256 caracteres.  


 O restante deste artigo descreve as outras configurações na guia **Propriedades** para cada etapa da sequência de tarefas.

#### <a name="options-tab"></a>Guia Opções  

 - **Desabilitar esta etapa**: a sequência de tarefas ignora essa etapa quando ela é executada em um computador. O ícone para esta etapa é esmaecido no editor de sequência de tarefas.  

 - **Continuar em caso de erro**: se ocorrer um erro durante a execução da etapa, a sequência de tarefas continuará. Para saber mais, confira [Considerações de planejamento para automatizar tarefas](/sccm/osd/plan-design/planning-considerations-for-automating-tasks#BKMK_TSGroups).   

 - **Adicionar Condição**: A sequência de tarefas avalia essas instruções condicionais para determinar se ela executa a etapa. Para obter um exemplo de como usar uma variável de sequência de tarefas como condição, confira [Como usar variáveis de sequência de tarefas](/sccm/osd/understand/using-task-sequence-variables#bkmk_access-condition).   


 As seções abaixo para etapas específicas de sequência de tarefas descrevem outras configurações possíveis na guia **Opções**.



##  <a name="BKMK_ApplyDataImage"></a> Aplicar Imagem de Dados   

 Use essa etapa para copiar a imagem de dados na partição de destino especificada.  

 Esta etapa é executada somente no Windows PE. Ela não é executada no sistema operacional completo. 

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [OSDDataImageIndex](/sccm/osd/understand/task-sequence-variables#OSDDataImageIndex)  
 - [OSDWipeDestinationPartition](/sccm/osd/understand/task-sequence-variables#OSDWipeDestinationPartition)  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Imagens** e selecione **Aplicar Imagem de Dados**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="image-package"></a>Pacote da imagem  
 Clique em **Procurar** para especificar o **Pacote de Imagem** usado por essa sequência de tarefas. Selecione o pacote que você deseja instalar na caixa de diálogo **Selecionar um pacote** . A parte inferior da caixa de diálogo exibe as informações de propriedade associadas para cada pacote de imagem existente. Use a lista suspensa para selecionar a **imagem** você deseja instalar por meio do **Pacote de imagem**selecionado.  

 > [!NOTE]  
 >  Esta ação da sequência de tarefas trata a imagem como um arquivo de dados. Esta ação não faz nenhuma configuração para inicializar a imagem como sistema operacional.  

#### <a name="destination"></a>Destino  
 Configure uma das seguintes opções:

 - **Próxima partição disponível**: use a próxima partição sequencial que ainda não foi usada como destino por uma etapa **Aplicar Sistema Operacional** ou **Aplicar Imagem de Dados** nessa sequência de tarefas.  

 - **Disco e partição específicos**: selecione o número do **Disco** (começando com 0) e o da **Partição** (começando com 1).  

 - **Letra da unidade lógica específica**: especifique a **Letra da Unidade** atribuída à partição pelo Windows PE. Essa letra de unidade pode ser diferente da letra de unidade atribuída pelo sistema operacional implantado recentemente.  

 - **Letra de unidade lógica armazenada em uma variável**: especifique a variável de sequência de tarefas que contém a letra da unidade atribuída à partição pelo Windows PE. Essa variável é normalmente definida na seção Avançado da caixa de diálogo **Propriedades da Partição** para a etapa da sequência de tarefa **Formatar e Particionar o Disco**.  

#### <a name="delete-all-content-on-the-partition-before-applying-the-image"></a>Excluir todo o conteúdo na partição antes de aplicar a imagem  
 Especifica que a sequência de tarefas exclui todos os arquivos na partição de destino antes de instalar a imagem. Não excluindo o conteúdo da partição, esta ação pode ser usada para aplicar o conteúdo adicional a uma partição de destino anterior.  



##  <a name="BKMK_ApplyDriverPackage"></a> Aplicar pacote de driver  

 Use esta etapa para baixar todos os drivers no pacote de driver e instalá-los no sistema operacional Windows.

 A etapa da sequência de tarefas **Aplicar pacote de Driver** disponibiliza todos os drivers de dispositivo em um pacote de driver para uso pelo Windows. Adicione esta etapa entre as etapas **Aplicar sistema operacional** e **Instalação do Windows e do ConfigMgr** para disponibilizar os drivers de dispositivo no pacote de drivers para o Windows. Normalmente, a etapa **Aplicar pacote de Driver** é posicionada após a **Aplicação automática de drivers** . A etapa da sequência de tarefas **Aplicar pacote de Driver** também é útil em cenários de implantação de mídia autônoma.  

 Coloque drivers de dispositivo similares em um pacote de driver e distribua-os aos pontos de distribuição apropriados. Por exemplo, coloque todos os drivers de um fabricante em um pacote de driver. Em seguida, distribua o pacote para pontos de distribuição em que os computadores associados possam acessá-lo.

 A etapa **Aplicar Pacote de Driver** é útil para mídia autônoma. Esta etapa também é útil para instalar um conjunto específico de drivers. Esses tipos de drivers incluem dispositivos não detectados pelo plug-and-play do Windows, como impressoras de rede.  

 Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada no sistema operacional completo. 

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [OSDApplyDriverBootCriticalContentUniqueID](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalContentUniqueID)  
 - [OSDApplyDriverBootCriticalHardwareComponent](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalHardwareComponent)  
 - [OSDApplyDriverBootCriticalID](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalID)  
 - [OSDApplyDriverBootCriticalINFFile](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalINFFile)  
 - [OSDInstallDriversAdditionalOptions](/sccm/osd/understand/task-sequence-variables#OSDInstallDriversAdditionalOptions)<!--516679/2840016--> (a partir da versão 1806)  


 Para adicionar essa etapa, no editor de sequência de tarefas, clique em **Adicionar**, selecione **Drivers** e selecione **Aplicar Pacote de Driver**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="driver-package"></a>Pacote de Drivers
 Especifique o pacote de drivers que contém os drivers de dispositivo necessários. Clique em **Procurar** para iniciar a caixa de diálogo **Selecionar um Pacote**. Selecione um pacote de driver existente para aplicação. A parte inferior da caixa de diálogo exibe as propriedades do pacote associado.  

#### <a name="select-the-mass-storage-driver-within-the-package-that-needs-to-be-installed-before-setup-on-pre-windows-vista-operating-systems"></a>Selecione o driver de armazenamento em massa dentro do pacote que precisa ser instalado antes da instalação em sistemas operacionais anteriores ao Windows Vista
 Especifique os drivers de armazenamento em massa necessários para instalar um sistema operacional clássico.  

#### <a name="driver"></a>Driver
 Selecione o arquivo de driver de armazenamento em massa para instalar antes da instalação de um sistema operacional clássico. A lista suspensa é populada do pacote especificado.  

#### <a name="model"></a>Modelo  
 Especifique a inicialização crítica de dispositivo necessária para implantações de sistemas operacionais anteriores ao Windows Vista.  

#### <a name="do-unattended-installation-of-unsigned-drivers-on-version-of-windows-where-this-is-allowed"></a>Faça uma instalação autônoma de drivers não assinados nas versões do Windows em que isso é permitido
 Essa opção permite que o Windows instale drivers sem uma assinatura digital.  



##  <a name="BKMK_ApplyNetworkSettings"></a> Aplicar Configurações de Rede   

 Use essa etapa para especificar as informações de configuração de rede ou grupo de trabalho do computador de destino. A sequência de tarefas armazena esses valores no arquivo de resposta apropriado. A Instalação do Windows usa esse arquivo de resposta durante a ação **Instalação do Windows e ConfigMgr**.  

 Essa etapa da sequência de tarefas é executada no sistema operacional completo ou no Windows PE. 

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [OSDAdapter](/sccm/osd/understand/task-sequence-variables#OSDAdapter)  
 - [OSDAdapterCount](/sccm/osd/understand/task-sequence-variables#OSDAdapterCount)  
 - [OSDDNSDomain](/sccm/osd/understand/task-sequence-variables#OSDDNSDomain)  
 - [OSDDNSSuffixSearchOrder](/sccm/osd/understand/task-sequence-variables#OSDDNSSuffixSearchOrder)  
 - [OSDDomainName](/sccm/osd/understand/task-sequence-variables#OSDDomainName)  
 - [OSDDomainOUName](/sccm/osd/understand/task-sequence-variables#OSDDomainOUName)  
 - [OSDEnableTCPIPFiltering](/sccm/osd/understand/task-sequence-variables#OSDEnableTCPIPFiltering)  
 - [OSDJoinAccount](/sccm/osd/understand/task-sequence-variables#OSDJoinAccount)  
 - [OSDJoinPassword](/sccm/osd/understand/task-sequence-variables#OSDJoinPassword)  
 - [OSDWorkgroupName](/sccm/osd/understand/task-sequence-variables#OSDWorkgroupName)  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Configurações** e selecione **Aplicar Configurações de Rede**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="join-a-workgroup"></a>Ingressar em um grupo de trabalho
 Selecione esta opção para fazer o computador de destino ingressar no grupo de trabalho especificado. Insira o nome do grupo de trabalho na linha **Grupo de trabalho** . O valor capturado pela etapa da sequência de tarefas **Capturar Configurações de Rede** pode ser substituído por esse valor. 

#### <a name="join-a-domain"></a>Ingressar em um domínio
 Selecione esta opção para fazer o computador de destino ingressar no domínio especificado. Especifique ou navegue para o domínio, como `fabricam.com`. Especifique ou procure um caminho LDAP (Lightweight Directory Access Protocol) para uma unidade organizacional. Por exemplo: `LDAP//OU=computers, DC=Fabricam.com, C=com`.  

#### <a name="account"></a>Conta
 Clique em **Definir** para especificar uma conta com as permissões necessárias para ingressar o computador no domínio. Na caixa de diálogo **Conta de Usuário do Windows**, insira o nome de usuário no seguinte formato: `Domain\User`. Para saber mais, confira [Conta de ingresso no domínio](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-domain-joining-account). 

#### <a name="adapter-settings"></a>Configurações do adaptador  
 Especifica configurações de rede para cada adaptador de rede no computador. Clique em **Novo** para abrir a caixa de diálogo **Configurações de rede** e especifique as configurações de rede. 
 - Se você também usar a etapa **Capturar Configurações de Rede**, a sequência de tarefas aplicará as configurações capturadas anteriormente ao adaptador de rede. 
 - Se a sequência de tarefas não tiver capturado as configurações de rede, ela aplicará as configurações especificadas nessa etapa. 
 - A sequência de tarefas aplica essas configurações a adaptadores de rede na ordem de enumeração de dispositivos do Windows.  
 - A sequência de tarefas não aplica imediatamente ao computador as configurações especificadas nesta etapa. 



##  <a name="BKMK_ApplyOperatingSystemImage"></a> Aplicar Imagem de Sistema Operacional  

 > [!TIP]  
 > Começando com o Windows 10, versão 1709, a mídia inclui várias edições. Quando você configura uma sequência de tarefas para usar uma imagem do sistema operacional ou um pacote de atualização do sistema operacional, é necessário selecionar uma [edição compatível](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).  

 Use essa etapa para instalar um sistema operacional no computador de destino. 

 > [!NOTE]  
 >  A etapa **Instalar o Windows e o ConfigMgr** inicia a Instalação do Windows. 

 Após a execução da ação **Aplicar sistema operacional**, ela define a variável **OSDTargetSystemDrive** como a letra da unidade da partição que contém os arquivos do sistema operacional.  

 Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada no sistema operacional completo. 

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [OSDConfigFileName](/sccm/osd/understand/task-sequence-variables#OSDConfigFileName)  
 - [OSDImageIndex](/sccm/osd/understand/task-sequence-variables#OSDImageIndex)  
 - [OSDTargetSystemDrive](/sccm/osd/understand/task-sequence-variables#OSDTargetSystemDrive)  


 Para adicionar essa etapa, no editor de sequência de tarefas, clique em **Adicionar**, selecione **Imagens** e selecione **Aplicar Imagem do Sistema Operacional**. 

 Esta etapa executa ações, dependendo de ela usar ou não uma imagem do SO ou um pacote de atualização do SO.  

#### <a name="os-image-actions"></a>Ações de imagem do sistema operacional
 A etapa **Aplicar imagem do sistema operacional** executa as seguintes ações ao usar uma imagem do SO:  

 1.  Exclua todo o conteúdo no volume de destino, exceto os arquivos na pasta especificada pela variável **\_SMSTSUserStatePath**.  

 2.  Extração do conteúdo do arquivo .wim especificado para a partição de destino especificada.  

 3.  Prepare o arquivo de resposta:  

    1.  Crie um novo arquivo de resposta padrão da Instalação do Windows (sysprep.inf ou unattend.xml) para o sistema operacional implantado.  

    2.  Mescle quaisquer valores do arquivo de resposta fornecido pelo usuário.  

 4.  Cópia de carregadores de inicialização do Windows para a partição ativa.  

 5.  Configuração do boot.ini ou do BCD (Banco de Dados de Configuração da Inicialização) para referenciar o sistema operacional recém-instalado.  

#### <a name="os-upgrade-package-actions"></a>Ações do pacote de atualização do sistema operacional
 A etapa **Aplicar imagem do sistema operacional** executa as seguintes ações ao usar um pacote de atualização do SO:  

 1.  Exclua todo o conteúdo no volume de destino, exceto os arquivos na pasta especificada pela variável **\_SMSTSUserStatePath**.  

 2.  Prepare o arquivo de resposta:  

    1.  Criação de um arquivo de resposta novo com valores padrão criados pelo Configuration Manager.  

    2.  Mescle quaisquer valores do arquivo de resposta fornecido pelo usuário.  


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="apply-operating-system-from-a-captured-image"></a>Aplicar o sistema operacional de uma imagem capturada
 Instala uma imagem do sistema operacional que você capturou. Clique em **Procurar** para abrir a caixa de diálogo **Selecionar um pacote**. Em seguida, selecione o pacote de imagem existente que você quer instalar. Se várias imagens forem associadas ao **pacote de imagem** especificado, selecione a imagem associada que será usada para essa implantação na lista suspensa. Veja as informações básicas sobre cada imagem existente clicando nela.  

#### <a name="apply-operating-system-image-from-an-original-installation-source"></a>Aplicar a imagem do sistema operacional de uma fonte de instalação original
 Instala um sistema operacional usando um pacote de atualização do sistema operacional, que também é uma fonte de instalação original. Clique em **Procurar** para abrir a caixa de diálogo **Selecionar um Pacote de Instalação do Sistema Operacional**. Em seguida, selecione o pacote de atualização do SO existente que você deseja usar. Clique em cada fonte de imagem existente para exibir informações básicas sobre ela. O painel de resultados na parte inferior da caixa de diálogo exibe as propriedades da fonte da imagem associada. Se houver várias edições associadas ao pacote especificado, use a lista suspensa para selecionar a **Edição** desejada.  

#### <a name="use-an-unattended-or-sysprep-answer-file-for-a-custom-installation"></a>Use um arquivo de resposta unattended ou sysprep para uma instalação personalizada
 Use essa opção para fornecer um arquivo de resposta de instalação do Windows (**unattend.xml**, **unattend.txt** ou **sysprep.inf**) dependendo do método de instalação e da versão do sistema operacional. O arquivo especificado pode incluir qualquer uma das opções de configuração padrão compatíveis com arquivos de resposta do Windows. Por exemplo, você pode usá-la para especificar a página inicial padrão do Internet Explorer. Especifique o pacote que contém o arquivo de resposta e o caminho associado ao arquivo no pacote.  

 > [!NOTE]  
 >  O arquivo de resposta de instalação do Windows que você fornece pode conter variáveis de sequência de tarefa integradas na forma `%varname%`, em que *varname* é o nome da variável. A etapa **Instalação do Windows e ConfigMgr** substitui a cadeia de caracteres da variável pelos valores reais da variável. Não é possível usar essas variáveis de sequência de tarefas integradas em campos somente numéricos em um arquivo de resposta unattend.xml.  

 Se você não fornecer um arquivo de resposta de Instalação do Windows, essa sequência de tarefas gerará automaticamente um arquivo de resposta.  

#### <a name="destination"></a>Destino  
 Configure uma das seguintes opções:  

 - **Próxima partição disponível**: use a próxima partição sequencial que ainda não foi usada como destino por uma etapa **Aplicar Sistema Operacional** ou **Aplicar Imagem de Dados** nessa sequência de tarefas.  

 - **Disco e partição específicos**: selecione o número do **Disco** (começando com 0) e o da **Partição** (começando com 1).  

 - **Letra da unidade lógica específica**: especifique a **Letra da Unidade** atribuída à partição pelo Windows PE. Essa letra de unidade pode ser diferente da letra de unidade atribuída pelo sistema operacional implantado recentemente.  

 - **Letra de unidade lógica armazenada em uma variável**: especifique a variável de sequência de tarefas que contém a letra da unidade atribuída à partição pelo Windows PE. Essa variável é normalmente definida na seção Avançado da caixa de diálogo **Propriedades da Partição** para a etapa da sequência de tarefa **Formatar e Particionar o Disco**.  


### <a name="options"></a>Opções  

 Além das opções padrão, defina as seguintes configurações adicionais na guia **Opções** dessa etapa da sequência de tarefas:  

#### <a name="access-content-directly-from-the-distribution-point"></a>Acessar o conteúdo diretamente do ponto de distribuição
 Configure a sequência de tarefas para acessar a imagem do sistema operacional diretamente do ponto de distribuição. Por exemplo, use essa opção ao implantar sistemas operacionais em dispositivos inseridos que têm a capacidade de armazenamento limitada. Ao selecionar essa opção, configure também as configurações de compartilhamento de pacote na guia **Acesso a Dados** das propriedades da imagem do sistema operacional.  

 > [!NOTE]  
 >  Essa configuração substitui a opção de implantação que você configura na página **Pontos de Distribuição** do **Assistente de Implantação de Software**. Essa substituição é apenas para a imagem do sistema operacional que esta etapa especifica, não para todo o conteúdo da sequência de tarefas.  



##  <a name="BKMK_ApplyWindowsSettings"></a> Aplicar as Configurações do Windows  

 Use essa etapa para definir as configurações do Windows no computador de destino. A sequência de tarefas armazena esses valores no arquivo de resposta apropriado. A Instalação do Windows usa esse arquivo de resposta durante a etapa **Instalação do Windows e ConfigMgr**.  

 Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada no sistema operacional completo.  

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [OSDComputerName](/sccm/osd/understand/task-sequence-variables#OSDComputerName-input)  
 - [OSDLocalAdminPassword](/sccm/osd/understand/task-sequence-variables#OSDLocalAdminPassword)  
 - [OSDProductKey](/sccm/osd/understand/task-sequence-variables#OSDProductKey)  
 - [OSDRandomAdminPassword](/sccm/osd/understand/task-sequence-variables#OSDRandomAdminPassword)  
 - [OSDRegisteredOrgName](/sccm/osd/understand/task-sequence-variables#OSDRegisteredOrgName-input)  
 - [OSDRegisteredUserName](/sccm/osd/understand/task-sequence-variables#OSDRegisteredUserName)  
 - [OSDServerLicenseConnectionLimit](/sccm/osd/understand/task-sequence-variables#OSDServerLicenseConnectionLimit)  
 - [OSDServerLicenseMode](/sccm/osd/understand/task-sequence-variables#OSDServerLicenseMode)  
 - [OSDTimeZone](/sccm/osd/understand/task-sequence-variables#OSDTimeZone-input)  


 Para adicionar essa etapa, no editor de sequência de tarefas, clique em **Adicionar**, selecione **Configurações** e selecione **Aplicar Configurações do Windows**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="user-name"></a>Nome de usuário
 Especifique o nome de usuário registrado para associar ao computador de destino. O valor capturado pela etapa da sequência de tarefas **Capturar Configurações do Windows** pode ser substituído por esse valor.  

#### <a name="organization-name"></a>Nome da organização
 Especifique o nome de organização registrado para associar ao computador de destino. O valor capturado pela etapa da sequência de tarefas **Capturar Configurações do Windows** pode ser substituído por esse valor.  

#### <a name="product-key"></a>Chave do produto  
 Especifique a chave do produto usada para a instalação do Windows no computador de destino.  

#### <a name="server-licensing"></a>Licenciamento do servidor  
 Especifique o modo de licenciamento do servidor. 
 - Selecione **Por servidor** ou **Por usuário** como o modo de licenciamento.  
 - Se você selecionar **Por servidor**, especifique também o número máximo de conexões permitidas por seu contrato de licença.  
 - Selecione **Não especificar** se o computador de destino não for um servidor, ou se você não quiser especificar o modo de licenciamento.   

#### <a name="maximum-connections"></a>Número máximo de conexões
 Especifique o número máximo de conexões que estão disponíveis para este computador conforme indicado no contrato de licença.  

#### <a name="randomly-generate-the-local-administrator-password-and-disable-the-account-on-all-supported-platforms-recommended"></a>Gerar aleatoriamente a senha do administrador local e desabilitar a conta em todas as plataformas com suporte (recomendado)  
 Selecione esta opção para definir a senha de administrador local para uma cadeia de caracteres gerada aleatoriamente. Essa opção também desabilita a conta de administrador local em plataformas compatíveis com essa funcionalidade.  

#### <a name="enable-the-account-and-specify-the-local-administrator-password"></a>Ativar a conta e especificar a senha do administrador local  
 Selecione esta opção para habilitar a conta de administrador local usando a senha especificada. Insira a senha na linha **Senha** e confirme a senha na linha **Confirmar senha** .  

#### <a name="time-zone"></a>Fuso horário
 Especifique o fuso horário para o computador de destino. O valor capturado pela etapa da sequência de tarefas **Capturar Configurações do Windows** pode ser substituído por esse valor.  



##  <a name="BKMK_AutoApplyDrivers"></a> Drivers de Aplicação Automática  

 Use essa etapa para realizar a correspondência de drivers e instalá-los como parte da implantação do sistema operacional.  

 A etapa da sequência de tarefas **Aplicação automática de drivers** executa as seguintes ações:  

 1. Verifica o hardware e localiza as IDs de Plug-and-Play para todos os dispositivos presentes no sistema.  

 2. Envia a lista de dispositivos e das respectivas IDs de Plug-and-Play para o ponto de gerenciamento. O ponto de gerenciamento retorna uma lista de drivers compatíveis do catálogo de drivers para cada dispositivo de hardware. A lista inclui todos os drivers habilitados, independentemente do pacote de driver em que eles estão, incluindo drivers marcados com a categoria de driver especificada.  

 3. A sequência de tarefas seleciona o melhor driver para cada dispositivo de hardware. Esse driver é apropriado para o sistema operacional implantado e está em um ponto de distribuição acessível.  

 4. A sequência de tarefas baixa os drivers selecionados de um ponto de distribuição e prepara-os no sistema operacional de destino.  

    1. Ao usar uma imagem do sistema operacional, a sequência de tarefas coloca os drivers no repositório de drivers do sistema operacional.  

    2. Ao usar um pacote de atualização do sistema operacional como uma fonte de instalação original, a sequência de tarefas configurará a Instalação do Windows com o local dos drivers.  

 5.  Durante a etapa **Instalar o Windows e o ConfigMgr** na sequência de tarefas, a Instalação do Windows encontra os drivers preparados por essa etapa.  


 > [!IMPORTANT]  
 >  A mídia autônoma não pode usar a etapa **Aplicar Drivers Automaticamente**. A sequência de tarefas não tem conexão com o site do Configuration Manager neste cenário.  

 Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada no sistema operacional completo.

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [OSDAutoApplyDriverBestMatch](/sccm/osd/understand/task-sequence-variables#OSDAutoApplyDriverBestMatch)  
 - [OSDAutoApplyDriverCategoryList](/sccm/osd/understand/task-sequence-variables#OSDAutoApplyDriverCategoryList)  
 - [SMSTSDriverRequestConnectTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestConnectTimeOut)  
 - [SMSTSDriverRequestReceiveTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestReceiveTimeOut)  
 - [SMSTSDriverRequestResolveTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestResolveTimeOut)  
 - [SMSTSDriverRequestSendTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestSendTimeOut)  


 Para adicionar esta etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Drivers** e selecione **Aplicar Drivers Automaticamente**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="install-only-the-best-matched-compatible-drivers"></a>Instalar apenas a melhor correspondência de drivers compatíveis
 Especifica que a etapa de sequência de tarefas instala apenas o melhor driver correspondente a cada dispositivo de hardware detectado.  

#### <a name="install-all-compatible-drivers"></a>Instalar todos os drivers compatíveis
 A sequência de tarefas instala todos os drivers compatíveis para cada dispositivo de hardware detectado. A Instalação do Windows escolhe então o melhor driver. Esta opção ocupa mais espaço em disco e largura de banda da rede. A sequência de tarefas baixa mais drivers, mas o Windows pode selecionar um driver melhor.  

#### <a name="consider-drivers-from-all-categories"></a>Considerar drivers de todas as categorias
 A sequência de tarefas pesquisa todas as categorias de driver disponíveis para os drivers de dispositivo apropriados.  

#### <a name="limit-driver-matching-to-only-consider-drivers-in-selected-categories"></a>Limitar os drivers correspondentes considerados a apenas drivers em categorias selecionadas
 A sequência de tarefas pesquisa todas as categorias de driver especificadas para os drivers de dispositivo apropriados.  

#### <a name="do-unattended-installation-of-unsigned-drivers-on-versions-of-windows-where-this-is-allowed"></a>Faça uma instalação autônoma de drivers não assinados nas versões do Windows em que isso é permitido
 Essa opção permite que o Windows instale drivers sem uma assinatura digital.   

 > [!IMPORTANT]  
 >  Essa opção não se aplica aos sistemas operacionais em que a política de assinatura de driver não pode ser configurada.  



##  <a name="BKMK_CaptureNetworkSettings"></a> Capturar configurações da rede  

 Use esta etapa para capturar as configurações de rede da Microsoft no computador que executa a sequência de tarefas. A sequência de tarefas salva essas configurações em variáveis de sequência de tarefas. Essas configurações substituem as configurações padrão definidas na etapa **Aplicar Configurações de Rede**.  

 Essa etapa de sequência de tarefas é executada somente no sistema operacional completo. Ela não é executada no Windows PE.  

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [OSDMigrateAdapterSettings](/sccm/osd/understand/task-sequence-variables#OSDMigrateAdapterSettings)  
 - [OSDMigrateNetworkMembership](/sccm/osd/understand/task-sequence-variables#OSDMigrateNetworkMembership)  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Configurações** e selecione **Capturar Configurações de Rede**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="migrate-domain-and-workgroup-membership"></a>Migrar a associação de domínio e grupo de trabalho 
 Captura as informações de associação de domínio e grupo de trabalho do computador de destino.  

#### <a name="migrate-network-adapter-configuration"></a>Migrar a configuração do adaptador de rede
 Captura a configuração do adaptador de rede do computador de destino. Ele captura as seguintes informações: 
 - Configurações globais de rede  
 - Número de adaptadores  
 - As configurações de rede a seguir associadas a cada adaptador: DNS, WINS, IP e filtros de porta



##  <a name="BKMK_CaptureOperatingSystemImage"></a> Capturar imagem do sistema operacional  

 Essa etapa captura uma ou mais imagens de um computador de referência. A sequência de tarefas cria um arquivo de imagem do Windows (.wim) no compartilhamento de rede especificado. Em seguida, use o assistente **Adicionar Pacote de Imagem de Sistema Operacional** para importar esta imagem para o Configuration Manager para que ele possa ser usado para implantações de sistema operacional baseadas em imagem.  

 O Configuration Manager captura cada volume (unidade) no computador de referência para uma imagem separada dentro do arquivo .wim. Se o computador de referência tiver vários volumes, o arquivo .wim resultante conterá uma imagem separada para cada volume. Esta etapa captura apenas os volumes formatados como NTFS ou FAT32. Ela ignora os volumes com outros formatos, e os volumes USB.  

 O sistema operacional instalado no computador de referência deve ser uma versão do Windows compatível com o Configuration Manager. Use a ferramenta SysPrep para preparar o sistema operacional no computador de referência. O volume do sistema operacional instalado e o volume de inicialização devem ser o mesmo volume.  

 Especifique uma conta com permissões de gravação para o compartilhamento de rede selecionado. Para saber mais sobre a conta de imagem do sistema operacional de captura, consulte [Contas](/sccm/core/plan-design/hierarchy/accounts#capture-operating-system-image-account).

 Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada no sistema operacional completo. 

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [OSDCaptureAccount](/sccm/osd/understand/task-sequence-variables#OSDCaptureAccount)  
 - [OSDCaptureAccountPassword](/sccm/osd/understand/task-sequence-variables#OSDCaptureAccountPassword)  
 - [OSDCaptureDestination](/sccm/osd/understand/task-sequence-variables#OSDCaptureDestination)  
 - [OSDImageCreator](/sccm/osd/understand/task-sequence-variables#OSDImageCreator)  
 - [OSDImageDescription](/sccm/osd/understand/task-sequence-variables#OSDImageDescription)  
 - [OSDImageVersion](/sccm/osd/understand/task-sequence-variables#OSDImageVersion)  
 - [OSDTargetSystemRoot](/sccm/osd/understand/task-sequence-variables#OSDTargetSystemRoot-input)  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Imagens** e selecione **Capturar Imagem do Sistema Operacional**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="target"></a>Destino  
 Caminho do sistema de arquivos até o local que o Configuration Manager usa ao armazenar a imagem capturada do sistema operacional.  

#### <a name="description"></a>Descrição  
 Uma descrição opcional definida pelo usuário da imagem capturada do sistema operacional que é armazenada no arquivo de imagem.  

#### <a name="version"></a>Version  
 Um número de versão opcional definido pelo usuário para atribuir à imagem capturada do sistema operacional. Esse valor pode ser qualquer combinação de letras e números. Ele é armazenado no arquivo de imagem.  

#### <a name="created-by"></a>Criado por  
 O nome opcional do usuário que criou a imagem do sistema operacional. Ele é armazenado no arquivo de imagem.  

#### <a name="capture-operating-system-image-account"></a>Capturar conta de imagem do sistema operacional  
 Insira a conta do Windows que tenha permissões para o compartilhamento de rede especificado. Clique em **Definir** para especificar o nome da conta do Windows.  



##  <a name="BKMK_CaptureUserState"></a> Capturar Estado do Usuário  

 Esta etapa usa a USMT (Ferramenta de Migração do Usuário) para capturar o estado do usuário e configurações do computador que executa a sequência de tarefas. Essa etapa de sequência de tarefas é usada em conjunto com a etapa da sequência de tarefas **Restaurar o estado do usuário** . Esta etapa sempre criptografa o armazenamento de estado do USMT usando uma chave de criptografia gerada e gerenciada pelo Configuration Manager.  

 Para mais informações sobre como gerenciar o estado do usuário ao implantar sistemas operacionais, confira [Gerenciar o estado do usuário](/sccm/osd/get-started/manage-user-state).  

 Se você quiser salvar e restaurar configurações de estado do usuário de um ponto de migração de estado, use essa etapa com as etapas **Solicitar Repositório de Estado** e **Liberar Repositório de Estado**.  

 Essa etapa fornece controle sobre um subconjunto limitado das opções da USMT mais usadas. Especifique outras opções de linha de comando usando a variável de sequência de tarefas **OSDMigrateAdditionalCaptureOptions**.  

 Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada no sistema operacional completo.   

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [_OSDMigrateUsmtPackageID](/sccm/osd/understand/task-sequence-variables#OSDMigrateUsmtPackageID)  
 - [OSDMigrateAdditionalCaptureOptions](/sccm/osd/understand/task-sequence-variables#OSDMigrateAdditionalCaptureOptions)  
 - [OSDMigrateConfigFiles](/sccm/osd/understand/task-sequence-variables#OSDMigrateConfigFiles)  
 - [OSDMigrateContinueOnLockedFiles](/sccm/osd/understand/task-sequence-variables#OSDMigrateContinueOnLockedFiles)  
 - [OSDMigrateEnableVerboseLogging](/sccm/osd/understand/task-sequence-variables#OSDMigrateEnableVerboseLogging)  
 - [OSDMigrateMode](/sccm/osd/understand/task-sequence-variables#OSDMigrateMode)  
 - [OSDMigrateSkipEncryptedFiles](/sccm/osd/understand/task-sequence-variables#OSDMigrateSkipEncryptedFiles)  
 - [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Estado de Usuário** e selecione **Capturar Estado de Usuário**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="user-state-migration-tool-package"></a>Pacote da ferramenta de migração de estado do usuário
 Especifique o pacote que contém a USMT (Ferramenta de Migração do Usuário). A sequência de tarefas usa esta versão da USMT para capturar o estado do usuário e as configurações. Este pacote não exige um programa. Especifique um pacote que contém a versão de 32 bits ou 64 bits do USMT. A arquitetura da USMT varia de acordo com a arquitetura do sistema operacional do qual a sequência de tarefas está realizando a captura de estado.  

#### <a name="capture-all-user-profiles-with-standard-options"></a>Capturar todos os perfis de usuário com opções padrão
 Migre todas as informações de perfil do usuário. Essa opção é o padrão.  

 Se você selecionar essa opção, mas não selecionar **Restaurar perfis de usuário do computador local** na etapa **Restaurar Estado do Usuário**, a sequência de tarefas falhará. O Configuration Manager não pode migrar as novas contas sem atribuir senhas a elas. 

 Quando você usa a opção **Instalar um pacote de imagem existente** do assistente **Nova Sequência de Tarefas**, a sequência de tarefas resultante assume como padrão **Capturar todos os perfis de usuário com opções padrão**. Essa sequência de tarefas padrão não seleciona a opção de **Restaurar perfis de usuário do computador local**, ou as contas de usuário de fora do domínio.  

 Selecione **Restaurar perfis de usuário do computador local** e forneça uma senha para a conta a ser migrada. Em uma sequência de tarefas criadas manualmente, essa configuração é encontrada na etapa **Restaurar estado do usuário**. Em uma sequência de tarefas criada pelo assistente **Nova sequência de tarefas** , essa configuração se encontra na página do assistente **Restaurar arquivos e configurações do usuário** .  

 Se você não tem nenhuma conta de usuário local, essa configuração não se aplica.  

#### <a name="customize-how-user-profiles-are-captured"></a>Personalizar como os perfis de usuário são capturados
 Selecione esta opção para especificar um arquivo de perfil personalizado para migração. Clique em **Arquivos** para selecionar os arquivos de configuração do USMT a serem usados com esta etapa. Especifique um arquivo .xml personalizado que contenha regras que definam os arquivos de estado do usuário para migrar.  

#### <a name="click-here-to-select-configuration-files"></a>Clique aqui para selecionar os arquivos de configuração
 Selecione esta opção para selecionar os arquivos de configuração do pacote da USMT que deseja usar para capturar os perfis de usuário. Clique no botão **Arquivos** para abrir a caixa de diálogo **Arquivos de configuração** . Para especificar um arquivo de configuração, insira o nome do arquivo na linha **Nome do arquivo** e clique no botão **Adicionar** .  

#### <a name="enable-verbose-logging"></a>Habilitar o log detalhado
 Habilite esta opção para gerar informações de arquivo de log mais detalhadas. Durante a captura de estado, a sequência de tarefas gera por padrão o **ScanState.log** na pasta de log de sequência de tarefas, `%WinDir%\ccm\logs`.   

#### <a name="skip-files-using-encrypted-file-system"></a>Ignorar arquivos usando o sistema de arquivos criptografados
 Habilite esta opção para ignorar a captura de arquivos criptografados com o EFS (sistema de arquivos com criptografia). Esses arquivos incluem arquivos de perfil do usuário. Dependendo do sistema operacional e versões do USMT, arquivos criptografados podem não ser lidos após a restauração. Para obter mais informações, consulte a documentação do USMT.  

#### <a name="copy-by-using-file-system-access"></a>Copiar usando o acesso do sistema de arquivos
 Habilite esta opção especificar qualquer uma das seguintes configurações:  

 - **Continuar se não for possível capturar alguns arquivos**: habilite essa configuração para continuar o processo de migração mesmo que não seja possível capturar alguns arquivos. Se você desabilitar essa opção e não conseguir capturar um arquivo, essa etapa da sequência de tarefas falhará. Essa opção é habilitada por padrão.  

 - **Capturar localmente usando links em vez de copiar arquivos**: habilite essa configuração para usar links físicos NTFS para capturar arquivos.  

     Para saber mais sobre como migrar dados usando links físicos, consulte [Repositório de migração de link físico](https://docs.microsoft.com/windows/deployment/usmt/usmt-hard-link-migration-store).  

 - **Capturar em modo offline (somente Windows PE)**: habilite essa configuração para capturar o estado de usuário no Windows PE em vez do sistema operacional completo.  

#### <a name="capture-by-using-volume-copy-shadow-services-vss"></a>Capturar usando o VSS (Serviços de Cópias de Sombra de Volume)
 Essa opção permite capturar arquivos mesmo se eles estiverem bloqueados para edição por outro aplicativo.  



##  <a name="BKMK_CaptureWindowsSettings"></a> Capturar Configurações do Windows  

 Use esta etapa para capturar as configurações do Windows no computador que executa a sequência de tarefas. A sequência de tarefas salva essas configurações em variáveis de sequência de tarefas. Essas configurações capturadas substituem as configurações padrão definidas na etapa **Aplicar Configurações do Windows**.  

 Essa etapa da sequência de tarefas é executada no sistema operacional completo ou no Windows PE.  

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [OSDComputerName](/sccm/osd/understand/task-sequence-variables#OSDComputerName-output)  
 - [OSDMigrateComputerName](/sccm/osd/understand/task-sequence-variables#OSDMigrateComputerName)  
 - [OSDMigrateRegistrationInfo](/sccm/osd/understand/task-sequence-variables#OSDMigrateRegistrationInfo)  
 - [OSDMigrateTimeZone](/sccm/osd/understand/task-sequence-variables#OSDMigrateTimeZone)  
 - [OSDRegisteredOrgName](/sccm/osd/understand/task-sequence-variables#OSDRegisteredOrgName-output)  
 - [OSDTimeZone](/sccm/osd/understand/task-sequence-variables#OSDTimeZone-output)  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Configurações** e selecione **Capturar Configurações do Windows**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="migrate-computer-name"></a>Migrar o nome do computador
 Capture o nome do computador NetBIOS do computador.  

#### <a name="migrate-registered-user-and-organization-names"></a>Migrar os nomes de usuário e organização registrados
 Capture os nomes de usuário e de organização registrados do computador.  

#### <a name="migrate-time-zone"></a>Migrar o fuso horário
 Capture a configuração de fuso horário no computador.  



##  <a name="BKMK_CheckReadiness"></a> Verificar Preparação  

 Use esta etapa para verificar se o computador de destino atende às condições de pré-requisitos de implantação especificadas.  

 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e selecione **Verificar Preparação**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="ensure-minimum-memory-mb"></a>Verifique o mínimo de memória (MB)
 Verifique se a quantidade de memória, em megabytes (MB), atende ou excede o valor especificado. A etapa habilita essa configuração por padrão.  

#### <a name="ensure-minimum-processor-speed-mhz"></a>Verificar velocidade mínima de processador (MHz)  
 Verifique se a velocidade do processador, em mega-hertz (MHz), atende ou excede o valor especificado. A etapa habilita essa configuração por padrão.  

#### <a name="ensure-minimum-free-disk-space-mb"></a>Verificar o espaço livre em disco mínimo (MB)
 Verificar se a quantidade de espaço livre em disco, em megabytes (MB), atende ou excede o valor especificado.  

#### <a name="ensure-current-os-to-be-refreshed-is"></a>verificar qual é o SO atual a ser atualizado
 Verifique se o sistema operacional instalado no computador de destino atende o requisito especificado. Por padrão, a etapa define essa configuração como **CLIENTE**.  


### <a name="options"></a>Opções

 > [!NOTE]  
 > Se você habilitar a configuração **Continuar em caso de erro** na guia **Opções** desta etapa, ele registra apenas os resultados da verificação de preparação. Se uma verificação falhar, a sequência de tarefas não será interrompida.  



##  <a name="BKMK_ConnectToNetworkFolder"></a> Conectar à Pasta de Rede  

 Use essa etapa para criar uma conexão a uma pasta de rede compartilhada.  

 Essa etapa da sequência de tarefas é executada no sistema operacional completo ou no Windows PE.  

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [SMSConnectNetworkFolderAccount](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderAccount)  
 - [SMSConnectNetworkFolderDriveLetter](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderDriveLetter)  
 - [SMSConnectNetworkFolderPassword](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderPassword)  
 - [SMSConnectNetworkFolderPath](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderPath)  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e selecione **Conectar-se à Pasta de Rede**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="path"></a>Caminho  
 Clique em **Procurar** para especificar o caminho da pasta de rede. Use o formato `\\server\share`.

#### <a name="drive"></a>Unidade  
 Selecione a letra da unidade local para atribuir a esta conexão. 

#### <a name="account"></a>Conta 
 Clique em **Definir** para especificar a conta de usuário com permissões para se conectar a esta pasta de rede. Para saber mais sobre a conta de conexão da pasta de rede da sequência de tarefas, confira [Contas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-network-folder-connection-account).



##  <a name="BKMK_DisableBitLocker"></a> Desabilitar BitLocker  

 Use esta etapa para desabilitar a criptografia BitLocker na unidade do sistema operacional atual ou em uma unidade específica. Essa ação deixa os protetores de chave visíveis em texto não criptografado no disco rígido. Ela não descriptografa o conteúdo da unidade. Essa ação é concluída quase instantaneamente.  

 > [!NOTE]  
 >  A criptografia de unidade de disco BitLocker fornece criptografia de baixo nível do conteúdo de um volume de disco.  

 Se você tiver várias unidades criptografadas, desabilite o BitLocker nas unidades de dados antes de desabilitar o BitLocker na unidade do sistema operacional.  

 Esta etapa é executada somente no sistema operacional completo. Ela não é executada no Windows PE.  

 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Discos** e selecione **Desabilitar BitLocker**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="current-operating-system-drive"></a>Unidade do sistema operacional atual
 Desabilita o BitLocker na unidade do sistema operacional atual.  

#### <a name="specific-drive"></a>Unidade específica  
 Desabilita o BitLocker em uma unidade específica. Use a lista suspensa para especificar a unidade em que o BitLocker será desabilitado.  



##  <a name="BKMK_DownloadPackageContent"></a> Baixar o conteúdo do pacote  

 Use essa etapa para baixar qualquer um dos seguintes tipos de pacote:  

 - Imagens do sistema operacional  
 - Pacotes de atualização do sistema operacional  
 - Pacotes de driver  
 - Pacotes  
 - Imagens de inicialização  


 Esta etapa funciona bem em uma sequência de tarefas para atualizar um sistema operacional nos seguintes cenários:  

 - Para usar uma sequência de tarefas de atualização única que pode funcionar com plataformas x86 e x64. Inclua duas etapas **Baixar Conteúdo do Pacote** no grupo **Preparar Upgrade**. Especificar as condições na guia **Opções** para detectar a arquitetura do cliente e baixar apenas o pacote de atualização do sistema operacional apropriado. Configure cada etapa **Baixar Conteúdo do Pacote** para usar a mesma variável. Use a variável para o caminho de mídia na etapa **Atualizar Sistema Operacional**.  

 - Para baixar um pacote de drivers aplicáveis dinamicamente, use duas etapas **Baixar Conteúdo do Pacote** com condições para detectar o tipo de hardware apropriado para cada pacote de drivers. Configure cada etapa **Baixar Conteúdo do Pacote** para usar a mesma variável. Use a variável para o valor **Conteúdo de teste** na seção Drivers da etapa **Atualizar sistema operacional**.  


 > [!NOTE]    
 > Quando você implanta uma sequência de tarefas que contém essa etapa, não selecione **Baixar todo o conteúdo localmente antes de iniciar a sequência de tarefas** ou **Acessar conteúdo diretamente de um ponto de distribuição** para **Opções de implantação** na página **Pontos de Distribuição** do Assistente de Implantação de Software.  

 Essa etapa é executada no sistema operacional completo ou no Windows PE. A opção para salvar o pacote no cache do cliente do Configuration Manager não tem suporte no Windows PE.

 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Software** e selecione **Baixar Conteúdo do Pacote**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="select-package"></a>Selecionar pacote  
 Clique no ícone para selecionar o pacote que será baixado. Depois de selecionar um pacote, clique no ícone novamente para escolher outro pacote.  

#### <a name="place-into-the-following-location"></a>Coloque no seguinte local
 Escolha a opção para salvar o pacote em um dos seguintes locais:  

 - **Diretório de trabalho da sequência de tarefas**: esse local também é conhecido como o cache de sequência de tarefas.  

 - **Cache do cliente do Configuration Manager**: use esta opção para armazenar o conteúdo no cache do cliente. Por padrão, esse caminho é `%WinDir%\ccmcache`.  

 - **Caminho personalizado**: primeiro, o mecanismo de sequência de tarefas faz o download do pacote no diretório de trabalho da sequência de tarefas. Depois, move o conteúdo até o caminho que você especificar. O mecanismo de sequência de tarefas agrega o caminho ao ID do pacote.  

#### <a name="save-path-as-a-variable"></a>Salvar caminho como uma variável
 Salve o caminho do pacote em uma variável de sequência de tarefas personalizada. Depois, use essa variável em outra etapa de sequência de tarefas. 

 O Configuration Manager adiciona um sufixo numérico ao nome da variável. Por exemplo, especifique uma variável de `%MyContent%` como uma variável personalizada. Essa é a raiz de onde a sequência de tarefas armazena todo o conteúdo referenciado para esta etapa. Esse conteúdo pode conter vários pacotes. Quando você fizer referência à variável, adicione um sufixo numérico. Para o primeiro pacote, consulte `%MyContent01%`. Quando você fizer referência à variável em etapas subsequentes, tais como **Atualizar Sistema Operacional**, use `%MyContent02%` ou `%MyContent03%`, em que o número corresponde à ordem na qual a etapa **Baixar Conteúdo do Pacote** lista os pacotes.  

#### <a name="if-a-package-download-fails-continue-downloading-other-packages-in-the-list"></a>Se o download do pacote falhar, continue o download de outros pacotes na lista
 Se a sequência de tarefas falhar ao baixar um pacote, ela começará a baixar o próximo pacote na lista.  



##  <a name="BKMK_EnableBitLocker"></a> Habilitar BitLocker  

 Use esta etapa para habilitar a criptografia BitLocker em pelo menos duas partições no disco rígido. A primeira partição ativa contém o código de inicialização do Windows. Outra partição contém o sistema operacional. A partição de inicialização deve permanecer descriptografada.  

 Use a etapa **Pré-provisionar o BitLocker** para habilitar o BitLocker em uma unidade no Windows PE. Para mais informações, consulte [Pré-provisionar o BitLocker](#BKMK_PreProvisionBitLocker).  

 > [!NOTE]  
 >  A criptografia de unidade de disco BitLocker fornece criptografia de baixo nível do conteúdo de um volume de disco.  

 Esta etapa é executada somente no sistema operacional completo. Ela não é executada no Windows PE.   

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [OSDBitLockerRecoveryPassword](/sccm/osd/understand/task-sequence-variables#OSDBitLockerRecoveryPassword)  
 - [OSDBitLockerStartupKey](/sccm/osd/understand/task-sequence-variables#OSDBitLockerStartupKey)  


 Quando você especificar **Somente TPM**, **TPM e chave de inicialização em USB** ou **TPM e PIN**, o TPM (Trusted Platform Module) deverá estar no seguinte estado antes de executar a etapa **Habilitar BitLocker**:  
 - Habilitada  
 - Ativado  
 - Propriedade permitida  


 Esta etapa conclui qualquer inicialização restante do TPM. As etapas restantes não exigem a presença física ou reinicializações. As etapas a seguir de inicialização de TPM restantes são concluídas de modo transparente pela etapa **Habilitar BitLocker**, se for necessário:  
 - Criar um par de chave de endosso  
 - Criar valor de autorização do proprietário e caução para o Active Directory, que devem ser estendidos para oferecer suporte a esse valor  
 - Apropriar-se  
 - Crie a chave de raiz de armazenamento ou redefina-a se existir, mas for incompatível  

   
 Se você deseja que a sequência de tarefas aguarde a etapa **Habilitar BitLocker** para concluir o processo de criptografia de unidade, selecione a opção **Aguardar**. Se você não selecionar a opção **Aguardar**, o processo de criptografia de unidade ocorrerá em segundo plano. A sequência de tarefas continua imediatamente para a próxima etapa.  

 O BitLocker pode ser usado para criptografar várias unidades em um sistema de computador, tanto unidades do sistema operacional quanto de dados. Para criptografar uma unidade de dados, primeiro criptografe a unidade do sistema operacional e conclua o processo de criptografia. Esse requisito existe porque a unidade do sistema operacional armazena os protetores de chave para as unidades de dados. Se você criptografar as unidades do sistema operacional e de dados na mesma sequência de tarefas, selecione a opção **Aguardar** na etapa **Habilitar BitLocker** para a unidade do sistema operacional.  

 Se o disco rígido já estiver criptografado, mas o BitLocker estiver desabilitado, a etapa **Habilitar BitLocker** habilitará novamente o protetor de chave e será concluída rapidamente. Nova criptografia da unidade de disco rígida não é necessária neste caso.  

 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Discos** e selecione **Habilitar BitLocker**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="choose-the-drive-to-encrypt"></a>Selecione a unidade para criptografar
 Especifica a unidade para criptografar. Para criptografar a unidade do sistema operacional atual, selecione **Unidade atual do sistema operacional**. Depois, configure uma das seguintes opções para gerenciamento de chave:  

 - **Somente TPM**: selecione esta opção para usar somente o TPM (Trusted Platform Module).  

 - **Chave de inicialização somente em USB**: selecione esta opção para usar uma chave de inicialização armazenada em uma unidade flash USB. Quando você seleciona essa opção, o BitLocker bloqueia o processo normal de inicialização até que um dispositivo USB que contém uma chave de inicialização do BitLocker é anexado ao computador.  

 - **TPM e chave de inicialização em USB**: selecione esta opção para usar o TPM e uma chave de inicialização armazenada em uma unidade flash USB. Quando você seleciona essa opção, o BitLocker bloqueia o processo normal de inicialização até que um dispositivo USB que contém uma chave de inicialização do BitLocker é anexado ao computador.  

 - **TPM e PIN**: selecione esta opção para usar o TPM e um PIN (número de identificação pessoal). Quando você seleciona essa opção, o BitLocker bloqueia o processo normal de inicialização até que o usuário forneça o PIN.  


 Para criptografar uma unidade de dados específica que não seja do sistema operacional, selecione **Unidade específica**. Em seguida, selecione a unidade na lista.  

#### <a name="use-full-disk-encryption"></a>Usar criptografia de disco cheio
 <!--SCCMDocs-pr issue 2671--> Por padrão, essa etapa só criptografa o espaço usado na unidade. Esse comportamento padrão é recomendável, pois é mais rápido e eficiente. A partir da versão 1806, se a sua organização exigir a criptografia de toda a unidade durante a instalação, habilite esta opção. A Instalação do Windows aguarda toda a unidade estar criptografada, o que leva muito tempo, especialmente em unidades grandes. 

#### <a name="choose-where-to-create-the-recovery-key"></a>Escolha onde criar a chave de recuperação
 Para especificar que o BitLocker deve criar a senha de recuperação e fazer caução dela no Active Directory, selecione **No Active Directory**. Essa opção exige que você estenda o Active Directory para caução de chave do BitLocker. O BitLocker pode salvar as informações de recuperação associadas no Active Directory. Selecione **Não criar a chave de recuperação** para não criar uma senha. Recomendamos a opção de criação de uma senha.  

#### <a name="wait-for-bitlocker-to-complete-the-drive-encryption-process-on-all-drives-before-continuing-task-sequence-execution"></a>Aguarde o BitLocker concluir o processo de criptografia de unidade em todas as unidades antes de continuar a execução da sequência de tarefas
 Selecione esta opção para permitir que a criptografia de unidade de disco BitLocker seja concluída antes de executar a próxima etapa na sequência de tarefas. Se você selecionar essa opção, todo o volume de disco será criptografado pelo BitLocker antes de o usuário entrar no computador.  

 O processo de criptografia pode levar horas para ser concluído quando um disco rígido grande está sendo criptografado. Não selecionar esta opção permite que a sequência de tarefas continue imediatamente.  



##  <a name="BKMK_FormatandPartitionDisk"></a> Formatar e Particionar Disco  

 Use esta etapa para formatar e particionar um disco especificado no computador de destino.  

 > [!IMPORTANT]  
 >  Todas as configurações que você especificar para esta etapa serão aplicadas a um único disco. Para formatar e particionar outro disco no computador de destino, você deve adicionar uma etapa **Formatar e Particionar Disco** adicional à sequência de tarefas.  

 Esta etapa é executada somente no Windows PE. Ela não é executada no sistema operacional completo.  

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [OSDDiskIndex](/sccm/osd/understand/task-sequence-variables#OSDDiskIndex)  
 - [OSDGPTBootDisk](/sccm/osd/understand/task-sequence-variables#OSDGPTBootDisk)  
 - [OSDPartitions](/sccm/osd/understand/task-sequence-variables#OSDPartitions)  
 - [OSDPartitionStyle](/sccm/osd/understand/task-sequence-variables#OSDPartitionStyle)  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Discos** e selecione **Formatar e Particionar Disco**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="disk-number"></a>Número do disco
 O número do disco físico a ser formatado. O número é baseado na ordem de enumeração de disco do Windows.  

#### <a name="disk-type"></a>Tipo de disco
 O tipo de disco a ser formatado. Há duas opções para selecionar na lista suspensa: 
 - **Padrão (MBR)**: Registro Mestre de Inicialização  
 - **GGT**: tabela de partição GUID  


 > [!NOTE]  
 >  Se você alterar o tipo de disco de **Padrão (MBR)** para **GPT** e o layout da partição contiver uma partição estendida, a sequência de tarefas removerá todas as partições estendidas e lógicas do layout. O editor de sequência de tarefas solicita que você confirme esta ação antes de alterar o tipo de disco.  
   
#### <a name="volume"></a>Volume
 Informações específicas sobre a partição ou volume que a sequência de tarefas cria, incluindo os seguintes atributos:  
 - Name  
 - Espaço restante em disco  


 Para criar uma nova partição, clique em **Novo** para abrir a caixa de diálogo **Propriedades da partição** . Especifique o tipo e o tamanho da partição, bem como se ela é uma partição de inicialização. Para modificar uma partição existente, clique na partição a ser modificada e no botão **Propriedades**. Para obter mais informações sobre como configurar partições de disco rígido, consulte os seguintes artigos:  

 - [Partições de disco rígido baseadas em UEFI/GGT](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions)  
 - [Partições de disco rígido baseadas em BIOS/MBR](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-biosmbr-based-hard-drive-partitions)  


 Para excluir uma partição, selecione a partição e clique em **Excluir**.  



##  <a name="BKMK_InstallApplication"></a> Instalar Aplicativo  

 Esta etapa instala os aplicativos especificados, ou então um conjunto de aplicativos definidos por uma lista dinâmica de variáveis de sequência de tarefas. Quando a sequência de tarefas executar essa etapa, a instalação do aplicativo começará imediatamente sem esperar um intervalo de sondagem de política.  

 O aplicativo deve atender aos seguintes critérios:  

 - O aplicativo deve ter um tipo de implantação do **Windows Installer** ou do instalador de **Script**. Não há suporte para tipos de implantação do pacote do aplicativo Windows (arquivo .appx).  

 - Ele deve executar sob a conta Sistema Local e não a conta de usuário.  

 - Ele não deve interagir com a área de trabalho. O programa deve ser executado silenciosamente ou em um modo autônomo.  

 - Ele não deve iniciar uma reinicialização por conta própria. O aplicativo deve solicitar uma reinicialização usando o código de reinicialização padrão, 3010. Esse comportamento assegura a manipulação correta da reinicialização por essa etapa. Se o aplicativo retornar um código de saída 3010, o mecanismo da sequência de tarefas reiniciará o computador. Após a reinicialização, a sequência de tarefas continua automaticamente.  


 Quando essa etapa for executada, o aplicativo verificará a aplicabilidade das regras de requisito e o método de detecção nos tipos de implantação. Com base nos resultados dessa verificação, o aplicativo instala o tipo de implantação aplicável. Se um tipo de implantação contém dependências, o tipo de implantação dependente é avaliado e instalado como parte dessa etapa. Dependências de aplicativos não têm suporte para mídia autônoma.  

 > [!NOTE]  
 >  Para instalar um aplicativo que substitui outro, os arquivos de conteúdo para o aplicativo substituído devem estar disponíveis. Caso contrário, essa etapa de sequência de tarefas falhará. Por exemplo, o Microsoft Visio 2010 é instalado em um cliente ou em uma imagem capturada. Quando a etapa **Instalar Aplicativo** instala o Microsoft Visio 2013, os arquivos de conteúdo para o Microsoft Visio 2010 (aplicativo substituído) devem estar disponíveis em um ponto de distribuição. Se o Microsoft Visio não é instalado em um cliente ou imagem capturada, a sequência de tarefas instala o Microsoft Visio 2013 sem verificar os arquivos de conteúdo do Microsoft Visio 2010.  

 > [!NOTE]  
 > Se o cliente não conseguir recuperar a lista de ponto de gerenciamento dos serviços de localização, use as variáveis de sequência de tarefas **SMSTSMPListRequestTimeoutEnabled** e **SMSTSMPListRequestTimeout**. Essas variáveis especificam quantos milissegundos uma sequência de tarefas espera antes de tentar novamente a instalação de um aplicativo. Para saber mais, confira [Variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables).

 Essa etapa de sequência de tarefas é executada somente no sistema operacional completo. Ela não é executada no Windows PE.  

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [_TSAppInstallStatus](/sccm/osd/understand/task-sequence-variables#TSAppInstallStatus)  
 - [SMSTSMPListRequestTimeoutEnabled](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeoutEnabled)  
 - [SMSTSMPListRequestTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeout)  
 - [TSErrorOnWarning](/sccm/osd/understand/task-sequence-variables#TSErrorOnWarning)  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Software** e selecione **Instalar Aplicativo**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="install-the-following-applications"></a>Instalar os seguintes aplicativos
 A sequência de tarefas instala esses aplicativos na ordem especificada.  

 O Configuration Manager filtra qualquer aplicativo desabilitado ou aplicativos com as seguintes configurações:  

 - Somente quando um usuário tiver efetuado logon  
 - Executar com direitos de usuário  


 Esses aplicativos não aparecem na caixa de diálogo **Selecione o aplicativo a ser instalado**.

#### <a name="install-applications-according-to-dynamic-variable-list"></a>Instalar aplicativos de acordo com a lista de variável dinâmica
 A sequência de tarefas instala os aplicativos que usam este nome de variável de base. O nome de variável de base é para um conjunto de variáveis de sequência de tarefas definido para uma coleção ou computador. Essas variáveis especificam os aplicativos que a sequência de tarefas instala para essa coleção ou computador. Cada nome de variável consiste em seu nome de base comum e um sufixo numérico, começando com 01. O valor de cada variável deve conter o nome do aplicativo e nada mais.  

 Para que a sequência de tarefas instale aplicativos usando uma lista de variáveis dinâmicas, habilite a seguinte configuração na guia **Geral** da caixa de diálogo **Propriedades** do aplicativo: **Permitir que este aplicativo seja instalado na ação de sequência de tarefas Instalar aplicativo em vez de implantar manualmente**.  

 > [!NOTE]  
 >  Você não pode instalar aplicativos usando uma lista dinâmica de variável para implantações de mídia autônoma.  

 Por exemplo, para instalar um único aplicativo usando uma variável de sequência de tarefas chamada AA01, especifique a seguinte variável:  

 |Nome da variável|Valor da variável|  
 |-------------------|--------------------|  
 |AA01|Microsoft Office|  

 Para instalar dois aplicativos, especifique estas variáveis:  

 |Nome da variável|Valor da variável|  
 |-------------------|--------------------|  
 |AA01|Microsoft Lync|  
 |AA02|Microsoft Office|  

 As condições a seguir afetam os aplicativos instalados pela sequência de tarefas:  

 - Se o valor de uma variável contém todas as informações que não seja o nome do aplicativo. A sequência de tarefas não instala o aplicativo e prossegue.  

 - Se a sequência de tarefas não encontrar uma variável com o nome de base especificado e o sufixo "01", a sequência de tarefas não instalará nenhum aplicativo.  


 > [!Important]  
 > Esses valores diferenciam maiúsculas de minúsculas. Por exemplo, "instalar" é diferente de "Instalar". Caso precise alterar o valor, o Editor de Sequência de Tarefas não detecta alterações de maiúsculas e minúsculas. Faça outra edição simultânea, por exemplo, modifique a descrição da etapa.<!--509714-->   

#### <a name="if-an-application-fails-continue-installing-other-applications-in-the-list"></a>Se um aplicativo falhar, continue a instalar outros aplicativos na lista
 Essa configuração especifica que a etapa continuará quando a instalação de um aplicativo individual falhar. Se você especificar essa configuração, a sequência de tarefas continuará, independentemente de eventuais erros de instalação. Se você não especificar essa configuração e a instalação falhar, a etapa terminará imediatamente.  


### <a name="options"></a>Opções

 > [!NOTE]  
 > Quando você seleciona **Continuar em caso de erro** na guia **Opções** dessa etapa, a sequência de tarefas continua quando um aplicativo falha ao instalar. Quando você não habilita essa opção, a sequência de tarefas falha e não instala os aplicativos restantes.  

 Além das opções padrão, defina as seguintes configurações adicionais na guia **Opções** dessa etapa da sequência de tarefas:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Execute essa etapa novamente se o computador reiniciar inesperadamente
 Se uma das instalações do aplicativo reiniciar o computador inesperadamente, tente realizar essa etapa novamente. A etapa habilita essa configuração por padrão com duas novas tentativas. Você pode especificar de uma a cinco novas tentativas.  



##  <a name="BKMK_InstallPackage"></a> Instalar Pacote

 Use essa etapa para instalar um pacote de software como parte da sequência de tarefas. Quando essa etapa é executada, a instalação começa imediatamente sem esperar que um intervalo de sondagem de política.  

 O pacote deve atender aos seguintes critérios:  

 - Ele deve executar sob a conta Sistema Local e não uma conta de usuário.  

 - Ele não deve interagir com a área de trabalho. O programa deve ser executado silenciosamente ou em um modo autônomo.  

 - Ele não deve iniciar uma reinicialização por conta própria. O software deve solicitar uma reinicialização, usando o código de reinicialização padrão, 3010. Este comportamento garante que a sequência de tarefas manipule adequadamente a reinicialização. Se o software retornar um código de saída 3010, o mecanismo de sequência de tarefas reiniciará o computador. Após a reinicialização, a sequência de tarefas continua automaticamente.  


 Programas que usam a opção **Executar outro programa primeiro** para instalar um programa dependente não são suportados ao implantar um sistema operacional. Se você habilitar a opção de pacote **Executar outro programa primeiro** e o programa dependente já tiver executado no computador de destino, o programa dependente será executado e a sequência de tarefas continuará. No entanto, se o programa dependente ainda não tiver sido executado no computador de destino, a etapa de sequência de tarefas falhará.  

 > [!NOTE]  
 >  O site de administração central não tem as políticas de configuração de cliente necessárias para habilitar o agente de distribuição de software durante a sequência de tarefas. Quando você cria mídia autônoma para uma sequência de tarefas no site de administração central, e a sequência de tarefas inclui uma etapa **Instalar pacote** , o seguinte erro pode aparecer no arquivo CreateTsMedia.log:  
 >   
 >  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
 >   
 >  Para mídia autônoma que inclui uma etapa **Instalar Pacote**, crie a mídia autônoma em um site primário que tem o agente de distribuição de software habilitado. Como alternativa, adicione uma etapa **Executar Linha de Comando** após a etapa **Instalar o Windows e o ConfigMgr** e antes da primeira etapa **Instalar o Pacote**. A etapa **Executar Linha de Comando** executa como um comando WMIC para habilitar o agente de distribuição de software antes da primeira etapa **Instalar Pacote**. Use o seguinte comando na etapa **Executar Linha de Comando**:  
 >   
 >  `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
 >   
 >  Para mais informações sobre como criar mídia autônoma, confira [Create stand-alone media](/sccm/osd/deploy-use/create-stand-alone-media) (Criar mídia autônoma).  


 Essa etapa de sequência de tarefas é executada somente no sistema operacional completo. Ela não é executada no Windows PE.  

 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Software** e selecione **Instalar Pacote**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="install-a-single-software-package"></a>Instalar um único pacote de software
 Essa configuração especifica um pacote de software do Configuration Manager. A etapa aguarda a conclusão da instalação.  

#### <a name="install-software-packages-according-to-dynamic-variable-list"></a>Instalar os pacotes de software de acordo com a lista de variável dinâmica
 A sequência de tarefas instala os pacotes que usam este nome de variável de base. O nome de variável de base é para um conjunto de variáveis de sequência de tarefas definido para uma coleção ou computador. Essas variáveis especificam os pacotes que a sequência de tarefas instala para essa coleção ou computador. Cada nome de variável consiste em seu nome de base comum e um sufixo numérico, começando com 001. O valor de cada variável deve conter uma ID de pacote e o nome do software separados por dois-pontos.  

 Para que a sequência de tarefas instale o software usando uma lista de variáveis dinâmicas, habilite a seguinte configuração na guia **Avançado** das **Propriedades** do pacote: **Permitir que este programa seja instalado da sequência de tarefas de Pacote de Instalação sem ser implantado**.  

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

 - Se você não criar o valor de uma variável no formato correto ou não especificar um nome e uma ID do pacote válidos, a instalação do software falhará.  

 - Se a ID do pacote contiver caracteres minúsculos, a instalação do software falhará.  

 - Se a sequência de tarefas não encontrar uma variável com o nome de base especificado e o sufixo "001", a sequência de tarefas não instalará qualquer pacote. A sequência de tarefas continua.  


 > [!Important]  
 > Esses valores diferenciam maiúsculas de minúsculas. Por exemplo, "instalar" é diferente de "Instalar". Caso precise alterar o valor, o Editor de Sequência de Tarefas não detecta alterações de maiúsculas e minúsculas. Faça outra edição simultânea, por exemplo, modifique a descrição da etapa.<!--509714-->   

#### <a name="if-installation-of-a-software-package-fails-continue-installing-other-packages-in-the-list"></a>Se a instalação de um pacote de software falhar, continuar a instalar outros pacotes na lista
 Essa configuração especifica que a etapa continuará se a instalação de um pacote de software individual falhar. Se você especificar essa configuração, a sequência de tarefas continuará, independentemente de eventuais erros de instalação. Se você não especificar essa configuração e a instalação falhar, a etapa terminará imediatamente.  



##  <a name="BKMK_InstallSoftwareUpdates"></a> Instalar Atualizações de Software  

 Use esta etapa para instalar as atualizações de software no computador de destino. O computador de destino não é avaliado para atualizações de software aplicáveis até que essa etapa de sequência de tarefas seja executada. Nesse momento, o computador de destino é avaliado para atualizações de software como qualquer outro cliente do Configuration Manager. Para que essa etapa instale atualizações de software, implante primeiro as atualizações em uma coleção da qual o computador de destino é membro.  

 > [!IMPORTANT]  
 > Para obter o desempenho ideal, instale a versão mais recente do Windows Update Agent.  

 Essa etapa de sequência de tarefas é executada somente no sistema operacional completo. Ela não é executada no Windows PE. 

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [SMSInstallUpdateTarget](/sccm/osd/understand/task-sequence-variables#SMSInstallUpdateTarget)  
 - [SMSTSMPListRequestTimeoutEnabled](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeoutEnabled)  
 - [SMSTSMPListRequestTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeout)  
 - [SMSTSSoftwareUpdateScanTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSSoftwareUpdateScanTimeout)  
 - [SMSTSWaitForSecondReboot](/sccm/osd/understand/task-sequence-variables#SMSTSWaitForSecondReboot)  


 > [!NOTE]  
 > Se o cliente não conseguir recuperar a lista de ponto de gerenciamento dos serviços de localização, use as variáveis **SMSTSMPListRequestTimeoutEnabled** e **SMSTSMPListRequestTimeout**. Essas variáveis especificam quantos milissegundos uma sequência de tarefas espera antes de tentar novamente a instalação de um aplicativo ou atualização de software. Para saber mais, confira [Variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables).  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Software** e selecione **Instalar Atualizações de Software**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="required-for-installation---mandatory-software-updates-only"></a>Necessário para instalação – somente atualizações de software obrigatórias
 Selecione esta opção para instalar todas as atualizações de software obrigatórias com prazos de instalação definidos pelo administrador.  

#### <a name="available-for-installation---all-software-updates"></a>Disponíveis para instalação – Todas as atualizações de software
 Selecione esta opção para instalar todas as atualizações de software disponíveis. Primeiro, implante essas atualizações em uma coleção da qual o computador é membro. Uma sequência de tarefas instala todas as atualizações de software disponíveis nos computadores de destino.  

#### <a name="evaluate-software-updates-from-cached-scan-results"></a>Avaliar atualizações de software dos resultados da verificação em cache
 Por padrão, essa etapa usa os resultados da varredura em cache do Windows Update Agent. Desabilite essa opção para instruir o Windows Update Agent a baixar o catálogo mais recente do ponto de atualização de software. Habilite essa opção ao usar uma sequência de tarefas para [capturar e criar uma imagem do sistema operacional](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system). Neste cenário, é provável que ocorra uma grande quantidade de atualizações de software. 

 Muitas dessas atualizações têm dependências. Por exemplo, instale a atualização ABC para a atualização XYZ aparecer como aplicável. Ao desabilitar essa configuração e implantar a sequência de tarefas em muitos clientes, todos eles se conectam ao ponto de atualização de software ao mesmo tempo. Esse comportamento resulta em problemas de desempenho durante o processo e o download do catálogo de atualizações. 

 Na maioria dos casos, use a configuração padrão para usar os resultados da verificação armazenados em cache. 

 A variável **SMSTSSoftwareUpdateScanTimeout** controla o tempo limite de verificação de atualizações de software durante essa etapa. O valor padrão é 30 minutos. Para saber mais, confira [Variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#SMSTSSoftwareUpdateScanTimeout).


### <a name="options"></a>Opções   

 Além das opções padrão, defina as seguintes configurações adicionais na guia **Opções** dessa etapa da sequência de tarefas:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Execute essa etapa novamente se o computador reiniciar inesperadamente
 Se uma das atualizações reiniciar o computador inesperadamente, tente realizar essa etapa novamente. A etapa habilita essa configuração por padrão com duas novas tentativas. Você pode especificar de uma a cinco novas tentativas.  

 > [!NOTE]  
 > Configure a variável **SMSTSWaitForSecondReboot** para especificar por quantos segundos a sequência de tarefas fica em pausa depois que o computador é reiniciado nesse cenário. Para saber mais, confira [Variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#SMSTSWaitForSecondReboot).  



##  <a name="BKMK_JoinDomainorWorkgroup"></a> Ingressar no Domínio ou Grupo de Trabalho  

 Use essa etapa para adicionar o computador de destino a um grupo de trabalho ou domínio.  

 Essa etapa de sequência de tarefas é executada somente no sistema operacional completo. Ela não é executada no Windows PE.   

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [OSDJoinAccount](/sccm/osd/understand/task-sequence-variables#OSDJoinAccount)  
 - [OSDJoinDomainName](/sccm/osd/understand/task-sequence-variables#OSDJoinDomainName)  
 - [OSDJoinDomainOUName](/sccm/osd/understand/task-sequence-variables#OSDJoinDomainOUName)  
 - [OSDJoinPassword](/sccm/osd/understand/task-sequence-variables#OSDJoinPassword)  
 - [OSDJoinSkipReboot](/sccm/osd/understand/task-sequence-variables#OSDJoinSkipReboot)  
 - [OSDJoinType](/sccm/osd/understand/task-sequence-variables#OSDJoinType)  
 - [OSDJoinWorkgroupName](/sccm/osd/understand/task-sequence-variables#OSDJoinWorkgroupName)  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e selecione **Ingressar no Domínio ou Grupo de Trabalho**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="join-a-workgroup"></a>Ingressar em um grupo de trabalho
 Selecione esta opção para fazer o computador de destino ingressar no grupo de trabalho especificado. Se o computador atualmente é um membro de um domínio, selecionar esta opção faz com que o computador seja reinicializado.  

#### <a name="join-a-domain"></a>Ingressar em um domínio
 Selecione esta opção para fazer o computador de destino ingressar no domínio especificado.  

 Opcionalmente, digite ou navegue para uma unidade organizacional (UO) no domínio especificado para ingressar o computador. Se o computador atualmente é um membro de algum outro domínio ou grupo de trabalho, essa opção causa a reinicialização do computador. Se o computador já é um membro de outra UO, a Instalação do Windows ignora esta configuração, já que o Active Directory Domain Services não permite alterar a unidade Organizacional por esse método.  

#### <a name="enter-the-account-which-has-permission-to-join-the-domain"></a>Insira a conta que tem permissão para ingressar no domínio
 Clique em **Definir** para inserir um nome de usuário e senha para uma conta com permissões para ingressar no domínio. Insira a conta no formato: `Domain\account`. Para saber mais sobre a conta de entrada no domínio da sequência de tarefas, confira [Contas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-domain-joining-account).  



## <a name="BKMK_PrepareConfigMgrClientforCapture"></a> Preparar ConfigMgr Client for Capture  

 Use esta etapa para remover ou configurar o cliente do Configuration Manager no computador de referência. Essa ação prepara o computador para captura como parte do processo de geração de imagens.

 Essa etapa remove completamente o cliente do Configuration Manager, em vez de apenas remover informações importantes. Quando a sequência de tarefas implantar a imagem capturada do sistema operacional, ela instalará um novo cliente do Configuration Manager a cada vez.  

 > [!Note]  
 >  O mecanismo da sequência de tarefas só remove o cliente durante a sequência de tarefas **Compilar e capturar uma imagem do sistema operacional de referência**. O mecanismo de sequência de tarefas não remove o cliente durante outros métodos de captura, tais como mídia de captura ou uma sequência de tarefas personalizadas.  

 Essa etapa de sequência de tarefas é executada somente no sistema operacional completo. Ela não é executada no Windows PE.  

 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Imagens** e selecione **Preparar o Cliente do ConfigMgr para Captura**. 


### <a name="properties"></a>Propriedades  

 Essa etapa não requer nenhuma configuração na guia **Propriedades**.



##  <a name="BKMK_PrepareWindowsforCapture"></a> Preparar Windows para Captura  

 Use essa etapa para especificar as opções do Sysprep ao capturar uma imagem do sistema operacional no computador de referência. Esta etapa executa o Sysprep e reinicia o computador na imagem de inicialização do Windows PE especificado para a sequência de tarefas. Essa ação falhará se o computador de referência estiver ingressado em um domínio.  

 Esta etapa é executada somente no sistema operacional completo. Ela não é executada no Windows PE.   

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [OSDKeepActivation](/sccm/osd/understand/task-sequence-variables#OSDKeepActivation)  
 - [OSDTargetSystemRoot](/sccm/osd/understand/task-sequence-variables#OSDTargetSystemRoot-output)  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Imagens** e selecione **Preparar o Windows para Captura**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="automatically-build-mass-storage-driver-list"></a>Criar automaticamente a lista de drivers de armazenamento em massa
 Selecione esta opção para fazer com que o Sysprep crie automaticamente uma lista de drivers de armazenamento em massa do computador de referência. Essa opção habilita a opção de criar drivers de armazenamento em massa no arquivo sysprep.inf no computador de referência. Para obter mais informações sobre essa configuração, consulte a documentação do Sysprep.  

#### <a name="do-not-reset-activation-flag"></a>Não redefina o sinalizador de ativação
 Selecione esta opção para impedir que o Sysprep redefina o sinalizador de ativação do produto.  

#### <a name="shutdown-the-computer-after-running-this-action"></a>Desligue o computador depois de executar essa ação
 <!--SCCMDocs-pr issue 2695--> A partir da versão 1806, essa opção instrui o Sysprep a desligar o computador em vez do comportamento de reinicialização padrão. 



##  <a name="BKMK_PreProvisionBitLocker"></a> Pré-provisionar o BitLocker  

 Use esta etapa para habilitar o BitLocker em uma unidade durante a execução do Windows PE. Por padrão, apenas o espaço usado em disco é criptografado. Portanto, a criptografia ocorre muito mais rápido. Aplique as opções de gerenciamento de chaves usando a etapa [Habilitar BitLocker](#BKMK_EnableBitLocker) após a instalação do sistema operacional. 

 Esta etapa é executada somente no Windows PE. Ela não é executada no sistema operacional completo.  

 > [!IMPORTANT]  
 >  Pré-provisionar o BitLocker requer no mínimo o Windows 7. O computador também deve conter um TPM (Trusted Platform Module) compatível e habilitado.  

 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Discos** e selecione **Pré-provisionar BitLocker**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="apply-bitlocker-to-the-specified-drive"></a>Aplicar o BitLocker à unidade especificada
 Especificar a unidade para a qual você deseja habilitar o BitLocker. O BitLocker criptografa apenas o espaço usado em disco.  

#### <a name="use-full-disk-encryption"></a>Usar criptografia de disco cheio
 <!--SCCMDocs-pr issue 2671--> Por padrão, essa etapa só criptografa o espaço usado na unidade. Esse comportamento padrão é recomendável, pois é mais rápido e eficiente. A partir da versão 1806, se a sua organização exigir a criptografia de toda a unidade durante a instalação, habilite esta opção. A Instalação do Windows aguarda toda a unidade estar criptografada, o que leva muito tempo, especialmente em unidades grandes. 

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>Ignore esta etapa para computadores que não têm um TPM ou quando o TPM não está habilitado
 Selecione esta opção para ignorar a criptografia de unidade em um computador que não tem um TPM compatível ou habilitado. Por exemplo, use esta opção ao implantar um sistema operacional em uma máquina virtual.  



##  <a name="BKMK_ReleaseStateStore"></a> Liberar Armazenamento de Estado  

 Use esta etapa para notificar o ponto de migração de estado de que a ação de captura ou restauração foi concluída. Use essa etapa junto com as etapas **Solicitar Repositório de Estado**, **Capturar Estado do Usuário** e **Restaurar Estado do Usuário**. Você pode usar estas etapas para migrar dados de estado do usuário usando um ponto de migração de estado e a USMT (Ferramenta de Migração do Usuário).  

 Para mais informações sobre como gerenciar o estado do usuário ao implantar sistemas operacionais, confira [Gerenciar o estado do usuário](/sccm/osd/get-started/manage-user-state).  

 Se você usar a etapa **Solicitar Repositório de Estado** para solicitar acesso a um ponto de migração de estado para *capturar* o estado do usuário, essa etapa notificará o ponto de migração de estado de que o processo de captura foi concluído. O ponto de migração de estado marca então os dados de estado do usuário como disponíveis para restauração. O ponto de migração de estado define as permissões de controle de acesso a dados de estado do usuário, de modo que somente o computador realizando a restauração tem acesso somente leitura.  

 Se você usar a etapa **Solicitar Repositório de Estado** para solicitar acesso a um ponto de migração de estado para *restaurar* o estado do usuário, essa etapa notificará o ponto de migração de estado de que o processo de restauração foi concluído. O ponto de migração de estado ativa então as respectivas definições de retenção de dados configuradas.  

 > [!IMPORTANT]  
 > Defina a opção **Continuar em Caso de Erro** para todas as etapas entre as etapas **Solicitar Repositório de Estado** e **Liberar Repositório de Estado**. Cada etapa **Solicitar Repositório de Estado** deve ter uma etapa **Liberar Repositório de Estado** correspondente.  

 Esta etapa é executada somente no sistema operacional completo. Ela não é executada no Windows PE.   

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Estado de Usuário** e selecione **Liberar Repositório de Estado**. 


### <a name="properties"></a>Propriedades  

 Essa etapa não requer nenhuma configuração na guia **Propriedades**.



##  <a name="BKMK_RequestStateStore"></a> Solicitar Armazenamento de Estado  

 Use essa etapa para solicitar acesso a um ponto de migração de estado durante a captura ou a restauração de estado.  

 Para mais informações sobre como gerenciar o estado do usuário ao implantar sistemas operacionais, confira [Gerenciar o estado do usuário](/sccm/osd/get-started/manage-user-state).  

 Use essa etapa junto com as etapas **Solicitar Repositório de Estado**, **Liberar Estado do Usuário** e **Restaurar Estado do Usuário**. Você pode usar estas etapas para migrar o estado do computador usando um ponto de migração de estado e a USMT (Ferramenta de Migração do Usuário).  

 > [!NOTE]  
 >  Ao criar um novo ponto de migração de estado, o armazenamento de estado do usuário permanece não disponível por até uma hora. Para agilizar a disponibilidade, ajuste quaisquer configurações de propriedade no ponto de migração do estado para disparar uma atualização de arquivo de controle do site.  

 Essa etapa é executada no sistema operacional completo e no Windows PE para USMT offline.   

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [OSDStateFallbackToNAA](/sccm/osd/understand/task-sequence-variables#OSDStateFallbackToNAA)  
 - [OSDStateSMPRetryCount](/sccm/osd/understand/task-sequence-variables#OSDStateSMPRetryCount)  
 - [OSDStateSMPRetryTime](/sccm/osd/understand/task-sequence-variables#OSDStateSMPRetryTime)  
 - [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Estado de Usuário** e selecione **Solicitar Repositório de Estado**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="capture-state-from-the-computer"></a>Capturar estado do computador
 Localize um ponto de migração de estado que atenda aos requisitos mínimos definidos nas configurações de ponto de migração de estado. Por exemplo, **Número máximo de clientes** e **Quantidade mínima de espaço livre em disco**. Essa opção não garante que exista espaço em disco disponível no momento da migração de estado. Esta opção solicita acesso ao ponto de migração de estado para capturar o estado do usuário e configurações de um computador.  

 Se o site do Configuration Manager tem vários pontos de migração de estado ativos, esta etapa encontra um ponto de migração de estado com espaço em disco disponível. A sequência de tarefas consulta o ponto de gerenciamento para obter uma lista de pontos de migração de estado e avalia cada um até encontrar um que atenda aos requisitos mínimos.  

#### <a name="restore-state-from-another-computer"></a>Restaurar o estado de outro computador
 Solicite acesso a um ponto de migração de estado para restaurar as configurações e o estado do usuário capturados anteriormente para um computador de destino.  

 Se há vários pontos de migração de estado, essa etapa localiza o ponto de migração de estado que tem o estado do computador de destino.  

#### <a name="number-of-retries"></a>Número de novas tentativas
 O número de vezes que essa etapa tenta localizar um ponto de migração de estado apropriado antes de falhar.  

#### <a name="retry-delay-in-seconds"></a>Intervalo entre tentativas (em segundos)
 A quantidade de tempo em segundos que a etapa de sequência de tarefas espera entre as novas tentativas.  

#### <a name="if-computer-account-fails-to-connect-to-a-state-store-use-the-network-access-account"></a>Se a conta de computador não conseguir se conectar a um armazenamento de estado, use a conta de acesso à rede
 Se a sequência de tarefas não puder acessar o ponto de migração de estado usando a conta de computador, ela usará as credenciais de conta de acesso de rede para se conectar. Essa opção é menos segura porque outros computadores poderiam usar a conta de acesso de rede para acessar o estado armazenado. Essa opção poderá ser necessária se o computador de destino não estiver ingressado no domínio.  



##  <a name="BKMK_RestartComputer"></a> Reiniciar Computador  

 Use essa etapa para reiniciar o computador que executa a sequência de tarefas. Após a reinicialização, o computador continua automaticamente com a próxima etapa na sequência de tarefas.  

 Esta etapa pode ser executada no sistema operacional completo ou no Windows PE.   

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [SMSRebootMessage](/sccm/osd/understand/task-sequence-variables#SMSRebootMessage)  
 - [SMSRebootTimeout](/sccm/osd/understand/task-sequence-variables#SMSRebootTimeout)  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e selecione **Reiniciar Computador**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="the-boot-image-assigned-to-this-task-sequence"></a>A imagem de inicialização atribuída a essa sequência de tarefas
 Selecione esta opção para o computador de destino usar a imagem de inicialização atribuída à sequência de tarefas. A sequência de tarefas usa a imagem de inicialização para executar as etapas subsequentes no Windows PE.  

#### <a name="the-currently-installed-default-operating-system"></a>O sistema operacional padrão atualmente instalado
 Selecione esta opção para o computador de destino ser reinicializado no sistema operacional instalado.  

#### <a name="notify-the-user-before-restarting"></a>Notificar o usuário antes de reiniciar
 Selecione esta opção para exibir uma notificação ao usuário antes que computador de destino seja reiniciado. A etapa seleciona esta opção, por padrão.  

#### <a name="notification-message"></a>Mensagem de notificação
 Digite uma mensagem de notificação a ser exibida ao usuário antes da reinicialização do computador de destino.  

#### <a name="message-display-time-out"></a>Tempo limite de exibição de mensagem
 Especifique a quantidade de tempo em segundos antes do computador de destino ser reiniciado. O padrão é 60 segundos.  



##  <a name="BKMK_RestoreUserState"></a> Restaurar Estado do Usuário  

 Use essa etapa para iniciar o USMT (Ferramenta de Migração do Usuário) para restaurar o estado do usuário e configurações para o computador de destino. Use essa etapa junto com a etapa **Capturar Estado do Usuário**.  

 Para mais informações sobre como gerenciar o estado do usuário ao implantar sistemas operacionais, confira [Gerenciar o estado do usuário](/sccm/osd/get-started/manage-user-state).  

 Use essa etapa com as etapas **Solicitar Repositório de Estado** e **Liberar Repositório de Estado** para salvar ou restaurar as configurações de estado com um ponto de migração de estado. Esta opção sempre descriptografa o armazenamento de estado do USMT usando uma chave de criptografia gerada e gerenciada pelo Configuration Manager.  

 A etapa **Restaurar Estado do Usuário** fornece controle sobre um subconjunto limitado das opções da USMT mais usadas. Especifique opções de linha de comando adicionais com a variável **OSDMigrateAdditionalRestoreOptions**.  

 > [!IMPORTANT]  
 >  Se você está usando essa etapa para uma finalidade não relacionada a um cenário de implantação de sistema operacional, adicione a etapa [Reiniciar Computador](#BKMK_RestartComputer) imediatamente após a etapa **Restaurar Estado do Usuário**.  

 Esta etapa é executada somente no sistema operacional completo. Ela não é executada no Windows PE.   

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [_OSDMigrateUsmtRestorePackageID](/sccm/osd/understand/task-sequence-variables#OSDMigrateUsmtRestorePackageID)  
 - [OSDMigrateAdditionalRestoreOptions](/sccm/osd/understand/task-sequence-variables#OSDMigrateAdditionalRestoreOptions)  
 - [OSDMigrateContinueOnRestore](/sccm/osd/understand/task-sequence-variables#OSDMigrateContinueOnRestore)  
 - [OSDMigrateEnableVerboseLogging](/sccm/osd/understand/task-sequence-variables#OSDMigrateEnableVerboseLogging)  
 - [OSDMigrateLocalAccounts](/sccm/osd/understand/task-sequence-variables#OSDMigrateLocalAccounts)  
 - [OSDMigrateLocalAccountPassword](/sccm/osd/understand/task-sequence-variables#OSDMigrateLocalAccountPassword)  
 - [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Estado de Usuário** e selecione **Restaurar Estado de Usuário**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="user-state-migration-tool-package"></a>Pacote da ferramenta de migração de estado do usuário
 Especifique o pacote que contém a versão da USMT a ser usada por esta etapa. Este pacote não exige um programa. Quando a etapa é executada, a sequência de tarefas usa a versão da USMT no pacote especificado. Especifique um pacote que contém a versão de 32 bits ou 64 bits do USMT. A arquitetura da USMT varia de acordo com a arquitetura do sistema operacional do qual a sequência de tarefas está restaurando o estado. 

#### <a name="restore-all-captured-user-profiles-with-standard-options"></a>Restaurar todos os perfis de usuário com opções padrão
 Restaura os perfis de usuário com as opções padrão. Para personalizar as opções a serem restauradas pela USMT, selecione **Personalizar captura de perfil do usuário**.  

#### <a name="customize-how-user-profiles-are-restored"></a>Personalizar como os perfis de usuário são restaurados
 Permite que você personalize os arquivos que você deseja restaurar o computador de destino. Clique em **Arquivos** para especificar os arquivos de configuração do pacote do USMT que deseja usar para restaurar os perfis de usuário. Para adicionar um arquivo de configuração, digite o nome do arquivo na caixa **Nome do arquivo** e clique em **Adicionar**. O painel de arquivos lista os arquivos de configuração usados pela USMT. O arquivo .xml que você especifica define qual arquivo de usuário é restaurado pela USMT.  

#### <a name="restore-local-computer-user-profiles"></a>Restaurar perfis de usuário do computador local
 Restaura os perfis de usuário do computador local. Esses perfis não são para usuários do domínio. Atribua novas senhas às contas de usuário local restauradas. A USMT não é capaz de migrar as senhas originais. Digite a senha nova na caixa **Senha** e confirme a senha em **Confirmar senha** .  

#### <a name="continue-if-some-files-cannot-be-restored"></a>Continuar se alguns arquivos não puderem ser restaurados
 Continuará a restauração das configurações e estado do usuário, mesmo se a USMT não puder restaurar alguns arquivos. Essa etapa habilita esta opção por padrão. Se você desabilitar essa opção, e a USMT encontrar erros durante a restauração de arquivos, essa etapa falhará imediatamente. A USMT não restaura todos os arquivos.   

#### <a name="enable-verbose-logging"></a>Habilitar o log detalhado
 Habilite esta opção para gerar informações de arquivo de log mais detalhadas. Durante a restauração de estado, a sequência de tarefas gera por padrão o **Loadstate.log** na pasta de log de sequência de tarefas, `%WinDir%\ccm\logs`.  



##  <a name="BKMK_RunCommandLine"></a> Executar Linha de Comando  

 Use essa etapa para executar a linha de comando especificada.  

 Esta etapa pode ser executada no sistema operacional completo ou no Windows PE.   

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [OSDDoNotLogCommand](/sccm/osd/understand/task-sequence-variables#OSDDoNotLogCommand) (a partir da versão 1806)<!--1358493-->  
 - [SMSTSDisableWow64Redirection](/sccm/osd/understand/task-sequence-variables#SMSTSDisableWow64Redirection)  
 - [SMSTSRunCommandLineUserName](/sccm/osd/understand/task-sequence-variables#SMSTSRunCommandLineUserName)  
 - [SMSTSRunCommandLinePassword](/sccm/osd/understand/task-sequence-variables#SMSTSRunCommandLinePassword)  
 - [WorkingDirectory](/sccm/osd/understand/task-sequence-variables#WorkingDirectory)  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e selecione **Executar Linha de Comando**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="command-line"></a>Linha de Comando
 Especifica a linha de comando executada pela sequência de tarefas. Esse campo é obrigatório. Inclui extensões de nome de arquivo, por exemplo, .vbs e .exe. Inclua todos os arquivos de configurações necessários e as opções de linha de comando.  

 Se você não especificar a extensão de nome de arquivo, o Configuration Manager tentará usar .com, .exe e .bat. Se o nome do arquivo tiver uma extensão que não é de um tipo executável, o Configuration Manager tentará aplicar uma associação local. Por exemplo, se a linha de comando for readme.gif, o Configuration Manager iniciará o aplicativo especificado no computador de destino para abrir arquivos .gif.  

 Exemplos:  

 `setup.exe /a`  

 `cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

 > [!NOTE]  
 >  Para executar com êxito, preceda as ações de linha de comando com o comando **cmd.exe /c**. Exemplos dessas ações incluem comandos de cópia, redirecionamento de saída e piping.  

#### <a name="disable-64-bit-file-system-redirection"></a>Desabilitar o redirecionamento de sistema de arquivo de 64 bits
 Por padrão, os sistemas operacionais de 64 bits usam o redirecionador de sistema de arquivos WOW64 para executar linhas de comando. Esse comportamento é para encontrar corretamente versões de 32 bits das bibliotecas e dos executáveis do sistema operacional. Selecione esta opção para desabilitar o uso do redirecionador de sistema de arquivos WOW64. O Windows executa o comando usando versões de 64 bits nativas de bibliotecas e executáveis do sistema operacional. Esta opção não terá nenhum efeito ao executar em um sistema operacional de 32 bits.  

#### <a name="start-in"></a>Iniciar em
 Especifica a pasta do executável do programa, até 127 caracteres. Essa pasta pode ser um caminho absoluto no computador de destino ou um caminho relativo à pasta do ponto de distribuição que contém os arquivos de instalação. Esse campo é opcional.  

 Exemplos:  

 `c:\officexp`  

 `i386`  

 > [!NOTE]  
 >  O botão **Procurar** procura arquivos e pastas no computador local. Qualquer coisa selecionada também deve existir no computador de destino. Deve existir no mesmo local e com os mesmos nomes de arquivo e de pasta.  

#### <a name="package"></a>Pacote
 Quando você especificar arquivos ou programas na linha de comando que ainda não estão presentes no computador de destino, selecione essa opção para especificar o pacote do Configuration Manager que contém os arquivos necessários. O pacote não exige um programa. Essa opção não será necessária se os arquivos especificados existirem no computador de destino.  

#### <a name="time-out"></a>Tempo limite
 Especifica um valor que representa quanto tempo o Configuration Manager permite para a execução da linha de comando. Esse valor pode ser de um a 999 minutos. O valor padrão é 15 minutos. Essa opção é desabilitada por padrão.  

 > [!IMPORTANT]  
 >  Se você inserir um valor que não permita tempo suficiente para o comando especificado ser concluído com êxito, a etapa atual falhará. A sequência de tarefas inteira poderá falhar dependendo das configurações da etapa ou do grupo. Se o tempo limite expirar, o Configuration Manager encerrará o processo de linha de comando.  

#### <a name="run-this-step-as-the-following-account"></a>Executar esta etapa como a seguinte conta
 Especifica que a linha de comando é executada como uma conta de usuário do Windows diferente da conta Sistema Local.  

 > [!NOTE]  
 >  Para executar comandos ou scripts simples com outra conta depois de instalar o sistema operacional, primeiro adicione a conta ao computador. Além disso, talvez seja necessário restaurar os perfis de usuário do Windows para executar programas mais complexos, como um Windows Installer.  

#### <a name="account"></a>Conta
 Especifica a conta de usuário do Windows usada por essa etapa para execução da linha de comando. A linha de comando é executada com as permissões da conta especificada. Clique em **Definir** para especificar o usuário local ou a conta de domínio. Para saber mais sobre a conta de execução da sequência de tarefas, confira [Contas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-run-as-account).

 > [!IMPORTANT]  
 >  Se esta etapa especifica uma conta de usuário e é executada no Windows PE, a ação falha. Você não pode ingressar o Windows PE em um domínio. O arquivo **smsts.log** registra essa falha.  



##  <a name="BKMK_RunPowerShellScript"></a> Executar Script do PowerShell  

 Use essa etapa para executar o script do Windows PowerShell especificado.  

 Esta etapa pode ser executada no sistema operacional completo ou no Windows PE. Para executar esta etapa no Windows PE, habilite o PowerShell na imagem de inicialização. Habilite o componente WinPE-PowerShell na guia **Componentes Opcionais** nas propriedades da imagem de inicialização. Para mais informações sobre como modificar uma imagem de inicialização, confira [Manage boot images](/sccm/osd/get-started/manage-boot-images) (Gerenciar imagens de inicialização).  

 > [!NOTE]  
 >  O PowerShell não está habilitado por padrão nos sistemas operacionais Windows Embedded.  

 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e selecione **Executar Script do PowerShell**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="package"></a>Pacote
 Especifique o pacote do Configuration Manager que contém o script do PowerShell. Um pacote pode conter vários scripts do PowerShell.  

#### <a name="script-name"></a>Nome do script
 Especifica o nome do script do PowerShell para executar. Esse campo é obrigatório.  

#### <a name="parameters"></a>Parâmetros
 Especifica os parâmetros passados para o script do PowerShell. Esses parâmetros são os mesmos que os parâmetros do script do PowerShell na linha de comando.  

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

#### <a name="powershell-execution-policy"></a>Política de execução do PowerShell
 Determinar quais scripts do PowerShell (se houver) podem ser executados no computador. Selecione uma das seguintes políticas de execução:  

 -   **AllSigned**: executar somente scripts assinados por um fornecedor confiável  

 -   **Undefined**: não definir nenhuma política de execução  

 -   **Bypass**: carregar todos os arquivos de configuração e executar todos os scripts. Se você baixar um script não assinado da Internet, o Windows PowerShell não solicitará permissão antes de executar o script.  


 > [!IMPORTANT]  
 >  O PowerShell 1.0 não suporta as políticas de execução Indefinido e Ignorar.  



##  <a name="child-task-sequence"></a> Executar sequência de tarefas

 > [!Note]  
 > O Configuration Manager não habilita esse recurso opcional por padrão. Habilite esse recurso antes de usá-lo. Para obter mais informações, consulte [Enable optional features from updates (Habilitar recursos opcionais de atualizações)](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).

 Começando com o Configuration Manager versão 1710, você pode adicionar uma nova etapa que executa outra sequência de tarefas. Essa etapa cria um relacionamento pai-filho entre as sequências de tarefas. Com uma sequência de tarefas filho, é possível criar sequências de tarefas mais modulares e reutilizáveis.

 Considere estes pontos ao adicionar uma sequência de tarefas filho a uma sequência de tarefas:  

 - As sequências de tarefas pai e filho efetivamente são combinadas em uma única política que o cliente executa.  

 - O ambiente é global. Se a sequência de tarefas pai define uma variável e, em seguida, a sequência de tarefas filho altera essa variável, a variável retém o valor mais recente. Se a sequência de tarefas filho criar uma nova variável, a variável estará disponível para o restante da sequência de tarefas pai.  

 - As mensagens de status são enviadas normalmente para uma operação de sequência de tarefas.  

 - A sequência de tarefas grava entradas no arquivo **smsts.log**, com novas entradas de log que deixam claro quando uma sequência de tarefas filho é iniciada.  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e selecione **Executar Sequência de Tarefas**. 


### <a name="properties"></a>Propriedades

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="select-task-sequence-to-run"></a>Selecionar sequência de tarefas para execução
 Clique em **Procurar** para selecionar a sequência de tarefas filho. A caixa de diálogo **Selecionar uma Sequência de Tarefas** não mostra a sequência de tarefas pai.



##  <a name="BKMK_SetDynamicVariables"></a> Definir Variáveis Dinâmicas  

 Use esta etapa para executar as seguintes ações:  

 1.  Colete informações do computador e seu ambiente. Em seguida, defina as variáveis de sequência de tarefas especificadas com as informações.  

 2.  Avalie as regras definidas. Defina variáveis de sequência de tarefas com base nas regras avaliadas como verdadeiras.  


 A sequência de tarefas define automaticamente as seguintes variáveis de sequência de tarefas somente leitura:  
 - [\_SMSTSMake](/sccm/osd/understand/task-sequence-variables#SMSTSMake)  
 - [\_SMSTSModel](/sccm/osd/understand/task-sequence-variables#SMSTSModel)  
 - [\_SMSTSMacAddresses](/sccm/osd/understand/task-sequence-variables#SMSTSMacAddresses)  
 - [\_SMSTSIPAddresses](/sccm/osd/understand/task-sequence-variables#SMSTSIPAddresses)  
 - [\_SMSTSSerialNumber](/sccm/osd/understand/task-sequence-variables#SMSTSSerialNumber)  
 - [\_SMSTSAssetTag](/sccm/osd/understand/task-sequence-variables#SMSTSAssetTag)  
 - [\_SMSTSUUID](/sccm/osd/understand/task-sequence-variables#SMSTSUUID)  


 Esta etapa pode ser executada no sistema operacional completo ou no Windows PE.  

 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e selecione **Definir Variáveis Dinâmicas**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="dynamic-rules-and-variables"></a>Variáveis e regras dinâmicas
 Para definir uma variável dinâmica para uso na sequência de tarefas, adicione uma regra. Em seguida, defina um valor para cada variável especificada na regra. Além disso, adicione uma ou mais variáveis sem adicionar uma regra. Quando você adicionar uma regra, poderá escolher entre as seguintes categorias:  

 - **Computador**: avaliar valores para a Marcação do ativo, UUID, número de série ou endereço MAC. Defina vários valores, conforme necessário. Se algum valor for true, a regra será avaliada como true. Por exemplo, a seguinte regra é avaliada como true se o número de série do dispositivo é 5892087 e o endereço MAC é 22-A4-5A-13-78-26:  

     `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

 - **Local**: avaliar valores para o gateway de rede padrão  

 - **Marca e Modelo**: avaliar valores para a marca e o modelo de um computador. A marca e o modelo devem ambas serem avaliadas como verdadeiro para a regra a ser avaliada como verdadeiro.   

    Especifique um asterisco (`*`) e o ponto de interrogação (`?`) como caracteres curinga. O asterisco corresponde a vários caracteres, e o ponto de interrogação corresponde a um único caractere. Por exemplo, a cadeia de caracteres `DELL*900?` corresponde a `DELL-ABC-9001` e `DELL9009`.  

 - **Variável de Sequência de Tarefas**: adicionar uma variável, condição e valor da sequência de tarefas a ser avaliada. A regra avalia como verdadeiro quando o valor definido para a variável atende a condição especificada.  

    Especifique uma ou mais variáveis a serem definidas para uma regra que é avaliada como verdadeiro ou definir variáveis sem usar uma regra. Selecione uma variável existente ou crie uma variável personalizada.  

     - **Variáveis de sequência de tarefas existentes**: selecione uma ou mais variáveis em uma lista de variáveis de sequência de tarefas existentes. Variáveis de matriz não estão disponíveis para selecionar.  

     - **Variáveis personalizadas da sequência de tarefas**: defina uma variável personalizada da sequência de tarefas. Você também pode especificar uma variável de sequência de tarefas existente. Essa configuração é útil para especificar uma matriz de variáveis existente, como **OSDAdapter**, pois matrizes de variáveis não estão na lista de variáveis de sequência de tarefas existente.  


 Depois de selecionar as variáveis de uma regra, forneça um valor para cada variável. A variável é definida como o valor especificado quando a regra for avaliada como verdadeiro. Para cada variável, você pode selecionar o **Valor secreto** para ocultar o valor da variável. Por padrão, algumas variáveis existentes ocultam valores, como a variável **OSDCaptureAccountPassword**.  

 > [!IMPORTANT]  
 >  O Configuration Manager remove quaisquer valores de variável marcados como um **valor secreto** quando você importa uma sequência de tarefas com a etapa **Definir Variáveis Dinâmicas**. Reinsira o valor da variável dinâmica novamente depois de importar a sequência de tarefas.  



##  <a name="BKMK_SetTaskSequenceVariable"></a> Definir Variável de Sequência de Tarefas  

 Use essa etapa para definir o valor de uma variável usada com a sequência de tarefas.  

 Esta etapa pode ser executada no sistema operacional completo ou no Windows PE. 

 Variáveis de sequência de tarefas são lidas por ações de sequência de tarefas e especificam o comportamento dessas ações. Para saber mais sobre variáveis de sequência de tarefas específicas e como usá-las, confira os artigos a seguir:  
 - [Como usar variáveis de sequência de tarefas](/sccm/osd/understand/using-task-sequence-variables)  
 - [Variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables)  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e selecione **Definir Variável de Sequência de Tarefas**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="task-sequence-variable"></a>Variável de Sequência de Tarefas
 Especifique o nome de uma variável interna ou de ação de sequência de tarefas ou especifique seu próprio nome de variável definido pelo usuário.  

#### <a name="do-not-display-this-value"></a>Não exibir este valor
 <!--1358330--> A partir da versão 1806, habilite esta opção para mascarar os dados confidenciais armazenados em variáveis de sequência de tarefas. Por exemplo, ao especificar uma senha. 

#### <a name="value"></a>Valor  
 A sequência de tarefas define a variável para esse valor. Defina essa variável de sequência de tarefas para o valor de outra variável de sequência de tarefas com a sintaxe `%varname%`.  



##  <a name="BKMK_SetupWindowsandConfigMgr"></a> Instalar Windows e ConfigMgr  

 Use esta etapa para fazer a transição do Windows PE para o novo sistema operacional. Esta etapa da sequência de tarefas é necessária em qualquer implantação de sistema operacional. Ele instala o cliente do Configuration Manager no novo sistema operacional e prepara a sequência de tarefas para continuar a execução no novo sistema operacional.  

 Esta etapa é executada somente no Windows PE. Ela não é executada no sistema operacional completo.  

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [SMSClientInstallProperties](/sccm/osd/understand/task-sequence-variables#SMSClientInstallProperties)  


 Esta etapa substitui as variáveis de diretório sysprep.inf ou unattend.xml, tais como `%WINDIR%` e `%ProgramFiles%`, pelo diretório de instalação do Windows PE, `X:\Windows`. A sequência de tarefas ignora variáveis especificadas usando essas variáveis de ambiente.  

 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Imagens** e selecione **Instalar o Windows e o ConfigMgr**. 


### <a name="step-actions"></a>Ações da etapa

 Esta etapa executa as seguintes ações:  

#### <a name="preliminaries-windows-pe"></a>Etapas preliminares: Windows PE  

 1.  Substitua as variáveis de sequência de tarefas no arquivo unattend.xml.  

 2.  Baixe o pacote que contém o cliente do Configuration Manager. Adicione o pacote à imagem implantada.  

#### <a name="set-up-windows"></a>Configurar o Windows  

 -  Instalação baseada em imagem  

    1.  Desabilite o cliente do Configuration Manager na imagem, se ele existir. Em outras palavras, desabilite o Início Automático para o serviço de cliente do Configuration Manager.  

    2.  Atualiza o registro da imagem implantada para que o sistema operacional implantado comece com a mesma letra de unidade que o computador de referência.  

    3.  Reinicie no sistema operacional implantado.  

    4.  Mini-instalação do Windows executada usando o arquivo de resposta sysprep.inf ou unattend.xml especificado com todas as interações do usuário final suprimidas. Se você usar a etapa **Aplicar Configurações de Rede** para ingressar em um domínio, essa informação estará no arquivo de resposta. A mini-instalação do Windows adiciona o computador ao domínio.  

 -  Instalação baseada em Setup.exe. Executa o Setup.exe que segue o processo de instalação típica do Windows:  

    1.  Copie o pacote de atualização do sistema operacional, especificado na etapa **Aplicar Sistema Operacional**, para a unidade de disco rígido.  

    2.  Reinicie no sistema operacional recém-implantado.  

    3.  Mini-instalação do Windows executada usando o arquivo de resposta sysprep.inf ou unattend.xml especificado com todas as interfaces do usuário suprimidas. Se você usar a etapa **Aplicar Configurações de Rede** para ingressar em um domínio, essa informação estará no arquivo de resposta. A mini-instalação do Windows adiciona o computador ao domínio.  

#### <a name="set-up-the-configuration-manager-client"></a>Instalar o cliente do Configuration Manager  

 1.  Após a conclusão da mini-instalação do Windows, a sequência de tarefas é retomada usando setupcomplete.cmd.  

 2.  Habilite ou desabilite a conta de Administrador local com base na opção selecionada na etapa **Aplicar Configurações do Windows**.  

 3.  Instale o cliente do Configuration Manager usando o pacote baixado anteriormente e as propriedades de instalação especificadas nesta etapa. O cliente é instalado no "modo de provisionamento". Esse modo impede que o cliente processe novas solicitações de política até a conclusão da sequência de tarefas.  

 4.  Aguarde até que o cliente esteja totalmente operacional.  

#### <a name="the-step-completes"></a>A etapa é concluída
 A sequência de tarefas continua executando a próxima etapa.  

<!-- Engineering confirmed that the task sequence does nothing with respect to group policy processing.
> [!NOTE]  
>  The **Setup Windows and ConfigMgr** task sequence action is responsible for running Group Policy on the newly installed computer. The Group Policy is applied after the task sequence is finished.  
-->


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="client-package"></a>Pacote do cliente
 Clique em **Procurar** e selecione o pacote de instalação de cliente do Configuration Manager a ser usado com essa etapa.  

#### <a name="use-pre-production-client-package-when-available"></a>Usar o pacote de cliente de pré-produção quando disponível
 Se houver um pacote de cliente de pré-produção disponível e o computador fizer parte de uma coleção piloto, a sequência de tarefas usará esse pacote em vez do pacote do cliente de produção. O cliente de pré-produção é uma versão mais recente para testes no ambiente de produção. Clique em **Procurar** e selecione o pacote de instalação de cliente de pré-produção a ser usado com essa etapa.  

#### <a name="installation-properties"></a>Propriedades de instalação
 A etapa de sequência de tarefas especifica automaticamente a atribuição de site e a configuração padrão. Use esse campo para especificar as propriedades adicionais de instalação a serem usada ao instalar o cliente. Para inserir várias propriedades de instalação, separe-as com um espaço.  

 Especifique as opções de linha de comando usadas durante a instalação do cliente. Por exemplo, insira `/skipprereq: silverlight.exe` para informar ao CCMSetup.exe para não instalar o pré-requisito do Microsoft Silverlight. Para mais informações sobre as opções de linha de comando disponíveis para o CCMSetup.exe, confira [About client installation properties](/sccm/core/clients/deploy/about-client-installation-properties) (Sobre as propriedades da instalação do cliente).  


### <a name="options"></a>Opções

 > [!NOTE]  
 > Não habilite **Continuar em caso de erro** na guia **Opções**. Se houver um erro durante essa etapa, a sequência de tarefas falhará, independentemente de você habilitar essa configuração ou não.  



##  <a name="BKMK_UpgradeOS"></a> Atualizar o sistema operacional  

 > [!TIP]  
 > Começando com o Windows 10, versão 1709, a mídia inclui várias edições. Quando você configura uma sequência de tarefas para usar uma imagem do sistema operacional ou um pacote de atualização do sistema operacional, é necessário selecionar uma [edição compatível](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).  

 Use essa etapa para atualizar uma versão mais antiga do Windows para uma versão mais recente do Windows 10.  

 Essa etapa de sequência de tarefas é executada somente no sistema operacional completo. Ela não é executada no Windows PE.  

 Use as variáveis de sequência de tarefas seguintes com esta etapa:  
 - [_SMSTSOSUpgradeActionReturnCode](/sccm/osd/understand/task-sequence-variables#SMSTSOSUpgradeActionReturnCode)  
 - [OSDSetupAdditionalUpgradeOptions](/sccm/osd/understand/task-sequence-variables#OSDSetupAdditionalUpgradeOptions)  


 Para adicionar essa etapa no editor de sequência de tarefas, clique em **Adicionar**, selecione **Imagens** e selecione **Atualizar Sistema Operacional**. 


### <a name="properties"></a>Propriedades  

 Na guia **Propriedades** desta etapa, defina as configurações descritas nesta seção.  

#### <a name="upgrade-package"></a>Atualizar pacote
 Selecione esta opção para especificar o pacote de atualização do sistema operacional Windows 10 a ser usado para a atualização.  

#### <a name="source-path"></a>Caminho de origem
 Especifica um caminho de rede ou local para a mídia do Windows 10 usada pela Instalação do Windows. Essa configuração corresponde à opção de linha de comando `/InstallFrom` da Instalação do Windows. 

 Você também pode especificar uma variável, como `%MyContentPath%` ou `%DPC01%`. Ao usar uma variável para o caminho de origem, defina o valor dela logo no início da sequência de tarefas. Por exemplo, use a etapa [Baixar o conteúdo do pacote](#BKMK_DownloadPackageContent) para especificar uma variável para o local do pacote de atualização do sistema operacional. Em seguida, use essa variável para o caminho de origem nesta etapa.  

#### <a name="edition"></a>Edição
 Especifique a edição na mídia do sistema operacional a ser usada para a atualização.  

#### <a name="product-key"></a>Chave do produto
 Especifique a chave do produto a ser aplicada ao processo de atualização.  

#### <a name="provide-the-following-driver-content-to-windows-setup-during-upgrade"></a>Fornecer o seguinte conteúdo de driver à Instalação do Windows durante a atualização
 Adicione drivers ao computador de destino durante o processo de atualização. Essa configuração corresponde à opção de linha de comando `/InstallDriver` da Instalação do Windows. Os drivers devem ser compatíveis com o Windows 10. especifique uma das seguintes opções:  

 - **Pacote de driver**: clique em **Procurar** e selecione um pacote de driver existente na lista.  

 - **Conteúdo de teste**: selecione esta opção para especificar o local para o pacote de drivers. Você pode especificar uma pasta local, um caminho de rede ou uma variável de sequência de tarefas. Ao usar uma variável para o caminho de origem, defina o valor dela logo no início da sequência de tarefas. Por exemplo, usando a etapa [Baixar conteúdo do pacote](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent).  

#### <a name="time-out-minutes"></a>Tempo limite (minutos)
 Especifique o número de minutos antes que o Configuration Manager falhe nesta etapa. Essa opção será útil se a Instalação do Windows parar o processamento, mas não encerrar.  

#### <a name="perform-windows-setup-compatibility-scan-without-starting-upgrade"></a>Executar verificação de compatibilidade da Instalação do Windows sem iniciar atualização
 Execute a verificação de compatibilidade da Instalação do Windows sem iniciar o processo de atualização. Essa configuração corresponde à opção de linha de comando `/Compat ScanOnly` da Instalação do Windows. Implante o pacote de atualização do sistema operacional inteiro com essa opção. 

 <!--SCCMDocs-pr issue 2812--> A partir da versão 1806, quando você habilitar essa opção, essa etapa não colocará o cliente do Configuration Manager no modo de provisionamento. A Instalação do Windows é executada silenciosamente em segundo plano, e o cliente continua a funcionar normalmente. 

 A instalação retorna um código de saída como resultado da verificação. A tabela a seguir fornece alguns dos códigos de saída mais comuns:  

 |Código de saída|Detalhes|  
 |-|-|  
 |MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Nenhum problema de compatibilidade (“êxito”).|  
 |MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|Problemas de compatibilidade acionáveis.|  
 |MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|A opção de migração selecionada não está disponível. Por exemplo, uma atualização do Enterprise para Professional.|  
 |MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Não qualificado para Windows 10.|  
 |MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|Não há espaço livre em disco suficiente.|  

 Para saber mais sobre esse parâmetro, confira [Opções de linha de comando da Instalação do Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#6).  

#### <a name="ignore-any-dismissible-compatibility-messages"></a>Ignorar mensagens de compatibilidade dispensáveis
 Especifica que a Configuração conclui a instalação, ignorando quaisquer mensagens de compatibilidade dispensáveis. Essa configuração corresponde à opção de linha de comando `/Compat IgnoreWarning` da Instalação do Windows.  

#### <a name="dynamically-update-windows-setup-with-windows-update"></a>Atualizar dinamicamente a Instalação do Windows com o Windows Update
 Habilite a instalação para executar operações de atualização dinâmica, tais como pesquisa, download e instalação de atualizações. Essa configuração corresponde à opção de linha de comando `/DynamicUpdate` da Instalação do Windows. Essa configuração não é compatível com as atualizações de software do Configuration Manager. Habilite esta opção quando você gerencia atualizações com o WSUS (Windows Server Update Services) autônomo ou o Windows Update para Empresas.  

#### <a name="override-policy-and-use-default-microsoft-update"></a>Substituir a política e usar o padrão do Microsoft Update
 Substitua temporariamente a política local em tempo real para executar operações de Atualização Dinâmica. O computador recebe atualizações do Windows Update.
