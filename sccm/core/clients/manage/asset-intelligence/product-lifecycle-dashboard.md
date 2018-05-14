---
title: Painel do Ciclo de Vida do Produto
titleSuffix: Configuration Manager
description: Obtenha informações sobre o Painel do Ciclo de Vida do Produto no System Center Configuration Manager.
ms.date: 02/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 8f24fcd2d75d34e2d2d69c9c54f4f47991be7301
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="use-the-product-lifecycle-dashboard-to-manage-microsoft-lifecycle-policy-in-system-center-configuration-manager"></a>Use o Painel do Ciclo de Vida do Produto para gerenciar a Política de Ciclo de Vida da Microsoft no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

A partir da [versão Technical Preview 1802](/sccm/core/get-started/capabilities-in-technical-preview-1802), você pode usar o Painel do Ciclo de Vida do Produto do Configuration Manager. O painel mostra o estado da política do Ciclo de Vida do Produto da Microsoft para produtos da Microsoft instalados em dispositivos gerenciados com o Configuration Manager. O painel fornece informações sobre produtos da Microsoft em seu ambiente, estado de capacidade de suporte e datas de término do suporte. Você pode usar o painel para entender a disponibilidade de suporte para cada produto. Ajudando você a planejar quando atualizar os produtos da Microsoft que você usa antes do término de seu período de suporte.  

Para saber mais sobre a Política do Ciclo de Vida do Produto da Microsoft, confira [Política do Ciclo de Vida da Microsoft](https://support.microsoft.com/en-us/lifecycle).

## <a name="prerequisites"></a>Pré-requisitos 

 Para ver os dados no Painel do Ciclo de Vida do Produto, são necessários os seguintes: 
- O Internet Explorer 9 ou posterior deve estar instalado no computador que executa o console do Configuration Manager. 
- É necessário um Ponto de Serviços de Relatórios para a funcionalidade de hiperlink no painel, uma vez que eles se vinculam a um relatório do SQL Server Reporting Services (SSRS). Para obter mais informações, consulte [Relatórios no System Center Configuration Manager](/sccm/core/servers/manage/reporting). 
- O ponto de sincronização do Asset Intelligence deve ser configurado e sincronizado. Para mais informações, consulte [Configurar o Asset Intelligence no System Center Configuration Manager](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).

Os dados no painel dependem de ter o ponto de sincronização do Asset Intelligence instalado. O painel usa o catálogo do Asset Intelligence como metadados para títulos de produtos. Os metadados são comparados com dados de inventário em sua hierarquia. 

>[!NOTE]
>Se você estiver configurando o ponto de serviço do Asset Intelligence pela primeira vez, certifique-se de [Habilitar as classes de inventário de hardware do Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence#BKMK_EnableAssetIntelligence). O Painel do Ciclo de Vida é dependente das classes de inventário de hardware do Asset Intelligence e não exibirá dados até que os clientes tenham verificado e devolvido o inventário de hardware.  

## <a name="use-the-microsoft-product-lifecycle-dashboard"></a>Use o Painel do Ciclo de Vida do Produto da Microsoft

Com base nos dados de inventário coletados em dispositivos gerenciados, o painel exibe informações sobre todos os produtos atuais. No entanto, as informações exibidas para sistemas operacionais e SQL Server estão limitadas às seguintes versões:

- Windows Server 2008 e posterior
- Windows XP e posterior
- SQL Server 2008 e posterior

Para acessar o Painel do Ciclo de Vida, no console do Configuration Manager, vá para **Ativos e conformidade** > **Asset Intelligence** > **Ciclo de Vida do Produto**.

>[!NOTE]
>Os dados no painel são baseados no site ao qual o console do Configuration Manager se conecta. Se o console se conectar ao seu site de nível superior, você verá dados para toda a hierarquia. Quando conectado a um site primário filho, apenas os dados desse site são exibidos.

### <a name="product-lifecycle-dashboard"></a>Painel do Ciclo de Vida do Produto

![Painel do Ciclo de Vida do Produto](/sccm/core/clients/manage/asset-intelligence/media/product-lifecycle-dashboard.png)

O painel contém os seguintes blocos: 
- **Os cinco principais produtos após o fim da vida útil:** Este bloco é uma visão de dados consolidada de produtos encontrados em seu ambiente após o fim de sua vida útil. O gráfico mostra o software instalado que expirou quando comparado com o ciclo de vida do suporte para sistemas operacionais e produtos do SQL Server.  
- **Os cinco principais produtos que se aproximam ao fim da vida útil:** Este bloco é uma visão de dados consolidada de produtos encontrados em seu ambiente que estão perto do fim da vida útil. O gráfico mostra o software instalado que está dentro do período de seis meses do ciclo de vida quando comparado com o ciclo de vida do suporte para sistemas operacionais e produtos do SQL Server.
- **Dados do ciclo de vida para produtos instalados:** Este bloco dá uma ideia geral de quando um produto transita do estado de “com suporte” para o estado “expirado”. O gráfico fornece uma especificação do número de clientes onde o produto está instalado, o estado de disponibilidade do suporte, juntamente com um link para saber mais sobre os próximos passos a serem realizados. A seguinte informação está incluída no gráfico:     
    - Tempo de suporte restante
    - Número no ambiente 
    - Data de término principal do suporte
    - Data de término prolongada do suporte
    - Próximas etapas 

>[!IMPORTANT]
>As informações apresentadas neste painel são fornecidas para sua conveniência e somente para uso interno em sua empresa. Você não deve depender exclusivamente dessas informações para confirmar a conformidade. Não deixe de verificar a precisão das informações fornecidas para você, juntamente com a disponibilidade de informações de suporte acessando https://support.microsoft.com/en-us/lifecycle.

## <a name="reporting"></a>Relatórios
Os seguintes novos relatórios são adicionados na categoria **Ciclo de Vida do Produto**:
- **Visão geral do Ciclo de Vida do Produto:** Veja uma lista de ciclos de vida de produtos. A lista pode ser filtrada pelo nome do produto e pelos dias até a expiração definível pelo usuário. 
- **Computadores com um produto de software específico:** Veja uma lista de computadores na qual um produto especificado é detectado.
- **Lista de produtos expirados encontrados na organização:** Veja detalhes de produtos em seu ambiente cujas datas do ciclo de vida tenham expirado. 
- **Lista de máquinas com produtos expirados na organização:** Veja computadores que têm produtos expirados neles. Você pode filtrar este relatório pelo nome do produto.

## <a name="next-steps"></a>Próximas etapas
Para obter informações de como instalar ou atualizar o branch da technical preview, consulte [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).  

