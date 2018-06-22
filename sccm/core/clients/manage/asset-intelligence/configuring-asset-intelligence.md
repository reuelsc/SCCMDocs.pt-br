---
title: Configurar o Asset Intelligence
titleSuffix: Configuration Manager
description: Configurar o Asset Intelligence no System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 182006f0e4fcaf2304570ef4110527a61180c290
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32341008"
---
# <a name="configure-asset-intelligence-in-system-center-configuration-manager"></a>Configurar Asset Intelligence no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Asset Intelligence faz o inventário e gerencia o uso de licença de software.   

## <a name="steps-to-configure-asset-intelligence"></a>Etapas para configurar o Asset Intelligence  
   

- **Etapa 1**: Para coletar os dados de inventário necessários para os relatórios do Asset Intelligence, você precisa habilitar o agente cliente de inventário de hardware, conforme descrito em [Como estender o inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).
- **Etapa 2**: [Habilitar as classes de relatório de inventário de hardware do Asset Intelligence](#BKMK_EnableAssetIntelligence).  
- **Etapa 3**: [Instalar um ponto de sincronização do Asset Intelligence](#BKMK_InstallAssetIntelligenceSynchronizationPoint)
- **Etapa 4**: [Habilitar a auditoria de eventos de logon com êxito](#BKMK_EnableSuccessLogonEvents)  
- **Etapa 5**: [Importar informações de licença de software](#BKMK_ImportSoftwareLicenseInformation)  
- **Etapa 6**: [Configurar tarefas de manutenção do Asset Intelligence](#BKMK_ConfigureMaintenanceTasks) 


###  <a name="BKMK_EnableAssetIntelligence"></a> Enable Asset Intelligence hardware inventory reporting classes  
 Para habilitar o Asset Intelligence nos sites do Configuration Manager, é necessário habilitar uma ou mais classes de relatório de inventário de hardware do Asset Intelligence. Você pode habilitar as classes na home page do **Asset Intelligence** ou no espaço de trabalho **Administração** , no nó **Configurações do Cliente** das propriedades de configurações do cliente. Use um dos procedimentos a seguir.  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>Para habilitar as classes de relatório de inventário de hardware do Asset Intelligence na home page do Asset Intelligence  

1.  No console do Configuration Manager, escolha **Ativos e Conformidade** > **Asset Intelligence**.  

3.  Na guia **Início** do grupo **Asset Intelligence**, escolha **Editar Classes de Inventário**.   

4.  Para habilitar o relatório do Asset Intelligence, selecione **Habilitar todas as classes de relatórios do Asset Intelligence** ou **Habilitar somente as classes de relatórios selecionadas do Asset Intelligence** e selecione, pelo menos, uma classe de relatório das classes exibidas.  

    > [!NOTE]  
    >  Os relatórios do Asset Intelligence que dependem das classes de inventário de hardware que permitem usar este procedimento não exibem dados até que os clientes tenham examinado e retornado o inventário de hardware.  


##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>Para habilitar as classes de relatório de inventário de hardware do Asset Intelligence nas propriedades de configurações do cliente  

1.  No console do Configuration Manager, escolha **Administração** >  **Configurações do Cliente** > **Configurações do Agente Cliente Padrão**. Se você criou configurações de cliente personalizadas, você pode selecioná-las em vez disso.  

3.  Na guia **Início** > grupo **Propriedades**, escolha **Propriedades**.   

4.  Escolha **Inventário de Hardware** > **Definir Classes**. .  

5.  Escolha **Filtrar por categoria** > **Classes de Relatórios Asset Intelligence**. A lista de classes é atualizada apenas com as classes de relatório de inventário de hardware do Asset Intelligence.  

6.  Selecione pelo menos uma classe de relatórios na lista.  

    > [!NOTE]  
    >  Os relatórios do Asset Intelligence que dependem das classes de inventário de hardware que permitem usar este procedimento não exibem dados até que os clientes tenham examinado e retornado o inventário de hardware.  
  

###  <a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Install an Asset Intelligence Synchronization Point  

A função do sistema de sites do ponto de sincronização do Asset Intelligence é usada para conectar sites do Configuration Manager ao System Center Online para sincronizar informações do catálogo do Asset Intelligence. O ponto de sincronização do Asset Intelligence só pode ser instalado em um sistema de sites localizado no site de nível superior da hierarquia do Configuration Manager e exige acesso à Internet para sincronizar com o System Center Online usando a porta TCP 443.

Além de baixar novas informações do catálogo do Asset Intelligence, o ponto de sincronização do Asset Intelligence pode carregar informações de título de software personalizado no System Center Online para categorização. A Microsoft trata todos os títulos de software carregados como informações públicas. Verifique se os títulos de software personalizados não contêm informações confidenciais ou proprietárias. Para obter mais informações sobre como solicitar a categorização de título de software, consulte [Request a catalog update for uncategorized software titles (Solicitar uma atualização de catálogo para títulos de software não categorizados)](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate).  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>Para instalar uma função do sistema de sites do ponto de sincronização do Asset Intelligence  

1.  No console do Configuration Manager, escolha **Administração**> **Configuração do Site** > **Funções de Servidores e Sistema de Site**.  

3.  Adicione a função do sistema de sites do ponto de sincronização do Asset Intelligence a um servidor do sistema de sites novo ou existente:  

    -  Para um **Novo servidor do sistema de sites**: na guia **Início**, no grupo **Criar**, escolha **Criar Servidor do Sistema de Site** para iniciar o assistente.   

        > [!NOTE]  
        >  Por padrão, quando o Configuration Manager instala uma função do sistema de sites, os arquivos de instalação são instalados na primeira unidade de disco rígido com formatação NTFS disponível que contém o maior espaço livre em disco disponível. Para impedir o Configuration Manager de instalar em unidades específicas, crie um arquivo vazio chamado No_sms_on_drive.sms e copie-o para a pasta raiz da unidade antes de instalar o servidor do sistema de sites.  

    -  Para um **Servidor do sistema de sites existente**: escolha o servidor no qual deseja instalar a função do sistema de sites do ponto de sincronização do Asset Intelligence. Quando você escolhe um servidor, uma lista das funções do sistema de sites que já estão instaladas no servidor é exibida no painel de detalhes.  

         Na guia **Início**, no grupo **Servidor**, escolha **Adicionar Função do Sistema de Sites** para iniciar o assistente.  

4.  Conclua a página **Geral**. Ao adicionar o ponto de sincronização do Asset Intelligence a um servidor do sistema de sites existente, verifique os valores que foram anteriormente configurados.  

5.  Na página **Seleção de Função do Sistema**, selecione **Ponto de Sincronização do Asset Intelligence** na lista de funções disponíveis.  

6.  Na página **Configurações de Conexão de Ponto de Sincronização do Asset Intelligence**, escolha **Avançar**.  

     Por padrão, a configuração **Usar este ponto de sincronização do Asset Intelligence** é marcada e não pode ser definida nesta página. O System Center Online aceita tráfego de rede somente pela porta TCP 443; portanto, a configuração do **número da porta SSL** não pode ser definida nesta página do assistente.  

7.  Opcionalmente, você pode especificar um caminho para o arquivo de certificado de autenticação (.pfx) do System Center Online. Normalmente, você não especifica um caminho para o certificado porque o certificado de conexão é provisionado automaticamente durante a instalação da função do site.  

8.  Na página **Configurações do Servidor Proxy**, especifique se o ponto de sincronização do Asset Intelligence usará um servidor proxy ao se conectar ao System Center Online para sincronizar o catálogo e se deseja usar as credenciais para se conectar ao servidor proxy.  

    > [!WARNING]  
    >  Se um servidor proxy for necessário para se conectar ao System Center Online, o certificado de conexão também poderá ser excluído se a senha da conta de usuário expirar para a conta configurada para a autenticação do servidor proxy.  

9. Na página **Agendamento de Sincronização** , especifique se deseja sincronizar o catálogo do Asset Intelligence em um agendamento. Quando você habilita o agendamento de sincronização, é possível especificar um agendamento de sincronização simples ou personalizado. Durante a sincronização agendada, o ponto de sincronização do Asset Intelligence se conecta ao System Center Online para recuperar o catálogo do Asset Intelligence mais recente. É possível sincronizar manualmente o catálogo do Asset Intelligence no nó do Asset Intelligence do console do Configuration Manager. Para conhecer as etapas para sincronizar manualmente o catálogo de Asset Intelligence, consulte a seção [Para sincronizar manualmente o catálogo do Asset Intelligence](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog) em [Operações do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).  

10. Concluir o assistente 

###  <a name="BKMK_EnableSuccessLogonEvents"></a> Enable auditing of success logon events  
 Quatro relatórios do Asset Intelligence exibem informações coletadas dos logs de eventos de Segurança do Windows em computadores cliente. Veja aqui como definir as configurações de logon da política de segurança do computador para habilitar a auditoria de eventos de Logon com êxito.  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>Para habilitar o log de eventos de logon com êxito usando uma política de segurança local  

1.  Em um computador cliente do Configuration Manager, escolha **Iniciar** > **Ferramentas Administrativas** > **Política de Segurança Local**.  

2.  Na caixa de diálogo **Política de Segurança Local**, em **Configurações de Segurança**, expanda **Políticas Locais**e, em seguida, escolha **Política de Auditoria**.  

3.  No painel de resultados, clique duas vezes em **Auditoria de eventos de logon**, certifique-se de que a caixa de seleção **Êxito** está marcada e, em seguida, escolha **OK**.  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>Para habilitar o log de eventos de logon com êxito usando uma política de segurança de domínio do Active Directory  

1.  Em um computador do controlador de domínio, escolha **Iniciar**, aponte para **Ferramentas Administrativas** e, em seguida, escolha **Política de Segurança de Domínio**.  

2.  Na caixa de diálogo **Política de Segurança Local**, em **Configurações de Segurança**, expanda **Políticas Locais**e, em seguida, escolha **Política de Auditoria**.  

3.  No painel de resultados, clique duas vezes em **Auditoria de eventos de logon**, certifique-se de que a caixa de seleção **Êxito** está marcada e, em seguida, escolha **OK**.  

###  <a name="BKMK_ImportSoftwareLicenseInformation"></a> Import software license information  
 As seções a seguir descrevem os procedimentos necessários para importar informações de licenciamento de software geral e da Microsoft para o banco de dados do site do Configuration Manager usando o Assistente para Importar Licença de Software. Ao importar informações de licença de software para o banco de dados do site dos arquivos de demonstrativo de licença, a conta de computador do servidor do site exigirá permissões de **Controle Total** para o sistema de arquivos NTFS ao compartilhamento de arquivo usado para importar informações de licença de software.  

> [!IMPORTANT]  
>  Quando as informações de licença de software são importadas para o banco de dados do site, as informações de licença de software existentes são substituídas. Verifique se o arquivo de informações de licença de software usado com o Assistente para Importar Licença de Software contém uma lista completa de todas as informações de licença de software necessárias.  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>Para importar informações de licença de software para o catálogo do Asset Intelligence  

1.  No espaço de trabalho **Ativos e Conformidade**, escolha **Asset Intelligence**.  

2.  Na guia **Início** do grupo **Asset Intelligence**, escolha **Importar Licenças de Software**.   

4.  Na página **Importação** , especifique se você está importando um arquivo MVLS (Licenciamento por Volume da Microsoft) (.xml ou .csv) ou um arquivo de Demonstrativo de Licença Geral (.csv). Para obter mais informações sobre como criar um arquivo de Demonstrativo de Licenças Geral, veja [Create a general license statement information file for import](#BKMK_CreateGeneralLicenseStatement) mais adiante neste tópico.  

    > [!WARNING]  
    >  Para baixar um arquivo MVLS no formato .csv que pode ser importado para o catálogo do Asset Intelligence, veja [Centro de Serviços de Licenciamento por Volume da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=226547). Para acessar essas informações, é necessário ter uma conta registrada no site. É necessário entrar em contato com seu representante de contas da Microsoft para obter informações sobre como obter o arquivo MVLS no formato .xml.  

5.  Digite o caminho UNC para o arquivo de demonstrativo de licença ou escolha **Procurar** para selecionar uma pasta e um arquivo compartilhado de rede.  

    > [!NOTE]  
    >  A pasta compartilhada deve ser protegida corretamente para evitar o acesso não autorizado ao arquivo de informações de licenciamento, e a conta do computador no qual o assistente está sendo executado deve ter permissões de Controle Completo ao compartilhamento que contém o arquivo de importação de licença.  

6. Conclua o assistente.  

###  <a name="BKMK_CreateGeneralLicenseStatement"></a> Create a general license statement information file for import  
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
  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>Para criar um arquivo de importação de demonstrativo de licença geral usando o Microsoft Excel  

1.  Abra o Microsoft Excel e crie uma nova planilha.  

2.  Na primeira linha da nova planilha, insira todos os nomes de campo dos dados de licença de software.  

3.  Na segunda linha e nas linhas posteriores da nova planilha, insira as informações de licença de software, necessárias. Verifique se, pelo menos, todos os campos de dados da licença de software necessários são inseridos em linhas posteriores de cada licença de software a ser importada. O nome do título de software inserido na planilha deve ser o mesmo que o título de software exibido no Gerenciador de Recursos para um computador cliente após a execução do inventário de hardware.  

4.  Salve o arquivo no formato .csv.  

5.  Copie o arquivo .csv no compartilhamento de arquivo que é usado para importar informações de licença de software para o catálogo do Asset Intelligence.  

6.  No console do Configuration Manager, use o Assistente para Importar Licença de Software para importar o arquivo .csv recém-criado.  

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

###  <a name="BKMK_ConfigureMaintenanceTasks"></a> Configure Asset Intelligence maintenance tasks  
 As seguintes tarefas de manutenção estão disponíveis para o Asset Intelligence:  

-   **Verificar Título do Aplicativo com as Informações de Inventário**: verifica se o título de software relatado no inventário de software concilia-se com o título de software no catálogo do Asset Intelligence. Por padrão, esta tarefa é habilitada e agendada para ser executada aos sábados após a meia-noite e antes das 5h. Esta tarefa de manutenção está disponível somente no site de nível superior em sua hierarquia do Configuration Manager.  

-   **Resumir Dados de Software Instalado**: fornece as informações exibidas no espaço de trabalho **Ativos e Conformidade** do nó **Software Inventariado**, no nó **Asset Intelligence**. Quando a tarefa é executada, o Configuration Manager reúne uma contagem de todos os títulos de software inventariado no site primário. Por padrão, esta tarefa é habilitada e agendada para ser executada todos os dias após a meia-noite e antes das 5h. Esta tarefa de manutenção está disponível somente em sites primários.  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>Para configurar tarefas de manutenção do Asset Intelligence  

1.  No console do Configuration Manager, escolha **Administração** > **Configuração de Site** > **Sites**.  

3.  Selecione o site no qual a tarefa de manutenção do Asset Intelligence será configurada.  

4.  Na guia **Início**, no grupo **Configurações**, escolha **Manutenção do Site**. Selecione uma tarefa e escolha **Editar** para modificar as configurações. 

    É recomendável que você defina o período de tempo para fora do horário de pico do site. O período de tempo é o intervalo de tempo em que a tarefa pode ser executada. É definido pela **Hora de início após** e **Hora de início mais recente** especificadas na caixa de diálogo **Propriedades da Tarefa** .  

    Você pode iniciar a tarefa imediatamente selecionando o dia atual e configurando a hora **Iniciar após** para alguns minutos após a hora atual.  

7.  Escolha **OK** para salvar as alterações. Agora a tarefa é executada de acordo com seu agendamento.  

    > [!NOTE]  
    >  Se uma tarefa falhar ao ser executada na primeira tentativa, o Configuration Manager tentará executá-la novamente até que ela seja executada com êxito ou até que tenha decorrido o período de sua execução.  
