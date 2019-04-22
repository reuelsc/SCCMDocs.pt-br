---
title: Práticas recomendadas para atualizações de software
titleSuffix: Configuration Manager
description: Use essas práticas recomendadas para atualizações de software no Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.collection: M365-identity-device-management
ms.openlocfilehash: eb5471c5a993a1a2f683807a12dfc01ea00bf275
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59802115"
---
# <a name="best-practices-for-software-updates-in-configuration-manager"></a>Práticas recomendadas para atualizações de software no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo inclui as práticas recomendadas para atualizações de software no Configuration Manager. As informações são classificadas em práticas recomendadas para a instalação inicial e para as operações contínuas.  



## <a name="bkmk_install"></a> Práticas recomendadas de instalação  

Use as seguintes práticas recomendadas ao instalar atualizações de software no Configuration Manager.  


### <a name="bkmk_shared-susdb"></a> Usar um banco de dados do WSUS compartilhado para pontos de atualização de software  

Quando você instalar mais de um ponto de atualização de software em um site primário, use o mesmo banco de dados do WSUS para cada ponto de atualização de software na mesma floresta do Active Directory. Se você compartilhar o mesmo banco de dados, o impacto no desempenho da rede e do cliente que pode ocorrer quando os clientes mudam para um novo ponto de atualização de software será atenuado significativamente, mas não eliminado completamente. Uma verificação delta ainda ocorre quando um cliente muda para um novo ponto de atualização de software que compartilha um banco de dados com o ponto de atualização de software antigo, mas a verificação é muito menor do que seria se o servidor WSUS tivesse seu próprio banco de dados. Para obter mais informações sobre a mudança de ponto de atualização de software, confira [Mudança de ponto de atualização de software](/sccm/sum/plan-design/plan-for-software-updates#BKMK_SUPSwitching).  

> [!IMPORTANT]  
>  Também compartilhe as pastas de conteúdo do WSUS locais ao usar um banco de dados do WSUS compartilhado para pontos de atualização de software.  

Para obter mais informações de como compartilhar o banco de dados do WSUS, confira as postagens no blog a seguir:  

- [How to implement a shared SUSDB for Configuration Manager software update points](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/How-to-implement-a-shared-SUSDB-for-Configuration-Manager/ba-p/274103) (Como implementar um SUSDB compartilhado para pontos de atualização de software do Configuration Manager)  

- [Considerations for multiple WSUS instances sharing a content database when using System Center Configuration Manager](https://blogs.technet.microsoft.com/wsus/2014/03/22/considerations-for-multiple-wsus-instances-sharing-a-content-database-when-using-system-center-configuration-manager-but-without-network-load-balancing-nlb/) (Considerações para várias instâncias doWSUS que compartilham um banco de dados de conteúdo ao usar o System Center Configuration Manager)  


### <a name="bkmk_sql-instance"></a> Quando o Configuration Manager e o WSUS usam o mesmo SQL Server, configure um para usar uma instância nomeada e outro para usar a instância padrão  

Quando os bancos de dados do Configuration Manager e do WSUS compartilham a mesma instância do SQL Server, você não pode determinar facilmente o uso de recursos entre os dois aplicativos. Use instâncias do SQL Server diferentes para o Configuration Manager e para o WSUS. Essa configuração facilita a solução de problemas e o diagnóstico de problemas de uso de recursos que podem ocorrer em cada aplicativo.  


### <a name="bkmk_store-local"></a> Especifique a configuração "Armazenar atualizações localmente"  

Ao instalar o WSUS, selecione a configuração **Armazenar atualizações localmente**. Essa configuração faz com que o WSUS baixe os termos de licença associados com as atualizações de software. Ele baixa os termos durante o processo de sincronização e armazena-os no disco rígido local para o servidor WSUS. Se você não selecionar essa configuração, os computadores cliente poderão não ser aprovados nas verificações de conformidade para atualizações de software que têm termos de licença. O componente **Gerenciador de Sincronização do WSUS** do ponto de atualização de software verifica se essa configuração está habilitada a cada 60 minutos, por padrão.  



## <a name="bkmk_operation"></a> Práticas recomendadas operacionais  

Use as seguintes práticas recomendadas quando for usar atualizações de software:  


### <a name="bkmk_object-limit"></a> Limitar as atualizações de software a 1.000 em uma única implantação de atualização de software  

Limite o número de atualizações de software a 1.000 em cada implantação de atualização de software. Ao criar uma regra de implantação automática, verifique se os critérios especificados não resultam em mais de 1000 atualizações de software. Se você implantar atualizações de software manualmente, não selecione mais de 1000 atualizações.  


### <a name="bkmk_new-group"></a> Criar grupo de atualização de software sempre que uma ADR for executada para "Patch Tuesday" e para implementações gerais  

Há um limite de 1000 atualizações de software em uma implantação. Ao criar uma ADR (regra de implantação automática), especifique se deseja usar um grupo de atualização existente ou criar um novo grupo de atualização sempre que a regra for executada. Se você especificar critérios em uma ADR que resultem em várias atualizações de software e a regra for executada em um agendamento recorrente, crie um novo grupo de atualização de software sempre que a regra for executada. Esse comportamento impede que a implantação ultrapasse o limite de 1000 atualizações de software por implantação.  


### <a name="bkmk_same-group"></a> Usar um grupo de atualização de software existente para ADRs para atualizações de definições do Endpoint Protection  

Se você usa uma ADR para implantar atualizações de definição do Endpoint Protection com frequência, sempre use um grupo de atualização de software existente. Caso contrário, a ADR poderá criar centenas de grupos de atualizações de software ao longo do tempo. Normalmente, os publicadores de atualização de definição configuram as atualizações de definição para expirar quando forem substituídas por quatro atualizações mais recentes. Portanto, o grupo de atualização de software que é criado pela ADR nunca conterá mais de quatro atualizações de definição para o publicador: uma ativa e três substituídas.  



## <a name="see-also"></a>Consulte também  
 [Planejar atualizações de software](/sccm/sum/plan-design/plan-for-software-updates)
