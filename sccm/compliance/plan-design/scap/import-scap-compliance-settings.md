---
title: Importar as configurações de conformidade do SCAP
titleSuffix: System Center Configuration Manager
description: Importar as configurações de conformidade do SCAP como linhas de base de configuração e exportar os resultados
ms.custom: na
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0bdcb018-bac2-4540-b786-6242bac73ff4
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 5863f8b9a79e8e22e215e9feac7744b4a6ce279d
ms.sourcegitcommit: 27da4be015f1496b7b89ebddb517a2685f1ecf74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="import-the-compliance-settings-compliant-cab-files-into-system-center-configuration-manager"></a>Importe os arquivos .cab compatíveis com as Configurações de conformidade para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

> [!Tip]  
> Esse recurso foi introduzido pela primeira vez na versão Technical Preview 1803 como um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features). Esta versão de pré-lançamento das extensões do SCAP pode ser instalada em todas as versões compatíveis no momento do branch atual do Configuration Manager e o LTSB 1606. O arquivo de instalação está localizado em cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi a partir da Technical Preview 1803. 

A próxima etapa no processo é usar o Console do Configuration Manager para importar os arquivos .cab em conformidade com as Configurações de conformidade no Configuration Manager. Ao importar os arquivos .cab que você criou anteriormente neste processo, um ou mais itens de configuração e linhas de base de configuração são criados no banco de dados do Configuration Manager. Mais adiante no processo, você pode atribuir cada uma das linhas de base de configuração a uma coleção de computadores no Configuration Manager.

## <a name="to-import-the-compliance-settings-compliant-cab-files-into-configuration-manager"></a>Para importar os arquivos .cab em conformidade com as Configurações de conformidade para o Configuration Manager

1. Abra o **Console do Configuration Manager**.
2. No **Console do Configuration Manager, no painel de navegação, acesse **Ativos e Conformidade**> **Configurações de Conformidade** > **Linhas de Base de Configuração**.

3. No painel de ações, clique em **Importar Dados de Configuração** para iniciar o Assistente de Importação de Dados de Configuração.

1. Conclua o **Assistente de Importação de Dados de Configuração** usando as informações na tabela a seguir e aceitando os valores padrão, a menos que especificado de outra forma.



Processo do Assistente de Importação de Dados de Configuração

| Nome da página do Assistente | Ação do usuário |
| --- | --- |
| **Escolher Arquivos** |1. Clique em **Adicionar**. </br>A caixa de diálogo Abrir é exibida.|
||2. Na caixa de diálogo **Abrir**, acesse **&lt;compliant cab output\_folder &gt;**. Clique no arquivo **&lt; compliant\_cab&gt;**.cab, em que _compliant cab **output\_folder** é a pasta que foi especificada após a opção -output quando você executou a ferramenta Sces.ScapToDcm.exe. **compliant\_file** é o nome de um arquivo .cab que você criou anteriormente no processo. Em seguida, clique em **Abrir**. </br> O Console do Configuration Manager – a caixa de diálogo Aviso de Segurança é exibida.|
||3. Na caixa de diálogo **Console do Configuration Manager – Aviso de Segurança**, clique em **Executar**. Na página Escolher Arquivos, os dados de configuração aparecem na lista de linhas de base a serem importadas.|
||3. Clique em **Avançar**.|
| **Resumo** |5. Clique em **Avançar**. |
| **Concluindo o Assistente de Importação de Dados de Configuração** |6. Clique em **Fechar**. |

A nova linha de base de configuração é exibida no painel de informações do Console do Configuration Manager.

>[!IMPORTANT]
> Você precisa repetir este processo para cada arquivo .cab que você criou anteriormente no processo. Há um arquivo .cab para cada perfil selecionado no arquivo XML do XCCDF/DataStream baixado do site da NVD, que pode ser processado com a ferramenta Microsoft.Sces.ScapToDcm.exe.

A linha de base de configuração importada é somente leitura e tem um Status de &#39;Habilitado&#39; e um estado Implantado inicial de &#39;Não&#39;.  A propriedade &#39;Data de Modificação&#39; indica a hora em que a linha de base foi importada.  O nome da linha de base de configuração é obtido da seção de nome de exibição do XCCDF/XML do DataStream. O nome é criado usando a seguinte convenção:

ABC[XYZ], em que ABC é a ID de Parâmetro de Comparação XCCDF e XYZ é a ID de Perfil XCCDF (caso um perfil seja selecionado).



## <a name="assign-configuration-baselines-to-the-computer-collections"></a>Atribuir linhas de base de configuração às coleções de computadores

Depois de criar as coleções de computadores apropriadas para os computadores que você deseja avaliar quanto à conformidade com o SCAP, você estará pronto para atribuir as linhas de base de configuração que você importou para associá-las às coleções de computadores. Esta seção fornece informações para atribuir uma linha de base a uma coleção de computadores por meio do Console do Configuration Manager.

Para atribuir uma linha de base de configuração a uma coleção de computadores:

1. Abra o **Console do** **Configuration Manager**.

2. No **Console do Configuration Manager, no painel de navegação, acesse **Ativos e Conformidade** > **Configurações de Conformidade** >**Linhas de Base de Configuração**.
3. No painel de navegação, clique em &lt; **configuration\_baseline>, em que &lt;_configuration\_baseline&gt;_ é o nome da linha de base de configuração que você deseja atribuir a uma coleção de computadores.

    A lista de itens de configuração para a linha de base de configuração é exibida no painel de informações do Configuration Manager.

4. No painel Ações, clique em **Implantar**.

5. Conclua o **Diálogo** **Implantar** **Linha de Base de Configuração** usando as informações na tabela a seguir e aceitando os valores padrão, a menos que especificado de outra forma.

### <a name="deploy-configuration-baseline-dialog-process"></a>Implantar Processo do Diálogo de Linha de Base de Configuração

| Nome da página do Assistente | Ação do usuário |
| --- | --- |
| **Escolher coleção** | 1. Clique em **Procurar**.|
||2. Na caixa de diálogo **Selecionar Coleção**, selecione **Coleções de Dispositivos**. Em seguida, clique em **&lt;computer\_collection&gt;**, em que &lt;_computer\_collection&gt;_ é o nome da coleção de computadores que você criou anteriormente no processo. Clique em **OK**.|
| **Definir agendamento** |3. Selecione o agendamento apropriado para a sua organização.|
 
>[!IMPORTANT]
> Repita este processo para cada coleção de computadores que deseja atribuir a cada linha de base de configuração. No mínimo, atribua cada linha de base de configuração a, pelo menos, uma coleção de computadores.

## <a name="verify-that-the-compliance-data-has-been-collected"></a>Verificar se os dados de conformidade foram coletados

Antes de exportar os dados de conformidade de volta para o formato SCAP, você precisa verificar se os dados foram coletados. Depois de atribuir uma linha de base de configuração para uma coleção de computadores, o cliente do Configuration Manager em cada computador na coleção coleta automaticamente as informações de conformidade. Em seguida, as informações de conformidade são armazenadas no banco de dados do Configuration Manager.

Exiba o status da implantação de linha de base de configuração no Configuration Manager para garantir que os dados apropriados foram coletados pelos clientes do Configuration Manager. É importante verificar se os dados de conformidade apropriados foram coletados no Configuration Manager, pois eles podem ajudá-lo a validar os arquivos de resultados do XCCDF/DataStream que serão criados mais adiante no processo.



### <a name="verify-that-the-compliance-data-has-been-collected"></a>Verifique se os dados de conformidade foram coletados

1. Abra o Console do Configuration Manager.
2. No Console do Configuration Manager, no painel de navegação, vá para **Monitoramento** > **Implantações**.
3. Clique em **Tipo de Recurso** para classificar o tipo de implantação e encontrar itens que são do tipo **Linha de Base** na lista.
4. Clique com o botão direito do mouse em &lt;configuration\_baseline&gt; na lista que você acabou de implantar na coleção e clique em **Exibir Status**.
5. Em seguida, mova para o nó &lt;configuration\_baseline&gt; para exibir o status de conformidade. Se houver um computador no estado desconhecido, isso significará que a coleta de dados de conformidade ainda não foi concluída para esse computador.

### <a name="validate-the-xccdfdatastream-results"></a>Validar os resultados do XCCDF/Fluxo de dados

1. Abra o console do gerenciador de configurações.
2. No console do Configuration Manager, no painel de navegação, vá para **Configurações de Conformidade** > **Painel do SCAP**.
3. Selecione a Linha de Base de Configuração, Atribuição, Arquivo do SCAP, Fluxo de Dados, Parâmetro de Comparação e Perfil (se aplicável).
4. Clique em **Mostrar Relatório**
 ![Relatório do SCAP](./media/scap-report.png)



## <a name="export-compliance-results-to-scap-format"></a>Exportar resultados de conformidade para o formato do SCAP

A próxima tarefa no processo é exportar os dados de conformidade das Configurações de conformidade para o formato SCAP, que é um arquivo de relatório ARF em formato XML/que pode ser compreendido pelo usuário. O Assistente para Exportação de Extensões do SCAP e a ferramenta Microsoft.Sces.DcmToScap.exe exportam um arquivo de resultados do XCCDF/DataStreamARF separado para cada linha de base de configuração de Configurações de Conformidade. Estes arquivos correspondem a cada arquivo de entrada do XCCDF/DataStream usado pela ferramenta Microsoft.Sces.ScapToDcm.exe para criar cada linha de base de configuração das Configurações de conformidade.

### <a name="export-the-compliance-settings-compliance-data-using-the-export-scap-report-wizard"></a>Exportar os dados de conformidade de Configurações de Conformidade usando o Assistente para Exportação de Relatório do SCAP

1. Inicie o Assistente para Exportação de Relatório do SCAP no menu de clique com o botão direito do mouse no Painel do SCAP.
![Importar do painel do SCAP](./media/import-from-scap-dashboard.png)

2. Selecione a Linha de Base de Configuração e a Atribuição ![Selecionar linha de base](./media/select-ci-baseline.png)

3. Escolha o local do arquivo de fluxo de dados do SCAP, arquivo XCCDF/CPE ou arquivos de conteúdo e a variável Oval.
![Escolher o fluxo de dados](./media/export-scap-report-datastream.png)

4. Especifique o nome da organização e escolha o local da pasta para exportar o relatório do SCAP.
 ![Escolher o fluxo de dados](./media/specify-org-export.png)

5. Confirme as configurações.
 ![Escolher o fluxo de dados](./media/confirm-export.png)

6. Escolha **Avançar para exportar o relatório.  Você verá uma barra de progresso e, em seguida, uma página de conclusão.
 ![Concluir a exportação](./media/complete-report-export.png)



### <a name="alternate-method-export-the-compliance-settings-compliance-data-using-the-microsoftscesdcmtoscapexe-tool"></a>(Método alternativo) Exporte os dados de conformidade de Configurações de Conformidade usando a ferramenta Microsoft.Sces.DcmToScap.exe

1. No prompt de comando, vá até a pasta AdminConsole\Bin, digite os parâmetros de linha de comando listados na tabela a seguir e pressione **ENTER:

    >[!NOTE] 
    >Sua conta deve ter permissões de leitura para o provedor do Configuration Manager e também ter permissões de gravação para a pasta de saída especificada no parâmetro –out da linha de comando.

**Para conteúdo do SCAP 1.0/1.1 (como conteúdo do USGCB e DISA):**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –xccdf &lt;xccdf.xml&gt; -cpe &lt;cpe.xml&gt;  -select &lt;xccdfBenchmark/profile&gt; -out &lt;outputResultFolder&gt;  [-log logFileName]

  >[!NOTE] 
    >Você deverá usar o parâmetro –select para especificar o parâmetro de comparação/perfil que foi avaliado nos clientes se houver vários parâmetros de comparação/perfis no conteúdo.

**Para conteúdo do SCAP 1.2 (como o conteúdo mais recente do USGCB):**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID  -select &lt;datastream/xccdfBenchmark/profile&gt; -out &lt;outputResultFolder&gt;  [-log logFileName]

   >[!NOTE] 
   >Você deverá usar o parâmetro –select para especificar o fluxo de dados/parâmetro de comparação/perfil que foi avaliado nos clientes se houver vários fluxos de dados/parâmetros de comparação/perfis no conteúdo.

**Para um único arquivo OVAL com variáveis externas:**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –oval &lt;singleOvalFile.xml&gt; [-variable &lt;externalVariableFile.xml&gt;]  -out &lt;outputResultFolder&gt;  [-log logFileName]

   >[!NOTE] 
    >O Microsoft.Sces.DcmToScap.exe _gerará apenas o relatório de resultados de definição de OVAL para cada computador de destino, o relatório ARF não será gerado.

#### <a name="how-to-get-baseline-ci-id-and-assignment-id"></a>Como obter a ID de CI de linha de base e a ID de Atribuição

No Console de Administração, acesse **Ativos e Conformidade** > **Configurações de Conformidade** > **Linhas de Base de Configuração**. A ID de CI é a ID de CI de Linha de Base de Configuração.

![Obter a ID de CI e a ID de Atribuição](./media/get-to-baselines.png)

Selecione a Linha de Base de Configuração desejada, clique na guia Implantações, se a ID de Atribuição não estiver na exibição, clique com o botão direito do mouse no cabeçalho da coluna, clique em ID de Atribuição para habilitá-la.
![Obter a ID de CI e a ID de Atribuição](./media/get-to-baselines.png)


#### <a name="microsoftscesdcmtoscapexe-command-line-parameters"></a>Parâmetros da linha de comandos de Microsoft.Sces.DcmToScap.exe

| **Parâmetro** | **Uso** | **Necessária** |
| --- | --- | --- |
| -baseline [ID de CI de Linha de Base] | Especificar a Linha de Base de Configuração | Sim |
| -assignment [ID de Atribuição] | Especificar a implantação de Linha de Base de Configuração | Sim |
| -organization [nome da organização] | Especifique o nome da organização que seria exibido no relatório. Pode ser separado por &#39;;&#39; para especificar um nome de organização de várias linhas. | Não |
| -type [dinâmico/completo/fullnosc] | Especifique o tipo de resultado OVAL: resultado dinâmico, resultado completo ou resultado completo sem característica do sistema. | Não (se não for especificado, o valor padrão será completo) |
| -scap [arquivo de fluxo de dados do SCAP] | Especificar o arquivo de fluxo de dados do SCAP | Sim (para o fluxo de dados do SCAP 1.2, mutuamente exclusivo com –xccdf e –oval / -variable) |
| -xccdf [arquivo xccdf] | Especifique o arquivo XCCDF | Sim (para SCAP 1.0/1.1 XCCDF, mutuamente exclusivo com –scap e –oval / -variable) |
| -cpe [cpe file] | Especificar o arquivo CPE | Sim (para SCAP 1.0/1.1 XCCDF, mutuamente exclusivo com –scap e –oval / -variable) |
| -oval [arquivo OVAL] | Especificar o arquivo OVAL | Sim (para o arquivo OVAL autônomo, mutuamente exclusivo com -xccdf e -scap) |
| -variable [arquivo de variável externa OVAL] | Especificar o arquivo de variável externa OVAL | Não (opcional para o arquivo OVAL autônomo quando há um arquivo OVAL de variável externa, mutuamente exclusivo com o -xccdf e -scap) |
| -select [xccdf benchmark/profile] | Selecione o perfil de parâmetro de comparação do XCCDF do fluxo de dados do SCAP ou do arquivo XCCDF | Sim (uma seleção deve ser feita para gerar um relatório para que possamos combinar a linha de base do DCM correspondente no banco de dados do Configuration Manager |
| -out [diretório de saída] | Especificar o local para exportar o arquivo .cab de Configurações de conformidade | Não (se não for especificado, a ferramenta só listará o conteúdo sem conversão) |
| -log [arquivo de log] | Especificar o arquivo de log | Não (se não for especificado, o log será gravado no arquivo Microsoft.Sces.DcmToScap.log) |
| -help/-? | Imprimir o uso da ferramenta | Não |



 >[!TIP] 
 >É possível especificar -? parâmetro –h ou –help para exibir a sintaxe da ferramenta Microsoft.Sces.DcmToScap.exe e uma lista dos parâmetros.

Por padrão, a ferramenta Microsoft.Sces.DcmToScap.exe acessa o banco de dados do Configuration Manager usando suas credenciais. A ferramenta Microsoft.Sces.DcmToScap.exe requer um mínimo de acesso de leitura no banco de dados do Configuration Manager.

Depois de verificar que o relatório **ARF** apropriado: relatório _ARF\_xxxx.xml_ e/ou **Compreensível pelo usuário**: xxx.txt, relatório **Cyberscope**: LASR\_xxx.xml, relatório **ConsumedOval**: xx-oval-&lt;machineName&gt;.xml, relatório **Resultado do parâmetro de comparação XCCDF**: existem arquivos xccdf\_xxx.xml, na linha de comando, digite exit e pressione **ENTER** para sair do prompt de comando.

## <a name="next-step"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Solução de problemas](/sccm/compliance/plan-design/scap/troubleshooting-scap)
