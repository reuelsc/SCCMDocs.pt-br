---
title: Instalar e configurar extensões do SCAP (Protocolo de Automação do Conteúdo de Segurança)
titleSuffix: Configuraton Manager
description: Instalar e configurar as extensões do SCAP (Protocolo de Automação do Conteúdo de Segurança)
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: f53b484b-5123-48f0-be2f-4e30318f3d39
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 891d21b44ed6efca73413a46d0483519b76f9cae
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="install-and-configure-the-scap-extensions-for-microsoft-system-center-configuration-manager"></a>Instalar e configurar as Extensões do SCAP para o Microsoft System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

> [!Tip]  
> Esse recurso foi introduzido pela primeira vez na versão Technical Preview 1803 como um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features). Esta versão de pré-lançamento das extensões do SCAP pode ser instalada em todas as versões compatíveis no momento do branch atual do Configuration Manager e o LTSB 1606. O arquivo de instalação está localizado em cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi a partir da Technical Preview 1803.   

Depois de preparar a infraestrutura de pré-requisito, você estará pronto para instalar e configurar as Extensões do SCAP para o Microsoft System Center Configuration Manager no computador por meio do qual você deseja executar este processo.

## <a name="install-scap-extensions-configuration-manager"></a>Instalar as Extensões do SCAP do Configuration Manager

1. Execute o ConfigMgr\_Extensions\_for\_SCAP.msi para instalar a ferramenta.
2. No Windows Explorer, vá para a pasta na qual você baixou o arquivo **ConfigMgr\_Extensions\_for\_SCAP.msi** e clique duas vezes no arquivo **ConfigMgr\_Extensions\_for\_SCAP.msi**. Isso inicia o Assistente de Instalação das Extensões do SCAP para o Microsoft System Center Configuration Manager.

Conclua o **Assistente de Instalação das Extensões do SCAP para o Microsoft System Center Configuration Manager** usando as informações na tabela a seguir e aceitando os valores padrão do assistente, a menos que você precise especificá-los.

**Tabela 1.0** Processo do Assistente de Instalação das Extensões do SCAP para o Microsoft System Center Configuration Manager

| Nome da página do Assistente | Ação do usuário |
| --- | --- |
| Bem-vindo e Contrato de Licença de Usuário Final |1. Examine o contrato de licença|
| Bem-vindo e Contrato de Licença de Usuário Final|2. Clique em **Aceito os termos do Contrato de Licença**.|
| Bem-vindo e Contrato de Licença de Usuário Final|3. Clique em **Instalar**.|
| O Assistente de Instalação das Extensões do SCAP para o Microsoft System Center Configuration Manager é concluído |4. Clique em **Finalizar**.|
 



As Extensões do SCAP para o Assistente de Instalação do Microsoft System Center Configuration Manager instalam as extensões por padrão na pasta de instalação do console do Configuration Manager.



## <a name="download-and-install-the-scap-data-stream-files"></a>Baixar e instalar os arquivos de fluxo de dados do SCAP

Antes de executar as Extensões do SCAP para converter arquivos de fluxo de dados do SCAP e depois importá-los para o recurso de Configurações de conformidade, é necessário baixar os arquivos de fluxo de dados do SCAP na [página de download](http://nvd.nist.gov/fdcc/download_fdcc.cfm) do site da NVD (National Vulnerability Database). Em seguida, copie-os na pasta em que você instalou as Extensões do SCAP

Dependendo do seu ambiente, talvez você não precise de todos os arquivos de fluxo de dados do SCAP listados na página de download.

Para instalar os fluxos de dados do SCAP

1. Visite o [Site da NVD](http://nvd.nist.gov/) para identificar os fluxos de dados do SCAP que são exigidos pela sua organização.
Os fluxos de dados do SCAP publicados pelo NIST são organizados em vários pacotes, que também são chamados de _listas de verificação_.

2. Baixe os fluxos de dados do SCAP do [Site da NVD](http://nvd.nist.gov/home.cfm), que são armazenados em arquivos compactados com uma extensão de nome de arquivo .zip ou marcados como um arquivo XML do DataStream.

    >[!IMPORTANT] 
    >Há vários arquivos de fluxo de dados do SCAP com a extensão .xml que podem ser baixados da NVD. No entanto, somente os arquivos .xml que incluem o conteúdo do XCCDF (SCAP 1.0 e 1.1)/DataStream (SCAP 1.2) são apropriados para uso com as Extensões do SCAP.

3. Extraia os arquivos .zip dos fluxos de dados do SCAP/arquivo XML do DataStream que você baixou na mesma pasta em que você instalou as Extensões do SCAP.

## <a name="convert-and-import-the-scap-data-stream-files-using-the-import-scap-content-wizard"></a>Converter e importar os arquivos de fluxo de dados do SCAP usando o Assistente de Importação de Conteúdo do SCAP

Depois de obter os fluxos de dados do SCAP, você estará pronto para importar e converter os fluxos de dados em linhas de base de configuração. Os fluxos de dados do SCAP publicados pelo NIST são organizados em vários pacotes. Siga as instruções do NIST para verificar quais pacotes devem ser usados em seu ambiente. Por exemplo, há um pacote separado para cada versão do Windows, outro pacote específico da versão para a configuração de firewall e um pacote para o Internet Explorer 8.0. Use os procedimentos a seguir para realizar esta tarefa.

### <a name="to-import-the-scap-data-streams-into-configuration-manager"></a>Para importar os fluxos de dados do SCAP para o Configuration Manager

1. Inicie o Assistente de Importação do Conteúdo do SCAP na faixa de opções da linha de base de configuração.

     ![Iniciar o Assistente de Importação do Conteúdo do SCAP da faixa de opções de linha de base de CI](./media/import-scap-content.png)

2. Selecione o Tipo de Conteúdo.

      ![Selecione o Tipo de Conteúdo](./media/import-new-scap-content.png)

3. Selecione o arquivo de fluxo de dados do SCAP, XCCDF e arquivo de dicionário de CPE ou o arquivo de conteúdo Oval.

     ![Selecione o arquivo de fluxo de dados do SCAP](./media/select-datastream-file.png)

4. Se o SCAP 1.2 selecionar o fluxo de dados. Selecione o parâmetro de comparação e o perfil para o SCAP 1. x.  Selecione **Próximo** para converter o conteúdo. Você verá uma barra de progresso.

      ![Selecione o parâmetro de comparação e o perfil para o SCAP 1.2](./media/select-benchmark-and-profile.png)

5. Confirme os dados de configuração a serem importados.

      ![Confirme a captura de tela de configuração](./media/confirm-configuration.png)

6. Clique em **Próximo** para importar os dados de configuração.

      ![Concluir a importação](./media/complete-import.png)

## <a name="alternate-method-convert-and-import-the-scap-data-stream-files-using-the-cmd-line-tool"></a>(Método alternativo) Converter e importar os arquivos de fluxo de dados do SCAP usando a ferramenta de linha de cmd

Depois de obter os fluxos de dados do SCAP, você pode usar a ferramenta Microsoft.Sces.ScapToDcm.exe para converter os fluxos de dados do SCAP em arquivos .cab em conformidade com as Configurações de Conformidade. Em seguida, importe os arquivos .cab no Configuration Manager. A ferramenta Microsoft.Sces.ScapToDcm.exe converte os fluxos de dados do SCAP em itens de configuração e em linhas de base de configuração que você pode acessar usando o recurso de Configurações de conformidade no Configuration Manager. A ferramenta Microsoft.Sces.ScapToDcm.exe converte os fluxos de dados do SCAP em manifestos XML. Ele, em seguida, empacota os manifestos XML em um arquivo .cab que você pode importar para o Configuration Manager.

Os fluxos de dados do SCAP publicados pelo NIST são organizados em vários pacotes. Siga as instruções do NIST para verificar quais pacotes devem ser usados em seu ambiente. Por exemplo, há um pacote separado para cada versão do Windows, outro pacote específico da versão para a configuração de firewall e um pacote para o Internet Explorer 8.0. Use os procedimentos a seguir para realizar esta tarefa.





## <a name="to-import-the-scap-data-streams-into-configuration-manager"></a>Para importar os fluxos de dados do SCAP para o Configuration Manager

1. Converta os fluxos de dados do SCAP em um arquivo .cab compatível com as Configurações de conformidade.
2. Importe o arquivo .cab para o Configuration Manager.

### <a name="convert-the-scap-data-streams-into-compliance-settings-compliant-cab-files"></a>Converter os fluxos de dados do SCAP em arquivos .cab em conformidade com as Configurações de Conformidade

Antes de analisar e avaliar a conformidade dos seus sistemas, é necessário converter os fluxos de dados do SCAP no formato XML em manifestos XML em conformidade com os itens de configuração das Configurações de conformidade e com as linhas de base de configuração. A ferramenta Microsoft.Sces.ScapToDcm.exe converte os fluxos de dados do SCAP em manifestos XML. Ele, em seguida, empacota os manifestos XML em um arquivo .cab que você pode posteriormente importar para o Configuration Manager.

#### <a name="to-convert-the-scap-data-streams-into-compliance-settings-compliant-cab-files-using-the-microsoftscesscaptodcmexe-tool"></a>**Para converter os fluxos de dados do SCAP em arquivos .cab em conformidade com as Configurações de conformidade usando a ferramenta Microsoft.Sces.ScapToDcm.exe**

No prompt de comando, vá para a pasta AdminConsole\Bin, execute Microsoft.Sces.ScapToDcm.exe para gerar um arquivo cab em conformidade com as Configurações de Conformidade e importá-lo para o site do Configuration Manager.

   >[!NOTE] 
   > Sua conta deve ter permissões de leitura/gravação para a pasta de saída

**Para conteúdo do SCAP 1.0/1.1 (arquivo XML do XCCDF, como conteúdo do USGCB e DISA):**

 Microsoft.Sces.ScapToDcm.exe –xccdf &lt;xccdf.xml&gt; -cpe &lt;cpe.xml&gt; -out &lt;outputFolder&gt; [-select benchmark/profile] [-log LogFileName]

   >[!NOTE] 
   >Se você não especificar o parâmetro de comparação/perfil usando o parâmetro –select, a ferramenta gerará um arquivo .cab do DCM para cada parâmetro de comparação no arquivo de conteúdo.

**Para conteúdo do SCAP 1.2 (arquivo XML do DataStream, como o conteúdo mais recente do USGCB):**

Microsoft.Sces.ScapToDcm.exe –scap &lt;scapdatastreamfile.xml&gt; -out &lt;outputFolder&gt; [-select datastream/benchmark/profile] [-log LogFileName]

   >[!NOTE] 
   > Se você não especificar o fluxo de dados/parâmetro de comparação/perfil usando o parâmetro –select, a ferramenta gerará um arquivo cab do DCM para cada parâmetro de comparação no arquivo de conteúdo.

**Para um único arquivo OVAL com variáveis externas:**

Microsoft.Sces.ScapToDcm.exe –oval &lt;singleOvalFile.xml&gt; [-variable &lt;externalVariableFile.xml&gt;] -out &lt;outputFolder&gt; [-log LogFileName]

   >[!NOTE] 
   > Se houver vários valores para uma variável no arquivo de variável externa, a ferramenta Microsoft.Sces.ScapToDcm.exe tratará os valores como uma matriz para essa variável.



#### <a name="microsoftscesscaptodcmexe-command-line-parameters"></a>Microsoft.Sces.ScapToDcm.exe. Parâmetros da linha de comando

| **Parâmetro** | **Uso** | **Necessária** |
| --- | --- | --- |
| -scap [arquivo de fluxo de dados do SCAP] | Especificar o arquivo de fluxo de dados do SCAP | Sim (para o fluxo de dados do SCAP 1.2, mutuamente exclusivo com -xccdf e -oval/-variable) |
| -xccdf [arquivo xccdf] | Especifique o arquivo XCCDF | Sim (para o SCAP 1.0/1.1 XCCDF, mutuamente exclusivo com -scap e -oval/-variable) |
| -cpe [cpe file] | Especificar o arquivo CPE | Sim (para o SCAP 1.0/1.1 XCCDF, mutuamente exclusivo com -scap e -oval/-variable) |
| -oval [arquivo OVAL] | Especificar o arquivo OVAL | Sim (para o arquivo OVAL autônomo, mutuamente exclusivo com -xccdf e -scap) |
| -variable [arquivo de variável externa OVAL] | Especificar o arquivo de variável externa OVAL | Não (opcional para o arquivo OVAL autônomo quando há um arquivo OVAL de variável externa, mutuamente exclusivo com o -xccdf e -scap) |
| -select [xccdf benchmark/profile] | Selecione o perfil de parâmetro de comparação do XCCDF do fluxo de dados do SCAP ou do arquivo XCCDF | Não (Recomendamos especificar esta opção. Se não for especificado, a ferramenta gerará um arquivo .cab para todos os perfis em todos os parâmetros de comparação/DataStream inseridos) |
| -out [diretório de saída] | Especifique o local para salvar o arquivo cab do DCM | Não (se não for especificado, a ferramenta listará apenas o conteúdo sem conversão) |
| -log [arquivo de log] | Especificar o arquivo de log | Não (se não for especificado, o log será gravado no arquivo Microsoft.Sces.ScapToDcm.log) |
| -help/-? | Imprimir o uso da ferramenta | Não |





#### <a name="the-following-command-lines-are-samples-for-the-microsoftscesscaptodcmexe-tool"></a>As linhas de comando a seguir estão exemplos para a ferramenta Microsoft.Sces.ScapToDcm.exe:

**SCAP1.2 Content:**

  Microsoft.Sces.ScapToDcm.exe –scap scap\_gov.nist\_USTCB-ie8.xml –out .\mytestfolder –select mySCAPDataStreamID/myBenchMarkID/myProfileID

**SCAP1.0/1.1 Content:**

   Microsoft.Sces.ScapToDcm.exe–xccdf scap\_gov.nist\_Test-WinXP\_xccdf.xml –cpe scap\_gov.nist\_Test-WinXP\_cpe.xml –out .\mytestfolder –select XCCDFBenchmarkID/MyProfileID

**SCAP OVAL Content:**

  Microsoft.Sces.ScapToDcm.exe –oval myOvalFile.xml –variable myOvalExternalVariableFile.xml –out .\mytestfolder

**A saída a seguir é um exemplo da ferramenta Microsoft.Sces.ScapToDcm.exe:**

  Compliance Settings compliant cab file created:

  Validate the schema of SCAP data stream file C:\24SCAP\BVT\_Test\_Data\_Stream.xml

  Successfully validate the schema of SCAP data stream file C:\24SCAP\BVT\_Test\_Data\_Stream.xml

  Process XCCDF Benchmark xccdf\_tst.bvt\_benchmark\_Windows-F

  Process XCCDF Profile: xccdf\_tst.bvt\_profile\_version\_1.0.0.0-BVT Profile #1

  Process OVAL: scap\_tst.bvt\_comp\_Windows-F-oval.xml

  Successfully finished process OVAL: scap\_tst.bvt\_comp\_Windows-F-oval.xml

  Process OVAL: scap\_tst.bvt\_comp\_Windows-F-cpe-oval.xml

  Successfully finished process OVAL: scap\_tst.bvt\_comp\_Windows-F-cpe-oval.xml Process SCAP data stream: scap\_tst.bvt\_datastream\_Windows-F.zip SCAP Data Stream: [scap\_tst.bvt\_datastream\_Windows-F.zip]

  Version:        [1.2]

  Timestamp:      [2/24/2012]

  Use-case:       [CONFIGURATION]

  CPE Dictionary:  [scap\_tst.bvt\_comp\_Windows-F-cpe-dictionary.xml]

  OVAL:              [Windows-F-cpe-oval.xml] Product name:    [National Institute of Standards and Technology]

  Product version: []

  Schema version:  [5.3]

  Timestamp:       [2/24/2012]

  XCCDF Benchmark: [xccdf\_tst.bvt\_benchmark\_Windows-F]

  Version:       [v1.0.0.0] Update:        [http://usgcb.nist.gov]

  Timestamp:     [2/24/2012]

  Status:        [accepted]

  Status date:   [2/24/2012]

  Title:         [Ohh New BVT for SCAP 1.2]

 Description:   [My description]

  XCCDF Profile: [xccdf\_tst.bvt\_profile\_version\_1.0.0.0]
 
  OVAL:              [Windows-F-oval.xml]

   Product name:    [scaptool]

   Product version: []

   Schema version:  [5.4]

   Timestamp:       [2/24/2012]

  Start SCAP to DCM conversion...

  Processing SCAP data stream: scap\_tst.bvt\_datastream\_Windows-F.zip

  Processing CPE dictionary: scap\_tst.bvt\_comp\_Windows-F-cpe-dictionary.xml

  …

  Generating CI baseline cab file: C:\28\bbt\xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

  Successfully generated CI baseline cab file: C:\28\bbt\xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

  Successfully converted XCCDF profile: xccdf\_tst.bvt\_profile\_version\_1.0.0.0 into DCM baseline xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

## <a name="next-step"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Importar configurações de conformidade do SCAP e exportar resultados de conformidade](/sccm/compliance/plan-design/scap/import-scap-compliance-settings)
