---
title: Solucionar problemas do MDT
titleSuffix: Microsoft Deployment Toolkit
description: 'Referência de solução de problemas para o Microsoft Deployment Toolkit '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 91a7a69a-deac-4b0f-aac9-b7bd187c53fb
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: efb65086878a46bfb3485fdd8b0be6f613225261
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2018
ms.locfileid: "27821010"
---
# <a name="troubleshooting-reference-for-the-microsoft-deployment-toolkit"></a>Referência de solução de problemas para o Microsoft Deployment Toolkit
 A implantação de sistemas operacionais e aplicativos, bem como a migração de estado do usuário pode ser um esforço desafiador, mesmo quando você está munido das ferramentas e diretrizes adequadas. Esta referência, que faz parte do MDT (Microsoft® Deployment Toolkit) 2013, fornece informações sobre problemas conhecidos atuais, soluções alternativas para esses problemas e diretrizes de solução de problemas.  

> [!NOTE]
>  Neste documento, *Windows* aplica-se aos sistemas operacionais Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2, salvo indicação em contrário. O MDT não é compatível com versões do Windows baseadas no processador ARM. Da mesma forma, *MDT* se refere ao MDT 2013, salvo indicação em contrário.  

> [!NOTE]
>  O Microsoft DaRT (Diagnostics and Recovery Toolset) contém ferramentas poderosas para recuperar e solucionar problemas de computadores cliente que não iniciam ou estão instáveis. Você pode usar o DaRT para determinar a causa de um travamento, restaurar arquivos perdidos e assim por diante. Você também pode usar o DaRT como uma ferramenta de solução de problemas ao desenvolver e implantar um sistema operacional Windows. Por exemplo, se uma imagem criada falhar em iniciar corretamente, você poderá iniciar o computador cliente que contém a imagem usando o ERD Commander, um ambiente de diagnóstico. Em seguida, você pode explorar o disco rígido do computador cliente, exibir o log de eventos, remover as atualizações, alterar as configurações do sistema operacional e assim por diante. O DaRT faz parte do Microsoft Desktop Optimization Pack para Software Assurance. Para saber mais sobre o DaRT, consulte [http://www.microsoft.com/windows/enterprise/products-and-technologies/mdop/dart.aspx](http://www.microsoft.com/windows/enterprise/products-and-technologies/mdop/dart.aspx).  

## <a name="understanding-logs"></a>Entendendo logs  
 Para iniciar a solução de problemas efetiva do MDT, você deve ter um entendimento claro dos vários arquivos .log usados durante uma implantação de sistema operacional. Quando você souber quais arquivos de log pesquisar para qual condição de falha e qual horário, os problemas que eram misteriosos e difíceis de entender poderão se tornar claros e compreensíveis.  

 O formato de arquivo de log do MDT é projetado para ser lido por Trace32, que faz parte do System Center Configuration Manager 2007 Toolkit V2, disponível para download no [Centro de Download da Microsoft](http://www.microsoft.com/download/details.aspx?id=9257). Os logs também podem ser lidos pela Ferramenta de Log de Rastreamento do Configuration Manager (CMTrace) que está disponível com o System Center 2012 Configuration Manager e versões posteriores. Use essas ferramentas sempre que possível para ler os arquivos de log, pois ele facilita muito a localização de erros.  

 O restante desta seção detalha os arquivos de log criados durante a implantação, bem como durante a Instalação do Windows. Esta seção também fornece exemplos de quando usar os arquivos para solução de problemas.  

### <a name="mdt-logs"></a>Logs do MDT  
 Cada script do MDT cria automaticamente arquivos de log durante a execução. Os nomes desses arquivos de log correspondem ao nome do script, por exemplo, ZTIGather.wsf cria um arquivo de log chamado *ZTIGather.log*. Cada script também atualiza um arquivo de log mestre comum (BDD.log) que agrega o conteúdo dos arquivos de log que os scripts do MDT criam. Os arquivos de log do MDT residem em C:\MININT\SMSOSD\OSDLOGS durante o processo de implantação. Dependendo do tipo de implantação que está sendo executado, os arquivos de log são movidos após a conclusão da implantação para %WINDIR%\SMSOSD ou %WINDIR%\TEMP\SMSOSD. Para implantações de LTI ( Lite Touch Installation), os logs começam em C:\MININT\SMSOSD\OSDLogs. Eles terminam em %WINDIR%\TEMP\DeploymentLogs quando o processamento de sequência de tarefas é concluído.  

 O MDT cria os seguintes arquivos de log:  

-   **BDD.log**. Este é o arquivo de log do MDT agregado que será copiado para um local de rede no final da implantação se você especificar a propriedade **SLShare** no arquivo Customsettings.ini.  

-   **LiteTouch.log**. Esse arquivo é criado durante as implantações de LTI. Ele reside em %WINDIR%\TEMP\DeploymentLogs a menos que você especifique a opção **/debug:true**.  

-   **Scriptname*.log**. Esse arquivo é criado por cada script do MDT. *Scriptname* representa o nome do script em questão.  

-   **SMSTS.log**. Esse arquivo é criado pelo Sequenciador de Tarefas e descreve todas as transações dele. Dependendo do cenário de implantação, ele pode residir em %TEMP%, %WINDIR%\System32\ccm\logs, C:\\\_SMSTaskSequence ou C:\SMSTSLog.  

-   **Wizard.log**. Os assistentes de implantação criam e atualizam esse arquivo.  

-   **WPEinit.log**. Esse arquivo é criado durante o processo de inicialização do Windows PE e é útil para solucionar problemas de erros encontrados ao iniciar o Windows PE.  

-   **DeploymentWorkbench_*id*.log**. Esse arquivo de log é criado na pasta %temp% quando você especifica **a /debug** ao iniciar o Workbench de Implantação.  

### <a name="configuration-manager-operating-system-deployment-logs"></a>Logs de implantação de sistema operacional do Configuration Manager  
 Para obter informações sobre quais arquivos de log de implantação de sistema operacional são criados pelo Microsoft System Center 2012 R2 Configuration Manager, consulte [Referência técnica para arquivos de log no Configuration Manager](http://technet.microsoft.com/library/hh427342.aspx).  

 Ao executar a USMT (Ferramenta de Migração do Usuário Windows), o MDT adiciona automaticamente as opções de log para salvar os arquivos de log da USMT para os locais de arquivo de log do MDT. Os arquivos de log e quando eles são criados são:  

-   **USMTEstimate.log**. Criado ao estimar os requisitos da USMT  

-   **USMTCapture.log**. Criado pela USMT durante a captura de dados  

-   **USMTRestore.log**. Criado pela USMT durante a restauração de dados  

 O script ZeroTouchInstallation.vbs verifica automaticamente os arquivos de log de andamento da USMT para verificar se há erros e avisos. O script gera a ID do evento 41010 para o Microsoft System Center Operations Manager com o seguinte resumo (em que *usmt_type* é **ESTIMATE**, **SCANSTATE** ou **LOADSTATE**, *error_count* é o número total de erros encontrados e *warning_count* é o número total de avisos encontrados):  

```  
ZTI USMT <usmt_type> reported <error_count> errors and <warning_count> warnings  
```  

 Se a contagem de erros for maior que 0, esse evento será um tipo de Erro. Se a contagem de avisos for maior que 0 sem erros, o evento será um tipo de Aviso. Caso contrário, o evento será um tipo Informativo.  

## <a name="identifying-error-codes"></a>Identificando códigos de erro  
A tabela 1 lista os códigos de erro que os scripts do MDT criam e fornece uma descrição de cada código. Esses códigos de erro são registrados no arquivo BDD.log.  

### <a name="table-1-error-codes-and-their-description"></a>Tabela 1. Códigos de erro e suas descrições  

|**Código de erro**|**Descrição**|  
|-|-|  
|5201|Não foi possível estabelecer uma conexão para o compartilhamento de implantação. A implantação não continuará.|  
|5203|Não foi possível estabelecer uma conexão para o compartilhamento de implantação. A implantação não continuará.|  
|5205|Não foi possível estabelecer uma conexão para o compartilhamento de implantação. A implantação não continuará.|  
|5206|O Assistente de Implantação foi cancelado ou não foi concluído com êxito. A implantação não continuará.|  
|5207|Não foi possível estabelecer uma conexão para o compartilhamento de implantação. A implantação não continuará.|  
|5208|**DeploymentType** não está definido. É necessário definir algum valor para **SkipWizard**.|  
|5208|Não é possível localizar o Sequenciador de Tarefas do SMS. A implantação não continuará.|  
|5400|Criar objeto: **Set *class_instance* = New *class_name***|  
|5490|Criar MSXML2.DOMDocument.|  
|5495|Criar MSXML2.DOMDocument.ParseErr.ErrCode.|  
|5496|LoadControlFile.FindFile: *ConfigFile*|  
|5601|Verificar GUID do sistema operacional: %OSGUID% existe.|  
|5602|Abrir o XML com OSGUID: %OSGUID%.|  
|5610|Verificar arquivo.|  
|5630|Verificar arquivo: *ImagePath*.|  
|5640|Verificar arquivo: *ImagePath*.|  
|5641|FindFile: ImageX.exe.|  
|5643|Localizar BootSect.exe.|  
|5650|Verificar diretório: *SourcePath*.|  
|5651|Verificar diretório: *SourcePath*\Platform.|  
|5652|FindFile: bootsect.exe.|  
|6001|Verificar a unidade.|  
|6002|Verificar a unidade.|  
|6010|Testar TSGUID.|  
|6020|Valor retornado de Robocopy: *Value*.|  
|6021|Valor retornado de Robocopy: *Value*.|  
|6101|Verificar o arquivo: *DeployCab*.|  
|6102|Expandir arquivos Sysprep do DEPLOY.CAB.|  
|6111|Executar Sysprep.exe.|  
|6121|Executar Sysprep.|  
|6191|Testar **CloneTag** no Registro para verificar a conclusão do Sysprep.|  
|6192|Testar **SystemSetupInProgress** no Registro para verificar a conclusão do Sysprep.|  
|6401|Servidor DHCP autorizado.|  
|6501|Não é possível fazer o backup do computador, não há nenhum caminho de rede (**BackupShare**, **BackupDir**) especificado.|  
|6502|ERRO: não é possível localizar IMAGEX, não é possível realizar o backup.|  
|6601|GetObject(... root/wmi:BCDStore).|  
|6602|BCD.OpenStore (*BCDStore*).|  
|6701|Protetores configurados.|  
|6702|Arquivos de inicialização movidos.|  
|6703|Criar partição BDE.|  
|6704|Desfragmentar unidade.|  
|6705|Reduza unidade.|  
|6706|Testando para mais de uma partição.|  
|6707|Criar arquivos de inicialização.|  
|6708|Criptografar o disco.|  
|6709|Conectar ao provedor WMI MicrosoftVolumeEncryption.|  
|6710|Criptografando o disco.|  
|6711|**ProtectKeyWithTPM**.|  
|6712|**ProtectKeyWithTPMAndPIN**.|  
|6713|**ProtectKeyWithTPMAndStartupKey**.|  
|6714|Salvar a chave externa no arquivo.|  
|6715|Proteger com chave externa.|  
|6716|Salvar a chave externa no arquivo.|  
|6717|Proteger chave com senha numérica.|  
|6718|**GetKeyProtectorNumberialP@ssword.**|  
|6718|Salvar senha no arquivo.|  
|6719|Abrir *PasswordFile*.|  
|6720|Criptografar a unidade.|  
|6721|Abrir *DiskPartFile*.|  
|6722|Criar partição.|  
|6723|Obter unidade BDE existente.|  
|6724|Abrir *DiskPartFile*.|  
|6727|Tentar abrir *DiskPartFile*.|  
|6729|Criar arquivo de texto *DiskPartFile*.|  
|6730|Executar **cmd /c DISKPART.EXE /s *DiskPartFile* >> *LogPath*\ZTIMarkActive_diskpart.log 2>&1**|  
|6731|Localizar bcdboot.exe.|  
|6732|Conectar ao provedor do Microsoft TPM.|  
|6733|Obter uma instância do TPM na classe do provedor.|  
|6734|Obter instância do TPM.|  
|6735|Verificar se o TPM está habilitado.|  
|6736|Verificar se o TPM está ativado.|  
|6737|Verificar se o TPM está atribuído.|  
|6738|Verificar se a propriedade do TPM é permitida.|  
|6739|Verificar se o TPM está habilitado.|  
|6740|Verificar se o TPM está ativado.|  
|6741|Verificar se o TPM está atribuído e se a propriedade é permitida.|  
|6741|Senha do proprietário do TPM definida|  
|6742|P@ssword do proprietário do TPM definida como **AdminP@ssword**.|  
|6743|Definir P@ssword do proprietário do TPM para o valor.|  
|6744|Verificar se o TPM está habilitado.|  
|6745|Verificar o proprietário do TPM.|  
|6746|Verificar um par de chaves de endosso.|  
|6747|Verificar se o TPM está ativado.|  
|6748|Verificar se a propriedade do TPM é permitida.|  
|6749|Converter o proprietário p@ssword para a autorização do proprietário.|  
|6750|Criar um par de chaves de endosso.|  
|6751|Alterar a autorização do proprietário.|  
|6752|Executar **Cmd**.|  
|6753|Validar TPM.|  
|6754|Obter instância de BDE.|  
|6755|Protege chave com o TPM.|  
|6756|Verificar se há mídias removíveis para configurar. **ProtectKeyWithTpmAndStartupKey**.|  
|6757|Proteger a chave com o TPM e a chave de inicialização.|  
|6758|Procurar o PIN do BDE.|  
|6759|Protege chave com o TPM e o PIN.|  
|6760|Localizar a mídia removível para **BDEKeyLocation**.|  
|6761|Proteger com chave externa.|  
|6762|P@ssword de recuperação sendo salva no *PasswordFile*.|  
|6764|Configure a política do BitLocker.|  
|7000|Não é possível localizar o ZTIConfigure.xml. Anulando.|  
|7001|Procurando AnswerFile autônomo.|  
|7100|ERRO: este script deve ser executado somente no sistema operacional completo.|  
|7101|ERRO: não há valores fornecidos suficientes para gerar o arquivo de resposta DCPromo.|  
|7102|ERRO: propriedades obrigatórias para criar um novo DC de réplica não foram especificadas.|  
|7103|ERRO: propriedades obrigatórias para criar um novo domínio filho não foram especificadas.|  
|7104|ERRO: propriedades obrigatórias para criar uma floresta não foram especificadas.|  
|7105|ERRO: propriedades obrigatórias para criar uma floresta não foram especificadas.|  
|7200|Não é possível configurar o servidor DHCP porque o serviço não está instalado.|  
|7201|Não é possível ler os detalhes do escopo. `GetScopeDetails()` falhou.|  
|7202|Não há valores especificados suficientes para a criação de escopo.|  
|7203|Não há valores fornecidos suficientes para definir o intervalo de IP para este escopo.|  
|7204|Nenhum valor especificado para o intervalo de exclusão de escopo.|  
|7300|Não é possível emitir comandos de DNS.|  
|7700|Não é um cenário do Novo Computador, partição de disco existente.|  
|7701|O disco não é grande o suficiente para o Sistema e partições BDE, necessário = 1,5 GB.|  
|7702|O disco não é grande o suficiente para o Sistema e partições WinRE, necessário = 10 GB.|  
|7703|DeployRoot está no disco nº *DiskIndex*. Executando um cenário de OEM: ignorar.|  
|7704|Executando um cenário de OEM: ignorar.|  
|7704|As partições estendidas e lógicas não são permitidas com o BitLocker.|  
|7712|Verifique se a Unidade/*Unidade do volume* está presente. Formato.|  
|7900|Findfile: Microsoft.BDD.PnpEnum.exe.|  
|7901|**AllDrivers.Exists("*GUID*").**|  
|7904|**AllDrivers.Exists("*GUID*").**|  
|9200|Findfile(PkgMgr.exe).|  
|9601|ERRO: a tarefa de restauração de estado ZTITatoo deve estar em execução no sistema operacional completo. Anulando.|  
|9701|Código de retorno diferente de zero da estimativa do USMT, rc = *Error*.|  
|9702|Não é possível realizar a captura de estado do usuário, espaço local insuficiente e nenhum caminho de rede (UDShare, UDDir) especificado.|  
|9703|Código de retorno diferente de zero da captura do USMT, rc = *Error*.|  
|9704|Nenhuma opção de linha de comando válida foi especificada.|  
|9801|ERRO: tentando implantar um sistema operacional cliente para um computador executando um sistema operacional de servidor.|  
|9802|ERRO: tentando implantar um sistema operacional de servidor para um computador executando um sistema operacional cliente.|  
|9803|Erro: o computador não tem autorização para atualizar (OSInstall=*OSInstall*). Anulando.|  
|9804|Erro: *Memory* MB de memória é insuficiente. É necessário pelo menos *Memory* MB de memória.|  
|9805|Erro: a velocidade do processador de *ProcessorSpeed* MHz é insuficiente.  É necessário um processador de pelo menos *ProcessorSpeed* MHz.|  
|9806|ERRO: espaço insuficiente disponível na *Unit*. São necessários *Size* MB adicionais.|  
|9807|ERRO: espaço insuficiente disponível na *Unit*. São necessários *Size* MB adicionais.|  
|9901|O script ZTIWindowsUpdate não deve ser executado no Windows PE.|  
|9902|ZTIWindowsUpdate foi executado e falhou muitas vezes. Contagem = *Count*.|  
|9903|Problema inesperado ao instalar o Windows Update Agent atualizado, rc = *Error*.|  
|9904|Falha ao criar o objeto: **Microsoft.Update.Session**.|  
|9905|Falha ao criar o objeto: **Microsoft.Update.UpdateColl**.|  
|9906|O arquivo crítico *File* não foi encontrado. Anulando.|  
|10000|Criar objeto: **Set oLTICleanup = New LTICleanup**.|  
|10201|Não é possível Ingressar no Domínio *Domain*. Parar instalação.|  
|10203|FindFile(LTISuspend.wsf).|  
|10204|Executar o programa *LTISuspend*.|  
|41024|Executar o ImageX.|  
|52012|Todos os parâmetros do assistente não estão definidos.|  

 A Listagem 1 fornece um trecho de um arquivo de log que ilustra como localizar o código de erro. Nesse trecho, o código de erro relatado é 5001.  

 **Listagem  1. Trecho de um arquivo SMSTS.log que contém o código de erro 5001**  

```  
.  
.  
.  
The operating system installation failed. Please contact your system administrator for assistance.  

The action "Zero Touch Installation - Validation" failed with exit code 5001  
.  
.  
.  

```  

### <a name="converting-error-codes"></a>Convertendo códigos de erro  
 Muitos códigos de erro apresentados nos arquivos de log parecerem complexos e difíceis de correlacionar com uma condição de erro real. No entanto, o processo a seguir demonstra como converter um código de erro e obter informações importantes que podem ajudar na resolução do problema.  

 **Problema**: ocorreu uma falha na captura de uma imagem como código de erro 0x80070040.  

 **Solução possível 1**: o código de erro apresentado está em formato hexadecimal que você precisa converter em formato decimal. Para fazer isso, você precisa de uma calculadora científica e a calculadora incluída com sistemas operacionais Windows é adequada para essa tarefa.  

 **Para converter um código de erro**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Acessórios**e clique em **Calculadora**.  

2.  No menu **Exibir**, clique em **Científica**.  

3.  Selecione **Hexa** e insira os quatro últimos dígitos do código, neste caso, **0040**, como mostrado na Figura 1.  

     ![TroubleshootingReference1](media/TroubleshootingReference1.jpg "TroubleshootingReference1")  
Figura 1. Conversão de erro  

     **Figura 1. Conversão de erro**  

     Observe que os zeros à esquerda não são exibidos enquanto a calculadora está no modo Hexadecimal.  

4.  Selecione **Dec**.  

     O valor hexadecimal *40* é convertido em um valor decimal de *64*.  

5.  Abra uma janela de Prompt de Comando, digite **NET HELPMSG 64** e pressione ENTER.  

     O comando **NET HELPMSG** converte o código de erro numérico em texto significativo. No caso do código de erro fornecido aqui, ele converte em “O nome de rede especificado não está mais disponível”.  

 Essa informação indica que pode haver um problema de rede no computador de destino ou entre o computador de destino e o servidor em que o compartilhamento de implantação reside. Esses problemas podem incluir os drivers de rede não estarem sendo instalados corretamente ou uma incompatibilidade entre a velocidade e as configurações duplex.  

 **Solução possível 2:** use o utilitário de Pesquisa de Código de Erro do Microsoft Exchange Server. Esse utilitário de linha de comando é útil na assistência com a conversão de código de erro. Ele está disponível para download no [Centro de Download da Microsoft](http://www.microsoft.com/download/details.aspx?id=985).  

### <a name="review-of-sample-logs"></a>Revisão dos logs de exemplo  
 O MDT cria arquivos de log que você pode usar para solucionar problemas no processo de implantação do MDT. As seções a seguir fornecem exemplos de como usar os arquivos de log do MDT para solucionar o problema de implantação:  

-   Problemas relacionados a falhas ao acessar o banco de dados do MDT (BD do MDT), conforme descrito em [Falha ao acessar o banco de dados](#FailuretoAccesstheDatabase)  

####  <a name="FailuretoAccesstheDatabase"></a> Falha ao acessar o banco de dados  
 **Problema:** ocorre um erro ao executar uma implantação que usou um arquivo CustomSettings.ini contendo várias seções e especificando, com a propriedade **Prioridade**, a prioridade de cada seção para ser processada. O BDD.log contém as seguintes mensagens de erro:  

-   ```  
    ERROR - Opening Record Set (Error Number = -2147217911) (Error Description: The SELECT permission was denied on the object 'ComputerAdministrators', database 'AdminDB', schema 'dbo'.)  
    ```  

-   ```  
    ADO error: The SELECT permission was denied on the object 'ComputerAdministrators', database 'AdminDB', schema 'dbo'. (Error #-2147217911; Source: Microsoft OLE DB Provider for SQL Server; SQL State: 42000; NativeError: 229  
    ```  

-   ```  
    ERROR - Unhandled error returned by ZTIGather: Object required (424)  
    ```  

> [!NOTE]
>  Para maior clareza, o conteúdo do arquivo de log acima foi representado como ele aparece enquanto é visualizado usando o programa Trace32.  

 **Solução possível:** o problema, conforme indicado na primeira linha do exemplo de arquivo de log, é que a permissão para acessar o banco de dados foi negada. Portanto, o script não pode estabelecer uma conexão segura com o banco de dados, possivelmente porque uma ID de usuário e a senha não estavam disponíveis. Como resultado, foi realizada a tentativa de acessar o banco de dados usando a conta do computador. A maneira mais fácil de contornar esse problema é conceder a todos acesso de leitura ao banco de dados.  

## <a name="troubleshooting"></a>Solução de problemas  
 Antes de embarcar em processos de solução de problemas detalhados, examine os seguintes itens e certifique-se de que todos os requisitos associados foram atendidos:  

-   Se todos os pré-requisitos de software e hardware não forem atendidos, poderão surgir problemas de instalação como resultado.  

### <a name="application-installation"></a>Instalação de aplicativo  
 Examine os problemas e soluções para problemas de instalação de aplicativo:  

-   Os arquivos de origem de instalação bloqueados por motivos de segurança são descritos em [Executáveis bloqueados](#BlockedExecutables)  

-   Perda de conectividade de rede, conforme descrito em [Conexões de rede perdidas](#LostNetworkConnections)  

-   Erro de instalação 30029 ao instalar o 2007 Microsoft Office system ou arquivos relacionados, conforme descrito em [O 2007 Microsoft Office system](#MicrosoftOfficeSystem)  

####  <a name="BlockedExecutables"></a> Executáveis bloqueados  
 **Problema:** se os arquivos de origem de instalação forem baixados da Internet, provavelmente eles serão marcados com um ou mais fluxos de dados do sistema de arquivos NTFS. Para obter mais informações sobre fluxos de dados NTFS, consulte [Fluxos de arquivos](http://msdn2.microsoft.com/library/aa364404\(VS.85\).aspx). A existência de fluxos de dados do sistema de arquivos NTFS pode fazer com que um prompt **Abrir Arquivo – Aviso de Segurança** seja exibido. A instalação não continuará até que você clique em **Executar** no prompt.  

 A Figura 2 mostra e você pode exibir fluxos de dados do sistema de arquivos NTFS usando o comando **Mais** e o [utilitário Streams](http://technet.microsoft.com/sysinternals/bb897440.aspx).  

 ![TroubleshootingReference2](media/TroubleshootingReference2.jpg "TroubleshootingReference2")  
Figura 2. Fluxos de dados NTFS  

 **Figura 2. Fluxos de dados NTFS**  

 **Solução possível 1:** clique com o botão direito do mouse no arquivo de origem de instalação e clicar em **Propriedades**. Clique em **Desbloquear** e, em seguida, em **OK** para remover os fluxos de dados do sistema de arquivos NTFS do arquivo. Repita esse processo para cada arquivo de origem de instalação que está bloqueado pela existência de um ou mais fluxos de dados do sistema de arquivos NTFS.  

 **Solução possível 2:** use o utilitário Streams, como REF \_Ref308173670 \\h a Figura 2 mostra, para remover os fluxos de dados do sistema de arquivos NTFS do arquivo de origem de instalação. O utilitário Streams pode remover fluxos de dados do sistema de arquivos NTFS de um ou mais arquivos ou pastas de uma vez.  

####  <a name="LostNetworkConnections"></a> Conexões de rede perdidas  
 **Problema:** uma instalação pode falhar se ela instala drivers de dispositivo ou altera as configurações de rede e dispositivo. Essas alterações podem resultar em um lapso na conectividade de rede que faz com que a instalação falhe.  

 **Solução possível:** implemente o script ZTICacheUtil.vbs para permitir o download e a execução para a instalação. Esse script foi desenvolvido para ajustar o anúncio para habilitar o download e a execução. O download usará o BITS \(Serviço de Transferência Inteligente em Segundo Plano\) se o ponto de distribuição do Configuration Manager for habilitado para BITS e Criação e Controle de Versão Distribuídos Baseado em Web. Ao mesmo tempo, ele modifica o Configuration Manager para executar o script ZTICache.vbs primeiro, o que garante que o programa não se exclua durante o processo de implantação.  

####  <a name="MicrosoftOfficeSystem"></a> O 2007 Microsoft Office system  
 **Problema:** durante a implantação do 2007 Office system e a inclusão do arquivo \(MSP\) de patch do Windows Installer, a instalação poderá falhar com o código de erro 30029.  

 A investigação adicional no ZTIApplications.log mostra as seguintes mensagens:  

-   ```  
    About to run command: \\Server\Deployment$\Tools\X86\bddrun.exe \\Server\Share\Microsoft\Office\2007\Professional\setup.exe /adminfile \\Server\Share\Microsoft\Office\2007\Professional\file.msp  
    ```  

-   ```  
    ZTI Heartbeat: command has been running for 12 minutes (process ID 1600) Return code from command = 30029  
    ```  

-   ```  
    Application Microsoft Office 2007 Professional returned an unexpected return code: 30029  
    ```  

 **Solução possível 1:** realoque o arquivo MSP para o diretório Atualizações e, em seguida, execute setup.exe sem especificar a opção **\/adminfile**. Para obter mais informações sobre como implantar as atualizações durante a instalação, consulte [Implantando o 2007 Office system](http://technet.microsoft.com/library/cc303395\(v=Office.12\).aspx).  

 **Solução possível 2:** verifique se arquivo MSP não está com a caixa de seleção **Suprimir modal** marcada. Para obter mais informações sobre essa configuração, consulte [Visão geral da implantação do 2007 Office system](http://technet.microsoft.com/library/bb490141.aspx).  

### <a name="autologon"></a>Logon automático  
 Examine os problemas e soluções para problemas de logon automático:  

-   Interrupção dos processos de implantação do LTI e do ZTI \(Zero Touch Installation\) por causa das faixas de segurança do logon conforme descrito em [Faixas de segurança de logon](#LogonSecutiryBanners)  

-   Interrupção da implantação de processos de implantação de LTI e ZTI por causa de prompts para as credenciais do usuário, conforme descrito em [Solicitação das credenciais do usuário](#PromtedforUserCredentials)  

####  <a name="LogonSecutiryBanners"></a> Faixas de segurança de logon  
 **Problema:** as sequências de tarefas do MDT são processadas durante uma sessão de usuário interativo, o que exige que o computador de destino tenha permissão para fazer logon automaticamente usando a conta administrativa especificada. Se um GPO \(Objeto de Política de Grupo\) em vigor impuser uma faixa de segurança de logon, esse logon automático não poderá continuar, porque a faixa de segurança interromperá o processo de logon enquanto espera o usuário aceitar a política determinada.  

 **Solução possível:** certifique-se de que o GPO esteja aplicado às OUs \(unidades organizacionais\) específicas e não incluído no GPO do domínio padrão. Quando você adicionar computadores ao domínio, especifique que eles sejam adicionados a uma OU não afetada por um GPO que impõe uma faixa de segurança de logon. No Editor de Sequência de Tarefas, inclua como uma das últimas etapas da sequência de tarefas um script que realoca a conta de computador para a OU desejada.  

> [!NOTE]
>  Se você estiver reutilizando contas do AD DS \(Active Directory® Domain Services\) existentes, certifique-se, antes de implantar no computador de destino, de ter realocado a conta do computador de destino para uma OU que não é afetada pelo GPO que impõe a faixa de logon de segurança.  

####  <a name="PromtedforUserCredentials"></a> Solicitação das credenciais do usuário  
 **Problema:** você criou uma imagem de um computador que ingressou no domínio. Ao implantar a nova imagem em um computador de destino, o processo de implantação para, pois o logon automático não ocorre e é solicitado que o usuário insira as credenciais apropriadas. O processo de implantação é retomado quando as credenciais são fornecidas e o usuário faz logon.  

 **Solução possível:** durante a captura de imagens, o computador de origem não deve estar ingressado em um domínio. Se o computador foi ingressado em um domínio, ingresse o computador em um grupo de trabalho, capture a imagem novamente e tente realizar a implantação em um computador de destino para determinar se o problema foi resolvido.  

### <a name="bios"></a>BIOS  
 **Problema:** durante a implantação em um computador de destino que está equipado com a tecnologia Intel vPro, a implantação pode terminar com um erro de parada. Mesmo que todos os drivers atualizados tenham sido incluídos como drivers não incluídos no Workbench de Implantação, o computador de destino não é iniciado.  

 Solução possível: examine as configurações no BIOS \(sistema BIOS\) do computador de destino para determinar se o modo Serial Advanced Technology Attachment padrão está configurado como AHCI \(Interface do Controlador de Host Avançada\). Infelizmente, determinados sistemas operacionais Windows não dão suporte à AHCI por padrão.  

### <a name="database-problems"></a>Problemas de banco de dados  
 Examine os problemas e soluções relacionados a banco de dados:  

-   Erros gerados como resultado de firewalls configurados incorretamente no servidor de banco de dados, conforme descrito em [Solicitações de navegador do SQL Server bloqueadas](#BlockedSQLServerBrowserRequests)  

-   Erros gerados como resultado de conexões com o servidor de banco de dados interrompidas, conforme descrito em [Conexões de pipe nomeado](#NamedPipeConnections)  

####  <a name="BlockedSQLServerBrowserRequests"></a> Solicitações de navegador do SQL Server bloqueadas  
 **Problema:** durante o processo de implantação do MDT, é possível recuperar informações de bancos de dados Microsoft SQL Server®. No entanto, podem ser gerados erros relacionados a um firewall configurado incorretamente no servidor de banco de dados.  

 **Solução possível:** o Firewall do Windows no Windows Server ajuda a impedir o acesso não autorizado aos recursos do computador. No entanto, se o firewall estiver configurado incorretamente, as tentativas de se conectar a uma instância do SQL Server poderão ser bloqueadas. Para acessar uma instância do SQL Server que está por trás do firewall, configure o firewall no computador que está executando o SQL Server. Para obter mais informações sobre como configurar portas de firewall para SQL Server, consulte o artigo do Suporte da Microsoft [Como abrir a porta de firewall para o SQL Server no Windows Server 2008](http://support.microsoft.com/kb/968872)  

####  <a name="NamedPipeConnections"></a> Conexões de pipe nomeado  
 **Problema:** durante o processo de implantação do MDT, é possível recuperar informações de bancos de dados SQL Server. No entanto, podem ser gerados erros relacionados às conexões do SQL Server interrompidas. Elas podem ser causadas por não habilitar conexões de pipe nomeado no Microsoft SQL Server.  

 **Solução possível:** para resolver esses problemas, habilite os pipes nomeados no SQL Server. Além disso, especifique a propriedade **SQLShare**, que é necessária ao fazer uma conexão com um banco de dados externo usando pipes nomeados. Ao se conectar usando pipes nomeados, use a segurança integrada para fazer a conexão com o banco de dados. No caso de implantações de LTI, a conta de usuário especificada faz a conexão com o banco de dados. Para implantações de ZTI que usam o Configuration Manager, a conta de acesso de rede se conecta ao banco de dados. Como o Windows PE não tem nenhum contexto de segurança por padrão, você deve fazer uma conexão de rede para o servidor de banco de dados para estabelecer um contexto de segurança para o usuário que fará a conexão.  

 O compartilhamento de rede que a propriedade **SQLShare** especifica fornece um meio de se conectar ao servidor para obter o contexto de segurança apropriado. Você deve ter acesso de leitura ao compartilhamento. Quando a conexão é feita, você pode então estabelecer a conexão de pipe nomeado para o banco de dados. A propriedade **SQLShare** não é necessária e não deve ser usada ao fazer uma conexão TCP\/IP para o banco de dados.  

 Habilite as conexões de pipe nomeado executando as seguintes tarefas com base na versão do SQL Server que você está usando:  

-   Habilite as conexões de pipe nomeado do SQL Server 2008 R2 conforme descrito em [Habilitar conexões de pipe nomeado no SQL Server 2008 R2](#EnableNamedPipeConnectionsinSQLServer).  

-   Habilite as conexões de pipe nomeado do SQL Server 2005 conforme descrito em [Habilitar conexões de pipe nomeado no SQL Server 2005](#EnableNamedPipeConnectionsinSQL).  

#####  <a name="EnableNamedPipeConnectionsinSQLServer"></a> Habilitar conexões de pipe nomeado no SQL Server 2008 R2  
 Para habilitar conexões de pipe nomeado no SQL Server 2008 R2, execute as seguintes etapas:  

1.  No computador executando o SQL Server 2008 R2 que hospeda o banco de dados a ser consultado, clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft SQL Server 2008 R2** e clique em **SQL Server Management Studio**.  

2.  No console **Microsoft SQL Server Management Studio**, no **Pesquisador de Objetos**, clique com o botão direito do mouse em ***sql\_server\_name*** e clique em **Propriedades**\(, em que *sql\_server\_name* é o nome do computador executando o SQL Server a ser configurado\).  

3.  A caixa de diálogo Propriedades do Servidor \- ***sql\_server\_name*** é exibida.  

4.  Na caixa de diálogo **Propriedades do Servidor** \- ***sql\_server\_name***, em **Selecionar uma página**, clique em **Conexões**.  

5.  Na página **Conexões**, certifique-se de que a caixa de seleção **Permitir conexões remotas com este servidor** esteja selecionada e clique em **OK**.  

6.  Feche o console do Microsoft SQL Server Management Studio.  

7.  No computador executando o SQL Server 2008 R2 que hospeda o banco de dados a ser consultado, clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft SQL Server 2008 R2**, aponte para **Ferramentas de Configuração** e clique em **SQL Server Configuration Manager**.  

8.  No console **SQL Server Configuration Manager**, acesse SQL Server Configuration Manager \(Local\) \/ Configuração de Rede do SQL Server Network \/ Protocolos para *instância\_sql* \(em que *instância\_sql* é o nome da instância do SQL Server a ser configurada\).  

9. No painel de detalhes, clique com o botão direito do mouse em **Pipes Nomeados** e clique em **Habilitar**.  

     A caixa de diálogo Aviso é exibida indicando que as alterações serão salvas, mas não entrarão em vigor até que o serviço seja interrompido e reiniciado.  

10. Na caixa de diálogo **Aviso**, clique em **OK**.  

11. No console **SQL Server Configuration Manager**, vá para SQL Server Configuration Manager \(Local\) \/ Serviços do SQL Server.  

12. No painel de detalhes, clique com o botão direito do mouse em **SQL Server*\(instância\_sql\)*** e clique em **Reiniciar** \(em que *instância\_sql* é nome da instância do SQL Server configurado na etapa 2\).  

     A barra de progresso do SQL Server Configuration Manager é exibida mostrando o status da reinicialização dos serviços. Depois que o serviço é reiniciado, a barra de progresso é fechada.  

13. Feche o console do SQL Server Configuration Manager.  

 Para obter informações adicionais, consulte [How to enable remote connections in SQL Server 2008](http://blogs.msdn.com/b/walzenbach/archive/2010/04/14/how-to-enable-remote-connections-in-sql-server-2008.aspx) (Como habilitar conexões remotas no SQL Server 2008).  

#####  <a name="EnableNamedPipeConnectionsinSQL"></a> Habilitar conexões de pipe nomeado no SQL Server 2005  
 Para habilitar conexões de pipe nomeado no SQL Server 2005, execute as seguintes etapas:  

1.  No computador executando o SQL Server 2005 que hospeda o banco de dados a ser consultado, clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft SQL Server 2005**, aponte para **Ferramentas de Configuração** e clique em **Configuração da Área da Superfície do SQL Server**.  

2.  Na caixa de diálogo **Configuração da Área da Superfície do SQL Server 2005**, clique em **Configuração da Área da Superfície para Serviços e Conexões**.  

3.  Na caixa de diálogo **Configuração da Área da Superfície para Serviços e Conexões – *server\_name*** \(em que *server\_name* é o nome do computador executando o SQL Server 2005\), em **Selecione um componente e configure seus serviços e conexões**, vá até MSSQLSERVER\\Mecanismo de Banco de Dados e clique em **Conexões Remotas**.  

4.  Clique em **Conexões locais e remotas**, em **Usando TCP\/IP e pipes nomeados** e, em seguida, clique em **Aplicar**.  

5.  Na caixa de diálogo **Configuração da Área da Superfície para Serviços e Conexões – *server\_name*** \(em que *server\_name* é o nome do computador executando o SQL Server 2005\), em **Selecione um componente e configure seus serviços e conexões**, vá até MSSQLSERVER\\Mecanismo de Banco de Dados e clique em **Serviço**.  

6.  Clique em **Parar**.  

     O serviço MSSQLSERVER é parado.  

7.  Clique em **Iniciar**.  

     O serviço MSSQLSERVER é iniciado.  

8.  Clique em **OK**.  

9. Feche a Configuração da Área da Superfície do SQL Server 2005.  

 Para obter informações adicionais, consulte o artigo do Suporte da Microsoft [Como configurar o SQL Server 2005 para permitir conexões remotas](http://support.microsoft.com/kb/914277)  

### <a name="deployment-scripts"></a>Scripts de implantação  
 Examine os problemas e soluções relacionados ao MDT:  

-   As credenciais do usuário são solicitadas e pode receber o erro 0x80070035, conforme descrito em [Credentials_script](#Credentials_script)  

-   A mensagem de erro "Wuredist.cab não encontrado" aparece, conforme descrito em [ZTIWindowsUpdate](#ZTIWindowsUpdate)  

####  <a name="Credentials_script"></a> Credenciais\_script  
 **Problema:** durante a última inicialização de um computador recém-implantado, é solicitado que o usuário forneça credenciais de usuário e ele pode receber o erro 0x80070035, que indica que o caminho de rede não foi encontrado.  

 **Solução possível:** certifique-se de que o arquivo WIM não inclui uma pasta MININT ou \_SMSTaskSequence. Para excluir essas pastas, primeiro use o utilitário ImageX para montar o arquivo WIM e, em seguida, exclua as pastas.  

> [!NOTE]
>  Se ocorrer um erro de Acesso Negado quando você tentar excluir as pastas do arquivo WIM, abra uma janela do prompt de comando, mude para a raiz da imagem contida no arquivo WIM e execute **RD MININT** e **RD \_SMSTaskSequence**.  

####  <a name="ZTIWindowsUpdate"></a> ZTIWindowsUpdate  
 **Problema:** se você usar o script ZTIWindowsUpdate.wsf para aplicar atualizações de software durante a implantação, observe que esse script pode se comunicar diretamente com o site Microsoft Update para baixar e instalar os binários necessários do Windows Update Agent, verificar se há atualizações de software aplicáveis, baixar os binários das atualizações de software aplicáveis e, em seguida, instalar os binários baixados. Esse processo exige que sua infraestrutura de rede esteja configurada para permitir que o computador de destino acesse o site Microsoft Update.  

 Se o compartilhamento de implantação não contém os arquivos de instalação do Windows Update Agent e o computador de destino não tem acesso apropriado à Internet, o erro "wuredist.cab não encontrado" é relatado nos arquivos ZTIWindowsUpdate.log e BDD.log.  

 **Solução possível:** siga as etapas descritas na seção "ZTIWindowsUpdate.wsf" no documento do MDT *Toolkit Reference* (Referência do Toolkit).  

### <a name="deployment-shares"></a>Compartilhamentos de implantação  
 Examine os problemas e soluções relacionados ao compartilhamento de implantação:  

-   A atualização de arquivos WIM falha ao atualizar um compartilhamento de implantação conforme descrito em [Falha ao atualizar arquivos WIM](#FailuretoUpdateWIMFiles).  

####  <a name="FailuretoUpdateWIMFiles"></a> Falha ao atualizar arquivos WIM  
 Em um ambiente "simples":  

-   O MDT geralmente pega o WIMGAPI.DLL de C:\\Windows\\system32 \(sempre no caminho\). A versão deste WIMGAPI.DLL deve corresponder ao \(build\) da versão do sistema operacional.  

-   Em um sistema operacional de 64 bits, o MDT sempre usa o arquivo WIMGAPI.DLL x64, somente esse arquivo deve estar no CAMINHO do sistema. Em um sistema operacional de 32 bits, o MDT sempre usa o arquivo WIMGAPI.DLL x86, somente esse arquivo deve estar no CAMINHO do sistema. \(Outros produtos, como o Configuration Manager, usam a versão de 32 bits do WIMGAPI.DLL, mesmo em um sistema operacional de 64 bits, mas eles gerenciam e instalam essa versão.\)  

 **Problema:** ao tentar atualizar um compartilhamento de implantação, o usuário será informado de que a montagem de um ou mais arquivos .wim não teve êxito.  

 **Solução possível:** abra uma janela do prompt de comando e execute **where WIMGAPI.DLL**. Para a primeira entrada na lista \(o primeiro local encontrado ao pesquisar o caminho\), certifique-se de que a propriedade **Version** corresponda ao build do ADK do Windows \(Kit de Avaliação e Implantação do Windows\) que está instalado. Além disso, certifique-se de que a propriedade corresponda ao número de build do sistema operacional.  

### <a name="the-windows-deployment-wizard"></a>O Assistente Implantação do Windows  
 Examine os problemas e soluções relacionados ao Assistente de Implantação do Windows:  

-   As páginas do Assistente de Implantação do Windows são exibidas mesmo quando o LTI está configurado para ignorar as páginas do assistente conforme descrito em [As páginas do Assistente não são ignoradas](#WizardPagesareNotSkipped).  

####  <a name="WizardPagesareNotSkipped"></a> As páginas do Assistente não são ignoradas  
 **Problema:** uma página do assistente é exibida mesmo que o arquivo de banco de dados do MDT ou CustomSettings.ini especifique que o assistente deve ser ignorado.  

 **Solução possível:** para ignorar corretamente uma página do assistente, inclua todas as propriedades que devem ser especificadas nessa página do assistente quando apropriado no arquivo de banco de dados do MDT ou CustomSettings.ini juntamente com os valores apropriados. Se uma propriedade estiver configurada incorretamente para uma página do assistente ignorada, essa página será exibida. Para obter mais informações sobre quais propriedades são necessárias para garantir que uma página do assistente seja ignorada, consulte a seção “Providing Properties for Skipped Deployment Wizard Pages” (Fornecendo propriedades para páginas do assistente de implantação ignoradas) no documento do MDT *Toolkit Reference* (Referência do Toolkit).  

### <a name="disks-and-partitioning"></a>Discos e particionamento  
 Examine os problemas e soluções de particionamento de disco:  

-   Problemas de Criptografia de Unidade de Disco BitLocker® conforme descrito em [Criptografia de Unidade de Disco BitLocker](#BitLockerDriveEncryption)  

-   Erros de particionamento de disco conforme descrito em Erros de particionamento de disco  

-   Falhas durante cenários de implantação de Atualizar computador causadas por discos lógicos ou dinâmicos conforme descrito em [Suporte para discos lógicos e dinâmicos](#SupportforLoogicalandDynamicDisks)  

####  <a name="BitLockerDriveEncryption"></a> Criptografia de Unidade de Disco BitLocker  
 Implantar o BitLocker exige uma configuração específica para uma implantação adequada. Os seguintes possíveis problemas podem estar relacionados à configuração do computador de destino:  

-   Em implantações de ZTI e de UDI, o script ZTIBde.wsf falha com o erro “Não foi possível abrir a chave do Registro ‘HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName’ para leitura”, conforme descrito em [O script ZTIBde.wsf falha com o erro “Não foi possível abrir a chave do Registro ‘HKEY_CURRENT_USER\Control Panel\International\LocaleName’ para leitura”](#ZTIBde.wsf).  

-   Dispositivos USB, unidades de CD, unidades de DVD ou outros dispositivos de mídia removível no computador de destino que são exibidos como várias letras de unidade, conforme descrito em [Dispositivos aparecem como várias letras de unidade](#DevicesAppearasMultipleDriveLetters)  

-   Redução da unidade C no computador de destino para fornecer espaço em disco não alocado suficiente conforme descrito em [Problemas com a redução de discos](#ProblemswithShrinkingDisks)  

#####  <a name="ZTIBde.wsf"></a> O script ZTIBde.wsf falha com o erro “Não foi possível abrir a chave do Registro ‘HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName’ para leitura”  
 **Problema:** durante a tentativa de implantar o BitLocker no computador de destino em ZTI ou UDI, o script ZTIBde.wsf falha com o erro “Não foi possível abrir a chave do Registro ‘HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName’ para leitura”.  

 **Solução possível:** especifique a localidade na propriedade **UILanguage**. No ZTI e UDI, o script ZTIBde.wsf é executado no controle do sistema, para que um perfil de usuário completo não seja carregado. Quando o script ZTIBde.wsf tenta ler as informações de localidade, elas não estão no Registro, porque o \(perfil de usuário\) do Registro não foi totalmente carregado. Como alternativa, especifique a localidade na propriedade **UILanguage**.  

#####  <a name="DevicesAppearasMultipleDriveLetters"></a> Dispositivos aparecem como várias letras de unidade  
 **Problema:** alguns dispositivos podem aparecer como várias letras de unidade lógica, dependendo de como eles estão particionados. Em alguns casos, eles podem emular uma unidade de disquete de 1,44\-megabytes \(MB\) e uma unidade de armazenamento de memória. Portanto, o Windows pode atribuir as mesmas letras de unidade do dispositivo A e B para a emulação de disquete e F para a unidade de armazenamento de memória. Por padrão, os scripts do MDT usam a primeira letra da unidade \(neste exemplo, A\).  

 **Solução possível:** substitua a configuração padrão na página **Especificar os detalhes de recuperação do BitLocker** no Assistente de Implantação do Windows. A página de resumo do Assistente de Implantação do Windows exibe um aviso para informar ao usuário qual letra da unidade foi selecionada para armazenar informações de recuperação do BitLocker. Além disso, os arquivos BDD.log e ZTIDE.log registram os dispositivos de mídia removível detectados e qual dispositivo foi selecionado para armazenar as informações de recuperação do BitLocker.  

#####  <a name="ProblemswithShrinkingDisks"></a> Problemas com a redução de discos  
 **Problema:** há espaço em disco não alocado insuficiente no computador de destino para habilitar o BitLocker. Para implantar o BitLocker em um computador de destino, são necessários pelo menos 2 gigabytes \(GB\) de espaço em disco não alocado para criar o volume do sistema. O *volume do sistema* é o volume que contém os arquivos específicos de hardware necessários para carregar o Windows depois que o BIOS inicializou o computador.  

 **Solução possível 1:** em computadores existentes, use a ferramenta Diskpart para reduzir a unidade C para que o volume do sistema possa ser criado. Em alguns casos, no entanto, a ferramenta Diskpart pode não conseguir reduzir a unidade C o suficiente para fornecer 2 GB de espaço em disco não alocado, possivelmente devido ao espaço em disco fragmentado na unidade C.  

 Uma solução possível para esse problema é desfragmentar a unidade C. Para fazer isso, execute as seguintes etapas:  

1.  Execute o comando **shrink querymax** do Diskpart para identificar a quantidade máxima de espaço em disco que pode ser desalocado.  

2.  Se o valor retornado na etapa 1 for menor que 2 GB, limpe todos os arquivos desnecessários da unidade C e desfragmente-a em seguida.  

3.  Execute o comando **shrink querymax** novamente para verificar se é possível desalocar mais de 2 GB de espaço em disco.  

4.  Se o valor retornado na etapa 3 é ainda for menor que 2 GB, execute uma das seguintes tarefas:  

    -   Desfragmentar a unidade C várias vezes para garantir que ela esteja completamente otimizada.  

    -   Fazer backup dos dados na unidade C, excluir a partição existente, criar uma nova partição e, em seguida, restaurar os dados para a nova partição.  

 **Solução possível 2:** o script ZTIBDE.wsf executa a Ferramenta de Preparação de Disco \(bdehdcfg.exe\) e configura o tamanho da partição do volume do sistema para 2 GB por padrão. Você pode personalizar o script ZTIBDE.wsf para alterar o padrão, se necessário. No entanto, não é recomendável modificar os scripts do MDT.  

####  <a name="SupportforLoogicalandDynamicDisks"></a> Suporte para discos dinâmicos e lógicos  
 **Problema:** ao executar um cenário de implantação de atualização de computador, o processo de implantação pode falhar ao implantar em um computador de destino que está usando unidades lógicas ou discos dinâmicos.  

 **Solução possível:** o MDT não dá suporte para a implantação de sistemas operacionais em unidades lógicas ou discos dinâmicos.  

### <a name="domain-join"></a>Junção de Domínios  
 **Problema:** durante a implantação, você deve usar o Assistente de Implantação do Windows para fornecer todas as informações necessárias para o computador de destino, incluindo credenciais, informações de ingresso no domínio e configuração de IP estático. Quando a instalação é concluída, você pode ver que o sistema não ingressou no domínio e ainda está em um grupo de trabalho.  

 **Solução possível:** uma implantação de LTI do MDT configura as informações de IP estático depois que o sistema operacional está em execução. Se o computador de destino estiver localizado em um segmento de rede que não tem o protocolo DHCP, um ingresso no domínio automatizado especificado em Unattend.xml falhará quando não houver nenhum DHCP presente.  

 Configure o Unattend.xml para ingressar em um grupo de trabalho. Em seguida, use a etapa da sequência tarefa **Recuperar do domínio** interna para adicionar uma etapa na sequência de tarefas para ingressar no domínio após o IP estático ter sido aplicado.  

### <a name="driver-installation"></a>Instalação do driver  
 Para garantir a melhor experiência do usuário possível, a instalação de dispositivos de hardware e drivers de software deve ser executada o mais perfeitamente possível, como pouca ou nenhuma intervenção do usuário. A Microsoft fornece ferramentas e diretrizes para ajudar a criar pacotes de instalação que atendem a essa meta. Para obter informações gerais sobre a instalação do driver, consulte [dispositivo e a instalação do driver](http://www.microsoft.com/whdc/driver/install/default.mspx).  

 Examine os problemas e soluções relacionados à instalação do driver de dispositivo:  

-   Problemas que ocorrem ao usar drivers de armazenamento em massa $OEM$ com o MDT conforme descrito em Combinar drivers de armazenamento em massa $OEM$ com a lógica de armazenamento em massa do MDT  

-   Solucionando problemas de instalação de driver de dispositivo usando o SetupAPI.log conforme descrito em [Solucionar problemas de instalação de dispositivo com o SetupAPI.log](#TroubleshootDeviceInstallationwithSetupAPI.log)  

####  <a name="TroubleshootDeviceInstallationwithSetupAPI.log"></a> Solucionar problemas de instalação de dispositivo com o SetupAPI.log  
 O whitepaper [Solucionar problemas de instalação de dispositivo com o arquivo de log SetupAPI](http://msdn.microsoft.com/windows/hardware/gg463393.aspx) fornece informações sobre a depuração da instalação de dispositivo do Windows. Especificamente, o documento fornece diretrizes para desenvolvedores de driver e testadores interpretarem o arquivo de log SetupAPI.  

 Um dos arquivos de log mais úteis para fins de depuração é o arquivo SetupAPI.log. Esse arquivo de texto sem formatação mantém as informações que o SetupAPI registra sobre a instalação do dispositivo, a instalação do service pack e a instalação da atualização. Especificamente, o arquivo mantém um registro de alterações de dispositivo e driver, bem como alterações importantes no sistema começando na instalação mais recente do Windows. Este documento se concentra em usar o arquivo de log SetupAPI para solucionar problemas de instalação do dispositivo, ele não descreve as seções do arquivo de log que estão associadas às instalações do service pack e da atualização.  

### <a name="new-computer-deployments"></a>Novas implantações de computador  
 Examine os problemas e soluções para cenários de implantação de novo computador:  

-   Problemas ao iniciar o processo de implantação usando a inicialização PXE \(Pre\-Boot Execution Environment\), conforme descrito em [Inicialização PXE](#PXEBoot)  

####  <a name="PXEBoot"></a> Inicialização PXE  
 Em suma, o protocolo PXE funciona da seguinte maneira: o computador cliente inicia o protocolo ao transmitir um pacote de descoberta DHCP que contém uma extensão que identifica a solicitação como proveniente de um computador cliente que implementa o protocolo PXE. Supondo que um servidor de inicialização implementando esse protocolo estendido esteja disponível, o servidor de inicialização envia uma oferta que contém o endereço IP do servidor que atenderá ao cliente. O cliente usa o protocolo TFTP para baixar o arquivo executável do servidor de inicialização. Por fim, o computador cliente executa o programa de inicialização baixado.  

 A fase inicial desse protocolo pega carona em um subconjunto de mensagens DHCP para habilitar o cliente a descobrir um servidor de inicialização \(ou seja, um servidor que distribui arquivos executáveis para a configuração do novo computador\). O computador cliente pode usar a oportunidade para obter um endereço IP \(que é o comportamento esperado\), mas não é necessário para fazer isso.  

 A segunda fase desse protocolo ocorre entre o computador cliente e um servidor de inicialização e usa o formato de mensagem DHCP como um formato conveniente para comunicação. Salvo indicação em contrário, essa segunda fase não está relacionada aos serviços DHCP padrão. As páginas a seguir descrevem o processo passo a passo durante a inicialização do computador cliente do PXE.  

 Para obter mais informações sobre como solucionar problemas relacionados à inicialização PXE nos Serviços de Implantação do Windows em execução no modo Misto ou Herdado, consulte o artigo do Suporte da Microsoft [Descrição da interação de PXE entre o cliente PXE, DHCP e servidor RIS](http://support.microsoft.com/kb/244036).  

 Examine as seguintes soluções para problemas de inicialização PXE:  

-   Desabilitar o registro em log do Windows PE para o SetupAPI.log conforme descrito em [Desabilitar o registro em log do Windows PE nos Serviços de Implantação do Windows](#DisableWindowsPELogginginWindowsDeploymentServices).  

-   Verifique se o DHCP está configurado corretamente conforme descrito em [Garantir a configuração correta do DHCP](#EnsuretheProperDHCPConfiguration).  

-   Melhorar os tempos de resposta para atribuir endereços IP para os computadores cliente PXE conforme descrito em [Melhorar o tempo de resposta de atribuição de endereço IP de PXE](#ImprovePXEIPAddressAssignmentResponseTime).  

#####  <a name="DisableWindowsPELogginginWindowsDeploymentServices"></a> Desabilitar o registro em log do Windows PE nos Serviços de Implantação do Windows  
 O primeiro procedimento recomendado é certificar-se de que o registro em log no setupapi.log foi desabilitado.  

#####  <a name="EnsuretheProperDHCPConfiguration"></a> Garantir a configuração correta do DHCP  
 Dependendo dos modelos de roteador em uso, a configuração de roteador específica do encaminhamento de difusão DHCP poderá ser compatível com uma sub-rede \(ou interface de roteador\) ou um host específico. Se os servidores DHCP e o computador executando Serviços de Implantação do Windows forem computadores separados, certifique-se de que os roteadores que encaminham difusões DHCP sejam criados para que os servidores DHCP e de Serviços de Implantação do Windows recebam difusões do cliente, caso contrário, o computador cliente não receberá uma resposta para sua solicitação de inicialização remota.  

 Há um roteador entre o computador cliente e o servidor de instalação remota que não está permitindo a passagem das permissões ou solicitações com base em DHCP? Quando o computador cliente de Serviços de Implantação do Windows e o servidor de Serviços de Implantação do Windows estão em sub-redes separadas, configure o roteador entre os dois sistemas para encaminhar pacotes DHCP para o servidor de Serviços de Implantação do Windows. Essa organização é necessária, porque os computadores cliente de Serviços de Implantação do Windows descobrem um servidor de Serviços de Implantação do Windows usando a mensagem de difusão DHCP. Sem o encaminhamento DHCP configurado em um roteador, as difusões DHCP dos computadores cliente não chegam ao servidor de Serviços de implantação do Windows. Esse processo de encaminhamento de DHCP às vezes é chamado de *Proxy DHCP* ou *Endereço Auxiliar de IP* em manuais de configuração de roteador. Consulte as instruções do roteador para obter mais informações sobre como configurar o encaminhamento de DHCP em um roteador específico.  

#####  <a name="ImprovePXEIPAddressAssignmentResponseTime"></a> Melhorar o tempo de resposta de atribuição de endereço IP de PXE  
 Verifique os seguintes elementos se estiver demorando muito tempo \(15 a 20 segundos\) para o computador cliente do PXE recuperar um endereço IP:  

-   O adaptador de rede no computador de destino e o comutador ou roteador definido para a mesma velocidade \(automática, duplex, total e assim por diante\)  

-   O endereço IP do servidor de Serviços de Implantação do Windows está no arquivo Auxiliar de IP no roteador pelo qual a conexão é feita? Se a lista de endereços IP no arquivo Auxiliar de IP for longa, você poderá mover o endereço do servidor de Serviços de Implantação do Windows para próximo da parte superior  

### <a name="restarting-the-deployment-process"></a>Reiniciando o processo de implantação  
 **Problema:** ao testar e solucionar problemas em uma sequência de tarefas nova ou modificada, talvez seja necessário reiniciar o computador de destino para que o processo de implantação possa começar novamente do início. Podem ocorrer resultados inesperados, porque o MDT mantém controle sobre seu progresso gravando dados no disco rígido. Qualquer reinicialização do computador de destino faz com que o MDT retome de onde parou na reinicialização anterior.  

 **Solução possível:** para permitir que o processo de implantação recomece, exclua as pastas C:\\MININT e C:\\\_SMSTaskSequence antes de reiniciar o computador de destino.  

### <a name="sysprep"></a>Sysprep  
 Examine os problemas e soluções relacionados ao Sysprep:  

-   O computador de destino não está aparecendo na UO do AD DS conforme descrito em [A conta do computador está na UO errada](#ComputerAccountisintheWrongOU).  

####  <a name="ComputerAccountisintheWrongOU"></a> A conta do computador está na UO errada  
 **Problema:** o computador de destino está corretamente ingressado no domínio, mas a conta de computador está na UO incorreta.  

 **Solução possível 1:** se existir uma versão anterior da conta para o computador de destino, ela permanecerá na sua UO original. Para mover a conta para a UO especificada, adicione uma etapa de sequência de tarefas que usa uma ferramenta de automação, como Microsoft Visual Basic® Scripting Edition.  

 **Solução possível 2:** confirme se a UO especificada está no formato correto e se ela existe. O formato correto da UO deve ser `OU=Reception,OU=NYC,DC=Woodgrovebank,DC=com`.  

### <a name="configuration-manager"></a>Gerenciador de Configurações  
 **Problema:** a mensagem de erro mostrada na REF \_Ref308174600 \\h Figura 3 é exibida quando você tenta criar um ponto de serviço PXE do Configuration Manager ponto usando a opção **Criar certificado PXE autoassinado**.  

 ![TroubleshootingReference3](media/TroubleshootingReference3.jpg "TroubleshootingReference3")  
Figura Figura SEQ \\\* ÁRABE 3. Erro do ponto do serviço PXE  

 **Figura Figura SEQ \\\* ÁRABE 3. Erro do ponto do serviço PXE**  

 **Solução possível:** se um ponto de serviço PXE existia anteriormente no servidor que você está configurando, o ponto de serviço PXE pode não ter excluído os certificados autocriados ao ser desinstalado. Exclua a pasta do certificado do PXE de C:\\Documents and Settings\\*user\_name*\\Application Data\\Microsoft\\Crypto\\RSA, em que *user\_name* é o nome do usuário executando a configuração atual ou quem executou a configuração anterior. O Assistente de Nova Função de Site no console do Configuration Manager deve ser concluído com êxito ao excluir a pasta.  

### <a name="task-sequences"></a>Sequências de tarefas  
 Examine os problemas e soluções relacionados à sequência de tarefas:  

-   A sequência de tarefas não é concluída com êxito ou tem um comportamento imprevisível conforme descrito em [A sequência de tarefas não é concluída com êxito](#TaskSequenceDoesNotFinishSuccessfully).  

-   As sequências de tarefas de OEM \(Fabricante de Equipamento Original\) no LTI são listadas em imagens de inicialização com a arquitetura de processador oposta conforme descrito em [A sequência de tarefas de OEM aparece de forma incorreta para uma imagem de inicialização criada para uma arquitetura de processador diferente](#OEMTaskSequenceIncorrectlyAppearsforBootImage).  

-   O Assistente de Implantação do Windows exibe a mensagem de erro “Item de sequência de tarefas inválido \(GUID do sistema operacional inválido\)” conforme descrito na [Mensagem de Item de sequência de tarefas inválido (GUID do sistema operacional inválido) no Assistente de implantação do Windows](#BadTaskSequenceItem).  

-   Ao configurar um nome de conexão de rede, a mensagem "Insira um nome válido para o adaptador de rede" é exibida conforme descrito em [Aplicar configurações de rede](#ApplyNetworkSettings).  

-   Problemas que podem ocorrer como resultado de uma configuração incorreta de continuar nas definições de configurações de erro para etapas da sequência de tarefas conforme descrito em [Continuar se houver erro](#UseContinueonError).  

####  <a name="TaskSequenceDoesNotFinishSuccessfully"></a> A sequência de tarefas não é concluída com êxito  
 **Problema:** a sequência de tarefas pode não ser concluída com êxito ou ter um comportamento imprevisível.  

 **Solução possível:** a etapa da sequência de tarefas **Instalar Sistema Operacional** \(para LTI\) ou a etapa da sequência de tarefas **Aplicar imagem do sistema operacional** \(para UDI e ZTI\) pode ter sido modificada após a criação da etapa da sequência de tarefas pode levar a resultados imprevisíveis. Por exemplo, se uma sequência de tarefas foi criada para implantar uma imagem do Windows 8.1 de 32 bits e, posteriormente a etapa da sequência de tarefas **Instalar sistema operacional** ou a **Aplicar imagem do sistema operacional** for modificada para fazer referência a uma imagem do Windows 8.1 de 64 bits, a sequência de tarefas poderá não ser executada com êxito.  

 É recomendável que a nova sequência de tarefas seja criada para implantar uma imagem de sistema operacional diferente.  

####  <a name="OEMTaskSequenceIncorrectlyAppearsforBootImage"></a> A sequência de tarefas de OEM aparece de forma incorreta para uma imagem de inicialização criada para uma arquitetura de processador diferente  
 **Problema:** uma sequência de tarefas com base em um modelo de sequência de tarefas de OEM de LTI está aparecendo para uma imagem de inicialização com uma arquitetura de processador diferente. Por exemplo, uma sequência de tarefas de OEM que implanta um sistema operacional de 64 bits está aparecendo em uma imagem de inicialização de 32 bits.  

 **Solução possível:** esse é o comportamento esperado uma vez que as sequências de tarefas em LTI não são consideradas como sendo “específicas de plataforma” e sempre serão listadas, independentemente da arquitetura de processador na imagem de inicialização.  

####  <a name="BadTaskSequenceItem"></a> Mensagem de Item de sequência de tarefas inválido \(GUID do sistema operacional inválido\) no Assistente de implantação do Windows  
 **Problema:** ao executar o Assistente de Implantação do Windows, o assistente exibe a mensagem de erro "Item de sequência de tarefa inválido \(GUID do sistema operacional inválido\)". O sistema operacional está listado no arquivo OperatingSystem.xml, no entanto, o sistema operacional não é exibido no Workbench de Implantação.  

 **Solução possível:** a fonte original do sistema operacional tem dois ou mais arquivos WIM associados. Uma SKU que está associada a uma sequência de tarefas é excluída, no entanto, outras SKUs para o sistema operacional de origem ainda existem. Quando a sequência de tarefas que referencia a SKU excluída estiver selecionada na página do assistente **Selecionar uma sequência de tarefas para executar no computador** no Assistente de Implantação do Windows, a mensagem de erro "Item de sequência de tarefa inválido \(GUID de sistema operacional inválido\)" é exibida depois que você clicar em **Próximo** na página do assistente.  

 Para resolver esse problema, execute uma das seguintes tarefas:  

-   Remova todas as SKUs da fonte de sistema operacional. O Assistente de Implantação do Windows se comporta normalmente e a mensagem de erro não é exibida.  

-   Altere a sequência de tarefas para usar uma imagem de sistema operacional diferente.  

####  <a name="ApplyNetworkSettings"></a> Aplicar Configurações de Rede  
 **Problema:** ao configurar o nome de conexão de rede no Workbench de Implantação, um erro de validação exibe a mensagem "Insira um nome válido para o adaptador de rede".  

 **Solução possível:** remova os espaços e caracteres inválidos do nome de conexão especificado.  

####  <a name="UseContinueonError"></a> Continuar se houver erro  
 Se uma sequência de tarefas do MDT estiver configurada para não continuar com erro e a sequência de tarefas retornar um erro, todas as sequências de tarefas restantes nesse grupo de sequência de tarefas serão ignoradas. No entanto, os grupos de sequência de tarefas restantes são processados. Considere o seguinte:  

 Dois grupos de sequência de tarefas foram criados e cada grupo contém mais de uma etapa de sequência de tarefas:  

-   Grupo A  

    -   Etapa A  

    -   Etapa B  

-   Grupo B  

    -   Etapa A  

    -   Etapa B  

 Se o Grupo A\\Etapa A estiver configurado para não continuar se houver erro, então o Grupo A\\Etapa B não será processado. No entanto, todas as etapas de sequência de tarefas no Grupo B serão processadas.  

### <a name="the-user-state-migration-tool"></a>A Ferramenta de Migração do Usuário  
 Examine os problemas e soluções relacionados ao USMT:  

-   Os atalhos que apontam para documentos armazenados em pastas compartilhadas de rede podem não ser restaurados adequadamente conforme descrito em [Atalhos da área de trabalho ausentes](#MissingDesktopShortcuts).  

####  <a name="MissingDesktopShortcuts"></a> Atalhos de área de trabalho ausentes  
 **Problema:** ao usar o USMT para migrar dados de usuário, os atalhos que apontam para documentos de rede não podem ser restaurados. Os atalhos são capturados durante Scanstate. No entanto, eles são nunca restaurados para o computador de destino durante Loadstate.  

 **Solução possível:** edite o arquivo MigUser.xml e comente a seguinte linha:  

 Original:  

```  
<include> filter='MigXmlHelper.IgnoreIrrelevantLinks()'>  
```  

 Modificado:  

```  
<include> <!-- filter='MigXmlHelper.IgnoreIrrelevantLinks()'> -->  
```  

### <a name="windows-imaging-format-files"></a>Arquivos de formato de geração de imagens do Windows  
 Examine os problemas e soluções relacionados ao WIN:  

-   As implantações de LTI e ZTI falharão com erros de arquivo do WIM no arquivo BDD.log conforme descrito em [Arquivo WIM corrompido](#CorruptWIMFile).  

####  <a name="CorruptWIMFile"></a> Arquivo WIM corrompido  
 **Problema:** ao implantar uma imagem, a implantação falhará com as seguintes entradas no arquivo BDD.log:  

-   ```  
    The image \\Server\Deployment$\Operating Systems\Windows\version1.wim was not applied successfully by ImageX, rc = 2  
    ```  

-   ```  
    LTIApply COMPLETED.  Return Value = 2  
    ```  

-   ```  
    ZTI ERROR - Non-zero return code by LTIApply, rc = 2  
    ```  

 Investigue o problema montando o arquivo WIM usando os resultados o ImageX no erro, “Os dados são inválidos”. As investigações mostram que o carimbo de data/hora do arquivo .wim é de muitos anos antes da data atual. É possível que outro processo, como um scanner de vírus, esteja mantendo o arquivo .wim aberto após ter sido fechado anteriormente na conclusão de um processo de leitura ou gravação.  

 **Solução possível:** restaure o arquivo .wim de mídia de backup.  

### <a name="windows-pe"></a>Windows PE  
 Examine os problemas e soluções relacionados ao Windows PE:  

-   O processo de implantação de LTI ou ZTI não for iniciado devido à RAM ou adaptadores de rede sem fio insuficientes conforme descrito em [Processo de implantação não iniciado – RAM ou adaptadores de rede sem fio limitados](#LimitedRamorWirelessNetworkAdapter).  

-   O processo de implantação de LTI ou ZTI não é iniciado devido à ausência de componentes do Windows PE conforme descrito em [Processo de implantação não iniciado – componentes ausentes](#MissingComponents).  

-   O processo de implantação de LTI ou ZTI não é iniciado devido a drivers de dispositivo ausentes ou incorretos conforme descrito em [Processo de implantação não iniciado – drivers ausentes ou incorretos](#MissingorIncorrectDrivers).  

####  <a name="LimitedRamorWirelessNetworkAdapter"></a> Processo de implantação não iniciado – RAM ou adaptadores de rede sem fio limitados  
 **Problema:** ao implantar uma imagem em determinados computadores de destino, o Windows PE é iniciado, executa **wpeinit**, abre uma janela de prompt de comando, mas não inicia de fato o processo de implantação. Solucionar o problema mapeando uma unidade de rede do computador de destino indica que os drivers de adaptador de rede não estão carregados.  

 **Solução possível 1:** o Assistente de Implantação não está iniciando, porque não há RAM suficiente. Verifique se o computador de destino tem pelo menos 512 MB de RAM e se nenhuma memória de vídeo compartilhada consome mais do que 64 MB dos 512 MB.  

 As versões do Windows PE para as quais o MDT dá suporte não podem ser executadas em um computador de destino com menos de 512 MB de RAM.  

 **Solução possível 2:** não incluir os drivers sem fio na imagem do Windows PE.  

####  <a name="MissingComponents"></a> Processo de implantação não iniciado – componentes ausentes  
 **Problema:** ao solucionar o problema de uma implantação com falha, uma revisão do arquivo BDD.log lista a seguinte entrada:  

```  
ERROR - Unable to create ADODB.Connection object, impossible to query SQL Server: ActiveX component can't create object (429).  
```  

 **Solução possível:** esse erro pode indicar que a imagem do Windows PE não foi criada usando o MDT. Se você estiver usando o Configuration Manager, não use uma das imagens do Windows PE que o Configuration Manager criou. Em vez disso, crie uma imagem usado o Assistente para Importar a sequência de tarefas de implantação da Microsoft.  

> [!NOTE]
>  As imagens do Windows PE que o Configuration Manager cria contêm componentes que dão suporte a script, XML e WMI (Instrumentação de Gerenciamento do Windows), mas elas não contêm componentes que dão suporte a Microsoft ADO (ActiveX® Data Objects).  

####  <a name="MissingorIncorrectDrivers"></a> Processo de implantação não iniciado – drivers ausentes ou incorretos  
 **Problema:** ao implantar em determinados computadores de destino, o Windows PE é iniciado, executa **wpeinit**, abre uma janela de prompt de comando, mas não inicia de fato o processo de implantação. Solucionar o problema mapeando uma unidade de rede do computador de destino indica que os drivers de adaptador de rede não estão carregados. Uma revisão do arquivo SetupAPI.log localizado em *X*:\Windows\System32\Inf indica que o Windows PE gera erros quando está configurando o adaptador de rede, um deles sendo “Este driver não é destinado para esta plataforma”. Os drivers da lista **Drivers Não Incluídos** foram inseridos na imagem.  

 **Solução possível:** é possível que o Windows PE esteja enfrentando um conflito de driver com outro driver. Ao definir as configurações para a imagem do Windows PE no Workbench de Implantação, crie um grupo de drivers do Windows PE que contém somente o adaptador de rede e drivers de armazenamento e, em seguida, configure o compartilhamento de implantação para usar apenas o grupo de drivers do Windows PE.  

## <a name="deployment-process-flow-charts"></a>Fluxogramas do processo de implantação  
 Esta seção fornece dois conjuntos de fluxogramas do MDT: um para implantações de LTI e um para implantações de ZTI com o Configuration Manager. Cada fluxograma ilustra as tarefas executadas durante esse tipo de implantação.  

 Familiarize-se com os fluxogramas do processo de implantação:  

-   Examinando os fluxogramas do processo de implantação de LTI conforme descrito em [Fluxogramas do processo de implantação de LTI](#LTIDeploymentProcessFlowcharts)  

-   Examinando os fluxogramas do processo de implantação de ZTI conforme descrito em [Fluxogramas do processo de implantação de ZTI](#ZTIDevelopmentProcessFlowcharts)  

###  <a name="LTIDeploymentProcessFlowcharts"></a> Fluxogramas do processo de implantação de LTI  
 Os fluxogramas são fornecidos para as seguintes fases:  

-   Validação (Figura 4)  

-   Captura de estado (Figura 5 e Figura 6)  

-   Pré-instalação (Figura 7, a Figura 8 e Figura 9)  

-   Instalação (Figura 10)  

-   Pós-instalação (Figura 11 e Figura 12)  

-   Restauração de estado (Figura 13, Figura 14, Figura 15 e Figura 16)  

 ![TroubleshootingReference4](media/TroubleshootingReference4.jpg "TroubleshootingReference4")  
Figura 4. Fluxograma da fase de validação  

 **Figura 4. Fluxograma da fase de validação**  

 ![TroubleshootingReference5](media/TroubleshootingReference5.jpg "TroubleshootingReference5")  
Figura 5. Fluxograma da fase de captura de estado (1 de 2)  

 **Figura 5. Fluxograma da fase de captura de estado (1 de 2)**  

 ![TroubleshootingReference6](media/TroubleshootingReference6.jpg "TroubleshootingReference6")  
Figura 6. Fluxograma da fase de captura de estado (2 de 2)  

 **Figura 6. Fluxograma da fase de captura de estado (2 de 2)**  

 ![TroubleshootingReference7](media/TroubleshootingReference7.jpg "TroubleshootingReference7")  
Figura 7. Fluxograma da fase pré-instalação (1 de 3)  

 **Figura 7. Fluxograma da fase pré-instalação (1 de 3)**  

 ![TroubleshootingReference8](media/TroubleshootingReference8.jpg "TroubleshootingReference8")  
Figura 8. Fluxograma da fase pré-instalação (2 de 3)  

 **Figura 8. Fluxograma da fase pré-instalação (2 de 3)**  

 ![TroubleshootingReference9](media/TroubleshootingReference9.jpg "TroubleshootingReference9")  
Figura 9. Fluxograma da fase pré-instalação (3 de 3)  

 **Figura 9. Fluxograma da fase pré-instalação (3 de 3)**  

 ![TroubleshootingReference10](media/TroubleshootingReference10.jpg "TroubleshootingReference10")  
Figura 10. Fluxograma da fase de instalação  

 **Figura 10. Fluxograma da fase de instalação**  

 ![TroubleshootingReference11](media/TroubleshootingReference11.jpg "TroubleshootingReference11")  
Figura 11. Fluxograma da fase pós-instalação (1 de 2)  

 **Figura 11. Fluxograma da fase pós-instalação (1 de 2)**  

 ![TroubleshootingReference12](media/TroubleshootingReference12.jpg "TroubleshootingReference12")  
Figura 12 Fluxograma da fase pós-instalação (2 de 2)  

 **Figura 12 Fluxograma da fase pós-instalação (2 de 2)**  

 ![TroubleshootingReference13](media/TroubleshootingReference13.jpg "TroubleshootingReference13")  
Figura 13. Fluxograma da fase de restauração de estado (1 de 4)  

 **Figura 13. Fluxograma da fase de restauração de estado (1 de 4)**  

 ![TroubleshootingReference14](media/TroubleshootingReference14.jpg "TroubleshootingReference14")  
Figura 14. Fluxograma da fase de restauração de estado (2 de 4)  

 **Figura 14. Fluxograma da fase de restauração de estado (2 de 4)**  

 ![TroubleshootingReference15](media/TroubleshootingReference15.jpg "TroubleshootingReference15")  
Figura 15. Fluxograma da fase de restauração de estado (3 de 4)  

 **Figura 15. Fluxograma da fase de restauração de estado (3 de 4)**  

 ![TroubleshootingReference16](media/TroubleshootingReference16.jpg "TroubleshootingReference16")  
Figura 16. Fluxograma da fase de restauração de estado (4 de 4)  

 **Figura 16. Fluxograma da fase de restauração de estado (4 de 4)**  

###  <a name="ZTIDevelopmentProcessFlowcharts"></a> Fluxogramas do processo de implantação de ZTI  
 Os fluxogramas são fornecidos para as seguintes fases da implantação do ZTI com o Configuration Manager:  

-   Inicialização (Figura 17)  

-   Validação (Figura 18)  

-   Captura de estado (Figura 19)  

-   Pré-instalação (Figura 20)  

-   Instalação (Figura 21)  

-   Pós-instalação (Figura 22)  

-   Restauração de estado (Figura 23 e Figura 24)  

-   Captura (Figura 25)  

 ![TroubleshootingReference17](media/TroubleshootingReference17.jpg "TroubleshootingReference17")  
Figura 17. Fluxograma da fase de inicialização  

 **Figura 17. Fluxograma da fase de inicialização**  

 ![TroubleshootingReference18](media/TroubleshootingReference18.jpg "TroubleshootingReference18")  
Figura 18. Fluxograma da fase de validação  

 **Figura 18. Fluxograma da fase de validação**  

 ![TroubleshootingReference19](media/TroubleshootingReference19.jpg "TroubleshootingReference19")  
Figura 19. Fluxograma da fase de captura de estado  

 **Figura 19. Fluxograma da fase de captura de estado**  

 ![TroubleshootingReference20](media/TroubleshootingReference20.jpg "TroubleshootingReference20")  
Figura 20. Fluxograma da fase pré-instalação  

 **Figura 20. Fluxograma da fase pré-instalação**  

 ![TroubleshootingReference21](media/TroubleshootingReference21.jpg "TroubleshootingReference21")  
Figura 21. Fluxograma da fase de instalação  

 **Figura 21. Fluxograma da fase de instalação**  

 ![TroubleshootingReference22](media/TroubleshootingReference22.jpg "TroubleshootingReference22")  
Figura 22. Fluxograma da fase pós-instalação  

 **Figura 22. Fluxograma da fase pós-instalação**  

 ![TroubleshootingReference23](media/TroubleshootingReference23.jpg "TroubleshootingReference23")  
Figura 23. Fluxograma da fase de restauração de estado (1 de 2)  

 **Figura 23. Fluxograma da fase de restauração de estado (1 de 2)**  

 ![TroubleshootingReference24](media/TroubleshootingReference24.jpg "TroubleshootingReference24")  
Figura 24. Fluxograma da fase de restauração de estado (2 de 2)  

 **Figura 24. Fluxograma da fase de restauração de estado (2 de 2)**  

 ![TroubleshootingReference25](media/TroubleshootingReference25.jpg "TroubleshootingReference25")  
Figura 25. Fluxograma da fase de captura  

 **Figura 25. Fluxograma da fase de captura**  

## <a name="finding-additional-help"></a>Encontrando ajuda adicional  
 Encontre ajuda adicional na resolução de problemas de implantação do MDT:  

-   Entrando em contato com o Suporte da Microsoft no [Suporte da Microsoft](#MicrosoftSupport)  

-   Obtendo suporte adicional por meio de blogs e outros recursos de Internet conforme descrito no [Suporte pela Internet](#InternetSupport)  

###  <a name="MicrosoftSupport"></a> Suporte da Microsoft  
 A Microsoft fornece suporte de nível Premier e Professional para o Microsoft Deployment Toolkit.  

 Suporte de nível Professional: [http://support.microsoft.com/](http://support.microsoft.com/)  

 Suporte de nível Premier: [https://premier.microsoft.com/](https://premier.microsoft.com/)  

> [!NOTE]
>  Ao contatar o suporte, seja claro indicando que o problema é com o MDT e a versão específica.  

###  <a name="InternetSupport"></a> Suporte da Internet  
 Muitas fontes online fornecem assistência de solução de problemas adicional para o MDT além do que é abordado nessa referência. Essas fontes online incluem:  

-   Blogs hospedado pela Microsoft  

    -   [Blog da Equipe do MDT](http://blogs.technet.com/b/msdeployment/)  

    -   [Blog da Equipe do Configuration Manager](http://blogs.technet.com/b/configmgrteam/)  

    -   [Blog de Michael Niehaus](http://blogs.technet.com/b/mniehaus/) (Michael Niehaus escreve sobre a implantação do Windows e do Microsoft Office.)  

-   Fóruns e grupos de discussão hospedados pela Microsoft:  

     Os grupos de discussão e os fóruns estão disponíveis com o suporte de funcionários da Microsoft, colegas do setor e Microsoft Valued Professionals:  

    -   [Configuration Manager – implantação de sistema operacional](http://social.technet.microsoft.com/Forums/home?forum=configmanagerosd)  

    -   [Instalação, configuração e implantação do Windows 8](http://social.technet.microsoft.com/Forums/windows/home?forum=w8itproinstall)  

-   Fontes de informações relacionadas à implantação de fora da Microsoft:  

    -   [DeployVista.com](http://www.deployvista.com/)  

    -   [myITforum.com](http://www.myitforum.com/)
