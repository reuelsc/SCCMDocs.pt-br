---
title: Cliente de interoperabilidade estendida
titleSuffix: Configuration Manager
description: Saiba mais sobre como usar o cliente de interoperabilidade estendida para dar suporte de longo prazo de um cliente do Configuration Manager estático com um site de branch atual.
ms.date: 05/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e339d096b64bb35cd344e601212ae5ec1f5504ec
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56119608"
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Usar o software cliente do Configuration Manager para interoperabilidade estendida com versões futuras de um site do Branch Atual

*Aplica-se a: System Center Configuration Manager (Branch Atual)*  

Os requisitos de sua empresa podem não permitir a atualização regular do cliente do Configuration Manager em alguns dispositivos. Por exemplo, talvez você precise estar em conformidade com políticas de gerenciamento de alterações, ou o dispositivo pode ser essencial. Acomode essas necessidades instalando um novo cliente para uso de longo prazo, chamado de EIC (cliente de interoperabilidade estendida). O EIC só deve ser usado para dispositivos específicos que não são atualizados com frequência, como quiosque ou dispositivos de ponto de venda. Continue a usar a [atualização automática do cliente](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade) para a maioria dos seus clientes. 

## <a name="how-this-scenario-works"></a>Como este cenário funciona

Normalmente, quando você instala uma nova [atualização no console](/sccm/core/servers/manage/install-in-console-updates) para o Configuration Manager, os clientes atualizam automaticamente o software cliente para que possam usar esses novos recursos. Neste cenário, você ainda atualiza para o branch atual e recebe as atualizações e os novos recursos. A maioria dos dispositivos atualiza o software cliente do Configuration Manager com cada atualização de versão que você instalar. No entanto, em um subconjunto de sistemas críticos que você não deseja receber atualizações de software cliente, instale o cliente de interoperabilidade estendida. Esses clientes não instalam o novo software cliente até que você implante explicitamente uma nova versão do software cliente neles.



## <a name="supported-versions"></a>Versões com suporte
A tabela a seguir lista as versões do cliente do Configuration Manager com suporte para este cenário:

| Version  | Data de disponibilidade  | Data de término do suporte  |
|---------|---------|---------|
|1802<br/>5.00.8634     | 1º de maio de 2018        | Não anterior a 1º de maio de 2020        |
|1606<br/>5.00.8412     | 18 de novembro de 2016        | 1º de maio de 2019        |

> [!TIP]  
> O EIC tem suporte de pelo menos dois anos a partir da data de lançamento. Para mais informações sobre as datas de lançamento, veja [Suporte para versões do branch atual do System Center Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).  

Planeje atualizar o cliente de interoperabilidade estendida em dispositivos gerenciados com o branch atual antes que o suporte do cliente expire. Para fazer isso, baixe uma nova versão do cliente da Microsoft e, em seguida, implante esse software cliente atualizado nos dispositivos que usam o cliente de interoperabilidade estendida atual.



## <a name="how-to-use-the-eic"></a>Como usar o EIC

1. Obter uma versão com suporte do EIC da pasta `\SMSSETUP\Client` da mídia de instalação de atualização do Configuration Manager. Copie todo o conteúdo da pasta.  

2. Instale manualmente o EIC nos dispositivos. Para obter mais informações, veja [Instalar manualmente o cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).  

    > [!Important]  
    > Ao atualizar os clientes da versão 1606 para a versão 1802, use a opção CCMSETUP **/AlwaysExcludeUpgrade:True**. Caso contrário, o cliente poderá receber a política do ponto de gerenciamento para atualizar automaticamente antes da política de exclusão.

3. Adicione esses dispositivos a uma coleção e exclua a coleção das atualizações automáticas do cliente. Para obter mais informações, consulte [Usar o upgrade automático do cliente](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade).  

> [!TIP]  
> Para localizar a mídia do Configuration Manager no VLSC [Centro de Serviços de Licenciamento por Volume](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), acesse a guia **Downloads e Chaves**, pesquise `System Center Config` e selecione **System Center Config Mgr (branch atual)**.



## <a name="limitations-of-the-extended-interoperability-client"></a>Limitações do cliente de interoperabilidade estendida

- Atualizações para o software cliente de interoperabilidade estendida não estão disponíveis por meio de atualizações no console. Para obter mais informações sobre como atualizar clientes EIC, veja [Como usar o EIC](#how-to-use-the-eic).  

- O EIC só é compatível com os seguintes recursos:  

   - Atualizações de software  
   - Inventário de hardware e software
   - Pacotes e programas



## <a name="next-steps"></a>Próximas etapas

Para garantir que os clientes estejam instalados corretamente nos dispositivos que você deseja, veja [Como monitorar os clientes](/sccm/core/clients/manage/monitor-clients).
