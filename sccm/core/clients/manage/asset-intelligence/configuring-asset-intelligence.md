---
title: Configurar Asset Intelligence | System Center Configuration Manager
description: Configurar o Asset Intelligence no System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
caps.latest.revision: 7
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 43e04a447b03885286c6c7201afb4d1b7a10aa91


---
# <a name="configure-asset-intelligence-in-system-center-configuration-manager"></a>Configurar Asset Intelligence no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

É necessário concluir várias etapas de configuração antes de poder usar o Asset Intelligence no System Center Configuration Manager para inventariar e gerenciar o uso de licença de software em toda a sua empresa.  

## <a name="steps-to-configure-asset-intelligence"></a>Etapas para configurar o Asset Intelligence  
 Para coletar os dados de inventário necessários para relatórios do Asset Intelligence, o Agente Cliente de Inventário de Hardware deve ser habilitado. Para obter informações sobre como habilitar o Agente Cliente de Inventário de Hardware, consulte [Como estender o inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

|Etapa|Detalhes|Mais informações|  
|----------|-------------|----------------------|  
|**Etapa 1**: Habilitar as classes de relatório de inventário de hardware do Asset Intelligence|A coleta de informações do Asset Intelligence não é habilitada quando o Configuration Manager é instalado pela primeira vez. Para habilitar o Asset Intelligence, pelo menos uma das classes de relatório de inventário de hardware necessárias das quais o Asset Intelligence depende deve estar habilitada.|Para obter mais informações, veja o seguinte procedimento neste tópico: [Enable Asset Intelligence hardware inventory reporting classes](#BKMK_EnableAssetIntelligence).|  
|**Etapa 2**: Instalar um ponto de sincronização do Asset Intelligence|A função do sistema de sites do ponto de sincronização do Asset Intelligence é usada para conectar sites do Configuration Manager ao System Center Online para sincronizar informações do catálogo do Asset Intelligence. O ponto de sincronização do Asset Intelligence pode ser instalado apenas em um sistema de sites localizado no site de nível superior da hierarquia do Configuration Manager e exige acesso à Internet para sincronizar com o System Center Online usando a porta TCP 443.<br /><br /> Além de baixar novas informações do catálogo do Asset Intelligence, o ponto de sincronização do Asset Intelligence pode carregar informações de título de software personalizado no System Center Online para categorização. A Microsoft trata todos os títulos de software carregados no System Center Online para categorização como informações públicas. Portanto, você deve garantir que os títulos de software personalizado não contêm informações confidenciais ou proprietárias. Para obter mais informações sobre como solicitar a categorização de título de software, consulte [Request a catalog update for uncategorized software titles (Solicitar uma atualização de catálogo para títulos de software não categorizados)](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate).|Para obter mais informações, veja o seguinte procedimento neste tópico: [Install an Asset Intelligence Synchronization Point](#BKMK_InstallAssetIntelligenceSynchronizationPoint).|  
|**Etapa 3**: Habilitar a auditoria de eventos de logon com êxito|Quatro relatórios do Asset Intelligence exibem informações coletadas dos logs de eventos de Segurança do Windows em computadores cliente. Se as configurações de log de eventos de Segurança não estiverem definidas para registrar todos os eventos de logon com Êxito, esses relatórios não conterão dados, mesmo que a classe apropriada de relatório de inventário de hardware esteja habilitada. Para habilitar o Agente Cliente de Inventário de Hardware para inventariar as informações necessárias para dar suporte a esses relatórios, primeiro você deve modificar as configurações de log de eventos de Segurança do Windows nos clientes para registrar todos os eventos de logon com Êxito e habilitar a classe de relatório de inventário de hardware **SMS_SystemConsoleUser** .|Para obter mais informações, veja os seguintes procedimentos neste tópico: [Enable auditing of success logon events](#BKMK_EnableSuccessLogonEvents).|  
|**Etapa 4**: Importar informações de licença de software|O Assistente para Importar Licença de Software é usado para importar informações de MVLS (Licenciamento por Volume da Microsoft) e demonstrativos de licença geral para o catálogo do Asset Intelligence.<br /><br /> O demonstrativo de licença MVLS contém informações sobre os direitos de licença, ou o número de licenças adquiridas, para produtos Microsoft.<br /><br /> Um demonstrativo de licença geral contém informações sobre as licenças compradas de qualquer editor.|Para obter mais informações, veja os seguintes procedimentos neste tópico: [Import software license information](#BKMK_ImportSoftwareLicenseInformation).|  
|**Etapa 5**: Configurar tarefas de manutenção do Asset Intelligence|As tarefas de manutenção a seguir são associadas ao Asset Intelligence. Por padrão, ambas as tarefas de manutenção estão habilitadas e configuradas em um agendamento padrão.<br /><br /> **Verificar título de aplicativo com informações de inventário**: esta tarefa de manutenção verifica se o título de software relatado no inventário de software está reconciliado com o título de software no catálogo do Asset Intelligence.<br /><br /> **Resumir dados do software instalado**: esta tarefa de manutenção fornece as informações exibidas no espaço de trabalho **Ativos e Conformidade** do nó **Software Inventariado** , no nó **Asset Intelligence** . Quando a tarefa é executada, o Configuration Manager reúne uma contagem de todos os títulos de software inventariado no site primário.|Para obter mais informações, veja os seguintes procedimentos neste tópico: [Configure Asset Intelligence maintenance tasks](#BKMK_ConfigureMaintenanceTasks).|  

> [!NOTE]  
>  A tarefa de manutenção **Resumir dados de software instalado** está disponível somente em sites primários.  

## <a name="supplemental-procedures-for-configuring-asset-intelligence"></a>Procedimentos complementares para configurar o Asset Intelligence  
 Use as informações a seguir para as etapas na tabela anterior.  

###  <a name="a-namebkmkenableassetintelligencea-enable-asset-intelligence-hardware-inventory-reporting-classes"></a><a name="BKMK_EnableAssetIntelligence"></a> Enable Asset Intelligence hardware inventory reporting classes  
 Para habilitar o Asset Intelligence nos sites do Configuration Manager, é necessário habilitar uma ou mais classes de relatório de inventário de hardware do Asset Intelligence. Você pode habilitar as classes na home page do **Asset Intelligence** ou no espaço de trabalho **Administração** , no nó **Configurações do Cliente** das propriedades de configurações do cliente. Use um dos procedimentos a seguir para habilitar as classes de relatório de inventário de hardware do Asset Intelligence.  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>Para habilitar as classes de relatório de inventário de hardware do Asset Intelligence na home page do Asset Intelligence  

1.  No console do Configuration Manager, clique em **Ativo e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Asset Intelligence**.  

3.  Na guia **Início** do grupo **Asset Intelligence** , clique em **Editar Classes de Inventário**. A caixa de diálogo **Editar Classes de Inventário** é aberta.  

4.  Para habilitar o relatório do Asset Intelligence, selecione **Habilitar todas as classes de relatório do Asset Intelligence** ou **Habilitar somente as classes de relatório selecionadas do Asset Intelligence**e selecione, pelo menos, uma classe de relatório das classes exibidas.  

    > [!NOTE]  
    >  Os relatórios do Asset Intelligence que dependem das classes de inventário de hardware que permitem usar este procedimento não exibem dados até que os clientes tenham examinado e retornado o inventário de hardware.  

5.  Clique em **OK** para habilitar as classes de relatório de inventário de hardware do Asset Intelligence selecionadas.  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>Para habilitar as classes de relatório de inventário de hardware do Asset Intelligence nas propriedades de configurações do cliente  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , clique em **Configurações do Cliente**e selecione **Configurações do Agente Cliente Padrão**.  

    > [!NOTE]  
    >  Se você criou configurações personalizadas do cliente, é possível selecionar as configurações personalizadas do cliente em vez das configurações padrão do cliente.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**. A caixa de diálogo **Propriedades de Configurações do Cliente** é aberta.  

4.  Clique em **Inventário de Hardware**e em **Definir Classes**. A caixa de diálogo **Classes de Inventário de Hardware** é aberta.  

5.  Clique em **Filtrar por categoria**e em **Classes de relatório do Asset Intelligence**. A lista de classes é atualizada apenas com as classes de relatório de inventário de hardware do Asset Intelligence.  

6.  Selecione, pelo menos, uma classe de relatório na lista de classes de relatório do Asset Intelligence.  

    > [!NOTE]  
    >  Os relatórios do Asset Intelligence que dependem das classes de inventário de hardware que permitem usar este procedimento não exibem dados até que os clientes tenham examinado e retornado o inventário de hardware.  

7.  Clique em **OK** para habilitar as classes de relatório de inventário de hardware do Asset Intelligence selecionadas.  

###  <a name="a-namebkmkinstallassetintelligencesynchronizationpointa-install-an-asset-intelligence-synchronization-point"></a><a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Install an Asset Intelligence Synchronization Point  
 Use o procedimento a seguir para instalar uma função do sistema de sites do ponto de sincronização do Asset Intelligence.  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>Para instalar uma função do sistema de sites do ponto de sincronização do Asset Intelligence  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Configuração de Site**e clique em **Funções de Servidores e Sistema de Site**.  

3.  Adicione a função do sistema de sites do ponto de sincronização do Asset Intelligence a um servidor do sistema de sites novo ou existente usando a etapa associada:  

    -   **Novo servidor do sistema de sites**: na guia **Início** , no grupo **Criar** , clique em **Criar Servidor do Sistema de Sites**. O Assistente para Criar Servidor do Sistema de Site se abre.  

        > [!NOTE]  
        >  Por padrão, quando o Configuration Manager instala uma função do sistema de sites, os arquivos de instalação são instalados na primeira unidade de disco rígido com formatação NTFS disponível que contém o maior espaço livre em disco disponível. Para impedir o Configuration Manager de instalar em unidades específicas, crie um arquivo vazio chamado No_sms_on_drive.sms e copie-o para a pasta raiz da unidade antes de instalar o servidor do sistema de sites.  

    -   **Servidor do sistema de sites existente**: clique no servidor no qual deseja instalar a função do sistema de sites do ponto de sincronização do Asset Intelligence. Quando você clica em um servidor, uma lista das funções de sistema de site que já estão instaladas no servidor é exibida no painel de detalhes.  

         Na guia **Início** , no grupo **Servidor** , clique em **Adicionar Função do Sistema de Site**. O Assistente para Adicionar Funções do Sistema de Site se abre.  

4.  Na página **Geral** , especifique as configurações gerais para o servidor do sistema de site. Ao adicionar o ponto de sincronização do Asset Intelligence a um servidor do sistema de sites existente, verifique os valores que foram anteriormente configurados.  

5.  Na página **Seleção de Função do Sistema** , selecione **Ponto de Sincronização do Asset Intelligence** na lista de funções disponíveis e clique em **Avançar**.  

6.  Na página **Configurações de Conexão de Ponto de Sincronização do Asset Intelligence** , clique em **Avançar**.  

     Por padrão, a configuração **Usar este ponto de sincronização do Asset Intelligence** é marcada e não pode ser definida nesta página. O System Center Online aceita tráfego de rede somente pela porta TCP 443; portanto, a configuração do **número da porta SSL** não pode ser definida nesta página do assistente.  

7.  Opcionalmente, você pode especificar um caminho para o arquivo de certificado de autenticação (.pfx) do System Center Online e clicar em **Avançar**. Normalmente, você não especifica um caminho para o certificado porque o certificado de conexão é provisionado automaticamente durante a instalação da função do site.  

8.  Na página **Configurações do Servidor Proxy** , especifique se o ponto de sincronização do Asset Intelligence usará um servidor proxy ao se conectar ao System Center Online para sincronizar o catálogo e se deseja usar as credenciais para se conectar ao servidor proxy e clique em **Avançar**.  

    > [!WARNING]  
    >  Se um servidor proxy for necessário para se conectar ao System Center Online, o certificado de conexão também poderá ser excluído se a senha da conta de usuário expirar para a conta configurada para a autenticação do servidor proxy.  

9. Na página **Agendamento de Sincronização** , especifique se deseja sincronizar o catálogo do Asset Intelligence em um agendamento. Quando você habilita o agendamento de sincronização, é possível especificar um agendamento de sincronização simples ou personalizado. Durante a sincronização agendada, o ponto de sincronização do Asset Intelligence se conecta ao System Center Online para recuperar o catálogo do Asset Intelligence mais recente. É possível sincronizar manualmente o catálogo do Asset Intelligence no nó do Asset Intelligence do console do Configuration Manager. Para conhecer as etapas para sincronizar manualmente o catálogo de Asset Intelligence, consulte a seção [Para sincronizar manualmente o catálogo do Asset Intelligence](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog) em [Operações do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).  

10. Na página **Resumo** do Assistente de Nova Função de Site, examine as configurações que você especificou para garantir que estão corretas antes de continuar. Para fazer alterações em qualquer configuração, clique em **Anterior** até retornar à página apropriada, faça as alterações e retorne à página **Resumo** .  

###  <a name="a-namebkmkenablesuccesslogoneventsa-enable-auditing-of-success-logon-events"></a><a name="BKMK_EnableSuccessLogonEvents"></a> Enable auditing of success logon events  
 Use o procedimento a seguir para definir as configurações de logon da política de segurança do computador para habilitar a auditoria de eventos de logon com êxito.  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>Para habilitar o log de eventos de logon com êxito usando uma política de segurança local  

1.  Em um computador cliente do Configuration Manager, clique em **Iniciar**, aponte para **Ferramentas Administrativas** e clique em **Política de Segurança Local**.  

2.  Na caixa de diálogo **Política de Segurança Local** , em **Configurações de Segurança**, expanda **Políticas Locais**e clique em **Política de Auditoria**.  

3.  No painel de resultados, clique duas vezes em **Auditoria de eventos de logon**, certifique-se de que a caixa de seleção **Êxito** está marcada e clique em **OK**.  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>Para habilitar o log de eventos de logon com êxito usando uma política de segurança de domínio do Active Directory  

1.  Em um computador do controlador de domínio, clique em **Iniciar**, aponte para **Ferramentas Administrativas**, e clique em **Política de Segurança de Domínio**.  

2.  Na caixa de diálogo **Política de Segurança Local** , em **Configurações de Segurança**, expanda **Políticas Locais**e clique em **Política de Auditoria**.  

3.  No painel de resultados, clique duas vezes em **Auditoria de eventos de logon**, certifique-se de que a caixa de seleção **Êxito** está marcada e clique em **OK**.  

###  <a name="a-namebkmkimportsoftwarelicenseinformationa-import-software-license-information"></a><a name="BKMK_ImportSoftwareLicenseInformation"></a> Import software license information  
 As seções a seguir descrevem os procedimentos necessários para importar informações de licenciamento de software geral e da Microsoft para o banco de dados do site do Configuration Manager usando o Assistente para Importar Licença de Software. Ao importar informações de licença de software para o banco de dados do site dos arquivos de demonstrativo de licença, a conta de computador do servidor do site exigirá permissões de **Controle Total** para o sistema de arquivos NTFS ao compartilhamento de arquivo usado para importar informações de licença de software.  

> [!IMPORTANT]  
>  Quando as informações de licença de software são importadas para o banco de dados do site, as informações de licença de software existentes são substituídas. Verifique se o arquivo de informações de licença de software usado com o Assistente para Importar Licença de Software contém uma lista completa de todas as informações de licença de software necessárias.  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>Para importar informações de licença de software para o catálogo do Asset Intelligence  

1.  No espaço de trabalho **Ativos e Conformidade** , clique em **Asset Intelligence**.  

2.  Na guia **Início** do grupo **Asset Intelligence** , clique em **Importar Licenças de Software**. O Assistente para Importar Licença de Software é aberto.  

3.  Na página **Bem-vindo** , clique em **Avançar**.  

4.  Na página **Importação** , especifique se você está importando um arquivo MVLS (Licenciamento por Volume da Microsoft) (.xml ou .csv) ou um arquivo de Demonstrativo de Licença Geral (.csv). Para obter mais informações sobre como criar um arquivo de Demonstrativo de Licenças Geral, veja [Create a general license statement information file for import](#BKMK_CreateGeneralLicenseStatement) mais adiante neste tópico.  

    > [!WARNING]  
    >  Para baixar um arquivo MVLS no formato .csv que pode ser importado para o catálogo do Asset Intelligence, veja [Centro de Serviços de Licenciamento por Volume da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=226547). Para acessar essas informações, é necessário ter uma conta registrada no site. É necessário entrar em contato com seu representante de contas da Microsoft para obter informações sobre como obter o arquivo MVLS no formato .xml.  

5.  Digite o caminho UNC para o arquivo de demonstrativo de licença ou clique em **Procurar** para selecionar uma pasta e um arquivo da rede compartilhada.  

    > [!NOTE]  
    >  A pasta compartilhada deve ser protegida corretamente para evitar o acesso não autorizado ao arquivo de informações de licenciamento, e a conta do computador no qual o assistente está sendo executado deve ter permissões de Controle Completo ao compartilhamento que contém o arquivo de importação de licença.  

6.  Na página **Resumo** , examine as informações que você especificou garantir que estão corretas antes de continuar. Para fazer alterações, clique em **Anterior** para retornar à página **Importação** .  

###  <a name="a-namebkmkcreategenerallicensestatementa-create-a-general-license-statement-information-file-for-import"></a><a name="BKMK_CreateGeneralLicenseStatement"></a> Create a general license statement information file for import  
 Um demonstrativo de licença geral também pode ser importado para o catálogo do Asset Intelligence usando um arquivo de importação de licença criado manualmente no formato de arquivo .csv (delimitado por vírgulas).  

> [!NOTE]  
>  Embora somente os campos **Name**, **Publisher**, **Version**e **EffectiveQuantity** sejam necessários para conter os dados, todos os campos devem ser inseridos na primeira linha do arquivo de importação de licença. Todos os campos de data devem ser exibidos no seguinte formato: Mês/Dia/Ano, por exemplo, 4/8/2008.  

 O Asset Intelligence faz a correspondência dos produtos que você especificar no demonstrativo de licença geral usando o nome e a versão do produto, exceto pelo nome do fornecedor. É necessário usar um nome de produto no demonstrativo de licença geral que seja uma correspondência exata do nome de produto armazenado no banco de dados do site. O Asset Intelligence usa o número de **EffectiveQuantity** fornecido no demonstrativo de licença geral e o compara com o número de produtos instalados encontrado no inventário do Configuration Manager.  

> [!TIP]  
>  Para obter uma lista completa de nomes de produtos armazenados no banco de dados do site do Configuration Manager, é possível executar a seguinte consulta no banco de dados do site: SELECT ProductName0 FROM v_GS_INSTALLED_SOFTWARE.  

 Você pode especificar versões exatas de um produto ou especificar parte da versão, como apenas a versão principal. Os exemplos a seguir fornecem as correspondências de versão resultantes para uma entrada de versão de demonstrativos de licença geral de um produto específico.  

|Entrada de demonstrativo de licenças geral|Correspondência de entradas do banco de dados do site|  
|-------------------------------------|------------------------------------|  
|Name: "MySoftware", ProductVersion0:"2"|ProductName0: "Mysoftware", ProductVersion0: "2.01.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.02.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.3579.000"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.10.1234"|  
|Name: "MySoftware", Version "2.05"|ProductName0: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.3579.000"|  
|Name: "Mysoftware", Version "2"<br /><br /> Name: "Mysoftware", Version "2.05"|Erro durante a importação. A importação falhará quando mais de uma entrada corresponder à mesma versão do produto.|  

 O procedimento a seguir descreve o processo que pode ser usado para criar um arquivo de importação de declaração de licença geral usando o Microsoft Excel.  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>Para criar um arquivo de importação de demonstrativo de licença geral usando o Microsoft Excel  

1.  Abra o Microsoft Excel e crie uma nova planilha.  

2.  Na primeira linha da nova planilha, insira todos os nomes de campo dos dados de licença de software.  

3.  Na segunda linha e nas linhas posteriores da nova planilha, insira as informações de licença de software, necessárias. Verifique se, pelo menos, todos os campos de dados da licença de software necessários são inseridos em linhas posteriores de cada licença de software a ser importada. O nome do título de software inserido na planilha deve ser o mesmo que o título de software exibido no Gerenciador de Recursos para um computador cliente após a execução do inventário de hardware.  

4.  No menu **Arquivo** , clique em **Salvar Como**e salve o arquivo no formato .csv.  

5.  Copie o arquivo .csv no compartilhamento de arquivo que é usado para importar informações de licença de software para o catálogo do Asset Intelligence.  

6.  No console do Configuration Manager, use o Assistente para Importar Licença de Software para importar o arquivo de informações de licença .csv recém-criado.  

7.  Execute o **Relatório Licença 15A – Reconciliação de software de terceiros** do Asset Intelligence para verificar se as informações de licenciamento foram importadas com êxito para o catálogo do Asset Intelligence.  

> [!NOTE]  
>  Para obter um exemplo de um arquivo de licença de software geral que você pode usar para fins de teste, consulte [Exemplo de arquivo de importação de licença geral do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md).  

#### <a name="sample-table-to-describe-software-licenses"></a>Tabela de exemplo para descrever as licenças de software  
 Ao criar um arquivo de importação de demonstrativo de licença geral, as informações na tabela a seguir podem ser usadas para descrever as licenças de software a ser importadas para o catálogo do Asset Intelligence.  

|Nome da coluna|Tipo de dados|Necessária|Exemplo|  
|-----------------|---------------|--------------|-------------|  
|Name|Até 255 caracteres|Sim|Título de software|  
|Publisher|Até 255 caracteres|Sim|Fornecedor de software|  
|Version|Até 255 caracteres|Sim|Versão do título de software|  
|Linguagem|Até 255 caracteres|Sim|Idioma do título de software|  
|EffectiveQuantity|Valor inteiro|Sim|Número de licenças adquiridas|  
|PONumber|Até 255 caracteres|Não|Informações de ordem de compra|  
|ResellerName|Até 255 caracteres|Não|Informações do revendedor|  
|DateOfPurchase|Valor de data no seguinte formato: DD/MM/AAAA|Não|Data da aquisição de licenças|  
|SupportPurchased|Valor de bit|Não|0 ou 1: insira 0 para Sim ou 1 para Não|  
|SupportExpirationDate|Valor de data no seguinte formato: DD/MM/AAAA|Não|Data de término do suporte adquirido|  
|Comentários|Até 255 caracteres|Não|Comentários opcionais|  

###  <a name="a-namebkmkconfiguremaintenancetasksa-configure-asset-intelligence-maintenance-tasks"></a><a name="BKMK_ConfigureMaintenanceTasks"></a> Configure Asset Intelligence maintenance tasks  
 As seguintes tarefas de manutenção estão disponíveis para o Asset Intelligence:  

-   **Verificar título de aplicativo com informações de inventário**: esta tarefa de manutenção verifica se o título de software relatado no inventário de software está reconciliado com o título de software no catálogo do Asset Intelligence. Por padrão, esta tarefa é habilitada e agendada para ser executada aos sábados após a meia-noite e antes das 5h. Esta tarefa de manutenção está disponível somente no site de nível superior em sua hierarquia do Configuration Manager.  

-   **Resumir dados do software instalado**: esta tarefa de manutenção fornece as informações exibidas no espaço de trabalho **Ativos e Conformidade** do nó **Software Inventariado** , no nó **Asset Intelligence** . Quando a tarefa é executada, o Configuration Manager reúne uma contagem de todos os títulos de software inventariado no site primário. Por padrão, esta tarefa é habilitada e agendada para ser executada todos os dias após a meia-noite e antes das 5h. Esta tarefa de manutenção está disponível somente em sites primários.  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>Para configurar tarefas de manutenção do Asset Intelligence  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Configuração do Site**e clique em **Sites**.  

3.  Selecione o site no qual a tarefa de manutenção do Asset Intelligence será configurada.  

    > [!NOTE]  
    >  A tarefa de manutenção **Resumir dados de software instalado** está disponível somente em sites primários.  

4.  Na guia **Início** , no grupo **Configurações** , clique em **Manutenção do Site**. É exibida uma lista de todas as tarefas de manutenção de site disponíveis.  

5.  Selecione a tarefa de manutenção desejada e clique em **Editar** para modificar as configurações.  

6.  Habilite e configure a tarefa de manutenção. Para minimizar a interferência com a operação do site, recomendamos que você defina o período de tempo para o horário fora de pico do site. O período de tempo é o intervalo de tempo em que a tarefa pode ser executada. É definido pela **Hora de início após** e **Hora de início mais recente** especificadas na caixa de diálogo **Propriedades da Tarefa** .  

    > [!WARNING]  
    >  Você pode iniciar a tarefa imediatamente selecionando o dia atual e configurando a hora **Iniciar após** para alguns minutos após a hora atual.  

7.  Clique em **OK** para salvar as alterações. Agora a tarefa é executada de acordo com seu agendamento.  

    > [!NOTE]  
    >  Se uma tarefa falhar ao ser executada na primeira tentativa, o Configuration Manager tentará executá-la novamente até que ela seja executada com êxito ou até que tenha decorrido o período de sua execução.  



<!--HONumber=Nov16_HO1-->


