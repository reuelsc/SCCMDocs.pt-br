---
title: Recursos no Technical Preview 1612
titleSuffix: Configuration Manager
description: Saiba mais sobre os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1612.
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bceab2e8-2f05-4a17-9ac8-a7a558670fb7
caps.latest.revision: 5
author: erikje
ms.author: erikje
manager: angrobe
ms.openlocfilehash: e0688c41978d95e0e1fd4da817e602a2c8a6483b
ms.sourcegitcommit: f65d4d24f0533e5e196ece0d8a4df0fb3e30eba1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="capabilities-in-technical-preview-1612-for-system-center-configuration-manager"></a>Funcionalidades do Technical Preview 1612 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*



Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1612. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview. Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.    


**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

## <a name="the-data-warehouse-service-point"></a>O ponto do Data Warehouse Service
Começando do Technical Preview versão 1612, o ponto do Data Warehouse Service permite armazenar e relatar dados históricos de longo prazo sobre sua implantação do Configuration Manager. Isso é possibilitado por meio de sincronizações automatizadas do banco de dados de site do Configuration Manager para um banco de dados de data warehouse. Essas informações estarão acessíveis no seu ponto do Reporting Services.

Por padrão, ao instalar a nova função do sistema de sites, o Configuration Manager cria o banco de dados de data warehouse para você em uma instância especificada do SQL Server. O data warehouse dá suporte a até 2 TB de dados, com carimbos de data e hora para controle de alterações.  Por padrão, os dados que são sincronizados no banco de dados do site incluem os grupos de dados para Dados Globais, Dados do Site, Global_Proxy, Dados de Nuvem e Exibições de Banco de Dados. Você também pode modificar o que é sincronizado para incluir tabelas adicionais ou excluir tabelas específicas dos conjuntos de replicação padrão.
Os dados padrão que são sincronizados incluam informações sobre:
- Integridade de infraestrutura
- Segurança
- Conformidade
- Malware   
- Implantações de software
- Detalhes de inventário (no entanto, o histórico de inventário não é sincronizado)

Além de instalar e configurar o banco de dados de data warehouse, vários novos relatórios são instalados para que você possa pesquisar e relatar esses dados com facilidade.

### <a name="data-warehouse-dataflow"></a>Fluxo de Dados do Data Warehouse   
![Datawarehouse_flow](./media/datawarehouse.png)

| Etapa         | Detalhes  |
|:------:|-----------|  
| **1**  |  O servidor do site transfere e armazena dados no banco de dados do site.  |  
| **2** |   O ponto do Data Warehouse Service obtém dados do banco de dados do site com base na sua agenda e configuração.  |  
| **3** |  O ponto do Data Warehouse Service transfere e armazena uma cópia dos dados sincronizados no banco de dados de data warehouse. |  
| **A** |  Usando relatórios internos, é criada uma solicitação dos dados, a qual é passada para o ponto do Reporting Services usando o SQL Server Reporting Services. |  
| **B** |   A maioria dos relatórios contém informações atuais, e tais solicitações são executadas no banco de dados do site. |  
| **C** | Quando um relatório solicita dados históricos usando um dos relatórios com uma *Categoria* de **Data Warehouse**, a solicitação é executada no banco de dados de data warehouse.   |  

### <a name="prerequisites-for-the-data-warehouse-service-point-and-database"></a>Pré-requisitos para o banco de dados e o ponto do Data Warehouse Service
- A hierarquia deve ter uma função do sistema de sites do ponto do Reporting Services instalada.
- O computador no qual você instala a função do sistema de sites requer o .NET Framework 4.5.2 ou posterior.
- A conta do computador no qual a função do sistema de sites será instalada deve ter permissões de administrador local no computador que hospedará o banco de dados de data warehouse.
- A conta administrativa usada para instalar a função do sistema de sites deve ser DBO na instância do SQL Server que hospedará o banco de dados de data warehouse.  
-  Há suporte para o banco de dados:
  - Com o SQL Server 2012 ou posterior, Enterprise ou Datacenter Edition.
  - Em uma instância padrão ou nomeada
  - Em um *Cluster do SQL Server*. Embora essa configuração provavelmente funcione, ela não foi testada e o suporte oferecido é o melhor esforço.
  - Quando localizado em conjunto com o banco de dados do site ou do Reporting Services. No entanto, recomendamos que ele seja instalado em um servidor separado.  
- A conta usada como a *Conta do Ponto do Reporting Services* deve ter a permissão **db_datareader** do banco de dados do data warehouse.  
- O banco de dados do site não tem suporte em um *Grupo de Disponibilidade AlwaysOn do SQL Server*.

### <a name="install-the-data-warehouse"></a>Instalar o data warehouse
Instale a função do sistema de sites do Data Warehouse em um site de administração central ou site primário usando o **Assistente para Adicionar Funções do Sistema de Site** ou o **Assistente para Criar Servidor do Sistema de Site**. Veja [Instalar funções do sistema de sites](/sccm/core/servers/deploy/configure/install-site-system-roles) para obter mais informações. Uma hierarquia dá suporte a várias instâncias dessa função, porém há suporte para apenas uma instância em cada site.  

Ao instalar a função, o Configuration Manager cria o banco de dados de data warehouse para você em uma instância especificada do SQL Server. Se você especificar o nome de um banco de dados existente (como você faria ao [mover o banco de dados de data warehouse para um novo SQL Server](#move-the-data-warehouse-database)), o Configuration Manager não criará um novo banco de dados, utilizando aquele que você especificou.

#### <a name="configurations-used-during-installation"></a>Configurações usadas durante a instalação
Use as informações a seguir para concluir a instalação da função do sistema de sites:

Página **Seleção de Função do Sistema**:  
Você deve instalar um ponto do Reporting Services para que o Assistente possa exibir uma opção para selecionar e instalar o ponto do Data Warehouse Service.

Página **Geral** ‑ As informações gerais a seguir são necessárias:
- **Configurações do banco de dados do Configuration Manager:**   
  - **Nome do Servidor** ‑ Especifique o FQDN do servidor que hospeda o banco de dados do site. Se você não usar uma instância padrão do SQL Server, deverá especificar a instância depois do FQDN no seguinte formato: ***&lt;Sqlserver_FQDN >\&lt;Nome_da_instância>***
  - **Nome do banco de dados** ‑ Especifique o nome do banco de dados do site.
  - **Verificar** – Clique em **Verificar** para certificar-se de que a conexão com o banco de dados do site foi bem-sucedida.
</br></br>
- **Configurações do banco de dados de data warehouse:**
  - **Nome do servidor** ‑ Especifique o FQDN do servidor que hospeda o banco de dados e o ponto do Data Warehouse Service. Se você não usar uma instância padrão do SQL Server, deverá especificar a instância depois do FQDN no seguinte formato: ***&lt;Sqlserver_FQDN >\&lt;Nome_da_instância>***
  - **Nome do banco de dados** ‑ Especifique o FQDN para o banco de dados de data warehouse.  O Configuration Manager criará o banco de dados com esse nome. Se você especificar um nome de banco de dados que já existe na instância do SQL Server, o Configuration Manager usará esse banco de dados.
  - **Verificar** – Clique em **Verificar** para certificar-se de que a conexão com o banco de dados do site foi bem-sucedida.

Página **Configurações de sincronização**:   
- **Configurações de dados:**
  - **Grupos de replicação a serem sincronizados** – Selecione os grupos de dados que você deseja sincronizar. Para obter informações sobre os diferentes tipos de grupos de dados, consulte [Replicação de banco de dados](/sccm/core/servers/manage/data-transfers-between-sites#a-namebkmkdbrepa-database-replication) e **Exibições distribuídas** em [Transferências de dados entre sites](/sccm/core/servers/manage/data-transfers-between-sites).
  - **Tabelas incluídas na sincronização** – Especifique o nome de cada tabela adicional que você deseja sincronizar. Separe várias tabelas usando uma vírgula. Essas tabelas serão sincronizadas no banco de dados do site, além dos grupos de replicação que você selecionar.
  - **Tabelas excluídas da sincronização** ‑ Especifique o nome das tabelas individuais dos grupos de replicação que você sincronizar. As tabelas especificadas serão excluídas da sincronização. Separe várias tabelas usando uma vírgula.
- **Configurações de sincronização:**
  - **Intervalo de sincronização (minutos)** ‑ Especifique um valor em minutos. Depois que o intervalo for atingido, uma nova sincronização é iniciada. Essa definição dá suporte a um intervalo de 60 a 1440 minutos (24 horas).
  - **Agenda** ‑ Especifique os dias que você deseja que a sincronização seja executada.

**Acesso de ponto de relatório**:   
Depois de instalar a função de data warehouse, verifique se a conta usada como a *Conta do Ponto do Reporting Services* tem a permissão **db_datareader** do banco de dados do data warehouse.

#### <a name="troubleshoot-installation-and-data-synchronization"></a>Solucionar problemas de sincronização de dados e instalação
Use os seguintes logs para investigar problemas com a instalação do ponto do Data Warehouse Service ou com a sincronização de dados:
- **DWSSMSI.log** e **DWSSSetup.log** ‑ Use esses logs para investigar erros ao instalar o ponto do Data Warehouse Service.
-   **Microsoft.ConfigMgrDataWarehouse.log** – Use este log para investigar a sincronização de dados entre o banco de dados do site e o banco de dados de data warehouse.

### <a name="reporting"></a>Relatórios
Depois de instalar uma função do sistema de sites do Data Warehouse, os seguintes relatórios estão disponíveis no seu ponto do Reporting Services com uma *Categoria* de **Data Warehouse:**

|Relatório                   | Detalhes                                  |
|-------------------------|------------------------------------------|
| **Relatório de Implantação de Aplicativos** | Exibe detalhes de implantação de aplicativo para um aplicativo e computador específicos.|
| **Endpoint Protection e Relatório de Conformidade de Atualização de Software**   | Exibe computadores com atualizações de software ausentes.|
| **Relatório Geral do Inventário de Hardware**  | Exibe todo o inventário de hardware para um computador específico.|
| **Relatório Geral do Inventário de Software**  | Exibe todo o inventário de software para um computador específico.|
| **Visão Geral de Integridade de Infraestrutura**  |Exibe uma visão geral da integridade da infraestrutura do seu Configuration Manager.|
| **Lista de Malwares Detectados**  |Exibe os malwares que foram detectados na sua organização.|
| **Relatório de Resumo de Distribuição de Software** | Um resumo da distribuição de software para um anúncio e computador específicos.|

### <a name="move-the-data-warehouse-database"></a>Mover o banco de dados de data warehouse
Use as seguintes etapas para mover o banco de dados de data warehouse para um novo SQL Server:

  1. Examine a configuração de banco de dados atual e registre os detalhes de configuração, incluindo:  
   - Os grupos de dados que você deseja sincronizar
   - As tabelas que devem ser incluídas ou excluídas da sincronização       

   Você reconfigurará essas tabelas e grupos de dados após restaurar o banco de dados para um novo servidor e reinstalar a função do sistema de sites.  

  2. Use o SQL Server Management Studio para fazer backup do banco de dados de data warehouse e clique novamente para restaurar o banco de dados para um SQL Server no novo computador que hospedará o data warehouse.

  Depois de restaurar o banco de dados para o novo servidor, verifique se as permissões de acesso ao novo banco de dados de data warehouse são as mesmas do original.

  3. Use o console do Configuration Manager para remover a função do sistema de sites do ponto do Data Warehouse Service do servidor atual.

  4. Instale um novo ponto de Data Warehouse Service e especifique o nome do novo SQL Server e a instância que hospeda o banco de dados de data warehouse restaurado.

  5. A movimentação será concluída depois de instalar a função do sistema de sites.

Você pode examinar os seguintes logs do Configuration Manager para confirmar se a função do sistema de site foi reinstalada com êxito:  
- **DWSSMSI.log** e **DWSSSetup.log** ‑ Use esses logs para investigar erros ao instalar o ponto do Data Warehouse Service.
-   **Microsoft.ConfigMgrDataWarehouse.log** – Use este log para investigar a sincronização de dados entre o banco de dados do site e o banco de dados de data warehouse.


## <a name="content-library-cleanup-tool"></a>Ferramenta de Limpeza da Biblioteca de Conteúdo
Começando do Technical Preview versão 1612, você pode usar uma nova ferramenta de linha de comando (**ContentLibraryCleanup.exe**) para remover o conteúdo que não está mais associado a nenhum pacote ou aplicativo de um ponto de distribuição (conteúdo órfão). Essa ferramenta é chamada de ferramenta de limpeza da biblioteca de conteúdo.

Essa ferramenta só afeta o conteúdo do ponto de distribuição que você especificar ao executá-la e não é possível remover o conteúdo da biblioteca de conteúdo no servidor do site.

Depois de instalar o Technical Preview 1612, você poderá encontrar o **ContentLibraryCleanup.exe** na pasta *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* no servidor do site do Technical Preview.

A ferramenta lançada com esse Technical Preview visa substituir as versões mais antigas de ferramentas similares lançadas para os produtos anteriores do Configuration Manager. Embora esta versão da ferramenta deixe de funcionar após 1º de março de 2017, novas versões serão lançadas com futuros Technical Previews até que essa ferramenta seja lançada como parte do Branch Atual ou de uma versão fora de banda pronta para produção.

### <a name="requirements"></a>requisitos  
 - A ferramenta pode ser executada diretamente no computador que hospeda o ponto de distribuição, ou remotamente de outro servidor. A ferramenta só pode ser executada em um único ponto de distribuição por vez.
 - A conta de usuário que executa a ferramenta diretamente deve ter permissões de administração baseada em funções equivalentes a um Administrador Completo na hierarquia do Configuration Manager.  A ferramenta não funcionará quando a conta de usuário tiver as permissões como um membro de um grupo de segurança do Windows que contém as permissões de Administrador Completo.

### <a name="modes-of-operation"></a>Modos de operação
A ferramenta pode ser executada em dois modos:
  1.    **Modo de hipóteses**:   
      Quando você não especifica a opção **/delete**, a ferramenta é executada no modo de hipóteses e identifica o conteúdo que seria excluído do ponto de distribuição, mas não exclui efetivamente nenhum dado.

      - Quando a ferramenta é executada nesse modo, as informações sobre o conteúdo que seria excluído são automaticamente gravadas no arquivo de log da ferramenta. Não é solicitado que o usuário confirme cada exclusão em potencial.
      - Por padrão, o arquivo de log é gravado na pasta temp dos usuários no computador em que a ferramenta é executada, no entanto, você pode usar a opção /log para redirecionar o arquivo de log para outro local.  
      </br>

    Recomendamos que você execute a ferramenta nesse modo e examine o arquivo de log resultante antes de executar a ferramenta com a opção /delete.  

  2. **Modo de exclusão**: quando você executa a ferramenta com a opção **/delete**, ela é executada no modo de exclusão.

     - Quando a ferramenta é executada nesse modo, o conteúdo órfão encontrado no ponto de distribuição especificado pode ser excluído da biblioteca de conteúdo do ponto de distribuição.
     -  Antes de excluir cada arquivo, é solicitado que o usuário confirme se o arquivo deve ser excluído.  Você pode selecionar, **Y** para sim, **N** para não ou **Sim para todos** para ignorar as futuras solicitações e excluir todo o conteúdo órfão.  
     </br>

     Recomendamos que você execute a ferramenta no modo de hipóteses modo e examine o arquivo de log resultante antes de executar a ferramenta com a opção /delete.  

Quando a ferramenta de limpeza da biblioteca de conteúdo é executada em um desses modos, ela cria automaticamente um log com um nome que inclui o modo no qual ela foi executada, o nome do ponto de distribuição, a data e a hora da operação. O arquivo de log é aberto automaticamente quando a ferramenta é concluída. Por padrão, esse log é gravado na pasta **temp** dos usuários no computador em que a ferramenta é executada, no entanto, você pode usar a opção de linha de comando para redirecionar o arquivo de log para outro local, inclusive para um compartilhamento de rede.   


### <a name="run-the-tool"></a>Executar a ferramenta
Para executar a ferramenta:
1. abra um prompt de comando administrativo para uma pasta que contém **ContentLibraryCleanup.exe**.  
2. Em seguida, insira uma linha de comando que inclui as opções de linha de comando necessárias e os comutadores opcionais que você deseja usar.

**Problema conhecido** Quando a ferramenta é executada, um erro semelhante ao seguinte pode ser retornado quando qualquer pacote ou implantação tiver falhado ou estiver em andamento:
-  *System.InvalidOperationException: esta biblioteca de conteúdo não pode ser limpa no momento porque o pacote <packageID> não está totalmente instalado.*

**Solução alternativa:** nenhuma. A ferramenta não é confiável para identificar arquivos órfãos quando o conteúdo está em andamento ou não pôde ser implantado. Portanto, a ferramenta não permitirá que você limpe conteúdo até que esse problema seja resolvido.



### <a name="command-line-switches"></a>Opções de linha de comando  
As opções de linha de comando a seguir podem ser usadas em qualquer ordem.   

|Alternar|Detalhes|
|---------|-------|
|**/delete**  |**Opcional** </br> Use essa opção quando você desejar excluir o conteúdo do ponto de distribuição. Você será perguntado antes do conteúdo ser efetivamente excluído. </br></br> Quando essa opção não for usada, a ferramenta registra os resultados de qual conteúdo seria excluído, mas não exclui nenhum conteúdo do ponto de distribuição. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**Opcional** </br> Execute a ferramenta no modo silencioso, o qual suprime todos os avisos (como avisos de quando você estiver excluindo conteúdo) e não abre automaticamente o arquivo de log. </br></br> Exemplo: ***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;FQDN do ponto de distribuição>**  | **Necessária** </br> Especifique o FQDN (nome de domínio totalmente qualificado) do ponto de distribuição que você deseja limpar. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/ps &lt;FQDN do site primário>**       | **Opcional** ao limpar o conteúdo de um ponto de distribuição em um site primário.</br>**Obrigatório** ao limpar o conteúdo de um ponto de distribuição em um site secundário. </br></br> Especifique o FQDN do site primário ao qual o ponto de distribuição pertence, ou do pai primário quando o ponto de distribuição estiver em um site secundário. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;código do site primário>**  | **Opcional** ao limpar o conteúdo de um ponto de distribuição em um site primário.</br>**Obrigatório** ao limpar o conteúdo de um ponto de distribuição em um site secundário. </br></br> Especifique o código do site primário ao qual o ponto de distribuição pertence, ou do site pai primário quando o ponto de distribuição estiver em um site secundário.</br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log <log file directory>**       |**Opcional** </br> Especifique um diretório no qual os arquivos de log serão colocados. Ele pode ser uma unidade local ou um compartilhamento de rede.</br></br> Quando essa opção não for usada, os arquivos de log são colocados automaticamente na pasta temp dos usuários.</br></br> Exemplo de unidade local: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>Exemplo de compartilhamento de rede: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\&lt;share>\&lt;folder>***|


## <a name="improvements-for-in-console-search"></a>Melhorias da pesquisa no console
Com base nos comentários do User Voice, adicionamos as seguintes melhorias à pesquisa no console:
 - **Caminho do Objeto:**  
  Muitos objetos agora dão suporte a uma nova coluna chamada **Caminho do Objeto**.  Quando você pesquisar e incluir essa coluna nos resultados da exibição, poderá exibir o caminho para cada objeto. Por exemplo, se você executar uma pesquisa por aplicativos no nó Aplicativos e também pesquisar nos subnós, a coluna *Caminho do Objeto* no painel de resultados mostrará o caminho para cada objeto retornado.   

- **Preservação do texto de pesquisa:**  
  Quando você inserir texto na caixa de texto de pesquisa e alternar entre a pesquisa de um subdiretório e o nó atual, o texto digitado persistirá e permanecerá disponível para uma nova pesquisa, sem a necessidade de redigitá-lo.

- **Preservação da sua decisão de pesquisar subnós:**  
 A opção selecionada para a pesquisa no *nó atual* ou em *todos os subnós* agora é mantida após alterar o nó no qual você está trabalhando.   Esse novo comportamento significa que você não precisa redefinir constantemente a decisão ao percorrer o console.  Ao abrir o console, a opção padrão é pesquisar somente o nó atual.

## <a name="prevent-installation-of-an-application-if-a-specified-program-is-running"></a>Impedir a instalação de um aplicativo se um programa especificado estiver em execução.
Agora você poderá configurar uma lista de arquivos executáveis (com a extensão .exe) nas propriedades de tipo de implantação que, se estiverem em execução, bloquearão a instalação de um aplicativo. Após a tentativa de instalação, os usuários verão uma caixa de diálogo solicitando que os processos que estão bloqueando a instalação sejam fechados.

### <a name="try-it-out"></a>Experimente
Para configurar uma lista de arquivos executáveis
1.  Na página de propriedades de qualquer tipo de implantação, escolha a guia **Tratamento do Instalador**.
2.  Clique em **Adicionar** para adicionar um ou mais arquivos executáveis à lista (por exemplo **Edge.exe**)
3.  Clique em **OK** para fechar a caixa de diálogo Propriedades do tipo de implantação.

Agora, quando você implantar esse aplicativo em um usuário ou dispositivo e um dos executáveis adicionados estiver em execução, o usuário final verá uma caixa de diálogo do Centro de Software informando que a instalação falhou porque um aplicativo está em execução.

## <a name="new-windows-hello-for-business-notification-for-end-users"></a>Nova notificação do Windows Hello para Empresas para usuários finais

Uma nova notificação do Windows 10 informa aos usuários finais que eles devem executar ações adicionais para concluir a instalação do Windows Hello para Empresas (por exemplo, definir um PIN).

## <a name="windows-store-for-business-support-in-configuration-manager"></a>Suporte da Windows Store para Empresas no Configuration Manager

Agora você pode implantar aplicativos licenciados online com a finalidade da implantação **Disponível** da Windows Store para Empresas para computadores que executam o cliente do Configuration Manager.
Para ver mais detalhes, confira [Gerenciar aplicativos da Windows Store para Empresas com o System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

Suporte para esse recurso só está disponível para computadores que executam a versão prévia do Windows 10 RS2.

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Retornar à página anterior quando uma sequência de tarefas falhar
Agora, você pode retornar à página anterior ao executar uma sequência de tarefas e ocorrer uma falha. Antes dessa versão, era necessário reiniciar a sequência de tarefas ao ocorrer uma falha. Por exemplo, você pode usar o botão **Anterior** nos seguintes cenários:

- Quando um computador é iniciado no Windows PE, a caixa de diálogo de inicialização da sequência de tarefas pode ser exibida antes da sequência estar disponível. Ao clicar em Avançar nesse cenário, a página final da sequência de tarefas exibe uma mensagem informando que não há sequências de tarefas disponíveis. Agora, você pode clicar em **Anterior** para pesquisar novamente por sequências de tarefas disponíveis. Você pode repetir esse processo até que a sequência de tarefas esteja disponível.
- Quando você executa uma sequência de tarefas, porém pacotes dependentes de conteúdo ainda não estão disponíveis nos pontos de distribuição, a sequência de tarefas falhará. Agora, você poderá distribuir o conteúdo ausente (se ainda não tiver sido distribuído) ou aguardar o conteúdo estar disponível nos pontos de distribuição e, em seguida, clicar em **Anterior** para que a pesquisa de sequência de tarefas pesquise novamente o conteúdo.

## <a name="express-installation-files-support-for-windows-10-updates"></a>Suporte dos arquivos de instalação expressa para atualizações do Windows 10
Adicionamos o suporte a arquivos de instalação expressa no Configuration Manager para atualizações do Windows 10. Ao usar uma versão do Windows 10 com suporte, agora você poderá usar as definições do Configuration Manager para baixar somente a diferença entre a Atualização Cumulativa do Windows 10 do mês atual e a atualização do mês anterior. Atualmente, no Branch Atual do Configuration Manager, a Atualização Cumulativa do Windows 10 (incluindo todas as atualizações dos meses anteriores) é baixada a cada mês. Usar arquivos de instalação expressa proporciona downloads menores e instalações mais rápidas nos clientes.

> [!IMPORTANT]
> Embora as configurações para dar suporte ao uso de arquivos de instalação expressa estejam disponíveis no Configuration Manager, apenas há suporte para esta funcionalidade no Windows 10 versão 1607 com uma atualização do Windows Update Agent que será lançada em 10 de janeiro de 2017 (corrigir terça-feira). Para obter mais informações sobre essas atualizações, consulte o [artigo de suporte 3213986](https://support.microsoft.com/help/4009938/january-10-2017-kb3213986-os-build-14393-693). Você pode tirar proveito dos arquivos de instalação expressa quando o próximo conjunto de atualizações for lançado em 14 de fevereiro de 2017. O Windows 10 versão 1607 sem a atualização de versão e versões anteriores não dão suporte a arquivos de instalação expressa.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>Para habilitar o download de arquivos de instalação expressa para atualizações do Windows 10 no servidor
Para começar a sincronizar os metadados para arquivos de instalação expressa do Windows 10, você deve habilitá-la nas Propriedades do Ponto de Atualização de Software.
1.  No console do Configuration Manager, navegue até **Administração** > **Configuração de Site** > **Sites**.
2.  Selecione o site de administração central ou um site primário autônomo.
3.  Na guia **Início** , no grupo **Configurações** , clique em **Configurar Componentes do Site**e **Ponto de Atualização de Software**. Na guia **Arquivos de Atualização**, selecione **Baixar arquivos completos para todas as atualizações aprovadas e arquivos de instalação expressa para o Windows 10**.

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>Para habilitar o suporte para clientes baixarem e instalarem os arquivos de instalação expressa
Para habilitar o suporte a arquivos de instalação expressa nos clientes, você deve habilitar os arquivos de instalação expressa em clientes na seção Atualizações de Software das configurações do cliente. Isso cria um novo ouvinte HTTP que escuta solicitações para baixar arquivos de instalação expressa na porta que você especificar. Depois de implantar as configurações de cliente para habilitar essa funcionalidade no cliente, ele tentará baixar a diferença entre a Atualização Cumulativa do Windows 10 do mês atual e a atualização do mês anterior (os clientes devem executar uma versão do Windows 10 com suporte a arquivos de instalação expressa).
1.  Habilite o suporte a arquivos de instalação expressa nas propriedades do Componente de Ponto de Atualização de Software (procedimento anterior).
2.  No console do Configuration Manager, navegue para **Administração** > **Configurações do Cliente**.
3.  Selecione as configurações de cliente apropriadas e, em seguida, na guia **Início**, clique em **Propriedades**.
4.  Selecione a página **Atualizações de Software**, defina **Sim** para a configuração **Habilitar instalação de Atualizações Expressas em clientes** e configure a porta usada pelo ouvinte HTTP no cliente para a configuração **Porta usada para baixar o conteúdo para as Atualizações Expressas**.


## <a name="odata-endpoint-data-access"></a>Acesso a dados do ponto de extremidade OData

 Agora, o Configuration Manager fornece um ponto de extremidade RESTful OData para acessar dados do Configuration Manager. O ponto de extremidade é compatível com Odata versão 4, que permite que ferramentas como o Excel e o Power BI acessem facilmente os dados do Configuration Manager por meio de um único ponto de extremidade Odata. O Technical Preview 1612 dá suporte apenas a acesso de leitura aos objetos no Configuration Manager.  

Os dados disponíveis no momento no [Provedor WMI do Configuration Manager](/sccm/develop/reference/configuration-manager-reference) agora também estão acessíveis com o novo ponto de extremidade OData RESTful. Os conjuntos de entidades expostos pelo ponto de extremidade OData permitem enumerar os mesmos dados que você pode consultar com o provedor WMI.

### <a name="try-it-out"></a>Experimente

Antes de usar o ponto de extremidade OData, você deve habilitá-lo para o site.

1.  Navegue para **Administração** > **Configuração do Site** > **Sites**.
2.  Selecione o site primário e clique em **Propriedades**.
3.  Na guia Geral da folha de propriedades do site primário, clique em **Habilitar ponto de extremidade REST para todos os provedores neste site** e, em seguida, clique em **OK**.

Em seu visualizador de consulta OData favorito, experimente consultas semelhantes aos exemplos a seguir para retornar vários objetos no Configuration Manager:

| Finalidade | Consulta OData |
|---|---|
| Obter todas as coleções | `http://localhost/CMRestProvider/Collection` |
| Obter uma coleção | `http://localhost/CMRestProvider/Collection('SMS00001')`
| Obter os 100 primeiros dispositivos na coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/Device?$top=100` |
| Obter um dispositivo com uma ID de recurso na coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)` |
| Obter o sistema operacional do dispositivo na coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)/OPERATING_SYSTEM` |
| Obter usuários na coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/User` |

> [!NOTE]
> As consultas de exemplo mostradas na tabela usem *localhost* como o nome do host na URL e podem ser usadas no computador que executa o Provedor de SMS. Se você estiver executando suas consultas em um computador diferente, substitua localhost pelo FQDN do servidor com o Provedor de SMS instalado.

## <a name="azure-active-directory-onboarding"></a>Integração do Azure Active Directory

A integração do Azure Active Directory (AD) cria uma conexão entre o Configuration Manager e o Azure Active Directory que será usada por outros serviços de nuvem. Ela pode ser usada no momento para criar a conexão necessária para o Gateway de Gerenciamento de Nuvem.

Execute essa tarefa com o administrador do Azure, pois você precisará de credenciais de administrador do Azure.

#### <a name="to-create-the-connection"></a>Para criar a conexão:

2. No espaço de trabalho **Administração**, escolha **Serviços de Nuvem** > **Azure Active Directory** > **Adicionar Azure Active Directory**.
2. Escolha **Entrar** para criar a conexão com o Azure AD.

#### <a name="configuration-manager-client-requirements"></a>Requisitos do cliente do Configuration Manager

Há vários requisitos para habilitar a criação da política de usuário no Gateway de Gerenciamento de Nuvem.

- O processo de integração do Azure AD deve ser concluído e o cliente precisa ser inicialmente conectado à rede corporativa para obter as informações de conexão.
- Os clientes devem ser ambos ingressados no domínio (registrados no Active Directory) e no domínio da nuvem (registrado no Azure AD).
- É necessário executar a [Descoberta de Usuários do Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#active-directory-user-discovery#active-directory-user-discovery).
- Você deve modificar o cliente do Configuration Manager para permitir solicitações de política de usuário pela Internet e implantar a alteração para o cliente. Como essa alteração para o cliente ocorre *no dispositivo cliente*, ele pode ser implantado por meio do Gateway de Gerenciamento de Nuvem, mesmo se você não tiver concluído as alterações de configuração necessárias para a política de usuário.
- O ponto de gerenciamento deve ser configurado para usar HTTPS para proteger o token na rede e deve ter o .Net 4.5 instalado.

Depois de fazer essas alterações de configuração, você poderá criar uma política de usuário e mover os clientes para a Internet para testar a política. Solicitações de política de usuário por meio do Gateway de Gerenciamento de Nuvem serão autenticadas com a autenticação baseada em token do Azure AD.

## <a name="change-to-configuring-multi-factor-authentication-for-device-enrollment"></a>Alterar a configuração da autenticação multifator para registro de dispositivo

Agora que você pode configurar a MFA (Autenticação Multifator) para o registro de dispositivo no Portal do Azure, a opção de MFA foi removida no console do Configuration Manager. Você pode encontrar mais informações sobre como configurar o MFA para registro [neste tópico do Microsoft Intune](https://docs.microsoft.com/en-us/intune/deploy-use/multi-factor-authentication-azure-active-directory).
