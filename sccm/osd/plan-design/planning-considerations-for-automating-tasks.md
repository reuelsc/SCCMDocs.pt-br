---
title: Plano para automatização de tarefas
titleSuffix: Configuration Manager
description: Planeje antes de criar sequências de tarefas para automatizar tarefas com o Gerenciador de Configurações.
ms.date: 10/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 14a70610886ad9c62f2003ae880a7f221f3b0db4
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68340380"
---
# <a name="planning-considerations-for-automating-tasks-in-configuration-manager"></a>Considerações de planejamento para automatizar tarefas no Gerenciador de Configurações

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

É possível criar sequências de tarefas para automatizar tarefas em seu ambiente do Gerenciador de Configurações. Essas tarefas vão da captura de um sistema operacional em um computador de referência à implantação do sistema operacional em um ou mais computadores de destino. As ações da sequência de tarefas são definidas nas etapas individuais da sequência. Durante a execução da sequência de tarefas, as ações de cada etapa no nível de linha de comando são executadas no contexto do sistema Local. Esse comportamento significa que a sequência de tarefas é executada de forma totalmente automatizada, sem intervenção do usuário. 



##  <a name="BKMK_TSStepsActions"></a> Etapas e ações de sequências de tarefas  

Etapas são os componentes básicos de uma sequência de tarefas. Elas podem incluir comandos como:  
- Configurar e capturar o sistema operacional de um computador de referência  
- Instalar o Windows, drivers de hardware, o cliente do Gerenciador de Configurações e o software no computador de destino   


As ações da etapa definem os comandos de uma etapa da sequência de tarefas. Há dois tipos de ações:  
- A ação que você define usando uma cadeia de caracteres de linha de comando é conhecida como *ação personalizada*  
- Uma ação predefinida pelo Gerenciador de Configurações é conhecida como *ação interna*.  


Uma sequência de tarefas pode executar qualquer combinação de ações personalizadas e internas.  

As etapas da sequência de tarefas também podem incluir condições que controlam como a etapa se comporta. Esses comportamentos incluem a interrupção da sequência de tarefas, ou a continuação da sequência de tarefas se ocorrer um erro. Um tipo de condição é uma variável de sequência de tarefas. Por exemplo, use a variável **SMSTSLastActionRetCode** para testar a condição da etapa anterior. Adicione condições a uma única etapa ou a um grupo de etapas.  

A sequência de tarefas processa as etapas em sequência. Essa sequência inclui a ação da etapa e quaisquer condições na etapa. Quando o Gerenciador de Configurações começa a processar uma etapa da sequência de tarefas, ele não inicia a etapa seguinte até que a ação anterior tenha sido concluída. 

Uma sequência de tarefas é considerada concluída quando: 
- Todas as suas etapas forem concluídas  
- Uma etapa com falha faz com que o Gerenciador de Configurações pare de executar a sequência de tarefas antes da conclusão de todas as suas etapas.  


Por exemplo, se a etapa de uma sequência de tarefas não puder localizar uma imagem ou pacote indicado em um ponto de distribuição, a sequência de tarefas incluirá uma referência desfeita. O Gerenciador de Configurações interromperá a execução da sequência de tarefas nesse ponto, a menos que a etapa que falhou tenha uma condição para continuar quando um erro ocorrer.  

> [!IMPORTANT]  
>  Por padrão, uma sequência de tarefas falha após a falha de uma etapa ou ação. Se desejar que a sequência de tarefas continue mesmo quando uma etapa falhar, edite a sequência de tarefas, clique na guia **Opções** e selecione **Continuar se houver erro**.  

Para obter mais informações sobre as etapas que podem ser adicionadas a uma sequência de tarefas, consulte [Etapas de sequência de tarefas](/sccm/osd/understand/task-sequence-steps).  



##  <a name="BKMK_TSGroups"></a> Grupos de sequências de tarefas  

É possível agrupar várias etapas em uma sequência de tarefas. Um grupo de sequências de tarefas é composto por um nome, uma descrição opcional e condições opcionais. A sequência de tarefas avalia as condições do grupo como uma unidade antes de continuar na próxima etapa. Aninhe grupos dentro uns dos outros ou inclua uma combinação de etapas e subgrupos. Os grupos são úteis para combinar várias etapas que compartilham uma condição comum.  

Atribua um nome aos grupos de sequência de tarefas. Ele não precisa ser exclusivo. Também é possível fornecer uma descrição opcional para o grupo de sequências de tarefas.  

> [!IMPORTANT]  
>  Por padrão, um grupo de sequências de tarefas falha quando alguma etapa ou grupo inserido no grupo falha. Se quiser que a sequência de tarefas continue após ocorrer uma falha em uma etapa ou grupo interno, defina a opção **Continuar se houver erro** na etapa ou grupo.  

A tabela a seguir mostra como a opção **Continuar se houver erro** funciona quando você agrupa as etapas.  

Neste exemplo, há dois grupos de sequências de tarefas que incluem três etapas cada.  

|Grupo de sequências de tarefas ou etapa|Opção Continuar se houver erro|  
|---------------------------------|-------------------------------|  
|**Grupo de sequências de tarefas 1**|**Continuar se houver erro** selecionado.|  
|Etapa da sequência de tarefas 1|**Continuar se houver erro** selecionado.|  
|Etapa da sequência de tarefas 2|Não definida.|  
|Etapa da sequência de tarefas 3|Não definida.|  
|**Grupo de sequências de tarefas 2**|Não definida.|  
|Etapa da sequência de tarefas 4|Não definida.|  
|Etapa da sequência de tarefas 5|Não definida.|  
|Etapa da sequência de tarefas 6|Não definida.|  


-   Se a etapa da sequência de tarefas 1 falhar, a sequência de tarefas continuará com a etapa 2.  

-   Se a etapa da sequência de tarefas 2 falhar, a sequência de tarefas não executará a etapa 3. Como o grupo de sequências de tarefas 1 está definido como **Continuar se houver erro**, a sequência de tarefas continuará com o grupo de sequências de tarefas 2. Em seguida, ele executa a etapa de sequência de tarefas 4.  

-   Se a etapa de sequência de tarefas 4 falhar, nenhuma outra etapa será executada. A sequência de tarefas falha porque a configuração **Continuar se houver erro** não está definida para o grupo de sequências de tarefas 2.  



## <a name="add-child-task-sequences-to-a-task-sequence"></a>Adicionar sequências de tarefas filho a uma sequência de tarefas
<!--1261338-->
Começando com o Configuration Manager versão 1710, você pode adicionar uma nova etapa de sequência de tarefas que executa outra sequência de tarefas. Essa etapa cria um relacionamento pai-filho entre as sequências de tarefas. O uso dessa etapa permite que você crie sequências de tarefas mais modulares que podem ser usadas novamente.  

Para saber mais, confira [Executar sequência de tarefas](/sccm/osd/understand/task-sequence-steps#child-task-sequence). 

> [!Note]  
> O Configuration Manager não habilita esse recurso opcional por padrão. É necessário habilitar esse recurso antes de usá-lo. Para obter mais informações, consulte [Enable optional features from updates (Habilitar recursos opcionais de atualizações)](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  



##  <a name="BKMK_TSVariables"></a> Variáveis de sequência de tarefas  

Variáveis de sequência de tarefas são um conjunto de pares de nome e valor. Elas fornecem a configuração e configurações de implantação de sistema operacional para o computador, tarefas de configuração do sistema operacional e de estado do usuário em um cliente do Gerenciador de Configurações. As variáveis de sequência de tarefas fornecem um mecanismo para configurar e personalizar as etapas de uma sequência de tarefas.  

Ao executar uma sequência de tarefas, muitas configurações da sequência de tarefas são armazenadas como variáveis do ambiente. Você pode acessar ou alterar os valores das variáveis de sequência de tarefas internas. Também pode criar novas variáveis de sequência de tarefas para personalizar a maneira como uma sequência de tarefas é executada em um computador de destino.  

Use as variáveis de sequência de tarefas para executar as ações a seguir:  

-   Configurar os parâmetros de uma ação da sequência de tarefas  

-   Fornecer argumentos de linha de comando para uma etapa da sequência de tarefas  

-   Avaliar uma condição que determina a execução de uma etapa ou um grupo de sequências de tarefas  

-   Fornecer valores de scripts personalizados usados em uma sequência de tarefas  


Por exemplo, você tem uma sequência de tarefas que inclui a etapa **Ingressar no Domínio ou Grupo de Trabalho**. Implante a sequência de tarefas em coleções diferentes, nas quais a associação da coleção é determinada pela associação do domínio. Especifique uma variável de sequência de tarefas por coleção para cada nome de domínio da coleção. Em seguida, use essa variável de sequência de tarefas para fornecer o nome de domínio apropriado na sequência de tarefas.  

Para saber mais, confira [Como usar variáveis ​​de sequência de tarefas](/sccm/osd/understand/using-task-sequence-variables).



##  <a name="BKMK_TSCreate"></a> Criar uma sequência de tarefas  

Crie sequências de tarefas usando o Assistente para Criar Sequência de Tarefas. O assistente pode criar sequências de tarefas internas que executam tarefas específicas ou sequências de tarefas personalizadas que podem realizar muitas tarefas diferentes. O assistente permite que você crie os seguintes tipos de sequências de tarefas:

- Instalar uma imagem de sistema operacional existente em um computador de destino  

- Compilar e capturar uma imagem de sistema operacional de um computador de referência  

- Atualizar para o Windows 10 de um pacote de atualização do sistema operacional em um computador de destino   

- Criar uma sequência de tarefas personalizada que executa uma tarefa personalizada ou uma implantação especializada de sistema operacional  


Para saber mais, confira [Criar sequências de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_CreateTaskSequence).  



##  <a name="BKMK_TSEdit"></a> Editar uma sequência de tarefas  

Edite a sequência de tarefas usando o **Editor de Sequência de Tarefas**. O editor pode fazer as seguintes alterações na sequência de tarefas:  

- Adicionar ou remover etapas da sequência de tarefas  

- Alterar a ordem das etapas da sequência de tarefas  

- Adicionar ou remover grupos de etapas  

- Especificar se a sequência de tarefas continua quando ocorre um erro  

- Adicionar condições às etapas e aos grupos de uma sequência de tarefas  


> [!IMPORTANT]  
>  Se a sequência de tarefas tiver referências não associadas a um objeto como resultado da edição, o editor exigirá a correção da referência antes de poder fechar. As ações possíveis incluem:  
> - Corrigir a referência  
> - Excluir o objeto não referenciado da sequência de tarefas  
> - Desabilitar temporariamente a etapa da sequência de tarefas com falha até que a referência desfeita seja corrigida ou removida  


Para obter mais informações sobre como editar sequências de tarefas, consulte [Editar uma sequência de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_ModifyTaskSequence).  



##  <a name="BKMK_TSDeploy"></a> Implantar uma sequência de tarefas  

Implante uma sequência de tarefas em computadores de destino que estiverem em qualquer coleção do Gerenciador de Configurações. Use a coleção **Todos os Computadores Desconhecidos** para implantar sistemas operacionais em computadores desconhecidos. Você não pode implantar uma sequência de tarefas em coleções de usuário.  

> [!IMPORTANT]  
>  Não implante sequências de tarefas que instalam sistemas operacionais em coleção inadequadas. Certifique-se de que a coleção na qual você implantará a sequência de tarefas inclua somente os computadores nos quais você deseja instalar o sistema operacional. Para ajudar a impedir implantações de sistema operacional indesejadas, defina configurações para implantações de alto risco. Para obter mais informações, consulte [Configurações para gerenciar implantações de alto risco](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments).  

Cada computador de destino que recebe a sequência de tarefas executa a sequência de acordo com as configurações especificadas na implantação. As sequências de tarefas em si não contêm arquivos ou programas associados. Os arquivos referenciados por uma sequência de tarefas já devem estar presentes no computador de destino ou residir em um ponto de distribuição que os clientes podem acessar. 

> [!NOTE]  
> A sequência de tarefas instala os pacotes que são referenciados por programas, mesmo que o programa ou o pacote já esteja instalado no computador de destino. 
> 
> Se a sequência de tarefas instalar um aplicativo, o aplicativo só será instalado se as regras de requisitos do aplicativo forem atendidas e se o aplicativo ainda não estiver instalado, com base no método de detecção especificado para ele.  

O cliente do Configuration Manager executa uma implantação da sequência de tarefas quando baixa a política do cliente. Para disparar essa ação, em vez de esperar até o próximo ciclo de sondagem, consulte [Iniciar recuperação de política para um cliente do Gerenciador de Configurações](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  

Ao implantar sequências de tarefas em dispositivos Windows Embedded com filtro de gravação habilitado, é possível especificar se você deseja desabilitar o filtro de gravação no dispositivo durante a implantação e reiniciá-lo após a implantação. Se o filtro de gravação não for desabilitado, a sequência de tarefas será implantada em uma sobreposição temporária e não estará disponível quando o dispositivo for reiniciado.  

> [!NOTE]  
>  Ao implantar uma sequência de tarefas em um dispositivo Windows Embedded, verifique se o dispositivo é membro de uma coleção com uma janela de manutenção configurada. Isso permite que você gerencie quando o filtro de gravação está desabilitado e habilitado e quando o dispositivo é reiniciado.  
>   
>  Se clientes baixarem sequências de tarefas fora de uma janela de manutenção, a sequência de tarefas será baixada duas vezes. Nesse cenário, o cliente faz o download da sequência de tarefas, desabilita o filtro de gravação, reinicia o computador e baixa a sequência de tarefas novamente. Esse comportamento ocorre porque a sequência de tarefas foi baixada originalmente em uma sobreposição temporária, que é apagada quando o dispositivo é reiniciado.  

Para obter mais informações sobre como implantar sequências de tarefas, consulte [Implantar uma sequência de tarefas](/sccm/osd/deploy-use/deploy-a-task-sequence).  



##  <a name="BKMK_TSExportImport"></a> Exportar e importar uma sequência de tarefas  

O Configuration Manager permite exportar e importar sequências de tarefas. Quando você exporta uma sequência de tarefas, pode incluir os objetos que são referenciados pela sequência. 

Para saber mais, confira [Exportar e importar sequências de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_ExportImport).  



##  <a name="BKMK_TSRun"></a> Executar uma sequência de tarefas  

As sequências de tarefas são sempre executadas usando a conta Sistema Local. Durante a execução da sequência de tarefas, o cliente do Gerenciador de Configurações verifica primeiro se há pacotes referenciados antes de começar as etapas da sequência de tarefas. Se não conseguir validar ou fazer download de um pacote referenciado, a sequência de tarefas retornará um erro para a etapa de sequência de tarefas associada.  

> [!Note]  
> A etapa **Executar linha de comando** da sequência de tarefas fornece a capacidade de executar um comando como uma conta diferente.  

Se você configurar a implantação de uma sequência de tarefas para baixar e executar, o cliente do Gerenciador de Configurações baixará todo o conteúdo dependente em seu cache. Se o cache do cliente for muito pequeno, ou não for possível encontrar o conteúdo, a sequência de tarefas falhará. O cliente gera uma mensagem de status. 

Você também pode especificar que o cliente baixe o conteúdo apenas quando necessário. Para executar essa ação, selecione **Baixar conteúdo localmente quando necessário executando a sequência de tarefas** na implantação da sequência de tarefas. Outra opção é **Executar o programa do ponto de distribuição**. Com essa opção, o cliente instala os arquivos diretamente do ponto de distribuição sem baixá-los primeiro no cache. 

Quando você configura a implantação de sequência de tarefas como **Disponível**, se o cliente não conseguir localizar o conteúdo dependente da sequência de tarefas, ele enviará imediatamente um erro. Nessa situação, para uma implantação **Obrigatória**, o cliente do Gerenciador de Configurações aguarda. Ele tentar baixar o conteúdo até o prazo, caso o conteúdo ainda não tenha sido replicado em um local de conteúdo que o cliente possa acessar.  

Quando uma sequência de tarefas é concluída com êxito ou falha, o Gerenciador de Configurações registra esse estado no histórico do cliente. 

Após o início de uma sequência de tarefas em um computador, você não pode cancelar ou interrompê-la.  

> [!IMPORTANT]  
>  Se uma etapa de sequência de tarefas exigir que o computador seja reiniciado, o cliente deverá ser capaz de inicializar a partir de uma partição de disco formatada. Caso contrário, a sequência de tarefas falhará, independentemente de qualquer manipulação de erro especificada na sequência.  

Quando um objeto dependente de uma sequência de tarefas é atualizado para uma versão mais recente, qualquer sequência de tarefas que faz referência ao pacote é atualizada automaticamente. Ela faz referência à versão mais recente, independentemente de quantas atualizações você implantou.  



##  <a name="BKMK_TSMaintenanceWindow"></a> Usar uma janela de manutenção para especificar quando uma sequência de tarefas pode ser executada  

Você pode especificar quando a sequência de tarefas pode ser executada definindo uma janela de manutenção para a coleção de dispositivos. Configure as janelas de manutenção com uma data de início, uma hora de início e término e um padrão de recorrência. Quando você define a agenda para a janela de manutenção, pode especificar que a janela de manutenção aplique-se apenas àquela sequências de tarefas. Para obter mais informações, consulte [Como usar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).  

> [!IMPORTANT]  
>  Quando você configura uma janela de manutenção para executar uma sequência de tarefas, uma vez que as sequências de tarefas iniciam, continuam a ser executadas mesmo depois que a janela de manutenção é fechada.  



##  <a name="BKMK_TSNetworkAccessAccount"></a> Sequências de tarefas e conta de acesso de rede  

> [!Important]  
> Começando na versão 1806, alguns cenários de implantação de sistema operacional não exigem o uso da conta de acesso de rede. Para obter mais informações, confira [HTTP aprimorado](#enhanced-http).

Embora as sequências de tarefas sejam executadas apenas no contexto da conta do Sistema Local, pode ser necessário configurar a [conta de acesso à rede](/sccm/core/plan-design/hierarchy/accounts#network-access-account) nas seguintes circunstâncias:  

- Se a sequência de tarefas tentar acessar o conteúdo do Gerenciador de Configurações nos pontos de distribuição. Configure corretamente a conta de acesso à rede, caso contrário, a sequência de tarefas falhará.   

- Quando você usa uma imagem de inicialização para iniciar uma implantação de sistema operacional. Nesse caso, o Gerenciador de Configurações usa o ambiente do Windows PE, que não é um sistema operacional completo. O ambiente do Windows PE usa um nome aleatório gerado automaticamente, que não é membro de nenhum domínio. Se você não configurar corretamente a conta de acesso à rede, o computador não poderá acessar o conteúdo necessário para a sequência de tarefas.  

> [!NOTE]  
>  A conta de acesso à rede nunca é usada como o contexto de segurança para executar programas, instalar aplicativos, atualizações ou executar sequências de tarefas. A conta de acesso à rede só é usada para acessar os recursos associados na rede.  

Para saber mais sobre a conta de acesso à rede, confira [Conta de acesso à rede](/sccm/core/plan-design/hierarchy/accounts#network-access-account).  


### <a name="enhanced-http"></a>HTTP aprimorado
<!--1358278-->

Começando na versão 1806, quando você habilita o **HTTP aprimorado**, os cenários a seguir não exigem uma conta de acesso de rede para baixar conteúdo de um ponto de distribuição:

- Sequências de tarefas em execução da mídia de inicialização ou do PXE  
- Sequências de tarefas em execução no Centro de Software  

Essas sequências de tarefas podem ser usadas para implantação de sistema operacional ou personalização. Também é compatível com computadores de grupo de trabalho.

Para obter mais informações, confira [HTTP aprimorado](/sccm/core/plan-design/hierarchy/enhanced-http).  

> [!Note]  
> Os cenários de implantação de sistema operacional a seguir ainda exigem o uso de uma conta de acesso à rede:
>  
> - A [opção de implantação](/sccm/osd/deploy-use/deploy-a-task-sequence) de sequência de tarefas, **Acessar conteúdo diretamente de um ponto de distribuição quando necessário executando a sequência de tarefas**   
> - A opção de etapa de [Armazenamento de Estado da Solicitação](/sccm/osd/understand/task-sequence-steps#BKMK_RequestStateStore), **Se a conta de computador não conseguir se conectar a um armazenamento de estado, use a conta de acesso à rede** 
> - Ao conectar-se com um domínio não confiável ou entre florestas do Active Directory 
> - A opção de etapa [Aplicar Imagem do Sistema Operacional](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyOperatingSystemImage), **Acessar o conteúdo diretamente do ponto de distribuição** 
> - A sequência de tarefas [configuração avançada](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#bkmk_prop-advanced) para **Executar outro programa primeiro** 
> - [Multicast](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network)  



##  <a name="BKMK_TSCreateMedia"></a> Criar mídia para sequências de tarefas  

Você pode gravar sequências de tarefas e seus arquivos relacionados e dependências em vários tipos de mídia. O Gerenciador de Configurações dá suporte à mídia removível, como um DVD ou uma unidade flash USB para mídia de captura, autônoma e inicializável. Mídia pré-configurada usa um arquivo WIM (imagem do Windows).  

Ao criar a mídia, especifique uma senha para controlar o acesso. Depois, a pessoa deve inserir a senha no computador de destino para executar a sequência de tarefas.  

Quando você executa uma sequência de tarefas pela mídia, a arquitetura de processador especificada da mídia não é reconhecida. Se a arquitetura especificada não corresponder ao computador de destino, a sequência de tarefas ainda tentará executar. Se a arquitetura da mídia não corresponder à arquitetura do computador de destino, a sequência de tarefas falhará.  

Para saber mais, confira [Criar mídia de sequência de tarefas](/sccm/osd/deploy-use/create-task-sequence-media).  


### <a name="media-types"></a>Tipos de mídia
O Gerenciador de Configurações dá suporte aos seguintes tipos de mídia:  

#### <a name="capture-media"></a>Mídia de captura
A mídia captura uma imagem do sistema operacional configurada e criada fora da infraestrutura do Gerenciador de Configurações. Mídia de captura pode conter programas personalizados que podem ser executados antes da execução de uma sequência de tarefas. O programa personalizado pode interagir com a área de trabalho, solicitar valores de entrada ao usuário ou criar variáveis ​​para serem usadas pela sequência de tarefas.  

Para obter mais informações, consulte [Criar mídia de captura](/sccm/osd/deploy-use/create-capture-media).  

#### <a name="stand-alone-media"></a>Mídia autônoma
Mídia autônoma contém a sequência de tarefas e todos os objetos associados necessários para a execução da sequência de tarefas. Sequências de tarefas de mídia autônoma podem ser executadas quando o Configuration Manager tem conectividade limitada ou nenhuma conectividade com a rede. Execute a mídia autônoma das seguintes maneiras:  

- Se o computador de destino não for inicializado, a imagem do Windows PE associada à sequência de tarefas será usada por meio da mídia autônoma e a sequência de tarefas terá início.  

- Inicie manualmente a mídia autônoma. Se um usuário estiver conectado ao computador, poderá iniciar a sequência de tarefas a partir da mídia.  


> [!IMPORTANT]  
>  As etapas de uma sequência de tarefas de mídia autônoma devem ser capazes de executar sem recuperar dados da rede. Caso contrário, a etapa de sequência de tarefas que tenta recuperar os dados falhará. Por exemplo, uma etapa de sequência de tarefas que exige um ponto de distribuição para obter um pacote falhará. Se a mídia autônoma contiver o pacote necessário, a etapa da sequência de tarefas será bem-sucedida.  


Para obter mais informações, consulte [Criar mídia autônoma](/sccm/osd/deploy-use/create-stand-alone-media).  

#### <a name="bootable-media"></a>Mídia inicializável
A mídia inicializável contém os arquivos necessários para iniciar um computador de destino para que ele possa se conectar à infraestrutura do Gerenciador de Configurações. Em seguida, ele determina quais sequências de tarefa executar com base nas associações de coleção. Essa mídia não inclui a sequência de tarefas ou os objetos dependentes. Em vez disso, o cliente baixa o conteúdo pela rede. Esse método é útil para novos computadores ou implantações bare-metal, quando nenhum sistema operacional está no computador de destino.  

Para obter mais informações, consulte [Criar mídia inicializável](/sccm/osd/deploy-use/create-bootable-media).  

#### <a name="prestaged-media"></a>Mídia em pré-teste
Mídia em pré-teste implanta uma imagem do sistema operacional em um computador de destino que não está provisionado. A mídia pré-configurada é armazenada como um arquivo WIM (imagem do Windows). Esse arquivo pode ser instalado em um computador bare-metal pelo fabricante ou em um centro de preparo corporativo. Um benefício da mídia pré-configurada é que esses locais não exigem uma conexão ao seu ambiente do Gerenciador de Configurações.  

Para mais informações, consulte [Criar mídia pré-configurada](/sccm/osd/deploy-use/create-prestaged-media).  
