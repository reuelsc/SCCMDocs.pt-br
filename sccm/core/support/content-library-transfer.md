---
title: Ferramenta de Transferência da Biblioteca de Conteúdo
titleSuffix: Configuration Manager
description: Use a ferramenta de Transferência da Biblioteca de Conteúdo para transferir o conteúdo de uma unidade de disco para outra em um ponto de distribuição do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7d07bd0a-7012-47f7-8bc5-509a402915b7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f7375a62349aba30ee239aa34fa594650f5a844
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121974"
---
# <a name="content-library-transfer-tool"></a>Ferramenta de Transferência da Biblioteca de Conteúdo

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A ferramenta de Transferência da Biblioteca de Conteúdo é uma das [ferramentas do Configuration Manager](/sccm/core/support/tools). Ela transfere o conteúdo de uma unidade de disco para outra. A ferramenta é projetada para ser executada em sistemas de site do ponto de distribuição. Ela dá suporte a pontos de distribuição colocados com um site ou sistemas de sites remotos.  

A ferramenta é útil para o cenário quando a unidade de disco que hospeda a biblioteca de conteúdo fica cheia. Primeiro adicione ou identifique outro disco rígido com espaço suficiente para hospedar a biblioteca de conteúdo. Em seguida, use **ContentLibraryTransfer.exe** para transferir o conteúdo do disco rígido preenchido antigo para a o novo disco vazio.
 
Depois que a transferência for concluída, o conteúdo estará acessível para computadores cliente do novo local.



## <a name="usage"></a>Uso 

Execute **ContentLibraryTransfer.exe** como um usuário com permissões administrativas no ponto de distribuição. 

#### <a name="syntax"></a>Sintaxe 
`ContentLibraryTransfer.exe –SourceDrive <drive letter of source drive> –TargetDrive <drive letter of destination drive>`

#### <a name="example"></a>Exemplo
`ContentLibraryTransfer –SourceDrive E –TargetDrive G`



## <a name="limitations"></a>Limitações

- Execute a ferramenta localmente no ponto de distribuição. Você não pode executá-la de um computador remoto.  

- Use-a apenas quando os clientes não estiverem acessando ativamente o ponto de distribuição. Se você executar a ferramenta enquanto os clientes estiverem acessando o conteúdo, a biblioteca de conteúdo na unidade de destino poderá ter dados incompletos. A transferência de dados poderá falhar completamente, levando a uma biblioteca de conteúdo inutilizável.  

- Não distribua o conteúdo ao ponto de distribuição quando você executar a ferramenta. Se você executar a ferramenta enquanto o conteúdo está sendo gravado no ponto de distribuição, a biblioteca de conteúdo na unidade de destino poderá ter dados incompletos. A transferência de dados poderá falhar completamente, levando a uma biblioteca de conteúdo inutilizável.



## <a name="see-also"></a>Consulte também

- [Conceitos fundamentais para o gerenciamento de conteúdo](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [Biblioteca de conteúdo](/sccm/core/plan-design/hierarchy/the-content-library)
