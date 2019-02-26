---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8305102657a5973c19ca161f65204587954b0232
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754577"
---
Use as seguintes definições para diferenciar entre o piloto e de produção:  

- **Piloto**: Um subconjunto de seus dispositivos que você deseja validar antes de implantar a um conjunto maior. Use análise de área de trabalho para marcar dispositivos como exclusivo para o conjunto de piloto. Dispositivos em projeto-piloto estiver prontos para atualizar quando nenhum ativo está bloqueando. Um bloqueio ativo está marcado como *críticos* e *não é possível* para atualizar.  

- **Produção**: Todos os outros dispositivos registrados para análise de área de trabalho que não estão no projeto-piloto. Dispositivos de produção estão prontos para atualizar quando todos os ativos são assinadas. Análise da área de trabalho aprova automaticamente todos os ativos não críticos.  

