---
title: Data warehouse
titleSuffix: Configuration Manager
description: Banco de dados e ponto de serviço de data warehouse para o Configuration Manager
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a4d95495f2f200eaff39699c65cc391a2a81b009
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54897552"
---
#  <a name="the-data-warehouse-service-point-for-configuration-manager"></a>O ponto de serviço do data warehouse para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

<!--1277922--> Use o ponto de serviço do data warehouse para armazenar e relatar dados históricos de longo prazo da sua implantação do Configuration Manager.

> [!Note]  
> O Configuration Manager não habilita esse recurso opcional por padrão. É necessário habilitar esse recurso antes de usá-lo. Para obter mais informações, veja [Habilitar recursos opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


O data warehouse dá suporte a até 2 TB de dados, com carimbos de data e hora para controle de alterações. O data warehouse armazena dados automaticamente sincronizando dados do banco de dados do site do Configuration Manager com o banco de dados de data warehouse. Essas informações ficam acessíveis de seu ponto do Reporting Services. Dados sincronizados com o banco de dados de data warehouse são mantidos por três anos. Periodicamente, uma tarefa interna remove os dados com mais de três anos.

Os dados sincronizados incluem o seguinte dos grupos de Dados Globais e Dados do Site:
- Integridade de infraestrutura
- Segurança
- Conformidade
- Malware   
- Implantações de software
- Detalhes de inventário (no entanto, o histórico de inventário não é sincronizado)

Quando a função de sistema de site é instalada, ele instala e configura o banco de dados do data warehouse. Também instala vários relatórios para que você possa procurar esses dados com facilidade e criar relatórios com base neles.

Da versão 1810 em diante, você pode sincronizar mais tabelas do banco de dados do site para o data warehouse. Essa alteração permite que você crie mais relatórios com base nas necessidades empresariais.<!--1358870--> 



## <a name="prerequisites"></a>Pré-requisitos

- A função do sistema de sites do data warehouse tem suporte apenas no site de nível superior da hierarquia. Por exemplo, um site de administração central ou site primário autônomo.  

- O computador no qual você instala a função do sistema de sites requer o .NET Framework 4.5.2 ou posterior.  

- Conceda a **Conta do Ponto do Reporting Services** a permissão **db_datareader** no banco de dados do data warehouse.  

- Para sincronizar dados com o banco de dados de data warehouse, o Configuration Manager usa a conta de computador da função de sistema de sites. Essa conta exige as seguintes permissões:  

    - O **administrador** no computador que hospeda o banco de dados de data warehouse.  

    - Permissão **DB_Creator** no banco de dados de data warehouse.  

    - O **DB_owner** ou o **DB_reader** com as permissões **execute** para o banco de dados do site de nível superior.  

- O banco de dados do data warehouse exige o uso do SQL Server 2012 ou posterior. A edição pode ser Standard, Enterprise ou Datacenter. A versão do SQL Server para o data warehouse não precisa ser igual à do servidor de banco de dados do site.<!--SCCMDocs issue 662-->  

- O banco de dados do warehouse tem suporte para as seguintes configurações do SQL Server:  

    - Um instância padrão ou nomeada  

    - Grupo de disponibilidade Always On do SQL Server  

    - Cluster de failover do SQL Server  

- Se você usar as [exibições distribuídas](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_distviews), o ponto de serviço do data warehouse deverá deve ser instalada no mesmo servidor que hospeda o banco de dados do site de administração central.  

Para obter mais informações sobre o licenciamento do SQL Server, confira [perguntas frequentes sobre produto e licenciamento](/sccm/core/understand/product-and-licensing-faq). <!-- sms500967 -->

Dimensione o banco de dados de data warehouse para que tenha o mesmo tamanho do banco de dados do site. Embora o data warehouse seja menor no início, ele aumentará com o tempo. <!--SCCMDocs issue 756-->



## <a name="install"></a>Instalar o

Cada hierarquia dá suporte a uma única instância dessa função, em qualquer sistema de sites desse site de nível superior. O SQL Server que hospeda o banco de dados para o warehouse pode ser local na função de sistema de site ou remoto. O data warehouse funciona com o ponto do reporting services instalado no mesmo site. Você não precisa instalar as duas funções de sistema de site no mesmo servidor.   

Para instalar a função, use o **Assistente para Adicionar Funções de Sistema de Site** ou o **Assistente para Criar Funções do Sistema de Site**. Para saber mais, confira [Instalar funções do sistema de sites](/sccm/core/servers/deploy/configure/install-site-system-roles). Na página **Seleção de Função do Sistema** do assistente, selecione a função **Ponto de serviço do Data Warehouse**. 

Ao instalar a função, o Configuration Manager cria o banco de dados de data warehouse para você em uma instância especificada do SQL Server. Se você especificar o nome de um banco de dados existente, o Configuration Manager não criará um novo banco de dados. Em vez disso, ele usa um que você especifica. Esse processo é o mesmo de quando você [move o banco de dados de data warehouse para um novo SQL Server](#move-the-data-warehouse-database).


### <a name="configure-properties"></a>Configurar propriedades

#### <a name="general-page"></a>Página Geral

- **Nome de domínio totalmente qualificado do SQL Server**: especifique o FQDN (nome de domínio totalmente qualificado) do servidor que hospeda o banco de dados do ponto de serviço do data warehouse.  

- **Nome da instância do SQL Server, se for aplicável**: se você não usar uma instância padrão do SQL Server, especifique a instância nomeada.  

- **Nome do banco de dados**: Especifique um nome para o banco de dados do data warehouse. O Configuration Manager cria o banco de dados do data warehouse com esse nome. Se você especificar um nome de banco de dados que já existe na instância do SQL Server, o Configuration Manager usará esse banco de dados.  

- **Porta do SQL Server usada para conexão**: especifique o número da porta TCP/IP usado pelo SQL Server que hospeda o banco de dados do data warehouse. O serviço de sincronização do data warehouse usa essa porta para conectar-se ao banco de dados do data warehouse. Por padrão, ele usa a porta do SQL Server **1433** para comunicação.  

- **Conta do ponto de serviço do data warehouse**: Começando na versão 1802, defina o **Nome de usuário** que o SQL Server Reporting Services usa ao conectar-se ao banco de dados de data warehouse.  


#### <a name="synchronization-schedule-page"></a>Página de agenda de sincronização
*Aplica-se à versão 1806 e anteriores*

- **Hora de início**: Especifique a hora de início da sincronização do data warehouse.  

- **Padrão de recorrência**

    - **Diário**: especifique que a sincronização é executada diariamente.  

    - **Semanal**: especifique um único dia de cada semana e a recorrência semanal para a sincronização.


#### <a name="synchronization-settings-page"></a>Página de configurações de sincronização
*Aplica-se à versão 1810 e posteriores*

- **Configuração personalizada de sincronização de dados**: escolha a opção para **Selecionar tabelas**. Na janela de tabelas do Banco de Dados, selecione os nomes de tabela para sincronizar o banco de dados do data warehouse. Use o filtro para pesquisar por nome ou selecione a lista suspensa para escolher grupos específicos. Selecione **OK** ao concluir para salvar.  

    > [!Note]  
    > Não é possível remover as tabelas que a função seleciona por padrão.  

- **Hora de início**: Especifique a hora de início da sincronização do data warehouse.  

- **Padrão de recorrência**

    - **Diário**: especifique que a sincronização é executada diariamente.  

    - **Semanal**: especifique um único dia de cada semana e a recorrência semanal para a sincronização.



## <a name="reporting"></a>Relatórios

Depois de instalar um ponto de serviço do data warehouse, vários relatórios são disponibilizados no ponto do Reporting Services para o site. Se você instalar o ponto de serviço do data warehouse antes de instalar um ponto do reporting services, os relatórios serão adicionados automaticamente ao instalar posteriormente o ponto do reporting services.

> [!WARNING]  
> Iniciando na versão 1802, o ponto do data warehouse dá suporte a credenciais alternativas.<!--507334--> Se você tiver atualizado de uma versão anterior do Configuration Manager, precisará especificar as credenciais que serão usadas pelo SQL Server Reporting Services para se conectar ao banco de dados de data warehouse. Relatórios do data warehouse não abrem até você adicionar as credenciais. 
> 
> Para especificar uma conta, defina o **Nome de usuário** para a conta de ponto de serviço do data warehouse nas propriedades da função. Para saber mais, confira [Configurar propriedades](#configure-properties). 

A função do sistema de sites do data warehouse inclui os seguintes relatórios na categoria **Data Warehouse**:  

- **Implantação de Aplicativos -Histórico**: Exibe detalhes de implantação de aplicativo para um aplicativo e computador específicos.  

- **Conformidade de Atualizações de software e do Endpoint Protection**: Exibe computadores com atualizações de software ausentes.  

- **Inventário Geral de Hardware - Histórico**: Exibe todo o inventário de hardware para um computador específico.  

- **Inventário Geral de Software - Histórico**: Exibe todo o inventário de software para um computador específico.  

- **Visão Geral de Integridade da Infraestrutura - Histórico**: Exibe uma visão geral da integridade da infraestrutura do seu Configuration Manager.  

- **Lista de Malwares Detectados - Histórico**:    Exibe os malwares que foram detectados na sua organização.  

- **Resumo de Distribuição de Software - Histórico**: Um resumo da distribuição de software para um anúncio e computador específicos.  



## <a name="site-expansion"></a>Expansão do site

Antes de instalar um site de administração central para expandir um site primário autônomo existente, desinstale a função de ponto de serviço do data warehouse. Depois de instalar o site de administração central, instale a função de sistema de site no site de administração central.  

Ao contrário da movimentação do banco de dados do data warehouse, essa alteração resulta em perda dos dados históricos sincronizadas antes no site primário. Não há suporte para fazer backup de banco de dados do site primário e restaurá-lo no site de administração central.



## <a name="move-the-database"></a>Mover o banco de dados

Use as seguintes etapas para mover o banco de dados de data warehouse para um novo SQL Server:  

1. Use o SQL Server Management Studio para fazer backup do banco de dados de data warehouse. Em seguida, restaure esse banco de dados para um SQL Server no novo computador que hospeda o data warehouse.  

    > [!NOTE]  
    > Depois de restaurar o banco de dados para o novo servidor, verifique se as permissões de acesso ao novo banco de dados de data warehouse são as mesmas do original.  

2. Use o console do Configuration Manager para remover a função do ponto de serviço do data warehouse do servidor atual.  

3. Reinstale o ponto de serviço do data warehouse. Especifique o nome do novo SQL Server e da instância que hospeda o banco de dados de data warehouse restaurado.  

4. A movimentação será concluída depois de instalar a função do sistema de sites.  



## <a name="troubleshooting"></a>Solução de problemas 

### <a name="log-files"></a>Arquivos de log 

Use os seguintes logs para investigar problemas com a instalação do ponto de serviço do data warehouse ou com a sincronização de dados:

- **DWSSMSI.log** e **DWSSSetup.log**: use esses logs para investigar erros ao instalar o ponto de serviço do data warehouse.  

- **Microsoft.ConfigMgrDataWarehouse.log**: use esse log para investigar a sincronização de dados entre o banco de dados do site e o banco de dados do data warehouse.  


### <a name="set-up-failure"></a>Configurar a falha 

Quando a função de ponto de serviço do data warehouse é a primeiro que você instala em um servidor remoto, a instalação falha para o data warehouse.  

#### <a name="workaround"></a>Solução alternativa 
Verifique se o computador no qual você instala o ponto de serviço de data warehouse já hospeda pelo menos outra função.  


### <a name="synchronization-failed-to-populate-schema-objects"></a>Falha da sincronização em preencher objetos de esquema de sincronização 

A sincronização falha com a seguinte mensagem em **Microsoft.ConfigMgrDataWarehouse.log**: `failed to populate schema objects`

#### <a name="workaround"></a>Solução alternativa 
Verifique se a conta de computador da função de sistema de site é um **db_owner** no banco de dados de data warehouse.


### <a name="reports-fail-to-open"></a>A abertura dos relatórios falha

Os relatórios do data warehouse não abrem quando o banco de dados do data warehouse e o ponto de serviço de relatório estão em sistemas de site diferente.  

#### <a name="workaround"></a>Solução alternativa
Conceda a **Conta do Ponto do Reporting Services** a permissão **db_datareader** no banco de dados do data warehouse.


### <a name="error-opening-reports"></a>Erro ao abrir o relatório

Quando você abre um relatório do data warehouse, ele retorna o seguinte erro:

```
An error has occurred during report processing. (rsProcessingAborted)
Cannot create a connection to data source 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection)
A connection was successfully established with the server, but then an error occurred during the pre-login handshake. (provider: SSL Provider, error: 0 - The certificate chain was issued by an authority that is not trusted.)
```

#### <a name="workaround"></a>Solução alternativa 
Use as etapas a seguir para configurar os certificados:

1. No computador que hospeda o banco de dados do data warehouse:  

    1. Abra o IIS, selecione **Certificados de Servidor** e, em seguida, clique com o botão direito do mouse em **Criar Certificado Autoassinado**. Em seguida, especifique o "nome amigável" do nome do certificado como **Certificado de Identificação do Data Warehouse SQL Server**. Selecione o repositório de certificados como **Pessoal**.  

    2. Abra o **SQL Server Configuration Manager**. Em **Configuração de Rede do SQL Server**, clique com o botão direito do mouse para selecionar **Propriedades** em **Protocolos para MSSQLSERVER**. Mude para a guia **Certificado**, selecione **Certificado de Identificação do Data Warehouse SQL Server** como o certificado e salve as alterações.  

    3. No **SQL Server Configuration Manager**, em **Serviços SQL Server**, reinicie o **Serviço SQL Server**. Se o SQL Reporting Services também estiver instalado no servidor que hospeda o banco de dados do data warehouse, reinicie também os serviços **Reporting Service**.  

    4. Abra o MMC (Console de Gerenciamento Microsoft) e adicione o snap-in **Certificados**. Selecione **Conta de computador** do computador local. Expanda a pasta **Pessoal** e selecione **Certificados**. Exporte o arquivo **Certificado de Identificação do Data Warehouse SQL Server** como um arquivo **X.509 binário codificado em DER (. CER)**.  

2. No computador que hospeda o SQL Server Reporting Services, abra o MMC e adicione o snap-in de **Certificados**. Selecione **Conta de computador**. Na pasta **Autoridades de Certificação Raiz Confiáveis**, importe o **Certificado de Identificação do Data Warehouse SQL Server**.  



## <a name="data-flow"></a>Fluxo de dados   

![Diagrama mostrando o fluxo de dados lógicos entre os componentes do site do data warehouse](./media/datawarehouse.png)

#### <a name="data-storage-and-synchronization"></a>Sincronização e armazenamento de dados

| Etapa   | Detalhes  |
|--------|----------|  
| **1**  | O servidor do site transfere e armazena dados no banco de dados do site. |  
| **2**  | O ponto de serviço do data warehouse obtém dados do banco de dados do site com base na sua agenda e configuração. |  
| **3**  | O ponto de serviço do data warehouse transfere e armazena uma cópia dos dados sincronizados no banco de dados de data warehouse. |  


#### <a name="reporting"></a>Relatórios

| Etapa   | Detalhes  |
|--------|----------|  
| **A**  | Com os relatórios internos, um usuário solicita dados. Essa solicitação é passada para o ponto do reporting services usando o SQL Server Reporting Services. |  
| **B**  | A maioria dos relatórios contém informações atuais, e tais solicitações são executadas no banco de dados do site. |  
| **C**  | Quando um relatório solicita dados históricos usando um dos relatórios com uma *Categoria* de **Data Warehouse**, a solicitação é executada no banco de dados de data warehouse. |  
