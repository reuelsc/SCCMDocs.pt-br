---
title: Implantar e monitorar a conformidade com SCAP
titleSuffix: Configuration Manager
description: Implante as configurações de conformidade do SCAP como linhas de base de configuração, monitore a conformidade e exporte os resultados.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 0bdcb018-bac2-4540-b786-6242bac73ff4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e3280edbe900e96cf97af8e59578ceab5322ee2a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137289"
---
# <a name="deploy-and-monitor-scap-compliance-in-configuration-manager"></a>Implantar e monitorar a conformidade do SCAP no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Depois de ter [convertido e importado](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_convert-and-import) os arquivos de fluxo de dados do SCAP, veja as próximas etapas a seguir:  

- [Implantar](#bkmk_deploy) as linhas de base de configuração às coleções para avaliar dispositivos quanto à conformidade do SCAP  

- [Monitorar](#bkmk_monitor) os dados de conformidade retornados de clientes de destino  

- [Exportar](#bkmk_export) os resultados de conformidade para o formato SCAP  



## <a name="bkmk_deploy"></a> Implantar linhas de base de configuração do SCAP

Primeiro crie as coleções de dispositivos para os computadores que você deseja avaliar quanto à conformidade do SCAP. Para obter mais informações, veja [Criar coleções](/sccm/core/clients/manage/collections/create-collections).  

Agora você está pronto para implantar as linhas de base de configuração importadas para essas coleções de dispositivos. Para obter mais informações, veja [Como implantar linhas de base de configuração](/sccm/compliance/deploy-use/deploy-configuration-baselines).  

> [!Tip]  
> Repita esse processo para cada linha de base de configuração que você deseja implantar para cada coleção de dispositivos. Como um mínimo, implante cada linha de base de configuração para pelo menos uma coleção de dispositivos.



## <a name="bkmk_monitor"></a> Monitorar os dados de conformidade do SCAP 

Antes de exportar os dados de conformidade de volta para o formato SCAP, você precisa verificar se o site coletou os dados. Depois de implantar uma linha de base de configuração para uma coleção de dispositivos, o cliente do Configuration Manager em cada computador na coleção coletará automaticamente as informações de conformidade. Em seguida, as informações de conformidade são armazenadas no banco de dados do Configuration Manager.

Exiba o status da implantação de linha de base de configuração no Configuration Manager para garantir que os dados apropriados tenham sido coletados pelos clientes do Configuration Manager. É importante verificar se os dados de conformidade apropriados foram coletados no Configuration Manager, pois eles podem ajudá-lo a validar os arquivos de resultados do XCCDF/DataStream que serão criados mais adiante no processo.

Para obter mais informações, veja [Monitorar configurações de conformidade](/sccm/compliance/deploy-use/monitor-compliance-settings).


### <a name="validate-the-xccdfdatastream-results"></a>Validar os resultados do XCCDF/Fluxo de dados

1. No console do Configuration Manager, vá para o workspace **Ativos e Conformidade**, expanda **Configurações de Conformidade** e selecione o **Painel do SCAP**.  

2. Selecione a Linha de Base de Configuração, Atribuição, Arquivo do SCAP, Fluxo de Dados, Parâmetro de Comparação e Perfil (se aplicável).  

3. Clique em **Mostrar Relatório**
 ![Relatório SCAP de exemplo](./media/scap-report.png)



## <a name="bkmk_export"></a> Exportar resultados de conformidade para o formato do SCAP

A próxima etapa no processo é exportar os dados de conformidade para o formato SCAP, que é um arquivo de relatório ARF em formato XML/legível por humanos. O assistente para Exportação de Extensões do SCAP e a ferramenta de linha de comando Microsoft.Sces.DcmToScap.exe exportam um arquivo de resultados XCCDF/DataStreamARF separado para cada linha de base de configuração. Esses arquivos correspondem a cada arquivo de entrada do XCCDF/DataStream usado pela ferramenta Microsoft.Sces.ScapToDcm.exe para criar cada linha de base de configuração.


### <a name="manually-export-with-the-console-wizard"></a>Exportar manualmente com o assistente do console

> [!Note]  
> Esta seção descreve o processo manual para exportar os resultados de conformidade com o console do Configuration Manager. Para automatizar esse processo, consulte a próxima seção para [Exportar automaticamente com a ferramenta de linha de comando](#bkmk_auto-export).  


1. Inicie o assistente **Exportar relatório do SCAP** clicando com o botão direito do mouse no nó **Painel do SCAP**.  
![Iniciar o assistente para Exportar Relatório do SCAP do Painel do SCAP](./media/import-from-scap-dashboard.png)

2. Selecione a Linha de Base de Configuração, a Atribuição e o Tipo de Conteúdo do SCAP.  
![Selecionar linha de base](./media/select-ci-baseline.png)

3. Escolha o local do arquivo de fluxo de dados do SCAP, arquivo XCCDF/CPE ou arquivos de conteúdo e a variável Oval.  
![Escolher o fluxo de dados](./media/export-scap-report-datastream.png)

4. Especifique o nome da organização e escolha o local da pasta para exportar o relatório do SCAP.  
 ![Escolher o fluxo de dados](./media/specify-org-export.png)
   > [!Tip]  
   > Esta página do assistente exibe a linha de comando que você usaria com a ferramenta **DcmToScap.exe** para automatizar o mesmo processo.  

5. Confirme as configurações.  
 ![Escolher o fluxo de dados](./media/confirm-export.png)

6. Escolha **Avançar** para exportar o relatório. Conclua o assistente.  
 ![Concluir a exportação](./media/complete-report-export.png)


### <a name="bkmk_auto-export"></a> Exportar automaticamente com a ferramenta de linha de comando

Abra o prompt de comando e vá para a pasta **AdminConsole\Bin** do Configuration Manager. Use um dos exemplos de linha de comando a seguir:  

> [!NOTE]  
> Sua conta deve ter permissões de leitura para o provedor do Configuration Manager. Você também precisa de permissões de gravação para a pasta especificada no parâmetro `–out` da linha de comando.

**Para conteúdo do SCAP 1.0/1.1 (como conteúdo do USGCB e DISA):**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –xccdf <xccdf.xml> -cpe <cpe.xml>  -select <xccdfBenchmark/profile> -out <outputResultFolder> [-log logFileName]`  

  > [!NOTE]  
  > Se houver vários parâmetros de comparação/perfis no conteúdo, use o parâmetro `–select` para especificar o parâmetro de comparação/perfil avaliado nos clientes.  

**Para conteúdo do SCAP 1.2 (como o conteúdo mais recente do USGCB):**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID -select <datastream/xccdfBenchmark/profile> -out <outputResultFolder> [-log logFileName]`  

   > [!NOTE]  
   > Se houver vários fluxos de dados/parâmetros de comparação/perfis no conteúdo, use o parâmetro `–select` para especificar o fluxo de dados/parâmetro de comparação/perfil avaliado nos clientes.  

**Para um único arquivo OVAL com variáveis externas:**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –oval <singleOvalFile.xml> [-variable <externalVariableFile.xml>] -out <outputResultFolder> [-log logFileName]`  

   > [!NOTE]  
   > O Microsoft.Sces.DcmToScap.exe gera apenas o relatório de resultados de definição de OVAL para cada computador de destino. O relatório ARF não é gerado.  


#### <a name="how-to-get-the-baselineciid-and-assignmentid"></a>Como obter BaselineCIID e AssignmentID

No console do Configuration Manager, vá para o workspace **Ativos e Conformidade**, expanda **Configurações de Conformidade** e selecione **Linhas de Base de Configuração**. O `BaselineCIID` é o identificador (ID) para a linha de base de configuração.  
![Obter a ID de CI e a ID de Atribuição](./media/get-to-baselines.png)

Selecione a linha de base de configuração desejada e, em seguida, clique na guia **Implantações**. O `AssignmentID` é o identificador (ID) para a implantação de linha de base de configuração para uma coleção de dispositivos. Se a ID de Atribuição não for exibida, clique com o botão direito do mouse no cabeçalho da coluna e selecione **ID da Atribuição**.  
![Obter a ID de CI e a ID de Atribuição](./media/get-to-baselines.png)


#### <a name="microsoftscesdcmtoscapexe-command-line-parameters"></a>Parâmetros de linha de comando de Microsoft.Sces.DcmToScap.exe

| Parâmetro | Uso | Necessária |
| --- | --- | --- |
| `-baseline [Baseline CI ID]` | Especificar a Linha de Base de Configuração | Sim |
| `-assignment [Assignment ID]` | Especificar a implantação de Linha de Base de Configuração | Sim |
| `-organization [organization name]` | Especifique o nome da organização que seria exibido no relatório. Pode ser separado por `;` para especificar um nome de organização de várias linhas. | Não |
| `-type [thin/full/fullnosc]` | Especifique o tipo de resultado OVAL: resultado dinâmico, resultado completo ou resultado completo sem característica do sistema. | Não (se não for especificado, o valor padrão será completo) |
| `-scap [scap data stream file]` | Especificar o arquivo de fluxo de dados do SCAP | Sim (para o fluxo de dados do SCAP 1.2, mutuamente exclusivo com -xccdf e -oval/-variable) |
| `-xccdf [xccdf file]` | Especifique o arquivo XCCDF | Sim (para o SCAP 1.0/1.1 XCCDF, mutuamente exclusivo com -scap e -oval/-variable) |
| `-cpe [cpe file]` | Especificar o arquivo CPE | Sim (para o SCAP 1.0/1.1 XCCDF, mutuamente exclusivo com -scap e -oval/-variable) |
| `-oval [oval file]` | Especificar o arquivo OVAL | Sim (para o arquivo OVAL autônomo, mutuamente exclusivo com -xccdf e -scap) |
| `-variable [oval external variable file]` | Especificar o arquivo de variável externa OVAL | Não (opcional para o arquivo OVAL autônomo quando há um arquivo de variável OVAL externo, com exclusão mútua entre -xccdf e -scap) |
| `-select [xccdf benchmark/profile]` | Selecione o perfil de parâmetro de comparação do XCCDF do fluxo de dados do SCAP ou do arquivo XCCDF | Sim (uma seleção deve ser feita para gerar um relatório para que possamos combinar a linha de base do DCM correspondente no banco de dados do Configuration Manager) |
| `-out [output directory]` | Especificar o local para exportar o arquivo .cab de Configurações de conformidade | Não (se não for especificado, a ferramenta listará apenas o conteúdo sem conversão) |
| `-log [log file]` | Especificar o arquivo de log | Não (se não for especificado, o log será gravado no arquivo Microsoft.Sces.DcmToScap.log) |
| `-help` ou `-?` | Imprimir o uso da ferramenta | Não |

 > [!TIP]  
 > Você pode especificar o parâmetro `-?`, `–h` ou `–help` para exibir a sintaxe da ferramenta Microsoft.Sces.DcmToScap.exe e uma lista dos parâmetros.

Por padrão, a ferramenta Microsoft.Sces.DcmToScap.exe acessa o banco de dados do Configuration Manager usando suas credenciais. A ferramenta Microsoft.Sces.DcmToScap.exe requer um mínimo de acesso de leitura no banco de dados do Configuration Manager.

Depois de executar a ferramenta, verifique se os seguintes arquivos existem: 
- Relatório **ARF**: `_ARF_xxxx.xml_` e/ou relatório **legível por humanos**: `xxx.txt`
- Relatório **Cyberscope**: `LASR_xxx.xml`
- Relatório **ConsumedOval**: `xx-oval-<machineName>.xml`
- Relatório de **resultado do Parâmetro de Comparação XCCDF**: `xccdf_xxx.xml` 



## <a name="next-step"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Solução de problemas](/sccm/compliance/plan-design/scap/troubleshooting-scap)
