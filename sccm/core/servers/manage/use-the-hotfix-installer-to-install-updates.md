---
title: Instalador de Hotfix | System Center Configuration Manager
description: "Saiba quando e como instalar atualizações usando o Instalador de Hotfix para o Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f3058277-c597-4dac-86d1-41b6f7e62b36
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 03940a499416ce4231bda5feb8a2e323abdff578


---
# <a name="use-the-hotfix-installer-to-install-updates-for-system-center-configuration-manager"></a>Usar o Instalador do Hotfix para instalar atualizações do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Algumas atualizações do System Center Configuration Manager não estão disponíveis no serviço de nuvem da Microsoft e são obtidas apenas fora de banda. Um exemplo é um hotfix de versão limitada para resolver um problema específico.   
Quando for necessário instalar uma atualização (ou um hotfix) que você receber da Microsoft e essa atualização tiver um nome de arquivo que termina com a extensão **.exe** (não **update.exe**), use o instalador de hotfix que é incluído com o download do hotfix em questão para instalar a atualização diretamente no servidor do site do Configuration Manager.  

 Se o arquivo de hotfix tiver a extensão de arquivo **.update.exe**, consulte [Usar a Ferramenta de Registro de Atualização para importar hotfixes para o System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).  

> [!NOTE]  
>  Este tópico fornece diretrizes gerais sobre como instalar os hotfixes que atualizam o System Center Configuration Manager. Para obter detalhes sobre uma atualização específica, consulte o artigo da KB (Base de Dados de Conhecimento) correspondente no Suporte da Microsoft.  

##  <a name="a-namebkmkoverviewa-overview-of-hotfixes-for-configuration-manager"></a><a name="bkmk_Overview"></a> Visão geral dos hotfixes do Configuration Manager  
 Os hotfixes do Configuration Manager são semelhantes aos de outros produtos da Microsoft, como o SQL Server, que contêm uma correção individual ou um pacote (um pacote cumulativo de atualizações de correções) e são descritos em um artigo da Base de Dados de Conhecimento da Microsoft.  

 Atualizações individuais incluem uma única atualização focada para uma versão específica do Configuration Manager.  
Os pacotes de atualização incluem várias atualizações para uma versão específica do Configuration Manager.  
Quando uma atualização for um pacote, você não poderá instalar atualizações individuais desse pacote.  

 Se você planejar criar implantações para instalar atualizações em computadores adicionais, será preciso instalar o pacote de atualização em um servidor do site de administração central ou em um servidor do site primário.  

 O seguinte acontece quando você executa o pacote de atualização:  

-   Ele extrai os arquivos de atualização para cada componente aplicável do pacote de atualização.  

-   Um assistente é iniciado para orientá-lo pelo processo para configurar as atualizações e as opções de implantação das atualizações.  

-   Ao concluir o assistente, as atualizações no pacote aplicável ao servidor do site são instaladas no servidor do site.  

O assistente também cria implantações que você pode usar para instalar as atualizações em computadores adicionais. Implante as atualizações em computadores adicionais usando um método de implantação com suporte, como um pacote de implantação de software ou o Microsoft System Center Updates Publisher 2011.  

 Quando o assistente é executado, ele cria um arquivo **.cab** no servidor do site para uso com o Updates Publisher 2011. Opcionalmente, é possível configurar o assistente para também criar um ou mais pacotes para a implantação de software. Você pode usar essas implantações para instalar atualizações em componentes, como clientes ou o console do Configuration Manager. Além disso, você pode instalar atualizações manualmente em computadores que não executam o cliente do Configuration Manager.  

 Os três grupos do Configuration Manager a seguir podem ser atualizados:  

-   Funções de servidor do Configuration Manager, que incluem:  

    -   Site de administração central  

    -   Site primário  

    -   Site secundário  

    -   Provedor de SMS remoto  

-   Console do Configuration Manager  

-   Cliente do Configuration Manager  

> [!NOTE]  
> As  **atualizações para funções de sistema de sites** (incluindo atualizações do banco de dados do site e pontos de distribuição baseados em nuvem) são instaladas como parte da atualização para serviços e servidores do site pelo gerenciador de componentes de site.  
>   
>  No entanto, os pontos de distribuição de recepção de atualizações são atendidos pelo gerenciador de distribuição, e não pelo gerenciador de componentes de site.  

 Cada pacote de atualização do Configuration Manager é um arquivo SFX (.exe autoextraível) que contém os arquivos necessários para instalar a atualização nos componentes aplicáveis do Configuration Manager. Normalmente, o arquivo SFX pode conter os arquivos a seguir.  

|Arquivo|Detalhes|  
|----------|-------------|  
|&lt;Versão do produto\>-QFE-KB&lt;ID do artigo da KB\>-&lt;plataforma\>-&lt;idioma\>.exe|Este é o arquivo de atualização. A linha de comando para este arquivo é gerenciada pelo Updatesetup.exe.<br /><br /> Por exemplo:<br />CM1511RTM-QFE-KB123456-X64-ENU.exe|  
|Updatesetup.exe|Esse wrapper. msi gerencia a instalação do pacote de atualização.<br /><br /> Quando você executa a atualização, o Updatesetup.exe detecta o idioma de exibição do computador onde ele é executado. Por padrão, a interface do usuário para a atualização está em inglês. No entanto, quando há suporte para o idioma de exibição, a interface do usuário é exibida no idioma local do computador.|  
|Licença_&lt;idioma\>.rtf|Quando aplicável, cada atualização contém um ou mais arquivos de licença para os idiomas com suporte.|  
|&lt;Product&updatetype>-&lt;versão do produto\>-&lt;ID do artigo da KB\>-&lt;plataforma\>.msp|Quando a atualização é aplicável ao console ou aos clientes do Configuration Manager, o pacote de atualização inclui arquivos separados do patch do Windows Installer (.msp).<br /><br /> Por exemplo:<br /><br /> **Atualização do console do Configuration Manager:** ConfigMgr1511-AdminUI-KB1234567-i386.msp<br /><br /> **Atualização do cliente:** ConfigMgr1511-client-KB1234567-i386.msp<br />ConfigMgr1511-client-KB1234567-x64.msp|  

 Por padrão, o pacote de atualização registra suas ações em um arquivo .log no servidor do site. O arquivo de log tem o mesmo nome do pacote de atualização e é gravado na pasta **%SystemRoot%/Temp** .  

 Quando você executa o pacote de atualização, ele extrai um arquivo com o mesmo nome do pacote de atualização para uma pasta temporária no computador e executa o Updatesetup.exe. Updatesetup.exe inicia a Atualização de Software para o Assistente do Configuration Manager &lt;versão do produto\> &lt;Número da KB\>.  

 Conforme for aplicável ao escopo da atualização, o assistente criará uma série de pastas na pasta de instalação do System Center Configuration Manager no servidor do site. A estrutura da pasta se parece com esta:   
 **\\\\&lt;Nome do servidor\>\SMS_&lt;Código do site\>\HotFix.\\&lt;Número da KB\>\\&lt;Tipo de atualização\>\\&lt;Plataforma\>**.  

 A tabela a seguir fornece detalhes sobre as pastas na estrutura de pasta:  

|Nome da pasta|Mais informações|  
|-----------------|----------------------|  
|&lt;Nome do servidor\>|Este é o nome do servidor do site em que você executa o pacote de atualização.|  
|SMS_&lt;Código do site\>|Este é o nome do compartilhamento da pasta de instalação do Configuration Manager.|  
|&lt;Número da KB\>|Este é o número de identificação do artigo da Base de Dados de Conhecimento para este pacote de atualização.|  
|&lt;Tipo de atualização\>|São os tipos de atualizações do Configuration Manager. O assistente cria uma pasta separada para cada tipo de atualização contida no pacote de atualização. Os nomes das pastas representam os tipos de atualização. Eles incluem o seguinte:<br /><br /> **Servidor**: inclui atualizações para servidores do site, servidores de banco de dados do site e computadores que executam o Provedor de SMS.<br /><br /> **Cliente**: inclui atualizações do cliente do Configuration Manager.<br /><br /> **AdminConsole**: inclui atualizações do console do Configuration Manager<br /><br /> Além dos tipos de atualização anteriores, o assistente cria uma pasta chamada **SCUP**. Essa pasta não representa um tipo de atualização, mas contém o arquivo .cab para o Updates Publisher.|  
|&lt;Plataforma\>|Esta é uma pasta específica de plataforma. Ela contém os arquivos de atualização que são específicos a um tipo de processador.  Essas pastas incluem:<br /><br />- x64<br /><br /> - I386|  

##  <a name="a-namebkmkinstalla-how-to-install-updates"></a><a name="bkmk_Install"></a> Como instalar atualizações  
 Para instalar atualizações, você deve primeiro instalar o pacote de atualização em um servidor do site. Quando você instala um pacote de atualização, ele inicia um assistente de instalação para a atualização em questão. Esse assistente faz o seguinte:  

-   extrai os arquivos de atualização  

-   ajuda você a configurar implantações  

-   instala as atualizações aplicáveis nos componentes de servidor do computador local  

Depois de instalar o pacote de atualização em um servidor do site, você poderá atualizar componentes adicionais do Configuration Manager. A tabela a seguir descreve as ações de atualização para esses diversos componentes:  

|Componente|Instruções|  
|---------------|------------------|  
|Servidor do site|Implante atualizações em um servidor de site remoto quando você não optar por instalar o pacote de atualização diretamente nesse servidor.|  
|Banco de dados do site|Para servidores de site remoto, implante atualizações do servidor que incluam uma atualização para o banco de dados do site se você não instalar o pacote de atualização diretamente nesse servidor de site remoto.|  
|Console do Configuration Manager|Após a instalação inicial do console do Configuration Manager, você poderá instalar atualizações do console do Configuration Manager em cada computador que executa o console. Não é possível modificar os arquivos de instalação do console do Configuration Manager para aplicar as atualizações durante a instalação inicial do console.|  
|Provedor de SMS remoto|Instale atualizações para cada instância do Provedor de SMS que é e executado em um computador que não seja do servidor do site em que você instalou o pacote de instalação.|  
|Clientes do Configuration Manager|Após a instalação inicial do cliente do Configuration Manager, você poderá instalar atualizações do cliente do Configuration Manager em cada computador que executa o cliente.|  

> [!NOTE]  
>  É possível implantar atualizações apenas em computadores que executam o cliente do Configuration Manager.  

 Se reinstalar um cliente, o console do Configuration Manager ou o Provedor de SMS, você também precisará reinstalar as atualizações desses componentes.  

 Use as informações nas seções a seguir para instalar atualizações em cada componente do Configuration Manager.  

###  <a name="a-namebkmkserversa-update-servers"></a><a name="bkmk_servers"></a> Atualizar servidores  
 As atualizações para servidores podem incluir atualizações para os **sites**, o **site database**e computadores que executam uma instância do **Provedor de SMS**:  

####  <a name="a-namebkmksitea-update-a-site"></a><a name="bkmk_site"></a> Atualizar um site  
 Para atualizar um site do Configuration Manager, você pode instalar o pacote de atualização diretamente no servidor do site ou pode implantar as atualizações em um servidor do site após instalar o pacote de atualização em um site diferente.  

 Quando você instala uma atualização em um servidor do site, o processo de instalação da atualização gerencia ações adicionais necessárias para aplicar a atualização, como atualizar funções do sistema de site. A exceção é o banco de dados do site. A seção a seguir contém informações sobre como atualizar o banco de dados do site.  

####  <a name="a-namebkmkdatabasea-update-a-site-database"></a><a name="bkmk_database"></a> Atualizar um banco de dados do site  
 Para atualizar o banco de dados do site, o processo de instalação executa um arquivo chamado **update.sql** no banco de dados do site. Você pode configurar o processo de atualização para atualizar automaticamente o banco de dados do site ou você pode atualizar manualmente esse banco de dados mais tarde.  

 **Atualização automática do banco de dados do site**  

 Quando você instala o pacote de atualização em um servidor do site, também pode optar por atualizar automaticamente o banco de dados do site quando a atualização do servidor for instalada. Essa decisão aplica-se somente ao servidor do site onde você instala o pacote de atualização e não se aplica a implantações criadas para instalar as atualizações em servidores de site remoto.  

> [!NOTE]  
>  Quando você opta por atualizar automaticamente o banco de dados do site, o processo atualiza um banco de dados independentemente de o banco de dados estar localizado no servidor do site ou em um computador remoto.  

> [!IMPORTANT]  
>  Antes de atualizar o banco de dados do site, crie um backup desse banco de dados. Não é possível desinstalar uma atualização para o banco de dados do site. Para obter informações sobre como criar um backup do Configuration Manager, consulte [Backup e recuperação para o System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  

 **Atualização manual do banco de dados do site**  

 Se você optar por não atualizar automaticamente o banco de dados do site ao instalar o pacote de atualização no servidor do site, a atualização do servidor não modificará o banco de dados no servidor do site onde o pacote de atualização é executado. No entanto, as implantações que usam o pacote que é criado para implantação de software ou que são instaladas sempre atualizam o banco de dados do site.  

> [!WARNING]  
>  Quando a atualização inclui atualizações para o servidor do site e o banco de dados do site, ela não funciona até que a atualização seja concluída para ambos. Até que a atualização seja aplicada ao banco de dados do site, o site ficará em um estado não compatível.  

 **Para atualizar manualmente um banco de dados do site:**  

1.  No servidor do site, interrompa o serviço SMS_SITE_COMPONENT_MANAGER e depois interrompa o serviço SMS_EXECUTIVE.  

2.  Feche o console do Configuration Manager.  

3.  Execute o script de atualização chamado **update.sql** no banco de dados desse site. Para obter informações sobre como executar um script para atualizar um banco de dados do SQL Server, veja a documentação da versão do SQL Server usada para o servidor de banco de dados do site.  

4.  Reinicie os serviços que foram interrompidos nas etapas anteriores.  

5.  Quando o pacote de atualização é instalado, ele extrai **update.sql** para o seguinte local no servidor do site: **\\\\&lt;Nome do Servidor\>\SMS_&lt;Código do Site\>\Hotfix\\&lt;Número da KB\>\update.sql**  

####  <a name="a-namebkmkprovidera-update-a-computer-that-runs-the-sms-provider"></a><a name="bkmk_provider"></a> Atualizar um computador que executa o Provedor de SMS  
 Depois de instalar um pacote de atualização que inclui atualizações para o Provedor de SMS, você deve implantar a atualização em cada computador que executa o Provedor de SMS. A única exceção a isso é a instância do Provedor de SMS instalada anteriormente no servidor do site onde você instalou o pacote de atualização. A instância local do Provedor de SMS no servidor do site é atualizada quando você instala o pacote de atualização.  

 Ao remover e depois reinstalar o Provedor de SMS em um computador, você deverá então reinstalar a atualização do Provedor de SMS nesse computador.  

###  <a name="a-namebkmkclientsa-update-clients"></a><a name="BKMK_clients"></a> Atualizar clientes  
 Ao instalar uma atualização que inclui atualizações do cliente do Configuration Manager, você tem a opção de atualizar os clientes automaticamente com a instalação da atualização ou atualizá-los manualmente posteriormente. Para obter mais informações sobre a atualização automática do cliente, consulte [Como atualizar clientes para computadores Windows](https://technet.microsoft.com/library/mt627885.aspx).  

 Você pode implantar atualizações usando o Updates Publisher ou um pacote de implantação de software, ou optar por instalar manualmente a atualização em cada cliente. Para obter mais informações sobre como usar implantações para instalar atualizações, consulte a seção [Implantar atualizações para o Configuration Manager](#BKMK_Deploy) neste tópico.  

> [!IMPORTANT]  
>  Quando, ao instalar atualizações para clientes, o pacote de atualização incluir atualizações de servidores, lembre-se de também instalar as atualizações de servidor no site primário ao qual os clientes são atribuídos.  

Para instalar manualmente a atualização do cliente, em cada cliente do Configuration Manager, execute **Msiexec.exe** e faça referência ao arquivo .msp de atualização do cliente específico à plataforma.  

 Por exemplo, você pode usar a seguinte linha de comando para uma atualização do cliente. Esta linha de comando executa o MSIEXEC no computador cliente e faz referência ao arquivo .msp extraído pelo pacote de atualização no servidor do site: **msiexec.exe /p \\\\&lt;ServerName\>\SMS_&lt;SiteCode\>\Hotfix\\&lt;KB Number\>\Client\\&lt;Platform\>\\&lt;msp\> /L\*v &lt;logfile\>REINSTALLMODE=mous REINSTALL=ALL**  

###  <a name="a-namebkmkconsolea-update-configuration-manager-consoles"></a><a name="BKMK_console"></a> Atualizar consoles do Configuration Manager  
 Para atualizar um console do Configuration Manager, instale a atualização no computador que executa o console após sua instalação ter sido concluída.  

> [!IMPORTANT]  
>  Quando você instala atualizações do console do Configuration Manager e o pacote de atualização inclui atualizações de servidores, instale as atualizações do servidor no site que você usa com o console do Configuration Manager.  

Se o computador que você atualizar executar o cliente do Configuration Manager:  

-   você poderá usar uma implantação para instalar a atualização. Para obter mais informações sobre como usar implantações para instalar atualizações, consulte a seção [Implantar atualizações para o Configuration Manager](#BKMK_Deploy) neste tópico.  

-   Se estiver conectado diretamente ao computador cliente, você poderá executar a instalação interativamente.  

-   Você pode instalar manualmente a atualização em cada computador. Para instalar manualmente a atualização do console do Configuration Manager, em cada computador que executa o console do Configuration Manager, você pode executar Msiexec.exe e fazer referência ao arquivo .msp de atualização do console do Configuration Manager.  

Por exemplo, você pode usar a seguinte linha de comando para atualizar um console do Configuration Manager. Esta linha de comando executa MSIEXEC no computador e faz referência ao arquivo .msp extraído pelo pacote de atualização no servidor do site: **msiexec.exe /p \\\\&lt;ServerName\>\SMS_&lt;SiteCode\>\Hotfix\\&lt;KB Number\>\AdminConsole\\&lt;Platform\>\\&lt;msp\> /L\*v &lt;logfile\>REINSTALLMODE=mous REINSTALL=ALL**  

##  <a name="a-namebkmkdeploya-deploy-updates-for-configuration-manager"></a><a name="BKMK_Deploy"></a> Implantar atualizações para o Configuration Manager  
 Depois de instalar o pacote de atualização em um servidor do site, você poderá usar um dos três métodos a seguir para implantar atualizações em computadores adicionais.  

###  <a name="a-namebkmkdeployscupa-use-updates-publisher-2011-to-install-updates"></a><a name="BKMK_DeploySCUP"></a> Usar o Updates Publisher 2011 para instalar atualizações  
 Quando você instala o pacote de atualização em um servidor do site, o assistente de instalação cria um arquivo de catálogo do Updates Publisher, que pode ser usado para implantar as atualizações nos computadores aplicáveis. O assistente sempre cria esse catálogo, mesmo quando você seleciona a opção **Usar pacote e programa para implantar esta atualização**.  

 O catálogo do Updates Publisher é chamado **SCUPCatalog.cab** e pode ser encontrado no seguinte local no computador em que é executado o pacote de atualização: **\\\\&lt;NomeDoServidor\>\SMS_&lt;CódigoDoSite\>\Hotfix\\&lt;Número da KB\>\SCUP\SCUPCatalog.cab**  

> [!IMPORTANT]  
>  Como o arquivo SCUPCatalog.cab é criado usando caminhos específicos para o servidor do site onde o pacote de atualização está instalado, ele não pode ser usado em outros servidores de site.  

 Concluído o assistente, você poderá importar o catálogo para o Updates Publisher e usar as atualizações de software do Configuration Manager para implantar as atualizações. Para obter informações sobre o Updates Publisher, consulte [Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkID=83449) na biblioteca do TechNet do System Center 2012.  

 Use o procedimento a seguir para importar o arquivo SCUPCatalog.cab no Updates Publisher e publicar as atualizações.  

##### <a name="to-import-the-updates-to-updates-publisher-2011"></a>Para importar as atualizações no Updates Publisher 2011  

1.  Inicie o console do Updates Publisher e clique em **Importar**.  

2.  Na página **Tipo de Importação** do Assistente para Importar Catálogo de Atualizações de Software, selecione **Especificar o caminho para o catálogo a ser importado**e especifique o arquivo SCUPCatalog.cab.  

3.  Clique em **Avançar**e em **Avançar** novamente.  

4.  Na caixa de diálogo **Aviso de Segurança - Validação de Catálogo** , clique em **Aceitar**. Depois de concluído, feche o assistente.  

5.  No console do Updates Publisher, selecione a atualização que deseja implantar e clique em **Publicar**.  

6.  Na página **Opções de Publicação** do Assistente para Publicar Atualizações de Software, selecione **Conteúdo Integral**e clique em **Avançar**.  

7.  Conclua o assistente para publicar as atualizações.  

###  <a name="a-namebkmkdeployswdista-use-software-deployment-to-install-updates"></a><a name="BKMK_DeploySWDist"></a> Usar a implantação de software para instalar atualizações  
 Quando você instala o pacote de atualização no servidor do site de um site primário ou no site de administração central, é possível configurar o assistente de instalação para criar pacotes de atualização para implantação de software. Você poderá implantar os pacotes na coleções de computadores que desejar atualizar.  

 Para criar um pacote de implantação de software, na página **Configurar Implantação de Atualização de Software** do assistente, selecione a caixa de seleção de cada tipo de pacote de atualização que você deseja atualizar. Os tipos disponíveis podem incluir servidores, consoles do Configuration Manager e clientes. Um pacote separado é criado para cada tipo de atualização que você seleciona.  

> [!NOTE]  
>  O pacote de servidores contém atualizações para os seguintes componentes:  
>   
>  -   Servidor do site  
>  -   Provedor de SMS  
>  -   Banco de dados do site  

 Em seguida, na página **Configurar Método de Implantação de Atualização de Software** do assistente, selecione a opção **Eu usarei a distribuição de software**. Essa seleção instrui o assistente para criar os pacotes de implantação de software.  

 Concluído o assistente, você pode exibir os pacotes que ele cria no console do Configuration Manager, no nó **Pacotes** no espaço de trabalho **Biblioteca de Software**. Você pode, então, usar seu processo padrão para implantar pacotes de software nos clientes do Configuration Manager. Quando um pacote é executado em um cliente, ele instala as atualizações dos componentes aplicáveis do Configuration Manager no computador cliente.  

 Para obter informações sobre como implantar pacotes em clientes do Configuration Manager, consulte [Pacotes e programas no System Center Configuration Manager](../../../apps/deploy-use/packages-and-programs.md).  

###  <a name="a-namebkmkdeploycollectionsa-create-collections-for-deploying-updates-to-configuration-manager"></a><a name="BKMK_DeployCollections"></a> Criar coleções para implantar atualizações no Configuration Manager  
 Você pode implantar atualizações específicas para clientes aplicáveis. As informações a seguir podem ajudá-lo a criar coleções de dispositivos para os diferentes componentes do Configuration Manager.  

|Componente do Configuration Manager|Instruções|  
|----------------------------------------|------------------|  
|Servidor do site de administração central|Criar uma consulta de associação direta e adicionar o computador do servidor do site de administração central.|  
|Todos os servidores de site primário|Criar uma consulta de associação direta e adicionar cada computador do servidor de site primário.|  
|Todos os servidores de site secundário|Criar uma consulta de associação direta e adicionar cada computador do servidor de site secundário.|  
|Todos os clientes x86|Crie uma coleção com os critérios de consulta a seguir:<br /><br /> **Selecione \* da junção interna SMS_G_System_SYSTEM de SMS_R_System em SMS_G_System_SYSTEM.ResourceID = SMS_R_System.ResourceId em que SMS_G_System_SYSTEM.SystemType = "PC baseado em x86"**|  
|Todos os clientes x64|Crie uma coleção com os critérios de consulta a seguir:<br /><br /> **Selecione \* da junção interna SMS_G_System_SYSTEM de SMS_R_System em SMS_G_System_SYSTEM.ResourceID = SMS_R_System.ResourceId em que SMS_G_System_SYSTEM.SystemType = "PC baseado em x64"**|  
|Todos os computadores que executam o console do Configuration Manager|Criar uma consulta de associação direta e adicionar cada computador.|  
|Computadores remotos que executam uma instância do Provedor de SMS|Criar uma consulta de associação direta e adicionar cada computador.|  

> [!NOTE]  
>  Para atualizar um banco de dados do site, implante a atualização para o servidor de site desse site.  

 Para obter informações sobre como criar coleções, consulte [Como criar coleções no System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  



<!--HONumber=Nov16_HO1-->


