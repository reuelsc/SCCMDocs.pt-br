---
title: "Ferramenta de conexão de serviço"
titleSuffix: Configuration Manager
description: "Saiba mais sobre esta ferramenta que permite que você se conecte ao serviço de nuvem do Configuration Manager para carregar manualmente as informações de uso."
ms.custom: na
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
caps.latest.revision: "11"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: dda4a9b3977d55dbe3e2a0bf746a658eadc788d5
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="use-the-service-connection-tool-for-system-center-configuration-manager"></a>Usar a ferramenta de conexão de serviço do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use a **ferramenta de conexão de serviço** quando o ponto de conexão de serviço estiver no modo offline ou quando os servidores do sistema de site do Configuration Manager não estiverem conectados à Internet. A ferramenta pode ajudá-lo a manter o site atualizado com as atualizações mais recentes do Configuration Manager.  

Quando executada, a ferramenta permite que você se conecte manualmente ao serviço de nuvem do Configuration Manager para carregar as informações de uso da sua hierarquia e baixar atualizações. Carregar dados de uso é necessário para permitir que o serviço de nuvem forneça as atualizações corretas para sua implantação.  

## <a name="prerequisites-for-using-the-service-connection-tool"></a>Pré-requisitos para usar a ferramenta de conexão de serviço
A seguir estão os pré-requisitos e problemas conhecidos.

**Pré-requisitos:**

-   Você tem um ponto de conexão de serviço instalado e ele está definido como **Offline, conexão sob demanda**.  

-   A ferramenta deve ser executada em um prompt de comando.  

-   Cada computador no qual a ferramenta é executada (o computador de ponto de conexão de serviço e o computador conectado à Internet) deve ser um sistema x64 (64 bits) e ter os seguintes itens instalados:  

    -   Os arquivos x86 e x64 dos **Pacotes Redistribuíveis do Visual C++** .   Por padrão, o Configuration Manager instala a versão x64 no computador que hospeda o ponto de conexão de serviço.  

         Para baixar uma cópia dos arquivos do Visual C++, visite [Pacotes Redistribuíveis do Visual C++ para Visual Studio 2013](http://www.microsoft.com/download/details.aspx?id=40784) no Centro de Download da Microsoft.  

    -   .NET Framework 4.5.2 ou posteriores.  

-   A conta usada para executar a ferramenta deve ter:
    -   Permissões de**Administrador local** no computador que hospeda o ponto de conexão de serviço (no qual a ferramenta é executada).
    -   Permissões de**Leitura** para o banco de dados do site.  



-   Você precisará de uma unidade USB com espaço livre suficiente para armazenar os arquivos e as atualizações ou outro método para transferir arquivos entre o computador do ponto de conexão de serviço e o computador que tem acesso à Internet. (Este cenário pressupõe que seu site e os computadores gerenciados não têm conexão direta com a Internet).  



## <a name="use-the-service-connection-tool"></a>Usar a ferramenta de conexão de serviço  

 Você pode encontrar a ferramenta de conexão de serviço (**serviceconnectiontool.exe**) na mídia de instalação do Configuration Manager, na pasta **%path%\smssetup\tools\ServiceConnectionTool**. Sempre use a ferramenta de conexão de serviço que corresponde à versão do Configuration Manager que você usa.


 Neste procedimento, os exemplos de linha de comando usam os seguintes nomes de arquivo e locais de pasta (você não precisa usar estes caminhos e nomes de arquivos e pode usar alternativas que correspondem ao seu ambiente e preferências):  

-   O caminho para um cartão USB no qual os dados são armazenados para transferência entre servidores: **D:\USB\\**  

-   O nome do arquivo .cab que contém dados exportados do seu site: **UsageData.cab**  

-   O nome da pasta vazia na qual as atualizações baixadas do Configuration Manager serão armazenadas para transferência entre servidores: **UpdatePacks**  

No computador que hospeda o ponto de conexão de serviço:  

-   Abra um prompt de comando com privilégios administrativos e altere os diretórios para o local que contém **serviceconnectiontool.exe**.  

     Por padrão, você pode encontrar essa ferramenta na mídia de instalação do Configuration Manager, na pasta **%path%\smssetup\tools\ServiceConnectionTool**. Todos os arquivos nessa pasta devem estar na mesma pasta para a ferramenta de conexão de serviço funcionar.  

Quando você executa o comando a seguir, a ferramenta prepara um arquivo .cab que contém informações de uso e as copia para um local especificado por você. Os dados no arquivo .cab se baseiam no nível dos dados de uso do diagnóstico que seu site está configurado para coletar. (consulte [Dados de diagnóstico e de uso para o System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)).  Execute o seguinte comando para criar o arquivo .cab:  

-   **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

Você também precisará copiar a pasta ServiceConnectionTool com todo seu conteúdo para a unidade USB ou, de alguma forma, disponibilizá-lo no computador que usará para as etapas 3 e 4.  

### <a name="overview"></a>Visão geral
#### <a name="there-are-three-primary-steps-to-using-the-service-connection-tool"></a>Há três etapas principais para usar a ferramenta de conexão de serviço  

1.  **Preparação**: esta etapa deve ser executada no computador que hospeda o ponto de conexão de serviço. Ao ser executada, a ferramenta coloca os dados de uso em um arquivo .cab e os armazena em uma unidade USB (ou em algum local de transferência alternativo que você especificar).  

2.  **Conexão**: nesta etapa, a ferramenta será executada em um computador remoto que se conecta à Internet para carregar dados de uso e baixar atualizações.  

3.  **Importação**: esta etapa deve ser executada no computador que hospeda o ponto de conexão de serviço. Ao ser executada, a ferramenta importará as atualizações baixadas e as adicionará ao site, assim, elas poderão ser exibidas e instaladas por meio do console do Configuration Manager.  

A partir da versão 1606, ao se conectar à Microsoft, você pode carregar vários arquivos .cab ao mesmo tempo (cada um de uma hierarquia diferente) e especificar um servidor proxy e um usuário para o servidor proxy.   

#### <a name="to-upload-multiple-cab-files"></a>Para carregar vários arquivos .cab
 -  Coloque cada arquivo .cab que exportar de hierarquias separadas na mesma pasta. O nome de cada arquivo deve ser exclusivo e você pode renomeá-los manualmente se necessário.
 -  Depois, quando executar o comando para carregar dados para a Microsoft, especifique a pasta que contém os arquivos .cab. (Antes da atualização 1606, você só podia carregar dados de uma hierarquia por vez e a ferramenta exigia que você especificasse o nome do arquivo .cab na pasta.)
 -  Posteriormente, quando você executar a tarefa de importação no ponto de conexão de serviço de uma hierarquia, a ferramenta importará automaticamente somente os dados daquela hierarquia.  

#### <a name="to-specify-a-proxy-server"></a>Para especificar um servidor proxy
Você pode usar os seguintes parâmetros opcionais para especificar um servidor proxy (mais informações sobre como usar esses parâmetros estão disponíveis na seção Parâmetros de linha de comando neste tópico):
  - **-proxyserveruri [FQDN_do_servidor_proxy]**  Use este parâmetro para especificar o servidor proxy a ser usado para esta conexão.
  -  **-proxyusername [nome de usuário]**  Use este parâmetro quando precisar especificar um usuário para o servidor proxy.

#### <a name="specify-the-type-of-updates-to-download"></a>Especifique o tipo de atualizações a serem baixadas
A partir da versão 1706, o comportamento padrão dos downloads de ferramentas foi alterado e a ferramenta dá suporte a opções para controlar quais arquivos são baixados.
-   Por padrão, a ferramenta baixa somente a atualização mais recente disponível que se aplica à versão do seu site. Ela não baixa os hotfixes.

Para modificar esse comportamento, use um dos parâmetros a seguir para alterar quais arquivos são baixados. A versão do seu site é determinada pelos dados no arquivo .cab que é carregado quando a ferramenta é executada.
-   **-downloadall** Essa opção baixa tudo, incluindo atualizações e hotfixes, independentemente da versão do seu site.
-   **-downloadhotfix** Essa opção baixa todos os hotfixes, independentemente da versão do seu site.
-   **-downloadsiteversion** Essa opção baixa atualizações e hotfixes com uma versão maior do que a do seu site.

Linha de comando de exemplo que usa *-downloadsiteversion*:
- **serviceconnectiontool.exe -connect  *-downloadsiteversion* -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks**




### <a name="to-use-the-service-connection-tool"></a>Para usar a ferramenta de conexão de serviço  

1.  No computador que hospeda o ponto de conexão de serviço:  

    -   Abra um prompt de comando com privilégios administrativos e altere os diretórios para o local que contém **serviceconnectiontool.exe**.   

2.  Execute o comando a seguir para que a ferramenta prepare um arquivo .cab que contém informações de uso e copiá-las para um local especificado por você:  

    -   **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

    Se for carregar arquivos .cab de mais de uma hierarquia ao mesmo tempo, cada arquivo .cab na pasta deverá ter um nome exclusivo. Você pode renomear manualmente os arquivos que adicionar à pasta.

    Se quiser exibir as informações de uso coletadas para serem carregadas para o serviço de nuvem do Configuration Manager, execute o seguinte comando para exportar os mesmos dados como um arquivo .csv que você pode exibir usando um aplicativo como o Excel:  

    -   **serviceconnectiontool.exe -export -dest D:\USB\UsageData.csv**  

3.  Após a conclusão da etapa de preparação, mova a unidade USB (ou transfira os dados exportados por outro método) para um computador que tenha acesso à Internet.  

4.  No computador com acesso à Internet, abra um prompt de comando com privilégios administrativos e altere os diretórios para o local que contenha uma cópia da ferramenta  **serviceconnectiontool.exe** e os arquivos adicionais dessa pasta.  

5.  Execute o seguinte comando para iniciar o upload de informações de uso e o download de atualizações para o Configuration Manager:  

    -   **serviceconnectiontool.exe -connect -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks**

    Para obter mais exemplos dessa linha de comando, consulte a seção [Opções de linha de comando](../../../core/servers/manage/use-the-service-connection-tool.md#bkmk_cmd) mais adiante neste tópico.

    > [!NOTE]  
    >  Ao executar a linha de comando para se conectar ao serviço de nuvem do Configuration Manager, pode ocorrer um erro semelhante ao seguinte:  
    >   
    >  -   Exceção sem tratamento: System.UnauthorizedAccessException:  
    >   
    >      O acesso ao caminho “C:\  
    >     Users\br\AppData\Local\Temp\extractmanifestcab\95F8A562.sql” foi negado.  
    >   
    > Esse erro pode ser ignorado e você pode fechar a janela de erro e continuar.  

6.  Após a conclusão do download das atualizações para o Configuration Manager, mova a unidade USB (ou transfira os dados exportados por outro método) para o computador que hospeda o ponto de conexão de serviço.  

7.  No computador que hospeda o ponto de conexão de serviço, abra um prompt de comando com privilégios administrativos, altere os diretórios para o local que contém **serviceconnectiontool.exe**e execute o seguinte comando:  

    -   **serviceconnectiontool.exe -import -updatepacksrc D:\USB\UpdatePacks**  

8.  Após a conclusão da importação, você pode fechar o prompt de comando. (Apenas atualizações da hierarquia aplicável são importadas).  

9. Abra o console do Configuration Manager e navegue até **Administração** > **Atualizações e Manutenção**. As atualizações que foram importadas estão disponíveis agora para instalação. (Antes da versão 1702, Atualizações e Manutenção ficava em **Administração** > **Serviços de Nuvem**.)

 Para obter informações sobre a instalação de atualizações, consulte [Install in-console updates for System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md) (Instalar atualizações no console para o System Center Configuration Manager).  

## <a name="bkmk_cmd"></a> Opções de linha de comando  
 Para exibir informações de ajuda para a ferramenta de ponto de conexão de serviço, abra um prompt de comando para a pasta que contém a ferramenta e execute o comando:  **serviceconnectiontool.exe**.  

|Opções de linha de comando|Detalhes|  
|---------------------------|-------------|  
|**-prepare -usagedatadest [unidade:][caminho][nome do arquivo.cab]**|Este comando armazena dados de uso atual em um arquivo .cab.<br /><br /> Execute-o como **administrador local** no servidor que hospeda o ponto de conexão de serviço.<br /><br /> Exemplo:   **-prepare -usagedatadest D:\USB\Usagedata.cab**|    
|**-connect -usagedatasrc [unidade:][caminho] -updatepackdest [unidade:][caminho] -proxyserveruri [FQDN do servidor proxy] -proxyusername [nome de usuário]** <br /> <br /> Se usar uma versão do Configuration Manager anterior à 1606, você deverá especificar o nome do arquivo .cab e não será possível usar as opções de um servidor proxy.  Os parâmetros de comando com suporte são: <br /> **-connect -usagedatasrc [unidade:][caminho][nome de arquivo] -updatepackdest [unidade:][caminho]** |Esse comando conecta ao serviço de nuvem do Configuration Manager para carregar os arquivos .cab de dados de uso do local especificado e para baixar conteúdo do console e pacotes de atualização disponíveis. As opções para servidores proxy são opcionais.<br /><br /> Execute o comando como **administrador local** em um computador que possa se conectar à Internet.<br /><br /> Exemplo para se conectar sem um servidor proxy: **-connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks** <br /><br /> Exemplo para se conectar quando estiver usando um servidor proxy: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itgproxy.redmond.corp.microsoft.com -proxyusername Meg** <br /><br /> Se usar uma versão anterior à 1606, você deverá especificar um nome de arquivo para o arquivo .cab e não poderá especificar um servidor proxy. Use a seguinte linha de comando de exemplo: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks**|      
|**-import -updatepacksrc [unidade:][caminho]**|Este comando importa os pacotes de atualização e o conteúdo do console que você baixou anteriormente no seu console do Configuration Manager.<br /><br /> Execute-o como **administrador local** no servidor que hospeda o ponto de conexão de serviço.<br /><br /> Exemplo:  **-import -updatepacksrc D:\USB\UpdatePacks**|  
|**-export -dest [unidade:][caminho][nome do arquivo.csv]**|Este comando exporta os dados de uso para um arquivo .csv, que você poderá visualizar posteriormente.<br /><br /> Execute-o como **administrador local** no servidor que hospeda o ponto de conexão de serviço.<br /><br /> Exemplo: **-export -dest D:\USB\usagedata.csv**|  
