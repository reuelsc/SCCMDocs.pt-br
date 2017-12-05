---
title: Data warehouse
titleSuffix: Configuration Manager
description: "Ponto de serviço e banco de dados do Data Warehouse para o System Center Configuration Manager"
ms.custom: na
ms.date: 8/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 2e6ac983e5ca63dacb77f2e26515d7123748d64d
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2017
---
#  <a name="the-data-warehouse-service-point-for-system-center-configuration-manager"></a>O ponto de serviço do Data Warehouse para o System Center Configuration Manager
*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Começando com a versão 1702, é possível usar o ponto de serviço do Data Warehouse para armazenar e relatar dados históricos de longo prazo para sua implantação do Configuration Manager.

> [!TIP]
> O ponto de serviço do Data Warehouse é um recurso de pré-lançamento apresentado na versão 1702. Para habilitá-lo, confira [Usar recursos de pré-lançamento](/sccm/core/servers/manage/pre-release-features).

> A partir da versão 1706, esse recurso não é mais um recurso de pré-lançamento.

O data warehouse dá suporte a até 2 TB de dados, com carimbos de data e hora para controle de alterações. O armazenamento dos dados é possibilitado por meio de sincronizações automatizadas do banco de dados de site do Configuration Manager para o banco de dados de data warehouse. Essas informações estarão acessíveis no seu ponto do Reporting Services. Os dados que são sincronizados com o banco de dados do data warehouse são retidos por três anos. Periodicamente, uma tarefa interna remove os dados com mais de três anos.

Os dados sincronizados incluem o seguinte dos grupos de Dados Globais e Dados do Site:
- Integridade de infraestrutura
- Segurança
- Conformidade
- Malware   
- Implantações de software
- Detalhes de inventário (no entanto, o histórico de inventário não é sincronizado)

Quando a função de sistema de site é instalada, ele instala e configura o banco de dados do data warehouse. Também instala vários relatórios para que você possa procurar esses dados com facilidade e criar relatórios com base neles.



## <a name="prerequisites-for-the-data-warehouse-service-point"></a>Pré-requisitos para o ponto de serviço do Data Warehouse
- A função do sistema de sites do data warehouse tem suporte apenas no site de nível superior da hierarquia. (Um site de administração central ou site primário autônomo).
- O computador no qual você instala a função do sistema de sites requer o .NET Framework 4.5.2 ou posterior.
- A conta de computador do computador no qual você instala a função de sistema de site é usada para sincronizar os dados com o banco de dados do data warehouse. Essa conta exige as seguintes permissões:  
  - **Administrador** no computador que hospedará o banco de dados do data warehouse.
  - Permissão **DB_Creator** no banco de dados de data warehouse.
  - As permissões **DB_owner** ou **DB_reader** com **execute** para o banco de dados de site de nível superior.
- O banco de dados do data warehouse exige o uso do SQL Server 2012 ou posterior. A edição pode ser Standard, Enterprise ou Datacenter.
- As seguintes configurações do SQL Server têm suporte para hospedar o banco de dados do data warehouse:  
  - Uma instância padrão
  - Instância nomeada
  - Grupo de disponibilidade Always On do SQL Server
  - Cluster de failover do SQL Server
-   Quando o banco de dados do data warehouse é remoto no servidor do site, é necessário ter uma licença separada para cada SQL Server que hospeda o banco de dados.
- Se você usar [exibições distribuídas](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_distviews), a função de sistema de sites do ponto de serviço do data warehouse deve ser instalada no mesmo servidor que hospeda o banco de dados de site de sites de administração central.



> [!IMPORTANT]  
> Não há suporte para o Data Warehouse quando o computador que executa o ponto de serviço do Data Warehouse ou que hospeda o banco de dados do data warehouse é executado em um dos seguintes idiomas:
> - JPN – japonês
> - KOR – coreano
> - CHS – chinês simplificado
> - CHT – chinês tradicional Esse problema será resolvido em uma versão futura.


## <a name="install-the-data-warehouse"></a>Instalar o data warehouse
Cada hierarquia dá suporte a uma única instância dessa função, em qualquer sistema de sites desse site de nível superior. O SQL Server que hospeda o banco de dados para o warehouse pode ser local na função de sistema de site ou remoto. Embora o data warehouse funcione com o ponto do Reporting Services instalado no mesmo site, as duas funções do sistema não precisam ser instaladas no mesmo servidor.   

Para instalar a função, use o **Assistente para Adicionar Funções de Sistema de Site** ou o **Assistente para Criar Funções do Sistema de Site**. Veja [Instalar funções do sistema de sites](/sccm/core/servers/deploy/configure/install-site-system-roles) para obter mais informações.  

Ao instalar a função, o Configuration Manager cria o banco de dados de data warehouse para você em uma instância especificada do SQL Server. Se você especificar o nome de um banco de dados existente (como você faria ao [mover o banco de dados de data warehouse para um novo SQL Server](#move-the-data-warehouse-database)), o Configuration Manager não criará um novo banco de dados, utilizando aquele que você especificou.

### <a name="configurations-used-during-installation"></a>Configurações usadas durante a instalação
Página **Seleção de Função do Sistema**:  

Página **Geral**:
-   **Configurações de conexão do banco de dados do data warehouse do Configuration Manager**:
 - **Nome de domínio totalmente qualificado do SQL Server**:  
 Especifique o FQDN (nome de domínio totalmente qualificado) do servidor que hospeda o banco de dados do ponto de serviço do Data Warehouse.
 - **Nome da instância do SQL Server, se for aplicável**:   
 Se você não usar uma instância padrão do SQL Server, especifique a instância.
 - **Nome do banco de dados**:   
 Especifique um nome para o banco de dados do data warehouse. O nome do banco de dados não pode ultrapassar 10 caracteres. (O tamanho do nome com suporte será aumentado em uma versão futura).
 O Configuration Manager cria o banco de dados do data warehouse com esse nome. Se você especificar um nome de banco de dados que já existe na instância do SQL Server, o Configuration Manager usará esse banco de dados.
 - **Porta do SQL Server usada para conexão**:   
 Especifique o número da porta TCP/IP configurado para o SQL Server que hospeda o banco de dados de data warehouse. Esta porta é usada pelo serviço de sincronização do data warehouse para se conectar ao banco de dados do data warehouse.  

Página **Agenda de sincronização**:   
- **Agenda de sincronização**:
 - **Hora de início**:  
 Especifique a hora de início da sincronização do data warehouse.
 - **Padrão de Recorrência**:
    - **Diário**: especifique a execução diária da sincronização.
    - **Semanal**: especifique um dia de cada semana, e a recorrência semanal para a sincronização.

## <a name="reporting"></a>Relatórios
Depois de instalar um ponto de serviço do Data Warehouse, vários relatórios são disponibilizados no ponto do Reporting Services instalado no mesmo site. Se você instalar o ponto de serviço do Data Warehouse antes de instalar um ponto do Reporting Services, os relatórios serão adicionados automaticamente ao instalar posteriormente o ponto do Reporting Services.

A função de sistema de site do Data Warehouse inclui os seguintes relatórios, que têm uma categoria de **Data Warehouse**:
 - **Implantação de Aplicativos -Histórico**:   
 Exibe detalhes de implantação de aplicativo para um aplicativo e computador específicos.
 - **Proteção de Ponto de Extremidade e Conformidade de Atualização de Software - Histórico**: veja os computadores que não têm atualizações de software.  
 - **Inventário Geral de Hardware - Histórico**:   
 Exibe todo o inventário de hardware para um computador específico.
 - **Inventário Geral de Software - Histórico**:   
 Exibe todo o inventário de software para um computador específico.
 - **Visão Geral de Integridade da Infraestrutura - Histórico**:  
 Exibe uma visão geral da integridade de sua infraestrutura do Configuration Manager
 - **Lista de Malwares Detectados - Histórico**:    
 Exibe os malwares que foram detectados na sua organização.
 - **Resumo de Distribuição de Software - Histórico**:   
 Um resumo da distribuição de software para um anúncio e computador específicos.


## <a name="expand-an-existing-stand-alone-primary-into-a-hierarchy"></a>Expandir um primário autônomo existente para uma hierarquia
Antes de instalar um site de administração central para expandir um site primário autônomo existente, desinstale a função de ponto de serviço do Data Warehouse. Depois de instalar o site de administração central, instale a função de sistema de site no site de administração central.  

Ao contrário da movimentação do banco de dados do data warehouse, essa alteração resulta em perda dos dados históricos sincronizadas antes no site primário. Não há suporte para backup de banco de dados do site primário e restaurá-lo no site de administração central.




## <a name="move-the-data-warehouse-database"></a>Mover o banco de dados de data warehouse
Use as seguintes etapas para mover o banco de dados de data warehouse para um novo SQL Server:

1.  Use o SQL Server Management Studio para fazer backup do banco de dados do data warehouse. Em seguida, restaure esse banco de dados para um SQL Server no novo computador que hospeda o data warehouse.   
> [!NOTE]     
> Depois de restaurar o banco de dados para o novo servidor, verifique se as permissões de acesso ao novo banco de dados de data warehouse são as mesmas do original.  

2.  Use o console do Configuration Manager para remover a função do sistema de sites do ponto do Data Warehouse Service do servidor atual.
3.  Reinstale o ponto de serviço do Data Warehouse e especifique o nome do novo SQL Server e a instância que hospeda o banco de dados de data warehouse restaurado.
4.  A movimentação será concluída depois de instalar a função do sistema de sites.

## <a name="troubleshooting-data-warehouse-issues"></a>Solucionar problemas do data warehouse
**Arquivos de log**:  
Use os seguintes logs para investigar problemas com a instalação do ponto de serviço do Data Warehouse ou com a sincronização de dados:
 - *DWSSMSI.log* e *DWSSSetup.log* ‑ use esses logs para investigar erros ao instalar o ponto de serviço do Data Warehouse.
 - *Microsoft.ConfigMgrDataWarehouse.log* – Use este log para investigar a sincronização de dados entre o banco de dados do site e o banco de dados de data warehouse.

**Configurar a falha**  
 A instalação do ponto de serviço do Data Warehouse falhará em um servidor de sistema de site remoto quando o data warehouse for a primeira função de sistema de sites instalada nesse computador.  
  - **Solução**:   
    Certifique-se de que o computador no qual você está instalando o ponto de serviço do Data Warehouse já hospede pelo menos uma outra função de sistema de site.  


**Problemas de sincronização conhecidos**:   
A sincronização falha com a seguinte mensagem no *Microsoft.ConfigMgrDataWarehouse.log*: **"Falha ao preencher objetos de esquema"**  
 - **Solução**:  
    Certifique-se de que a conta de computador do computador que hospeda a função de sistema de site seja um **db_owner** no banco de dados do data warehouse.

Os relatórios do data warehouse não abrem quando o banco de dados do data warehouse e o ponto de serviço de relatório estão em sistemas de site diferente.  

 - **Solução**:  
    Conceda a **Conta do Ponto do Reporting Services** a permissão **db_datareader** no banco de dados do data warehouse.

Quando você abre um relatório do data warehouse, o seguinte erro retorna:

*Ocorreu um erro durante o processamento do relatório. (rsProcessingAborted) Não é possível criar uma conexão com a fonte de dados 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection) Uma conexão foi estabelecida com êxito com o servidor, mas ocorreu um erro durante o handshake pré-logon. (provedor: Provedor SSL, erro: 0 - A cadeia de certificado foi emitida por uma autoridade não confiável.)*

- **Solução**: use as etapas a seguir para configurar os certificados:

  1. No computador que hospeda o banco de dados do data warehouse:

    1. Abra o IIS, clique em **Certificados de Servidor**, clique com o botão direito em **Criar um Certificado Autoassinado** e especifique o "nome amigável" do nome do certificado como **Certificado de Identificação do Data Warehouse SQL Server**. Selecione o repositório de certificados como **Pessoal**.
    2. Abra **SQL Server Configuration Manager**, em **Configuração de Rede do SQL Server**, clique com o botão direito para selecionar **Propriedades** em **Protocolos para MSSQLSERVER**. Em seguida, na guia **Certificado**, selecione **Certificado de Identificação do Data Warehouse SQL Server** como o certificado e salve as alterações.  
    3. Abra **SQL Server Configuration Manager**, em **Serviços do SQL Server**, reinicie **Serviço do SQL Server** e **Reporting Service**.
    4.  Abra o Console de Gerenciamento da Microsoft (MMC) e adicione o snap-in para **Certificados**, escolha gerenciar o certificado para **Conta de computador** do computador local. Em seguida, no MMC, expanda o **Pessoal** pasta > **Certificados** e exporte o **Certificado de Identificação do Data Warehouse SQL Server** como um arquivo **Binário X.509 codificado por DER (.CER)**.    
  2.    No computador que hospeda os Serviços de Relatório do SQL Server, abra o MMC e adicione o snap-in para **Certificados**. Em seguida, selecione para gerenciar certificados para **Conta do computador**. Na pasta **Autoridades de Certificação Raiz Confiáveis**, importe o **Certificado de Identificação do Data Warehouse SQL Server**.


## <a name="data-warehouse-dataflow"></a>Fluxo de Dados do Data Warehouse   
![Datawarehouse_flow](./media/datawarehouse.png)

**Sincronização e armazenamento de dados**

| Etapa   | Detalhes  |
|:------:|-----------|  
| **1**  |  O servidor do site transfere e armazena dados no banco de dados do site.  |  
| **2**  |      O ponto de serviço do Data Warehouse obtém dados do banco de dados do site com base na sua agenda e configuração.  |  
| **3**  |  O ponto de serviço do Data Warehouse transfere e armazena uma cópia dos dados sincronizados no banco de dados de data warehouse. |  
**Relatórios**

| Etapa   | Detalhes  |
|:------:|-----------|  
| **A**  |  Com os relatórios internos, um usuário solicita dados. Essa solicitação é passada para o ponto do Reporting Services usando o SQL Server Reporting Services. |  
| **B**  |      A maioria dos relatórios contém informações atuais, e tais solicitações são executadas no banco de dados do site. |  
| **C**  | Quando um relatório solicita dados históricos usando um dos relatórios com uma *Categoria* de **Data Warehouse**, a solicitação é executada no banco de dados de data warehouse.   |  
