---
title: "Etapas de sequência de tarefas – Configuration Manager | Microsoft Docs"
description: "Saiba mais sobre as etapas de sequência de tarefas que você pode adicionar a uma sequência de tarefas do Configuration Manager."
ms.custom: na
ms.date: 03/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
caps.latest.revision: "26"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: e0726febc4c36a26c5e067914734838bf2681e6c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="task-sequence-steps-in-system-center-configuration-manager"></a>Etapas da sequência de tarefas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As etapas de sequência de tarefas a seguir podem ser adicionadas à sequência de tarefas do Configuration Manager. Para obter informações sobre como editar uma sequência de tarefas, veja [Edit a task sequence](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  


##  <a name="BKMK_ApplyDataImage"></a> Aplicar a etapa de sequência de tarefas de imagem de dados  
 Use a etapa de sequência de tarefas **Aplicar imagem de dados** para copiar a imagem de dados para a partição de destino especificada.  

 Esta etapa é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão. Para mais informações sobre as variáveis de sequência de tarefas para esta ação, confira [Task sequence action variables](task-sequence-action-variables.md) (Variáveis de ação da sequência de tarefas).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Pacote da imagem**  
 Especifique o **Pacote de imagem** que será usado por essa etapa de sequência de tarefas clicando em **Procurar**. Selecione o pacote que você deseja instalar na caixa de diálogo **Selecionar um pacote** . As informações de propriedade associada para cada pacote de imagem existente são exibidas na parte inferior da caixa de diálogo **Selecionar um pacote** . Use a lista suspensa para selecionar a **imagem** você deseja instalar por meio do **Pacote de imagem**selecionado.  

> [!NOTE]  
>  Esta ação de sequência de tarefas trata a imagem como um arquivo de dados e não realiza nenhuma a configuração necessária para inicializar a imagem como um sistema operacional.  

 **Destino**  
 Especifica que um arquivo formatado partição e disco rígido, letra de unidade lógica específica ou o nome de uma variável de sequência de tarefas que contém a letra da unidade lógica.  

-   **Próxima partição disponível** – Use a próxima partição sequencial que não foi visada anteriormente por uma ação Aplicar Sistema Operacional ou Aplicar Imagem de Dados nessa sequência de tarefas.  

-   **Disco e partição específicos** – Selecione o número do **Disco** (começando com 0) e o da **Partição** (começando com 1).  

-   **Letra da unidade lógica específica** – Especifique a **Letra da Unidade** atribuída à partição pelo Windows PE. Observe que essa letra de unidade pode ser diferente da letra de unidade atribuída pelo sistema operacional implantado recentemente.  

-   **Letra de unidade lógica armazenada em uma variável** – Especifique a variável de sequência de tarefas que contém a letra da unidade atribuída à partição pelo Windows PE. Essa variável normalmente seria definida na seção avançada da caixa de propriedades **Propriedades da partição** para a ação da sequência de tarefa **Formatar e particionar o disco** .  

 **Excluir todo o conteúdo da partição antes de aplicar a imagem**  
 Especifica que todos os arquivos da partição de destino serão excluídos antes que a imagem seja instalada. Não excluindo o conteúdo da partição, esta etapa pode ser usada para aplicar o conteúdo adicional a uma partição de destino anterior.  

##  <a name="BKMK_ApplyDriverPackage"></a> Aplicar pacote de driver  
 Use a etapa da sequência de tarefas **Aplicar pacote de Driver** para baixar todos os drivers no pacote de driver e instalá-los no sistema operacional Windows.

 A etapa da sequência de tarefas **Aplicar pacote de Driver** disponibiliza todos os drivers de dispositivo em um pacote de driver para uso pelo Windows. Esta etapa pode ser adicionada a uma sequência de tarefas entre as etapas **Aplicar sistema operacional**  e **Instalação do Windows e do ConfigMgr** para disponibilizar os drivers de dispositivo no pacote de drivers para o Windows. Normalmente, a etapa **Aplicar pacote de Driver** é posicionada após a **Aplicação automática de drivers** . A etapa da sequência de tarefas **Aplicar pacote de Driver** também é útil em cenários de implantação de mídia autônoma.  

 Verifique se os drivers de dispositivo similares são colocados em um pacote de driver e distribua-os aos pontos de distribuição apropriados. Depois de serem distribuídos, os computadores cliente do Configuration Manager poderão instalá-los. Por exemplo, você pode colocar todos os drivers de dispositivo de um fabricante em um pacote de driver e distribuir o pacote para pontos de distribuição onde os computadores associados possam acessá-los.

 Esta etapa é útil para mídia autônoma e para os administradores que desejam instalar um conjunto específico de drivers, incluindo drivers de dispositivos que não seriam detectados em uma varredura de Plug-n-Play (por exemplo, impressoras de rede).  

 Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Apply Driver Package Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyDriverPackage).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Pacote de drivers**  
 Especifique o pacote de driver que contém os drivers de dispositivo necessários clicando em **Procurar** e iniciando a caixa de diálogo **Selecionar um pacote** . Especifique um pacote existente para disponibilizar. As propriedades do pacote associado são exibidas na parte inferior da caixa de diálogo.  

 **Selecione o driver de armazenamento em massa dentro do pacote que precisa ser instalado antes da instalação em sistemas operacionais anteriores ao Windows Vista**  
 Especifique os drivers de dispositivos de armazenamento em massa que são necessários para instalações de sistemas operacionais anteriores ao Windows Vista.  

 **Driver**  
 Selecione o arquivo de driver de dispositivo de armazenamento em massa a serem instalados antes da instalação em implantações de sistemas operacionais anteriores ao Windows Vista. A lista suspensa é preenchida com o pacote especificado.  

 **Modelo**  
 Especifique a inicialização crítica de dispositivo necessária para implantações de sistemas operacionais anteriores ao Windows Vista.  

 **Faça uma instalação autônoma de drivers não assinados nas versões do Windows em que isso é permitido**  
 Selecione esta opção para permitir que o Windows instale drivers que não são assinados no computador de referência.  

##  <a name="BKMK_ApplyNetworkSettings"></a> Etapa Aplicar configurações de rede  
 Use a etapa da sequência de tarefas **Aplicar configurações de rede** para especificar as informações de configuração de rede ou grupo de trabalho do computador de destino. Os valores especificados são armazenados no formato de arquivo de resposta apropriado para uso pela instalação do Windows quando a etapa da sequência de tarefas **Instalação do Windows e ConfigMgr** é executada.  

 Essa etapa de sequência de tarefas é executada em um sistema operacional padrão ou o Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Apply Network Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyNetworkSettings).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Ingressar no grupo de trabalho**  
 Selecione esta opção para fazer o computador de destino ingressar no grupo de trabalho especificado. Insira o nome do grupo de trabalho na linha **Grupo de trabalho** . Esse valor pode ser substituído pelo valor capturado pela etapa da sequência de tarefas **Capturar as configurações de rede** .  

 **Ingressar em um domínio**  
 Selecione esta opção para fazer o computador de destino ingressar no domínio especificado. Especifique ou navegue para o domínio, como *fabricam.com*. Especifique ou procure um caminho LDAP (Lightweight Directory Access Protocol) para uma unidade organizacional (ou seja, LDAP//OU=computadores, DC=Fabricam.com, C=com).  

 **Conta**  
 Clique em **Definir** para especificar uma conta com as permissões necessárias para ingressar o computador no domínio. Na caixa de diálogo **Conta de Usuário do Windows** , é possível inserir o nome de usuário usando o seguinte formato: **Domínio\Usuário** .  

 **Adapter settings (Configurações do adaptador)**  
 Especifica configurações de rede para cada adaptador de rede no computador. Clique em **Novo** para abrir a caixa de diálogo **Configurações de rede** e especifique as configurações de rede. Se as configurações de rede foram capturadas em uma etapa da sequência de tarefas **Capturar as configurações de rede** anterior, as configurações anteriores serão aplicadas ao adaptador de rede e não às configurações especificadas nesta etapa. Se as configurações de rede não foram capturadas anteriormente, as configurações especificadas na etapa **Aplicar configurações de rede** etapa serão aplicadas aos adaptadores de rede na ordem de enumeração de dispositivo do Windows.  

##  <a name="BKMK_ApplyOperatingSystemImage"></a> Aplicar Imagem de Sistema Operacional  
 Use a etapa da sequência de tarefas **Aplicar imagem do sistema operacional** para instalar um sistema operacional no computador de destino. Essa etapa de sequência de tarefas executa um conjunto de ações, dependendo de se você estiver usando uma imagem do sistema operacional ou um pacote de instalação do sistema operacional para instalar o sistema operacional.  

 A etapa **Aplicar imagem do sistema operacional** executa as seguintes ações quando uma imagem do sistema operacional é usada.  

1.  Exclui todo o conteúdo no volume de destino, exceto os arquivos na pasta especificada pela variável de sequência de tarefas &#95;SMSTSUserStatePath.  

2.  Extrai o conteúdo do arquivo .wim especificado para a partição de destino especificado.  

3.  Prepara o arquivo de resposta:  

    1.  Cria um novo arquivo de resposta padrão da Instalação do Windows (sysprep.inf ou unattend.xml) para o sistema operacional que está sendo implantado.  

    2.  Mescla os valores do arquivo de resposta fornecido pelo usuário.  

4.  Copia carregadores de inicialização do Windows para a partição ativa.  

5.  Configura o boot.ini ou o Banco de Dados de Configuração da Inicialização (BCD) para referenciar o sistema operacional recém-instalado.  

 A etapa **Aplicar imagem do sistema operacional** executa as seguintes ações quando um pacote de instalação do sistema operacional é usado.  

1.  Exclui todo o conteúdo no volume de destino, exceto os arquivos na pasta especificada pela variável de sequência de tarefas &#95;SMSTSUserStatePath.  

2.  Prepara o arquivo de resposta:  

    1.  Cria um arquivo de resposta novo com valores padrão criados pelo Configuration Manager.  

    2.  Mescla os valores do arquivo de resposta fornecido pelo usuário.  

> [!NOTE]  
>  A instalação real do Windows é iniciada pela etapa da sequência de tarefas **Instalação do Windows e ConfigMgr** . Após a ação da sequência de tarefas **Aplicar sistema operacional** ser executada, a variável de sequência de tarefas OSDTargetSystemDrive é definida como a letra da unidade da partição que contém os arquivos do sistema operacional.  

 Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Apply Operating System Image Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyOperatingSystem).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   **Acessar o conteúdo diretamente do ponto de distribuição**:  

     Use esta opção para especificar se deseja que a sequência de tarefas para acessar a imagem do sistema operacional diretamente do ponto de distribuição. Por exemplo, você pode usar essa opção ao implantar sistemas operacionais em dispositivos inseridos que têm a capacidade de armazenamento limitada. Quando essa opção é selecionada, você também deve configurar as configurações de compartilhamento de pacote na guia **Acesso aos dados** das propriedades do pacote.  

    > [!NOTE]  
    >  Essa configuração substitui a opção de implantação configurada na página **Pontos de distribuição** no **Assistente de implantação de software** somente para a imagem de sistema operacional especificada nessa etapa de sequência de tarefas e não todo o conteúdo da sequência de tarefas inteira.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Aplicar o sistema operacional de uma imagem capturada**  
 Instala uma imagem do sistema operacional que foi capturada anteriormente. Clique em **Procurar** para abrir a caixa de diálogo **Selecionar um pacote** e selecione o pacote de imagem existente que você deseja instalar. Se várias imagens forem associadas ao **pacote de imagem**especificado, use a lista suspensa para especificar a imagem associada que será usada para essa implantação. Você pode exibir informações básicas sobre cada imagem existente clicando na imagem.  

 **Apply operating system image from an original installation source (Aplicar a imagem do sistema operacional de uma fonte de instalação original)**  
 Instala um sistema operacional usando a instalação original. Clique em **Procurar** para abrir a caixa de diálogo **Selecione o pacote de instalação do sistema operacional** e selecione o pacote de instalação do sistema operacional existente que deseja usar. Você pode exibir informações básicas sobre cada origem de imagem existente clicando na origem da imagem. As propriedades da origem da imagem associada são exibidas no painel de resultados, na parte inferior da caixa de diálogo. Se houver várias edições associadas ao pacote especificado, use a lista suspensa para especificar a **Edição** associada a ser usada.  

 **Usar um arquivo de resposta autônomo ou Sysprep para uma instalação personalizada**  
 Use esta opção para fornecer um arquivo de resposta de instalação do Windows (**unattend.xml**, **unattend.txt**, ou **sysprep.inf**) dependendo do método de instalação e da versão do sistema operacional. O arquivo especificado pode incluir qualquer uma das opções de configuração padrão compatíveis com arquivos de resposta do Windows. Por exemplo, você pode usá-la para especificar a página inicial padrão do Internet Explorer. Você deve especificar o pacote que contém o arquivo de resposta e o caminho associado ao arquivo no pacote.  

> [!NOTE]  
>  O arquivo de resposta de instalação que você fornece pode conter de variáveis de sequência de tarefa integradas do formulário %*varname*%, onde varname é o nome da variável. A cadeia de caracteres %*varname*% substituirá os valores reais de variável na ação da sequência de tarefas **Instalação do Windows e ConfigMgr** . No entanto, observe que essas variáveis de sequência de tarefas integradas não podem ser usadas em campos somente numérico em um arquivo de resposta unattend.xml.  

 Se você não fornecer um arquivo de resposta de instalação do Windows, essa ação da sequência de tarefas gerará automaticamente um arquivo de resposta.  

 **Destino**  
 Especifica que um arquivo formatado partição e disco rígido, letra de unidade lógica específica ou o nome de uma variável de sequência de tarefas que contém a letra da unidade lógica.  

-   **Próxima partição disponível** – Use a próxima partição sequencial que não foi visada anteriormente por uma ação Aplicar Sistema Operacional ou Aplicar Imagem de Dados nessa sequência de tarefas.  

-   **Disco e partição específicos** – Selecione o número do **Disco** (começando com 0) e o da **Partição** (começando com 1).  

-   **Letra da unidade lógica específica** – Especifique a **Letra da Unidade** atribuída à partição pelo Windows PE. Observe que essa letra de unidade pode ser diferente da letra de unidade atribuída pelo sistema operacional implantado recentemente.  

-   **Letra de unidade lógica armazenada em uma variável** – Especifique a variável de sequência de tarefas que contém a letra da unidade atribuída à partição pelo Windows PE. Essa variável normalmente seria definida na seção avançada da caixa de propriedades **Propriedades da partição** para a ação da sequência de tarefa **Formatar e particionar o disco** .  

##  <a name="BKMK_ApplyWindowsSettings"></a> Aplicar as Configurações do Windows  
 Use a etapa da sequência de tarefas **Aplicar configurações do Windows** para definir as configurações do Windows no computador de destino. Os valores especificados são armazenados no formato de arquivo de resposta apropriado para uso pela instalação do Windows quando a etapa da sequência de tarefas **Instalação do Windows e ConfigMgr** é executada.  

 Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Apply Windows Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyWindowsSettings).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Nome de usuário**  
 Especifique o nome de usuário registrado que está associado com o computador de destino. Esse valor pode ser substituído pelo valor capturado pela etapa da sequência de tarefas **Capturar as configurações do Windows** .  

 **Nome da organização**  
 Especifique o nome de organização registrado que está associado com o computador de destino. Esse valor pode ser substituído pelo valor capturado pela etapa da sequência de tarefas **Capturar as configurações do Windows** .  

 **Chave do produto (Product Key)**  
 Especifique a chave do produto que é usada para a instalação do Windows no computador de destino.  

 **Licenciamento por servidor**  
 Especifique o modo de licenciamento do servidor. Você pode selecionar **Por servidor** ou **Por usuário** como o modo de licenciamento. Se você selecionar por servidor como o modo de licenciamento, também precisará especificar o número máximo de conexões que serão permitidas por seu contrato de licença. Selecione **Não especificar** se o computador de destino não é um servidor ou se você não quiser especificar o modo de licenciamento.  

 **Máximo de conexões**  
 Especifique o número máximo de conexões que estão disponíveis para este computador conforme indicado no contrato de licença.  

 **Gerar aleatoriamente a senha do administrador local e desabilitar a conta em todas as plataformas com suporte (recomendado)**  
 Selecione esta opção para gerar aleatoriamente uma senha de administrador local. Isso cria uma senha de administrador local e faz com que a conta seja desativada em plataformas com suporte.  

 **Habilitar a conta e especificar a senha do administrador local**  
 Selecione esta opção para habilitar a conta de administrador local e criar a senha de administrador local. Insira a senha na linha **Senha** e confirme a senha na linha **Confirmar senha** .  

 **Fuso Horário**  
 Especifique o fuso horário para o computador de destino. Esse valor pode ser substituído pelo valor capturado pela etapa da sequência de tarefas **Capturar as configurações do Windows** .  

##  <a name="BKMK_AutoApplyDrivers"></a> Drivers de Aplicação Automática  
 Use a etapa da sequência de tarefas **Aplicação automática de drivers** para corresponder e instalar drivers como parte da implantação de sistema operacional.  

 A etapa da sequência de tarefas **Aplicação automática de drivers** executa as seguintes ações:  

1.  Verifica o hardware e localiza os IDs Plug-and-Play para todos os dispositivos presentes no sistema.  

2.  Envia a lista de dispositivos e seus IDs de Plug-and-Play para o ponto de gerenciamento. O ponto de gerenciamento retorna uma lista de drivers compatíveis do catálogo de drivers para cada dispositivo. O ponto de gerenciamento considera todos os drivers, independentemente de qual pacote de driver eles possam estar localizados. Somente os drivers marcados com a categoria de driver especificada e os drivers que não são marcados como desabilitados são considerados.  

3.  Para cada dispositivo, o cliente seleciona o melhor driver apropriado para o sistema operacional no qual ele está sendo implantado e em um ponto de distribuição acessível.  

4.  O driver ou drivers selecionados são baixados de um ponto de distribuição e preparados em sistema operacional de destino.  

    1.  Para instalações baseadas em imagem, os drivers são colocados no repositório de drivers do sistema operacional.  

    2.  Para instalações diretas, a Instalação do Windows é configurada com o local onde encontrar os drivers.  

5.  Quando a ação da sequência de tarefas **Instalação do Windows e ConfigMgr** é executada e o Windows é inicializado pela primeira vez, ele encontrará os drivers configurados por esta ação.  

> [!IMPORTANT]
>  A etapa da sequência de tarefas **Drivers de Aplicação Automática** não pode ser usada com mídia autônoma porque a instalação do Windows não terá nenhuma conexão com o site do Configuration Manager.

Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Auto Apply Drivers Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_AutoApplyDrivers).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Instalar apenas os drivers compatíveis que mais correspondam**  
 Especifica que a etapa de sequência de tarefas instala apenas o melhor driver correspondente a cada dispositivo de hardware detectado.  

 **Instalar todos os drivers compatíveis**  
 Especifica que a etapa de sequência de tarefas instala todos os drivers compatíveis para cada dispositivo de hardware detectado e permite à instalação do Windows escolher o melhor driver. Essa opção ocupa mais espaço em disco e largura de banda de rede porque baixa mais drivers, mas pode resultar na seleção de um melhor driver.  

 **Considerar os drivers de todas as categorias**  
 Especifica que a ação da sequência de tarefas pesquisa todas as categorias de driver disponíveis para os drivers de dispositivo apropriados.  

 **Limitar a correspondência de driver para considerar somente os drivers nas categorias selecionadas**  
 Especifica que a ação de sequência de tarefa procura por drivers de dispositivo em categorias de drivers específicas para os drivers de dispositivo apropriados.  

 **Fazer instalação autônoma de drivers não assinados em versões do Windows, onde permitido**  
 Permite que essa ação de sequência de tarefas instale drivers de dispositivo não assinados do Windows.  

> [!IMPORTANT]  
>  Essa opção não se aplica aos sistemas operacionais onde a política de assinatura de driver não pode ser configurada.  

##  <a name="BKMK_CaptureNetworkSettings"></a> Capturar configurações da rede  
 Use a etapa da sequência de tarefas **Capturar as configurações de rede** para capturar as configurações de rede da Microsoft no computador que executa a sequência de tarefas. As configurações são salvas em variáveis de sequência de tarefas que substituirão as configurações padrão definidas na etapa da sequência de tarefas **Aplicar configurações de rede** .  

 Essa etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Capture Network Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureNetworkSettings).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Especifica um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Fornece informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Migrar associação de domínio e grupo de trabalho**  
 Captura as informações de associação de domínio e grupo de trabalho do computador de destino.  

 **Migrar configuração do adaptador de rede**  
 Captura a configuração do adaptador de rede do computador de destino. As informações capturadas incluem as configurações de rede global, o número de adaptadores e as configurações de rede associadas a cada adaptador. Essas configurações incluem as configurações associadas com DNS, WINS, IP e filtros de porta.  

##  <a name="BKMK_CaptureOperatingSystemImage"></a> Capturar imagem do sistema operacional  
 Use a etapa da sequência de tarefas **Capturar imagem do sistema operacional** para capturar imagens de um ou mais computadores de referência e armazená-las em um arquivo WIM no compartilhamento de rede especificado. O Assistente de Adição do Pacote de Imagem de Sistema Operacional poderá ser usado para importar este arquivo .WIM para o Configuration Manager para que ele possa ser usado para implantações de sistema operacional baseadas em imagem.  

 Cada volume (unidade) no computador de referência é capturado como uma imagem separada dentro do arquivo. wim. Se o computador de referência tiver vários volumes, o arquivo WIM resultante conterá uma imagem separada para cada volume. Apenas volumes formatados como NTFS ou FAT32 são capturados. Volumes com outros formatos e USB são ignorados.  

 O sistema operacional instalado no computador de referência deve ser uma versão do Windows que tenha suporte pelo Configuration Manager e deve ter sido preparada usando a ferramenta SysPrep. O volume do sistema operacional instalado e o volume de inicialização devem ser o mesmo volume.  

 Você também deve inserir uma conta do Windows que tenha permissões de gravação ao compartilhamento de rede que você selecionou.  

 Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Capture Operating System Image Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureOperatingSystemImage).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

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
 Use a etapa da sequência de tarefas **Capturar estado do usuário** para usar a ferramenta de migração de estado do usuário (USMT) para capturar o estado do usuário e configurações do computador que executa a sequência de tarefas. Essa etapa de sequência de tarefas é usada em conjunto com a etapa da sequência de tarefas **Restaurar o estado do usuário** . Com o USMT 3.0.1 e posterior, essa opção sempre criptografa o armazenamento de estado do USMT usando uma chave de criptografia geradas e gerenciadas por Configuration Manager.  

 Para mais informações sobre como gerenciar o estado do usuário ao implantar sistemas operacionais, confira [Gerenciar o estado do usuário](../get-started/manage-user-state.md).  

 Você também poderá usar a etapa da sequência de tarefas **Capturar Estado do Usuário** com as etapas **Solicitar Armazenamento de Estado** e **Liberar Armazenamento de Estado** se quiser salvar as configurações de estado ou restaurar as configurações de um ponto de migração de estado no site do Configuration Manager.  

 A etapa da sequência de tarefas **Capturar estado do usuário** fornece controle sobre um subconjunto limitado dos mais opções mais usadas do USMT. Opções de linha de comando adicionais podem ser especificadas usando a variável de sequência de tarefas OSDMigrateAdditionalCaptureOptions.  

 Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Capture User State Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureUserState).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Pacote da ferramenta de migração do usuário**  
 Insira o pacote do Configuration Manager que contém a versão do USMT para essa etapa de sequência de tarefas para usar durante a captura de estado do usuário e suas configurações. Este pacote não exige um programa. Quando a etapa da sequência de tarefas é executada, a sequência de tarefas usará a versão da USMT no pacote que você especificar. Especifique um pacote contendo a versão 32 bits ou x64 do USMT de acordo com a arquitetura do sistema operacional do qual você está capturando o estado.  

 **Capture all user profiles with standard options (Capturar todos os perfis de usuário com opções padrão)**  
 Selecione esta opção para migrar todas as informações de perfil do usuário. Essa opção é habilitada por padrão.  

 Se você selecionar essa opção, mas não selecionar a opção de Restaurar perfis de usuário do computador local na etapa da sequência de tarefas Restaurar Estado do Usuário, a sequência de tarefas falhará porque o Configuration Manager não migrará as novas contas sem atribuir senhas a elas. Além disso, se você usar o assistente de **Nova sequência de tarefas** e criar uma sequência de tarefas para **Instalar um pacote de imagem existente**, a sequência de tarefas resultante por padrão irá Capturar todos os perfis de usuário com opções padrão, mas não selecionará a opção de Restaurar perfis de usuário do computador local (ou seja, contas de fora do domínio).  

 Selecione **Restaurar perfis de usuário do computador local** e forneça uma senha para a conta a ser migrada. Em uma sequência de tarefas criadas manualmente, essa configuração é encontrada na etapa Restaurar estado do usuário. Em uma sequência de tarefas criada pelo assistente **Nova sequência de tarefas** , essa configuração se encontra na página do assistente **Restaurar arquivos e configurações do usuário** .  

 Se você não tiver nenhuma conta de usuário local, isso não se aplica.  

 **Personalizar o modo como perfis de usuários são capturados**  
 Selecione esta opção para especificar uma migração de arquivo de perfil personalizado. Clique em **Arquivos** para selecionar os arquivos de configuração do USMT a serem usados com esta etapa. Você deve especificar um arquivo .xml personalizado que contém regras que definem os arquivos de estado do usuário para migrar.  

 **Clique aqui para selecionar os arquivos de configuração:**  
 Selecione esta opção para selecionar os arquivos de configuração do pacote da USMT que deseja usar para capturar os perfis de usuário. Clique no botão **Arquivos** para abrir a caixa de diálogo **Arquivos de configuração** . Para especificar um arquivo de configuração, insira o nome do arquivo na linha **Nome do arquivo** e clique no botão **Adicionar** .  

 **Habilitar log detalhado**  
 Habilite esta opção para gerar informações de arquivo de log mais detalhadas. Durante a captura de estado, o Scanstate.log é gerado e armazenado na pasta de Log de sequência de tarefas na pasta \windows\system32\ccm\logs por padrão.  

 **Skip files using encrypted file system (Ignorar arquivos usando o sistema de arquivos criptografados)**  
 Habilite esta opção se você quiser ignorar capturas de arquivos criptografados com o Sistema de Arquivo Criptografado (EFS), incluindo arquivos de perfil. Dependendo do sistema operacional e a versão do USMT, arquivos criptografados podem não ser lidos após a restauração. Para obter mais informações, consulte a documentação do USMT.  

 **Copiar usando o acesso ao sistema de arquivos**  
 Habilite esta opção especificar qualquer uma das seguintes configurações:  

-   **Continuar se não for possível capturar alguns arquivos**: habilite essa configuração para continuar o processo de migração mesmo que alguns arquivos não possam ser capturados. Se você desabilitar essa opção e um arquivo não puder ser capturado, a etapa da sequência de tarefas falhará. Essa opção é habilitada por padrão.  

-   **Capturar localmente usando links em vez de copiar arquivos**: habilite essa configuração para usar links físicos NTFS para capturar arquivos.  

     Para obter mais informações sobre como migrar dados usando links físicos, consulte [Repositório de migração de link físico](http://go.microsoft.com/fwlink/p/?LinkId=240222)  

-   **Capturar em modo offline (somente Windows PE)**: habilite essa configuração para capturar o estado de usuário no Windows PE em vez do sistema operacional completo.  

 **Capture by using Volume Copy Shadow Services (VSS) (Capturar usando o VSS (Serviços de Cópias de Sombra de Volume))**  
 Essa opção permite capturar arquivos mesmo se eles estiverem bloqueados para edição por outro aplicativo.  

##  <a name="BKMK_CaptureWindowsSettings"></a> Capturar Configurações do Windows  
 Use a etapa da sequência de tarefas **Capturar as configurações do Windows** para capturar as configurações do Windows no computador que executa a sequência de tarefas. As configurações são salvas em variáveis de sequência de tarefas que substituirão as configurações padrão definidas na etapa da sequência de tarefas **Aplicar configurações do Windows** .  

 Essa etapa de sequência de tarefas é executada em um sistema operacional padrão ou o Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Capture Windows Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureWindowsSettings).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Migrar nome do computador**  
 Selecione esta opção para capturar o nome do computador NetBIOS do computador.  

 **Migrar nomes de usuário e de organização registrados**  
 Selecione esta opção para capturar os nomes de usuário e organização registrados do computador.  

 **Migrar fuso horário**  
 Selecione esta opção para capturar a configuração de fuso horário no computador.  

##  <a name="BKMK_CheckReadiness"></a> Verificar Preparação  
 Use a etapa da sequência de tarefas **Verificar preparação** para verificar se o computador de destino atende as condições de pré-requisitos de implantação especificadas.  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa. Para esta etapa, não selecione essa configuração ou a etapa registrará apenas as verificações de preparação e não interromperá a sequência de tarefas quando uma verificação falhar.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Assegurar o mínimo de memória (MB)**  
 Selecione esta configuração para verificar se a quantidade de memória, em megabytes, instalada no computador de destino atende ou excede o valor especificado. Por padrão, essa configuração está selecionada.  

 **Assegurar o mínimo de velocidade do processador (MHz)**  
 Selecione esta configuração para verificar se a velocidade do processador em megahertz (MHz) instalada no computador de destino atende ou excede o valor especificado. Por padrão, essa configuração está selecionada.  

 **Assegurar o mínimo de espaço livre em disco (MB)**  
 Selecione esta configuração para verificar se a quantidade de espaço livre em disco, em megabytes, no computador de destino atende ou excede o valor especificado.  

 **Assegurar que o SO atual a ser atualizado seja**  
 Selecione esta configuração para verificar se o sistema operacional instalado no computador de destino atende o requisito que você especificar. Por padrão, essa configuração é selecionada com um valor de **CLIENTe**.  

##  <a name="BKMK_ConnectToNetworkFolder"></a> Conectar à Pasta de Rede  
 Use a ação da sequência de tarefas **Conectar à pasta de rede** para criar uma conexão com uma pasta de rede compartilhada.  

 Essa etapa de sequência de tarefas é executada em um sistema operacional padrão ou o Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Connect to Network Folder Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ConnecttoNetworkFolder).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

##  <a name="BKMK_ConvertDisktoDynamic"></a> Converter Disco em Dinâmico  
 Use a etapa da sequência de tarefas **Converter disco em dinâmico** para converter um disco físico de um tipo de disco básico para um tipo de disco dinâmico.  

 Esta etapa é executada em um sistema operacional padrão ou no Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Convert Disk to Dynamic Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ConvertDisk).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Número do Disco**  
 O número do disco físico que será convertido.  

##  <a name="BKMK_DisableBitLocker"></a> Desabilitar BitLocker  
 Use a etapa da sequência de tarefas **Desativar BitLocker** para desabilitar a criptografia de BitLocker na unidade do sistema operacional atual ou em uma unidade específica. Essa ação deixa os protetores de chave visíveis em texto não criptografado no disco rígido, mas não descriptografa o conteúdo da unidade. Consequentemente, essa ação é concluída quase instantaneamente.  

> [!NOTE]  
>  A criptografia de unidade de disco BitLocker fornece criptografia de baixo nível do conteúdo de um volume de disco.  

 Se você tiver várias unidades criptografadas, você deve desabilitar o BitLocker nas unidades de dados antes de desativar o BitLocker na unidade do sistema operacional.  

 Esta etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE.  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Especifica um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Fornece informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Unidade do sistema operacional atual**  
 Desabilita o BitLocker na unidade do sistema operacional atual.  

 **Unidade específica**  
 Desabilita o BitLocker em uma unidade específica. Use a lista suspensa para especificar a unidade em que o BitLocker será desabilitado.  

##  <a name="BKMK_DownloadPackageContent"></a> Baixar o conteúdo do pacote  
 Use a etapa da sequência de tarefas **Baixar Conteúdo do Pacote** para baixar qualquer um dos seguintes tipos de pacote:  

-   Imagens do sistema operacional  

-   Pacotes de atualização de sistema operacional  

-   Pacotes de driver  

-   Pacotes  

 Esta etapa funciona bem em uma sequência de tarefas para atualizar um sistema operacional nos seguintes cenários:  

-   Para usar uma sequência de tarefas de atualização única que pode funcionar com plataformas x86 e x64. Para fazer isso, inclua duas etapas **Baixar Conteúdo do Pacote** no grupo **Preparar para Atualização** com condições para detectar a arquitetura do cliente e baixar apenas o Pacote de atualização do sistema operacional apropriado. Configure cada etapa **Baixar Conteúdo do Pacote** para usar a mesma variável e use a variável para o caminho de mídia na etapa **Atualizar Sistema Operacional** .  

-   Para baixar um pacote de drivers aplicáveis dinamicamente, use duas etapas **Baixar Conteúdo do Pacote** com condições para detectar o tipo de hardware apropriado para cada pacote de drivers. Configure cada etapa **Baixar Conteúdo do Pacote** para usar a mesma variável e use a variável para o valor **Conteúdo de Teste** na seção de drivers da etapa **Atualizar Sistema Operacional** .  

> [!NOTE]    
> Quando você implanta uma sequência de tarefas que contém a etapa Baixar Conteúdo do Pacote, não selecione **Baixar todo o conteúdo localmente antes de iniciar a sequência de tarefas** para **Opções de implantação** na página **Pontos de Distribuição** do Assistente de Implantação de Software.  

Esta etapa é executada em um sistema operacional padrão ou no Windows PE. No entanto, a opção para salvar o pacote no cache do cliente do Configuration Manager não tem suporte no WinPE.

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Especifica um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Fornece informações mais detalhadas sobre a ação realizada nesta etapa.  

 Ícone**Selecionar pacote**  
 Clique no ícone para selecionar o pacote que será baixado. Depois de selecionar um pacote, você pode clicar no ícone novamente para escolher outro pacote.  

 **Coloque no seguinte local**  
 Escolha esta opção para salvar o pacote em um dos seguintes locais:  

 -   **Diretório de trabalho da sequência de tarefas**  

 -   **Cache do cliente do Configuration Manager**: use esta opção para armazenar o conteúdo no cache dos clientes. Isso permite que o cliente atue como uma fonte de cache de sistemas pares para outros clientes de cache de sistemas pares. Para mais informações, confira [Prepare Windows PE peer cache to reduce WAN traffic](../get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md) (Preparar o cache par do Windows PE para reduzir o tráfego da WAN).  

 -   **Caminho personalizado**  

 **Salvar caminho como uma variável**  
 Você pode salvar o caminho como uma variável que pode ser usada em outra etapa da sequência de tarefas. O Configuration Manager adiciona um sufixo numérico ao nome da variável. Por exemplo, se você especificar uma variável de %*mycontent*% como uma variável personalizada, essa será a raiz de onde todo o conteúdo referenciado está armazenado (que podem ser vários pacotes). Quando você faz referência à variável, adicionará um sufixo numérico à variável. Por exemplo, para o primeiro pacote, você fará referência à variável %*mycontent01*%. Quando você fizer referência à variável em etapas subsequentes, como uma atualização do sistema operacional, usa %*mycontent02*% ou %*mycontent03*% em que o número corresponde à ordem na qual o pacote está listado na etapa.  

 **Se o download do pacote falhar, continue baixando outros pacotes na lista**  
 Especifica que, caso haja falha no download do pacote, será feito o download do próximo pacote da lista.  

##  <a name="BKMK_EnableBitLocker"></a> Habilitar BitLocker  
 Use a etapa da sequência de tarefas **Habilitar BitLocker** para habilitar a criptografia BitLocker em pelo menos duas partições no disco rígido. A primeira partição ativa contém o código de inicialização do Windows. Outra partição contém o sistema operacional. A partição de inicialização deve permanecer descriptografada.  

 Use a etapa **Pré-provisionar o BitLocker** para habilitar o BitLocker em uma unidade no Windows PE. Para obter mais informações, consulte a seção [Pré-provisionar o BitLocker](#BKMK_PreProvisionBitLocker) neste tópico.  

> [!NOTE]  
>  A criptografia de unidade de disco BitLocker fornece criptografia de baixo nível do conteúdo de um volume de disco.  

 A etapa **Habilitar BitLocker** só é executada em um sistema operacional padrão. Ela não é executada no Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Enable BitLocker Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

 O Trusted Platform Module (TPM) deve estar no seguinte estado quando você especificar **Somente TPM**, **TPM e chave de inicialização em USB** ou **TPM e PIN**, antes de executar a etapa **Habilitar BitLocker** :  

-   Habilitada  

-   Ativado  

-   Propriedade permitida  

 A etapa de sequência de tarefas pode concluir qualquer inicialização do TPM restante, porque as etapas restantes não exigem reinicializações ou presença física. As etapas de inicialização de TPM restantes que podem ser concluídas de forma transparente por **Habilitar BitLocker** (se necessário) incluem:  

-   Criar um par de chave de endosso  

-   Criar valor de autorização do proprietário e caução para o Active Directory, que devem ser estendidos para oferecer suporte a esse valor  

-   Apropriar-se  

-   Crie a chave de raiz de armazenamento ou redefina-a se existir, mas for incompatível  

 Se você quiser que a etapa **Habilitar BitLocker** aguarde até que o processo de criptografia de unidade seja concluído antes de continuar com a próxima etapa na sequência de tarefas, marque a caixa de seleção **Aguardar** . Se você não marcar a caixa de seleção **Aguardar** , o processo de criptografia de unidade será executado em segundo plano e execução de sequência de tarefas continuará imediatamente para a próxima etapa.  

 O BitLocker pode ser usado para criptografar várias unidades em um sistema de computador (sistema operacional e unidades de dados). Para criptografar uma unidade de dados, o sistema operacional já devem ter sido criptografado e o processo de criptografia deve estar concluído, porque os protetores de chave para as unidades de dados são armazenados na unidade do sistema operacional. Como resultado, se você criptografar a unidade do sistema operacional e a unidade de dados no mesmo processo, a opção de espera deve ser selecionada para a etapa que habilita o BitLocker na unidade do sistema operacional.  

 Se o disco rígido já está criptografado, mas o BitLocker está desabilitado, quando o Habilitar BitLocker habilita novamente o protetor de chave, isso será concluído quase instantaneamente. Nova criptografia da unidade de disco rígida não é necessária neste caso.  

 Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Enable BitLocker Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Especifica um nome descritivo para esta etapa de sequência de tarefas.  

 **Descrição**  
 Permite que você, opcionalmente, insira uma descrição para essa etapa de sequência de tarefas.  

 **Escolher a unidade a ser criptografada**  
 Especifica a unidade para criptografar. Para criptografar a unidade do sistema operacional atual, selecione **Unidade do sistema operacional atual** e configure as seguintes opções para o gerenciamento de chaves:  

-   **Somente TPM**: selecione esta opção para usar somente o TPM (Trusted Platform Module).  

-   **Chave de inicialização somente em USB**: selecione esta opção para usar uma chave de inicialização armazenada em uma unidade flash USB. Quando você seleciona essa opção, o BitLocker bloqueia o processo normal de inicialização até que um dispositivo USB que contém uma chave de inicialização do BitLocker é anexado ao computador.  

-   **TPM e chave de inicialização em USB**: selecione esta opção para usar o TPM e uma chave de inicialização armazenada em uma unidade flash USB. Quando você seleciona essa opção, o BitLocker bloqueia o processo normal de inicialização até que um dispositivo USB que contém uma chave de inicialização do BitLocker é anexado ao computador.  

-   **TPM e PIN**: selecione esta opção para usar o TPM e um PIN (número de identificação pessoal). Quando você seleciona essa opção, o BitLocker bloqueia o processo normal de inicialização até que o usuário forneça o PIN.  

 Para criptografar uma unidade de dados específicos e não do sistema operacional, selecione **Unidade específica**e selecione a unidade na lista.  

 **Escolher onde criar a chave de recuperação**  
 Para especificar onde a senha de recuperação é criada, selecione **No Active Directory** para efetuar o caução da senha no Active Directory. Se você selecionar essa opção, deverá estender o Active Directory para o site para que as informações de recuperação do BitLocker associadas sejam salvas. Você pode optar por não criar uma senha selecionando **Não criar a chave de recuperação**. No entanto, a criação de uma senha é uma prática recomendada.  

 **Aguarde o BitLocker concluir o processo de criptografia de unidade em todas as unidades antes de continuar a execução da sequência de tarefas**  
 Selecione esta opção para permitir que a criptografia de unidade do BitLocker seja concluída antes de executar a próxima etapa na sequência de tarefas. Se essa opção for selecionada, todo o volume de disco será criptografado antes que o usuário seja capaz de fazer logon computador.  

 O processo de criptografia pode levar horas para ser concluído quando um disco rígido grande está sendo criptografado. Esta opção não permitirá que a sequência de tarefas continue imediatamente.  

##  <a name="BKMK_FormatandPartitionDisk"></a> Formatar e Particionar Disco  
 Use a etapa da sequência de tarefas **Formatar e particionar disco** para formatar e particionar um disco especificado no computador de destino.  

> [!IMPORTANT]  
>  Todas as configurações que você especificar para esta etapa se aplicam a um único disco. Se você deseja formatar e particionar outro disco no computador de destino, deverá adicionar uma etapa **Formatar e particionar disco** adicional à sequência de tarefas.  

 Essa etapa de sequência de tarefas é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Format and Partition Disk Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_FormatPartitionDisk).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Número do Disco**  
 O número do disco físico que será formatado. O número é baseado na ordem de enumeração de disco do Windows.  

 **Tipo de Disco**  
 O tipo de disco que é formatado. Há duas opções para selecionar na lista suspensa:  

-   Padrão(MBR) – Registro Mestre de Inicialização.  

-   GGT – Tabela de partição GUID  

> [!NOTE]  
>  Se você alterar o tipo de disco de **Padrão (MBR)** para **GPT**e o layout da partição contiver uma partição estendida, todas as partições estendidas e lógicas serão removidas do layout. Você será solicitado a confirmar esta ação antes de alterar o tipo de disco.  

 **Volume**  
 Informações específicas sobre a partição ou volume que será criado, incluindo o seguinte:  

-   Nome  

-   Espaço restante em disco  

 Para criar uma nova partição, clique em **Novo** para abrir a caixa de diálogo **Propriedades da partição** . Você pode especificar o tipo e tamanho da partição, bem como se esta será uma partição de inicialização. Para modificar uma partição existente, clique na partição a ser modificada e no botão Propriedades. Para obter mais informações sobre como configurar partições de disco rígido, consulte um destes procedimentos:  

-   [Como configurar partições de disco rígido baseadas em UEFI/GGT](http://go.microsoft.com/fwlink/?LinkID=272104)  

-   [Como configurar partições de disco rígido baseado em BIOS/MBR](http://go.microsoft.com/fwlink/?LinkId=272105)  

 Para excluir uma partição, selecione a partição a ser excluída e clique em **Excluir**.  

##  <a name="BKMK_InstallApplication"></a> Instalar Aplicativo  
 Use a etapa da sequência de tarefa **Instalar aplicativo** para instalar aplicativos como parte da sequência de tarefas. Esta etapa pode instalar um conjunto de aplicativos que são especificados pela etapa de sequência de tarefas ou um conjunto de aplicativos que são especificados por uma lista dinâmica de variáveis de sequência de tarefas. Quando essa etapa é executada, a instalação do aplicativo começa imediatamente sem esperar que um intervalo de sondagem de política.  

 Os aplicativos que são instalados devem atender aos seguintes critérios:  

-   O aplicativo deve ser um tipo de implantação do Windows Installer ou do Instalador de script. Não há suporte para tipos de implantação do pacote do aplicativo Windows (arquivo .appx).  

-   Ele deve executar sob a conta sistema local e não a conta de usuário.  

-   Ele não deve interagir com a área de trabalho. O programa deve ser executado silenciosamente ou em um modo autônomo.  

-   Ele não deve iniciar uma reinicialização por conta própria. O aplicativo deve solicitar uma reinicialização, usando o código de reinicialização padrão, um código de saída 3010. Isso garante que a etapa de sequência de tarefas manipulará corretamente a reinicialização. Se o aplicativo retornar um código de saída 3010, o mecanismo subjacente de sequência de tarefas executará a reinicialização. Após a reinicialização, a sequência de tarefas continua automaticamente.  

 Quando a etapa **Instalar aplicativo** é executada, o aplicativo verifica a aplicabilidade das regras de requisito e método de detecção de tipos de implantação do aplicativo. Com base nos resultados dessa verificação, o aplicativo instala o tipo de implantação aplicável. Se um tipo de implantação contém dependências, o tipo de implantação dependente é avaliado e instalado como parte da etapa de aplicativo de instalação. Dependências de aplicativos não têm suporte para mídia autônoma.  

> [!NOTE]  
>  Para instalar um aplicativo que substitui outro, os arquivos de conteúdo para o aplicativo substituído devem estar disponíveis ou a etapa de sequência de tarefas falhará. Por exemplo, o Microsoft Visio 2010 é instalado em um cliente ou em uma imagem capturada. Quando a etapa de sequência de tarefas Instalar aplicativo é executada para instalar o Microsoft Visio 2013, os arquivos de conteúdo para o Microsoft Visio 2010 (aplicativo substituído) devem estar disponíveis em um ponto de distribuição ou a sequência de tarefas falhará. Um cliente ou a imagem capturada com o Microsoft Visio instalado concluirá a instalação do Microsoft Visio 2013 sem verificar os arquivos de conteúdo do Microsoft Visio 2010.  

> [!NOTE]
> Você pode usar as variáveis internas SMSTSMPListRequestTimeoutEnabled e SMSTSMPListRequestTimeout para habilitar e especificar quantos milissegundos uma sequência de tarefas espera antes de tentar instalar novamente uma atualização de software ou aplicativo após uma falha ao recuperar a lista de pontos de gerenciamento dos serviços de localização. Para mais informações, confira [Task sequence built-in varliables](task-sequence-built-in-variables.md) (Variáveis internas da sequência de tarefas).

 Essa etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE.  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especifique para repetir esta etapa se o computador for reiniciado de forma inesperada. Também é possível especificar a quantidade de vezes da repetição após uma reinicialização.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Instalar os seguintes aplicativos**  
 Essa configuração especifica os aplicativos que são instalados na ordem em que foram especificados.  

 O Configuration Manager filtrará qualquer aplicativo desabilitado ou com as seguintes configurações. Esses aplicativos não aparecerão na caixa de diálogo **Selecionar aplicativo para instalar** .  

-   Somente quando um usuário tiver efetuado logon  

-   Executar com direitos de usuário  

 **Instalar aplicativos de acordo com a lista de variáveis dinâmicas**  
 Essa configuração especifica o nome de base para um conjunto de variáveis de sequência de tarefas que são definidas para uma coleção ou um computador. Essas variáveis especificam os aplicativos que serão instalados para essa coleção ou computador. Cada nome de variável consiste em seu nome de base comum e um sufixo numérico, começando com 01. O valor de cada variável deve conter o nome do aplicativo e nada mais.  

 Para os aplicativos a ser instalados usando uma lista de variáveis dinâmicas, a seguinte configuração deve ser habilitada na guia **Geral** da caixa de diálogo **Propriedades** do aplicativo: **Allow this application to be installed from the Install Application task sequence action instead of deploying manually (Permitir que este aplicativo seja instalado da ação de sequência de tarefas instalar aplicativo em vez de implantar manualmente)**  

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

 As condições a seguir afetam o que será instalado:  

-   Se o valor de uma variável contém todas as informações que não seja o nome do aplicativo. Esse aplicativo não está instalado e continua a sequência de tarefas.  

-   Se nenhuma variável com o nome de base especificado e o sufixo "01" for encontrado, nenhum aplicativo será instalado. Quando você seleciona **Continuar em caso de erro** na guia Opções da etapa de sequência de tarefas, a sequência de tarefas continua quando um aplicativo falhar ao instalar. Quando esta configuração não estiver selecionada, a sequência de tarefas falhará e não instalará os aplicativos restantes.  

 **If an application fails, continue installing other applications in the list (Se um aplicativo falhar, continue a instalar outros aplicativos na lista)**  
 Essa configuração especifica que a etapa continuará se a instalação de um aplicativo individual falhar. Se essa configuração estiver especificada, a sequência de tarefas continuará independentemente de qualquer erro de instalação que é retornado. Se isso não for especificado e a instalação falhar, a etapa de sequência de tarefas terminará imediatamente.  

##  <a name="BKMK_InstallDeploymentTools"></a> Instalar Ferramentas de Implantação  
 Use a etapa da sequência de tarefas **Instalar Ferramentas de Implantação** para instalar o pacote do Configuration Manager que contém as ferramentas de implantação do Sysprep.  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Pacote Sysprep**  
 Essa configuração especifica o pacote do Configuration Manager que contém as ferramentas de implantação do Sysprep para os seguintes sistemas operacionais:  

-   Windows XP SP3  

-   Windows XP X64 SP2  

-   Windows Server 2003 SP2  

##  <a name="BKMK_InstallPackage"></a> Instalar Pacote

 Use a etapa da sequência de tarefa **Instalar pacote** para instalar software como parte da sequência de tarefas. Quando essa etapa é executada, a instalação começa imediatamente sem esperar que um intervalo de sondagem de política  

 O software a ser instalado deve atender aos seguintes critérios:  

-   Ele deve executar sob a conta sistema local e não a conta de usuário.  

-   Ele não deve interagir com a área de trabalho. O programa deve ser executado silenciosamente ou em um modo autônomo.  

-   Ele não deve iniciar uma reinicialização por conta própria. O software deve solicitar uma reinicialização, usando o código de reinicialização padrão, um código de saída 3010. Isso garante que a etapa de sequência de tarefas manipulará corretamente a reinicialização. Se o software retornar um código de saída 3010, o mecanismo subjacente de sequência de tarefas executará a reinicialização. Após a reinicialização, a sequência de tarefas continua automaticamente.  

 Programas que usam a opção **Executar outro programa primeiro** para instalar um programa dependente não são suportados ao implantar um sistema operacional. Se **Executar outro programa primeiro** estiver habilitado para o software e o programa dependente já foi executado no computador de destino, o programa dependente será executado e a sequência de tarefas continuará. No entanto, se o programa dependente ainda não tiver sido executado no computador de destino, a etapa de sequência de tarefas falhará.  

> [!NOTE]  
>  O site de administração central não possui as políticas de configuração de cliente necessárias para habilitar o agente de distribuição de software durante a execução da sequência de tarefas. Quando você cria mídia autônoma para uma sequência de tarefas no site de administração central, e a sequência de tarefas inclui uma etapa **Instalar pacote** , o seguinte erro pode aparecer no arquivo CreateTsMedia.log:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>   
>  Para mídia autônoma que inclui uma etapa de Instalar Pacote, você deve criar a mídia autônoma em um site primário que possui o agente de distribuição de software habilitado ou adicionar uma etapa de **Executar linha de comando** após a etapa **Configurar Windows e ConfigMgr** e antes da primeira etapa **Instalar pacote** . A etapa **Executar linha de comando** executa como um comando WMIC para habilitar o agente de distribuição de software antes da primeira etapa de Instalar pacote ser executada. Você pode usar o seguinte em sua etapa de sequência de tarefas de **Executar linha de comando** :  
>   
>  **Linha de comando**: **WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  
>   
>  Para mais informações sobre como criar mídia autônoma, confira [Create stand-alone media](../deploy-use/create-stand-alone-media.md) (Criar mídia autônoma).  

 Essa etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE.  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Instalar um pacote de software único**  
 Essa configuração especifica um pacote de software do Configuration Manager. A etapa aguardará até que a instalação seja concluída.  

 **Instalar pacotes de software de acordo com a lista de variáveis dinâmicas**  
 Essa configuração especifica o nome de base para um conjunto de variáveis de sequência de tarefas que são definidas para uma coleção ou um computador. Essas variáveis especificam os pacotes que serão instalados para essa coleção ou computador. Cada nome de variável consiste em seu nome de base comum e um sufixo numérico, começando com 001. O valor de cada variável deve conter uma ID de pacote e o nome do software separados por dois-pontos.  

 Para que o software seja instalado usando uma lista de variáveis dinâmicas, a seguinte configuração deve ser habilitada na guia **Avançado** da caixa de diálogo **Propriedades** do pacote: **Permitir que este programa seja instalado da sequência de tarefas de Pacote de Instalação sem ser implantado**  

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

 As condições a seguir afetam o que será instalado:  

-   Se o valor de uma variável não for criado no formato correto ou não especificar uma ID de aplicativo válido e o nome, a instalação do software falhará.  

-   Se a ID do pacote contiver caracteres minúsculos, a instalação desse software falhará.  

-   Se nenhuma variável com o nome de base especificado e o sufixo "001" for encontrado, nenhum pacote será instalado e a sequência de tarefas continuará.  

 **Se a instalação de um pacote de software falhar, continue instalando os outros pacotes da lista**  
 Essa configuração especifica que a etapa continuará se a instalação de um pacote de software individual falhar. Se essa configuração estiver especificada, a sequência de tarefas continuará independentemente de qualquer erro de instalação que é retornado. Se isso não for especificado e a instalação falhar, a etapa de sequência de tarefas terminará imediatamente.  

##  <a name="BKMK_InstallSoftwareUpdates"></a> Instalar Atualizações de Software  
 Use a etapa da sequência de tarefas **Instalar atualizações de software** para instalar atualizações de software no computador de destino. O computador de destino não é avaliado para atualizações de software aplicáveis até que essa etapa de sequência de tarefas seja executada. Nesse momento, o computador de destino é avaliado para atualizações de software como qualquer outro cliente gerenciado pelo Configuration Manager. Em particular, esta etapa instala somente as atualizações de software que são destinadas às coleções dais qual o computador atualmente é um membro.  
>  [!IMPORTANT]
>Recomendamos que você instale a versão mais recente do Windows Update Agent para obter um desempenho muito melhor ao usar a etapa da sequência de tarefas Instalar Atualizações de Software.
>* Para o Windows 7, consulte na [Base de Dados de Conhecimento o artigo 3161647](https://support.microsoft.com/kb/3161647).
>* Para o Windows 8, consulte na [Base de Dados de Conhecimento o artigo 3163023](https://support.microsoft.com/kb/3163023).

 Essa etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE. Para obter informações sobre variáveis de sequência de tarefas para esta ação da sequência de tarefas, veja [Install Software Updates Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_InstallSoftwareUpdates).

 > [!NOTE]
 > Você pode usar as variáveis internas SMSTSMPListRequestTimeoutEnabled e SMSTSMPListRequestTimeout para habilitar e especificar quantos milissegundos uma sequência de tarefas espera antes de tentar instalar novamente uma atualização de software ou aplicativo após uma falha ao recuperar a lista de pontos de gerenciamento dos serviços de localização. Para obter mais informações, consulte [Variáveis internas da sequência de tarefas](task-sequence-built-in-variables.md).

> [!NOTE]
>Na guia Opções, você pode configurar esta sequência de tarefas para ser repetida se o computador for reiniciado inesperadamente. Por exemplo, uma instalação de atualização de software que reinicia automaticamente o computador. A partir do Configuration Manager 1602, você pode configurar a variável SMSTSWaitForSecondReboot para especificar por quanto tempo (em segundos) a sequência de tarefas deve pausar após o computador ser reiniciado ao instalar as atualizações de software. Para obter mais informações, consulte [Variáveis internas da sequência de tarefas](task-sequence-built-in-variables.md).

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especifique para repetir esta etapa se o computador for reiniciado de forma inesperada. Também é possível especificar a quantidade de vezes da repetição após uma reinicialização.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Necessárias para instalação – somente atualizações de software obrigatórias**  
 Selecione esta opção para instalar todas as atualizações de software sinalizadas no Configuration Manager como obrigatórias para os computadores de destino que recebem a sequência de tarefas. Atualizações de software obrigatórias têm prazos definidos pelo administrador para a instalação.  

 **Disponíveis para instalação – todas as atualizações de software**  
 Selecione esta opção para instalar todas as atualizações de software disponíveis direcionando a coleção do Configuration Manager que receberá a sequência de tarefas. Todas as atualizações de software disponíveis serão instaladas nos computadores de destino.  

 **Avaliar as atualizações de software dos resultados da varredura em cache**  
A partir da versão 1606 do Configuration Manager, você tem a opção de fazer uma verificação completa em busca de atualizações de software em vez de usar os resultados da verificação em cache. Por padrão, a sequência de tarefas usa resultados em cache. Você pode desmarcar a caixa de seleção para que o cliente se conecte ao ponto de atualização de software para processar e baixar o catálogo de atualizações de software mais recente. Você pode escolher essa opção quando usar uma sequência de tarefas para [capturar e criar uma imagem de sistema operacional](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md), em que você sabe que haverá um grande número de atualizações de software, especialmente muitas que têm dependências (é necessário instalar X antes que Y apareça como aplicável). Ao desmarcar essa configuração e implantar a sequência de tarefas em um grande número de clientes, todos eles se conectarão ao ponto de atualização de software ao mesmo tempo. Isso pode resultar em problemas de desempenho durante o processo e o download do catálogo. Na maioria dos casos, é recomendável que você use a configuração padrão.

A nova variável de sequência de tarefas, SMSTSSoftwareUpdateScanTimeout, foi introduzida na versão 1606 do Configuration Manager para possibilitar que você controle o tempo limite da verificação de atualizações de software durante a etapa da sequência de tarefas de Instalar atualizações de software. O valor padrão é 30 minutos. Para obter mais informações, consulte [Variáveis internas da sequência de tarefas](task-sequence-built-in-variables.md).


##  <a name="BKMK_JoinDomainorWorkgroup"></a> Ingressar no Domínio ou Grupo de Trabalho  
 Use a etapa da sequência de tarefas **Ingressar no domínio ou grupo de trabalho** para adicionar o computador de destino a um grupo de trabalho ou domínio.  

 Essa etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE. Para obter informações sobre variáveis de sequência de tarefas para esta ação da sequência de tarefas, veja [Join Domain or Workgroup Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_JoinDomainWorkgroup).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Ingressar no grupo de trabalho**  
 Selecione esta opção para fazer o computador de destino ingressar no grupo de trabalho especificado. Se o computador atualmente é um membro de um domínio, selecionar esta opção fará com que o computador seja reinicializado.  

 **Ingressar em um domínio**  
 Selecione esta opção para fazer o computador de destino ingressar no domínio especificado.  

 Opcionalmente, digite ou navegue para uma unidade organizacional (UO) no domínio especificado para ingressar o computador. Se o computador atualmente for um membro de algum outro domínio ou grupo de trabalho, isso causará a reinicialização do computador. Se o computador já for um membro de alguma outra OU, o Active Directory Domain Services não permitirá alterar a unidade organizacional e essa configuração será ignorada.  

 **Insira a conta que tem permissão para ingressar no domínio**  
 Clique em **Definir** para inserir uma conta e senha com permissões para ingressar no domínio. A conta deve ser inserida no seguinte formato:  

 *Domínio\conta*  

## <a name="BKMK_PrepareConfigMgrClientforCapture"></a> Preparar ConfigMgr Client for Capture  
Use a etapa **Preparar o Cliente do ConfigMgr para Captura** para remover o cliente do Configuration Manager ou configurar o cliente no computador de referência e prepará-lo para captura como parte do processo de geração de imagens.

Com início no Configuration Manager versão 1610, a etapa Preparar o Cliente do ConfigMgr agora removerá completamente o cliente do Configuration Manager, em vez de apenas remover informações importantes. Quando a sequência de tarefas implantar a imagem capturada do sistema operacional, ela instalará um novo cliente do Configuration Manager sempre.  

Antes do Configuration Manager versão 1610, esta etapa executa as seguintes tarefas:  

-   Remove a seção de propriedades de configuração de cliente do arquivo smscfg.ini no diretório do Windows. Essas propriedades incluem informações específicas do cliente incluindo o GUID do Configuration Manager e outros identificadores de cliente.  

-   Exclui todos os certificados do computador do SMS ou do Configuration Manager.  

-   Exclui o cache do cliente do Configuration Manager.  

-   Apaga a variável de site atribuída ao cliente do Configuration Manager.  

-   Exclui todas as políticas locais do Configuration Manager.  

-   Remove a chave raiz confiável para o cliente do Configuration Manager.  

 Essa etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE.  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

##  <a name="BKMK_PrepareWindowsforCapture"></a> Preparar Windows para Captura  
 Use a etapa da sequência de tarefas **Preparar o Windows para captura** para especificar as opções do Sysprep a usar ao capturar uma imagem do sistema operacional no computador de referência. Esta ação de sequência de tarefas executa o Sysprep e reinicia o computador na imagem de inicialização do Windows PE especificado para a sequência de tarefas. O computador de referência não deve estar associado a um domínio para essa ação ser concluída com êxito.  

 Essa etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE. Para obter informações sobre variáveis de sequência de tarefas para esta ação da sequência de tarefas, veja [Prepare Windows for Capture Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_PrepareWindowsCapture).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Construir lista de drivers de armazenamento em massa automaticamente**  
 Selecione esta opção para fazer com que o Sysprep crie automaticamente uma lista de drivers de armazenamento em massa do computador de referência. Essa opção habilita a opção de criar drivers de armazenamento em massa no arquivo sysprep.inf no computador de referência. Para obter mais informações sobre essa configuração, consulte a documentação do Sysprep.  

 **Não redefinir sinalizador de ativação**  
 Selecione esta opção para impedir que o Sysprep redefina o sinalizador de ativação do produto.  

##  <a name="BKMK_PreProvisionBitLocker"></a> Pré-provisionar o BitLocker  
 Use a etapa **Pré-provisionar o BitLocker** para habilitar o BitLocker em uma unidade no Windows PE. Apenas o espaço em disco usado é criptografado e, portanto, os tempos de criptografia são muito mais rápidos. Aplique as opções de gerenciamento de chaves usando a etapa da sequência de tarefas do [Habilitar BitLocker](#BKMK_EnableBitLocker) depois que o sistema operacional for instalado. Esta etapa é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão.  

> [!IMPORTANT]  
>  Para pré-provisionar o BitLocker, você deve implantar um sistema operacional mínimo do Windows 7 e o TPM deve ser suportado e estar habilitado no computador.  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Especificar um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Especificar informações detalhadas sobre a ação realizada nesta etapa.  

 **Aplicar BitLocker à unidade especificada**  
 Especificar a unidade para a qual você deseja habilitar o BitLocker. Apenas o espaço usado em disco está criptografado.  

 **Ignorar esta etapa para computadores que não têm um TPM ou quando o TPM não está habilitado**  
 Selecione esta opção para ignorar a criptografia de unidade quando o hardware do computador não oferece suporte a TPM ou TPM não está habilitado. Por exemplo, você pode usar esta opção ao implantar um sistema operacional em uma máquina virtual.  

##  <a name="BKMK_ReleaseStateStore"></a> Liberar Armazenamento de Estado  
 Use a etapa da sequência de tarefas **Liberar armazenamento de estado** para notificar a migração de estado do ponto que a ação de captura ou restauração foi concluída. Esta etapa é usada em conjunto com as etapas de sequência de tarefas **solicitar armazenamento de estado**, **Capturar estado do usuário**, e **Restaurar estado do usuário** para migrar dados de estado do usuário usando um ponto de migração de estado e a ferramenta de migração de estado do usuário (USMT).  

 Para mais informações sobre como gerenciar o estado do usuário ao implantar sistemas operacionais, confira [Gerenciar o estado do usuário](../get-started/manage-user-state.md).  

 Se você solicitou acesso a um ponto de migração de estado para capturar o estado do usuário na etapa da sequência de tarefas **Solicitar armazenamento de estado**  , esta etapa notifica o ponto de migração de estado de que o processo de captura foi concluído e que os dados de estado do usuário estão disponíveis para restauração. O ponto de migração de estado define as permissões de controle de acesso ao estado capturado, para que somente possa ser acessado (como somente leitura) pelo computador de restauração.  

 Se você solicitar acesso a um ponto de migração de estado para restaurar o estado do usuário na etapa da sequência de tarefa **Solicitar armazenamento de estado** , ela notifica o ponto de migração de estado que o processo de restauração foi concluído. Neste ponto, quaisquer configurações de retenção configuradas para o ponto de migração de estado são ativadas.  

> [!IMPORTANT]  
>  É uma prática recomendada definir **Continuar em caos de erro** em qualquer tarefa de sequência de etapas entre as etapas **Solicitar armazenamento de estado** e **Liberar armazenamento de estado** para que cada ação **solicitar armazenamento de estado** tenha uma ação **Liberar armazenamento de estado** correspondente.  

 Essa etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE. Para obter informações sobre variáveis de sequência de tarefas para esta ação da sequência de tarefas, veja [Release State Store Sequence Action Variables](task-sequence-action-variables.md#BKMK_ReleaseStateStore).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

##  <a name="BKMK_RequestStateStore"></a> Solicitar Armazenamento de Estado  
 Use a etapa da sequência de tarefas **Solicitar armazenamento de estado** para solicitar acesso a um ponto de migração de estado durante a captura de estado ou a restauração de estado em um computador.  

 Para mais informações sobre como gerenciar o estado do usuário ao implantar sistemas operacionais, confira [Gerenciar o estado do usuário](../get-started/manage-user-state.md).  

 Você pode usar a etapa **Solicitar armazenamento de estado** da sequência de tarefas em conjunto com o as etapas **Liberar armazenamento de estado**, **Capturar estado do usuário**, e **Restaurar estado do usuário** para migrar o estado do computador usando um ponto de migração de estado e a ferramenta de migração de estado do usuário (USMT).  

> [!NOTE]  
>  Se você acabou de estabelecer uma nova função de site do ponto de migração estado (SMP), poderá levar até uma hora para ela estar disponível para armazenamento de estado do usuário. Para agilizar a disponibilidade do SMP, você pode ajustar qualquer configuração de propriedade de ponto de migração do estado para disparar uma atualização de arquivo de controle do site.  

 Essa etapa de sequência de tarefas é executada em um sistema operacional padrão e no Windows PE para USMT offline. Para obter informações sobre as variáveis de sequência de tarefas para esta ação da sequência de tarefas, veja [Request State Store Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RequestState).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Capturar estado do computador**  
 Localiza um ponto de migração de estado que atenda aos requisitos mínimos definidos nas configurações de ponto de migração de estado (número máximo de clientes e a quantidade mínima de espaço livre em disco), mas não garante que o espaço em disco esteja disponível no momento da migração de estado. Esta opção solicitará acesso ao ponto de migração de estado para capturar o estado do usuário e configurações de um computador.  

 Se o site do Configuration Manager tiver vários pontos de migração de estado habilitados, essa etapa de sequência de tarefas encontrará um ponto de migração de estado com espaço em disco disponível consultando o ponto de gerenciamento do site para obter uma lista dos pontos de migração de estado e avaliará cada um até encontrar um que atenda aos requisitos mínimos.  

 **Restaurar estado de outro computador**  
 Selecione esta opção para solicitar acesso a um ponto de migração de estado para a restauração de estado do usuário e configurações capturados anteriormente no computador de destino.  

 Se site do Configuration Manager tiver vários pontos de migração, essa etapa de sequência de tarefas localizará o ponto de migração de estado que tem o estado do computador que foi armazenado no computador de destino.  

 **Número de tentativas**  
 O número de vezes que essa etapa de sequência de tarefas tentará localizar um ponto de migração de estado apropriado antes de falhar.  

 **Atraso na repetição (em segundos)**  
 A quantidade de tempo em segundos que a etapa de sequência de tarefas espera entre as novas tentativas.  

 **Se a conta de computador não conseguir se conectar a um armazenamento de estado, use a conta de acesso à rede.**  
 Especifica que as credenciais da conta de acesso de rede do Configuration Manager serão usadas para se conectar ao ponto de migração de estado, se o cliente do Configuration Manager não conseguir acessar o armazenamento de estado do SMP usando a conta de computador. Essa opção é menos segura porque outros computadores poderiam usar a conta de acesso à rede para acessar o estado armazenado, mas pode ser necessária se o computador de destino não estiver integrado ao domínio.  

##  <a name="BKMK_RestartComputer"></a> Reiniciar Computador  
 Use a etapa da sequência de tarefas **Reiniciar computador** para reiniciar o computador que executa a sequência de tarefas. Após a reinicialização, o computador continuará automaticamente com a próxima etapa na sequência de tarefas.  

 Esta etapa pode ser executada em um sistema operacional padrão ou no Windows PE. Para mais informações sobre as variáveis de sequência de tarefas para esta ação da sequência de tarefas, confira [Restart computer task sequence action variables](task-sequence-action-variables.md#BKMK_RestartComputer) (Reiniciar as variáveis de ação da sequência de tarefas do computador).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **A imagem de inicialização atribuída a esta sequência de tarefas**  
 Selecione esta opção para o computador de destino usar a imagem de inicialização atribuída à sequência de tarefas. A imagem de inicialização será usada para executar as etapas da sequência de tarefas subsequentes que executadas no Windows PE.  

 **Sistema operacional padrão instalado atualmente**  
 Selecione esta opção para o computador de destino ser reinicializado no sistema operacional instalado.  

 **Notificar usuário antes de reiniciar**  
 Selecione esta opção para exibir uma notificação ao usuário que o computador de destino será reiniciado. Essa opção é habilitada por padrão.  

 **Mensagem de notificação**  
 Digite uma mensagem de notificação será exibida para o usuário antes do computador de destino ser reiniciado.  

 **Tempo limite de exibição da mensagem**  
 Especifique a quantidade de tempo em segundos um usuário terá antes do computador de destino ser reiniciado. A quantidade de tempo padrão é de sessenta (60) segundos.  

##  <a name="BKMK_RestoreUserState"></a> Restaurar Estado do Usuário  
 Use a etapa da sequência de tarefas **Restaurar estado do usuário** para iniciar a Ferramenta de Migração do Estado do Usuário (USMT) para restaurar o estado do usuário e configurações no computador de destino. Essa etapa de sequência de tarefas é usada em conjunto com a etapa da sequência de tarefas **Capturar o estado do usuário** .  

 Para mais informações sobre como gerenciar o estado do usuário ao implantar sistemas operacionais, confira [Gerenciar o estado do usuário](../get-started/manage-user-state.md).  

 Você também poderá usar a etapa da sequência de tarefas **Restaurar Estado do Usuário** com as etapas **Solicitar Armazenamento de Estado** e **Liberar Armazenamento de Estado** se quiser salvar as configurações de estado ou restaurar as configurações de um ponto de migração de estado no site do Configuration Manager. Com o USMT 3.0 e superior, essa opção sempre criptografa o armazenamento de estado do USMT usando uma chave de criptografia geradas e gerenciadas por Configuration Manager.  

 A etapa da sequência de tarefas **Restaurar estado do usuário** fornece controle sobre um subconjunto limitado dos mais opções mais usadas do USMT. Opções de linha de comando adicionais podem ser especificadas usando a variável de sequência de tarefas OSDMigrateAdditionalRestoreOptions.  

> [!IMPORTANT]  
>  Se estiver usando a etapa da sequência de tarefas **Restaurar Estado do Usuário** para uma finalidade não relacionada a um cenário de implantação de sistema operacional, adicione a etapa [Reiniciar Computador](#BKMK_RestartComputer) imediatamente após a etapa da sequência de tarefas **Restaurar Estado do Usuário** .  

 Essa etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE. Para obter informações sobre as variáveis de sequência de tarefas para esta ação da sequência de tarefas, veja [Restore User State Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RestoreUserState).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Especifica um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Especifica informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Pacote da ferramenta de migração do usuário**  
 Insira o pacote do Configuration Manager que contém a versão do USMT para essa etapa usar durante a restauração de estado do usuário e suas configurações. Este pacote não exige um programa. Quando a etapa da sequência de tarefas é executada, a sequência de tarefas usará a versão da USMT no pacote que você especificar. Especifique um pacote contendo a versão 32 bits ou x64 do USMT de acordo com a arquitetura do sistema operacional para o qual você está restaurando o estado.  

 **Restaurar todos os perfis de usuários capturados com as opções padrão**  
 Restaura os perfis de usuário com as opções padrão. Para personalizar as opções que serão restauradas, selecione **Personalizar captura de perfil do usuário**.  

 **Personalizar o modo como os perfis de usuário são restaurados**  
 Permite que você personalize os arquivos que você deseja restaurar o computador de destino. Clique em **Arquivos** para especificar os arquivos de configuração do pacote do USMT que deseja usar para restaurar os perfis de usuário. Para adicionar um arquivo de configuração, digite o nome do arquivo na caixa **Nome do arquivo** e clique em **Adicionar**. Os arquivos de configuração que serão usados para a operação são listados no painel de arquivos. O arquivo .xml que você especificar define qual arquivo de usuário será restaurado.  

 **Restaurar perfis de usuário do computador local**  
 Restaura os perfis de usuário do computador local (ou seja, não o usuário de domínio). Você precisará atribuir novas senhas para as contas de usuário local restaurado porque as senhas de conta de usuário local original não podem ser migradas. Digite a senha nova na caixa **Senha** e confirme a senha em **Confirmar senha** .  

 **Continuar, se alguns arquivos não forem restaurados**  
 Continua a restauração das configurações e estado do usuário, mesmo se alguns arquivos não puderem ser restaurados. Essa opção é habilitada por padrão. Se você desabilitar essa opção e forem encontrados erros durante a restauração de arquivos, a etapa da sequência de tarefas terminará imediatamente com falha e nem todos os arquivos serão restaurados.  

 **Habilitar log detalhado**  
 Habilite esta opção para gerar informações de arquivo de log mais detalhadas. Durante a restauração de estado, o Loadtate.log é gerado e armazenado na pasta de log da sequência de tarefas na pasta \windows\system32\ccm\logs por padrão.  

##  <a name="BKMK_RunCommandLine"></a> Executar Linha de Comando  
 Use a etapa da sequência de tarefas **Executar linha de comando** para executar uma linha de comando especificada.  

 Esta etapa pode ser executada em um sistema operacional padrão ou no Windows PE. Para obter informações sobre variáveis de sequência de tarefas para esta ação da sequência de tarefas, veja [Run Command Line Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RunCommand).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Especifica um nome curto definido pelo usuário que descreve a linha de comando executada.  

 **Descrição**  
 Especifica as informações mais detalhadas sobre a linha de comando que é executada.  

 **Linha de comando**  
 Especifica a linha de comando que é executada. Esse campo é obrigatório. A inclusão das extensões no nome de arquivo é uma prática recomendada, por exemplo, .vbs e .exe. Inclua todos os arquivos de configurações necessários, as opções de linha de comando ou opções.  

 Se o nome do arquivo não tiver uma extensão de nome de arquivo especificada, o Configuration Manager tentará usar .com, .exe, e.bat. Se o nome do arquivo tiver uma extensão que não é um executável, o Configuration Manager tentará aplicar uma associação local. Por exemplo, se a linha de comando for readme.gif, o Configuration Manager iniciará o aplicativo especificado no computador de destino para abrir arquivos .gif.  

 Exemplos:  

 **setup.exe /a**  

 **cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat**  

> [!NOTE]  
>  Ações de linha de comando, como redirecionamento de saída, tubulação ou cópia, como no exemplo anterior, devem ser precedidas pelo comando **cmd.exe /c** para serem executadas com êxito.  

 **Desabilitar o redirecionamento de sistema de arquivos de 64 bits**  
 Por padrão, quando executado em um sistema operacional de 64 bits, o executável na linha de comando é localizado e executado usando o redirecionador do sistema de arquivos do WOW64 para que as versões de 32 bits dos executáveis e DLLs do sistema operacional sejam encontradas.  Selecionar esta opção desabilita o uso do redirecionador do sistema de arquivos do WOW64 para que as versões nativas de 64 bits de DLLs e executáveis do sistema operacional possam ser encontradas.  Selecionar esta opção não terá nenhum efeito em um sistema operacional de 32 bits.  

 **Iniciar em**  
 Especifica a pasta do executável do programa, até 127 caracteres. Essa pasta pode ser um caminho absoluto no computador de destino ou um caminho relativo à pasta do ponto de distribuição que contém os arquivos de instalação. Esse campo é opcional.  

 Exemplos:  

 **c:\officexp**  

 **i386**  

> [!NOTE]  
>  O botão **Procurar** procura o computador local em busca de arquivos e pastas, assim qualquer coisa selecionada desta forma deverá existir no computador de destino no mesmo local e com os mesmos nomes de arquivo e pasta.  

 **Pacote**  
 Quando você especificar arquivos ou programas na linha de comando que ainda não estão presentes no computador de destino, selecione essa opção para especificar o pacote do Configuration Manager que contém os arquivos apropriados. Este pacote não exige um programa. Esta opção não é necessária se os arquivos especificados existirem no computador de destino.  

 **Tempo limite**  
 Especifica um valor que representa quanto tempo o Configuration Manager permitirá para execução da linha de comando. Esse valor pode ser de 1 a 999 minutos. O valor padrão é 15 minutos.  

 Essa opção é desabilitada por padrão.  

> [!IMPORTANT]  
>  Se você inserir um valor que não reserva tempo suficiente para a etapa de sequência de tarefas Executar linha de comando ser concluída com êxito, ela falhará e a sequência de tarefas inteira poderá falhar dependendo de outras configurações de controle. Se o tempo limite expirar, o Configuration Manager encerrará o processo de linha de comando.  

 **Executar esta etapa usando a seguinte conta**  
 Especifica que a linha de comando é executada como uma conta de usuário do Windows diferente da conta sistema local.  

> [!NOTE]  
>  Quando você especificar outra conta para esta etapa e ela ocorrer após uma etapa de instalação do sistema operacional, a conta deverá ser adicionada ao computador para que seja possível executar comandos ou scripts simples, e o perfil da conta de usuário do Windows deverá ser restaurado para executar programas mais complexos, como um MSI.  

 **Conta**  
 Especifica a conta de usuário do Windows para execução da tarefa de linha de comando na sequência de tarefas executada por esta ação. A linha de comando será executada com as permissões da conta especificada. Clique em **Definir** para especificar o usuário local ou a conta de domínio.  

> [!IMPORTANT]  
>  Se uma ação da sequência de tarefa **Executar linha de comando** especificando uma conta de usuário for executada no Windows PE, a ação falhará, porque o Windows PE não pode ser associado a um domínio. A falha será registrada no arquivo smsts.log.  

##  <a name="BKMK_RunPowerShellScript"></a> Executar Script do PowerShell  
 Use a etapa da sequência de tarefas **Executar Script do PowerShell** para executar um script do PowerShell especificado.  

 Esta etapa pode ser executada em um sistema operacional padrão ou no Windows PE. Para executar esta etapa no Windows PE, o PowerShell deve ser habilitado na imagem de inicialização. Você pode habilitar o Windows PowerShell (WinPE-PowerShell) na guia **Componentes opcionais** nas propriedades da imagem de inicialização. Para mais informações sobre como modificar uma imagem de inicialização, confira [Manage boot images](../get-started/manage-boot-images.md) (Gerenciar imagens de inicialização).  

> [!NOTE]  
>  O PowerShell não é habilitado por padrão nos sistemas operacionais Windows Embedded.  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Especifica um nome curto definido pelo usuário que descreve a linha de comando executada.  

 **Descrição**  
 Especifica as informações mais detalhadas sobre a linha de comando que é executada.  

 **Pacote**  
 Especifique o pacote do Configuration Manager que contém o script do PowerShell. Um pacote pode conter vários scripts do PowerShell.  

 **Nome do script**  
 Especifica o nome do script do PowerShell para executar. Esse campo é obrigatório.  

 **Parâmetros**  
 Especifica os parâmetros a serem passados para o script do Windows PowerShell. Configure os parâmetros, como se você estivesse adicionando-os ao script do Windows PowerShell em uma linha de comando.  

> [!IMPORTANT]  
>  Forneça parâmetros consumidos pelo script, não pela linha de comando do Windows PowerShell.  
>   
>  O exemplo a seguir contém parâmetros válidos:  
>   
>  **-MyParameter1 MyValue1 -MyParameter2 MyValue2**  
>   
>  O exemplo a seguir contém parâmetros inválidos. Os itens em negrito são parâmetros de linha de comando do Windows PowerShell (-nologo e -executionpolicy unrestricted) e não consumidos pelo script.  
>   
>  **-nologo-executionpolicy unrestricted-File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2**  

 **Política de execução do PowerShell**  
 Selecione a política de execução do PowerShell que permite determinar quais scripts do Windows PowerShell (se houver) poderão ser executados no computador. Selecione uma das seguintes políticas de execução:  

-   **AllSigned**: somente scripts assinados por um fornecedor confiável podem ser executados.  

-   **Undefined**: nenhuma política de execução é definida. .  

-   **Bypass**: carrega todos os arquivos de configuração e executa todos os scripts. Se você executar um script não assinado que foi baixado da Internet, nenhuma permissão será solicitada antes de executar.  

> [!IMPORTANT]  
>  O PowerShell 1.0 não suporta as políticas de execução Indefinido e Ignorar.  

##  <a name="BKMK_SetDynamicVariables"></a> Definir Variáveis Dinâmicas  
 Use a etapa da sequência de tarefas **Definir variáveis dinâmicas** para executar o seguinte:  

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

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

**Nome**  
 Um nome curto do definido pelo usuário para essa etapa de sequência de tarefas.  

**Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

**Regras e variáveis dinâmicas**  
 Para definir uma variável dinâmica para usar na sequência de tarefas, você pode adicionar uma regra e especificar um valor para cada variável especificada para a regra, ou então adicionar uma ou mais variáveis para definir sem adicionar uma regra. Quando você adiciona uma regra, poderá escolher entre as seguintes categorias de regra:  

 -   **Computador**: use esta categoria de regra para avaliar valores para a marcação de Ativo, UUID, número de série ou endereço MAC. Você pode definir vários valores, e se qualquer valor for verdadeiro, então a regra será avaliada como verdadeira. Por exemplo, a regra a seguir retornará verdadeiro se o número de série for 5892087 independentemente de o endereço MAC ser igual a 26-78-13-5A-A4-22.  

     `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

-   **Local**: use esta categoria de regra para avaliar valores para o gateway padrão.  

-   **Marca e modelo**: use esta categoria de regra para avaliar valores para a marca e o modelo de um computador. A marca e o modelo devem ambas serem avaliadas como verdadeiro para a regra a ser avaliada como verdadeiro.   

    Começando no Configuration Manager versão 1610, você pode especificar um asterisco (*****) e um ponto de interrogação (**?**) como caracteres curinga, em que ***** corresponde a vários caracteres e **?** corresponde a um único caractere. Por exemplo, a cadeia de caracteres "DELL*900?" corresponderá a DELL-ABC-9001 e DELL9009.

-   **Variável de Sequência de Tarefas**: use esta categoria de regra para adicionar uma variável de sequência de tarefas, uma condição e um valor a ser avaliado. A regra avalia como verdadeiro quando o valor definido para a variável atende a condição especificada.  

Você pode especificar uma ou mais variáveis que serão definidas para uma regra que é avaliada como verdadeiro ou definir variáveis sem usar uma regra. Você pode selecionar entre as variáveis existentes ou criar uma variável personalizada.  

 -   **Variáveis de sequência de tarefas existentes**: use essa configuração para selecionar uma ou mais variáveis em uma lista de variáveis de sequência de tarefas existentes. Variáveis de matriz não estão disponíveis para selecionar.  

 -   **Variáveis personalizadas da sequência de tarefas**: use essa configuração para definir uma variável personalizada da sequência de tarefas. Você também pode especificar uma variável de sequência de tarefas existente. Isso é útil para especificar uma matriz de variáveis existente, como OSDAdapter, pois matrizes de variáveis não estão na lista de variáveis de sequência de tarefas existente.  

Depois de selecionar as variáveis de uma regra, você deve fornecer um valor para cada variável. A variável é definida como o valor especificado quando a regra for avaliada como verdadeiro. Para cada variável, você pode selecionar o **Valor secreto** para ocultar o valor da variável. Por padrão, algumas variáveis existentes ocultam valores, como a variável de sequência de tarefas OSDCaptureAccountPassword.  

> [!IMPORTANT]  
>  Quando você importa uma sequência de tarefas com a etapa Definir variáveis dinâmicas, o **Valor secreto** é selecionado para o valor da variável, sendo o valor removido ao importar a sequência de tarefas. Como resultado, você deve reinserir o valor da variável dinâmica novamente depois de importar a sequência de tarefas.  

##  <a name="BKMK_SetTaskSequenceVariable"></a> Definir Variável de Sequência de Tarefas  
Use a etapa **Definir variável de sequência de tarefas** para definir o valor de uma variável usada com a sequência de tarefas.  

Esta etapa pode ser executada em um sistema operacional padrão ou no Windows PE. Variáveis de sequência de tarefas são lidas por ações de sequência de tarefas e especificam o comportamento dessas ações. Para mais informações sobre variáveis de sequência de tarefas específicas, confira [Task sequence action variables](task-sequence-action-variables.md) (Variáveis de ação de sequência de tarefas).  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto do definido pelo usuário para essa etapa de sequência de tarefas.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Variável de sequência de tarefas**  
 Um nome definido pelo usuário para a variável de sequência de tarefas.  

 **Valor**  
 O valor que associado à variável de sequência de tarefas. O valor pode ser outra variável de sequência de tarefas na sintaxe %<varname\>%.  

## <a name="hide-task-sequence-progress"></a>Ocultar o progresso da sequência de tarefas
<!-- 1354291 -->
Com a versão 1706, você pode controlar quando o andamento da sequência de tarefas é exibido aos usuários finais por meio de uma nova variável. Em sua sequência de tarefas, use a etapa **Definir Variável de Sequência de Tarefas** para definir o valor para a variável **TSDisableProgressUI** a fim de ocultar ou exibir o andamento da sequência de tarefas. Você pode usar a etapa Definir Variável de Sequência de Tarefas várias vezes em uma sequência de tarefas para alterar o valor da variável. Isso permite que você oculte ou exiba o andamento da sequência de tarefas em diferentes seções da sequência de tarefas.

 - **Para ocultar o progresso da sequência de tarefas**  
No editor de sequência de tarefas, use a etapa [Definir Variável de Sequência de Tarefas](#BKMK_SetTaskSequenceVariable) para definir o valor da variável **TSDisableProgressUI** como **True** a fim de ocultar o andamento da sequência de tarefas.

 - **Para exibir o andamento da sequência de tarefas**  
No editor de sequência de tarefas, use a etapa [Definir Variável de Sequência de Tarefas](#BKMK_SetTaskSequenceVariable) para definir o valor da variável **TSDisableProgressUI** como **False** a fim de exibir o andamento da sequência de tarefas.

##  <a name="BKMK_SetupWindowsandConfigMgr"></a> Instalar Windows e ConfigMgr  
 Use a etapa **Instalação do Windows e ConfigMgr** para realizar a transição do Windows PE para o novo sistema operacional. Esta etapa da sequência de tarefas é necessária em qualquer implantação de sistema operacional. Ele instala o cliente do Configuration Manager no novo sistema operacional e prepara a sequência de tarefas para continuar a execução no novo sistema operacional.  

 Esta etapa é executada somente no Windows PE. Ela não é executada em um sistema operacional padrão. Para obter mais informações sobre variáveis de sequência de tarefas para esta ação, consulte [Setup Windows and ConfigMgr task sequence action variables](task-sequence-action-variables.md#BKMK_SetupWindows) (Variáveis da ação da sequência de tarefas de Instalar Windows e ConfigMgr).  

 A ação de sequência de tarefas **Instalar o Windows e o ConfigMgr** substitui as variáveis de diretório sysprep.inf ou unattend.xml, tais como %WINDIR% e %ProgramFiles%, pelo diretório de instalação do Windows PE X:\Windows. Variáveis de sequência de tarefas especificadas usando essas variáveis de ambiente serão ignorados.  

 Use essa etapa de sequência de tarefas para executar as seguintes ações:  

1.  Etapas preliminares: Windows PE  

    1.  Executa a substituição de variável de sequência de tarefas no arquivo unattend.xml.  

    2.  Baixa o pacote que contém o cliente do Configuration Manager e o coloca na imagem implantada.  

2.  Configurar o Windows  

    1.  Instalação baseada em imagem.  

        1.  Desabilita o cliente do Configuration Manager na imagem (ou seja, desabilita a Inicialização automática para o serviço do cliente do Configuration Manager).  

        2.  Atualiza o registro da imagem implantada para garantir que o sistema operacional implantado comece com a mesma letra que a unidade tinha no computador de referência.  

        3.  Reinicia o sistema operacional implantado.  

        4.  Mini-instalação do Windows executada usando o arquivo sysprep.inf ou unattend.xml especificado com todas as interações do usuário final suprimidas. Observação: se a opção **Aplicar Configurações de Rede** especificou o ingresso em um domínio, essa informação estará no arquivo sysprep.inf ou unattend.xml e a mini-instalação do Windows executará o ingresso no domínio.  

    2.  Instalação baseada em Setup.exe.  Executa o Setup.exe que segue o processo de instalação típica do Windows:  

        1.  Copia o pacote de instalação do sistema operacional especificado em uma sequência de tarefas **Aplicar sistema operacional** anterior para a unidade de disco rígido.  

        2.  Reinicia o sistema operacional recém-implantado.  

        3.  Mini-instalação do Windows executada usando o arquivo sysprep.inf ou unattend.xml especificado com todas as interfaces do usuário suprimidas. Observação: se a opção **Aplicar Configurações de Rede** especificou o ingresso em um domínio, essa informação estará no arquivo sysprep.inf ou unattend.xml e a mini-instalação do Windows executará o ingresso no domínio.  

3.  Instalar o cliente do Configuration Manager  

    1.  Após a conclusão da mini-instalação do Windows, a sequência de tarefas é retomada usando setupcomplete.cmd.  

    2.  Habilita ou desabilita a conta de administrador local, com base na opção selecionada na etapa **Aplicar configurações do Windows** .  

    3.  Instala o cliente do Configuration Manager usando o pacote baixado anteriormente (1.b) e as propriedades de instalação especificadas no Editor de Sequência de Tarefas. O cliente está instalado em "modo de provisionamento" para impedir o processamento de novas solicitações de política de até que a sequência de tarefas seja concluída.  

    4.  Aguarda até que o cliente esteja totalmente operacional.  

    5.  Se o computador estiver operando em um ambiente com proteção de acesso à rede habilitado, o cliente verifica e instala as atualizações necessárias para que todas as atualizações necessárias estejam presentes antes de continuar com a sequência de tarefas em execução.  

4.  A sequência de tarefas continua sendo executada na sua próxima etapa.  

> [!NOTE]  
>  A ação **Instalação do Windows e ConfigMgr** da sequência de tarefas é responsável pela execução da política de grupo no computador recém-instalado. A Política de Grupo é aplicada após a conclusão da sequência de tarefas.  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Não especifique que a sequência de tarefas continue se ocorrer um erro durante a execução da etapa. Se houver um erro, a sequência de tarefas falhará, independentemente se você selecionar ou não esta configuração.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Especifica um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Especifica informações adicionais sobre a ação realizada nesta etapa.  

 **Pacote do cliente**  
 Especifica o pacote de instalação do cliente do Configuration Manager que será usado por essa etapa de sequência de tarefas. Clique em **Procurar** e selecione o pacote de instalação de cliente que você deseja usar para instalar o cliente do Configuration Manager.  

 **Usar pacote de cliente de pré-produção quando disponível**  
 Especifica que, se houver um pacote de cliente de pré-produção disponível, a etapa da sequência de tarefas usará esse pacote em vez do pacote do cliente de produção. Normalmente, o cliente de pré-produção é uma versão mais recente que está sendo testada no ambiente de produção. Clique em **Procurar** e selecione o pacote de instalação de cliente de pré-produção que você deseja usar para instalar o cliente do Configuration Manager.  

 **Propriedades de Instalação**  
 Atribuição de site e a configuração padrão são automaticamente especificadas pela ação de sequência de tarefas. Você pode usar esse campo para especificar as propriedades adicionais de instalação a serem usada ao instalar o cliente. Para inserir várias propriedades de instalação, separe-as com um espaço.  

 Você pode especificar as opções de linha de comando usadas durante a instalação do cliente. Por exemplo, você pode inserir **/skipprereq: silverlight.exe** para informar o CCMSetup.exe para não instalar o pré-requisito do Microsoft Silverlight. Para mais informações sobre as opções de linha de comando disponíveis para o CCMSetup.exe, confira [About client installation properties](../../core/clients/deploy/about-client-installation-properties.md) (Sobre as propriedades da instalação do cliente).  

##  <a name="BKMK_UpgradeOS"></a> Atualizar o sistema operacional  
 Use a etapa da sequência de tarefas **Atualizar Sistema Operacional** para atualizar um sistema operacional existente do Windows 7, Windows 8, Windows 8.1 ou Windows 10 para um Windows 10.  

 Essa etapa só é executada em um sistema operacional padrão. Ela não é executada no Windows PE.  

### <a name="details"></a>Detalhes  
 Na guia **Propriedades** desta etapa, você pode definir as configurações descritas nesta seção.  

 Além disso, use a guia **Opções** guia para executar as seguintes ações:  

-   Desabilitar a etapa.  

-   Especificar se a sequência de tarefas continuará se ocorrer um erro ao executar a etapa.  

-   Especificar condições que devem ser atendidas para a etapa a ser executada.  

 **Nome**  
 Um nome curto definido pelo usuário que descreve a ação realizada nesta etapa.  

 **Descrição**  
 Informações mais detalhadas sobre a ação realizada nesta etapa.  

 **Atualizar pacote**  
 Selecione esta opção para especificar o pacote de atualização do sistema operacional Windows 10 a ser usado para a atualização.  

 **Caminho de origem**  
 Especifica um local ou caminho de rede para a mídia do Windows 10 que deve ser usado (corresponde à opção /installFrom da linha de comando). Você também pode especificar uma variável, como %mycontentpath% ou %DPC01%. Quando você usa uma variável para o caminho de origem, ele deve ser especificado anteriormente na sequência de tarefas. Por exemplo, se você usar a etapa [Baixar o conteúdo do pacote](#BKMK_DownloadPackageContent) na sequência de tarefas, é possível especificar uma variável para o local do pacote de atualização do sistema operacional. Em seguida, você pode usar essa variável para o caminho de origem nesta etapa.  

 **Edição**  
 Especifique a edição na mídia do sistema operacional a ser usada para a atualização.  

 **Chave do produto (Product Key)**  
 Especificar a chave do produto (Product Key) a ser aplicada ao processo de atualização  

 **Forneça o conteúdo do driver a seguir para a Instalação do Windows durante a atualização**  
 Selecione esta configuração para adicionar drivers ao computador de destino durante o processo de atualização (corresponde à opção /InstallDriver da linha de comando). Os drivers devem ser compatíveis com o Windows 10. Especifique uma das seguintes opções:  

-   **Pacote de driver**: clique em **Procurar** e selecione um pacote de driver existente na lista.  

-   **Conteúdo de teste**: selecione esta opção para especificar o local para o pacote de drivers. Você pode especificar uma pasta local, um caminho de rede ou uma variável de sequência de tarefas. Quando você usa uma variável para o caminho de origem, ele deve ser especificado anteriormente na sequência de tarefas. Por exemplo, usando a etapa [Download Package Content](task-sequence-steps.md#BKMK_DownloadPackageContent) .  

 **Time-out (minutes) (Tempo limite (minutos))**  
 Especifica o número de minutos durante os quais a Instalação precisa ser executada antes que o Configuration Manager provoque uma falha na etapa de sequência de tarefas.  

 **Executar a verificação de compatibilidade da Instalação do Windows sem iniciar a atualização**  
 Especifica a execução da verificação de compatibilidade da Instalação do Windows sem iniciar o processo de atualização (corresponde à opção \Compat ScanOnly da linha de comando). Você ainda deve implantar a origem de instalação inteira ao usar essa opção. A instalação retorna um código de saída como resultado da verificação. A tabela a seguir fornece alguns dos códigos de saída mais comuns.  

|Código de saída|Detalhes|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Nenhum problema de compatibilidade (“êxito”).|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|Problemas de compatibilidade acionáveis.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|A opção de migração selecionada não está disponível. Por exemplo, uma atualização do Enterprise para Professional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Não qualificado para Windows 10.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|Não há espaço livre em disco suficiente.|  

 Para obter mais informações sobre este parâmetro, veja [Opções de Linha de Comando da Instalação do Windows](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx)  

 **Ignorar quaisquer mensagens de compatibilidade rejeitadas**  
 Especifica que a Configuração conclui a instalação, ignorando quaisquer mensagens de compatibilidade dispensáveis (corresponde à opção \Compat IgnoreWarning da linha de comando).  

 **Atualizar dinamicamente a Instalação do Windows com o Windows Update**  
 Especifica se a instalação executará operações de Atualização Dinâmica, como pesquisa, download e instalação de atualizações (corresponde à opção /DynamicUpdate da linha de comando). Essa configuração não é compatível com as atualizações de software do Configuration Manager, mas pode ser habilitada ao manipular atualizações usando o WSUS (autônomo) ou o Windows Update.  

 **Substituir política e usar o Microsoft Update padrão**: selecione esta configuração para substituir temporariamente a política local em tempo real para executar operações de Atualização Dinâmica e fazer com que o computador obtenha atualizações do Windows Update.  
