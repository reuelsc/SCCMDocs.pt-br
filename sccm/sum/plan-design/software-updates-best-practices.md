---
title: "Práticas recomendadas para atualizações de software | Microsoft Docs"
description: "Use as práticas recomendadas para atualizações de software no System Center Configuration Manager."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.openlocfilehash: 5df20f3703442de1be6220ca2770e182e330c036
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="best-practices-for-software-updates-in-system-center-configuration-manager"></a>Práticas recomendadas para atualizações de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico inclui as práticas recomendadas para atualizações de software no System Center Configuration Manager. As informações são classificadas em práticas recomendadas para a instalação inicial e práticas recomendadas para operações contínuas.  

## <a name="installation-best-practices"></a>Práticas recomendadas de instalação  
 Use as seguintes práticas recomendadas ao instalar atualizações de software no Configuration Manager.  

### <a name="use-a-shared-wsus-database-for-software-update-points"></a>Usar um banco de dados compartilhado do WSUS para pontos de atualização de software  
 Quando você instalar mais de um ponto de atualização de software em um site primário, use o mesmo banco de dados do WSUS para cada ponto de atualização de software na mesma floresta do Active Directory. Compartilhando o mesmo banco de dados, é possível reduzir significativamente o impacto sobre o desempenho do cliente e da rede que pode ocorrer quando clientes mudam para um novo ponto de atualização de software. Quando um cliente muda para a um novo ponto de atualização de software que compartilha um banco de dados com o ponto de atualização de software antigo, uma verificação delta ainda ocorre, mas essa verificação é bem menor do que seria se o servidor do WSUS tivesse o próprio banco de dados.  

> [!IMPORTANT]  
>  Você também deve compartilhar as pastas de conteúdo do WSUS locais quando usar um banco de dados compartilhado do WSUS para pontos de atualização de software.  

 Para saber mais sobre a troca do ponto de atualização de software, consulte a seção [Troca de ponto de atualização de software](../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching) no tópico [Planejar atualizações de software no System Center Configuration Manager](../../sum/plan-design/plan-for-software-updates.md).  

### <a name="when-configuration-manager-and-wsus-use-the-same-sql-server-configure-one-of-these-to-use-a-named-instance-and-the-other-to-use-the-default-instance-of-sql-server"></a>Quando o Configuration Manager e o WSUS usam o mesmo SQL Server, configurar um deles para usar uma instância nomeada e o outro para usar a instância padrão do SQL Server  
 Quando os bancos de dados do Configuration Manager e do WSUS usam o mesmo SQL Server e compartilham a mesma instância do SQL Server, não é possível determinar facilmente o uso de recursos entre os dois aplicativos. Quando instâncias diferentes do SQL Server são usada para o Configuration Manager e para o WSUS, é mais fácil solucionar e diagnosticar problemas de uso de recursos que podem ocorrer em cada aplicativo.  

### <a name="specify-the-store-updates-locally-setting-for-the-wsus-installation"></a>Especificar a configuração "Armazenar atualizações localmente" para a instalação do WSUS  
 Ao instalar o WSUS, selecione a configuração **Armazenar atualizações localmente**. Quando essa configuração é selecionada, os termos de licença associados às atualizações de software são baixados durante o processo de sincronização e armazenados no disco rígido local do servidor do WSUS. Quando essa configuração não é selecionada, os computadores cliente podem falhar em verificar a conformidade das atualizações de software que possuem termos de licença. Ao instalar o ponto de atualização de software, o Gerenciador de Sincronização do WSUS verifica se que essa configuração está habilitada a cada 60 minutos, por padrão.  

## <a name="operational-best-practices"></a>Práticas recomendadas operacionais  
 Use as seguintes práticas recomendadas quando for usar atualizações de software:  

### <a name="limit-software-updates-to-1000-in-a-single-software-update-deployment"></a>Limitar as atualizações de software a 1.000 em uma única implantação de atualização de software  
 É necessário limitar o número de atualizações de software a 1000 para cada implantação de atualização de software. Ao criar uma regra de implantação automática, verifique se os critérios especificados não resultam em mais de 1000 atualizações de software. Ao implantar atualizações de software manualmente, não selecione mais de 1.000 atualizações para implantar.  

### <a name="create-a-new-software-update-group-each-time-an-automatic-deployment-rule-runs-for-patch-tuesday-and-for-general-deployment"></a>Criar um novo grupo de atualizações de software sempre que uma regra de implantação automática for executada para a Patch Tuesday e para implantação geral  
 Há um limite de 1000 atualizações de software por implantação de atualização de software. Ao criar uma regra automática de implantação, você especifica se é para usar um grupo existente de atualizações ou criar um novo grupo de atualizações sempre que a regra for executada. Quando for especificar os critérios em uma regra de implantação automática que resulta em várias atualizações de software e a regra for executada em uma programação recorrente, especifique para criar um novo grupo de atualizações sempre que a regra for executada. Isso impedirá que a implantação ultrapasse o limite de 1000 atualizações de software por implantação.  

### <a name="use-an-existing-software-update-group-for-automatic-deployment-rules-for-endpoint-protection-definition-updates"></a>Usar um grupo de atualizações de software existente para as regras de implantação automática de atualizações de definições do Endpoint Protection  
 Use sempre um grupo de atualizações de software existente quando usar uma regra de implantação automática para implantar atualizações de definição do Endpoint Protection com frequência. Caso contrário, possivelmente centenas de grupos de atualizações de software serão criados ao longo do tempo. Normalmente, os editores das atualizações de definição configuram as atualizações de definição para expirar quando elas são substituídas por quatro atualizações mais recentes. Portanto, o grupo de atualizações de software criado pela regra de implantação automática nunca conterá mais de quatro atualizações de definição para o fornecedor: uma ativa e três substituídas.  

## <a name="see-also"></a>Consulte também  
 [Planejar atualizações de software no System Center Configuration Manager](../../sum/plan-design/plan-for-software-updates.md)
