---
title: Introdução à emissão de relatórios
titleSuffix: Configuration Manager
description: Saiba mais sobre o conjunto de ferramentas e recursos disponível para gerenciar relatórios no Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 760b159114796922e2c8707e3b7f14484591f7a2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141486"
---
# <a name="introduction-to-reporting-in-system-center-configuration-manager"></a>Introdução à emissão de relatórios no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os relatórios no System Center Configuration Manager fornece um conjunto de ferramentas e recursos que ajudam a usar os recursos avançados de relatórios do SSRS (SQL Server Reporting Services) e a sofisticada experiência de criação que o Reporting Services Report Builder oferece. Os relatórios ajudam a coletar, organizar e apresentar informações sobre usuários, inventário de hardware e software, atualizações de software, aplicativos, status do site e outras operações do Configuration Manager na sua organização. A geração de relatórios fornece vários relatórios predefinidos que você pode usar sem alterações ou que você pode modificar para atender a seus requisitos, e você pode criar relatórios personalizados. Use as seções a seguir para ajudá-lo a gerenciar os relatórios no Configuration Manager.  

##  <a name="BKMK_SQLServerReportingServices"></a> SQL Server Reporting Services  
 O SQL Server Reporting Services oferece uma gama completa de ferramentas e serviços prontos para uso para ajudá-lo a criar, implantar e gerenciar relatórios para sua organização, além de recursos de programação que permitem estender e personalizar sua funcionalidade de geração de relatórios. O Reporting Services é uma plataforma de relatórios baseada em servidor que oferece funcionalidade de relatório abrangente para uma variedade de fontes de dados.  

 O Configuration Manager usa o SQL Server Reporting Services como sua solução de relatórios. A integração com o Reporting Services fornece as seguintes vantagens:  

- Usa um sistema de relatórios padrão para consultar o banco de dados do Configuration Manager.  

- Exibe relatórios usando o Visualizador de Relatórios do Configuration Manager ou o Gerenciador de Relatórios, uma conexão baseada na Web com o relatório.  

- Oferece escalabilidade, disponibilidade e alto desempenho.  

- Fornece assinaturas para relatórios que os usuários podem assinar; por exemplo, um gerente pode assinar para receber automaticamente um relatório por email todo dia e que detalhe o status de uma distribuição de atualização de software.  

- Exporta relatórios que os usuários podem selecionar em uma variedade de formatos populares.  

  Para obter mais informações sobre o Reporting Services, consulte [SQL Server Reporting Services](http://go.microsoft.com/fwlink/p/?LinkID=212032) nos Manuais Online do SQL Server 2008.  

##  <a name="BKMK_ReportingServicesPoint"></a> Ponto do Reporting Services  
 O ponto do Reporting Services é uma função do sistema de site que está instalada em um servidor com o Microsoft SQL Server Reporting Services. O ponto do Reporting Services copia as definições de relatório do Configuration Manager para o Reporting Services, cria pastas de relatórios baseadas em categorias de relatório e define políticas de segurança nessas pastas e relatórios com base nas permissões baseadas em funções para usuários administrativos do Configuration Manager. Em um intervalo de 10 minutos, o ponto do Reporting Services conecta-se ao Reporting Services para reaplicar a política de segurança caso ele tenha sido alterada, por exemplo, usando o Gerenciador de Relatórios. Para obter mais informações sobre como planejar e instalar um ponto do Reporting Services, consulte a documentação a seguir:  

-   [Planejamento para emissão de relatórios no System Center Configuration Manager](planning-for-reporting.md)  

-   [Configurando relatórios no System Center Configuration Manager](configuring-reporting.md)  

##  <a name="BKMK_ConfigurationManagerReports"></a> Relatórios do Configuration Manager  
 O Configuration Manager fornece definições de relatório para mais de 400 relatórios em mais de 50 pastas de relatório, que são copiadas para a pasta de relatório raiz no SQL Server Reporting Services durante o processo de instalação do ponto do Reporting Services. Os relatórios são exibidos no console do Configuration Manager e organizados em subpastas com base na categoria do relatório. Os relatórios não são propagados para cima nem para baixo na hierarquia do Configuration Manager; eles são executados somente contra o banco de dados do site em que são criados. Entretanto, como o Configuration Manager replica dados globais em toda a hierarquia, você tem acesso a informações de toda a hierarquia. Quando um relatório recupera dados de um banco de dados do site, ele tem acesso aos dados do site para o site atual e sites filho, além de dados globais para cada site na hierarquia. Assim como outros objetos do Configuration Manager, um usuário administrativo deve ter as permissões apropriadas para executar ou modificar relatórios. Para executar um relatório, um usuário administrativo deve ter a permissão **Executar Relatório** para o objeto. Para criar ou modificar um relatório, um usuário administrativo deve ter a permissão **Modificar Relatório** para o objeto.  

###  <a name="BKMK_CreatingReports"></a> Criando e modificando relatórios  
 O Configuration Manager usa o Construtor de Relatórios do Microsoft SQL Server como ferramenta exclusiva de criação e edição para relatórios baseados em modelo e em SQL. Quando você cria ou edita um relatório no console do Configuration Manager, o Construtor de Relatórios é aberto. Para obter mais informações sobre como gerenciar relatórios, consulte [Operações e manutenção de relatórios no System Center Configuration Manager](operations-and-maintenance-for-reporting.md).  

###  <a name="BKMK_RunningReports"></a> Executando relatórios  
 Quando você executa um relatório no console do Configuration Manager, o Visualizador de Relatórios é aberto e se conecta ao Reporting Services. Depois que você especifica os parâmetros de relatório necessários, o Reporting Services irá recuperar os dados e exibir os resultados no visualizador. Você também pode conectar-se ao SQL Services Reporting Services, conectar-se à fonte de dados do site e executar relatórios.  

###  <a name="BKMK_ReportPrompts"></a> Solicitações de relatório  
 Uma solicitação de relatório ou um parâmetro de relatório no Configuration Manager é uma propriedade do relatório que você configura quando um relatório é criado ou modificado. As solicitações de relatório são criadas para limitar ou apontar os dados que um relatório recupera. Um relatório pode conter mais de uma solicitação desde que os nomes da solicitação seja únicos e contenham somente caracteres alfanuméricos de acordo com as regras do SQL Server para identificadores.  

 Quando você executa um relatório, a solicitação requer um valor para o parâmetro solicitado e, com base no valor, recupera os dados do relatório. Por exemplo, o relatório **Informações de um computador específico** recupera as informações de um computador específico e solicita ao usuário administrativo um nome do computador. O Reporting Services passa o valor específico para uma variável definida na instrução SQL do relatório.  

###  <a name="BKMK_ReportLinks"></a> Links de relatório  
 Os links de relatório no Configuration Manager são usados em um relatório de origem para fornecer aos usuários administrativos fácil acesso a dados adicionais, como informações mais detalhadas sobre cada item no relatório de origem. Se o relatório de destino requerer a execução de uma ou mais solicitações, o relatório de origem deverá conter uma coluna com os valores apropriados para cada solicitação. Você deve especificar o número da coluna que fornece o valor para a solicitação. Por exemplo, você pode vincular um relatório que lista computadores descobertos recentemente a um relatório que lista as últimas mensagens recebidas de um computador específicos. Quando o link é criado, você pode especificar que a coluna 2 no relatório de origem contém nomes de computadores, que é uma solicitação necessária para o relatório de destino. Quando o relatório de origem é executado, ícones do link aparecem à esquerda de cada linha de dados. Quando você clica no ícone em uma linha, o Visualizador de Relatórios passa o valor na coluna especificada para a linha como o valor da solicitação necessário para exibir o relatório de destino. Um relatório pode ser configurado somente com um link, e esse link pode se conectar somente a um recurso de destino.  

> [!WARNING]  
>  Se você mover um relatório de destino para outra pasta de relatório, o local do relatório de destino será alterado. O link do relatório no relatório de origem não é atualizado automaticamente com o novo local, e o link do relatório não funcionará no relatório de origem.  

##  <a name="BKMK_ReportFolders"></a> Pastas de relatório  
 As pastas de relatório no System Center Configuration Manager fornecem um método para classificar e filtrar relatórios armazenados no Reporting Services. As pastas de relatório são especialmente úteis quando você tem vários relatórios para gerenciar. Quando você instala um ponto do Reporting Services, os relatórios são copiados para o Reporting Services e organizados em mais de 50 pastas de relatório. As pastas de relatório são somente leitura. Não é possível modificá-las no console do Configuration Manager.  

##  <a name="BKMK_ReportSubscriptions"></a> Assinaturas de relatório  
 Uma assinatura de relatório no Reporting Services é uma solicitação recorrente para entregar um relatório em uma hora específica ou em resposta a um evento, e em um formato de arquivo do aplicativo especificado na assinatura. As assinaturas oferecem uma alternativa para executar um relatório sob demanda. Os relatórios sob demanda requerem que você selecione ativamente o relatório sempre que desejar exibir o relatório. Por outro lado, as assinaturas podem ser usadas para agendar e automatizar a entrega de um relatório.  

 É possível gerenciar assinaturas de relatório no console do Configuration Manager. Elas são processadas no servidor de relatório. As assinaturas são distribuídas com o uso de extensões de entrega que são implantadas no servidor. Por padrão, você pode criar assinaturas que enviam relatórios a uma pasta compartilhada ou a um endereço de email. Para obter mais informações sobre como gerenciar inscrições em relatórios, consulte [Operações e manutenção de relatórios no System Center Configuration Manager](operations-and-maintenance-for-reporting.md).  

##  <a name="BKMK_ReportBuilder"></a> Construtor de Relatórios  
 O Configuration Manager usa o Construtor de Relatórios do Microsoft SQL Server Reporting Services como ferramenta exclusiva de criação e edição para relatórios baseados em modelo e em SQL. Quando você inicia a ação de criar ou editar um relatório no console do Configuration Manager, o Construtor de Relatórios é aberto. Quando você cria ou modifica um relatório pela primeira vez, o Construtor de Relatórios é instalado automaticamente. A versão do Construtor de Relatórios associada à versão instalada do SQL Server é aberta quando você executa ou edita relatórios.  

 A instalação do Construtor de Relatórios adiciona suporte para mais de 20 idiomas. Quando você executa o Construtor de Relatórios, ele exibe dados no idioma do sistema operacional executado no computador local. Se o Construtor de Relatórios não oferecer suporte ao idioma, os dados serão exibidos em inglês. O Construtor de Relatórios oferece suporte a todos os recursos do SQL Server 2008 Reporting Services, que inclui os seguintes recursos:  

- Oferece um ambiente de criação de relatórios intuitivos com uma aparência semelhante ao Microsoft Office.  

- Oferece o layout flexível de relatório da RDL (Linguagem de Definição de Relatório) do SQL Server 2008.  

- Fornece várias formas de visualização de dados, incluindo gráficos e medidores.  

- Fornece caixas de texto com formatação sofisticada.  

- Exporta para o formato do Microsoft Word.  

  Você também pode abrir o Construtor de Relatórios do SQL Server Reporting Services.  

##  <a name="BKMK_ReportModels"></a> Modelos de relatório no SQL Server Reporting Services  
 O SQL Reporting Services no Configuration Manager usa modelos de relatório para ajudar usuários administrativos a selecionar itens do banco de dados para incluir nos relatórios baseados em modelos. Para o usuário administrativo que está criando o relatório, os modelos de relatório expõem somente exibições e itens especificados dos quais escolher. Para criar relatórios baseados em modelos, pelo menos um modelo de relatório deve estar disponível. Os modelos de relatório têm os seguintes recursos:  

- Você pode dar nomes de negócios lógicos a campos e exibições de banco de dados para facilitar a produção de relatórios. Não é necessário conhecimento da estrutura de banco de dados para produzir relatórios.  

- Você pode agrupar itens logicamente.  

- Você pode definir relações entre itens.  

- Você pode proteger elementos do modelo para que usuários administrativos possam ver somente os dados aos quais eles têm permissão para ver.  

  Embora o Configuration Manager forneça exemplo dos modelos de relatório, também é possível definir modelos de relatório para atender a seus requisitos de negócios. Para obter mais informações sobre como criar modelos de relatório, veja [Creating custom report models for System Center Configuration Manager in SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md)(Criando modelos de relatório personalizados para o System Center Configuration Manager no SQL Server Reporting Services).  

## <a name="next-steps"></a>Próximas etapas
[Planejamento para relatórios](planning-for-reporting.md)
