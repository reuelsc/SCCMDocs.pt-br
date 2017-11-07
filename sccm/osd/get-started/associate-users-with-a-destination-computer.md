---
title: "Associar usuários a um computador de destino"
titleSuffix: Configuration Manager
description: "Configure o System Center Configuration Manager para associar os usuários a computadores de destino ao implantar sistemas operacionais."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
caps.latest.revision: "9"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 4c0231057c2ac154b050cc7020eb1fbb4ed93228
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="associate-users-with-a-destination-computer-in-system-center-configuration-manager"></a>Associar usuários ao computador de destino no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Ao usar o System Center Configuration Manager para implantar o sistema operacional, é possível associar usuários ao computador de destino em que o sistema operacional é implantado. Essa configuração inclui o seguinte:  

-   Se um único usuário é o usuário principal do computador de destino.  

-   Se vários usuários são os usuários principais do computador de destino.  

 A afinidade de dispositivo de usuário oferece suporte ao gerenciamento centrado no usuário para a implantação de aplicativos. Ao associar um usuário ao computador de destino em que um sistema operacional será instalado, você pode implantar aplicativos para esse usuário posteriormente, e os aplicativos são instalados automaticamente no computador de destino. No entanto, embora seja possível configurar o suporte para a afinidade de dispositivo de usuário ao implantar sistemas operacionais, não é possível usar a afinidade de dispositivo de usuário para implantar sistemas operacionais.  

 Para obter mais informações sobre afinidade de dispositivo de usuário, consulte [Vincular usuários e dispositivos com a afinidade de dispositivo de usuário](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

## <a name="how-to-specify-a-user-when-you-deploy-operating-systems"></a>Como especificar um usuário ao implantar sistemas operacionais  
 A tabela a seguir lista as ações que podem ser executadas para integrar a afinidade de dispositivo de usuário em implantações de sistemas operacionais. É possível integrar a afinidade de dispositivo de usuário em implantações por PXE, implantações por mídia inicializável e implantações por mídia em pré-teste.  

|Ação|Mais informações|  
|------------|----------------------|  
|Criar uma sequência de tarefas que inclua a variável **SMSTSAssignUsersMode**|Adicione a variável **SMSTSAssignUsersMode** ao início da sequência de tarefas usando a etapa da sequência de tarefas  [Set Task Sequence Variable](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) . Essa variável especifica como a sequência de tarefas trata as informações do usuário.<br /><br /> Defina a variável para um dos seguintes valores:<br /><br /> <br /><br /> **Auto**: a sequência de tarefas cria automaticamente uma relação entre o usuário e o computador de destino e implanta o sistema operacional.<br /><br /> **Pendente**: a sequência de tarefas cria uma relação entre o usuário e o computador de destino, mas espera a aprovação do usuário administrativo antes de o sistema operacional ser implantado.<br /><br /> **Desabilitado**: a sequência de tarefas não associa um usuário ao computador de destino e continua a implantar o sistema operacional.<br /><br /> <br /><br /> Essa variável também pode ser definida em um computador ou uma coleção. Para obter mais informações sobre as variáveis internas, consulte [Variáveis internas de sequência de tarefas](../../osd/understand/task-sequence-built-in-variables.md).|  
|Criar um comando de pré-inicialização que reúna as informações do usuário|O comando de pré-inicialização pode ser um script do Visual Basic (VB) que tenha uma caixa de entrada ou pode ser um aplicativo HTML (HTA) que valide os dados do usuário que são inseridos.<br /><br /> O comando de pré-inicialização deve definir a variável **SMSTSUdaUsers** que é usada quando a sequência de tarefas é executada. Essa variável pode ser definida em uma variável de computador, de coleção ou de sequência de tarefas. Use o seguinte formato ao adicionar vários usuários: *domain\user1, domain\user2, domain\user3*.|  
|Configurar como pontos de distribuição e mídia associam o usuário ao computador de destino|Ao [configurar um ponto de distribuição para aceitar solicitações de inicialização por PXE](https://technet.microsoft.com/library/mt627944\(TechNet.10\).aspx#BKMK_PXEDistributionPoint) e ao criar uma [mídia inicializável](http://technet.microsoft.com/library/mt627921\(TechNet.10\).aspx) ou em [pré-teste](https://technet.microsoft.com/library/mt627922\(TechNet.10\).aspx) usando o Assistente para Criar Mídia de Sequência de Tarefas, é possível especificar como o ponto de distribuição ou a mídia dá suporte à associação de usuários ao computador de destino em que o sistema operacional é implantado.<br /><br /> A configuração do suporte para afinidade de dispositivo de usuário não tem um método interno para validar a identidade do usuário. Isso pode ser importante quando um técnico insere as informações em nome do usuário durante o provisionamento do computador. Além de definir como as informações de operador serão tratadas pela sequência de tarefas, configurar essas opções no ponto de distribuição e na mídia permite restringir as implantações iniciadas em uma inicialização por PXE ou por um tipo específico de mídia.|  
