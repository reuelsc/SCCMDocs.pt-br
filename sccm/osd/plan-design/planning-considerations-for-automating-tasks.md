---
title: "Considerações sobre o planejamento para automatizar tarefas | Microsoft Docs"
description: Planeje antes de automatizar tarefas no System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
caps.latest.revision: 13
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: 830f715b688cc9929a179da94eba9c81de8db11a


---
# <a name="planning-considerations-for-automating-tasks-in-system-center-configuration-manager"></a>Considerações de planejamento para automatizar tarefas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

É possível criar sequências de tarefas para automatizar tarefas no seu ambiente do System Center Configuration Manager. Essas tarefas vão da captura de um sistema operacional em um computador de referência à implantação do sistema operacional em um ou mais computadores de destino. As ações da sequência de tarefas são definidas nas etapas individuais da sequência. Quando a sequência de tarefas é executada, as ações de cada etapa são executadas no nível de linha de comando no contexto do Sistema Local sem a necessidade de intervenção do usuário. Use as seções a seguir para ajudar a planejar a automação de tarefas no Configuration Manager.

##  <a name="a-namebkmktsstepsactionsa-task-sequence-steps-and-actions"></a><a name="BKMK_TSStepsActions"></a> Etapas e ações de sequências de tarefas  
 Etapas são os componentes básicos de uma sequência de tarefas. Elas podem conter comandos que configuram e capturam o sistema operacional de um computador de referência, ou podem conter comandos que instalam o sistema operacional, drivers, o cliente do Configuration Manager e softwares no computador de destino. Os comandos de uma etapa da sequência de tarefas são definidos pelas ações da etapa. Existem dois tipos de ações. A ação que você define usando uma cadeia de caracteres de linha de comando é conhecida como ação personalizada. Uma ação predefinida pelo Configuration Manager é conhecida como ação interna. Uma sequência de tarefas pode executar qualquer combinação de ações personalizadas e internas.  

 As etapas da sequência de tarefas também podem incluir condições que controlam como a etapa se comporta, como interromper ou continuar a sequência de tarefas em caso de erro. Condições são adicionadas à etapa incluindo uma variável de sequência de tarefas na etapa. Por exemplo, você poderia usar variável **SMSTSLastActionRetCode** para testar a condição da etapa anterior. Variáveis podem ser adicionados a uma única etapa ou a um grupo de etapas.  

 As etapas da sequência de tarefas são processadas sequencialmente, o que inclui a ação da etapa e as condições atribuídas à etapa. Quando o Configuration Manager começa a processar uma etapa da sequência de tarefas, a etapa seguinte não é iniciada até que a ação anterior seja concluída. Uma sequência de tarefas é considerada concluída quando todas as suas etapas terminam ou quando uma falha de uma etapa faz com que o Configuration Manager interrompa a execução da sequência de tarefas antes do término de todas as etapas. Por exemplo, se a etapa de uma sequência de tarefas não conseguir localizar uma imagem ou um pacote referenciado em um ponto de distribuição, então a sequência de tarefas conterá uma referência corrompida e o Configuration Manager interromperá a execução da sequência de tarefas nesse ponto, a menos que a etapa que falhou tenha uma condição para continuar em caso de erro.  

> [!IMPORTANT]  
>  Por padrão, uma sequência de tarefas falha após a falha de uma etapa ou ação. Se desejar que a sequência de tarefas continue mesmo quando uma etapa falhar, edite a sequência de tarefas, clique na guia **Opções** e selecione **Continuar se houver erro**.  

 Para obter mais informações sobre as etapas que podem ser adicionadas a uma sequência de tarefas, consulte [Etapas de sequência de tarefas](../understand/task-sequence-steps.md).  

##  <a name="a-namebkmktsgroupsa-task-sequence-groups"></a><a name="BKMK_TSGroups"></a> Grupos de sequências de tarefas  
 **Grupos** são várias etapas dentro de uma sequência de tarefas. Um grupo de sequências de tarefas consiste em um nome, uma descrição opcional e condições opcionais que são avaliadas como uma unidade antes de essa sequência de tarefas seguir para a próxima etapa. Os grupos podem ser aninhados um dentro do outro, e um grupo pode conter uma combinação de etapas e subgrupos. Os grupos são úteis para combinar várias etapas que compartilham uma condição comum.  

> [!IMPORTANT]  
>  Por padrão, um grupo de sequências de tarefas falha quando alguma etapa ou grupo inserido no grupo falha. Se desejar que a sequência de tarefas continue após ocorrer uma falha em uma etapa ou grupo interno, edite a sequência de tarefas, clique na guia **Opções** e selecione **Continuar se houver erro**.  

 A tabela a seguir mostra como a opção **Continuar se houver erro** funciona quando você agrupa as etapas.  

 Neste exemplo, há dois grupos de sequências de tarefas que contêm três etapas cada.  

|Grupo de sequências de tarefas ou etapa|Opção Continuar se houver erro|  
|---------------------------------|-------------------------------|  
|**Grupo de Sequências de Tarefas 1**|**Continuar se houver erro** selecionado.|  
|Etapa da Sequência de Tarefas 1|**Continuar se houver erro** selecionado.|  
|Etapa da Sequência de Tarefas 2|Não definida.|  
|Etapa da Sequência de Tarefas 3|Não definida.|  
|**Grupo de Sequência de Tarefas 2**|Não definida.|  
|Etapa da Sequência de Tarefas 4|Não definida.|  
|Etapa da Sequência de Tarefas 5|Não definida.|  
|Etapa da Sequência de Tarefas 6|Não definida.|  

-   Se a etapa da sequência de tarefas 1 falhar, a sequência de tarefas continuará com a etapa 2.  

-   Se a etapa da sequência de tarefas 2 falhar, a sequência de tarefas não executará a etapa 3, mas continuará a execução das etapas 4 e 5, que estão em um grupo de sequências de tarefas diferente.  

-   Se a etapa da sequência de tarefas 4 falhar, nenhuma outra etapa será executada e a sequência de tarefas falhará porque a opção **Continuar se houver erro** não foi configurada para o grupo de sequências de tarefas 2.  

 É necessário atribuir um nome aos grupos de sequências de tarefas, embora o nome do grupo não tenha de ser exclusivo. Também é possível fornecer uma descrição opcional para o grupo de sequências de tarefas.  

##  <a name="a-namebkmktsvariablesa-task-sequence-variables"></a><a name="BKMK_TSVariables"></a> Variáveis de sequência de tarefas  
 Variáveis de sequência de tarefas são um conjunto de pares de nome e valore que fornecem a configuração e os parâmetros de implantação do sistema operacional para tarefas de configuração do computador, sistema operacional e estado do usuário em um computador cliente do Configuration Manager. As variáveis de sequência de tarefas fornecem um mecanismo para configurar e personalizar as etapas de uma sequência de tarefas.  

 Quando você executa uma sequência de tarefas, muitas das configurações da sequência de tarefas são armazenadas como variáveis do ambiente. Você pode acessar ou alterar os valores das variáveis de sequência de tarefas internas, além de poder criar novas variáveis de sequência de tarefa para personalizar a forma com que a sequência de tarefas é executada em um computador de destino.  

 É possível usar variáveis de sequência de tarefas no ambiente da sequência de tarefas para executar as seguintes ações:  

-   Configurar os parâmetros de uma ação da sequência de tarefas  

-   Fornecer argumentos de linha de comando para uma etapa da sequência de tarefas  

-   Avaliar uma condição que determina se uma etapa ou um grupo de sequências de tarefas é executada(o)  

-   Fornecer valores de scripts personalizados usados em uma sequência de tarefas  

 Por exemplo, você pode ter uma sequência de tarefas que inclui a etapa **Ingressar no Domínio ou Grupo de Trabalho**. A sequência de tarefas pode ser implantada em coleções diferentes, onde a associação da coleção é determinada pela associação do domínio. Nesse caso, você pode especificar uma variável de sequência de tarefas por coleção para cada nome de domínio da coleção e depois usar essa variável de sequência de tarefas para fornecer o nome de domínio apropriado na sequência de tarefas.  

###  <a name="a-namebkmktscreatevariablesa-create-task-sequence-variables"></a><a name="BKMK_TSCreateVariables"></a> Criar variáveis de sequência de tarefas  
 É possível adicionar novas variáveis de sequência de tarefas para personalizar e controlar as etapas em uma sequência de tarefas. Por exemplo, é possível criar uma variável de sequência de tarefas para anular uma configuração de uma etapa de sequência de tarefas interna. Também é possível criar uma variável de sequência de tarefas personalizada para usar com condições, linhas de comando ou etapas personalizadas na sequência de tarefas. Ao criar uma variável de sequência de tarefas, essa variável e o valor associado são preservados no ambiente da sequência de tarefas, mesmo quando a sequência reinicia o computador de destino. A variável e seu valor podem ser usados na sequência de tarefas em ambientes de sistema operacional diferentes. Por exemplo, ela pode ser usada em um sistema operacional Windows completo e no ambiente do Windows PE.  

 A tabela a seguir descreve os métodos para criar uma variável de sequência de tarefas e informações adicionais de uso.  

|Método de criação|Uso|  
|-------------------|-----------|  
|Configurar campos nas etapas da sequência de tarefas usando o Editor de Sequência de Tarefas|Especifica os valores padrão para a etapa da sequência de tarefas. A variável e o valor são acessíveis somente quando a etapa é executada na sequência de tarefas. Eles não fazem parte do ambiente da sequência em geral, e não são acessíveis por outras etapas da sequência de tarefas.<br /><br /> Para obter uma lista das variáveis internas e as ações associadas a elas, consulte [Variáveis de ação de sequência de tarefas](../understand/task-sequence-action-variables.md).|  
|Adicionar uma etapa de variável de sequência de tarefas em uma sequência de tarefas|Especifica a variável de sequência de tarefas e o valor no ambiente da sequência de tarefas quando a etapa da sequência de tarefas é executada como parte da sequência. Todas as etapas subsequentes da sequência de tarefas podem acessar a variável do ambiente e seu valor.|  
|Definir uma variável por coleção|Especifica variáveis de sequência de tarefas e valores para uma coleção de computadores. Todas as sequências de tarefas voltadas para a coleção podem acessar as variáveis de sequência de tarefas e seus valores.|  
|Definir uma variável por computador|Especifica variáveis de sequência de tarefas e valores para determinado computador. Todas as sequências de tarefas voltadas para o computador podem acessar as variáveis de sequência de tarefas e seus valores.|  
|Adicionar uma variável ​​de sequência de tarefas na página **Personalização** do Assistente de Mídia de Sequência de Tarefas|Especifica variáveis de sequência de tarefas e valores para a sequência de tarefas que é executada por meio da mídia que pode acessar a variável de sequência de tarefas e seu valor.|  

 Para anular o valor padrão para uma variável de sequência de tarefas interna, é necessário definir uma variável de sequência de tarefas de mesmo nome como a variável de sequência de tarefas interna. Para obter uma lista de variáveis internas de sequência de tarefas com as ações e o uso associado a elas, consulte [Variáveis internas de sequência de tarefas](../understand/task-sequence-built-in-variables.md).  

 Você pode excluir uma variável de sequência de tarefas do ambiente da sequência de tarefas usando os mesmos métodos da criação de uma variável de sequência de tarefas. Nesse caso, para excluir uma variável do ambiente da sequência de tarefas, você configura o valor da variável de sequência de tarefas como uma cadeia de caracteres vazia.  

 Você pode combinar métodos para configurar uma variável de sequência de tarefas do ambiente com valores diferentes para a mesma sequência. Em um cenário avançado, você pode configurar os valores padrão para etapas de uma sequência usando o Editor de Sequência de Tarefas e depois configurar um valor de variável personalizado usando os diferentes métodos de criação. A lista a seguir descreve as regras que determinam o valor que é usado quando uma variável de sequência de tarefas é criada usando mais de um método.  

1.  A etapa **Definir Variável de Sequência de Tarefas** substitui todos os outros métodos de criação.  

2.  Variáveis por computador têm precedência sobre variáveis por coleção. Se você especificar o mesmo nome de variável de sequência de tarefas para uma variável por computador e para uma variável por coleção, a variável por computador será usada quando o computador de destino executar a sequência de tarefas implantada.  

3.  As sequências de tarefas podem ser executadas por meio de uma mídia. Use as variáveis de mídia em vez de variáveis por coleção ou por computador. Se a sequência de tarefas for executada por meio de uma mídia, as variáveis por computador e por coleção não se aplicarão e não serão usadas. Em vez disso, as variáveis de sequência de tarefas definidas na página **Personalização** do assistente de Mídia de Sequência de Tarefas são usadas para definir valores específicos para uma sequência de tarefas que é executada por meio de uma mídia  

4.  Se uma variável de sequência de tarefas não for definida no ambiente da sequência em geral, as ações internas usarão o valor padrão para a etapa, conforme definido no Editor de Sequência de Tarefas.  

 Além de anular os valores das configurações da etapa da sequência de tarefas interna, você também pode criar uma nova variável de ambiente para usar em uma etapa, um script, uma linha de comando ou condição da sequência de tarefas. Quando você for especificar um nome para a nova variável de sequência de tarefas, siga estas diretrizes:  

-   O nome da variável de sequência de tarefas que você especificar pode conter letras, números, o caractere underscore (_) e hífen (-).  

-   Os nomes das variáveis de sequência de tarefas podem ter no mínimo 1 e no máximo 256 caracteres.  

-   As variáveis definidas pelo usuário devem começar com uma letra (A-Z ou a-z).  

-   Os nomes das variáveis definidas pelo usuário não podem começar com o caractere underscore. Somente variáveis de sequência de tarefas somente leitura são precedidas pelo caractere underscore  

    > [!NOTE]  
    >  As variáveis de sequência de tarefas somente leitura podem ser lidas pelas etapas de uma sequência de tarefas, mas não podem ser configuradas. Por exemplo, você pode usar uma variável de sequência de tarefas somente leitura como parte da linha de comando de uma variável de ação de sequência de tarefas **Executar Linha de Comando**, mas não pode configurar uma variável somente leitura usando a variável de ação **Definir Variável de Sequência de Tarefas**.  

-   Os nomes das variáveis de sequência de tarefas não diferenciam maiúsculas de minúsculas. Por exemplo, OSDVAR e osdvar representam a mesma variável de sequência de tarefas.  

-   Os nomes das variáveis de sequência de tarefas não podem começar nem terminar com um espaço, nem conter espaços inseridos. Os espaços deixados no começo ou no fim do nome de uma variável de sequência de tarefas serão ignorados.  

 A tabela a seguir exibe exemplos de variáveis de sequência de tarefas válidas e não válidas especificadas pelo usuário.  

|Exemplos de nNames de variável válida especificados pelo usuário|Exemplos de nomes de variável não válida especificadas pelo usuário|  
|-------------------------------------------------------|----------------------------------------------------------|  
|MyVariable|1Variable<br /><br /> Variáveis de sequência de tarefas especificadas pelo usuário não podem começar com um número.|  
|My_Variable|MyV@riable<br /><br /> Variáveis de sequência de tarefas especificadas pelo usuário não podem conter o símbolo @.|  
|My_Variable_2|_MyVariable<br /><br /> Variáveis de sequência de tarefas especificadas pelo usuário não podem começar com um sublinhado.|  

 Limitações gerais para variáveis de sequência de tarefas:  

-   Valores de variáveis de sequência de tarefas não podem ter mais de 4.000 caracteres.  

-   Não é possível criar nem substituir uma variável de sequência de tarefas somente leitura. Variáveis somente leitura são designadas por nomes que começam com um caractere de sublinhado (_). Você pode acessar o valor de variáveis de sequência de tarefas ​​somente leitura em sua sequência de tarefas; no entanto, não é possível alterar seus valores associados.  

-   Os valores das variáveis de sequência de tarefas podem diferenciar maiúsculas de minúsculas dependendo do uso do valor. Na maioria dos casos, os valores das variáveis de sequência de tarefas não diferenciam maiúsculas de minúsculas. No entanto, alguns valores podem diferenciar maiúsculas de minúsculas, como uma variável que contém uma senha.  

-   Não há um limite para quantas variáveis de sequência de tarefas podem ser criadas. No entanto, o número de variáveis é limitado pelo tamanho do ambiente de sequência de tarefas. O limite do tamanho total para o ambiente da sequência de tarefas é de 32 MB.  

###  <a name="a-namebkmktsenvironmentvariablesa-access-environment-variables"></a><a name="BKMK_TSEnvironmentVariables"></a> Variáveis de ambiente de acesso  
 Depois de especificar a variável de sequência de tarefas e seu valor usando um dos métodos da seção anterior, você pode usar o valor da variável do ambiente em suas sequências de tarefas. Você pode acessar os valores padrão para variáveis ​​de sequência de tarefas internas, especificar um novo valor para uma variável interna ou usar uma variável de sequência de tarefas personalizada em uma linha de comando ou script.  

 A tabela a seguir resume as operações de sequência de tarefas que podem ser realizadas acessando as variáveis ​​do ambiente de sequência de tarefas.  

|Operação de sequência de tarefas|Uso|  
|-----------------------------|-----------|  
|Definir as configurações de ação|Você pode especificar que uma configuração de etapa de sequência de tarefas seja fornecida por um valor de variável durante a execução da sequência.<br /><br /> Para fornecer uma configuração de etapa de sequência de tarefas usando uma tarefa variável de ambiente, use o Editor de Sequência de Tarefas para editar a etapa e especificar o nome da variável como o valor do campo. O nome da variável deve ser delimitado por sinais de porcentagem (%) para indicar que é uma variável de ambiente.|  
|Fornecer argumentos de linha de comando|Você pode especificar parte ou toda uma linha de comando personalizada usando um valor de variável de ambiente.<br /><br /> Para fornecer uma configuração de linha de comando usando uma variável de ambiente, use o nome da variável como parte do campo **Linha de Comando** da etapa de sequência de tarefas **Executar Linha de Comando**. O nome da variável deve estar entre sinais de porcentagem (%).<br /><br /> Por exemplo, a seguinte linha de comando usa uma variável de ambiente interna para gravar o nome do computador em C:\File.txt.<br /><br /> <br /><br /> **Cmd /C %_SMSTSMachineName% > C:\File.txt**|  
|Avaliar uma condição da etapa|Você pode variáveis de ambiente de sequência de tarefas internas ou personalizadas como parte de uma etapa de sequência de tarefas ou condição de grupo. O valor da variável de ambiente será avaliado antes da etapa de sequência de tarefas ou execuções do grupo.<br /><br /> Para adicionar uma condição que avalia um valor de variável, faça o seguinte:<br /><br /> 1.  Selecione a etapa ou grupo ao qual você deseja adicionar a condição.<br />2.  Na guia **Opções** da etapa ou grupo, selecione **Variável de Sequência de Tarefas** na lista suspensa **Adicionar Condição**.<br />3.  Na caixa de diálogo **Variável de Sequência de Tarefas**, especifique o nome da variável, a condição testada e o valor da variável.|  
|Fornecer informações para um script personalizado|As variáveis da sequência de tarefas podem ser lidas e gravadas usando o objeto COM do Microsoft.SMS.TSEnvironment enquanto a sequência de tarefas está em execução.<br /><br /> O exemplo a seguir ilustra um arquivo de script do Visual Basic que consulta a variável da sequência de tarefas **_SMSTSLogPath** para obter o local do log atual. O script também define uma variável personalizada.<br /><br /> <br /><br /> **dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")**<br /><br /> <br /><br /> **dim logPath**<br /><br /> <br /><br /> **' Você pode consultar o ambiente para obter uma variável existente.**<br /><br /> **logPath = env("_SMSTSLogPath")**<br /><br /> <br /><br /> **' Você também pode definir uma variável no ambiente do OSD.**<br /><br /> **env("MyCustomVariable") = "varname"**<br /><br /> <br /><br /> Para obter mais informações sobre como usar variáveis de sequência de tarefas em scripts, consulte a documentação do SDK|  

###  <a name="a-namebkmkcomputercollectionvariablesa-computer-and-collection-variables"></a><a name="BKMK_ComputerCollectionVariables"></a> Variáveis de computador e coleção  
 Você pode configurar sequências de tarefas para serem executadas simultaneamente em vários computadores ou coleções. Você pode especificar informações exclusivas por computador ou coleção, como uma chave única de produto de sistema operacional ou associar todos os membros de uma coleção a um domínio especificado.  

 Você pode atribuir variáveis de sequência de tarefas a um único computador ou coleção. Quando a sequência de tarefas começa a ser executada no computador ou na coleção de destino, os valores especificados são aplicados ao computador ou à coleção de destino.  

 Você pode especificar variáveis de sequência de tarefas para um único computador ou coleção. Quando a sequência de tarefas começa a ser executada no computador ou na coleção de destino, as variáveis ​​especificadas são adicionadas ao ambiente e os valores ficam disponíveis para todas as etapas da sequência de tarefas na sequência.  

> [!WARNING]  
>  Se você usar o mesmo nome de variável por coleção ou por computador, o valor de variável do computador terá precedência sobre a variável de coleção. Variáveis de sequência de tarefas que você atribui a coleções têm precedência sobre variáveis de sequência de tarefas internas.  

 Para obter mais informações sobre como criar variáveis ​​de sequência de tarefas para computadores e coleções, consulte [Criar variáveis de sequência de tarefas em computadores e coleções](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTSVariables).  

###  <a name="a-namebkmktsmediavariablesa-task-sequence-media-variables"></a><a name="BKMK_TSMediaVariables"></a> Variáveis de mídia de sequência de tarefas  
 Você pode especificar variáveis de sequência de tarefas para sequências de tarefas executadas por meio da mídia. Ao usar mídia para implantar o sistema operacional, você adiciona as variáveis ​​da sequência de tarefas e especifica seus valores ao criar a mídia; as variáveis ​​e seus valores são armazenados na mídia.  

> [!NOTE]  
>  As sequências de tarefas são armazenadas em mídia autônoma. No entanto, todos os outros tipos de mídia, tais como mídia em pré-teste, recuperam a sequência de tarefas por meio de um ponto de gerenciamento.  

 É possível especificar as variáveis ​​de sequência de tarefas na página **Personalização** do Assistente de Mídia de Sequência de Tarefas. Para obter informações sobre como criar mídia, veja [Criar mídia de sequência de tarefas](../deploy-use/create-task-sequence-media.md).  

> [!TIP]  
>  A sequência de tarefas grava a ID do pacote e a linha de comando prestart, incluindo o valor das variáveis de sequência de tarefas, no arquivo de log CreateTSMedia.log, no computador que executa o console do Configuration Manager. Você poderá analisar esse arquivo de log para verificar o valor das variáveis de sequência de tarefas.  

##  <a name="a-namebkmktscreatea-create-a--task-sequence"></a><a name="BKMK_TSCreate"></a> Criar uma sequência de tarefas  
 Você pode criar sequências de tarefas usando o Assistente para Criar Sequência de Tarefas. O assistente pode criar sequências de tarefas internas que executam tarefas específicas ou sequências de tarefas personalizadas que podem realizar muitas tarefas diferentes.  

 Por exemplo, você pode criar sequências de tarefas que criam e capturam uma imagem do sistema operacional de um computador de referência, instalar uma imagem de um sistema operacional existente em um computador de destino ou criar uma sequência de tarefas personalizada que executa uma tarefa personalizada. Você pode usar sequências de tarefas personalizadas para realizar implantações de sistemas operacionais especializados.  

 Para obter mais informações sobre como criar sequências de tarefas, consulte [Criar sequências de tarefas](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTaskSequence).  

##  <a name="a-namebkmktsedita-edit-a-task-sequence"></a><a name="BKMK_TSEdit"></a> Editar uma sequência de tarefas  
 Edite a sequência de tarefas usando o **Editor de Sequência de Tarefas**. O editor pode fazer as seguintes alterações na sequência de tarefas:  

-   Adicionar ou remover etapas da sequência de tarefas.  

-   Alterar a ordem das etapas da sequência de tarefas.  

-   Adicionar ou remover grupos de etapas.  

-   Especificar se a sequência de tarefas continua quando ocorre um erro.  

-   Adicionar condições às etapas e aos grupos de uma sequência de tarefas.  

> [!IMPORTANT]  
>  Se a sequência de tarefas tiver quaisquer referências não associadas a um pacote ou um programa como um resultado da edição, você deve corrigir a referência, excluir o programa sem referência da sequência de tarefas ou desabilitar temporariamente a etapa da sequência de tarefas com erro até que a referência seja corrigida ou removida.  

 Para obter mais informações sobre como editar sequências de tarefas, consulte [Editar uma sequência de tarefas](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

##  <a name="a-namebkmktsdeploya-deploy-a-task-sequence"></a><a name="BKMK_TSDeploy"></a> Implantar uma sequência de tarefas  
 É possível implantar uma sequência de tarefas em computadores de destino que estiverem em qualquer coleção do Configuration Manager. Isso inclui a coleção **Todos os Computadores Desconhecidos** que é usada para implantar sistemas operacionais em computadores desconhecidos. No entanto, você não pode implantar uma sequência de tarefas em coleções de usuário.  

> [!IMPORTANT]  
>  Não implante sequências de tarefas que instalam sistemas operacionais em coleções inadequadas, como, a coleção **Todos os Sistemas** . Certifique-se de que a coleção na qual irá você implantar a sequência de tarefas contenha somente computadores em que você deseja que o sistema operacional seja instalado. Para evitar uma implantação de sistema operacional indesejada, é possível gerenciar as configurações de implantação. Para obter mais informações, consulte [Configurações para gerenciar implantações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

 Cada computador de destino que recebe a sequência de tarefas executa a sequência de acordo com as configurações especificadas na implantação. As sequências de tarefas em si não contêm arquivos ou programas associados. Os arquivos referenciados por uma sequência de tarefas já devem estar presentes no computador de destino ou residir em um ponto de distribuição que os clientes podem acessar. Além disso, a sequência de tarefas instala os pacotes que são referenciados por programas, mesmo que o programa ou o pacote já esteja instalado no computador de destino.  

> [!NOTE]  
>  Em comparação com pacotes e programas, se a sequência de tarefas instalar um aplicativo, o aplicativo só será instalado se as regras de requisitos do aplicativo forem atendidas e se o aplicativo ainda não estiver instalado, com base no método de detecção especificado para ele.  

 O cliente do Configuration Manager executa uma implantação da sequência de tarefas quando baixa a política do cliente. Para iniciar esta ação, em vez de esperar até o próximo ciclo de sondagem, consulte [Iniciar recuperação de política para um cliente do Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

 Ao implantar sequências de tarefas em dispositivos Windows Embedded com filtro de gravação habilitado, é possível especificar se deseja desabilitar o filtro de gravação no dispositivo durante a implantação e reiniciá-lo após a implantação. Se o filtro de gravação não for desabilitado, a sequência de tarefas será implantada em uma sobreposição temporária e não estará disponível quando o dispositivo for reiniciado.  

> [!NOTE]  
>  Ao implantar uma sequência de tarefas em um dispositivo Windows Embedded, verifique se o dispositivo é membro de uma coleção com uma janela de manutenção configurada. Isso permite que você gerencie quando o filtro de gravação está desabilitado e habilitado e quando o dispositivo é reiniciado.  
>   
>  Se clientes baixarem sequências de tarefas fora de uma janela de manutenção, a sequência de tarefas será baixada duas vezes. Neste cenário, os clientes irão baixar a sequência de tarefas, desabilitar os filtros de gravação, reiniciar o computador e depois baixar a sequência de tarefas novamente, porque ela foi baixada em uma sobreposição temporária que é apagada quando o dispositivo é reiniciado.  

 Para obter mais informações sobre como implantar sequências de tarefas, consulte [Implantar uma sequência de tarefas](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

##  <a name="a-namebkmktsexportimporta-export-and-import-a-task-sequences"></a><a name="BKMK_TSExportImport"></a> Exportar e importar uma sequência de tarefas  
 O Configuration Manager permite exportar e importar sequências de tarefas. Quando você exporta uma sequência de tarefas, pode incluir os objetos que são referenciados pela sequência. Esses incluem uma imagem do sistema operacional, uma imagem de inicialização, um pacote de agente de cliente, um pacote de drivers e aplicativos com dependências.  

> [!NOTE]  
>  O processo de exportação e importação de sequências de tarefas é muito semelhante ao processo de exportação e importação de aplicativos no Configuration Manager.  

 Para obter mais informações sobre como exportar e importar sequências de tarefas, consulte [Exportar e importar sequências de tarefas](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ExportImport).  

##  <a name="a-namebkmktsruna-run-a-task-sequence"></a><a name="BKMK_TSRun"></a> Executar uma sequência de tarefas  
 Por padrão, as sequências de tarefas são sempre executadas usando a conta Sistema Local. A etapa de linha de comando da sequência de tarefas fornece a capacidade de executar a sequência de tarefas como uma conta diferente. Quando a sequência de tarefas é executada, o cliente do Configuration Manager verifica primeiro se há pacotes referenciados antes de começar as etapas da sequência de tarefas. Se um pacote referenciado não for validado ou não estiver disponível em um ponto de distribuição, a sequência de tarefas retornará um erro para a etapa da sequência de tarefas associada.  

 Se uma sequência de tarefas distribuída estiver configurada para ser baixada e executada, todos os pacotes e aplicativos dependentes serão baixados para o cache do cliente do Configuration Manager. Os pacotes e aplicativos necessários serão obtidos dos pontos de distribuição e, se o tamanho do cache do cliente do Configuration Manager for muito pequeno ou o pacote ou aplicativo não puder ser encontrado, a sequência de tarefas falhará e uma mensagem de status será gerada. Você também pode especificar que o cliente baixe o conteúdo apenas quando necessário quando você selecionar **Baixar conteúdo localmente quando necessário, executando a sequência de tarefas**, ou pode usar a opção **Executar programa do ponto de distribuição** para especificar que o cliente instale os arquivos diretamente do ponto de distribuição sem baixá-los para o cache primeiro. A opção **Executar programa do ponto de distribuição** só estará disponível se os pacotes referenciados tiverem a configuração **Copiar o conteúdo deste pacote em um compartilhamento de pacote nos pontos de distribuição** habilitada na guia **Acesso a Dados** nas propriedades do **Pacote**.  

 Se um aplicativo ou pacote dependente não puder ser localizado pelo cliente que executa a sequência de tarefas, o cliente enviará imediatamente uma mensagem de erro quando a implantação for configurada como **Disponível**. No entanto, se a implantação estiver configurada como **Obrigatória**, o cliente do Configuration Manager esperará e tentará baixar o conteúdo até o prazo, no caso de o conteúdo ainda não ter sido replicado para um ponto de distribuição que o cliente possa acessar.  

 Quando uma sequência de tarefas é concluída com êxito ou falha, o Configuration Manager registra isso em seu histórico do cliente. Não é possível cancelar nem parar uma sequência de tarefas depois que ela é iniciada em um computador.  

> [!IMPORTANT]  
>  Se uma etapa de sequência de tarefas exigir que o computador cliente seja reiniciado, o cliente deverá ser capaz de inicializar a partir de uma partição de disco formatada. Caso contrário, a sequência de tarefas falhará, independentemente de qualquer manipulação de erro especificada pela sequência.  

 Quando um objeto dependente de uma sequência de tarefas, como um pacote de distribuição de software, é atualizado para uma versão mais recente, qualquer sequência de tarefas que referencia o pacote é atualizada automaticamente e faz referência à versão mais recente, independentemente de quantas atualizações foram implantadas.  

> [!NOTE]  
>  Para que um cliente do Configuration Manager execute uma sequência de tarefas, ele verifica todas as sequências de tarefas quanto a possíveis dependências e quanto à disponibilidade dessas dependências em um ponto de distribuição. Se o cliente encontrar um objeto excluído do qual a sequência de tarefas depende, o cliente gerará um erro e não executará a sequência de tarefas.  

###  <a name="a-namebkmkrunprograma-run-a-program-before-the-task-sequence-is-run"></a><a name="BKMK_RunProgram"></a> Executar um programa antes que a sequência de tarefas seja executada  
 Você pode selecionar um programa que seja executado para que a sequência de tarefas seja executada. Para especificar um programa para ser executado primeiro, abra a caixa de diálogo **Propriedades** da sequência de tarefas e selecione a guia **Avançado** para definir as seguintes opções:  

> [!IMPORTANT]  
>  Para executar um programa para que a sequência de tarefas seja executada, todo o conteúdo da sequência de tarefas e do programa deve estar disponível em um compartilhamento de pacotes. Você pode configurar o compartilhamento de pacotes na guia **Acesso a Dados** nas propriedades do pacote.  

-   **Executar outro programa primeiro**: especifique que você quer que outro programa seja executado antes que a sequência de tarefas seja executada.  

    > [!IMPORTANT]  
    >  Esta configuração aplica-se apenas às sequências de tarefas que são executadas no sistema operacional completo. O Configuration Manager ignorará esta configuração se a sequência de tarefas for iniciada usando o PXE ou a mídia de inicialização.  

-   **Pacote**: especifique o pacote que contém o programa.  

-   **Programa**: especifique o programa a ser executado.  

-   **Sempre executar este programa primeiro**: especifique que você deseja que o Configuration Manager execute este programa cada vez que executar a sequência de tarefas no mesmo cliente. Por padrão, depois que um programa é executado com sucesso, ele não será executado novamente se a sequência de tarefas for reexecutada no mesmo cliente.  

 Se o programa selecionado não for executado em um cliente, a sequência de tarefas não será executada.  

##  <a name="a-namebkmktsmaintenancewindowa-use-a-maintenance-window-to-specify-when-a-task-sequence-can-run"></a><a name="BKMK_TSMaintenanceWindow"></a> Usar uma janela de manutenção para especificar quando uma sequência de tarefas pode ser executada  
 Você pode especificar quando a sequência de tarefas pode ser executada definindo uma janela de manutenção para a coleção que contém os computadores de destino. As janelas de manutenção são configuradas com uma data de início, hora de início e término e um padrão de recorrência. Além disso, quando você define a agenda para a janela de manutenção, pode especificar que a janela de manutenção aplique-se apenas àquela sequências de tarefas. Para obter mais informações, consulte [Como usar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

> [!IMPORTANT]  
>  Quando você configura uma janela de manutenção para executar uma sequência de tarefas, uma vez que as sequências de tarefas iniciam, continuam a ser executadas mesmo depois que a janela de manutenção é fechada. A sequência de tarefas será concluída com êxito ou erro.  

##  <a name="a-namebkmktsnetworkaccessaccounta-task-sequences-and-the-network-access-account"></a><a name="BKMK_TSNetworkAccessAccount"></a> Sequências de tarefas e Conta de acesso de rede  
 Embora as sequências de tarefas sejam executadas apenas no contexto da conta do Sistema Local, pode ser necessário configurar a conta de acesso à rede nas seguintes circunstâncias:  

-   Você precisa configurar a Conta de Acesso à Rede corretamente ou a sequência de tarefas falhará se tentar acessar os pacotes do Configuration Manager nos pontos de distribuição para concluir a tarefa. Para obter mais informações sobre a Conta de Acesso à Rede, consulte [Conta de Acesso à Rede](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#a-namebkmknaaa-network-access-account).  

    > [!NOTE]  
    >  A Conta de Acesso à Rede nunca é usada como contexto de segurança para a execução de programas, instalação de aplicativos, instalação de atualizações, ou execução de sequências de tarefas; no entanto, a Conta de Acesso à Rede é usada para acessar recursos associados à rede.  

-   Quando você usa uma imagem de inicialização para iniciar uma implantação de sistema operacional, o Configuration Manager usa o ambiente do Windows PE, que não é um sistema operacional completo. O ambiente do Windows PE usa um nome aleatório gerado automaticamente, que não é membro de nenhum domínio. Se você não configurar a Conta de Acesso à Rede corretamente, o computador poderá não ter as permissões necessárias para acessar os pacotes exigidos do Configuration Manager para concluir a sequência de tarefas.  

##  <a name="a-namebkmktscreatemediaa-create-media-for-task-sequences"></a><a name="BKMK_TSCreateMedia"></a> Criar mídia para sequências de tarefas  
 Você pode gravar sequências de tarefas e seus arquivos relacionados e dependências em vários tipos de mídia. Isso inclui a gravação em mídia removível, como um conjunto de DVD ou CD ou unidade flash USB para mídia de captura, autônoma e inicializável, ou gravação em um arquivo WIM (Windows Imaging Format) para mídia em pré-teste.  

 Você pode criar os seguintes tipos de mídia:  

-   **Mídia de captura**. Esse tipo de mídia captura uma imagem do sistema operacional configurada e criada fora da infraestrutura do Configuration Manager. Mídia de captura pode conter programas personalizados que podem ser executados antes da execução de uma sequência de tarefas. O programa personalizado pode interagir com a área de trabalho, solicitar valores de entrada ao usuário ou criar variáveis ​​para serem usadas pela sequência de tarefas.  

     Para obter mais informações, consulte [Criar mídia de captura](../deploy-use/create-capture-media.md).  

-   **Mídia autônoma**. Mídia autônoma contém a sequência de tarefas e todos os objetos associados necessários para a execução da sequência de tarefas. Sequências de tarefas de mídia autônoma podem ser executadas quando o Configuration Manager tem conectividade limitada ou nenhuma conectividade com a rede. Mídia autônoma pode ser executada das seguintes maneiras:  

    -   Se o computador de destino não for inicializado, a imagem do Windows PE associada à sequência de tarefas será usada por meio da mídia autônoma e a sequência de tarefas terá início.  

    -   A mídia autônoma pode ser iniciada manualmente se um usuário estiver conectado à rede e iniciar a instalação.  

    > [!IMPORTANT]  
    >  As etapas de uma sequência de tarefas de mídia autônoma devem ser capazes de executar sem recuperar dados da rede; caso contrário, a etapa que tenta recuperar os dados falhará. Por exemplo, uma etapa de sequência de tarefas que requer um ponto de distribuição para obter um pacote falha; no entanto, se o pacote necessário estiver contido na mídia autônoma, a etapa terá êxito.  

     Para obter mais informações, consulte [Criar mídia autônoma](../deploy-use/create-stand-alone-media.md).  

-   **Mídia inicializável**. A mídia inicializável contém os arquivos necessários para iniciar um computador de destino para que ele possa se conectar à infraestrutura do Configuration Manager para determinar qual sequência de tarefas será executada com base na sua associação a uma coleção. A sequência de tarefas e os objetos dependentes não estão contidos na mídia. Em vez disso, eles são obtidos pela rede por meio do cliente do Configuration Manager. Esse método é útil para novos computadores ou implantações bare-metal, ou quando não há nenhum cliente ou sistema operacional do Configuration Manager no computador de destino.  

     Para obter mais informações, consulte [Criar mídia inicializável](../deploy-use/create-bootable-media.md).  

-   **Mídia pré-configurada**. Mídia em pré-teste implanta uma imagem do sistema operacional em um computador de destino que não está provisionado. A mídia pré-configurada é armazenada como um arquivo em formato WIM (Windows Imaging) que pode ser instalado em um computador bare-metal pelo fabricante ou em um centro de preparo corporativo que não está conectado ao ambiente do Configuration Manager.  

     Para mais informações, consulte [Criar mídia pré-configurada](../deploy-use/create-prestaged-media.md).  

 Ao criar mídia, especifique uma senha para a mídia para controlar o acesso aos arquivos contidos nela. Se você especificar uma senha, um usuário deverá estar presente para digitar a senha no computador de destino quando a sequência de tarefas for executada.  

 Quando você executa uma sequência de tarefas usando mídia, a arquitetura do chip do computador especificado contido na mídia não será reconhecida e a sequência tarefa tentará ser executada, mesmo que a arquitetura especificada não corresponda à que está atualmente instalada no computador de destino. Se a arquitetura do chip contido na mídia não corresponder à arquitetura do chip instalado no computador de destino, a instalação falhará.  

 Para obter mais informações sobre como implantar sistemas operacionais usando a mídia, consulte [Criar mídia de sequência de tarefas](../deploy-use/create-task-sequence-media.md).  



<!--HONumber=Dec16_HO3-->


