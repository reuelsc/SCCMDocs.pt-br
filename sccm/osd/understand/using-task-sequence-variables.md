---
title: Como usar variáveis de sequência de tarefas
titleSuffix: Configuration Manager
description: Saiba mais sobre como usar as variáveis em uma sequência de tarefas do Configuration Manager.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bc7de742-9e5c-4a70-945c-df4153a61cc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18305b26937c87cbdb4d5726bded571699416793
ms.sourcegitcommit: be8c0182db9ef55a948269fcbad7c0f34fd871eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42756273"
---
# <a name="how-to-use-task-sequence-variables-in-configuration-manager"></a>Como usar as variáveis de sequência de tarefas no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 O mecanismo de sequência de tarefas no recurso de implantação de sistema operacional do Configuration Manager usa muitas variáveis para controlar seus comportamentos. Use essas variáveis para: 
 - Definir as condições nas etapas  
 - Alterar os comportamentos de etapas específicas  
 - Usar em scripts para ações mais complexas  


 Para obter uma referência de todas as variáveis de sequência de tarefas disponíveis, consulte [Variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables).



## <a name="bkmk_types"></a> Tipos de variáveis

 Há muitos tipos de variáveis:  
 - [Interna](#bkmk_built-in)  
 - [Ação](#bkmk_action)  
 - [Personalizado](#bkmk_custom)  
 - [Somente leitura](#bkmk_read-only)  
 - [Matriz](#bkmk_array)  


### <a name="bkmk_built-in"></a> Variáveis internas

 Variáveis internas fornecem informações sobre o ambiente em que a sequência de tarefas é executada. Seus valores estão disponíveis em toda a sequência de tarefas. Normalmente, o mecanismo de sequência de tarefas inicia variáveis internas antes de executar qualquer etapa. 

 Por exemplo, a variável interna **\_SMSTSLogPath** é uma variável de ambiente que especifica o caminho em que os componentes do Configuration Manager gravam arquivos de log. Qualquer etapa de sequência de tarefas pode acessar essa variável de ambiente. 

 A sequência de tarefas avalia algumas variáveis antes de cada etapa. Por exemplo, **\_SMSTSCurrentActionName** lista o nome da etapa atual. 

### <a name="bkmk_action"></a> Variáveis de ação

 Variáveis de ação de sequência de tarefas especificam definições de configuração usadas por uma única etapa em uma sequência de tarefas. Por padrão, a etapa inicia suas configurações antes da execução. Essas configurações estão disponíveis apenas enquanto a etapa de sequência de tarefas associada está em execução. A sequência de tarefas adiciona o valor da variável de ação ao ambiente antes de executar a etapa. E remove o valor do ambiente após a etapa ser executada.

 Por exemplo, você adiciona a etapa **Executar Linha de Comando** a uma sequência de tarefas. Esta etapa inclui uma propriedade **Iniciar em**. A sequência de tarefas armazena um valor padrão para essa propriedade como a variável **WorkingDirectory**. A sequência de tarefas inicia esse valor antes de executar a etapa **Executar Linha de Comando**. Enquanto esta etapa estiver em execução, acesse o valor de propriedade **Iniciar em** pelo valor **WorkingDirectory**. Depois que a etapa for concluída, a sequência de tarefas remove o valor da variável **WorkingDirectory** do ambiente. Se a sequência de tarefas inclui outra etapa **Executar Linha de Comando**, ela inicia uma nova variável **WorkingDirectory**. Nesse momento, a sequência de tarefas define a variável como o valor inicial da etapa atual. Para saber mais, confira [WorkingDirectory](using-task-sequence-variables.md#WorkingDirectory).  

 O valor *padrão* de uma variável de ação está presente quando a etapa é executada. Se você definir um valor *novo*, ele estará disponível para várias etapas na sequência de tarefas. Se você substituir um valor padrão, o novo valor permanecerá no ambiente. Esse novo valor substitui o valor padrão das outras etapas na sequência de tarefas. Por exemplo, você adiciona uma etapa **Definir Variável de Sequência de Tarefas** como a primeira etapa da sequência de tarefas. Esta etapa define a variável **WorkingDirectory** como `C:\`. Qualquer etapa **Executar Linha de Comando** na sequência de tarefas usa o novo valor de diretório inicial.  

 Algumas etapas de sequência de tarefas marcam determinadas variáveis de ação como *saída*. Etapas posteriores na sequência de tarefas leem essas variáveis de saída.

 > [!Note]  
 > Nem todas as etapas de sequência de tarefas têm variáveis de ação. Por exemplo, embora existam variáveis associadas à ação **Habilitar BitLocker**, não há variáveis associadas à ação **Desabilitar BitLocker**.  


### <a name="bkmk_custom"></a> Variáveis personalizadas

 Essas variáveis são as que o Configuration Manager não cria. Inicie suas próprias variáveis para usar como condições, nas linhas de comando ou em scripts. 

 Quando você for especificar um nome para a nova variável de sequência de tarefas, siga estas diretrizes:  

 - O nome da variável da sequência de tarefas pode conter letras, números, o caractere sublinhado (`_`) e um hífen (`-`).  

 - Os nomes das variáveis da sequência de tarefas podem ter no mínimo um e no máximo 256 caracteres.  

 - As variáveis definidas pelo usuário devem começar com uma letra (`A-Z` ou `a-z`).  

 - Os nomes das variáveis definidas pelo usuário não podem começar com o caractere sublinhado. Somente variáveis de sequência de tarefas somente leitura são precedidas pelo caractere sublinhado.  

 - Os nomes das variáveis de sequência de tarefas não diferenciam maiúsculas de minúsculas. Por exemplo, `OSDVAR` e `osdvar` são a mesma variável de sequência de tarefas.  

 - Os nomes das variáveis de sequência de tarefas não podem começar nem terminar com um espaço. Também não podem conter espaços. A sequência de tarefas ignora os espaços no começo ou no fim do nome de uma variável.  


 Não há um limite para quantas variáveis de sequência de tarefas podem ser criadas. No entanto, o número de variáveis é limitado pelo tamanho do ambiente de sequência de tarefas. O limite do tamanho total para o ambiente da sequência de tarefas é de 32 MB.  


### <a name="bkmk_read-only"></a> Variáveis somente leitura

 Não é possível alterar o valor de algumas variáveis que são somente leitura. Normalmente, o nome começa com um caractere de sublinhado (\_). A sequência de tarefas as usa para suas operações. Variáveis somente leitura ficam visíveis no ambiente da sequência de tarefas. 

 Essas variáveis são úteis em scripts ou linhas de comando. Por exemplo, a execução de uma linha de comando e o direcionamento da saída para um arquivo de log em **\_SMSTSLogPath** com os outros arquivos de log.

 > [!NOTE]  
 >  As variáveis de sequência de tarefas somente leitura podem ser lidas pelas etapas de uma sequência de tarefas, mas não podem ser configuradas. Por exemplo, use uma variável somente leitura como parte da linha de comando para uma etapa **Executar Linha de Comando**. Você não pode definir uma variável somente leitura usando a etapa **Definir Variável de Sequência de Tarefas**.  



### <a name="bkmk_array"></a> Variáveis de matriz

 A sequência de tarefas armazena algumas variáveis como uma matriz. Cada elemento na matriz representa as configurações de um único objeto. Quando um dispositivo tem mais de um objeto para configurar, use essas variáveis. As seguintes etapas de sequência de tarefas usam variáveis de matriz:

 - [Aplicar Configurações de Rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  

 - [Formatar e Particionar Disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk)  



## <a name="bkmk_set"></a> Como definir variáveis

 Para as variáveis personalizadas ou variáveis que não são somente leitura, há vários métodos para iniciar e definir o valor da variável:  

 - [Definir Variável de Sequência de Tarefas](#bkmk_set-ts-step)  
 - [Definir Variáveis Dinâmicas](#bkmk_set-dyn-step)  
 - [Variáveis de coleção e dispositivo](#bkmk_set-coll-var)  
 - [Objeto COM TSEnvironment](#bkmk_set-com)  
 - [Comando prestart](#bkmk_set-prestart)  
 - [Assistente de Mídia de Sequência de Tarefas](#bkmk_set-media)  


 Exclua uma variável do ambiente usando os mesmos métodos da criação de uma variável. Para excluir uma variável, defina seu valor como uma cadeia de caracteres vazia.  

 Você pode combinar métodos para configurar uma variável de sequência de tarefas com valores diferentes para a mesma sequência. Por exemplo, defina os valores padrão usando o editor de sequência de tarefas e, em seguida, defina valores personalizados, usando um script. 

 Se você definir a mesma variável por métodos diferentes, o mecanismo de sequência de tarefas usa a seguinte ordem:  

 1. Ela primeiro avalia as variáveis da coleção.  

 2. Variáveis específicas de dispositivos substituem a mesma variável definida em uma coleção.  

 3. As variáveis definidas por qualquer método durante a sequência de tarefas têm precedência sobre variáveis de coleção ou dispositivo.  


#### <a name="general-limitations-for-task-sequence-variable-values"></a>Limitações gerais para valores de variáveis de sequência de tarefas  

 - Valores de variáveis de sequência de tarefas não podem ter mais de 4.000 caracteres.  

 - Você não pode alterar uma variável de sequência de tarefas somente leitura. Variáveis somente leitura têm nomes que começam com um caractere de sublinhado (`_`).  

 - Os valores das variáveis de sequência de tarefas podem diferenciar maiúsculas de minúsculas dependendo do uso do valor. Na maioria dos casos, os valores das variáveis de sequência de tarefas não diferenciam maiúsculas de minúsculas. Uma variável que inclui uma senha diferencia maiúsculas de minúsculas.  


### <a name="bkmk_set-ts-step"></a> Definir Variável de Sequência de Tarefas

 Use essa etapa na sequência de tarefas para definir uma única variável em um único valor. 

 Para saber mais, confira [Definir Variáveis de Sequência de Tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable). 


### <a name="bkmk_set-dyn-step"></a> Definir Variáveis Dinâmicas

 Use essa etapa na sequência de tarefas para definir uma ou mais variáveis de sequência de tarefas. Você pode definir regras nesta etapa para determinar quais variáveis e valores usar. 

 Para obter mais informações, consulte [Definir Variáveis Dinâmicas](/sccm/osd/understand/task-sequence-steps#BKMK_SetDynamicVariables).


### <a name="bkmk_set-coll-var"></a> Variáveis de coleção e dispositivo

 Defina variáveis nas propriedades de uma coleção ou de um dispositivo específico. 

 Para saber mais, confira [Criar variáveis de sequência de tarefas em computadores e coleções](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_CreateTSVariables).


### <a name="bkmk_set-com"></a> Objeto COM TSEnvironment

 Para trabalhar com variáveis de um script, use o objeto **TSEnvironment**. 

 Para saber mais, confira [Como usar variáveis em uma sequência de tarefas em execução](/sccm/develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence) no SDK do Configuration Manager.


### <a name="bkmk_set-prestart"></a> Comando prestart

 O comando prestart é um script ou um executável que é processado no Windows PE antes de o usuário selecionar a sequência de tarefas. O comando prestart pode consultar uma variável ou solicitar que o usuário forneça informações e, em seguida, salvá-la no ambiente. Use o objeto COM [TSEnvironment](#bkmk_set-com) para ler e gravar as variáveis do comando prestart. 

 Para mais informações, consulte [Comandos prestart para mídia de sequência de tarefas](/sccm/osd/understand/prestart-commands-for-task-sequence-media).


### <a name="bkmk_set-media"></a> Assistente de Mídia de Sequência de Tarefas

 Especifica variáveis de sequências de tarefas que são executadas da mídia. Ao usar a mídia para implantar o sistema operacional, você adiciona as variáveis ​​da sequência de tarefas e especifica seus valores durante a criação da mídia. As variáveis e seus valores são armazenados na mídia.  

 > [!NOTE]  
 >  As sequências de tarefas são armazenadas em mídia autônoma. No entanto, todos os outros tipos de mídia, tais como mídia em pré-teste, recuperam a sequência de tarefas por meio de um ponto de gerenciamento.  

 Ao executar uma sequência de tarefas de mídia, é possível adicionar uma variável na página **Personalização** do assistente. 

 Use as variáveis de mídia em vez de variáveis por coleção ou por computador. Se a sequência de tarefas for executada por meio de uma mídia, as variáveis por computador e por coleção não se aplicam e não são usadas.  

 > [!TIP]  
 >  A sequência de tarefas grava a ID do pacote e a linha de comando prestart no arquivo **CreateTSMedia.log** no computador que executa o console do Configuration Manager. Esse arquivo de log inclui o valor de quaisquer variáveis da sequência de tarefas. Examine este arquivo de log para verificar o valor das variáveis da sequência de tarefas.  

 Para saber mais, confira [Criar mídia de sequência de tarefas](/sccm/osd/deploy-use/create-task-sequence-media).



## <a name="bkmk_access"></a> Como acessar variáveis

 Após especificar a variável e seu valor usando um dos métodos da seção anterior, use-a em suas sequências de tarefas. Por exemplo, acesse os valores padrão das variáveis de sequência de tarefas internas ou crie uma etapa condicional ao valor de uma variável.  

 Use os seguintes métodos para acessar valores de variáveis no ambiente da sequência de tarefas:
 - [Usar em uma etapa](#bkmk_access-step)  
 - [Condição da etapa](#bkmk_access-condition)  
 - [Script personalizado](#bkmk_access-script)  
 - [Arquivo de resposta de instalação do Windows](#bkmk_access-answer)  
  

### <a name="bkmk_access-step"></a> Usar em uma etapa

 Especifique um valor de variável para uma configuração em uma etapa da sequência de tarefas. No editor de sequência de tarefas, edite a etapa e especifique o nome da variável como o valor do campo. Coloque o nome da variável entre sinais de porcentagem (`%`). 

 Por exemplo, use o nome de uma variável como parte do campo **Linha de Comando** da etapa **Executar Linha de Comando**. A linha de comando a seguir grava o nome do computador em um arquivo de texto. 

 `cmd.exe /c %_SMSTSMachineName% > C:\File.txt`


### <a name="bkmk_access-condition"></a> Condição da etapa

 Use variáveis de sequência de tarefas internas ou personalizadas como parte de uma condição em uma etapa ou grupo. A sequência de tarefas avalia o valor da variável antes de executar a etapa ou grupo.

 Para adicionar uma condição que avalia um valor de variável, faça o seguinte:  

 1. No editor de sequência de tarefas, selecione a etapa ou grupo ao qual você deseja adicionar a condição.  

 2. Alterne para a guia **Opções** da etapa ou do grupo. Clique em **Adicionar Condição** e selecione **Variável de Sequência de Tarefas**.  

 3. Na caixa de diálogo **Variável de Sequência de Tarefas**, especifique as seguintes configurações:  

    - **Variável**: o nome da variável. Por exemplo, `_SMSTSInWinPE`.  

    - **Condição**: a condição para avaliar o valor da variável. Por exemplo, **igual a**.  

    - **Valor**: o valor da variável a verificar. Por exemplo, `false`.  


 Os três exemplos anteriores formam uma condição comum para testar se a sequência de tarefas está em execução de uma imagem de inicialização no Windows PE: 

 > **Variável de Sequência de Tarefas** `_SMSTSInWinPE equals "false"`

 Consulte essa condição no grupo **Capturar Arquivos e Configurações** do modelo da sequência de tarefas padrão para instalar uma imagem de sistema operacional existente.


### <a name="bkmk_access-script"></a> Script personalizado

 Leia e grave variáveis usando o objeto COM **Microsoft.SMS.TSEnvironment** enquanto a sequência de tarefas está em execução.

 O exemplo do Windows PowerShell a seguir consulta a variável **smstslogpath** para obter o local do log atual. O script também define uma variável personalizada.

 ```PowerShell
 # Create an object to access the task sequence environment
 $tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment
 
 # Query the environment to get an existing variable
 # Set a variable for the task sequence log path
 $LogPath = $tsenv.Value("_SMSTSLogPath")

 # Or, convert all of the variables currently in the environment to PowerShell variables
 $tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }

 # Write a message to a log file
 Write-Output "Hello world!" | Out-File -FilePath "$_SMSTSLogPath\mylog.log" -Encoding "Default" -Append
 
 # Set a custom variable "startTime" to the current time
 $tsenv.Value("startTime") = (Get-Date -Format HH:mm:ss) + ".000+000"
 ```


###  <a name="bkmk_access-answer"></a> Arquivo de resposta de instalação do Windows

O arquivo de resposta de instalação do Windows que você fornece pode conter as variáveis da sequência de tarefas. Use o formulário `%varname%`, em que *varname* é o nome da variável. A etapa **Instalar Windows e ConfigMgr** substitui a cadeia de caracteres do nome da variável pelos valores reais da variável. Essas variáveis de sequência de tarefas integradas não podem ser usadas em campos somente numéricos em um arquivo de resposta unattend.xml.

Para mais informações, consulte [Configurar Windows e ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr).



## <a name="see-also"></a>Consulte também

- [Etapas da sequência de tarefas](/sccm/osd/understand/task-sequence-steps)
- [Variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables)
- [Considerações sobre o planejamento para automatizar tarefas](/sccm/osd/plan-design/planning-considerations-for-automating-tasks)
