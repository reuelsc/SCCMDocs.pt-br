---
title: Associar usuários a um computador
titleSuffix: Configuration Manager
description: Configure o Configuration Manager para associar os usuários a computadores de destino ao implantar sistemas operacionais.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bb271aa0ea5733e956d7ba244374af9437db3d6c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131873"
---
# <a name="associate-users-with-a-destination-computer-in-configuration-manager"></a>Associar usuários ao computador de destino no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Ao usar o Configuration Manager para implantar sistemas operacionais, é possível associar usuários ao computador de destino. Essa opção funciona se um único usuário ou vários usuários forem os usuários primários do computador de destino.  

 A afinidade de dispositivo de usuário oferece suporte ao gerenciamento centrado no usuário para a implantação de aplicativos. Ao associar um usuário ao computador de destino em que um SO será instalado, é possível implantar aplicativos para esse usuário posteriormente, e os aplicativos são instalados automaticamente no computador de destino. Embora você possa configurar o suporte para a afinidade de dispositivo de usuário durante a implantação do SO, não é possível usar a afinidade de dispositivo de usuário para implantar o SO.  

 Para obter mais informações sobre afinidade de dispositivo de usuário, consulte [Vincular usuários e dispositivos com a afinidade de dispositivo de usuário](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  

 Existem vários métodos pelos quais você pode integrar a afinidade de dispositivo de usuário em suas implantações de SO. É possível integrar a afinidade de dispositivo de usuário em implantações por PXE, implantações por mídia inicializável e implantações por mídia em pré-teste.  


### <a name="create-a-task-sequence-that-includes-the-smstsassignusersmode-variable"></a>Criar uma sequência de tarefas que inclua a variável **SMSTSAssignUsersMode**

 Adicione a variável **SMSTSAssignUsersMode** ao início da sequência de tarefas usando a etapa [Definir Variável de Sequência de Tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable). Essa variável especifica como a sequência de tarefas trata as informações do usuário.

 Para saber mais, confira [Variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#SMSTSAssignUsersMode).


### <a name="create-a-prestart-command-that-gathers-the-user-information"></a>Criar um comando de pré-inicialização que reúna as informações do usuário

 O comando prestart pode ser um VBScript com uma caixa de entrada. Também pode ser um aplicativo HTML (HTA) que valida os dados que os usuários digitam. 

 O comando prestart deve definir a variável **SMSTSUDAUsers** usada quando a sequência de tarefas é executada. Essa variável pode ser definida em uma variável de computador, de coleção ou de sequência de tarefas.

 Para saber mais, confira [Variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#SMSTSUDAUsers).


### <a name="configure-how-distribution-points-and-media-associate-the-user-with-the-destination-computer"></a>Configurar como pontos de distribuição e mídia associam o usuário ao computador de destino

 O ponto de distribuição ou a mídia oferece suporte à associação de usuários ao computador de destino em que o sistema operacional é implantado. Use um dos métodos a seguir: 

 - [Configurar um ponto de distribuição para aceitar solicitações de inicialização PXE](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_PXEDistributionPoint)  
 - [Criar mídia inicializável](/sccm/osd/deploy-use/create-bootable-media)  
 - [Criar mídia pré-configurada](/sccm/osd/deploy-use/create-prestaged-media)  


 A configuração do suporte para afinidade de dispositivo de usuário não tem um método interno para validar a identidade do usuário. Esse comportamento é importante quando um técnico está provisionando o computador e insere as informações em nome do usuário. Além de definir como a sequência de tarefas lida com as informações do usuário, a configuração dessas opções no ponto de distribuição e na mídia possibilita restringir as implantações estabelecidas a partir de uma inicialização por PXE ou por um tipo específico de mídia.
