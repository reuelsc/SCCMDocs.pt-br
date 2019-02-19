---
title: Ferramenta de Propriedade de Conteúdo
titleSuffix: Configuration Manager
description: Use a Ferramenta de Propriedade de Conteúdo para alterar a propriedade de pacotes órfãos no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 753d2681-ea72-4f47-94d1-ac10188d9d5b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3ba864914afb6794d460b81f5df346902b8ab0ce
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121873"
---
# <a name="content-ownership-tool"></a>Ferramenta de Propriedade de Conteúdo

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A Ferramenta de Propriedade de Conteúdo é uma das [ferramentas do Configuration Manager](/sccm/core/support/tools). Ela muda a propriedade de pacotes órfãos no Configuration Manager. Pacotes órfãos não têm um servidor de site proprietário. Os pacotes podem se tornar órfãos removendo o servidor do site enquanto eles ainda são de propriedade desse servidor do site.

Execute a Ferramenta de Propriedade de Conteúdo em qualquer servidor do site na hierarquia do Configuration Manager. Entre como um usuário administrativo com permissões suficientes de pacote.  

> [!Tip]  
> Use **ContentLibraryCleanup.exe** em `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` para *remover* conteúdo órfão de um ponto de distribuição. Para obter mais informações, veja [Ferramenta de limpeza da biblioteca de conteúdo](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool).  



## <a name="features"></a>Recursos

- Exibir todos os pacotes órfãos  

- Exibir todos os pacotes, mesmo que não estejam órfãos  

- Exibir o status da conexão a um site  

- Filtrar os pacotes por nome, código do site ou tipo de pacote  

- Classificar por qualquer coluna exibida  

- Alterar a atribuição de um ou mais pacotes com uma única ação  

- Exibir o progresso da atividade de transferência de propriedade  



## <a name="usage"></a>Uso

Execute **ContentOwnershipTool.exe** para iniciar a ferramenta. Permissões de administrador local no computador não são necessárias para executar a ferramenta.

Não há parâmetros de linha de comando.

> [!Important]   
> Essa ferramenta muda a propriedade de um pacote de órfão. O pacote em si não se move do ponto de distribuição em que está armazenado. Essa alteração de propriedade não faz o pacote ser atualizado nos pontos de distribuição. Ela também não faz os clientes reavaliarem a política para a implantação do pacote. Depois que a propriedade mudar, verifique se o novo servidor do site pode acessar os arquivos de origem. Ele deve ter pelo menos permissões de **Leitura** para os arquivos de origem de cada pacote. 



## <a name="see-also"></a>Consulte também

- [Conceitos fundamentais para o gerenciamento de conteúdo](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [Biblioteca de conteúdo](/sccm/core/plan-design/hierarchy/the-content-library)
