---
title: Painel do Ciclo de Vida do Produto
titleSuffix: Configuration Manager
description: Exiba a Política de Ciclo de Vida da Microsoft com o painel de ciclo de vida do produto no Configuration Manager.
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b8876f00ecb26aabd84f863ee1fcef4f2aac283a
ms.sourcegitcommit: 53f2380ac67025fb4a69fc1651edad15d98e0cdd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65673413"
---
# <a name="manage-microsoft-lifecycle-policy-with-configuration-manager"></a>Gerenciar a Política de Ciclo de Vida da Microsoft com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Começando com a versão 1806, você pode usar o painel de ciclo de vida do produto do Configuration Manager para exibir a Política de Ciclo de Vida da Microsoft. O painel mostra o estado da Política de Ciclo de Vida da Microsoft para produtos da Microsoft instalados em dispositivos gerenciados com o Configuration Manager. Ele também fornece informações sobre os produtos da Microsoft em seu ambiente, o estado da capacidade de suporte e as datas de término do suporte. Use o painel para entender a disponibilidade do suporte para cada produto. Essas informações ajudam a planejar quando atualizar os produtos da Microsoft que você usa, antes que eles atinjam o término do suporte atual.  

Para obter mais informações, confira [Política de Ciclo de Vida da Microsoft](https://support.microsoft.com/lifecycle).

A partir da versão 1810, o painel inclui informações para o System Center 2012 Configuration Manager e posteriores.<!--1358702-->  



## <a name="prerequisites"></a>Pré-requisitos 

 Para ver os dados no painel do ciclo de vida do produto, são necessários os seguintes componentes:  

- O Internet Explorer 9 ou posterior deve estar instalado no computador que executa o console do Configuration Manager.  

- Uma função do ponto de conexão de serviço deve ser instalada e configurada. Para obter atualizações para os dados nesse painel, o ponto de conexão de serviço deve estar online ou deve ser sincronizado regularmente se estiver offline. Para obter mais informações, consulte [Sobre o ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point).

- Um ponto do Reporting Services é necessário para a funcionalidade de hiperlink no painel. Os links do painel para relatórios do SSRS (SQL Server Reporting Services). Para obter mais informações, confira [Reporting in Configuration Manager](/sccm/core/servers/manage/reporting) (Relatórios no Configuration Manager).  

- O ponto de sincronização do Asset Intelligence precisa ser configurado e sincronizado. O painel usa o catálogo do Asset Intelligence como metadados para títulos de produtos. Os metadados são comparados com dados de inventário em sua hierarquia. Para obter mais informações, confira [Configurar o Asset Intelligence no Configuration Manager](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).  

     > [!NOTE]  
     > Se você estiver configurando o ponto de serviço do Asset Intelligence pela primeira vez, escolha a opção [Habilitar classes de inventário de hardware do Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence#BKMK_EnableAssetIntelligence). O painel do ciclo de vida depende dessas classes de inventário de hardware do Asset Intelligence. O painel não exibirá dados até que os clientes tenham examinado e retornado o inventário de hardware.  



## <a name="use-the-product-lifecycle-dashboard"></a>Usar o painel do ciclo de vida do produto

Com base nos dados de inventário que o site coleta dos dispositivos gerenciados, o painel exibe informações sobre todos os produtos atuais. No entanto, as informações exibidas para sistemas operacionais e SQL Server estão limitadas às seguintes versões:

- Windows Server 2008 e posterior
- Windows XP e posterior
- SQL Server 2008 e posterior

Para acessar o painel do ciclo de vida no console do Configuration Manager, acesse o workspace **Ativos e Conformidade**, expanda **Asset Intelligence** e selecione o nó **Ciclo de Vida do Produto**.

> [!NOTE]  
> Os dados no painel são baseados no site ao qual o console do Configuration Manager se conecta. Se o console se conectar ao seu site de nível superior, você verá dados para toda a hierarquia. Quando conectado a um site primário filho, apenas os dados desse site são exibidos.

### <a name="product-lifecycle-dashboard"></a>Painel do Ciclo de Vida do Produto

![Captura de tela do painel do ciclo de vida do produto no console](media/product-lifecycle-dashboard.png)

Altere o modo de exibição selecionando uma das seguintes opções na lista **Categoria de produtos**:  
- **Todos**: exibir todos os produtos juntos  
- **Windows Client**: exibir versões de sistema operacional do cliente Windows  
- **Windows Server**: exibir versões do sistema operacional do Windows Server  
- **Banco de dados**: Exibir versões do SQL Server  
- **Configuration Manager**: iniciando na versão 1810, exibir versões do Configuration Manager 
- **Microsoft Office**: começando na versão 1902, exiba as informações de versões instaladas do Office 2003 até o Office 2016 <!--3556026-->

O painel contém os seguintes blocos:  

- **Cinco principais produtos após o fim da vida útil**: esse bloco é uma exibição de dados consolidada de produtos encontrados em seu ambiente após o fim da vida. O grafo mostra o software instalado que expirou quando comparado com o ciclo de vida do suporte para sistemas operacionais e produtos do SQL Server.  

- **Cinco principais produtos que se aproximam do fim da vida útil**: esse bloco é uma exibição de dados consolidada de produtos encontrados em seu ambiente que estão perto do fim da vida útil nos próximos dezoito meses. O grafo mostra o software instalado que está dentro do período de dezoito meses para o fim da vida útil, em comparação com o ciclo de vida do suporte para sistemas operacionais e produtos do SQL Server.  

- **Dados de ciclo de vida dos produtos instalados**: esse bloco oferece uma ideia geral de quando um produto passará do estado com suporte para o estado expirado. O gráfico fornece um detalhamento do número de clientes em que o produto está instalado, o estado de disponibilidade do suporte e um link para saber mais sobre os próximos passos a serem realizados. A seguinte informação está incluída no gráfico:     
    - Tempo de suporte restante
    - Número no ambiente 
    - Data de término principal do suporte
    - Data de término prolongada do suporte
    - Próximas etapas  

> [!IMPORTANT]  
> As informações apresentadas neste painel são fornecidas para sua conveniência e somente para uso interno em sua empresa. Você não deve depender exclusivamente dessas informações para confirmar a conformidade. Verifique a precisão das informações fornecidas, juntamente com a disponibilidade das informações de suporte acessando a [Política de Ciclo de Vida da Microsoft](https://support.microsoft.com/lifecycle).  



## <a name="reporting"></a>Relatórios

Também há relatórios adicionais disponíveis. No console do Configuration Manager, acesse o workspace **Monitoramento**, expanda **Relatório** e, em seguida, expanda **Relatórios**. Os seguintes novos relatórios são adicionados na categoria **Asset Intelligence**:  

- **Ciclo de vida 01A: computadores com um produto de software específico**: Veja uma lista de computadores nos quais um produto especificado é detectado.  

- **Ciclo de vida 02A: lista de máquinas com produtos expirados na organização**: Veja os computadores que apresentam produtos expirados. Você pode filtrar este relatório pelo nome do produto.

- **Ciclo de vida 03A: lista de produtos expirados encontrados na organização**: Veja detalhes de produtos em seu ambiente que apresentam datas de ciclo de vida expiradas.  

- **Ciclo de vida 04A: visão geral do ciclo de vida de produtos**: Veja uma lista de ciclos de vida de produtos. Filtre a lista por nome do produto e dias para expiração.  

- **Ciclo de vida 05A – painel de ciclo de vida do produto**: Começando na versão 1810, esse relatório inclui informações semelhantes às do painel no console. Selecione uma categoria para exibir a contagem de produtos em seu ambiente e os dias de suporte restantes.  

Para saber mais, confira a [Lista de relatórios](/sccm/core/servers/manage/list-of-reports#asset-intelligence).<!--SCCMDocs issue 997-->  
