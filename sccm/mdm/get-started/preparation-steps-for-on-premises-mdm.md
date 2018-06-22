---
title: 'Etapas de preparação '
titleSuffix: Configuration Manager
description: Prepare-se para gerenciar dispositivos com o Gerenciamento de Dispositivo Móvel local no System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1ef60106-8f31-46d6-95a6-25a6495f22c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 711af365353d68020a7bbbef8026f452d4203ce3
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346749"
---
# <a name="preparation-steps-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Etapas de preparação para o gerenciamento de dispositivo móvel local no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O gerenciamento de dispositivos com o Gerenciamento de Dispositivo Móvel Local do System Center Configuration Manager requer que a infraestrutura do Configuration Manager seja configurada para que as funções do sistema de sites necessárias (ponto proxy do registro, ponto de registro, ponto de gerenciamento de dispositivo e ponto de distribuição) possam se comunicar por um canal confiável com os dispositivos móveis a serem gerenciados.  

 As seguintes tarefas de alto nível são necessárias para preparar o sistema do Configuration Manager para o Gerenciamento de Dispositivo Móvel Local:  

-   [Configure uma assinatura do Microsoft Intune para o gerenciamento de dispositivo móvel local no System Center Configuration Manager](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md)  

     Nesta tarefa, inscreva-se no Microsoft Intune e adicione a assinatura para o Configuration Manager por meio do console do Configuration Manager. Essa etapa é necessária para fins de licenciamento. O Intune não é usado para gerenciar os dispositivos ou armazenar informações de gerenciamento. Toda coordenação e gerenciamento de dispositivos está com a iniciativa da sua organização usando a infraestrutura local do Configuration Manager.  

-   [Instalar funções do sistema de sites para o gerenciamento de dispositivo móvel local no System Center Configuration Manager](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     Nesta tarefa, você pode instalar e configurar as funções do sistema de sites necessárias para gerenciar dispositivos com a infraestrutura local do Configuration Manager. O Gerenciamento de Dispositivo Móvel Local requer, no mínimo, as funções ponto proxy do registro, ponto de registro, ponto de gerenciamento de dispositivos e sistema de sites do ponto de distribuição.  

-   [Configurar certificados para comunicações confiáveis do Gerenciamento de Dispositivo Móvel Local no System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)  

     Nesta tarefa, você configura a infraestrutura local do Configuration Manager para permitir comunicações confiáveis (HTTPS) entre os dispositivos gerenciados e os servidores que hospedam as funções do sistema local.  

-   [Configurar o registro de dispositivo para o gerenciamento de dispositivo móvel local no System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

     Nesta tarefa, você concede permissão aos usuários para registrar computadores e dispositivos e instalar o certificado raiz confiável nos dispositivos (normalmente aqueles que não ingressaram no domínio) para permitir conexões de HTTPS para servidores do sistema de site.  
