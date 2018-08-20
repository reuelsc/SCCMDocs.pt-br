---
title: Instalar e configurar extensões SCAP
titleSuffix: Configuration Manager
description: Instale e configure as extensões SCAP (Security Content Automation Protocol) para o Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: f53b484b-5123-48f0-be2f-4e30318f3d39
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4fd440905bb736dfbfac01de804373d29c9fbb59
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384607"
---
# <a name="install-and-configure-the-scap-extensions-for-configuration-manager"></a>Instalar e configurar as extensões SCAP para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Depois de [preparar a infraestrutura](/sccm/compliance/plan-design/scap/about-scap#bkmk_prepare), você está pronto para instalar e configurar as extensões SCAP para o Configuration Manager no computador no qual deseja executar esse processo.



## <a name="bkmk_install"></a> Instalar extensões SCAP

O arquivo de instalação está localizado no seguinte caminho no diretório de instalação no servidor do site do Configuration Manager:  
`cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi`

1. Copie **ConfigMgrExtensionsforSCAP.msi** para o computador com o console do Configuration Manager em que você deseja executar esse processo.  

2. No Windows Explorer, acesse a pasta em que você copiou o **ConfigMgrExtensionsforSCAP.msi**. Clique duas vezes no arquivo para abri-lo e iniciar as extensões SCAP para o assistente de instalação do Configuration Manager.  

3. Leia o Contrato de Licença. Clique em **Aceito os termos do contrato de licença** e, em seguida, clique em **Instalar**.  

4. Quando a instalação for concluída, clique em **Concluir** para fechar o assistente de instalação.  

O assistente de instalação instala as extensões SCAP na pasta de instalação do console do Configuration Manager. Por padrão, a pasta de instalação do console é `C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole`.  



## <a name="bkmk_scap-data-stream-files"></a> Baixe e instale os arquivos de fluxo de dados SCAP

Antes de executar as extensões SCAP, você precisa baixar os arquivos de fluxo de dados SCAP da [página de download](https://csrc.nist.gov/Projects/United-States-Government-Configuration-Baseline) do NVD (National Vulnerability Database). Em seguida, copie-as na pasta em que você instalou as extensões SCAP.

Dependendo do seu ambiente, talvez você não precise de todos os arquivos de fluxo de dados do SCAP listados na página de download.

### <a name="install-the-scap-data-streams"></a>Instalar os fluxos de dados SCAP

1. Visite o [Site da NVD](http://nvd.nist.gov/) para identificar os fluxos de dados do SCAP que são exigidos pela sua organização.
Os fluxos de dados do SCAP publicados pelo NIST são organizados em vários pacotes, que também são chamados de _listas de verificação_.  

2. Baixe os fluxos de dados do SCAP do [Site da NVD](http://nvd.nist.gov/home.cfm), que são armazenados em arquivos compactados com uma extensão de nome de arquivo .zip ou marcados como um arquivo XML do DataStream.  

    > [!IMPORTANT]  
    > Há vários arquivos de fluxo de dados do SCAP com a extensão .xml que podem ser baixados da NVD. No entanto, somente os arquivos .xml que incluem o conteúdo do XCCDF (SCAP 1.0 e 1.1)/DataStream (SCAP 1.2) são apropriados para serem usados com as extensões SCAP.  

3. Extraia os arquivos .zip dos fluxos de dados do SCAP ou o arquivo XML do DataStream que você baixou na mesma pasta em que instalou as extensões SCAP.  



## <a name="bkmk_convert-and-import"></a> Converter e importar os arquivos de fluxo de dados SCAP manualmente 

Depois de obter os fluxos de dados SCAP, você estará pronto para importar e converter os fluxos de dados em linhas de base de configuração. Os fluxos de dados do SCAP publicados pelo NIST são organizados em vários pacotes. Siga as instruções do NIST para verificar quais pacotes devem ser usados em seu ambiente. Por exemplo, há um pacote separado para cada versão do Windows, outro pacote específico da versão para a configuração de firewall e um pacote para o Internet Explorer. Use os procedimentos a seguir para realizar esta tarefa.  

> [!Note]  
> Esta seção descreve o processo manual para converter e importar os arquivos de fluxo de dados com o console do Configuration Manager. Para automatizar esse processo, confira a próxima seção para [Converter e importar automaticamente os arquivos de fluxo de dados SCAP](#bkmk_auto-convert-and-import).  

1. Clique no assistente para **Importar conteúdo SCAP** na faixa de opções do grupo de linha de base de configuração.

     ![Botão Importar conteúdo SCAP na faixa de opções do console](./media/import-scap-content.png)

2. Selecione a opção de conteúdo SCAP.

      ![Selecione a página de opções de conteúdo SCAP do assistente para importação](./media/import-new-scap-content.png)

3. Selecione o arquivo de fluxo de dados SCAP, o arquivo de dicionário XCCDF e CPE ou o arquivo de conteúdo Oval.

     ![Selecione o arquivo de fluxo de dados do SCAP](./media/select-datastream-file.png)

4. Se for o SCAP 1.2, selecione o fluxo de dados. Selecione o parâmetro de comparação e o perfil para o SCAP 1. x. Clique em **Avançar** para converter o conteúdo. 

      ![Selecione o parâmetro de comparação e o perfil para o SCAP 1.2](./media/select-benchmark-and-profile.png)

      > [!Tip]  
      > Esta página do assistente exibe a linha de comando que você usaria com a ferramenta **ScapToDcm.exe** para automatizar o mesmo processo.  

5. Confirme os dados de configuração a serem importados.

      ![Confirme a captura de tela de configuração](./media/confirm-configuration.png)

6. Clique em **Avançar** para importar os dados de configuração.

      ![Concluir a importação](./media/complete-import.png)



## <a name="bkmk_auto-convert-and-import"></a> Converter e importar automaticamente os arquivos de fluxo de dados SCAP 

### <a name="import-with-the-command-line-tool"></a>Importar com a ferramenta de linha de comando

Depois de obter os fluxos de dados SCAP, você poderá usar a ferramenta **Microsoft.Sces.ScapToDcm.exe** para converter os fluxos de dados SCAP em arquivos .cab que atendem às configurações de conformidade. Em seguida, importe os arquivos .cab no Configuration Manager. A ferramenta Microsoft.Sces.ScapToDcm.exe converte os fluxos de dados SCAP em itens de configuração e em linhas de base de configuração que você pode usar no Configuration Manager. A ferramenta Microsoft.Sces.ScapToDcm.exe converte os fluxos de dados do SCAP em manifestos XML. Ele, em seguida, empacota os manifestos XML em um arquivo .cab que você pode importar para o Configuration Manager.

> [!Tip]  
> A etapa 4 do processo manual na seção anterior mostra a página do assistente que exibe a linha de comando que você usaria com a ferramenta **ScapToDcm.exe** para automatizar o mesmo processo.  


#### <a name="use-microsoftscesscaptodcmexe-to-convert-scap-data-streams-into-cab-files"></a>Use Microsoft.Sces.ScapToDcm.exe para converter os fluxos de dados SCAP em arquivos .cab

No prompt de comando, acesse a pasta **AdminConsole\Bin** e execute **Microsoft.Sces.ScapToDcm.exe**. Essa ferramenta gera um arquivo .cab que atende às configurações de conformidade e o importa para o site do Configuration Manager.

   > [!NOTE]  
   > Sua conta precisa ter permissões de leitura/gravação para a pasta de saída.

**Uso para o conteúdo SCAP 1.0/1.1 (arquivo XML do XCCDF, como o conteúdo do USGCB e do DISA):**  

`Microsoft.Sces.ScapToDcm.exe –xccdf <xccdf.xml> -cpe <cpe.xml> -out <outputFolder> [-select benchmark/profile] [-log LogFileName]`  

   > [!NOTE]  
   > Se você não especificar o parâmetro de comparação ou o perfil usando o parâmetro `–select`, a ferramenta gerará um arquivo .cab para cada parâmetro de comparação no arquivo de conteúdo.  

**Uso para o conteúdo SCAP 1.2 (arquivo XML do DataStream, como o conteúdo mais recente do USGCB):**  

`Microsoft.Sces.ScapToDcm.exe –scap <scapdatastreamfile.xml> -out <outputFolder> [-select datastream/benchmark/profile] [-log LogFileName]`  

   > [!NOTE]  
   > Se você não especificar o datastream, o parâmetro de comparação ou o perfil usando o parâmetro `–select`, a ferramenta gerará um arquivo .cab para cada parâmetro de comparação no arquivo de conteúdo.

**Uso para um único arquivo OVAL com variáveis externas:**  

`Microsoft.Sces.ScapToDcm.exe –oval <singleOvalFile.xml> [-variable <externalVariableFile.xml>] -out <outputFolder> [-log LogFileName]`  

   > [!NOTE]  
   > Se houver vários valores para uma variável no arquivo de variável externa, a ferramenta Microsoft.Sces.ScapToDcm.exe tratará os valores como uma matriz para essa variável.  



#### <a name="microsoftscesscaptodcmexe-command-line-parameters"></a>Parâmetros da linha de comandos de Microsoft.Sces.ScapToDcm.exe

| Parâmetro | Uso | Necessária |
| --- | --- | --- |
| `-scap [scap data stream file]` | Especificar o arquivo de fluxo de dados do SCAP | Sim (para o fluxo de dados do SCAP 1.2, mutuamente exclusivo com -xccdf e -oval/-variable) |
| `-xccdf [xccdf file]` | Especifique o arquivo XCCDF | Sim (para o SCAP 1.0/1.1 XCCDF, mutuamente exclusivo com -scap e -oval/-variable) |
| `-cpe [cpe file]` | Especificar o arquivo CPE | Sim (para o SCAP 1.0/1.1 XCCDF, mutuamente exclusivo com -scap e -oval/-variable) |
| `-oval [oval file]` | Especificar o arquivo OVAL | Sim (para o arquivo OVAL autônomo, mutuamente exclusivo com -xccdf e -scap) |
| `-variable [oval external variable file]` | Especificar o arquivo de variável externa OVAL | Não (opcional para o arquivo OVAL autônomo quando há um arquivo de variável OVAL externo, com exclusão mútua entre -xccdf e -scap) |
| `-select [xccdf benchmark/profile]` | Selecione o perfil de parâmetro de comparação do XCCDF do fluxo de dados do SCAP ou do arquivo XCCDF | Nenhum (esse parâmetro não é obrigatório, mas é recomendado. Se ele não for especificado, a ferramenta gerará um arquivo cab para todos os perfis em todos os parâmetros de comparação/DataStream inseridos) |
| `-out [output directory]` | Especifique o local para salvar o arquivo cab do DCM | Não (se ele não for especificado, a ferramenta listará apenas o conteúdo sem conversão) |
| `-log [log file]` | Especificar o arquivo de log | Não (se ele não for especificado, o log será gravado no arquivo Microsoft.Sces.ScapToDcm.log) |
| `-help` ou `-?` | Imprimir o uso da ferramenta | Não |


#### <a name="microsoftscesscaptodcmexe-examples"></a>Exemplos de Microsoft.Sces.ScapToDcm.exe

**Conteúdo SCAP 1.2:**  

`Microsoft.Sces.ScapToDcm.exe –scap scap_gov.nist_USTCB-ie8.xml –out .\mytestfolder –select mySCAPDataStreamID/myBenchMarkID/myProfileID`  

**Conteúdo SCAP 1.0/1.1:**  

`Microsoft.Sces.ScapToDcm.exe–xccdf scap_gov.nist_Test-WinXP_xccdf.xml –cpe scap_gov.nist_Test-WinXP_cpe.xml –out .\mytestfolder –select XCCDFBenchmarkID/MyProfileID`  

**Conteúdo SCAP OVAL:**  

`Microsoft.Sces.ScapToDcm.exe –oval myOvalFile.xml –variable myOvalExternalVariableFile.xml –out .\mytestfolder`  


#### <a name="sample-output-from-microsoftscesscaptodcmexe"></a>Exemplo de saída do Microsoft.Sces.ScapToDcm.exe

```
  Compliance Settings compliant cab file created:

  Validate the schema of SCAP data stream file C:\24SCAP\BVT_Test_Data_Stream.xml

  Successfully validate the schema of SCAP data stream file C:\24SCAP\BVT_Test_Data_Stream.xml

  Process XCCDF Benchmark xccdf_tst.bvt_benchmark_Windows-F

  Process XCCDF Profile: xccdf_tst.bvt_profile_version_1.0.0.0-BVT Profile #1

  Process OVAL: scap_tst.bvt_comp_Windows-F-oval.xml

  Successfully finished process OVAL: scap_tst.bvt_comp_Windows-F-oval.xml

  Process OVAL: scap_tst.bvt_comp_Windows-F-cpe-oval.xml

  Successfully finished process OVAL: scap_tst.bvt_comp_Windows-F-cpe-oval.xml
   Process SCAP data stream: scap_tst.bvt_datastream_Windows-F.zip
    SCAP Data Stream: [scap_tst.bvt_datastream_Windows-F.zip]

  Version:        [1.2]

  Timestamp:      [2/24/2012]

  Use-case:       [CONFIGURATION]

  CPE Dictionary:  [scap_tst.bvt_comp_Windows-F-cpe-dictionary.xml]

  OVAL:              [Windows-F-cpe-oval.xml]
  Product name:    [National Institute of Standards and Technology]

  Product version: []

  Schema version:  [5.3]

  Timestamp:       [2/24/2012]

  XCCDF Benchmark: [xccdf_tst.bvt_benchmark_Windows-F]

  Version:       [v1.0.0.0]
   Update:        [http://usgcb.nist.gov]

  Timestamp:     [2/24/2012]

  Status:        [accepted]

  Status date:   [2/24/2012]

  Title:         [Ohh New BVT for SCAP 1.2]

 Description:   [My description]

  XCCDF Profile: [xccdf_tst.bvt_profile_version_1.0.0.0]
 
  OVAL:              [Windows-F-oval.xml]

   Product name:    [scaptool]

   Product version: []

   Schema version:  [5.4]

   Timestamp:       [2/24/2012]

  Start SCAP to DCM conversion...

  Processing SCAP data stream: scap_tst.bvt_datastream_Windows-F.zip

  Processing CPE dictionary: scap_tst.bvt_comp_Windows-F-cpe-dictionary.xml

  …

  Generating CI baseline cab file: C:\28\bbt\xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab

  Successfully generated CI baseline cab file: C:\28\bbt\xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab

  Successfully converted XCCDF profile: xccdf_tst.bvt_profile_version_1.0.0.0 into DCM baseline xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab
```


### <a name="import-the-cab-file"></a>Importar o arquivo .cab

A próxima etapa no processo é usar o console do Configuration Manager para importar os arquivos .cab que atendem às configurações de conformidade no Configuration Manager. Ao importar os arquivos .cab que você criou anteriormente neste processo, um ou mais itens de configuração e linhas de base de configuração são criados no banco de dados do Configuration Manager. Mais para frente no processo, você poderá implantar as linhas de base de configuração em coleções de dispositivos. Para obter mais informações, confira [Importar dados de configuração](/sccm/compliance/deploy-use/import-configuration-data).

O local do arquivo .cab que você já criou é a pasta especificada pelo parâmetro `–output` da ferramenta Microsoft.Sces.ScapToDcm.exe.

> [!IMPORTANT]  
> Repita esse processo para cada arquivo .cab que você já criou no processo. Há um arquivo .cab para cada perfil selecionado no arquivo XCCDF/DataStreamXML que você baixou do site do NVD. Você pode processar esses arquivos executando a ferramenta Microsoft.Sces.ScapToDcm.exe.  

A linha de base de configuração importada é somente leitura, seu status é *Habilitado* e seu estado implantado é *Não*. A propriedade **Data de Modificação** mostra a hora em que você importou a linha de base. O nome da linha de base de configuração é obtido da seção de nome de exibição do XML do XCCDF/Datastream. O nome é criado usando a convenção `ABC[XYZ]`, em que **ABC** é a ID de parâmetro de comparação do XCCDF e **XYZ** é a ID de perfil do XCCDF (se um perfil é selecionado).



## <a name="next-step"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Implantar e monitorar a conformidade com o SCAP e exportar resultados de conformidade](/sccm/compliance/plan-design/scap/deploy-monitor-export)
